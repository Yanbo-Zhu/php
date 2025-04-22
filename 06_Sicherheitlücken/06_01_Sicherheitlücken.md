
# 1  Funktionsweise einer Web-Anwendung

Früher gab es eine strickte Trennung zwischen der Client- und der Serverseite. Auf der Clientseite werden Daten dargestellt und auf der Serverseite befindet sich die Anwendungslogik. Durch Parametermanipulationen können Anwendungen gezwungen werden, Operationen auszuführen, die nicht vorgesehen waren und dadurch einen Schaden anrichten.

Durch den Einsatz von clientseitigen Datenverarbeitungen, wie Javascript und Ajax, vergrößert sich das Sicherheitsrisiko zusätzlich.

**Gefahren durch Parametermanipulationen**
Parameter = Argumente, die einer Anwendungslogik übergeben werden um eine Webanwendung zu „steuern“.

Paramenter können hierbei sein
- Cookie-Daten
- POST-Daten
- GET-Daten



Parametermanipulation = gezielte Übergabe von unerwarteten Parametern um die Arbeitsweise einer Webanwendung zu verändern oder zu beschädigen.

Um eine Webanwendung zu manipulieren kann als Parameter folgendes übergeben werden:
- Unerwartete Werte
- Unerwartete Datentypen
- Unerwartete Parameter
- Unerwartete Längen (Buffer Overflow)


# 2 CSRF-Attacken

Cross-Site Request Forgery bezeichnet alle Angriffe bei denen Daten mittels einer HTTP-Anfrage manipuliert werden. Dabei muss das Opfer ein privilegierter Benutzer auf einer Webseite sein und gewisse Rechte haben (eingeloggt sein).  
Sollte das Opfer beispielsweise als Administrator eingeloggt sein und wird von einem Angreifer folgender Link im Kontext des Opfer-Browsers ausgeführt, so hätte der Angreifer es geschafft einen neuen Benutzer anzulegen.



Diese Links könnten sich z.B. hinter einer harmlosen Grafik verstecken. Beispielsweise kann es passieren, dass man diese Operation ausführt, in dem man auf ein „Fenster schließen“-Link eines [Popup-Fensters](https://isp.eduloop.de/loop/Popup-Fensters "Popup-Fensters") klickt. Im folgenden harmlosen Beispiel wird man auf der Seite [www.wikipedia.org](https://www.wikipedia.org/) abgemeldet. Der Link wird beim Anvisieren in der Statusleiste angezeigt, doch wenn man anstatt eines Links ein Button verwendet, so wird die CSRF-Attacke nicht vorher sichtbar.


**Funktionsweise**  
Damit der Angreifer eine CSRF-Attacke ausführen kann, muss der Browser des Opfers dazu gebracht werden, einen manipulierten HTTP-Request auszuführen. Dazu gibt es drei Möglichkeiten:

- Cross Site Scripting/XSS (s. Kapitel: Cross Site Scripting/XSS)
- Unterschieben einer [URL](https://isp.eduloop.de/loop/URL "URL") (z.B. ein versteckter Link unter einer Grafik)
- [Local Exploit](https://isp.eduloop.de/loop/Local_Exploit "Local Exploit") (z.B. eine Schadsoftware lokal auf einem Rechner)

  
**Abwehrmaßnahmen serverseitig**

- Alle Requests mit [Shared Secret](https://isp.eduloop.de/loop/Shared_Secret "Shared Secret") versehen

  
**Abwehrmaßnahmen clientseitig**

- Sicherstellung, dass das lokale System virenfrei ist
- Deaktivierung von [Javascript](https://isp.eduloop.de/mediawiki/index.php?title=Javascript&action=edit&redlink=1 "Javascript (Seite nicht vorhanden)")
- Nur vertrauenswürdigen Quellen glauben (Zertifikate)

  
**Nutzlose Maßnahmen**

- Requests über HTTP-Post



## 2.1 Beispiel CSRF in einem Popup-Fenster

Quellcode des Popup-Fensters.
```
<html>
<head>
<title>Warnung</title>
<meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1">
</head>

<body>
<table width="100%" border="0" cellspacing="0" cellpadding="0">
<tr>
<td width="21%"><img src="virus.jpg" width="300" height="430"></td>
<td width="79%">
<table width="100%" border="0" cellspacing="0" cellpadding="0">
<tr>
<td>Sie sind Opfer eines Hacker-Angriffs geworden!<br>
Den Virus konnten wir f&uuml;r Sie vernichten.</td>
</tr>
<tr>
<td><div align="right"><a href="http://de.wikipedia.org/w/index.php?title=Spezial:Userlogout">Fenster schlie&szlig;en</a> </div></td>
</tr>
</table></td>
</tr>
</table>
</body>
</html>
```



# 3 Cross Site Scripting/XSS


Cross-Site Scripting (XSS) bezeichnet das Ausnutzen einer Computersicherheitslücke, indem Informationen aus einem Kontext, in dem sie nicht vertrauenswürdig sind, in einen anderen Kontext eingefügt werden, in dem sie als vertrauenswürdig eingestuft sind. Aus diesem vertrauenswürdigen Kontext kann dann ein Angriff gestartet werden.

Cross-Site Scripting（缩写为 XSS，跨站脚本攻击）是一种利用计算机安全漏洞的攻击方式。

它的核心思想是：**将不受信任的数据从一个上下文中插入到另一个被认为是“可信”的上下文中**，从而发动攻击。

举个例子来说明：
1. 假设一个网站允许用户在网页上发布留言或评论。
2. 如果这个网站没有对用户输入的内容进行过滤或转义，攻击者就可以提交一段包含 JavaScript 脚本的内容。
3. 这些脚本会被原样保存在网页中，当其他用户访问这条留言时，浏览器会**信任**网页内容并执行那段恶意脚本。
4. 脚本可能会窃取用户的 Cookie、伪造表单提交、跳转到钓鱼网站等。

XSS 是指**将恶意代码注入网页中，让其他用户在毫无防备的情况下执行它**，因为这些代码来自被浏览器“信任”的上下文（比如你自己的网站），攻击就成功了。

为了防止 XSS，开发者需要：
- 对所有用户输入进行转义或过滤
- 使用安全的框架（如 Twig）自动转义输出
- 设置合适的 Content Security Policy (CSP) 等安全措施


**Funktionsweise**  
Grundsätzlich kann ein [XSS](https://isp.eduloop.de/loop/XSS "XSS")-Angriff serverseitig oder clientseitig durchgeführt werden. In beiden Fällen werden Operationen oder Daten übergeben, die nicht vorgesehen waren und daher meist schädlicher Natur sind. Bei beiden Angriffsmethoden liegt die Schwachstelle in der Web-Anwendung. Der Programmierer muss möglichst alle Angriffsmöglichkeiten im Hinterkopf behalten und dagegen Vorkehrungen treffen.

**Variante 1 – serverseitiger Angriff**
- Ausführung von Code auf dem Server (z.B. durch PHP-Include)
- Einbindung der Dateien von anderen Rechnern
- Ausführung von Programmen über [Shell](https://isp.eduloop.de/loop/Shell "Shell")

  

**Variante 2 – clientseitiger Angriff**
- Ausführung des Codes clientseitig durch einen versteckten Link (Webbrowser, E-Mail-Programm)
- Übergabe an Parametern an ein CGI-Script einer Web-Anwendung


---

Beispiel 
`Username: <script>alert("test");</script>`

  
In dem Beispiel wird anstatt eines Usernamen als ASCII-Zeichenfolge ein Javascript-Code übergeben. Dieser wird im Browser ausgeführt und als ein Alarmfenster angezeigt.

**Schlussfolgerung für den Serverbetreiber**
- Alle eingehende Parameter als unsicher betrachten
- Alle Daten, die vom Client kommen, sind potentiell verseucht

**Abwehrmaßnahmen serverseitig**
- Übersetzen der Steuerzeichen „_<>_“ und Tags wie „`<script>`“ in HTML
- Bei der Nutzung von PHP mit _htmlspecialchars()_ arbeiten
- selektive Tag-Filterung (umfangreich)

  
**Abwehrmaßnahmen clientseitig**
- Sicherstellung, dass das lokale System virenfrei ist
- Deaktivierung von [Javascript](https://isp.eduloop.de/mediawiki/index.php?title=Javascript&action=edit&redlink=1 "Javascript (Seite nicht vorhanden)")

# 4 HTTP Response Splitting

Das HTTP Response Splitting ist eine Sicherheitslücke, die zur Durchführung von Cross Site Scripting Attacken verwendet werden kann. Dabei wird Code per POST oder GET an den Server gesendet, der diesen Code ungeprüft in den Antwort-Header ausgibt. Z.B. gibt der folgende Code alle Daten einfach im Header-Bereich wieder aus:

HTTP Response Splitting 是一种安全漏洞，可以被用来发起 Cross-Site Scripting（跨站脚本）攻击。
其基本原理是：**攻击者通过 POST 或 GET 请求向服务器发送恶意代码，而服务器没有对这些输入进行检查，就直接将其内容输出到了 HTTP 响应头中**。这样，攻击者可以操控响应头并注入恶意内容。


---

Beispiel

服务器中有一段代码
`<?php header("Location: /login.php?action=" .$_GET['action']); ?>`
这段代码的意思是：从 URL 参数中获取 `action`，然后把它拼接进跳转地址中。  
如果用户访问这个地址： /vulnerable.php?action=login
那么页面会跳转到：   /login.php?action=login


但如果攻击者传入如下内容：
`/vulnerable.php?action=login%0D%0AContent-Length:%200%0D%0A%0D%0A<script>alert('XSS')</script>`

其中 `%0D%0A` 是 HTTP 协议中的换行符。服务器会把这些内容原样写入响应头中，导致：
- 响应头被分割
- 后面的 JavaScript 被浏览器当作正文内容执行
- 实现了 XSS 攻击


---


Durch mehrere Zeilenumbrüche kann ein Angreifer eine Aufsplittung der Antwort erzwingen. Somit werden aus der ursprünglichen Antwort zwei. Die zweite Antwort wird dabei vom Client nur verabreitet, wenn die selbe TCP-Verbindung wieder benutzt wird. Die zweite Antwort kann dabei beliebigen Inhalt haben, den der Angreifer festlegt. 

Verändert der Angreifer noch zusätzlich die Header für das Zwischenspeichern z.B. auf einem WebProxy, können diese Antworten auch an andere Clients gesendet werden, die den selben WebProxy nutzen (sog. Cache Poisoning, dt.: Cache-Vergiftung).

通过多个换行符，攻击者可以强制服务器将 HTTP 响应「拆分」成两个部分。也就是说：
- 原本的一次 HTTP 响应被**分割成了两次响应**；
- 如果客户端（如浏览器）**继续使用同一个 TCP 连接**，那么这第二个伪造的响应也会被处理；
- 这个第二个响应的内容**完全由攻击者控制**，可以嵌入恶意的 HTML、JavaScript 或伪造的页面内容。


更严重的是：
如果攻击者还进一步修改了 HTTP 响应中的缓存控制头部（例如设置为 `Cache-Control: public`），并且请求经过了**中间代理服务器（如 Web Proxy）**，那么：
- 这个被攻击者伪造的响应可能会被 **缓存**；
- 使用相同代理的 **其他用户** 也可能从缓存中拿到这份伪造响应，而不是原本的真实响应；
- 这就形成了所谓的 **Cache Poisoning（缓存投毒 / 缓存污染）** 攻击。


---

  
**Abwehrmaßnahmen serverseitig**

- Alle Daten überprüfen, die in den Header geschrieben werden.


# 5 Shell Command Injektion

Bei dieser Angriffsmethode greift man über eine Parameterübergabe direkt auf die [Shell](https://isp.eduloop.de/loop/Shell "Shell") des Servers. Wenn dazu auch noch root-Rechte bestehen kann mit dem Server und den enthaltenen Daten alles Mögliche gemacht werden.

In PHP erlauben folgende Methoden die Ausführung von Shell-Kommandos:

- shell_exec()
- system()
- passthru()
- exec()
- proc_open()
- popen()

---

Beispiel 
1 
`<?php system("convert ".$_GET['bild'].".jpg ".$_GET['bild'].".png"); ?>`
**Problem**  
Der Parameter „_bild_“ wird ungeprüft in den [Shell](https://isp.eduloop.de/loop/Shell "Shell")-Befehl eingefügt. Jetzt ist es möglich ein beliebiges Kommando durch das verwenden eines Metazeichens auszuführen.

`bild=;touch /tmp/i-was-here;`

---


**Abwehrmaßnahmen serverseitig**
- auf externe Programme verzichten, sonst ohne Shell starten
- Shell-Metazeichen behandeln
- Validieren und überarbeiten von Parameter-Daten z.B. mit _„[escapeshellarg()](https://isp.eduloop.de/loop/Escapeshellarg\(\) "Escapeshellarg()")“_

**Abwehrmaßnahmen clientseitig**
- Sicherstellung, dass das lokale System virenfrei ist
- Verzicht auf Cookies und Session-IDs
- Deaktivierung von [Javascript](https://isp.eduloop.de/mediawiki/index.php?title=Javascript&action=edit&redlink=1 "Javascript (Seite nicht vorhanden)")




# 6 SQL Injection

SQL-Injection ist das Ausnutzen einer Sicherheitslücke bei der Benutzung einer Datenbank. Aufgrund mangelnder Überprüfung der Parameter, die an die Datenbank weitergeleitet werden, kann ein Angreifer über die Anwendung eigene SQL-Befehle einschleusen.  
  

Verwundbar sind generell alle Parameter, auf die der Angreifer Zugriff hat. Dies können POST- und auch GET-Parameter sein. Im folgenden Beispiel wird ein GET-Parameter dahingehend manipuliert, dass er durch einen SQL-Befehl ersetzt wird.  
  

Beispiel: 
Bei einer Übergabe von Parametern an den Server, können zusätzliche, oft unerwünschte Informationen übergeben werden. Im folgendem Beispiel wird die _ID= 42_ übergeben. Daraus wird der entsprechende SQL-String generiert.

```
Erwarteter Parameter:

http://webserver/cgi-bin/find.cgi?ID= 42
ergibt:

SELECT author, subjekt, text FROM artikel WHERE ID= 42

SQL-Injection:

http://webserver/cgi-bin/finduser.cgi?
ID= 42 +UNION+SELECT+login,+password,+'x'+FROM+user
ergibt:

SELECT author, subjekt, text FROM artikel WHERE 
ID= 42  UNION SELECT login, password, 'x' FROM user
```

Durch Manipulation des GET-Parameters, wird die im Skript generierte SQL-Anfrage so manipuliert, dass sie die vom Angreifer gewünschten Daten aus der Datenbank ausliest.


## 6.1 **Abwehrmaßnahmen serverseitig**
- Neutralisierung von SQL-Metazeichen (z.B. [Escaping](https://isp.eduloop.de/loop/Escaping "Escaping"))
- [Prepared Statements](https://isp.eduloop.de/loop/Prepared_Statements "Prepared Statements") („Abfrage-Templates“ werden zur Laufzeit an DB gesendet, weitere Parameter werden danach verworfen).
- Gutes Datenbank-Design (Auslagerung von sensiblen Daten in separate Tabellen)
- Verschlüsselung von sensiblen Daten (Passwörter etc.) in der Datenbank.


**Standard-Abfrage:**
```
$abfrage = "SELECT spalte1 FROM tabelle WHERE spalte2 = 
'".$_POST['spalte2Wert']."'";
$query = mysql_query($abfrage) or die("Datenbankabfrage ist 
fehlgeschlagen!");
```



**Escaping:**
Bei der Neutralisierung werden gefährliche Zeichen wie `'` (einfaches Anführungszeichen) **automatisch entschärft** – z. B. durch `\'` – oder die Werte werden **sicher eingebunden**.

mysql_real_escape_string(...): 把用户输入中所有**对 SQL 有特殊含义的字符（如 `'`, `"`, `\`, `NULL`）进行转义**，防止 SQL 注入。`


```
$abfrage = "SELECT spalte1 FROM tabelle WHERE spalte2 = 
'".mysql_real_escape_string($_POST['spalte2Wert'])."'";
$query = mysql_query($abfrage) or die("Datenbankabfrage ist 
fehlgeschlagen!");
```




**Prepared Statements:**
Der Datenbanktreiber kümmert sich hier automatisch um das Escaping und schützt vor SQL-Injection.
```
$stmt = $dbh->prepare("INSERT INTO REGISTRY (name, value) 
VALUES (:name,:value)");
$stmt->bindParam(':name', $name); 
$stmt->bindParam(':value', $value);
```

