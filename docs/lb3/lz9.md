# Indexierungsarten

## Entscheidung für Indexierungstypen

Indextypen | Beschreibung | Link
:-------- | :----------  | :----------
Primary Key |   Je Tabelle ist nur ein Primary Key möglich, dies ist typischerweise die ID-Spalte. Jeder Eintrag in dieser Spalte muss eindeutig sein, eine Doppelung ist ausgeschlossen. Der Primary Key unterscheidet sich nicht von Unique, nur dass es maximal einen Primary Key pro Tabelle geben darf. |  https://www.w3schools.com/sql/sql_primarykey.asp
Foreign Key   |   Der Foreign Key braucht es für die Verbindung zwischen den Tabellen er wird auch Indexiert. | https://www.w3schools.com/sql/sql_foreignkey.asp
Unique   |   Spalten mit einem Index des Typs Unique können nur eindeutige Werte enthalten. Dass zwei Datensätze den selben Wert in der Spalte enthalten ist ausgeschlossen. | https://www.w3schools.com/sql/sql_unique.asp
Index |   Spalten die mittels Index gekennzeichnet werden können im Gegensatz zu Unique und Primary Key auch doppelte Werte in der Spalte enthalten. |  https://www.w3schools.com/sql/sql_create_index.asp
Fulltext |    Der Typ Fulltext ist geeignet für Spalten die längere Texte enthalten. Jedes Wort wird dabei indiziert und eine Suche nach einzelnen Wörtern oder Teilwörtern ist möglich. Diesen Typ zu wählen macht nur Sinn, wenn mit der Volltextsuche von MySQL gearbeitet wird. | https://www.w3schools.com/sql/sql_create_index.asp


<br>
<br>

## Primary Key

```SQL
CREATE TABLE IF NOT EXISTS roehFix.sensoren (
  sensorenID INT NOT NULL AUTO_INCREMENT,
  kennung VARCHAR(20) NOT NULL,
  PRIMARY KEY (sensorenID),
ENGINE = InnoDB;
```

<br>
<br>

## Foreign Key

<img width="40%" src='./bilder/gHasS.png'></img>

```SQL
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

<br>

<img width="40%" src='./bilder/kunden.png'></img>

```SQL
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
```

<br>
<br>

## Unique

```SQL
CREATE TABLE IF NOT EXISTS roehFix.sensoren (
  sensorenID INT NOT NULL AUTO_INCREMENT,
  PRIMARY KEY (sensorenID),
  UNIQUE KEY unique_kennung (kennung))
ENGINE = InnoDB;
```

<br>
<br>

## Index

```SQL
CREATE TABLE IF NOT EXISTS roehFix.adressen (
  adressenID INT NOT NULL AUTO_INCREMENT,
  strasse VARCHAR(30) NOT NULL,
  plz SMALLINT(6) NOT NULL,
  stadt VARCHAR(20) NOT NULL,
  PRIMARY KEY (adressenID),
  INDEX (strasse ASC))
ENGINE = InnoDB;
```

<br>
<br>

## Fulltext 

```
CREATE TABLE tutorial (
  id INT UNSIGNED AUTO_INCREMENT NOT NULL PRIMARY KEY, 
  title VARCHAR(200), 
  description TEXT, 
  FULLTEXT(title,description)
) ENGINE=InnoDB;
```


<br>
<br>


## ERM
<img width="100%" src='./bilder/ERM.png'></img>
