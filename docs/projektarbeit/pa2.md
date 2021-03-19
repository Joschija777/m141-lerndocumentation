# PA 2:  Konfiguration eines RDBMS

<br>

## 2.1 Storage Engines bei MySQL

#### 2.1.1 Storage-Engines
Dokumentieren 2 wichtigesten Storage-Engines genau beschrieben:

- __InnoDB__
ist ein freies Speichersubsystem für das Datenbankmanagementsystem MySQL. Sein Hauptvorteil gegenüber anderen Speichersubsystemen für MySQL ist, dass Transaktionssicherheit und referenzielle Integrität über Fremdschlüssel gewährleistet werden.
Sie sind optimal für eine maximale Leistung bei der Bearbeitung von grossen Datenmengen. Sie sind transaktionssicher und sie beherrschen das sperren auf Zeilenebene, sowie auch ein konsistentes nicht sperrendes Lesen. Wenn die referenzierten Tabellen denselben Typ haben, wird sogar eine referenzielle Integrität unterstützt. Man ist nicht an die maximale Dateigrösse des Systemgeknüpft, da die Tabellen in einem eigenen Tabellenplatz, welcher aus mehreren Dateien bestehen kann, bestehen.

    InnoDB entspricht dem ACID-Standard (Atomicity Consistency Isolation Durability). Alle Transaktionen laufen voneinander isoliert ab, aber es können beliebig viele Anwendungen gleichzeitig Daten in eine Tabelle schreiben. Bei der Datenabfrage, dem SELECT, hat InnoDB deutlich die Nase vorne, aber bei den Schreibzugriffen auf eine Datenbank, den INSERT und UPDATE, ist MyISAM etwas schneller.

    - __ACID__ 

        - Atomicity oder Atomarität: Ausführung aller oder keiner Informationsteile einer Transaktion
        - Consistency oder Konsistenz: Transaktionen erzeugen einen gültigen Zustand oder fallen in den alten Zustand zurück
        - Isolation oder Abgrenzung: Transaktionen verschiedener Anwender oder Prozesse bleiben voneinander isoliert
        - Durability oder Dauerhaftigkeit: Nach einer erfolgreichen Transaktion bleiben die Daten dauerhaft gespeichert


<br>
<br>

- __MyISAM__
Bei der MyISAM Tabelle gibt es drei verschiedene Arten, es gibt die Statische, die Dynamische und die Komprimierte. Alle gemeinsam haben das sie nicht transaktionssicher sind und keine referenzielle Integrität unterstützen.

    Die Statische ist sehr schnell und einfach wiederherzustellen, da sich die Datensätze an festen Positionen befinden, aus dem Grund weil die Inhalte der Spalten immer gleich lang sind. Sie brauchen jedoch mehr Speicherplatz als die anderen beiden Varianten.

    Die zweite Variante ist die Dynamische. Wie bereits gesagt braucht die Dynamische weniger Speicherplatz als die Statische, den hier werden die Datensätze fragmentiert wenn sie grösser werden.

    Die letzte Variante ist die Komprimierte, sie ist für die Statische und die Dynamische verfügbar. Die Daten werden komprimiert abgespeichert und können nur gelesen werden.

    ISAM steht für Indexed Sequential Access Method (dt. Index-sequenzielle Zugriffsmethode) – es ist also nicht möglich, dass mehrere User oder Anwendungen gleichzeitig in einer Tabelle schreiben. Das sequenzielle Speichern erlaubt immer nur den Schreibzugriff durch eine Anwendung.

    - __ISAM__
    Index Sequential Access Method (ISAM) ist eine von IBM entwickelte Zugriffsmethode für Datensätze einer Datei, die sowohl (sortiert) sequentiellen als auch wahlfreien (random) index-basierten Zugriff zulässt.

<br>
<br>

#### 2.1.2 Restlichen Storage-Engines

__Befehl:__

```mysql
SHOW ENGINES;
```
<img width="100%" src='./bilder/enginesMysql.png'></img>

> [!NOTE|style:flat]
> Ich habe 9 Engines auf meinem System bei MySQL.

<br>

__Liste:__

- __ARCHIVE:__ Archive ist eine Speicher-Engine für das relationale Datenbankverwaltungssystem MySQL. Benutzer können diese analytische Speicher-Engine verwenden, um eine Tabelle zu erstellen, die nur "archiviert" ist. Daten können nicht aus dieser Tabelle gelöscht, sondern nur hinzugefügt werden.

- __BLACKHOLE:__ Die BLACKHOLESpeicher-Engine fungiert als „ Schwarzes Loch “ , das Daten akzeptiert, aber wegwirft und nicht speichert. Abfragen geben immer ein leeres Ergebnis zurück.

- __FEDERATED:__ Mit dem Storage-Engine können Sie auf Daten aus einer entfernten MySQL-Datenbank zugreifen, ohne Replikations- oder Clustertechnologie zu verwenden. Beim Abfragen einer lokalen Tabelle werden die Daten automatisch aus den entfernten (verbundierten) Tabellen abgezogen. In den lokalen Tabellen werden keine Daten gespeichert. FEDERATEDFEDERATED

- __PERFORMANCE-SCHEMA:__ Das Leistungsschema bietet eine Möglichkeit, die interne Ausführung des Servers zur Laufzeit zu überprüfen. Sie wird mithilfe des PERFORMANCE_SCHEMA Speichermoduls und der Datenbank implementiert. Das Leistungsschema konzentriert sich in erster Linie auf Leistungsdaten

- __MEMORY:__ Das Speichermodul erstellt Spezielle Tabellen mit Inhalten, die im Speicher gespeichert sind. Da die Daten anfällig für Abstürze, Hardwareprobleme oder Stromausfälle sind, verwenden Sie diese Tabellen nur als temporäre Arbeitsbereiche oder schreibgeschützte Caches für Daten, die aus anderen Tabellen gezogen werden

- __CSV:__ Das CSV-Speichermodul speichert Daten in Textdateien im Format "Durchkommasgetrennte Werte". Die CSV-Speicher-Engine wird immer in den MySQL-Server kompiliert. Um die Quelle für das CSV-Modul zu untersuchen, suchen Sie im Speicher-/csv-Verzeichnis einer MySQL-Quellverteilung.


<br>
<br>

#### 2.1.3 Datenanwendung Storage Enginge 

Engine | Anwendung  | Begründung
:-------- | :---------- | :----------
InnoDB | Bankdaten, Kundendaten | ACID, Commit, Rollback, Crash-Recovery, keine Daten verloren
MyISAM   | Webanwendungen   | Schnelle Speicher-Engine, leselastigen Anwendungen, Volltextsuchindizes
ARCHIVE | Archivieren und Abrufen vergangener Daten | Tabellen werden nicht indiziert, und die Komprimierung erfolgt beim Einfügen
BLACKHOLE  | verteilten Datenbankumgebung     | Akzeptiert aber speichert keine Daten, Abfragen immer einen leeren Satz zurück
FEDERATED | einzelnen, lokalen, logischen Datenbank |  Keine Daten gespeichert und Abfragen automatisch auf Remote-Server
PERFORMANCE-SCHEMA   | Monitoring    | Leistungsdaten, überwacht Serverereignisse
MEMORY | für temporäre Tabellen mit externen Abfragedaten | Speichert Daten im RAM, gleichzeitige Datenzugriff wird synchronisiert.
CSV   | CSV-formatierte Daten   |  Sobald man eine CSV Datei importieren möchte 

> [!TIP|style:flat]
> In den meisten Fällen verwendet man InnoDB = default oder MyISAM

<br>

#### 2.1.4 Tabelleanwendung Storage Engine
Dokumentieren Sie wie eine Storage Engine auf eine Tabelle angwendet wird

1. Datenbank auswählen
```mysql
use dbname;
```
2. Tabelle erstellen mit (MyISAM)
```mysql
create table test1 (
id int not null,
column1 int (11),
column2 varchar (100)
) ENGINE=MyISAM;
```

<img width="100%" src='./bilder/engineTa.png'></img>

> [!TIP|style:flat]
> Mit "Engine=passendeEngine" auswählen.

<br>
<br>
<br>
<br>


## 2.2 Benutzer und Berechtigungen

__Alle Users anzeigen:__

```mysql
use mysql;
select user,host,authentication_string from user;
```
<img width="100%" src='./bilder/userTabelle.png'></img>

<br>

#### 2.2.1 Root-Benutzer konfiguriert 


__Root konfigurieren:__

```Terminal
sudo mysql_secure_installation
```
<img width="100%" src='./bilder/rootpw.png'></img>

> [!Note|style:flat]
> Muss man nur einmal machen am besten wenn man mysql-server installiert hat.

<br>

__Login:__


```mysql
mysql -u root 
```

<img width="100%" src='./bilder/rootlogin.png'></img>

> [!TIP|style:flat]
> - mysql -u root -> ohne Passwort abfrage!
> - mysql -u root **-p** -> mit Passwort abfrage!

> [!Attention|style:flat]
> ERROR 1698 (28000): Access denied for user 'root'@'localhost'
> ```Terminal
> sudo mysql -u root
> ```
> ```mysql
> USE mysql;
> UPDATE user SET plugin='mysql_native_password' WHERE User='root';
> FLUSH PRIVILEGES;
> exit;
>  ```
>  ```Terminal
> sudo service mysql restart
>  ```

<br>

__Passwort:__

-  Wenn root noch kein Passwort hat
```Terminal
mysqladmin -u root password Admin_123
```

- Wenn root schon ein Passwort hat
```mysql
mysqladmin -u root -p ALTESPASSWORT NEUESPASSWORT
```

<img width="100%" src='./bilder/rootpasswort.png'></img>

> [!TIP|style:flat]
> Userrechte neu laden
> ```mysql
> FLUSH PRIVILEGES;
> exit;
>  ```

<br>
<br>

#### 2.2.2 Sensoren-Benutzer konfiguriert

__Benutzer erstellen und Rechte:__

1. Als Root anmelden
```Terminal
mysql -u root -p    
```
2. Benutzer erstellen
```mysql
CREATE USER 'benutzer'@'localhost' IDENTIFIED BY 'Test_123';
```

3. (Optional) -> Zeigt alle Datenbanken auf.
```mysql
show databases;
```

4. Datenbank auswählen wo man Recht vergeben möchte.  
```mysql
use meineTestDB;
```

5. Berrechtigung vergeben
```mysql
GRANT SELECT,INSERT on meineTestDB.* to 'TestBenutzer'@'localhost';
```

6. Privilegien im Arbeitsspeicher updaten
```mysql
FLUSH PRIVILEGES;
```

7. Mysql verlassen
```mysql
exit;
```
<img width="100%" src='./bilder/sensorenBeAn.png'></img>


> [!TIP|style:flat]
> Im nächsten Abschnitt, Login kann man grad testen ob es funktioniert hat.  

<br>

__Login:__

```Terminal
mysql -u TestBenutzer -p
```

```mysql
show databases;
```

<img width="100%" src='./bilder/loginB.png'></img>

> [!Note|style:flat]
> show databases = zeigt die Datenbanken die der Benutzer zugriff hat. 

<br>

__Passwort ändern:__

1. Als Root anmelden
```Terminal
mysql -u root -p
```
2. Mysql Datenbank verwenden
```mysql
use mysql;
```
3. Neues Passwort setzen
```mysql
ALTER USER 'user-name'@'localhost' IDENTIFIED BY 'NEW_USER_PASSWORD';
```
4. Privilegien im Arbeitsspeicher updaten
```mysql
FLUSH PRIVILEGES;
```

<img width="100%" src='./bilder/pwuser.png'></img>

> [!NOTE|style:flat]
> Wenn man einen Benutzer erstellt vergieb man ihm gerade ein Passwort mit IDENTIFIED
> ```mysql
> CREATE USER 'benutzer'@'localhost' IDENTIFIED BY 'Test_123';
> ```

<br>

__Berechtigung Datenbank:__


Berrechtigung anzeigen:
```mysql
SHOW GRANTS FOR 'TestBenutzer'@'localhost';
```

Berrechtigung vergeben:
```mysql
GRANT SELECT,INSERT on meineTestDB.* to 'TestBenutzer'@'localhost';
```

> [!TIP|style:flat]
> - GRANT SELECT,INSERT = Welche Berechtigung
> - on meineTestDB.* = Welche Datenbank
> - to 'TestBenutzer'@'localhost' = Welcher Benutzer

<br>

<br>

#### 2.2.3 Admin-Benutzer konfiguriert

__Login:__

```Terminal
mysql -u admin -p
```

```mysql
show databases;
```

<img width="100%" src='./bilder/loginA.png'></img>

> [!Warning|style:flat]
> __Bevor Login:__
> 1. Benutzer erstellen
> ```mysql
> CREATE USER 'admin@'localhost' IDENTIFIED BY 'Admin_123';
> ```
>
> 2. Rechte vergeben
> ```mysql
> GRANT ALL PRIVILEGES ON *.* TO 'admin'@'localhost';
> ```

<br>

__Passwort ändern:__

1. Als Root anmelden
```Terminal
mysql -u root -p
```
2. Mysql Datenbank verwenden
```mysql
use mysql;
```
3. Neues Passwort setzen
```mysql
ALTER USER 'admin'@'localhost' IDENTIFIED BY 'NEW_USER_PASSWORD';
```
4. Privilegien im Arbeitsspeicher updaten
```mysql
FLUSH PRIVILEGES;
```


<br>

__Berechtigung Datenbank:__


Vollzugriff auf alle Datenbanken:

```Terminal
GRANT ALL PRIVILEGES ON *.* TO 'admin'@'localhost';
```

> [!TIP|style:flat]
> - __ALL PRIVILEGES__: Ein Wildcard für alle Rechte auf das gewählte Datenbankobjekt, mit einem *.* auf alle Datenbanken.
> - __CREATE__: Erlaubt einem Benutzer, neue Datenbanken zu erstellen
> - __DROP__: Erlaubt einem Benutzer, Datenbanken zu löschen
> - __DELETE__: Erlaubt einem Benutzer, einzelne Zeilen in einer Tabelle zu löschen
> - __INSERT__: Erlaubt einem Benutzer, neue Zeilen in eine Tabelle zu schreiben
> - __SELECT__: Leseberechtigungen auf eine Datenbank oder Tabelle
> - __UPDATE__: Erlaubnis, eine Zeile zu aktualisieren
> - __GRANT OPTION__: Erlaubt einem Benutzer, die Rechte anderer Benutzer zu setzen oder zu widerrufen

<br>
<br>

#### 2.2.4 MySQL Konfiguration 

- Anzeige der aktuellen Werte
```mysql
SHOW VARIABLES;
```

- Zeige alles an was irgendwie mit "size" heisst
```mysql
SHOW VARIABLES LIKE '%size%';
```

- Status Variablen Global
```mysql
SHOW GLOBAL STATUS;
```

- Status Variablen für Sessions
```mysql
SHOW SESSION STATUS;
```

> [!Note|style:flat]
> Möchte da jetzt kein Screenshot hinzufügen da es unzählige Werte gibt.

<br>

__Konfigurationen - systemweite Anpassungen__


File Name | Purpose  
:-------- | :---------- 
/etc/my.cnf |   Global options
/etc/mysql/my.cnf   |   Global options
SYSCONFDIR/my.cnf   |   Global options
$MYSQL_HOME/my.cnf  |   Server-specific options (server only)
defaults-extra-file |   The file specified with --defaults-extra-file, if any
~/.my.cnf   |   User-specific options
~/.mylogin.cnf  |   User-specific login path options (clients only)
DATADIR/mysqld-auto.cnf |   System variables persisted with SET PERSIST or SE PERSIST_ONLY (server only)


> [!TIP|style:flat]
> Für Sie ist folgende Datei relevant
> /etc/mysql/mysql.conf.d/mysqld.cnf

<br>
<br>
<br>
<br>

## 2.3 Server-Konfiguration

#### 2.3.1 Transaktions-Isolation

__Verstösse:__

> [!TIP|style:flat]
> __Dirty Read__ tritt auf, wenn die Transaktion eine andere nicht festgeschriebene Transaktion liest

> [!NOTE|style:flat]
> __Non Repeatable Read__ tritt auf, wenn im Verlauf einer Transaktion eine Zeile zweimal abgerufen wird und sich die Werte innerhalb der Zeile zwischen den Lesevorgängen unterscheiden.

> [!ATTENTION|style:flat]
> __Phantom Read__ tritt auf, wenn im Verlauf einer Transaktion neue Zeilen durch eine andere Transaktion zu den gelesenen Datensätzen hinzugefügt werden.

<br>

__Isolationsstufen:__

> [!TIP|style:flat]
> __read-uncommitted__ Dies ist die niedrigste Isolationsstufe, da dadurch schmutziges Lesen möglich ist. Es hat jedoch einen Leistungsvorteil, da es das Erfassen und Freigeben der Sperre vermeidet.

> [!NOTE|style:flat]
> __read-committed__ tIn dieser Isolationsstufe wird sichergestellt, dass nur festgeschriebene Daten gelesen werden.

> [!ATTENTION|style:flat]
> __repeatable-read__ In dieser Isolationsstufe wird ein nicht wiederholbares Lesen verhindert. Es hält Lese- und Schreibsperren (erfasst für ausgewählte Daten) bis zum Ende der Transaktion. Die Bereichssperre wird jedoch nicht verwaltet, sodass diese Isolationsstufe das Lesen von Phantomen nicht verhindern kann.

> [!WARNING|style:flat]
> __Serializable__ In dieser Isolationsstufe sind Schreiben und Lesen gesperrt, und auch der gesperrte Bereich muss erfasst werden (wenn wir ihn verwenden selectund wherein Transaktion sind).

<img width="100%" src='./bilder/isolation.png'></img>

<br>

__Befehl__

Anzeigen: (+global)

```mysql
select @@transaction_isolation;
```

```mysql
select @@global.transaction_isolation;
```
<img width="100%" src='./bilder/isolationB.png'></img>

Ändern:

```mysql
set session transaction isolation level read uncommitted;
```

<img width="100%" src='./bilder/isolationAe.png'></img>

<br>
<br>

#### 2.3.2 Exportieren Sie die aktuelle Liste an System-Variablen

- Anzeige der aktuellen Werte

```mysql
SHOW VARIABLES;
```

```AUSGABE
+--------------------------------------------+------------------------------+
| Variable_name                              | Value                        |
+--------------------------------------------+------------------------------+
| activate_all_roles_on_login                | OFF                          |
| auto_generate_certs                        | ON                           |
| auto_increment_increment                   | 1                            |
| auto_increment_offset                      | 1                            |
| autocommit                                 | ON                           |
| automatic_sp_privileges                    | ON                           |
| avoid_temporal_upgrade                     | OFF                          |
| back_log                                   | 151                          |
| basedir                                    | /usr/                        |
| big_tables                                 | OFF                          |
+--------------------------------------------+------------------------------+
etc ...
```

- Zeige alles an was irgendwie mit "size" heisst
```mysql
SHOW VARIABLES LIKE '%size%';
```

- Status Variablen Global
```mysql
SHOW GLOBAL STATUS;
```

- Status Variablen für Sessions
```mysql
SHOW SESSION STATUS;
```




<br>
<br>

#### 2.3.3 Netzwerkkonfiguration DBMS-Server anpassen und dokumentieren

```Terminal
sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
```

```mysqld.cnf
# * Basic Settings
#
user            = mysql
# pid-file      = /var/run/mysqld/mysqld.pid
# socket        = /var/run/mysqld/mysqld.sock
# port          = 3306
# datadir       = /var/lib/mysql


# If MySQL is running as a replication slave, this should be
# changed. Ref https://dev.mysql.com/doc/refman/8.0/en/server-system-variables.html#sysvar_tmpdir
# tmpdir                = /tmp
#
# Instead of skip-networking the default is now to listen only on
# localhost which is more compatible and is not less secure.
bind-address            = 127.0.0.1
mysqlx-bind-address     = 127.0.0.1
#
# * Fine Tuning
#
key_buffer_size         = 16M
# max_allowed_packet    = 64M
# thread_stack          = 256K

# thread_cache_size       = -1

# This replaces the startup script and checks MyISAM tables if needed
# the first time they are touched
myisam-recover-options  = BACKUP

# Error log - should be very few entries.
#
log_error = /var/log/mysql/error.log
#
# Here you can see queries with especially long duration
# slow_query_log                = 1
# slow_query_log_file   = /var/log/mysql/mysql-slow.log
# long_query_time = 2
# log-queries-not-using-indexes

```

> [!TIP|style:flat]
> - log_error:
>   - Pfad der Log-Datei für Fehler
> 
> - datadir:
>   - Verzeichnis, in der die Daten gespeichert werden
>
> - bind_address:
>   - Defaultmässig auf 127.0.0.1 - das bedeutet, dass man nicht aus dem Netzwerk auf den Server zugreifen kann. Um auf allen Interfaces zu hören, muss diese Einstellung auf 0.0.0.0 gesetzt werden.
> 
> - port:
>   - er Default-Port von MySQL ist 3306.

<br>
<br>
<br>
<br>

## 2.4 Server-Betrieb

#### 2.4.1 Protokollierung langsamer Abfragen aktivieren

1. Configfile öffnen
```Terminal
sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
```

2. slow_query_log_file & slow_query_log auskommentieren und den Wert(1) bei low_query_log reinschreiben
```mysqld.cnf
# Here you can see queries with especially long duration
slow_query_log                = 1
slow_query_log_file   = /var/log/mysql/mysql-slow.log
# long_query_time = 2
# log-queries-not-using-indexes
```
> [!NOTE|style:flat]
> Im langsamen MySQL-Abfrageprotokoll registriert der MySQL- Datenbankserver alle Abfragen , die einen bestimmten Schwellenwert für die Ausführungszeit überschreiten. Dies kann oft ein guter Ausgangspunkt sein, um zu sehen, welche Abfragen am langsamsten und wie oft sie langsam sind

<br>
<br>


#### 2.4.2 Data-Directories auf Listen

1. als root unterweges
```Terminal
sudo -s
```

2. Ins Verzeichnis wo Data-Directories aufgelistet sind
```Terminal
cd /var/lib/mysql
```

3. Alles im Verzeichnis auflisten
```Terminal
ls -l
```

<img width="100%" src='./bilder/datadir.png'></img>

<br>
<br>

#### 2.4.3 Default-Datenbanken 

> [!TIP|style:flat]
>__mysql:__
Ist die Systemdatenbank, die Tabellen enthält, in denen die vom MySQL-Server benötigten Informationen gespeichert sind


> [!NOTE|style:flat]
>__sys:__
Eine Reihe von Objekten, mit denen Datenbankadministratoren und Entwickler die vom Leistungsschema erfassten Daten interpretieren können

> [!ATTENTION|style:flat]
> __performance-schema:__
Ist eine Funktion zum Überwachen der MySQL Server-Ausführung auf niedriger Ebene