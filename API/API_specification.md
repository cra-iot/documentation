# **CRA IoT Platforma**

# **Průvodní dokument k novému API**

# **Obsah**

[1 Úvod](#úvod)

[2 Základní pravidla API](#základní-pravidla-api)

[2.1 Ověření](#ověření)

[2.2 Pagination](#pagination)

[2.3 Řazení](#řazení)

[2.4 Filtrace](#filtrace)

[2.5 Fulltextové vyhledávání](#fulltextové-vyhledávání)

[2.6 Našeptávače](#našeptávače)

[2.7 Lokalizace](#lokalizace)

[2.8 Standardní Success Response u GET](#standardní-success-response-u-get)

[2.9 Standardní Error Response](#standardní-error-response)

[2.10 Indikace v komentářích Swagger](#indikace-v-komentářích-swagger)

[2.11 Obecné](#obecné)

[3 API](#api)

[3.1 Customers](#customers)

[3.1.1 GET ​/customers](#get-customers)

[3.1.2 GET /customers​/{id}](#get-customersid)

[3.1.3 GET /customers​/{id}​/services](#get-customersidservices)

[3.1.4 GET /customers​/{id}​/projects](#get-customersidprojects)

[3.2 Services](#services)

[3.2.1 GET /services](#get-services)

[3.2.2 GET ​/services​/{id}](#get-servicesid)

[3.2.3 GET ​/services​/{id}​/counters](#get-servicesidcounters)

[3.2.4 GET ​/services​/{id}​/projects](#get-servicesidprojects)

[3.2.5 POST ​/services​/{id}​/projects​/{projectId}​/assign](#post-servicesidprojectsprojectidassign)

[3.2.6 DELETE ​/services​/{id}​/projects​/{projectId}​/assign](#delete-servicesidprojectsprojectidassign)

[3.2.7 POST ​/services​/{id}​/devices​/{protocol}/{deviceId}​/assign](#post-servicesiddevicesprotocoldeviceidassign)

[3.3 Projects](#projects)

[3.3.1 GET ​/projects](#get-projects)

[3.3.2 POST ​/projects](#post-projects)

[3.3.3 GET ​/projects​/{id}](#get-projectsid)

[3.3.4 PUT ​/projects​/{id}](#put-projectsid)

[3.3.5 DELETE ​/projects​/{id}](#delete-projectsid)

[3.3.6 PUT ​/projects​/{id}​/parameters](#put-projectsidparameters)

[3.3.7 GET ​/projects​/{id}​/counters](#get-projectsidcounters)

[3.3.8 GET ​/projects​/{id}​/services](#get-projectsidservices)

[3.3.9 GET ​/projects​/{id}​/endpoints​/overview](#get-projectsidendpointsoverview)

[3.3.10 GET ​/projects​/{id}​/devices​/overview](#get-projectsiddevicesoverview)

[3.3.11 GET /projects/{id}/device-groups/overview](#get-projectsiddevice-groupsoverview)

[3.4 HTTP](#http)

[3.4.1 Endpoints](#endpoints)

[3.4.1.1 GET /http​/endpoints](#get-httpendpoints)

[3.4.1.2 POST ​/http​/endpoints](#post-httpendpoints)

[3.4.1.3 GET ​/http​/endpoints​/suggestions](#get-httpendpointssuggestions)

[3.4.1.4 GET ​/http​/endpoints​/{id}](#get-httpendpointsid)

[3.4.1.5 PUT ​/http​/endpoints​/{id}](#put-httpendpointsid)

[3.4.1.6 DELETE ​/http​/endpoints​/{id}](#delete-httpendpointsid)

[3.4.1.7 GET ​/http​/endpoints​/{id}​/deliveries](#get-httpendpointsiddeliveries)

[3.4.1.8 GET ​/http​/endpoints​/{id}​/deliveries/full-detail](#get-httpendpointsiddeliveriesfull-detail)

[3.4.1.9 POST ​/http​/endpoints​/{id}​/ping](#post-httpendpointsidping)

[3.4.1.10 [NYI] PUT ​/http​/endpoints​/{id}​/tags](#nyi-put-httpendpointsidtags)

[3.4.1.11 [NYI] PUT ​/http​/endpoints​/{id}​/attributes](#nyi-put-httpendpointsidtags)

[3.5 MQTT](#mqtt)

[3.5.1 Gateways](#gateways)

[3.5.1.1 GET /mqtt​/gateways](#get-mqttgateways)

[3.5.1.2 POST ​/mqtt​/gateways](#post-mqttgateways)

[3.5.1.3 GET ​/mqtt​/gateways ​/suggestions](#get-mqttgateways-suggestions)

[3.5.1.4 GET ​/mqtt​/gateways ​/{id1](#get-mqttgateways-id)

[3.5.1.5 PUT ​/mqtt​/gateways ​/{id}](#put-mqttgateways-id)

[3.5.1.6 DELETE ​/mqtt​/gateways ​/{id}](#delete-mqttgateways-id)

[3.5.1.7 GET ​/mqtt​/gateways​/{id}​/deliveries](#get-mqttgatewaysiddeliveries)

[3.5.1.8 GET ​/mqtt​/gateways​/{id}​/deliveries/full-detail](#get-mqttgatewaysiddeliveriesfull-detail)

[3.5.1.9 [NYI] PUT ​/mqtt​/gateways​/{id}​/tags](#nyi-put-mqttgatewaysidtags)

[3.5.1.10 [NYI] PUT ​/mqtt​/gateways​/{id}​/attributes](#nyi-put-mqttgatewaysidattributes)

[3.6 MQTT](#mqtt-1)

[3.6.1 Devices](#devices)

[3.6.1.1 GET ​/mqtt​/devices​/](#get-mqttdevices)

[3.6.1.2 POST ​/mqtt​/devices​/](#post-mqttdevices)

[3.6.1.3 GET ​/mqtt​/devices​/suggestions](#get-mqttdevicessuggestions)

[3.6.1.4 GET ​/mqtt​/devices​/{id}](#get-mqttdevicesid)

[3.6.1.5 PUT ​/mqtt​/devices​/{id}](#put-mqttdevicesid)

[3.6.1.6 DELETE ​/mqtt​/devices​/{id}](#delete-mqttdevicesid)

[3.6.1.7 PUT ​/mqtt​/devices​/{id}​/tags](#put-mqttdevicesidtags)

[3.6.1.8 PUT ​/mqtt​/devices​/{id}​/attributes](#put-mqttdevicesidattributes)

[3.6.1.9 GET ​/mqtt​/devices​/import​/{id}](#get-mqttdevicesimportid)

[3.6.1.10 GET ​/mqtt​/devices​/{id}​/counters](#get-mqttdevicesidcounters)

[3.6.1.11 POST ​/mqtt​/devices​/{id}​/enable](#post-mqttdevicesidenable)

[3.6.1.12 DELETE ​/mqtt​/devices​/{id}​/enable](#delete-mqttdevicesidenable)

[3.6.1.13 GET ​/mqtt​/devices​/{id}​/down​/messages](#get-mqttdevicesiddownmessages)

[3.6.1.14 POST ​/mqtt​/devices​/{id}​/down​/messages](#post-mqttdevicesiddownmessages)

[3.6.1.15 GET /mqtt/devices/{id}/up/messages](#get-mqttdevicesidupmessages)

[3.6.1.16 GET ​/mqtt​/devices​/{id}​/up​/messages/{messageId}/deliveries](#get-mqttdevicesidupmessagesmessageiddeliveries)

[3.6.1.17 GET /mqtt​/devices​/{id}​/down​/messages/stats](#get-mqttdevicesiddownmessagesstats)

[3.6.1.18 GET ​​/mqtt​/devices​/{id}​/up​/messages/stats](#get-mqttdevicesidupmessagesstats)

[3.7 LoRa](#lora)

[3.7.1 Devices](#devices-1)

[3.7.1.1 GET ​/lora​/devices](#get-loradevices)

[3.7.1.2 GET ​/lora/devices​/suggestions](#get-loradevicessuggestions)

[3.7.1.3 POST /lora​/devices​/abp​/csv](#post-loradevicesabpcsv)

[3.7.1.4 POST /lora​/devices​/otaa​/csv](#post-loradevicesotaacsv)

[3.7.1.5 POST /lora​/devices​/abp](#post-loradevicesabp)

[3.7.1.6 POST /lora​/devices​/otaa](#post-loradevicesotaa)

[3.7.1.7 GET ​/lora​/devices​/{id}](#get-loradevicesid)

[3.7.1.8 PUT ​/lora​/devices​/{id}](#put-loradevicesid)

[3.7.1.9 DELETE ​/lora​/devices​/{id}](#delete-loradevicesid)

[3.7.1.10 PUT ​/lora​/devices​/{id}​/tags](#put-loradevicesidtags)

[3.7.1.11 PUT ​/lora/devices​/{id}​/attributes](#put-loradevicesidattributes)

[3.7.1.12 GET ​/lora​/devices​/import​/{id}](#get-loradevicesimportid)

[3.7.1.13 GET ​/lora/devices​/{id}​/counters](#get-loradevicesidcounters)

[3.7.1.14 POST ​/lora​/devices​/{id}​/enable](#post-loradevicesidenable)

[3.7.1.15 DELETE ​/lora​/devices​/{id}​/enable](#delete-loradevicesidenable)

[3.7.1.16 GET ​/lora​/devices​/{id}​/down​/messages](#get-loradevicesiddownmessages)

[3.7.1.17 POST ​/lora/devices​/{id}​/down​/messages](#post-loradevicesiddownmessages)

[3.7.1.18 GET ​/lora​/devices​/{id}​/up​/messages](#get-loradevicesidupmessages)

[3.7.1.19 GET ​/lora​/devices​/{id}​/up​/messages/{messageId}/deliveries](#get-loradevicesidupmessagesmessageiddeliveries)

[3.7.1.20 ​POST /lora/signal/{id})](#post-lorasignalid)

[3.7.1.21 GET /lora/devices​/{id}​/down​/messages/stats](#get-loradevicesiddownmessagesstats)

[3.7.1.22 ​GET lora/devices​/{id}​/up​/messages/stats](#get-loradevicesidupmessagesstats)

[3.7.1.23 PUT /lora/devices/{id}/parameters](#put-loradevicesidparameters)

[3.7.1.24 POST /lora/devices/{id}/activate](#post-loradevicesidactivate)

[3.8 Device Groups](#device-groups)

[3.8.1 GET ​/device-groups](#get-device-groups)

[3.8.2 POST ​/device-groups](#post-device-groups)

[3.8.3 GET ​/device-groups​/suggestions](#get-device-groupssuggestions)

[3.8.4 GET ​/device-groups​/{id}](#get-device-groupsid)

[3.8.5 PUT ​/device-groups​/{id}](#put-device-groupsid)

[3.8.6 DELETE ​/device-groups​/{id}](#delete-device-groupsid)

[3.8.7 [NYI] PUT ​/device-groups​/{id}​/tags](#nyi-put-device-groupsidtags)

[3.8.8 [NYI] PUT /device-groups​/{id}​/attributes](#nyi-put-device-groupsidattributes)

[3.8.9 GET ​/device-groups​/devices](#get-device-groupsdevices)

[3.8.10 GET ​/device-groups​/endpoints](#get-device-groupsendpoints)

[3.8.11 POST ​/device-groups​/{id}​/devices/{protocol} ​/{deviceId}​/assign](#post-device-groupsiddevicesprotocol-deviceidassign)

[3.8.12 DELETE ​/device-groups​/{id}​/devices​/{protocol}/{deviceId}​/assign](#delete-device-groupsiddevicesprotocoldeviceidassign)

[3.8.13 POST ​/device-groups​/{id}​/endpoints​/{endpointId}​/assign](#post-device-groupsidendpointsendpointidassign)

[3.8.14 DELETE ​/device-groups​/{id}​/endpoints​/{endpointId}​/assign](#delete-device-groupsidendpointsendpointidassign)

[3.9 Users](#users)

[3.9.1 GET ​/users](#get-users)

[3.9.2 GET ​/users​/suggestions](#get-userssuggestions)

[3.9.3 GET ​/users​/{id}](#get-usersid)

[3.9.4 PUT ​/users​/{id}0](#put-usersid)

[3.9.5 PUT ​/users​/{id}​/customers​/{customerId}​/projects​/{projectId}​/privileges](#put-usersidcustomerscustomeridprojectsprojectidprivileges)

[3.10 Notifications](#notifications)

[3.10.1 GET ​/notifications](#get-notifications)

[3.10.2 GET ​/notifications​/customers​/{customerId}](#get-notificationscustomerscustomerid)

[3.10.3 [NYI] GET ​/notifications​/customers​/{customerId}​/sent](#nyi-get-notificationscustomerscustomeridsent)

[3.10.4 GET ​/notifications​/customers​/{customerId}​/emails](#get-notificationscustomerscustomeridemails)

[3.10.5 POST /notifications​/customers​/{customerId}​/emails](#post-notificationscustomerscustomeridemails)

[3.10.6 GET ​/notifications​/customers​/{customerId}​/emails​/{email}](#get-notificationscustomerscustomeridemailsemail)

[3.10.7 DELETE ​/notifications​/customers​/{customerId}​/emails​/{email}](#delete-notificationscustomerscustomeridemailsemail)

[3.10.8 [NYI] GET ​/notifications​/customers​/{customerId}​/emails​/{email}​/sent](#nyi-get-notificationscustomerscustomeridemailsemailsent)

[3.10.9 PATCH ​/notifications​/customers​/{customerId}​/templates​/{template}](#patch-notificationscustomerscustomeridtemplatestemplate)

[3.10.10 PATCH ​/notifications​/customers​/{customerId}​/templates​/{template}​/emails​/{email}](#patch-notificationscustomerscustomeridtemplatestemplateemailsemail)

[3.11 Audits](#audits)

[3.11.1 GET /audits](#get-audits)

[3.11.2 GET ​/audits​/customers​/{customerId}](#get-auditscustomerscustomerid)

[3.11.3 GET ​/audits​/projects​/{projectId}](#get-auditsprojectsprojectid)

[3.11.4 [NYI] GET ​/audits​/devices​/{protocol}/{deviceId}](#nyi-get-auditsdevicesprotocoldeviceid)

[3.11.5 [NYI] GET ​/audits​/device-groups​/{groupId}](#nyi-get-auditsdevice-groupsgroupid)

[3.12 Tags](#tags)

[3.12.1 GET /tags/devices](#get-tagsdevices)

[3.13 Attributes](#attributes)

[3.13.1 GET /attributes/devices](#get-attributesdevices)

# Úvod

Tento dokument slouží jako doprovodný dokument k dodanému swagger. Definuje základy použití API a také v případě potřeby upřesňuje použití konkrétních REST volání.

# Základní pravidla API

Následující kapitola popisuje základní pravidla pro použití API, jako ověření, filtrace, atd.


## Ověření

U všech volání je vyžadováno ověření volajícího pomocí metody _Bearer authorization_, kde token je OpenId token získaný ověřením na SSO. Tzn., že každé volání musí obsahovat hlavičku authorization, např.:

```
curl --request GET \
--url http://api.iot.cra.cz/cxf/api/v1/customers \
--header 'Authorization: Bearer $access\_token' \
```

access\_token získáte požadavkem na naši SSO platformu takto:
```
curl --request POST \
--url https://sso.cra.cz/auth/realms/CRA/protocol/openid-connect/token \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'username=$email\>' \
--data-urlencode 'password=$password\>' \
--data-urlencode 'grant\_type=password' \
--data-urlencode 'client\_id=iot-api-client' \
--data-urlencode 'client\_secret=41a113b7-5486-45e3-8a3d-e0b106a5d446'
```

Detailní popis autentizačního API najdete zde: [API Documentation Red Hat Single Sign-On 7.2 | Red Hat Customer Portal](https://access.redhat.com/documentation/en-us/red_hat_single_sign-on/7.2/html/api_documentation/index)

## Pagination

Volání, která podporují stránkování, obsahují ve specifikaci query parametr offset a limit. Limit definuje maximální počet vrácených záznamů a Offset stanovuje číslo záznamu (v rámci řazení), od kterého budou záznamy vráceny.

Standardně volání také vracejí celkový počet záznamů, viz kapitola 2.9.

## Řazení

Řazení dat je definováno pomocí query parametru sort. Ten specifikuje atribut, přes který je požadováno řazení, kdy tento je uvozen znakem + popř. jeho reprezentace jako %2B pro vzestupné řazení (implicitní), resp. – (resp. %2D) pro sestupné řazení.

Seznam konkrétních atributů, přes které lze v daném volání řadit, je vždy uveden u konkrétního volání.

```
curl --request GET \
--url http://api.iot.cra.cz/cxf/api/v1/lora/devices?sort=%2BlastMessageIn \
--header'authorization: Bearer dXNlcjpw…' \
```

## Filtrace

Seznam konkrétních atributů, přes které lze v daném volání řadit, je vždy uveden u konkrétního volání.

Syntaxe query parametru je atribut[operátor]=hodnota.

Operátory:

| **Operátor** | **Význam** |
| --- | --- |
| eq | rovnost (implicitní) |
| lte | menší než |
| gte | větší než |
| like | klasický „like" s tím že wildcard je doplněn jen jako postfix |

Atribut tags připouští použití seznamu slov oddělených znakem „,", ale pouze v případě, že je použit operátor eq.

Příklad: customerName[like]=CRA

V řeči SQL bude výsledkem dotaz:

*SELECT \* FROM customers WHERE customerName LIKE 'CRA%';*

Pokud je uveden více než jeden filtrační parametr, tak tyto jsou spojeny pomocí logického operátoru AND.

Pokud je třeba filtrovat prázdné hodnoty, lze pomocí kombinace eq a NULL. Příklad: batteryStatus[eq]=NULL

## Fulltextové vyhledávání

Fulltextové vyhledávání je prováděno pomocí query parametru search. U relevantního volání je vždy uvedeno, zda umožňuje fulltextové vyhledávání.

Syntaxe query parametru je taková, že obsahuje hledané výrazy doplněné o operátory:

| **Operátor** | **Význam** |
| --- | --- |
| + | Slovo se musí vyskytovat v daném řádku (implicitní) |
| - | Slovo se nesmí vyskytovat v daném řádku |
| \* | Wildcard - může se vyskytovat pouze na konci slova |
| () | Seskupení výrazu do podvýrazu |
| " | Citace |

Vzorová data:

| **Text** |
| --- |
| České Radiokomunikace a.s. |
| České2 Radiokomunikace a.s. |

Příklady (bez URL encode):

search=Čes\*

| **Text** |
| --- |
| České Radiokomunikace a.s. |
| České2 Radiokomunikace a.s. |

search=Čes\* -České2

| **Text** |
| --- |
| České Radiokomunikace a.s. |

search="České Ra"

| **Text** |
| --- |
| České Radiokomunikace a.s. |

## Našeptávače

Pokud je pro daný resource implementován _našeptávač_, tak existuje URI \*/suggestions. Jako query parametr je použít atribut search, popsaný v kapitole 2.6.

Našeptávač vrátí vždy maximálně prvních 5 záznamů. Našeptávače podporují pouze vyhledávání pomocí výrazu _text\*_, např. Elektro\*

## Lokalizace

Lokalizace se předpokládá na úrovni GUI dle předaného katalogu. Pokud API předává text, u kterého je třeba lokalizace, uvede do daného řetězce kód textu z katalogu, např. MQTT-INVALIDADDRESSFORMAT.

Pokud obsahuje katalogové hlášení tzv. placeholders, jsou tyto uvedeny v pořadí výskytu v textu za kódem hlášení z katalogu. Oddělovačem výrazu je znak „,".

Příklad:

Katalogové hláška - MQTT-DUPLICITDEVICE – Zařízení %deviceId% již existuje

Chybové hlášení z API - MQTT-DUPLICITDEVICE,951DCE3092180032

## Standardní Success Response u GET

Standardní JSON odpověď JSON u GET metod obsahuje následující atributy:

| **Atribut** | **Význam** |
| --- | --- |
| status | Vždy success |
| metadata | Obsahuje metadata o dotazu, tj. kolik záznamů splňující dotaz existuje celkem a kolik bylo vráceno |
| data | Data odpovědi a referenční odkaz |
| links | Referenční odkaz |

Příklad:

```JSON
{
  "status": "success",
  "metadata": {
    "count": 1,
    "result": 1
  },
  "data": [
    {
      "deviceGroupId": 634,
      …
      "links": {
        "self": "/cxf/api/v1/device-groups/634"
      }
    }
  ],
  "links": {
    "self": "/cxf/api/v1/device-groups"
  }
}
```

## Standardní Error Response

Standartní chybová odpověď obsahuje následující JSON (viz swagger).

Příklad:

```
{
  "code": 100,
  "status": "error",
  "errors": [
    "error"
  ]
}
```

status je vždy error

Pokud je hodnota code \<= 100, pak se jedná o interní chybu (např. špatně použité API) a chyby v atributu errors jsou v plné textaci.

Pokud je hodnotacode \> 100, jedná se o uživatelskou chybu a v atributuerrors budou kódy z katalogu a případně parametry dle specifikace v kapitole 2.8.

## Indikace v komentářích Swagger

| **Zkratka** | Význam |
| --- | --- |
| INT | Interní atribut |
| **NYI** | Zatím není implementováno |

## Obecné

Pokud se v rámci popisu API hovoří o vrácení _všech_ záznamů (případně kompletním seznamu), tak se vždy jedná o kompletní seznam v rámci práv daného uživatele.

Doplňující tabulka v jednotlivých volání:

| **URL** | \<METODA\> http://\<URL\>/\<cesta\> |
| --- | --- |
| **Filtr** | Seznam atributů, nad kterými lze filtrovat |
| **Řazení** | Seznam atributů, nad kterými lze řadit |
| **Fulltext** | Zda je možné použít query parametrsearch |
| **Katalog** | Seznam atributů, které obsahují hlášku z katalogu k lokalizaci |

# API

# Customers

# GET ​/customers

Kompletní seznam zákazníků.

| **URL** | GET http://\<URL\>/cxf/api/v1/customers |
| --- | --- |
| **Filtr** | customerId<br/>customerName<br/>isReseller<br/>portalId |
| **Řazení** | customerId<br/>customerName<br/>isReseller<br/>portalId |
| **Fulltext** | Ano |
| **Katalog** |

# GET /customers​/{id}

Informace o konkrétním zákazníkovi.

| **URL** | GET http://\<URL\>/cxf/api/v1/customers/{id} |
| --- | --- |
| **Filtr** |
| **Řazení** |
| **Fulltext** | Ne |
| **Katalog** |


# GET /customers​/{id}​/services

Vrátí seznam všech nasmlouvaných služeb zákazníka (včetně parametrů).

| **URL** | GEThttp://\<URL\>/cxf/api/v1/customers/{id}/services |
| --- | --- |
| Filtr | custServiceIdcustServiceNametarifIdtarifNamecustomerIdproductElementIdserviceActivationTimesuspendedsuspendTimeresumeTimeenableddeviceServiceIddiscontinueddiscontinuationTime |
| **Řazení** | custServiceIdcustServiceNametarifIdtarifNamecustomerIdproductElementIdserviceActivationTimesuspendedsuspendTimeresumeTimeenableddeviceServiceIddiscontinueddiscontinuationTime |
| **Fulltext** | Ano |
| **Katalog** | data.parameters.name |

# GET /customers​/{id}​/projects

Vrátí seznam všech projektů (včetně parametrů) daného zákazníka.

| **URL** | GEThttp://\<URL\>/cxf/api/v1/customers/{id}/projects |
| --- | --- |
| Filtr | projectIdprojectNamecustomerIdsuspendedsuspendTimeresumeTimefreemium |
| **Řazení** | projectIdprojectNamecustomerIdsuspendedsuspendTimeresumeTimefreemium |
| **Fulltext** | Ano |
| **Katalog** | data.parameters.name |

# Services

# GET /services

Vrátí seznam všech služeb (včetně parametrů).

| **URL** | GEThttp://\<URL\>/cxf/api/v1/services |
| --- | --- |
| Filtr | custServiceIdcustServiceNametarifIdtarifNamecustomerIdproductElementIdserviceActivationTimesuspendedsuspendTimeresumeTimeenableddeviceServiceIddiscontinueddiscontinuationTime |
| **Řazení** | custServiceIdcustServiceNametarifIdtarifNamecustomerIdproductElementIdserviceActivationTimesuspendedsuspendTimeresumeTimeenableddeviceServiceIddiscontinueddiscontinuationTime |
| **Fulltext** | Ano |
| **Katalog** | data.parameters.name |

# GET ​/services​/{id}

Informace o konkrétní službě (včetně parametrů).

| **URL** | GEThttp://\<URL\>/cxf/api/v1/services/{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** | data.parameters.name |

# GET ​/services​/{id}​/counters

Stav counterů dané služby.

| **URL** | GEThttp://\<URL\>/cxf/api/v1/services/{id}/counters |
| --- | --- |
| Filtr | counterIdnamevaluelimit |
| **Řazení** | counterIdnamevaluelimit |
| **Fulltext** | Ne |
| **Katalog** | data.name |

# GET ​/services​/{id}​/projects

Vrátí seznam všech projektů (včetně parametrů), které mají přiřazenu danou službu.

| **URL** | GEThttp://\<URL\>/cxf/api/v1/services/{id}/projects |
| --- | --- |
| Filtr | projectIdprojectNamecustomerIdsuspendedsuspendTimeresumeTimefreemium |
| **Řazení** | projectIdprojectNamecustomerIdsuspendedsuspendTimeresumeTimefreemium |
| **Fulltext** | Ano |
| **Katalog** | data.parameters.name |

# POST ​/services​/{id}​/projects​/{projectId}​/assign

Přiřadí službu na projekt. Bez této akce nelze v rámci daného projektu čerpat danou službu a importovat na ni zařízení.

| **URL** | POSThttp://\<URL\>/cxf/api/v1/services/{id}/projects/{projectId}/assign |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# DELETE ​/services​/{id}​/projects​/{projectId}​/assign

Odebere službu z projektu. Nelze provést, pokud existují zařízení, která jsou na tuto službu přiřazena.

| **URL** | DELETEhttp://\<URL\>/cxf/api/v1/services/{id}/projects/{projectId}/assign |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# POST ​/services​/{id}​/devices​/{protocol}/{deviceId}​/assign

Migrace zařízení na novou službu v rámci stejného projektu a zákazníka. Projekt musí mít cílovou službu k dispozici.

| **URL** | POSThttp://\<URL\>/cxf/api/v1/services/{id}/devices/{protocol}/{deviceId}/assign |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# Projects

# GET ​/projects

Vrátí seznam všech projektů (včetně parametrů).

| **URL** | GEThttp://\<URL\>/cxf/api/v1/projects |
| --- | --- |
| Filtr | projectIdprojectNamecustomerIdsuspendedsuspendTimeresumeTimefreemium |
| **Řazení** | projectIdprojectNamecustomerIdsuspendedsuspendTimeresumeTimefreemium |
| **Fulltext** | Ano |
| **Katalog** | data.parameters.name |

# POST ​/projects

Založení nového projektu. Akce obvykle trvá déle (10-20s), protože je třeba provést např. založení databáze, atd.

| **URL** | POSThttp://\<URL\>/cxf/api/v1/projects |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# GET ​/projects​/{id}

Informace o projektu včetně parametrů.

| **URL** | GEThttp://\<URL\>/cxf/api/v1/projects/{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** | data.parameters.name |

# PUT ​/projects​/{id}

Aktualizace atributů projektu.

| **URL** | PUThttp://\<URL\>/cxf/api/v1/projects/{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# DELETE ​/projects​/{id}

Zrušení projektu. Projekt nelze zrušit, pokud obsahuje některý z podřízených objektů, jako zařízení, endpoint, skupinu zařízení, atd.

| **URL** | DELETEhttp://\<URL\>/cxf/api/v1/projects/{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# PUT ​/projects​/{id}​/parameters

Editace parametrů projektu. Tato funkcionalita je dostupná pouze zákazníkům typu _Reseller_.

| **URL** | PUThttp://\<URL\>/cxf/api/v1/projects/{id}/parameters |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

Přípustné atributy:

| **Atribut** | **Hodnota** |
| --- | --- |
| DEV\_LMT\_ACTUAL | Integer – Maximální počet zařízení |
| DEV\_LMT\_ACTUAL\_IS\_INDEF | 1/0: 1 – nekonečno |
| IN\_MSG\_LMT\_USR | Integer – Limit počtu zpráv ze zařízení |
| IN\_MSG\_LMT\_USR\_IS\_INDEF | 1/0: 1 – nekonečno |
| MSG\_LMT\_USR\_PERIOD | Perioda counteru – DAY, WEEK, MONTH, YEAR, INFINITE |
| OUT\_MSG\_LMT\_USR | Integer – Limit počtu zpráv na zařízení |
| OUT\_MSG\_LMT\_USR\_IS\_INDEF | 1/0: 1 – nekonečno |

_Další specifika je třeba konzultovat se zadavatelem._

# GET ​/projects​/{id}​/counters

Informace o konkrétní službě (včetně parametrů).

| **URL** | GEThttp://\<URL\>/cxf/api/v1/projects/{id}/counters |
| --- | --- |
| Filtr | counterIdnamevaluelimit |
| **Řazení** | counterIdnamevaluelimit |
| **Fulltext** | Ne |
| **Katalog** | name |

# GET ​/projects​/{id}​/services

Vrátí seznam všech služeb (včetně parametrů), které jsou přiřazeny projektu.

| **URL** | GEThttp://\<URL\>/cxf/api/v1/projects/{id}/services |
| --- | --- |
| Filtr | custServiceIdcustServiceNametarifIdtarifNamecustomerIdproductElementIdserviceActivationTimesuspendedsuspendTimeresumeTimeenableddeviceServiceIddiscontinueddiscontinuationTime |
| **Řazení** | custServiceIdcustServiceNametarifIdtarifNamecustomerIdproductElementIdserviceActivationTimesuspendedsuspendTimeresumeTimeenableddeviceServiceIddiscontinueddiscontinuationTime |
| **Fulltext** | Ano |
| **Katalog** | data.parameters.name |

# GET ​/projects​/{id}​/endpoints​/overview

Analytický přehled o endpointech na projektu.

| **URL** | GEThttp://\<URL\>/cxf/api/v1/projects/{id}/endpoint/overview |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# GET ​/projects​/{id}​/devices​/overview

Vrátí analytický přehled o zařízeních na projektu.

| **URL** | GEThttp://\<URL\>/cxf/api/v1/projects/{id}/devices/overview |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# GET /projects/{id}/device-groups/overview

Vrátí analytický přehled skupin zařízení.

| **URL** | GEThttp://\<URL\>/cxf/api/v1/projects/{id}/device-groups/overview |
| --- | --- |
| Filtr | deviceGroupIddeviceGroupNameenabledlastEnableTimelastDisableTime |
| **Řazení** | deviceGroupIddeviceGroupNameenabledlastEnableTimelastDisableTime |
| **Fulltext** | Ne |
| **Katalog** |
 |

# HTTP

# Endpoints

# GET /http​/endpoints

Vrátí seznam všech http endpointů (včetně parametrů, tagů, atributů a seznamu skupin, do kterých je přiřazen).

| **URL** | GEThttp://\<URL\>/cxf/api/v1/http/endpoints |
| --- | --- |
| Filtr | custDestIdprojectIdcustDestNamecustDestEnabledtransformationIdlastSuccessfulDeliveryfailedDeliveries |
| **Řazení** | custDestIdprojectIdcustDestNamecustDestEnabledtransformationIdlastSuccessfulDeliveryfailedDeliveries |
| **Fulltext** | Ano |
| **Katalog** |
 |

# POST ​/http​/endpoints

Založení http endpointu.

| **URL** | POSThttp://\<URL\>/cxf/api/v1/http/endpoints |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# GET ​/http​/endpoints​/suggestions

Našeptávač k http endpointům.

| **URL** | GEThttp://\<URL\>/cxf/api/v1/http/endpoints /suggestions |
| --- | --- |
| Filtr | projectId |
| **Řazení** |
 |
| **Fulltext** | Ano |
| **Katalog** |
 |

# GET ​/http​/endpoints​/{id}

Vrátí informace o http endpointu (včetně parametrů, tagů, atributů a seznamu skupin, do kterých je přiřazen).

| **URL** | GEThttp://\<URL\>/cxf/api/v1/http/endpoints ​/{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# PUT ​/http​/endpoints​/{id}

Aktualizace nastavení http endpointu.

| **URL** | PUThttp://\<URL\>/cxf/api/v1/http/endpoints/​{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# DELETE ​/http​/endpoints​/{id}

Výmaz http endpointu. Nelze provést, pokud je endpoint přiřazen skupině zařízení.

| **URL** | DELETEhttp://\<URL\>/cxf/api/v1/http/endpoints/​{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# GET ​/http​/endpoints​/{id}​/deliveries

Zobrazení doručení zpráv na endpoint.

Maximální rozpětí mezi query parametry from a to je 31 dní.

Parametr from je validován konstantou 2021-04-20 06:26 V případě požadavku před touto konstantou dojde k odpovědi s response code 303 a textem v body : „From is less than minimal 2021-04-20 06:26:00.000"

| **URL** | GEThttp://\<URL\>/cxf/api/v1/http​/endpoints​/{id}​/deliveries |
| --- | --- |
| Filtr | messageIdtransformationIdcodeerror |
| **Řazení** | messageIdtransformationIdrequestTime |
| **Fulltext** | Ne |
| **Katalog** |
 |

# GET ​/http​/endpoints​/{id}​/deliveries/full-detail

Zobrazení doručení zpráv na endpoint včetně obsahu zpráv a ID zařízení.

Maximální rozpětí mezi query parametry from a to je 31 dní.

Parametr from je validován konstantou 2021-04-20 06:26 V případě požadavku před touto konstantou dojde k odpovědi s response code 303 a textem v body : „From is less than minimal 2021-04-20 06:26:00.000"

| **URL** | GEThttp://\<URL\>/cxf/api/v1/http​/endpoints​/{id}​/deliveries/full-detail |
| --- | --- |
| Filtr | messageIdtransformationIdcodeerrorcustDeviceName |
| **Řazení** | messageIdtransformationIdrequestTime |
| **Fulltext** | Ne |
| **Katalog** |
 |

# POST ​/http​/endpoints​/{id}​/ping

Test http endpointu. Zašle požadavek dle specifikace a vrátí odpověď.

| **URL** | POSThttp://\<URL\>/cxf/api/v1​/http​/endpoints​/{id}​/ping |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# [NYI] PUT ​/http​/endpoints​/{id}​/tags

Aktualizace tagů endpointu.

| **URL** | POSThttp://\<URL\>/cxf/api/v1​/http​/endpoints​/{id}​/ping |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# [NYI] PUT ​/http​/endpoints​/{id}​/attributes

Aktualizace atributů endpointu.

| **URL** | POSThttp://\<URL\>/cxf/api/v1​/http​/endpoints​/{id}​/ping |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# MQTT

# Gateways

# GET /mqtt​/gateways

Vrátí seznam všech mqtt gateways (včetně parametrů, tagů, atributů a seznamu skupin, do kterých je přiřazen).

| **URL** | GEThttp://\<URL\>/cxf/api/v1/mqtt/gateways |
| --- | --- |
| Filtr | custDestIdprojectIdcustDestNamecustDestEnabledtransformationIdlastSuccessfulDeliveryfailedDeliveries |
| **Řazení** | custDestIdprojectIdcustDestNamecustDestEnabledtransformationIdlastSuccessfulDeliveryfailedDeliveries |
| **Fulltext** | Ano |
| **Katalog** |
 |

# POST ​/mqtt​/gateways

Založení mqtt gateway.

| **URL** | POSThttp://\<URL\>/cxf/api/v1/mqtt/ gateways |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# GET ​/mqtt​/gateways ​/suggestions

Našeptávač k mqtt gateways.

| **URL** | GEThttp://\<URL\>/cxf/api/v1/mqtt/ gateways /suggestions |
| --- | --- |
| Filtr | projectId |
| **Řazení** |
 |
| **Fulltext** | Ano |
| **Katalog** |
 |

# GET ​/mqtt​/gateways ​/{id}

Vrátí informace o mqtt gateway (včetně parametrů, tagů, atributů a seznamu skupin, do kterých je přiřazen).

| **URL** | GEThttp://\<URL\>/cxf/api/v1/mqtt/ gateways ​/{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# PUT ​/mqtt​/gateways ​/{id}

Aktualizace nastavení mqtt gateway.

| **URL** | PUThttp://\<URL\>/cxf/api/v1/mqtt/ gateways /​{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# DELETE ​/mqtt​/gateways ​/{id}

Výmaz mqtt gateway. Nelze provést, pokud je gatewaypřiřazena skupině zařízení.

| **URL** | DELETEhttp://\<URL\>/cxf/api/v1/mqtt/ gateways /​{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# GET ​/mqtt​/gateways​/{id}​/deliveries

Zobrazení informací jednotlivých pokusech o doručení na gateway.

Maximální rozpětí mezi query parametry from a to je 31 dní.

Parametr from je validován konstantou 2021-04-20 06:26 V případě požadavku před touto konstantou dojde k odpovědi s response code 303 a textem v body : „From is less than minimal 2021-04-20 06:26:00.000"

| **URL** | GEThttp://\<URL\>/cxf/api/v1/mqtt​/ gateways ​/{id}​/deliveries |
| --- | --- |
| Filtr | messageIdtransformationIdcodeerror |
| **Řazení** | messageIdtransformationIdrequestTime |
| **Fulltext** | Ne |
| **Katalog** |
 |

# GET ​/mqtt​/gateways​/{id}​/deliveries/full-detail

Zobrazení informací jednotlivých pokusech o doručení na gateway, včetně obsahu zpráv a ID zařízení.

Maximální rozpětí mezi query parametry from a to je 31 dní.

Parametr from je validován konstantou 2021-04-20 06:26 V případě požadavku před touto konstantou dojde k odpovědi s response code 303 a textem v body : „From is less than minimal 2021-04-20 06:26:00.000"

| **URL** | GEThttp://\<URL\>/cxf/api/v1/mqtt​/ gateways ​/{id}​/deliveries/full-detail |
| --- | --- |
| Filtr | messageIdtransformationIdcodeerrorcustDeviceName |
| **Řazení** | messageIdtransformationIdrequestTime |
| **Fulltext** | Ne |
| **Katalog** |
 |

# [NYI] PUT ​/mqtt​/gateways​/{id}​/tags

Aktualizace tagů gateway.

| **URL** | POSThttp://\<URL\>/cxf/api/v1​/mqtt​/ gateways ​/{id}​/ping |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# [NYI] PUT ​/mqtt​/gateways​/{id}​/attributes

Aktualizace atributů gateways.

| **URL** | POSThttp://\<URL\>/cxf/api/v1​/mqtt​/endpoints​/{id}​/ping |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# MQTT

# Devices

# GET ​/mqtt​/devices​/

Vrátí seznam všech mqtt zařízení (včetně tagů, atributů a seznamu skupin, do kterých jsou přiřazena).

| **URL** | GEThttp://\<URL\>/cxf/api/v1/mqtt​/devices​/ |
| --- | --- |
| Filtr | deviceIdcustDeviceNamecustServiceIdstatusenabledenableTimedisableTimesuspendedsuspendTimeresumeTimeprovisionTimecustomerIdprojectIdlastMessageInlastMessageOuttagsdeviceGroupId |
| **Řazení** | deviceIdcustDeviceNamecustServiceIdstatusenabledenableTimedisableTimesuspendedsuspendTimeresumeTimeprovisionTimecustomerIdprojectIdlastMessageInlastMessageOuttags |
| **Fulltext** | Ano |
| **Katalog** |
 |

# POST ​/mqtt​/devices​/

Import MQTT zařízení (lze importovat více než jedno zařízení najednou). Provádí se asynchronně. Pokud je základní validace úspěšná, je v odpovědi vráceno batchId, přes které se dá dotazovat na stav, viz kapitola 3.6.1.9.

Importní dávka musí obsahovat pouze jednu službu a projekt.

| **URL** | POSThttp://\<URL\>/cxf/api/v1/mqtt​/devices​/ |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# GET ​/mqtt​/devices​/suggestions

Našeptávač pro MQTT zařízení.

| **URL** | GEThttp://\<URL\>/cxf/api/v1/mqtt​/devices​/suggestions |
| --- | --- |
| Filtr | projectId |
| **Řazení** |
 |
| **Fulltext** | Ano |
| **Katalog** |
 |

# GET ​/mqtt​/devices​/{id}

Vrátí informace o mqtt zařízení (včetně tagů, atributů a seznamu skupin, do kterých je přiřazeno).

| **URL** | GEThttp://\<URL\>/cxf/api/v1/mqtt​/devices​/{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# PUT ​/mqtt​/devices​/{id}

Editace mqtt zařízení.

| **URL** | PUThttp://\<URL\>/cxf/api/v1/mqtt​/devices​/{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# DELETE ​/mqtt​/devices​/{id}

Výmaz mqtt zařízení. Zařízení nelze vymazat, pokud je přiřazeno do skupiny zařízení.

| **URL** | DELETEhttp://\<URL\>/cxf/api/v1/mqtt​/devices​/{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# PUT ​/mqtt​/devices​/{id}​/tags

Aktualizace tagů mqtt zařízení.

| **URL** | PUThttp://\<URL\>/cxf/api/v1/mqtt​/devices​/{id}/tags |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# PUT ​/mqtt​/devices​/{id}​/attributes

Aktualizace atributů mqtt zařízení.

| **URL** | PUThttp://\<URL\>/cxf/api/v1/mqtt​/devices​/{id}/attributes |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# GET ​/mqtt​/devices​/import​/{id}

Zjištění stavu importu zařízení.

| **URL** | GEThttp://\<URL\>/cxf/api/v1/mqtt​/devices/import​/{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** | errors.errorMessage |

# GET ​/mqtt​/devices​/{id}​/counters

Výpis stavu counterů na zařízení.

| **URL** | GEThttp://\<URL\>/cxf/api/v1/mqtt​/devices /counters |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** | name |

# POST ​/mqtt​/devices​/{id}​/enable

Povolení zařízení (implicitní stav). Zprávy z takového zařízení jsou přijímány na platformu a jsou doručovány.

| **URL** | POSThttp://\<URL\>/cxf/api/v1/mqtt​/devices​/{id}​/enable |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# DELETE ​/mqtt​/devices​/{id}​/enable

Pozastavení zařízení. Zprávy z takového zařízení jsou přijímány na platformu, ale nejsou doručovány.

| **URL** | DELETEhttp://\<URL\>/cxf/api/v1/mqtt​/devices​/{id}​/enable |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# GET ​/mqtt​/devices​/{id}​/down​/messages

Zobrazení zpráv odeslaných na zařízení.

Maximální rozpětí mezi query parametry from a to je 31 dní.

| **URL** | GEThttp://\<URL\>/cxf/api/v1/mqtt​/devices​/{id}​/down​/messages |
| --- | --- |
| Filtr | data |
| **Řazení** | messageTime |
| **Fulltext** | Ne |
| **Katalog** |
 |

# POST ​/mqtt​/devices​/{id}​/down​/messages

Odeslání zprávy na MQTT zařízení.

| **URL** | POSThttp://\<URL\>/cxf/api/v1/mqtt​/devices​/{id}​/down​/messages |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# GET /mqtt/devices/{id}/up/messages

Výpis zpráv z MQTT zařízení.

Maximální rozpětí mezi query parametry from a to je 31 dní.

| **URL** | GEThttp://\<URL\>/cxf/api/v1/mqtt​/devices​/{id}​/up​/messages |
| --- | --- |
| Filtr | data |
| **Řazení** | messageTime |
| **Fulltext** | Ne |
| **Katalog** |
 |

# GET ​/mqtt​/devices​/{id}​/up​/messages/{messageId}/deliveries

Výpis doručení zprávy na endpointy.

Parametr messageId je validován konstantou 2021-04-20 06:26 V případě požadavku před touto konstantou dojde k odpovědi s response code 303 a textem v body : „MessageId datetime is less than minimal 2021-04-20 06:26:00.000"

| **URL** | GEThttp://\<URL\>/cxf/api/v1/mqtt​/devices​/{id}​/up​/messages/{messageId}/deliveries |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# GET /mqtt​/devices​/{id}​/down​/messages/stats

Denní statistika zpráv odeslaných na MQTT zařízení.

Maximální rozpětí mezi query parametry from a to je 31 dní.

| **URL** | GEThttp://\<URL\>/cxf/api/v1/mqtt​/devices​/{id}​/down​/messages/stats |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# GET ​/mqtt​/devices​/{id}​/up​/messages/stats

Denní statistika zpráv z MQTT zařízení. Jedná se o kompletní počty, tj. včetně zpráv, které byly přijaty, ale nebyly doručeny z důvodu překročení limitu.

Maximální rozpětí mezi query parametry from a to je 31 dní.

| **URL** | GEThttp://\<URL\>/cxf/api/v1/mqtt​/devices​/{id}​/up​/messages/stats |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# LoRa

# Devices

# GET ​/lora​/devices​/

Vrátí seznam všech lora zařízení (včetně tagů, atributů a seznamu skupin, do kterých jsou přiřazena).

| **URL** | GEThttp://\<URL\>/cxf/api/v1/lora​/devices​/ |
| --- | --- |
| Filtr | deviceIdcustDeviceNamecustServiceIdstatusenabledenableTimedisableTimesuspendedsuspendTimeresumeTimeprovisionTimecustomerIdprojectIdlastMessageInlastMessageOuttagssignalStrengthbateryStatusdeviceTypedeviceGroupIddeviceStatus |
| **Řazení** | deviceIdcustDeviceNamecustServiceIdenabledenableTimedisableTimestatussuspendedsuspendTimeresumeTimeprovisionTimecustomerIdprojectIdlastMessageInlastMessageOuttagssignalStrengthbateryStatusdeviceTypedeviceStatus |
| **Fulltext** | Ano |
| **Katalog** |
 |

# GET ​/lora/devices​/suggestions

Našeptávač pro lora zařízení.

| **URL** | GEThttp://\<URL\>/cxf/api/v1/lora/devices​/suggestions |
| --- | --- |
| Filtr | projectId |
| **Řazení** |
 |
| **Fulltext** | Ano |
| **Katalog** |
 |

# POST /lora​/devices​/abp​/csv

Hromadný import ABP zařízení z CSV souboru (definice dle dokumentace). Provádí se asynchronně. Pokud je základní validace úspěšná, je v odpovědi vráceno batchId, přes které se dá dotazovat na stav, viz kapitola 3.7.1.12.

Importní dávka musí obsahovat pouze jednu službu a projekt.

| **URL** | POSThttp://\<URL\>/cxf/api/v1/lora​/devices​/abp​/csv |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# POST /lora​/devices​/otaa​/csv

Hromadný import OTAA zařízení z CSV souboru (definice dle dokumentace). Provádí se asynchronně. Pokud je základní validace úspěšná, je v odpovědi vráceno batchId, přes které se dá dotazovat na stav, viz kapitola 3.7.1.12.

Importní dávka musí obsahovat pouze jednu službu a projekt.

| **URL** | POSThttp://\<URL\>/cxf/api/v1/lora​/devices​/otaa​/csv |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# POST /lora​/devices​/abp

Hromadný import ABP zařízení. Provádí se asynchronně. Pokud je základní validace úspěšná, je v odpovědi vráceno batchId, přes které se dá dotazovat na stav, viz kapitola 3.7.1.12.

Importní dávka musí obsahovat pouze jednu službu a projekt.

| **URL** | POSThttp://\<URL\>/cxf/api/v1/lora​/devices​/abp​ |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# POST /lora​/devices​/otaa

Hromadný import OTAA zařízení. Provádí se asynchronně. Pokud je základní validace úspěšná, je v odpovědi vráceno batchId, přes které se dá dotazovat na stav, viz kapitola 3.7.1.12.

Importní dávka musí obsahovat pouze jednu službu a projekt.

| **URL** | POSThttp://\<URL\>/cxf/api/v1/lora​/devices​/otaa​ |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# GET ​/lora​/devices​/{id}

Vrátí informace o lora zařízení (včetně tagů, atributů a seznamu skupin, do kterých je přiřazeno).

| **URL** | GEThttp://\<URL\>/cxf/api/v1/lora​/devices​/{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# PUT ​/lora​/devices​/{id}

Editace lora zařízení.

| **URL** | PUThttp://\<URL\>/cxf/api/v1/lora​/devices​/{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# DELETE ​/lora​/devices​/{id}

Výmaz lora zařízení. Zařízení nelze vymazat, pokud je přiřazeno do skupiny zařízení.

| **URL** | DELETEhttp://\<URL\>/cxf/api/v1/lora​/devices​/{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# PUT ​/lora​/devices​/{id}​/tags

Aktualizace tagů lora zařízení.

| **URL** | PUThttp://\<URL\>/cxf/api/v1/lora​/devices​/{id}/tags |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# PUT ​/lora/devices​/{id}​/attributes

Aktualizace atributů lora zařízení.

| **URL** | PUThttp://\<URL\>/cxf/api/v1/lora/devices​/{id}/attributes |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# GET ​/lora​/devices​/import​/{id}

Zjištění stavu importu zařízení.

| **URL** | GEThttp://\<URL\>/cxf/api/v1/lora​/devices/import​/{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** | errors.errorMessage |

# GET ​/lora/devices​/{id}​/counters

Výpis stavu counterů na zařízení.

| **URL** | GEThttp://\<URL\>/cxf/api/v1/lora​/devices /counters |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** | name |

# POST ​/lora​/devices​/{id}​/enable

Povolení zařízení (implicitní stav). Zprávy z takového zařízení jsou přijímány na platformu a jsou doručovány.

| **URL** | POSThttp://\<URL\>/cxf/api/v1/mqtt​/devices​/{id}​/enable |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# DELETE ​/lora​/devices​/{id}​/enable

Pozastavení zařízení. Zprávy z takového zařízení jsou přijímány na platformu, ale nejsou doručovány.

| **URL** | DELETEhttp://\<URL\>/cxf/api/v1/lora​/devices​/{id}​/enable |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# GET ​/lora​/devices​/{id}​/down​/messages

Zobrazení zpráv odeslaných na zařízení.

Maximální rozpětí mezi query parametry from a to je 31 dní.

| **URL** | GEThttp://\<URL\>/cxf/api/v1/lora​/devices​/{id}​/down​/messages |
| --- | --- |
| Filtr | data |
| **Řazení** | messageTime |
| **Fulltext** | Ne |
| **Katalog** |
 |

# POST ​/lora/devices​/{id}​/down​/messages

Odeslání zprávy na lora zařízení.

| **URL** | POSThttp://\<URL\>/cxf/api/v1/lora​/devices​/{id}​/down​/messages |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# GET ​/lora​/devices​/{id}​/up​/messages

Výpis zpráv z lora zařízení.

Maximální rozpětí mezi query parametry from a to je 31 dní.

| **URL** | GEThttp://\<URL\>/cxf/api/v1/lora/devices​/{id}​/up​/messages |
| --- | --- |
| Filtr | dataid |
| **Řazení** | messageTimeid |
| **Fulltext** | Ne |
| **Katalog** |
 |

# GET ​/lora​/devices​/{id}​/up​/messages/{messageId}/deliveries

Výpis doručení zprávy na endpointy.

Parametr messageId je validován konstantou 2021-04-20 06:26 V případě požadavku před touto konstantou dojde k odpovědi s response code 303 a textem v body : „MessageId datetime is less than minimal 2021-04-20 06:26:00.000"

| **URL** | GEThttp://\<URL\>/cxf/api/v1/lora​/devices​/{id}​/up​/messages/{messageId}/deliveries |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# ​POST /lora/signal/{id}

Zjištění síly signálu dle souřadnic a typu zařízení.

| **URL** | POSThttp://\<URL\>/cxf/api/v1/lora/signal/{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# GET /lora/devices​/{id}​/down​/messages/stats

Denní statistika zpráv odeslaných na LoRa zařízení.

Maximální rozpětí mezi query parametry from a to je 31 dní.

| **URL** | GEThttp://\<URL\>/cxf/api/v1/lora​/devices​/{id}​/down​/messages/stats |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# ​GET lora/devices​/{id}​/up​/messages/stats

Denní statistika zpráv z LoRa zařízení. Jedná se o kompletní počty, tj. včetně zpráv, které byly přijaty, ale nebyly doručeny z důvodu překročení limitu.

Maximální rozpětí mezi query parametry from a to je 31 dní.

| **URL** | GEThttp://\<URL\>/cxf/api/v1/lora​/devices​/{id}​/up​/messages/stats |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# PUT /lora/devices/{id}/parameters

Aktualizace parametrů lora zařízení.

| **URL** | PUThttp://\<URL\>/cxf/api/v1/lora/devices​/{id}/parameters |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# POST /lora/devices/{id}/activate

Aktivace LoRa zařízení z prekativního stavu

| **URL** | PUThttp://\<URL\>/cxf/api/v1/lora/devices​/{id}/activate |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# Device Groups

# GET ​/device-groups

Vrátí seznam všech skupin zařízení (včetně tagů a atributů).

| **URL** | GEThttp://\<URL\>/cxf/api/v1/device-groups |
| --- | --- |
| Filtr | deviceGroupIdprojectIddeviceGroupNameenabledlastEnableTimelastDisableTime |
| **Řazení** | deviceGroupIdprojectIddeviceGroupNameenabledlastEnableTimelastDisableTime |
| **Fulltext** | Ano |
| **Katalog** |
 |

# POST ​/device-groups

Založení skupiny zařízení

| **URL** | POSThttp://\<URL\>/cxf/api/v1/device-groups |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# GET ​/device-groups​/suggestions

Našeptávač pro skupiny zařízení.

| **URL** | GEThttp://\<URL\>/cxf/api/v1/device-groups​/suggestions |
| --- | --- |
| Filtr | projectId |
| **Řazení** |
 |
| **Fulltext** | Ano |
| **Katalog** |
 |

# GET ​/device-groups​/{id}

Vrátí informace o skupině zařízení (včetně tagů a atributů).

| **URL** | GEThttp://\<URL\>/cxf/api/v1/device-groups​/{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# PUT ​/device-groups​/{id}

Editace skupiny zařízení.

| **URL** | PUThttp://\<URL\>/cxf/api/v1/device-groups​/{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# DELETE ​/device-groups​/{id}

Výmaz skupiny zařízení. Skupinu nelze vymazat, pokud je k ní přiřazeny endpointy nebo zařízení.

| **URL** | DELETEhttp://\<URL\>/cxf/api/v1/device-groups​/{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# [NYI] PUT ​/device-groups​/{id}​/tags

Aktualizace tagů skupiny zařízení.

| **URL** | PUThttp://\<URL\>/cxf/api/v1/device-groups​/{id}​/tags |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# [NYI] PUT /device-groups​/{id}​/attributes

Aktualizace atributů skupiny zařízení.

| **URL** | PUThttp://\<URL\>/cxf/api/v1/device-groups​/{id}​/attributes |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# GET ​/device-groups​/devices

Výpis zjednodušeného seznamu zařízení přiřazených ke skupině. Pro detail k zařízení je třeba provést extra dotaz.

| **URL** | GEThttp://\<URL\>/cxf/api/v1/device-groups​/devices |
| --- | --- |
| Filtr | deviceIddeviceProtocolprojectIdcustDeviceName |
| **Řazení** | deviceIddeviceProtocolprojectIdcustDeviceName |
| **Fulltext** | Ano |
| **Katalog** |
 |

# GET ​/device-groups​/endpoints

Výpis zjednodušeného seznamu endpointů přiřazených ke skupině. Pro detail k endpontu je třeba provést extra dotaz.

| **URL** | GEThttp://\<URL\>/cxf/api/v1/device-groups​/endpoints |
| --- | --- |
| Filtr | custDestIdprojectIdcustDestNamecustDestType |
| **Řazení** | custDestIdprojectIdcustDestNamecustDestType |
| **Fulltext** | Ano |
| **Katalog** |
 |

# POST ​/device-groups​/{id}​/devices/{protocol} ​/{deviceId}​/assign

Přiřazení zařízení skupině zařízení. Povolené hodnoty atributu protocol jsou _lora_ a _mqtt._

| **URL** | POSThttp://\<URL\>/cxf/api/v1/device-groups​/{id}​/devices/{protocol} /{deviceId}​/assign |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# DELETE ​/device-groups​/{id}​/devices​/{protocol}/{deviceId}​/assign

Odebrání zařízení ze skupiny. Povolené hodnoty atributu protocol jsou _lora_ a _mqtt._

| **URL** | DELETEhttp://\<URL\>/cxf/api/v1/device-groups​/{id}​/devices​/{protocol} /{deviceId}​/assign |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# POST ​/device-groups​/{id}​/endpoints​/{endpointId}​/assign

Přiřazení endpointu skupině zařízení.

| **URL** | POSThttp://\<URL\>/cxf/api/v1/device-groups​/{id}​/endpoints​/{endpointId}​/assign |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# DELETE ​/device-groups​/{id}​/endpoints​/{endpointId}​/assign

Odebrání endpointu ze skupiny.

| **URL** | DELETEhttp://\<URL\>/cxf/api/v1​/device-groups​/{id}​/endpoints​/{endpointId}​/assign |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# Users

# GET ​/users

Vrátí seznam všech uživatelů (včetně práv a parametrů).

| **URL** | GEThttp://\<URL\>/cxf/api/v1/users |
| --- | --- |
| Filtr | userIdfirstNamelastNamephoneemailcustomerIdprojectId |
| **Řazení** | userIdfirstNamelastNamephoneemail |
| **Fulltext** | Ano |
| **Katalog** |
 |

# GET ​/users​/suggestions

Našeptávač pro uživatele.

| **URL** | GEThttp://\<URL\>/cxf/api/v1​/users​/suggestions |
| --- | --- |
| Filtr | customerId |
| **Řazení** |
 |
| **Fulltext** | Ano |
| **Katalog** |
 |

# GET ​/users​/{id}

Informace o uživateli (včetně práv a parametrů).

| **URL** | GEThttp://\<URL\>/cxf/api/v1/users/{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# PUT ​/users​/{id}​

Aktualizace uživatelských preferencí.

| **URL** | PUThttp://\<URL\>/cxf/api/v1/users​/{id}​ |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# PUT ​/users​/{id}​/customers​/{customerId}​/projects​/{projectId}​/privileges

Přiřazení, případně odebrání práva uživatele k danému projektu.

| **URL** | GEThttp://\<URL\>/cxf/api/v1/users​/{id}​/customers​/{customerId}​/projects​/{projectId}​/privileges |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# Notifications

# GET ​/notifications

Načtení nastavení notifikací uživatelů.

| **URL** | GEThttp://\<URL\>/cxf/api/v1/notifications |
| --- | --- |
| Filtr | emailcustomeId |
| **Řazení** | emailcustomeId |
| **Fulltext** | Ano |
| **Katalog** |
 |

# GET ​/notifications​/customers​/{customerId}

Načtení nastavení notifikací uživatele.

| **URL** | GEThttp://\<URL\>/cxf/api/v1 /notifications​/customers​/{customerId} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# [NYI] GET ​/notifications​/customers​/{customerId}​/sent

Načtení odeslaných notifikací uživatele.

| **URL** | GEThttp://\<URL\>/cxf/api/v1 /notifications​/customers​/{customerId}​/sent |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ano |
| **Katalog** |
 |

# GET ​/notifications​/customers​/{customerId}​/emails

Načtení nastavení notifikací neuživatelských emailů.

| **URL** | GEThttp://\<URL\>/cxf/api/v1/notifications​/customers​/{customerId}​/emails |
| --- | --- |
| Filtr | email |
| **Řazení** | email |
| **Fulltext** | Ano |
| **Katalog** |
 |

# POST /notifications​/customers​/{customerId}​/emails

Registrace notifikačního emailu.

| **URL** | POSThttp://\<URL\>/cxf/api/v1/notifications​/customers​/{customerId}​/emails |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# GET ​/notifications​/customers​/{customerId}​/emails​/{email}

Načtení nastavení notifikací neuživatelského emailu.

| **URL** | GEThttp://\<URL\>/cxf/api/v1 ​/notifications​/customers​/{customerId}​/emails​/{email} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# DELETE ​/notifications​/customers​/{customerId}​/emails​/{email}

Odregistrace notifikačního emailu.

| **URL** | DELETEhttp://\<URL\>/cxf/api/v1/notifications​/customers​/{customerId}​/emails |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# [NYI] GET ​/notifications​/customers​/{customerId}​/emails​/{email}​/sent

Načtení odeslaných notifikací neuživatelského emailu.

| **URL** | GEThttp://\<URL\>/cxf/api/v1/notifications​/customers​/{customerId}​/emails​/{email}​/sent |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ano |
| **Katalog** |
 |

# PATCH ​/notifications​/customers​/{customerId}​/templates​/{template}

Úprava nastavení notifikací uživatele.

| **URL** | PATCHhttp://\<URL\>/cxf/api/v1 /notifications​/customers​/{customerId}​/templates​/{template} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |


# PATCH ​/notifications​/customers​/{customerId}​/templates​/{template}​/emails​/{email}

Úprava nastavení notifikací neuživatelského emailu.

| **URL** | PATCHhttp://\<URL\>/cxf/api/v1/notifications​/customers​/{customerId}​/templates​/{template}​/emails​/{email} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# Audits

# GET /audits

Zobrazení kompletního auditního logu.

parameters obsahuje páry klíč hodnota dle placeholderů v textu dané katalogové hlášky. Tyto jsou standardně označeny postfixem a prefixem %.

| **URL** | GEThttp://\<URL\>/cxf/api/v1/audits |
| --- | --- |
| Filtr | customerIdprojectIdcodeleveltimestamporiginatorsource |
| **Řazení** | customerIdprojectIdcodeleveltimestamporiginatorsource |
| **Fulltext** | Ano |
| **Katalog** | code |

# GET ​/audits​/customers​/{customerId}

Zobrazení auditního logu zákazníka.

parameters obsahuje páry klíč hodnota dle placeholderů v textu dané katalogové hlášky. Tyto jsou standardně označeny postfixem a prefixem %.

| **URL** | GEThttp://\<URL\>/cxf/api/v1/audits​/customers​/{customerId} |
| --- | --- |
| Filtr | customerIdprojectIdcodeleveltimespamporiginatorsource |
| **Řazení** | customerIdprojectIdcodeleveltimespamporiginatorsource |
| **Fulltext** | Ano |
| **Katalog** | code |

# GET ​/audits​/projects​/{projectId}

Zobrazení auditního logu projektu.

parameters obsahuje páry klíč hodnota dle placeholderů v textu dané katalogové hlášky. Tyto jsou standardně označeny postfixem a prefixem %.

| **URL** | GEThttp://\<URL\>/cxf/api/v1/audits​/projects​/{projectId} |
| --- | --- |
| Filtr | customerIdprojectIdcodeleveltimestamporiginatorsource |
| **Řazení** | customerIdprojectIdcodeleveltimestamporiginatorsource |
| **Fulltext** | Ano |
| **Katalog** | code |

# [NYI] GET ​/audits​/devices​/{protocol}/{deviceId}

Zobrazení auditního logu zařízení.

parameters obsahuje páry klíč hodnota dle placeholderů v textu dané katalogové hlášky. Tyto jsou standardně označeny postfixem a prefixem %.

| **URL** | GEThttp://\<URL\>/cxf/api/v1/audits​/devices​/{protocol}/{deviceId} |
| --- | --- |
| Filtr | customerIdprojectIdcodeleveltimespamporiginatorsource |
| **Řazení** | customerIdprojectIdcodeleveltimespamporiginatorsource |
| **Fulltext** | Ano |
| **Katalog** | code |

# [NYI] GET ​/audits​/device-groups​/{groupId}

Zobrazení auditního logu skupiny zařízení.

parameters obsahuje páry klíč hodnota dle placeholderů v textu dané katalogové hlášky. Tyto jsou standardně označeny postfixem a prefixem %.

| **URL** | GEThttp://\<URL\>/cxf/api/v1/audits​/device-groups​/{groupId} |
| --- | --- |
| Filtr | customerIdprojectIdcodeleveltimespamporiginatorsource |
| **Řazení** | customerIdprojectIdcodeleveltimespamporiginatorsource |
| **Fulltext** | Ano |
| **Katalog** | code |

# Tags

# GET /tags/devices

Načtení tagu zařízení

Kompletní seznam tagů.

| **URL** | GEThttp://\<URL\>/cxf/api/v1/tags/devices |
| --- | --- |
| Filtr | customerIdprojectIddeviceIdtag |
| **Řazení** | tag |
| **Fulltext** | Ano |
| **Katalog** |
 |

# Attributes

# GET /attributes/devices

Načtení atributů zařízení

Kompletní seznam atributů.

| **URL** | GEThttp://\<URL\>/cxf/api/v1/tags/devices |
| --- | --- |
| Filtr | customerIdprojectIddeviceIdattributevalue |
| **Řazení** | attribute |
| **Fulltext** | Ano |
| **Katalog** |
 |
```
