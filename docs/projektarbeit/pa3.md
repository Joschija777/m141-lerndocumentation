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

<br>
<br>

#### 3.2.2 Datentypen zweckmässig / angepasst

<br>
<br>

#### 3.2.3 Inhaltlich korrekt (Anforderungen abgedeckt)

<br>
<br>
<br>
<br>

## 3.3 Script


~~~SQL

-- -----------------------------------------------------
-- Datenbank erstellen RoehFix
-- Datenbank auswählen
-- -----------------------------------------------------
CREATE DATABASE IF NOT EXISTS RoehFix DEFAULT CHARACTER SET utf8 ;
USE RoehFix ;

-- -----------------------------------------------------
-- Tabelle RoehFix.Kontaktdaten erstellen
-- Attribute (KontaktdatenID, Telefonnummer, Email) hinzufügen
-- Primärschlüssel definieren (KontaktdatenID)
-- Indexierung für schnellere Suche (Telefonnummer, Email)
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS RoehFix.Kontaktdaten (
  KontaktdatenID INT NOT NULL,
  Telefonnummer VARCHAR(18) NOT NULL,
  Email VARCHAR(45) NOT NULL,
  PRIMARY KEY (KontaktdatenID),
  INDEX (Telefonnummer ASC),
  INDEX (Email ASC))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Tabelle RoehFix.Adressen erstellen
-- Attribute (AdressenID, Strasse, PLZ, Stadt) hinzufügen
-- Primärschlüssel definieren (AdressenID)
-- Indexierung für schnellere Suche (Telefonnummer, Email)
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS RoehFix.Adressen (
  AdressenID INT NOT NULL,
  Strasse VARCHAR(30) NOT NULL,
  PLZ SMALLINT(6) NOT NULL,
  Stadt VARCHAR(20) NOT NULL,
  PRIMARY KEY (AdressenID),
  INDEX (Strasse ASC))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table RoehFix.Kunden
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS RoehFix.Kunden (
  KundenNr VARCHAR(8) NOT NULL,
  Vorname VARCHAR(25) NOT NULL,
  Nachname VARCHAR(25) NOT NULL,
  Technische_Kontaktdaten INT NOT NULL,
  Administrative_Kontaktdaten INT NOT NULL,
  Kontaktadresse INT NOT NULL,
  Rechnungsadresse INT NOT NULL,
  PRIMARY KEY (KundenNr),
  FOREIGN KEY (Technische_Kontaktdaten REFERENCES RoehFix.Kontaktdaten(KontaktdatenID),
  FOREIGN KEY (Administrative_Kontaktdaten) REFERENCES RoehFix.Kontaktdaten(KontaktdatenID),
  FOREIGN KEY (Kontaktadresse) REFERENCES RoehFix.Adressen(AdressenID),
  FOREIGN KEY (Rechnungsadresse) REFERENCES RoehFix.Adressen(AdressenID),
  INDEX (Vorname ASC),
  INDEX (Nachname ASC))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table RoehFix.Gatways
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS RoehFix.Gatways (
  GatwaysID INT NOT NULL,
  Kennung VARCHAR(20) NOT NULL,
  LaengeKoordinaten FLOAT NOT NULL,
  BreiteKoordinaten FLOAT NOT NULL,
  Beschreibung LONGTEXT NULL,
  KundenNr VARCHAR(8) NOT NULL,
  PRIMARY KEY (GatwaysID),
  FOREIGN KEY (KundenNr) REFERENCES RoehFix.Kunden(KundenNr),
  INDEX (Kennung))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table RoehFix.Sensoren
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS RoehFix.Sensoren (
  SensorenID INT NOT NULL,
  Kennung VARCHAR(20) NOT NULL,
  LaengeKoordination FLOAT NOT NULL,
  BreiteKoordination FLOAT NOT NULL,
  PRIMARY KEY (SensorenID))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table RoehFix.Typ
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS RoehFix.Typ (
  TypID INT NOT NULL,
  Heizung VARCHAR(25) NOT NULL,
  Temperatur FLOAT NOT NULL,
  Klima VARCHAR(30) NULL,
  SensorenID INT,
  PRIMARY KEY (TypID),
  FOREIGN KEY (SensorenID) REFERENCES RoehFix.Sensoren(SensorenID),
  INDEX (Heizung ASC))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table RoehFix.Sensordaten
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS RoehFix.Sensordaten (
  SensordatenID INT NOT NULL,
  Daten FLOAT NOT NULL,
  Zeitpunkt DATETIME(6) NOT NULL,
  SensorenID INT NOT NULL,
  PRIMARY KEY (SensordatenID),
  FOREIGN KEY (SensorenID) REFERENCES RoehFix.Sensoren(SensorenID),
  INDEX (Zeitpunkt ASC),
  INDEX (Daten ASC))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table RoehFix.Gatways_has_Sensoren
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS RoehFix.Gatways_has_Sensoren (
  Gatways_GatwaysID INT NOT NULL,
  Sensoren_SensorenID INT NOT NULL,
  PRIMARY KEY (Gatways_GatwaysID, Sensoren_SensorenID),
  FOREIGN KEY (Gatways_GatwaysID) REFERENCES RoehFix.Gatways(GatwaysID),
  FOREIGN KEY (Sensoren_SensorenID) REFERENCES RoehFix.Sensoren(SensorenID),
  INDEX (Sensoren_SensorenID ASC),
  INDEX (Gatways_GatwaysID ASC)
  )
ENGINE = InnoDB;



~~~


~~~SQL

-- -----------------------------------------------------
-- Datenbank erstellen RoehFix
-- Datenbank auswählen
-- -----------------------------------------------------
CREATE DATABASE IF NOT EXISTS `RoehFix` DEFAULT CHARACTER SET utf8 ;
USE `RoehFix` ;

-- -----------------------------------------------------
-- Table `RoehFix`.`Kontaktdaten`

-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `RoehFix`.`Kontaktdaten` (
  idKontaktdaten INT NOT NULL,
  `Telefonnummer` VARCHAR(18) NOT NULL,
  `Email` VARCHAR(45) NOT NULL,
  PRIMARY KEY (`idKontaktdaten`),
  UNIQUE INDEX `Telefonnummer_UNIQUE` (`Telefonnummer` ASC),
  UNIQUE INDEX `Email_UNIQUE` (`Email` ASC))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `RoehFix`.`Adressen`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `RoehFix`.`Adressen` (
  `idAdressen` INT NOT NULL,
  `Strasse` VARCHAR(30) NOT NULL,
  `PLZ` SMALLINT(6) NOT NULL,
  `Stadt` VARCHAR(20) NOT NULL,
  PRIMARY KEY (`idAdressen`),
  UNIQUE INDEX `Strasse_UNIQUE` (`Strasse` ASC))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `RoehFix`.`Kunden`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `RoehFix`.`Kunden` (
  `KundenNr.` VARCHAR(8) NOT NULL,
  `Technische_Kontaktdaten` INT NOT NULL,
  `Administrative_Kontaktdaten` INT NOT NULL,
  `Kontaktadresse` INT NOT NULL,
  `Rechnungsadresse` INT NOT NULL,
  PRIMARY KEY (`KundenNr.`, `Technische_Kontaktdaten`, `Administrative_Kontaktdaten`, `Kontaktadresse`, `Rechnungsadresse`),
  INDEX `fk_Kunden_Kontaktdaten1_idx` (`Technische_Kontaktdaten` ASC),
  INDEX `fk_Kunden_Kontaktdaten2_idx` (`Administrative_Kontaktdaten` ASC),
  INDEX `fk_Kunden_Adressen1_idx` (`Kontaktadresse` ASC),
  INDEX `fk_Kunden_Adressen2_idx` (`Rechnungsadresse` ASC),
  CONSTRAINT `fk_Kunden_Kontaktdaten1`
    FOREIGN KEY (`Technische_Kontaktdaten`)
    REFERENCES `RoehFix`.`Kontaktdaten` (`idKontaktdaten`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_Kunden_Kontaktdaten2`
    FOREIGN KEY (`Administrative_Kontaktdaten`)
    REFERENCES `RoehFix`.`Kontaktdaten` (`idKontaktdaten`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_Kunden_Adressen1`
    FOREIGN KEY (`Kontaktadresse`)
    REFERENCES `RoehFix`.`Adressen` (`idAdressen`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_Kunden_Adressen2`
    FOREIGN KEY (`Rechnungsadresse`)
    REFERENCES `RoehFix`.`Adressen` (`idAdressen`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `RoehFix`.`Gatways`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `RoehFix`.`Gatways` (
  `idGatways` INT NOT NULL,
  `Kennung` VARCHAR(20) NOT NULL,
  `LaengeKoordination` FLOAT NOT NULL,
  `BreiteKoordination` FLOAT NOT NULL,
  `Beschreibung` LONGTEXT NULL,
  `Kunden_KundenNr.` VARCHAR(8) NOT NULL,
  PRIMARY KEY (`idGatways`),
  INDEX `fk_Gatways_Kunden1_idx` (`Kunden_KundenNr.` ASC),
  CONSTRAINT `fk_Gatways_Kunden1`
    FOREIGN KEY (`Kunden_KundenNr.`)
    REFERENCES `RoehFix`.`Kunden` (`KundenNr.`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `RoehFix`.`Sensoren`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `RoehFix`.`Sensoren` (
  `idSensoren` INT NOT NULL,
  `Kennung` VARCHAR(20) NOT NULL,
  `LaengeKoordination` FLOAT NOT NULL COMMENT '\n',
  `BreiteKoordination` FLOAT NOT NULL,
  PRIMARY KEY (`idSensoren`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `RoehFix`.`Typ`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `RoehFix`.`Typ` (
  `idTyp` INT NOT NULL,
  `Heizung` VARCHAR(25) NOT NULL,
  `Temperatur` FLOAT NOT NULL,
  `Klima` VARCHAR(30) NULL,
  `Sensoren_idSensoren` INT NOT NULL,
  PRIMARY KEY (`idTyp`, `Sensoren_idSensoren`),
  INDEX `fk_Typ_Sensoren1_idx` (`Sensoren_idSensoren` ASC),
  CONSTRAINT `fk_Typ_Sensoren1`
    FOREIGN KEY (`Sensoren_idSensoren`)
    REFERENCES `RoehFix`.`Sensoren` (`idSensoren`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `RoehFix`.`Sensordaten`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `RoehFix`.`Sensordaten` (
  `idSensordaten` INT NOT NULL,
  `Daten` FLOAT NOT NULL,
  `Zeitpunkt` DATETIME(6) NOT NULL,
  `Sensoren_idSensoren` INT NOT NULL,
  PRIMARY KEY (`idSensordaten`, `Sensoren_idSensoren`),
  INDEX `fk_Sensordaten_Sensoren1_idx` (`Sensoren_idSensoren` ASC),
  CONSTRAINT `fk_Sensordaten_Sensoren1`
    FOREIGN KEY (`Sensoren_idSensoren`)
    REFERENCES `RoehFix`.`Sensoren` (`idSensoren`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `RoehFix`.`Gatways_has_Sensoren`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `RoehFix`.`Gatways_has_Sensoren` (
  `Gatways_idGatways` INT NOT NULL,
  `Sensoren_idSensoren` INT NOT NULL,
  PRIMARY KEY (`Gatways_idGatways`, `Sensoren_idSensoren`),
  INDEX `fk_Gatways_has_Sensoren_Sensoren1_idx` (`Sensoren_idSensoren` ASC),
  INDEX `fk_Gatways_has_Sensoren_Gatways1_idx` (`Gatways_idGatways` ASC),
  CONSTRAINT `fk_Gatways_has_Sensoren_Gatways1`
    FOREIGN KEY (`Gatways_idGatways`)
    REFERENCES `RoehFix`.`Gatways` (`idGatways`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_Gatways_has_Sensoren_Sensoren1`
    FOREIGN KEY (`Sensoren_idSensoren`)
    REFERENCES `RoehFix`.`Sensoren` (`idSensoren`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


SET SQL_MODE=@OLD_SQL_MODE;
SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS;
SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS;

~~~



reproduzierbar?
Beschreiben?

<br>
<br>
<br>
<br>

## 3.4 Indexierung

#### 3.4.1 Argumentative Entscheidung für Indexierungstypen

<br>
<br>

#### 3.4.2 Argumentative Entscheidung für indizierte Attribute

<br>
<br>

#### 3.4.3 Umsetzung in Script separat erklärt

