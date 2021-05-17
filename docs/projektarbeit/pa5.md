
# PA 5: Sichern und dokumentieren der Arbeitsschritte 
    
## 5.1 Installation Apache2 und PHP

### 5.1.1 Dokumentieren Sie die Installation von Apache2

__Installation:__

1. Lokale Pakete aktualisieren
```Terminal
sudo apt update
```


2. Apache2 installieren 
```Terminal
sudo apt install apache2
```

<br>

__Firewall anpassen:__

3. Anwendungsprofile auflisten
```Terminal
sudo ufw app list
```
```Output
Available applications:
  Apache
  Apache Full
  Apache Secure
  OpenSSH
```


4. Port 80 für Datenverkehr zulassen
```Terminal
sudo ufw allow 'Apache'
```


5. Überprüfen
```Terminal
sudo ufw status
```
```Output
Status: active
To                         Action      From
OpenSSH                    ALLOW       Anywhere                  
Apache                     ALLOW       Anywhere                
OpenSSH (v6)               ALLOW       Anywhere (v6)             
Apache (v6)                ALLOW       Anywhere (v6)
```

<br>

__Webserver Testen:__

6. Apache2 Status überprüfen
```Terminal
sudo systemctl status apache2
```
> [!TIP|style:flat]
>
>__Webserver stoppen__
>
>sudo systemctl stop apache2
>
>__Webserver starten__
>
>sudo systemctl start apache2
>
>__Neustart__
>
>sudo systemctl restart apache2
>
>__Konfigurationsänderungen vornehmen__
>
>sudo systemctl reload apache2


7. IP herausfinden
```Terminal
hostname -I
```

8. Firefox öffnen
```Firefox
http://your_server_ip
```




        

<br>
<br>

### 5.1.2 Dokumentieren Sie die Installation von PHP (oder entsprechende Technologie)

1. PHP Paket installieren
```Terminal
sudo apt-get install php libapache2-mod-php
```


2. Überprüfen 
```Terminal
php -v
```

<br>
<br>
<br>
<br>

## 5.2 Einrichten Applikationsbenutzer für die Visualisierungszugriffe
        
#### 5.2.1 Benutzer erstellen
        
       
#### 5.2.2 Berechtigungen erstellt


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


<br>
<br>

### 5.2.3 Zugriff getestet

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
DROP USER 'DBrFAbfrage'@'localhost';
DROP USER 'DBrFAbfrage'@'AppliServer';
DROP USER 'DBrFUpdate'@'localhost';
DROP USER 'DBrFUpdate'@'AppliServer';
DROP USER 'DBrFDatenadmin'@'localhost';
DROP USER 'DBrFAdmin'@'localhost';

# Benutzer: DBrFAbfrage
# auf Localhost
CREATE USER 'DBrFAbfrage'@'localhost' IDENTIFIED BY 'abfrage';
GRANT SELECT ON DBschweizerPolitiker.* TO 'DBrFAbfrage'@'localhost';
# auf AppliServer
CREATE USER 'DBrFAbfrage'@'AppliServer' IDENTIFIED BY 'abfrage';
GRANT SELECT ON DBschweizerPolitiker.* TO 'DBrFAbfrage'@'AppliServer';

# Benutzer: DBrFUpdate
# auf Localhost
CREATE USER 'DBrFUpdate'@'localhost' IDENTIFIED BY 'aktualisierung';
# auf Tabelle tblVorstoesse
GRANT SELECT ON DBschweizerPolitiker.tblVorstoesse TO 'DBrFUpdate'@'localhost';
GRANT INSERT ON DBschweizerPolitiker.tblVorstoesse TO 'DBrFUpdate'@'localhost';
GRANT DELETE ON DBschweizerPolitiker.tblVorstoesse TO 'DBrFUpdate'@'localhost';
GRANT UPDATE ON DBschweizerPolitiker.tblVorstoesse TO 'DBrFUpdate'@'localhost';
# auf Tabelle tblPolitiker
GRANT SELECT ON DBschweizerPolitiker.tblPolitiker TO 'DBrFUpdate'@'localhost';
GRANT INSERT ON DBschweizerPolitiker.tblPolitiker TO 'DBrFUpdate'@'localhost';
GRANT DELETE ON DBschweizerPolitiker.tblPolitiker TO 'DBrFUpdate'@'localhost';
GRANT UPDATE ON DBschweizerPolitiker.tblPolitiker TO 'DBrFUpdate'@'localhost';
# auf Tabelle tblInteressenbindungen
GRANT SELECT ON DBschweizerPolitiker.tblInteressenbindungen TO 'DBrFUpdate'@'localhost';
GRANT INSERT ON DBschweizerPolitiker.tblInteressenbindungen TO 'DBrFUpdate'@'localhost';
GRANT DELETE ON DBschweizerPolitiker.tblInteressenbindungen TO 'DBrFUpdate'@'localhost';
GRANT UPDATE ON DBschweizerPolitiker.tblInteressenbindungen TO 'DBrFUpdate'@'localhost';
# auf AppliServer
CREATE USER 'DBrFUpdate'@'AppliServer' IDENTIFIED BY 'aktualisierung';
# auf Tabelle tblVorstoesse
GRANT SELECT ON DBschweizerPolitiker.tblVorstoesse TO 'DBrFUpdate'@'AppliServer';
GRANT INSERT ON DBschweizerPolitiker.tblVorstoesse TO 'DBrFUpdate'@'AppliServer';
GRANT DELETE ON DBschweizerPolitiker.tblVorstoesse TO 'DBrFUpdate'@'AppliServer';
GRANT UPDATE ON DBschweizerPolitiker.tblVorstoesse TO 'DBrFUpdate'@'AppliServer';
# auf Tabelle tblPolitiker
GRANT SELECT ON DBschweizerPolitiker.tblPolitiker TO 'DBrFUpdate'@'AppliServer';
GRANT INSERT ON DBschweizerPolitiker.tblPolitiker TO 'DBrFUpdate'@'AppliServer';
GRANT DELETE ON DBschweizerPolitiker.tblPolitiker TO 'DBrFUpdate'@'AppliServer';
GRANT UPDATE ON DBschweizerPolitiker.tblPolitiker TO 'DBrFUpdate'@'AppliServer';
# auf Tabelle tblInteressenbindungen
GRANT SELECT ON DBschweizerPolitiker.tblInteressenbindungen TO 'DBrFUpdate'@'AppliServer';
GRANT INSERT ON DBschweizerPolitiker.tblInteressenbindungen TO 'DBrFUpdate'@'AppliServer';
GRANT DELETE ON DBschweizerPolitiker.tblInteressenbindungen TO 'DBrFUpdate'@'AppliServer';
GRANT UPDATE ON DBschweizerPolitiker.tblInteressenbindungen TO 'DBrFUpdate'@'AppliServer';

# Benutzer: DBrFDatenadmin
# auf Localhost
CREATE USER 'DBrFDatenadmin'@'localhost' IDENTIFIED BY 'daten';
GRANT SELECT ON DBschweizerPolitiker.* TO 'DBrFDatenadmin'@'localhost';
GRANT INSERT ON DBschweizerPolitiker.* TO 'DBrFDatenadmin'@'localhost';
GRANT DELETE ON DBschweizerPolitiker.* TO 'DBrFDatenadmin'@'localhost';
GRANT UPDATE ON DBschweizerPolitiker.* TO 'DBrFDatenadmin'@'localhost';

# Benutzer: DBrFAdmin
# auf Localhost
CREATE USER 'DBrFAdmin'@'localhost' IDENTIFIED BY 'admin';
GRANT ALL PRIVILEGES ON DBschweizerPolitiker.* TO 'DBrFAdmin'@'localhost';

FLUSH PRIVILEGES;
```

<br>
<br>
<br>
<br>



## 5.3 Umsetzung PHP-Script mit Plotting der Daten

1. Verzeichnis erstellen
```Terminal
sudo mkdir /var/www/roehfix
```


2. Dem User Rechte auf das Verzeichnis geben
```Terminal
sudo chown -R $USER:$USER /var/www/roehfix
```


3. Berechtigungen vergeben 
```Terminal
sudo chmod -R 755 /var/www/roehfix
```



4. Index.php erstellen
```Terminal
sudo nano /var/www/roehfix/index.php
```
```index.php
Skript.php
```


5. Host Konfiguration erstellen
```Terminal
sudo nano /etc/apache2/sites-available/roehfix.conf
```
```/etc/apache2/sites-available
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    ServerName roehfix
    ServerAlias www.roehfix
    DocumentRoot /var/www/roehfix
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```


6. Konfiguration Activieren
```Terminal
sudo a2ensite roehfix.conf
```

7. Default Konfiguration deaktivieren
```Terminal
sudo a2dissite 000-default.conf
```


8. Konfiguration auf Fehler testen
```Terminal
sudo apache2ctl configtest
```


9. Neustart des Apache 
```Terminal
sudo systemctl restart apache2
```

10. Firefox öffnen
```Firefox
http://your_server_ip
```



<br>
<br>
<br>
<br>

## 5.4 Reflexion der Arbeit


__Wie haben Sie die Arbeiten an dieser Projekt erlebt?__

<br>



__Was hat bei der gesamten Projektarbeit gut funktioniert?__

<br>


__Was hat bei der gesamten Projektarbeit nicht gut funktioniert?__

<br>


__Wo sehen Sie Verbesserungspotential bei dieser Projektarbeit? Inhaltlich, organsisatorisch?__

<br>
