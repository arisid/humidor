# AI Smart Humidor
This project features an AI smart humidor built using CPU heatsinks and a Peltier element installed in an XPS box, controlled by ESPHome at ESP32-S3 with OV2640 for AI functions powered by ATX power supply and used Home Assistant to manage the operational logic.

Projektový popis (CZ)
AI Smart Humidor je inteligentní chladicí box s kapacitou pro dvě láhve vína, zkonstruovaný z izolačních XPS desek. Systém využívá Peltierův článek v kombinaci s aktivními CPU chladiči pro efektivní tepelný management. Mozkem zařízení je mikrokontroler ESP32-S3 (GOOUUU V1.3), který monitoruje vnitřní teplotu pomocí precizního senzoru DS18B20 (umístěného v pravém horním rohu vnitřního prostoru boxu). Unikátní vlastností je integrace s Home Assistantem a AI modelem Gemini 3.1 Flash Lite; po vložení nápoje a stisku tlačítka kamera OV2640 pořídí snímek, AI identifikuje obsah a automaticky nastaví optimální cílovou teplotu.

Project Description (EN)
The AI Smart Humidor is an intelligent cooling box designed for two wine bottles, constructed from high-insulation XPS foam. The system employs a Peltier element paired with active CPU heatsinks for effective thermal management. It is powered by an ESP32-S3 (GOOUUU V1.3) microcontroller, which monitors internal temperature via a DS18B20 sensor (positioned in the upper right corner of the box interior). A standout feature is the integration with Home Assistant and the Gemini 3.1 Flash Lite AI model; upon inserting a beverage and pressing a button, the OV2640 camera captures an image, the AI identifies the drink, and automatically configures the optimal target temperature.

Hardwarová specifikace
Mikrokontroler: GOOUUU ESP32-S3-CAM V1.3
Kamera: OV2640
Teplotní senzor: DS18B20 / MY18E20 (1-Wire)
Chlazení: Peltierův článek, 2x CPU chladič (vnitřní a vnější okruh)
Napájení: ATX zdroj s breakout boardem pro stabilní 12V/5V větve
Indikace: Adresovatelná RGB LED (WS2812B) připojená na GPIO48
Vstupy: Fyzické tlačítko pro spuštění analýzy

Instalace a první spuštění
ESPHome: V Home Assistantovi vytvořte novou instanci ESPHome a vložte obsah souboru esphome_config.yaml.
Unikátní ID senzoru: V konfiguraci esphome_config.yaml MUSÍTE změnit adresu 0x650b24a17f7ae128 na ID vašeho senzoru. Toto ID naleznete v logu ESPHome po prvním zapnutí zařízení.
API Klíče: Doplňte vlastní šifrovací klíč do sekce api: encryption: key:.
Tepelná regulace: PI regulátor v kódu využívá vyladěné parametry (Kp: 0.08, Ki: 0.003, alpha: 0.35). Nedoporučuje se tyto hodnoty měnit bez hlubší znalosti termodynamiky vašeho XPS boxu.
Home Assistant - Konfigurace: Obsah souboru ha_configuration.yaml přidejte do vašeho hlavního souboru configuration.yaml.
Home Assistant - Automatizace: Obsah souborů ha_automation.yaml a ha_led_logic.yaml vložte do souboru automations.yaml (nebo importujte přes rozhraní automatizací).
AI Provider: V souboru ha_automation.yaml nahraďte text "<VAŠE_PROVIDER_ID>" skutečným ID z vaší integrace LLM Vision (najdete v: Nástroje pro vývojáře -> Akce -> llmvision.image_analyzer).
