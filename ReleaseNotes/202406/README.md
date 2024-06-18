# Release 2024-06

## Seznam změn

- změny ve formátu zprávy z čidla

### Popis změn ve formátu zprávy z čidla

* **seqno** - nově bude vždy **null**
* **bat** - nově bude vždy s hodnotou **255**. LoRaWAN standardně nepodporuje stav baterie. Ten je podle konkrétního čidla obsažen v payloadu.
* **toa** - nově bude vždy s hodnotou **null**
* gws - informace o bránách(gateways), které zprávu zachytily
  * **gws.lat** - nově bude mít vždy hodnotu **0.0**
  * **gws.lon** - nově bude mít vždy hodnotu **0.0**
  * **gws.ts** - TBD
  * **gws.time** - TBD
  * **gws.tmms** - TBD
