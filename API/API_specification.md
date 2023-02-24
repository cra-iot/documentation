# **CRA IoT Platforma**

# **Průvodní dokument k novému API**

# **Obsah**

[1.Úvod 7](#_Toc128137629)

[2.Základní pravidla API 7](#_Toc128137630)

[2.1.Ověření 7](#_Toc128137631)

[2.2.Pagination 8](#_Toc128137632)

[2.3.Řazení 8](#_Toc128137633)

[2.4.Filtrace 8](#_Toc128137634)

[2.5.Fulltextové vyhledávání 9](#_Toc128137635)

[2.6.Našeptávače 10](#_Toc128137636)

[2.7.Lokalizace 10](#_Toc128137637)

[2.8.Standardní Success Response u GET 10](#_Toc128137638)

[2.9.Standardní Error Response 11](#_Toc128137639)

[2.10.Indikace v komentářích Swagger 12](#_Toc128137640)

[2.11.Obecné 12](#_Toc128137641)

[2.12.Interní poznámky 12](#_Toc128137642)

[3.API 12](#_Toc128137643)

[3.1.Customers 12](#_Toc128137644)

[3.1.1.GET ​/customers 13](#_Toc128137645)

[3.1.2.GET /customers​/{id} 13](#_Toc128137646)

[3.1.3.GET /customers​/{id}​/services 13](#_Toc128137647)

[3.1.4.GET /customers​/{id}​/projects 14](#_Toc128137648)

[3.2.Services 15](#_Toc128137649)

[3.2.1.GET /services 15](#_Toc128137650)

[3.2.2.GET ​/services​/{id} 16](#_Toc128137651)

[3.2.3.GET ​/services​/{id}​/counters 16](#_Toc128137652)

[3.2.4.GET ​/services​/{id}​/projects 17](#_Toc128137653)

[3.2.5.POST ​/services​/{id}​/projects​/{projectId}​/assign 17](#_Toc128137654)

[3.2.6.DELETE ​/services​/{id}​/projects​/{projectId}​/assign 18](#_Toc128137655)

[3.2.7.POST ​/services​/{id}​/devices​/{protocol}/{deviceId}​/assign 18](#_Toc128137656)

[3.3.Projects 19](#_Toc128137657)

[3.3.1.GET ​/projects 19](#_Toc128137658)

[3.3.2.POST ​/projects 19](#_Toc128137659)

[3.3.3.GET ​/projects​/{id} 20](#_Toc128137660)

[3.3.4.PUT ​/projects​/{id} 20](#_Toc128137661)

[3.3.5.DELETE ​/projects​/{id} 20](#_Toc128137662)

[3.3.6.PUT ​/projects​/{id}​/parameters 21](#_Toc128137663)

[3.3.7.GET ​/projects​/{id}​/counters 22](#_Toc128137664)

[3.3.8.GET ​/projects​/{id}​/services 22](#_Toc128137665)

[3.3.9.GET ​/projects​/{id}​/endpoints​/overview 23](#_Toc128137666)

[3.3.10.GET ​/projects​/{id}​/devices​/overview 23](#_Toc128137667)

[3.3.11.GET /projects/{id}/device-groups/overview 24](#_Toc128137668)

[3.4.HTTP 24](#_Toc128137669)

[3.4.1.Endpoints 24](#_Toc128137670)

[3.4.1.1.GET /http​/endpoints 24](#_Toc128137671)

[3.4.1.2.POST ​/http​/endpoints 25](#_Toc128137672)

[3.4.1.3.GET ​/http​/endpoints​/suggestions 25](#_Toc128137673)

[3.4.1.4.GET ​/http​/endpoints​/{id} 26](#_Toc128137674)

[3.4.1.5.PUT ​/http​/endpoints​/{id} 26](#_Toc128137675)

[3.4.1.6.DELETE ​/http​/endpoints​/{id} 26](#_Toc128137676)

[3.4.1.7.GET ​/http​/endpoints​/{id}​/deliveries 27](#_Toc128137677)

[3.4.1.8.GET ​/http​/endpoints​/{id}​/deliveries/full-detail 27](#_Toc128137678)

[3.4.1.9.POST ​/http​/endpoints​/{id}​/ping 28](#_Toc128137679)

[3.4.1.10.[NYI] PUT ​/http​/endpoints​/{id}​/tags 28](#_Toc128137680)

[3.4.1.11.[NYI] PUT ​/http​/endpoints​/{id}​/attributes 29](#_Toc128137681)

[3.5.MQTT 29](#_Toc128137682)

[3.5.1.Endpoints 29](#_Toc128137683)

[3.5.1.1.GET /mqtt​/gateways 29](#_Toc128137684)

[3.5.1.2.POST ​/mqtt​/gateways 30](#_Toc128137685)

[3.5.1.3.GET ​/mqtt​/gateways ​/suggestions 30](#_Toc128137686)

[3.5.1.4.GET ​/mqtt​/gateways ​/{id} 31](#_Toc128137687)

[3.5.1.5.PUT ​/mqtt​/gateways ​/{id} 31](#_Toc128137688)

[3.5.1.6.DELETE ​/mqtt​/gateways ​/{id} 31](#_Toc128137689)

[3.5.1.7.GET ​/mqtt​/gateways​/{id}​/deliveries 32](#_Toc128137690)

[3.5.1.8.GET ​/mqtt​/gateways​/{id}​/deliveries/full-detail 32](#_Toc128137691)

[3.5.1.9.[NYI] PUT ​/mqtt​/gateways​/{id}​/tags 33](#_Toc128137692)

[3.5.1.10.[NYI] PUT ​/mqtt​/gateways​/{id}​/attributes 33](#_Toc128137693)

[3.6.MQTT 34](#_Toc128137694)

[3.6.1.Devices 34](#_Toc128137695)

[3.6.1.1.GET ​/mqtt​/devices​/ 34](#_Toc128137696)

[3.6.1.2.POST ​/mqtt​/devices​/ 35](#_Toc128137697)

[3.6.1.3.GET ​/mqtt​/devices​/suggestions 35](#_Toc128137698)

[3.6.1.4.GET ​/mqtt​/devices​/{id} 36](#_Toc128137699)

[3.6.1.5.PUT ​/mqtt​/devices​/{id} 36](#_Toc128137700)

[3.6.1.6.DELETE ​/mqtt​/devices​/{id} 37](#_Toc128137701)

[3.6.1.7.PUT ​/mqtt​/devices​/{id}​/tags 37](#_Toc128137702)

[3.6.1.8.PUT ​/mqtt​/devices​/{id}​/attributes 37](#_Toc128137703)

[3.6.1.9.GET ​/mqtt​/devices​/import​/{id} 38](#_Toc128137704)

[3.6.1.10.GET ​/mqtt​/devices​/{id}​/counters 38](#_Toc128137705)

[3.6.1.11.POST ​/mqtt​/devices​/{id}​/enable 38](#_Toc128137706)

[3.6.1.12.DELETE ​/mqtt​/devices​/{id}​/enable 39](#_Toc128137707)

[3.6.1.13.GET ​/mqtt​/devices​/{id}​/down​/messages 39](#_Toc128137708)

[3.6.1.14.POST ​/mqtt​/devices​/{id}​/down​/messages 40](#_Toc128137709)

[3.6.1.15.GET /mqtt/devices/{id}/up/messages 40](#_Toc128137710)

[3.6.1.16.GET ​/mqtt​/devices​/{id}​/up​/messages/{messageId}/deliveries 41](#_Toc128137711)

[3.6.1.17.GET /mqtt​/devices​/{id}​/down​/messages/stats 41](#_Toc128137712)

[3.6.1.18.GET ​​/mqtt​/devices​/{id}​/up​/messages/stats 42](#_Toc128137713)

[3.7.LoRa 42](#_Toc128137714)

[3.7.1.Devices 42](#_Toc128137715)

[3.7.1.1.GET ​/lora​/devices​/ 42](#_Toc128137716)

[3.7.1.2.GET ​/lora/devices​/suggestions 43](#_Toc128137717)

[3.7.1.3.POST /lora​/devices​/abp​/csv 44](#_Toc128137718)

[3.7.1.4.POST /lora​/devices​/otaa​/csv 44](#_Toc128137719)

[3.7.1.5.POST /lora​/devices​/abp 45](#_Toc128137720)

[3.7.1.6.POST /lora​/devices​/otaa 45](#_Toc128137721)

[3.7.1.7.GET ​/lora​/devices​/{id} 46](#_Toc128137722)

[3.7.1.8.PUT ​/lora​/devices​/{id} 46](#_Toc128137723)

[3.7.1.9.DELETE ​/lora​/devices​/{id} 46](#_Toc128137724)

[3.7.1.10.PUT ​/lora​/devices​/{id}​/tags 47](#_Toc128137725)

[3.7.1.11.PUT ​/lora/devices​/{id}​/attributes 47](#_Toc128137726)

[3.7.1.12.GET ​/lora​/devices​/import​/{id} 47](#_Toc128137727)

[3.7.1.13.GET ​/lora/devices​/{id}​/counters 48](#_Toc128137728)

[3.7.1.14.POST ​/lora​/devices​/{id}​/enable 48](#_Toc128137729)

[3.7.1.15.DELETE ​/lora​/devices​/{id}​/enable 49](#_Toc128137730)

[3.7.1.16.GET ​/lora​/devices​/{id}​/down​/messages 49](#_Toc128137731)

[3.7.1.17.POST ​/lora/devices​/{id}​/down​/messages 49](#_Toc128137732)

[3.7.1.18.GET ​/lora​/devices​/{id}​/up​/messages 50](#_Toc128137733)

[3.7.1.19.GET ​/lora​/devices​/{id}​/up​/messages/{messageId}/deliveries 50](#_Toc128137734)

[3.7.1.20.​POST /lora/signal/{id} 51](#_Toc128137735)

[3.7.1.21.GET /lora/devices​/{id}​/down​/messages/stats 51](#_Toc128137736)

[3.7.1.22.​GET lora/devices​/{id}​/up​/messages/stats 51](#_Toc128137737)

[3.7.1.23. PUT /lora/devices/{id}/parameters 52](#_Toc128137738)

[3.7.1.24. POST /lora/devices/{id}/activate 52](#_Toc128137739)

[3.8.Device Groups 53](#_Toc128137740)

[3.8.1.GET ​/device-groups 53](#_Toc128137741)

[3.8.2.POST ​/device-groups 53](#_Toc128137742)

[3.8.3.GET ​/device-groups​/suggestions 54](#_Toc128137743)

[3.8.4.GET ​/device-groups​/{id} 54](#_Toc128137744)

[3.8.5.PUT ​/device-groups​/{id} 54](#_Toc128137745)

[3.8.6.DELETE ​/device-groups​/{id} 55](#_Toc128137746)

[3.8.7.[NYI] PUT ​/device-groups​/{id}​/tags 55](#_Toc128137747)

[3.8.8.[NYI] PUT /device-groups​/{id}​/attributes 56](#_Toc128137748)

[3.8.9.GET ​/device-groups​/devices 56](#_Toc128137749)

[3.8.10.GET ​/device-groups​/endpoints 56](#_Toc128137750)

[3.8.11.POST ​/device-groups​/{id}​/devices/{protocol} ​/{deviceId}​/assign 57](#_Toc128137751)

[3.8.12.DELETE ​/device-groups​/{id}​/devices​/{protocol}/{deviceId}​/assign 57](#_Toc128137752)

[3.8.13.POST ​/device-groups​/{id}​/endpoints​/{endpointId}​/assign 58](#_Toc128137753)

[3.8.14.DELETE ​/device-groups​/{id}​/endpoints​/{endpointId}​/assign 58](#_Toc128137754)

[3.9.Users 59](#_Toc128137755)

[3.9.1.GET ​/users 59](#_Toc128137756)

[3.9.2.GET ​/users​/suggestions 59](#_Toc128137757)

[3.9.3.GET ​/users​/{id} 60](#_Toc128137758)

[3.9.4.PUT ​/users​/{id}​ 60](#_Toc128137759)

[3.9.5.PUT ​/users​/{id}​/customers​/{customerId}​/projects​/{projectId}​/privileges 60](#_Toc128137760)

[3.10.Notifications 61](#_Toc128137761)

[3.10.1.GET ​/notifications 61](#_Toc128137762)

[3.10.2.GET ​/notifications​/customers​/{customerId} 61](#_Toc128137763)

[3.10.3.[NYI] GET ​/notifications​/customers​/{customerId}​/sent 62](#_Toc128137764)

[3.10.4.GET ​/notifications​/customers​/{customerId}​/emails 62](#_Toc128137765)

[3.10.5.POST /notifications​/customers​/{customerId}​/emails 62](#_Toc128137766)

[3.10.6.GET ​/notifications​/customers​/{customerId}​/emails​/{email} 63](#_Toc128137767)

[3.10.7.DELETE ​/notifications​/customers​/{customerId}​/emails​/{email} 63](#_Toc128137768)

[3.10.8.[NYI] GET ​/notifications​/customers​/{customerId}​/emails​/{email}​/sent 64](#_Toc128137769)

[3.10.9.PATCH ​/notifications​/customers​/{customerId}​/templates​/{template} 64](#_Toc128137770)

[3.10.10.PATCH ​/notifications​/customers​/{customerId}​/templates​/{template}​/emails​/{email} 65](#_Toc128137771)

[3.11.Audits 65](#_Toc128137772)

[3.11.1.GET /audits 65](#_Toc128137773)

[3.11.2.GET ​/audits​/customers​/{customerId} 66](#_Toc128137774)

[3.11.3.GET ​/audits​/projects​/{projectId} 66](#_Toc128137775)

[3.11.4.[NYI] GET ​/audits​/devices​/{protocol}/{deviceId} 67](#_Toc128137776)

[3.11.5.[NYI] GET ​/audits​/device-groups​/{groupId} 68](#_Toc128137777)

[3.12.Tags 68](#_Toc128137778)

[3.12.1 GET /tags/devices 68](#_Toc128137779)

[3.13 Attributes 69](#_Toc128137780)

[3.13.1 GET /attributes/devices 69](#_Toc128137781)

# Úvod

Tento dokument slouží jako doprovodný dokument k dodanému swagger. Definuje základy použití API a také v případě potřeby upřesňuje použití konkrétních REST volání.

1.
# Základní pravidla API

Následující kapitola popisuje základní pravidla pro použití API, jako ověření, filtrace, atd.

  1.
# Ověření

U všech volání je vyžadováno ověření volajícího pomocí metody _Bearer authorization_, kde token je OpenId token získaný ověřením na SSO. Tzn., že každé volání musí obsahovat hlavičku authorization, např.:

curl --request GET \

--url http://localhost:8185/cxf/api/v1/customers \

--header'authorization: Bearer eyJhbGciOiJSUzI1 …' \

Access\_token získáte požadavkem na naši SSO platformu takto:

POST '[https://sso.cra.cz/auth/realms/CRA/protocol/openid-connect/token](https://sso.cra.cz/auth/realms/CRA/protocol/openid-connect/token)' \

--header 'Content-Type: application/x-www-form-urlencoded' \

--data-urlencode 'username=\>' \

--data-urlencode 'password=\>' \

--data-urlencode 'grant\_type=password' \

--data-urlencode 'client\_id=iot-api-client' \

--data-urlencode 'client\_secret=41a113b7-5486-45e3-8a3d-e0b106a5d446'

Detailní popis autentizačního API najdete zde: [API Documentation Red Hat Single Sign-On 7.2 | Red Hat Customer Portal](https://access.redhat.com/documentation/en-us/red_hat_single_sign-on/7.2/html/api_documentation/index)

  1.
# Pagination

Volání, která podporují stránkování, obsahují ve specifikaci query parametr offset a limit. Limit definuje maximální počet vrácených záznamů a Offset stanovuje číslo záznamu (v rámci řazení), od kterého budou záznamy vráceny.

Standardně volání také vracejí celkový počet záznamů, viz kapitola 2.9.

  1.
# Řazení

Řazení dat je definováno pomocí query parametru sort. Ten specifikuje atribut, přes který je požadováno řazení, kdy tento je uvozen znakem + popř. jeho reprezentace jako %2F pro vzestupné řazení (implicitní), resp. – pro sestupné řazení.

Seznam konkrétních atributů, přes které lze v daném volání řadit, je vždy uveden u konkrétního volání.

curl --request GET \

--url http://localhost:8185/cxf/api/v1/customers?sort=- customerName \

--header'authorization: Bearer dXNlcjpw…' \

  1.
# Filtrace

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

SELECT \* FROM customers WHERE customerName LIKE 'CRA%';

Pokud je uveden více než jeden filtrační parametr, tak tyto jsou spojeny pomocí logického operátoru AND.

Pokud je třeba filtrovat prázdné hodnoty, lze pomocí kombinace eq a NULL. Příklad: batteryStatus[eq]=NULL

  1.
# Fulltextové vyhledávání

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

  1.
# Našeptávače

Pokud je pro daný resource implementován _našeptávač_, tak existuje URI \*/suggestions. Jako query parametr je použít atribut search, popsaný v kapitole 2.6.

Našeptávač vrátí vždy maximálně prvních 5 záznamů. Našeptávače podporují pouze vyhledávání pomocí výrazu _text\*_, např. Elektro\*

  1.
# Lokalizace

Lokalizace se předpokládá na úrovni GUI dle předaného katalogu. Pokud API předává text, u kterého je třeba lokalizace, uvede do daného řetězce kód textu z katalogu, např. MQTT-INVALIDADDRESSFORMAT.

Pokud obsahuje katalogové hlášení tzv. placeholders, jsou tyto uvedeny v pořadí výskytu v textu za kódem hlášení z katalogu. Oddělovačem výrazu je znak „,".

Příklad:

Katalogové hláška - MQTT-DUPLICITDEVICE – Zařízení %deviceId% již existuje

Chybové hlášení z API - MQTT-DUPLICITDEVICE,951DCE3092180032

  1.
# Standardní Success Response u GET

Standardní JSON odpověď JSON u GET metod obsahuje následující atributy:

| **Atribut** | **Význam** |
| --- | --- |
| status | Vždy success |
| metadata | Obsahuje metadata o dotazu, tj. kolik záznamů splňující dotaz existuje celkem a kolik bylo vráceno |
| data | Data odpovědi a referenční odkaz |
| links | Referenční odkaz |

Příklad:

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

"self": "/cxf/api/v1/devices/FA3134WQWE"

}

}

],

"links": {

"self": "/cxf/api/v1/devices"

}

}

  1.
# Standardní Error Response

Standartní chybová odpověď obsahuje následující JSON (viz swagger).

Příklad:

{

"code": 100,

"status": "error",

"errors": [

"error"

]

}

status je vždy error

Pokud je hodnota code \<= 100, pak se jedná o interní chybu (např. špatně použité API) a chyby v atributu errors jsou v plné textaci.

Pokud je hodnotacode \> 100, jedná se o uživatelskou chybu a v atributuerrors budou kódy z katalogu a případně parametry dle specifikace v kapitole 2.8.

  1.
# Indikace v komentářích Swagger

| **Zkratka** | Význam |
| --- | --- |
| INT | Interní atribut |
| **NYI** | Zatím není implementováno |

  1.
# Obecné

Pokud se v rámci popisu API hovoří o vrácení _všech_ záznamů (případně kompletním seznamu), tak se vždy jedná o kompletní seznam v rámci práv daného uživatele.

Doplňující tabulka v jednotlivých volání:

| **URL** | \<METODA\>http://\<host\>:\<port\>/\<cesta\> |
| --- | --- |
| Filtr | Seznam atributů, nad kterými lze filtrovat |
| **Řazení** | Seznam atributů, nad kterými lze řadit |
| **Fulltext** | Zda je možné použít query parametrsearch |
| **Katalog** | Seznam atributů, které obsahují hlášku z katalogu k lokalizaci |

  1.
# Interní poznámky

Interní poznámky, u kterých se neočekává zveřejnění:

- Call PUT /projects/{id}/parameters (kapitola 3.3.6) je docela komplexní a velmi spoléhá na znalost IoT business na counterů. Domnívám se, že možná v této podobě není ke zveřejnění pro někoho, kdo nezná aplikaci.
-

1.
# API

  1.
# Customers

    1.
# GET ​/customers

Kompletní seznam zákazníků.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/customers |
| --- | --- |
| Filtr | customerIdcustomerNameisResellerportalId |
| **Řazení** | customerIdcustomerNameisResellerportalId |
| **Fulltext** | Ano |
| **Katalog** |
 |

    1.
# GET /customers​/{id}

Informace o konkrétním zákazníkovi.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/customers/{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

    1.
# GET /customers​/{id}​/services

Vrátí seznam všech nasmlouvaných služeb zákazníka (včetně parametrů).

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/customers/{id}/services |
| --- | --- |
| Filtr | custServiceIdcustServiceNametarifIdtarifNamecustomerIdproductElementIdserviceActivationTimesuspendedsuspendTimeresumeTimeenableddeviceServiceIddiscontinueddiscontinuationTime |
| **Řazení** | custServiceIdcustServiceNametarifIdtarifNamecustomerIdproductElementIdserviceActivationTimesuspendedsuspendTimeresumeTimeenableddeviceServiceIddiscontinueddiscontinuationTime |
| **Fulltext** | Ano |
| **Katalog** | data.parameters.name |

    1.
# GET /customers​/{id}​/projects

Vrátí seznam všech projektů (včetně parametrů) daného zákazníka.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/customers/{id}/projects |
| --- | --- |
| Filtr | projectIdprojectNamecustomerIdsuspendedsuspendTimeresumeTimefreemium |
| **Řazení** | projectIdprojectNamecustomerIdsuspendedsuspendTimeresumeTimefreemium |
| **Fulltext** | Ano |
| **Katalog** | data.parameters.name |

  1.
# Services

    1.
# GET /services

Vrátí seznam všech služeb (včetně parametrů).

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/services |
| --- | --- |
| Filtr | custServiceIdcustServiceNametarifIdtarifNamecustomerIdproductElementIdserviceActivationTimesuspendedsuspendTimeresumeTimeenableddeviceServiceIddiscontinueddiscontinuationTime |
| **Řazení** | custServiceIdcustServiceNametarifIdtarifNamecustomerIdproductElementIdserviceActivationTimesuspendedsuspendTimeresumeTimeenableddeviceServiceIddiscontinueddiscontinuationTime |
| **Fulltext** | Ano |
| **Katalog** | data.parameters.name |

    1.
# GET ​/services​/{id}

Informace o konkrétní službě (včetně parametrů).

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/services/{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** | data.parameters.name |

    1.
# GET ​/services​/{id}​/counters

Stav counterů dané služby.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/services/{id}/counters |
| --- | --- |
| Filtr | counterIdnamevaluelimit |
| **Řazení** | counterIdnamevaluelimit |
| **Fulltext** | Ne |
| **Katalog** | data.name |

    1.
# GET ​/services​/{id}​/projects

Vrátí seznam všech projektů (včetně parametrů), které mají přiřazenu danou službu.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/services/{id}/projects |
| --- | --- |
| Filtr | projectIdprojectNamecustomerIdsuspendedsuspendTimeresumeTimefreemium |
| **Řazení** | projectIdprojectNamecustomerIdsuspendedsuspendTimeresumeTimefreemium |
| **Fulltext** | Ano |
| **Katalog** | data.parameters.name |

    1.
# POST ​/services​/{id}​/projects​/{projectId}​/assign

Přiřadí službu na projekt. Bez této akce nelze v rámci daného projektu čerpat danou službu a importovat na ni zařízení.

| **URL** | POSThttp://\<host\>:\<port\>/cxf/api/v1/services/{id}/projects/{projectId}/assign |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

    1.
# DELETE ​/services​/{id}​/projects​/{projectId}​/assign

Odebere službu z projektu. Nelze provést, pokud existují zařízení, která jsou na tuto službu přiřazena.

| **URL** | DELETEhttp://\<host\>:\<port\>/cxf/api/v1/services/{id}/projects/{projectId}/assign |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

    1.
# POST ​/services​/{id}​/devices​/{protocol}/{deviceId}​/assign

Migrace zařízení na novou službu v rámci stejného projektu a zákazníka. Projekt musí mít cílovou službu k dispozici.

| **URL** | POSThttp://\<host\>:\<port\>/cxf/api/v1/services/{id}/devices/{protocol}/{deviceId}/assign |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

  1.
# Projects

    1.
# GET ​/projects

Vrátí seznam všech projektů (včetně parametrů).

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/projects |
| --- | --- |
| Filtr | projectIdprojectNamecustomerIdsuspendedsuspendTimeresumeTimefreemium |
| **Řazení** | projectIdprojectNamecustomerIdsuspendedsuspendTimeresumeTimefreemium |
| **Fulltext** | Ano |
| **Katalog** | data.parameters.name |

    1.
# POST ​/projects

Založení nového projektu. Akce obvykle trvá déle (10-20s), protože je třeba provést např. založení databáze, atd.

| **URL** | POSThttp://\<host\>:\<port\>/cxf/api/v1/projects |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

    1.
# GET ​/projects​/{id}

Informace o projektu včetně parametrů.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/projects/{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** | data.parameters.name |

    1.
# PUT ​/projects​/{id}

Aktualizace atributů projektu.

| **URL** | PUThttp://\<host\>:\<port\>/cxf/api/v1/projects/{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

    1.
# DELETE ​/projects​/{id}

Zrušení projektu. Projekt nelze zrušit, pokud obsahuje některý z podřízených objektů, jako zařízení, endpoint, skupinu zařízení, atd.

| **URL** | DELETEhttp://\<host\>:\<port\>/cxf/api/v1/projects/{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

    1.
# PUT ​/projects​/{id}​/parameters

Editace parametrů projektu. Tato funkcionalita je dostupná pouze zákazníkům typu _Reseller_.

| **URL** | PUThttp://\<host\>:\<port\>/cxf/api/v1/projects/{id}/parameters |
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

    1.
# GET ​/projects​/{id}​/counters

Informace o konkrétní službě (včetně parametrů).

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/projects/{id}/counters |
| --- | --- |
| Filtr | counterIdnamevaluelimit |
| **Řazení** | counterIdnamevaluelimit |
| **Fulltext** | Ne |
| **Katalog** | name |

    1.
# GET ​/projects​/{id}​/services

Vrátí seznam všech služeb (včetně parametrů), které jsou přiřazeny projektu.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/projects/{id}/services |
| --- | --- |
| Filtr | custServiceIdcustServiceNametarifIdtarifNamecustomerIdproductElementIdserviceActivationTimesuspendedsuspendTimeresumeTimeenableddeviceServiceIddiscontinueddiscontinuationTime |
| **Řazení** | custServiceIdcustServiceNametarifIdtarifNamecustomerIdproductElementIdserviceActivationTimesuspendedsuspendTimeresumeTimeenableddeviceServiceIddiscontinueddiscontinuationTime |
| **Fulltext** | Ano |
| **Katalog** | data.parameters.name |

    1.
# GET ​/projects​/{id}​/endpoints​/overview

Analytický přehled o endpointech na projektu.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/projects/{id}/endpoint/overview |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

    1.
# GET ​/projects​/{id}​/devices​/overview

Vrátí analytický přehled o zařízeních na projektu.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/projects/{id}/devices/overview |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

    1.
# GET /projects/{id}/device-groups/overview

Vrátí analytický přehled skupin zařízení.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/projects/{id}/device-groups/overview |
| --- | --- |
| Filtr | deviceGroupIddeviceGroupNameenabledlastEnableTimelastDisableTime |
| **Řazení** | deviceGroupIddeviceGroupNameenabledlastEnableTimelastDisableTime |
| **Fulltext** | Ne |
| **Katalog** |
 |

  1.
# HTTP

    1.
# Endpoints

      1.
# GET /http​/endpoints

Vrátí seznam všech http endpointů (včetně parametrů, tagů, atributů a seznamu skupin, do kterých je přiřazen).

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/http/endpoints |
| --- | --- |
| Filtr | custDestIdprojectIdcustDestNamecustDestEnabledtransformationIdlastSuccessfulDeliveryfailedDeliveries |
| **Řazení** | custDestIdprojectIdcustDestNamecustDestEnabledtransformationIdlastSuccessfulDeliveryfailedDeliveries |
| **Fulltext** | Ano |
| **Katalog** |
 |

      1.
# POST ​/http​/endpoints

Založení http endpointu.

| **URL** | POSThttp://\<host\>:\<port\>/cxf/api/v1/http/endpoints |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# GET ​/http​/endpoints​/suggestions

Našeptávač k http endpointům.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/http/endpoints /suggestions |
| --- | --- |
| Filtr | projectId |
| **Řazení** |
 |
| **Fulltext** | Ano |
| **Katalog** |
 |

      1.
# GET ​/http​/endpoints​/{id}

Vrátí informace o http endpointu (včetně parametrů, tagů, atributů a seznamu skupin, do kterých je přiřazen).

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/http/endpoints ​/{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# PUT ​/http​/endpoints​/{id}

Aktualizace nastavení http endpointu.

| **URL** | PUThttp://\<host\>:\<port\>/cxf/api/v1/http/endpoints/​{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# DELETE ​/http​/endpoints​/{id}

Výmaz http endpointu. Nelze provést, pokud je endpoint přiřazen skupině zařízení.

| **URL** | DELETEhttp://\<host\>:\<port\>/cxf/api/v1/http/endpoints/​{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# GET ​/http​/endpoints​/{id}​/deliveries

Zobrazení doručení zpráv na endpoint.

Maximální rozpětí mezi query parametry from a to je 31 dní.

Parametr from je validován konstantou 2021-04-20 06:26 V případě požadavku před touto konstantou dojde k odpovědi s response code 303 a textem v body : „From is less than minimal 2021-04-20 06:26:00.000"

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/http​/endpoints​/{id}​/deliveries |
| --- | --- |
| Filtr | messageIdtransformationIdcodeerror |
| **Řazení** | messageIdtransformationIdrequestTime |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# GET ​/http​/endpoints​/{id}​/deliveries/full-detail

Zobrazení doručení zpráv na endpoint včetně obsahu zpráv a ID zařízení.

Maximální rozpětí mezi query parametry from a to je 31 dní.

Parametr from je validován konstantou 2021-04-20 06:26 V případě požadavku před touto konstantou dojde k odpovědi s response code 303 a textem v body : „From is less than minimal 2021-04-20 06:26:00.000"

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/http​/endpoints​/{id}​/deliveries/full-detail |
| --- | --- |
| Filtr | messageIdtransformationIdcodeerrorcustDeviceName |
| **Řazení** | messageIdtransformationIdrequestTime |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# POST ​/http​/endpoints​/{id}​/ping

Test http endpointu. Zašle požadavek dle specifikace a vrátí odpověď.

| **URL** | POSThttp://\<host\>:\<port\>/cxf/api/v1​/http​/endpoints​/{id}​/ping |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# [NYI] PUT ​/http​/endpoints​/{id}​/tags

Aktualizace tagů endpointu.

| **URL** | POSThttp://\<host\>:\<port\>/cxf/api/v1​/http​/endpoints​/{id}​/ping |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# [NYI] PUT ​/http​/endpoints​/{id}​/attributes

Aktualizace atributů endpointu.

| **URL** | POSThttp://\<host\>:\<port\>/cxf/api/v1​/http​/endpoints​/{id}​/ping |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

  1.
# MQTT

    1.
# Endpoints

      1.
# GET /mqtt​/gateways

Vrátí seznam všech mqtt gateways (včetně parametrů, tagů, atributů a seznamu skupin, do kterých je přiřazen).

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/mqtt/gateways |
| --- | --- |
| Filtr | custDestIdprojectIdcustDestNamecustDestEnabledtransformationIdlastSuccessfulDeliveryfailedDeliveries |
| **Řazení** | custDestIdprojectIdcustDestNamecustDestEnabledtransformationIdlastSuccessfulDeliveryfailedDeliveries |
| **Fulltext** | Ano |
| **Katalog** |
 |

      1.
# POST ​/mqtt​/gateways

Založení mqtt gateway.

| **URL** | POSThttp://\<host\>:\<port\>/cxf/api/v1/mqtt/ gateways |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# GET ​/mqtt​/gateways ​/suggestions

Našeptávač k mqtt gateways.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/mqtt/ gateways /suggestions |
| --- | --- |
| Filtr | projectId |
| **Řazení** |
 |
| **Fulltext** | Ano |
| **Katalog** |
 |

      1.
# GET ​/mqtt​/gateways ​/{id}

Vrátí informace o mqtt gateway (včetně parametrů, tagů, atributů a seznamu skupin, do kterých je přiřazen).

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/mqtt/ gateways ​/{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# PUT ​/mqtt​/gateways ​/{id}

Aktualizace nastavení mqtt gateway.

| **URL** | PUThttp://\<host\>:\<port\>/cxf/api/v1/mqtt/ gateways /​{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# DELETE ​/mqtt​/gateways ​/{id}

Výmaz mqtt gateway. Nelze provést, pokud je gatewaypřiřazena skupině zařízení.

| **URL** | DELETEhttp://\<host\>:\<port\>/cxf/api/v1/mqtt/ gateways /​{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# GET ​/mqtt​/gateways​/{id}​/deliveries

Zobrazení informací jednotlivých pokusech o doručení na gateway.

Maximální rozpětí mezi query parametry from a to je 31 dní.

Parametr from je validován konstantou 2021-04-20 06:26 V případě požadavku před touto konstantou dojde k odpovědi s response code 303 a textem v body : „From is less than minimal 2021-04-20 06:26:00.000"

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/mqtt​/ gateways ​/{id}​/deliveries |
| --- | --- |
| Filtr | messageIdtransformationIdcodeerror |
| **Řazení** | messageIdtransformationIdrequestTime |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# GET ​/mqtt​/gateways​/{id}​/deliveries/full-detail

Zobrazení informací jednotlivých pokusech o doručení na gateway, včetně obsahu zpráv a ID zařízení.

Maximální rozpětí mezi query parametry from a to je 31 dní.

Parametr from je validován konstantou 2021-04-20 06:26 V případě požadavku před touto konstantou dojde k odpovědi s response code 303 a textem v body : „From is less than minimal 2021-04-20 06:26:00.000"

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/mqtt​/ gateways ​/{id}​/deliveries/full-detail |
| --- | --- |
| Filtr | messageIdtransformationIdcodeerrorcustDeviceName |
| **Řazení** | messageIdtransformationIdrequestTime |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# [NYI] PUT ​/mqtt​/gateways​/{id}​/tags

Aktualizace tagů gateway.

| **URL** | POSThttp://\<host\>:\<port\>/cxf/api/v1​/mqtt​/ gateways ​/{id}​/ping |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# [NYI] PUT ​/mqtt​/gateways​/{id}​/attributes

Aktualizace atributů gateways.

| **URL** | POSThttp://\<host\>:\<port\>/cxf/api/v1​/mqtt​/endpoints​/{id}​/ping |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

  1.
# MQTT

    1.
# Devices

      1.
# GET ​/mqtt​/devices​/

Vrátí seznam všech mqtt zařízení (včetně tagů, atributů a seznamu skupin, do kterých jsou přiřazena).

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/mqtt​/devices​/ |
| --- | --- |
| Filtr | deviceIdcustDeviceNamecustServiceIdstatusenabledenableTimedisableTimesuspendedsuspendTimeresumeTimeprovisionTimecustomerIdprojectIdlastMessageInlastMessageOuttagsdeviceGroupId |
| **Řazení** | deviceIdcustDeviceNamecustServiceIdstatusenabledenableTimedisableTimesuspendedsuspendTimeresumeTimeprovisionTimecustomerIdprojectIdlastMessageInlastMessageOuttags |
| **Fulltext** | Ano |
| **Katalog** |
 |

      1.
# POST ​/mqtt​/devices​/

Import MQTT zařízení (lze importovat více než jedno zařízení najednou). Provádí se asynchronně. Pokud je základní validace úspěšná, je v odpovědi vráceno batchId, přes které se dá dotazovat na stav, viz kapitola 3.6.1.9.

Importní dávka musí obsahovat pouze jednu službu a projekt.

| **URL** | POSThttp://\<host\>:\<port\>/cxf/api/v1/mqtt​/devices​/ |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# GET ​/mqtt​/devices​/suggestions

Našeptávač pro MQTT zařízení.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/mqtt​/devices​/suggestions |
| --- | --- |
| Filtr | projectId |
| **Řazení** |
 |
| **Fulltext** | Ano |
| **Katalog** |
 |

      1.
# GET ​/mqtt​/devices​/{id}

Vrátí informace o mqtt zařízení (včetně tagů, atributů a seznamu skupin, do kterých je přiřazeno).

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/mqtt​/devices​/{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# PUT ​/mqtt​/devices​/{id}

Editace mqtt zařízení.

| **URL** | PUThttp://\<host\>:\<port\>/cxf/api/v1/mqtt​/devices​/{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# DELETE ​/mqtt​/devices​/{id}

Výmaz mqtt zařízení. Zařízení nelze vymazat, pokud je přiřazeno do skupiny zařízení.

| **URL** | DELETEhttp://\<host\>:\<port\>/cxf/api/v1/mqtt​/devices​/{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# PUT ​/mqtt​/devices​/{id}​/tags

Aktualizace tagů mqtt zařízení.

| **URL** | PUThttp://\<host\>:\<port\>/cxf/api/v1/mqtt​/devices​/{id}/tags |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# PUT ​/mqtt​/devices​/{id}​/attributes

Aktualizace atributů mqtt zařízení.

| **URL** | PUThttp://\<host\>:\<port\>/cxf/api/v1/mqtt​/devices​/{id}/attributes |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# GET ​/mqtt​/devices​/import​/{id}

Zjištění stavu importu zařízení.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/mqtt​/devices/import​/{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** | errors.errorMessage |

      1.
# GET ​/mqtt​/devices​/{id}​/counters

Výpis stavu counterů na zařízení.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/mqtt​/devices /counters |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** | name |

      1.
# POST ​/mqtt​/devices​/{id}​/enable

Povolení zařízení (implicitní stav). Zprávy z takového zařízení jsou přijímány na platformu a jsou doručovány.

| **URL** | POSThttp://\<host\>:\<port\>/cxf/api/v1/mqtt​/devices​/{id}​/enable |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# DELETE ​/mqtt​/devices​/{id}​/enable

Pozastavení zařízení. Zprávy z takového zařízení jsou přijímány na platformu, ale nejsou doručovány.

| **URL** | DELETEhttp://\<host\>:\<port\>/cxf/api/v1/mqtt​/devices​/{id}​/enable |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# GET ​/mqtt​/devices​/{id}​/down​/messages

Zobrazení zpráv odeslaných na zařízení.

Maximální rozpětí mezi query parametry from a to je 31 dní.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/mqtt​/devices​/{id}​/down​/messages |
| --- | --- |
| Filtr | data |
| **Řazení** | messageTime |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# POST ​/mqtt​/devices​/{id}​/down​/messages

Odeslání zprávy na MQTT zařízení.

| **URL** | POSThttp://\<host\>:\<port\>/cxf/api/v1/mqtt​/devices​/{id}​/down​/messages |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# GET /mqtt/devices/{id}/up/messages

Výpis zpráv z MQTT zařízení.

Maximální rozpětí mezi query parametry from a to je 31 dní.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/mqtt​/devices​/{id}​/up​/messages |
| --- | --- |
| Filtr | data |
| **Řazení** | messageTime |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# GET ​/mqtt​/devices​/{id}​/up​/messages/{messageId}/deliveries

Výpis doručení zprávy na endpointy.

Parametr messageId je validován konstantou 2021-04-20 06:26 V případě požadavku před touto konstantou dojde k odpovědi s response code 303 a textem v body : „MessageId datetime is less than minimal 2021-04-20 06:26:00.000"

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/mqtt​/devices​/{id}​/up​/messages/{messageId}/deliveries |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# GET /mqtt​/devices​/{id}​/down​/messages/stats

Denní statistika zpráv odeslaných na MQTT zařízení.

Maximální rozpětí mezi query parametry from a to je 31 dní.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/mqtt​/devices​/{id}​/down​/messages/stats |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# GET ​/mqtt​/devices​/{id}​/up​/messages/stats

Denní statistika zpráv z MQTT zařízení. Jedná se o kompletní počty, tj. včetně zpráv, které byly přijaty, ale nebyly doručeny z důvodu překročení limitu.

Maximální rozpětí mezi query parametry from a to je 31 dní.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/mqtt​/devices​/{id}​/up​/messages/stats |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

  1.
# LoRa

    1.
# Devices

      1.
# GET ​/lora​/devices​/

Vrátí seznam všech lora zařízení (včetně tagů, atributů a seznamu skupin, do kterých jsou přiřazena).

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/lora​/devices​/ |
| --- | --- |
| Filtr | deviceIdcustDeviceNamecustServiceIdstatusenabledenableTimedisableTimesuspendedsuspendTimeresumeTimeprovisionTimecustomerIdprojectIdlastMessageInlastMessageOuttagssignalStrengthbateryStatusdeviceTypedeviceGroupIddeviceStatus |
| **Řazení** | deviceIdcustDeviceNamecustServiceIdenabledenableTimedisableTimestatussuspendedsuspendTimeresumeTimeprovisionTimecustomerIdprojectIdlastMessageInlastMessageOuttagssignalStrengthbateryStatusdeviceTypedeviceStatus |
| **Fulltext** | Ano |
| **Katalog** |
 |

      1.
# GET ​/lora/devices​/suggestions

Našeptávač pro lora zařízení.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/lora/devices​/suggestions |
| --- | --- |
| Filtr | projectId |
| **Řazení** |
 |
| **Fulltext** | Ano |
| **Katalog** |
 |

      1.
# POST /lora​/devices​/abp​/csv

Hromadný import ABP zařízení z CSV souboru (definice dle dokumentace). Provádí se asynchronně. Pokud je základní validace úspěšná, je v odpovědi vráceno batchId, přes které se dá dotazovat na stav, viz kapitola 3.7.1.12.

Importní dávka musí obsahovat pouze jednu službu a projekt.

| **URL** | POSThttp://\<host\>:\<port\>/cxf/api/v1/lora​/devices​/abp​/csv |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# POST /lora​/devices​/otaa​/csv

Hromadný import OTAA zařízení z CSV souboru (definice dle dokumentace). Provádí se asynchronně. Pokud je základní validace úspěšná, je v odpovědi vráceno batchId, přes které se dá dotazovat na stav, viz kapitola 3.7.1.12.

Importní dávka musí obsahovat pouze jednu službu a projekt.

| **URL** | POSThttp://\<host\>:\<port\>/cxf/api/v1/lora​/devices​/otaa​/csv |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# POST /lora​/devices​/abp

Hromadný import ABP zařízení. Provádí se asynchronně. Pokud je základní validace úspěšná, je v odpovědi vráceno batchId, přes které se dá dotazovat na stav, viz kapitola 3.7.1.12.

Importní dávka musí obsahovat pouze jednu službu a projekt.

| **URL** | POSThttp://\<host\>:\<port\>/cxf/api/v1/lora​/devices​/abp​ |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# POST /lora​/devices​/otaa

Hromadný import OTAA zařízení. Provádí se asynchronně. Pokud je základní validace úspěšná, je v odpovědi vráceno batchId, přes které se dá dotazovat na stav, viz kapitola 3.7.1.12.

Importní dávka musí obsahovat pouze jednu službu a projekt.

| **URL** | POSThttp://\<host\>:\<port\>/cxf/api/v1/lora​/devices​/otaa​ |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# GET ​/lora​/devices​/{id}

Vrátí informace o lora zařízení (včetně tagů, atributů a seznamu skupin, do kterých je přiřazeno).

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/lora​/devices​/{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# PUT ​/lora​/devices​/{id}

Editace lora zařízení.

| **URL** | PUThttp://\<host\>:\<port\>/cxf/api/v1/lora​/devices​/{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# DELETE ​/lora​/devices​/{id}

Výmaz lora zařízení. Zařízení nelze vymazat, pokud je přiřazeno do skupiny zařízení.

| **URL** | DELETEhttp://\<host\>:\<port\>/cxf/api/v1/lora​/devices​/{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# PUT ​/lora​/devices​/{id}​/tags

Aktualizace tagů lora zařízení.

| **URL** | PUThttp://\<host\>:\<port\>/cxf/api/v1/lora​/devices​/{id}/tags |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# PUT ​/lora/devices​/{id}​/attributes

Aktualizace atributů lora zařízení.

| **URL** | PUThttp://\<host\>:\<port\>/cxf/api/v1/lora/devices​/{id}/attributes |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# GET ​/lora​/devices​/import​/{id}

Zjištění stavu importu zařízení.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/lora​/devices/import​/{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** | errors.errorMessage |

      1.
# GET ​/lora/devices​/{id}​/counters

Výpis stavu counterů na zařízení.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/lora​/devices /counters |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** | name |

      1.
# POST ​/lora​/devices​/{id}​/enable

Povolení zařízení (implicitní stav). Zprávy z takového zařízení jsou přijímány na platformu a jsou doručovány.

| **URL** | POSThttp://\<host\>:\<port\>/cxf/api/v1/mqtt​/devices​/{id}​/enable |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# DELETE ​/lora​/devices​/{id}​/enable

Pozastavení zařízení. Zprávy z takového zařízení jsou přijímány na platformu, ale nejsou doručovány.

| **URL** | DELETEhttp://\<host\>:\<port\>/cxf/api/v1/lora​/devices​/{id}​/enable |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# GET ​/lora​/devices​/{id}​/down​/messages

Zobrazení zpráv odeslaných na zařízení.

Maximální rozpětí mezi query parametry from a to je 31 dní.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/lora​/devices​/{id}​/down​/messages |
| --- | --- |
| Filtr | data |
| **Řazení** | messageTime |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# POST ​/lora/devices​/{id}​/down​/messages

Odeslání zprávy na lora zařízení.

| **URL** | POSThttp://\<host\>:\<port\>/cxf/api/v1/lora​/devices​/{id}​/down​/messages |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# GET ​/lora​/devices​/{id}​/up​/messages

Výpis zpráv z lora zařízení.

Maximální rozpětí mezi query parametry from a to je 31 dní.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/lora/devices​/{id}​/up​/messages |
| --- | --- |
| Filtr | dataid |
| **Řazení** | messageTimeid |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# GET ​/lora​/devices​/{id}​/up​/messages/{messageId}/deliveries

Výpis doručení zprávy na endpointy.

Parametr messageId je validován konstantou 2021-04-20 06:26 V případě požadavku před touto konstantou dojde k odpovědi s response code 303 a textem v body : „MessageId datetime is less than minimal 2021-04-20 06:26:00.000"

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/lora​/devices​/{id}​/up​/messages/{messageId}/deliveries |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# ​POST /lora/signal/{id}

Zjištění síly signálu dle souřadnic a typu zařízení.

| **URL** | POSThttp://\<host\>:\<port\>/cxf/api/v1/lora/signal/{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# GET /lora/devices​/{id}​/down​/messages/stats

Denní statistika zpráv odeslaných na LoRa zařízení.

Maximální rozpětí mezi query parametry from a to je 31 dní.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/lora​/devices​/{id}​/down​/messages/stats |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

      1.
# ​GET lora/devices​/{id}​/up​/messages/stats

Denní statistika zpráv z LoRa zařízení. Jedná se o kompletní počty, tj. včetně zpráv, které byly přijaty, ale nebyly doručeny z důvodu překročení limitu.

Maximální rozpětí mezi query parametry from a to je 31 dní.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/lora​/devices​/{id}​/up​/messages/stats |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# 3.7.1.23. PUT /lora/devices/{id}/parameters

Aktualizace parametrů lora zařízení.

| **URL** | PUThttp://\<host\>:\<port\>/cxf/api/v1/lora/devices​/{id}/parameters |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

# 3.7.1.24. POST /lora/devices/{id}/activate

Aktivace LoRa zařízení z prekativního stavu

| **URL** | PUThttp://\<host\>:\<port\>/cxf/api/v1/lora/devices​/{id}/activate |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

  1.
# Device Groups

    1.
# GET ​/device-groups

Vrátí seznam všech skupin zařízení (včetně tagů a atributů).

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/device-groups |
| --- | --- |
| Filtr | deviceGroupIdprojectIddeviceGroupNameenabledlastEnableTimelastDisableTime |
| **Řazení** | deviceGroupIdprojectIddeviceGroupNameenabledlastEnableTimelastDisableTime |
| **Fulltext** | Ano |
| **Katalog** |
 |

    1.
# POST ​/device-groups

Založení skupiny zařízení

| **URL** | POSThttp://\<host\>:\<port\>/cxf/api/v1/device-groups |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

    1.
# GET ​/device-groups​/suggestions

Našeptávač pro skupiny zařízení.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/device-groups​/suggestions |
| --- | --- |
| Filtr | projectId |
| **Řazení** |
 |
| **Fulltext** | Ano |
| **Katalog** |
 |

    1.
# GET ​/device-groups​/{id}

Vrátí informace o skupině zařízení (včetně tagů a atributů).

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/device-groups​/{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

    1.
# PUT ​/device-groups​/{id}

Editace skupiny zařízení.

| **URL** | PUThttp://\<host\>:\<port\>/cxf/api/v1/device-groups​/{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

    1.
# DELETE ​/device-groups​/{id}

Výmaz skupiny zařízení. Skupinu nelze vymazat, pokud je k ní přiřazeny endpointy nebo zařízení.

| **URL** | DELETEhttp://\<host\>:\<port\>/cxf/api/v1/device-groups​/{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

    1.
# [NYI] PUT ​/device-groups​/{id}​/tags

Aktualizace tagů skupiny zařízení.

| **URL** | PUThttp://\<host\>:\<port\>/cxf/api/v1/device-groups​/{id}​/tags |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

    1.
# [NYI] PUT /device-groups​/{id}​/attributes

Aktualizace atributů skupiny zařízení.

| **URL** | PUThttp://\<host\>:\<port\>/cxf/api/v1/device-groups​/{id}​/attributes |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

    1.
# GET ​/device-groups​/devices

Výpis zjednodušeného seznamu zařízení přiřazených ke skupině. Pro detail k zařízení je třeba provést extra dotaz.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/device-groups​/devices |
| --- | --- |
| Filtr | deviceIddeviceProtocolprojectIdcustDeviceName |
| **Řazení** | deviceIddeviceProtocolprojectIdcustDeviceName |
| **Fulltext** | Ano |
| **Katalog** |
 |

    1.
# GET ​/device-groups​/endpoints

Výpis zjednodušeného seznamu endpointů přiřazených ke skupině. Pro detail k endpontu je třeba provést extra dotaz.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/device-groups​/endpoints |
| --- | --- |
| Filtr | custDestIdprojectIdcustDestNamecustDestType |
| **Řazení** | custDestIdprojectIdcustDestNamecustDestType |
| **Fulltext** | Ano |
| **Katalog** |
 |

    1.
# POST ​/device-groups​/{id}​/devices/{protocol} ​/{deviceId}​/assign

Přiřazení zařízení skupině zařízení. Povolené hodnoty atributu protocol jsou _lora_ a _mqtt._

| **URL** | POSThttp://\<host\>:\<port\>/cxf/api/v1/device-groups​/{id}​/devices/{protocol} /{deviceId}​/assign |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

    1.
# DELETE ​/device-groups​/{id}​/devices​/{protocol}/{deviceId}​/assign

Odebrání zařízení ze skupiny. Povolené hodnoty atributu protocol jsou _lora_ a _mqtt._

| **URL** | DELETEhttp://\<host\>:\<port\>/cxf/api/v1/device-groups​/{id}​/devices​/{protocol} /{deviceId}​/assign |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

    1.
# POST ​/device-groups​/{id}​/endpoints​/{endpointId}​/assign

Přiřazení endpointu skupině zařízení.

| **URL** | POSThttp://\<host\>:\<port\>/cxf/api/v1/device-groups​/{id}​/endpoints​/{endpointId}​/assign |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

    1.
# DELETE ​/device-groups​/{id}​/endpoints​/{endpointId}​/assign

Odebrání endpointu ze skupiny.

| **URL** | DELETEhttp://\<host\>:\<port\>/cxf/api/v1​/device-groups​/{id}​/endpoints​/{endpointId}​/assign |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

  1.
# Users

    1.
# GET ​/users

Vrátí seznam všech uživatelů (včetně práv a parametrů).

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/users |
| --- | --- |
| Filtr | userIdfirstNamelastNamephoneemailcustomerIdprojectId |
| **Řazení** | userIdfirstNamelastNamephoneemail |
| **Fulltext** | Ano |
| **Katalog** |
 |

    1.
# GET ​/users​/suggestions

Našeptávač pro uživatele.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1​/users​/suggestions |
| --- | --- |
| Filtr | customerId |
| **Řazení** |
 |
| **Fulltext** | Ano |
| **Katalog** |
 |

    1.
# GET ​/users​/{id}

Informace o uživateli (včetně práv a parametrů).

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/users/{id} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

    1.
# PUT ​/users​/{id}​

Aktualizace uživatelských preferencí.

| **URL** | PUThttp://\<host\>:\<port\>/cxf/api/v1/users​/{id}​ |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

    1.
# PUT ​/users​/{id}​/customers​/{customerId}​/projects​/{projectId}​/privileges

Přiřazení, případně odebrání práva uživatele k danému projektu.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/users​/{id}​/customers​/{customerId}​/projects​/{projectId}​/privileges |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

  1.
# Notifications

    1.
# GET ​/notifications

Načtení nastavení notifikací uživatelů.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/notifications |
| --- | --- |
| Filtr | emailcustomeId |
| **Řazení** | emailcustomeId |
| **Fulltext** | Ano |
| **Katalog** |
 |

    1.
# GET ​/notifications​/customers​/{customerId}

Načtení nastavení notifikací uživatele.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1 /notifications​/customers​/{customerId} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

    1.
# [NYI] GET ​/notifications​/customers​/{customerId}​/sent

Načtení odeslaných notifikací uživatele.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1 /notifications​/customers​/{customerId}​/sent |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ano |
| **Katalog** |
 |

    1.
# GET ​/notifications​/customers​/{customerId}​/emails

Načtení nastavení notifikací neuživatelských emailů.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/notifications​/customers​/{customerId}​/emails |
| --- | --- |
| Filtr | email |
| **Řazení** | email |
| **Fulltext** | Ano |
| **Katalog** |
 |

    1.
# POST /notifications​/customers​/{customerId}​/emails

Registrace notifikačního emailu.

| **URL** | POSThttp://\<host\>:\<port\>/cxf/api/v1/notifications​/customers​/{customerId}​/emails |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

    1.
# GET ​/notifications​/customers​/{customerId}​/emails​/{email}

Načtení nastavení notifikací neuživatelského emailu.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1 ​/notifications​/customers​/{customerId}​/emails​/{email} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

    1.
# DELETE ​/notifications​/customers​/{customerId}​/emails​/{email}

Odregistrace notifikačního emailu.

| **URL** | DELETEhttp://\<host\>:\<port\>/cxf/api/v1/notifications​/customers​/{customerId}​/emails |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

    1.
# [NYI] GET ​/notifications​/customers​/{customerId}​/emails​/{email}​/sent

Načtení odeslaných notifikací neuživatelského emailu.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/notifications​/customers​/{customerId}​/emails​/{email}​/sent |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ano |
| **Katalog** |
 |

    1.
# PATCH ​/notifications​/customers​/{customerId}​/templates​/{template}

Úprava nastavení notifikací uživatele.

| **URL** | PATCHhttp://\<host\>:\<port\>/cxf/api/v1 /notifications​/customers​/{customerId}​/templates​/{template} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

    1.
# PATCH ​/notifications​/customers​/{customerId}​/templates​/{template}​/emails​/{email}

Úprava nastavení notifikací neuživatelského emailu.

| **URL** | PATCHhttp://\<host\>:\<port\>/cxf/api/v1/notifications​/customers​/{customerId}​/templates​/{template}​/emails​/{email} |
| --- | --- |
| Filtr |
 |
| **Řazení** |
 |
| **Fulltext** | Ne |
| **Katalog** |
 |

  1.
# Audits

    1.
# GET /audits

Zobrazení kompletního auditního logu.

parameters obsahuje páry klíč hodnota dle placeholderů v textu dané katalogové hlášky. Tyto jsou standardně označeny postfixem a prefixem %.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/audits |
| --- | --- |
| Filtr | customerIdprojectIdcodeleveltimestamporiginatorsource |
| **Řazení** | customerIdprojectIdcodeleveltimestamporiginatorsource |
| **Fulltext** | Ano |
| **Katalog** | code |

    1.
# GET ​/audits​/customers​/{customerId}

Zobrazení auditního logu zákazníka.

parameters obsahuje páry klíč hodnota dle placeholderů v textu dané katalogové hlášky. Tyto jsou standardně označeny postfixem a prefixem %.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/audits​/customers​/{customerId} |
| --- | --- |
| Filtr | customerIdprojectIdcodeleveltimespamporiginatorsource |
| **Řazení** | customerIdprojectIdcodeleveltimespamporiginatorsource |
| **Fulltext** | Ano |
| **Katalog** | code |

    1.
# GET ​/audits​/projects​/{projectId}

Zobrazení auditního logu projektu.

parameters obsahuje páry klíč hodnota dle placeholderů v textu dané katalogové hlášky. Tyto jsou standardně označeny postfixem a prefixem %.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/audits​/projects​/{projectId} |
| --- | --- |
| Filtr | customerIdprojectIdcodeleveltimestamporiginatorsource |
| **Řazení** | customerIdprojectIdcodeleveltimestamporiginatorsource |
| **Fulltext** | Ano |
| **Katalog** | code |

    1.
# [NYI] GET ​/audits​/devices​/{protocol}/{deviceId}

Zobrazení auditního logu zařízení.

parameters obsahuje páry klíč hodnota dle placeholderů v textu dané katalogové hlášky. Tyto jsou standardně označeny postfixem a prefixem %.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/audits​/devices​/{protocol}/{deviceId} |
| --- | --- |
| Filtr | customerIdprojectIdcodeleveltimespamporiginatorsource |
| **Řazení** | customerIdprojectIdcodeleveltimespamporiginatorsource |
| **Fulltext** | Ano |
| **Katalog** | code |

    1.
# [NYI] GET ​/audits​/device-groups​/{groupId}

Zobrazení auditního logu skupiny zařízení.

parameters obsahuje páry klíč hodnota dle placeholderů v textu dané katalogové hlášky. Tyto jsou standardně označeny postfixem a prefixem %.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/audits​/device-groups​/{groupId} |
| --- | --- |
| Filtr | customerIdprojectIdcodeleveltimespamporiginatorsource |
| **Řazení** | customerIdprojectIdcodeleveltimespamporiginatorsource |
| **Fulltext** | Ano |
| **Katalog** | code |

  1.
# Tags

# 3.12.1 GET /tags/devices

Načtení tagu zařízení

Kompletní seznam tagů.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/tags/devices |
| --- | --- |
| Filtr | customerIdprojectIddeviceIdtag |
| **Řazení** | tag |
| **Fulltext** | Ano |
| **Katalog** |
 |

# 3.13 Attributes

# 3.13.1 GET /attributes/devices

Načtení atributů zařízení

Kompletní seznam atributů.

| **URL** | GEThttp://\<host\>:\<port\>/cxf/api/v1/tags/devices |
| --- | --- |
| Filtr | customerIdprojectIddeviceIdattributevalue |
| **Řazení** | attribute |
| **Fulltext** | Ano |
| **Katalog** |
 |
```