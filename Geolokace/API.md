![image](https://github.com/cra-iot/documentation/assets/118526137/861bf3fa-520f-43e7-966a-0e591e5126bb)# API Geolokace

Geolokační zprávy lze vyčítat přes API, podobně jako jiné LoRAWAN zprávy.

Aktuálně jsou dostupné na URL:
GET https://node-red.iot.cra.cz/devices/lora/{id}/geo/messages

URI parametry:
id * - string - DevEUI Zařízení

Path parametry:<br>
from * - string - datum a čas od (yyyy-MM-dd'T'HH:mm:ss.SSSXXX) - příklad: 2022-11-23T00:00:00.000Z<br>
to * - string - datum a čas do (yyyy-MM-dd'T'HH:mm:ss.SSSXXX) - příklad: 2022-11-26T23:59:59.000Z<br>
limit - integer($int32) - minimum: 1 - maximum: 1000 - query row limit, např. 20 - default value : 10

Response:
```json
{
    "status": "success",
    "metadata": {
        "count": 16,
        "result": 1
    },
    "data": [
        {
            "id": "db4155e2668633849231",
            "messageTime": "2022-11-23T21:24:08.979Z",
            "message": {
                "cmd": "geo",
                "EUI": "0004A30B001968C8",
                "ts": "2022-11-23T21:24:08.979Z",
                "lat": 50.079835725503685,
                "lon": 14.375803342484645,
                "alt": 406,
                "accuracy": null,
                "method": "TDOA",
                "gws": 3,
                "seqno": 811021424,
                "fcnt": 32850
            }
        }
    ],
    "links": {
        "self": "/cxf/api/v1/lora/devices/0004A30B001968C8/geo/messages/"
    }
}
```

Struktura geo zprávy je následující:
* `"EUI":"A81758FFFE04505A"`		Id LoRa zařízení (pozor velkými - "upper case")
* `"ts":1638178757178`  			čas související LoRa zprávy
* `"lat":50.10953803374609`		Zeměpisná šířka
* `"lon":14.470567400491364`		Zeměpisná délka
* `"alt":311.3333333333333`		Nadmořská výška
* `"accuracy":null`			Očekávaná přesnost
* `"method":"TDOA"`			Metoda výpočtu geo zprávy
* `"gws":7`				Počet GW využitých pro výpočet
* `"seqno":811021424`			Globální pořadové číslo
* `"fcnt":79404`				LoRa pořadové číslo
