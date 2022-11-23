# LoRaWAN Geolokace

CRA vám od konce roku 2022 poskytuje geolokační funkcionalitu u LoRaWAN zařízení.

Geolokace v LoRaWAN je metoda určování polohy koncových zařízení (čidel) využitím metadat ze sítě, bez nutnosti použití GPS chipsetu, a bez dalších úprav na straně koncových zařízení. 

Geolokaci lze určit pomocí dvou metod:
• RSSI – určování polohy pomocí síly signálů přijatých z koncových zařízení na daných GW
• TDoA – určování polohy dle přesných časových značek, vytvořených na jednotlivých GW

TDoA metoda vyžaduje v dosahu dostatečné množství IoT GW, poskytujích časové značky pro LoRaWAN zprávy.

Každá LoRaWAN zpráva generuje geolokační zprávu. Ty lze získat také přes rozhraní [API](API.md).