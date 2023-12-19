# MQTT příjem

CRA platforma podporuje dva druhy způsoby MQTT komunikace:
- [MQTT zařízení](#mqtt-zařízení)
- [MQTT gateway](/Výstup%20z%20IoT%20platformy/MQTT%20gateway)

## MQTT obecně
[MQTT](http://mqtt.org/) je protokol, který je optimální pro posílání malých zpráv. Je [velmi jednoduchý](https://en.wikipedia.org/wiki/MQTT) na implementaci a proto je vhodný pro IoT. Pro komunikaci je potřeba MQTT server (MQTT broker) do kterého klienti posílají (publish) zprávy a naopak je z něj také čtou (subscribe). Zprávy mohou mít prakticky libovolný obsah a jsou umístěny v takzvaných topicích (topic). Zpráva může být tedy bez formátu (raw) nebo třeba v JSON formátu. 

Tento protokol byl do CRA IoT platformy přidán proto, aby umožnil širší způsob konektivity z a na platformu a také proto, aby byl snadným můstkem k LoRa zařízením. Výhodou celého řešení je to, že LoRa i MQTT jsou vzájemně propojeny. 

K MQTT brokeru je potřeba mít přístupový účet (uživatelské jméno a heslo) a práva k topikům pro zmíněné operace publish a nebo subscribe.

Z pohledu CRA IoT platformy je možné si založit MQTT zařízení a MQTT gateway.

## MQTT zařízení
MQTT zařízení je vlastně vytvoření účtu a práv k dvěma topikům určených pro zařízení téhož jména. Jeden topic pro publish a druhý pro subscribe. Lze číst a zapisovat z/do vnořených subtopiců.

Do CRA IoT platformy lze posílat IoT zprávy také přes MQTT protokol. V tomto případě je potřeba založit MQTT zařízení.
To lze udělat jako přes GUI, tak přes REST API.

Pro MQTT zařízení je potřeba chápat následující parametry:
| Parametr | Popis | Detail/poznámka |
| --- | --- | --- |
| username	| Uživatelské jméno	| pro přihlášení k MQTT brokeru |
| password	| Heslo	| pro přihlášení k MQTT brokeru |
| topic up	| topik pro posílání zpráv	| do něj lze udělat publish |
| topic down	| topic pro příjem zpráv	| do něj lze udělat subscribe |
| customerId	| CRA: ID zákazníka 	| je potřeba pro plnou cestu k topiku |
| tenantId	| CRA: ID účtu	| je potřeba pro plnou cestu k topiku a založení zařízení |
| serviceId	| CRA: ID služby	| je potřeba určit, ke které služby bude patřit |
| label	| CRA: poznámka k zařízení/gateway	| pole pro popis |
| tech	| typ technologie	| v našem případě „MQTT“ |
| clientName	| identifikátor MQTT klienta	| v CRA platformě nehraje žádnou roli |
| clientId	| jméno zařízení v IoT platformě	| bez mezer, češtiny |
| gatewayId	| jméno Gateway v IoT platformě	| bez mezer, češtiny |
| qos	| kvalita doručování (QoS) používá klient spojení	| 0 - odešle min. jednou, 1 - odesílá, dokud nedostane potvrzení, 2 - doručení jednou |

MQTT zařízení lze vytvořit přes REST „POST ImportMQTT“:<br>
[https://api.iot.cra.cz/cxf/api/v1/mqtt/devices](https://api.iot.cra.cz/cxf/api/v1/mqtt/devices)<br>
kde header musí obsahovat, že kódování je v json a sessionId.

V body bude pak seznam těchto parametrů:
| Parametr	| Popis |
| ---	| --- |
| clientId	| Libovolné jméno vašeho zařízení |
| label	| Poznámka k zařízení |
| tech	| Hodnota: MQTT |
| username	| uživatelské jméno |
| password	| heslo |
| tenantId	| ID účtu - je k dispozici po přihlášení do GUI |
| serviceId	| V GUI /Služby |


Příklad:
```bash
curl --location --request POST 'https://api.iot.cra.cz/cxf/api/v1/mqtt/devices' \
--header 'Content-Type: application/json' \
--header 'sessionId: 11b00070-6716-11ea-bcc4-97141855c777' \
--data-raw '[
 {
  "clientId": "zasuvkaOkno",
  "label": "MQTT zasuvka okno",
  "tech": "MQTT",
  "username": "root",
  "password": "toor",
  "tenantId": "T202003241250003xdv",
  "serviceId": "OP-20-01704-00002s01"
 }
]'
```

Pokud chcete poslat zprávu do MQTT zařízení z IoT platformy (musí být připojeno přes MQTT protokol a poslouchat "příkazy" pomoci subscribe), pak můžete zprávu poslat buď:
- z GUI přes "Poslat zprávu" (v detailu MQTT zařízení) (NYI - zatím není v GUI)
- přes naše [REST API](https://app.swaggerhub.com/apis-docs/cra-iot/GUI/1.0.40#/MQTT%20Devices/post_mqtt_devices__id__down_messages)
- přes [MQTT gateway](/Výstup%20z%20IoT%20platformy/MQTT%20gateway)

### Připojení a komunikace
Klient pro CRA IoT platformu, resp. jeho MQTT broker použije následující parametry:
| Parametr	| Popis	| Detail/poznámka |
| ---	| ---	| --- |
| Name	| jméno klienta	| Jakýkoliv text, IoT platforma nepoužívá. |
| Validate certificate	| zapnuto/vypnuto	| Zda má klient ověřovat platnost certifikátu. Mělo by fungovat obojí. |
| Encryption	| tls zapnuto	| spojení je kryptované, máme port 8883 |
| protocol	| mqtt://	| ev. mqtts, pokud nemáte možnost přepnout Encryption |
| MQTT client ID	| $clientId	| Uveďte jméno zařízení, ke kterému patří username |
| host	| mqtt.iot.cra.cz	| URL, kde je umístěn CRA MQTT broker |
| port	| 8883	| Port, na kterém broker čeká na spojení |
| username	| Uživatelské jméno	| to, které jste uvedli při zakládání zařízení |
| password	| Heslo	| to, které jste uvedli při zakládání zařízení |
| topic up	| topik pro posílání zpráv	| do něj, a všech vnořených, lze udělat publish. Má tento tvar: $customerId/$tenantId/in/$clientId/* |
| topic down	| topic pro příjem zpráv	| do něj lze udělat subscribe. Má tvar (# čte ze všech vnořených): $customerId/$tenantId/out/$clientId/# |
| qos	| QoS	| tento parametr se uvádí až při odesílání zprávy |


Jelikož mají všichni MQTT uživatelé stejná práva, tak může i device číst nebo zapisovat do přiděleného topiku …/broker, který má chování jako samostatný Broker mimo CRA IoT platformu. 

Tam lze dělat jak publish, tak subscribe, do libovolného subtopiku. Tyto zprávy však nenajdete v CRA IoT platformě, jsou pouze v MQTT brokeru.

**Obousměrný MQTT broker**

Již vznikem zařízení je k dispozici také specifický topic a jeho subtopicy, které lze použít jako klasický MQTT broker, tj. pro obousměrnou komunikaci. Topic je v následující struktuře:
$customerId/$tenantId/broker

Je ale potřeba si uvědomit, že zprávy v rámci tohoto topicu nejdou přes CRA IoT platformu a jsou výhradně v MQTT brokeru.

### Smazání MQTT zařízení
MQTT zařízení lze smazat přes klasický REST „DELETE Device/{deviceId}”, kde deviceId je clientId.
