# MQTT gateway

MQTT gateway má více funkcí. Lze do ní nasměrovat zprávy z platformy, včetně LoRa zpráv. Lze přes ni dokonce odesílat zprávy (říkáme Downlink zprávy) do všech typů zařízení (jak MQTT,tak i LoRaWAN).

MQTT gateway má dokonce i samostatnou část vyhrazenou pro shodnou funkčnost jako běžný broker.

Přístup k MQTT gateway (potažmo brokeru) vzniká založením zařízení - ano, pro možnost využití MQTT gateway je potřeba [založit zařízení](../../Vstup%20do%20IoT%20platformy/MQTT/README.md).
Takto vzniklá identita má všechna potřebná práva (všechny identity pod jedním účtem mají identická práva).

Vytvořením MQTT gateway v IoT platformě nevzniká další identita k přihlášení do MQTT brokeru. Můžete použít jakoukoliv existující. Pokud žádnou nemáte, je potřeba založit jedno zařízení, jen pro tento účel. Jak již bylo řečeno, MQTT gateway má více funkcí. Nyní si je popíšeme detailně.

## Vytvoření MQTT gateway

MQTT gateway lze vytvořit přes REST:

```
POST https://api.iot.cra.cz/cxf/api/v1/mqtt/gateways
```

kde header musí obsahovat, že kódování je v json, a přístupový token (viz [API](../../API/README.md)).

V body bude pak seznam těchto parametrů:

| Parametr            | Povinný | Popis                                                                                                          |
|---------------------|---------|----------------------------------------------------------------------------------------------------------------|
| projectId           | ano     | ID účtu - je k dispozici po přihlášení do GUI                                                                  |
| custDestName        | ano     | Název MQTT gateway, max. 60 znaků                                                                              |
| custDestParameters  | ano     | Objekt `{ "address": "..." }`, kde `address` je adresa topicu ve tvaru `$customerId.$tenantId.gate.$gatewayId` |
| custDestEnabled     | ano     | Zda má být aktivní - true/false                                                                                |
| custDestDescription | ne      | Poznámka k MQTT gateway, max. 60 znaků                                                                         |
| transformationId    | ne      | ID transformační funkce                                                                                        |

Id MQTT gateway, tedy gatewayId, je definováno v custDestParameters

`transformationId` je ID [transformace](../../Funkcionality%20platformy/Transformace/README.md), která se spustí nad zprávou těsně před doručením do této gateway.

Příklad:

```bash
curl --location --request POST 'https://api.iot.cra.cz/cxf/api/v1/mqtt/gateways' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhb....6d26' \
--data-raw '{
  "projectId": "T202003241250003xdv",
  "custDestName": "Muj MQTT vystup",
  "custDestParameters": {
    "address": "10147695.T202003241250003xdv.gate.myMqttApp"
  },
  "custDestEnabled": true
}'
```

## Příjem zpráv ze zařízení

Po založení MQTT gateway lze udělat nasměrování zpráv stejně, jako u HTTP Endpointu. Tj. mít skupinu (nově již "Datový tok"), přiřadit k ní zařízení a skupinu přiřadit k MQTT gateway. Tím, budou zprávy zmíněného zařízení k dispozici ke čtení v MQTT gateway v topicu (použít metodu subscribe):

* `$address/devices/$tech/$clientId/up/#`

(kde v $address obsahuje tečky za lomítka)

Kde $tech je buď mqtt nebo lora, podle typu zařízení.

$clientId je ID zařízení, tj. u LoRa DevEUI.

Pokud chcete číst zprávy ze všech nasměrovaných MQTT zařízení, pak topic:

* `$address/devices/mqtt/*/up/#`

(případně `$address/devices/mqtt/+/up/#`)

Zprávy od LoRa zařízení jsou v root topicu a mají formát JSON, jako při stažení přes REST.

To znamená topic:

* `$address/devices/lora/*/up`

(tj. nepoužívejte /# na konci)

Případně zkuste „+“ místo „*“. Někteří MQTT klienti to tak potřebují.

## Odesílání zpráv do zařízení

MQTT gateway lze využít také pro odesílání zpráv do zařízení. Těmto zprávám říkáme Downlink zprávy, dle principu LoRa.

Topic pro odesílání je tento:

* `$address/devices/$tech/$clientId/down/#`

Pro LoRa to bude tedy např.:

* `$address/devices/lora/48FFFFFFA11B0069/down`

a pro LoRa musí být obsah JSON ve stejném formátu jako pro REST, tj.:

```json
{ "cmd": "tx", "port":10, "data":"00","seqno":12, "confirmed":true, "EUI":"48FFFFFFA11B0069"}
```

Pro MQTT je možné poslat zprávy standardním způsobem pro MQTT komunikaci, tj. včetně subtopiců. Formát zpráv není nijak omezen. Topic pro odeslání zpráv do připojeného MQTT zařízení vypadá tedy takto (kde „rele“ je subtopic, do kterého chceme zapsat):

* `$address/devices/mqtt/zasuvkaOkno/down/rele`

## Smazání MQTT gateway

MQTT gateway lze smazat přes klasický REST „DELETE `$URI/mqtt/gateways/{gatewayId}`”.
