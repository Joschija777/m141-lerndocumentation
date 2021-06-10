# MySQL-Script (ERD)

## ERM
<img width="100%" src='./bilder/ERM.png'></img>

<br>
<br>

## Script


```SQL

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
  kontaktdatenID INT NOT NULL AUTO_INCREMENT,
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
  adressenID INT NOT NULL AUTO_INCREMENT,
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
  gatwaysID INT NOT NULL AUTO_INCREMENT,
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
  sensorenID INT NOT NULL AUTO_INCREMENT,
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
  typID INT NOT NULL AUTO_INCREMENT,
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
  sensordatenID INT NOT NULL AUTO_INCREMENT,
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



```

```SQL

CREATE DATABASE IF NOT EXISTS dbPerProJG DEFAULT CHARACTER SET utf8 ;
USE dbPerProJG ;


CREATE TABLE IF NOT EXISTS dbPerProJG.tblPerson (
  perIDJG INT NOT NULL AUTO_INCREMENT,
  perNameJG VARCHAR(18) NOT NULL,
  abtIDJG INT,
  PRIMARY KEY (perIDJG),
  FOREIGN KEY (abtIDJG) REFERENCES dbPerProJG.tblAbteilungJG(abtIDJG))
ENGINE = InnoDB;

CREATE TABLE IF NOT EXISTS dbPerProJG.tblAbteilung (
  abtIDJG INT NOT NULL AUTO_INCREMENT,
  abtNameJG VARCHAR(25) NOT NULL,
  PRIMARY KEY (abtIDJG))
ENGINE = InnoDB;

CREATE TABLE IF NOT EXISTS dbPerProJG.tblProJG (
  proIDJG INT NOT NULL AUTO_INCREMENT,
  proNameJG VARCHAR(18) NOT NULL,
  proStdJG INT,
  PRIMARY KEY (perIDJG))
ENGINE = InnoDB;

CREATE TABLE IF NOT EXISTS dbPerProJG.perHasAbt (
  perPerID INT NOT NULL,
  proProID INT NOT NULL,
  PRIMARY KEY (perPerID, proProID),
  FOREIGN KEY (perPerID) REFERENCES dbPerProJG.gatways(gatwaysID),
  FOREIGN KEY (proProID) REFERENCES dbPerProJG.sensoren(sensorenID),
  UNIQUE KEY unique_proProID (proProID ASC),
  UNIQUE KEY unique_perPerID (perPerID ASC)
  )
ENGINE = InnoDB;


```

<br>
<br>

## Reproduzierbar:

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
