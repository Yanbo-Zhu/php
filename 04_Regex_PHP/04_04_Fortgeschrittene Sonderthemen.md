

# 1 Maskieren von Sonderzeichen preg_quote

Wenn ein zu durchsuchender String **Sonderzeichen** enthält, wie beispielsweise:  
_**Er hatte die $-Zeichen in "den Augen"**_,  
so müssen diese mittels Backslash-Maskierung in einen String ohne Sonderzeichen umgewandelt werden:  
_**Er hatte \$-Zeichen in den \"Augen\"**_.

Nur ohne diese Sonderzeichen bzw. mit maskierten Sonderzeichen kann dieser String mit einem regulären Ausdruck behandelt werden.

Eine Maskierung von Hand ist oftmals nicht möglich, beispielsweise, wenn eine Zeile (ein String) aus einer Datei ausgelesen wird. Hierzu dient die PHP-Funktion  
_**$mein_string = [preg_quote](http://php.net/manual/en/function.preg-quote.php) ($meine_dateizeile);**_


# 2 Für Fortgeschrittene: Single-line-Mode

Der Single-line-Mode kann dafür verwendet werden in HTML-Dateien vom Begin-Tag bis zum End-Tag alles zu bearbeiten, auch wenn der Tag über mehrere Zeilen geht.

Selbstverständlich können auch mehrzeilige Kommentare (C, Java) hiermit bearbeitet werden. **In dem kleinen Beispiel sollen Kommentare gelöscht werden, die zwischen /* und */ über mehrere Zeilen gehen.**


```php
$text = "
 //Auszug aus einer Klasse in einen String geschrieben
 //String wird so bearbeitet, dass jeweils Kommentare geloescht werden.
 /**
  * displays test
  */
 public function test()
 {
    echo('test');
 }
 ";
 print "Mit Kommentaren:<br />
    <pre>"   .   $text   .   "</pre>";
 $suchmuster = '/\/\*.*?\*\//s';
 $ersetzen = '';
 $neuerText = preg_replace($suchmuster, $ersetzen, $text);
 print "- - - <br />
    Ohne Kommentare:<br />
    <pre>"   .   $neuerText   .   "</pre>";
 ?>
```

 List. 10: Ersetzen von mehrzeiligen Kommentaren

  
Ausgabe:  

Mit Kommentaren:

```php
 //Auszug aus einer Klasse in einen String geschrieben
 //String wird so bearbeitet, dass jeweils Kommentare geloescht werden.

 /**
  * displays test
  */
 public function test()
 {
    echo('test');
 }
 
```

- - -
Ohne Kommentare:

```php
 //Auszug aus einer Klasse in einen String geschrieben
 //String wird so bearbeitet, dass jeweils Kommentare geloescht werden.

 
 public function test()
 {
    echo('test');
 }
```


# 3 Beispiel mod rewrite für den Apache Webserver

Das Modul mod_rewrite kann verwendet werden um URLs zu erkennen, umzuschreiben und intern oder auch beim Benutzer weiterzuleiten. So findet man heute häufig schöne URLs die keine Dateinamen oder lange Parameterketten mehr enthalten. Für solche Zwecke wird häufig dieses Modul verwendet.

Sie haben bereits die .htaccess im Kapitel Apache kennengelernt. Mit Hilfe dieser Datei können wir nun nicht nur die verwendete Sprache verstecken, sondern auch die Seite ein wenig besser leserlich machen (Wikipedia Stichwort [SEO](https://de.wikipedia.org/wiki/Suchmaschinenoptimierung)).  
  

Code

```
RewriteEngine On
 RewriteBase /
# der Inhalt nach dem ersten Slash wird als Seite bestimmt
# weitere Parameter werden angehängt
 RewriteRule ^(.*)\/(.*)\/(.*)$ index.php?page=$1&id=$2&$3
```

 List. 11: Beispiel für eine .htaccess mit aktiviertem mod_rewrite Modul

  
Beispiel:  
_http://www.abc.de/home/4/sid=123456  
_Leitet intern weiter auf:  
_index.php?page=home&id=4&sid=123456_

  
Natürlich können Sie **beliebig viele Regeln** produzieren die unterschiedlich viele Parameter verarbeiten. Es gilt allerdings dann auch festzulegen, dass nur eine passt.

Die Apache Konfigurationsdatei wird von oben nach unten gelesen und **jeder** passende Ausdruck wird verwendet, es sei denn, Sie markieren diesen mit _[L]_ **für "last rule"**. Dies hat auch einen kleinen Geschwindigkeitsvorteil, da dann das Vergleichen der Strings abbricht.

Das Beispiel _http://www.abc.de/home/4/sid=123456_ passt auf die folgenden regulären Ausdrücke.  
  

Code

```
RewriteRule ^home\/(.*)\/(.*)$ index.php?id=$1&$2
 RewriteRule ^(.*)\/(.*)\/(.*)$  alle.php?page=$1&id=$2&$3
```

 List. 12: Zwei Regeln die auf unsere URL passen und somit auch beide verwendet werden

  
Um dieses nun zu verhindern hängen sie ein _[L]_ **für "last rule"** an.

Code

```
RewriteRule ^home\/(.*)\/(.*)$ index.php?id=$1&$2  [L]
 RewriteRule ^(.*)\/(.*)\/(.*)$  alle.php?page=$1&id=$2&$3
```

 List. 13: Korrektur um dafür zu sorgen, dass nur die erste Regel verwendet wird


# 4 Finite Automaten und Reguläre Ausdrücke

**Drei finite Automaten**  
Es gibt drei Varianten für Werkzeuge, die reguläre Ausdrücke bearbeiten können:

- **DFA:** Deterministischer finiter Automat  
    Der DFA betrachtet Zeichen für Zeichen und kann intern keine Suchtreffer speichern. Somit kann DFA nicht „suchen und ersetzen“, da die Treffer nicht zwischengespeichert wurden.
- **NFA:** Nicht-deterministischer finiter Automat  
    Der NFA basiert auf Backtracking und merkt sich alle Stellen, wenn mehr als eine Treffermöglichkeit existiert. Anschließend werden alle Treffermöglichkeiten nacheinander bearbeitet. Somit können Muster wie _s/(Internet)(Programmierung)/$2 im $1/_ erfolgreich umgesetzt werden.
- **POSIX-NFA:** als eine Abwandlung des NFA

  

Hinweis

Alle in dem gesamten Kapitel behandelten Regeln und Beispiele beruhen auf dem POSIX-NFA. Dieser wird in PHP (wie auch in Perl) verwendet. Manchmal wird der Begriff POSIX-NFA in der Literatur verwendet und Sie können dann direkt an die hier beschriebenen Regeln und Beispiele denken.


