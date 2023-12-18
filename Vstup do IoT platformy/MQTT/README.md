# MQTT příjem

CRA platforma podporuje dva druhy způsoby MQTT komunikace:
- [MQTT zařízení](#mqtt-zařízení)
- [MQTT gateway](#mqtt-gateway)

## MQTT obecně
MQTT je protokol, který je optimální pro posílání malých zpráv. Je velmi jednoduchý na implementaci a proto je vhodný pro IoT. Pro komunikaci je potřeba MQTT server (MQTT broker) do kterého klienti posílají (publish) zprávy a naopak je z něj také čtou (subscribe). Zprávy mohou mít prakticky libovolný obsah a jsou umístěny v takzvaných topicích (topic). Zpráva může být tedy bez formátu (raw) nebo třeba v JSON formátu. 
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
| label	| CRA: poznámka k zařízení/endpointu	| pole pro popis |
| tech	| typ technologie	| v našem případě „MQTT“ |
| clientName	| identifikátor MQTT klienta	| v CRA platformě nehraje žádnou roli |
| clientId	| jméno zařízení v IoT platformě	| bez mezer, češtiny |
| endpointName	| jméno Endpointu v IoT platformě	| bez mezer, češtiny |
| qos	| kvalita doručování (QoS) používá klient spojení	| 0 - odešle min. jednou, 1 - odesílá, dokud nedostane potvrzení, 2 - doručení jednou |

## MQTT gateway
MQTT gateway má více funkcí. Lze do něj nasměrovat zprávy z platformy, včetně LoRa zpráv. Lze přes něj odesílat zprávy (říkáme Downlink zprávy) do všech typů zařízení (jak MQTT,tak i LoRaWAN). 
MQTT gatewat má dokonce i samostatnou část vyhrazenou pro shodnou funkčnost jako běžný broker. 

Přístup k MQTT gateway (potažmo brokeru) vzniká založením zařízení. 

Takto vzniklá identita má všechna potřebná práva a všechny identity pod jedním účtem mají identická práva.



Pokud chcete poslat zprávu do MQTT zařízení z IoT platformy (musí být připojeno přes MQTT protokol a poslouchat "příkazy" pomoci subscribe), pak můžete zprávu poslat buď z GUI přes "Poslat zprávu" (v detailu MQTT zařízení) (NYI - zatím není v GUI) nebo přes API (https://app.swaggerhub.com/apis-docs/cra-iot/GUI/1.0.40#/MQTT%20Devices/post_mqtt_devices__id__down_messages), případně přes MQTT gateway.

Jednou z možností je např. poslat downlink zprávu přes REST API, nebo uložit zprávu do MQTT topicu v MQTT gateway.
