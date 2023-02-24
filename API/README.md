# API pro CRA IoT platformu

CRA pro vás začátkem roku 2021 vystavilo nové API, společně s novým portálem.

Nové API využívá dvoufázovou autentizaci, ve spolupráci s naším centrálním SSO.

Swagger dokumentace k API je umístěna zde:
https://app.swaggerhub.com/apis-docs/cra-iot/GUI/

Informace, které se do Swagger nevešly, najdete v tomto článku: [API dokumentace](API_specification.md)

Každý endpoint očekává v hlavičce Authorization: Bearer $access_token
(pozor, velikost písmen hraje roli)

"access_token" získáte požadavkem na naši SSO platformu takto:

  POST 'https://sso.cra.cz/auth/realms/CRA/protocol/openid-connect/token' \
  --header 'Content-Type: application/x-www-form-urlencoded' \
  --data-urlencode 'username=<< email >>' \
  --data-urlencode 'password=<< heslo >>' \
  --data-urlencode 'grant_type=password' \
  --data-urlencode 'client_id=iot-api-client' \
  --data-urlencode 'client_secret=41a113b7-5486-45e3-8a3d-e0b106a5d446'

client_secret je pro všechny uživatele stejný, souvisí s client_id.
Je tedy potřeba jen nahradit váš email a heslo.

Detailní popis autentizačního API najdete zde: 
https://access.redhat.com/documentation/en-us/red_hat_single_sign-on/7.2/html/api_documentation/index

Následné API requesty mají hlavní URI: https://api.iot.cra.cz/cxf/api/v1/

Tj. dotaz na získání informací na jaké máte přístup zákazníky je takto:
GET 'https://api.iot.cra.cz/cxf/api/v1/customers' \\
--header 'Authorization: Bearer << access token >>'

Pro ty z vás, kteří používají starší API, je jeho popis dostupný zde:
https://app.swaggerhub.com/apis-docs/cra-iot/craiot
ale pozor, toto API bude v do léta 2023 vypnuto!!!
