# CPU-Erweiterung für den c't-Bot mit einem BeagleBoard

## Einleitung

Die Standard-Hardware des c't-Bots lässt sich mit dem umfangreichen Software-Framework inzwischen nahezu vollständig ausreizen.
Um weitere Features implementieren zu können, entstand daher die Idee, den c't-Bot um eine CPU-Erweiterung zu ergänzen, die auch im c't Sonderheft [c't Hacks/Make 01/2012, S.108](https://shop.heise.de/katalog/c-t-bot-roboter-selbst-bauen) vorgestellt wird.

Diese Wiki-Seite soll darüber informieren wie sich ein c't-Bot mit einem BeagleBoard erweitern lässt und welche Anpassungen an Hard- und Software dafür nötig sind.
Hierbei sei angemerkt, dass eine CPU-Erweiterung den "Bastel-Aspekt" des c't-Bot Projekts in den Vordergrund stellt, sodass keine abgeschlossene Baugruppe oder ausgereifte Software zur Verfügung steht.
Daher enthält dieser Artikel im Allgemeinen auch keine einsteigerfreundlichen und vollständigen Schritt-für-Schritt-Anleitungen.
Vielmehr geht es darum, Ideen und Lösungsansätze zusammenzutragen um das Konzept einer solchen Erweiterung auszubauen und zu optimieren.


## Idee

* Anstelle des offiziellen Erweiterungs-Boards mit WLAN- und MMC-Funktion zusätzlich zur Hauptplatine des c't-Bots ein BeagleBoard montieren.
* Der ATmega Mikrocontroller des Bots führt einen sogenannten Low-Level Code aus und kommuniziert mit dem BeagleBoard über eine serielle Schnittstelle (UART, SPI).
* Das BeagleBoard führt eine Linux-Distribution (z.B. Ubuntu für die ARM-Prozessorarchitektur) aus und ermöglicht die folgenden Features:
    * SSH Login
    * Filetransfer zwischen Bot und PC
    * NFS-Mounts
    * Ausführung fast jeder Linux-Software
* Das BeagleBoard bietet weitere Schnittstellen (USB, LAN, I2C, Audio, GPIOs) welche sich für zusätzliche Hardware (WLAN-USB-Dongle, weitere Sensoren, Kamera, etc.) nutzen lassen.
* Die Funktionalität des WiPorts wird mit einem einfachen WLAN-USB-Stick und socat bereitgestellt (Voraussetzung: Der Treiber ist im Linux-Kernel enthalten).
* Die GPIO-Pins des BeagleBoards steuern die Reset-Leitung des ATmega Mikrocontrollers und fragen Fehler- und Batteriestatus ab.
* Mit den Audio-Ports des BeagleBoards lassen sich die folgenden Funktionen realisieren:
    * Sound- und Sprachausgabe (Verstärkerschaltung nötig)
    * Mikrofon (Verstärkerschaltung nötig)
    * Line-In Anschluss
* Erweiterung des c't-Bots um eine Kamera, die über den Kamera-Port des BeagleBoards xM oder per USB angeschlossen wird


## Voraussetzungen

* Bastelinteresse an Hard- und Software
* c't-Bot (oder kompatibler Roboter bzw. ähnliche Hardware)
* PC oder virtuelle Maschine mit installiertem Linux (Linux-VM)
* Eingebundene Cross-Toolchain für die Übersetzung des Bot-Codes nach ARM-Linux (Archtektur: ARMv7-A, hardfloat), verfügbar für Linux und Windows in Form der Linaro Toolchain
* Installierte c't-Bot [Toolchain](../Installationsanleitung/Installationsanleitung.md)

Als Betriebssystem wurde Ubuntu 12.04 verwendet - die Nutzung verwandter Distributionen ist vermutlich ebenfalls möglich.


## Hardware

Die CPU-Erweiterung für den c't-Bot umfasst nicht nur das CPU-Board selbst, sondern auch ein dafür notwendiges Interface-Board.
Dieses verbindet die c't-Bot Hardware mit dem BeagleBoard und nimmt die notwendige Konvertierung der Signal-Spannungspegel von 1,8 V (BeagleBoard) auf 5,0 V TTL (c't-Bot Hauptplatine) vor.


### BeagleBoard

Bei dem Vorhaben den c't-Bot mit einer leistungsfähigeren CPU auszustatten, fiel die Wahl auf das BeagleBoard von Texas Instruments.
Diese Seite umfasst keine detaillierte Anleitung zur Einrichtung eines BeagleBoards, sondern verweist im Folgenden auf die entsprechenden (zumeist englischsprachigen) Informationen der BeagleBoard-Community.


#### Technische Daten / Versionen

Zum Zeitpunkt der Erstellung dieser Seite gibt es drei Versionen des BeagleBoards _(Stand: Januar 2012)_ :

1. **BeagleBoard Rev. C4**

    Hierbei handelt es sich um das ursprüngliche BeagleBoard; im Folgenden als _BeagleBoard_ bezeichnet wird.

    Spezifikationen:
    * Super-scalar ARM Cortex-A8 ([OMAP3530](https://www.ti.com/lit/ds/symlink/omap3530.pdf)), CPU 720 MHz, DSP 520 MHz
    * 256 MB LPDDR RAM
    * 256 MB NAND Flash
    * High-speed USB 2.0 OTG port
    * High-speed (only) USB 2.0 host port
    * Stereo audio out / in
    * DVI-D video out
    * S-video out
    * SD/MMC slot
    * Preis: 119 € (in Deutschland)

1. **BeagleBoard-xM Rev. C**

    Diese Version unterscheidet sich vom obigen Board im Wesentlichen durch einen schnelleren Prozessor, mehr Speicher und einen integrierten USB-Hub; im Folgenden als _BeagleBoard-xM_ bezeichnet

    Spezifikationen:
    * Super-scalar ARM Cortex-A8 ([DM3730](https://www.ti.com/lit/ds/symlink/dm3730.pdf)), CPU 1 GHz, DSP 800 MHz
    * 512 MB LPDDR RAM
    * High-speed USB 2.0 OTG port
    * On-board four-port high-speed USB 2.0 hub with 10/100 MBit Ethernet
    * Stereo audio out / in
    * DVI-D video out
    * S-video out
    * microSD slot and 4 GB microSD card
    * Camera port
    * Overvoltage Protection
    * Preis: 143 € (in Deutschland)

Ein technischer Vergleich von _BeagleBoard-xM_ und _BeagleBone_ findet sich [hier](https://beagleboard.org/static/flyer_latest.pdf).


#### Reference Manuals

* [BeagleBoard Reference Manual](https://beagleboard.org/static/BBSRM_latest.pdf)
* [BeagleBoard-xM Reference Manual](https://beagleboard.org/static/BBxMSRM_latest.pdf)

#### Weblinks

* BeagleBoard Projekt:
    * Offizielle [BeagleBoard Projektseite](https://beagleboard.org)
    * Offizielle [BeagleBoard FAQ](https://beagleboard.org/support/faq)
    * [Google Groups Forum](https://groups.google.com/forum/#!forum/beagleboard) zum BeagleBoard

* eLinux-Wiki:
    * [BeagleBoard Varianten](https://elinux.org/Beagleboard:Main_Page)
    * [Einsteiger-Infos](https://elinux.org/BeagleBoardBeginners)
    * [Ubuntu auf dem Beagle Board](https://elinux.org/BeagleBoardUbuntu)
    * [SPI-Interface des BeagleBoards](http://elinux.org/BeagleBoard/SPI)
    * [BeagleBoard FAQ](http://elinux.org/BeagleBoardFAQ)

* Sonstiges:
    * Anleitung für die Installation von [Ubuntu auf ARM Server developer boards](https://wiki.ubuntu.com/ARM/Server/Install) _(Support für TI OMAP3-based platform eingestellt)_
    * Wissenschaftlich/technisches Paper welches ein älteres (600 MHz) BeagleBoard mit einem System auf Basis von Intels Atom CPU (N330) vergleicht und ein paar Hintergründe zur ARM Cortex-A8 Architektur erläutert:
        * [K. Roberts-Hoffman, P. Hegde (2009): "ARMCortex-A8 vs. Intel Atom: Architecturaland Benchmark Comparisons", University of Texas](http://caxapa.ru/thumbs/229665/armcortexa8vsintelatomarchitecturalandbe.pdf)

### WLAN

Für die kabellose Verbindung zur Außenwelt wird ein handelsüblicher USB-WLAN-Dongles verwendet, wobei zu berücksichtigen ist, dass der Linux-Kernel einen Treiber für den verwendeten Chipsatz mitbringt.

Getestete USB-WLAN-Dongles:
* D-Link Wireless N Nano USB Adapter (DWA-131):
    * \+ kompakte Abmessungen (18 mm x 34 mm x 7 mm inkl. USB-Stecker)
    * \- eher geringe WLAN-Reichweite aufgrund der (Antennen-) Abmessungen

* D-Link Wireless N 150 Pico USB Adapter (DWA-121)
    * \+ sehr kompakte Abmessungen (14 mm x 20 mm x 6 mm inkl. USB-Stecker)
    * \+ ragt eingesteckt nicht über den Bot-Geometrie hinaus
    * \- eher geringe WLAN-Reichweite aufgrund der (Antennen-) Abmessungen

* FRITZWLAN USB Stick N
    * \+ unterstützt das 5 GHz Band
    * \+ sehr gute Übertragungsleistung (ca. 5 MB/s auf BeagleBoard xM)
    * \- relativ große Gehäuse-Abmessungen (73 mm x 24,5 mm x 10,5 mm)
    * \- Anschluss über eine USB-Verlängerung sinnvoll

### Interface-Board

Das Interface-Board bindet das BeagleBoard (BeagleBoard und BeagleBoard-xM) an die Hardware des c't-Bots an und bietet die folgenden Features:
* Pegelanpassung 1,8 V <-> 5,0 V (TTL) der **UART2-Signale**
* Pegelanpassung 1,8 V <-> 5,0 V (TTL) für **GPIO-Pins** (Reset-Leitung zum ATmega & Fehler-Signal)
* Pegelanpassung 1,8 V <-> 5,0 V (TTL) der **McSPI4.0-Signale**
* Steckplatz für den **ATmega1284P** Mikrocontroller, welcher den originalen Microcontroller auf dem Mainboard des c't-Bots ersetzt.
* SPI-Anschluss für ISP oder externen MMC- / SD-Slot
* Stereo **Audio-Out Verstärker** für zwei Lautsprecher (8 Ω, 0,5 W)

Hinweise zum Interface-Board:
* Das Interface-Board verwendet belegt den SPI-Port des ATmega Mikrocontrollers, weshalb der Maus-Sensor nicht mehr verwendet werden kann.
* Auf dem Interface-Board befinden sich zwei SMD-Bauteile: *IC3* im SOIC-14 Package und *IC2* im TSSOP-16 Package.
Allgemein sind für die Bestückung von SMD-Bauteilen per Hand fortgeschrittene Lötkenntnisse und eine feine Motorik erforderlich.
Sofern keine Verbindung per SPI-Bus zwischen BeagleBoard und ATmega1284P benötigt wird, kann auf die Bestückung von *IC2* auch verzichtet werden.
* Das Interface-Board lässt sich alternativ auch auf einer Lochraster-Platine aufbauen, welche jedoch sehr kompakt bestückt werden sollte, sodass sie die Abmessungen des BeagleBoards möglichst nicht überschreitet und auf den Bot passt.

#### Schaltplan & Stückliste

[Schaltplan des Interface-Boards](../documents/bb_interface_schematic.pdf)

| Bauteil                         | Bezeichnung                                       |
| :---                            | :---                                              |
| C1 - C6, C9, C14, C15, C18, C19 | Kondensator 100 nF                                |
| C7, C8                          | Kondensator 22 pF                                 |
| C10                             | Elektrolyt-Kondensator 22 µF                      |
| C12, C13                        | Elektrolyt-Kondensator 100 µF                     |
| C16, C17                        | Elektrolyt-Kondensator 220 µF                     |
| D1 - D4                         | Schalt-Diode 1N4148                               |
| IC1                             | Mikrocontroller ATmega1284P                       |
| IC2                             | [SN74AVC4T774](http://www.ti.com/product/sn74avc4t774)|
| IC3                             | 4-Bit Bidirectional Voltage-Level Shifter TXB0104 |
| IC4                             | Dual Power Amplifier TDA2822M                     |
| J4 - J8                         | Stiftleiste 1x8                                   |
| JP1                             | Stecker für BeagleBoard-Erweiterung               |
| JP2                             | Stecker für Audio-In 1x3                          |
| JP3                             | Stecker für Lautsprecher 1x4                      |
| JP4                             | Stecker für ISP-Programmer 2x5                    |
| JP5                             | Stecker für LDDR/BPS 1x3                          |
| L1, L2                          | Drossel 100 µH                                    |
| Q1                              | n-Channel Feldeffekttransistor (MOSFET) BS170     |
| Q2                              | Quarz 20 MHz                                      |
| R1 - R3, R6, R13                | Widerstand 10 kΩ                                  |
| R4, R5                          | Widerstand 4,7 Ω                                  |
| R7, R8                          | Widerstand 220 Ω                                  |
| R9, R11                         | Widerstand 2,7 kΩ                                 |
| R10, R12                        | Widerstand 4,7 kΩ                                 |



### Montage

* ATmega auf der Bot-Hauptplatine entfernen.
* Interface-Board anstelle des [originalen Erweiterungsmoduls](../ct-Bot-Erweiterung/ct-Bot-Erweiterung.md) montieren, längere Abstandsbolzen verwenden, Kabel auf J4 bis J8 verbinden.
* BeagleBoard auf Interface-Board montieren, elektrische Verbindung über BB-Extension-Header.
* Display mit zusätzlichen Abstandsbolzen oberhalb des BeagleBoards anbringen.

## Toolchain

*Die Anleitung für die Toolchain wurde für Ubuntu 12.04 LTS / hardfloat-ABI aktualisiert. Die alte Version für Ubuntu 11.04 ist [wiki:BeagleBoard?version=23 hier] zu finden.*

Um den c't-Bot Code (oder andere Programme) für die ARM-Architektur des BeagleBoards zu übersetzen, wird ein Cross-Compiler benötigt. Alternativ lässt sich der entsprechende Code auch direkt auf dem BeagleBoard übersetzen, wenn dort gcc & Co. installiert sind, was allerdings deutlich umständlicher und langsamer ist.

### Cross-Compiler Linux

Unter Ubuntu (getestet 12.04 LTS oder neuer) wird die nötige Cross-Toolchain für die BeagleBoard-Plattform *arm-linux-gnueabihf* durch das Paket **g++-arm-linux-gnueabihf** installiert: `sudo apt-get install g++-arm-linux-gnueabihf`.

Andere Linux-Distributionen bieten vermutlich ähnliche Pakete an, *Hinweise willkommen*. Wichtig ist dabei, dass die *hardflot*-ABI verwendet wird.

Zum Compilieren des Bot-Codes mit dem Cross-Compiler der Distribution als Target *Debug-ARM-Linux-BB* auswählen und in den Projekteinstellungen für Compiler, Assembler und Linker `arm-linux-gnueabihf-gcc` eintragen.

### Cross-Compiler Windows

Die [Linaro Toolchain](https://launchpad.net/linaro-toolchain-binaries) stellt einen kostenlosen Cross-Compiler für ARM-Linux (hardfloat) unter Windows zur Verfügung.

Als Installer [hier](https://launchpad.net/linaro-toolchain-binaries/+download) herunterladbar. Getestete Version: *2012.05-20120523_win32.exe*.

Zum Compilieren des Bot-Codes unter Windows als Target *Debug-ARM-Linux-BB* auswählen und in den Projekteinstellungen für Compiler, Assembler und Linker `"arm-linux-gnueabihf-gcc"` eintragen (Installationspfad sollte im PATH eingetragen sein, ansonsten absoluten Pfad angeben).

### Libraries

Derzeit werden die folgenden Libraries sowohl auf der Linux-Distribution des BeagleBoards, als auch auf dem Rechner zum Cross-Compilieren benötigt:

#### Flite, Alsa

Die Sprachsynthese-Bibliothek *Flite* kann optional zur Sprachausgabe benutzt werden. Dazu muss auf dem BeagleBoard die Bibliothek *Alsa* installiert sein (`sudo apt-get install alsa-base libasound2-dev`).

* Cross-Compilieren aus dem Quelltext. Zuvor die Datei */usr/lib/arm-linux-gnueabihf/libasound.so.2.0.0* und das Verzeichnis */usr/include/alsa* der *Alsa-Bibliothek* vom BeagleBoard nach */usr/local/arm-linux/arm-cortex_a8-linux-gnueabi/sysroot/usr/lib* bzw. *usr/local/arm-linux/arm-cortex_a8-linux-gnueabi/sysroot/include/* kopieren. Außerdem nach `cd /usr/local/arm-linux/arm-cortex_a8-linux-gnueabi/sysroot/usr/lib` mit `sudo ln -s libasound.so.2.0.0 libasound.so` einen Link anlegen. Unter Linux oder Mac OS X sind dann diese Schritte nötig:
* Archiv herunterladen und entpacken (*!ToDo: Link*)
* `./configure --with-audio=alsa --host=arm-linux --enable-shared`
* `make`
* Dateien aus *lib* nach *ct-Bot/contrib/flite/lib/arm-linux-gnueabihf/* kopieren

## Software

Auf dem BeagleBoard wird eine Linux-Distribution ausgeführt, die auf der SD-Karte installiert ist.

### Ubuntu (ARM)

Getestete und empfohlene Version: **12.04 LTS** (*Precise Pangolin*).

#### Installation

Siehe [Installation von Ubuntu 12.04 LTS für ARM auf einem BeagleBoard](/BeagleBoardUbuntu1204Install.md).

#### Anpassungen

Damit das BeagleBoard mit dem c't-Bot kommunizieren kann, sind ein paar Anpassungen am Linux-Kernel erforderlich. Sie sorgen dafür, dass die nötigen Schnittstellen auf die Erweiterungspins geroutet werden und konfigurieren die Schnittstellen entsprechend.

Zur Installation siehe [Ubuntu 12.04 Installationsanleitung](/BeagleBoardUbuntu1204Install.md#AngepasstenKernelinstallieren).

#### Konfiguration

Siehe [Ubuntu 12.04 Installationsanleitung](../BeagleBoardUbuntu1204Install/BeagleBoardUbuntu1204Install.md#WLANkonfigurieren).

### Low-level Bot-Code für ATmega

Der ATmega1284P auf dem Interface-Board führt den Low-level Code aus und stellt somit die Schnittstelle zur c't-Bot-Hardware bereit. Der Vorteil durch die Verwendung eines zusätzlichen Mikrocontrollers neben dem BeagleBoard besteht in der Kompatibilität zum originalen c't-Bot und der Wiederverwendbarkeit sämtlicher Treiber für die Bot-Hardware. Der Low-level Code besteht aus einer leicht modifizierten Untermenge des originalen c't-Bot Codes. Verzichtet wird dabei auf sämtlichen Verhaltenscode und weitere Features wie Kartographie oder Positionsspeicher, all das übernimmt der High-level Code, den die BeagleBoard-CPU ausführt. Zusätzlich implementiert ist eine CRC16-Prüfsumme, welche die Kommunikation mit dem BeagleBoard gegen Übertragungsfehler absichert. Um den Low-level Code zu aktivieren, muss in *ct-Bot.h* der Schalter `BOT_2_RPI_AVAILABLE` aktiviert werden.

### High-level Bot-Code für ARM

Das BeagleBoard führt den für die ARM-Linux Architektur compilierten High-level Code aus und übernimmt somit die Ausführung von Verhalten, Kartographie usw.

Um den c't-Bot Code für einen Bot mit BeagleBoard-Erweiterung zu übersetzen als Build-Konfiguration in Eclipse *Debug-ARM-Linux* wählen und den Schalter `ARM_LINUX_BOARD` in *ct-Bot.h* aktivieren.

Die wesentlichen Unterschiede zum originalen ct-Bot-Code:

* CRC16-Prüfsumme für Kommunikation
* Anpassungen für Kommunikation (Synchronisation, Anmeldung als realer Bot)
* Anpassungen für Auswertung der Distanzsensoren (Umrechnung gemäß Kennlinie erfolgt bereits im Low-level Code)
* Anpassungen für Motorsteuerung (1:1 Weitergabe der Geschwindigkeit)
* Anpassungen für RC5-Code (Toggle-Bit Auswertung)

### BeagleBoard-Emulation

Ein BeagleBoard lässt sich (inkl. Linux Installation) mit Qemu emulieren. Eine Installationsanleitung für Ubuntu Hosts ist [hier](http://www.cnx-software.com/2011/09/26/beagleboard-emulator-in-ubuntu-with-qemu) zu finden.

[![License: CC BY-SA 4.0](../../License.svg)](https://creativecommons.org/licenses/by-sa/4.0/)
