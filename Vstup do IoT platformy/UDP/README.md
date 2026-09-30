# UDP příjem

## Podporované formáty

* [CRa protocol](CRa_protocol/version_1_0.md)

## Kam zprávy posílat

Produkční UDP rozhraní platformy je dostupné na adrese `udp.iot.cra.cz`, na portu podle tabulky níže.

Vždy používejte doménové jméno, nikoliv IP adresu — ta se může bez ohlášení změnit.

## Tabulka portů

* aby platforma mohla rozpoznat jaká data jsou posílána přes UDP je třeba je posílat na konkrétní porty ve správném formátu

| Port | Format                     |
|------|----------------------------|
| 5003 | CRA Protocol - version 1.0 |
