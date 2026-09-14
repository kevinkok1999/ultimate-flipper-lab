# Ultimate Flipper Lab

Modulair onderzoeksplatform voor een Flipper Zero en eigen/geautoriseerde testhardware.

## Status

Repository bootstrap. De volgende commits voegen de officiële SDK-app, protocol-engine, simulaties, tests en documentatie toe.

## Veiligheidsgrens

Alleen eigen apparatuur, zelfgebouwde testtargets en expliciet geautoriseerde systemen. Geen bypass van auto's, sloten, accounts of toegangssystemen. TX staat standaard uit.

## Kernprincipes

- Flipper Zero blijft de centrale interface.
- Onbekende signalen blijven RAW of UNDECODED.
- GPIO wordt behandeld als 3,3V-logica.
- Externe modules gebruiken een expliciete identificatie en een gedocumenteerd UART/SPI-protocol.
- Elke technische claim krijgt een primaire bron en versiedatum.

Zie ARCHITECTURE.md en TESTING.md voor de geplande uitvoering.
