# PA 4:  Importieren von Testdaten


## 4.1 Testdatenimport für Kunden (SQL-Script mit Daten)



#### 4.1.1 SQL-Script mit allen "statischen" Kundeninformationen

```sql

-- -----------------------------------------------------
-- Datenbank roehFix auswählen
-- -----------------------------------------------------
USE roehFix ;

-- -----------------------------------------------------
-- Tabelle Adressen mit allen Attribute befüllen
-- 3 Besispieldaten eingetragen
-- -----------------------------------------------------
INSERT INTO `adressen` (`adressenID`, `strasse`, `plz`, `stadt`)
VALUES
  (1, 'Kesswilerstrasse 23', '8582', 'Dozwil'),
  (2, 'Uttwilerstrasse 11', '8000', 'Ustiwil'),
  (3, 'Teststrasse 1', '1000', 'Bern');

-- -----------------------------------------------------
-- Tabelle Konaktdaten mit allen Attribute befüllen
-- 3 Besispieldaten eingetragen
-- -----------------------------------------------------
INSERT INTO `kontaktdaten` (`kontaktdatenID`, `telefonnummer`, `email`)
VALUES
  (1, '+41 71 342 34 34', 'blabla@hotmail.com'),
  (2, '+41 71 111 11 11', 'joschija@hotmail.com'),
  (3, '+41 71 231 23 21', 'test@hotmail.com');

-- -----------------------------------------------------
-- Tabelle Kunden mit allen Attribute befüllen
-- Da Referenzen auf andere Tabelle kann die Daten erst nachher befüllt werden.
-- 3 Besispielkunden eingetragen
-- -----------------------------------------------------
INSERT INTO `kunden` (`kundenNr`, `vorname`, `nachname`, `technischeKontaktdaten`, `administrativeKontaktdaten`, `kontaktAdresse`, `rechnungsAdresse`)
VALUES
  ('K_01', 'Joschija', 'Gruss', '3', '3', '2', '2'),
  ('K_02', 'Max', 'Meier', '1', '1', '1', '1'),
  ('K_03', 'Fredy', 'Nur', '2', '2', '1', '1');

```

> [!WARNING|style:flat]
> Bei den Adressen und den Kontaktdaten könnte man die ID auch auf `null` setzen, da ich die Werte auf AUTO_INCREMENT gesetzt habe.
> Das Problem ist aber, falls man das Testen möchte und die Spalten nochmals löscht und neu erstellt stimmen bei den Kunden die Referenzen nicht mehr.
>
> Daher lieber bei Testdaten fixe ID geben!!!


__Löschen:__


__Datenbank auswählen:__

<br>
<br>

#### 4.1.2 Befehl um Daten einzulesen dokumentiert

__INSERT INTO:__

Die INSERT INTO Anweisung wird verwendet, um neue Datensätze in eine Tabelle einzufügen.

```sql
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);
```
> [!TIP|style:flat]
> Falls man alle Attribute von der Tabelle mitgeben möchte kann man die columen weglassen und nur table_name schreiben.

<br>

__INSERT INTO SELECT:__

Die INSERT INTO SELECT Anweisung kopiert Daten aus einer Tabelle und fügt sie in eine andere Tabelle ein.

```sql
INSERT INTO table2 (column1, column2, column3, ...)
SELECT column1, column2, column3, ...
FROM table1
WHERE condition;
```

> [!TIP|style:flat]
> Beispiel
> ```SQL
> INSERT INTO Customers (CustomerName, City, Country)
> SELECT SupplierName, City, Country FROM Suppliers
> WHERE Country='Germany';
> ```


<br>
<br>

#### 4.1.3 Printscreen für die erfolgreiche Ausführung

1. Ordner im tmp Verzeichnis erstellt.
```Terminal
sudo mkdir /tmp/sql
```

2. Sql Skript erstellet.
```Terminal
sudo nano /tmp/sql/testKunden.sql
```
<img width="100%" src='./bilder/sqlSkript.png'></img>


3. In mysql angemeldet
```Terminal
mysql -u root -p
```

4. SQL Skript ausgeführt.
```sql
source /tmp/sql/testKunden.sql;
```
<img width="60%" src='./bilder/sqlSkriptAus.png'></img>

5. Testen
```sql
SELECT * FROM kunden
```
<img width="100%" src='./bilder/sqlAbfrage.png'></img>

<br>
<br>
<br>
<br>


## 4.2 CSV-Datenimport Gatway-Daten



#### 4.2.1 CSV-Datei mit Gateway-Informationen vorbereiten

```CSV
gatwaysID,kennung,laengeKoordinaten,breiteKoordinaten,beschreibung,kundenNr
"1","wef_23","123.12","12.12","test daten komme nicht drauss!!","K_01"
"2","qwer_23","11.11","1221310","blblablablalbal","K_03"
"3","sad_23","12321300","7657.46",NULL,"K_02"
"4","hshh_34","1.1","324.023","nichts.","K_02"
"5","sdss_23","5555.55","5543.23","hahhahahah","K_01"
```


<br>
<br>

#### 4.2.2 Befehl um Daten aus CSV einzulesen dokumentiert

```sql
LOAD DATA INFILE '/var/lib/mysql/gateways.csv'
INTO TABLE gatways
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS;
```


<br>
<br>

#### 4.2.3 Printscreen für die erfolgreiche Ausführung

1. Als Root anmelden.

```Terminal
sudo su
```

2. CSV Datei speichern
```Terminal
sudo nano /var/lib/mysql/gateways.csv
```

3. Mysql anmelden
```Terminal
mysql -u root -p
```

4. Datenbank verwenden
```sql
use roehFix;
```

5. Skript laden
```sql
LOAD DATA INFILE '/var/lib/mysql/gateways.csv'
INTO TABLE gatways
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS;
```
<img width="100%" src='./bilder/csvSkript.png'></img>

6. Schauen ob die Daten auch eingetragen wurden
```sql
select * from gatways;
```
<img width="100%" src='./bilder/csvTest.png'></img>

<br>
<br>
<br>
<br>


## 4.3 Export von Kunden und Gateway-Daten (SQL)



#### 4.3.1 Befehl um mehrere Tabellen in SQL-Dateien exportieren

Allgemein mysqldump:

```Terminal
# Allgemein
mysqldump [options] db_name [tbl_name ...] > dump.sql

# Datenbanken angeben
mysqldump [options] --databases db_name ... > dump.sql

# ...oder einfach alle zusammen
mysqldump [options] --all-databases > dump.sql
```

> [!NOTE|style:flat]
> Beispiel
> ```Terminal
> mysqldump roehFix adressen kundendaten kunden gatways > /tmp/roehFix.sql
> ```


<br>
<br>

#### 4.3.2 Printscreen für die erfolgreiche Ausführung

1. mysqldump Befehl ausführen
```Terminal
mysqldump roehFix adressen kundendaten kunden gatways > /tmp/roehFix.sql
```
<img width="100%" src='./bilder/sqlExport.png'></img>

2. SQL Skript öffnen
```Terminal
sudo nano /tmp/roehFix.sql
```
<img width="100%" src='./bilder/sqlExport2.png'></img>

<br>
<br>
<br>
<br>



## 4.4 PHP-Script für Zufallsdatengenerierung (Sensoren)



#### 4.4.1 PHP-Script mit Inline-Kommentaren zu Überlegungen

<br>
<br>

#### 4.4.2 Zufallsgenerierung von Daten

<br>
<br>

#### 4.4.3 Printscreen für die erfolgreiche Ausführung
<br>
<br>
