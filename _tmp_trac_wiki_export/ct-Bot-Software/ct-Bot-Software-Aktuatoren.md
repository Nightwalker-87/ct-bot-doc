# Aktuatoren des c't-Bot

>> **Trac-2-Markdown Konvertierung:** *unchecked*

## Motoren / Motorregelung

### Einleitung

Die Ansteuerung der Motoren funktioniert wie folgt:

Die Funktion **`motor_set(int16_t left, int16_t right)`** setzt die gewünschte Sollgeschwindigkeit (Führungsgröße). Ist diese für mindestens einen Motor ungleich null, kümmert sich die Funktion **`speed_control()`** um die Einhaltung der Geschwindigkeit. Wurde eine neue Sollgeschwindigkeit vorgegeben und war außerdem die vorherige Geschwindigkeit gleich null (Anfahren aus dem Stand), so sorgen **`motor_set()`** und **`speed_control()`** für ein zunächst langsames Anfahren (Hintergrund ist das relativ geringe Drehmoment zu diesem Zeitpunkt, eine genauere Erklärung hierzu findet sich unter [Die eigentliche Regelung](/#Die-eigentliche-Regelung)). Die Istgeschwindigkeit (Regelgröße) des Bots wird mit den Radencodern gemessen, indem die seit der letzten (bzw. vor- oder viertletzten, siehe auch [Sensorauswertung](#Sensorauswertung)) Encoderflanke vergangene Zeit berechnet wird.

Ist die Regelung aktiv (also das #define **`SPEED_CONTROL_AVAILABLE`** in ct-Bot.h an), werden die Motoren mit einer wesentlich höheren PWM-Frequenz angesteuert (31.200 Hz anstatt 120 Hz), was erstens den Verschleiß der Motorbürsten deutlich reduziert und zweitens für ein eleganteres Fahrverhalten des Bots sorgt. Die besten (je kleiner die letzten Fehler waren, desto besser ist das Rating der Werte) PWM-Stellwerte zum Anfahren werden im EEPROM gespeichert, um ein möglichst sofortiges (und somit für beide Räder gleichzeitiges) Anfahren zu ermöglichen.

Wer sich nicht für die internen Details der Regelung interessiert, sollte zumindest den kompletten Abschnitt [Kalibrieren der Motorregelung](#Kalibrieren-der-Motorregelung) lesen, um die Regelung korrekt einzustellen.

### Eine Übersicht aller Konfigurationsparameter

Folgende Parameter der Regelung lassen sich in *[include/bot-local.h](https://github.com/tsandmann/ct-bot/blob/master/include/bot-local.h)* einstellen:

* **`PID_Kp`** Der proportionale Anteil des PID-Reglers. Er gibt an, wie stark sich der aktuelle Fehler auf die  Korrektur der Geschwindigkeit auswirkt. Hier ist in der Regel ein relativ hoher Wert sinnvoll, zugelassen sind Werte von 0 (schaltet den P-Anteil komplett aus) bis 127.
* **`PID_Ki`** Der integrale Anteil des PID-Reglers. Er gibt an, wie stark sich die Summe der letzten Fehler auf die Korrektur der Geschwindigkeit auswirkt. Hier ist in der Regel ein eher kleinerer Wert günstig, zugelassen sind Werte von 0 (schaltet den I-Anteil komplett aus) bis 127.
* **`PID_Kd`** Der differentielle Anteil des PID-Reglers. Er gibt an, wie stark sich die aktuelle Änderung der Geschwindigkeit (also die Beschleunigung) auf die Korrektur auswirkt. Auch hier ist nur ein kleiner Wert passend, zugelassen sind Werte von 0 (schaltet den D-Anteil komplett aus) bis 127.
* **`PID_Ta`** Die Abtastzeit. Sie gibt das Verhältnis zwischen der Zeitspanne, die seit dem letzten Regleraufruf vergangen ist, und der für die Berechnung erwarteten Zeitspanne an. Normalerweise braucht man hier nichts ändern und lässt den Wert auf 1.
* **`PID_SHIFT`** Der Divisor der Korrektur. Er gibt an, durch welchen Wert die berechnete Änderung geteilt wird. Anzugeben ist hier der Logarithmus zur Basis 2 (die Division erfolgt durch Bit-Shifting). Damit wird eine möglichst genaue Einstellung von `PID_Kp`, `PID_Ki` und `PID_Kd` ermöglicht.
* **`PID_TIME`** Das Zeitintervall, nach dem der Regler spätestens aufgerufen wird in Millisekunden. Wurde nach dieser Zeit keine Encoderflanke registriert, wird von Stillstand ausgegangen. Hier sollte man sich an dem Defaulwert orientieren, Feintuning verbessert evetuell das Verhalten bei sehr kleinen Geschindigkeiten. Zugelassen sind Werte von 0 (das ist aber nicht sinnvoll!) bis 655.
* **`PID_SPEED_THRESHOLD`** Die (Soll-)Geschwindigkeit, ab der die Berechnung der Istgeschwindigkeit per Interpolation zwischen mehreren Messwerten erfolgt. Sinvoll sind hier `BOT_SPEED_SLOW`, `BOT_SPEED_FOLLOW` oder `BOT_SPEED_MEDIUM`. Detaillierte Informationen finden sich im Erklärungstext.
* **`PWMMAX`** Maximaler PWM-Wert. Normalerweise nicht zu verändern.
* **`PWMMIN`** Minimaler PWM-Wert. Normalerweise nicht zu verändern.
* **`PWMSTART_L`** PWM-Startwert für den linken Motor. Hier sollte man einstellen, ab wann der Motor zu drehen beginnt (unter Last, nicht im Leerlauf).
* **`PWMSTART_R`** PWM-Startwert für den rechten Motor. Hier sollte man einstellen, ab wann der Motor zu drehen beginnt (unter Last, nicht im Leerlauf).
* **`PID_START_DELAY`** Dauer der Anfahrverzögerung in Anzahl von Regleraufrufen. Ein kleiner Wert sorgt für schnelleres Anfahren, vermindert aber die Stabilität der Regelung. Sinnvolle Werte liegen zwischen 10 und 30.
* **`ENC_CORRECT_L`** Korrektur der vom linken Encoder gemessenen Geschwindigkeit in mm/s, falls die Sollgeschwindigkeit kleiner als `PID_SPEED_THRESHOLD` ist. Da das Messverhalten der Radencoder nicht symmetrisch ist, kommt es zu falschen Geschwindigkeitsdaten, wenn die Zeit zwischen zwei direkt aufeinander folgenden Flanken gemessen wird. Um den hier angegebenen Wert wird die errechnete Geschwindigkeit korrigiert, falls der Encoderpegel der letzten Flanke HIGH war, anderfalls wird um das Inverse korrigiert. Sinvoll sind Werte zwischen -15 und +15. Wenn der Radencoder kalibriert wurde (Vorwiderstand angepasst) und symmetrisch arbeitet, auf 0 setzen!
* **`ENC_CORRECT_R`** Korrektur der vom rechten Encoder gemessenen Geschwindigkeit in mm/s.

### Die eigentliche Regelung

Die Motorregelung basiert auf einem gewöhnlichen PID-Regler. Dieser ist in der Funktion **`speed_control(uint8_t dev, int16_t * actVar, uint16_t * encTime, uint8_t i_time, uint8_t enc)`** implementiert. Diese Funktion wird an zwei Stellen aufgerufen: Erstens aus **`bot_encoder_isr()`** heraus, wenn dort eine neue Flanke eine Radencoders festgestellt wurde und zweitens aus **`bot_sens()`** heraus, falls in den letzten `PID_TIME` ms keine Flanke registriert wurde. Letzteres deshalb, damit ein Stillstand des Bots nicht zum Verhungern des Reglers führt.

Wird durch den Aufruf von **`motor_set()`** eine neue Sollgeschwindigkeit gesetzt, sind zwei Fälle zu unterscheiden:

1. Die vorherige Geschwindigkeit war gleich null, es liegt also ein Anlaufen des jeweiligen Rades vor. In diesem Fall ist die Sollgeschwindigkeit zuächst immer `BOT_SPEED_SLOW` (oder -`BOT_SPEED_SLOW`) und wird in den nächsten `PID_START_DELAY` Regleraufrufen schrittweise auf die gewünschte Sollgeschwindigkeit erhöht. Hierdurch wird einerseits eine einheitliche Behandlung des Anlauf-Falls ermöglicht, was die Codekomplexität deutlich reduziert und andererseits ein (nahezu) ruckfreies Anfahren des Bots erreicht (ist der Verlauf der Geschwindigkeit eine Sinusfunktion, so ist die Beschleunigung (1. Ableitung) eine Cosinusfunktion und der Ruck (2. Ableitung) wieder eine Sinusfunktion - wir arbeiten auf Rücksicht der fehlenden FPU der MCU allerdings nicht mit Sinus, sondern nur mit einer groben Näherung).
1. Die vorherige Geschwindigkeit war ungleich Null, das Rad ist also bereits in Bewegung. In diesem Fall entfallen die unter 1. beschriebenen Spezialfälle vollständig und der Regler nimmt einfach die neue Sollgeschwindigkeit als Führungsgröße, den Rest übernimmt der Code automatisch.

### Sensorauswertung

Zur Berechnung der aktuellen Geschwindigkeit werden die Radencoder benutzt. Das Messverfahren für die Motorregelung weicht von der allgemeinen Geschwindigkeitsberechnung des Bots aus zwei Gründen ab: Erstens ist die per **`sensor_update()`** berechnete Geschwindigkeit für die Regelung zu ungenau und erfolgt zweitens viel zu selten. Eine schnelle Regelung erfordert das Vorhandensein wirklich aktueller und zu garantierten Zeiten bereitstehenden Geschwindigkeitsdaten. Berechnet wird die Geschwindigkeit des jeweiligen Rades aus der Zeitdifferenz zweier Encoderflanken. Hierbei ist zu beachten, dass zwei direkt aufeinander folgende Flanken unterschiedlicher Natur sind - war die Letzte eine steigende Flanke, so muss die Nächste zwangsläufig eine Fallende sein und umgekehrt. Die Radencoder registrieren die Flanken in Abhängigkeit der Lichtreflexion der Encoderscheiben, was zur Folge hat, dass bei konstanter Drehgeschwindigkeit des Rades die Zeitspanne zwischen einer Steigenden und einer fallenden Flanke nicht gleich der Zeitspanne zwischen einer Fallenden und einer steigenden Flanke sein muss. Zwischen Flanken gleicher Art vergeht jedoch bei konstanter Geschwindigkeit immer gleich viel Zeit. Hieraus ergibt sich folgende Konsequenz: Entweder zieht man zur Berechnung der Geschwindigkeit jeweils nur Flanken gleicher Art heran, oder man korrigiert die Ungleichheit der Zeitdifferenzen
per Software. Ersteres sorgt für eine deutlich langsamere Geschwindigkeitserfassung, Letzteres für komplexeren Code und mehr Konfigurationsparameter. Da bei hohen Geschwindigkeiten sehr oft eine Flanke der Encoder eintrifft, verwendet der Regelungscode das erstgenannte Verfahren, falls die Sollgeschwindigkeit größer als `PID_SPEED_THRESHOLD` ist. Außerdem wird die Geschwindkeit aus den letzten vier Encoderflanken berechnet, wenn die Sollgeschwindigkeit größer als `2 * PID_SPEED_THRESHOLD` ist, um Ungenauigkeiten zu vermeiden, wenn das Zeitintervall zwischen zwei Flanken auf Grund der hohen Geschwindigkeit sehr klein ist. Für langsame Geschwindigkeiten erweist sich das Verfahren allerdings als zu träge, deshalb wird bei Geschwindigkeiten unterhalb von `PID_SPEED_THRESHOLD` mit jeder Encoderflanke gerechnet und die gemessene Geschwindigkeit um den Betrag `ENC_CORRECT_L` bzw. `ENC_CORRECT_R` korrigiert.

#### Kalibrieren der Radencoder

Eine genauere Messung der Geschwindigkeiten ist mit einer Kalibrierung der Radencoder zu erreichen: Dazu passt man den Vorwiderstand so an, dass die Zeitspanne zwischen zwei direkt aufeinander folgenden Flanken bei konstanter Geschwindigkeit immer nahezu gleich ist. Dadurch kann auch eine Geschwindigkeit von nur 30 mm/s noch ausreichend gut eingeregelt werden (`BOT_SPEED_MIN` in [include/motor.h](https://github.com/tsandmann/ct-bot/blob/master/include/motor.h) anpassen!). Anschliessend muss man `ENC_CORRECT_L` und `ENC_CORRECT_R` auf 0 setzen, da die Rohdaten der Encoder bereits eine genaue Geschwindigkeitsmessung ergeben. Insgesamt erreicht man so eine deutliche Verbesserung der Motorregelung.

### Kalibrieren der Motorregelung

Um die optimalen Fahreingenschaften des Bots zu erreichen, muss die Motorregelung passend kalibriert sein. Da dieser Vorgang jedoch etwas langwieriger ist, empfiehlt es sich, den Bot zunächst mit den Standardparametern auszuprobieren. Wichtig ist hier das Anfahrverhalten, die Geradeausfahrt und die Gleichmäßigkeit beim Drehen mit langsamer Geschwindigkeit zu überprüfen. Sind diese Kriterien ausreichend gut erfüllt, kann man die Kalibrierung auch erstmal zurückstellen oder darauf ganz verzichten.

#### Automatische Kalibrierung

Das Wichtigste für eine gut funktionierende Regelung sind die passenden Parameter *Kp*, *Ki* und *Kd*. Allerdings ist das Berechnen nicht ganz einfach. Deshalb gibt es ein kleines Verhalten, das automatisch versucht die besten Parameter zu finden. Um es zu benutzen, sind folgende Schritte nötig:

1. Idealerweise zunächst die Radencoder kalibrieren (Vorwiderstand anpassen, siehe [Sensorauswertung](#Sensorauswertung)).
1. Einschalten des Verhaltens `BEHAVIOUR_CALIBRATE_PID_AVAILABLE` in *[ct-Bot.h](https://github.com/tsandmann/ct-bot/blob/master/ct-Bot.h)* (siehe auch [Übersicht der optionalen Codeteile](../../doc/wiki_pages/ct-bot_h.md)).
1. Code neu Übersetzen und auf den Bot übertragen (siehe auch **[Übertragen von Firmware in den AVR-Mikrocontroller](../Flash/Flash.md)**).
1. Die Funktion **`bot_calibrate_pid(Behaviour_t* caller, int16_t speed)`** aufrufen, sehr elegant geht das per Bot-Remote-Call. Alternativ kann man auch einfach eine Taste der Fernbedienung (FB Taste **6**) für den Aufruf verwenden. Als Parameter **`speed`** übergibt man eine Geschwindigkeit, mit der kalibriert werden soll, `BOT_SPEED_SLOW` eignet sich hier am besten.
1. Nun führt der Bot einige Drehungen aus, auf dem Regelungs-Screen im Display sieht man den aktuellen Status und die verbleibende Zeit bis zum Ende der Kalibrierung. Dabei werden per LOG Zwischenergebnisse ausgegeben, falls LOG aktiviert ist im Code. Ist die Kalibrierung beendet, stellt das Verhalten die gefundenen Parameter ein und zeigt sie im Display an. Allerdings werden sie **nicht** dauerhaft gespeichert, hierzu überträgt man sie in *[include/bot-local.h](https://github.com/tsandmann/ct-bot/blob/master/include/bot-local.h)* und deaktiviert das Verhalten wieder (ist das Verhalten aktiv, arbeitet die Regelung nicht ganz so effizient, weil die Parameter variabel sind).

Hinweis: Der im nächsten Absatz beschriebene Parameter `PID_SHIFT` wird durch das Verhalten nicht verändert, wenn man ihn (leicht!) variiert, arbeitet das Verhalten also in unterschiedlichen "Regionen", genaueres dazu s.u.

#### Manuelle Kalibrierung

Alternativ lassen sich die Parameter auch manuell bestimmen, das folgende Einstellverfahren liefert dazu bei vertretbarem Aufwand die besten Ergebnisse:

1. Zuerst stellt man **`PID_Kp`**, **`PID_Ki`** und **`PID_Kd`** in *[include/bot-local.h](https://github.com/tsandmann/ct-bot/blob/master/include/bot-local.h)* auf **0** und aktiviert das #define **`ADJUST_PID_PARAMS`** in *[ct-Bot.h](https://github.com/tsandmann/ct-bot/blob/master/ct-Bot.h)* sowie **`DISPLAY_REGELUNG_AVAILABLE`** in *[ui/available_screens.h](https://github.com/tsandmann/ct-bot/blob/master/ui/available_screens.h)*. Flasht man nun das erzeugte hex-File auf den Bot, so gibt es einen Display-Screen für die Regelung, der außerdem eine spezielle Tastenbelegung aktiviert. Die erste Displayzeile stellt Istgeschwindigkeit / Sollgeschwindigkeit dar, die Zweite den Betrag des aktuellen Regelfehlers und die Dritte den zurzeit gestellten PWM-Wert, jeweils für links und rechts. Die letzte Zeile gibt die derzeit einstellten PID-Parameter aus.
1. Nun sollte der Bot mit `BOT_SPEED_SLOW`, also 50 mm/s, auf der Stelle drehen. Das erreicht man am Einfachsten mit der Pfeiltaste links oder rechts auf der Fernbedienung.
1. Anschließend erhöht man schrittweise `Kp` mit der Taste 1, bis sich der Bot noch mit annähernd konstanter Geschwindigkeit auf der Stelle dreht. Wird `Kp` zu groß, beginnt der Regler zu schwingen und man stellt `Kp` mit der Taste 4 wieder etwas zurück, bis das Schwingen aufhört.
1. Jetzt kann man `Ki` mit der Taste 2 vergrößern, der Wert sollte aber deutlich kleiner als `Kp` bleiben. Mit der Taste 5 kann man `Ki` wieder verringern. Mit erhöhtem `Ki` kann man auch `Kp` noch ein wenig vergrößern, da der Regler nun stabiler geworden sein sollte.
1. Es empfiehlt sich, während des Einstellens den Bot ab und zu anzuhalten und das Drehen oder Fahren aus dem Stand von Neuem beginnen zu lassen, um überprüfen zu können, ob der Regler auch schnell genug die gewünschte Sollgeschwindigkeit einregelt. Hier hilft eventuell der D-Anteil des PID-Reglers, den man mit dem Parameter `PID_Kd` aktiviert. Taste 3 erhöht diesen, Taste 6 verringert ihn. Vorsicht, ist `Kd` zu groß, leidet die Stabilität der Regelung darunter.
1. Hat man die Parameter gefunden, die zum besten Ergebnis führen, so trägt man diese in *[include/bot-local.h](https://github.com/tsandmann/ct-bot/blob/master/include/bot-local.h)* ein und schaltet das #define `ADJUST_PID_PARAMS` in *[ct-Bot.h](https://github.com/tsandmann/ct-bot/blob/master/ct-Bot.h)* wieder aus, damit ein Teil der PID-Regler-Gleichung bereits zur Compilezeit berechnet und der Mikrocontroller somit entlastet werden kann.

Allgemein gilt für die Parameter: Je größer sie sind, desto *schneller* ist die Regelung, je kleiner sie sind, desto *stabiler* ist die Regelung. Sollte der Wertebereich von 0 bis 127 nicht ausreichen, so kommt der Parameter `PID_SHIFT` ins Spiel. Erhöht man ihn um eins, so ist das Gleichbedeutend mit der Halbierung von `Kp`, `Ki` und `Kd`. Verringert man ihn um eins, so entspricht das einer Verdoppelung von `Kp`, `Ki` und `Kd`. Für die beste Einstellgenauigkeit wählt man also `PID_SHIFT` so, dass `PID_Kp` (sollte den größten Wert unter den Parametern haben) zwischen 64 und 127 liegt.

Da das Einstellen der Parameter etwas knifflig ist, wäre es schön und hilfreich, die eingestellten Parameter ebenso wie weitere Erfahrungen mit der Regelung zu sammeln. Dazu dazu bietet sich das [Forum](https://www.ctbot.de) an. Wenn dann z.B. auf 90 % aller Bots die Parameter x, y, z die besten Ergebnisse liefern, werden dies die Default-Werte.

### Die Logging-Funktion

> **Trac-2-Markdown Konvertierung:** *deprecated*

Möchte man genauer analysieren, wann der Bot wie schnell fuhr und wie exakt die gewünschte Geschwindigkeit eingeregelt wurde, kann man dafür während des Fahrens einige Daten mitloggen lassen, die auf einer MMC oder SD-Karte gespeichtert werden. Dazu aktiviert man das #define **`SPEED_LOG_AVAILABLE`** in *[ct-Bot.h](https://github.com/tsandmann/ct-bot/blob/master/ct-Bot.h)* und stellt außerdem sicher, dass **`MMC_AVAILABLE`** und **`BOT_FS_AVAILABLE`** (siehe [SD-Karten Dateisystem BotFS](../deprecated/DokuBotFs/DokuBotFs.md)) an sind. Nun werde einige Daten im Bot-Betrieb gesammelt und automatisch aufgezeichnet.

Hat der Bot seine Fahraufgaben beendet, nimmt man die SD-Karte heraus, steckt sie in einen PC und ruft **`ct-Bot -l /pfad/zur/sd-karte/botfs.img`** (Linux / Mac OS X) bzw. **`ct-Bot.exe -l S:\botfs.img`** (Windows) auf, was die Log-Datei auf der SD-Karte aus dem Bot-Format in eine txt-Datei mit dem Namen slog.txt im Arbeitsverzeichnis von ct-Bot konvertiert. Diese kann man entweder mit einem Texteditor seiner Wahl oder - und das ermöglicht eine schnelle und anschauliche Auswertung - mit einer Tabellenkalkulation öffnen. Die Spalten sind durch Tabs getrennt, der Inhalt der jeweiligen Spalte geht aus der Überschrift hervor. Der erste / obere Teil der txt-Datei enthält die Daten des linken Rades, der Untere die des Rechten. Man sollte die Tabelle als erstes nach der Spalte *Timestamp* sortieren, damit die Reihenfolge der Daten korrekt ist. Multipliziert man die Einträge der Spalte *Timestamp* mit 176, so erhält man als Einheit Mikrosekunden. Jede gängige Tabellenkalkulation stellt die Daten nun mit wenigen Mausklicks als Diagramm dar oder rechnet beliebige Dinge aus.

Alternativ gibt es in *[contrib/tools](https://github.com/tsandmann/ct-bot/tree/master/contrib/tools)* ein GNU-Plot Script von Harald W. Leschner zur grafischen Auswertung der slog.txt-Datei.

Es sei noch angemerkt, dass die Priorität dieses Log-Verfahrens zum Entstehungszeitpunkt auf Performance lag, um die Laufzeit der Funktionen auf dem Bot möglichst unverändert zu lassen. Außerdem ist das Ganze als Debug-Ausgabe während der Entwicklung entstanden und glänzt nicht mit üppiger Funktionalität oder gar Schönheit. Es ist aber auch zum Einstellen und / oder bewerten von Ergebnissen hilfreich und daher im Code geblieben.

## Klappe des Transportfachs

ToDo

[![License: CC BY-SA 4.0](../../License.svg)](https://creativecommons.org/licenses/by-sa/4.0/)