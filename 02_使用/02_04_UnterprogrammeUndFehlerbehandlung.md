
# 1 Unterprogramme (function) in PHP

Ein Unterprogramm in PHP ist eine _function_ (= Funktion). Hier ein Beispiel:

```php
function add($x, $y)
{
    $z = $x+$y;
    echo "$z";
}
$a = 1;
$b = 2;
add($a, $b);
```

Die Funktion wird in **Zeile 1** definiert und es wird angegeben, welche Variablen (hier $x und $y) an die Funktion übergeben werden. In den Zeilen 2-5 steht, was die Funktion mit den Variablen macht.

In **Zeile 9** wird die Funktion aufgerufen und es werden **die Werte der Variablen** $a und $b an die Funktion übergeben.

  
Um zu kennzeichnen, dass es sich bei einem Unterprogramm um eine Prozedur (keine Rückgabe) handelt, verwendet man in der Dokumentation häufig folgende Syntax:  

/**
* Text der erklärt was die Prozedur macht.
* @return void
*/

---
  
**Werte aus einer Funktion zurückgeben _return_**  
Im bisherigen Beispiel hatten wir keine Rückgabe, sondern die Funktion hat mit _echo_ direkt Daten ausgegeben (also über das PHP-Modul des Webservers zum Browser geschickt). Oftmals möchten wir aber das Ergebnis einer Funktion im Hauptprogramm nutzen. Dann arbeiten wir mit _**return**_.

Code

```
function add($x, $y)
{
    $z = $x+$y;
    return $z;
}
$a = 1;
$b = 2;
echo add($a, $b);
```
Achten Sie darauf, wie sich die **Zeilen 4 & 9** geändert haben. Die Ausgabe erfolgt nun nicht mehr in der Funktion, sondern zuerst wurde das Ergebnis mit _return_ ans Hauptporgramm übergeben und dort dann ausgegeben.


---

  
**Initialisieren eine Funktionsvariable mit _static_**  
Wenn innerhalb einer _function_ eine Variable nur einmal initialisiert werden soll, so kann dies mit _static_ erfolgen. Dies ist oft nützlich. So könnte man beispielsweise bei einem Online-Shop zählen, wie viele unterschiedliche Waren in den Warenkorb gelegt worden sind. Man müsste hierzu nur eine Funktion haben, die beim ersten Mal "0" ist und dann mit jeder Ware im Warenkorb hochgezählt wird.

```
function multipleRuns()
{
    static $a = 0;
    echo $a;
    $a++;
}
```

---

  
**Verwendung von _global_**  
Variablen haben in PHP grundsätzlich einen **lokalen Gültigkeitsbereich**. Also: alle Variablen innerhalb einer Funktion können nur in der Funktion selbst genutzt werden und alle Variablen außerhalb einer Funktion sind in der Funktion wiederum nicht nutzbar.

Somit gilt: eine Variable `$name`kann innerhalb einer Funktion stehen und vielleicht gibt es auch eine Variable _$name_ außerhalb der Funktion. So etwas findet man sehr oft und es muss klar sein, dass dies zwei verschiedene Variablen sind.

Mit dem Schlüsselwort _global_ können Variablen auch im globalen Scope genutzt werden - dies ist aber absolut nicht zu empfehlen (fehleranfällig und unprofessionell)! Stattdessen sollten alle Werte von außen nur als Parameter an eine Funktion übergeben werden.

---


**Verwendung von Referenzen**  
Man kann _function `add(&$x, &$y)`_ schreiben und dann werden an die Variable nicht die Werte, sondern Referenzen übergeben. Hierauf wollen wir nicht weiter eingehen, da es nicht nur unschön aussieht, sondern auch zu unerwartetem Verhalten führen kann (fehleranfällig) und somit vermieden werden sollte.


# 2 Standard-Werte für Unterprogramme

In PHP können Parameter einer Funktion mit Standardparametern versehen werden, was erlaubt, dass diese Parameter beim späteren Funktionsaufruf nicht übergeben werden müssen. Sehen Sie sich die **Zeilen 1, 8 & 12** an.

Code

```php
function writeUni($name, $uni, $zip, $city = "Emden")
{
    echo "$name ist an der $uni, $zip, $city.<br>";
}
echo "vollständige Übergabe:<br>";
// Vier Werte werden nun übergeben
writeUni("Bernd", "HS EL", "26723", "Emden"); 
echo "<br>teilweise Übergabe:<br>";
// Gut, wenn es einen Standardparameter gibt (hier: "Emden")
writeUni("Bernd", "HS EL", "26723");
```

Ausgabe:  
_vollständige Übergabe:_  
_Bernd ist an der HS EL, 26723, Emden._  

_teilweise Übergabe:_  
_Bernd ist an der HS EL, 26723, Emden._

---

  
**Nutzung mehrerer Standardparameter**  
Es ist auch möglich mehrere Standardparameter anzugeben. Die Standardparameter müssen immer am Ende der Parameterliste in der Funktion stehen und die Abarbeitung erfolgt in der Reihenfolge der Nennung.

```php
function writeUni($name, $uni = "HS EL", $zip = "26723", $city = "Emden")
{
    echo "$name ist an der $uni, $zip, $city.<br>";
}
echo "vollständige Übergabe:<br>";
// Vier Werte werden nun übergeben
writeUni("Bernd", "HS EL", "26723", "Emden"); 
echo "<br>teilweise Übergabe:<br>";
// Nutzung aller Standardparameter 
writeUni("Bernd");
```

Ausgabe:  
_vollständige Übergabe:_  
_Bernd ist an der HS EL, 26723, Emden._  

_teilweise Übergabe:_  
_Bernd ist an der HS EL, 26723, Emden._

Es ist aber nicht möglich, im Funktionsaufruf nur den Namen und den Ort anzugeben _writeUni("Bernd", "Leer");_ und auf die "mittleren" Standardparameter zuzugreifen, da die Übergabe genau in der Reihenfolge des Aufrufs erfolgt.


---
  
**Praxisbeispiel**  
Die Nutzung von Standardparametern bietet sich beispielsweise an, wenn die Funktion mit einer unterschiedlichen Anzahl von Werten aus einem HTML-Formular arbeiten soll.

Aufgabe

Schreiben Sie eine Funktion, die ein Formularfeld erzeugt. Als Standard soll das Formularfeld eine Länge von 15 Zeichen haben.

`echo "<input type=\"text\" name=\"$name\" size=\"$size\" id=\"$name\">";
`
Rufen Sie das Formularfeld aus dem Hauptprogramm auf und erstellen Sie somit ein Formular mit den Feldern _Name_, _Vorname_, _Straße_, _PLZ_, _Ort_. Das Formularfeld PLZ soll eine size=5 haben. Alle anderen Felder sollen den Default 15 nutzen.


```php
<?php
// Funktion zur Erzeugung eines Textformularfeldes mit Standardgröße 15
function createInputField(string $name, int $size = 15) {
    echo "<label for=\"$name\">$name:</label> ";
    echo "<input type=\"text\" name=\"$name\" size=\"$size\" id=\"$name\"><br><br>";
}
?>

<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Formular mit Standardparametern</title>
</head>
<body>

<form method="post" action="">
    <?php
    createInputField("Name");
    createInputField("Vorname");
    createInputField("Straße");
    createInputField("PLZ", 5);  // Spezielle Größe
    createInputField("Ort");
    ?>
    <input type="submit" value="Absenden">
</form>

</body>
</html>
```


# 3 Funktionsaufrufe innerhalb einer Funktion

Wir verwenden jetzt zwei Funktionen, und die erste Funktion ruft die zweite Funktion auf (siehe **Zeile 4**).


```php
function writeStudent($name, $uni, $zip, $city)
{ 
    echo "$name ist an der ";
    writeUni($uni, $zip, $city);
}

function writeUni($uni, $zip, $city)
{
    echo "$uni, $zip, $city.<br>";
}

writeStudent("Ute", "HS EL", "26723", "Emden");
```

Ausgabe:  
_Ute ist an der HS EL, 26723, Emden._  

  
**Rekursion**  
Eine Funktion kann sich auch selbst aufrufen. Wenn wir dies mit der Funktion _writeStudent_ machen, dann haben wir eine wunderschöne Endlosschleife, da keine der aufgerufenen Funktionen jemals ans Funktionsende kommt. Aber irgendwann wird die Ausführung vom PHP-Modul mit einer Fehlermeldung unterbrochen.

```php
function writeStudent($name)
{ 
    echo "$name";
    writeStudent($name)
}

writeStudent("Ute");
```

  
Rekursion kann aber sinnvoll sein. Jedoch sollte immer eine Abbruchbedinung eingebaut werden. Hier ein Beispiel:

```
function add($x)
{ 
    echo "x startet mit: $x <br>";
    if ($x === 0) {
      return 0;
    }
    $result = add($x - 1) + $x;
    echo "x ist nun $x <br>";
    return $result;
}
$total = add(5); 
echo "<br>Das Gesamtergebnis ist $total";
```

Ausgabe:  
_x startet mit: 5_  
_x startet mit: 4_  
_x startet mit: 3_  
_x startet mit: 2_  
_x startet mit: 1_  
_x startet mit: 0_  
_x ist nun 1_  
_x ist nun 2_  
_x ist nun 3_  
_x ist nun 4_  
_x ist nun 5_  
  
_Das Gesamtergebnis ist 15_


Wenn Ihnen es nicht auf Anhieb klar ist (weil Sie Rekursion schon mehrfach in anderen Programmierprachen angewendet haben), dann nehmen Sie sich JETZT Zeit und ein Blatt Papier und versuchen Sie unbedingt zu verstehen, warum die Ausgabe der Zeilen genau in dieser Reihenfolge passiert und wie das Programm zum _Gesamtergebnis 15_ kommt.  
  
Auch müssen Sie erklären können, was das return in **Zeile 5** macht und was das return in **Zeile 9** macht.


# 4 Fehlerbehandlung in PHP

In PHP gibt es sogenannte [**Magische Konstanten**](http://php.net/manual/de/language.constants.predefined.php). Die Magischen Konstanten __FILE__ und __LINE__ können beim Erkennen und Lokalisieren von Fehlern helfen.

```php
function report_error($file, $line, $message)
{
    echo "Fehler in $file in Zeile $line aufgetreten: $message";
}
report_error( __FILE__ , __LINE__ , "Irgendwas funktioniert nicht.");
```

  
**Exceptionhandling**  
Fehler können mit einem _try_-Block, abgefangen werden. Hierzu ist der Code, in dem ein Fehler auftreten könnte, in den Block hineinzuschreiben. Falls nun ein Fehler auftritt, wird ein Objekt durch die Anweisung _throw_ erzeugt. Bei einem Fehler wird der Code im _catch_-Block ausgeführt.

Wenn man verschiedene Arten von Fehlern behandeln will, sollte man mit mehreren Fehlerklassen arbeiten, die aus der Fehlerklasse _Exception_ abgeleitet werden.


```php
function division($numerator, $denominator)  
// numerator = Zähler, denominator = Nenner
{
    if ($denominator == 0) {
      throw new Exception("Es kann nicht durch 0 dividiert werden!");
    }    
    $result = $numerator/$denominator;
    return $result;
}
try {
    echo division(5, 0);
}
catch (Exception $error) {
    echo "Fehler: ".$error->getMessage();
}
```

- `catch (Exception $error)`: Fängt eine Ausnahme ab und speichert sie in der Variablen `$error`.
- `$error->getMessage()`: Gibt den Text der Fehlermeldung zurück,

  
PHP ermöglicht Ihnen den Austausch der gesamten Fehlerbehandlung durch die Funktionen [set_error_handler](http://php.net/manual/de/function.set-error-handler.php) und [set_exception_handler](http://php.net/manual/de/function.set-exception-handler.php). So können Sie Fehler auf der Seite unterdrücken, aber im Hintergrund alles mitschreiben und darauf reagieren.



# 5 Beispiel Formulare - Daten einlesen

Das eben Erlernte soll nun an einem praxisnahen Beispiel erklärt werden. Das hier gezeigte Beispiel wird in den nächsten Unterkapiteln erweitert.

Zunächst muss über _echo_-Befehle ein HTML-Formular erstellt werden. Dieses Formular wird auf dem Webbrowser angezeigt und kann vom Nutzer ausgefüllt werden. Beim Klick auf den Button "Formular abschicken" werden die Daten aus dem Formular an den Webserver geschickt.

```php
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
?>
```


Screenshot des erzeugten Formulars

![](images/Pasted%20image%2020250419193759.png)

Das Hauptprogramm besteht nur aus Funktionsaufrufen.
- **Zeile 8:** Die Funktion _writeHeaderAndHeadline()_ erstellt den HTML-Header und einen ersten Teil des HTML-Body mit einer Überschrift.
- **Zeile 18:** Die Funktion _startForm()_ erstellt den Beginn des eigentlichen HTML-Formulars. Übergeben werden die Parameter für die HTTP-Methode und die URL bzw. Datei, an die die Formulardaten geschickt werden. In **Zeile 41** erfolgt der Funktionsaufruf mit den Parametern _"post"_ und _"formular2.php"_.
- **Zeile 23:** Die Funktion _writeInputField()_ erzeugt ein Eingabefeld zur Dateneingabe. Die Funktion wird zweimal aufgerufen **Zeile 42 & 43** und somit werden zwei Eingabefelder erzeugt.
- **Zeile 31:** Abschließend wird in der Funktion _closeFormAndFooter()_ der Absendebutton erstellt und das Formular geschlossen. Anschließend werden der HTML-Body und das gesamte HTML-Dokument geschlossen.


Die Daten werden also an die Datei _formular2.php_ geschickt und sind dort im assoziativen Array _$_POST_ gespeichert.

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
?>
```


![](images/Pasted%20image%2020250419194022.png)


Das eigentliche Einlesen der Daten erledigt der Webserver, genauer gesagt das PHP-Modul im Webserver. Daher befinden die Daten bereits in dem Array `$_POST`. Durch `print_r()` geben wir diese hier vorformatiert zum Testen aus.
  
Zur nochmaligen Veranschaulichung, wie der Client, der Server, sowie HTTP und PHP zusammenarbeiten, sehen Sie nachfolgend eine Grafik:


![](images/Pasted%20image%2020250419194029.png)


Im ersten Schritt stellt der Client die Anforderung an den Webserver, dass er die Seite `seite.php` haben möchte. Der Webserver übergibt die Anforderung an PHP, welches dann die Seite ausführt und die gewünschte HTML-Seite wieder an den Webserver übergibt. Der Webserver liefert dann die erzeugte HTML-Seite an den Client zurück. Der Client kann dann die eben erzeugte Seite `seite.php` darstellen.



