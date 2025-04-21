
https://isp.eduloop.de/loop/Syntax_regul%C3%A4rer_Ausdr%C3%BCcke

# 1 Runde Klammern bilden eine Gruppe

Wichtig

- Sofern nicht anders angegeben beziehen sich die Beispiele auf _preg_match()_.
- Die Texte werden nicht in Anführungszeigen gesetzt, um Verwirrungen zu vermeiden.
- Die Fundstelle ist im Ergebnis unterstrichen.

  
**Die runden Klammern ( ) werden zur Gruppierung genutzt**. Sie gruppieren die Elemente zu einem einzigen Element. Es muss eine Übereinstimmung in der Reihenfolge mit allen Elementen vorliegen.

Text: _Hier teste ich die Texte_  
Suchmuster: _/**(die)**/_  
Ergebnis: _Hier teste ich die Texte_

  
Auch ohne Klammer muss das gesamte Suchmuster erfüllt sein. Somit ist die runde Klammer in diesem einfachen Beispiel überflüssig. Bei komplexeren regulären Ausdrücken wird eine runde Klammer oft zur Gruppierung eingesetzt.

Text: _Hier teste ich die Texte_  
Suchmuster: _/**die**/_  
Ergebnis: _Hier teste ich die Texte_

  
**Alternativen können mit dem Pipe-Zeichen | gebildet werden.**  
Text: _Das Hotel ist 70km vom Strand und 30km vom See entfernt_  
Suchmuster: _/**(30|50|70|90)km**/_  
Ergebnis: _Das Hotel ist 70km vom Strand und 30km vom See entfernt_

Hinweis

Die Reihenfolge der Alternativen im Suchmuster spielt keine Rolle. Der erste Treffer im Text wird gefunden.

# 2 Eckige Klammern als Mengenklammer

**Die eckige Klammer [ ] dient als Mengenklammer**. Es muss nur ein beliebiges Element aus der Menge gefunden werden.

Text: _Hier teste ich die Texte_  
Suchmuster: _/ **[die]** /_  
Ergebnis für preg_match(): _Hier teste ich die Texte_  
Ergebnis für preg_match_all(): _Hier teste ich die Texte_

  
In der eckigen Klammer lassen sich vereinfachte Mengenangaben schreiben. Der Bindestrich ist damit ein Sonderzeichen dieser Klammer.

- [0-9] alle Ziffern
- [A-Z] alle großen Buchstaben
- [a-z] alle Kleinbuchstaben
- [A-Za-z] alle Buchstaben (keine Umlaute)

Für alle oben genannten Mengen sind auch Teilbereich möglich z.B. [3-8].

Text: _Hier teste ich 1000 Texte_  
Suchmuster: _/ **[0-9]** /_  
Ergebnis: _Hier teste ich 1000 Texte_

  
**Die eckige Klammer kann negiert werden [^ ]**. Das Negationszeichen ^ steht dann am Anfang in der Klammer.

Text: _Hier teste ich die Texte_  
Suchmuster: _/ **[^die]** /_  
Ergebnis: _Hier teste ich die Texte_

  
**Sonderzeichen in der Mengenklammer sind**  
Die Zeichen [^ - / \] gelten in der Mengenklammer als Sonderzeichen.

  
**Keine Sonderzeichen in der Mengenklammer sind**  
Die Zeichen [, . * + ? | ( ) # ~ ] gelten in der Mengenklammer als einfache Zeichen ohne Sonderfunktion.


# 3 Zeichenklassen für Wörter, Zahlen etc.

Einige Mengen kommen sehr oft vor, beispielsweise die Menge aller Ziffern [0-9]. Für diese Menge wird nun ein abkürzendes Sonderzeichen \d eingeführt. Jedes dieser Sonderzeichen hat auch eine Negation. Z.B. entspricht \D der Menge `[^0-9]`.

|Sonderzeichen|Negation|Erklärung|
|---|---|---|
|\d|\D|Digit (entsprechend [0-9]) bzw. nicht Digit (entsprechend [^0-9])|
|\w|\W|Alphanumerische Zeichen (Wort) entsprechend [a-zA-Z0-9_] bzw. nicht alphanumerische Zeichen entsprechend [^a-zA-Z0-9_]|
|\s|\S|Whitespace (Leerzeichen und Tabulator) bzw. nicht whitespace|
|\b|\B|Wortgrenze (_b =boundary_) bzw. nicht Wortgrenze.  <br>Eine Wortgrenze ist definiert als \W Zeichen vor oder hinter einem \w-Zeichen.|

 Tab. 43: Sonderzeichen für Wörter, Zahlen etc.

  
Text: _Hier teste ich 1000 Texte_  
Suchmuster: _/ **\d** /_  
Ergebnis: _Hier teste ich 1000 Texte_

  
Text: _Hier teste ich 1000 Texte_  
Suchmuster: _/ **\w\w\w\s\d\d\d\d** /_  
Ergebnis: Hier teste ich 1000 Texte

  
Bisher hat jedes Zeichen im Suchmuster immer genau auf ein Zeichen im Text gepasst. Dies ist mit \b nun erstmalig anders. _\b_ findet die Wortgrenze, markiert aber kein einzelnes Zeichen.  
Text: _Hier teste ich 1000 Texte  
_Suchmuster: _/ **\b**\w\w\w\s\d\d\d\d**\b** /_  
Ergebnis: _Hier teste ich 1000_ Texte  
  

Hinweis

Achtung: Deutsche Umlaute sind nicht in der Menge von \w enthalten und werden entsprechend als Wortgrenze angesehen. Umlaute sind „fies“ und darauf wird später noch eingegangen.


# 4 Sonderzeichen maskieren mit Backslash \

Der Backslash wird für Sonderzeichen wie z.B. \d = digit genutzt und dient auch zur Maskierung von anderen vordefinierten Sonderzeichen in regulären Ausdrücken.

Text: Er hatte $-Zeichen in den Augen  
Suchmuster: / **\$-Zeichen** /  
Ergebnis: Er hatte $-Zeichen in den Augen

  
Text: Ich suche nach allen _\d_ Sonderzeichen  
Suchmuster: /**\\d**/  
Ergebnis: Ich suche nach allen _\d_ Sonderzeichen


# 5 Geschweifte Klammern für Wiederholungen

**Die geschweifte Klammer** { } **gibt ein Wiederholungsintervall an**. Also wie oft das vorstehende Zeichen vorkommen soll. {2,3} bedeutet, dass das vor der geschweiften Klammer stehende Zeichen 2 bis 3-mal vorkommen darf.

Notation:  

- {5} genau 5-mal
- {5,} mindestens 5-mal
- {,5} maximal 5-mal
- {2,5} mindestens 2 und maximal 5-mal

  
Text: _Hier teste ich 1000 Texte_  
Suchmuster: /_**[0-9]**_{_**2**_}/  
Ergebnis: _Hier teste ich 1000 Texte_

  
Text: _Hier teste ich 1000 Texte_  
Suchmuster: /_**\d**_{_**1,3**_}/  
Ergebnis: _Hier teste ich 1000 Texte_  
Achtung: bei einem variablen Bereich nimmt das Wiederholungsintervall immer den **maximal möglichen Wert** an.

  
Text: _Hier teste ich 1000 Texte_  
Suchmuster: /_**\d**_{_**1,3**_}_**?**_/  
Ergebnis: _Hier teste ich 1000 Texte_  
Ein **Fragezeichen** dahinter bewirkt, dass das Wiederholungsintervall den **minimal möglichen Wert** annimmt.

# 6 Joker-Zeichen

Wenn man einen beliebigen Text mit beliebiger Länge überprüfen möchte, dann sind die Joker-Zeichen (auch **Quantoren**) wichtig.

|Zeichen|Erklärung|
|---|---|
|.|Der „Punkt“ steht für ein beliebiges Zeichen (Ausnahme: Zeilenumbruch Newline).|
|?|Das vorstehende Zeichen 0 oder 1-mal.|
|+|Das vorstehende Zeichen 1-mal oder beliebig oft.|
|*|Das vorstehende Zeichen 0-mal oder beliebig oft.|

 Tab. 44: Sonderzeichen für die Zeichen-Wiederholung

  
Text: _Hier teste ich 1000 Texte_  
Suchmuster: _/**.+1000**/_  
Ergebnis: _Hier teste ich 1000 Texte_  
Hier wirkt .+ wie ein „Gummiband“, das so lange gedehnt wird, bis ein maximaler Treffer möglich ist.

  
Text: _Hier teste ich 1000 Texte_  
Suchmuster: _/[A-Z]?(ich)+/_  
Ergebnis: _Hier teste ich 1000 Texte_  
Da vor dem festen Suchausdruck ich kein Großbuchstabe steht (sondern ein Leerzeichen), wirkt sich das  ? mit der Option „0-mal treffen“ aus.


# 7 Gefräßigkeit (auch: Gier, greed, greedy)

**Gieriger Operator (oder alternativ Gefräßiger Operator)**  
„Gier“ (eng. greed) bedeutet, dass bei der Verwendung von **+** und ***** der gesamte Suchstring erst abgearbeitet wird und dann von hinten das letzte passende Ergebnis genommen wird.

  
Text: _vorname; name; strasse; ort_  
Suchmuster: _/ .*****; /_  
Ergebnis: _vorname; name; strasse; ort_  
Hier wirkt .***** wie ein „Gummiband“, das so lange gedehnt wird, bis ein maximaler Treffer möglich ist.

  
**Nicht-gieriger Operator**  
Man kann die gierigen Operatoren in „nicht-gierig“ verwandeln, indem ein  ? nachgestellt wird. Dann wird die kürzeste Zeichenkette gefunden. Dies wird sehr häufig verwendet (weil es normalerweise sehr sinnvoll ist).

  
Text: _vorname; name; strasse; ort_  
Suchmuster: _/ .*****?; /_  
Ergebnis: _vorname; name; strasse; ort_  
Hier wirkt .*****? wie ein „Gummiband“, das nur so lange gedehnt wird, bis ein erster, minimaler Treffer möglich ist.

  
Die Joker-Zeichen sind normalerweise nur sinnvoll in Kombination mit anderen (festen) Suchbegriffen. In den oben gezeigten Beispielen stellt das Semikolon  ; ein solches „festes Zeichen“ dar, an dem sich die Joker-Zeichen als „Gummiband“ orientieren.

  
**3. Regel:** Joker-Zeichen sollten möglichst „vorn“ und „hinten“ von „festen Suchbegriffen“ eingegrenzt werden.

  

Hinweis

Die unkontrollierte Verwendung von .* oder .+ ist ein typischer Anfängerfehler.



# 8 Markierung von Anfang und Ende

Damit wir diese 3. Regel auch auf den Textanfang und das Textende anwenden können, gibt es Zeichen für den Anfang des Suchstring bzw. deren Ende.

Der Anfang eines Textes kann gefunden werden mit **^** und das Ende mit **$**.

Text: _vorname; name; strasse; ort_  
Suchmuster: / **^.*?$** /  
Ergebnis: _vorname; name; strasse; ort_  
Dieses Suchmuster findet grundsätzlich alles von Anfang bis Ende.

  
Suchmuster: /**^\s*$**/ findet Leerzeilen.

Suchmuster: /**^#.*$**/ findet alle einzeilige Kommentarzeilen. Mit diesem Suchmuster lassen sich beispielsweise alle Kommentare einer Apache-Konfigurationsdatei löschen.

  

Aufgabe

Aufg. 15: Kommentarzeilen mit regulären Ausdrücken entfernen

Erstellen Sie eine PHP-Datei, die eine Apache-Konfigurationsdatei einliest und die Kommentarzeilen aus der Datei löscht. Schreiben Sie das Ergebnis in eine neue Datei.

  

Hinweis

Alternativ zur Markierung des Textanfangs mit ^ gibt es \A

und alternativ zu $ gibt es \z bzw. \Z.

# 9 Gefundene Stellen ersetzen

Bislang konnten wir mit [preg_replace()](http://php.net/manual/de/function.preg-replace.php) nur festgelegte Ersetzungen vornehmen. Interessant wird es nun, da _**preg_replace** ($suchmuster, $ersetzen, $text)_ auch die zuvor gefundenen Textstücke verwenden kann.

  
**Beispiel: Konvertieren des ISO Datum-Formats _yyyy-mm-dd_** in ein deutsches Datumsformat _dd.mm.yyyy_.Text: _2011-05-31_  
Suchmuster: _/(\d_{_4_}_)-(\d_{_2_}_)-(\d_{_2_}_)/_  
Ersetzen: _$3.$2.$1_  
Ergebnis: _31.05.2011_  
Jedes Teilergebnis einer runden Klammer (z.B. _**(\d**_{_**4**_}_**)**_) wird automatisch in eine Reguläre-Ausdruck-Variable geschrieben. Die erste öffnende Klammer in _$1_, die zweite öffnende Klammer in _$2_, usw..

  
Hier das Beispiel als komplettes PHP-Miniprogramm:

Code

```
<?php
 $date = '2011-05-31';
 $such = '/(\d{4})-(\d{2})-(\d{2})/';
 $ersetz = '$3.$2.$1';
 $datum = preg_replace($such, $ersetz, $date);
 print $datum;
 ?>
```

 List. 6: Konvertieren des ISO Datum-Formats yyyy-mm-dd in ein deutsches Datumsformat dd.mm.yyyy


# 10 Modifikatoren für Reguläre Ausdrücke

Hinter dem abschließenden Slash des Suchstrings kann ein sogenannter Modifikator angegeben werden.

|Modifikator|Erklärung|
|---|---|
|/ /i|Groß-/Kleinschreibung ignorieren.|
|/ /s|Single-line-Mode: Zeichenketten als eine einzige Zeile betrachten. Der Punkt-Operator gilt auch für das newline-Zeichen.|
|/ /x|Ignoriert Whitespace und erlaubt Kommentare (#). So kann bei längeren Suchmustern eine Formatierung zur besseren Lesbarkeit des Suchmusters vorgenommen werden, indem das Suchmuster über mehrere Zeilen geschrieben wird.|
|/ /u|Schaltet auf UTF-8 um, damit Umlaute und andere Buchstaben-Sonderzeichen in Mengenklammern gefunden werden. Dies ist nur notwendig, wenn UTF-8 noch nicht automatisch im System als Default vorhanden ist.|

 Tab. 45: Modifikatoren

  ---
  
**Beispiel für den Modifikator /i**  
Text: _Die Tester testen die Software_  
Suchmuster: _/(test)/ **i**_  
Ergebnis: Die Tester testen die Software  
  

Der Modifikator /_i_ ist oftmals sehr praktisch. Anstelle der Menge _/[A-Za-z]/_ kann nun _/[A-Z]/i_ geschrieben werden.

---


**Beispiel für die Formatierung mit dem Modifikator _/x_**  
Hierbei wird das Suchmuster in mehreren kommentierten Zeilen geschrieben. Dies ist für einen längeren regulären Ausdruck sehr sinnvoll!

```php
<?php
 $text = "Ich habe 122,50 € ausgegeben.";
  
 # RegExp. in einer Linie
 # $such = '/^.*?(\d{1,6},?(\d{1,2})?\s?€).*$/';

 # RegExp. mit Kommentaren und  / x
 $such   =   '/
          ^.*?          # Am Textanfang beginnen
          (             # Klammer für $1
          \d{1,6}       # 1-6 Zahlen für Eurobetrag
          ,?            # Komma für Cent-Beträge (optional)
          (\d{1,2})?    # Zwei Nachkommastellen (optional)
          \s?€          # Leerzeichen (optional) und €-Zeichen
          )             # Klammer für $1 schließen
         . *$           # bis zum Ende
           /x ';

 $ersetz = '$1';
 $b   =   preg_replace ($such,   $ersetz,   $text);
 print $b;
 ?>
```

Ausgabe:  
122,50 €


---

Aufg. 16: Reguläre Ausdrücke: Eine Rate-Mal-Übungsaufgabe

  
Was steht in $b (s. Listing) bei folgendem Text?  
_$text = "Ich habe nix ausgegeben.";_

_$b_ enthält den gesamten Text "_Ich habe nix ausgegeben._"  
Der reguläre Ausdruck trifft nicht, denn es kommt keine Zahl darin vor. Dann jedoch wird der gesamte String in die Variable _**`$b`**_ übernommen. _$b = "Ich habe nix ausgegeben_."



---

Aufg. 17: Reguläre Ausdrücke: Schwierige – aber wichtige – Übungsaufgabe

  
Was steht in _$b_ (s. Listing) bei folgendem Text?  
_$text = "Ich habe 12200000000,50 € ausgegeben.";_

- Was steht dabei in $b?
- Was ist dabei das Problem?
- Wie kann man das Problem lösen?

_$b = 000000,50 €_ und der „Rest“ steht im Ausdruck _.*?_, der auch auf den Stringanfang _Ich habe 12200_ passt.  
Das Problem ist der zu unspezifische Ausdruck am Anfang / ^ .*****? Das Problem kann man lösen, indem in **Zeile 9** ^.*****? ersetzt wird durch **^[A-Za-z\s]*?**, denn dann dürfen im ersten Textbereich keine Zahlen mehr vorkommen. Und in **Zeile 11** muss die Einschränkung auf 6 Digits entfallen, also z.B. \d{1,12}.


# 11 Mit Arrays arbeiten

Bislang war `$text`  immer als String gegeben. Sehr praktisch ist, dass `$text` auch ein Array sein kann und dass [preg_replace()](http://php.net/manual/de/function.preg-replace.php) das Array automatisch nimmt und den regulären Ausdruck auf jedes Element des Arrays anwendet.

```php
<?php
$text = ["Er hat 122,50 € auf dem Konto",
         "Er hat 122€ auf dem Konto",
         "Er hat 0,5 €",
         "Er hat 1220000000 € auf dem Konto",
         "Er hat nix",
         "Er hat ,5€"];

$such = '/^([A-Z\s]*?)(\d{1,6},?(\d{1,2})?\s?€)(.*)$/i';
$ersetz = '($1)($2)($4)';

$b = preg_replace ($such, $ersetz, $text);
foreach($b as $value){
    echo "$value <br \> ";
}
?>
```


[![RegEx-array.png](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/1/10/RegEx-array.png "RegEx-array.png")](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/1/10/RegEx-array.png)

 Abb. 75: Ergebnis

Die ersten 3 Zeilen des Ergebnisses zeigen anhand der runden Klammern, dass der reguläre Ausdruck erfolgreich durchgelaufen ist und in den Klammern finden sich die Inhalte der Variablen **$1, $2** und **$4** (**$3** ist nur eine Hilfsvariable und wurde daher nicht mit ausgegeben.

# 12 Problem Umlaute

Umlaute und reguläre Ausdrücke können ein sehr großes Problem darstellen, je nachdem mit welchem Zeichensatz das Betriebssystem arbeitet. (Ich habe leider kein Generalrezept wann es gut geht und wann nicht).

  
**Aufgabenstellung**  
Umlaute und andere Schriftzeichen im Namen sollen erlaubt sein, aber andere Sonderzeichen nicht. Unser Test-Text sei:  
_**$text = "Jörg André Meier (+#,.-)";**_  
Der Name soll gefunden werden und die Sonderzeichen in der Klammer sollen gelöscht werden. Im folgenden Sourcecode sehen Sie drei Ansätze.


```php
<?php
 $text = "Jörg André Meier (+#,.-)";

 # Alles finden – nur zur Kontrolle
 $such1 = '/^.*$/';
 preg_match_all($such1,   $text,   $treffer);
 print_r($treffer);
 echo "<hr \>";

 # Mit \w arbeiten
 $such2 = '/[\w\s]+/';
 preg_match_all($such2,   $text,   $treffer);
 print_r($treffer);
 echo "<hr \>";

 # Sonderzeichen einzeln angeben
 $such3  = '/[a-zäöü\s]+/i';
 preg_match_all($such3,   $text,   $treffer);
 print_r($treffer);
 echo "<hr \>";
 ?>
```


- **In Zeile 5:** _/^.*$/_ ist alles erlaubt. Dies dient nur zur Kontrolle des Scripts.

- **In Zeile 11:** _/[\w\s]+/_ klappt es je nach Betriebssystem und Spracheinstellung, da \w definiert ist als Menge der alphanumerischen Zeichen.

- **In Zeile 17:** _/[a-zäöü\s]+/i_ funktioniert es nur teilweise. Im Internet und in Büchern wird empfohlen in die Menge [a-z] die Umlaute mit aufzunehmen. Davon möchte ich abraten, denn viel zu viele Schriftzeichen werden dann nicht erlaubt. Eine weitere, oft vorkommende Empfehlung lautet die verbotenen Zeichen auszuschließen. Auch dies ist sehr kritisch, da zu leicht Sonderzeichen übersehen werden, die z.B. hexadezimal codiert sein können.

Wenn es mit den Umlauten nicht wie in Zeile 11 klappt, dann sollten Sie den Modifierer **u** verwenden. Dieser Modifierer schaltet **UTF-8** an. Der reguläre Ausdruck sollte dann wie folgt aussehen: _$such2 = '/[\w\s]+/**u**';_

- Weitere Hinweise zu dem Modifier **u** finden Sie unter [https://www.regular-expressions.info/unicode.html](https://www.regular-expressions.info/unicode.html)
- Weitere Hinweise zu allen Modifiern finden Sie unter [http://php.net/manual/de/reference.pcre.pattern.modifiers.php](http://php.net/manual/de/reference.pcre.pattern.modifiers.php)


# 13 Zusammenfassung der Syntax

In der Tabelle wird die bisherige Syntax zusammengefasst dargestellt. Es handelt sich hierbei um einen Ausschnitt aus einer weit umfangreicheren Syntax.  
  

|Sonderzeichen|Erklärung|
|---|---|
|( )|Gruppiert die Elemente zu einem einzigen Element. Es muss eine Übereinstimmung in der Reihenfolge mit allen Elementen vorliegen, z.B. (_tee_).|
|(...\|...\|...)|tea\|te)_._|
|[ ]|Bezeichnet eine Klasse von Elementen, die erkannt werden sollen. Es muss eine Übereinstimmung mit nur einem der Elemente vorliegen, z.B. _[0-9]_.<br><br>Sonderzeichen der Mengenklammer sind _[^ - / \]_, alle anderen Zeichen haben keine Sonderfunktion.|
|[^ ]|Bezeichnet eine negierte Klasse von Elementen. Das Zeichen _^_ negiert die gesamte Klasse.<br><br>Anmerkung: Der Operator gilt für die Negation nur in der Mengenklammer _[ ]_, z.B. _[^0-9]_.|
|_\d_ bzw. Negation _\D_|Digit (entsprechend _[0-9]_) bzw. nicht Digit (entsprechend _[^0-9]_).|
|\w bzw. Negation \W|Alphanumerische Zeichen (Wort) entsprechend _[a-zA-Z0-9_]_ bzw. nicht alphanumerische Zeichen entsprechend _[^a-zA-Z0-9_]_.|
|_\s_ bzw. Negation _\S_|Whitespace (Leerzeichen und Tabulator) bzw. nicht whitespace.|
|_\b_ bzw. Negation _\B_|Wortgrenze (_b_ = boundary) bzw. nicht Wortgrenze.<br><br>Bei der Wortgrenze handelt es sich nicht um ein eigenes Zeichen, sondern nur um eine Markierung. Eine Wortgrenze ist definiert als Übergang zwischen einem \W-Zeichen und einem \w-Zeichen (also vor einem \w-Zeichen oder hinter einem \w-Zeichen).|
|.|Der „Punkt“ steht für ein beliebiges Zeichen (Ausnahme: Zeilenumbruch Newline).|
|{n,m}|Wiederholungsintervall (gierig).  <br>{n} genau n-mal  <br>{n,} mindestens n-mal  <br>{,m} maximal m-mal  <br>{n,m} mindestens n-mal und maximal m-mal|
|{n,m}?|Wiederholungsintervall (nicht-gierig).|
|?|Das vorstehende Zeichen 0 oder 1-mal (gierig).|
|+|Das vorstehende Zeichen 1-mal oder beliebig oft (gierig).|
|*|Das vorstehende Zeichen 0-mal oder beliebig oft (gierig).|
|??|Das vorstehende Zeichen 0 oder 1-mal (nicht-gierig).|
|+?|Das vorstehende Zeichen 1-mal oder beliebig oft (nicht-gierig).|
|*?|Das vorstehende Zeichen 0-mal oder beliebig oft (nicht-gierig).|
|^|Markiert, dass der Suchausdruck am Anfang stehen muss. Im Mehrzeilenmodus wird auch jedes Newline-Zeichen erkannt.|
|$|Erkennt das Zeilenende bzw. das Zeichen unmittelbar vor dem letzten Newline-Zeichen.|
|/ /i|Modifikator: Groß-/Kleinschreibung ignorieren.|
|/ /s|Modifikator: Single-line-Mode: Zeichenketten als eine einzige Zeile betrachten. Der Punkt-Operator gilt auch für das Newline-Zeichen.|
|/ /x|Modifikator: Ignoriert Whitespace und erlaubt Kommentare ( #). So kann bei längeren Suchmustern eine Formatierung zur besseren Lesbarkeit des Suchmusters vorgenommen werden, indem das Suchmuster über mehrere Zeilen geschrieben wird.|

 Tab. 46: Syntax regulärer Ausdrücke für PHP

  
Wer sich mehr mit der Syntax beschäftigen möchte:

- [Wikibooks](https://de.wikibooks.org/wiki/Websiteentwicklung:_PHP:_Regul%C3%A4re_Ausdr%C3%BCcke)
- [http://regexp-evaluator.de/tutorial/](http://regexp-evaluator.de/tutorial/)
- Sehr viele, professionelle Beispiele finden sind im Buch:  
    Goyvaerts, Jan; Levithan, Steven: Reguläre Ausdrücke Kochbuch. [detaillierte Lösungen für acht Programmiersprachen; mit Einstiegs-Tutorial]. O'Reilly Verlag.
- Stubblebine, Tony; Klicman, Peter; Schulten, Lars: Reguläre Ausdrücke. Kurz & gut. O'Reilly Verlag.

Und wer reguläre Ausdrücke aus Sicht der theoretischen Informatik kennen lernen möchte, der möge sich das folgende Video ansehen ;-)  
[https://www.youtube.com/watch?v=d_Rc4-1Pzbc](https://www.youtube.com/watch?v=d_Rc4-1Pzbc).



