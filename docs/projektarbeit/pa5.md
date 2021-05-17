
# PA 5: Sichern und dokumentieren der Arbeitsschritte 
    
## 5.1 Installation Apache2 und PHP

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










### 5.1.1 Dokumentieren Sie die Installation von Apache2
        

<br>
<br>

### 5.1.2 Dokumentieren Sie die Installation von PHP (oder entsprechende Technologie)



<br>
<br>
<br>
<br>

## 5.2 Einrichten Applikationsbenutzer für die Visualisierungszugriffe
        
### 5.2.1 Benutzer erstellen
        
        
<br>
<br>
       
### 5.2.2 Berechtigungen erstellt


<br>
<br>

### 5.2.3 Zugriff getestet


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
