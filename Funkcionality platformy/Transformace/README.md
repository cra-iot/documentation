# Transformace

Transformace je skript, který platforma spustí nad tělem zprávy v okamžiku, kdy
zpráva prochází platformou. Návratová hodnota skriptu se stává novým tělem
zprávy — tedy tím, co se uloží a co se doručí na výstup.

Typicky se transformace používá pro:

- dekódování binárního payloadu na fyzické veličiny,
- doplnění, přejmenování nebo odstranění atributů zprávy,
- převod zprávy z nestandardního zařízení do struktury, které platforma rozumí
  (viz příklad [Netlia](../../Zařízení/Dle%20výrobce/Netlia/README.md)).

## Kdy se transformace spustí

Transformace se k objektům přiřazuje přes `transformationId`. Atribut `type`
určuje, ve kterém místě průchodu zprávy platformou skript běží:

| `type`     | Název v portálu              | Přiřazuje se k                | Kdy běží                                 |
|------------|------------------------------|-------------------------------|------------------------------------------|
| `IN`       | Vstupní transformace         | zařízení                      | nad zprávou ze zařízení, hned po příjmu  |
| `PAYLOAD`  | Dekódování zprávy            | zařízení z HW katalogu        | po vstupní transformaci                  |
| `DATAFLOW` | Transformace na datovém toku | datový tok (skupina zařízení) | po dekódování zprávy                     |
| `OUT`      | Výstupní transformace        | výstup z platformy            | těsně před doručením na konkrétní výstup |

Pokud je nastaveno více transformací najednou, spouštějí se v pořadí uvedeném
v tabulce a každá dostane na vstup výsledek té předchozí.

Starší funkce mohou mít ještě původní hodnoty `DEV` (odpovídá `IN`) a `MSG`
(odpovídá `DATAFLOW`). Platforma obě hodnoty stále zpracovává.

Atribut `subType` (`LORA`, `MQTT`, `HTTP`, `UDP`) říká, pro kterou technologii
je funkce napsaná. Slouží především pro filtrování nabídky v portálu — platforma
při přiřazení nekontroluje, že `type` a `subType` odpovídají místu, kam funkci
přiřazujete.

## Vstupní zpráva

Proměnná `message` je vždy **řetězec** a obsahuje tělo zprávy v té podobě,
v jaké do dané transformace vstupuje. První transformace v pořadí dostane
zprávu tak, jak přišla ze vstupního rozhraní, každá další pak dostane výstup
té předchozí.

Podoba zprávy na vstupu se liší podle technologie, kterou zpráva do platformy
přišla:

### LoRaWAN

Na vstupu je [IoT zpráva](../IoT%20zpráva%20a%20její%20struktura.md) v JSON.
Naměřená data jsou v atributu `data` jako hexadecimální řetězec:

```json
{
  "cmd": "gw",
  "seqno": 1203319294,
  "EUI": "000DB53112743570",
  "ts": 1705048875592,
  "fcnt": 787465,
  "port": 2,
  "freq": 867900000,
  "toa": 102,
  "dr": "SF8 BW125 4/5",
  "ack": false,
  "gws": [{ "rssi": -108, "snr": 4.2, "gweui": "647FDAFFFF0069F5" }],
  "bat": 255,
  "data": "010af0061e01c8",
  "_id": "65a0fb2bed4643031c768ce8"
}
```

Transformace, která z payloadu počítá fyzické veličiny, tedy pracuje
s `m.data`:

```javascript
function (message) {
  var m = JSON.parse(message);
  var teplota = parseInt(m.data.slice(2, 6), 16) / 10;
  return JSON.stringify({ EUI: m.EUI, ts: m.ts, teplota: teplota });
}
```

### MQTT

Zprávu z MQTT zařízení platforma zabalí do obálky s informacemi o topicu:

```json
{
  "qos": 1,
  "topic_full": "10147695.T202003241250003xdv.devices.mqtt.zasuvkaOkno.up",
  "topic": "up",
  "data": { "teplota": 21.5 },
  "base64": false
}
```

| Atribut      | Obsah                                                         |
|--------------|---------------------------------------------------------------|
| `qos`        | QoS, se kterým zařízení zprávu publikovalo                    |
| `topic_full` | celý topic včetně adresy účtu                                 |
| `topic`      | koncová část topicu (subtopic), do které zařízení publikovalo |
| `data`       | vlastní payload zařízení                                      |
| `base64`     | příznak, že obsah `data` je zakódovaný v Base64               |

Je-li payload platný JSON, vloží se do `data` tak, jak je — `data` je pak
objekt nebo pole, nikoli řetězec. V ostatních případech je `data` řetězec.
Payload, který není platný text nebo obsahuje řídicí znaky, platforma zakóduje
do Base64 a nastaví `base64` na `true`; příznak se nastaví i tehdy, když
payload pouze odpovídá tvaru Base64.

### UDP

Na vstupu je to, co zařízení odeslalo, ve formátu daného
[UDP portu](../../Vstup%20do%20IoT%20platformy/UDP/README.md). Například čidlo
Netlia posílá:

```json
{
  "payload": "023002953000054718005f40630000050303000000",
  "imsi": "230029530000547"
}
```

### Výstupní transformace a integrační obálka

Zprávy doručované na [HTTP endpoint](../../Výstup%20z%20IoT%20platformy/HTTP/README.md)
platforma běžně zabaluje do integrační obálky
(`{"type": "D", "data": ..., "tech": ..., "tags": [...]}`).

Pokud je ale na výstupu nastavená výstupní transformace (`OUT`), obálka se
**nepoužije**. Transformace dostane na vstup samotnou zprávu bez obálky a na
endpoint se doručí přesně to, co transformace vrátí. Pokud obálku potřebujete,
musí si ji taková transformace sestavit sama.

## Podporované jazyky

| `definitionType` | Jazyk      | Běhové prostředí   |
|------------------|------------|--------------------|
| `JAVASCRIPT`     | JavaScript | GraalVM JavaScript |
| `GROOVY`         | Groovy     | Apache Groovy 4    |

Jiné jazyky platforma nepodporuje.

Skript má v obou jazycích k dispozici tyto vstupy:

| Proměnná     | Obsah                         |
|--------------|-------------------------------|
| `message`    | tělo zprávy jako řetězec      |
| `tags`       | tagy zařízení                 |
| `attributes` | uživatelské atributy zařízení |

Způsob, jakým jsou `tags` a `attributes` předány, se ale mezi jazyky liší — viz
následující kapitoly.

### JavaScript

Definice musí být **funkční výraz**, tedy `function (message) { ... }`, případně
pojmenovaná funkce. Platforma ji volá takto:

```javascript
fce(message, null, tags, attributes)
```

Novým tělem zprávy se stane hodnota vrácená příkazem `return`.

`tags` i `attributes` dostane JavaScript jako řetězec, nikoli jako pole nebo
objekt — nelze nad nimi tedy volat `tags.length` ani `attributes.teplota`.
`attributes` má tvar `klíč: hodnota, klíč: hodnota`. `tags` má tvar
`"prvni", "druhy"` — názvy tagů jsou oddělené čárkou a **každý je navíc
v uvozovkách**. Pokud s tagy ve skriptu pracujete, uvozovky odstraňte.

```javascript
function (message) {
  var m = JSON.parse(message);
  return JSON.stringify({ teplota: parseInt(m.data.slice(0, 4), 16) / 10 });
}
```

### Groovy

Definice je běžný skript. Novým tělem zprávy se stane hodnota posledního
vyhodnoceného výrazu, případně hodnota vrácená příkazem `return`.

Na rozdíl od JavaScriptu je `tags` typu `List` a `attributes` typu `Map`.

Pozor na obsah `tags`: seznam vzniká rozdělením řetězce `"prvni", "druhy"` podle
čárky, takže jednotlivé prvky obsahují uvozovky a od druhého prvku i úvodní
mezeru. Před porovnáním je proto potřeba prvek oříznout (`trim()`) a zbavit
uvozovek.

```groovy
import groovy.json.JsonOutput
import groovy.json.JsonSlurper

def m = new JsonSlurper().parseText(message)
def teplota = Integer.parseInt(m.data.substring(0, 4), 16) / 10

return JsonOutput.toJson([teplota: teplota])
```

Vracejte vždy řetězec. Pokud skript vrátí například `Map`, platforma jej převede
na řetězec vlastním způsobem a výsledek nemusí být platný JSON — proto
`JsonOutput.toJson(...)`.

### Chyby při vykonávání

Pokud skript skončí chybou — nepřeloží se nebo spadne za běhu — platforma zprávu
nezahodí. Místo transformovaného těla dosadí text začínající
`ScriptEvaluationException cause:` a zprávu s tímto obsahem doručí dál. Pokud
tento řetězec uvidíte na svém výstupu, je chyba ve skriptu transformace.

Výpisy ze skriptu (například `println` v Groovy) se zapisují do logu platformy,
ke kterému mají přístup pouze administrátoři CRA. Ve svém výstupu je tedy
neuvidíte — pro ladění skriptu se na ně nespoléhejte.

## API

Základní URI podle prostředí a způsob přihlášení najdete v sekci
[API](../../API/README.md).

| Metoda   | URI                                                        | Popis                               |
|----------|------------------------------------------------------------|-------------------------------------|
| `GET`    | `/transformations`                                         | seznam transformací dostupných účtu |
| `GET`    | `/projects/{projectId}/transformations`                    | seznam transformací účtu            |
| `POST`   | `/projects/{projectId}/transformations`                    | založení transformace               |
| `GET`    | `/projects/{projectId}/transformations/{transformationId}` | detail transformace                 |
| `PUT`    | `/projects/{projectId}/transformations/{transformationId}` | úprava transformace                 |
| `DELETE` | `/projects/{projectId}/transformations/{transformationId}` | smazání transformace                |

Zakládat, upravovat a mazat transformace lze pouze pod účtem, ke kterému máte
přístup — u cizího účtu vrátí API odpověď `403`. Správa transformací v portálu
je zatím vyhrazena administrátorům CRA, přes API ale transformace založit lze.

Pro čtení doporučujeme `GET /transformations`. Volání pod
`/projects/{projectId}/` zná u atributu `type` jen starší hodnoty, takže
u funkcí typu `IN`, `PAYLOAD` a `DATAFLOW` vrátí `type` nevyplněný.

Výpis obsahuje veřejné transformace a dále transformace účtů, ke kterým máte
přístup.

### Tělo požadavku pro POST a PUT

| Parametr         | Povinný | Popis                                                    |
|------------------|---------|----------------------------------------------------------|
| `label`          | ano     | název transformace, 1 až 64 znaků                        |
| `type`           | ano     | `IN`, `PAYLOAD`, `DATAFLOW`, `OUT` (starší `DEV`, `MSG`) |
| `subType`        | ano     | `LORA`, `MQTT`, `HTTP`, `UDP`                            |
| `definitionType` | ano     | `JAVASCRIPT` nebo `GROOVY`                               |
| `definition`     | ano     | vlastní kód skriptu                                      |
| `description`    | ne      | popis transformace, max. 160 znaků                       |

`definition` se předává jako jeden JSON řetězec. Kód je proto potřeba zapsat do
jednoho řádku a uvozovky v něm escapovat.

### Příklad založení

```bash
curl --location --request POST 'https://api.iot.cra.cz/cxf/api/v1/projects/T202003241250003xdv/transformations' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhb....6d26' \
--data '{
  "label": "Prevod teploty",
  "description": "Prevede prvni dva bajty payloadu na teplotu",
  "type": "DATAFLOW",
  "subType": "MQTT",
  "definitionType": "JAVASCRIPT",
  "definition": "function (message) { var m = JSON.parse(message); return JSON.stringify({ teplota: parseInt(m.data.slice(0, 4), 16) / 10 }); }"
}'
```

Odpověď obsahuje `transformationId`, kterým se transformace přiřazuje dál:

```json
{
  "status": "success",
  "transformationId": 156,
  "links": {
    "self": "/cxf/api/v1/projects/T202003241250003xdv/transformations/156"
  }
}
```

### Přiřazení transformace

Získané `transformationId` se uvádí v parametru `transformationId` při zakládání
nebo úpravě objektu:

| Kam se transformace přiřazuje | Volání                                                                               |
|-------------------------------|--------------------------------------------------------------------------------------|
| MQTT zařízení                 | [`POST /mqtt/devices`](../../Vstup%20do%20IoT%20platformy/MQTT/README.md)            |
| MQTT gateway                  | [`POST /mqtt/gateways`](../../Výstup%20z%20IoT%20platformy/MQTT%20gateway/README.md) |
| HTTP endpoint                 | `POST /http/endpoints`                                                               |

Přiřadit ji lze také v portálu, v detailu zařízení, datového toku nebo výstupu.

## Omezení

- Transformaci nelze smazat, dokud je přiřazená k nějakému zařízení, datovému
  toku nebo výstupu. Nejdříve ji odeberte ze všech míst, kde se používá.
- Veřejné transformace (`public: true`) připravuje CRA. Jsou dostupné všem
  účtům, ale pouze pro čtení — upravit ani smazat je nelze.

## Příklady

- [Netlia](../../Zařízení/Dle%20výrobce/Netlia/README.md) — převod zprávy
  z NB-IoT čidla přijaté přes UDP do struktury, které platforma rozumí
