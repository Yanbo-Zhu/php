
Das Zusammenspiel von regulären Ausdrücken und PHP soll an sehr einfachen Beispielen gezeigt werden. Wir konzentrieren uns auf die Verwendung der PHP-Funktionen **preg_match()**, **preg_match_all()** und **preg_replace()**.

| Element                                                                      | Beschreibung                                                                                                                                      |
| ---------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| **[preg_match()](http://php.net/manual/de/function.preg-match.php)**         | Speichert den ersten Eintrag und gibt 1 zurück wenn etwas gefunden wurde.  `preg_match ($suchmuster,$text)`                                       |
| **[preg_match_all()](http://php.net/manual/de/function.preg-match-all.php)** | Speichert alle Strings, die auf das gesuchte Muster passen und gibt die Anzahl der Treffer zurück.  `preg_match_all ($suchmuster,$text,$treffer)` |
| **[preg_replace()](http://php.net/manual/de/function.preg-replace.php)**     | Suchen und Ersetzen von Strings mit einem regulären Ausdruck.  `preg_replace ($suchmuster,$ersetzen,$text)`                                       |

 Tab. 42: Wichtige PHP-Funktionen für reguläre Ausdrücke



Es gibt noch [eine Reihe weiterer Funktionen für reguläre Ausdrücke](http://de.php.net/manual/de/ref.pcre.php), auf die wir aber in den folgenden Unterkapiteln nicht weiter eingehen. Hier eine Auswahl daraus:
- **preg_filter()** — Suchen und ersetzen. Funktioniert ähnlich wie preg_replace()
- **preg_grep()** — Liefert alle Elemente, die auf ein Suchmuster passen. Als Eingabe dient ein Array (anstelle eines einfachen Strings).
- **preg_quote()** — Maskiert Zeichen regulärer Ausdrücke, indem ein ein Backslash vor jedes Zeichen der durchsuchende Zeichenkette gesetzt wird. Das sinvoll, wenn ein Text Sonderzeichen enthält.
- **preg_split()** — Zerlegt eine Zeichenkette anhand eines regulären Ausdrucks.


Wir verwenden für PHP die [PCRE-Befehle](http://de.php.net/manual/de/ref.pcre.php) (Perl Compatible Regular Expressions). Die noch vorhandenen Posix Alternativen (ereg, ereg_replace, …) wurden mit PHP 6 abgeschafft und sind schon seit 5.3 als deprecated markiert und daher nicht mehr zu verwenden.

Wer schon in Perl mit regulären Ausdrücken gearbeitet hat, der kann diese so in PHP übernehmen. Weitere Informationen hierzu gibt es unter [http://php.net/manual/de/book.pcre.php](http://php.net/manual/de/book.pcre.php).


# 1 Einfaches Beispiel für preg match()

Schauen Sie sich diese Beispiele für die Verwendung der regulären Ausdrücke in PHP genau an. Sie werden diese oft brauchen.
Zuerst ein Beispiel für eine einfache Suche mit _**[preg_match()](http://php.net/manual/de/function.preg-match.php)**_ und eine _if_-Abfrage, ob das Suchmuster in einem Textstring vorkommt.


```php
<?php
$text = "PHP macht viel Spass";
$suchmuster = '/viel/';
if(preg_match ($suchmuster, $text, $treffer)) {
    print_r($treffer);
}else{
    print "Kein Treffer";
}
?>
```

 List. 1: Beispiel für die einfache Suche mit regulären Ausdrücken

Zurückgegeben wird ein Array mit einem Element.  
Die Ausgabe in _`$treffer`_ lautet:  `Array([0] => viel)` .

In der **4. Zeile** sehen Sie, dass die PHP-Funktion _**preg_match()**_ direkt in der if-Abfrage steht. Also Achtung: die Funktion `preg_match()`  selbst gibt nur _1_ (=Treffer) oder _FALSE_ (=kein Treffer) zurück.

 `preg_match()`  erwartet als Parameter  `$suchmuster` und  `$text` . Die Variable  `$treffer`  ist optional. Auch sind bei allen preg-Funktionen weitere Parameter (z.B. für einen Offset) möglich.


# 2 Einfaches Beispiel für preg match all()

Manchmal möchte man wissen, wie oft etwas vorkommt. Hierzu kann man _**[preg_match_all()](http://php.net/manual/de/function.preg-match-all.php)**_ gut verwenden.

Beispiel

```php
<?php
$text = "PHP macht viel Spass";
$suchmuster = '/a/';
if (preg_match_all ($suchmuster, $text, $treffer)) {
    print_r($treffer);
}else{
    print "Kein Treffer";
}
?>
```

 List. 2: Beispiel für die Suche nach allen Treffern mit regulären Ausdrücken

Zurückgegeben wird ein Array mit allen Treffern.  
Die Ausgabe in  `$treffer`  lautet:  `Array ([0] => Array([0]=>a [1]=>a))` .

```
Array
(
    [0] => Array
        (
            [0] => a
            [1] => a
        )
)
```


Your regex: `/a/`
- This **doesn't have any capture group** (no parentheses `()`).
- `preg_match_all()` still returns the matches in a **default group [0]** — which means **the entire match**.

So the `[0]` key is for group 0, which is the **whole match** (`a` in this case).

Since there are **three "a"s** in your string, you get:

```
[0] => Array
    (
        [0] => a
        [1] => a
        [2] => a
    )
```



If your regex had a capture group, for example `/([a])/`
Then you'd get:
```
Array
(
    [0] => Array
        (
            [0] => a
            [1] => a
            [2] => a
        )
    [1] => Array
        (
            [0] => a
            [1] => a
            [2] => a
        )
)
```

- `[0]`: the **full match** (same as before)
- `[1]`: the **first capture group** (still just `a` in this case)


---


Die Anzahl der Vorkommnisse kann gezählt werden:

`$anzahl=preg_match_all($suchmuster,$text)`

_preg_match_all()_ erwartet als Parameter _`$suchmuster`_, _`$text`_ und _`$treffer`_. Seit PHP 5.4 ist _`$treffer`_ optional. Weitere Parameter (z.B. für einen Offset) sind möglich.

# 3 Einfaches Beispiel für preg replace()

Sehr häufig soll ein Ausdruck durch einen anderen ersetzt werden. Das ist die Aufgabe von _**[preg_replace()](http://php.net/manual/de/function.preg-replace.php)**_.

Beispiel

```
<?php
$text = "PHP macht viel Spass";
$suchmuster = '/ viel /';
$ersetzen   = 'mir' ;
$neuerText  = preg_replace($suchmuster, $ersetzen, $text);
print $neuerText;
?>
```

 List. 3: Beispiel für suchen und ersetzen mit regulären Ausdrücken

Zurückgegeben wird ein String.  
Die Ausgabe in _$neuerText_ lautet: _**PHP macht mir Spass**_.

In der **5. Zeile** sehen Sie, dass die PHP-Funktion _preg_replace()_ anders funktioniert, denn dort wird das Ergebnis in einer Variablen _$neuerText_ gespeichert.

---


_**[preg_replace()](http://php.net/manual/de/function.preg-replace.php)**_ ist aber noch mächtiger, als in dem trivialen Beispiel angegeben. Denn _preg_replace()_ findet ohne Limitierung alle Treffer und ersetzt diese, wenn das Limit nicht explizit angegeben wird.

Hier suchen wir nach dem Buchstaben _a_ und löschen diesen, indem wir in _$ersetzen_ einen leeren String schreiben.

```php
<?php
$text = "PHP macht viel Spass";
$suchmuster = '/a/';
$ersetzen   = '' ;
$neuerText  = preg_replace($suchmuster, $ersetzen, $text);
print $neuerText;
?>
```

 List. 4: Beispiel für suchen und ersetzen mit regulären Ausdrücken

Ausgabe:  
_PHP mcht viel Spss_

  


Wenn wir eine feste Anzahl von Treffern ersetzen möchten, dann kann dies in _preg_replace()_ mit angegeben werden. Wir führen hierfür die Variable _$limit" ein._

```php
<?php
$text = "Regen, Regen, nichts als Regen";
$suchmuster = '/Regen/';
$ersetzen   = 'Schnee';
$limit = 2;
$neuerText  = preg_replace($suchmuster, $ersetzen, $text, $limit);
print $neuerText;
?>
```

 List. 5: Beispiel für suchen und ersetzen mit regulären Ausdrücken

Ausgabe:  
_Schnee, Schnee, nichts als Regen_

In der **5. Zeile** haben wir ` $limit` = 2, gesetzt, sodass nur die ersten beiden Treffer ersetzt wurden. Mit  `$limit` = -1  (Default-Einstellung) werden alle Treffer gefunden und ersetzt.



Auch eine Kurzschreibweise ohne Variablen ist möglich, in der wir die Strings direkt einsetzen:
```
$neuerText=preg_replace("/H/","M","Haus<Auto");
```



