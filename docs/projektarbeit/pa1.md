# PA 1: Installation eines RDBMS

<br>

## 1.1 Recherche zu MySQL

#### 1.1.1 Hersteller:
- 1994 vom schwedischen Unternehmen MySQL AB entwickelt
- 2008 wurde MySQL AB vom Unternehmen Sun Microsystems übernommen
- 2010 von Oracle gekauft

<br>

#### 1.1.2 Lizenzen:
__MySQL Standard Edition__   
- Preis
    - 2000 USD
- Features MySQL
  - Database Server
  - Connectors
  - Replication
  - Workbench  
- Produkt Zertifikation
  - Oracle Linux
  - Oracle VM
  - Oracle Solaris

<br>


__MySQL Enterprise Edition__
    
- Preis
  - 5000 USD
- Features MySQL    
  - Database Server
  - Document Store
  - Connectors
  - Replication
  - Router
  - Partitoning
  - Workbench
  - Oracle Enterprise Manager
  - Enterprise Monitor
  - Enterprise Backup
  - Enterprise Security
- Produkt Zertifikation
  - Oracle Linux
  - Oracle VM
  - Oracle Solaris
  - Oracle Enterprise Manager
  - Oracle GoldenGate
  - Oracle Data Integrator

<br>


__MySQL Cluster Carrier Grade Edition__
- Preis
  - 10000 USD
- Features MySQL
  - Database Server
  - Document Store
  - Connectors
  - Replication
  - Router
  - Partitoning
  - Workbench
  - Oracle Enterprise Manager
  - Enterprise Monitor
  - Enterprise Backup
  - Enterprise Security
  - Cluster Manager
- Produkt Zertifikation
  - Oracle Linux
  - Oracle VM
  - Oracle Solaris
  - Oracle Enterprise Manager
  - Oracle GoldenGate
  - Oracle Data Integrator

<br>
<br>

#### 1.1.3 Support:

__Premier__
- Dauer
    - 1 - 5 Jahre
- Umfasst
    - MySQL-Wartungsversionen
    - Updates
    - Fehlerkorrektur
    - Sicherheitswarnungen

<br>

__Extended__
- Dauer
  - 6 - 8 Jahre
- Umfasst
  - MySQL-Wartungsversionen
  - Updates
  - Fehlerkorrektur
  - Sicherheitswarnungen

<br>

__Sustain__
- Dauer
  - ab 9 Jahre
- Umfasst
  - Updates
  - Korrekturen
  - Warnungen


<br>
<br>

#### 1.1.4 Software:
- MySQL ist ein Open-Source-Datenbank-Management-System (RDBMS)
- SQL ist die Abkürzung für Structured Query Language
- Neuste Version ist 8.0.23 stand 26.02.2021
- MySQL in 23 Sprachen verfügbar
  

<br>
<br>
<br>
<br>






## 1.2 Voraussetzungen der Installation (VM) 

#### 1.2.1 OS & Hardware

__Betriebsystem:__

<img width="80%" src='./bilder/OS_Version.png'></img>

> [!NOTE|style:flat]
> OS Version: Linux Ubuntu 64GB

<br>

__Hardware:__

<img width="80%" src='./bilder/Konfiguration_VM2.png'></img>

<img width="80%" src='./bilder/Konfiguration_VM1.png'></img>

> [!NOTE|style:flat]
> - CPU: 1 Prozessor
> - RAM: 4096 MB
> - Grafikspeicher: 16MB
> - SSD: 10GB
> - Notebook

<br>
<br>

#### 1.2.2 OS Version & Kernel

__OS Version:__

```Terminal
lsb_release -a
```

<img width="100%" src='./bilder/osVersion.png'></img>

> [!NOTE|style:flat]
> OS_Version: Ubuntu 20.10

<br>

__Kernel:__

```Terminal
hostnamectl | grep Kernel
```

<img width="100%" src='./bilder/kernel.png'></img>

> [!NOTE|style:flat]
> Kernel: Linux 5.8.0-44-generic

<br>

#### 1.2.3 Installations Quelle

> [!TIP|style:flat]
> Download Ubuntu Server (neuste Version): https://ubuntu.com/download/server

<br>
<br>

#### 1.2.4 Software Version & Abhängigkeiten

__Software Version:__

<img width="100%" src='./bilder/mysqlVersion.png'></img>

> [!NOTE|style:flat]
> Die Software MYSQL wird in der Version: 8.0.23 installiert. Das ist der Stand vom 04.03.2021.


<br>


__Abhängigkeit:__

<img width="100%" src='./bilder/mysql_ab.png'></img>

> [!NOTE|style:flat]
> Zusätzliche Packete 
> - libmecab2 
> - mecab-ipadic 
> - mecab-ipadic-utf8 
> - mecab-utils 
> - mysql-client-8.0
> - mysql-client-core-8.0 
> - mysql-common 
> - mysql-server 
> - mysql-server-8.0
> - mysql-server-core-8.0


<br>
<br>

#### 1.2.5 Sonstige Serverdienste

```Terminal
service --status-all
```

<img width="100%" src='./bilder/services.png'></img>

> [!NOTE|style:flat]
> - (+) laufende Services
> - (-) angehaltene Services


<br>
<br>
<br>
<br>


## 1.3 Prozess der Installation

#### 1.3.1 Software Version & Abhängigkeiten

__Software Version:__

```Terminal
mysql -V
```

<img width="100%" src='./bilder/mysqlVersion.png'></img>

<br>



__Abhängigkeit:__

```Terminal
sudo apt install mysql-server
```

<img width="100%" src='./bilder/mysqlVersion.png'></img>

> [!NOTE|style:flat]
> Sobald man einen **apt install mysql-server** macht werden die Abhängikeiten automatisch installiert.

<br>
<br>

<br>
<br>

#### 1.3.2 Installations Ablauf & Installationsschritte

__1. Ubuntu update und upgrade:__

```Terminal
sudo apt-get update && apt-get uprade
```
<img width="100%" src='./bilder/mysql_1.png'></img>

<img width="100%" src='./bilder/mysql_2.png'></img>

> [!WARNING|style:flat]
> Befor man die Installtion mysql startet sollte man ubuntu und alle Packes auf den neusten Stand bringen. 

<br>

__2. Installation MYSQL:__

```Terminal
sudo apt install mysql-server
```

<img width="100%" src='./bilder/mysql_3.png'></img>

<br>

__3. Konfiguration MYSQL:__

```Terminal
sudo mysql_secure_installation
```
<img width="100%" src='./bilder/mysql_4.png'></img>

<img width="100%" src='./bilder/mysql_5.png'></img>

> [!NOTE|style:flat]
> 1. Yes (Y)
> 2. Strong (2)
> 3. Root Password

<br>
<br>
<br>
<br>

## 1.4 Test der Installation

__Service Test:__

```Terminal
sudo service mysql status
```

<img width="100%" src='./bilder/mysql_status.png'></img>

> [!TIP|style:flat]
> Wenn der status aktive ist ist der Service am laufen!

<br>
<br>
<br>

__Beispiel Tabelle:__

```Terminal
sudo mysql
```

> [!NOTE|style:flat]
> zuerst muss ich das MYSQL Kommandozeile öffnen

<br>

__1. Datenbank Erstellen__

```mysql
create database dbname;
```

<img width="100%" src='./bilder/mysql_be1.png'></img>

> [!NOTE|style:flat]
> Datenbank wurde erstellt!

<br>

__2. Datenbank auswählen__

```mysql
use dbname;
```

<img width="100%" src='./bilder/mysql_be2.png'></img>

> [!NOTE|style:flat]
>  Über diesen Befehl verbindet man sich direkt mit einer Datenbank! Dies hat den Vorteil, dass die Befehle direkt ausgeführt werden können!

<br>

__3. Datenbank löschen__

```mysql
drop database dbname;
```

<img width="100%" src='./bilder/mysql_be3.png'></img>

> [!NOTE|style:flat]
> Datenbank wird gelöscht!

<br>

__4. Tabelle erstellen__

```mysql
create table tblname (
id int not null,
column1 int (11),
column2 varchar (100)
);
```

<img width="100%" src='./bilder/mysql_be4.png'></img>

> [!NOTE|style:flat]
> hier muss man natürlich wissen, was man haben möchte! Hier in diesem Beispiel wird eine Tabelle mit drei Spalten erstellt!
> - Spalte1 -> “id” -> eindeutige Zuordnung der Spalte
> - Spalte2 -> “int” -> eine Spalte für Zahlen
> - Spalte3 -> “varchar” -> Spalte für Buchstaben und Zahlen

<br>

__5. Tabellen anzeigen__

```mysql
show tables;
```

<img width="100%" src='./bilder/mysql_be5.png'></img>

> [!NOTE|style:flat]
> zeigt die Tabellen einer Datenbank an

<br>

__6. Tabellenstruktur anzeigen__

```mysql
show fields from tblname;
```

<img width="100%" src='./bilder/mysql_be6.png'></img>

> [!NOTE|style:flat]
> zeigt den Inhalt von einer Tabelle an

<br>



