# Ultimate Flipper Lab

Modulair onderzoeksplatform voor een Flipper Zero en eigen/geautoriseerde testhardware.

## Doel

Eén overzichtelijke Flipper-app met een groeiende verzameling legitieme hardware- en protocoltools voor:

- **Infrared**: universele afstandsbediening voor eigen tv, airco, audio en andere IR-apparaten.
- **Sub-GHz**: ontvangen, classificeren en analyseren van signalen van eigen testzenders. Geen automatische replay of toegangs-bypass.
- **NFC / 13.56 MHz**: kaarttype, protocol en technische metadata van eigen testtags onderzoeken.
- **LF RFID / 125 kHz**: eigen testtags identificeren en protocolkenmerken bekijken.
- **iButton / 1-Wire**: eigen testkeys en zelfgebouwde 1-Wire-hardware onderzoeken.
- **GPIO**: veilige 3.3 V UART, I2C, SPI en digitale I/O-tools voor sensoren en modules.
- **USB/BLE**: legitieme remote-, console- en diagnosefuncties voor eigen computers en apparatuur.
- **Lab Vault**: captures, notities, apparaatprofielen en testresultaten op de SD-kaart organiseren.

## Veiligheidsmodel

Het project is een **eigen hardwarelab**, geen universele sleutel. Functies die bedoeld zijn om auto's, deuren, garagedeuren, accounts of andere beveiligde toegang zonder officiële pairing/autorisatie te omzeilen horen niet in dit project.

Belangrijke defaults:

- Sub-GHz TX/replay staat buiten de kernapp en wordt niet geautomatiseerd.
- Onbekende signalen blijven `RAW` / `UNDECODED`.
- Geen brute-force van sleutels, rolling codes of credentials.
- Geen import van gestolen/gelekte toegangssleutels.
- IR-transmit is toegestaan voor normale consumentenapparatuur zoals tv/airco/audio.
- Labprotocollen gebruiken herkenbare testdata en zijn bedoeld voor zelfgebouwde targets.

## Huidige status

V1-bootstrap bevat:

1. architectuur en veiligheidsgrenzen;
2. modulair menu voor de Flipper FAP;
3. roadmap voor IR, Sub-GHz RX-analyse, NFC/RFID-inspectie, iButton, GPIO, USB/BLE en Lab Vault;
4. teststrategie voor echte hardware en simulaties.

De officiële Flipper-firmware bouwt externe apps als FAP vanuit `applications_user` met `FlipperAppType.EXTERNAL`.

## Structuur

```text
applications_user/ultimate_lab/   Flipper FAP
ARCHITECTURE.md                    systeemarchitectuur
ROADMAP.md                         ontwikkelfasen
SAFETY_SCOPE.md                    grenzen en threat model
docs/MODULES.md                    module-specificaties
```

## Bouwen

Plaats deze app in een checkout van de officiële Flipper Zero firmware en bouw hem met de officiële FBT-flow:

```bash
./fbt build APPSRC=applications_user/ultimate_lab
```

Voor build + upload naar een aangesloten Flipper:

```bash
./fbt launch APPSRC=applications_user/ultimate_lab
```

## Ontwerpprincipe

De Flipper Zero blijft de centrale interface. Externe modules zijn uitbreidingen, nooit een vervanging van het hoofdapparaat. Iedere module moet duidelijk aangeven of hij **observeert**, **analyseert** of **zendt** en welke veiligheidsgrens daarbij geldt.
