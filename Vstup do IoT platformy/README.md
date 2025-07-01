# Vstupy do IoT platformy
Vstupem se rozumí rozhraní, ze kterého platforma přijímá zprávy z IoT čidel (zařízení).

CRA IoT platforma původně vznikla za účelem příjmu LoRaWAN zpráv z našeho LNS (LoRaWAN Network Serveru). Postupem času jsme přidali MQTT rozhraní. Od roku 2023 podporujeme i HTTP a UDP protokoly. U HTTP a UDP je poměrně různorodé užití, proto je potřeba pro každou rodinu vytvořit speciální podporu. 

Více najdete v detailním popisu pro každý typ rozhraní:
- [LoRaWAN](LoRaWAN/README.md) - bude popsáno později
- [MQTT](MQTT/README.md)
- [HTTP](HTTP/README.md) - bude popsáno později
- [UDP](UDP/README.md)
