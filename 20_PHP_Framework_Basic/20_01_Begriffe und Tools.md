

# 1 **Composer**  
Der Composer ist ein **Paketmanager für PHP**, ähnlich dem Linux-Paketmanager _`apt-get`_, den Sie vielleicht auf Linux schon mit _`apt-get install name-des-Softwarepakets`_ schon verwendet haben (andere Linux-Paketmanager sind z.B. _npm_ oder _gem_).

Mit einem Paketmanager kann ein Softwarepaket automatisch installiert werden. Hierzu wird in der Kommandozeile der Befehl ausgeführt und somit das Paket und ggf. weitere notwendige Pakete installiert.

Der Paketmanager **Composer** muss aber natürlich zuerst selbst installiert werden. Die Nutzung von _Composer_ ist sehr einfach.

- [Erklärung auf Wikipedia zu Composer](https://de.wikipedia.org/wiki/Composer_\(Paketverwaltung\))
- [Link zur Homepage getcomposer.org](https://getcomposer.org/)



# 2 **Twig**  

Twig ist eine **Template-Engine** für PHP. Wenn wir eine HTML-Anwendung erstellen, dann gibt es immer HTML-Bereiche und Bereiche in denen PHP-Funktionalitäten genutzt werden (z.B. um eine Tabelle zu füllen oder um einen Artikel aus der Datenbank einzufügen). Die reinen HTML-Bereiche haben wir bislang sehr gering gehalten und mittels _echo_ HTML erzeugt, mit der Konsequenz, dass alle bisherigen Beispiele dieses Moduls Internetserver-Programmierung wenig ansprechend ausgesehen haben.

Eine gut gestaltete Website, die auf vielen Endgeräten nutzbar ist, hat aber sehr umfangreiche reine HTML-Bereiche (inklusive CSS und JavaScript), deren Ausgabe mit _echo_ nicht sinnvoll ist.

Das Ziel der Template-Engine Twig ist die übersichtliche Trennung von umfangreichem HTML und sehr mächtiger PHP-Programmierung. Es wird also ein übersichtliches Template erstellt und genau angegeben, an welchen Stellen HTML-Bereiche importiert werden und an welchen Stellen PHP genutzt wird.

当我们创建一个 HTML 应用程序时，页面中总会同时包含纯 HTML 的部分和需要使用 PHP 功能的部分（例如，用来填充表格或从数据库中插入一篇文章）。

到目前为止，我们几乎没有使用纯 HTML 部分，而是通过 `echo` 语句来生成 HTML。这种做法的结果是：我们在本模块“Internet服务器编程”中的所有示例看起来都不太美观。

然而，一个设计良好的网站，尤其是在多个设备上都能正常显示的网站，通常会包含大量的纯 HTML 内容（包括 CSS 和 JavaScript）。而这些内容如果用 `echo` 来输出是非常不合理的。

Twig 模板引擎的目标就是：**将大段的 HTML 与功能强大的 PHP 编程清晰地分离开来**。  
也就是说，我们可以创建一个结构清晰的模板，并明确指出哪些位置导入 HTML 内容，哪些位置使用 PHP 逻辑。这样代码就更容易维护，也更容易设计美观的页面。






Hier ein Beispiel von [https://twig.symfony.com/doc/3.x/templates.html](https://twig.symfony.com/doc/3.x/templates.html):

```html
<!DOCTYPE html>
<html>
    <head>
        <title>My Webpage</title>
    </head>
    <body>
        <ul id="navigation">
        {% for item in navigation %}
            <li><a href="{{ item.href }}">{{ item.caption }}</a></li>
        {% endfor %}
        </ul>

        <h1>My Webpage</h1>
        {{ a_variable }}
    </body>
</html>
```
Die Verwendung von Twig erinnert mich sehr an eine Pseudo-Programmiersprache

- [Erklärung auf Wikipedia zu Twig](https://de.wikipedia.org/wiki/Twig_\(Template-Engine\))
- [Link zur Homepage twig.symfony.com](https://twig.symfony.com/)


# 3 **Doctrine**  

Doctrine ist ein **Framework zur Anbindung einer Datenbank** und bietet einen "database abstraction layer" für ein "object-relational mapping (ORM)". Ein erstes, sehr rudimentäres "object-relational mapping (ORM)" haben wir bereits im Unterkapitel [Datenbankverbindung professionell](https://isp.eduloop.de/loop/Datenbankverbindung_professionell "Datenbankverbindung professionell") im untersten Beispiel durchgeführt. Dort hatten wir z.B. mit _$row->firstName_ einen Datenbankeintrag angesprochen als wäre es eine Eigenschaft eines Objekts.

Doctine ist sehr mächtig und verwendet statt SQL die eigene Doctrine Query Language (DQL).

- [Erklärung auf Wikipedia zu Doctrine](https://de.wikipedia.org/wiki/Doctrine_\(PHP\))
- [Link zur Homepage www.doctrine-project.org](https://www.doctrine-project.org/)

