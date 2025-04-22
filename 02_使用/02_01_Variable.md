Die Initialisierung der Variablen kann in PHP durch direkte Wertzuweisung erfolgen. Bei der ersten Verwendung einer Variable initialisiert und deklariert PHP diese Variable automatisch mit einer NULL-Referenz, das bedeutet, dass die Variable keinen Inhalt besitzt. Eine Initialisierung der Variablen ist sehr empfehlenswert.

Hier einige Beispiele für die explizite Initialisierung

```
$name  = "";   //Deklaration und Initialisierung als String
$age   = 0;    //Deklaration und Initialisierung als Integer
$price = 0.0;  //Deklaration und Initialisierung als Float
```
Es gibt die Variablentypen Boolean, String, Integer und Float, welche auf den nächsten Seiten beschrieben werden.

Es gibt zusätzlich den Datentyp Objekt, der in der objektbasierten Programmierung verwendet wird.


Weitere Informationen zur Variablenbehandlung finden Sie in der PHP-Dokumentation [http://php.net/manual/de/language.variables.php](http://php.net/manual/de/language.variables.php)



# 1 Boolean

Casting-Operator _(bool) $variable_  
Überprüfung mit _is_bool()_

Eine Variable vom Typ Boolean kann zwei Werte annehmen (_true | false_). Bei einer Berechnung mit einer Boolean-Variablen wird _true_ als 1 interpretiert und _false_ als 0.  
  
```
$var = (bool) "false";
if (is_bool($var)) {
    echo "Ja, es ist ein Boolean-Typ.";
} else {
    echo "Nein, es ist kein Boolean-Typ.";
}

echo "var_dump: ";

var_dump($var);

```

Ausgabe:  
_Ja, es ist ein Boolean-Typ._  
_var_dump: bool(true)_

  
Durch den in **Zeile 1** angegebenen Casting-Operator (_bool_) wird der **String** _false_ in eine Boolean-Variable konvertiert. Hier ist zu beachten, dass es sich dabei um einen String handelte. Denn Strings werden grundsätzlich mit _true_ übersetzt, auch wenn der String die Zeichenfolge _false_ enthielt!

In **Zeile 2** wird durch die Funktion is_bool() festgestellt, dass es sich dabei um eine Boolean-Variable handelt. **Zeile 8** gibt dann den Datentyp, sowie dessen Wert zurück.

# 2 String

Casting-Operator _(string)_  
Überprüfung mit _is_string()_

Strings werden in PHP mit "..." oder '...' zugewiesen. Sollte der Eintrag innerhalb doppelter Anführungszeichen eine Variable enthalten, wird diese ausgewertet, das ist bei einfachen Anführungszeichen nicht der Fall. Die maximale Länge eines Strings ist dabei in PHP nicht begrenzt.  
  

**Strings mit einem „Anhang“ erweitern**  
Um zuvor deklarierte Variablen in einem Text mit einem „Anhang“ zu ergänzen, gibt es verschiedene Möglichkeiten. In unserem Beispiel wollen wir den Text „lern“ als „lernen“ ausgeben lassen.
```
$var = (string) "lern";
$a = "Wir $varen PHP! <br>";
$b = "Wir " . $var . "en PHP! <br>";
$c = "Wir {$var}en PHP! <br>";
echo $a, $b, $c;
```

Ausgabe:  
_Wir PHP!_  
_Wir lernen PHP!_  
_Wir lernen PHP!_

  
**Stringblöcke**  
Es können auch Stringblöcke verwendet werden. Innerhalb dieser dürfen Variablen vorkommen.  

```
$a = "PHP";
$b = <<<STRINGENDE
Wir lernen
$a!
STRINGENDE;
echo $b;
```

Ausgabe:  
_Wir lernen PHP!_  
  

**Auf Zeichen in einem String zugreifen**  
Man kann auf einzelne Zeichen innerhalb eines Strings mittels geschweifter Klammern zugreifen.  

```
$var = "Wir lernen PHP!";
echo $var{0};
echo $var{5};
echo $var{7};
```

Ausgabe:  
_Wen_


# 3 Integer

Casting-Operator _(int)_  
Überprüfung mit _is_int()_

Im Allgemeinen umfassen Integer den Wertebereich von -2147483648 bis 2147483648, allerdings können auch hexadezimale Zahlen oder Oktalwerte ausgegeben werden. Zahlen, die mit einer 0x beginnen, werden so **automatisch** in eine **hexadezimale** **Zahl** umgerechnet.  
Zahlen, die mit einer 0 beginnen, werden so **automatisch** in einen **Oktalwert** umgerechnet.  

```
$normal = (int) 42;
$hexa   = (int) 0x11;
$octal1 = (int) 042;
echo "Normaler Integer: $normal <br>";
echo "Hex: $hexa <br>";
echo "Oktal#1: $octal1 <br>";
```

Ausgabe:  
_Normaler Integer: 42_  
_Hex: 17_  
_Oktal#1: 34_

Wenn wir im obrigen Beispiel _$octal1 = 0815;_ schreiben würden, dann würde dies eine Fehlermeldung _Parse error: Invalid numeric literal..._ erzeugen, da die Ziffer 8 im oktalen Zahlensystem nicht existiert.

  

Übung

Um eine Eingabe daraufhin zu überprüfen, ob es sich um den Typen **Integer** handelt, geht man wie im folgenden Code-Beispiel vor. Schreiben Sie zu jeder Zeile, ob die Lösung _true_ oder _false_ ist:

```
var_dump(is_int(7));
var_dump(is_int(7.8));
var_dump(is_int('7'));
var_dump(is_int('7.8')); 
var_dump(is_int(1995e0));
var_dump(is_int('0x18'));
var_dump(is_int(0x18));
var_dump(is_int(echo));
var_dump(is_int(-224));
```
Lösung
```
var_dump(is_int(7)); // Ausgabe: bool(true)
var_dump(is_int(7.8)); // Ausgabe: bool(false)
var_dump(is_int('7')); // Ausgabe: bool(false)
var_dump(is_int('7.8'));  // Ausgabe: bool(false)
var_dump(is_int(1995e0)); // Ausgabe: bool(true)
var_dump(is_int('0x18'));  // Ausgabe: bool(false)
var_dump(is_int(0x18)); // Ausgabe: bool(true)
var_dump(is_int(echo));  // Ausgabe: bool(false)
var_dump(is_int(-224)); // Ausgabe: bool(true)
```

# 4 Float

Casting-Operator _(float)_  
Überprüfung mit _is_float()_

Auch wenn dieser Variablentyp mit Float bezeichnet wird, so handelt es sich genau genommen um den Typ Double des verwendeten C-Compilers, der auch diesen Wertebereich unterstützt. Dabei unterscheidet PHP nicht zwischen einfacher und doppelter Genauigkeit, sondern arbeitet mit einer Genauigkeit von 14 Stellen.

Eine gute Möglichkeit, die Genauigkeit zu erhöhen, ist die Verwendung der [BCMath-Funktionen](http://php.net/manual/de/ref.bc.php) wie z.B. [bcdiv()](http://php.net/manual/de/function.bcdiv.php) oder [bcsqrt()](http://php.net/manual/de/function.bcsqrt.php). Um diese jedoch nutzen zu können, muss man PHP mit --enable-bcmath konfigurieren.


Um eine Eingabe daraufhin zu überprüfen, ob es sich um den Typen Float handelt, geht man wie im folgenden Code-Beispiel vor. Schreiben Sie zu jeder Zeile, ob die Lösung true oder false ist:

```
var_dump(is_float(47)); // Ausgabe: bool(false)
var_dump(is_float(6.11)); // Ausgabe: bool(true)
var_dump(is_float(95.1)); // Ausgabe: bool(true)
var_dump(is_float(66e6)); // Ausgabe: bool(true)
var_dump(is_float('xyz')); // Ausgabe: bool(false)
var_dump(is_float(false)); // Ausgabe: bool(false)
```


# 5 Arrays in PHP

Casting-Operator _(array)_  
Überprüfung mit _is_array()_  
  

Es gibt bei PHP zwei Typen von Arrays: **indizierte und assoziative Arrays**. Beispiele und Erläuterungen hierzu kommen in den nächsten Unterkapiteln.

Gerade assoziative Arrays sind in PHP besonders wichtig, da diese Array-Art genutzt wird, um Daten von einem Client (z.B. aus einem Formular) an einen Server zu übertragen. Dabei sind assoziative nicht so fehleranfällig wie indizierte Arrays. Allerdings kann in PHP ein Array auf den ersten Blick nicht eindeutig von einer Variablen unterschieden werden.

Die Initialisierung von Arrays sollte in PHP mit der leeren Klammer _[]_ erfolgen (oder in einer älteren Notation mit der Funktion _array()_), da so sichergestellt wird, dass dem ersten Element der Index 0 zugewiesen ist.




# 6 Indizierte Arrays

Bei **indizierten Arrays** wird jedem Element automatisch ein **Index** zugewiesen. Das erste Element enthält den Index "0".
**Füllen von indizierten Arrays**  

```
$name = ["Maria", "Ute", "Jürgen"];
// automatische Indexzuweisung – alternative Schreibweise
$name[] = "Maria";
$name[] = "Ute";
$name[] = "Jürgen";
// manuelle Indexzuweisung
$name[0] = "Maria";
$name[1] = "Ute";
$name[2] = "Jürgen";
```

Zum Vergleich hier die veraltete Schreibweise mittels der array-Funktion.
```
// veraltete Schreibweise: array()-Funktion
$name = array("Maria", "Ute", "Jürgen");
```


**Ausgeben von indizierten Arrays**  
```
echo "2. Name im Array: $name[1] <br>";
echo "1. Name im Array: $name[0] <br>";
echo "3. Name im Array: $name[2]";
```

Ausgabe:  
_2. Name im Array: Ute_  
_1. Name im Array: Maria_  
_3. Name im Array: Jürgen_


# 7 Assoziative Arrays

Bei **assoziativen Arrays** wird jedem Element ein **Schlüssel (=Key)** zugewiesen.

  
**Füllen von assoziativen Arrays**  
```php
$flower = ["Tulpe" => "Gelb", "Rose" => "Rot", "Kornblume" => "Blau"];
// alternative Schreibweise
$flower["Tulpe"] = "Gelb";
$flower["Rose"] = "Rot";
$flower["Kornblume"] = "Blau";
```

Zum Vergleich hier die veraltete Schreibweise mittels der array-Funktion.

```php
// veraltete Schreibweise: array()-Funktion
$flower = 
    array("Tulpe" => "Gelb", "Rose" => "Rot", "Kornblume" => "Blau");
```

  
**Auslesen von assoziativen Arrays**  
Der Zugriff erfolgt mittels Schlüssel, wobei die Anführungszeichen richtig zu setzen sind!
> `.` → The **concatenation operator** in PHP. It joins strings together.

```php
echo "flower 3:" . $flower["Kornblume"] . "<br>";
echo "flower 1:" . $flower["Tulpe"] . "<br>";
echo "flower 2:" . $flower["Rose"];
```
Ausgabe:  
_flower 3: Blau_  
_flower 1: Gelb_  
_flower 2: Rot_

  
**Variablen zum Füllen und Auslesen verwenden**  
Oftmals wird ein Array nicht "von Hand" gefüllt, sondern die Werte gelangen über Variablen in das Array. Variablen können sowohl aus _Key_ als auch als _Value_ verwendet werden.
```php
// Variablen $type1...3 und $color1...3 zuvor definieren
$flower = ["$type1"=>"$color1", "$type2"=>"$color2", "$type3"=>"$color3"];

echo "flower 3:" . $flower["$type3"] . "<br>";
```

Somit können Arrays auch gut mittels _for_-Schleifen gefüllt werden.

  

Übung

Warum funktioniert folgende Zeile nicht?

```php
echo "flower 2: $flower["Tulpe"]";
```

Wie könnte das Problem behoben werden?

Der echo-Befehl beginnt mit einem doppelten Anführungszeichen und geht daher nur bis zum nächsten doppelten Anführungszeichen.

```echo "flower 2: $flower["```

Der korrekte Sourcecode (wie oben angegeben) lautet:

```php
echo "flower 2:" . $flower["Tulpe"];
```


# 8 Arrays im Array

Bisher haben wir nur einfache Arrays kennen gelernt. Sie können aber innerhalb eines Arrays weitere Arrays einbinden. Damit dies übersichtlich bleibt, schreiben wir unser indiziertes Array zunächst einmal um und geben es aus.

```php
// Schreibweise für sehr einfache Arrays
$name = ["Maria", "Ute", "Jürgen"];

// Bessere Schreibweise, sobald die Arrays komplexer werden
$name = [
  "Maria",
  "Ute", 
  "Jürgen"
];
```

Nun sollen nicht nur die Namen, sondern zugehörige Daten abgespeichert werden.
```php
$data = [
  "Maria"  => ["7201234", "Medientechnik", "6. Semester"],
  "Ute"    => ["7208888", "Informatik", "2. Semester"], 
  "Jürgen" => ["7211111", "Medientechnik", "2. Semester"],
];

echo "Die Matr.-Nr. von Ute ist: " . $data["Ute"][0];
```

Ausgabe:  
_Die Matr.-Nr. von Ute ist: 7208888_

Im gezeigten Beispiel wurde aus dem ehemaligen indiziertem Array nun ein assoziatives Array, wobei (in **Zeilen 2-4**) die Namen _"Maria", "Ute", "Jürgen"_ nun als Keys verwendet werden. Jedem Key wurde nun ein indiziertes Array mit den zugehörigen Daten angefügt.  
Durch `_$data["Ute"][0]_` wird in **Zeile 8** zunächst der Datensatz zum Key _"Ute"_ gesucht. Dieser zugehörige Datensatz ist ein indiziertes Array. Aus dem indizierten Array wird dann die Stelle `_[0]_` ausgelesen, die der Matrikelnummer _7208888_ von Ute entspricht.


**Keys auslesen mit _array_keys()_**  
Vielleicht ist es Ihnen schon aufgefallen, dass ich oben bei der Ausgabe etwas "geschummelt" habe. Das Wort _Ute_ habe ich direkt in den String geschrieben. Da _Ute_ nun der Key zum zugehörigen Datensatz ist, kann man diesen Key nicht so einfach auslesen, sondern es muss die PHP-Funktion _array_keys()_ verwendet werden (**Zeile 7**). _array_keys()_ liefert ein indiziertes Array mit allen Keys zurück, also `_["Maria", "Ute", "Jürgen"]_`.

```php
$data = [
  "Maria"  => ["7201234", "Medientechnik", "6. Semester"],
  "Ute"    => ["7208888", "Informatik", "2. Semester"], 
  "Jürgen" => ["7211111", "Medientechnik", "2. Semester"],
];

$name = array_keys($data);
echo "Die Matr.-Nr. von " . $name[1] . " ist: " . $data["Ute"][0];

// Auch die folgende "Kurzform" ist möglich
echo "Die Matr.-Nr. von ".array_keys($data)[1]." ist: ".$data["Ute"][0];
```



# 9 Vergleich von Arrays

Arrays können miteinander verglichen werden, wobei es den Vergleich nur nach den Inhalten gibt, sowie den Vergleich danach, ob nicht nur der Inhalt, sondern auch der Typ und der Schlüssel gleich sind.


```php
$one = [1, 2, 3];
$two = [1, 2, "3"];
$three = ["x" => 1, "y" => 2, "z" => 3];

if ($one == $two) {
    echo '1: $one & $two haben den gleichen Inhalt!';
}

if ($one === $two) {
    echo '2: $one & $two sind identisch!';
}

if ($one == $three) {
    echo '3: $one & $three haben den gleichen Inhalt!';
}
```


Ausgabe:  
_1: $one & $two haben den gleichen Inhalt!_

Die zweite _if-_Bedingung (Zeile 9) wird nicht durchlaufen, da die Typen in den Elementen unterschiedlich sind.  
Die dritte _if_-Bedingung (Zeile 13) wird nicht durchlaufen, da es sich um verschiedene Arraytypen handelt.

Um herauszufinden, worin sich zwei Arrays unterscheiden bzw. welche Elemente in beiden Arrays vorkommen, gibt es die Funktionen [array_intersect()](http://php.net/manual/de/function.array-intersect.php) und [array_diff()](http://php.net/manual/de/function.array-diff.php).

array_intersect() liefert ein Array zurück, das die Elemente beinhaltet, die in den geprüften Arrays vorhanden sind.  
_array_diff()_ liefert ein Array zurück, das nur Elemente des ersten Arrays beinhaltet, welche nicht ebenfalls in einem anderen der geprüften Arrays vorkommt.



# 10 Schwache Typisierung

**Achtung**: PHP ist eine ["schwach typisierte Sprache"](https://de.wikipedia.org/wiki/Typisierung_\(Informatik\)). Was dies bedeutet, soll folgendes Beispiel verdeutlichen:


```
$varString = "111";  // dies ist ein String
$varInt    =  222;   // dies ist eine Integer-Zahl

// wir addieren einen String mit einer Zahl
$sum = $varString + $varInt;
echo $sum;
```

Ausgabe: _333_

Stark typisierte Sprachen wie z.B. C oder Java würden einen Fehler ausgeben. Aber PHP wandelt den String in eine Zahl um und addiert. Nur deshalb mussten wir eben beim Vergleich der Arrays auch `===` verwenden, um Typ und Wert zu verglichen.

Beim Vergleich mit _`==`_ werden nur die Werte verglichen und es erfolgt eine automatische Konvertierung, die normalerweise nicht gewünscht ist.

In PHP wird die automatische Umwandlung der Typen als [_Type Juggling"_](https://www.php.net/manual/de/language.types.type-juggling.php) _bezeichnet._

Man kann ab PHP 7 nun den PHP-Interpreter anweisen Datentypen strikt zu verwenden. Die schwache Typisierung wird aber an dieser Stelle nicht aufgehoben, wie folgendes Beispiel zeigt:

```
<?php declare(strict_types=1);
$varString = (string) "111";  // dies ist ein String
$varInt    = (int)     222;   // dies ist eine Integer-Zahl
// wir addieren einen String mit einer Zahl
$sum = (string) $varString + (int) $varInt;
echo $sum;
?>
```

Ausgabe: _333_

