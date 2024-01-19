# IoT zpráva a její struktura

Naše IoT platforma je inspirována robustním IoT řešením vyplývající z LoRaWAN standardu.
Díky tomu má i IoT zpráva vnitřní strukturu inspirovanou touto technologií.
Vlastní zpráva je v JSON formátu a má tyto atributy:
- ts (timestamp)
- tech (technology)
- EUI (deviceId)
- data (payload)
- encdata (encrypted payload)
- seqno (sequence number)
- bat (battery level)

## Detailní informace k atributům
### ts (timestamp)
  "ts": 1685019178341,
### EUI 
Původně LoRa unikátní identifikátor, využíváno však plošně přes platformu.
Unikátní je vždy v rámci technologie (LoRa, MQTT, HTTP, UDP, atp.).

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
