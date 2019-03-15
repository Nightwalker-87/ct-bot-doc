# Willkommen beim c't-Bot- und c't-Sim-Projekt

> **Hinweis:** Diese Dokumentationsseiten wurde aus dem ehemaligen Trac des Projekts exportiert und nach Markdown konvertiert, aber noch nicht auf Korrektheit überprüft! Daher können Fehler enthalten sein, außerdem sind einige Teile stark veraltet und nicht mehr aktuell, ihre Überarbeitung steht derzeit noch aus. Entsprechende Marker finden sich auf den jeweiligen Seiten:
>>>> **Trac-2-Markdown Konvertierung:** *incomplete*
>
>>> **Trac-2-Markdown Konvertierung:** *unchecked*
>
>> **Trac-2-Markdown Konvertierung:** *deprecated*

<img style="float: right; margin-left:2em;" src="bot.png" />

c't-Bot und c't-Sim gehören zusammen und sind ein Roboterprojekt der Zeitschrift c't. Dies hier ist die im Laufe des Projekts entstandene Dokumentation, die ursprünglich im Trac zum Projekt entstanden war. Auf diese Weise soll sichergestellt werden, dass das Projekt auch nach dem Erscheinen des letzten c't-Artikels in der Community weiterleben kann. Daher ergänzen diese Seiten die offizielle **[c't-Projektseite](http://www.heise.de/ct/projekte/ct-bot)**. Sämtliche Inhalte sind unter [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) lizenziert.

## c't-Bot in Aktion

Zur Einstimmung gibt es in der **[Galerie](../Galerie/Galerie.md)** Videos und Bilder rund um das Projekt.

## Anlaufstellen

Zum Projekt gibt es viel Doku, hier ein paar generelle Anlaufadressen:

1. **[c't-Artikel](../../doc/wiki_pages/ct_articles.md)**
1. Dieses **[Wiki](../WikiStart/WikiStart.md)**
1. Das **[Fan Forum zum c't-Bot](https://www.ctbot.de)**
1. Die **[Projektseite](http://www.ct-bot.de)**
1. Die **[FAQ](http://www.heise.de/ct/artikel/FAQ-fuer-c-t-Bot-und-c-t-SIM-291940.html)**
1. Das **[Heise Forum](http://www.heise.de/ct/foren/go.shtml?list=1&forum_id=89813)**
1. Die **[Ersten Schritte](../FirstSteps/FirstSteps.md)**
1. **Direkter Kontakt** über:
    * das Matrix-Netzwerk mit **[Riot.im](https://riot.im/app/#/room/#ctbot:matrix.org)** (auch als Gast ohne Registrierung nutzbar)
    * oder **[Slack](https://ct-bot-slack.herokuapp.com)**
    * Matrix/Riot.im und Slack sind synchronisiert, zeigen also immer dieselben Inhalte und können je nach persönlicher Präferenz gewählt werden.

## Schnelleinstieg in das Projekt

1. Mal ausprobieren, wie das ganze so geht (auch ohne Geld auszugeben): **[Erste Schritte mit dem c't-Bot](../FirstSteps/FirstSteps.md)**
1. c't-Bot **[aufbauen](../ct-Bot-Hardware/ct-Bot-Hardware.md#Aufbau-und-Montage)**
1. c't-Bot **[testen](../ct-Bot-Hardware/ct-Bot-Hardware.md#Test-eines-frisch-aufgebauten-ct-Bots)**
1. Die Firmware für die eigene Hardware **[kalibrieren](../ct-Bot-Software/ct-Bot-Software.md#Kalibrierung)**
1. Demo-Firmware **[ausprobieren](../ct-Bot-Software/ct-Bot-Software.md#Und-los-geht-es)**
1. **[Eigenen Code](../ct-Bot-Software/ct-Bot-Software.md#Eigene-Schritte)** schreiben
1. **[Firmware](../AVRToolchainInterna/AVRToolchainInterna.md)** für den realen Bot generieren
1. Firmware auf den realen Bot **[Übertragen (Flashen)](../Flash/Flash.md)**

## Hardware

* Überblick über die **[ct-Bot-Hardware](../ct-Bot-Hardware/ct-Bot-Hardware.md)**
  * **[Schaltpläne](../ct-Bot-Hardware/ct-Bot-Hardware.md#Schaltplaene)**
  * **[Stücklisten](../ct-Bot-Hardware/ct-Bot-Hardware.md#Stuecklisten)**
  * **[Aufbauanleitung](../ct-Bot-Hardware/ct-Bot-Hardware.md#Aufbau-und-Montage)**
  * **[Erweiterungen](../ct-Bot-Hardware/ct-Bot-Hardware.md#Erweiterungen)**
  * **[Firmware flashen](../Flash/Flash.md)**
* c't-Bot **[testen](../ct-Bot-Hardware/ct-Bot-Hardware.md#Test-eines-frisch-aufgebauten-ct-Bots)**

## Software

**[Installationsanleitung](../InstallationsanleitungR23/InstallationsanleitungR23.md)** für c't-Bot und c't-Sim

### c't-Bot

Dieses Teilprojekt umfasst den C-Code für reale und simulierte c't-Bots

* Überblick über die **[ct-Bot-Software](../ct-Bot-Software/ct-Bot-Software.md)**
* **[Dokumentation](../ct-Bot-Software/ct-Bot-Software.md#Dokumentation)** zum bestehenden Code
* **[Howto](../ct-Bot-Software/ct-Bot-Software.md#Howto)** zum Bot
* **[Ideen & mehr](../ct-Bot-Software/ct-Bot-Software.md#Ideen-und-mehr)**
* **[Kalibrierungen](../ct-Bot-Software/ct-Bot-Software.md#Kalibrierung)**
* **[Eigenen Code](../ct-Bot-Software/ct-Bot-Software.md#Eigene-Schritte)** schreiben

### c't-Sim

Dieses Teilprojekt umfasst den Java-Code für den Simulator c't-Sim

* Überblick über die **[ct-Sim Software](https://www.heise.de/ct/artikel/c-t-Bot-und-c-t-Sim-284119.html?seite=3)**
* **[Konfiguration](../ct-Sim/ct-Sim.md#Konfiguration)** der ct-Sim Optionen
* **[Howto](../ct-Sim/ct-Sim.md#Howto)** zum ct-Sim

### Zugang zum Sourcecode

Aller Sourcecode steht in einem frei zugänglichen Git-Repository auf GitHub. Damit eigener Code den Weg in das Repository findet, sollte er den **[Code Richtlinien](../../doc/wiki_pages/coding_conventions.md)** entsprechen.

* Code Repository: Ab sofort findet sich der aktuelle Bot-Code in einem [Repository auf GitHub](https://github.com/tsandmann/ct-bot). Die URLs, um den Code in Eclipse oder andere Tools zu holen lauten: `https://github.com/tsandmann/ct-bot.git` und `https://github.com/tsandmann/ct-sim.git`.
* **[Detailierte Beschreibung](../GITUndEclipse/GITUndEclipse.md)** zum Repository und der Integration in Eclipse.
* Der aktuell stabile Code liegt jeweils im Branch **[master](https://github.com/tsandmann/ct-bot/tree/master)**, der Neueste (aber teilweise auch Experimentelle)  im Branch **[develop](https://github.com/tsandmann/ct-bot/tree/develop)**.
* **[Zip-Files](https://github.com/tsandmann/ct-bot/releases)** mit dem Code der bisherigen Releases
* Ältere **[Erweiterungen](../deprecated/Patches/Patches.md)** von Lesern

### Entwicklungsumgebung

* Allgemeine **[Installationsanleitung](../InstallationsanleitungR23/InstallationsanleitungR23.md)** für c't-Bot und c't-Sim
* Entwicklungsumgebung
  * **[Eclipse-Installation](../EclipseInstallation/EclipseInstallation.md)** inkl. der nötigen Plugins
  * **[Code aus dem Repository](../GITundEclipse/GITundEclipse.md)** in Eclipse einbinden
  * **[Tipps, Tricks und Hotkeys](../EclipseTipps/EclipseTipps.md)** rund um Eclipse
* AVR-Toolchain
  * **[Installation der AVR-Toolchain](../AVRToolchain/AVRToolchain.md)** zur Entwicklung des Steuercodes eines *realen* c't-Bots
  * **[Hintergründe](../AVRToolchainInterna/AVRToolchainInterna.md)** zur AVR-Toolchain
  * **[AVR-Tools und Tricks](../Utils/Utils.md)** für die (Bot-)Softwareentwicklung

## Jagd auf den Fehlerteufel

* **[Fehlerberichte und Erweiterungsvorschläge zum c't-Bot](https://github.com/tsandmann/ct-bot/issues)**
* **[Fehlerberichte und Erweiterungsvorschläge zum c't-Sim](https://github.com/tsandmann/ct-sim/issues)**

## Organisatorisches

* Die **[Projekthistorie](../Historie/Historie.md)**
* Weitere **[Links](../Links/Links.md)** rund um den c't-Bot und auf Leserprojekte

[![License: CC BY-SA 4.0](../../License.svg)](https://creativecommons.org/licenses/by-sa/4.0/)
