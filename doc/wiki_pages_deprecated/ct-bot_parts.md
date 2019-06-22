# Teilelisten & Design-Dokumente für den c't-Bot

## Schaltpläne

* [Hauptplatine](https://github.com/tsandmann/ct-bot-hw/tree/master/v1/schematics/01_mainboard.pdf)
* [Sensorplatinen](https://github.com/tsandmann/ct-bot-hw/tree/master/v1/schematics/02_sensorboard_L_R.pdf)
* [Maussensorplatine](https://github.com/tsandmann/ct-bot-hw/tree/master/v1/schematics/03_sensorboard_mouse.pdf)
* [Erweiterungsplatine](https://github.com/tsandmann/ct-bot-hw/tree/master/v1/schematics/05_extensionboard.pdf)


## Bestückungspläne

* [Hauptplatine mit Sensorplatinen](https://github.com/tsandmann/ct-bot-hw/tree/master/v1/pcb-layout/01_pcb_mainboard.pdf)
* [Maussensorplatine](https://github.com/tsandmann/ct-bot-hw/tree/master/v1/pcb-layout/03_sensorboard_mouse.pdf)
* [Erweiterungsplatine](https://github.com/tsandmann/ct-bot-hw/tree/master/v1/pcb-layout/05_extensionboard.pdf)


## Mechanische Teile

| Bauteil                         | Anzahl | Bezeichnung                                                                                          |
| :---                            |        |                                                                                                      |
| Grundplatte                     |      1 | gemäß [Technischer Zeichnung](https://github.com/tsandmann/ct-bot-hw/tree/master/v1/drawings/baseplate.pdf) |
| Motorflansch                    |      2 | links / rechts identisch                                                                             |
| Motor                           |      2 |                                                                                                      |
| Rad                             |      2 | ohne Reifen                                                                                          |
| Reifen                          |      2 |                                                                                                      |
| Madenschraube M3x4 GWST         |      2 | für die Radfixierung auf der Motorachse                                                              |
| Imbus-Schlüssel 1,5             |      1 | Werkzeug für die Madenschrauben                                                                      |
| Schraube M2x6                   |      6 | für Motorflansche                                                                                    |
| Teflongleiter                   |      1 | mit Gewinde                                                                                          |
| Aluminiumträger                 |      3 |                                                                                                      |
| Kreuzschlitzschraube M3x6K      |     19 |                                                                                                      |
| Mutter M3                       |      4 | für die Befestigung der Motorflansche auf der Grundplatte                                            |
| Kunststoffschrauben M3x18       |      4 | für Maussensor-Sandwich                                                                              |
| Kunststoff-Unterlegscheiben 3,2 |     14 | 12x für Maussensor-Sandwich, je 1x für Sensorplatinen L/R                                            |
| Kunststoff-Muttern M3           |     16 | für Maussensor-Sandwich                                                                              |
| Kabel-Halteschellen             |      2 | für Maussensor-Kabelbaum an hinterem Aluminiumträger                                                 |
| Kabelbinder                     |      2 | für Kabelbäume der Sensorplatinen an vorderen Aluminiumträgern                                       |
|	Moosgummifüße                   |      4 | Auflage für Akkupack auf Abdeckplatte des Maussensor-Sandwichs                                       |
|	Klettbinder                     |      1 | als Akkupack-Befestigung                                                                             |
|	Batteriehalter 3x Mignon        |      1 |                                                                                                      |
|	Batteriehalter 2x Mignon        |      1 |                                                                                                      |
|	Encoderscheibe                  |      2 | seit der 5. Auflage enthalten                                                                        |


## Stücklisten

### Hauptplatine

| Bauteil           | Bezeichnung                                                  | Bemerkungen                                                               |
| :---              | :---                                                         | :---                                                                      |
| C1, C2            | Keramik-Kondensator 22 pF                                    |                                                                           |
| C3, C4            | Keramik-Kondensator 100 nF                                   | Stempelung 104                                                            |
| C5                | Elektrolyt-Kondensator 100 µF                                | Polung beachten                                                           |
| D1, D2            | Diode 1N4148                                                 | Polung beachten                                                           |
| D3                | Diode SB140                                                  | Polung beachten                                                           |
| IC1               | ATmega-Mikrocontroller                                       | mit IC-Sockel; kompatible Modelle: ATmega1284P / 644P / 644 / 32          |
| IC2               | Push-Pull 4 Channel Driver with Diodes L293D                 | mit IC-Sockel                                                             |
| IC3               | Hex Schmitt-Trigger Inverter 74HC14N                         | mit IC-Sockel                                                             |
| IC4, IC5, IC6     | 8-Bit Schieberegister mit 3-State Output Registern 74HC595N  | jeweils mit IC-Sockel                                                     |
| IC7, IC8          | Komparator LM311N                                            | jeweils mit IC-Sockel                                                     |
| IC9               | FB-Empfänger TSOP34836                                       |                                                                           |
| IC10              | Spannungsregler L4940V5                                      |                                                                           |
| J1 - J8           | Stiftleiste                                                  | jeweils passend zuschneiden                                               |
| LDR1, LDR2        | Helligkeitssensor MPY54C569                                  |                                                                           |
| LED1, LED2, LED7  | LED (blau)                                                   | kurzes Bein ist die Kathode (Minus)                                       |
| LED3              | LED (rot)                                                    | kurzes Bein ist die Kathode (Minus)                                       |
| LED4              | LED (orange)                                                 | kurzes Bein ist die Kathode (Minus)                                       |
| LED5              | LED (gelb)                                                   | kurzes Bein ist die Kathode (Minus)                                       |
| LED6              | LED (grün)                                                   | kurzes Bein ist die Kathode (Minus)                                       |
| LED8              | LED (weiß)                                                   | kurzes Bein ist die Kathode (Minus)                                       |
| L1                | Drossel 100 µH SMCC 5%                                       | Farbring-Kennung: braun-schwarz-braun-gold                                |
| POT1              | Trimmpotentiometer 5kOhm                                     | für die Einstellung des Displaykontrasts                                  |
| P1                | DC-Hohlstecker-Buchse 2,1-R                                  |                                                                           |
| Q1                | Quarz 16 MHz LP                                              | mit Abstandshalter; alternativ 20 MHz Quarz                               |
| R1                | Widerstand 10 kΩ 1%                                          | Farbring-Kennung: braun-schwarz-rot-braun                                 |
| R2                | Widerstand 20 Ω 1%                                           | Farbring-Kennung: rot-schwarz-schwarz-gold-braun; alternativ: Drahtbrücke |
| R3, R4, R8        | Widerstand 4,7 kΩ 1%                                         | Farbring-Kennung: gelb-violett-schwarz-braun-braun                        |
| R5 - R7, R30, R31 | Widerstand 47 kΩ 1%                                          | Farbring-Kennung: gelb-violett-schwarz-rot-braun                          |
| R9 - R16          | Widerstand 160 Ω 1%                                          | Farbring-Kennung: braun-blau-schwarz-schwarz-braun                        |
| R17, R18, R32     | Widerstand 39 kΩ 1%                                          | Farbring-Kennung: orange-weiß-schwarz-rot-braun                           |
| R19, R20          | Widerstand 6,2 kΩ 1%                                         | Farbring-Kennung: blau-rot-schwarz-braun-braun                            |
| R21, R22          | Widerstand 470 kΩ 1%                                         | Farbring-Kennung: gelb-violett-schwarz-orange-braun                       |
| R23 - R26         | Widerstand 180 Ω 1%                                          | Farbring-Kennung: braun-grau-schwarz-schwarz-braun                        |
| R27               | Widerstand 100 Ω 1%                                          | Farbring-Kennung: braun-schwarz-schwarz-schwarz-braun                     |
| R28               | MOX-Widerstand 6,8 Ω 5%                                      | Farbring-Kennung: blau-grau-gold-gold                                     |
| R29               | Zener-Diode 2,4 V 0,5 W                                      | Polung beachten                                                           |
| R33               | Widerstand 1 kΩ 1%                                           | Farbring-Kennung: braun-schwarz-schwarz-braun-braun                       |
| R34               | Widerstand 5,1 kΩ 1%                                         | Farbring-Kennung: grün-braun-schwarz-braun-braun                          |


### Bauteile des c't-Bot Basispakets

<table>
<tr>
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
