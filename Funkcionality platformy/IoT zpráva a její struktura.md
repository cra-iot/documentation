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
  "seqno": 977937300,
  "bat": 255,
  "data": "0108870e8b01b3",
  "encdata": null,
  "EUI": "000DB53112743570"

Standardní LoRa atributy
