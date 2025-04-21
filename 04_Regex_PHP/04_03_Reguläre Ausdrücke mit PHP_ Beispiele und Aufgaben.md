
# 1 raktische Beispiele für reguläre Ausdrücke

|Praktische Bespiele für reguläre Ausdrücke|Erklärung|
|---|---|
|preg_replace  <br>( ' /^\s*$/ ' , _, $datei);_|Löscht alle Leerzeilen einer Datei|
|preg_replace  <br>( ' /^#.*$/ ' , _, $datei);_|Löscht alle einzeiligen  <br>Kommentarzeilen einer Datei|
|preg_replace  <br>( ' /^.*\// ' , _, $pfad);_|Entfernt in absoluten Pfaden die  <br>Verzeichnisse und lässt den  <br>Dateinamen übrig|
|preg_match  <br>( ' /^\d{5}$/ ' , $feld);|Überprüft ein PLZ-Formularfeld auf 5 Digits|
|preg_match  <br>( ' /^\S+@\S+\.[A-Z]{2,6}$/i ' , $feld);|Einfache Überprüfung eines E-Mail-Formularfeldes|
|preg_match  <br>('/^#[0-9A-F]{3}([0-9A-F]{3})?$/i', $farbe)|Überprüft einen HTML-Hexcode für  <br>Farben (sowohl 3-stellig als auch 6-stellig)|

 Tab. 47: Praktische Beispiele

  

- Sehr viele, professionelle Beispiele finden sind im Buch:  
    Goyvaerts, Jan; Levithan, Steven (2010): Reguläre Ausdrücke Kochbuch. [detaillierte Lösungen für acht Programmiersprachen; mit Einstiegs-Tutorial]. O'Reilly Verlag.



# 2 Erste Übungsaufgaben

Verwendet wird: _preg_replace($suchmuster, $ersetzen, $text)_.  
Wie lautet das Ergebnis?

  

Übung

Text: _Er, sein Name ist Eric, ist 23 Jahre alt_  

Suchmuster: _/\W.*/_  
Ersetzen: _' '_

Ergebnis: _Er_  
  
Löscht von der ersten Stelle an, an der ein Zeichen vorkommt, dass nicht zu einem Wort gehört. Von dort an bis zum Ende der Zeile.

  

Übung

Text: _Er, sein Name ist Eric, ist 23 Jahre alt_  

Suchmuster: _/,.*/_  
Ersetzen: _' '_

Ergebnis: _Er_  
  
Alle Zeichen hinter dem ersten Komma und das Komma werden gelöscht.

  

Übung

Text: _Er, sein Name ist Eric, ist 23 Jahre alt_  

Suchmuster: _/.,._{_3_}_/_  
Ersetzen: _' '_

Ergebnis: _Ein Name ist Erit 23 Jahre alt_  
  

Der reguläre Ausdruck geht zum ersten Komma. Von dort aus werden gelöscht: ein Zeichen vor dem Komma, das Komma und drei Zeichen nach dem Komma. Da wir kein _$limit_ (siehe [Einfaches Beispiel für preg replace()](https://isp.eduloop.de/loop/Einfaches_Beispiel_f%C3%BCr_preg_replace\(\) "Einfaches Beispiel für preg replace()")) angegeben haben, werden alle Treffer gelöscht. Somit geht der reguläre Ausdruck auch zum zweiten Komma und löscht dort entsprechend.

  

Übung

Text: _Er, sein Name ist Eric, ist 23 Jahre alt_  

Suchmuster: _/,.*,/_  
Ersetzen: _' '_

Ergebnis: _Er ist 23 Jahre alt_  
  
Der reguläre Ausdruck geht vom ersten **bis zum letzten Komma** und löscht dazwischen alles.

  

Übung

Text: _Er, sein Name ist Eric, ist 23 Jahre alt_  

Suchmuster: _/,.*?,/_  
Ersetzen: _' '_

Ergebnis: _Er ist 23 Jahre alt_  
  
Der reguläre Ausdruck geht vom ersten **bis zum nächsten Komma** und löscht dazwischen alles.

  

Übung

Text: _Meier, Eric ist 23 Jahre alt_  

Suchmuster: _/(\w*),\s(\w*)/_  
Ersetzen: _"$2 $1";_

Ergebnis: _Eric Meier ist 23 Jahre alt_  
  
Im Ausdruck _( \w*)_ werden alle Buchstaben des ersten Wortes gefunden (hier: _Meier_) und in der Variable _$1_ automatisch gespeichert. Dann folgen im Suchmuster Komma und Leerzeichen, gefolgt von den Buchstaben des zweiten Wortes (hier: _Eric_), das in _$2_ gespeichert wird.

  

Übung

Text: _Meier, Eric ist 23 Jahre alt_  

Suchmuster: _/(\w),\s(\w)/_  
Ersetzen: _"$2 $1";_

Ergebnis: _MeieE rric ist 23 Jahre alt_  
  
Im Ausdruck _(\w)_ wird nur ein Buchstabe (hier das _„r“_ von _Meier_) gefunden und in der Variablen _$1_ gespeichert. Dann folgt im Suchmuster das Leerzeichen. Anschließend wird der erste Buchstabe des zweiten Wortes gefunden (hier das _„E“_ von _Eric_) und in _$2_ gespeichert.


# 3 Nachvollziehen von Lösungen

Gegeben sind Aufgaben mit Lösungen. Sie sollen **die unterstrichene Lösung nachvollziehen** können.

|PHP-Funktion|Suchstring|Text|
|---|---|---|
|`preg_match()`|`/[^mas]{4}/`|"Wer was macht, macht was"|
|`preg_match()`|`/W.+/`|"Wer was macht, macht was"|
|`preg_match()`|`/\w+/`|"Wer was macht, macht was"|
|`preg_match()`|`/.\./`|"Zwischen 1.220 und 1.300 Euro"|
|`preg_match()`|`/\D.{5}/`|"Zwischen 1.220 und 1.300 Euro"|
|`preg_match()`|`/\b\W.*0/`|"Zwischen 1.220 und 1.300 Euro"|
|`preg_match()`|`/[A-Z][a-z]\d/`|"Zwischen 1.220 und 1.300 Euro"  <br>(kein Treffer)|
|`preg_match()`|`/(Text\|Briefe)/`|"Dies ist ein Text einer 1. Testseite"|
|`preg_match()`|`/[a-z]{3}$/`|"Dies ist ein Text einer 1. Testseite"|
|`preg_match()`|`/\d\.\s\w\w\w/`|"Dies ist ein Text einer 1. Testseite"|
|`preg_match()`|`/(\s\w+){2,3}/`|"Dies ist ein Text einer 1. Testseite"|
|`preg_match()`|`/\w.\s\w{1,3}/`|"Dies ist ein Text einer 1. Testseite"|

 Tab. 48: Nachvollziehen von Lösungen zu regulären Ausdrücken


# 4 Reguläre Ausdrücke mit PHP: Weitere Übungsaufgaben

Aufgabe

Zeigen Sie anhand von eigenen Beispielen  

(a) den Unterschied zwischen _/Ha.?s/_ und _/Ha.+s/_  
(b) den Unterschied zwischen _abc*_ und _(abc)*?_  

  

Übung

Nutzen Sie anstelle der Quantoren _* + ?_ das Wiederholungsintervall { }  

Wie lautet das Wiederholungsintervall für den Quantor _*_  
Wie lautet das Wiederholungsintervall für den Quantor _+_  
Wie lautet das Wiederholungsintervall für den Quantor _?_  

  
Gegeben sind Aufgaben ohne Lösungen. Die Lösungen ermitteln Sie bitte über das [Online-Tool für reguläre Ausdrücke](http://moodle.oncampus.de/modules/ir280/onmod/material/regexp.php)

|   |   |   |
|---|---|---|
|**PHP-Funktion**|**Suchstring**|**Text**|
|_preg_match()_|_/.../_|"Dagobert Duck, Donald Duck u.s.w."|
|_preg_match()_|_/.*,./_|"Dagobert Duck, Donald Duck u.s.w."|
|_preg_match_all()_|_/u._{_3_}_/_|"Dagobert Duck, Donald Duck u.s.w."|
|_preg_match_all()_|_/.\s/_|"Dagobert Duck, Donald Duck u.s.w."|
|_preg_match_all()_|_/D\w+/_|"Dagobert Duck, Donald Duck u.s.w."|
|_preg_match()_|_/\s.*\s/_|"Zwei Zwerge zeigen zwanzig Zehen"|
|_preg_match()_|_/\b[a-z].*?\s/_|"Zwei Zwerge zeigen zwanzig Zehen"|
|_preg_match()_|_/\D+/i_|"Zwei Zwerge zeigen zwanzig Zehen"|
|_preg_match_all()_|_/Z/i_|"Zwei Zwerge zeigen zwanzig Zehen"|
|_preg_match_all()_|_/D\w+/_|"Zwei Zwerge zeigen zwanzig Zehen"|

 Tab. 49: Reguläre Ausdrücke: Aufgaben zum Selbstlösen

