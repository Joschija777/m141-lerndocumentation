# PA 3:  Anlegen der Datenbanken und Tabelle



## 3.1 ERD / ERM / Normalisierung

#### 3.1.1 ERD

__Erste Überlegung__
<img width="100%" src='./bilder/ERD_1.jpg'></img>

> [!TIP|style:flat]
>
> __Vorgang:__
> 1. Alle Entitäten vom Text aufgeschrieben.
> 2. Mit der wichtigsten Entität (Kunde) angefangen.
> 3. Alle Verbindungen zwischen den Entitäten aufgezeichnet.
> 4. Falls m zu n eine Zwischentabelle gemacht.
> 5. Alle Attribute zu den Entitäten hinzugefügt.
> 6. Primary Key ausgesucht.

<br>

__Fertiges ERD__
<img width="100%" src='./bilder/ERD_2.jpg'></img>

> [!TIP|style:flat]
>
> __Vorgang:__
> 1. Erstes ERD nochmals ruhig durchdenken.
> 2. Überprüfen auf Tabellen die man nicht braucht z.B leer nur Foreign Key
> 3. Überprüfen ob Tabellen nicht auch ein Attribut sein kann.
> 4. Auf Doppelte werte schauen.
> 5. Falls Doppelte werte vorhanden umbauen.

<br>
<br>

#### 3.1.2 ERM
<img width="100%" src='./bilder/ERM.png'></img>

> [!NOTE|style:flat]
> Ich habe das ERM fast 1 zu 1 wie das ERD erstellt. Es hat noch paar kleine Abänderungen, der Grösste unterschied ist das ich die Tabelle Sensordaten vergessen habe.

<br>
<br>

#### 3.1.3 Normalisierung

__Erstes ERD__
1. Text durchlesen
2. Entitäten erfassen und aufzeichnen (Kunden, Adressen, Gatway, Sensoren, GeoPosition, ...)
3. Attribute zu den Entitäten vom Text aufschreiben
4. Verbindungen zwischen den Entitäten erstellen
5. Primary Key bestimmen

__*Genauers ERD__
1. Erstes ERD nochmals ruhig durchdenken.
2. Überprüfen auf Tabellen die man nicht braucht z.B leer nur Foreign Key
3. Überprüfen ob Tabellen nicht auch ein Attribut sein kann.
4. Auf Doppelte werte schauen.
5. Falls Doppelte werte vorhanden umbauen.

__ERM__
1. Das ganze Darstellen wie beim ERM
2. Alle Foreign Key erstellen.
3. Den text nochmals durchlesen ob es zusätlich Angaben gibt.
4. Da man bei ERM eine bessere Übersicht hat sieht man schnell ob man noch Fehler hat.

> [!WARNING|style:flat]
> *Genaueres ERD --> muss nicht zwingend sein, mann kan auch die Verbesserungen direkt beim ERM machen.
>
> Die Normalisierung sieht man auch auf den einzelnen Bilder oben. Das ERM muss noch nicht perfekt sein, man sieht die Fehler, dann wenn man ein Script erstellen und repliziert. Später auch mit Testdaten.



<br>
<br>
<br>
<br>

## 3.2 Datentypen / Attribute

#### 3.2.1 Syntax eingehalten

```SQL
CREATE TABLE IF NOT EXISTS roehFix.gatways (
  gatwaysID INT NOT NULL,
  kennung VARCHAR(20) NOT NULL,
  laengeKoordinaten FLOAT NOT NULL,
  breiteKoordinaten FLOAT NOT NULL,
  beschreibung LONGTEXT NULL,
  kundenNr VARCHAR(8) NOT NULL,
  PRIMARY KEY (gatwaysID),
  FOREIGN KEY (kundenNr) REFERENCES roehFix.kunden(kundenNr),
  UNIQUE KEY unique_kennung (kennung))
ENGINE = InnoDB;
```

> [!TIP|style:flat]
> CamelCase = Bei Camel Case wird das erste Wort immer klein geschrieben und jedes folgende Wort mit einem Großbuchstaben begonnen, ohne dass dazwischen ein Leerzeichen oder ein anderes Trennzeichen kommt.

<br>
<br>

#### 3.2.2 Datentypen zweckmässig / angepasst

__Verwendete Datentypen erklärt:__

Datentyp | Verwendung im Projekt  | Beschreibung  
:-------- | :---------- | :---------- 
VARCHAR |  E-Mail,  Telefonnummer(wegen 0 kein Double), Strasse, Stadt, Name,   |    Zeichenkette variabler Länge, Maximum ist M. Wertebereich für M: 0 bis 255.
INT |  Primary Key wie(ID), FOREIGN KEY   |    Ganzzahlen von 0 bis ~4,3 Mill. oder von -2.147.483.648 bis 2.147.483.647.
SMALLINT |  Kleine Zahlen wie(Postleizahl)   |    	Ganzzahlen von 0 bis 65.535 oder von -32.768 bis 32.767.
FLOAT |  Daten, Temperatur, BreiteKoordinaten, LaengeKoordinaten   |    	Fließkommazahl mit Vorzeichen. Wertebereich von -(3,402823466×1038) bis -(1,175494351×10-38)



<br>
<br>

#### 3.2.3 Inhaltlich korrekt (Anforderungen abgedeckt)

__Zu den Anforderungen:__

<img width="60%" src='./bilder/Anforderungen.png'></img>

https://moodle.bztf.ch/pluginfile.php/106086/mod_resource/content/1/site/02_PA_18-22/712_PA3/

<br>
<br>
<br>
<br>

## 3.3 Script


~~~SQL

-- -----------------------------------------------------
-- Datenbank erstellen roehFix
-- Datenbank auswählen
-- -----------------------------------------------------
CREATE DATABASE IF NOT EXISTS roehFix DEFAULT CHARACTER SET utf8 ;
USE roehFix ;

-- -----------------------------------------------------
-- Tabelle roehFix.Kontaktdaten erstellen
-- Attribute (KontaktdatenID, Telefonnummer, Email) hinzufügen
-- Primärschlüssel definieren (KontaktdatenID)
-- Indexierung für schnellere Suche (Telefonnummer, Email)
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS roehFix.kontaktdaten (
  kontaktdatenID INT NOT NULL,
  telefonnummer VARCHAR(18) NOT NULL,
  email VARCHAR(45) NOT NULL,
  PRIMARY KEY (kontaktdatenID),
  INDEX (telefonnummer ASC),
  INDEX (email ASC))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Tabelle RoehFix.Adressen erstellen
-- Attribute (AdressenID, Strasse, PLZ, Stadt) hinzufügen
-- Primärschlüssel definieren (AdressenID)
-- Indexierung für schnellere Suche (Telefonnummer, Email)
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS roehFix.adressen (
  adressenID INT NOT NULL,
  strasse VARCHAR(30) NOT NULL,
  plz SMALLINT(6) NOT NULL,
  stadt VARCHAR(20) NOT NULL,
  PRIMARY KEY (adressenID),
  INDEX (strasse ASC))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Tabelle RoehFix.Kunden erstellen
-- Attribute (KundenID, Vorname, Nachname) hinzufügen
-- Primärschlüssel definieren (KundenID)
-- Foreign Key(Technische_Kontaktdaten,  Administrative_Kontaktdaten, Kontaktadresse, Rechnungsadresse)
-- Indexierung für schnellere Suche (Vorname, Nachname)
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS roehFix.kunden (
  kundenNr VARCHAR(8) NOT NULL,
  vorname VARCHAR(25) NOT NULL,
  nachname VARCHAR(25) NOT NULL,
  technischeKontaktdaten INT NOT NULL,
  administrativeKontaktdaten INT NOT NULL,
  kontaktAdresse INT NOT NULL,
  rechnungsAdresse INT NOT NULL,
  PRIMARY KEY (kundenNr),
  FOREIGN KEY (technischeKontaktdaten) REFERENCES roehFix.kontaktdaten(kontaktdatenID),
  FOREIGN KEY (administrativeKontaktdaten) REFERENCES roehFix.kontaktdaten(kontaktdatenID),
  FOREIGN KEY (kontaktAdresse) REFERENCES roehFix.adressen(adressenID),
  FOREIGN KEY (rechnungsAdresse) REFERENCES roehFix.adressen(adressenID),
  INDEX (vorname ASC),
  INDEX (nachname ASC))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Tabelle roehFix.Gatways erstellen
-- Attribute (GatwaysID, Kennung, LKordinaten, BKordinate, Beschreibung) hinzufügen
-- Primärschlüssel definieren (GatwaysID)
-- Foreign Key(KundenNr)
-- Indexierung für schnellere Suche (Kennung)
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS roehFix.gatways (
  gatwaysID INT NOT NULL,
  kennung VARCHAR(20) NOT NULL,
  laengeKoordinaten FLOAT NOT NULL,
  breiteKoordinaten FLOAT NOT NULL,
  beschreibung LONGTEXT NULL,
  kundenNr VARCHAR(8) NOT NULL,
  PRIMARY KEY (gatwaysID),
  FOREIGN KEY (kundenNr) REFERENCES roehFix.kunden(kundenNr),
  UNIQUE KEY unique_kennung (kennung))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Tabelle roehFix.Sensoren erstellen
-- Attribute (SensorenID, Kennung, LKordinaten, BKordinate) hinzufügen
-- Primärschlüssel definieren (SensorenID)
-- Indexierung für schnellere Suche (Kennung)
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS roehFix.sensoren (
  sensorenID INT NOT NULL,
  kennung VARCHAR(20) NOT NULL,
  laengeKoordination FLOAT NOT NULL,
  breiteKoordination FLOAT NOT NULL,
  PRIMARY KEY (sensorenID),
  UNIQUE KEY unique_kennung (kennung))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Tabelle roehFix.Typ erstellen
-- Attribute (TypID, Heizung,Temperatur, Klima) hinzufügen
-- Primärschlüssel definieren (TypID)
-- Foreign Key(sensorenID)
-- Indexierung für schnellere Suche (Heizung)
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS roehFix.typ (
  typID INT NOT NULL,
  heizung VARCHAR(25) NOT NULL,
  temperatur FLOAT NOT NULL,
  klima VARCHAR(30) NULL,
  sensorenID INT,
  PRIMARY KEY (typID),
  FOREIGN KEY (sensorenID) REFERENCES roehFix.sensoren(sensorenID),
  UNIQUE KEY unique_heizung (heizung ASC))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Tabelle roehFix.sensorendaten erstellen
-- Attribute (sensorendatenID, Daten, Zeitpunkt) hinzufügen
-- Primärschlüssel definieren (sensorendatenID)
-- Foreign Key(sensorenID)
-- Indexierung für schnellere Suche (Daten)
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS roehFix.sensordaten (
  sensordatenID INT NOT NULL,
  daten FLOAT NOT NULL,
  zeitpunkt DATETIME(6) NOT NULL,
  sensorenID INT NOT NULL,
  PRIMARY KEY (sensordatenID),
  FOREIGN KEY (sensorenID) REFERENCES roehFix.sensoren(sensorenID),
  UNIQUE KEY unique_zeitpunkt (zeitpunkt ASC),
  INDEX (daten ASC))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Zwischentabelle roehFix.gatwayshas_sensoren erstellen
-- Attribute (gatwaysGatwaysID, sensorenSensorenID) hinzufügen
-- Primärschlüssel definieren (gatwaysGatwaysID, sensorenSensorenID)
-- Foreign Key(gatwaysGatwaysID, sensorenSensorenID)
-- Indexierung für schnellere Suche (gatwaysGatwaysID, sensorenSensorenID)
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS roehFix.gatwaysHasSensoren (
  gatwaysGatwaysID INT NOT NULL,
  sensorenSensorenID INT NOT NULL,
  PRIMARY KEY (gatwaysGatwaysID, sensorenSensorenID),
  FOREIGN KEY (gatwaysGatwaysID) REFERENCES roehFix.gatways(gatwaysID),
  FOREIGN KEY (sensorenSensorenID) REFERENCES roehFix.sensoren(sensorenID),
  UNIQUE KEY unique_sensorenSensorenID (sensorenSensorenID ASC),
  UNIQUE KEY unique_gatwaysGatwaysID (gatwaysGatwaysID ASC)
  )
ENGINE = InnoDB;



~~~

<br>
<br>

#### Reproduzierbar:

1. Script ausführen (wurde vorher im TMP Verzeichnis erstellt)

```sql
source /tmp/roehFix.sql
```
<img width="100%" src='./bilder/myScript.png'></img>

<br>

2. Kurzen Test!

```sql
USE Databse;
```

```sql
show tables;
```

```sql
show fields from Kunden;
```

<img width="100%" src='./bilder/myTest.png'></img>


<br>
<br>
<br>
<br>

## 3.4 Indexierung

#### 3.4.1 Argumentative Entscheidung für Indexierungstypen

<br>
<br>

#### 3.4.2 Argumentative Entscheidung für indizierte Attribute

__INDEX:__
- Telefonnummer: Später falls sich mehrere Kunden von der gleichen Firma ein Konto haben und sie eine allgemeine Telefonnummer haben.
- Email: Allgemeine Email von der Firma wo z.B ein Abteilung, daher können mehrere Kunden von eine Firma die gleiche Email haben, aber eine andere Telefonnummer.
- Strasse: In einer Strasse können mehrere wohnen.
- Vorname: Viele Personen haben den gleichen Vornamen.
- Nachname: Viele Personen haben den gleichen Nachnamen.

__UNIQUE:__

<br>
<br>

#### 3.4.3 Umsetzung in Script separat erklärt

