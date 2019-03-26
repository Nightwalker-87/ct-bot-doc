# Die Hardware des c't-Bot

>> **Trac-2-Markdown Konvertierung:** *unchecked*

## Schnellstart

Erst einmal ein weniger schnuppern während der Lötkolben vorheizt? Dann helfen die **[ersten Schritte](../FirstSteps/FirstSteps.md)** -- auch wenn die Teile für den realen Bot noch gar nicht da sind.

## Aufbau und Montage

Zu allererst hilft hier leider gar nichts außer das Lesen dieser **beiden** Artikel:

* c't-Artikel: **[Aufbau des c't-Bot](https://www.heise.de/ct/artikel/Hallo-Welt-290314.html)**
* Aufbauanleitung der **[Basisversion](../ct-Bot-Aufbau/ct-Bot-Aufbau.md)** mit Fotos

Wenn es dann doch mal klemmt:

* c't-Artikel: **[Fehlersuche](https://www.heise.de/ct/artikel/Kammerjaeger-290506.html)** an der Hardware des c't-Bot
* **[FAQ](https://www.heise.de/ct/artikel/FAQ-fuer-c-t-Bot-und-c-t-SIM-291940.html)-Einträge**
* Das **[Forum](https://www.ctbot.de)**
* Das **[Archiv der Mailingliste](https://www.heise.de/ct/newsletter/archiv/ct-bot-entwickler/)**
* **Direkter Kontakt** über:
  * das Matrix-Netzwerk mit **[Riot.im](https://riot.im/app/#/room/#ctbot:matrix.org)** (auch als Gast ohne Registrierung nutzbar)
  * oder **[Slack](https://ct-bot-slack.herokuapp.com)**

Beim Aufbau lohnt es, ein paar Modifikationen gleich mit einzubauen

* Empfehlenswerte **[Hardware-Modifikationen](../ct-Bot-Modifikationen/ct-Bot-Modifikationen.md)**

Ist die Hardware soweit fertig, muss die Firmware auf den Bot:

* Software in den c't-Bot **[flashen](../Flash/Flash.md)**
* **[Programmieradapter](http://www.heise.de/ct/Redaktion/cm/klangcomputer/index1.htm)** (Achtung, diese Beschreibung des Adapters entstammt dem Klangcomputer-Projekt, das andere Einstellungen für die Fuse-Bits verwendet als der c't-Bot!)

Noch mehr Hardware gibt es auch:

* Aufbauanleitung **[USB-2-Bot-Adapter](../USB2Bot/USB2Bot.md)** mit Fotos
* Aufbauanleitung **[Erweiterungsmodul und Klappe](../ct-Bot-Erweiterung/ct-Bot-Erweiterung.md)** mit Fotos

## Test eines frisch aufgebauten ct-Bots

1. **[Test-Programm](ziped-releases/test-binaries.zip)** herunterladen
1. Das Testprogramm **[flashen](../Flash/Flash.md)**
1. Die Fernbedienung (falls das Modell *HQ RC Univers 29* verwendet wird) auf den Gerätecode **TV 334** (siehe beiliegende Anleitung) programmieren. Wer diese Fernbedienung mit vierstelligen Gerätecodes siehe Anleitung) besitzt, sollte unseren [Support](../FirstSteps/FirstSteps.md#Support) kontaktieren - der Gerätecode 334 funktioniert hier nicht.
1. Die Hardware des Bots **[testen](https://www.heise.de/ct/artikel/Hallo-Welt-290314.html)**. Wenn etwas nicht wie im Artikel beschrieben funktioniert, geht es weiter mit der **[Hardware-Fehlersuche](https://www.heise.de/ct/artikel/Kammerjaeger-290506.html)**. Wenn alle Tests erfolgreich abgeschlossen sind: Herzlichen Glückwunsch! Nun geht es an die eigene Roboter-Software oder die Erkundung der bereits vorhandenen. Bitte lesen Sie auf der **[Software-Seite](../ct-Bot-Software/ct-Bot-Software.md)** weiter.

## Erweiterungen

Wenn der c't-Bot erst einmal fährt, gibt es ein paar Erweiterungen:

### Erweiterungsmodul

Das **[Erweiterungsmodul](../ct-Bot-Erweiterung/ct-Bot-Erweiterung.md)** beschert dem c't-Bot WLAN, MMC- oder SD-Karten und eine Transportklappe. Siehe auch:

* **[c't 2/2007, S. 184](https://www.heise.de/ct/artikel/Aussendienstler-290830.html)** Außendienstler, Funkmodul, Massenspeicher und Klappe für den c't-Bot
* **[Aufbauanleitung Erweiterungsmodul](../ct-Bot-Erweiterung/ct-Bot-Erweiterung.md)** und Klappe mit Fotos

### CPU-Erweiterung

Unter [Raspberry Pi](../RaspberryPi/RaspberryPi.md) und [BeagleBoard](../deprecated/BeagleBoard/BeagleBoard.md) finden sich Informationen über eine leistungsfähige CPU-Erweiterung des c't-Bots mit Hilfe eines Raspberry Pi oder BeagleBoards.

### Weitere Ideen

* Sammlung von Ideen oder Leservorschlägen für [Erweiterung des c't-Bots](../HWErweiterungen/HWErweiterungen.md) um zusätzliche Hardware

## Korrekturen und Hinweise

Es haben sich im Laufe des Projekts einige kleine Fehler eingeschlichen. Zum Glück nur in der Dokumentation, nicht in der Hardware (auch wenn es hier mittlerweile einige [Verbesserungsvorschläge](../ct-Bot-Modifikationen/ct-Bot-Modifikationen.md) gibt). Hier daher die offizielle, bereinigte Version. Umstände und Irrtümer bitten wir zu entschuldigen.

Als Aufbauanleitung gilt nach wie vor, die in [c't 04/06 ab S. 208](https://www.heise.de/ct/artikel/Hallo-Welt-290314.html) abgedruckte. Sie enthält nach unserem derzeitigen Wissensstand keine Fehler. Lediglich in einem Schaltplan und der Stückliste hatte der Fehlerteufel seine Finger im Spiel. Da etwas Verwirrung durch unterschiedliche Versionen entstanden ist, stehen auf [dieser Seite](../ct-Bot-Aufbau/ct-Bot-Aufbau.md) der entsprechende Teil des Artikels mit einigen zusätzlichen Fotos und Anmerkungen, sowie alle Schalt- und Bestückungspläne. Auch die aktualisierte Stückliste findet sich hier. Sie entspricht bis auf die Bestellnummern der, die auch [Segor](http://www.segor.de/L1Bausaetze/ct-robot.shtml) auf seiner Homepage hat und ist etwas ausführlicher, als die in c't 04/06 abgedruckte.

Die Aufbauanleitung und die Korrekturhinweise, die den Teilesätzen beiliegen, die vor dem 12.2.2006 ausgeliefert wurden, bitte nicht mehr beachten. Sie werden durch die hier aufgelisteten Dokumente komplett ersetzt.

Überarbeitet gegenüber den in c't abgedruckten Informationen:

* Stückliste (aus c't 04/06)
* Schaltplan Sensorplatinen (aus c't 04/06)
* Bestückungsdruck Hauptplatine (aus c't 04/06)
* Schaltplan Hauptplatine (aus c't 02/06)

Nach wie vor aktuell, und hier der Vollständigkeithalber nochmals aufgeführt:

* Schaltplan Maussensor (aus c't 04/06)
* Bestückungsplan Maussensor aus c'2 04/06

Wer bereits angefangen hat zu bauen findet hier eine Zusammenfassung der wichtigsten Korrekturen:

* Gegenüber dem ersten Schaltplan aus c't 02/06 haben sich diverse Widerstandswerte geändert. Neu hinzugekommen ist auch die Schutzschaltung gegen Verpolen der Spannungsversorgung. Des Weiteren hat sich die Polung der DC-Buchse geändert. Alle diese Änderungen dokumentiert bereits c't 04/06.
* In der Stückliste in c't 04/06 haben R6, R32, Pot1 falsche Werte. Des Weiteren sind die LEDs verrutscht.
* In dem Bestückungsplan in c't 04/06 sind R7 und R27 vertauscht.
* Im Maussensorschaltplan in c't 04/06 ist U102 verpolt.
* Die Montageanleitung der IR-Distanzsensoren im Beipackzettel ist fehlerhaft.

## Schaltpläne <a name="Schaltplaene"></a>

* [Hauptplatine](schaltplan-final.pdf) Stand: 13.02.2006
* [Sensorplatinen](schaltplan-sensoren.pdf) Stand: 13.02.2006
* [Maussensor](schaltplan-maus.pdf) Stand: 13.02.2006
* [USB-2-Bot-Adapter](schaltplan-usb-2-bot.pdf) Stand: 20.03.2006
* [Erweiterungsmodul](schaltplan-erweiterung.pdf) Stand: 06.01.2007

## Bestückungspläne

* [Hauptplatine und Sensorplatinen](bestueckung.pdf) Stand: 13.02.2006
* [USB-2-Bot-Adapter](bestueckung-usb-2-bot.pdf) Stand: 20.03.2006
* [Erweiterungsmodul](bestueckung-erweiterung.pdf) Stand: 06.01.2007

## Mechanische Teile des Bot

* [Grundplatte](grundplatte_bemassung.pdf) Stand: 13.02.2006

## Stücklisten <a name="Stuecklisten"></a>

### Bauteile des Erweiterungsmoduls

Stand: 06.01.2007

<table>
  <tr>
    <td><b>Bauteil</b></td>
    <td><b>Wert</b></td>
  </tr>
  <tr>
    <td>C1,C2</td>
    <td>470uF/16V</td>
  </tr>
  <tr>
    <td>C3,C4,C5,C6,C7,C9</td>
    <td>100nF</td>
  </tr>
  <tr>
    <td>D1,D2,D3,D4,D5</td>
    <td>1N4148</td>
  </tr>
  <tr>
    <td>IC1</td>
    <td>WiPort (WP2001000G)</td>
  </tr>
  <tr>
    <td>IC2</td>
    <td>LM3940IT-3,3</td>
  </tr>
  <tr>
    <td>IC3</td>
    <td>74HC74</td>
  </tr>
  <tr>
    <td>IC4</td>
    <td>74HCT125</td>
  </tr>
  <tr>
    <td>IC5,IC6</td>
    <td>74HCT4053</td>
  </tr>
  <tr>
    <td>J4, J5, J6, J7</td>
    <td>Buchsenleisten (Best&uuml;ckung erfolgt von unten)</td>
  </tr>
  <tr>
    <td>J12</td>
    <td>Stiftleiste, gewinkelt</td>
  </tr>
  <tr>
    <td>J10</td>
    <td>SD-Kartenschacht</td>
  </tr>
  <tr>
    <td>J11</td>
    <td>Einzelstift, gewinkelt</td>
  </tr>
  <tr>
    <td>J14</td>
    <td>Stiftwanne, gewinkelt</td>
  </tr>
  <tr>
    <td>J15</td>
    <td>nicht bestückt,</td>
  </tr>
  <tr>
    <td>P1</td>
    <td>RJ45-Buchse mit Ferrit</td>
  </tr>
  <tr>
    <td>und</td>
    <td>LED</td>
  </tr>
  <tr>
    <td>R4,R6,R8</td>
    <td>1,8 kOhm</td>
  </tr>
  <tr>
    <td>R5,R7,R9</td>
    <td>3,3 kOhm</td>
  </tr>
  <tr>
    <td>R10,R11</td>
    <td>220 Ohm</td>
  </tr>
  <tr>
    <td>R12, R13, R16, R17</td>
    <td>10 kOhm</td>
  </tr>
  <tr>
    <td>R15</td>
    <td>4,7 kOhm</td>
  </tr>
  <tr>
    <td>ST51</td>
    <td>Buchsenleiste, zweireihig</td>
  </tr>
  <tr>
    <td>SW1</td>
    <td>Schalter</td>
  </tr>
  <tr>
    <td>Servo</td>
    <td>Futaba S3107</td>
  </tr>
</table>

### Bauteile des c't-Bot Basispakets

Stand: 13.02.2006

<table>
<tr>
<th align="left">Rubrik</th>
<th align="left">Bezeichnung</th>
<th align="left">Anzahl</th>
<th align="left">Bemerkung</th>
</tr>
<tr>
<td class="mitlinie"><em>Mechanik</em></td>
<td class="mitlinie">&nbsp;</td>
<td class="mitlinie">&nbsp;</td>
<td class="mitlinie">&nbsp;</td>
</tr>
<tr class="hellgrau">
<td>&nbsp;</td>
<td>Grundplatte</td>
<td align="right">1</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>&nbsp;</td>
<td>Motorflansch</td>
<td align="right">2</td>
<td>links/rechts identisch</td>
</tr>
<tr class="hellgrau">
<td>&nbsp;</td>
<td>Motor</td>
<td align="right">2</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>&nbsp;</td>
<td>Rad</td>
<td align="right">2</td>
<td>ohne Reifen</td>
</tr>
<tr class="hellgrau">
<td>&nbsp;</td>
<td>Reifen</td>
<td align="right">2</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td align="right">2</td>
<td>Madenschraube f&uuml;r Rad auf Motorachse</td>
</tr>
<tr class="hellgrau">
<td>&nbsp;</td>
<td>&nbsp;</td>
<td align="right">1</td>
<td>f&uuml;r Madenschraube</td>
</tr>
<tr>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td align="right">6</td>
<td>Schraube f&uuml;r Motor in Motorflansch</td>
</tr>
<tr class="hellgrau">
<td>&nbsp;</td>
<td>Gleiter</td>
<td align="right">1</td>
<td>Teflongleiter mit Gewinde</td>
</tr>
<tr>
<td>&nbsp;</td>
<td>Alu-Tr&auml;ger</td>
<td align="right">3</td>
<td>&nbsp;</td>
</tr>
<tr class="hellgrau">
<td>&nbsp;</td>
<td>&nbsp;</td>
<td align="right">19</td>
<td>Kreuzschlitzschraube - 1 Gr&ouml;&szlig;e f&uuml;r fast alles</td>
</tr>
<tr>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td align="right">4</td>
<td>f&uuml;r Motorflansche an Grundplatte</td>
</tr>
<tr class="hellgrau">
<td>&nbsp;</td>
<td>&nbsp;</td>
<td align="right">4</td>
<td>Kunststoffschrauben f&uuml;r Maussensor-Sandwich</td>
</tr>
<tr>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td align="right">14</td>
<td>Kunststoffscheiben 12 x f&uuml;r Maussensor-Sandwich, je 1x
Sensorplatine links/rechts</td>
</tr>
<tr class="hellgrau">
<td>&nbsp;</td>
<td>&nbsp;</td>
<td align="right">16</td>
<td>Kunststoffmuttern f&uuml;r Maussensor-Sandwich</td>
</tr>
<tr>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td align="right">2</td>
<td>Halteschellen Maussensor-Kabelbaum an hinteren Alu-Tr&auml;ger</td>
</tr>
<tr class="hellgrau">
<td>&nbsp;</td>
<td>&nbsp;</td>
<td align="right">2</td>
<td>Kabelbinder Sensorplatinen-Kabelb&auml;ume an vordere
Alu-Tr&auml;ger</td>
</tr>
<tr>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td align="right">4</td>
<td>Moosgummif&uuml;&szlig;e zwischen Abdeckplatte und Akkupack</td>
</tr>
<tr class="hellgrau">
<td>&nbsp;</td>
<td>&nbsp;</td>
<td align="right">1</td>
<td>Klettbinder als Akkupack-Halterung</td>
</tr>
<tr>
<td>Batteriehalter</td>
<td>3xMignon</td>
<td align="right">1</td>
<td>&nbsp;</td>
</tr>
<tr class="hellgrau">
<td>Batteriehalter</td>
<td>2xMignon</td>
<td align="right">1</td>
<td>&nbsp;</td>
</tr>
<tr>
<td class="mitlinie"><em>ELEKTRONIK Hauptplatine</em></td>
<td class="mitlinie">&nbsp;</td>
<td class="mitlinie">&nbsp;</td>
<td class="mitlinie">&nbsp;</td>
</tr>
<tr class="hellgrau">
<td>C1,C2</td>
<td>22pF</td>
<td align="right">2</td>
<td>Richtung beliebig</td>
</tr>
<tr>
<td>C3,C4</td>
<td>100nF</td>
<td align="right">2</td>
<td>Stempelung 104, Richtung beliebig</td>
</tr>
<tr class="hellgrau">
<td>C5</td>
<td>100uF</td>
<td align="right">1</td>
<td>Polung beachten</td>
</tr>
<tr>
<td>D1,D2</td>
<td>1N4148</td>
<td align="right">2</td>
<td>Polung beachten</td>
</tr>
<tr class="hellgrau">
<td>D3</td>
<td>SB140</td>
<td align="right">1</td>
<td>Polung beachten</td>
</tr>
<tr>
<td>IC1</td>
<td>ATmega32-16PU</td>
<td align="right">1</td>
<td>&nbsp;</td>
</tr>
<tr class="hellgrau">
<td>&nbsp;</td>
<td>&nbsp;</td>
<td align="right">1</td>
<td>Sockel f&uuml;r IC1</td>
</tr>
<tr>
<td>IC2</td>
<td>L293D</td>
<td align="right">1</td>
<td>&nbsp;</td>
</tr>
<tr class="hellgrau">
<td>IC3</td>
<td>74HC14N</td>
<td align="right">1</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>IC4,IC5,IC6</td>
<td>74HC595N</td>
<td align="right">3</td>
<td>&nbsp;</td>
</tr>
<tr class="hellgrau">
<td>&nbsp;</td>
<td>&nbsp;</td>
<td align="right">4</td>
<td>Sockel f&uuml;r IC2,4,5,6</td>
</tr>
<tr class="hellgrau">
<td>IC7,IC8</td>
<td>LM311N</td>
<td align="right">2</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td align="right">2</td>
<td>Sockel f&uuml;r IC7,8</td>
</tr>
<tr class="hellgrau">
<td>IC9</td>
<td>TSOP34836</td>
<td align="right">1</td>
<td>FB-Empf&auml;nger</td>
</tr>
<tr>
<td>IC10</td>
<td>L4940V5</td>
<td align="right">1</td>
<td>&nbsp;</td>
</tr>
<tr class="hellgrau">
<td>J1-J8</td>
<td>Stiftleiste</td>
<td align="right">2</td>
<td>schneiden</td>
</tr>
<tr>
<td>LDR1,LDR2</td>
<td>MPY54C569</td>
<td align="right">2</td>
<td>&nbsp;</td>
</tr>
<tr class="hellgrau">
<td>LED1,LED2,LED7</td>
<td>LEDblau</td>
<td align="right">3</td>
<td>kurzes Bein ist Kathode (Minus)</td>
</tr>
<tr>
<td>LED3</td>
<td>LEDrot</td>
<td align="right">1</td>
<td>kurzes Bein ist Kathode (Minus)</td>
</tr>
<tr class="hellgrau">
<td>LED4</td>
<td>LEDorange</td>
<td align="right">1</td>
<td>kurzes Bein ist Kathode (Minus)</td>
</tr>
<tr>
<td>LED5</td>
<td>LEDgelb</td>
<td align="right">1</td>
<td>kurzes Bein ist Kathode (Minus)</td>
</tr>
<tr class="hellgrau">
<td>LED6</td>
<td>LEDgr&uuml;n</td>
<td align="right">1</td>
<td>kurzes Bein ist Kathode (Minus)</td>
</tr>
<tr>
<td>LED8</td>
<td>LEDwei&szlig;</td>
<td align="right">1</td>
<td>kurzes Bein ist Kathode (Minus)</td>
</tr>
<tr class="hellgrau">
<td>L1</td>
<td>100uH-SMCC</td>
<td align="right">1</td>
<td>dicker Widerstand, braun-schwarz-braun-gold</td>
</tr>
<tr>
<td>POT1</td>
<td>67W 5k</td>
<td align="right">1</td>
<td>Trimmpoti Displaykontrast</td>
</tr>
<tr class="hellgrau">
<td>P1</td>
<td>DCBU 2,1-R</td>
<td align="right">1</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>Q1</td>
<td>Q 16,0-LP</td>
<td align="right">1</td>
<td>&nbsp;</td>
</tr>
<tr class="hellgrau">
<td>&nbsp;</td>
<td>Abstandshalter</td>
<td align="right">1</td>
<td>f&uuml;r Q1</td>
</tr>
<tr>
<td>R1</td>
<td>10kOhm</td>
<td align="right">1</td>
<td>braun-schwarz-schwarz-rot-braun</td>
</tr>
<tr class="hellgrau">
<td>R2</td>
<td>20 Ohm</td>
<td align="right">1</td>
<td>rot-schwarz-schwarz-gold-braun oder Drahtbr&uuml;cke
(Displaybeleuchtung)</td>
</tr>
<tr>
<td>R3,R4,R8</td>
<td>4,7kOhm</td>
<td align="right">3</td>
<td>gelb-violett-schwarz-braun-braun</td>
</tr>
<tr class="hellgrau">
<td>R5,R6,R7,R30,R31</td>
<td>47kOhm</td>
<td align="right">5</td>
<td>gelb-violett-schwarz-rot-braun</td>
</tr>
<tr>
<td>R9-R16</td>
<td>160 Ohm</td>
<td align="right">8</td>
<td>braun-blau-schwarz-schwarz-braun</td>
</tr>
<tr class="hellgrau">
<td>R17,R18,R32</td>
<td>39 kOhm</td>
<td align="right">3</td>
<td>orange-wei&szlig;-schwarz-rot-braun</td>
</tr>
<tr>
<td>R19,R20</td>
<td>6,2 kOhm</td>
<td align="right">2</td>
<td>blau-rot-schwarz-braun-braun</td>
</tr>
<tr class="hellgrau">
<td>R21,R22</td>
<td>470 kOhm</td>
<td align="right">2</td>
<td>gelb-violett-schwarz-orange-braun</td>
</tr>
<tr>
<td>R23,R24,R25,R26</td>
<td>180 Ohm</td>
<td align="right">4</td>
<td>braun-grau-schwarz-schwarz-braun</td>
</tr>
<tr class="hellgrau">
<td>R27</td>
<td>100 Ohm</td>
<td align="right">1</td>
<td>braun-schwarz-schwarz-schwarz-braun</td>
</tr>
<tr>
<td>R28</td>
<td>6,8 Ohm</td>
<td align="right">1</td>
<td>blau-grau-gold-gold</td>
</tr>
<tr>
<td>R33</td>
<td>1 kOhm</td>
<td align="right">1</td>
<td>braun-schwarz-schwarz-braun-braun</td>
</tr>
<tr class="hellgrau">
<td>R34</td>
<td>5,1 kOhm</td>
<td align="right">1</td>
<td>gr&uuml;n-braun-schwarz-braun-braun</td>
</tr>
<tr>
<td>R29</td>
<td>ZD 2V4 0,5W</td>
<td align="right">1</td>
<td>Polung beachten</td>
</tr>
<tr class="hellgrau">
<td>ST1,ST2,ST3</td>
<td>Stecker+Buchse mit Kabel</td>
<td align="right">3</td>
<td>Set aus Stiftleiste und Buchse mit Kabeln</td>
</tr>
<tr>
<td>ST4</td>
<td>Stiftwanne</td>
<td align="right">1</td>
<td>Displayanschlu&szlig;</td>
</tr>
<tr class="hellgrau">
<td>ST5</td>
<td>Stiftwanne</td>
<td align="right">1</td>
<td>isp-Programmierstecker nach Atmel-Standard</td>
</tr>
<tr>
<td>ST6</td>
<td>Stiftwanne</td>
<td align="right">1</td>
<td>isp-Programmierstecker f&uuml;r BlueMP3/ISP</td>
</tr>
<tr class="hellgrau">
<td>ST7,ST8,ST9</td>
<td>Stecker+Buchse mit Kabel</td>
<td align="right">3</td>
<td>Set aus Stiftleiste und Buchse mit Kabeln</td>
</tr>
<tr>
<td>SW1</td>
<td>Taster</td>
<td align="right">1</td>
<td>Reset-Taster</td>
</tr>
<tr class="hellgrau">
<td>SW2</td>
<td>Kippschalter</td>
<td align="right">1</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>TR1-TR6</td>
<td>BS250</td>
<td align="right">6</td>
<td>&nbsp;</td>
</tr>
<tr class="hellgrau">
<td>U1</td>
<td>CNY70</td>
<td align="right">1</td>
<td>&nbsp;</td>
</tr>
<tr>
<td class="mitlinie"><em>ELEKTRONIK Sensorplatinen links/rechts</em></td>
<td class="mitlinie">&nbsp;</td>
<td class="mitlinie">&nbsp;</td>
<td class="mitlinie">&nbsp;</td>
</tr>
<tr class="hellgrau">
<td>U101-U104</td>
<td>CNY70</td>
<td align="right">4</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>U105</td>
<td>IS471F</td>
<td align="right">1</td>
<td>&nbsp;</td>
</tr>
<tr class="hellgrau">
<td>LED101</td>
<td>LD274-3</td>
<td align="right">1</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>Abstandssensor</td>
<td>GP2D12</td>
<td align="right">2</td>
<td>&nbsp;</td>
</tr>
<tr class="hellgrau">
<td>&nbsp;</td>
<td>&nbsp;</td>
<td align="right">2</td>
<td>Kabelsatz f&uuml;r Abstandssensor</td>
</tr>
<tr>
<td><em>ELEKTRONIK Maussensor-Platine</em></td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
</tr>
<tr class="hellgrau">
<td>C1</td>
<td>100nF</td>
<td align="right">1</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>C2</td>
<td>1uF</td>
<td align="right">1</td>
<td>&nbsp;</td>
</tr>
<tr class="hellgrau">
<td>LED1</td>
<td>HLMP-ED80-K0T00</td>
<td align="right">1</td>
<td>kurzes Bein ist Kathode (Minus)</td>
</tr>
<tr>
<td>Klammer f&uuml;r LED</td>
<td>HDNS-2200</td>
<td align="right">1</td>
<td>&nbsp;</td>
</tr>
<tr class="hellgrau">
<td>Linsenplatte</td>
<td>HDNS-2100</td>
<td align="right">1</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>Q1</td>
<td>Q24,0-LP/GW</td>
<td align="right">1</td>
<td>&nbsp;</td>
</tr>
<tr class="hellgrau">
<td>&nbsp;</td>
<td>Abstandshalter</td>
<td align="right">1</td>
<td>f&uuml;r Q1</td>
</tr>
<tr>
<td>Q2</td>
<td>BC557B</td>
<td align="right">1</td>
<td>&nbsp;</td>
</tr>
<tr class="hellgrau">
<td>R1.R4</td>
<td>180 Ohm</td>
<td align="right">2</td>
<td>braun-grau-schwarz-schwarz-braun</td>
</tr>
<tr>
<td>R2.R3</td>
<td>47 kOhm</td>
<td align="right">2</td>
<td>gelb-violett-schwarz-rot-braun</td>
</tr>
<tr class="hellgrau">
<td>R5</td>
<td>100 Ohm</td>
<td align="right">1</td>
<td>braun-schwarz-schwarz-schwarz-braun</td>
</tr>
<tr>
<td>R6</td>
<td>100 kOhm</td>
<td align="right">1</td>
<td>braun-schwarz-schwarz-orange-braun</td>
</tr>
<tr class="hellgrau">
<td>R7</td>
<td>1 kOhm</td>
<td align="right">1</td>
<td>braun-schwarz-schwarz-braun-braun</td>
</tr>
<tr>
<td>U1,U2</td>
<td>CNY70</td>
<td align="right">2</td>
<td>&nbsp;</td>
</tr>
<tr class="hellgrau">
<td>U</td>
<td>ADNS2610</td>
<td align="right">1</td>
<td>&nbsp;</td>
</tr>
</table>

[![License: CC BY-SA 4.0](../../License.svg)](https://creativecommons.org/licenses/by-sa/4.0/)
