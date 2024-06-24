# Release 2024-07

## Seznam změn

Payload odesílaný na zákaznické endpointy bude nově uprave následujícím způsobem

* **bat** - stav baterie měl být odebrán (resp. konstanta 255) pro zvýšení výdrže baterie (byla vyčítána MAC příkazem na denní bázi), ale nakonec se nám podařilo zajistit volbu na úrovni zařízení, kde si můžete definovat frekvenci vyčítání v rozmezí: vypnuto, denně, týdně, měsíčně.
* **seqno** - nově bude odstraněn
* **toa** - nově bude odstraněn
* gws - informace o bránách (gateways), které zprávu zachytily
  * **gws.lat** - nově bude odstraněn
  * **gws.lon** - nově bude odstraněn
  * **gws.ts** - nově bude odstraněn
  * **gws.time** - nově bude odstraněn
  * **gws.tmms** - nově bude odstraněn
