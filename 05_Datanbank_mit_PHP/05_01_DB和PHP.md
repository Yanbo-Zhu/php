
# 1 PHP und MySQL verbinden

PHP und MySQL verbinden Zur Arbeit mit einer Datenbank nutzen wir die fertigen Klassen des PHP Data Objects (PDO). Hierdurch können wir mit einer Schnittstelle unterschiedlichste Datenbanken ansprechen.

Zunächst sollten wir nachsehen, ob PDO aktiv ist. Mit dem uns schon bekannten _phpinfo()_ lässt sich dies sehr einfach ermitteln.
```
<?php
phpinfo();
```


Und dann bis zum Abschnitt "P" auf der Website scrollen. Wenn wir so eine Ausgabe sehen, dann ist PDO aktiv.

[![Pdo-aktiv.png](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/thumb/b/bb/Pdo-aktiv.png/650px-Pdo-aktiv.png)](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/b/bb/Pdo-aktiv.png)

 Abb. 80: Nachsehen, ob PDO aktiv ist.

  
**Daten aus einer Datenbank abfragen:**  
Im letzten Unterabschnitt haben Sie eine Datenbank mittels phpMyAdmin in die SQL-Datenbank angelegt und diese mit den Beispieldaten gefüllt:

|id|name|matnr|semester|course|
|---|---|---|---|---|
|1|Sonja Musterfrau|5001111|10|Medientechnik|
|2|Sascha Student|5009999|12|Medientechnik|

Hier wollen wir Daten aus der Tabelle abfragen

```php
<?php
// Verbindung zum Datenbankserver und der Datenbank "example" herstellen
$pdo = new PDO('mysql:host=localhost; dbname=example', 'root', '');

// Abfrage der Tabelle "php"
$result = $pdo->query("SELECT name, matnr FROM php");

// Nachsehen, was in $result enthalten ist
print_r($result);
echo "<hr>";
// Ausgeben der Inhalte
foreach ($result as $row) {
    echo $row['name']
        . " hat die Matrikelnummer "
        . $row['matnr']
        . "<br>";
}
```

Die Ausgabe auf dem Browser:
[![Pdo-ausgabe1.png](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/1/19/Pdo-ausgabe1.png)](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/1/19/Pdo-ausgabe1.png)

- In **Zeile 4** stellen wir die Verbindung zum Datenbankserver her und geben als Ziel die Datenbank "example" ein.
- In **Zeile 7** führen wir eine Datenbankabfrage durch.
- In **Zeile 10** schauen wir, was _$result_ eigentlich ist und erhalten als Ergebnis, dass es sich dabei um ein Objekt der Datenbankabfrage handelt (siehe "Die Ausgabe auf dem Browser").
- Trotzdem können wir dieses Objekt in **Zeile 14** in _foreach ($result as $row)_ wie ein Array benutzen. Also wird im Hintergrund ein [ArrayAccess-Interface](https://isp.eduloop.de/loop/ArrayAccess-Interface "ArrayAccess-Interface") vorhanden sein, die uns dies ermöglicht. Wir haben hier also ein Beispiel, wie wir ein Objekt wie ein Array behandeln.




**Daten in einer Datenbank ändern**  
Mit der PDO-Methode _query()_ können wir nicht nur Daten abfragen, sondern beliebige SQL-Befehle ausführen. Also die Daten auch ändern.


```php
<?php

// Verbindung zum Datenbankserver und der Datenbank "example" herstellen
$pdo = new PDO('mysql:host=localhost; dbname=example', 'root', '');

// Abfrage der Tabelle "php"
$pdo->query("UPDATE `php` SET `semester` = '13' WHERE `php`.`matnr` = '5009999'");
$result = $pdo->query("SELECT name, semester FROM php");

// Nachsehen, was in $result enthalten ist
print_r($result);
echo "<hr>";

// Ausgeben der Inhalte
foreach ($result as $row) {
    echo $row['name']
        . " ist nun im Semester: "
        . $row['semester']
        . "<br>";
}
```


Gerade wenn Sie erste Programmierungen mit einer Datenbankanbindung realisieren, sollten Sie wie folgt vorgehen:

- Datenbank und Tabellen in phpMyAdmin erstellen.
- Datenbank mit realistischen Daten in phpMyAdmin füllen.
- SQL-Befehle immer in phpMyAdmin ausprobieren und wenn das Ergebnis "wie gewünscht" ist, dann die SQL-Abfrage in das PHP-Script kopieren.
- Zunächst üben, ob Sie die Daten der Datenbank mit ihrem PHP-Script abrufen können.
- Danach erst Daten mit dem PHP-Script ändern oder neue Datensätze in die Datenbank schreiben. Dabei sollten Sie phpMyAdmin immer geöffnet haben und nachsehen, was in die Datenbank geschrieben wurde.


# 2 Datenbankverbindung verbessern

## 2.1 **Prepared Statements**  

Wir hatten bereits im Unterkapitel [SQL](https://isp.eduloop.de/loop/SQL "SQL") die Vorteile benannt und geschrieben: "Ein Prepared Statement führt eine Datenbankabfrage durch und nutzt dabei keine konkreten Parameterwerte, sondern Platzhalter anstelle der Parameter". Hier wollen wir uns nun die Durchführung ansehen.

Eigentlich ist es ganz einfach, wenn wir die Methode _query()_ durch die Methoden _prepare()_ und _execute()_ ersetzen.

Code

```php
<?php
$pdo = new PDO('mysql:host=localhost; dbname=example', 'root', '');
$stmt = $pdo->prepare("SELECT name, matnr FROM php");
$stmt->execute();
foreach ($stmt as $row) {
    echo $row['name']
        . " hat die Matrikelnummer "
        . $row['matnr']
        . "<br>";
}
```


Ausgabe:  
_Sonja Musterfrau hat die Matrikelnummer 5001111_  
_Sascha Student hat die Matrikelnummer 5009999_

In **Zeile 5** schreiben wir das Prepared Statement und in **Zeile 6** führen wir dieses aus.


---


Im nächsten Beispiel wird klar, wie wir ein Prepared Statement sinnvoll nutzen können, denn oftmals soll nur ein Teilbereich ausgegeben werden.

```php
<?php

$start = 5000000;
$end = 5005000;

$pdo = new PDO('mysql:host=localhost; dbname=example', 'root', '');

$stmt = $pdo->prepare(
    "SELECT * FROM php WHERE matnr BETWEEN :start AND :end"
);

$stmt->bindParam(":start", $start);
$stmt->bindParam(":end", $end);
$stmt->execute();

foreach ($stmt as $row) {
    echo $row['name']
        . " hat die Matrikelnummer "
        . $row['matnr']
        . "<br>";
}
```

Ausgabe:  
_Sonja Musterfrau hat die Matrikelnummer 5001111_

Mit der Methode _bindParam()_ in den **Zeilen 12 und 13** können wir Parameter angeben. Diese Parameter könnten z.B. durch ein Webformular an das PHP-Programm geschickt werden.


---

Aufgabe

Erstellen Sie ein Webformular mit zwei Formularfeldern, sodass die Variablen `$start` und `$end` nun über das Formular eingegeben werden können.

**Sicherheitshinweis: Arbeiten Sie bitte immer mit Prepared Statements** (anstelle von einfachen _query_-Abfragen), denn in _query_-Abfragen kann man SQL-Befehle einschleusen, die zu SQL-Injections und damit zu sehr großen Sicherheitsrisiken führen. Bei _prepare()_ kann dies nicht passieren, da nur einzelne Parameter und keine SQL-Befehle zur Datenbank übernommen werden.

Um dann noch potentielle Sicherheitslücken zu SQL-Injections über unterschiedliche Zeichensätze zu vermeiden, sollten wir beim Aufruf der Datenbank 'charset=utf8 _mit angeben:_

```
PDO('mysql:host=localhost; charset=utf8; dbname=example', 'root', '');
```

Außerdem sollten wir bei PDO noch eine Zeile als Sicherheitseinstellung mit hinzufügen:

```
$pdo->setAttribute(PDO::ATTR_EMULATE_PREPARES, false);
```


---


### 2.1.1 禁用“模拟预处理语句（emulated prepared statements）

```
$pdo->setAttribute(PDO::ATTR_EMULATE_PREPARES, false);
```

是在配置 PDO（PHP Data Objects） 的行为，具体是 禁用“模拟预处理语句（emulated prepared statements）”，使用 数据库原生的预处理语句（native prepared statements）。
- 默认情况下，PDO 可能并不会把你的 `prepare()` 语句直接发送给数据库。
- 相反，它会在 PHP 层面模拟这个过程，把 SQL 语句和参数拼接好之后，一次性发送到数据库执行。
- `false` 表示 **禁用模拟**，也就是说：
    - SQL 的 `prepare()` 和 `execute()` 会真实地在数据库端处理。
    - 参数绑定是在数据库里完成的，而不是由 PHP 来拼接。

使用 `false` 的好处
1. **更安全：** 防止 SQL 注入更彻底，尤其是涉及 `LIMIT`、`ORDER BY` 等敏感关键字。
2. **更真实：** 可以测试数据库实际支持的预处理功能。
3. **更稳定：** 一些数据库驱动（如 MySQL）在原生处理时会表现得更标准。



## 2.2 **Datenbank mit Password schützen!!!**  

Nun müssen wir unbedingt unsere Datenbank **mit einem Password schützen**! Und natürlich sollte man einen Datenbankzugriff auf keinen Fall mit root-Rechten erlauben. Also müssen wir einen Datenbank-Nutzer (=Benutzerkonto) anlegen. Dieses Benutzerkonto wird verwendet, damit das PHP-Script mit dem Nutzernamen und dem Passwort auf die Datenbanktabelle zugreifen darf (aber nur auf die angegebene Tabelle und nicht auf die gesamte Datenbank!).

Ein Benutzerkonto können wir über phpMyAdmin anlegen. Dazu im Reiter "Benutzerkonten" klicken auf "Benutzerkonto hinzufügen":

[![Mysql-benutzer1.png](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/thumb/0/0a/Mysql-benutzer1.png/450px-Mysql-benutzer1.png)](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/0/0a/Mysql-benutzer1.png)

 Abb. 81: Benutzerkonto über phpMyAdmin anlegen (1)

  
Auf der Seite "Benutzerkonto hinzufügen" die Felder entsprechend des Screenshots ausfüllen:

[![Mysql-benutzer2.png](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/thumb/3/39/Mysql-benutzer2.png/450px-Mysql-benutzer2.png)](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/3/39/Mysql-benutzer2.png)

 Abb. 82: Benutzerkonto über phpMyAdmin anlegen (2)

  
Weiter unten auf der Seite noch die Rechte vergeben, was natürlich je nach Anwendung genau überlegt sein muss. Wir vergeben für unser Beispiel alle "Daten-Rechte".

[![Mysql-benutzer3.png](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/thumb/5/5c/Mysql-benutzer3.png/450px-Mysql-benutzer3.png)](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/5/5c/Mysql-benutzer3.png)

 Abb. 83: Benutzerkonto über phpMyAdmin anlegen (3)

Unsere Beispielanwendung sieht inzwischen wie folgt aus und enthält in **Zeile 8** das Password zur Datenbank.
```php
<?php

$start = 5000000;
$end = 5005000;

$pdo = new PDO('mysql:host=localhost; charset=utf8; dbname=example',
    'StudAdmin',
    'D0AugLBs8uvTiPE2'
);

$pdo->setAttribute(PDO::ATTR_EMULATE_PREPARES, false);

$stmt = $pdo->prepare(
    "SELECT * FROM php WHERE matnr BETWEEN :start AND :end"
);

$stmt->bindParam(":start", $start);
$stmt->bindParam(":end", $end);
$stmt->execute();

foreach ($stmt as $row) {
    echo $row['name']
        . " hat die Matrikelnummer "
        . $row['matnr']
        . "<br>";
}
```

Ausgabe:  
_Sonja Musterfrau hat die Matrikelnummer 5001111_

Mit  `$start` = 5000000_ und  `$end` = 6000000 erhalten wir beide Datensätze. Probieren Sie es aus!


# 3 Datenbankverbindung professionell (repo model controller)

Natürlich wollen wir die Datenbankverbindung in eine Klasse auslagern. Klassen, die für eine Verbindung mit einer Datenbank stehen, kann man gut mit dem Wort "Repository" kennzeichnen. Wir erstellen uns also eine Klasse _StudentRepository_.

Wenn wir im Unterkapitel [Klassen in Dateien auslagern und MVC-Prinzip](https://isp.eduloop.de/loop/Klassen_in_Dateien_auslagern_und_MVC-Prinzip "Klassen in Dateien auslagern und MVC-Prinzip") nachsehen, dann wurde dort das MVC-Prinzip erläutert. Dieses MVC-Prinzip wollen wir hier durch ein Repositoy ergänzen.

[![MVC-Repository.png](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/4/4f/MVC-Repository.png)](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/4/4f/MVC-Repository.png)


Was wir eben in einer Datei _index.php_ hatten, wird nun **in drei Dateien** aufgeteilt**.**



1 
**index.php** ist das Hauptprogramm und muss mit _require_once_ die anderen Dateien einbinden. Anschließend kommen die Variablen und die Verbindung zur Datenbank. Bis **Zeile 16** entspricht es dem bekannten Sourcecode aus dem letzten Unterkapitel.


Datei index.php (nur erste Zeilen) 
```php
<?php declare(strict_types=1);

require_once __DIR__.DIRECTORY_SEPARATOR.'StudentRepository.php';
require_once __DIR__.DIRECTORY_SEPARATOR.'StudentModel.php';

$start = 5000000;
$end   = 6000000;


// Verbindung zur Datenbank herstellen
$pdo = new PDO('mysql:host=localhost; charset=utf8; dbname=example',
    'StudAdmin',
    'D0AugLBs8uvTiPE2'
);

$pdo->setAttribute(PDO::ATTR_EMULATE_PREPARES, false);


// Datenbankabfrage über die Klasse StudentRepository() vornehmen
$studentRepository = new StudentRepository($pdo);
$student = $studentRepository->fetchStudentByMatNr($start, $end);

...
```

In **Zeile 20** erstellen wir ein Objekt der (noch neu zu erstellenden Klasse) _StudentRepository_ und müssen der Klasse das Datenbankobjekt _$pdo_ übergeben, damit eine Verbindung zur Datenbank vorhanden ist.

In **Zeile 21** rufen wir die Methode _fetchStudentByMatNr()_ auf, die dann die eigentliche Datenbankabfrage enthalten wird.



2 
**StudentRepository.php** führt die Datenbankabfrage durch. Die Datenbankabfrage haben wir in eine Methode _fetchStudentByMatnr()_ geschrieben. Sicherlich würden in einem realen Projekt einige weitere Abfragen hinzukommen, die man dann alle in eigene Methoden schreiben kann.


**Datei StudentRepository.php (nur erste Zeilen)**
```php
<?php declare(strict_types=1);

class StudentRepository
{
    private $pdo;

    public function __construct(PDO $pdo)
    {
        $this->pdo = $pdo;
    }

    public function fetchStudentByMatnr(int $start, int $end)
    {
        $stmt = $this->pdo->prepare(
            "SELECT * FROM php WHERE matnr BETWEEN :start AND :end"
        );
        $stmt->bindParam(":start", $start);
        $stmt->bindParam(":end", $end);
        $stmt->execute();

...
```

In Repository-Klassen finden "echte" Datenbankabfragen statt. Aber oftmals möchte man Datenbankabfragen noch bearbeiten, z.B. um Teilbereiche zu bekommen. Wir haben in unserer Datenbanktabelle z.B. Vorname und Nachname in einem Feld (sollte man nicht machen!) und wollen nun jeweils die Vornamen auslesen. Hierfür ist eine Model-Klasse gut, die die Datenbankabfragen um _"virtuelle Abfragen"_ ergänzen kann. Mit der Model-Klasse werden also Datenbankstrukturen sinnvoll erweitert, ohne dass redundante Daten in der Datenbank gespeichert werden müssen.

**StudentRepository.php** enthält als Eigenschaften (_`$id_, _$name_, _$matnr_, _$semester_ und _$course_`) alle Spalten der Datenbank (id, name, matnr, semester und course), sowie weitere Eigenschaften, die über Methoden gefüllt werden. In unserem Fall wird mittels regulärem Ausdruck aus dem Gesamtnamen der Vorname ermittelt.

3 
**Datei StudentModel.php (fertig)**

```php
<?php declare(strict_types=1);
class StudentModel
{
    // Spalten der Datenbank
    public $id;
    public $name;
    public $matnr;
    public $semester;
    public $course;
    
    // Zusätzliche Eigenschaften
    public $firstName;
    
    public function extractFirstName(string $name): void
    {
        // geht bis zum 1. Leerzeichen und speichert dies in $1
        $this->firstName = preg_replace(
            '/^(.+?)\s(.+)$/',
            "$1",
            $name
        );
    }
}
```

  
**Daten von _StudentRepository_ an _StudentModel_ übergeben**  
Wir wollen später in der _index.php_ mit Objekten arbeiten und nicht mit Arrays. Dies hat in der professionellen Programmierung viele Vorteile.

4 
**Datei StudentRepository.php (vollständig, aber noch vorläufig)**

```php
<?php declare(strict_types=1);

class StudentRepository
{
    private $pdo;

    public function __construct(PDO $pdo)
    {
        $this->pdo = $pdo;
    }

    public function fetchStudentByMatnr(
        int $start, 
        int $end
    ): object {
        $stmt = $this->pdo->prepare(
            "SELECT * FROM php WHERE matnr BETWEEN :start AND :end"
        );
        $stmt->bindParam(":start", $start);
        $stmt->bindParam(":end", $end);
        $stmt->execute();

        // Objekt $student erstellen (und von Hand befüllen)
        // - 使用 `fetch()` 从结果集中获取**第一条记录**，作为一个关联数组返回（默认是 `PDO::FETCH_BOTH`）。
        // - 如果没有记录返回，`$studentArray` 会是 `false`。
        $studentArray = $stmt->fetch();

        $student = new StudentModel();
        $student->id = $studentArray["id"];
        $student->name = $studentArray["name"];
        $student->matnr = $studentArray["matnr"];
        $student->semester = $studentArray["semester"];
        $student->course = $studentArray["course"];

        echo 'Das Objekt $student sieht wie folgt aus:<pre>';
        print_r($student);
        echo '</pre>';

        return $student;

    }
}
```


Die Ausgabe auf dem Browser:
[![Studentmodell.png](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/a/a1/Studentmodell.png)](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/a/a1/Studentmodell.png)

Bis **Zeile 19** kennen wir die Datei schon (siehe oben).  
In **Zeile 24** nutzen wir die PDO-Methode _fetch()_, die uns die erste Zeile des Ergebnisses in ein Array liefert.  
In **Zeile 26** wird die Klasse _StudentModel_ instanziert, sodass z.B. mit _$student->id_ auf die Eigenschaften zugegriffen werden kann.  
In **Zeilen 27 - 31** werden alle Eigenschaften "gefüllt".  
In **Zeilen 33 - 35** wird das Objekt _$student_ ausgegeben. Es kann erkannt werden, dass es sich wirklich um ein Objekt handelt.

Somit kann jetzt in der _index.php_ ein Datenbankeintrag mit z.B. _$student->name_ angesprochen werden.

Sie können sich immer mal wieder mit _print_r()_ oder _var_dump()_ vergewissern, was Sie gerade in Variablen haben! An der Ausgabe oben können Sie sehen, dass das HTML-Tag `<pre>` hierfür sehr hilfreich sein kann. Vergessen Sie aber diese Befehle nicht im Quellcode wieer zu löschen, da es zu Fehlern bei der Ausgabe von HTML und HTTP Headern kommen kann.



5 
 Eine weitere Verbesserung

 In der Datei StudentRepository.php hatten wir die Eigenschaften der Klasse StudentModel alle einzeln gefüllt. Mit PDO-Methoden können wir dies automatisch erledigen, sodass der finale Sourcecode dann wie folgt aussieht: 

```php
<?php declare(strict_types=1);

class StudentRepository
{
    private $pdo;

    public function __construct(PDO $pdo)
    {
        $this->pdo = $pdo;
    }

    public function fetchStudentByMatnr(
        int $start,
        int $end
    ): array {
        $stmt = $this->pdo->prepare(
            "SELECT * FROM php WHERE matnr BETWEEN :start AND :end"
        );
        $stmt->bindParam(":start", $start);
        $stmt->bindParam(":end", $end);
        $stmt->execute();

        // Ergebnis soll in "StudentModel" gefüllt werden
        // Objekt "$student" der Klasse "StudentModel" wird 
        // automatisch erstellt, ohne "$student = new StudentModel()" 
        $stmt->setFetchMode(PDO::FETCH_CLASS, "StudentModel");
        $student =  $stmt->fetchAll(PDO::FETCH_CLASS, "StudentModel");

        echo 'Das Objekt $student sieht wie folgt aus:<pre>';
        print_r($student);
        echo '</pre>';

        return $student;
    }
}
```

Die Ausgabe auf dem Browser:

[![Studentmodell2.png](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/1/1b/Studentmodell2.png)](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/1/1b/Studentmodell2.png)

- Bis **Zeile 21** kennen wir die Datei schon (siehe oben).
- Mit _fetch()_ hatten wir nur den ersten Eintrag bekommen. Mit _fetchAll()_ in **Zeile 27** erhalten wir nun alle abgefragten Datenbankeinträge.
- Die PDO-Methoden _setFetchMode()_ in **Zeile 26** und _fetchAll()_ in **Zeile 27** benötigen als Paramater _PDO::FETCH_CLASS_ und die Zielklasse _StudentModel_. _PDO::FETCH_CLASS_ ist eine [PDO-Konstante](https://www.php.net/manual/en/pdostatement.fetchall.php) für die Datenformatierung.

Zwei weitere Dinge sind bemerkenswert:

- Wir haben ein Objekt _$student_ der Klasse _StudentModel_, das direkt über den Aufruf von _setFetchMode()_ erstellt wurde. Die Zeile _$student = new StudentModel()_ ist somit nicht mehr notwendig.

- Wir haben nun ein indiziertes Array _$student_ und die einzelnen Einträge im Array sind Objekte, jeweils ein Objekt für eine (Ergebnis-)Zeile der Datenbank.





6 
**Datei index.php (fertig)**

```
<?php declare(strict_types=1);

require_once __DIR__.DIRECTORY_SEPARATOR.'StudentRepository.php';
require_once __DIR__.DIRECTORY_SEPARATOR.'StudentModel.php';

$start = 5000000;
$end   = 6000000;


// Verbindung zur Datenbank herstellen
$pdo = new PDO('mysql:host=localhost; charset=utf8; dbname=example',
    'StudAdmin',
    'D0AugLBs8uvTiPE2'
);

$pdo->setAttribute(PDO::ATTR_EMULATE_PREPARES, false);


// Datenbankabfrage über die Klasse StudentRepository vornehmen
$studentRepository = new StudentRepository($pdo);
$student = $studentRepository->fetchStudentByMatNr($start, $end);

// 1. Ausgabe
echo 'Das Objekt $student sieht wie folgt aus:<pre>';
print_r($student);
echo '</pre>';

echo "<hr>";

// 2. Ausgabe
foreach ($student as $row) {
    echo $row->name . " ist im Studiengang " . $row->course . "<br>";
}

echo "<hr>";

// 3. Ausgabe
foreach ($student as $row) {
    $row->extractFirstName($row->name);
    echo $row->firstName . " im " . $row->semester . ". Semester <br>";
}

echo "<hr>";

// 4. Ausgabe
echo $student[1]->firstName . " studiert " . $student[1]->course;
?>
```


Die Ausgabe auf dem Browser: [![Studentmodell3.png](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/c/ce/Studentmodell3.png)](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/c/ce/Studentmodell3.png)

Sie haben hier mehrere Dinge gelernt.

- Die Datenbankverbindung wird im Hauptprogramm erstellt (hier: Objekt _$pdo_).
- Das Objekt _$pdo_ wird an die Repository-Klasse (hier: StudentRepository) weitergegeben und die Datenbankabfrage in einer Methode (hier: fetchStudentByMatNr()) ausgeführt.
- Anschließend wird das Ergebnis der Datenbankabfrage an die Model-Klasse (hier: StudentModel) weitergereicht. Dazu wird ein Objekt der Model-Klasse erstellt oder aber eine PDO-Methode erstellt dieses Objekt automatisch.
- Dadurch, dass dem Repository sowohl die Objekte der Klasse PDO als auch die Model-Klasse bekannt sind, kann man im Hauptprogramm auf die Zeilen- und Spalteneinträge der Datenbankergebnisse zugreifen (z.B. _$student[1]->course_).

  
Hier können Sie eine Zip-Datei herunterladen, die den gesamten Sourcecode enthält. Sie sollten das Programm unbedingt **auf Ihrem Server installieren und ausprobieren**: [StudentDatabaseRequest.zip](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/c/c8/StudentDatabaseRequest.zip "StudentDatabaseRequest.zip").


# 4 Datenbankverbindung Fehlerausgabe abfangen

Es ist immer wieder problematisch, dass das Datenbankpasswort im Klartext im PHP-Programm steht. Schauen wir uns mal an, was passiert, wenn die Verbindung zur Datenbank nicht wie gewünscht hergestellt werden kann.

[![DatenbankError.png](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/thumb/6/64/DatenbankError.png/650px-DatenbankError.png)](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/6/64/DatenbankError.png)

 Abb. 85: Fehlerhafte Datenbankverbindung

In der Fehlermeldung stehen der Nutzername _StudAdmin_ und das Passwort zur Anmeldung an die Datenbank im Klartext! So etwas darf nicht passieren und daher ist es in diesem Fall besonders wichtig den Fehler abzufangen.

  

Beispiel

**Datei index.php (nur erste Zeilen)**

```
<?php declare(strict_types=1);
require_once __DIR__.DIRECTORY_SEPARATOR.'StudentRepository.php';
require_once __DIR__.DIRECTORY_SEPARATOR.'StudentModel.php';

$start = 5000000;
$end   = 6000000;

// Verbindung zur Datenbank herstellen
try {
    $pdo = new PDO('mysql:host=localhost; charset=utf8; dbname=example',
        'StudAdmin',
        'D0AugLBs8uvTiPE2'
    );
} catch (Exception $e) {
    echo "Verbindung zur Datenbank funktioniert nicht";
    exit;
}
...
```
Ausgabe  
_Verbindung zur Datenbank funktioniert nicht_

- Mit einem try-catch-Block (**Zeilen 11, 16, 19**) werden Fehlermeldungen abgefangen, sodass es nicht mehr zur Ausgabe des Passwortes kommt.
- Mit _try_ wird der nachfolgende Block ausprobiert und wenn es zu einem Fehler kommt, dann wird der _catch_-Block ausgeführt. Somit wird dann mit _echo_ der String ausgegeben und in **Zeile 18** wird der PHP-Befehl _**exit**_ verwendet, damit die weitere Programmausführung abgebrochen wird, weil es ja ohne Datenbankverbindung keinen Sinn macht und nur zu anderen Fehlermeldungen führen würde.

Bei der Fehlerbehandlung wird auf die vordefinierte PHP-Klasse [Exception](https://www.php.net/manual/de/class.exception.php) (siehe **Zeile 16**) zugegriffen.

  

Anmerkung

Eine professionelle Fehlerbehandlung (Exception handling) wäre - wie so vieles in PHP - ein eigenes Kapitel wert. Aber wie so oft müssen wir und in diesem Modul auf einige Grundlagen beschränken. Wenn Sie professionell programmieren möchten, dann sollten Sie sich mit dem vielschichtigen Thema "Exception handling" ausführlich beschäftigen.





