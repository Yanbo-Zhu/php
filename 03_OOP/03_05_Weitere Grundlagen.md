

Hier lernen Sie wichtige Begriffe und nützliche Konzepte aus der objektorientierten Programmierung kennen.

Es werden Klassen vorgestellt, die PHP bereits mitliefert. Dabei muss man verschiedene Sammlungen von Klassen unterscheiden:

- Klassen die PHP immer dabei hat, z.B. die Klasse _DateTime_,
- Klassen aus der "Standard PHP Library (SPL)", die auch immer mitinstalliert sind,
- und Klassen der "PHP Data Objects (PDO)" als Schnittstelle zur Datenbank, die aber erst später behandelt werden.


Bisher haben wir die Objektorientierung damit begründet, dass wir Klassen als "Behälter für Methoden und Eigenschaften" betrachten (siene [Warum Objektorientierung](https://isp.eduloop.de/loop/Warum_Objektorientierung "Warum Objektorientierung")).  

Hier sollen Sie nun ein Gefühl dafür bekommen, dass "noch mehr geht". Wichtig ist nun die Verwendbarkeit und Austaschbarkeit von Objekten zur Laufzeit.

# 1 Datum ausgeben mit DateTime

Bereits im Unterkapitel [Datum ausgeben mit date()](https://isp.eduloop.de/loop/Datum_ausgeben_mit_date\(\) "Datum ausgeben mit date()") hatten wir gesehen, wie man mit der PHP-Funktion _date()_ ein Datum formatieren und ausgeben kann.

Hier wollen wir nun die objektorientierte Version der Datumsausgabe zeigen, denn PHP hat eine **vordefinierte Klasse _DateTime_**.

Anmerkung

Wenn wir mit vordefinierten Klassen arbeiten, dann müssen wir uns zunächst einen ersten Überblick über die vorhandenen Eigenschaften und Methoden machen, die man nutzen kann.  
Viele vordefinierte Klassen können auch ["statisch"](https://isp.eduloop.de/loop/Statische_Aufrufe_von_Klassen "Statische Aufrufe von Klassen") aufgerufen werden. Wir bevorzugen in diesen Beispielen aber die Bildung von Objekten.


Die _[Klasse DateTime](https://www.php.net/manual/de/class.datetime.php)_ bietet sehr viele Möglichkeiten und Methoden, von denen wir hier nur eine kleine Auswahl verwenden.

- Beim Instanzieren die **Klasse DateTime** werden Daten an den Konstruktor übergeben.
- Die Methode _**[format()](https://www.php.net/manual/de/datetime.format.php)**_ wird zur formatierten Ausgabe genutzt.
- Die Methode _**[modify()](https://www.php.net/manual/de/datetime.modify.php)]**_ wird zur Änderung des Datums genutzt, beispielsweise um Wochen hinzuzählen oder Stunden abziehen.
- Die Methode _**[getTimestamp()](https://www.php.net/manual/de/datetime.gettimestamp.php)**_ wird zur Bestimmung der Sekunden seit Beginn der Unix-Zeitrechnung am 01.01.1970 genutzt.


---

Beginnen wir mit dem einfachen Beispiel der Ermittlung und Ausgabe des aktuellen Datums.

```
<?php
$dt = new DateTime("now");

// Deutsches Standardformat
echo $dt->format("d.m.Y H:i:s");
?>
```
Ausgabe des heutigen Formats in der Form:  
_05.05.2020 12:02:27_

---

Man kann aber bereits beim Instanzieren andere Datumsangaben angeben.
```
<?php

// Festes Datum angeben. 
// Es sind verschiedene Formate im Konstruktor möglich.
// Die Ausgabe wird unabhängig mit ''format()'' festgelegt.
$dt = new DateTime("31.01.2021");
echo $dt->format("d.m.Y") . "<br>";

$dt = new DateTime("2021-01-31");
echo $dt->format("d.m.Y") . "<br>";
?>
```
Ausgabe:  
_31.01.2021_  
_31.01.2021_

--- 


Man kann aber bereits beim Instanzieren schon Berechnungen durchführen.
```
<?php
// Immer englischsprachig angeben
$dt = new DateTime("now + 1 day");
echo "Morgen: " . $dt->format("d.m.Y H:i:s") . "<br>";
$dt = new DateTime("yesterday 10:00");
echo "Gestern um 10:00 Uhr: " . $dt->format("d.m.Y H:i:s") . "<br>";
$dt = new DateTime("now - 3 weeks");
echo "Vor 3 Wochen: " . $dt->format("d.m.Y H:i:s") . "<br>";
$dt = new DateTime("next Sunday");
echo "Nächster Sonntag: " . $dt->format("d.m.Y H:i:s") . "<br>";
$dt = new DateTime("First Sunday May 2021");
echo "Erster So. im Mai 2021: " . $dt->format("d.m.Y H:i:s") . "<br>";
?>
```

Ausgabe:  
_Morgen: 06.05.2020 12:02:27_  
_Gestern um 10:00 Uhr: 04.05.2020 10:00:00_  
_Vor 3 Wochen: 14.04.2020 12:02:27_  
_Nächster Sonntag: 10.05.2020 00:00:00_  
_Erster So. im Mai 2021: 02.05.2021 00:00:00_

---


Wichtiger ist aber, dass mit _modify()_ Datumsangaben ändern kann.
```
<?php
// Nutzung von modify()
$dt = new DateTime("now");
$dt->modify("+2 weeks -1 hours");
echo "In 2 Wochen (minus 1 Stunde): " . $dt->format("d.m.Y H:i:s");
?>
```
Ausgabe:  
_In 2 Wochen (minus 1 Stunde): 19.05.2020 11:02:27_

  ---
  

**Deutschsprachige Monate und Tage ausgeben**  
Bereits im Unterkapitel [Datum ausgeben mit date()](https://isp.eduloop.de/loop/Datum_ausgeben_mit_date\(\) "Datum ausgeben mit date()") haben wir gesehen, dass viel mehr Formatierungen möglich sind, nicht nur "tt.mm.jjjj". Die Formatangaben gelten auch hier.

|Zeichen|Beschreibung|Beispiel|
|---|---|---|
|_Y_|Vierstellige Jahresangabe|_1946_ oder _2007_|
|_y_|Zweistellige Jahresangabe|_46_ oder _07_|
|_m_|Monat mit führender Null|_01_ bis _12_|
|_n_|Monat|_1_ bis _12_|
|_M_|Monat, 3 Buchstaben|_Jan_ oder _Dec_|
|_F_|Monat ausgeschrieben|_January_ oder _December_|
|_d_|Tag des Monats mit führender Null|_01_ bis _31_|
|_j_|Tag des Monats ohne Null|_1_ bis _31_|
|_D_|Wochentag in 3 Buchstaben|_Sun_ oder _Mon_|
|_l_|Wochentag ausgeschrieben|"Sunday" oder "Monday"|
|_h_|Stunde im 12er Format mit führender Null|_01_ bis _12_|
|_H_|Stunde im 24er Format mit führender Null|_00_ bis _24_|
|_g_|Stunde im 12er Format ohne Null|_1_ bis _12_|
|_G_|Stunde im 24er Format ohne Null|_0_ bis _24_|
|_i_|Minuten mit führender Null|_00_ bis _59_|
|_s_|Sekunden mit führender Null|_00_ bis _59_|
|_t_|Anzahl der Tage im Monat|_28_ bis _31_|
|_z_|Tag eines Jahres|_0_ bis _365_|


---

Solange wir reine Zahlenformate verwenden, fällt uns nicht auf, dass alle Monate und Wochentage englischsprachig sind.
```
<?php
$dt = new DateTime("now");
// Problem mit DateTime: alles englischsprachig
echo $dt->format("d. F Y"),"<br>";
// Format auf einem Briefkopf
echo $dt->format("l, d F Y ") ;
?>
```

Ausgabe:  
_5. May 2020_  
_Tuesday, 05 May 2020_


---


Dieses Problem kann man lösen, indem wir eine andere Datumsdarstellung nehmen, die auf das lokale Computerdatum mit der PHP-Funktion _**[strftime()](https://www.php.net/manual/de/function.strftime.php)**_ direkt zugreift und wir zuvor sagen, dass die deutschsprachigen Begriffe mit _**[setlocale()](https://www.php.net/manual/de/function.setlocale.php)**_ gesetzt werden.

- Wir nutzen _setlocale(LC_TIME, "de_DE", "de_DE.utf-8", "deu", "german");_  
    Der erste Parameter _LC_TIME_ gibt an, dass die lokalen Zeitbegriffe genutzt werden sollen. Danach wird angegeben, wo die Begriffe auf dem lokalen Computer vorhanden sind und dies ist abhängig vom Betriebssystem.
    - Für Linux und MAC sind dies normalerweise _"de_DE"_ bzw. _"de_DE.utf-8"_.
    - Für Windows sind dies normalerweise _"deu"_ bzw. _"german"_.

- Wir nutzen _strftime()_ zur Ausgabe des Datumsformats. Aber Achtung _strftime()_ hat andere Abkürzungen als die Klasse DateTime. Und außerdem gleten nicht alle Abkürzungen auf allen Betriebssystemen.

```php
<?php
// Setlocale verwendet Funktionen des Betriebssystems
setlocale(LC_TIME, "de_DE", "de_DE.utf-8", "deu", "german");

// Heutiges Datum ausgeben mit strftime()
echo "Heute ist " . strftime("%A, der %d %B %Y um %H:%M");
?>
```


Ausgabe:  
_Heute ist Dienstag, den 05 Mai 2020 um 12:02_  

---

**Die Klasse DateTime verwenden und mit strftime() auf deutsch ausgeben**  
Zusammenfassend kann man sagen, dass die Klasse **DateTime** sehr gute Möglichkeiten zur Manipulation von Datumsangaben ermöglicht und es mit _**strftime()**_ möglich ist, diese auf deutsch formatier darzustellen. In beiden Fällen wird intern immer eine Integer-Zahl in Sekunden ab dem 01.01.1970 verwendet.

Somit können wir **DateTime** nutzen und müssen am Ende die Ausgabe mit _**strftime()**_ vornehmen.

Mit der Methode _getTimestamp()_ erhalten wir die Sekunden des im Objekt gespeicherten Datums und geben diese als Parameter an _**strftime()**_ zur formatierten Ausgabe weiter.
```php
<?php
setlocale(LC_TIME, "de_DE", "de_DE.utf-8", "deu", "german");

$dt = new DateTime("now - 3 weeks");

echo "Vor 3 Wochen war " 
    . strftime("%A, der %d %B %Y um %H:%M", $dt->getTimestamp());
?>
```
Ausgabe:  
_Vor 3 Wochen war Dienstag, der 14 April 2020 um 12:02_  


---

  
**DateTime in [Vererbung - weiteres Beispiel](https://isp.eduloop.de/loop/Vererbung_-_weiteres_Beispiel "Vererbung - weiteres Beispiel")**  
Bereits im Unterkapitel [Vererbung - weiteres Beispiel](https://isp.eduloop.de/loop/Vererbung_-_weiteres_Beispiel "Vererbung - weiteres Beispiel") wurde ein Objekt von DateTime mit in den Sourcecode "geschmuggelt".

```
$professor = new Professor(
    'Alberta',
    'Zweistein',
    new DateTime('1970-02-01'),
    42,
    'Prof. Dr.'
);
```

Auch wurde der Hinweis gegeben, dass man ein Objekt nicht per _echo_ ausgeben kann. Aber nun können Sie die Ausgabe des Geburtstags schaffen, denn Sie wissen, dass _DateTime_ eine vordefinierte Klasse ist und dass die Methode _format()_ zur Formatierung genutzt werden kann.


---


Übung

Nutzen Sie den Sourcecode [Vererbung2.zip](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/f/fa/Vererbung2.zip "Vererbung2.zip") aus dem Unterkapitel [Vererbung - weiteres Beispiel](https://isp.eduloop.de/loop/Vererbung_-_weiteres_Beispiel "Vererbung - weiteres Beispiel") und geben Sie den Geburtstag des Professors auf dem Browser aus.


```
`$dt = $professor->getBirthday(); // Dies ist das Objekt von DateTime
// Formatierung mit der Methode format() 
// der vordefinierten PHP-Klasse DateTime
echo $dt->format("d.m.Y");
```
  

Alternative Schreibweise
`echo $professor->getBirthday()->format("d.m.Y");`

Was kann man hieraus alles erkennen?
- Man kann erkennen, dass _$professor_ ein Objekt ist.
- `$professor->getBirthday()` ruft eine Methode (einen Getter) im Objekt _$professor_ auf.
- Die Rückgabe dieser Methode ist wieder ein Objekt. Und in dem zurückgegebenen Objekt wird die Methode _format()_ aufgerufen.
- Vermutlich handelt es sich um ein Objekt der Klasse _DateTime_ mit der entsprechenden Methode _format()_.
- Die Rückfabe der Methode _format()_ ist mit _echo_ darstellbar, also ist es ein String (oder ein Integer).

Sie haben hier also drei Dinge gelernt.
- Sie können externe Klassen instanzieren und die Methoden verwenden.
- Datum und Uhrzeit können Sie nun bearbeiten und ausgeben.
- Sie können die deutschen Datumsbegriffe verwenden, indem Sie zwar die Klasse DateTime verwenden, aber die Ausgabe an die Methode _strftime()_ umleiten.


# 2 Dateien lesen und schreiben (SPL)

Im Unterkapitel [Dateien lesen und schreiben](https://isp.eduloop.de/loop/Dateien_lesen_und_schreiben "Dateien lesen und schreiben") wurde anhand eines kleinen Beispiels gezeigt, wie Daten mit PHP-Funktionen in eine Textdatei geschrieben werden können.

Hier möchten wir die fertige _**Klasse [SplFileObject](https://www.php.net/manual/de/class.splfileobject.php)**_ der "Standard PHP Library (SPL)" nutzen. Dies hat den Vorteil, dass alle Methoden der Klasse genutzt werden können.

Hier verwenden wir nur eine kleine Auswahl der vorhandenen Methoden.

- Beim Instanzieren die **Klasse SplFileObject** wird der Pfad und Dateiname an den Konstruktor übergeben. Ebenso wird der Modul w (= write file ) bzw. r (= read file) mitgegeben.
- Die Methode _**[fwrite()](https://www.php.net/manual/de/splfileobject.fwrite.php)**_ wird zum Schreiben des Inhalts in die Datei genutzt.
- Die Methode _**[ftruncate()](https://www.php.net/manual/de/splfileobject.ftruncate.php)**_ wird dazu genutzt, um Zeichen aus dem String zu entfernen.
- Die Methode _**[getRealPath()](https://www.php.net/manual/de/splfileinfo.getrealpath.php)**_ liest den Speicherot und den Dateinamen aus.
- Die Methode _**[eof()](https://www.php.net/manual/de/splfileobject.eof.php)**_ wird verwendet um das Dateiende (End-of-File = eof) zu finden.
- Die Methode _**[fgets()](https://www.php.net/manual/de/splfileobject.fgets.php)**_ liest Daten aus der Datei zeilenweise aus.

Hier ein einfachdes Beispiel zum Schreiben und Lesen einer Textdatei.
```php
<?php
$textIn = "Dies ist ein Beispiel-Text.\nZweite Zeile";


// $file-Objekt zum Schreiben erzeugen
$fileWrite = new SplFileObject("a.txt", "w");

// Text in Datei schreiben (normalerweise Text aus einem Formular)
$fileWrite->fwrite($textIn);

// Objekt löschen, wenn alles geschrieben wurde
$fileWrite = null;


// $file-Objekt zum Lesen erzeugen
$fileRead = new SplFileObject("a.txt", "r");

// Beispiel: Die ersten 9 Zeichen in der ersten Zeile löschen
$fileRead->ftruncate(9);

// Dateipfad und Dateiname ausgeben
echo $fileRead->getRealPath() . "<br>";

// Alle Zeilen bis End-of-File =eof() ausgeben
while (!$fileRead->eof()) {
    echo $fileRead->fgets() . "<br>";
}
?>
```


```
Ausgabe:  
_C:\...mein..Pfad...\a.txt_  
_ein Beispiel-Text_  
_Zweite Zeile mit mehr Text_
```
Damit haben Sie eine gute Alternative zu den "normalen" PHP-Funktionen.

Bitte beachten Sie, dass zum besseren Verständnis hier das Error-Handling weggelassen wurde. Da es aber aus verschiedensten Gründen sein kann, dass eine Datei nicht geschrieben oder gelesen werden kann, ist ein Error-Handling an dieser Stelle besonders wichtig.

# 3 Autoloading (SPL)

Im Unterkapitel [Beispiel mit Vererbung, Aggregation und Komposition](https://isp.eduloop.de/loop/Beispiel_mit_Vererbung,_Aggregation_und_Komposition "Beispiel mit Vererbung, Aggregation und Komposition") haben wir die Klassen in verschiedene Dateien geschrieben (je Klasse eine Datei) und mussten im Hauptprogramm jeweils die Datein mit _require_once_ laden:

Code

```
<?php
require_once __DIR__.DIRECTORY_SEPARATOR.'Course.php';
require_once __DIR__.DIRECTORY_SEPARATOR.'Office.php';
require_once __DIR__.DIRECTORY_SEPARATOR.'Person.php';
require_once __DIR__.DIRECTORY_SEPARATOR.'Professor.php';
require_once __DIR__.DIRECTORY_SEPARATOR.'Student.php';
...
```

Stellen Sie sich nun vor, dass Sie viele umfangreiche Klassenbibliotheken einbinden müssen, also hunderte von Dateien. Das **Einbinden von Hand wäre sehr mühsam und fehlerträchtig**.

  
Mit **Autoloading** bezeichnet man das automatische Einbinden dieser Dateien. Hierzu gibt es eine PHP Funktion **[spl_autoload_register](https://www.php.net/manual/de/function.spl-autoload-register.php)**. Damit werden alle _require_once_-Aufrufe überflüssig.

Beim Autoload werden die Fehlermeldungen von PHP ausgenutzt, die dadurch entstehen, dass die notwendigen Dateien nicht gefunden werden. Wenn der Klassenname gleich dem Dateinamen ist, könnten über die Fehlermeldung die Dateien identifiziert und eingebunden werden. Eine gute Erklärung finden Sie im Video [https://www.youtube.com/watch?v=VC5HM0J0_Vo](https://www.youtube.com/watch?v=VC5HM0J0_Vo).


Also statt einer langen Erklärung auf dieser Seite schauen Sie einfach das Video an [https://www.youtube.com/watch?v=VC5HM0J0_Vo](https://www.youtube.com/watch?v=VC5HM0J0_Vo) (2:47 Min).

Die Lösung für das Autoloading-Problem ist im folgenden Sourcecode:

```
<?php
function autoload($className)
{
    if (file_exists(__DIR__.DIRECTORY_SEPARATOR."{$className}.php")) {
        require_once __DIR__.DIRECTORY_SEPARATOR."{$className}.php";
    }
}
spl_autoload_register("autoload");
...
```

**Hinweis für Profis**  
Die gezeigte Lösung enthält noch keine Sonderfälle, ist dafür aber didaktisch nachvollziehbar. Wer ein wirklich komplettes Autoloading möchte (inklusive der Berücksichtigung von Namespaces), der sollte die [PSR-4: Autoloader](https://www.php-fig.org/psr/psr-4/) berücksichtigen oder gleich die [PSR-4 Example Implementations](https://www.php-fig.org/psr/psr-4/examples/) verwenden.

**PSR** = **P**HP **S**tandard **R**ecommendations


# 4 ArrayAccess-Interface

Das **ArrayAccess-Interface** gibt uns die Möglickeit auf ein Objekt zuzugreifen, als wäre es ein assoziatives Array. Dies kommt in einige PHP-Frameworks vor und daher sollten Sie die Schreibweise verstehen.


PHP-Frameworks werden in der professionellen Programmierung oft genutzt, da diese vorgefertigte Lösungen zu vielen Standardproblemen bieten. Diese Frameworks wie z.B. "Symfony", "Laravel" oder "CodeIgniter" haben umfangreiche Klassenbibliotheken. Welches Framework "das Beste ist", darüber können Profi-Programmierer*innen stundenlang diskutieren und es gibt verschiedene Top-PHP-Framework-Listen (einfach mal in die Suchmaschine eingeben ;-)

  
Hier soll Ihnen also eine "seltsame Schreibweise" gezeigt werden, die bei der Nutzung eines Frameworks auftreten kann.
- Schauen wir uns mal im Hauptprogramm an, wie diese Schreibweise aussieht.
- Gegeben sei z.B. eine Klasse **Content** (als beliebiges Beispiel), die wir instanzieren und so z.B. das Objekt _**$content**_ erhalten (siehe **Zeile 2**).
- Und wir verwenden das Objekt _**$content**_ als wäre es ein Array (siehe **Zeile 4**), was natürlich normalerweise zu einer netten Fehlermeldung führt.

Code

```
<?php
$content = new Content();
$content["title"] = "Mein Hunde-Blog";
```

  
Ermöglicht wird diese Schreibweise (dies sich übrigens später als sehr praktisch herausstellt) durch das **[ArrayAccess-Interface](https://www.php.net/manual/en/class.arrayaccess.php)**


Kurze Wiederholung zum Begriff "Interface"  

Ein Interface ist eine vollständig abstrakte Klasse, die nur die Methodennamen vorgibt, die in der abgeleiteten Klasse zu implementieren sind (siehe [Abstrakte Klassen und Interfaces (=Schnittstellen)](https://isp.eduloop.de/loop/Abstrakte_Klassen_und_Interfaces_\(%3DSchnittstellen\) "Abstrakte Klassen und Interfaces (=Schnittstellen)")). Ein Interface kann nicht instanziert werden, sondern es wird "vererbt". Man nutzt aber "implements" statt "extends".

  
In der Dokumetation zum **[ArrayAccess-Interface](https://www.php.net/manual/en/class.arrayaccess.php)** sind vier Methoden beschrieben, die in unserem Beispiel in der Klasse **Content** implementiert werden müssen.

[![ArrayAccess-Interface.png](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/6/6c/ArrayAccess-Interface.png)](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/6/6c/ArrayAccess-Interface.png)

 Abb. 71: Dokumentation zum ArrayAccess-Interface

[https://www.php.net/manual/de/class.arrayaccess.php](https://www.php.net/manual/de/class.arrayaccess.php)

Somit müssen also die Methoden _offsetExists()_, _offsetGet()_, _offsetSet()_ und _offsetUnset()_ implementiert werden, damit ein Objekt wie ein assoziatives Array verwendet werden kann. Und genau dies wurde immer dann in Frameworks (oder anderen Klassen) gemacht.


这个 `Student` 类实现了 `ArrayAccess` 接口，因此可以像数组一样通过 `[]` 来设置、读取、检查和删除值。
这种写法在大型框架（如 Laravel）中非常常见，比如访问配置项、模型属性时会用类似数组的方式，非常方便又灵活。



## 4.1 Beispiel 
  
Hier ein Beispiel, wie die Implementation der Methoden in einer eigenen Klasse Content erfolgen könnte.

- _**offsetExists()**_ wird aufgerufen, wenn man mit _isset($content["tiltle"])_ ermitteln möchte, ob ein Array-Eintrag existiert.
- _**offsetGet()**_ wird aufgerufen, wenn man den Wert für _$content["tiltle"]_ mit einem Getter bekommen möchte.
- _**offsetSet()**_ wird aufgerufen, wenn man den Wert für _$content["tiltle"] = "Mein Koch-Blog"_ mit einem Setter setzen möchte.
- _**offsetUnset()**_ wird aufgerufen, wenn man mit _unset_ einen Eintrag löschen möchte.

```
class Content implements ArrayAccess
{

    public $title = "Mein Koch-Blog";

    public function offsetExists(string $key): void
    {
        if ($key === "title") {
            echo 'offsetExists() wurde aufgerufen und der '
                . 'Eintrag existiert <br>';
        }
    }

    public function offsetGet(string $key): string
    {
        if ($key === "title") {
            echo 'offsetGet() wurde aufgerufen und der '
                . 'Eintrag mit return zurückgegeben <br>';
            return $this->title;
        }
    }

    public function offsetSet(string $key, string $value): void
    {
        if ($key === "title") {
            echo 'offsetGet() wurde aufgerufen und der '
                . 'Eintrag in die Eigenschaft $title geschrieben <br>';
            $this->title = $value;
        }
    }

    public function offsetUnset(string $key): void
    {
        if ($key === "title") {
            echo 'offsetUnset() wurde aufgerufen und der '
                . 'Eintrag gelöscht <br>';
            $this->title = NULL;
        }

    }
}
```

Ausgabe:  
_offsetExists() wurde aufgerufen und der Eintrag existiert_  
_offsetGet() wurde aufgerufen und der Eintrag mit return zurückgegeben_  
_Eintrag: Mein Koch-Blog_  
_offsetGet() wurde aufgerufen und der Eintrag in die Eigenschaft $title geschrieben_  
_offsetGet() wurde aufgerufen und der Eintrag mit return zurückgegeben_  
_Eintrag: Mein Hunde-Blog_  
_offsetUnset() wurde aufgerufen und der Eintrag gelöscht_  
_offsetGet() wurde aufgerufen und der Eintrag mit return zurückgegeben_  

_Eintrag:_

Bitte versuchen Sie die Ausgabe nachzuvollziehen. Es ist gar nicht so schwer.

Sie haben hier also zwei Dinge gelernt.
- Sie können ein (vorgegebenes) Interface implementieren.
- Sie wissen, dass man mit **ArrayAccess-Interface** auf ein Objekt zugreifen kann, als wäre es ein assoziatives Array.

  
Hier zum Download ein wirklich nutzbares ArrayAccess-Interface (ohne die didaktischen echo-Befehle) [ContentModel.zip](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/1/15/ContentModel.zip "ContentModel.zip").



# 5 Anonyme Funktionen und Closure

Wir gehen hier einen Schritt zurück und schauen uns Funktionen (also keine Methoden, sondern normale Funktionen) an. Hierbei kommen wir aber gleich zu einer Besonderheit, den **anonymen Funktionen**.

==Anonyme Funktionen sind interessant, da man nun eine Funktion in einer Variablen speichern kann. Und die Variable kann beispielsweise wiederum in einem Array gespeichert werden. Damit hätten wir Funktionen, die über den Umweg einer Variablen in einem Array speicherbar sind. So etwas konnten wir bisher nicht machen.==

  
**Beispiel einer anonymen Funktion**  
Die Funktion _function add($x, $y)_ in **Zeile 4** ist eine normale Funktion, die in **Zeile 11** normal aufgerufen wird.

Die Funktion _function`($x, $y)`_ in **Zeile 16** ist eine **anonyme Funktion**, da der Name der Funktion fehlt. Aber dafür wird die Funktion einer Variablen zugewiesen: _$multiply = function($x, $y)_. Auch der Aufruf der Funktion in **Zeile 23** ist anders als gewohnt.

Code

```
<?php
// normale Funktion
function add($x, $y)
{
    $z = $x + $y;
    echo "Die Addition hat als Ergebnis: $z <br>";
}
// Aufruf der normalen Funktion
add(3, 4);
// anonyme Funktion definieren in dem man eine Variable zuweist
$multiply = function($x, $y)
{
    $z = $x * $y;
    echo "Die Multiplikation hat als Ergebnis: $z <br>";
};  // Symikolon ist hier notwendig
// Aufruf der anonymen Funktion
$multiply(3, 4);
// Aber was ist eigentlich $multiply für eine "seltsame Variable"
print_r($multiply);
```

Ausgabe:  
_Die Addition hat als Ergebnis: 7_  
_Die Multiplikation hat als Ergebnis: 12_  
_Closure Object ( [parameter] => Array ( [$x] => [$y] => ) )_

In der Ausgabe ergeben die ersten beiden Zeilen das gewünschte Resultat. Aber die Ausgabe mit _print_r($multiply);_ (**Zeile 26**) ist "seltsam".

Intern erzeugt PHP für eine anonyme Funktion eine **Klasse _Closure_**. Und _**$multiply** enthält nun ein Objekt der Klasse. Diesem Objekt werden die Variablen_ $x _und_ $y _übergeben._


Hinweis für PHP Experten: PHP-intern ist die Closure als Klasse implementiert und nutzt die [magische Methode __invoke()](https://www.php.net/manual/de/language.oop5.magic.php#object.invoke).
Die __invoke()-Methode wird aufgerufen, wenn ein Skript versucht, ein Objekt als Funktion aufzurufen.

  
Sie haben hier also drei Dinge gelernt.
- Man kann anonyme Funktionen erstellen, indem man die Funktion einer Variablen zuweist, also _$variable = function (...)_ zugewiesen werden.
- Intern arbeitet PHP oft objektorientiert, ohne das wir dies merken.
- Sie haben die Begriffe "anonyme Funktion" und "Closure" kennen gelernt.

  
**Objektorientiertes Beispiel einer anonymen Funktion**  
Wenn Sie das Vorherige verstanden haben, dann kommt hier etwas ungewohntes zum Knobeln. Aber damit es nicht ganz so schwierig wird, ist der nachfolgende Sourcecode entsprechend kommentiert. Also bitte versuchen Sie den Sourcecode anhand der Kommentare zu verstehen.

```php
<?php
// Klasse Value bekommt im Konstruktor eine Variable $value
// und speichert diese als Eigenschaft
class Value {
    protected $value;
    public function __construct(int $value) 
    {
        $this->value = $value;
    }
    public function getValue(): int 
    {
        return $this->value;
    }
}
// Hauptprogramm
// Objekte der Klasse Value erzeugen
$three = new Value(3);
$four = new Value(4);

// Anonyme Funktion erzeugt automatisch eine Klasse Closure
// und instanziert automatisch ein Objekt (hier: $add)
// 这段代码创建了一个 **匿名函数**，它使用了 `$this->getValue()`。通常来说，在函数外部定义的闭包中 `$this` 是不能用的，**除非你通过 `Closure::call()` 或 `bindTo()` 把一个对象“绑定”进去。**
// 在 `Closure::call($obj)` 中，匿名函数里的 `$this` 指的就是传入的 `$obj`。
$add = function ($delta)
    {
        // Die anonyme Funktion hat über call() - siehe Zeile 38 bzw. 39
        // das Objekt $three bzw. $four übergeben bekommen 
        // und es kann $this->getValue() aufgerufen werden.
        $sum = $this->getValue() + $delta;
        echo $sum . "<br>";
    };
// call() ist vorgefertigte eine Methode der Klasse Closure
// und übergibt ein Objekt (hier $three bzw. $four)
// und damit wird die anonyme Funktion aufgerufen.
$add->call($three, 10); // 把 `$three` 这个对象作为 **上下文对象**，临时绑定到 `$add` 这个匿名函数中，然后执行它并传入参数 `10`。 $this->getValue() 等同于 $three->getValue()
$add->call($four, 10);
```

Ausgabe:  
_13_  
_14_  

  

Hinweis

Auf den ersten Blick unverständlichen Sourcecode sollten Sie immer in Ihren Editor kopieren (z.B. PHPStorm) und dort analysieren. Dann ist das Verständnis des Sourcecodes wirklich leichter.


# 6 Namespaces

Bisher müssen unsere Klassen **eindeutige Namen** haben, da ansonsten bei der Instanzierung z.B. _$ute = new Student()_ unklar wäre, welche Klasse _Student_ gemeint ist. Also **darf bisher jeder Klassenname nur einmal vergeben werden**.

In kleineren Projekten ist dies ok, aber wenn viele Entwickler*innen an einem Projekt arbeiten oder wenn man ein Framework einsetzt (also hunderte von Klassen installiert hat), dann ist dies ein großes Problem.

**Das Problem der eindeutigen Namen kann aber mit dem Konzept _Namespaces_ gelöst werden.**

Zunächst organisiert man die Dateistruktur auf der Festplatte so, dass unterschiedliche Bereiche in unterschiedlichen Ordnern gespeichert werden (siehe Abbildung, linke Seite mit der Ordnerstruktur). So kann es nun beispielsweise eine Datei (=Klasse) "Database.php" im Ordner "Exams" und eine gleichnamige Datei (=Klasse) "Database.php" im Ordner "Library" geben. Jetzt wird **in der Klasse _Database_ die im Ordner "Exams" liegt, der _namespace Exams_** eingeführt. Dabei sollte **der Namespace immer benannt werden, wie der Ordnername**.

[![File:namspaces2.png](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/7/7c/Namspaces2.png "File:namspaces2.png")](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/7/7c/Namspaces2.png)

 Abb. 72: Eine Klasse einem Namespace zuordnen

  
Wenn man dies auch für die Klasse _Database_ im Ordner "Library" macht, dann kann man die Klassen mit den identischen Klassennamen wieder eindeutig ansprechen. Hierzu wird beim Instanzieren der Namespace vor den Klassennahmen geschrieben (siehe Abbildung, rechte Seite mit _Exams\Database()_ und _Library\Database()_.

[![Namspaces1.png](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/thumb/4/4d/Namspaces1.png/650px-Namspaces1.png)](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/4/4d/Namspaces1.png)

 Abb. 73: Instanzieren unter Verwendung des Namespaces

  
Angenommen man greift normalerweise immer auf die Klassen im Namespace _Exams_ zu und nur selten auf andere Klassen in anderen Namespaces. Dann kann man mit _use Exams_ eine Abkürzung einführen. Somit muss man beim Instanzieren den Namespace nicht mehr mit angeben.

[![Namspaces3.png](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/thumb/f/fb/Namspaces3.png/650px-Namspaces3.png)](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/f/fb/Namspaces3.png)

 Abb. 74: Verwendung von ''use'' als Abkürzung eines Namespaces

  
**Regeln**

- In der Datei muss der Befehl _namespace_ immer am Anfang stehen, bevor die Klasse mit _class ..._ begonnen wird.
- Ein Namespace besteht normalerweise nicht nur aus einem Namen, sondern bildet die Verzeichnisstruktur ab. Dabei wird zur Trennung immer der Backslash "\" verwendet. Also beispielsweise _Ordner\Unterordner_.
- Ein Namespace sollte so heißen, wie der Ordner bzw. wenn es sich um eine verschachtelte Ordnerstruktur handelt, so wie der komplette Pfad zum Ordner.
- Alle Klassen eines Unterordners haben somit normalerweise denselben Namespace.