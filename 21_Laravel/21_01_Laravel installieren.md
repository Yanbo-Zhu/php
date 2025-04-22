
Bevor wir mit Laravel beginnen, bitte den Composer installieren von [https://getcomposer.org/](https://getcomposer.org/) (bei Windows Neustart erforderlich) und mit _**C:\xampp\htdocs>composer -V**_ ausprobieren, ob die Installation erfolgreich war.

# 1 步骤

Das nachfolgende Beispiel wurde unter Windows 10 (mit zuvor installiertem XAMPP) in der Kommandozeile von PHPStorm durchgeführt.


- Nachsehen, ob _PHP_ installiert ist
    - C:\xampp\htdocs>php -v
- Nachsehen, ob _Composer_ installiert ist
    - C:\xampp\htdocs>composer -V
- Laravel installieren mit
    - C:\xampp\htdocs>composer global require laravel/installer
- Nachsehen, ob der _Laravel-Installer_ installiert ist
    - C:\xampp\htdocs>laravel -V
- Ein leeres Laravel-Projekt installieren
    - C:\xampp\htdocs>laravel new freshproject
    - [![Laravel1.png](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/d/df/Laravel1.png "Laravel1.png")](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/d/df/Laravel1.png)
- In das Projektverzeichnis wechseln
    - C:\xampp\htdocs>cd freshproject
- Den für Laravel zuständigen Webserver starten
    - C:\xampp\htdocs\freshproject>php artisan serve
    - Der Webserver kann mit _Strg + c_ beendet werden.


Unter [http://http://127.0.0.1:8000/](http://http//127.0.0.1:8000/) sollte nun folgende Seite erscheinen

[![Laravel10.png](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/thumb/5/5b/Laravel10.png/600px-Laravel10.png)](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/5/5b/Laravel10.png)





