# IoT zpráva a její struktura

Naše IoT platforma je inspirována robustním IoT řešením vyplývající z LoRaWAN standardu.

Díky tomu má i IoT zpráva vnitřní strukturu inspirovanou touto technologií.

Vlastní zpráva je v JSON formátu a má tyto atributy:
- [cmd (command type)](#cmd)
- [seqno (sequence number)](#seqno)
- [EUI (deviceId)](#eui)
- [ts (timestamp)](#ts)
- [fcnt (frame counter)](#fcnt)
- [port (port)](#port)
- [freq (in Hz)](#freq)
- [toa (in dBm)](#toa)
- [dr (in dB)](#dr)
- [ack (acknowledgement)](#ack)
- [gws (gateways)](#gws)
- [bat (battery level)](#bat)
- [data (payload)](#data)
- [encdata (encrypted payload)](#encdata)
- [tech (technology)](#tech)
- [_id (Identifier)](#id)

## Detailní informace k atributům
### cmd
  cmd = command type, identifies type of message, rx = uplink message, gw = gateway message

  Příklad: "cmd": gw,

  Jde o typ zprávy. Typy jsou:
  - rx - jde o LoRaWAN RX zprávu. Tj. LoRaWAN zpráva, kterou zachytila první IoT GW. Shodná zprávy z ostatních GW, které ji poslali pozdeji už není poslána jako RX, ale informace o ostatních IoT LoRaWAN GW se objeví v "gw" zprávě
  - gw - jde o LoRaWAN GW zprávu. Tj. deduplikována z více RX zpráv

### seqno
  seqno = global sequence number

  Příklad: "seqno": 1210628284,

  Globální sekvenční číslo. CRA specifické globální číslo LoRaWAN zprávy. 

### EUI 
  EUI = device EUI = device Extended Unique Identifier, 16 hex digits (without dashes)

  Příklad: "EUI": "0004A30B001968C8",

  Původně LoRa unikátní identifikátor, využíváno však plošně přes platformu.
Unikátní je vždy v rámci technologie (LoRa, MQTT, HTTP, UDP, atp.).

### ts 
  ts = server timestamp as number (milliseconds from Linux epoch)

  Příklad: "ts": 1685019178341,

  Čas přijetí v [UNIX timestamp](https://en.wikipedia.org/wiki/Unix_time) v časovém pásmu [GMT](https://cs.wikipedia.org/wiki/Greenwichsk%C3%BD_st%C5%99edn%C3%AD_%C4%8Das), i když je ČR v [CET](https://cs.wikipedia.org/wiki/UTC%2B02:00)

### fcnt
  fcnt = frame counter, a 32-bit number

  Příklad: "fcnt": 74021,

  Pořadové číslo uplink zprávy z pohledu zařízení.

### port
  port = port as sent by the end device

  Příklad: "port": 2,

### freq
  freq = frequence

  Příklad: "freq\":868100000

  Frekvence, na které byla zpráva vysílána

### toa
  toa = time on air

  Příklad: "toa": 1318,

  Čas, jak dlouho byla zpráva vysílána

### dr
  dr = radio data rate - spreading factor, bandwidth and coding rate

  Příklad: "dr":"SF12 BW125 4/5"

### ack
  Příklad: "ack" = false

  ack = acknowledgement flag as set by device

  Potvrzení o přijetí DL (downlink) zprávy. Nemusí být obsaženo ve zprávě.

### gws
  gws = list of gateways

  Příklad: "gws": [{"rssi": -102, "snr": 4.5, "ts": 1705681716051,....
  
  Detailněji:
  ```JSON 
  "gws": [
    {
      "rssi": -105,
      "snr": -13.2,
      "ts": 1705682132640,
      "tmms": 875979118909,
      "time": "2024-01-19T16:35:32.596439000Z",
      "gweui": "647FDAFFFF00808A",
      "ant": 0,
      "lat": 50.037834,
      "lon": 14.518459
    },
  ```

  Seznam IoT GW které přijali tuto zprávu. 
  
  Každý záznam obsahuje tyto atributy:
  * ["rssi"](#rssi) - rádio rssi
  * ["snr"](#snr) - rádio snr
  * "ts" - timestamp - interní čas z GW
  * "time" - GPS čas přijetí - dle ISO 8601 s přesností na nanosecondy
  * "tmms" - UTC čas přijetí - v UNIX čase -  dostupné jen u gateway s GPS
  * "gweui" - id IoT GW
  * "lat" a "lon" - součadnice IoT GW

### rssi
  rssi = frame rssi, in dBm, as integer number

  Příklad: "rssi": -110,

  Při RX zprávě je v hlavní struktuře JSONu, v GW zprávě je u gateway, která ji přijala v gws části JSONu

### snr
  snr = frame snr, in dB, one decimal place

  Příklad: "snr": -10.2,
  
  Při RX zprávě je v hlavní struktuře JSONu, v GW zprávě je u gateway, která ji přijala v gws části JSONu

### tech
 (technology)](#tech)

### bat
  bat = device battery status, response to the DevStatusReq LoRaWAN MAC Command

  Příklad: "bat": 255,

  Stav baterie v decimální hodnota 0-255 stavu baterie, odpovídající 0-100%

Detailně pak takto:
1-254=odpovídá stavu baterie 0-100%
0= je tedy externí napájení
255=stav baterie není přenášen

Ve filtru v GUI se požávájí následující filtry:
| DEC  | Hodnota ve filtru |
|------|-------------------|
|>152  | 100%-60%          |
|<=152 | méně než 60%      |
|<=102 | méně než 40%      |
|<=52  | méně než 20%      |
|=255  | N/A ~ nezjištěno  |
|=0    |externí napájení   |

### data
  data - decrypted data payload as hexadecimal string, only present if APPSKEY is assigned to device

  Příklad: "data": "0108870e8b01b3",

### encdata
  encdata = encrypted data payload as hexadecimal string, only present if APPSKEY is not assigned to device

  Příklad: "encdata": null,

### id
  _id - message identifier

  Příklad: "_id": "65aa7fdb244659031da4154c"
  
  Unikátní identifikátor zprávy

### tech
  tech - technology

  Příklad: "tech": "mqtt",

  Identifikátor technologie, kterou byla zpráva přijata. Nejde o povinný parametr. U LoRaWAN chybí.
