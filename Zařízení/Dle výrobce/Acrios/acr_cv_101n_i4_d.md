# Acrios

Ukázka kódu (Lua) pro vytvoření payload ve formatu CRA ([UDP](../../../Vstup%20do%20IoT%20platformy/UDP/CRa_protocol/version_1_0.md)) pro Acrios zařízení:

```lua

------- NB-IoT --------
protocol = "UDP"        -- UDP or TCP
APN = "iot.melita.io"
PLMNID = "23001"

ip = "84.244.71.169"
port = 5003

-- Marcker for begin/end of message
beginMsg = 0xAB
endMsg = 0xBA

-- Message structure description
protocol_version=0x40
message_type=0x10
payload_type=0x01

-- device ID previx
device_id_prefix=0xAC


function calculateXOR(data)
    local checksum = 0
    for i = 1, #data do
        checksum = bit.bxor(checksum, string.byte(data, i))
    end
    return checksum
end

function packDeviceID(deviceId)

    -- split into little-endian bytes
    local b1 =  bit.band(deviceId, 0xFF)  -- low byte
    local b2 =  bit.band(bit.rshift(deviceId,8), 0xFF)
    local b3 =  bit.band(bit.rshift(deviceId,16), 0xFF)  -- high byte

    -- pack four unsigned bytes: prefix + b1, b2, b3
    return pack.pack("<bbbb",device_id_prefix, b1, b2, b3)
end


function formatCRAMessage(deviceId, payload)
    if not deviceId then
        error("deviceId is required")
    end
    if not payload then
        error("payload is required")
    end

    local content = ""

    local messageStructure = bit.bor(payload_type, message_type, protocol_version)
    content = content .. pack.pack("<b", messageStructure)

    -- Device ID (4 bytes)
    content = content .. packDeviceID(deviceId)

    -- Payload length (2 bytes)
    content = content .. pack.pack("<H", #payload)

    -- Payload
    content = content .. payload

    -- Simple XOR checksum (1 byte) - basic error detection
    local checksum = calculateXOR(content)
    content = content .. pack.pack("<b", checksum)


    -- Add markers
    local message = pack.pack("<b", beginMsg) .. content .. pack.pack("<b", endMsg)

    return message
end

function processInputs()
    txbuf = ""

    -- get battery voltage
    v = api.getBatteryVoltage()
    txbuf = txbuf .. pack.pack("<H", v)

    directState = api.DIOreadPin(directInput)
    invertedState = api.DIOreadPin(invertedInput)

    retry = 0
    detectedError = 0
    while directState == invertedState do -- if equal, then we have error with the sensor
        print(
                "Detected bad sensor state, direct = " ..
                        tostring(directState) .. ", indirect = " .. tostring(invertedState)
        )
        retry = retry + 1
        if retry >= errorStateRetryCount then
            -- report an error!
            print("Detected error condition " .. tostring(retry) .. " times in row, report it!")
            detectedError = 1
            break
        end

        -- delay for next trial
        api.delayms(errorStateRetryPeriod)

        -- try read again
        directState = api.DIOreadPin(directInput)
        invertedState = api.DIOreadPin(invertedInput)
    end

    txbuf = txbuf .. pack.pack("<I2", directState, detectedError)

    local message = formatCRAMessage(17101, txbuf)

    api.dumpArray(message)
    res = api.nbSend(ip, port, message, receiveTimeout, protocol)

    if res == 0 then
        print("Done, sent to NB-IoT")
    else
        print("Error " .. tostring(res) .. ", failed to send to NB-IoT!")
    end

    print("Wake up in " .. tostring(periodicWakeup) .. " minutes")
    api.wakeUpIn(0, 0, periodicWakeup, 0)

end
```
