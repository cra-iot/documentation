# Výrobce Netlia

Hlavní seznam výrobků najdete na jejich webových stránkách: https://netlia.com/cs/senzory-netlia/

Konfigurace, včetně identifikace zařízení je popsána na této stránce:
https://github.com/Netlia/documentation/blob/main/DeviceComunication/DeviceComunication_CZ.md

Pokud používáte tato čidla s připojením NB IoT, pak je potřeba převést příchozí zprávu, pokud chcete, aby jí CRA IoT cloud rozumněl (zobrazoval stav baterie, payload, uměl parsovat data na fyzické veličiny, atp.)

Při využití O2 SIM s CRA APN lze čidla nasměrovat na námi vystavený UDP port. Díky tomu začnou IoT zprávy přicházet v JSON struktuře:
```json
{
  "payload": "023002953000054718005f40630000050303000000",
  "imsi":"230029530000547"
}
```
ale to je stále pro CRA IoT cloud nesrozumitelné.

Je potřeba definovat transformaci pro Netlia čidlo.

Zde je příklad transformace (zatím není implementováno převádění stavu baterie na DEC hodnotu jako je uvedena u LoRa zařízení)
```JavaScript
function parceNetlia(msg) { 
  o = {}; 
  m = JSON.parse(msg); 
  o.imsi = m.payload.slice(1, 16); 
  o.header = m.payload.slice(16,32); 
  o.seqno = (parseInt(m.payload.slice(16, 18), 16)).toString(); 
  o.bat_V = (((parseInt(m.payload.slice(20, 22), 16)) / 100) + 1.8).toFixed(2); 
  o.data = m.payload.slice(32); 
  return JSON.stringify(o); 
}   
```

Do API je potřeba vložit jako jednořádkový string
```JavaScript
function parceNetlia(msg) { o = {}; m = JSON.parse(msg); o.imsi = m.payload.slice(1, 16); o.header = m.payload.slice(16,32); o.seqno = (parseInt(m.payload.slice(16, 18), 16)).toString(); o.bat_V = (((parseInt(m.payload.slice(20, 22), 16)) / 100) + 1.8).toFixed(2); o.data = m.payload.slice(32); return JSON.stringify(o); }   
```

tj. API request bude vypadat např. takto:
```
curl --location --request PUT 'https://api.iot.cra.cz/cxf/api/v1/projects/T202108231049932zrp/transformations/60' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhb....6d26' \
--data '{
  "type": "DEV",
  "subType": "MQTT",
  "label": "Netlia NB IoT v01",
  "definition": "function parceNetlia(msg) { o = {}; m = JSON.parse(msg); o.imsi = m.payload.slice(1, 16); o.header = m.payload.slice(16,32); o.seqno = (parseInt(m.payload.slice(16, 18), 16)).toString(); o.bat_V = (((parseInt(m.payload.slice(20, 22), 16)) / 100) + 1.8).toFixed(2); o.data = m.payload.slice(32); return JSON.stringify(o); }"
}'
```

Napětí převádíme cca tímto převodem:

|V|%|DEC|
|-|-|-|
|2,5|20|51|
|2,51|22|57|
|2,52|23|59|
|2,53|25|63|
|2,54|26|67|
|2,55|28|71|
|2,56|30|77|
|2,57|31|79|
|2,58|33|83|
|2,59|34|87|
|2,6|36|91|
|2,61|38|97|
|2,62|39|99|
|2,63|41|105|
|2,64|42|107|
|2,65|44|111|
|2,66|46|117|
|2,67|47|119|
|2,68|49|125|
|2,69|50|127|
|2,7|52|131|
|2,71|54|137|
|2,72|55|139|
|2,73|57|145|
|2,74|58|147|
|2,75|60|151|
|2,76|62|157|
|2,77|63|159|
|2,78|65|165|
|2,79|66|167|
|2,8|68|173|
|2,81|70|177|
|2,82|71|179|
|2,83|73|185|
|2,84|74|187|
|2,85|76|193|
|2,86|78|197|
|2,87|79|199|
|2,88|81|205|
|2,89|82|207|
|2,9|84|213|
|2,91|86|217|
|2,92|87|219|
|2,93|89|225|
|2,94|90|227|
|2,95|92|233|
|2,96|94|237|
|2,97|95|241|
|2,98|97|245|
|2,99|98|247|
|3|100|253|
|>3|100|254|


