# DBMS konfigurienen (Betrieb & Config)

## Benutzer

__Anzeigen:__

```mysql
use mysql;
select user,host,authentication_string from user;
```

<br>

__Passwort ändern:__

- Terminal
```Terminal
mysqladmin -u'dein-user' -p'dein-altes-passwort' password 'dein-neues-passwort'
```

- MYSQL
```SQL
update user set password=PASSWORD('dein-neues-passwort') where User='dein-user';
```
```Mysql
flush privileges;
```

quit


<br>

## Root

__Anmelden:__

- Anmelden ohne DB
```Terminal
mysql -u root -p
```

- Anmelden direkt in DB
```mysql
mysql -u root -p roehFix
```

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

<br>
<br>

## MYSQL Config

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

<br>
<br>

## Allgemein Config-File

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

## Netzwerkkonfiguration DBMS-Server

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

## Server-Betrieb (langsame Abfragen)


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
