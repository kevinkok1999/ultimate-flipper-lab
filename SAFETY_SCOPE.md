# Safety Scope

## Toegestaan binnen dit project

- Eigen tv, airco, audio en andere normale IR-apparaten bedienen.
- Eigen sensoren, afstandsbedieningen en testzenders ontvangen/analyseren.
- Zelfgemaakte NFC/RFID-tags en labtargets onderzoeken.
- GPIO-, UART-, I2C- en SPI-experimenten met eigen hardware.
- USB/BLE-tools voor eigen computers en zelfgebouwde apparaten.
- Protocolkennis, signaalvisualisatie, logging en diagnostiek.

## Niet onderdeel van het project

- Sleutels of credentials brute-forcen.
- Rolling codes kraken, voorspellen of omzeilen.
- Auto-keyless, immobilizers of alarmsystemen omzeilen.
- Deur-, garage- of hektoegang openen zonder officiële pairing/autorisatie.
- Gelekte of gestolen key-databases importeren.
- Betaalpassen, accounts of andere beveiligde credentials klonen.
- Jamming, denial-of-service of verstoring van radiosystemen.

## Ontwerpregels

1. RX/analyse is standaard; TX wordt per module expliciet ontworpen.
2. IR-consumer-control mag TX gebruiken.
3. GPIO mag TX gebruiken naar fysiek aangesloten eigen labhardware.
4. Sub-GHz analyse bevat geen automatische replayfunctie.
5. Testcredentials zijn herkenbaar als labdata en niet afkomstig uit echte toegangssystemen.
6. Nieuwe functies worden beoordeeld op misbruikrisico voordat ze in de hoofdapp komen.
