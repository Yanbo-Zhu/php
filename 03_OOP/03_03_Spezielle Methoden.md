

# 1 Getter und Setter

Es ist oftmals eine gute Lösung, wenn _Eigenschaften_ nicht direkt gelesen oder geschrieben werden, sondern _private_ sind und der Zugriff nur über sogenannte Getter- und Setter-Methoden erfolgt. Denn dies hat folgende Vorteile:

- Bevor eine _Eigenschaft_ einen Wert zugewiesen bekommt, kann man prüfen, dass der neue Wert keinen "Datenmüll" enthält und der Wert dem Wertebereich entspricht (es sich also um einen gültigen Wert handelt).
- _public_-Eigenschaften können von überall gelesen und geschrieben werden. Oftmals möchte man aber den "schreibenden Zugriff" nicht von überall zulassen. So kann es Eigenschaften geben, die über einen Getter immer lesbar sind, bei denen aber schreibende Änderungen an Bedingungen geknüpft sind.
- Später werden wir auch sehen, dass es somit möglich ist, mit dem [Beobachter-Pattern](https://isp.eduloop.de/loop/Verhaltensmuster_-_Beobachter_\(Observer\) "Verhaltensmuster - Beobachter (Observer)") die Information der Wertänderng einer _Eigenschaft_ an andere Programmteile weiterzuleiten.


```php
class Student
{
    private $matrNumber  = "1324345";      
    private $phoneNumber = "keine Angabe"; 

    public function getMatriculationNumber(): string
    {
        return $this->matrNumber; 
    }

    public function setPhoneNumber(string $newPhoneNumber): void
    {
        $this->phoneNumber = $newPhoneNumber;
    }
	
    public function getPhoneNumber(): string
    {
        return $this->phoneNumber;
    }
  ...
}
```


Im gezeigten Beispiel kann man die Matrikelnummer `$matrNumber`  zwar über  `getMatriculationNumber()` auslesen, aber nicht ändern. Die Telefonnummer `$phoneNumber` hingegen kann man über die Methode  `getPhoneNumber()` auslesen und über  `setPhoneNumber()` auch ändern.


# 2 Konstruktor construct()

Der Konstruktor wird genutzt, um einem Objekt bei seiner Erzeugung Anfangswerte zuzuweisen. Der Konstruktor hat in PHP immer die Bezeichnung _**[__construct()](https://secure.php.net/manual/de/language.oop5.decon.php)**_ und **wird mit zwei Unterstrichen geschrieben**.

Wir wollen in unserem Beispiel den Studierenden eine Matrikelnummer zuweisen. Anders als bei einer Telefonnummer soll jede/jeder Studierende eine eindeutige, nicht änderbare Matrikelnummer erhalten.


Klasse _**Student.php**_. Nun hat die Klasse einen Konstruktor, der bei der Erzeugung des Objektes automatisch aufgerufen und ausgeführt wird. Im Konstruktor steht hier nur zu Testzwecken eine echo-Ausgabe.


```php
<?php
class Student
{
    private $name         = "keine Angabe";
    private $matrNumber   = 0;    
    private $phoneNumber  = "keine Angabe";

    public function __construct(string $name, int $matrNumber)
    {
        $this->matrNumber = $matrNumber;
        $this->name   = $name;
        echo "Der Konstruktor wurde für $name aufgerufen <br>";
    }

    public function getName(): string
    {
        return $this->name; 
    }

    public function getMatriculationNumber(): int
    {
        return $this->matrNumber; 
    }

    public function setPhoneNumber(string $newPhoneNumber): void
    {
        $this->phoneNumber = $newPhoneNumber;
    }
	
    public function getPhoneNumber(): string
    {
        return $this->phoneNumber;
    }
}
```

Erstellen Sie nun ein Klassendiagramm für diese Klasse.

![](images/Pasted%20image%2020250421142528.png)

Das Hauptprogramm _**index.php**_ kann dann wie folgt aussehen:

```php
<?php
$classPath = __DIR__.DIRECTORY_SEPARATOR.'class'.DIRECTORY_SEPARATOR;
require_once $classPath.'Student.php';

$max = new Student("Max", 7201234);
$ute = new Student("Ute", 7209999);

echo 'Methode aufrufen und die Telefonnummer speichern<br>';
$max->setPhoneNumber("0170123456"); 

echo $max->getName() . " hat die Tel.-Nr. " . $max->getPhoneNumber();
?>
```

Ausgabe:  
_Der Konstruktor wurde für Max aufgerufen_  
_Der Konstruktor wurde für Ute aufgerufen_  
_Methode aufrufen und die Telefonnummer speichern_  
_Max hat die Tel.-Nr. 0170123456_

**Basisregel**  
- Eigenschaften eines Objekts, die bereits bei der Erzeugung vorhanden sind, sollten in einem Konstruktor übergeben werden. Hier sind dies der Name und die Matrikelnummer.
- Eigenschaften eines Objekts, die erst später festgelegt werden können oder die optional sind, sollen erst in einer anderen Methode gesetzt werden.

Eigenschaften, die ein Objekt nicht benötigt, sollten auch nicht als Eigenschaften festgelegt werden. Beispiele wäre hier, dass die Studierenden müde oder hungrig sind, da dies (normalerweise) keine festen Eigenschaften, sondern temporäre Zustände sind.


**Ein ganz typischer Konstruktor**  
Eine Klasse, die eine Verbindung zur Datenbank herstellt benötigt eigentlich immer
- IP-Adresse oder Host-Adresse der Datenbank
- Name der Datenbank
- User und Passwort


```php
class DbMysql
{
    // ... Eigenschaften ...
    private $connect = []; 
  
    // Konstruktor
    public function __construct(
        string $host, 
        string $database, 
        string $user, 
        string $passwd
    ) {
        $this->connect = [$host, $database, $user, $passwd];
    }
  
    // ... weitere Methoden ...
```



# 3 Destruktor destruct()

Der Destruktor ist, wie der Name schon sagt, sozusagen das Gegenstück zum Konstruktor. Er wird aufgerufen, wenn die Existenz eines Objekts endet. Er dient dem "Aufräumen". In ihm können Funktionalitäten realisiert werden, die bei Existenzende ausgeführt werden sollen.

**Falls der Programmierer keinen eigenen Destruktor definiert, wird ein Standard-Destruktor aufgerufen.** Und aus diesem Grund kann normalerweise auf den Destruktor verzichtet werden.

Die Destruktor-Methode hat den festgelegten Namen [__destruct()](https://secure.php.net/manual/de/language.oop5.decon.php). Ein Destruktor kann explizit mit _$meinObjekt->__destruct();_ aufgerufen werden, was dazu führt, dass der Speicherplatz des Objektes freigegeben werden kann.

# 4 Magische Methoden

Wir haben bereits ___construct()_ und ___destruct()_ kennen gelernt. Hierbei handelt es sich um sogenannte "Magische Methoden", die jeweils mit zwei Unterstrichen beginnen.

PHP stellt eine Reihe von ["Magischen Methoden"](https://secure.php.net/manual/de/language.oop5.magic.php) bereit, die Klassen implementieren können, um auf bestimmte Ereignisse zu reagieren.

Wir behandeln hier eine Auswahl dieser "Magischen Methoden".

|   |   |
|---|---|
|Funktion|Verwendung|
|[__construct()](https://secure.php.net/manual/de/language.oop5.decon.php#object.construct)|Wird beim Erzeugen eines Objektes aufgerufen.|
|[__destruct()](https://secure.php.net/manual/de/language.oop5.decon.php#object.destruct)|Wird beim Löschen eines Objektes aufgerufen.|
|[__get()](https://secure.php.net/manual/de/language.oop5.overloading.php#object.get)|Wird aufgerufen, wenn eine Eigenschaft einer Klasse gelesen werden soll, die nicht deklariert war.|
|[__set()](https://secure.php.net/manual/de/language.oop5.overloading.php#object.set)|Wird aufgerufen, wenn eine Eigenschaft einer Klasse geschrieben werden soll, die nicht deklariert war.|

- `__get($name)` —— 当访问一个不存在的属性时触发
    
- `__set($name, $value)` —— 当为一个不存在的属性赋值时触发

# 5 Methode set

Mit _**__set()**_ kann ein Objekt Eigenschaften erhalten, die vorher nicht deklariert wurden. Wir wollen dem Objekt _$ute_ aus unserem Beispiel nun bestandene Prüfungen und die zugehörigen Noten zuweisen. Dazu könnte man natürlich zuvor alle möglichen Prüfungen als Eigenschaften deklarieren, was aber nicht sinnvoll ist. Schließlich könnte Uta ja auch eine Lehrveranstaltung aus einem ganz anderen Fachbereich belegen. Somit muss eine flexible Form gefunden werden, die es ermöglicht Prüfungen und Noten hinzuzufügen.


```php
class Student
{
    private $name       = "keine Angabe";
    private $matrNumber = 0;      
    protected $exams    = [];  // Eigenschaft $exams als assoz. Array

    public function __construct(string $name, int $matrNumber)
    {
        $this->matrNr = $matrNumber;
        $this->name   = $name;
    }

    public function __set(string $subject, float $grade): void
    {
        $this->exams[$subject] = $grade;
    }
}

// Hauptprogramm
$ute = new Student("Ute", 7209999);
$ute->Internetprogrammierung = 1.3;
```


In **Zeile 21** wird so getan, als gäbe es eine Eigenschaft _Internetprogrammierung_ in der Klasse _Student_ und dieser Eigenschaft _Internetprogrammierung_ wird der Wert _1.3_ zugewiesen

Jetzt gibt es diese Eigenschaft _Internetprogrammierung_ aber gar nicht! Somit wird nachgeschaut, ob es eine **__set()**-Methode gibt, die stattdessen aufgerufen wird.

你**表面上**是在给对象 `$ute` 添加一个新属性 `Internetprogrammierung`，并赋值为 `1.3`（成绩），但：
1. 这个类 `Student` **没有声明名为 `Internetprogrammierung` 的属性**；
2. 所以 PHP 就自动去找类里有没有实现 `__set()`；
3. 有的话，它就调用： `$this->__set("Internetprogrammierung", 1.3);`

在 `__set()` 方法中
- 这个方法会把**属性名当作考试科目名称**（如 Internetprogrammierung）；
- 把赋的值（1.3）当作该考试的成绩； 
- 存进 `$exams` 这个关联数组里。


这段代码的设计意图是：
- 不需要提前写死每一门考试；
- 通过 `__set()` 动态地将新考试及其成绩添加进学生对象；
- 利用了 PHP 的魔术方法来实现“灵活属性扩展”。

如果你以后想**查看这些成绩**，可以实现 `__get()` 或定义一个自定义方法（比如 `printExams()`）来输出 `$exams` 内容。
要不要我也帮你写一个 `printExams()` 方法

---


Natürlich lassen sich die Prüfungen auch ganz explizit über eine Methode setzen und auslesen, was normalerweise der bessere Programmierstil ist:

```php
public function setExamResult(string $subject, float $grade): void
```


# 6 Methode get

Die Methode _**__get()**_ wird aufgerufen, sobald ein Zugriff auf eine nicht existente Eigenschaft einer Klasse erfolgt, z.B. weil die Eigenschaft mit _**__set()**_ gesetzt wurde.

```php
class Student
{
    private $name       = "keine Angabe";
    private $matrNumber = 0;
    protected $exams    = [];  // Eigenschaft $exams als assoz. Array

    public function __construct(string $name, int $matrNumber)
    {
        $this->matrNumber = $matrNumber;
        $this->name   = $name;
    }

    public function __set(string $subject, float $grade): void
    {
        $this->exams[$subject] = $grade;
    }

    public function __get(string $subject): ?float
    {
        if (isset($this->exams[$subject])) {
            return $this->exams[$subject];
        } else {
            return null;
        }
    }
}

$ute = new Student("Ute", 7201234);
$ute->Internetprogrammierung=1.3;  // Wert einer Eigenschaft zuweisen
echo $ute->Internetprogrammierung; // Wert aus der Eigenschaft auslesen
```


Ausgabe:  
_1.3_  


In **Zeile 30** wird nun eine Eigenschaft aufgerufen, die in der Klasse nicht deklariert ist. Somit wird nachgeschaut, ob es eine **__get()**-Methode gibt, die stattdessen aufgerufen wird.
In **Zeile 18** sehen wir mit _`?float`_ etwas Neues. Das _?_ vor dem _float_ bedeutet, dass auch der Wert _null_ zurückgegeben werden kann und ist notwendig, da ein _return null_ in Zeile 23 steht.


# 7 Selbsttest Nr. 2 zu OOP in PHP


1 
Einige Übungen (mit Lösungen) und Aufgaben (ohne Lösungen) zum Verständnis.

```php
<?php
class Horse
{
    private $horseType;
  
    public function __construct(string $horseType)
    {
        $this->horseType = $horseType;
    }

    public function ride(string $location): void
    {
        echo "Ich habe ein {$this->horseType} 
              und reite {$location} <br>";
    }
}

// Hauptprogramm
$anna  = new Horse("Deutsches Reitpony");
$paula = new Horse("Welsh B"); 
  
  
$anna->ride("in der Halle");
$paula->ride("am Strand");
```

Welche Ausgabe erzeugt dieser Sourcecode auf dem Browser? 
Ausgabe:
Ich habe ein Deutsches Reitpony und reite in der Halle
Ich habe ein Welsh B und reite am Strand


Schreiben Sie den Sourcecode so um, dass die Ausgabe nicht mehr in der Methode erfolgt, sondern die Methode einen String an das Hauptprogramm liefert, der dort ausgegeben wird. 



---

2 
Schreiben Sie den Sourcecode so um, dass die Ausgabe nicht mehr in der Methode erfolgt, sondern die Methode einen String an das Hauptprogramm liefert, der dort ausgegeben wird. 


```php
<?php
class Horse
{
    private $horseType;
  
    public function __construct(string $horseType)
    {
        $this->horseType = $horseType;
    }

    public function ride(string $location): void
    {
        return "Ich habe ein {$this->horseType} 
                und reite {$location} <br>";
    }
}

// Hauptprogramm
$anna  = new Horse("Deutsches Reitpony");
$paula = new Horse("Welsh B"); 
  
echo "{$anna->ride("in der Halle")}";
echo "{$paula->ride("am Strand")}";
```



---

3 
Schreiben Sie das Programm weiter, sodass auf dem Browser ausgegeben wird

a) "Der edelmann besitzt einen Goldklumpen".

b) Nutzen Sie dann eine Stringfunktion, damit der Großbuchstabe E erzeugt wird und ausgegeben wird

"Der Edelmann besitzt einen Goldklumpen"

c) Und mit Hilfe einer Schleife dann die drei Sätze

"Der Ritter besitzt einen Helm"
"Der Edelmann besitzt einen Goldklumpen"
"Der Zauberer besitzt einen Stab" 

```php
<?php

class Avatar
{
  public $feature;

  public function __construct(string $feature)
  {
    $this->feature = $feature;
  }
  
 // Hier Methoden ergänzen 
  
}

// Hauptprogramm
$avatar = [
  ritter => new Avatar("Helm"),
  edelmann => new Avatar("Goldklumpen"),
  zauberer => new Avatar("Stab"),
];

// Hier das Hauptprogramm ergänzen
```


---


4 
Wissen anwenden! Diese Aufgabe ist für den weiteren Wissenserwerb total wichtig!

Wir hatten im Abschnitt [Beispiel Formulare - Daten einlesen](https://isp.eduloop.de/loop/Beispiel_Formulare_-_Daten_einlesen "Beispiel Formulare - Daten einlesen") den Aufbau eines Programms zur Erstellung eines Formulars gezeigt. Hier nun eine wichtige Transferaufgabe in fünf Schritten. Lesen Sie sich bitte zunächst alle Aufgabenteile durch und gehen Sie dann schrittweise wie beschrieben vor.

1. Schreiben sie das Programm **formular2.php** so um, dass aus den bisherigen Funktionen nun Methoden werden ([Sichtbarkeit](https://isp.eduloop.de/loop/Sichtbarkeit "Sichtbarkeit") public). Erstellen Sie also eine Klasse **Html** und instanzieren sie diese Klasse im Hauptprogramm. Aus den Funktionsaufrufen im Hauptprogramm werden nun Methodenaufrufe. Probieren Sie das Programm anschließend aus.

2. Schreiben Sie die Methoden so um, dass sich darin keine echo-Befehle mehr befinden. Die echo-Ausgabe soll nur noch im Hauptprogramm stattfinden.

3. Lagern Sie nun die Klasse in eine eigene Datei **Html.php** aus und vergessen Sie nicht im Hauptprogramm eine Zeile einzufügen mit der die Klasse inkludiert wird. Kommentieren Sie nun die Klasse (Kommentarheader und Kommentare an den wichtigen Programmstellen).

4. Bearbeiten Sie die Datei **formular2a.php** entsprechend, sodass auch hierin nur noch die Methodenaufrufe der Klasse **Html.php** vorhanden sind.

Und wer es jetzt wirklich schön mag, der sollte die Inhalte der Dateien **formular2.php** und **formular2a.php** nun in einer Datei **index.php** zusammenfassen. Die Abfrage, ob die Formularseite oder die Ausgabeseite angezeigt wird, soll mit einer Fallunterscheidung (= if-Abfrage) erfolgen, bei der das Array $_POST auf [empty()](https://isp.eduloop.de/loop/Funktionen_empty\(\)_und_isset\(\) "Funktionen empty() und isset()") überprüft wird.


Programm zur Erzeugung der Formuarseite
```
<?php
/**
 * Beispiel Formular - Daten einlesen
 * Dateiname: formular2.php
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
```

Screenshot des erzeugten Formulars  
![File:formular1.png](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/d/db/Formular1.png "File:formular1.png")




 Programm zur Erzeugung der Formuarseite
```php
 <?php
/**
 * Beispielformular - gesendete Formulardaten verarbeiten
 * Dateiname: formular2a.php
 * @author Lisa Meijer & Jörg Thomaschewski
 * @date 19.04.2019
 */
function writeHeaderAndHeadline()
{
    echo "<!DOCTYPE html>
          <html lang=\"de\">
          <head><title>Formular</title>
          </head>
          <body>
          <h1>Beispielformular - Daten ausgeben</h1>
          <pre>";
}

function writeHtmlEnd()
{
    echo "</pre>
          </body></html>";
}


// Beginn des Hauptprogramms
writeHeaderAndHeadline();
print_r($_POST);
writeHtmlEnd();
```

Screenshot der erzeugten Ausgabeseite, wenn zuvor in die Formularfelder die Daten _Jörg_ und _Thomaschewski_ eingetragen wurden.  
![File:formular2.png](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/6/6f/Formular2.png "File:formular2.png")


