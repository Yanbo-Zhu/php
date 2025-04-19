
**PHP kennt zahlreiche Kontrollstrukturen, wie z.B.:**

- [if](http://php.net/manual/de/control-structures.if.php)
- [for](http://php.net/manual/de/control-structures.for.php)
- [continue](http://php.net/manual/de/control-structures.continue.php)
- [foreach](http://php.net/manual/de/control-structures.foreach.php)
- [while](http://php.net/manual/de/control-structures.while.php)
- [switch](http://php.net/manual/de/control-structures.switch.php)
- [break](http://php.net/manual/de/control-structures.break.php)

  
Weitere sind unter [http://php.net/manual/de/language.control-structures.php](http://php.net/manual/de/language.control-structures.php) aufgelistet.

Diese Funktionen weichen nicht vom üblichen Gebrauch der Syntax ab, außer _foreach_, welches auf einer der folgenden Seiten erläutert wird.

_unless_, _until_ und _do-until_ gibt es in PHP nicht.

# 1 If & if-elseif-else

**if-Bedingung**  
```
if ($day === 0 or $day === 6) {
    echo "Wochenende"!;
}
```

  
**if-elseif-else-Bedingung**  
```
if ($digit === 0) {
    echo "digit ist gleich 0";
} elseif ($digit > 0) {
    echo "digit ist größer als 0";
} else {
    echo "digit ist kleiner als 0";
}
```
Ein negiertes _if_ schreibt sich mit dem Ausrufezeichen: _if (!$value == $password)_. Hierbei wird die gesamte _if_-Abfrage negiert und nicht der erste Wert.

  
**Kurzform für if-else (Ternäre Operatoren)**  
In PHP gibt es verschiedene Formen die _if-elseif-else-_Bedingungen zu schreiben. Es wird allerdings empfohlen die Standardversion zu nutzen, um die Lesbarkeit zu erhöhen. Bei zeitkritischen Anwendungen empfehlen sich aber die Ternären Operatoren.
```
$c = $a > $b ? $a : $b;

entspricht

if ($a > $b) {
    $c = $a;
} else {
    $c = $b;
}
```


Ternäre Operatoren eignen sich sehr gut, um in sehr kurzer Form Wörter in Abhängigkeit von Anzahl auszugeben.  

```
echo "Anzahl: $count " . ($count == 1 ? "Buch" : "Bücher") . " gefunden";
```



Ein Student hat ein Problem mit der folgenden Zeile PHP-Code:  

```
echo '<input name="postcode" value="', (isset($_POST['postcode'])) ? 
$_POST['postcode'] : ''; , '" />';
```

Das Problem: "Er meckert immer das Komma nach dem ersten ; an."  
Können Sie den Fehler finden und Ihr helfen?

Das Problem ist hier nicht das Komma, sondern das Semikolon. Dieses kann in diesem Fall einfach entfernt werden, da der PHP-Interpreter ein Semikolon als Anweisungsende interpretiert und deshalb eine neue Anweisung erwartet. Ein Komma stellt jedoch keine Anweisung dar, deshalb bricht der PHP-Interpreter hier mit einer Fehlermeldung bezüglich des Kommas ab.

# 2 For, continue

Die _for_-Schleife ist eine oft genutzte Schleife in PHP und verhält sich wie die _for_-Schleife in C. Sie erwartet drei durch Semikolons getrennte Anweisungen. Die erste Anweisung wird dabei vor jeder Ausführung der Schleife ausgeführt. Die zweite Anweisung wird zur Überprüfung genutzt. Dabei wird die Schleife nur ausgeführt, wenn diese Anweisung den Wert Wahr (_true_) zurückgibt. Am Ende jedes Schleifendurchlaufes wird dann die dritte Anweisung ausgeführt.

Üblicherweise nutzt man diese Schleife, wenn etwas für eine bestimmte Anzahl wiederholt werden soll.

```
for ($count = 1; $count <= 10; $count++) {
    echo "$count <br>";
}
```

In der Ausgabe wird so einfach von 1 bis 10 hoch gezählt. Die Schleife wird somit 10-mal durchlaufen, da _`$count`_ kleiner oder gleich 10 ist. Erst nach dem 10. Durchlauf wird `_$count_` auf 11 gesetzt, wodurch die Schleife nicht mehr ausgeführt wird.

In einer for-Schleife sollten aber nie feste Werte eingetragen werden. Der folgende Sourcecode ist somit viel professioneller:

```
$start =  1;
$stop  = 10;
for ($count = $start; $count <= $stop; $count++) {
    echo "$count <br>";
}
```



Überlegen Sie sich eine for-Schleife, die von 200 in 5er-Schritten runter zählt auf 100.
```
$start = 200;
$stop  = 100;
$step  =   5;
for ($count = $start; $count >= $stop; $count -= $step) {
    echo "$count <br>";
}
```



Überlegen Sie sich eine for-Schleife, die die Summe der Zahlen im Bereich 20 bis 50 bildet. Die Ausgabe soll wie folgt aussehen: 20+21+22+...+49+50=1085  

Achtung: Die Aufgabe ist nicht ganz trivial.
```
$start  = 20;
$stop   = 50;
$result =  0; // wird als Integer initialisiert
for ($count = $start; $count < $stop; $count++) {
    echo "$count"."+";
    $result = $result + $count;
} 
// noch den letzten Wert $stop addieren
$result = $result + $stop;
echo "$stop" . "=" . "$result";
```


continue
Die continue-Anweisung ist in manchen Situationen sehr hilfreich. Hierdurch wird der aktuelle Schleifen-Durchgang sofort unterbrochen und die Bedingung neu geprüft.
In der for-Schleife soll nun die Ausgabe des Wertes 6 übersprungen werden:
```
$start =  1;
$stop  = 10;
$skip  =  6;
for ($count = $start; $count <= $stop; $count++) {
    if ($count === $skip) {
        continue;
    }
    echo "$count <br>";
}
```

Ein continue kann in auch in foreach- und while-Schleifen verwendet werden.




# 3 Foreach

Diese Schleife arbeitet alle Elemente eines Arrays ab, wobei dies unabhängig vom Arraytyp ist. Durch die automatische Zuweisung in eine Variable pro Schleifendurchgang, kann mit nur minimalem Code schon eine umfangreiche Iteration durchgeführt werden.


```
$rgb = ["Red", "Green", "Blue"];
$cmyk = ["C" => "Cyan", "M" => "Magenta", "Y" => "Yellow", "K" => "Key"];   
echo "rgb besteht aus: ";
foreach ($rgb as $color) {
    echo "$color, ";
}   
echo "<br>cmyk besteht aus: ";
foreach ($cmyk as $letter => $color) {
    echo "$letter für $color, ";
}
```
Ausgabe:  
_rgb besteht aus: Red, Green, Blue,_  
_cmyk besteht aus: C für Cyan, M für Magenta, Y für Yellow, K für Key,_

  
**Letzten Wert entfernen mit _array_pop()_**  
Das assoziative Array _$_POST_ kann Daten aus einem Formular enthalten. Der letzte Datensatz besteht dabei typischerweise aus den Daten des Absendebuttons. Somit ist es oft sinnvoll, dass ein letzter Datensatz einfach entfernt werden soll. Dies kann mit _array_pop()_ erfolgen (siehe **Zeilen 4 & 5**).

```
$rgb = ["Red", "Green", "Blue"];
$cmyk = ["C" => "Cyan", "M" => "Magenta", "Y" => "Yellow", "K" => "Key"];   
$lastRgb  = array_pop($rgb);
$lastCmyk = array_pop($cmyk);
echo "rgb besteht aus: ";
foreach ($rgb as $color) {
    echo "$color, ";
}   
echo "<br>cmyk besteht aus: ";
foreach ($cmyk as $letter => $color) {
    echo "$letter für $color, ";
}
```
Ausgabe:  
_rgb besteht aus: Red, Green,_  
_cmyk besteht aus: C für Cyan, M für Magenta, Y für Yellow,_

In den Variablen `$lastRgb`_ bzw. `$lastCmyk`_ (siehe **Zeilen 4 & 5**) stehen die gelöschten Elemente drin. Somit kann man die gelöschten Elemente im Programm noch anderweitig verwenden.

  ---
  
**Achtung Sicherheitshinweis**
`foreach ($_POST as $color)` funktioniert zwar, ist aber nicht sicher, da eventuell nicht nur die gewünschten Variablen in dem Array `_$_POST`_ stehen, sondern auch manipulierte Variablen an das PHP-Programm weitergereicht werden könnten. Somit sollte `foreach ($_POST as $color)` nur verwendet werden, wenn anschließend mit regulären Ausdrücken ALLE ungewünschten Daten herausgefiltert werden.

---


Wie kann man ein assoziatives Array unbekannter Länge mittels foreach() einfach in ein indiziertes Array umwandeln?


Gegeben sei das assoziative Array _$wish_ unbekannter Länge mit der Struktur  
`_$wish = ["w1" => "Urlaub", "w2" => "Sonne", "w3" => "Meer", "w4" => "Eis",...]_.  `
Die Umwandlung mit _foreach()_ in ein indiziertes Array kann hierbei sinnvoll sein, wenn die _Keys_ nicht benötigt werden.

```
$wish = ["w1" => "Urlaub", "w2" => "Sonne", "w3" => "Meer", "w4" => "Eis"];
foreach($wish as $key => $value) {
    $wishes[] = $value; // neues indiziertes Array der Reihe nach füllen.
}
```

Die foreach-Syntax für assoziative Arrays _foreach ($array as $key => $value)_ funktioniert übrigens auch bei indizierten Arrays. Was kommt dabei wohl heraus? Probieren Sie doch einmal aus.


# 4 Arrays im Array - Teil 2

Hier soll noch ein weiteres Beispiel gezeigt werden, wie Arrays zu einem Array sinnvoll verbunden werden können.

```
$fruits     = ["Äpfel", "Birnen", "Pflaumen"];
$vegetables = ["Tomaten", "Gurken", "Paprika", "Bohnen", "Spargel"];
$drinks     = ["Wasser", "Saft"];
$products   = [
    "Obst"     => $fruits,
    "Gemüse"   => $vegetables,
    "Getränke" => $drinks
];
foreach ($products as $category => $items) {
    echo "<h2>$category</h2>";
    echo "<ol>";
    foreach ($items as $item) {
        echo "<li>$item</li>";
    }
     echo "</ol>";
}
```


![](images/Pasted%20image%2020250419195212.png)


# 5 While

Die _while_-Schleife ist eine Schleife, die dann nützlich ist, wenn ein Stop-Wert nicht bekannt ist. Die Schleife erwartet lediglich eine Anweisung, die überprüft wird und bei "true" die Anweisungen in der geschweiften Klammer ausführt. Zu beachten ist, dass die Anweisung immer zu Rundenbeginn überprüft wird, das bedeutet, dass die Schleife z.B. auch überhaupt nicht ausgeführt werden kann oder endlos laufen könnte.

Einfache _while_-Schleife zur Ausgabe der Zahlen 1 bis 10.

```php
$start =  1;
$stop  = 10;
while ($start <= $stop) {
    echo $start++ . "<br>";
}
```
  
Die nächste _while_-Schleife soll so lange laufen, bis die Summe aller Zahlen, beginnend bei der Zahl "1" den Wert "20" überschritten hat. Also 1+2+3+4+5+...>20. Dies ist ein typisches Beispiel für eine sinnvolle _while_-Schleife.

```php
$value      =    1;
$stopResult =   20;
$result     =    0; // Initialisierng
while($result < $stopResult) {       
    $result = $result + $value;
    echo " $value <br>";
    $value++;
} 
echo "=== <br>";
echo "$result ist die Summe";
```

Ausgabe:  
```
Ausgabe:
1
2
3
4
5
6
===
21 ist die Summe
```



# 6 Switch, case, break, default

Die _switch-case_-Anweisung wird gerne benutzt, wenn mehrere genau definierte Zustände vorhanden sind. Sie wird z.B. verwendet, wenn man einen Wert mit verschiedenen anderen vergleichen will und abhängig vom Ergebnis verschiedene Funktionen ausgeführt werden sollen. Vergleichbar ist dies mit der _if/elseif-_Anweisung.  
_default_ wird ausgeführt, wenn keine der oben genannten _case_-Bedingungen zutrifft und sollte somit immer als letzte _case_-Anweisung angegeben sein.

```
$hour = date("H");
switch($hour) {
    case 8:
        echo "Gääähn";
        break;
    case 9:
        echo "Kaffee";
        break;
    case 10:
        echo "Aufstehen???";
        break;
    default:
        echo "OK";
}
```
  

Hinweis

Wenn am Ende einer _case_-Anweisung kein _break_ steht, werden alle folgenden _case_-Anweisungen ebenfalls ausgeführt. Dieses Verhalten kann manchmal sehr sinnvoll sein. Stellen Sie sich vor, Sie wollen einen Kalender erstellen, der die verbleibenden Wochentage bis Sonntag darstellt. Wenn heute Mittwoch wäre, dann würde diese Art der Schleife sehr einfach alle Tage bis Sonntag auflisten können.

# 7 Beispiel Formulare - Daten ausgeben

Durch bedingte Anweisungen, Schleifen und Sprungbefehlen können die übertragenen Daten nun überprüft und verarbeitet werden. Um jedoch den Rahmen dieses Kapitels nicht zu sprengen, wird die Überprüfung einfach gehalten und nur überprüft, ob diese Felder leer sind. Diese Überprüfung findet mit der Funktion [_empty()_](http://php.net/manual/de/function.empty.php) statt.

Zunächst wird zur Darstellung des Formulars das bereits bekannte Beispiel aus dem [Unterkapitel Formulare - Daten einlesen](https://isp.eduloop.de/loop/Beispiel_Formulare_-_Daten_einlesen "Beispiel Formulare - Daten einlesen") hier verwendet.

```php
<?php
/**
 * Beispiel Formular - Daten einlesen
 * @author Lisa Meijer 
 * @date 19.04.2019
 */

function writeHeaderAndHeadline()
{
    echo "<!DOCTYPE html>
          <html lang=\"de\">
          <head><title>Formular</title>
          </head>
          <body>
          <h1>Beispielformular</h1>";
}

function startForm($method, $url)
{
    echo "<form method=\"$method\" action=\"$url\">";
}

function writeInputField($text, $name)
{
    echo "<label for=\"$name\">$text: </label>
          <input type=\"text\" name=\"$name\" id=\"$name\">
          <br><br>";
}

function closeFormAndFooter()
{
    echo "<input type=\"submit\" value=\"Formular abschicken\">
          </form>
          </body></html>";
}


// Beginn des Hauptprogramms
writeHeaderAndHeadline();
startForm("post", "formular2a.php");
writeInputField("Vorname", "vorname");
writeInputField("Name",    "nachname");
closeFormAndFooter();
?>

```

![](images/Pasted%20image%2020250419195603.png)



Die Neuerungen sind im folgenden PHP-Sourcecode, in dem die Formulardaten verarbeitet werden.
```php
<?php
/**
 * Beispiel Formular - Daten mit foreach() ausgeben
 * @author Lisa Meijer & Jörg Thomaschewski 
 * basiert auf einer Version von Michael Gerbracht
 * @date 02.05.2019
 */

function writeHeaderAndHeadline()
{
    echo "<!DOCTYPE html>
          <html lang=\"de\">
          <head><title>Formular</title>
          </head>
          <body>
          <h1>Daten mit foreach() ausgeben</h1>";
}

function writeHtmlEnd()
{
    echo "</body></html>";
}


// Beginn des Hauptprogramms
writeHeaderAndHeadline();
$error = false;

// Alle POST-Daten mit foreach() auslesen und überprüfen
foreach ($_POST as $field => $content) {
    if (empty($content)) {
        echo "Das Feld $field enthält keinen Text!<br />";
        $error = true;
    }
}

if (!$error) {
    echo "Hallo " . $_POST["vorname"] . " " . $_POST["nachname"] . "!";
}

writeHtmlEnd();
?>
```



Screenshot der Ausgabe, wenn beide Felder ausgefüllt wurden  
[![File:formular2a-ok.png](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/7/73/Formular2a-ok.png "File:formular2a-ok.png")](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/7/73/Formular2a-ok.png)  
  
Screenshot der Ausgabe, wenn ein Feld nicht ausgefüllt wurde.  
[![File:formular2a-error.png](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/9/91/Formular2a-error.png "File:formular2a-error.png")](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/9/91/Formular2a-error.png)  
  
Screenshot der Ausgabe, wenn beide Felder nicht ausgefüllt wurden.  
[![File:formular2a-2error.png](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/3/32/Formular2a-2error.png "File:formular2a-2error.png")](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/3/32/Formular2a-2error.png)

  
In **Zeile 27** wird hier die Variable _$error_ mit dem Boolean _false_ initialisiert, die in einem Fehlerfall auf Wahr (true) gesetzt wird.

In **Zeile 30** beginnt die _foreach_-Schleife. Diese geht alle Elemente des Arrays `$_POST` durch und speichert jeweils den aktuellen Key des Arrays in der Variable `$field` und den Inhalt in der Variable `$content`.

In **Zeile 31** erfolgt die eigentliche Prüfung. Hierbei prüft die Funktion _empty()_, ob der Inhalt leer ist. Ist dies der Fall, wird ein Text (**Zeile 32**) ausgegeben und die Variable _$error_ auf _true_ gesetzt. Die Überprüfung wird jedoch noch weiter fortgesetzt (die gesamte foreach-Schleife wird durchlaufen), somit sieht der Anwender alle Fehler und nicht nur einen.

In **Zeile 37** wird nun geprüft, ob es einen Fehler gab oder nicht. Nur wenn das Formular fehlerfrei ausgefüllt wurde, wird der Text ausgegeben.

**Achtung Sicherheitshinweis**: das Formular ist sehr unsicher, da die Daten vor der Weiterverarbeitung nicht überprüft werden und es dient hier nur didaktischen Zwecken. Die Programmierung **DARF SO NICHT PRODUKTIV EINGESETZT WERDEN**. Alle mit POST oder GET übertragende Daten MÜSSEN mit [Regulären Ausdrücken](https://isp.eduloop.de/loop/Regul%C3%A4re_Ausdr%C3%BCcke_mit_PHP "Reguläre Ausdrücke mit PHP") zuvor geprüft werden.


In einem Fehlerfall könnte anstelle der einfachen Fehlermeldung auch das vorausgefüllte Formular und zusammen mit der Fehlermeldung wieder angezeigt werden, damit der Anwender die korrekten Daten nicht nochmals eingeben muss.

