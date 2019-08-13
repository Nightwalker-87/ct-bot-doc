# Die Hardware des c't-Bot

## Elektronische Bauteile

### Feldeffekt-Transistor

FET ist eine Abkürzung für "Field Effect Transistor", also Feldeffekt-Transistor.
Es handelt sich hierbei um einen unipolaren Transistor.
Beim c't-Bot werden mehrere BS250 P-Kanal FETs zum Einschalten (enable) bzw. Ausschalten (disable) von Schaltungsteilen eingesetzt.


## Schnittstellen

### Port-Erweiterung

Die Port-Erweiterung wird beim c't-Bot durch drei Schieberegister vom Typ 74HC595 realisiert.
Ein Schieberegister ist im Prinzip ein Seriell-zu-Parallel-Wandler.
Synchron zu einem Taktsignal werden die Daten seriell über einen Port vom Prozessor in das Schieberegister geschoben.
Nach Übertragung von 8 Bits liegt das Signal dann am 8-Bit Parallel-Ausgangsport an.
Während der Übertragung bleiben die Ausgangssignale durch den Ausgangs-Datenlatch des 74HC595 stabil.
Für die Auswahl (Enable) des entsprechenden Schieberegisters wird jeweils ein Mikrocontroller-Pin benötigt.

Zur Ansteuerung aller drei Schieberegister werden insgesamt 6 Mikrocontroller-Pins benötigt.

| Port | Funktion             |
| ---  | ---                  |
| PC0  | serielle Daten (SDA) |
| PC1  | serieller Takt (SCK) |
| PC2  | Enable LCD Port      |
| PC3  | Enable Enable Port   |
| PC4  | Enable LED Port      |
| PC5  | Busy Flag LCD Port   |


#### LED-Port

Auf dem c't-Bot befinden sich insgesamt 8 LEDs, die als Statusanzeigen dienen können.
Über den Port _PC4_ wird der LED-Port aktiviert (enable) oder deaktiviert (disable).
Die serielle Datenübertragung in das Schieberegister via Port _PC0_ erfolgt synchron zum Takt von _PC1_.

##### Portbelegung

| Port | Bezeichnung | Funktion           |
| ---  | ---         | ---                |
| P0   | LED1        | blau, vorne links  |
| P1   | LED2        | blau, vorne rechts |
| P2   | LED3        | rot                |
| P3   | LED4        | orange             |
| P4   | LED5        | gelb               |
| P5   | LED6        | grün               |
| P6   | LED7        | blau               |
| P7   | LED8        | weiß               |

##### Schaltbild

![Image: '01_port_led.jpg'](../images/hw_schematics_detail/01_port_led.jpg)


#### Enable-Port

Über den Enable-Port können einzelne Baugruppen (Sensoren) des c't-Bots ein- oder ausgeschaltet werden.
Durch das selektive Aktivieren von Baugruppen nach Bedarf lässt sich der Energieverbrauch des Roboters optimieren.
Über Port _PC3_ wird der Enable Port aktiviert (enable) oder deaktiviert (disable).
Die serielle Datenübertragung in das Schieberegister via Port _PC0_ erfolgt synchron zum Takt von _PC1_.


##### Portbelegung

| Port | Bezeichnung  | Funktion                                                                                                      |
| ---  | ---          | ---                                                                                                           |
| P0   | ENA_ABSTAND  | Enable Distanzsensoren (GP2D12)                                                                               |
| P1   | ENA_RADLED   | Enable der integrierten IR-LEDs in den Radencodern (CNY70)                                                    |
| P2   | ENA_SCHRANKE | Enable Lichtschranke (IS471F)                                                                                 |
| P3   | ENA_KANTLED  | Enable der integrierten IR-LEDs in den Kantensensoren (CNY70)                                                 |
| P4   | ENA_KLAPPLED | Enable der integrierten IR-LED im Klappensensor (CNY70) und der IR-LED für die Lichtschranke im Transportfach |
| P5   | ENA_MAUS     | Enable der integrierten IR-LEDs in den Liniensensoren (CNY70)                                                 |
| P6   | ENA_ERW1     | Enable Erweiterung 1                                                                                          |
| P7   | ENA_ERW2     | Enable Erweiterung 2                                                                                          |


##### Schaltbild

![Image: '02_port_enable.jpg'](../images/hw_schematics_detail/02_port_enable.jpg)


#### LCD-Port

Der c't-Bot lässt sich mit einem [LCD-Display](ct-bot_display.md) erweitern.
Über Port _PC2_ wird der LCD-Port aktiviert (enable) oder deaktiviert (disable).
Die serielle Datenübertragung in das Schieberegister via Port _PC0_ erfolgt synchron zum Takt von _PC1_.


##### Portbelegung

| Port | Bezeichnung | Funktion       |
| ---  | ---         | ---            |
| P0   | LCD1        | Datenbus Bit 0 |
| P1   | LCD2        | Datenbus Bit 1 |
| P2   | LCD3        | Datenbus Bit 2 |
| P3   | LCD4        | Datenbus Bit 3 |
| P4   | LCD5        | Datenbus Bit 4 |
| P5   | LCD6        | Datenbus Bit 5 |
| P6   | LCD7        | Datenbus Bit 6 |
| P7   | LCD8        | Datenbus Bit 7 |

Das LCD-Modul selbst wird über einen 16-poligen (2x8) Wannenstecker (ST4) angeschlossen.
Die Belegung entspricht dem üblichen Standard der meisten LCD-Module.
Über einen Jumper (BR1) kann man die Hintergrundbeleuchtung ein- bzw. ausschalten.


##### Steckerbelegung ST4

| Pin | Bezeichnung | Beschreibung                                                                              |
| --- | ---         | ---                                                                                       |
|   1 | GND         | Masse                                                                                     |
|   2 | VCC         | Spannungsversorgung +5V                                                                   |
|   3 | VEE         | Kontrast; Potentiometer 0 ... 0,5V                                                        |
|   4 | RS          | Register Select: 0 = Kommando senden; 1 = Daten schreiben                                 |
|   5 | R/W         | Display RAM: 0 = Daten schreiben; 1 = Daten lesen                                         |
|   6 | Enable      | fallende Flanke -> Übertragen des Kommandos oder der Daten; High-Pegel -> Lesen von Daten |
|   7 | DB0         | Datenbus Bit 0 LSB                                                                        |
|   8 | DB1         | Datenbus Bit 1                                                                            |
|   9 | DB2         | Datenbus Bit 2                                                                            |
|  10 | DB3         | Datenbus Bit 3                                                                            |
|  11 | DB4         | Datenbus Bit 4                                                                            |
|  12 | DB5         | Datenbus Bit 5                                                                            |
|  13 | DB6         | Datenbus Bit 6                                                                            |
|  14 | DB7         | Datenbus Bit 7 MSB                                                                        |
|  15 | GND         | Masse Hintergrundbeleuchtung                                                              |
|  16 | VCC         | Spannungsversorgung Hintergrundbeleuchtung, mit Vorwiderstand                             |


##### Schaltbild

![Image: '03_port_lcd.jpg'](../images/hw_schematics_detail/03_port_lcd.jpg)


#### Signalverlauf

![Image: 'lcd_signal_timing.jpg'](../images/hw_components/lcd_signal_timing.jpg)


**Achtung:** Im Schaltplan der Hauptplatine befindet sich ein Fehler.
Der Port _PC5_ sollte eigentlich das Busy-Flag des LCD-Moduls abfragen.
Dieses liegt aber LCD-seitig an _DB7_ (MSB) an und nicht an _DB0_ (LSB).
Aus diesem Grund ist eine Abfrage des Busy-Flags nicht möglich.
Der c't-Bot-Code verzichtet daher auf dieses Signal und arbeitet stattdessen mit Delays.


## Sensoren

### Reflex-Optokoppler (CNY70)

Der CNY70 ist ein sogenannter Reflex-Optokoppler.
Er besteht aus einer Infrarot-LED und einem Foto-Transistor, die sich beide im selben Gehäuse befinden.
Das von der Infrarot-LED emittierte Licht wird von Oberflächen die sich im Strahlengang befinden reflektiert und anschließend vom Fototransistor wieder detektiert.
Je nach der Menge des reflektierten Lichts erhöht oder reduziert sich die elektrische Leitfähigkeit des Fototransistors entsprechend.
Die Reichweite des Sensors beträgt hierbei nur wenige Millimeter.
Da das emittierte Licht der Infrarot-LED nicht gepulst wird, ist das detektierte Signal störanfällig gegenüber Fremdlichteinstrahlung.

![Image: 'CNY70.jpg'](../images/hw_components/CNY70.jpg)

Das elektrische Pinout des CNY70-Sensors findet sich im zugehörigen [Datenblatt](https://github.com/tsandmann/ct-bot-hw/blob/master/v1/datasheets/CNY70_Vishay_2012-07.pdf).

**Hinweis:** Der CNY70 Sensor im Bausatz stammt vom Hersteller Vishay.
Daneben existiert noch eine augenscheinlich baugleiche CNY70-Alternative von Temic, bei der jedoch die Pinbelegung des Fototransistors vertauscht ist!

Auf dem c't-Bot werden insgesamt 7 CNY70-Sensoren eingesetzt:

* 2 für den Liniensensor
* 2 für die Kantensensoren
* 2 für die Radencoder
* 1 für den Klappensensor des Transportfachs


#### Liniensensor

Der Liniensensor des c't-Bots wird von zwei CNY70-Sensoren gebildet, die vorne auf der Maussensor-Platine positioniert sind.
Mit den beiden Sensoren kann der Bot Linien mit einer Dicke von bis zu ??? mm erkennen, was dem mittleren Abstand der beiden Sensoren entspricht.

Die analogen Ausgangssignale der beiden CNY70 Reflex-Optokoppler sind direkt an die Ports ADC2 (_MLINKS_) und ADC3 (_MRECHTS_) des Analog-Digital-Wandlers angeschlossen.
Durch das [Enable-Signal](#Enable-Port) _ENA_MAUS_ können die Infrarot-LEDs der CNY70-Sensoren vom Mikrocontroller aus über den zugehörigen [FET](#Feldeffekt-Transistor) ein- bzw. ausgeschaltet werden.


##### Schaltbild

![Image: '04_sensor_line.jpg'](../images/hw_schematics_detail/04_sensor_line.jpg)


##### weitere Informationen

* [Aufbau eines Liniensensors mit CNY70 (kreatives-chaos.com)](http://www.kreatives-chaos.com/artikel/liniensensor-mit-cny70)


#### Kantensensoren

Die Kantensensoren des c't-Bots befinden sich auf den Sensorplatinen an der Vorderseite des Roboters.
Auf der linken und der rechten Sensorplatine ist jeweils ein CNY70-Reflex-Optokoppler installiert dessen Detektionsfläche senkrecht nach unten ausgerichtet ist.
Beide Detektoren ermöglichen es dem c't-Bot Abgründe wie Treppen oder Tischkanten zu erkennen und vor der Gefahrenstelle anzuhalten.

Die analogen Ausgangssignale _KANTEL_ (Kante links) und _KANTER_ (Kante rechts) der beiden CNY70 sind direkt an die A/D-Ports _ADC6_ und _ADC7_ des Mikrocontrollers angeschlossen.
Durch das [Enable-Signal](#Enable-Port) _ENA_KANTLED_ können die Infrarot-LEDs der CNY70-Sensoren vom Mikrocontroller aus über den zugehörigen [FET](#Feldeffekt-Transistor) ein- bzw. ausgeschaltet werden.


##### Schaltbild

![Image: '05_sensor_edge.jpg'](../images/hw_schematics_detail/05_sensor_edge.jpg)

Die Abgrunderkennung ist in der Firmware des c't-Bots als Nebenverhalten aktiviert.
Das kann bei bestimmten Untergründen dazu führen, dass der Roboter fälschlicherweise sein Fluchtverhalten aktiviert und ständig rückwärts fährt, da er die detektierte Fläche als Abgrund interpretiert.
Bei dem Verhalten der Linienverfolgung führt dieser Effekt dazu, dass der Bot stehenbleibt, wenn er mit den Kantensensoren eine Linie als Abgrund erkennt.


#### Radencoder

Mit Hilfe seiner beiden Radencoder kann der c't-Bot die zurückgelegte Wegstrecke bestimmen, eine bestimmte Strecke geradeaus fahren, sowie sich um einen bestimmten Winkel drehen.
Die Encoderscheiben, auf denen insgesamt 30 schwarze Streifen kreisförmig angeordnet sind, werden auf die Innenseite der Räder aufgeklebt.

Die Radencoder, bestehend aus zwei CNY70 Reflex-Optokopplern, sind so am Bot angebracht, das sie diese Streifen detektieren können.
Damit der Mikrocontroller diese Rohsignale einfacher verarbeiten kann, werden diese durch ein invertierendes Schmitt-Trigger-Gatter (SN74HC14) in digitale Signale umgesetzt.
Dadurch braucht der Mikrocontroller nur noch die Flankenwechsel von _HIGH_ nach _LOW_ zu zählen.

Durch das [Enable-Signal](#Enable-Port) _ENA_RADLED_ können die Infrarot-LEDs der CNY70-Sensoren vom Mikrocontroller aus über den zugehörigen [FET](#Feldeffekt-Transistor) ein- bzw. ausgeschaltet werden.

In den ersten ausgelieferten Bausätzen waren die Encoderscheiben beim Zusammenbau noch selbst zu erstellen und auf die Räder aufzukleben.
Hierzu musste die folgende Bild-Vorlage in der richtigen Skalierung (Außendurchmesser von 50 mm) mit einem Laserdrucker auf Transparentfolie gedruckt werden.

![Image: 'encoder_ring.jpg'](../images/hw_components/encoder_ring.jpg)

Anschließend waren diese Ausdrucke dann als Encoderscheiben auszuschneiden und mit transparentem Alleskleber auf die Innenseite der Aluminium-Räder aufzukleben.

Mit diesen Radencoderscheiben gab es allerdings viele Probleme, wie z.B. Fremdlichteinstreuung, unsaubere Signale und keine eindeutige High/Low-Erkennung.

Nachfolgende Versionen des Bausatzes enthielten bereits fertig zugeschnittene Encoderscheiben aus Kunststoff mit denen diese Probleme nicht mehr auftreten.
Ein besonderer Dank gilt hier dem ct-Bot-Nutzer "V2" für seinen konstruktiven Beitrag zur Lösung dieses Problems.


##### Odometrie-Verfahren zur Messung der Wegstrecke

Mithilfe des Rad Durchmessers kann somit die zurückgelegte Wegstrecke bestimmt werden.
Die Messung der zurückgelegten Wegstrecke durch Beobachtung der Räder nennt man Odometrie oder Hodometrie.

Bei diesem Verfahren wird die Anzahl der Radumdrehungen zwischen zwei Messzeitpunkten gezählt.
Zusammen mit dem Radumfang lässt sich daraus die zurückgelegte Wegdifferenz gemäß der folgenden Formel berechnen:

s = Pi * d * n

Die 30 schwarzen Streifen auf den Encoderscheiben des c't-Bot resultieren in 60 Encoderschritten pro Radumdrehung.
Da der _Raddurchmesser (Reifendurchmesser) d = 57 mm_ beträgt, legt der c't-Bot mit einer Radumdrehung eine Strecke von _U = Pi * d = 179 mm_ zurück, die dem _Reifenumfang_ entspricht.
Der zurückgelegte _Weg je Encoderschritt_ beträgt _s' = U / 60 = 2,98 mm ≈ 3 mm_ und bestimmt die Auflösung der Wegstreckenmesssung.

Der axiale Radabstand des c't-Bots beträgt 97 mm, was für weitergehende Berechnungen relevant ist.

Fehler in der Messung können u.a. dann entstehen, wenn die Räder des c't-Bots auf glattem Untergrund durchdrehen.
Aus diesem Grund hat der Roboter zusätzlich noch einen [optischen Maussensor](#Maussensor) zur Wegstreckenmesssung.
Durch die Kombination beider Messverfahren lassen sich solche Fehler eliminieren.


##### Punktdrehung um einen bestimmten Winkel

Um den c't-Bot einen bestimmten Winkel auf der Stelle drehen zu lassen, genügt es ein Rad die gewünschte Schritt-Anzahl vorwärts drehen zu lassen,
während das andere Rad die gleiche Anzahl Schritte rückwärts dreht.


##### Schaltbild

![Image: '06_sensor_encoder.jpg'](../images/hw_schematics_detail/06_sensor_encoder.jpg)


#### Klappensensor

Als Klappensensor des c't-Bots dient ein CNY70 Reflex-Optokoppler, der auf der Unterseite der Grundplatine sitzt.
Mit diesem Sensor kann der Bot erkennen ob die Klappe des [Transportfachs](#Transportfach) geöffnet oder geschlossen ist.

Das digitale Ausgangssignal _KLAPPE_ des Reflex-Optokopplers ist an den Pin _PD6_ des Mikrocontrollers angeschlossen.
Durch das [Enable-Signal](#Enable-Port) _ENA_KLAPPLED_ kann die Infrarot-LED des CNY70-Sensors vom Mikrocontroller aus über den zugehörigen [FET](#Feldeffekt-Transistor) ein- bzw. ausgeschaltet werden.


### Infrarot-Empfänger (IS471F)

#### Lichtschranke

Zur Überwachung des [Transportfachs](#Transportfach) beinhaltet dieses eine Lichtschranke.
Diese entsteht durch eine Infrarot-LED (Emitter) und einen gegenüberliegenden Infrarot-Empfänger (Detektor), die sich auf den beiden Sensorplatinen befinden.

Als Infrarot-Empfänger kommt hier der IS471F von Sharp zum Einsatz.
Dieser IC besteht aus einem Infrarot-Fototransistor, einer Auswertelogik und enthält einen Pulserzeuger für eine externe Infrarot-LED.
Durch den gepulsten Betrieb ist die Lichtschranke relativ unempfindlich gegenüber Fremdlichteinstreuung.
Das Licht der gegenüberliegenden LED wird vom Fototransistor registiert, dessen Reichweite ca. 8 cm beträgt.

Befindet sich ein Objekt im Transportfach, wird der Lichtstrahl zwischen der Emitter und dem Detektor abgeschwächt oder ganz unterbrochen.
Der Fototransistor empfängt dann ein abgeschwächtes oder gar kein Signal und die Auswertelogik schaltet in Folge den digitalen Ausgang ab einer bestimmten Schwelle auf _LOW_.

Das digitale Ausgangssignal _SCHRANKE_ des IS471F ist an den Port _PB0_ des Mikrocontrollers angeschlossen.
Durch das [Enable-Signal](#Enable-Port) _ENA_SCHRANKE_ kann der IS471F vom Mikrocontroller aus über den zugehörigen [FET](#Feldeffekt-Transistor) ein- bzw. ausgeschaltet werden.
Das Enable-Signal _ENA_KLAPPLED_ schaltet neben dem Klappensensor auch die Infrarot-LED der Lichtschranke ein bzw. aus.


##### Schaltbild

![Image: '07_sensor_door_barrier.jpg'](../images/hw_schematics_detail/07_sensor_door_barrier.jpg)


### LDR-Widerstände (MPY54C569)

Der c't-Bot enthält vorne links und rechts auf der Grundplatine zwei Lichtsensoren für die jeweils ein LDR-Fotowiderstand vom Typ MPY54C569 verwendet wird.
Die Abkürzung LDR steht für "Light Dependent Resistor", also lichtempfindlicher Widerstand.
Ein solcher Widerstand ändert seinen Widerstandswert abhängig von der Intensität des einfallenden Lichts.
Im Elektronikdesign des c't-Bot bildet jeder LDR-Widerstand zusammen mit einem 470 kΩ Widerstand einen Spannungsteiler.
Hierbei ist der LDR der Widerstand unter Teilspannungsabfall, sodass das Ausgangssignal für diese Schaltung antiproportional zur detektierten Helligkeit ist.

Dank der beiden Lichtsensoren kann Roboter Verhaltensmuster prägen, wie z.B. einer Lichtquelle zu folgen (Motte) oder davor zu flüchten (Kakerlake).

Da die Fotowiderstände relativ nahe an den beiden vorderen blauen LEDs platziert sind, kann es zu unerwünschter Lichteinstreuung auf die Sensoren kommen.
Mögliche Lösungen hierfür sind die benachbarten LEDs mit Schrumpfschlauch bzw. einer lichtundurchlässigen Hülse zur Seite hin abzuschirmen oder die LDRs von der Unterseite der Grundplatine einzulöten.

Die analogen Ausgangssignale der beiden LDR-Spannungsteiler _LDRL_ (linker LDR) und _LDRR_ (rechter LDR) sind direkt an die Ports _ADC3_ bzw. _ADC4_ des Analog-Digital-Wandlers angeschlossen.


##### Schaltbild

![Image: '08_sensor_brightness.jpg'](../images/hw_schematics_detail/08_sensor_brightness.jpg)


##### weitere Informationen

* [LDR-Fotowiderstand (Elektronik-Kompendium.de)](https://www.elektronik-kompendium.de/sites/bau/0110301.htm)

### Maussensor (ADNS-2610)

(TBC)

------

Die Transportklappe selbst wird durch einen Servo-Motor betätigt.

------

[![License: CC BY-SA 4.0](../../LICENSE.svg)](https://creativecommons.org/licenses/by-sa/4.0/)

Autoren: Marvin, V2, Nightwalker-87
