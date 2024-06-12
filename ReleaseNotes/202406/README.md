# Release 202406

## Seznam změn

- [změna formátu zprávy](#změna formátu zprávy)

### změna formátu zprávy

* seqno – bude nově null, ostatní operátoři takovou hodnotu nemají. Globální číslo zprávy je vlastně jen v čase generované číslo CRA network serverem a není v LoRaWAN stadnardnu nijak podpořeno.
* bat – nebude nově 255. LoRaWAN standardně nepodporuje stav baterie. Ten je případně obsažen v payloadu. Ukončením zjišťování stavu (bylo 1x denně) bude zvýšena výdrž baterie. 
* toa - nebude nově null, ostatní operátoři takovou hodnotu nemají.
* gws - informace o GW, které zprávu zachytily, bude nově obsahovat jen atributy: gweui, rssi, snr, ant. Atributy: ts, time, lat a lon již nebudou obsaženy. Ostatní operátoři tyto informace neposkytují. 
