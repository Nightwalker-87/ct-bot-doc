# Erweiterungsmodul für den c't-Bot

>> **Trac-2-Markdown Konvertierung:** *unchecked*

Das Erweiterungsmodul erlaubt es dem c't-Bot per LAN und WLAN zu kommunizieren. Über einen Steckplatz für SD- oder MMC-Karten lässt sich der Speicher des Roboters stark erweitern. Näheres beschreibt der c't-Artikel in c't 02/07, S. 184. Auf der Hardware-Seite finden sich alle aktuellen Schalt- und Bestückungspläne, sowie eine Stückliste.

## Ergänzungen und Hinweise

* Der Programmierstecker auf dem Erweiterungsmodul (J14) ist leider verdreht. Wer ihn benutzen will, muss das Flachbandkabel um 180 Grad gedreht einstecken (Pin 1 zeigt dann nach vorne, in Richtung Transportfach des Bots). Damit das klappt muss man unter Umständen die kleine Nase am Flachbandstecker entfernen.
* Unbedingt prüfen, ob der dem Bausatz der Erweiterungsplatine beiligende SD-Kartenslot einen "Hebel" hat, der zum Auswerfen der Karte dient. Dieser kollidiert mit dem hinter dem Slot liegenden IC und verhindert so ein korrektes Einsetzen einer SD-Karte (was später nicht sofort ersichtlich ist), kann aber mit einer Zange zerstörungsfrei entfernt werden. Die Bilder im Wiki zeigen diesen "Hebel" nicht, weil der Slot wahrscheinlich erst später aufgrund eines Herstellerwechsels den originalen Slot ersetzt hat.

## Erweiterungsmodul

### Aufbau des Erweiterungsmoduls

Stand: 15.01.2007

### Bauteile des Erweiterungsmoduls

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

Alle Bauteile sorgfältig einlöten. Dabei sollte man ST5 vor J14 einlöten. Bitte auch darauf achten, dass einige Buchsenleisten (J4, J5, J6, J7, ST5) von unten auf die Platine kommen.

**Die Buchsenleisten J4, J5, J6, J7 und ST5 werden von unten eingelötet:**
  ![Image: 'Erweiterung_01.jpg'](Erweiterung_01.jpg)

Der Kartenschacht (J10) muss in die Führungslöcher einrasten, bevor man ihn festlötet. Er sitzt oben auf der Platine und nicht wie auf den Prototypen-Fotos in c't 02/07 auf der Unterseite. Die Halo-Buchse (P1) soll möglichst flach auf der Platine aufsitzen. Dazu muss man die Federlaschen etwas wegbiegen.

**Die Halo-Buchse und der MMC-Slot müssen plan aufliegen:**
  ![Image: 'Erweiterung_02.jpg'](Erweiterung_02.jpg)

Auf die von unten eingelöteten Buchsenleisten (J4, J5, J6, J7, ST5) steckt man jeweils zwei weitere Reihen an Buchsenleisten auf, damit die Pins lang genug werden, um die Hauptplatine zu erreichen.

**Drei Reihen Buchsenleisten verbinden Erweiterungsmodul und Hauptplatine:**
  ![Image: 'Erweiterung_03.jpg'](Erweiterung_03.jpg)

Beim Einschrauben der WiPort-Antennenleitung sollte man nur eine der beiden mitgelieferten Federscheiben verwenden. Diese sollte oberhalb der Platine sitzen. Die Buchse muss also so weit wie moeglich nach oben. Das Antennenkabel darf nicht geknickt werden, man sollte auch nicht daran ziehen.

**Die Antennenleitung des WiPorts darf nicht knicken. Daher muss die Buchse so hoch wie möglich sitzen:**
  ![Image: 'Erweiterung_04.jpg'](Erweiterung_04.jpg)

Den Pin 4 aus dem Maussensorkabelstrang entfernt man aus dem zehnpoligen Stecker. Die Verriegelung lässt sich mit einer Nadel oder einem kleinen Schraubendreher leicht lösen. Den angelöteten Metallstift schneidet man ab und lötet statt dessen einen einzelnen Buchsenpin an.

**Der Pin 4 des Maussensors wird mit einem Buchsenpin versehen und später auf das Erweiterungsmodul gesteckt:**
  ![Image: 'Erweiterung_11.jpg'](Erweiterung_11.jpg)

### Einbau des Erweiterungsmoduls

Nun ist es an der Zeit die drei zehnpoligen Stecker wieder auf die Hauptplatine zu stecken und die Kabel mit Kabelbindern so festzuzurren, dass, falls vorhanden, der Klappenarm der Klappen-Erweiterung nicht daran schleift.

Die Erweiterungsplatine kommt oben auf die drei neuen Bolzen, die die Hauptplatine festhalten. Bevor man die das Erweiterungsmodul mit den drei Schrauben, die vor dem Umbau die Hauptplatine in Position hielten, fixiert, sollte man prüfen, ob auch alle Stecker (J4, J5, J6, J7 und ST5) sauberen Kontakt haben. Dabei ist unbedingt darauf zu achten, dass das WiPort-Antennkabel nicht geknickt wird. Auch hält es keinen Zug aus.

Wenn das Display wieder an seinem alten Platz sitzt — der Stecker muss jetzt zum U-Ausschnitt zeigen und das umgebaute Kabel vier des Maussensors auf J11 des Erweiterungsmoduls gesteckt, ist der Umbau abgeschlossen.

**Das Erweiterungsmodul sitzt auf drei Abstandsbolzen, die wiederum die Hauptplatine mit den Alutragsäulen verbinden:**
  ![Image: 'Erweiterung_12.jpg'](Erweiterung_12.jpg)

**Das Display darf die RJ45-Buchse nicht berühren:**
  ![Image: 'Erweiterung_13.jpg'](Erweiterung_13.jpg)

### Konfiguration des WiPorts

**Bei den WLAN-Einstellungen des WiPort ist Vorsicht geboten, denn sonst sperrt man sich leicht aus:**
  ![Image: 'wiport_wlansettings.jpg'](wiport_wlansettings.jpg)

**Der WiPort unterstützt sowohl statische IP-Adressen als auch DHCP:**
  ![Image: 'wiport_lansettings.jpg'](wiport_lansettings.jpg)

**Damit der c't-Bot von sich aus Verbindung zum Sim aufnimmt, muss man "Active Connection" aktivieren:**
  ![Image: 'wiport_activeconnectionsettings.jpg'](wiport_activeconnectionsettings.jpg)

**Damit der Bootloader nicht Daten sieht, die der Bot vor dem Reset in den Puffer gelegt hat, bietet der WiPort die Möglichkeit bei einer eingehenden Verbindung alte Daten zu verwerfen ("Flush Mode"):**
  ![Image: 'wiport_serialsettings.jpg'](wiport_serialsettings.jpg)

**Hat man sich auf dem LAN- oder WLAN-Interface ausgesperrt, kommt man noch über den USB-2-Bot-Adapter mit einem Teralprogramm an den WiPort heran:**
  ![Image: 'wiport_config_usb2bot.jpg'](wiport_config_usb2bot.jpg)

Wichtig sind die Baudrate (9600, 8N1) und das deaktivieren der Flusskontrolle. Dann bietet der WiPort ein Setup-Menü, wenn er während des Bootens drei "x"-Zeichen empfängt.

## Auf- und Einbau der Klappen-Erweiterung

Wer den c't-Bot schon aufgebaut hat, muss zuerst das Display abschrauben und entfernen. Die Bolzen für das Display bleiben dabei stehen. Nun zieht man die drei 10-poligen Stecker von der Hauptplatine ab und löst die drei Befestigungsschrauben von derselben.

Jetzt kann muss man den dreipoligen Stecker am rechten Distanzsensor (GP2D12) abziehen. Den Stecker lötet man aus und stattdessen die drei Kabel direkt ein.

**Der Stecker des GP2D12 liegt im Weg des Klappenarms und muss daher weichen:**
  ![Image: 'Erweiterung_05.jpg'](Erweiterung_05.jpg)

Die drei Kabel werden stattdessen direkt eingelötet.

### Servo-Möglichkeit 1: Futaba

Die Pin-Belegung des Futaba-Steckers entspricht nicht der von J1 auf der Hauptplatine. Mit einer Stecknadel lassen sich die Plastikhäckchen des Steckers entriegeln, um das rote und das schwarze Kabel zu tauschen: An Pin 1 von J1 (zeigt zum U-Ausschnitt) kommt das rote Servo-Kabel, an Pin 2 das schwarze und an Pin 3 das weiße.
Den Servo steckt man kopfüber von oben in die Hauptplatine und schraubt ihn mit zwei Schrauben M3x8 unter Verwendung der Gummilager aus dem Servozubehör fest. Die Achse des Servos zeigt dabei in Richtung des U-förmigen Ausschnitts. Danach kommt der Stecker des Servos so auf J1 der Hauptplatine, dass die rote Ader zum U-Ausschnitt zeigt.

**Beim Futaba-Servo-Stecker muss man zwei Adern vertauschen, damit er zum c't-Bot passt:**
  ![Image: 'Erweiterung_06.jpg'](Erweiterung_06.jpg)

**Vom Servozubehör braucht man nur den runden Betätiger, die kleine Befestigungsschraube und die beiden Gummilager:**
  ![Image: 'Erweiterung_07.jpg'](Erweiterung_07.jpg)

**Der runde Betätiger wird mit zwei Schrauben und zwei Muttern mit dem Tragarm verschraubt:**
  ![Image: 'Erweiterung_08.jpg'](Erweiterung_08.jpg)

### Servo-Möglichkeit 2: SG90

Falls der Futaba-Servo nicht mehr zu beziehen ist kann auch der SG90-Servo genutzt werden. Bei diesem sind einige Anpassungen notwendig. Nachfolgend wird ein Beispiel für einen Futaba-kompatiblen Einbau von SG90-Servo und Tragarm gezeigt. Andere Lösungen sind möglich.

In diesem Beispiel wird der Tragarm **auf** der Servo-Halterung liegend eingebaut, damit er am Ende nicht zu tief sitzt und mit den Mods der Abstandssensoren kollidiert, die beim betreffenden Bot allesamt direkt am Sensor eingebaut wurden (vgl. [Modifkation der Abstandssensoren](../ct-Bot-Modifikationen/ct-Bot-Modifikationen.md)).
Dafür wiederum wurde das Loch des Tragarms leicht aufgebohrt, damit die Halterung des Servos in das Loch des Tragarms passt. Auch die Löcher der Servo-Halterung selbst mussten leicht aufgebohrt werden. In den weißen runden Betätiger des Servozubehörs bohrt man mit dem 2-mm-Bohrer aus dem Bausatz zwei Löcher. Der Tragarm dient dabei als Schablone. Anschliessend verschraubt man Klappenarm und Betätiger mit zwei M2x6-Schrauben und den zugehörigen Muttern. Der Klappenarm ist symmetrisch, so dass die Richtung keine Rolle spielt.

Nachfolgende Bilder dienen als Verständnishilfe oder Inspiration für andere Einbaumöglichkeiten:

**Anpassung der kreisförmigen Öffnungen des SG90, die zur Verschraubung mit der Hauptplatine dienen:**
  ![Image: 'ct-bot_anonybot20151113_130936_sg90-anpassung_small.jpg'](ct-bot_anonybot20151113_130936_sg90-anpassung_small.jpg)

**Draufsicht der Aufbohrung:**
  ![Image: 'ct-bot_anonybot20151113_131211_sg90-anpassung_small.jpg'](ct-bot_anonybot20151113_131211_sg90-anpassung_small.jpg)

**SG90 in der Aussparung der Hauptplatine:**
  ![Image: 'ct-bot_anonybot20151113_131532_sg90-anpassung_small_cut.jpg'](ct-bot_anonybot20151113_131532_sg90-anpassung_small_cut.jpg)

**Aufbohrung des Tragarms für die Halterung des SG90:**
  ![Image: 'ct-bot_anonybot20151113_135301_tragarm-richtig_small.jpg'](ct-bot_anonybot20151113_135301_tragarm-richtig_small.jpg)

**Tragarm an Halterung des SG90; Sicht auf Seite, die später nach unten vom Servo weg zeigt:**
  ![Image: 'ct-bot_anonybot20151113_135522_tragarm-richtig_small.jpg'](ct-bot_anonybot20151113_135522_tragarm-richtig_small.jpg)

**Tragarm an Halterung des SG90; Sicht auf Seite, die später nach oben zum Servo hin zeigt:**
  ![Image: 'ct-bot_anonybot20151113_135531_tragarm-richtig_small.jpg'](ct-bot_anonybot20151113_135531_tragarm-richtig_small.jpg)

**Tragarm an Halterung des SG90; Sicht auf Seite, die später nach oben zum Servo hin zeigt:**
  ![Image: 'ct-bot_anonybot20151113_135539_tragarm-richtig_small.jpg'](ct-bot_anonybot20151113_135539_tragarm-richtig_small.jpg)

**Tragarm an Halterung des SG90; Sicht von der Seite (in diesem Bild ist der Servo noch nicht hochgesetzt):**
  ![Image: 'ct-bot_anonybot20151113_135845_tragarm-richtig_small.jpg'](ct-bot_anonybot20151113_135845_tragarm-richtig_small.jpg)

**Tragarm an Halterung des SG90 auf Hauptplatine:**
  ![Image: 'ct-bot_anonybot20151113_135908_tragarm-richtig_small_cut.jpg'](ct-bot_anonybot20151113_135908_tragarm-richtig_small_cut.jpg)

**Die Höhe des Tragarms kann zusätzlich über einige Plastik-Muttern an der Halterung des SG90 justiert werden (3 in diesem Beispiel):**
  ![Image: 'ct-bot_anonybot20160120_145024_sg90-hoehe_cut.jpg'](ct-bot_anonybot20160120_145024_sg90-hoehe_cut.jpg)

Dies kann notwendig sein, falls Mods für die Distanzsensoren ansonsten mit dem Tragarm kollidieren oder der Klappen-Sensor Probleme hat, den Tragarm zu erkennen.

**Vor Inbetriebnahme** sollte unbedingt auf die korrekte **Pin-Belegung** des Servos geachtet werden, da diese für dne c't-Bot angepasst werden muss. Die nachfolgenden zwei Bilder zeigen das Original und darunter die korregierte Belegung:

**SG90-Originalbelegung:**
  ![Image: 'sg90-servo_pin-org_small.jpg'](sg90-servo_pin-org_small.jpg)

**SG90-Belegung passend zu J1 auf der Hauptplatine:**
  ![Image: 'sg90-servo_pin-ctbot-j1_small.jpg'](sg90-servo_pin-ctbot-j1_small.jpg)

* J1pin1: rot / VCC,
* J1pin2: braun / GND
* J1pin3: orange / PWM

**[Datenblatt des SG-90 Servos](sg90-servo_datenblatt.pdf)**

### Einbau des Tragarms und Verlöten von Tragarm und Klappe

Nun ist es an der Zeit die Sensorkabel der rechten Sensorplatine durch den Klappenarm zu fädeln und den Klappenarm lose auf den Servo zu stecken. Bevor man ihn jedoch festschraubt, legt man die Hauptplatine auf und prüft den Schwenkbereich. Evetnuell muss man den Klappenarm nochmal vom Servo abziehen und in einem anderen Winkel aufstecken. Der Tragarm sollte dabei so auf der Servoachse sitzen, dass er in in geöffneter Stellung von innen an die rechte vordere Stütze des Bots anschlägt und bei geschlossener Klappe von außen an die einzelne hintere Stütze. In geschlossener Position steht der Tragarm genau unterhalb des Klappensensors auf der Unterseite der Hauptplatine. Passt alles, kann man den Betätiger mit dem Servo verschrauben.

**Den Tragarm verschraubt man erst mit dem Servo, wenn man geprüft hat, dass die Klappe auch alle Positionen erreichen kann:**
  ![Image: 'Erweiterung_09.jpg'](Erweiterung_09.jpg)

Da sowohl der Tragarm als auch die Klappe mit Kupfer kaschiert sind, kann man sie einfach miteinander verlöten. Dazu biegt man am besten zuerst das rechteckige Platinenstück in die richtige Form. Nun dreht man den Tragarm in die geschlossene Stellung (gegen den Uhrzeigersinn bis auf Anschlag) und fixiert dann die Klappe mit zwei winzigen Lötpunkten. Sie sollte dabei weder einen der beiden Abstandssensoren abdecken noch auf der Grundplatte aufstehen. Sollte die Klappe in geöffnetem Zustand den rechten Sensor blockieren, so muss man sie nochmals verschieben. Steht die optimale Position fest, verbinden zwei dicke Zinnspuren die Klappe oben und unten mit dem Tragarm.

**Zwei dicke Zinnspuren verbinden Klappenarm und Klappe miteinander:**
  ![Image: 'Erweiterung_10.jpg'](Erweiterung_10.jpg)

Wer beide Teile nur mit Handschuhen anfasst und nach dem Löten mit einer dünnen Schicht Klarlack besprüht, behält den Glanz auf Dauer

Nun schraubt man je zwei Abstandsbolzen (3x12) inneinander und erhält somit drei lange Bolzen mit denen man die Hauptplatine wieder festschraubt.

[![License: CC BY-SA 4.0](../../License.svg)](https://creativecommons.org/licenses/by-sa/4.0/)
