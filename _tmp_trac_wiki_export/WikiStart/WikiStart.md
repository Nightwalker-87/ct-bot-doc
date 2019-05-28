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

Zur Einstimmung gibt es in der **[Galerie](../../doc/wiki_pages/gallery.md)** Videos und Bilder rund um das Projekt.

## Anlaufstellen

Zum Projekt gibt es viel Doku, hier ein paar generelle Anlaufadressen:

1. **[c't-Artikel](../../doc/wiki_pages/ct_articles.md)**
1. Dieses **[Wiki](../WikiStart/WikiStart.md)**
1. Das **[Fan Forum zum c't-Bot](https://www.ctbot.de)**
1. Die **[Projektseite](http://www.ct-bot.de)**
1. Die **[FAQ](http://www.heise.de/ct/artikel/FAQ-fuer-c-t-Bot-und-c-t-SIM-291940.html)**
1. Das **[Heise Forum](http://www.heise.de/ct/foren/go.shtml?list=1&forum_id=89813)**
1. Die **[Ersten Schritte](../FirstSteps/FirstSteps.md)**
1. Das **[Heise Forum](https://www.heise.de/forum/c-t/Kommentare-zu-c-t-Artikeln/c-t-Bot-und-c-t-Sim/forum-23074/)** (dient als Archiv)
   * Das **[Archiv der Mailingliste](https://www.heise.de/ct/newsletter/archiv/ct-bot-entwickler/)**


## Schnelleinstieg in das Projekt

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
* Die Datenblätter für die Elektronik-Komponenten finden sich [hier](https://github.com/tsandmann/ct-bot-hw/tree/master/v1/datasheets).
* Herzstück des Funkmoduls [WiPort](http://www.lantronix.com/pdf/WiPort_UG.pdf)

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
  * **[AVR-Tools und Tricks](../AVRToolchain/AVRToolchain.md#Nützliche Tools für AVR)** für die (Bot-)Softwareentwicklung
  1. c't-Bot compilieren [Bot compilieren, Simulator starten und c't-Bot starten](../InstallationsanleitungR23/InstallationsanleitungR23.md#ct-Sim-und-virtuelle-Bots-starten)
  1. Fernbedienung öffnen und Wandfolger (Taste 5) starten

## Jagd auf den Fehlerteufel

* **[Fehlerberichte und Erweiterungsvorschläge zum c't-Bot](https://github.com/tsandmann/ct-bot/issues)**
* **[Fehlerberichte und Erweiterungsvorschläge zum c't-Sim](https://github.com/tsandmann/ct-sim/issues)**

## Leserprojekte
* Diplomarbeit mit einer [Ladestation und WLAN](http://www.db-thueringen.de/servlets/DerivateServlet/Derivate-13826/Schmidt_Diplom_ct-Bot.pdf) sowie einer guten Einführung in den c't-Bot.

# Erste Schritte mit dem c't-Bot

Vorne weg ein paar [heitere Worte](https://www.heise.de/ct/artikel/Hallo-mein-Name-ist-Benjamin-Ich-bin-suechtig-290260.html) zur Motivation und eine [Einführung](https://www.heise.de/ct/artikel/Spielgefaehrten-290274.html) in das Projekt.

Das c't-Bot-/c't-Sim-Projekt läuft schon eine ganze Weile und folglich gibt es auch eine ganze Menge an Dokumentation, Artikeln, FAQs und so weiter. Damit der Einstieg etwas leichter wird, haben wir hier ein paar nützliche Tipps und Literaturhinweise gesammelt.

## Testen/Spielen ohne Geld für Hardware auszugeben

Möchte man dem Bot eigene Kunststückchen beibringen, kommt man um die Installation der Toolchain nicht herum. Wie man den Bot programmiert haben wir bereits ausführlich beschrieben:

1. c't-Artikel: [Idee des c't-Sim](https://www.heise.de/ct/artikel/Virtuelle-Spielgefaehrten-290294.html)
1. c't-Artikel: [Interna des c't-Sim](https://www.heise.de/ct/artikel/Draengelnde-Spielgefaehrten-290334.html)
1. c't-Artikel: [Programmierung](https://www.heise.de/ct/artikel/Hohe-Schule-290392.html) des (virtuellen) c't-Bot
1. c't-Artikel: [Tutorial](https://www.heise.de/ct/artikel/Ausgang-gesucht-290460.html) für die Programmierung des c't-Bot
1. c't-Artikel: [Eigene Welten](https://www.heise.de/ct/artikel/Genesis-290480.html) für den c't-Sim
1. c't-Artikel: [Kartographie](https://www.heise.de/ct/artikel/An-der-naechsten-Ecke-links-290662.html) für den c't-Bot

## Weitere externe Dokumentation

1. Eine Bachelorarbeit zur [Entwicklung einer Bibliothek als Basis für die Programmierung und Steuerung des c't-Bots](http://users.informatik.haw-hamburg.de/~kvl/teske/bachelor_teske.pdf) der HAW Hamburg
1. Eine Diplomarbeit zur [Konzeption und Umsetzung eines Remote Engineering Praktikums für mobile Roboter](https://www.db-thueringen.de/servlets/MCRFileNodeServlet/dbt_derivate_00013826/Schmidt_Diplom_ct-Bot.pdf) der TU Ilmenau

[![License: CC BY-SA 4.0](../../License.svg)](https://creativecommons.org/licenses/by-sa/4.0/)
