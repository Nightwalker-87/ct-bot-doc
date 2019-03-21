# Hardware-Erweiterungen für den c't-Bot

## Sprachmodul SP03

Siehe [PDF-Dokumentation](sp03.pdf) von Harald W. Leschner.

## CMPS03-Kompass

Anschluss an den I^2^C-Bus des ATmegas wie unter [Sprachmodul SP03](sp03.pdf) beschrieben. Softwareseitiger Konfigurationsschalter `CMPS03_AVAILABLE` (siehe [Konfigurationsschalter](../ctBotH/ctBotH.md)).

## Ultraschallsensor SRF10

Anschluss an den I^2^C-Bus des ATmegas wie unter [Sprachmodul SP03](sp03.pdf) beschrieben. Softwareseitiger Konfigurationsschalter `SRF10_AVAILABLE` (siehe [Konfigurationsschalter](../ctBotH/ctBotH.md)).

## MMC per Hardware-SPI

Die MMC / SD-Karte kann auf zwei Weisen angesprochen werden:

1. Per Software-Steuerung (das ist die Standard-Einstellung), dafür muss `SPI_AVAILABLE` in [include/bot-local.h](https://github.com/tsandmann/ct-bot/blob/master/include/bot-local.h) **aus** sein.
1. Per Hardware-SPI-Steuerung, dafür ist ein kleiner Hardware-Umbau nötig: Es muss die Verbindung zwischen Prozessor-Pin *PC5* (*IC1 Pin 27*) und dem Display-Anschluss (*ST4 Pin 7*) getrennt werden (die Busy-Leitung wird vom Display-Treiber nicht genutzt, darum hat das keine Nachteile) und an *PC5* (*IC1 Pin 27*) der linke Radencoder (*RADL* / *IC3C Pin 6*) angeschlossen werden. Die Verbindung von *IC4 Pin 15* darf dabei jedoch **nicht** vom Display-Anschluss (*ST4 Pin 7*) getrennt werden! Ausserdem ist Prozessor-Pin *PB4* (*IC1 Pin 5*) von *IC3C Pin 6* zu trennen (der *PB4*-Pin kann für andere Zwecke genutzt werden, er muss jedoch immer als *Output* konfiguriert sein).

Nun schaltet man in [include/bot-local.h](https://github.com/tsandmann/ct-bot/blob/master/include/bot-local.h) die Option `SPI_AVAILABLE` **an**, dadurch wird die Kommunikation mit der SD-Karte über das Hardware-SPI Modul des Prozessors gesteuert. Der Vorteil ist eine höhere Transfer-Geschwindigkeit zur SD-Karte (Faktor 2) und es sind ca. 430 Byte weniger im Flash-Speicher des Prozessors belegt. Zu beachten ist, dass `SPI_AVAILABLE` von jetzt an immer eingeschaltet sein muss, auch wenn man keine MMC-Unterstützung benötigt, weil die Radencoder-Auswertung die veränderte Pin-Belegung immer berücksichtigen muss.

*Hinweis*: Es handelt sich hierbei um eine **reine Optimierungsmaßnahme**, durch die *keine* weiteren Features ermöglicht werden! Von der schnelleren Anbindung der SD-Karte profitiert z.B. die Kartographie, weil die Map-Updates so weniger Prozessorzeit beanspruchen und daher häufiger ausgeführt werden können, ohne die Bot-Verhalten zu stören.

## Lokalisierung

Siehe [Lokalisierung des c't-Bots](../Localization/Localization.md) mit Zusatzhardware.

## CPU-Erweiterung mit Raspberry Pi

Siehe [CPU-Erweiterung](../RaspberryPi/RaspberryPi.md) für den c't-Bot.

[![License: CC BY-SA 4.0](../license.svg)](https://creativecommons.org/licenses/by-sa/4.0/)
