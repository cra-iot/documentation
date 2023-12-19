# Výstupy z IoT platformy
Výstupem se myslí to, jak lze z IoT platformy získat zprávy přijaté z IoT čidel.

CRA IoT platforma podporuje tyto metody:
- vyčítání přes [REST API](REST/README.md) (popis bude doplněn později)
- doručování na [http Endpoint](HTTP/README.md) zákazníka, či do jiné aplikace (tedy webhook) (popis bude doplněn později)
- vyčítání z [MQTT gateway](MQTT%20gateway/README.md), tj. subscribe z našeho brokeru

Plánujeme ještě:
- doručováno do cizího MQTT brokeru
- notifikace Email, SMS, Slack, Teams atp.
