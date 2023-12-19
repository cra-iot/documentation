## MQTT gateway
MQTT gateway má více funkcí. Lze do ní nasměrovat zprávy z platformy, včetně LoRa zpráv. Lze přes ni dokonce odesílat zprávy (říkáme Downlink zprávy) do všech typů zařízení (jak MQTT,tak i LoRaWAN). 

MQTT gateway má dokonce i samostatnou část vyhrazenou pro shodnou funkčnost jako běžný broker. 

Přístup k MQTT gateway (potažmo brokeru) vzniká založením zařízení - ano, pro možnost využití MQTT gateway je potřeba [založit zařízení](/Vstup%20do%20IoT%20platformy/MQTT/README.md). 
Takto vzniklá identita má všechna potřebná práva (všechny identity pod jedním účtem mají identická práva).

Vytvořením MQTT gateway v IoT platformě nevzniká další identita k přihlášení do MQTT brokeru. Můžete použít jakoukoliv existující. Pokud žádnou nemáte, je potřeba založit jedno zařízení, jen pro tento účel. Jak již bylo řečeno, MQTT gateway má více funkcí. Nyní si je popíšeme detailně.

### Vytvoření MQTT gateway
MQTT gateway lze vytvořit přes REST:<br>
POST https://api.iot.cra.cz/cxf/api/v1/mqtt/gateways<br>
kde header musí obsahovat, že kódování je v json a sessionId.

V body bude pak seznam těchto parametrů:
| Parametr	| Popis |
| ---	| --- |
| projectId	| ID účtu - je k dispozici po přihlášení do GUI |
| custDestName	|  Název MQTT gateway |
| custDestDescription	| Poznámka pro MQTT gateway |
| custDestParameters	| Jméno topicu ve formátu: $customerId/$tenantId/gate/<gatewayId> |
| custDestEnabled	| zda má být aktivní - true/false |
| transformationId	| Poznámka k MQTT gateway |

Id MQTT gateway, tedy gatewayId, je definováno v custDestParameters

Příklad:
```bash
curl --location --request POST 'https://api.iot.cra.cz/cxf/api/v1/mqtt/gateways' \
--header 'Content-Type: application/json' \
--header 'sessionId: 11b00070-....-97141855c777' \
--data-raw '{
  "tenantId": "T202003241250003xdv",
  "label": "Muj MQTT vystup",
  "protocol": "MQTT",
  "address": "10147695.T201903051359003xdv.gate.myMqttApp"
}'
```

### Příjem zpráv ze zařízení
Po založení MQTT gateway lze udělat nasměrování zpráv stejně, jako u HTTP Endpointu. Tj. mít skupinu (nově již "Datový tok"), přiřadit k ní zařízení a skupinu přiřadit k MQTT gateway. Tím, budou zprávy zmíněného zařízené k dispozici ke čtení v MQTT gateway v topicu (použít metodu subcribe): <br>
* $address/devices/$tech/$clientId/up/# <br>
(kde v $address obsahuje tečky za lomítka)

Kde $tech je buď mqtt nebo lora, podle typu zařízení.<br>
$clientId je ID zařízení, tj. u LoRa DevEUI.

Pokud chcete číst zprávy ze všech nasměrovaných MQTT zařízení, pak topic:<br>
$address/devices/mqtt/*/up/#<br> 
(případně $address/devices/mqtt/+/up/#)

Zprávy od LoRa zařízení jsou v root topicu a mají formát JSON, jako při stažení přes REST.

To znamená topic:<br>$address/devices/lora/*/up<br>
(tj. nepoužívejte /# na konci)

Případně zkuste „+“ namíst „*“. Někteří MQTT klienti to tak potřebují.

**Odesílání zpráv do zařízení**<br>
MQTT gateway lze využít také pro odesílání zpráv do zařízení. Těmto zprávám říkáme Downlink zprávy, dle principu LoRa.

Topic pro odesílání je tento:<br>
$address/devices/$tech/$clientId/down/#<br>

Pro LoRa to bude tedy např.:<br>
$address/devices/lora/48FFFFFFA11B0069/down<br>
a pro LoRa musí být obsah JSON ve stejném formátu jako pro REST, tj.:
```json 
{ "cmd": "tx", "port":10, "data":"00","seqno":12, "confirmed":true, "EUI":"48FFFFFFA11B0069"}
```

Pro MQTT je možné poslat zprávy standardním způsobem pro MQTT komunikaci, tj. včetně subtopiců. Formát zpráv není nijak omezen. Topic pro odeslání zpráv do připojeného MQTT zařízení vypadá tedy takto (kde „rele“ je subtopic, do kterého chceme zapsat):<br>
$address/devices/mqtt/zasuvkaOkno/down/rele.

### Smazání MQTT gateway
MQTT gateway lze smazat přes klasický REST „DELETE \$URI/mqtt/gateways/{gatewayId}”.
