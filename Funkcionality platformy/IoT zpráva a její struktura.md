# IoT zpráva a její struktura

Naše IoT platforma je inspirována robustním IoT řešením vyplývající z LoRaWAN standardu.

Díky tomu má i IoT zpráva vnitřní strukturu inspirovanou touto technologií.

Vlastní zpráva je v JSON formátu a má tyto atributy:
- [cmd (command type)](#cmd)
- [seqno (sequence number)](#seqno)
- [EUI (deviceId)](#EUI)
- [ts (timestamp)](#ts)
- [tech (technology)](#tech)
- [data (payload)](#data)
- [encdata (encrypted payload)](#encdata)
- [bat (battery level)](#bat)

## Detailní informace k atributům
### cmd (timestamp)
  Příklad: "cmd": gw,

  Jde o typ zprávy. Typy jsou:
  - rx - jde o LoRaWAN RX zprávu. Tj. LoRaWAN zpráva, kterou zachytila první IoT GW. Shodná zprávy z ostatních GW, které ji poslali pozdeji už není poslána jako RX, ale informace o ostatních IoT LoRaWAN GW se objeví v "gw" zprávě
  - gw - jde o LoRaWAN GW zprávu. Tj. deduplikována z více RX zpráv

### seqno (global seqno)
  Příklad: "seqno": 1210628284,
  Globální sekvenční číslo. CRA specifické globální číslo LoRaWAN zprávy. 

### EUI 
Příklad: "EUI": "0004A30B001968C8",

Původně LoRa unikátní identifikátor, využíváno však plošně přes platformu.
Unikátní je vždy v rámci technologie (LoRa, MQTT, HTTP, UDP, atp.).

### ts (timestamp)
  Příklad: "ts": 1685019178341,

### fcnt (frame contract number)
  "fcnt": 74021,

### bat
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


## dopopsat
  "seqno": 977937300,
  "bat": 255,
  "data": "0108870e8b01b3",
  "encdata": null,
  "EUI": "000DB53112743570"

Standardní LoRa atributy
