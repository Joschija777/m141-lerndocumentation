# Fragen

## Angriffsvektoren Datenbank

__Beschreiben Sie die 3 möglichen Angriffsvektoren auf eine Datenbank. Benennen und erklären Sie die Problematiken?__

1. Missbräuchler Zugriff über MYSQL-Client

```
Missbräuchler Zugriff über MYSQL-Client:
Anwender mit einem Persönlichen Benutzerkonto können in versuchung geraten mit ihrem eigenen Konto über den MySQL-Client statt über die Applikation(Webserver) eine Verbindung aufzubauen und an nicht für Sie berrechtigte Daten zu gelangen.
```

Lösung:

```
Der Benutzer sollte kein direkten zugriff auf die Datenbank sonder nur über die Applikation (Webserver). Zudem sollten die Zugriffsrechte richtig gesetz werden. Nicht allen Adminrechte.
```

<br>


2. Benutzerkonto in Applikation ausspähen

```
Benutzerkonto in Applikation ausspähen:
Sobald ein Benutzer Recht auf die Applikation(Webserver) hat kann er versuchen die Passwörter auszuspähen z.B vom Benutzer root. 
```

Lösung:

```
Privilegen sorgfältig vergeben. Vorallem da wo die Passwörter gespeichert werden (Verzeichnis) dürfen nur einzelne Admiuser einsehen.
```

<br>


3. Benutzerkonto im Datenverkehr auspähen

```
Benutzerkonto im Datenverkehr auspähen:
Technisch visierte Anwender können auf die Idee kommen das Passwort auszuspähen im dem sie den Datenverkehr ausschnüffeln. 
```

Lösung:

```
Die Verbindung zwischen Anwender und Datenbank sollte sicher  also verschlüsselt stattfinden. 
```

<br>
<br>
<br>

## Backup und Restore

__Was sind cold, warm, hot - Backups in Bezug auf Datenbank-Servern?__


- cold
```
Als "kaltes" Backup werden Vorgehen bezeichnet, bei welchen die Daten während dem Export und Import dem Endbenutzer nicht zur Verfügung stehen
```

- warm
```
Als "warmes" Backup werden Vorgehen bezeichnet, bei welchen die Daten während dem Export und Import dem Endbenutzer eingeschränkt (z.Bsp. nur lesend) zur Verfügung stehen
```

- hot
```
Als "heisses" Backup werden Vorgehen bezeichnet, bei welchen die Daten während dem Export und Import dem Endbenutzer voll funktionsfähig zur Verfügung stehen
```

<br>
<br>

__Was sind logische Backups oder physische Backups? Vor- und Nachteile?__

- Physische
```
Als physisches Backup werden Vorgehen bezeichnet, bei welchem die Backup-Informationen in binärer Form zur Verfügung stehen (z.Bsp. Filesystem-Snapshot)
```
```
Vorteile:
Einfachheit
Wenn die ganze VM kaputt geht kann man schnell die Infrastrucktur nachbauen.
Nachteile:
grosse Speicheraufwand
Führt man das ganze unter dem laufenden Betrieb durch, dann ist es nicht im neusten stand
```


- Logische
```
Als logisches Backup werden Vorgehen bezeichnet, bei welchem das Backup in "menschlesbarer Form" (z.Bsp. SQL-Script) zur Verfügung stehen
```
```
Vorteile:
einfach Teilmengen zu Speichern
versionübergreifend
kleiner Speicheraufwand
Nachteile:
Grosse Datein mit viel Inhalt
unübersichtlich
```

<br>
<br>

## Point-in-Time
```
Point-in-Time-Recovery bezieht sich auf die Wiederherstellung von Datenänderungen bis zu einem bestimmten Zeitpunkt. Normalerweise wird diese Art der Wiederherstellung nach der Wiederherstellung einer vollständigen Sicherung durchgeführt, die den Server in den Zustand zum Zeitpunkt der Sicherung versetzt.  Die Point-in-Time-Wiederherstellung bringt den Server dann inkrementell vom Zeitpunkt der vollständigen Sicherung auf den neuesten Stand in letzter Zeit.
```


<br>
<br>
<br>

## Views & Stored Procudures

__Weshalb/Wofür werden Stored Procudures eingesetzt?__

- Was sind Stored Procedures

```
Stored Procedures sind SQL-Anweisungen, die datenbankseitig gespeichert sind. Eine
komplizierte Lese-, Einfüge- und Änderungslogik kann in einer Prozedur in der Datenbank
ebenfalls zur Verfügung gestellt werden. Wenn Sie den Applikationen keine Schreibrechte
geben, sondern nur Rechte, Stored Procedures aufzurufen, werden die Tabellen- und Spal-
tennamen der Datenbank ebenfalls verborgen.
Um die Geschwindigkeit zu erhöhen, werden im Datenbankschema gezielt Redundanzen
eingefügt.
```


- Einsetzungsgrund

```
Wenn Sie den Applikationen keine Schreibrechte
geben, sondern nur Rechte, Stored Procedures aufzurufen, werden die Tabellen- und Spal-
tennamen der Datenbank ebenfalls verborgen.
Um die Geschwindigkeit zu erhöhen, werden im Datenbankschema gezielt Redundanzen
eingefügt. Werden Stored Procedures verwendet, muss dies den Applikationsentwickler
nicht kümmern.
```

- Vorteile

```txt
Stored Procedures sind über die gesamte Laufzeit gesehen schneller, da
sie nur einmal eingelesen und übersetzt werden müssen und ständig wiederverwendet
werden können. (Redudanz)

Ein weiterer Aspekt sind Sicherheitsbedenken. Stored Procedures können nur ändern,
wofür sie geschrieben worden sind.

Hat eine Applikation Schreibrechte auf eine Tabelle,
kann sie beliebige Statements absetzen
```


<br>




__Weshalb/Wofür werden Views eingesetzt?__

- Was sind Views

```
Views sind Sichten auf Tabellen oder andere Views. Sie können Views auf eine Tabelle oder
auf eine View oder auf eine Kombination von mehreren Tabellen bzw. Views definieren. Die
ursprüngliche Idee von Views war es, sensitive Daten nicht allen zur Verfügung zu stellen
und komplizierte Abfragen in einer Sicht zusammenzufassen.
```


- Einsetzungsgrund

```
Mithilfe der View können sie Einzelne Datensätze freigeben oder sperren. 
(So ist es z.B. mittels Benutzerrechten nicht möglich, Filme ab 18 Jahren auszublenden. Mit einer View können Sie genau dies.)

Views können auch eingesetzt werden, um Applikationen Daten aus Tabellen zur Verfügung zu stellen, ohne die tatsächliche Implementierung der Datenbank zu verraten
```

- Vorteile

```txt
Die Views kapseln die Implementierung der Datenbank nach aussen ab.

Ein weiterer Vorteil dieser «Kapselung» besteht darin, dass für jede Applikation eine eigene View zusammengestellt werden kann. 

Views können nicht nur lesen sondern auch schreiben
```


<br>
<br>
<br>

## Testing


##### Katastrophentest 

```
Bei Katastrophentests wird untersucht, wie sich die Systeme verhalten wenn man sie böswillig "kaputt" machen will. Dabei wird überprüft was passiert wenn Dinge ausgesteckt, umgesteckt, rausgezogen und demoliert wird. 
```

- Anwendungsfälle
```
Strom abschalten
Disk rausziehen
Disk füllen mit Daten
```

##### Stresstest 

```
Beim Stresstest wird die maximale Belastungsgrenze gesucht, bei welcher das System gerade noch die geforderten Leistungen erbringt. Die Erfahrung aus diesen Tests haben grossen Einfluss auf die Konfiguration des Alarmings und zukünftige Ausbaustufen der Infrastruktur.
```

- Anwendungsfälle
```
Strom abschalten
Disk rausziehen
Disk füllen mit Daten
```


##### Volumentest

```
Bei einem Volumentest werden die Systeme einer vorgegebenen, zu erwartenden, Belastung ausgesetzt und überprüft.
Dabei wird überprüft ob die Systeme während den Belastungen den Betrieb aufrechterhalten können.
```