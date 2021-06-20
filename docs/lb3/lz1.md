# Tabelle konfigurieren (Storage Engine)

##  Tabelle erstellen
Dokumentieren Sie wie eine Storage Engine auf eine Tabelle angwendet wird

1. Datenbank auswählen
```mysql
use dbname;
```
2. Tabelle erstellen mit (MyISAM)
```mysql
create table test1 (
id int not null,
column1 int (11),
column2 varchar (100)
) ENGINE=MyISAM;
```

<img width="100%" src='./bilder/engineTa.png'></img>

> [!TIP|style:flat]
> Mit "Engine=passendeEngine" auswählen.

<br>
<br>


## Anwendungsgrund 

Engine | Anwendung  | Begründung
:-------- | :---------- | :----------
InnoDB | Bankdaten, Kundendaten | ACID, Commit, Rollback, Crash-Recovery, keine Daten verloren
MyISAM   | Webanwendungen   | Schnelle Speicher-Engine, leselastigen Anwendungen, Volltextsuchindizes
ARCHIVE | Archivieren und Abrufen vergangener Daten | Tabellen werden nicht indiziert, und die Komprimierung erfolgt beim Einfügen
BLACKHOLE  | verteilten Datenbankumgebung     | Akzeptiert aber speichert keine Daten, Abfragen immer einen leeren Satz zurück
FEDERATED | einzelnen, lokalen, logischen Datenbank |  Keine Daten gespeichert und Abfragen automatisch auf Remote-Server
PERFORMANCE-SCHEMA   | Monitoring    | Leistungsdaten, überwacht Serverereignisse
MEMORY | für temporäre Tabellen mit externen Abfragedaten | Speichert Daten im RAM, gleichzeitige Datenzugriff wird synchronisiert.
CSV   | CSV-formatierte Daten   |  Sobald man eine CSV Datei importieren möchte 

> [!TIP|style:flat]
> In den meisten Fällen verwendet man InnoDB = default oder MyISAM


## Alle Storage-Engines

__Befehl:__

```mysql
SHOW ENGINES;
```
<img width="100%" src='./bilder/enginesMysql.png'></img>

> [!NOTE|style:flat]
> Ich habe 9 Engines auf meinem System bei MySQL.

<br>

__Liste:__

- __InnoDB__
ist ein freies Speichersubsystem für das Datenbankmanagementsystem MySQL. Sein Hauptvorteil gegenüber anderen Speichersubsystemen für MySQL ist, dass Transaktionssicherheit und referenzielle Integrität über Fremdschlüssel gewährleistet werden.
Sie sind optimal für eine maximale Leistung bei der Bearbeitung von grossen Datenmengen. Sie sind transaktionssicher und sie beherrschen das sperren auf Zeilenebene, sowie auch ein konsistentes nicht sperrendes Lesen. Wenn die referenzierten Tabellen denselben Typ haben, wird sogar eine referenzielle Integrität unterstützt. Man ist nicht an die maximale Dateigrösse des Systemgeknüpft, da die Tabellen in einem eigenen Tabellenplatz, welcher aus mehreren Dateien bestehen kann, bestehen.

    InnoDB entspricht dem ACID-Standard (Atomicity Consistency Isolation Durability). Alle Transaktionen laufen voneinander isoliert ab, aber es können beliebig viele Anwendungen gleichzeitig Daten in eine Tabelle schreiben. Bei der Datenabfrage, dem SELECT, hat InnoDB deutlich die Nase vorne, aber bei den Schreibzugriffen auf eine Datenbank, den INSERT und UPDATE, ist MyISAM etwas schneller.

    - __ACID__ 

        - Atomicity oder Atomarität: Ausführung aller oder keiner Informationsteile einer Transaktion
        - Consistency oder Konsistenz: Transaktionen erzeugen einen gültigen Zustand oder fallen in den alten Zustand zurück
        - Isolation oder Abgrenzung: Transaktionen verschiedener Anwender oder Prozesse bleiben voneinander isoliert
        - Durability oder Dauerhaftigkeit: Nach einer erfolgreichen Transaktion bleiben die Daten dauerhaft gespeichert


<br>
<br>

- __MyISAM__
Bei der MyISAM Tabelle gibt es drei verschiedene Arten, es gibt die Statische, die Dynamische und die Komprimierte. Alle gemeinsam haben das sie nicht transaktionssicher sind und keine referenzielle Integrität unterstützen.

    Die Statische ist sehr schnell und einfach wiederherzustellen, da sich die Datensätze an festen Positionen befinden, aus dem Grund weil die Inhalte der Spalten immer gleich lang sind. Sie brauchen jedoch mehr Speicherplatz als die anderen beiden Varianten.

    Die zweite Variante ist die Dynamische. Wie bereits gesagt braucht die Dynamische weniger Speicherplatz als die Statische, den hier werden die Datensätze fragmentiert wenn sie grösser werden.

    Die letzte Variante ist die Komprimierte, sie ist für die Statische und die Dynamische verfügbar. Die Daten werden komprimiert abgespeichert und können nur gelesen werden.

    ISAM steht für Indexed Sequential Access Method (dt. Index-sequenzielle Zugriffsmethode) – es ist also nicht möglich, dass mehrere User oder Anwendungen gleichzeitig in einer Tabelle schreiben. Das sequenzielle Speichern erlaubt immer nur den Schreibzugriff durch eine Anwendung.

    - __ISAM__
    Index Sequential Access Method (ISAM) ist eine von IBM entwickelte Zugriffsmethode für Datensätze einer Datei, die sowohl (sortiert) sequentiellen als auch wahlfreien (random) index-basierten Zugriff zulässt.

- __ARCHIVE:__ Archive ist eine Speicher-Engine für das relationale Datenbankverwaltungssystem MySQL. Benutzer können diese analytische Speicher-Engine verwenden, um eine Tabelle zu erstellen, die nur "archiviert" ist. Daten können nicht aus dieser Tabelle gelöscht, sondern nur hinzugefügt werden.

- __BLACKHOLE:__ Die BLACKHOLESpeicher-Engine fungiert als „ Schwarzes Loch “ , das Daten akzeptiert, aber wegwirft und nicht speichert. Abfragen geben immer ein leeres Ergebnis zurück.

- __FEDERATED:__ Mit dem Storage-Engine können Sie auf Daten aus einer entfernten MySQL-Datenbank zugreifen, ohne Replikations- oder Clustertechnologie zu verwenden. Beim Abfragen einer lokalen Tabelle werden die Daten automatisch aus den entfernten (verbundierten) Tabellen abgezogen. In den lokalen Tabellen werden keine Daten gespeichert. FEDERATEDFEDERATED

- __PERFORMANCE-SCHEMA:__ Das Leistungsschema bietet eine Möglichkeit, die interne Ausführung des Servers zur Laufzeit zu überprüfen. Sie wird mithilfe des PERFORMANCE_SCHEMA Speichermoduls und der Datenbank implementiert. Das Leistungsschema konzentriert sich in erster Linie auf Leistungsdaten

- __MEMORY:__ Das Speichermodul erstellt Spezielle Tabellen mit Inhalten, die im Speicher gespeichert sind. Da die Daten anfällig für Abstürze, Hardwareprobleme oder Stromausfälle sind, verwenden Sie diese Tabellen nur als temporäre Arbeitsbereiche oder schreibgeschützte Caches für Daten, die aus anderen Tabellen gezogen werden

- __CSV:__ Das CSV-Speichermodul speichert Daten in Textdateien im Format "Durchkommasgetrennte Werte". Die CSV-Speicher-Engine wird immer in den MySQL-Server kompiliert. Um die Quelle für das CSV-Modul zu untersuchen, suchen Sie im Speicher-/csv-Verzeichnis einer MySQL-Quellverteilung.