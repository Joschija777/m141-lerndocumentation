
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

Ich habe für die Datenbank 4 User mit verschiedenen Rechte erstellt. Sie haben jeweils verschieden tiefe Berechtigungen und sind nur für ihr Gebiet berechtigt.
- DBrFAbfrage
- DBrFUpdate
- DBrFDatenAdmin
- DBrFAdmin

<br>

__DBrFAbfrage:__
 
Dieser Benutzer ist dafür da um Abfragen auf der DB zu machen. Er hat keine Berechtigung, um irgendwelche Daten oder gar die Struktur zu ändern. Er hat nur die Berechtigung um SELECT-Befehle auszuführen. 

```MYSQL
# Benutzer: DBrFAbfrage
# auf Localhost
CREATE USER 'DBrFAbfrage'@'localhost' IDENTIFIED BY 'abfrage';

# auf AppliServer
CREATE USER 'DBrFAbfrage'@'AppliServer' IDENTIFIED BY 'abfrage';
```

<br>


__DBrFUpdate:__

Die Benutzer ist dafür da um die Kundendaten, Sensoren und Gatways Daten auf dem aktuellen Stand zuhalten. Mann kann alles mit den angegeben Tabellen machen ausser die Strucktur ändern. 

```MYSQL
# Benutzer: DBrFUpdate
# auf Localhost
CREATE USER 'DBrFUpdate'@'localhost' IDENTIFIED BY 'aktualisierung';

# auf AppliServer
CREATE USER 'DBrFUpdate'@'AppliServer' IDENTIFIED BY 'aktualisierung';
```


<br>


__DBrFDatenAdmin:__

Dieser Benutzer hat das Recht alle Tabellen die Daten zu manipulieren, einzufügen und zu Lesen.

```MYSQL
# Benutzer: DBrFDatenadmin
# auf Localhost
CREATE USER 'DBrFDatenadmin'@'localhost' IDENTIFIED BY 'daten';
```

<br>

__DBrFAdmin:__

Dieser Benutzer hat die gleichen Rechte wie der User Root. Er ist somit ein Super-User und hat alle Rechte auf die Datenbank.

```MYSQL
# Benutzer: DBrFAdmin
# auf Localhost
CREATE USER 'DBrFAdmin'@'localhost' IDENTIFIED BY 'admin';
```


<br>
<br>

       
#### 5.2.2 Berechtigungen erstellt


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


<br>


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
# Benutzer: DBrFAbfrage
# auf Localhost
GRANT SELECT ON roehFix.* TO 'DBrFAbfrage'@'localhost';

# auf AppliServer
GRANT SELECT ON roehFix.* TO 'DBrFAbfrage'@'AppliServer';
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
# Benutzer: DBrFUpdate
# auf Localhost
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
# Benutzer: DBrFDatenadmin
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
# Benutzer: DBrFAdmin
# auf Localhost
GRANT ALL PRIVILEGES ON roehFix.* TO 'DBrFAdmin'@'localhost';
```

<br>
<br>

#### 5.2.3 Zugriff getestet

__Test 1: DBrFAbfrage__

1. Mit User in Datenbank anmelden
```
mysql -u user -p roeFix
```

<br>

__Test 2: DBrFUpdate__

1. Mit User in Datenbank anmelden
```
mysql -u user -p roeFix
```

<br>


__Test 3: DBrFAdmin__

1. Mit User in Datenbank anmelden
```
mysql -u user -p roeFix
```


<br>
<br>

#### 5.2.4 Script

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
GRANT SELECT ON roehFix.* TO 'DBrFAbfrage'@'localhost';

# auf AppliServer
CREATE USER 'DBrFAbfrage'@'AppliServer' IDENTIFIED BY 'abfrage';
GRANT SELECT ON roehFix.* TO 'DBrFAbfrage'@'AppliServer';



# Benutzer: DBrFUpdate
# auf Localhost
CREATE USER 'DBrFUpdate'@'localhost' IDENTIFIED BY 'aktualisierung';
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
CREATE USER 'DBrFUpdate'@'AppliServer' IDENTIFIED BY 'aktualisierung';
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
CREATE USER 'DBrFDatenadmin'@'localhost' IDENTIFIED BY 'daten';
GRANT SELECT, INSERT, DELETE, UPDATE ON roehFix.* TO 'DBrFDatenadmin'@'localhost';



# Benutzer: DBrFAdmin
# auf Localhost
CREATE USER 'DBrFAdmin'@'localhost' IDENTIFIED BY 'admin';
GRANT ALL PRIVILEGES ON roehFix.* TO 'DBrFAdmin'@'localhost';

FLUSH PRIVILEGES;
```

<br>
<br>
<br>
<br>



## 5.3 Umsetzung PHP-Script mit Plotting der Daten

__Script:__

```HTML

<?php

    $conn = mysqli_connect('localhost','root','Admin_123','roehFix');
    $sql = "SELECT kennung, laengeKoordination, breiteKoordination FROM sensoren ;
    $result = mysqli_query($conn, $sql);
    while($row = mysqli_fetch_assoc($result))
    {
	   $dataPoints[] = array("j"=>$row['kennung'],"x"=>$row['laengeKoordination'], "y"=>$row['breiteKoordination']);
    }
?>

<!DOCTYPE HTML>
<html>
<head>  
<script>
window.onload = function () {

var chart = new CanvasJS.Chart("chartContainer", {
	animationEnabled: true,
	zoomEnabled: true,
	title:{
		text: "RoeFix Sensordaten"
	},
	axisX: {
		title:"Laenge Koordination",
	},
	axisY:{
		title: "Breite Koordination",
	},
	data: [{
		type: "scatter",
		toolTipContent: "<b>Kennung: </b>{j} sq.ft<br/><b>Laenge Kordination: </b>{x} sq.ft<br/><b>Breite Kordination: </b>{y}",
    dataPoints: <?php echo json_encode($dataPoints, JSON_NUMERIC_CHECK); ?>
	}]
});
chart.render();

}
</script>
</head>
<body>
<div id="chartContainer" style="height: 370px; width: 100%;"></div>
<script src="https://canvasjs.com/assets/script/canvasjs.min.js"></script>
</body>
</html>
```

<br>

__Anleitung:__

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

```HTML

<?php

    $conn = mysqli_connect('localhost','root','Admin_123','roehFix');
    $sql = "SELECT kennung, laengeKoordination, breiteKoordination FROM sensoren ;
    $result = mysqli_query($conn, $sql);
    while($row = mysqli_fetch_assoc($result))
    {
	   $dataPoints[] = array("j"=>$row['kennung'],"x"=>$row['laengeKoordination'], "y"=>$row['breiteKoordination']);
    }
?>

<!DOCTYPE HTML>
<html>
<head>  
<script>
window.onload = function () {

var chart = new CanvasJS.Chart("chartContainer", {
	animationEnabled: true,
	zoomEnabled: true,
	title:{
		text: "RoeFix Sensordaten"
	},
	axisX: {
		title:"Laenge Koordination",
	},
	axisY:{
		title: "Breite Koordination",
	},
	data: [{
		type: "scatter",
		toolTipContent: "<b>Kennung: </b>{j} sq.ft<br/><b>Laenge Kordination: </b>{x} sq.ft<br/><b>Breite Kordination: </b>{y}",
    dataPoints: <?php echo json_encode($dataPoints, JSON_NUMERIC_CHECK); ?>
	}]
});
chart.render();

}
</script>
</head>
<body>
<div id="chartContainer" style="height: 370px; width: 100%;"></div>
<script src="https://canvasjs.com/assets/script/canvasjs.min.js"></script>
</body>
</html>
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

Ich habe bei diesem Projekt sehr viel dazugelernt. Besonders gut gefallen ist die Mischung der repetition von dem altem zu etwas neuem Lernen. Das bringt mich am meisten an dem Lerneffekt. Zusätlich das man von Anfang ein eigenes Projekt aufbaut, sah man wie gut das man mitgemacht hat.

<br>



__Was hat bei der gesamten Projektarbeit gut funktioniert?__

Es hat nach meiner Meinung sehr viel gut Funktioniert in diesem Projekt. In Grossen bin ich sehr Stolz auf meine Arbeit, da ich praktisch ohne Probleme durchgekommen bin. 
Zwar hatte ich Teils Probleme bei den Script, aber ich wurde immer schneller und habe es auch verstanden was drin Stand.

<br>


__Was hat bei der gesamten Projektarbeit nicht gut funktioniert?__

Der Abschnitt 5 hat mir am meisten Probleme bereiten mit dem Scripts. Aber im Grossen und ganuen ist eigentlich alles gut geangen. Ich glaube ich habe immer noch am meistten Schwirigkeiten an den JOINS. Villeicht könnte ich den Punkt mit der erstellung des ERD und ERM auch zunehmen da ich mehrere Anläfe gebraucht habe, bis ich zufieden war. 

<br>


__Wo sehen Sie Verbesserungspotential bei dieser Projektarbeit? Inhaltlich, organsisatorisch?__

Ich kann praktisch nur positives da lassen. Mein Grösster Kritscher Punkt wäre die Letzte Aufgabenstellung. Die war für mich nicht Verständlich. Und das der Test verschoben wurde, mussten wir noch andere Aufgaben machen die haben mich noch zusätlich verwirrt. Aber dies war sicherlich keine Abbsicht. Organisatorich hat für mich alles super gepasst, vorallem mit den 5 verschieden Abganen.  

<br>
