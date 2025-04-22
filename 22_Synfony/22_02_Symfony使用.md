
# 1 **Installation eines "leeren" Symfony-Projekts**  


Jedes Tutorial und jedes Symfony-Beispiel beginnt mit der Installation eines "leeren" Symfony-Projekts. Man muss sich bei der Installation festlegen, ob die ganzen Zusatzmodule mitinstalliert werden sollen (dies mach das "leere" Symfony-Projekt bereits am Anfang sehr umfangreich) oder ob man mit einem Basisprojekt beginnt (dies wird empfohlen) und dann die benötigten Module nachinstalliert.

Wichtig ist zu wissen, **dass bei der Installation ein Unterverzeichnis (mit dem angegebenen Projektnamen) erstellt wird**. Daher ist es gut, wenn Sie die Kommandos aus dem DocumentRoot des Webservers ausführen, also z.B. aus _C:\xampp\htdocs_

Installation des "leeren" Symfony-Projekts mit Zusatzmodulen:  

Beide Arten der Installation sind gleich:  
(a) _C:\xampp\htdocs>symfony new MeinProjektName --full_ oder  
(b) _C:\xampp\htdocs>composer create-project symfony/website-skeleton MeinProjektName_.

Installation des "leeren" Symfony-Projekts ohne Zusatzmodule **(empfohlen)**:  

Beide Arten der Installation sind gleich:  
(a) _C:\xampp\htdocs>symfony new MeinProjektName_ oder  
(b) _C:\xampp\htdocs>composer create-project symfony/skeleton MeinProjektName_.

Nach der Installation in das Verzeichnis wechseln, also _C:\xampp\htdocs>cd MeinProjektName_. Anschließend den Webserver starten. Auch hierfür gibt es zwei in den Tutorial gezeigte Möglichkeiten:  
(a) _C:\xampp\htdocs\MeinProjektName>symfony serve_ oder  
(b) _php -S 127.0.0.1:8000 -t public_.

Unter [http://localhost:8000](http://localhost:8000/) sollten Sie dann den folgenden Screen sehen (oder einen ähnlichen, je nach Symfony-Version). Dabei handelt es sich um eine Standard-Fehlermeldungsseite (404 not found), die aber anzeigt, dass ein leeres Sympony Projekt vorhanden ist.

[![Symfony3.png](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/thumb/b/be/Symfony3.png/550px-Symfony3.png)](https://isp.eduloop.de/mediawiki/images/isp.eduloop.de/b/be/Symfony3.png)
