
# 1 PHP-Konventionen

Codekonventionen sind für Unternehmen und Entwickler aus verschiedenen Gründen wichtig:

- 40%-80% der Lebenszykluskosten einer Software gehen in die Wartung.
- Kaum eine Software wird vom Originalautor ein Leben lang gewartet.
- Codekonventionen verbessern die Lesbarkeit der Software und ermöglichen es Entwicklern, neuen Sourcecode schneller und gründlicher zu verstehen.
- Sourcecode wird normalerweise im Team entwickelt. Codekonventionen führen dazu, dass der Sourcecode dann über die verschiedenen Bereiche lesbar bleibt.

![](images/Pasted%20image%2020250419171028.png)

**Kontrollstrukturen (z.B.: _if_-Bedingungen, _while_-, _for-_ und _foreach_-Schleifen usw.)**  
Zwischen dem Schlüsselwort und der ersten Klammer sollte ein Leerzeichen stehen, um sie von Funktionsaufrufen zu unterscheiden, und die geschweiften Klammern sollten stets gesetzt werden, selbst wenn ihre Verwendungen optional sind (wenn nur ein Befehl in ihnen steht).

```
if ((Bedingung 1) || (Bedingung 2)) {
    Ausdruck 1
} else {
    Ausdruck 2
}
```


**Funktionsaufrufe & Variablenzuweisung**  
Zwischen dem Funktionsnamen und der ersten Klammer sollte kein Leerzeichen eingefügt werden, ebenso wird zwischen der Klammer und dem ersten Parameter kein Leerzeichen verwendet. Bei mehreren Parametern steht hinter jedem Komma ein Leerzeichen.  
Bei der Zuweisung einer Variablen sollte vor und hinter dem Gleichheitszeichen jeweils ein Leerzeichen stehen, wobei die Gleichheitszeichen bei mehreren untereinander stehenden Zuweisungen eingerückt werden können.

```
$variable1 = function1($par1, $par2, $par3);
$variable2 = function2($par4, $par5);
```

**Funktionsdefinitionen**  
Auch hier gilt anders als bei Kontrollstrukturen, dass zwischen dem Funktionsnamen und der ersten Klammer kein Leerzeichen eingefügt werden sollte, ebenso wird zwischen der Klammer und dem ersten Parameter kein Leerzeichen verwendet. Ebenfalls anders als bei Kontrollstrukturen sollten geschweifte Klammern immer in die nächste Zeile gesetzt werden und nicht hinter dem Funktionsnamen. Übergabeparameter mit einem Standardwert stehen am Ende der Parameterliste. Wenn möglich, sollte ein Rückgabewert mit return definiert sein.

```
function functionName($par1, $par2, $par3 = "standard")
{
    //Irgendwas
    return true;
}
```


# 2 Namenskonventionen

Folgende Namenskonventionen sollten eingehalten werden:

- **Variablen** beginnen mit einem klein geschriebenen Buchstaben, jedes weitere Wort mit einem Großbuchstaben. Für ein leichtes "Herunterlesen" des Codes, sollten Variablen aussagekräftig nach ihrem jeweiligen Zweck benannt werden, beispielsweise _**$name**_. Einer Variable wird ein Wert (Zahl, Text) nach einem Gleichheitszeichen zugewiesen, der später erneut überschrieben werden kann. Beispiele: _**$pizzaTyp = "Salami"; $pizzaAnzahl = 2; $pizzaPreis = 9.50;**_ Die Ausgabe erfolgt durch echo.
- **Klassen** sollten immer mit einem Großbuchstaben beginnen und einen aussagekräftigen Namen besitzen – z.B. _**HTMLCleaner**_. Unbedingt zu beachten ist, dass Verben niemals am Anfang eines Klassennamens stehen sollten.  
- **Methoden und Funktionen** werden stets klein geschrieben und jedes weitere Wort beginnt mit einem Großbuchstaben (dies wird auch „Kamel-Notation“ genannt) – z.B. _**getUser()**_. Hierbei sollten Funktionen stets ausdrücken, was sie im Programm ausführen.  
- **Konstanten** bestehen ausschließlich aus Großbuchstaben – z.B. _**HOST**_;


# 3 Kommentare

In PHP gibt es unterschiedliche Arten von Kommentaren. Hier folgt eine Übersicht.

**Einfache Kommentare**  
- Für einzeilige Kommentare: // ... (siehe **Zeile 1**)
- Mehrzeilige Kommentare verwendet man /* ... */ (siehe **Zeile 10-13**).

```php
// Funktion für Formularfelder
function createFormInput()
{
    echo "Name:       <input type='text' name='nachname'></br>
          Vorname:    <input type='text' name='vorname'></br>
          Matr.-Nr.:  <input type='text' name='matrnr'></br>";
}


/* Eine Funktion, die ein Formular erstellt, innerhalb dessen man
 * die Möglichkeit hat, Eingaben für Name, Vorname und Matrikel-Nr.
 * zu tätigen
 */
function createFormInput()
{
    echo "Name:       <input type='text' name='nachname'></br>
          Vorname:    <input type='text' name='vorname'></br>
          Matr.-Nr.:  <input type='text' name='matrnr'></br>";
}
```


**DocBlock**  
Ein _DocBlock_ ist ein strukturierter Kommentar _/** ... */_ und dient der Beschreibung aller Funktionen und Methoden. Diese Syntax kann mit Programmen (z.B. [[PHPDocumentor](https://phpdoc.org/) ]) automatisiert ausgelesen werden, sodass klar wird, welche Parameter übergeben werden müssen und welches Format der Rückgabewert hat.
- **@param** beschreibt die Eingabeparameter (in der Reihenfolge der Nennung).
- **@return** beschreibt die Rückgabe an das Hauptprogramm

```php
/**
 * Funktion addiert zwei Werte
 * @param float $firstValue    Erster Wert
 * @param float $secondValue   Zweiter Wert
 * @return float               Rückgabe des Ergebnisses
 */
function addValues($firstValue, $secondValue)
{
    return $firstValue + $secondValue;
}
```


**Kommentarheader**  
**Jede (!)** Datei beginnt in der zweiten Zeile mit Kommentarzeilen (= Kommentarheader oder Programmheader), der im Stil des _DocBlock_ geschrieben werden muss.

- **@author** Angabe des Autors der Datei mit Angabe einer E-Mail-Adresse
- **@since** beschreibt was ab welcher Version neu ist


```php
<?php
/**
 * Datei zu Aufgabe 1
 *
 * @author       Jörg Thomaschewski <jt@imut.de>
 * @since 2.0    englische Namen für Variablen eingeführt
 * @since 2.1    kleine Verbesserungen
 */

...
```
