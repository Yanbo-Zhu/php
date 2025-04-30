
# 1 Configuration file php.ini


==PHP is typically used as **a module of the Apache web server** ==. The PHP module must also be configured independently of the web server's configuration settings.

These PHP configuration settings can be made in the _php.ini configuration file. The_ _php.ini file_ is read when PHP (or the web server) starts. A detailed description of the individual parameters can be found in the [php.ini manual](http://php.net/manual/de/ini.php) .

- For security reasons , the _php.ini_ file can only be modified by the system administrator (root). The settings can be displayed with < _?php phpinfo(); ?_ >.
- Any settings made in _php.ini_ override the precompiled settings of the PHP module. This file is called when the module starts (i.e., when the Apache web server starts).
- On a Linux system, the _php.ini_ file is usually located in the _/etc/php/_ directory or in a corresponding subdirectory.
- If changes have been made to _php.ini_ , Apache must be restarted for them to take effect.


**_php.ini_** **directives**  
The default settings are marked in bold in the table.


| parameter                                                                                 | Explanation                                                                                                                                                                                                                                                                                                                                                                                                  |
| ----------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| _display_errors = **On** \|Off_                                                           | If the value is set to _On_ , error messages are displayed on the screen. This is very useful on a development or test system. For production systems, error display should be set to _Off_ for security reasons .  是否给出 Fehlermeldung .                                                                                                                                                                     |
| _log_errors = On\| **Off**  <br>error_log = path/file_                                    | Error messages should be written to a file for monitoring purposes using **log_errors = On . This is the only way to reproduce errors.**<br><br>The directory can be freely chosen, but the server must have write access to it. The files in this folder should be locked from external access.                                                                                                             |
| _log_errors_max_len = **1024**_                                                           | Specifies the maximum size of the log file in bytes. The **default value for this parameter is 1024 bytes (which is very small)** . If 0 is specified as the value, the file can grow to any size, which should be avoided. Therefore, enter a reasonable value here, for example, 100000.                                                                                                                   |
| _error_reporting = E_ERROR \| E_WARNING \| E_STRICT \| E_DEPRECATED \| E_NOTICE \| E_ALL_ | Filters the errors to be displayed; different types can be specified (e.g., _E_ERROR_ displays only serious errors, _E_NOTICE_ displays notices, etc.). The constants can be combined with the bit operators & (=and) or ~ (=not) (e.g., _E_ALL & ~E_NOTICE_ ). On a development system, the _E_ALL_ setting is often useful. If you then see too many notice messages, you should use _E_ALL & ~E_NOTICE_ . |
| _track_errors = On\| **Off**_                                                             | If this parameter is set to _On_ , the most recent error message from the interpreter is available via the variable _$php_errormsg_ .                                                                                                                                                                                                                                                                        |
| _auto_prepend_file = file  <br>auto_append_file = file_                                   | Here you can specify that a file is automatically included ( _via include_ ) in every script. Please use with caution and keep in mind that no one will discover this automatic behavior during debugging.                                                                                                                                                                                                   |
| _max_execution_time = **30**_                                                             | Specifies the maximum execution time in seconds for a script. A timeout occurs if the timeout is exceeded. This value can be increased for complex database connections.                                                                                                                                                                                                                                     |
| _file_uploads = **On** \|Off  <br>upload_tmp_dir =  <br>upload_max_filesize = **2M**_     | With these parameters, you allow file uploads of up to 2 MB to the specified directory. If no upload is required, the parameter should be set to _Off_ . If you allow uploads, you should specify the corresponding directory and also automatically check this directory (for malware).                                                                                                                     |

# 2 Umgebungsvariablen auslesen


Mit nur einer einzigen Zeile PHP-Code kann man die kompletten Variablen auslesen, die dem PHP-Modul bekannt sind. Dies ist überaus hilfreich.

`<?php phpinfo(); ?>`

这样的话 所有的 的 variable 就在 browser  中 显示出来 

Hier kann man nun auch erfahren, welche Erweiterungen geladen und wie diese konfiguriert sind. Außerdem kann in der Abbildung sehr gut erkannt werden, dass es noch viele andere _ini_-Dateien gibt, die eingelesen werden.


![](images/Pasted%20image%2020250419170510.png)



