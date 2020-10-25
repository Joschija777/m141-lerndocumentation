# Architekturkonzept

<br>

## Dokumentationen

- [Model View Controller](fallstudie/woche1.md)

- [Template Engine Twig](fallstudie/woche2.md)

- [SSR & CSR](fallstudie/woche3.md)

<br>

## Beschreibung Aufgabenstellung


### Aufgabenstellung

Meine Aufgabe ist kurz gesagt, in wenigen Wochen eine interaktive PHP Webseite mittels Server Side Rendering zu erstellen.
Das ganze PHP Projekt wird mittels MVC und Twig erstellt.
Zu der Programmierung muss man Wöchentlich das erarbeitete und neu erlernte in einer Dokumentation zusammenfassen.



**Probleme:**
- Bei dem Formular für den Reiseantrag gibt es sehr viele Möglichkeiten als auswahl die nicht immer nötig sind.
- Da die Formulareblatt hat einen grössere Laufweg und geht somit zu mehrere Personen.



**Ziel:**

- Das Formular über eine interaktive Webseite bedienen.
- Später villeicht noch das ganze über eine digitale Signatur bestätigen.



**Details:**

- Reiseantrag
- Mittels PHP
- Mittels MVC
- Mittels Twig


**Vorgehen:**

<img width="70%"  src='./bilder/Zeitplan.png'></img>


<br>

### Formular

<img width="70%"  src='./bilder/Reiseantrag.jpeg'></img>


<br>
<br>

## Umsetzung MVC

### Model

- Klasse Person - Attributen: Vorname, Nachname
- Klasse Reiseinformationen - Attributen: Resedaten, Reiseziel, Reisezweck

Entweder:
- Klasse Reisemittel - Attributen: ÖV, Flugzeug, Auto

Oder:
- Klasse ÖV - Attributen: Abo
- Klasse Flugzeug - Attributen: Fluggesellschaft, Preis
- Klasse Auto - Attributen: Fahrzeug

### View

- Mittels Twig
- HTML
- CSS Framework (Materialize)
- Header (Navbar)
- Main (interaktives Formular)
- Footer (Kontaktangaben)


### Controller

- Button bei Reisemittel (interaktiv)
- Arrays
- Konstrucktor
- Tabelle
- Selectfeld
- Dropdown
- Verbindung mit Datenbank
- evt. digitaler Signatur



<br>
<br>


## Umsetzung Twig


### Layout
Im Layout werde alle Twig-Html Sites eingebunden. Wie Header, Main und Footer.
Dies dient dazu, das man nicht immer das gleiche einbinden wiederholt ausführen.

***

### Header
Den Header werde ich nur einmal erstellen da der ja sozusagen statisch ist. Der Header wird so aussehen, dass ich eine Nav habe.

Das Nav wird wahrscheinlich beinhalten:
- FirmenLogo
- Forumlar (Reiseantrag)
- Tabelle (Wo das Formular ausgewertet wird)
- evt. Kalender

***


### Footer
Der Footer wird auch statisch sein und dieser wird nicht soviel beinhalten:
- aktuelle Zeit
- aktuelles Datum
- Informationen

***

### Main
Da das main interaktiv ist und nich wie bei Footer und Header gleich aufgebaut ist, muss ich diese immer anderst gestallen.

Was es sicher beinhaltet ist zu einem:
- interaktive Formular
- Time
- Select Boxes
- Dropdown
- Tabelle (Array)
