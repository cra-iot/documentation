# Doručování zpráv na HTTP "Endpoint"

Jde o metodu známou jako Webhook. V naší IoT platformě ji nazýváme už historicky "Výstypy/HTTP endpoint"

Takový endpoint si můžete vyrobit jakýmikoliv programovacími prostředky, případně již použít existující na nějakém hotovém softwaru.

Naše platforma odesílá zprávy z IP adresy: 82.99.180.180. Tato IP adresa se 16.1.2024 změní na 84.244.71.160, protože přejdeme na modernější verzi, která je umístěna v jiné síťové zóně. 

Odchozí zpráva je zapouzdřena do integrační obálky. Vše je předáváno v těle HTTP požadavku jako JSON řetězec.

Atribut	Datový typ	Popis
type	STRING	Identifikuje typ integračního rámci. Pro příchozí zprávy platí hodnota „D“.
data	STRING	Datová zpráva
tech	STRING	Technologie použitá pro přenos dat. Pro LoRa bude rovna „L“
