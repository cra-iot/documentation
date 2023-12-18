# MQTT příjem

CRA platforma podporuje dva druhy způsoby MQTT komunikace:
- [MQTT zařízení](## MQTT zařízení)
- [MQTT gateway](## MQTT gateway)

## MQTT zařízení
Do CRA IoT platformy lze posílat IoT zprávy také přes MQTT protokol. V tomto případě je potřeba založit MQTT zařízení.

## MQTT gateway


Pokud chcete poslat zprávu do MQTT zařízení z IoT platformy (musí být připojeno přes MQTT protokol a poslouchat "příkazy" pomoci subscribe), pak můžete zprávu poslat buď z GUI přes "Poslat zprávu" (v detailu MQTT zařízení) (NYI - zatím není v GUI) nebo přes API (https://app.swaggerhub.com/apis-docs/cra-iot/GUI/1.0.40#/MQTT%20Devices/post_mqtt_devices__id__down_messages), případně přes MQTT gateway.

Jednou z možností je např. poslat downlink zprávu přes REST API, nebo uložit zprávu do MQTT topicu v MQTT gateway.
