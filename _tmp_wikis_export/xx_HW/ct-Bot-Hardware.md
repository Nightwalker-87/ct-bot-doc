**Da der Maintainer nicht der Autor folgender Inhalte ist, welche bereits zuvor als freie Inhalte veröffentlicht worden sind, übernimmt er für diese keine Haftung und handelt gemäß der vorhandenen Lizenzbestimmungen (CC-BY-SA 4.0) für diese Inhalte nach bestem Wissen und Gewissen. Bei rechtlich bedenklichen Inhalten, die trotz Sichtung noch unentdeckt geblieben sind, bittet der Maintainer um eine kurze Benachrichtigung, damit diese umgehend entfernt werden können.**

# Die Hardware des c't-Bot

## Aufbau und Montage

* c't-Artikel: [Aufbau des c't-Bot](../../ct_articles_heise/04_Aufbau_und_Inbetriebnahme.pdf)
* c't-Artikel: **[Fehlersuche](https://www.heise.de/ct/artikel/Kammerjaeger-290506.html)** an der Hardware des c't-Bot
* **[FAQ](https://www.heise.de/ct/artikel/FAQ-fuer-c-t-Bot-und-c-t-SIM-291940.html)-Einträge**
* Empfehlenswerte **[Hardware-Modifikationen](../ct-Bot-Modifikationen/ct-Bot-Modifikationen.md)**

Ist die Hardware soweit fertig, muss die Firmware auf den Bot:
* **[Programmieradapter](http://www.heise.de/ct/Redaktion/cm/klangcomputer/index1.htm)** (Achtung, diese Beschreibung des Adapters entstammt dem Klangcomputer-Projekt, das andere Einstellungen für die Fuse-Bits verwendet als der c't-Bot!)

## Test eines frisch aufgebauten ct-Bots

1. **[Test-Programm](ziped-releases/test-binaries.zip)** herunterladen
1. Das Testprogramm **[flashen](../Flash/Flash.md)**
1. Die Fernbedienung (falls das Modell *HQ RC Univers 29* verwendet wird) auf den Gerätecode **TV 334** (siehe beiliegende Anleitung) programmieren. Wer diese Fernbedienung mit vierstelligen Gerätecodes siehe Anleitung) besitzt, sollte unseren [Support](../FirstSteps/FirstSteps.md#Support) kontaktieren - der Gerätecode 334 funktioniert hier nicht.
1. Die Hardware des Bots **[testen](https://www.heise.de/ct/artikel/Hallo-Welt-290314.html)**. Wenn etwas nicht wie im Artikel beschrieben funktioniert, geht es weiter mit der **[Hardware-Fehlersuche](https://www.heise.de/ct/artikel/Kammerjaeger-290506.html)**. Wenn alle Tests erfolgreich abgeschlossen sind: Herzlichen Glückwunsch! Nun geht es an die eigene Roboter-Software oder die Erkundung der bereits vorhandenen. Bitte lesen Sie auf der **[Software-Seite](../ct-Bot-Software/ct-Bot-Software.md)** weiter.

## Erweiterungen

Das **[Erweiterungsmodul](../ct-Bot-Erweiterung/ct-Bot-Erweiterung.md)** beschert dem c't-Bot WLAN, MMC- oder SD-Karten und eine Transportklappe. Siehe auch:
* **[c't 2/2007, S. 184](https://www.heise.de/ct/artikel/Aussendienstler-290830.html)** Außendienstler, Funkmodul, Massenspeicher und Klappe für den c't-Bot
* **[Aufbauanleitung Erweiterungsmodul](../ct-Bot-Erweiterung/ct-Bot-Erweiterung.md)** und Klappe mit Fotos

Unter [Raspberry Pi](../RaspberryPi/RaspberryPi.md) finden sich Informationen über eine leistungsfähige CPU-Erweiterung des c't-Bots mit Hilfe eines Raspberry Pi.

## Korrekturen und Hinweise

Es haben sich im Laufe des Projekts einige kleine Fehler eingeschlichen. Zum Glück nur in der Dokumentation, nicht in der Hardware (auch wenn es hier mittlerweile einige [Verbesserungsvorschläge](../ct-Bot-Modifikationen/ct-Bot-Modifikationen.md) gibt). Hier daher die offizielle, bereinigte Version. Umstände und Irrtümer bitten wir zu entschuldigen.

Als Aufbauanleitung gilt nach wie vor, die in [c't 04/06 ab S. 208](https://www.heise.de/ct/artikel/Hallo-Welt-290314.html) abgedruckte. Sie enthält nach unserem derzeitigen Wissensstand keine Fehler. Lediglich in einem Schaltplan und der Stückliste hatte der Fehlerteufel seine Finger im Spiel. Da etwas Verwirrung durch unterschiedliche Versionen entstanden ist, stehen auf [dieser Seite](../ct-Bot-Aufbau/ct-Bot-Aufbau.md) der entsprechende Teil des Artikels mit einigen zusätzlichen Fotos und Anmerkungen, sowie alle Schalt- und Bestückungspläne. Auch die aktualisierte Stückliste findet sich hier. Sie entspricht bis auf die Bestellnummern der, die auch [Segor](http://www.segor.de/L1Bausaetze/ct-robot.shtml) auf seiner Homepage hat und ist etwas ausführlicher, als die in c't 04/06 abgedruckte.

Die Aufbauanleitung und die Korrekturhinweise, die den Teilesätzen beiliegen, die vor dem 12.2.2006 ausgeliefert wurden, bitte nicht mehr beachten. Sie werden durch die hier aufgelisteten Dokumente komplett ersetzt.

Überarbeitet gegenüber den in c't abgedruckten Informationen:

* Stückliste (aus c't 04/06)
* Schaltplan Sensorplatinen (aus c't 04/06)
* Bestückungsdruck Hauptplatine (aus c't 04/06)
* Schaltplan Hauptplatine (aus c't 02/06)

Wer bereits angefangen hat zu bauen findet hier eine Zusammenfassung der wichtigsten Korrekturen:

* Gegenüber dem ersten Schaltplan aus c't 02/06 haben sich diverse Widerstandswerte geändert. Neu hinzugekommen ist auch die Schutzschaltung gegen Verpolen der Spannungsversorgung. Des Weiteren hat sich die Polung der DC-Buchse geändert. Alle diese Änderungen dokumentiert bereits c't 04/06.
* In der Stückliste in c't 04/06 haben R6, R32, Pot1 falsche Werte. Des Weiteren sind die LEDs verrutscht.
* In dem Bestückungsplan in c't 04/06 sind R7 und R27 vertauscht.
* Im Maussensorschaltplan in c't 04/06 ist U102 verpolt.
* Die Montageanleitung der IR-Distanzsensoren im Beipackzettel ist fehlerhaft.

# Hardware-Erweiterungen für den c't-Bot

Sammlung von Ideen oder Leservorschlägen:

## Sprachmodul SP03

Siehe [PDF-Dokumentation](sp03.pdf) von Harald W. Leschner.

## CMPS03-Kompass

Anschluss an den I^2^C-Bus des ATmegas wie unter [Sprachmodul SP03](sp03.pdf) beschrieben. Softwareseitiger Konfigurationsschalter `CMPS03_AVAILABLE` (siehe [Konfigurationsschalter](../../doc/wiki_pages/ct-bot_h.md)).

## Ultraschallsensor SRF10

Anschluss an den I^2^C-Bus des ATmegas wie unter [Sprachmodul SP03](sp03.pdf) beschrieben. Softwareseitiger Konfigurationsschalter `SRF10_AVAILABLE` (siehe [Konfigurationsschalter](../../doc/wiki_pages/ct-bot_h.md)).

## MMC per Hardware-SPI

Die MMC / SD-Karte kann auf zwei Weisen angesprochen werden:

1. Per Software-Steuerung (das ist die Standard-Einstellung), dafür muss `SPI_AVAILABLE` in [include/bot-local.h](https://github.com/tsandmann/ct-bot/blob/master/include/bot-local.h) **aus** sein.
1. Per Hardware-SPI-Steuerung, dafür ist ein kleiner Hardware-Umbau nötig: Es muss die Verbindung zwischen Prozessor-Pin *PC5* (*IC1 Pin 27*) und dem Display-Anschluss (*ST4 Pin 7*) getrennt werden (die Busy-Leitung wird vom Display-Treiber nicht genutzt, darum hat das keine Nachteile) und an *PC5* (*IC1 Pin 27*) der linke Radencoder (*RADL* / *IC3C Pin 6*) angeschlossen werden. Die Verbindung von *IC4 Pin 15* darf dabei jedoch **nicht** vom Display-Anschluss (*ST4 Pin 7*) getrennt werden! Ausserdem ist Prozessor-Pin *PB4* (*IC1 Pin 5*) von *IC3C Pin 6* zu trennen (der *PB4*-Pin kann für andere Zwecke genutzt werden, er muss jedoch immer als *Output* konfiguriert sein).

Nun schaltet man in [include/bot-local.h](https://github.com/tsandmann/ct-bot/blob/master/include/bot-local.h) die Option `SPI_AVAILABLE` **an**, dadurch wird die Kommunikation mit der SD-Karte über das Hardware-SPI Modul des Prozessors gesteuert. Der Vorteil ist eine höhere Transfer-Geschwindigkeit zur SD-Karte (Faktor 2) und es sind ca. 430 Byte weniger im Flash-Speicher des Prozessors belegt. Zu beachten ist, dass `SPI_AVAILABLE` von jetzt an immer eingeschaltet sein muss, auch wenn man keine MMC-Unterstützung benötigt, weil die Radencoder-Auswertung die veränderte Pin-Belegung immer berücksichtigen muss.

*Hinweis*: Es handelt sich hierbei um eine **reine Optimierungsmaßnahme**, durch die *keine* weiteren Features ermöglicht werden! Von der schnelleren Anbindung der SD-Karte profitiert z.B. die Kartographie, weil die Map-Updates so weniger Prozessorzeit beanspruchen und daher häufiger ausgeführt werden können, ohne die Bot-Verhalten zu stören.

## Lokalisierung

Siehe [Lokalisierung des c't-Bots](../Localization/Localization.md) mit Zusatzhardware.

== Optionale Bausätze und Bauteile ==

* [[LCD-Modul|LCD-Display]] beleuchtet mit Abstandsbolzen und Kabel (ct-Robot/Displaysatz)
* Platine und Teilesatz für den BlueMP3/ISP-Programmieradapter (BlueMP3/ISP-Platine), (BlueMP3/ISP-Teilesatz) oder STK200/500 kompatibler [[AVR_ISP_Programmer|ISP Programmer]].
* Platine und Teilesatz incl. Gehäuse für Diagnoseverbindung [[USB-Modul|Robot-USB]] mit FT232RL aufgelötet (USB-2-Bot/Platine), (USB-2-Bot/Teilesatz)
* [[RC_Univers_29|Universal-Fernbedienung]] (ct-Robot/Fernbedienung)
* Mignon-Akkus 2500mAh Sanyo (5 Stück werden ggf. benötigt)

=== LCD-Display Bausatz===

{|
!|Segor-Bezeichnung
!|Anzahl
!|Bemerkung
|----
|LCD 4x20-LED
|1
|
|----
|M3x40 II
|4 (8)
|Abstandsbolzen mit Gewinde
|----
|M3x6K
|8 (100)
|Schrauben
|----
|FB 16/BELDEN
|15cm (1m)
|Flachbandkabel
|----
|AWP 16
|1
|Stecker
|}


[![License: CC BY-SA 4.0](../../License.svg)](https://creativecommons.org/licenses/by-sa/4.0/)
