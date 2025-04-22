

# 1 Übersicht String-Funktionen

Es gibt verschiedene Funktionen zur Bearbeitung eines Strings, hier ein paar Beispiele:

|Funktion|Erklärung|
|---|---|
|[strlen()](https://www.php.net/manual/de/function.strlen.php)|Ermittelt die Länge eines Strings|
|[trim()](https://php.net/manual/de/function.trim.php)|Entfernt Whitespaces am Anfang und Ende eines Strings|
|[rtrim()](http://php.net/manual/de/function.rtrim.php)|Auch _chop()._ Entfernt Leerraum am Ende eines Strings|
|[strtoupper()](https://php.net/manual/de/function.strtoupper.php)|Wandelt alle Zeichen des Strings in Großbuchstaben um|
|[strtolower()](https://php.net/manual/de/function.strtolower.php)|Wandelt alle Zeichen des Strings in Kleinbuchstaben um|
|[ucfirst()](https://php.net/manual/de/function.ucfirst.php)|Wandelt erstes Zeichen eines Strings in einen Großbuchstaben um|
|[ucwords()](https://php.net/manual/de/function.ucwords.php)|Wandelt jedes erste Zeichen eines Wortes in einen Großbuchstaben um|
|[strstr()](https://php.net/manual/de/function.strstr.php)|Findet erstes Vorkommen eines Strings innerhalb eines anderen Strings und gibt diesen ab dem Suchergebnis zurück|
|[strrev()](https://php.net/manual/de/function.strrev.php)|Gibt String in umgekehrter Reihenfolge zurück|
|[implode()](https://php.net/manual/de/function.implode.php)|Verbindet die Elemente eines Arrays zu einem String. Bei assoziativen Arrays werden nur die Werte (und nicht die Keys) verwendet.|
|[explode()](https://php.net/manual/de/function.explode.php)|Gegenteil zu _implode()_. Macht also aus einem String ein indiziertes Array.|

  
1 

```php
$stringExample = "Wir lernen PHP! ";
echo ucwords($stringExample), "<br>";
echo strtoupper($stringExample), "<br>";
echo strstr($stringExample, "n"), "<br>";
echo strrev($stringExample);
```

Ausgabe:  
_Wir Lernen PHP!_  
_WIR LERNEN PHP!_  
_nen PHP!_  
_!PHP nenrel riW_


2 
Beispiel für implode()
```php
$data = ["firstname", "lastname", "zip", "city"];
$stringData = implode(";", $data);
echo "$stringData <br>";
$color = ["r" => 127, "g" => 127, "b" => 255];
$stringColor = implode(", ", $color);
echo "$stringColor <br>";
```

Ausgabe:  
_firstname;lastname;zip;city_  
_127, 127, 255_

  
3 
Beispiel für explode()

```php
$stringData = "firstname;lastname;zip;city";
$data = explode(";", $stringData);
print_r($data);
```

Ausgabe:  
`_Array ( [0] => firstname [1] => lastname [2] => zip [3] => city )_`



# 2 Übersicht Array-Funktionen

|Funktion|Erklärung|
|---|---|
|[count()](http://php.net/manual/de/function.count.php)|Bestimmt die Anzahl der Elemente in einem Array|
|[next()](http://php.net/manual/de/function.next.php)|Rückt den Zeiger des Arrays auf das folgende Element|
|[prev()](http://php.net/manual/de/function.prev.php)|Rückt den Zeiger des Arrays auf das vorherige Element|
|[end()](http://php.net/manual/de/function.end.php)|Setzt den Zeiger des Arrays auf das letzte Element|
|[current()](http://php.net/manual/de/function.current.php)|Liefert das aktuelle Element eines Arrays|
|[key()](http://php.net/manual/de/function.key.php)|Liefert den Schlüssel eines assoziativen Arrays|
|[list()](http://php.net/manual/de/function.list.php)|Überträgt Elemente eines Arrays auf einzelne Variablen|

 Tab. 35: Weitere Array-Funktionen

  

|Funktion|Erklärung|
|---|---|
|[array_keys()](https://www.php.net/manual/de/function.array-keys.php)|Auslesen der Keys eines assoziativen Arrays. [Hier ein Beispiel](https://isp.eduloop.de/loop/Arrays_im_Array "Arrays im Array")|
|[array_pop()](https://www.php.net/manual/de/function.array-pop.php)|Liefert und löscht das letzte Element einen indizierten oder assoziativen Arrays [Hier ein Beispiel](https://isp.eduloop.de/loop/Foreach "Foreach")|
|[array_shift()](https://www.php.net/manual/de/function.array-shift.php)|Liefert und löscht das erste Element einen indizierten oder assoziativen Arrays|
|[array_unshift()](https://www.php.net/manual/de/function.array-unshift.php)|Fügt ein oder mehr Elemente am Anfang eines Arrays ein.|
|[array_slice()](https://www.php.net/manual/de/function.array-slice.php)|Extrahiert ein Teil-Array aus einem Array.|

1 

```
$cmyk = ["Cyan", "Magenta", "Yellow", "Key"];
echo "Elementanzahl: ", count($cmyk);
echo "<br>aktuelles Element: ", current($cmyk);
echo "<br>nächstes Element: ", next($cmyk);
echo "<br>letztes Element: ", end($cmyk);
```

Ausgabe:  
_Elementanzahl: 4_  
_aktuelles Element: Cyan_  
_nächstes Element: Magenta_  
_letztes Element: Key_  



2 

Beispiel für array_slice()

```
// Daten aus einer "Tabelle", nur die Ziffern in der 
// Mitte sollen "herausgeholt" werden
$data = [
    ['x', 'x', 1, 2, 3, 'x', 'x'],
    ['x', 'x', 4, 5, 6, 'x', 'x'],
    ['x', 'x', 7, 8, 9, 'x', 'x']
];
// Extraktion der Nutzdaten
foreach ($data as $row) {
    echo implode(", ", array_slice($row, 2, 3)) . "<br>";
}
```

Ausgabe:  
_1, 2, 3_  
_4, 5, 6_  
_7, 8, 9_  

Die Funktion` _array_slice(Arry, Offset, Anzahl)_` arbeitet mit drei Parametern. Zuerst wird das Array angegeben, dann wird angegeben, wie viele Elemente übersprungen werden sollen (= Offset) und als drittes wird die Anzahl der Elemente angegeben, die ausgelesen werden sollen.


# 3 Erzeugen von HTTP-Headern mit header()

[header()](http://php.net/manual/de/function.header.php) beschreibt das "Grundmodell" eines HTTP-Headers. Dabei muss die Ausgabe der Zeilen für den HTTP-Header natürlich **VOR der sonstigen HTML-Ausgabe** erfolgen.  

In diesem Beispiel wird ein Header erzeugt, der das Caching beeinflusst.

```php
header("Expires: Sun, 28 May 2000 10:00:00 GMT");
header("Last-Modified: ".date("D, d M Y H:i:s")."GMT");
header("Pragma: no-cache");
```



Häufig verwendete Header-Funktionalitäten sind _Location_, um einen Redirect zu erzeugen, oder _Content-Type_, um den Zeichensatz festzulegen.

```php
header("Location: http://www.medieninformatik-emden.de");
header("Content-Type: text/html; charset=utf-8");
```
Weitere HTTP-Headerinformationen können hier nachgelesen werden: [HTTP/1.1 Spezifikation](https://tools.ietf.org/html/rfc2616)

  
Beachten Sie bitte, dass einige Header beim Client zwischengespeichert werden können, es aber nicht müssen. Zum Beispiel speichern einige Browser den Statuscode 301 zwischen, viele tun dies jedoch nicht. Berücksichtigen Sie das bei der Programmierung, ersparen Sie sich viel Zeit bei der Suche nach dem Fehler.



# 4 Htmlspecialchars()


问题 
Eine der ersten Dinge, die Sie bei der Erstellung eines Formularfeldes unbedingt beachten müssen: **Ein Angreifer wird versuchen, ein Formularfeld als Sicherheitslücke auszunutzen**.

Angenommen, Sie haben ein Formularfeld mit PHP erstellt und möchten die übermittelten Daten dann weiter verarbeiten (auf einer Seite anzeigen oder in eine Datenbank speichern). Zum Anzeigen der Daten auf einer Seite könnten Sie beispielsweise folgenden Sourcecode verwenden:

```php
echo "Name: " . $_POST["$name"] . "<br>";
```

Das Problem dabei ist, dass die eingegebenen Daten nicht überprüft, sondern direkt in der Ausgabe verwendet oder (noch schlimmer) in eine Datenbank geschrieben werden.
问题在于：这些输入的数据并未经过任何检查，就被直接用于输出显示，甚至（更糟）直接写入数据库。



Ein Angreifer könnte folgendes in das Formularfeld eingeben:

`test <b>`

Oder

`test<script>prompt("Bitte Passwort eingeben")</script>`

Oder wirklich schädlichen JavaScript-Code. Die Art des Angriffes ist als XSS-Attacke (XSS 攻击（跨站脚本攻击）) bekannt und muss auf mehreren Ebenen verhindert werden.

---


解决方式 
使用 `htmlspecialchars()` 处理数据
首要的防护手段之一就是：你要“处理”所有来自客户端的数据。例如，如果你使用 PHP 的 `htmlspecialchars()` 函数，那么 HTML 特殊字符就会被转义处理，从而失去原本的 HTML 或 JavaScript 功能，变得“无害”。

Eine der ersten Schutzmaßnahmen ist, dass Sie alle Daten vom Client "behandeln". Verwenden Sie beispielsweise die PHP-Funktion **[htmlspecialchars()](https://www.php.net/manual/de/function.htmlspecialchars.php)**, so werden HTML-Sonderzeichen maskiert und somit unschädlich gemacht.

`echo "Name: " . htmlspecialchars($_POST["$name"]) . "<br>";`

Hinweis
Sie müssen alle Daten, die ein PHP-Programm als Eingabedaten bekommt, sehr kritisch behandeln. Vertiefend wird darauf im Kapitel [Reguläre Ausdrücke mit PHP](https://isp.eduloop.de/loop/Regul%C3%A4re_Ausdr%C3%BCcke_mit_PHP "Reguläre Ausdrücke mit PHP") eingegangen.
你必须非常谨慎地处理所有作为输入传递给 PHP 程序的数据。在后续章节“PHP 的正则表达式”中会更深入探讨这一主题。

Weitere Links zum Thema:

- [https://www.a-coding-project.de/ratgeber/php/code-hacken](https://www.a-coding-project.de/ratgeber/php/code-hacken)
- [https://d-mueller.de/blog/angriffe-auf-webanwendungen-teil-1-xss-beispielangriff/](https://d-mueller.de/blog/angriffe-auf-webanwendungen-teil-1-xss-beispielangriff/)


## 4.1 htmlspecialchars() 示例

```php
$input = '<script>alert("XSS")</script>';
echo htmlspecialchars($input);

# 输出 &lt;script&gt;alert(&quot;XSS&quot;)&lt;/script&gt;

这样，浏览器不会将这段字符串当作脚本执行，而是原样显示为文字，防止了 XSS 攻击。

```


```
$input = "5 > 3 & 2 < 4 ©";
echo htmlentities($input);

# 输出 5 &gt; 3 &amp; 2 &lt; 4 &copy;
```

常见字符转义情况

![](images/Pasted%20image%2020250421125634.png)


`htmlspecialchars()` vs `htmlentities()`
![](images/Pasted%20image%2020250421125651.png)



# 5 Datum ausgeben mit date()

Mit der Funktion [date()](http://php.net/manual/de/function.date.php) kann nach Belieben ein Zeitdatum angeben werden, welches von PHP dann in einen String formatiert wird. Die Reihenfolge der Angaben ist hier optional.

```php
echo date("d. F Y"),"<br>";
echo "Datum: ", date("l, d F Y "), "um ", date("H:i:s "), "Uhr";
```

Ausgabe:  
_13. February 2018  
Datum: Tuesday, 13 February 2018 um 18:49:15 Uhr

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

 Tab. 37: date()-Parameter

**Hinweis**: Die Tabelle soll Ihnen die Mächtigkeit der Einstellmöglichkeiten zeigen. Selbstverständlich sind die einzelnen Formatierungsmöglichkeiten nicht Gegenstand einer Klausur/Prüfung.


# 6 Übersicht Sortierungsfunktionen

Es gibt verschiedene vordefinierte Funktionen in PHP, mit denen Arrays sortiert werden können. Diese Funktionen bekommen ein Array übergeben, sortieren dies nach einem bestimmten Algorithmus und geben ein neues Array mit sortiertem Inhalt zurück.

|Aufsteigend|Absteigend|Benutzerdefiniert|Funktion|
|---|---|---|---|
|[sort()](http://php.net/manual/de/function.sort.php)|[rsort()](http://php.net/manual/de/function.rsort.php)|[usort()](http://php.net/manual/de/function.usort.php)|Sortiert die Werte eines Arrays und weist numerische Indizes zu. Die Zuordnung von Schlüssel zu Wert bleibt dabei nicht erhalten. Ein vorher assoziatives Array wird in ein indiziertes Array umgewandelt.|
|[asort()](http://php.net/manual/de/function.asort.php)|[arsort()](http://php.net/manual/de/function.arsort.php)|[uasort()](http://php.net/manual/de/function.uasort.php)|Die Funktion _asort()_ sortiert ein assoziatives Array aufsteigend nach den Werten der Elemente. Die Zuordnung von Schlüssel zu Wert bleibt dabei erhalten.|
|[ksort()](http://php.net/manual/de/function.ksort.php)|[krsort()](http://php.net/manual/de/function.krsort.php)|[uksort()](http://php.net/manual/de/function.uksort.php)|Die Funktion _ksort()_ sortiert ein assoziatives Array aufsteigend nach den Schlüsseln. Die Beziehung zwischen Schlüssel und Wert bleibt erhalten.|


Hinweis
Bei benutzerdefinierten Sortierungsfunktionen werden die Elemente mittels einer zuvor definierten Vergleichsfunktion sortiert.
Syntax-Beispiel: _usort (Array , "Name der Vergleichsfunktion");_

```
$personen = [
    ["name" => "Tom"],
    ["name" => "Anna"],
    ["name" => "Bernd"]
];

function vergleicheNamen($a, $b) {
    return strcmp($a["name"], $b["name"]);
}

usort($personen, "vergleicheNamen");

print_r($personen);

```


## 6.1 Beispiel für die Sortierungsfunktionen sort() & rsort()

Hier wird ein Beispiel für die häufig verwendeten Sortierfunktionen _sort()_ und _rsort()_ gezeigt. Wie wir am Beispiel sehen, sortieren die PHP-Funktionen das Array direkt, also ohne eine Zuweisung an ein anderes Array: also nur `sort($digits)` verwenden und nicht `$sortDigits = sort($digits)`.


```
$digits = [17, 19, 21, 15, 9, 13];
$size = sizeof($digits);

//unsortiert
echo "unsortiert: ";
for ($count = 0; $count < $size; $count++) {
    echo "$digits[$count] ";
}

//aufsteigend sortiert
sort($digits);
echo "<br>aufsteigend sortiert: ";
for ($count = 0; $count < $size; $count++) {
    echo "$digits[$count] ";
}

//absteigend sortiert
rsort($digits);
echo "<br>absteigend sortiert: ";
for ($count = 0; $count < $size; $count++) {
    echo "$digits[$count] ";
}
```


Ausgabe:  
_unsortiert: 17 19 21 15 9 13_  
_aufsteigend sortiert: 9 13 15 17 19 21_  
_absteigend sortiert: 21 19 17 15 13 9_


## 6.2 Beispiel für die Sortierungsfunktion uksort()

Es macht Sinn, eine eigene Vergleichsfunktion zu verwenden, wenn die Entscheidung über die Sortierreihenfolge nicht trivial ist. Dann wird die Sortierung mit _[usort()](https://www.php.net/manual/de/function.usort.php)_ oder _[uksort()](https://www.php.net/manual/de/function.uksort)_ durchgeführt.

Code

```
function compare($one, $two)
{
    if ($two > $one)  return 1;
    if ($two < $one)  return -1;
    if ($two == $one) return 0;
}
$digits = [4 => "vier", 3 => "drei", 20 => "zwanzig", 10 => "zehn"];
uksort($digits, "compare");
print_r($digits);
echo "<br><br>";
while (list($key, $value) = each($digits)) {
    echo "$key: $value<br />";
}
```

Ausgabe:  
`_Array ( [20] => zwanzig [10] => zehn [4] => vier [3] => drei )_  `
  
_20: zwanzig_  
_10: zehn_  
_4: vier_  
_3: drei_

Hinweis

Die Sortierung erfolgt nach den Schlüsseln, wobei die Zuordnung "Schlüssel-zu-Wert" erhalten bleibt.

Mit dem _return-_Wert 1, -1, oder 0 wird _uksort()_ angewiesen, dass das **zweite** Argument größer, gleich oder kleiner ist als das **erste** Argument.

Wir sehen hier, dass in **Zeile 9** die vordefinierte PHP-Funktion _uksort($digits, "compare")_ die eigene Funktion _compare($one, $two)_ aufruft. Die eigene Funktion _compare_ wird dann auch als [_**Callbacks / Callables**_](https://www.php.net/manual/de/language.types.callable.php) bezeichnet.

Hinweis

_Callables_ sind sehr interessant. Eine PHP-Funktion wird anhand ihres Namens als String übergeben, wie das Beispiel mit der Funktion _compare($one, $two)_ zeigt, die als String übergeben wird an _uksort($digits, "compare")_.

Jede PHP-eigene Funktion (außer array(), echo, empty(), eval(), exit(), isset(), list(), print, unset()) und jede selbst erstellte Funktion kann für die Übergabe verwendet werden



# 7 Zufallsgenerierter Inhalt

Oftmals sind mehr Informationen vorhanden, als „Platz“ auf der Startseite. Wenn aus einer festen Anzahl von Bildern oder Texten ausgewählt werden soll, so bietet sich folgende Funktionalität an.


Bilder oder Texte zufällig auf die Webseite stellen

```php
$numbers = mt_rand(1, 3);
echo "<img src=\"datei{$numbers}.png\">";
```

| Funktion                                                     | Erklärung                                                                                                                                                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [mt_srand()](http://php.net/manual/de/function.mt-srand.php) | Legt einen internen Startwert für einen Zufallsgenerator mit _mt_rand()_ fest. Diese Werte werden über die aktuelle Uhrzeit festgelegt, da gleiche Startwerte sonst zu Pseudo-Zufallssequenzen führen. |
| [mt_rand()](http://php.net/manual/de/function.mt-rand.php)   | Erzeugt „bessere“ Zufallszahlen.  <br>Für die bereitgestellten Funktionen bietet _mt_rand()_ einen Drop-In Ersatz. Es benutzt einen Zufallsgenerator.                                                  |
|                                                              |                                                                                                                                                                                                        |

- 设置 `mt_rand()` 随机数生成器的**起始种子**（seed），常用于为了保证随机结果的可重复性，或者是调试时控制输出。
- 生成一个伪随机整数（默认在 0 到 `mt_getrandmax()` 之间）。这是一个比传统 `rand()` 更快更“随机”的替代方案。

|函数|功能|必须调用吗？|说明|
|---|---|---|---|

|   |   |   |   |
|---|---|---|---|
|`mt_srand()`|设置随机数生成器的种子值|❌（可选）|如果不设置，PHP 会使用当前时间作为默认种子|

|   |   |   |   |
|---|---|---|---|
|`mt_rand()`|生成一个伪随机整数|✅（核心功能）|如果你想得到一个“看起来更随机”的数，就用这个而不是 `rand()`|


```
mt_srand(123);         // 设置种子（可选）
$zahl = mt_rand();     // 得到一个伪随机数
echo $zahl;
```

    每次用相同种子执行，mt_rand() 生成的数是一样的，这在调试、测试、加密等场景中很重要。



---


Ein weiteres Beispiel ist ein Lottozahlen-Generator. Dieser erzeugt sechs unterschiedliche, zufällige Zahlen zwischen 1 und 49. Der Code wird in der folgenden Abbildung gezeigt.
```php
for ($number = 1; $number <= 49; $number++) {
    $numbers[] = $number;
}
for ($quantity = 1; $quantity <= 6; $quantity++) {
    $key = mt_rand(0, count($numbers) - 1);
    $drawnNumbers[] = $numbers[$key];
    unset($numbers[$key]);
    $numbers = array_values($numbers);
}
sort($drawnNumbers);
foreach ($drawnNumbers as $number) {
    echo "$number <br>\r\n";
}
```


Das Problem bei einem Lottozahlen-Generator ist, dass die Zahlen nur einmal vorkommen sollen und das natürlich bei gleicher Wahrscheinlichkeit. Deswegen verwendet man ein Array, welches man mit den möglichen Werten füllt (**Zeilen 1 bis 3**).

Anschließend werden sechs Zahlen gezogen. Dabei wird zufällig ein Array-Schlüssel ermittelt (**Zeile 5**) und der zugehörige Wert in ein neues Array geschrieben (**Zeile 6**). Anschließend wird die gezogene Zahl aus dem Zahlenvorrat entfernt, da sie bereits gezogen wird (**Zeile 7**). Da sich nun allerdings die hinteren Schlüssel des Arrays nicht geändert haben, muss das Array neu aufgebaut werden, was in **Zeile 8** durch die Funktion _array_values()_ realisiert wird.

In **Zeile 10** erfolgt eine aufsteigende Sortierung der gezogenen Zahlen, bis sie schließlich in **Zeile 12** wieder ausgegeben werden.

---


Aufg. 14: Lottozahlen-Generator

Der Lottozahlen-Generator kann vereinfacht werden. Finden Sie eine Funktion, die die Zeilen 4 bis 10 kombiniert und nur eine einfache Änderung in der Zeile 12 bedarf.


```php
Die Funktion array_rand() kombiniert die Zeilen 4 bis 10 zu einer zusammen:
$drawnNumbers = array_rand($numbers, 6);


Die Änderung der Zeile 12 ist dann wie folgt:
echo $numbers[$number] . "<br>";

```


# 8 Beispiel Formulare - Daten sortieren

In diesem Beispiel verwenden wir vier Orte. Diese sollen sortiert ausgegeben werden.

Zunächst wird zur Darstellung des Formulars das bereits bekannte Beispiel aus dem [Unterkapitel Formulare - Daten einlesen](https://isp.eduloop.de/loop/Beispiel_Formulare_-_Daten_einlesen "Beispiel Formulare - Daten einlesen") leicht abgewandelt verwendet.


```php
<?php
/**
 * Beispiel Formular - Daten einlesen
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
writeInputField("1. Ort", "ort1");
writeInputField("2. Ort", "ort2");
writeInputField("3. Ort", "ort3");
writeInputField("4. Ort", "ort4");
closeFormAndFooter();
?>
```

  
Screenshot des erzeugten Formulars  
[![File:formular4.png](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/7/7e/Formular4.png "File:formular4.png")](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/7/7e/Formular4.png)

  
Die Ausgabe der Daten auf dem Browser erfolgt wie im [Unterkapitel Formulare - Daten ausgeben](https://isp.eduloop.de/loop/Beispiel_Formulare_-_Daten_ausgeben "Beispiel Formulare - Daten ausgeben") gezeigt und ist hier nur leicht abgewandelt.


```php
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
          <h1>Daten mit foreach() ausgeben</h1>";
}
function writeHtmlEnd()
{
    echo "</body></html>";
}
// Beginn des Hauptprogramms
writeHeaderAndHeadline();
$error = false;
// Alle POST-Daten auslesen und auf leere Felder überprüfen
echo "Es wurden Daten in dieser Reihenfolge eingetragen:<br>";
foreach ($_POST as $field => $content) {
    if (!empty($content)) {
        echo "$content <br>";
    }
}
// Alle POST-Daten sortiert auslesen und auf leere Felder überprüfen
echo "<hr>Ausgabe der sortierten Daten:<br>";
asort($_POST);
foreach ($_POST as $field => $content) {
    if (!empty($content)) {
        echo "$content <br>";
    }
}
writeHtmlEnd();
?>
```

  
Screenshot des erzeugten Formulars  
[![File:formular4b.png](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/9/9c/Formular4b.png "File:formular4b.png")](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/9/9c/Formular4b.png)

**Zeile 38** enthält die Sortierfunktion. So leicht kann das Sortieren eines Arrays in PHP sein.

Hier sei noch mal unbedingt erwähnt, dass es immer gut ist zwischendurch mit dem Quellcode "zu spielen". Probieren Sie es also auf ihrem eigenen Webserver aus!

---

Übung

Der obere Sourcecode ist auf 4 Orte begrenzt und die Funktionsaufrufe finden nicht über eine for-Schleife statt, was sehr "unschön" ist. Schreiben Sie das Programm um, sodass eine for-Schleife genutzt wird und sechs Felder erzeugt werden.

```php
// Beginn des Hauptprogramms
$fieldCount = 6;
writeHeaderAndHeadline();
startForm("post", "formular4a.php");
for ($count = 1; $count <= $fieldCount; $count++) {
    writeInputField("$count. Ort", "ort$count");
}
closeFormAndFooter();
```




