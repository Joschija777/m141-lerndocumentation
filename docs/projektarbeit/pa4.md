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


## 4.2 CSV-Datenimport Gatway-Daten und (export)



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

#### 4.2.4 Export CSV

1. Sql Befehl ausführen
```sql
SELECT gatwaysID, kennung, laengeKoordinaten, breiteKoordinaten, beschreibung, kundenNr FROM gatways
WHERE gatwaysID < 5 -- Alle die ID unter 5 haben
INTO OUTFILE '/var/lib/mysql/Gatways.csv' -- Speicherort
FIELDS ENCLOSED BY '"'  
TERMINATED BY ',' -- Feld wird mit einem Semikolon beendet
LINES TERMINATED BY '\n'; -- Zeilenendings nach Linux-Style (\r\n für Windows)
```
<img width="100%" src='./bilder/exportCsv.png'></img>

2. Testen

```sql
SELECT * FROM gatways;
```
<img width="100%" src='./bilder/testCsv.png'></img>

<br>

```sql
sudo nano /var/lib/mysql/Gatways.csv
```
<img width="100%" src='./bilder/testCsv2.png'></img>

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
```php
<?php

//Variablen deklarien für eine Verbindung
$servername = "localhost";
$username = "root";
$password = "Admin_123";
$dbname = "roehFix";

// Verbindung herstellen
$conn = new mysqli($servername, $username, $password, $dbname);

// Verbindung überprüfen
if ($conn->connect_error) {
  die("Connection failed: " . $conn->connect_error);
}

// Funktion erstellen um einen Random String mit default Länge von 6 Zu geben
function generateRandomKennung($length = 6) {
    $characters = '0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ';
    $charactersLength = strlen($characters);
    $randomString = '';
    for ($i = 0; $i < $length; $i++) {
        $randomString .= $characters[rand(0, $charactersLength - 1)];
    }
    return $randomString;
}

//Funktion um einen Random Float mit Default Wert zwischen 0 bis 1 zu erstellen für Laenge Kordinaten
function generateLaengeKordination($start_number = 0,$end_number = 1,$mul = 1000000) {
     if ($start_number > $end_number) return false;
     return mt_rand($start_number * $mul,$end_number * $mul)/$mul;
}

// Funktion um einen Random Float mit Default Wert zwischen 0 bis 1 zu erstellen für Breite Kordinaten ist nicht umbeding notwentig weil das die gleiche Funktion wie die LaengenKordination ist)
function generateBreiteKordination($start_number = 0,$end_number = 1,$mul = 1000000) {
     if ($start_number > $end_number) return false;
     return mt_rand($start_number * $mul,$end_number * $mul)/$mul;
}

// Variable deklarieren für Vorschleiffe
$j = 9;

// Tabelle Sensoren Befüllen
$sql = "INSERT INTO sensoren (sensorenID, kennung, laengeKoordination, breiteKoordination)VALUES ";

// Forschleife $i=0 solang bis i kleiner gleich $j ist und $i+1
for($i=0; $i <= $j; $i++) {
    // Default String Länge 6 da nicht reingeschrieben ist
    $kennung = generateRandomKennung();
    // Float Wert zwischen 1000 und 19203
    $laengeKordination = generateLaengeKordination(1000,19203);
    $breiteKordination = generateBreiteKordination(1000,19203);

   // Nur Solang machen bis $i kleiner wie $j ist
   if($i < $j){
          // Hat immer Komma am schluss da es eine Aufzählung ist
          $sql .= "(NULL, '" . $kennung . "', " . $laengeKordination . ", " . $breiteKordination . "),";
        } else { // Der Letze braucht ein Semikolon am schluss
          $sql .= "(NULL, '" . $kennung . "', " . $laengeKordination . ", " . $breiteKordination . ");";
          }
  }


// Troubleshooting ausgabe Terminal
echo $sql;

// Auch Troubleshoting ob alles erstellt worden ist und die Verbindung mit der Datenbank gestummen hat.
if ($conn->query($sql) === TRUE) {
  echo "New record created successfully";
} else {
  echo "Error: " . $sql . "<br>" . $conn->error;
}
$conn->close();
?>
```



<br>
<br>

#### 4.4.2 Zufallsgenerierung von Daten

__Zufallszahlen integer:__
```php
function generateRandomNumber($min=0, $max=1) {
  return rand($min,$max);
}
```

<br>

__Zufallszahlen float:__
```php
function generateRandomFloat($start_number = 0,$end_number = 1,$mul = 1000000) {
 	// If start number is greater than end number then return false
 	if ($start_number > $end_number) return false;
	// Return random float number
 	return mt_rand($start_number * $mul,$end_number * $mul)/$mul;
}
```

<br>

__Zufallsstring varchar:__
```php
function generateRandomString($length = 6) {
    $characters = '0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ';
    $charactersLength = strlen($characters);
    $randomString = '';
    for ($i = 0; $i < $length; $i++) {
        $randomString .= $characters[rand(0, $charactersLength - 1)];
    }
    return $randomString;
}
```

<br>

__Funktionen Testen:__
```php
for($i=0; $i < 10; $i++) {
   echo generateRandomNumber(0,19203)."<br>";
   echo generateRandomFloat(1000,19203)."<br>";
   echo generateRandomString()."<br>";
}
```



<br>
<br>

#### 4.4.3 Printscreen für die erfolgreiche Ausführung

1. PHP Installieren
```Terminal
sudo apt install php7.4-cli
```

2. MYSQLI in PHP installieren
```Terminal
sudo apt-get install -y php-mysqli
```

3. PHP Skript erstellen (4.4.1 PHP-Skript)
```Terminal
sudo nano /var/lib/mysql/phpTest.php
```

4. Als root anmelden
```Terminal
sudo su
```

5. PHP Skript ausführen
```Terminal
php -f /var/lib/mysql/phpTest.php
```
<img width="100%" src='./bilder/phpSkript.png'></img>

6. Testen

```Terminal
mysql -u root -p
```

```sql
use roehFix;
```

```sql
select * from sensoren;
```
<img width="70%" src='./bilder/phpSkriptTest.png'></img>
