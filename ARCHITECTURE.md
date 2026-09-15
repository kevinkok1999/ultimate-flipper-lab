# Architectuur — Ultimate Flipper Lab

## 1. Overzicht

Ultimate Flipper Lab wordt opgebouwd als één centrale FAP met losse modules achter een gemeenschappelijke interface.

```text
+--------------------------------------------------+
|                 Ultimate Lab UI                  |
+--------------------------------------------------+
| IR | Sub-GHz RX | NFC | LF RFID | iButton       |
| GPIO | USB/BLE | Lab Vault | Diagnostics         |
+--------------------------------------------------+
| Capability Registry | Safety Gate | Storage      |
+--------------------------------------------------+
|        Officiële Flipper firmware/API            |
+--------------------------------------------------+
| IR | CC1101 | NFC/RFID | 1-Wire | GPIO | BLE/USB |
+--------------------------------------------------+
```

## 2. Kerncomponenten

### 2.1 UI shell

Verantwoordelijk voor:

- hoofdmenu;
- module-status;
- veilige foutmeldingen;
- capability-detectie;
- informatie over actieve RX/TX-state;
- terugkeren naar één consistente interface.

### 2.2 Capability Registry

Iedere module registreert minimaal:

- `module_id`;
- naam;
- hardwarevereisten;
- modus: `OBSERVE`, `ANALYZE`, `CONTROL`;
- TX nodig: ja/nee;
- opslag nodig: ja/nee;
- experimenteel: ja/nee.

Hierdoor kan de UI duidelijk tonen wat een functie werkelijk doet.

### 2.3 Safety Gate

De Safety Gate voorkomt dat analysefuncties automatisch veranderen in toegangsbypass.

Regels:

- geen brute-force van credentials;
- geen automatische rolling-code generatie;
- geen automatische replay van ontvangen toegangs-/keyless-signalen;
- geen geheime sleutel-dumps uit online bronnen;
- geen workflows voor auto's, deuren of accounts buiten officiële pairing;
- IR voor normale consumentenapparatuur mag wel zenden;
- GPIO-labtests mogen zenden naar expliciet aangesloten zelfgebouwde hardware.

### 2.4 Lab Vault

Voorgestelde opslagstructuur op SD:

```text
/ext/apps_data/ultimate_lab/
  devices/
  infrared/
  captures/
  gpio/
  notes/
  diagnostics/
```

De vault slaat metadata op zoals:

- datum/tijd;
- module;
- protocol;
- frequentie indien relevant;
- zelfgekozen apparaatnaam;
- notities;
- classificatie `LAB`, `OWNED`, `UNKNOWN`.

Geen geheime toegangssleutels worden automatisch geëxporteerd.

## 3. Modules

### IR Universal Remote

Doel: eigen consumentenapparatuur bedienen.

Functies:

- categorieën TV / Audio / Airco / Overig;
- merkprofielen;
- favorieten;
- macro's zoals `TV aan -> receiver aan -> juiste input`;
- eigen aangeleerde IR-commando's ordenen;
- compatibiliteit met Flipper IR-bestandsformaat.

### Sub-GHz Signal Inspector

Doel: RF-signalen van eigen testzenders begrijpen zonder automatische toegangsbypass.

Functies:

- RX-status;
- RSSI-indicatie;
- frequentie en preset tonen;
- protocolnaam tonen indien officiële decoder hem kent;
- onbekende signalen classificeren als RAW/UNDECODED;
- pulse timing statistieken;
- sessienotities.

Geen replayknop in deze module.

### NFC Inspector

Doel: eigen NFC-testtags begrijpen.

Functies:

- technologie/familie herkennen;
- tagtype en ondersteunde features tonen;
- geheugen-/protocolinformatie op hoog niveau;
- notities en inventaris;
- labtags markeren als testobject.

### LF RFID Inspector

Doel: eigen 125/134 kHz testtags herkennen en inventariseren.

Functies:

- protocolherkenning;
- leeskwaliteit/status;
- inventarisatie;
- vergelijking tussen twee eigen testtags op metadata.

### iButton / 1-Wire Lab

Doel: 1-Wire leren en eigen testhardware controleren.

Functies:

- family code herkennen;
- ROM/CRC-validatie;
- busdiagnose;
- zelfgebouwde testtarget controleren.

### GPIO Workbench

Doel: Flipper als draagbare elektronicatool gebruiken.

Modules:

- UART console;
- I2C scanner voor aangesloten eigen modules;
- SPI demonstratiemodus;
- digitale input monitor;
- veilige GPIO outputtest;
- ADC/meetfuncties waar door hardware/API ondersteund.

3.3 V-logica blijft uitgangspunt; externe spanningen vragen passende level shifting.

### USB/BLE Tools

Legitieme functies:

- presentatie-afstandsbediening;
- mediacontrol voor eigen computer;
- diagnostische BLE-informatie;
- eigen app/RPC-koppeling;
- seriële console via USB waar ondersteund.

### Diagnostics

Toont:

- firmware/API-versie;
- batterijstatus;
- opslagstatus;
- GPIO/module-detectie;
- actieve records/resources;
- laatste foutcode.

## 4. Uitbreidingsmodel

Nieuwe modules moeten:

1. een eigen map krijgen;
2. hun capabilities declareren;
3. geen directe afhankelijkheid van andere modules hebben;
4. fouten afvangen zonder de shell te laten crashen;
5. testdata gescheiden houden van echte apparaatdata;
6. minimaal één unit- of host-side test hebben waar praktisch mogelijk.

## 5. Hardware-uitbreidingen

Toegestane richting voor later:

- sensormodules via I2C/SPI/UART;
- GPS/GNSS voor eigen meetprojecten;
- environmental sensors;
- logic-level analysetools;
- eigen testtargets op ESP32/RP2040/Arduino;
- externe radio alleen voor legitieme meet-/labdoeleinden en binnen lokale regelgeving.

## 6. Versiebeheer

Elke release noteert:

- geteste officiële Flipper firmware/API;
- gebruikte buildmethode;
- bekende beperkingen;
- hardware waarop getest;
- nieuwe TX-capabilities expliciet apart.
