
# 1 Übersicht über Operatoren

In diesem Unterkapitel erhalten Sie eine tabellarische Übersicht über die Operatoren. Vergleichen Sie diese Operatoren mit den Ihnen bekannten Operatoren aus der von Ihnen meistgenutzten Programmiersprache.

---

**Allgemeine Operatoren**  

|   |   |
|---|---|
|**Operator**|**Beschreibung**|
|.|String-Verkettungsoperator|
|=|Zuweisungsoperator|

 Tab. 19: Allgemeine Operatoren

---

**Rechenoperatoren**  

|              |                                                                                                      |
| ------------ | ---------------------------------------------------------------------------------------------------- |
| **Operator** | **Beschreibung**                                                                                     |
| +            | Addition                                                                                             |
| -            | Subtraktion                                                                                          |
| **           | Potentieren                                                                                          |
| *            | Multiplikation                                                                                       |
| /            | Division                                                                                             |
| %            | Modulo; Ergibt den Rest einer Ganzzahligen Division  <br>(z.B. 13 % 4 ergibt 1, da 13/4 = 3, Rest 1) |


 Tab. 20: Rechenoperatoren
 
Der Operator "+" funktioniert auch für Arrays (als [Array-Operator](https://www.php.net/manual/de/language.operators.array.php)). Er "addiert" die Arrays indem er sie hintereinander hängt.

---

  
**Kombinierte Zuweisungsoperatoren**

|   |   |
|---|---|
|**Operator**|**Beschreibung**|
|+=|Addiert neuen Wert zum alten Wert.  <br>_$count += 2_ ist die Kurzform von _$count = $count + 2_  <br>und kommt oft in for-Schleifen zum Einsatz.|
|-=|Zieht neuen Wert vom alten Wert ab|
|/=|Teilt alten Wert durch den neuen Wert|
|*=|Multipliziert alten und neuen Wert|
|%=|Modulo vom alten und neuen Wert|
|.=|Schreibt neuen Wert anhängend an den alten Wert|

 Tab. 21: kombinierte Zuweisungsoperatoren

Code

Beispiel für **.=**
```
$var = 5;
$var .= 1;
echo $var;
```

Ausgabe: _51_

---

**Inkrement- und Dekrement-Operatoren**  
(funktionieren auch mit Buchstaben)

|   |   |
|---|---|
|**Operator**|**Beschreibung**|
|$digit++|Erhöht $digit um 1|
|$digit--|Verringert $digit um 1|
|++$digit|Erhöht $digit um 1, welche sofort auf die Variable geschrieben wird|
|--$digit|Verringert $digit um 1, welche sofort von der Variablen abgezogen wird|

 Tab. 22: Inkrement- und Dekrement-Operatoren


---

[**Vergleichsoperatoren**](http://php.net/manual/de/language.operators.comparison.php)

|   |   |
|---|---|
|**Operator**|**Beschreibung**|
|==|Prüft, ob Inhalt der Variablen gleich ist  <br>(ungeachtet des Typs)|
|!=|Prüft, ob Inhalt der Variablen ungleich ist  <br>(ungeachtet des Typs)|
|===|Prüft, ob Inhalt sowie Typ der Variablen gleich ist|
|!==|Prüft, ob Inhalt oder Typ der Variablen ungleich ist  <br>"Gibt TRUE zurück, wenn _$one_ nicht gleich _$two_ ist, oder  <br>wenn beide nicht vom gleichen Typ sind"|
|>|Größer als…|
|<|Kleiner als…|
|>=|Größer oder gleich…|
|<=|Kleiner oder gleich…|

 Tab. 23: Vergleichsoperatoren

Die Vergleichsoperatoren werden Sie in der PHP-Programmierung sehr oft benutzen.

Aufgrund der Art wie Fließkommazahlen (float) intern dargestellt werden, sollten zwei Fließkommazahlen nicht auf Gleichheit getestet werden.


---

  
[**Logische Operatoren**](http://php.net/manual/de/language.operators.logical.php)

|   |   |
|---|---|
|**Operator**|**Beschreibung**|
|&&|_und_-Verknüpfung z.B. _$a && $b_ (_&&_ hat Vorrang vor _and_)|
|and|_und_-Verknüpfung z.B. _$a and $b_|

 Tab. 24: Logische Operatoren für UND

Der Unterschied zwischen _and_ und _&&_ liegt in der Abarbeitungsreihenfolge, ähnlich der Punkt-vor-Strich-Rechnung. Dabei hat _&&_ stets Vorrang.

|   |   |
|---|---|
|**Operator**|**Beschreibung**|
|\||_oder_-Verknüpfung z.B. _$a \| $b_ (_\|_ hat Vorrang vor _or_)|
|or|_oder_-Verknüpfung z.B. _$a or $b_|

 Tab. 25: Logische Operatoren für ODER

Auch hierbei ist wieder zu beachten, dass || in der Rangfolge höhergestellt ist, als dies bei or der Fall ist.

|   |   |
|---|---|
|**Operator**|**Beschreibung**|
|xor|entweder-oder (aber nicht beide) z.B. _$a xor $b_|
|!|_nicht-Operator z.B. !$a_|

 Tab. 26: Logische Operatoren


```
$a && $b or $c;
$a and $b || $c;
```

In diesem Beispiel ist die Rangfolge entscheidend. In der ersten Zeile ergibt die Gleichung _**($a und $b) oder $c**_, während die zweite Zeile _**$a und ($b oder $c)**_ meint. _&&_ ist somit höherrangig als _and_, und _||_ höherrangig als _or_.

---


**Bitorientierte Operatoren**

|   |   |
|---|---|
|**Operator**|**Beschreibung**|
|~|Negation, ungesetzte Bits werden gesetzt und umgekehrt|
|&|Bits, die in einer Variablen _und_ der damit Verknüpften gesetzt sind, werden gesetzt|
|\||Bits, die in einer Variablen _oder_ der damit Verknüpften gesetzt sind, werden gesetzt|
|^|Bits, die in einer Variablen _oder_ der damit Verknüpften gesetzt sind, werden gesetzt, aber nicht in beiden (xor)|
|>>|Bits nach rechts verschieben  <br>(entspricht Division durch 2)|
|<<|Bits nach links verschieben  <br>(entspricht Multiplikation mit 2)|

 Tab. 27: Bitorientierte Operatoren

  
---

Auch ein _@_ gilt als Operator. Er dient dazu, Fehler zu unterdrücken und dabei das Programm nicht abzubrechen. Das _@_ muss vor der Funktion stehen, die ausgeführt werden soll: z.B. _@readfile ("DATEI")_.

# 2 Beispiele für Operatoren

In diesem Unterkapitel sehen Sie zwei Beispiele für den Einsatz von Operatoren.

```php
$number = 5;
$location = "Seminar";
$location .= "raum";

echo "$number Männer und ", --$number, " Frauen sitzen im $location.<br>";
echo "Die Frauen sind im ", $number--, ". Semester<br>";
echo "und $number Männer sind im ", $number*2, ". Semester.";
```

Ausgabe:  
5 Männer und 4 Frauen sitzen im Seminarraum.
Die Frauen sind im 4. Semester
und 3 Männer sind im 6. Semester._


```php
$a= 202;
$b= "S";
$b .= $a;

var_dump($a);
echo "<br>";
var_dump($b);
echo "<br>";

if ($a == $b)   {
    echo '$a und $b sind gleich!<br>';
} else {
    echo '$a und $b sind nicht gleich!<br>';
}

if ($a === $b) {
    echo '$a und $b sind identisch!<br>';
} else {
    echo '$a und $b sind nicht identisch!<br>';
}
```

Ausgabe:
int(202)
string(4) "S202"
$a und $b sind nicht gleich!
$a und $b sind nicht identisch!



# 3 Konvertierung zwischen Variablendeklarationen

Vorsicht mit der Variablendeklaration und _if_-Abfragen.
```php
$var = "text";
if ((string)0 == $var)   {
    /* Bedingung wird nicht durchlaufen */
}
```
Die Variable _$var_ wird durch direkte Zuweisung als Text deklariert. Die Bedingung wird nicht durchlaufen, da der String 0 nicht dem String _text_ entspricht.

  
```php
$var = "text";
if (0 == $var)   {
    /* Bedingung wird durchlaufen */
}
```

Hier wird die Bedingung durchlaufen, da eine implizite Umwandlung des Strings in eine Zahl vorgenommen wird, damit der Vergleich stattfinden kann. Der String erhält während der Umwandlung den Wert _NULL_ und somit ist die Bedingung erfüllt. Auch bei _`$var == 0`_ wird dem String die Variable zugewiesen. Wenn wir also in unserem String eine Zahl hätten, würde die Bedingung nicht durchlaufen!

Zur Lösung des Problems sollte man nicht den Vergleichsoperator `==` verwenden, sondern`===`, welcher auch den Typ der Variablen vergleicht.