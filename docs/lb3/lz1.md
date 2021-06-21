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
<br>

## Views & Stored Procudures

__Weshalb/Wofür werden Stored Procudures eingesetzt?__
