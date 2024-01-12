# Doručování zpráv na HTTP "Endpoint"

Jde o metodu známou jako Webhook. V naší IoT platformě ji nazýváme už historicky "Výstypy/HTTP endpoint"

Takový endpoint si můžete vyrobit jakýmikoliv programovacími prostředky, případně již použít existující na nějakém hotovém softwaru.

Naše platforma odesílá zprávy z IP adresy: 82.99.180.180. Tato IP adresa se 16.1.2024 změní na 84.244.71.160, protože přejdeme na modernější verzi, která je umístěna v jiné síťové zóně. 

Odchozí zpráva je zapouzdřena do integrační obálky. Vše je předáváno v těle HTTP požadavku jako JSON řetězec.

|Atribut | Datový typ | Popis |
|-|-|-|
|type | STRING | Identifikuje typ integračního rámci. Pro příchozí zprávy platí hodnota „D“. |
|data | STRING | Datová zpráva |
|tech | STRING | Technologie použitá pro přenos dat. Pro LoRa bude rovna „L“ |
|tags | STRING | Tagy zařízení, ze kterého zpráva přišla |

Příklad zprávy je:


```json
{
    "type":"D",
    "data":"{\"cmd\":\"gw\",\"seqno\":1203319294,\"EUI\":\"000DB53112743570\",\"ts\":1705048875592,\"fcnt\":787465,\"port\":2,\"freq\":867900000,\"toa\":102,\"dr\":\"SF8 BW125 4/5\",\"ack\":false,\"gws\":[{\"rssi\":-108,\"snr\":4.2,\"ts\":1705048875601,\"tmms\":0,\"time\":\"2024-01-12T08:41:15.582031000Z\",\"gweui\":\"647FDAFFFF0069F5\",\"ant\":0,\"lat\":50.054771,\"lon\":14.439468},{\"rssi\":-110,\"snr\":-7,\"ts\":1705048875601,\"tmms\":0,\"time\":\"2024-01-12T08:41:15.582038000Z\",\"gweui\":\"647FDAFFFF0069CE\",\"ant\":0,\"lat\":50.071449,\"lon\":14.430869},{\"rssi\":-113,\"snr\":-8.2,\"ts\":1705048875592,\"tmms\":0,\"time\":\"2024-01-12T08:41:15.582040000Z\",\"gweui\":\"647FDAFFFF00956C\",\"ant\":0,\"lat\":50.067696,\"lon\":14.468881},{\"rssi\":-114,\"snr\":-0.2,\"ts\":1705048875597,\"tmms\":0,\"time\":\"2024-01-04T22:55:25.454932000Z\",\"gweui\":\"647FDAFFFF009541\",\"ant\":0,\"lat\":50.052292,\"lon\":14.472598}],\"bat\":255,\"data\":\"010af0061e01c8\",\"_id\":\"65a0fb2bed4643031c768ce8\"}",
    "tech":"L",
    "tags":["geolocation"]
}
```
zpráva není zalamována, jako v příkladu
