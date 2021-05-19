# Benutzer Berrechtigungen

## Wichtigste Befehle 


Einem Benutzer alle Rechte auf Datenbank oder Tabelle geben
```Mysql
GRANT ALL PRIVILEGES ON roehFix.* TO 'DBrFAdmin'@'localhost';
```


Einem Benutzer alle Rechte auf eine Datenbank oder Tabelle entziehen:
```Mysql
REVOKE ALL PRIVILEGES ON datenbankname.tabellename FROM 'benutzername'@'localhost';
```

Benutzerrechte neuladen
```Mysql
FLUSH PRIVILEGES;
```

<br>

## Script (User Erstellen/Berrechtigen)

```roehfixBerechtigungen
# ------------------------------------------------------------------------------
# Scriptname:   roehfixberechtigungen.sql
# Projekt:      RoehFix
# Autor:        Joschija Gruss
# Datum:        17.05.2021
# Kommando:     mysql -u root -p < roehfixberechtigungen.sql
# ------------------------------------------------------------------------------

#Alte Benuter löschen
USE mysql;
DROP USER IF EXISTS 'DBrFAbfrage'@'localhost';
DROP USER IF EXISTS 'DBrFAbfrage'@'AppliServer';
DROP USER IF EXISTS 'DBrFUpdate'@'localhost';
DROP USER IF EXISTS 'DBrFUpdate'@'AppliServer';
DROP USER IF EXISTS 'DBrFDatenadmin'@'localhost';
DROP USER IF EXISTS 'DBrFAdmin'@'localhost';


# Benutzer: DBrFAbfrage
# auf Localhost
CREATE USER 'DBrFAbfrage'@'localhost' IDENTIFIED BY 'Abfrage_123';
GRANT SELECT ON roehFix.* TO 'DBrFAbfrage'@'localhost';

# auf AppliServer
CREATE USER 'DBrFAbfrage'@'AppliServer' IDENTIFIED BY 'Abfrage_123';
GRANT SELECT ON roehFix.* TO 'DBrFAbfrage'@'AppliServer';



# Benutzer: DBrFUpdate
# auf Localhost
CREATE USER 'DBrFUpdate'@'localhost' IDENTIFIED BY 'Aktualisierung_123';
# auf Tabelle Kontaktdaten
GRANT SELECT, INSERT, DELETE, UPDATE ON roehFix.kontaktdaten TO 'DBrFUpdate'@'localhost';
# auf Tabelle Adressen
GRANT SELECT, INSERT, DELETE, UPDATE ON roehFix.adressen TO 'DBrFUpdate'@'localhost';
# auf Tabelle Kunden
GRANT SELECT, INSERT, DELETE, UPDATE ON roehFix.kunden TO 'DBrFUpdate'@'localhost';
# auf Tabelle Gatways
GRANT SELECT, INSERT, DELETE, UPDATE ON roehFix.gatways TO 'DBrFUpdate'@'localhost';
# auf Tabelle Sensoren
GRANT SELECT, INSERT, DELETE, UPDATE ON roehFix.sensoren TO 'DBrFUpdate'@'localhost';

# auf AppliServer
CREATE USER 'DBrFUpdate'@'AppliServer' IDENTIFIED BY 'Aktualisierung_123';
# auf Tabelle Kontaktdaten
GRANT SELECT, INSERT, DELETE, UPDATE ON roehFix.kontaktdaten TO 'DBrFUpdate'@'AppliServer';
# auf Tabelle Adressen
GRANT SELECT, INSERT, DELETE, UPDATE ON roehFix.adressen TO 'DBrFUpdate'@'AppliServer';
# auf Tabelle Kunden
GRANT SELECT, INSERT, DELETE, UPDATE ON roehFix.kunden TO 'DBrFUpdate'@'AppliServer';
# auf Tabelle Gatways
GRANT SELECT, INSERT, DELETE, UPDATE ON roehFix.gatways TO 'DBrFUpdate'@'AppliServer';
# auf Tabelle Sensoren
GRANT SELECT, INSERT, DELETE, UPDATE ON roehFix.sensoren TO 'DBrFUpdate'@'AppliServer';



# Benutzer: DBrFDatenadmin
# auf Localhost
CREATE USER 'DBrFDatenadmin'@'localhost' IDENTIFIED BY 'Daten_123';
GRANT SELECT, INSERT, DELETE, UPDATE ON roehFix.* TO 'DBrFDatenadmin'@'localhost';



# Benutzer: DBrFAdmin
# auf Localhost
CREATE USER 'DBrFAdmin'@'localhost' IDENTIFIED BY 'Admin_123';
GRANT ALL PRIVILEGES ON roehFix.* TO 'DBrFAdmin'@'localhost';

FLUSH PRIVILEGES;
```
<br>
<br>


## Benutzer (Berrechtigung)

Rechte | MYSQL Berrechtigungen | 
:-------- | :---------- 
Strucktur ändern  |   CREATE, DROP 
Daten manibulieren |  DELETE, UPDATE 
Daten einfügen | INSERT  
Lesen |  SELECT

> [!NOTE|style:flat]
> __ALL PRIVILEGES:__ Ein Wildcard für alle Rechte auf das gewählte Datenbankobjekt, mit einem *.* auf alle Datenbanken.
>
> __CREATE:__ Erlaubt einem Benutzer, neue Datenbanken zu erstellen
>
> __DROP:__ Erlaubt einem Benutzer, Datenbanken zu löschen
>
> __DELETE:__ Erlaubt einem Benutzer, einzelne Zeilen in einer Tabelle zu löschen
>
> __INSERT:__ Erlaubt einem Benutzer, neue Zeilen in eine Tabelle zu schreiben
>
> __SELECT:__ Leseberechtigungen auf eine Datenbank oder Tabelle
>
> __UPDATE:__ Erlaubnis, eine Zeile zu aktualisieren

__DBrFAbfrage:__
 
Tabelle | Strucktur ändern | Daten manibulieren | Daten einfügen | Lesen 
:-------- | :---------- | :---------- | :---------- | :---------- 
Kunden |   |   |   | x |
Konttaktdaten |   |   |   | x |
Adressen |   |   |   | x |
Gatways |   |   |   | x |
Gatways_has_Sensoren |   |   |   | x |
Sensoren  |   |   |   | x |
Sendordaten  |   |   |   | x |
Typ |   |   |   | x |

```MYSQL
GRANT SELECT ON roehFix.* TO 'DBrFAbfrage'@'localhost';
```


<br>

__DBrFUpdate:__

Tabelle | Strucktur ändern | Daten manibulieren | Daten einfügen | Lesen 
:-------- | :---------- | :---------- | :---------- | :---------- 
Kunden |  | x | x | x |
Konttaktdaten |   | x | x | x |
Adressen |   | x | x | x |
Gatways |   | x | x | x |
Gatways_has_Sensoren |   |   |   |   |
Sensoren  |   | x | x | x |
Sendordaten  |   |   |   |   |
Typ |   |   |   |   |


```MYSQL
# auf Tabelle Kontaktdaten
GRANT SELECT, INSERT, DELETE, UPDATE ON roehFix.kontaktdaten TO 'DBrFUpdate'@'localhost';
# auf Tabelle Adressen
GRANT SELECT, INSERT, DELETE, UPDATE ON roehFix.adressen TO 'DBrFUpdate'@'localhost';
# auf Tabelle Kunden
GRANT SELECT, INSERT, DELETE, UPDATE ON roehFix.kunden TO 'DBrFUpdate'@'localhost';
# auf Tabelle Gatways
GRANT SELECT, INSERT, DELETE, UPDATE ON roehFix.gatways TO 'DBrFUpdate'@'localhost';
# auf Tabelle Sensoren
GRANT SELECT, INSERT, DELETE, UPDATE ON roehFix.sensoren TO 'DBrFUpdate'@'localhost';
```

<br>

__DBrFDatenAdmin:__


Tabelle | Strucktur ändern | Daten manibulieren | Daten einfügen | Lesen 
:-------- | :---------- | :---------- | :---------- | :---------- 
Kunden |   | x | x | x |
Konttaktdaten |   | x | x | x |
Adressen |   | x | x | x |
Gatways |   | x | x | x |
Gatways_has_Sensoren |   | x | x | x |
Sensoren  |   | x | x | x |
Sendordaten  |   | x | x | x |
Typ |   | x | x | x |


```MYSQL
GRANT SELECT, INSERT, DELETE, UPDATE ON roehFix.* TO 'DBrFDatenadmin'@'localhost';
```

<br>

__DBrFAdmin:__


Tabelle | Strucktur ändern | Daten manibulieren | Daten einfügen | Lesen 
:-------- | :---------- | :---------- | :---------- | :---------- 
Kunden | x | x | x | x |
Konttaktdaten | x | x | x | x |
Adressen | x | x | x | x |
Gatways | x | x | x | x |
Gatways_has_Sensoren | x | x | x | x |
Sensoren  | x | x | x | x |
Sendordaten  | x | x | x | x |
Typ | x | x | x | x |


```MYSQL
GRANT ALL PRIVILEGES ON roehFix.* TO 'DBrFAdmin'@'localhost';
```


