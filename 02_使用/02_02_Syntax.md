
**Generelle Syntax-Regeln**  
- Sonderzeichen sind: . \ + *  ? ^ $ [ ] ( ) { } &'
- Strings mit Variablenauswertung werden eingeschlossen in "…"
- Strings ohne Variablenauswertung werden eingeschlossen in '…'
- Variablen sind case sensitive
- Auch Indizes in Arrays sind case sensitive: _$Array['index'] != $Array['Index']_
- Vordefinierte Funktionen, Funktionsnamen und Klassennamen sind nicht case sensitive. Dies kommt historisch aus der Einbindung von PHP in HTML.


Als einfaches Einbindungs-Beispiel für PHP-Code in HTML ein Hello-World:

<?php echo "Hello world"; ?>


# 1 Ausgabe von Text (Sting Interpolation)

_echo_ ist der meistgenutzte Ausgabebefehl in PHP. Auch _print_ (analog zu _echo_) und _printf_ (formatierte Ausgabe) sind möglich.

Die Ausgabe von Text ist eine ganz zentrale Funktionalität in PHP-Anwendungen. Der Browser kann PHP nicht interpretieren, sondern es wird HTML zum Browser geschickt und diese HTML-Elemente werden im PHP-Script durch entsprechende Textausgaben erstellt. PHP-Programme erstellen also über _echo_-Befehle das HTML-Dokument.


1 **Unterschiedliche Anführungszeichen**  
Der _echo_-Befehl kann mit einfachen Anführungszeichen und doppelten Anführungszeichen verwendet werden.

```
$variable = "Test";
echo "Gib die Variable $variable aus";  //Ausgabe: Gib die Variable Test aus

echo 'Gib das Wort $variable aus';      //Ausgabe: Gib das Wort $variable aus
```


Fehlerhafte _echo_-Befehle kommen sehr häufig vor. Daher ist es wichtig, dass Sie einen Editor benutzen, der Sie visuell unterstützt. Beim [Editoren ''Atom''](https://isp.eduloop.de/mediawiki/index.php?title=Editoren_%27%27Atom%27%27&action=edit&redlink=1 "Editoren ''Atom'' (Seite nicht vorhanden)") können Sie anhand der Farben sehr einfach erkennen, ob im _echo_-Befehl _$variable_ als Variable oder als Wort verwendet wird.

![](images/Pasted%20image%2020250419181245.png)

Häufig wird auch die folgende Variante benutzt, da sie das Erkennen von Variablen erleichtert und es ermögicht, dass man Variablen ohne Leerzeichen hintereinander schreiben kann:

`echo "Gib zweimal die Variable {$variable}{$variable} aus";`




2 **Teilabschnitte im _echo_-Befehl**  
Durch die Möglichkeit, entweder einfache Anführungszeichen oder doppelte Anführungszeichen zu verwenden, sowie durch die Möglichkeit, zur Verbindung von Teilstrings einen Punkt oder ein Komma zu verwenden, ergeben sich viele mögliche Varianten. Nachfolgend ein paar Beispiele, wie Sie echo verwenden können.

```php
$velocity = 3;
echo "Mein Ergebnis lautet: ", $velocity, " km/h";
echo "Mein Ergebnis lautet: " . $velocity . " km/h";
echo "Mein Ergebnis lautet: $velocity km/h";
echo 'Mein Ergebnis lautet: ', $velocity, ' km/h';
echo 'Mein Ergebnis lautet: ' . $velocity . ' km/h';
```
Schauen Sie sich die Möglichkeiten sehr genau an! Alle Zeilen geben den identischen String aus: _Mein Ergebnis lautet: 3 km/h_.

  
Auch eine Verschachtelung ist möglich. Diese wird beispielsweise genutzt, wenn Sie HTML-Code mit PHP ausgeben möchten:
```php
echo '<input type="text" name="', $name, '">';
echo "<input type=\"text\" name=\"$name\">";
```

Beide Zeilen geben den identischen String aus.
```php
Finden Sie den Fehler! Die folgende Zeile PHP-Code ist fehlerhaft:

echo '<img alt="Picture" src=" . $path . " title="Title">';
```
Beim src-Attribut fehlen einfache Anführungszeichen, ansonsten wird der Variablenname, nicht der Variableninhalt ausgegeben. Richtig muss es wie folgt sein:

`echo '<img alt="Picture" src="' . $path . '" title="Title">';`

Beim _src_-Attribut fehlen einfache Anführungszeichen, ansonsten wird der Variablenname, nicht der Variableninhalt ausgegeben. Richtig muss es wie folgt sein:

`echo '<img alt="Picture" src="' . $path . '" title="Title">';`





3 **Zahlen formatiert ausgeben mit printf()**  
Mithilfe dieser Funktion kann über einen Formatierungs-String eine Zeichenkette gebildet und ausgegeben werden. Somit lässt sich z.B. eine Uhrzeit mit Nullen auffüllen:

`printf("%02d:%02d:%02d", $hour, $minute, $second);`
Ausgabe:  
_09:08:24_

Dabei leitet das Prozent-Zeichen jeweils eine neue Formatierungs-Anweisung ein. Die Null deklariert in diesem Fall ein Füllzeichen. Das heißt der String soll mit Nullen gefüllt werden und zwar bis auf zwei Zeichen lang. Das kleine „d“ besagt, dass es sich bei dem angegeben Wert um einen vorzeichenbehafteten Dezimalwert handelt. Die Doppelpunkte werden nicht interpretiert und unbehandelt ausgegeben.

Mehr Möglichkeiten zur Formatierung finden Sie auf der PHP-Seite: _[printf()](http://php.net/manual/de/function.printf.php)_.


# 2 Konstanten

Die Verwendung von Konstanten bietet den Vorteil, dass der Wert nicht irgendwo im Programm geändert werden kann. Konstanten sollten im Programmkopf oder in einer _.ini.php_-Datei gesetzt werden, beispielsweise in einer Datei _config.ini.php_ oder _const.ini.php_, die über _require_once()_ eingebunden wird.

- Konstanten werden gemäß den [Namenskonventionen](https://isp.eduloop.de/loop/Namenskonventionen "Namenskonventionen") in Großbuchstaben geschrieben. Verwendet werden Konstanten wie Variablen jedoch ohne das _$_-Zeichen.
- Mit der Funktion _defined()_ kann man überprüfen, ob eine Konstante bereits gesetzt ist.  

---

**Verwendung von _const_**  
```
const AUTOR = "Thomaschewski";
echo "Ausgabe der Konstanten: ", AUTOR, "<br>";
if (defined('AUTOR')) {
    echo "Die Konstante AUTOR ist gesetzt.";
}
```
Ausgabe:  
_Ausgabe der Konstanten: Thomaschewski_  
_Die Konstante AUTOR ist gesetzt._


---

**Verwendung von _define()_**  
Dies ist die ältere Schreibweise, bei der eine Konstante über die PHP-Funktion _define()_ gesetzt und über _constant()_ ausgegeben wurde.

```
define('AUTOR', "Thomaschewski");
echo "Ausgabe mittels Funktion constant(): ", constant('AUTOR'), "<br>";
if (defined('AUTOR')) {
    echo "Die Konstante AUTOR ist gesetzt.";
}
```
Ausgabe:  
_Ausgabe mittels Funktion constant(): Thomaschewski_  
_Die Konstante AUTOR ist gesetzt._

Hinweis
Bei größeren Projekten sollten alle Konstanten in einer eigenen (Konfigurations-)Datei stehen, da so das Anpassen der Software deutlich vereinfacht wird.


---


**Magische Konstanten**Es gibt in PHP auch Konstanten, die direkt vom PHP-Modul gefüllt und im Sourcecode genutzt werden können.

|Magische Konstante|Beschreibung|
|---|---|
|**__LINE__**|**Aktuelle Zeile**  <br>Beinhaltet die aktuelle Zeilennummer, in der **__LINE__** verwendet wird.|
|**__FILE__**|**Aktuelle Datei**  <br>Beinhaltet den Dateinamen, in dem **__FILE__** verwendet wird.|
|**__DIR__**|**Aktuelles Verzeichnis**  <br>Beinhaltet das aktuelle Verzeichnis, in dem die Datei liegt, in der **__DIR__** verwendet wird.|
|**__FUNCTION__**|**Aktuelle Funktion**  <br>Beinhaltet die aktuelle Funktion, in der **__FUNCTION__** verwendet wird.|
|**__METHOD__**|**Aktuelle Methode**  <br>Beinhaltet die aktuelle Methode, in der **__METHOD__** verwendet wird.|
|**__CLASS__**|**Aktuelle Klasse**  <br>Beinhaltet die aktuelle Klasse, in der **__CLASS__** verwendet wird.|
|**__TRAIT__**|**Aktuelles Trait**  <br>Beinhaltet das aktuelle Trait, in der **__TRAIT__** verwendet wird.|
|**__NAMESPACE__**|**Aktueller Namensraum**  <br>Beinhaltet den aktuellen Namensraum, in dem **__NAMESPACE__** verwendet wird.|

# 3 Vordefinierte Variablen

In PHP gibt es einige sogenannte [Superglobals](https://www.php.net/manual/de/language.variables.superglobals.php). Dies sind vordefinierte assoziative Arrays, die überall im Sourcecode verfügbar sind.

Nachfolgend sollen einige dieser Variablen-Typen kurz erklärt werden. Es gibt jedoch noch weitere Variablen, die auf der PHP-Seite erläutert werden: [Vordefinierte Variablen](http://php.net/manual/de/reserved.variables.php).

`**$_GET, $_POST**  `
In diesen Arrays werden die per GET oder POST vom Client übermittelten Daten bereitgestellt. Wird zum Beispiel die folgende URL aufgerufen:  
_http://iprog-modul.de/index.php?autor=Thomaschewski_, so kann man den Wert _Thomaschewski_ über die Variable _$_GET["autor"]_ abrufen. Gleiches gilt für per POST-Methode übergebene Daten.

`**$_COOKIE**  `
In diesem Array befinden sich die Daten, die mittels eines Cookies vom Client an den Server übermittelt wurden. Sie können Cookies mit _setcookie()_ erstellen, um sie eventuell später wieder über das Array abzurufen.

`**$_REQUEST**  `
Dieses Array enthält standardmäßig den gesamten Inhalt aus den Arrays _$_GET, $_POST und $_COOKIE_.

`**$_SESSION**  `
Dieses Array enthält die Sessionvariablen. Sie können innerhalb einer Session beliebig Daten in dieses Array schreiben und wieder auslesen. Dabei ist jedoch die Verwendung der Funktion _session_start()_ zu Beginn des Skripts erforderlich, sofern dies nicht automatisch geschieht.

`**$GLOBALS**  `
Beinhaltet alle Variablen, die im globalen Gültigkeitsbereich vorhanden sind.

`**$_SERVER**  `
In diesem Array sind Informationen aus dem HTTP-Header, der Apache-Konfiguration und einige Server-Verzeichnisse enthalten. Auf der [PHP-Seite](http://php.net/manual/de/reserved.variables.server.php) sind alle Array-Einträge aufgelistet, die jedoch nicht von allen Webservern unterstützt und befüllt werden. Ein Beispiel für `$_SERVER`: Mit _`$_SERVER["REMOTE_ADDR"]`_ kann die aktuelle IP-Adresse des Clients abgerufen werden.

```php
<?php

echo "<pre>";
print_r($_SERVER);
echo "</pre>";

?>
```

`echo "<pre>"` and `echo "</pre>"` wrap the output in `<pre>` tags so that it displays in **preformatted (monospaced)** style in the browser — preserving indentation and line breaks.


# 4 Funktionen empty() und isset()

|Funktion|Beschreibung|
|---|---|
|[empty()](https://www.php.net/manual/de/function.empty.php)]|Prüft, ob eine Variable einen Wert enthält|
|[isset()](https://www.php.net/manual/de/function.isset.php)|Prüft, ob eine Variable existiert und ob sie nicht NULL ist|

## 4.1 empty()
Oft ist es notwendig abzufragen, ob schon Daten über GET oder POST übermittelt wurden.

Betrachten wir eine Internetseite, die ein Formular enthält. So wird beim ersten Aufruf der URL zunächst einmal mittels PHP-Programm das Formular selbst erstellt und im Browser angezeigt, aber es werden noch keine Daten aus dem Formular übermittelt.

Anschließend kann das Formular vom Nutzer ausgefüllt und abgeschickt werden, sodass beim erneuten Aufruf des PHP-Programms Formulardaten via GET oder POST übermittelt wurden. Es wird also dasselbe PHP-Programm aufgerufen, aber je nachdem, ob schon Daten übermittelt wurden oder nicht, reagiert es anders.

Somit überprüfen wir mit _empty()_, ob `_$_GET` sbzw. _`$_POST`_ leer sind.


```php
if (empty($_POST)) {
    // erzeuge das leere Formular
} else {
    // verarbeite die aus dem Formular übertragenen Daten
}
```

Häufig ist es besser, wenn die Logik umgedreht wird und man prüft, ob etwas gefüllt ist. Hierzu kann die Negation _"!"_ in der if-Bedingung verwendet werden.

```php
if (!empty($_POST)) {
    // verarbeite die aus dem Formular übertragenen Daten
} else {
    // erzeuge das leere Formular
}
```

Im Beispiel wurde abgefragt, ob $_POST Werte der Variablen enthält. Genauso kann man eine spezifische Variable aus dem [assoziativen](https://isp.eduloop.de/loop/Assoziative_Arrays "Assoziative Arrays") $_POST-Array abfragen. Stellen wir uns vor, wir hätten ein Formular mit dem Formularfeld` <input type="text" name="prename">`.  
Dann könnten man mit `if (empty($_POST["prename"]))` abfragen, ob das Formularfeld ausgefüllt wurde.

Achtung: PHP ist eine ["schwach typisierte Sprache"](https://de.wikipedia.org/wiki/Typisierung_\(Informatik\)). 
==Überprüft man `$name = "0"` , dann wird dies als "empty" gewertet und in der if-Bedingung wird `$name` ist leer ausgegeben.==
==Überprüft man `$name = "1"` , dann wird dies als "nicht empty" gewertet und in der if-Bedingung wird `$name` ist nicht leer ausgegeben.==


```
$name = "0";
if (empty($name)) {
    echo '$name ist leer';
} else {
    echo '$name ist nicht leer';
}
```


---

Erstellen Sie ein einfaches Formular und füllen Sie in die Formularfelder jeweils "0" und schicken Sie das Formular ab.

a) Überlegen Sie sich, ob dann `$_POST` (bzw. `$_GET`) ebenfalls als "leer" angesehen werden.  
zu a) POST bzw. GET sind nur deshalb für die empty-Funktion nicht leer, da auch der Absende-Button mit einem Variablennamen und einem Wert übergeben werden.  

在 PHP 中，`$_POST` 和 `$_GET` 是 **数组**，它们只要有键值对（哪怕值是 `"0"`），它们就**不是空的**。
但是，`empty($_POST['fieldname'])` 会返回 `true`，**因为 `empty("0")` 是 `true`**！

form_test.php
```php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>POST Test</title>
</head>
<body>
    <form method="post" action="">
        <label for="a">Enter something:</label>
        <input type="text" name="a" id="a" value="0">
        <button type="submit" name="submit" value="Send">Submit</button>
    </form>

    <pre>
<?php
if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    echo "var_dump(\$_POST):\n";
    var_dump($_POST);

    echo "\n\nempty(\$_POST): ";
    var_dump(empty($_POST)); // false – array is not empty

    echo "empty(\$_POST['a']): ";
    var_dump(empty($_POST['a'])); // true – because "0" is considered empty
}
?>
    </pre>
</body>
</html>
```


---


b) Wie können Sie (unabhängig von PHP) ermitteln, ob in POST bzw. GET Daten vorhanden sind.
zu b) Was genau in POST bzw. GET übertragen wird, können Sie immer mit der Firefox Netzwerkanalyse erkennen.
你可以使用 **浏览器开发者工具的「网络(Network) 面板」** 来分析请求：
方法（以 Firefox / Chrome 为例）：

1. 打开网页，按 `F12` 打开开发者工具。
    
2. 切换到 **Network / Netzwerkanalyse** 面板。
    
3. 提交表单后，会看到请求（通常是 `POST` 或 `GET` 类型）。
    
4. 点击该请求 → 查看 **Payload**（对于 POST 请求） 或 **URL 参数**（对于 GET）。
    
5. 你就能看到提交的数据是否真的存在（即使是 `"0"`）以及 key/value 值。

## 4.2 **isset()**
Während _empty()_ überprüft, ob eine Variable einen Wert enthält, wird mit _isset()_ überprüft, ob eine Variable überhaupt existiert.


# 5 Einbetten von Programmteilen

Zum Einbinden von PHP-Teilen verwendet man _include_ oder _require_.
- Die Dateiendung _.inc.php_ entspricht den Konventionen und verdeutlicht, dass diese Datei nicht für sich ausgeführt werden soll.
- Das Einbinden von Klassen kann man daran erkennen, dass die Klassennamen mit einem Großbuchstaben anfangen.

Natürlich ist es auch möglich, Dateien einzubinden, deren Dateiname nicht auf _.php_ endet, beispielsweise eine Datei _footer.inc_. Dies ist aber gefährlich, da nun die Datei _footer.inc_ direkt im Browser aufgerufen werden kann und ein potentieller Angreifer somit direkt auf den PHP-Sourcecode in der Datei _footer.inc_ zugreifen kann. Der Dateiname sollte also IMMER auf _.php_ enden.

|Funktion|Erklärung|
|---|---|
|[include](http://php.net/manual/de/function.include.php)|Liest eine Datei ein und wertet diese aus. Es wird eine Warnung ausgegeben, wenn die Datei nicht eingelesen werden kann.|
|[require](http://php.net/manual/de/function.require.php)|Liest eine Datei ein. Das Programm wird abgebrochen, wenn die Datei nicht eingelesen werden kann (Fatal Error).|
|[include_once](http://php.net/manual/de/function.include-once.php) bzw. [require_once](http://php.net/manual/de/function.require-once.php)|Einmal eingebundener Code wird nicht nochmals eingeb|

Anstelle von _include 'pfad/dateiname.inc.php'_ können auch Klammern _include('pfad/dateiname.inc.php')_ verwendet werden. Dies ist jedoch eine ältere Schreibweise und kommt aus einer Zeit, in der _include_, _require_ sowie _include_once_ und _require_once_ als PHP-Funktionen betrachtet wurden.


```
include_once '../inc/footer.inc.php';
require '../class/HtmlInput.php';
```
- Steht _include_ innerhalb einer Funktion, so gilt der gesamte eingebundene Code auch nur im Inneren dieser Funktion.
- Typischerweise verwendet man _require_once_ zum Einbinden von Klassen und _include_ für Programmteile, die nicht unbedingt im Programmablauf benötigt werden.


**Profitipp**: systemunabhängig funktioniert folgende Syntax.

```
$incPath   = __DIR__.DIRECTORY_SEPARATOR.'inc'.DIRECTORY_SEPARATOR;
$classPath = __DIR__.DIRECTORY_SEPARATOR.'class'.DIRECTORY_SEPARATOR;
require_once $incPath.'footer.inc.php';
require_once $classPath.'HtmlInput.php';
```


## 5.1 例子 

```
your-project/
│
├── index.php  ← this file
├── inc/
│   └── footer.inc.php
└── class/
    └── HtmlInput.php
```

 `class/HtmlInput.php`
 - Defines a class `HtmlInput` with static methods to generate `<input>` elements.
- Ensures safe HTML output using `htmlspecialchars()`.
```php
<?php

class HtmlInput {
    public static function text($name, $value = '', $placeholder = '') {
        return "<input type='text' name='" . htmlspecialchars($name) . 
               "' value='" . htmlspecialchars($value) . 
               "' placeholder='" . htmlspecialchars($placeholder) . "'>";
    }

    public static function submit($label = 'Submit') {
        return "<input type='submit' value='" . htmlspecialchars($label) . "'>";
    }
}
```


`inc/footer.inc.php`
- Outputs a simple footer with the current year.
- Included automatically at the end of your main PHP page.
```php
<?php

echo "<footer style='margin-top: 20px; font-size: 0.9em; color: #555;'>";
echo "&copy; " . date('Y') . " My Simple PHP App";
echo "</footer>";
```


index.php
```php
<?php
$incPath   = __DIR__ . DIRECTORY_SEPARATOR . 'inc' . DIRECTORY_SEPARATOR;
$classPath = __DIR__ . DIRECTORY_SEPARATOR . 'class' . DIRECTORY_SEPARATOR;

require_once $classPath . 'HtmlInput.php';
?>

<!DOCTYPE html>
<html>
<head>
    <title>Simple PHP Form</title>
</head>
<body>
    <h2>Example Form</h2>
    <form method="post">
        <?php 
            echo HtmlInput::text('username', '', 'Enter your username');
            echo HtmlInput::submit('Login');
        ?>
    </form>

    <?php
        if ($_POST) {
            echo "<p>Submitted username: <strong>" . htmlspecialchars($_POST['username'] ?? '') . "</strong></p>";
        }

        require_once $incPath . 'footer.inc.php';
    ?>
</body>
</html>
```

- Defines a class `HtmlInput` with static methods to generate `<input>` elements.
- Ensures safe HTML output using `htmlspecialchars()`.

---

# 6 without closing `?>`

In PHP, the closing `?>` tag at the end of a file is **optional**, and in many modern PHP practices, it’s actually **recommended to leave it out** — especially in **pure PHP files** (like configuration or class files).

Omit the closing `?>` in **pure PHP-only files** (especially in:
- config files
- class files
- any file where you're not directly outputting HTML)

This ensures **clean output**, prevents hard-to-debug header issues, and is considered good style by most PHP developers.
Let me know if you'd like a small demo of this issue in action!


**Why omit the `?>` tag?**
- Avoids accidental **whitespace or newline output**, which could break header redirects or session handling.
- Makes the codebase cleaner and reduces the risk of “Headers already sent” errors.

---


Here’s your example, written **without** the closing tag:

```php
<?php

echo "<footer style='margin-top: 20px; font-size: 0.9em; color: #555;'>";
echo "&copy; " . date('Y') . " My Simple PHP App";
echo "</footer>";
```


---

If you include the closing ?> and accidentally have a space or a new line after it, like this:
```php
<?php
// Some PHP logic
?>
 
<!-- This is an unintended whitespace -->
```

That tiny space or newline will be sent as **output to the browser**, which can cause issues **before your PHP script even starts sending headers** (like for `setcookie()`, `session_start()`, or `header()` redirects).


Example of what could go wrong:
```php
<?php
session_start();  // ⚠️ Warning: Cannot send session cache limiter - headers already sent
?>
```

If there's whitespace after `?>`, PHP thinks the response has already started, and **it won’t let you set headers anymore**.

# 7 Fehlerausgabe auf dem Browser

Wenn in der php.ini der Eintrag _display_errors_ On steht, werden Fehler im Browser ausgegeben. Mit dem Eintrag _error_reporting_ kann in der php.ini die Fehlerausgabe sehr detailliert eingestellt werden.

Oftmals ist es wichtig, die Anzahl der Fehlermeldungen einzuschränken.
```
<?php
error_reporting (-1);  //Fehler im Browser ausgeben
echo "Nachfolgende Zeile ist fehlerhaft <br>";
bla
?>
```

  
Folgende Einstellungen sind sinnvoll
- _error_reporting (-1)_ alle Fehler und Warnungen ausgeben
- _error_reporting (0)_ Fehlerausgabe abschalten  

Eine genauere Betrachtung ist in der [PHP-Dokumentation](http://php.net/manual/de/function.error-reporting.php) nachzulesen.

Mit _`ini_set('display_errors', true)`_ kann die Fehleranzeige eingeschaltet und mit _`ini_set('display_errors', false)`_ abgeschaltet werden. Jedoch können auf diese Weise keine Fehlermeldungen des Compilers durch das zu kompilierende Script abgeschaltet werden.

Mit `ini_get()` lassen sich übrigens alle Einstellungen ermitteln.

Beispiel:
`echo ini_get(error_reporting);`

Wenn Sie eine Einsendeaufgabe abgeben, dann schalten Sie bitte nur die _notice_-Meldungen ab. Sinnvoll hierfür ist `error_reporting(E_ALL & ~E_NOTICE);`


# 8 Debugging

Das Finden der Fehler wird als Debugging bezeichnet und kann auf verschiedene Arten erfolgen. Hier wollen wir eine einfache Art beschreiben. Eine sehr wichtige Einstellung für das Debugging erfolgt in der [Konfigurationsdatei php.ini](https://isp.eduloop.de/loop/Konfigurationsdatei_php.ini "Konfigurationsdatei php.ini") mit _display_errrors = On_, da nur dann Fehler, Warnungen und Hinweise in dem Browser ausgegeben werden.

Aber selbst wenn das PHP-Programm keine Fehler ausgibt, macht es vielleicht nicht, was es machen soll. So ist es oftmals notwendig, die Inhalte einer Variablen oder eines Arrays zu ermitteln, um einen Fehler zu finden. Hier wird eine sehr einfache, hilfreiche Art des Debuggings benötigt, beispielsweise um festzustellen, welche Daten per POST übermittelt wurden.

---

1 **Alle Daten eines Arrays ausgeben**  
Zur einfachen Ausgabe aller Informationen einer Variablen gibt es die Funktionen [var_dump](http://php.net/manual/de/function.var-dump.php) und [print_r()](http://php.net/manual/de/function.print-r.php). Sie sind bei der Entwicklung eines Programms eine sehr praktische Alternative zum Befehl _echo_ und liefern eine strukturierte Ausgabe eines Arrays.

```php
$cmyk = ["c" => "cyan", "m" => "magenta", "yk" => ["yellow", "key"]];

echo "Ausgabe mit print_r() <br>";
print_r($cmyk);
echo "<hr>";

echo "Ausgabe mit var_dump() <br>";
var_dump($cmyk);
echo "<hr>";

echo "Ausgabe mit einem pre-Element";
echo "<pre>";
print_r($cmyk);
echo "</pre>";
```

![](images/Pasted%20image%2020250419190809.png)


Sowohl `print_r()` sls auch `var_dump()` eignen sich, um eine schnelle Übersicht über Variableninhalte zu bekommen. Während die Funktion `print_r()` eine übersichtlichere Ausgabe des geschachtelten Arrays enthält, gibt `var_dump()` zusätzlich die Längen der Arrays und Strings aus. Für eine noch schönere und ausformatierte Ausgabe geschachtelter Arrays, empfiehlt sich die Nutzung von `<pre>-Elements`.


Wenn Sie PHP mit einem normalen Editor erstellen, dann ist es oftmals schwierig zu erkennen, ob aus einem Formular die Daten richtig an den Server übermittelt wurden. Hilfreich kann dann folgender Sourcecode sein, der auf jeder Seite eingebunden wird.

```
// Unter den Includes
$debug="ja";
session_start();
if ($debug==="ja") {
    error_reporting (-1);
    echo "POST/GET <br>";
    print_r($_REQUEST);        
    echo "<hr>";
    echo "SESSION <br>";
    print_r($_SESSION);  
} else {
    error_reporting (0);  
}
```

Die hier noch unbekannten PHP-Befehle werden auf den kommenden Seiten erläutert.


_print_r()_ und _var_dump()_ dürfen nur während der Entwicklung für das Debugging verwendet werden und sind in einem produktiven System abzuschalten. Also nie im produktiven Code verwenden!








