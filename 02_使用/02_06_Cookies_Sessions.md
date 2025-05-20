
Für das Setzen von Cookies gibt es die Funktion [setcookie](http://php.net/manual/de/function.setcookie.php) (_"Name", "Inhalt", Verfallsdatum, "Pfad", "Domain", secure_).

Diese Funktion sendet einen mit HTTP Header-Informationen zu übertragenden Cookie. Dies muss vor der Ausgabe des Scripts geschehen, also vor dem eigentlichen HTTP-Body.  
Schlägt `setcookie()` fehl, wird _false_ zurückgegeben, bei Erfolg _true_. Dies allerdings ist keine Aussage darüber, ob der User den Cookie akzeptiert hat oder nicht.

Als Beispiel wird hier wieder das Formular verwendet, welches nach einem Vor- und Nachnamen fragt.


```php
<?php
/**
 * Beispiel Formular - Cookies
 * @author Michael Gerbracht, Mirko Groenewold
 * @date 14.05.2019
 */

function writeHeaderAndHeadline()
{
    echo "<!DOCTYPE html>
          <html lang=\"de\">
          <head><title>Cookies</title>
          </head>
          <body>
          <h1>Beispiel Cookies</h1>";
}

function startForm($method, $url)
{
    echo "<form method=\"$method\" action=\"$url\">";
}

/**
 * Erstellt Textfelder für ein simples Formular, wobei Text = der
 * Text, der dem Benutzer angezeigt werden soll und Name = der Name
 * des Textfeldes
 */

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
startForm("post", "cookies2.php");
writeInputField("Vorname", "vorname");
writeInputField("Name",    "nachname");
closeFormAndFooter();
?>
```



Die Daten werden dabei nun an die zweite PHP-Datei _cookies2.php_ gesendet. Dieses Skript sendet die eingegebenen Daten als Cookie zurück an den Browser, wie in **Zeile 8 und 9** zusehen ist:

```php
<?php
/**
 * Beispiel Formular - Cookies
 * @author Michael Gerbracht, Mirko Groenewold
 * @date 14.05.2019
 */

 setcookie("vorname",  $_POST["vorname"]);
 setcookie("nachname", $_POST["nachname"]);

function writeHeaderAndHeadline()
{
    echo "<!DOCTYPE html>
          <html lang=\"de\">
          <head><title>Cookies</title>
          </head>
          <body>
          <h1>Beispiel Cookies</h1>";
}

function startForm($method, $url)
{
    echo "<form method=\"$method\" action=\"$url\">";
}

function closeFormAndFooter()
{
    echo "</form>
          </body></html>";
}


// Beginn des Hauptprogramms
writeHeaderAndHeadline();
startForm("post", "cookies3.php");
print("Die Daten wurden nun als Cookie an Ihren Browser übermittelt.
       Klicken Sie <a href='cookies3.php'>hier</a>,
       um die Daten anzuzeigen.\n");
closeFormAndFooter();
?>
```


Klickt der Besucher nun auf den Link zur dritten PHP-Datei _cookies3.php_, werden die Daten, sofern der Browser sie wieder mitsendet, von PHP ausgegeben. Somit sind die Daten über ein Cookie gesendet worden:

```php
<?php
/**
 * Beispiel Formular - Cookies
 * @author Michael Gerbracht, Mirko Groenewold
 * @date 14.05.2019
 */

function writeHeaderAndHeadline()
{
    echo "<!DOCTYPE html>
          <html lang=\"de\">
          <head><title>Cookies</title>
          </head>
          <body>
          <h1>Beispiel Cookies</h1>";
}

function makeOutput()
{
    echo "Ihr Browser lieferte folgende Daten <br />\r\n";
    echo "Vorname: " . $_COOKIE["vorname"] . "<br />\r\n";
    echo "Name: " . $_COOKIE["nachname"];
}


function closeFooter()
{
    echo "</body></html>";
}


// Beginn des Hauptprogramms
writeHeaderAndHeadline();
makeOutput("vorname", "nachname");
closeFooter();
?>
```

Die Prozedur kann beliebig oft wiederholt werden, da das Cookie im Browser immer wieder automatisch überschrieben wird.


# 1 Sessions

Die Verwendung von Sessions bietet sich immer dann an, wenn Daten über mehrere Webaufrufe hinweg transportiert werden müssen, beispielsweise um Formulardaten auch auf den nachfolgenden Seiten auswerten zu können oder damit die Login-Daten auf mehreren Seiten zur Verfügung stehen. Auf einer ersten Seite wird eine Session gestartet, die dann entsprechende Parameter an alle folgenden Seiten übergibt.  
  

|Funktion|Beschreibung|
|---|---|
|[session_start()](https://www.php.net/manual/de/function.session-start.php)|Initialisiert eine Session oder nimmt die aktuelle wieder auf (Funktion gibt immer _true_ zurück)|
|[session_destroy()](https://www.php.net/manual/de/function.session-destroy.php)|Logout – löscht also alle registrierten Daten|
|[session_name()](https://www.php.net/manual/de/function.session-name.php)|Liefert den Session-Namen|
|[session_id()](https://www.php.net/manual/de/function.session-id.php)|Setzt und liefert die aktuelle Session-ID|
|[session_encode()](https://www.php.net/manual/de/function.session-encode.php)|Kodiert die aktuellen Session-Daten als Zeichenkette|
|[session_decode()](https://www.php.net/manual/de/function.session-decode.php)|Dekodiert Session-Daten aus der Zeichenkette|

Das Zulassen von Sessions ohne Session-Cookies stellt ein Sicherheitsrisiko dar. URLs mit Session-ID können in Browsercaches gefunden und missbraucht werden.

Das Beispiel zeigt, wie mittels einer Session Informationen auf dem Server gespeichert und abgerufen werden können.

```php
<?php
    session_start();
    echo "Der letzte Reload war am: ";
    if (empty($_SESSION["zeit"])) {
        echo "Noch nie!";
    } else {
        echo date("d.m.Y H:i:s", $_SESSION["zeit"]) . " Uhr";
    }
    echo "<br />Warten Sie kurz und drücken Sie dann die F5-Taste!";
    $_SESSION["zeit"] = time();
?>
```


Bei dem ersten Aufruf ist noch kein Datum hinterlegt, weshalb der Text „Noch nie!“ angezeigt wird. Ausgabe:  
_Der letzte Reload war am: Noch nie!  
Warten Sie kurz und drücken Sie dann die F5-Taste!_

Erst nach einer Aktualisierung der Website erscheint das Datum. Ausgabe:  
_Der letzte Reload war am: 26.08.2019 17:52:34  
Warten Sie kurz und drücken Sie dann die F5-Taste!_


