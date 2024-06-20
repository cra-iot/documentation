# Release 2024-07

## Seznam změn

Payload odesílaný na zákaznické endpointy bude nově uprave následujícím způsobem

* **bat** - nově bude obsahovat hodnotu **255**. LoRaWAN standardně nepodporuje stav baterie. Ten je podle konkrétního čidla obsažen v payloadu. Plánujeme umožnění volby frekvence zjišťování stavu baterie MAC příkazem v rozmezí: denně, týdně, měsíčně.
* **seqno** - nově bude odstraněn
* **toa** - nově bude odstraněn
* gws - informace o bránách (gateways), které zprávu zachytily
  * **gws.lat** - nově bude odstraněn
  * **gws.lon** - nově bude odstraněn
  * **gws.ts** - nově bude odstraněn
  * **gws.time** - nově bude odstraněn
  * **gws.tmms** - nově bude odstraněn
