# PA 2:  Konfiguration eines RDBMS

<br>

## 2.1 Storage Engines bei MySQL

#### 2.1.1 Storage-Engines unter MySQL
Dokumentieren 2 wichtigesten Storage-Engines genau beschrieben:

- __InnoDB__
ist ein freies Speichersubsystem für das Datenbankmanagementsystem MySQL. Sein Hauptvorteil gegenüber anderen Speichersubsystemen für MySQL ist, dass Transaktionssicherheit und referenzielle Integrität über Fremdschlüssel gewährleistet werden.
InnoDB-Tabellen sind die Standard-Tabelle seit MySQL 5.6. Sie sind optimal für eine maximale Leistung bei der Bearbeitung von grossen Datenmengen. Sie sind transaktionssicher und sie beherrschen das sperren auf Zeilenebene, sowie auch ein konsistentes nicht sperrendes Lesen. Wenn die referenzierten Tabellen denselben Typ haben, wird sogar eine referenzielle Integrität unterstützt. Man ist nicht an die maximale Dateigrösse des Systemgeknüpft, da die Tabellen in einem eigenen Tabellenplatz, welcher aus mehreren Dateien bestehen kann, bestehen.


<br>

- __MyISAM__
Bei der MyISAM Tabelle gibt es drei verschiedene Arten, es gibt die Statische, die Dynamische und die Komprimierte. Alle gemeinsam haben das sie nicht transaktionssicher sind und keine referenzielle Integrität unterstützen.

    Die Statische ist sehr schnell und einfach wiederherzustellen, da sich die Datensätze an festen Positionen befinden, aus dem Grund weil die Inhalte der Spalten immer gleich lang sind. Sie brauchen jedoch mehr Speicherplatz als die anderen beiden Varianten.

    Die zweite Variante ist die Dynamische. Wie bereits gesagt braucht die Dynamische weniger Speicherplatz als die Statische, den hier werden die Datensätze fragmentiert wenn sie grösser werden.

    Die letzte Variante ist die Komprimierte, sie ist für die Statische und die Dynamische verfügbar. Die Daten werden komprimiert abgespeichert und können nur gelesen werden.

<br>
<br>

#### 2.1.2 Restlichen Storage-Engines

__Befehl:__

```mysql
SHOW ENGINES;
```
<img width="100%" src='./bilder/enginesMysql.png'></img>

> [!NOTE|style:flat]
> Ich habe 9 Engines auf meinem System bei MySQL.

<br>

__Liste:__

- __ARCHIVE:__ Archive ist eine Speicher-Engine für das relationale Datenbankverwaltungssystem MySQL. Benutzer können diese analytische Speicher-Engine verwenden, um eine Tabelle zu erstellen, die nur "archiviert" ist. Daten können nicht aus dieser Tabelle gelöscht, sondern nur hinzugefügt werden.

- __BLACKHOLE:__ Die BLACKHOLESpeicher-Engine fungiert als „ Schwarzes Loch “ , das Daten akzeptiert, aber wegwirft und nicht speichert. Abfragen geben immer ein leeres Ergebnis zurück.

- __MRG-MYISAM:__

- __FEDERATED:__

- __PERFORMANCE-SCHEMA:__

- __MEMORY:__

- __CSV:__


<br>
<br>

#### 2.1.3 Machen Sie sich Gedanken welche Daten aus Ihrem Projekt mit welcher Storage Engine verwaltet werden könnten. Begründen Sie Ihr Gedanken.

<br>

### 2.1.4 Dokumentieren Sie wie eine Storage Engine auf eine Tabelle angwendet wird

<br>
<br>
<br>
<br>


## 2.2 Benutzer und Berechtigungen

### 2.2.1 Root-Benutzer konfiguriert (Login/Passwort)


<br>

### 2.2.2 Sensoren-Benutzer konfiguriert (Login/Passwort/Berechtigung auf Datenbank eingeschränkt)

<br>

### 2.2.3 Admin-Benutzer konfiguriert (Login/Passwort/Berechtigung auf Datenbank eingeschränkt)

<br>

### 2.2.4 Verfizieren Sie Ihre Konfiguration und speichern Sie das Resultat in Ihrer Dokumentation

<br>
<br>
<br>
<br>

## 2.3 Server-Konfiguration

Transaktions-Isolation : Verfizieren Sie welche Transaktions-Isolation auf Ihrem Server aktiviert ist. Dokumentieren Sie, was das bezüglich den Anomalien für Ihre Installation bedeutet.
Exportieren Sie die aktuelle Liste an System-Variablen
Netzwerkkonfiguration DBMS-Server anpassen und dokumentieren

<br>
<br>
<br>
<br>

## 2.4 Server-Betrieb

Protokollierung langsamer Abfragen aktivieren
Listen Sie den Inhalt des Data-Directories auf
Dokumentieren Sie die Default-Datenbanken mysql, sys, performance_schema
