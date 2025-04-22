


# 1 Verzeichnisfunktionen

Über ein PHP-Script können Sie auch Verzeichnisinhalte auflisten.

|Funktion|Beschreibung|
|---|---|
|[opendir()](http://php.net/manual/de/function.opendir.php)|öffnet ein Verzeichnis-Handle (danach können weitere Aufrufe getätigt werden)|
|[readdir()](http://php.net/manual/de/function.readdir.php)|ein Eintrag wird aus einem Verzeichnis-Handle gelesen|
|[closedir()](http://php.net/manual/de/function.closedir.php)|ein Verzeichnis-Handle wird geschlossen|
|[mkdir()](http://php.net/manual/de/function.mkdir.php)|erstellt ein Verzeichnis|
|[rmdir()](http://php.net/manual/de/function.rmdir.php)|löscht ein Verzeichnis|
|[chdir()](http://php.net/manual/de/function.chdir.php)|wechselt in ein anderes Verzeichnis|


Auslesen aller Dateien im aktuellen Verzeichnis>

```php
$directory = opendir('..\..');
while ($file = readdir($directory)) {
    echo "$file <br>";
}
closedir($directory);
```



**Sicherheitshinweis: Die folgende Aufgabe dürfen Sie nur auf dem Ihnen im Modul zur Verfügung gestelltem Server probieren!**  

Nehmen Sie dieses kleine Script und probieren sie es auf IHREM Webserver aus. Ändern Sie _opendir('.')_ in _opendir('..')_ um und versuchen Sie auch das übergeordnete Verzeichnis auszulesen. Probieren Sie es anschließend mit einem beliebigen Verzeichnis, z.B. _/etc/apache2_, oder gehen Sie mit _opendir('../../..')_ schrittweise immer weiter im Dateibaum vor.  
  
Im Kapitel [Dateien lesen und schreiben](https://isp.eduloop.de/loop/Dateien_lesen_und_schreiben "Dateien lesen und schreiben") erfahren Sie, wie die Daten aus Dateien ausgelesen werden können. Gelingt es Ihnen, die Datei **/etc/passwd** auszulesen?

# 2 Prozesse starten und schließen

Ein PHP-Script kann Systembefehle (z.B. Unix-Befehle) ausführen, um beispielsweise ein Mail-Programm aufzurufen.

|Funktion|Beschreibung|
|---|---|
|[popen()](http://php.net/manual/de/function.popen.php)|öffnet eine Verbindung zu einem Prozess|
|[pclose()](http://php.net/manual/de/function.pclose.php)|schließt die Verbindung mit dem Prozess|

 Tab. 30: Prozesse starten und schließen

  

Beispiel

Der Abschnitt für den Aufruf des Mailprogramms lautet:
```
$fd = popen("/usr/sbin/sendmail -t", "w");
fputs($fd, "To: studi@technik-emden.de\n");
fputs($fd, "Subject: Internetanfrage\n\n");
fputs($fd, "Sie haben folgende Anfrage erhalten:\n$text");
pclose($fd);
```

  

Hinweis

**Sicherheitshinweis:** Die Mächtigkeit von PHP führt dazu, dass jeder Nutzer, der PHP-Scripte auf den Webserver stellen kann, auch Unix-Befehle ausführen darf. Wenn Sie also einen Webserver konfigurieren und andere Nutzer darauf arbeiten dürfen (beispielsweise PHP-Skripte hochladen), dann müssen Sie sich umfangreich um Sicherheitseinstellungen in der php.ini kümmern.

Das Problem sind dabei weniger die vertrauenswürdigen Nutzer, sondern deren gegenbenenfalls unprofessionell geschriebenen PHP-Programme.



# 3 Dateien lesen und schreiben

Um Dateien vollständig zu lesen oder zu schreiben, sprich ohne sich viel Gedanken um einen Dateizeiger machen zu müssen, kann man die folgenden Befehle nutzen. Diese bieten einen einfachen und schnellen Weg, Daten zu lesen oder zu schreiben.

|Funktion|Beschreibung|
|---|---|
|[file_get_contents()](http://php.net/manual/de/function.file-get-contents.php)|Liest den Inhalt einer Datei in einen String.|
|[file_put_contents()](http://php.net/manual/de/function.file-put-contents.php)|Schreibt den Inhalt einer String-, oder Array-Variable in eine Datei.|
|[file()](http://php.net/manual/de/function.file.php)|Liest eine ganze Datei zeilenweise in ein Array.|
|[file_exists()](http://php.net/manual/de/function.file-exists.php)|Prüft, ob eine Datei existiert.|

 Tab. 31: Dateien lesen und schreiben, einfache Funktionen

---

Somit lassen sich recht einfach Text oder Daten in eine Datei schreiben und wieder auslesen.


```
$textIn = "Dies ist ein Beispiel-Text.\nZweite Zeile";
// Text in Datei a.txt schreiben
file_put_contents("a.txt", $textIn); 
// Text aus der Datei a.txt auslesen 
$textOut = file_get_contents("a.txt");
print_r($textOut);
```
Ausgabe:  
_Dies ist ein Beispiel-Text. Zweite Zeile_  


---

  
Beim Auslesen gibt es neben der Funktion _file_get_contents()_ auch die Möglichkeit, die Funktion _file()_ zu nutzen. Dabei unterscheiden sich die beiden hauptsächlich in der Art der Ausgabe. Während die Funktion _file_get_contents()_ den Inhalt der Datei als String zurück gibt, gibt die Funktion _file()_ den Inhalt der Datei als Array zurück. Dabei enthält jedes Element des Arrays eine Zeile des Dateiinhalts.

```
$textIn = "Dies ist ein Beispiel-Text.\nZweite Zeile";
// Text in Datei a.txt schreiben
file_put_contents("a.txt", $textIn); 
// Text aus der Datei a.txt auslesen 
$textOut = file("a.txt");
print_r($textOut);
```

Ausgabe:  
_Array ( [0] => Dies ist ein Beispiel-Text. [1] => Zweite Zeile )_

---

Auch mit _readfile()_ kann eine Datei einfach ausgelesen werden. Dabei hat _readfile()_ die Eigenart, dass die Datei direkt auf dem Browser ausgegeben wird, also ohne die Verwendung von _print_r()_. Damit eignet sich _readfile()_ vorallem zum Debugging, um schnell mal festzustellen, was sind in der Datei befindet.

```
$textIn = "Dies ist ein Beispiel-Text.\nZweite Zeile";
// Text in Datei a.txt schreiben
file_put_contents("a.txt", $textIn); 
// Text aus der Datei a.txt auslesen 
readfile("a.txt");
```

Ausgabe:  
_Dies ist ein Beispiel-Text. Zweite Zeile_


---
  
**Teile einer Datei auslesen**  
Sind jedoch nur Teile einer Datei von Interesse, kann man die folgenden Befehle in Kombination verwenden. Hiermit sind weitaus komplexere Abfragen und Zugriffe auf Dateien möglich.

|Funktion|Beschreibung|
|---|---|
|[fopen()](http://php.net/manual/de/function.fopen.php)|Öffnet eine Datei|
|[feof()](http://php.net/manual/de/function.feof.php)|Prüft, ob der Dateizeiger am Ende der Datei steht|
|[fgets()](http://php.net/manual/de/function.fgets.php)|Liest eine Zeile von Beginn des Dateizeigers|
|[fread()](http://php.net/manual/de/function.fread.php)|Liest Binärdaten aus einer Datei|
|[fwrite()](http://php.net/manual/de/function.fwrite.php)|Schreibt den Inhalt einer Zeichenkette in eine Datei. Die Zeichenkette kann auch binäre Daten enthalten (= Binär-sicheres Schreiben).|
|[fclose()](http://php.net/manual/de/function.fclose.php)|Schließt den geöffneten Dateizeiger|

 Tab. 32: Dateien lesen und schreiben


## 3.1 fopen()

Für _fopen("Dateiname", "Aktion")_ sind folgende Aktionen zugelassen:

|Aktion|Beschreibung vom [Manual](http://php.net/manual/de/function.fopen.php)|
|---|---|
|_r_|Öffnet die Datei nur zum Lesen und positioniert den Dateizeiger auf den Anfang der Datei.|
|_r+_|Öffnet die Datei zum Lesen und Schreiben und setzt den Dateizeiger auf den Anfang der Datei.|
|_w_|Öffnet die Datei nur zum Schreiben und setzt den Dateizeiger auf den Anfang der Datei, sowie die Länge der Datei auf 0 Byte. Wenn die Datei nicht existiert, wird versucht sie anzulegen.|
|_w+_|Öffnet die Datei zum Lesen und Schreiben und setzt den Dateizeiger auf den Anfang der Datei, sowie die Länge der Datei auf 0 Byte. Wenn die Datei nicht existiert, wird versucht sie anzulegen.|
|_a_|Öffnet die Datei nur zum Schreiben. Positioniert den Dateizeiger auf das Ende der Datei. Wenn die Datei nicht existiert, wird versucht sie anzulegen.|
|_a+_|Öffnet die Datei zum Lesen und Schreiben. Positioniert den Dateizeiger auf das Ende der Datei. Wenn die Datei nicht existiert, wird versucht sie anzulegen.|

 Tab. 33: fopen()-Aktionen

## 3.2 Beispiel


Eine Datei zeilenweise auslesen und auf dem Browser ausgeben.

```
$testfile = fopen("a.txt", "r");
while (!feof($testfile)) {
    $line = fgets($testfile, 1000);
    echo "$line <br>";
}
fclose($testfile);
```


Ausgabe (der zuvor angelegten Datei a.txt):  
_Dies ist ein Beispiel-Text._  
_Zweite Zeile_

# 4 Daten im JSON-Format speichern

JSON (= **J**ava**S**cript **O**bject **N**otation) basiert auf JavaScript (ECMA-Script 3) und ist ein kompaktes Datenformat.

Es bietet sich in sehr vielen Projekten als Alternative zum viel komplexeren Datenformat XML an und kann aufgrund seiner **sehr einfachen Struktur** ideal zum **Datenaustausch** zwischen Systemen verwendet werden. Parser zum Einlesen und Ausgeben des JSON-Formats gibt es für alle gängigen (Web-)Programmiersprachen. Außerdem bieten viele Web-Frameworks an, die Daten mittels JSON als Alternative zu XML auszutauschen. Dies ist besonders interessant für Web-Anwendungen, da diese JSON mittels JavaScript sehr einfach als Datenobjekt interpretieren können.

Das JSON-Format ist für Menschen und Maschinen einfach lesbar, viel einfacher als ein XML-Dokument. JSON-Elemente bestehen aus Werten, für die die JavaScript-Regeln gelten:

- String
- Number
- Boolean (true/false)
- null

und können nur in zwei Strukturen gespeichert werden:

- **Arrays**: Sortierte Listen, also im Sinne anderer Programmiersprachen **"indizierte Arrays"**. Ein JSON-Array wird in eckigen Klammern dargestellt: ["Value1", "Value2", "Value3", "Value4"].
- **Objekte**: Dies sind keine Objekte im Sprachgebrauch der objektorientierten Programmierung, sondern **Name-Wert-Paare**, und diese entsprechen in anderen Programmiersprachen **assoziativen Arrays**. Ein JSON-Objekt wird in geschweiften Klammern dargestellt: {"Name1": "Value1", "Name2": "Value2", "Name3": "Value3", "Name4": "Value4"}.

Die Mächtigkeit ergibt sich durch die Möglichkeit (wie bei Arrays üblich), die beiden Strukturen ineinander zu verschachteln.

Beispiel

Hier ein typisches Beispiel eines JSON-Objekts, das ein Array enthält.

```
{
    "name": "Thomas",
    "age": 36,
    "hobbys": ["music", "arts", "sports"]
}
```

  
## 4.1 **JSON und PHP**  : json_encode() and json_decode()

Nehmen wir nun ein anderes Beispiel. Gegeben sei ein PHP-Formular. Die Daten daraus sollen im JSON-Format gespeichert werden.

[![Php2-json.png](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/1/16/Php2-json.png)](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/1/16/Php2-json.png)

 Abb. 61: Beispielformular

Dann könnte die dazugehörige JSON-Datei wie folgt aussehen. Und hier ein Beispiel für ein verschachteltes JSON-Objekt:

```
{
    "name": "Schmid",
    "prename": "Ute",
    "exams": ["Mathe 2", "BWL", "Design", "IProg"]
}
```
Dieses JSON-Format erzeugt die PHP-Funktion [_**json_encode(ARRAY)**_](https://secure.php.net/manual/de/function.json-encode.php) automatisch, wenn das PHP-Array korrekt aufgebaut ist. Das dazugehörige PHP-Array muss wie folgt aussehen:

```
$person = [
    "name"    => "Schmid", 
    "prename" => "Ute", 
    "exams"   => ["Mathe 2", "BWL", "Design", "IProg"]
];

$jsonString = json_encode($person);
echo $jsonString;
```

Ausgabe:  
```
{_"name":"Schmid","prename":"Ute","exams":["Mathe 2","BWL","Design","IProg"]_}
```

  
Da JSON ein übliches Format zum Datenaustausch ist, können die so erzeugten Daten von anderen Programmen gut eingelesen werden.

Ein JSON-Objekt kann mit [_**json_decode(STRING)**_](https://secure.php.net/manual/en/function.json-decode.php) wieder in ein PHP-Array umgewandelt werden. Weitere Hinweise gibt es beispielsweise auf der Seite von [Michael Nitschinger](http://nitschinger.at/Handling-JSON-like-a-boss-in-PHP/).


# 5 Beispiel Formulare - Daten speichern

In diesem Beispiel sollen die übertragenen Daten auf der Festplatte des Server in einer Textdatei gespeichert werden.

Zunächst wird zur Darstellung des Formulars das bereits bekannte Beispiel aus dem [Unterkapitel Formulare - Daten einlesen](https://isp.eduloop.de/loop/Beispiel_Formulare_-_Daten_einlesen "Beispiel Formulare - Daten einlesen") hier verwendet.


```
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
startForm("post", "formular3a.php");
writeInputField("Vorname", "vorname");
writeInputField("Name",    "nachname");
closeFormAndFooter();
?>
```

  
Screenshot des erzeugten Formulars  
[![File:formular1.png](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/d/db/Formular1.png "File:formular1.png")](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/d/db/Formular1.png)

  
Die Neuerungen sind im folgenden PHP-Sourcecode enthalten (**Zeilen 27-40**). Dort werden die Formulardaten in einer Textdatei auf dem Server gespeichert.


```
<?php
/**
 * Beispiel Formular - Daten mit foreach() ausgeben
 * @author Lisa Meijer & Jörg Thomaschewski 
 * @date 04.09.2019
 */
function writeHeaderAndHeadline()
{
    echo "<!DOCTYPE html>
          <html lang=\"de\">
          <head><title>Formular</title>
          </head>
          <body>
          <h1>Daten auslesen</h1>";
}
function writeHtmlEnd()
{
    echo "</body></html>";
}
// Beginn des Hauptprogramms
writeHeaderAndHeadline();
// Dateiinhalt wird gelöscht
file_put_contents("formular3b.txt", "");
// Alle POST-Daten mit foreach() auslesen und speichern
foreach ($_POST as $field => $content) {
    if (!empty($content)) {
        file_put_contents("formular3b.txt", $content, FILE_APPEND); 
    }
}
// Gespeicherte Datei auslesen
echo "Es wurden folgende Daten gespeichert:<br>";
$textOut = file_get_contents("formular3b.txt");
echo "$textOut";
writeHtmlEnd();
?>
```

  
Screenshot des erzeugten Formulars  
[![File:formular3b.png](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/c/c1/Formular3b.png "File:formular3b.png")](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/c/c1/Formular3b.png)

Hier werden nun die Daten in das Dateisystem des Servers gespeichert.

In **Zeile 33** wird jeweils ein Datensatz in die datei geschrieben. Damit die vorherigen Daten nicht überschrieben werden, wird die Syntax _FILE_APPEND_ genutzt.

Mit diesem Wissen lässt sich auch verstehen, warum **Zeile 28** benötigt wird. Hier ist kein _FILE_APPEND_ vorhanden, sodass ein Datensatz die bisherigen Einträge überschreibt. Dieses Überschreiben findet mit einem leeren String _""_ statt. Somit steht vor dem ersten Aufruf der Zeile 33 eine leere Textdatei zur Verfügung.

  
**Sicherheitshinweis**: Bitte an die Sicherheit denken und NIE Benutzereingaben als Variable in einen Funktionsaufruf schreiben! Und schon gar nicht auf dem Server abspeichern. Überlegen Sie einmal, was passieren könnte und diskutieren Sie dies im Moodle-Forum oder in einer Webkonferenz.

Aufgabe

Die Programmierung ist nicht gut, denn bei jedem Durchlauf der for-Schleife wird die Datei erneut aufgerufen und es wird nur ein Datensatz geschrieben. **So darf man nicht programmieren, denn jeder externe Aufruf (Textdatei, Datenbank, etc.) verbraucht viele Rechner-Ressourcen!**  
  
Überlegen Sie, wie sie dies Problem lösen würden, sodass auf die externe Datei nur ein Schreibzugriff durchgeführt wird.


