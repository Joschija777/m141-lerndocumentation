# Fragen

## Angriffsvektoren Datenbank

__Beschreiben Sie die 3 möglichen Angriffsvektoren auf eine Datenbank. Benennen und erklären Sie die Problematiken?__

**1. Missbräuchler Zugriff über MYSQL-Client**

```
Anwender mit einem Persönlichen Benutzerkonto können in versuchung geraten mit ihrem eigenen Konto über den MySQL-Client statt über die Applikation(Webserver) eine Verbindung aufzubauen und an nicht für Sie berrechtigte Daten zu gelangen.
```

**Lösung:**

```
Der Benutzer sollte kein direkten zugriff auf die Datenbank sonder nur über die Applikation (Webserver). Zudem sollten die Zugriffsrechte richtig gesetz werden. Nicht allen Adminrechte.
```

<br>


**2. Benutzerkonto in Applikation ausspähen**

```
Sobald ein Benutzer Recht auf die Applikation(Webserver) hat kann er versuchen die Passwörter auszuspähen z.B vom Benutzer root. 
```

**Lösung:**

```
Privilegen sorgfältig vergeben. Vorallem da wo die Passwörter gespeichert werden (Verzeichnis) dürfen nur einzelne Admiuser einsehen.
```

<br>


**3. Benutzerkonto im Datenverkehr auspähen**

```
Technisch visierte Anwender können auf die Idee kommen das Passwort auszuspähen im dem sie den Datenverkehr ausschnüffeln. 
```

**Lösung:**

```
Die Verbindung zwischen Anwender und Datenbank sollte sicher  also verschlüsselt stattfinden. 
```

