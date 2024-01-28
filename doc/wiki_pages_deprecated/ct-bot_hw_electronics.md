# Die Elektronik des c't-Bot

## Elektronische Bauteile

### AVR-Mikrocontroller

'''AVR''' ist eine 8-Bit-RISC-Mikrorozessor-Familie des Halbleiter-Herstellers Microchip.
Bis zur Übernahme durch Microchip wurde das zugehörige Produktspektrum vom Chip-Hersteller Atmel geführt.
Ähnlich wie die Produktserie der PIC-Mikrocontroller von Microchip erfreut sich auch die AVR-Familie einer großen Beliebtheit, die auch weit in den Hobby- und semi-professionellen Bereich hinein reicht.

Die große Beliebtheit der AVRs ergibt sich u.a. aus ihrer einfachen Handhabung.
Fast alle Typen können über eine sogenannte ISP-Schnittstelle (AVR ISP) programmiert werden.
Bei einem solchen In-System Programmer handelt es sich um einen Programmieradapter welcher an die serielle, parallele oder USB-Schnittstelle eines PCs angeschlossen wird.
Die Besonderheit liegt hierbei in der Möglichkeit, den Mikrocontroller nicht aus der Zielschaltung herausnehmen zu müssen, um ihn zu programmieren.
Neuere Controller-Typen besitzen darüber hinaus noch eine JTAG-Schnittstelle, über die man den IC-Baustein nach dem IEEE-Standard 1149.1 debuggen kann.


### RISC-Architektur

RISC ist eine Abkürzung für "**R**educed **I**nstruction **S**et **C**omputing" und beschreibt eine Prozessor-Architektur. Übersetzt bedeutet dies in etwa "Rechnen mit reduziertem Befehlssatz". Beispiele für RISC-Prozessoren sind Microchip AVR sowie MIPS.
Ein Vorteil gegenüber anderen Mikroprozessor-Familien ist, dass sich dank der RISC-Architektur die meisten Befehle auf Registern innerhalb eines Systemtakts abarbeiten lassen, was in einer höhere Rechengeschwindigkeit gegenüber anderen Architekturen resultiert.
Hiervon ausgenommen sind Sprung- und Multiplikationsbefehle, sowie Zugriffe auf das Speicherinterface (u.a. RAM und I/O-Ports).

Durch das auf Hochsprachen wie C ausgelegte Hardware-Design können auch Compiler sehr effizienten Code erzeugen, sodass man sich hierfür nicht mehr unbedingt auf Assembler-Ebene begeben muss.


### Speicherarchitektur

Das Speicher-Management folgt den Richtlinien der Harvard-Architektur.
Es gibt also getrennte Adressräume für den Flash-Speicher, das RAM und das EEPROM.
Im Gegensatz zu einfacheren Mikrocontrollern besitzen die AVRs 32 Register, mit welchen direkt Operationen ausgeführt werden können.
Ein umständliches Verschieben von Werten aus dem RAM, um dann mit ihnen Operationen durchführen zu können, entfällt hiermit.


### Befehlssatz

Im Gegensatz zu den PICmicro-Mikrocontrollern wurde der AVR-Befehlssatz, abgesehen von wenigen Ausnahmen wie beispielsweise dem AT90S1200 mit eingeschränktem und der ATmega-Serie mit erweitertem Befehlssatz, weitestgehend über alle Modelle kompatibel gehalten.

| Modell               | Anzahl der Befehle |
| -------------------- | ------------------ |
| AT90S1200            | 52                 |
| AT90xxxx ("Classic") | 62                 |
| ATtiny               | bis 123            |
| ATMega               | 130 - 135          |

Die AVR-Prozessoren sind für die effiziente Ausführung von kompiliertem C-Code konzipiert worden.
Um Optimierungspotentiale zu erkennen, wurde noch vor Fertigstellung des AVR-Kerns mit der Entwicklung eines C-Compilers begonnen.

So wurde die Instruktion "Addition mit direktem Parameter" (''add immediate'') entfernt, weil anstatt dieser Instruktion ebenso gut der Befehl "Subtrahiere direkt" (''subtract immediate'') mit dem Komplement verwendet werden kann.

Der dadurch auf dem Silizium frei werdende Platz wurde dann zum Realisieren einer "Addition mit direktem 16-Bit-Parameter" (''add immediate word'') frei.
Ein Befehl "Vergleich mit Carry-Flag" (''compare with carry'') wurde eingeführt, um einen effizienten Vergleich von 16- und 32-Bit-Werten zu ermöglichen, wie er in Hochsprachen üblich ist.
Anstatt zwei Adressregistern wurden drei Adressregister vorgesehen und auf ein anfangs geplantes segmentiertes Speicher-Layout komplett verzichtet, weil dieses nur schwer von Compilern zu handhaben ist.


### ATmega32, ATmega644 und ATmega1284

Der ATmega32 Mikrocontroller bildet das Herzstück der Steuerung des c't-Bots.
Zum Zeitpunkt der Entwicklung des c't-Bots war er mit seinen 32 Ein-und Ausgängen und 32 kB Flash Speicher der leistungsfähigste Mikrocontroller (MCU)aus der AVR Reihe in einem Standard-DIL Gehäuse.

Ab Ende 2006 wurde dessen Grunddesign um die pin-kompatiblen Mikrocontroller ATmega644 oder ATmega1284 erweitert.
Diese Modelle zeichnen sich durch einen erweiterten Funktionsumfang aus (u.a. größerer Flash-Speicher & Interrupt-fähige I/O-Ports).

Die wichtigsten Eigenschaften des ATmega32/644/1284P im Überblick:

* 32 / **64** / **128** kByte internes Flash-Memory, bis zu 10000 Schreib/Lösch Zyklen
* 1024 / **2048** Byte EEPROM, bis zu 100000 Schreib/Lösch Zyklen
* 2048 / **4096** Byte SRAM
* bis zu 32 programmierbare I/O Ports, **interruptfähig**
* 8 10-bit AD-Wandler
* 1 Analog Komparator
* USART, JTAG, ISP, SPI und I2C(TWI) Schnittstelle
* 2 8-bit und 1 16-bit Timer
* 4 PWM Ausgänge / **6 PWM Ausgänge**
* 16 MIPS bei 16MHz Takt / **20 MIPS bei 20MHz Takt**

Unterschiede gegenüber dem ATmega32 sind **fett** hervorgeboben.

Aufgrund der Pinkompatibilität und der Unterstützung durch den Programmcode, können letztere MCU-Modelle als Ersatztypen für den ATmega32 verwendet werden.
Dafür ist lediglich eine Compiler- **und** Linker-Einstellung im Projekt anzupassen.
Konkret muss hier jeweils die Ziel-CPU `mmcu=*` von `mega32` auf `mega644` bzw. `mega128P` geändert werden.

Trotz der relativ großen Anzahl von Ports sind alle Ports des Microcontrollers belegt. Deshalb werden über Schieberegister noch drei 8-Bit [Port-Erweiterungen](#I/O-Erweiterung) angebunden. Dort sind die LEDs und die Enable-Leitungen für die einzelnen Baugruppen angebunden. Über den dritten Erweiterungsport kann optional ein [LCD-Display-Modul](ct-bot_display#LCD-Display-Modul für den c't-Bot) angeschlossen werden.

Die MCU führt das Steuer-Programm für den c't-Bot aus über das die Sensoren abgefragt sowie die Aktoren (Motoren, LEDs, Servos) gesteuert werden.
Außerdem übernimmt der Microcontroller noch die Kommunikation mit dem PC oder anderen c't-Bots.


#### Schaltbild

![Image: '15_ic_ATmega32.jpg'](../images/hw_schematics_detail/15_ic_ATmega32.jpg)


#### Portbelegung

| Port | Pin | I/O       | Funktion | Bemerkungen                                                         |
| ---- | --- | --------- | -------- | ------------------------------------------------------------------- |
| PB0  | 1   | XCK/T0    | SCHRANKE | [Lichtschranke](ct-bot_hw_sensors#Lichtschranke)                    |
| PB1  | 2   | T1        | FERNBED  | Fernbedienung (Infrarot Empfänger)                                  |
| PB2  | 3   | INT2/AIN0 | FEHLER   | Spannungsüberwachung                                                |
| PB3  | 4   | OC0/AIN1  | PWM0     | Geschwindigkeit & Richtung [Servo](ct-bot_hw_actuators#Servo) 1     |
| PB4  | 5   | /SS       | RADL     | [Radencoder links](ct-bot_hw_sensors#Radencoder)                    |
| PB5  | 6   | MOSI      | MOSI     | ISP, Maussensor                                                     |
| PB6  | 7   | MISO      | MISO     | ISP, Maussensor                                                     |
| PB7  | 8   | SCK       | SCLK     | ISP, Maussensor                                                     |
| PD0  | 14  | RXD       | RXD      | [UART Receive](#UART)                                               |
| PD1  | 15  | TXD       | TXD      | [UART Transmit](#UART)                                              |
| PD2  | 16  | INT0      | CTS      | [UART Clear to Send](#UART)                                         |
| PD3  | 17  | INT1      | RADR     | [Radencoder rechts](ct-bot_hw_sensors#Radencoder)                   |
| PD4  | 18  | OC1B      | PWM1B    | Geschwindigkeit [Motor](ct-bot_hw_actuators#Motoren) Links          |
| PD5  | 19  | OC1A      | PWM1A    | Geschwindigkeit [Motor](ct-bot_hw_actuators#Motoren) Rechts         |
| PD6  | 20  | ICP1      | KLAPPE   | [Klappensensor](ct-bot_hw_sensors#Klappensensor)                    |
| PD7  | 21  | OC2       | PWM2     | Geschwindigkeit & Richtung [Servo](ct-bot_hw_actuators#Servo) 2     |
| PA0  | 40  | ADC0      | ABSTL    | [Distanzsensor](ct-bot_hw_sensors#Distanzsensoren_(GP2D12)) links   |
| PA1  | 39  | ADC1      | ABSTR    | [Distanzsensor](ct-bot_hw_sensors#Distanzsensoren_(GP2D12)) rechts  |
| PA2  | 38  | ADC2      | MLINKS   | [Liniensensor](ct-bot_hw_sensors#CNY70) links                       |
| PA3  | 37  | ADC3      | MRECHTS  | [Liniensensor](ct-bot_hw_sensors#CNY70) rechts                      |
| PA4  | 36  | ADC4      | LDRL     | [Lichtsensor](ct-bot_hw_sensors#LDR-Widerstände_(MPY54C569)) links  |
| PA5  | 35  | ADC5      | LDRR     | [Lichtsensor](ct-bot_hw_sensors#LDR-Widerstände_(MPY54C569)) rechts |
| PA6  | 34  | ADC6      | KANTEL   | [Kantensensoren](ct-bot_hw_sensors#CNY70) links                     |
| PA7  | 33  | ADC7      | KANTER   | [Kantensensoren](ct-bot_hw_sensors#CNY70) rechts                    |
| PC0  | 22  | SCL       | PC0      | [Erweiterungsport](#I/O-Erweiterung)(LED-, LCD-, Enable- Port)      |
| PC1  | 23  | SDA       | PC1      | [Erweiterungsport](#I/O-Erweiterung)(LED-, LCD-, Enable- Port)      |
| PC2  | 24  | TCK       | PC2      | [Erweiterungsport](#I/O-Erweiterung) (LCD Port)                     |
| PC3  | 25  | TMS       | PC3      | [Erweiterungsport](#I/O-Erweiterung) (Enable Port)                  |
| PC4  | 26  | TDO       | PC4      | [Erweiterungsport](#I/O-Erweiterung) (LED Port)                     |
| PC5  | 27  | TDI       | PC5      | [Erweiterungsport](#I/O-Erweiterung) (LCD Port Busy-Flag)           |
| PC6  | 28  | TOSC1     | PC6      | Richtung [Motor](ct-bot_hw_actuators#Motoren) links                 |
| PC7  | 29  | TOSC2     | PC7      | Richtung [Motor](ct-bot_hw_actuators#Motoren) rechts                |


### Feldeffekt-Transistor

FET ist eine Abkürzung für "Field Effect Transistor", also Feldeffekt-Transistor.
Es handelt sich hierbei um einen unipolaren Transistor.
Beim c't-Bot werden mehrere BS250 P-Kanal FETs zum Einschalten (enable) bzw. Ausschalten (disable) von Schaltungsteilen eingesetzt.


### Motortreiber L293D

Der Antrieb des c't-Bot besteht aus zwei DC-Getriebemotoren der Firma Faulhaber.
Da der [Mikrocontroller](#AVR-Mikrocontroller) diese Motoren nicht direkt ansteuern kann, wird ein sogenannter Motor Treiber benötigt.
Das ist in diesem Falle der L293D.

Dieser Baustein beinhaltet vier Halb-H-Brücken Treiber und ist ein gängiger Motortreiber-IC für zwei Getriebemotoren bzw. einen Schrittmotor. Damit lassen sich zwei DC-Motoren bidirektional betreiben (als 2-fach H-Brücke), oder ein Schrittmotor birektional. Die Belastbarkeit pro Halbbrücke beträgt 600 mA. Im Gegensatz zum pin-kompatiblen L293 und dem großen Bruder L298 beinhaltet der L293D interne Freilaufdioden. Diesen schützen den IC vor vom Motor ausgehenden Spannungsspitzen.

Angesteuert wird der L293D durch vier Ausgangssignale des Mikrocontrollers.

Die wichtigsten Eigenschaften des L293D im Überblick:

* Großer Spannungsbereich von 4,5 - 36 V
* serarate Eingangs-Logik Spannungsversorgung (z.B. TTL-Pegel kompatibel)
* interner ESD Schutz
* automatische Abschaltung bei Übertemperatur
* Ausgangsstrom 500 mA pro Kanal
* kurzeitige Spitzen Strom bis zu 1,2 A je Kanal
* integrierte Freilaufdioden
* _Nachteil_: Hohe Ruhestromaufnahme (> 50 mA)


#### Drehrichtung & Geschwindigkeit

Die beiden Eingangssignale PC6 und PC7 bestimmen die Richtung, in die die Motoren laufen.
Das einzelne Richtungs-Signal vom Mikrocontroller wird dazu über ein invertierendes Gatter dem L293D zugeführt.

Die beiden Eingangssignale PWM1A und PWM1B bestimmen die Geschwindigkeit, mit der die Motoren laufen.
Am Enable Eingang des L293D liegt ein sogenanntes Pulsweitenmoduliertes (PWM) Signal. Dieses PWM Signal kann der Mikrocontroller mithilfe seiner Timer selbstständig erzeugen. Vom Programm her muss nur noch das Verhältnis zwischen Signal und Signalpause konfiguriert werden. Damit wird die Geschwindigkeit des Motors geregelt.


#### Schaltbild

![Image: '14_ic_L293D.jpg'](../images/hw_schematics_detail/14_ic_L293D.jpg)

**Achtung:**: Nach Einschalten des c't-Bots, bzw. während eines Resets (z.B. beim Flashen), drehen beide Motoren mit voller Kraft, sodass sich der Bot im Kreis dreht. Grund hierfür ist, dass das während der Bootphase und solange das Reset Signal auf Low liegt, alle Ports des Mikrocontrollers auf Input geschaltet sind. Deshalb liegen auch die beiden Enable Ports am Motortreiber auf HIGH Pegel, und damit drehen die Motoren. Abhilfe schafft hier ein Hardware Patch durch den die beiden Enable Ports mit Pulldown Widerständen nach LOW gezogen werden. Somit bleiben die Motoren während der Bootphase bzw. bei einem Reset ausgeschaltet.

Die Pinbelegung und ein Blockdiagramm des L293D findet sich im zugehörigen [Datenblatt](https://github.com/tsandmann/ct-bot-hw/blob/master/v1/datasheets/L293D_ST_2003-07.pdf).


## Schnittstellen

### I/O-Erweiterung

Die I/O-Erweiterung wird beim c't-Bot durch drei Schieberegister vom Typ 74HC595 (Seriell-Parallel-Wandler) realisiert.
Synchron zu einem Taktsignal werden die Daten seriell vom Prozessor in das Schieberegister übertragen.
Nach Übertragung von 8 Bit kann das Signal dann am 8-Bit Parallel-Ausgangsport ausgegeben werden.
Während der Übertragung bleiben die Ausgangssignale durch den Ausgangslatch des 74HC595 stabil.

Zur Ansteuerung der drei Schieberegister werden insgesamt fünf Mikrocontroller-Pins benötigt.

| Pin | Funktion                                                        |
| --- | --------------------------------------------------------------- |
| PC0 | Serielle Daten                                                  |
| PC1 | Takt für Storage Register (LED & ENA) bzw. Shift Register (LCD) |
| PC2 | Takt für Storage Register LCD                                   |
| PC3 | Takt für Shift Register ENA                                     |
| PC4 | Takt für Shift Register LED                                     |


#### LEDs

Auf dem c't-Bot befinden sich insgesamt 8 LEDs, die als Statusanzeigen dienen können.
Die serielle Datenübertragung in das Schieberegister via Pin _PC0_ erfolgt synchron zum Takt von _PC4_.


##### Portbelegung

| Port | Bezeichnung | Funktion           |
| ---- | ----------- | ------------------ |
| Q0   | LED1        | blau, vorne links  |
| Q1   | LED2        | blau, vorne rechts |
| Q2   | LED3        | rot                |
| Q3   | LED4        | orange             |
| Q4   | LED5        | gelb               |
| Q5   | LED6        | grün               |
| Q6   | LED7        | blau               |
| Q7   | LED8        | weiß               |


##### Schaltbild

![Image: '01_port_led.jpg'](../images/hw_schematics_detail/01_port_led.jpg)


#### Enable-Signale

Über die Enable-Signale können einzelne Baugruppen (Sensoren) des c't-Bots ein- oder ausgeschaltet werden.
Durch das selektive Aktivieren von Baugruppen nach Bedarf lässt sich der Energieverbrauch des Roboters optimieren.
Die serielle Datenübertragung in das Schieberegister via Pin _PC0_ erfolgt synchron zum Takt von _PC3_.


##### Portbelegung

| Port | Bezeichnung      | Funktion                                                                                                      |
| ---- | ---------------- | ------------------------------------------------------------------------------------------------------------- |
| Q0   | ENA_ABSTAND      | Enable der Distanzsensoren (GP2D12)                                                                           |
| Q1   | ENA_RADLED       | Enable der integrierten IR-LEDs in den Radencodern (CNY70)                                                    |
| Q2   | ENA_SCHRANKE     | Enable der Lichtschranke (IS471F)                                                                             |
| Q3   | ENA_KANTLED      | Enable der integrierten IR-LEDs in den Kantensensoren (CNY70)                                                 |
| Q4   | ENA_KLAPPLED     | Enable der integrierten IR-LED im Klappensensor (CNY70) und der IR-LED für die Lichtschranke im Transportfach |
| Q5   | ENA_LINE         | Enable der integrierten IR-LEDs in den Liniensensoren (CNY70)                                                 |
| Q6   | ENA_MMC          | Enable Erweiterung 1 oder Chip-Select für MMC, falls Erweiterungsboard vorhanden                              |
| Q7   | ENA_MOUSE_SENSOR | Enable Erweiterung 2 oder Chip-Select für Maussensor, falls Erweiterungsboard vorhanden                       |


##### Schaltbild

![Image: '02_port_enable.jpg'](../images/hw_schematics_detail/02_port_enable.jpg)


#### LCD

Der c't-Bot lässt sich mit einem [LC-Display](ct-bot_display.md) erweitern.
Die serielle Datenübertragung in das Schieberegister via Pin _PC0_ erfolgt synchron zum Takt von _PC1_.
Über Port PC2 wird der LCD Port enabled/disabled.


##### Portbelegung

| Port | Funktion       |
| ---- | -------------- |
| Q0   | Datenbus Bit 0 |
| Q1   | Datenbus Bit 1 |
| Q2   | Datenbus Bit 2 |
| Q3   | Datenbus Bit 3 |
| Q4   | Datenbus Bit 4 |
| Q5   | Datenbus Bit 5 |
| Q6   | Datenbus Bit 6 |
| Q7   | Datenbus Bit 7 |

Das LCD-Modul selbst wird über einen 16-poligen (2x8) Wannenstecker (ST4) angeschlossen.
Die Belegung entspricht dem üblichen Standard der meisten LCD-Module.
Über einen Jumper (BR1) kann man die Hintergrundbeleuchtung ein- bzw. ausschalten.


##### Steckerbelegung ST4

| Pin | Bezeichnung | Beschreibung                                                                              |
| --- | ----------- | ----------------------------------------------------------------------------------------- |
| 1   | GND         | Masse                                                                                     |
| 2   | VCC         | Spannungsversorgung +5V                                                                   |
| 3   | VEE         | Displayspannung (Kontrast) 0 ... 1,5V                                                     |
| 4   | RS          | Register Select: 0 = Kommando senden; 1 = Daten schreiben                                 |
| 5   | R/W         | Auswahl Lese-/Schreibmodus: 0 = Daten schreiben; 1 = Daten lesen                          |
| 6   | Enable      | Steigende Flanke: Einlesen von RS und R/W. Fallende Flanke: Einlesen / Schreiben Datenbus |
| 7   | DB0         | Datenbus Bit 0 LSB                                                                        |
| 8   | DB1         | Datenbus Bit 1                                                                            |
| 9   | DB2         | Datenbus Bit 2                                                                            |
| 10  | DB3         | Datenbus Bit 3                                                                            |
| 11  | DB4         | Datenbus Bit 4                                                                            |
| 12  | DB5         | Datenbus Bit 5                                                                            |
| 13  | DB6         | Datenbus Bit 6                                                                            |
| 14  | DB7         | Datenbus Bit 7 MSB                                                                        |
| 15  | GND         | Masse Hintergrundbeleuchtung                                                              |
| 16  | VCC         | Spannungsversorgung Hintergrundbeleuchtung (interner Vorwiderstand vorhanden)             |


##### Schaltbild

![Image: '03_port_lcd.jpg'](../images/hw_schematics_detail/03_port_lcd.jpg)


#### Signalverlauf

![Image: 'lcd_signal_timing.jpg'](../images/hw_components/lcd_signal_timing.jpg)

**Achtung:** Im Schaltplan der Hauptplatine befindet sich ein Fehler.
Der Pin _PC5_ sollte eigentlich das Busy-Flag des LCD-Moduls abfragen.
Dieses liegt aber LCD-seitig an _DB7_ (MSB) an und nicht an _DB0_ (LSB), weshalb eine Abfrage des Busy-Flags nicht möglich ist.
Der c't-Bot-Code verzichtet aber ohnehin auf dieses Signal und arbeitet stattdessen mit Delays.


### I²C-Bus

'''I<sup>2</sup>C''': Ein von Philips entwickelter serieller Kommunikationsbus. I<sup>2</sup>C wird "''I-Quadrat-C''" bzw. "''I-square-C''" ausgesprochen und bedeuted "'''''I'''nter-'''I'''ntegrated '''C'''ircuit''". Der I<sup>2</sup>C Bus ist ein 2-Draht-Bus, d.h. es werden lediglich 2 Prozessor Ports benötigt, SDA (Data) und SCL (Clock). Der  maximale Datentakt beträgt 100kHz im Standard Mode, bzw. 400kHz im Fast Mode. Der AVR unterstützt I<sup>2</sup>C per Hardware durch sein TWI-Interface. TWI bedeutet "'''''T'''wo '''W'''ire '''I'''nterface''" und ist die Bezeichnung von Atmel für I2C.


### SPI-Bus

'''SPI''': Ein von der Firma [http://www.motorola.com Motorola] entwickleter synchroner serieller Bus. SPI ist eine Abkürzung für ''"'''S'''erial '''P'''eripheral '''I'''nterface"''. Es werden mind. 3 Ports benötigt, SDO (Data Out) bzw MOSI, SDI (Data In) bzw. MISO und SCLK (Datentakt) und ggf. ein oder mehrere Chip Select Signale.


### UART

'''UART''': [[UART]] nennt man ein Kommunikationsmodul eines Prozessors. UART ist eine Abkürzung für ''&quot;'''U'''niversal '''A'''synchron '''R'''eceiver '''T'''ransmitter&quot;''. Übersetzt bedeutet das Universeller asynchroner Empfänger und Sender. Die Datenübertragung erfolgt seriell. Asnchron bedeutet, es wird kein Takt mitübertragen, Der Empfänger muß anhand der Daten den Takt rückgewinnen. Typische Anwendung einer UART ist z.B. die RS232 Schnittstelle.

----

=== ISP ===
Programmierschnittstelle für Prozessoren. ISP ist eine Abkürzung für ''&quot;'''I'''n '''S'''ystem '''P'''rogramming&quot;'' oder ''&quot;'''I'''n '''S'''ystem '''P'''rogrammer&quot;''. Durch eine relativ einfache Zusatzhardware ist es möglich, den Mikrocontrollers im System (d.h. auf der Platine) zu programmieren.

=== USB ===
USB ist eine Abkürzung für ''&quot;'''U'''niversal '''S'''erial '''B'''us&quot;''. Ein Bussystem zur Anbindung von Peripherie Geräten an einen Computer. USB ersetzt nach und nach ältere Schnittstellen und Bussysteme wie RS232, LPT. Siehe auch [[USB-Modul]].


== Stromversorgung ==

Für die Stromversorgung des ct-bot sind zwei über SW2 wählbare Alternativen vorgesehen:

'''A:''' POWER1 (U-Bat): '''Akkupack 5x1,2V''' Mignon Akku (AA), eingespeist über Stiftleiste ST1. Marktübliche Kapazität z.Zt.(2/06) max. ca. 2,5Ah. (Bei '''Bestückung mit Batterien''' sollte die '''Anzahl auf 4 begrenzt''' werden, max 6,25V!) [http://www.ctbot.de/index.php?page=5&smartor_mode=album_showpage&pic_id=141 Batteriehalter]; [http://www.ctbot.de/index.php?page=5&smartor_mode=album_showpage&pic_id=28 Batteriehalter Montage]

'''B:''' POWER2 (U-Netz): '''Netzteil 6V Gleichspannung''', eingespeist über DCBU2, 1-PR (der in der Buchse integrierte Schalter bleibt als Akku/Netzteil-Umschalter ungenutzt, statt dessen hat ct, unnötigerweise als zusätzliches  Bauteil, den Umschalter SW2 vorgesehen).
Der Minuspol beider Quellen ist auf die gemeinsame Masse gelegt, der Pluspol über den Versorgungswechsler SW SPDT und die Verpolschutzdiode D3 an folgende Komponenten:

* zur '''Versorgung mit geregelten 5V,  maximal 1,5A Belastbarkeit''', an den '''Low Drop Spannungswandler''' [http://www.st.com/stonline/products/literature/ds/2141/l4940xx5.pdf L4940V5], dessen Ausgang über C5 mit 100μF(25V) geblockt ist und danach für Prozessor und die gesamte Glue-Logik verwendet wird.
'''Achtung Patch!!!''' Bei sporadischen, unerwarteten Resets hat sich bei einigen Usern hier ein [http://www.ctbot.de/index.php?page=5&smartor_mode=album_showpage&pic_id=138[ein 100nF Kondensator parallel zu C5 bewährt.]
* '''Leistungseingang der Motortreiber''' [http://www.st.com/stonline/books/pdf/docs/1330.pdf L293D]
* '''J3 für Erweiterungskomponenten''' (diesen stehen, an Pin2, sowohl die ungeregelte 6V-Versorgung als auch, an Pin1, die geregelten 5V zur Verfügung).
* zum '''Schutz vor Tiefentladung''', über Spannungsteiler R31/R32, an den nicht invertierenden Komparatoreingang eines LM311, der sie mit der Zenerspannung von 2,4V vergleicht und bei Unterschreiten ein Fehlersignal auslöst. Dies entspricht einem Unterschreiten der Akku- oder Netzteilspannung von ca. 5,5 bis 5,6V.
* als '''Versorgung der Servos''', über R28, jeweils an Pin 1 von J1+J2 .
* und, zur '''Indikation einer klemmenden Transportklappe''', ebenfalls über R28 an den nicht invertierenden Komparatoreingang eines weiteren LM311. Dieser vergleicht die, um den Spannungsabfall an R28 reduzierte, Versorgungsspannung mit der, über Spannungsteiler R34/R30 anliegenden, Referenzspannung von 4,5V und löst bei Unterschreiten ebenfalls einen Fehler aus.

Zu 5.: Das ist keine Notbremse, wie in den ctBot-Foren vermutet, sondern tritt ein wenn die Transportklappe klemmt und dadurch der Servostrom wesentlich höher als der Leerlaufstrom ist.
Servospezifikation: "Leerlauf" (100mA); "voll abgebremst" (300mA).

Bei vollen Akkus (6,25V) wird der Fehler bei (6,25V - 4,5V)/6,8 Ohm = 257mA und bei leeren Akkus(5,5V) bei (5,5V - 4,5V)/6,8 Ohm = 147mA ausgelöst.

R28 muß so klein bleiben, daß der Spannungsabfall im Leerlauf der Servos noch nicht zum Unterschreiten der 4,5V ausreicht.

Dieser Indikator soll mit einer Auswertung der Klappen-Lichtschranke kombiniert werden um, z.B. im Fehlerfall, den Servo nur noch langsam anzusteuern und dabei den Strom zu überwachen. Durch diesen frühen Hinweis, "daß vielleicht etwas nicht stimmt", soll vermieden werden, "mit Volldampf in die Überlast" zu fahren und erst danach abzuschalten.

R34 könnte man laut Thorsten Thiele auch an die Batteriespannung hängen. Die aktuelle Schaltung habe aber den Vorteil des einfacheren Routings.

Die Fehlersignale aus 3) und 5) stehen (leider) verodert dem µC zur Verfügung.

(z.T. zitiert aus einer  Mail [Re: debatte schaltungsdetails] Thorsten Thieles aus dem ct-Forum vom 9. Januar 2006 15:01)

* [http://www.st.com/stonline/products/literature/ds/4848/lm311.pdf Datenblatt Komparator LM311]

----

### Schaltbild

![Image: '13_powersupply.jpg'](../images/hw_schematics_detail/13_powersupply.jpg)

[![License: CC BY-SA 4.0](../../LICENSE.svg)](https://creativecommons.org/licenses/by-sa/4.0/)

Autoren: Peter Recktenwald, Lomdar67, Noxon, Nightwalker-87, Mkosch, Marvin, Salü

--------

== Weblinks ==

* [https://www.mikrocontroller.net/articles/AVR Mikrocontroller.net Artikelsammlung - AVR]
* [http://www.roboternetz.de/wissen/index.php/ATMega32 Roboternetz Wissen - ATmega32]
* [http://www.nongnu.org/avr-libc/ AVR-Port der C-Standardbibliothek]
* [http://winavr.sourceforge.net/ GNU C/C++-Cross-Compiler (Windowsversion)]
* [http://cdk4avr.sourceforge.net/ GNU C/C++-Cross-Compiler (Linuxversion)]
* [http://www.e-lab.de/ AVRco Embedded Pascal Compiler (Windows)]
* [http://www.roboternetz.de/wissen/index.php/Getriebemotoren_Ansteuerung Roboternetz Wissen - Getriebemotoren Ansteuerung]

Weiterhin existiert eine Vielzahl freier Entwicklungswerkzeuge, wie z.B. die für AVR-Cross-Compiling portierten GNU-Tools.
