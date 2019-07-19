**Da der Maintainer nicht der Autor folgender Inhalte ist, welche bereits zuvor als freie Inhalte veröffentlicht worden sind, übernimmt er für diese keine Haftung und handelt gemäß der vorhandenen Lizenzbestimmungen (CC-BY-SA 4.0) für diese Inhalte nach bestem Wissen und Gewissen. Bei rechtlich bedenklichen Inhalten, die trotz Sichtung noch unentdeckt geblieben sind, bittet der Maintainer um eine kurze Benachrichtigung, damit diese umgehend entfernt werden können.**

# Willkommen beim c't-Bot- und c't-Sim-Projekt

<img src="bot.jpg" style="float: right; margin-left:2em; height: 64px;" />

Dies ist das Portal für die Reste der **alten, noch nicht aufbereitete Dokumentation**.
Da es sich hierbei um zusammengetragene Inhalte aus unterschiedlichen Quellen und von verschiedenen Autoren innerhalb des Projekts handelt, sind noch nicht alle Inhalte gründlich gesichtet und überprüft. Das bedeutet auch, dass einige Verlinkungen nicht oder nicht mehr funktionieren.

Die neue, überarbeitete und geprüfte Dokumentation findet sich **[hier](../doc/wiki_main.md)** (**Hauptanlaufstelle**) und ist unter den [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) Lizenzbestimmungen veröffentlicht.


## Anlaufstellen (*deprecated*)

1. Die **[FAQ](http://www.heise.de/ct/artikel/FAQ-fuer-c-t-Bot-und-c-t-SIM-291940.html)**
1. Das **[Heise Forum](https://www.heise.de/forum/c-t/Kommentare-zu-c-t-Artikeln/c-t-Bot-und-c-t-Sim/forum-23074/)** (dient nur als Archiv)
1. Das **[Mailingliste](https://www.heise.de/ct/newsletter/archiv/ct-bot-entwickler/)** (dient nur als Archiv)
1. Ältere **[Erweiterungen](./Patches/Patches.md)** von Lesern

=====

## Markdown Dokumentation

> **Hinweis:** Diese Dokumentationsseiten wurde aus dem ehemaligen Trac des Projekts exportiert und nach Markdown konvertiert, aber noch nicht auf Korrektheit überprüft! Daher können Fehler enthalten sein, außerdem sind einige Teile stark veraltet und nicht mehr aktuell, ihre Überarbeitung steht derzeit noch aus. Entsprechende Marker finden sich auf den jeweiligen Seiten:
>>>> **Trac-2-Markdown Konvertierung:** *incomplete*
>
>>> **Trac-2-Markdown Konvertierung:** *unchecked*
>
>> **Trac-2-Markdown Konvertierung:** *deprecated*

c't-Bot und c't-Sim gehören zusammen und sind ein Roboterprojekt der Zeitschrift c't, das 2006 entstanden ist. Dies hier ist die im Laufe des Projekts entstandene Dokumentation, die ursprünglich im Trac zum Projekt entstanden war. Auf diese Weise soll sichergestellt werden, dass das Projekt auch nach dem Erscheinen des letzten c't-Artikels in der Community weiterleben kann. Daher ergänzen diese Seiten die offizielle **[c't-Projektseite](http://www.heise.de/ct/projekte/ct-bot)**.

## Hardware

* Überblick über die **[Hardware](./xx_HW/ct-Bot-Hardware.md)**

## Software

### c't-Bot

Dieses Teilprojekt umfasst den C-Code für reale und simulierte c't-Bots

* Überblick über die **[ct-Bot-Software](./ct-Bot-Software/ct-Bot-Software.md)**
* Demo-Firmware **[ausprobieren](./ct-Bot-Software/ct-Bot-Software.md#Und-los-geht-es)**
* **[Eigenen Code](./ct-Bot-Software/ct-Bot-Software.md#Eigene-Schritte)** schreiben
* **[Dokumentation](./ct-Bot-Software/ct-Bot-Software.md#Dokumentation)** zum bestehenden Code
* **[Howto](./ct-Bot-Software/ct-Bot-Software.md#Howto)** zum Bot
* **[Ideen & mehr](./ct-Bot-Software/ct-Bot-Software.md#Ideen-und-mehr)**
* Die Firmware für die eigene Hardware **[kalibrieren](./ct-Bot-Software/ct-Bot-Software.md#Kalibrierung)**

### c't-Sim

Dieses Teilprojekt umfasst den Java-Code für den Simulator c't-Sim

* Überblick über die **[ct-Sim Software](https://www.heise.de/ct/artikel/c-t-Bot-und-c-t-Sim-284119.html?seite=3)**
* **[Konfiguration](./ct-Sim/SimConfig.md)** der ct-Sim Optionen
* **[Howto](./ct-Sim/DokuSimulationsArchitektur)** zum ct-Sim

### Entwicklungsumgebung

* Allgemeine **[Installationsanleitung](./Installationsanleitung/InstallationsanleitungR23.md)** für c't-Bot und c't-Sim
* Entwicklungsumgebung
  * **[Eclipse-Installation](./Eclipse/EclipseInstallation.md)** inkl. der nötigen Plugins
  * **[Code aus dem Repository](./Eclipse/GITundEclipse.md)** in Eclipse einbinden
  * **[Tipps, Tricks und Hotkeys](./Eclipse/EclipseTipps.md)** rund um Eclipse
* AVR-Toolchain
  * **[Installation der AVR-Toolchain](./AVRToolchain/AVRToolchain.md)** zur Entwicklung des Steuercodes eines *realen* c't-Bots
  * **[Hintergründe](./AVRToolchain/AVRToolchainInterna.md)** zur AVR-Toolchain
  * **[AVR-Tools und Tricks](./AVRToolchain/AVRToolchain.md#Nützliche Tools für AVR)** für die (Bot-)Softwareentwicklung
  1. c't-Bot compilieren [Bot compilieren, Simulator starten und c't-Bot starten](../Installationsanleitung/InstallationsanleitungR23.md#ct-Sim-und-virtuelle-Bots-starten)
  1. Fernbedienung öffnen und Wandfolger (Taste 5) starten
