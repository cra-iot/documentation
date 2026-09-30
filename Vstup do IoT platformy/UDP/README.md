# UDP příjem

## Podporované formáty

* [CRa protocol](CRa_protocol/version_1_0.md)

## Kam zprávy posílat

Produkční UDP rozhraní platformy je dostupné na adrese `udp.iot.cra.cz`, na portu podle tabulky níže.

Vždy používejte doménové jméno, nikoliv IP adresu — ta se může bez ohlášení změnit.

## Tabulka portů

* aby platforma mohla rozpoznat jaká data jsou posílána přes UDP je třeba je posílat na konkrétní porty ve správném formátu

| Port | Výrobce  | Model            | Poznámka                                                                                                                           |
|------|----------|------------------|------------------------------------------------------------------------------------------------------------------------------------|
| 5001 | CRA      | Electric-Meter   | SW senzor pro testování UDP příjmu                                                                                                 |
| 5002 | Prodomy  | Retran Unit      | koncentrátor M-Bus                                                                                                                 |
| 5003 | Acrios   | ACR-CV-101N-I4-D | formát [CRA Protocol 1.0](CRa_protocol/version_1_0.md), [ukázka Lua kódu](../../Zařízení/Dle%20výrobce/Acrios/acr_cv_101n_i4_d.md) |
| 5004 | Elgas    | ELCORplus        | transformace aktuálně není podporována                                                                                             |
| 5005 | Acrios   | ACR-EX           | převodník impulzního výstupu na NB-IoT                                                                                             |
| 5010 | Sagemcom | WM20-NB8-20      | vodoměr                                                                                                                            |
| 5555 | Other    | Other UDP        | záložní port, pokud zpráva neodpovídá žádnému jinému portu                                                                         |
