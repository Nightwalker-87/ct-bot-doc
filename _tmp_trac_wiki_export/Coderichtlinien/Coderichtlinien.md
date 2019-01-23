# Richtlinien für Erweiterungen am c't-Bot und c't-Sim (coding conventions)

>> **Trac-2-Markdown Konvertierung:** *unchecked*

Fremden Code lesen kann ganz sch&#246;n anstrengend sein &mdash; ein Variablenname, der dem einen selbsterkl&#228;rend vorkommt, kann auf den anderen kryptisch wirken. Wenn Sie einen Patch schreiben und Ihren Code m&#246;glichst verst&#228;ndlich programmieren und dokumentieren, steigen die Chancen, dass andere c't-Bot-Fans von Ihrer Arbeit ebenfalls profitieren. Als Hilfe haben wir ein paar Richtlinien zusammengestellt, die f&#252;r &#220;bersicht im c't-Roboter-Projekt sorgen sollen.

Zugegeben: Bislang erf&#252;llt die offizielle Codebasis diese Richtlinie ebenfalls (noch) nicht bis ins letzte Detail &mdash; wir arbeiten aber daran, das zu &#228;ndern. Deshalb kommen uns Patches von Ihrer Seite sehr entgegen, welche die aufgestellten Regeln einhalten.

Damit Patches f&#252;r den Code m&#246;glichst kompatibel zueinander sind und &#252;berschaubar bleiben, sollten sie schlank sein. Faustregel: Ein Patch pro Thema. Insbesondere Formatierungs&#228;nderungen usw. bl&#228;hen den Patch stark auf und machen ihn im Zweifelsfall inkompatibel zu anderen.

## Allgemeine Richtlinien

* *Namen von Variablen, Konstanten, Funktionen und alles, was direkt mit dem Quellcode zu tun hat, sollten rein englisch sein.
* *Kommentare und Dokumentation sollen dagegen auf Deutsch verfasst werden. Bitte benutzen Sie hierbei keine Umlaute und kein '&#223;', da diese Zeichen von Windows, Linux, Mac, Solaris, usw. unterschiedlich gehandhabt werden &mdash; sie tauchen bald nur noch als Zeichensalat im Code auf.
* Variablen, die in c't-Bot und c't-Sim die gleichen Werte haben, sollten auch die gleichen Namen bekommen. Das macht vieles einfacher und vermeidet Verwechslungen.
* Alle Funktionen und Methoden sollen vollst&#228;ndig kommentiert werden. Hierzu geh&#246;rt eine kurze Beschreibung, WAS die Funktion tut (aber nicht zwingend, WIE sie das tut), eine Erl&#228;uterung von &#220;bergabeparametern und R&#252;ckgabewerten sowie der im Java-Teil unter Umst&#228;nden geworfenen Exceptions. Bei trivialen Methoden wie Konstruktoren oder get()- und set()-Methoden kann die Kurzbeschreibung oft auch weggelassen werden.
* Die Kommentare zu Klassen, Funktionen und Methoden sollen [Doxygen-](http://www.stack.nl/~dimitri/doxygen/docblocks.html) beziehungsweise [Javadoc](http://java.sun.com/j2se/javadoc/writingdoccomments)-konform gestaltet werden &mdash; auf diese Weise kann man aus dem Code bequem durchsuchbare HTML-Seiten generieren.
* Bei allen &#196;nderungen bitte Eintr&#228;ge in die jeweilige Changelog-Datei nicht vergessen. Hier sollte neben dem Datum der &#196;nderung, Ihrem Namen und der E-Mail-Adresse noch ein kurzer Text stehen, der darstellt, inwiefern Ihre Erweiterung den Roboter oder den Simulator verbessert. Wird der Patch (vorerst) nicht ins offizielle Release &#252;bernommen, sondern separat auf der Projektseite ver&#246;ffentlicht, sollte dieser Text auch als Beschreibung des Patches tauglich sein.
* Der komplette Code - und damit auch jede Erweiterung - steht unter der GPL. Daher m&#252;ssen neu hinzugef&#252;gte Dateien auch einen GPL-Header besitzen.

## c't-Bot

* Bitte verwenden Sie NICHT den Datentyp int &mdash; PC und MCU interpretieren diesen verschieden! Stattdessen stehen die Typen `int8_t`, `uint8_t`, `int16_t`, `uint16_t`, `int32_t` und `uint32_t` zur Verf&#252;gung. Hierbei steht die angeh&#228;ngte Zahl f&#252;r die Bits, die zum Speichern des Integer-Werts verwendet werden, das vorangestellte 'u' steht f&#252;r 'unsigned', diese Typen speichern nur positive Werte. Bitte pr&#252;fen Sie sorgf&#228;ltig, in welchem Bereich die Werte Ihrer Variable liegen werden und w&#228;hlen Sie den passenden Datentyp.

    Die Wertebereiche liegen im Einzelnen bei:
    ```C
    int8_t zwischen -128 und 127
    uint8_t zwischen 0 und 255
    int16_t zwischen -32.768 und 32.767
    uint16_t zwischen 0 und 65.535
    int32_t zwischen -2.147.483.648 und 2.147.483.647
    uint32_t zwischen 0 und 4.294.967.295
    ```

  * Den Datentyp char sollten Sie ebenfalls nur verwenden, wenn es sich wirklich um ein Zeichen handelt. Ansonsten verwenden Sie bitte ebenfalls `uint8_t` oder `int8_t`.
  * Bei Programmieren von Verhaltensweisen f&#252;r das c't-Bot-Framework gilt folgende Konvention:
    * Verhaltensweisen (Behaviours), die vom Framework bearbeitet werden, hei&#223;en `bot_xxx_behaviour`.
    * Die Botenfunktionen, die solche Verhaltensweisen aufrufen und aktivieren, hei&#223;en `bot_xxx`. Beispiel: Die Botenfunktion `bot_drive_distance()` ruft die Verhaltensweise `bot_drive_distance_behaviour()` auf.

## c't-Sim

* Alle Variablen und Konstanten, die sich auf Sensoren beziehen, beginnen mit `sens` oder `SENS`, alle Aktuator-Wert mit `act`. Auch in Methoden, die mit den Sensoren oder Aktuatoren zu tun haben, finden sich die Bezeichner `sens` und `akt` wieder (`getSensBorderPosition()`).
* Bitte beachten Sie beim Programmieren auch die &#252;blichen [Java-Coding-Conventions](http://java.sun.com/docs/codeconv), etwa:
  * Methodennamen sollten aus Verben bestehen und mit einem kleinen Buchstaben beginnen. Bestehen Namen aus mehreren W&#246;rtern, werden diese direkt hintereinander geschrieben, wobei alle au&#223;er dem ersten mit einem Gro&#223;buchstaben beginnen (`senseGroundReflectionCross()`).
  * F&#252;r Variablennamen gilt die gleiche Schreibweise wie f&#252;r Methoden (vorne mit einem kleinen und im Inneren mit gro&#223;en ersten Buchstaben). Variablennamen sollten kurz, aber verst&#228;ndlich sein (`lightBG` f&#252;r die BranchGroup der Lichtquellen im c't-Sim).
  * F&#252;r Variablennamen gilt die gleiche Schreibweise wie f&#252;r Methoden (vorne mit einem kleinen und im Inneren mit gro&#223;en ersten Buchstaben). Variablennamen sollten kurz, aber verst&#228;ndlich sein (`lightBG` f&#252;r die BranchGroup der Lichtquellen im c't-Sim).
  * Variablennamen aus einem einzelnen Buchstaben sind zu vermeiden, Ausnahme sind Z&#228;hlervariablen, die beispielsweise nur innerhalb einer Schleife existieren (`for (int i=0; i<10; i++) {...}`).
  *F&#252;r Variablennamen gilt die gleiche Schreibweise wie f&#252;r Methoden (vorne mit einem kleinen und im Inneren mit gro&#223;en ersten Buchstaben). Variablennamen sollten kurz, aber verst&#228;ndlich sein (`lightBG` f&#252;r die BranchGroup der Lichtquellen im c't-Sim).
  * Konstanten sollen in Gro&#223;buchstaben geschrieben werden, die einzelnen W&#246;rter zusammengesetzter Bezeichner werden mit Unterstrichen getrennt (`LIGHT_SOURCE_REACH`).

* *Haben Sie an einer Datei etwas ver&#228;ndert (beispielsweise eine neue Methode hinzugef&#252;gt), k&#246;nnen Sie sich unter dem Dokumentationstext der gesamten Klasse &#252;ber das Tag `@author` mit Namen und E-Mail-Adresse verewigen.

[![License: CC BY-SA 4.0](../license.svg)](https://creativecommons.org/licenses/by-sa/4.0/)
