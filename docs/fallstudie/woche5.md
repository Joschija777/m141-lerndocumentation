# Use-Case Diagramm


```plantuml
@startuml
left to right direction
skinparam packageStyle rect
actor Benutzer
rectangle interneWebseite {
    (Personeninformationen erfassen) as PI
    (Reisedaten wählen) as RD
    (Reiseziel eintragen) as RZi
    (Reisezweck wählen) as RZw
    (Reisemittel herausfiltern) as RM
    (Öffentliche Verkehrsmittel auswählen) as ÖV
    (Flugzeuginformationen erfassen) as FI
    (Farzeug aussuchen) as FZ
    (Button zum speichern drücken) as BT
    
    Benutzer --> PI
    Benutzer --> RD
    Benutzer --> RZi
    Benutzer --> RZw
    Benutzer --> RM
    Benutzer --> BT
    
    RM --> ÖV
    RM --> FI
    RM --> FZ
    
    
    
}
@enduml


```

<br>
<br>

## Personeninformationen erfassen

<br>

| Name: | Personeninformationen erfassen | 
|----------------------------|-----------------------------------|
| __Nummer:__ | 01 |
| __Ziel im Kontext:__ | User erfasst seine Personeninformationen |
| __Akteure:__ | Benutzer |
| __Trigger:__ | Der Benutzer trägt seine eigene Personeninformationen <br> in ein online Resiseantrag Formular ein |
| __Vorbedingung:__ | Internetzugriff |
| __Essentielle Schritte:__ | 1. Der Benutzer öffnet die angegebene Webseite  <br> 2. Neue Reiseantrag eröffnen <br> 3. Vorname eingeben <br> 4. Nachname eingeben <br>  |
| __Erweiterungen:__ |  3a. Der Vorname wird nicht eingegeben <br> 3a1. Das Sytem merkt das kein Vorname eingegeben wurde <br> 3a2. Das System gibt eine Fehlermeldung aus <br><br> 4a. Der Nachname wird nicht eingegeben <br> 4a1. Das Sytem merkt das kein Nachname eingegeben wurde <br> 4a2. Das System gibt eine Fehlermeldung aus|
| __Kommentare:__ | ~ ||


[Funktionale Anforderungen](fallstudie/woche6.md#_1-personeninformationen-erfassen)



<br>
<br>

## Reisedaten wählen 

<br>

| Name: | Reisedaten wählen  | 
|----------------------------|-----------------------------------|
| __Nummer:__ | 02 |
| __Ziel im Kontext:__ | User wählt die Reisedaten aus  |
| __Akteure:__ | Benutzer |
| __Trigger:__ | Der Benutzer trägt die Reisedaten in ein online Resiseantrag <br> Formular ein |
| __Vorbedingung:__ | User muss die genaue Reisedauer und wann er Abreisen will <br> kennen. |
| __Essentielle Schritte:__ | 1. Der Benutzer muss Personeninformationen eingeben  <br> 2. Abreise eintragen <br> 3. Rückreise eingeben <br>  |
| __Erweiterungen:__ |  2a. Das Abreisedatum wurde nicht ausgewählt <br> 2a1. Das Sytem merkt das kein Abreisedatum gewählt wurde <br> 2a2. Das System gibt eine Fehlermeldung aus <br><br>  3a. Das Rückreisdatum wurde nicht ausgewählt <br> 3a1. Das Sytem merkt das kein Rückreisdatum gewählt wurde <br> 3a2. Das System gibt eine Fehlermeldung aus |
| __Kommentare:__ | ~ ||

[Funktionale Anforderungen](fallstudie/woche6.md#_2-reisedaten-wählen)

<br>
<br>

## Reiseziel eintragen 

<br>

| Name: | Reiseziel eintragen | 
|----------------------------|-----------------------------------|
| __Nummer:__ | 03 |
| __Ziel im Kontext:__ | User erfasst sein Reiseziel |
| __Akteure:__ | Benutzer |
| __Trigger:__ | Der Benutzer trägt sein Reiseziel <br> in ein online Resiseantrag Formular ein |
| __Vorbedingung:__ | ~ |
| __Essentielle Schritte:__ | 1. Der Benutzer gibt sein Reseziel ein.  <br>  |
| __Erweiterungen:__ |  1a. Der Reiseziel wird nicht eingegebn <br> 1a1. Das Sytem merkt das das Reiseziel nicht eingegeben wurde <br> 1a2. Das System gibt eine Fehlermeldung aus <br> |
| __Kommentare:__ | ~ ||

[Funktionale Anforderungen](fallstudie/woche6.md#_3-reiseziel-eintragen)
<br>
<br>

## Reisezweck wählen 

<br>

| Name: | Reisezweck wählen  | 
|----------------------------|-----------------------------------|
| __Nummer:__ | 04 |
| __Ziel im Kontext:__ | User wählt sein Reisezweik aus |
| __Akteure:__ | Benutzer |
| __Trigger:__ | Der Benutzer trägt sein Reisezweck <br> in ein online Resiseantrag Formular ein |
| __Vorbedingung:__ | ~ |
| __Essentielle Schritte:__ | 1. Der Benutzer gibt sein Resezweck ein.  <br>  |
| __Erweiterungen:__ |  1a. Der Reisezweck wird nicht eingegebn <br> 1a1. Das Sytem merkt das das Reisezweck nicht eingegeben wurde <br> 1a2. Das System gibt eine Fehlermeldung aus <br> |
| __Kommentare:__ | ~ ||

[Funktionale Anforderungen](fallstudie/woche6.md#_4-reisezweck-wählen)
<br>
<br>

## Reisemittel herausfiltern 

<br>

| Name: | Reisemittel herausfiltern  | 
|----------------------------|-----------------------------------|
| __Nummer:__ | 05 |
| __Ziel im Kontext:__ | User sucht ein Reisemittel aus |
| __Akteure:__ | Benutzer |
| __Trigger:__ | Der Benutzer filtert sein gewünschtes Reisemittel <br> in ein online Resiseantrag Formular aus |
| __Vorbedingung:__ | ~ |
| __Essentielle Schritte:__ | 1. Der Benutzer wählt dur die Radiobox ein Reisemittel aus  <br>  |
| __Erweiterungen:__ |  1a. Der Reisemitttel wird nicht ausgesucht <br> 1a1. Das Sytem merkt das kein Reisemitttel ausgesucht wurde <br> 1a2. Das System gibt eine Fehlermeldung aus <br> |
| __Kommentare:__ | ~ ||

[Funktionale Anforderungen](fallstudie/woche6.md#_5-reisemittel-herausfiltern)
<br>
<br>

## Öffentliche Verkehrsmittel auswählen 

<br>

| Name: | Öffentliche Verkehrsmittel auswählen | 
|----------------------------|-----------------------------------|
| __Nummer:__ | 06 |
| __Ziel im Kontext:__ | User erfasst seine ÖV-informationen |
| __Akteure:__ | Benutzer |
| __Trigger:__ | Der Benutzer trägt seine eigene ÖV-informationen <br> in ein online Resiseantrag Formular ein |
| __Vorbedingung:__ | Bei Reisemittel ÖV ausgewählt |
| __Essentielle Schritte:__ | 1. Der Benutzer wählt bei Reisemittel ÖV aus  <br> 2. Der User trägt seine ÖV-informationen ein <br>  |
| __Erweiterungen:__ |  2a. Die öv-informationen wurden nicht mitgegeben <br> 2a1. Das Sytem merkt das kein Informationen eingetragen wurde <br> 2a2. Das System gibt eine Fehlermeldung aus <br> |
| __Kommentare:__ | ~ ||

[Funktionale Anforderungen](fallstudie/woche6.md#_6-Öffentliche-verkehrsmittel-auswählen)

<br>
<br>

## Flugzeuginformationen erfassen 

<br>

| Name: | Flugzeuginformationen erfassen  | 
|----------------------------|-----------------------------------|
| __Nummer:__ | 07 |
| __Ziel im Kontext:__ | User erfasst seine Flugzeuginformationen |
| __Akteure:__ | Benutzer |
| __Trigger:__ | Der Benutzer trägt seine eigene Flugzeuginformationen <br> in ein online Resiseantrag Formular ein |
| __Vorbedingung:__ | Bei Reisemittel Flugzeug ausgewählt |
| __Essentielle Schritte:__ | 1. Der Benutzer wählt bei Reisemittel Flugzeug aus  <br> 2. Der User trägt seine Fluginformationen ein <br>  |
| __Erweiterungen:__ |  2a. Die Flugzeuginformationen wurden nicht eingetragen <br> 2a1. Das Sytem merkt das kein Informationen eingetragen wurde <br> 2a2. Das System gibt eine Fehlermeldung aus <br> |
| __Kommentare:__ | ~ ||

[Funktionale Anforderungen](fallstudie/woche6.md#_7-flugzeuginformationen-erfassen)

<br>
<br>

## Farzeug aussuchen

<br>

| Name: | Farzeug aussuchen | 
|----------------------------|-----------------------------------|
| __Nummer:__ | 08 |
| __Ziel im Kontext:__ | User wählt ein Fahrzeug aus |
| __Akteure:__ | Benutzer |
| __Trigger:__ | Der Benutzer wählt ein Fahrzeug <br> in ein online Resiseantrag Formular aus |
| __Vorbedingung:__ | Bei Reisemittel Fahrzeug ausgewählt |
| __Essentielle Schritte:__ | 1. Der Benutzer wählt bei Reisemittel Fahrzeug aus  <br> 2. Der User wählt ein Fahrzeug <br>  |
| __Erweiterungen:__ |  2a. Kein Fahrzeug wurde ausgesucht <br> 2a1. Das Sytem merkt das kein Fahrzeug ausgesucht wurde <br> 2a2. Das System gibt eine Fehlermeldung aus <br><br> 2b. Das Fahrzeug ist nicht mehr Verfügbar <br> 2b1. Das Sytem merkt das das Fahrzeug nicht mehr Verfügber ist <br> 2b2. Das System gibt eine Fehlermeldung aus|
| __Kommentare:__ | ~ ||

[Funktionale Anforderungen](fallstudie/woche6.md#_8-farzeug-aussuchen)

<br>
<br>

## Button zum speichern drücken

<br>

| Name: | Button zum speichern drücken | 
|----------------------------|-----------------------------------|
| __Nummer:__ | 09 |
| __Ziel im Kontext:__ | User speichert die Daten vom Formular |
| __Akteure:__ | Benutzer |
| __Trigger:__ | Der Benutzer klickt auf den Button <br> und das Sytem speichert diese Daten in einer Datenbank |
| __Vorbedingung:__ | Ausgefühltes Formular |
| __Essentielle Schritte:__ | 1. Der Benutzer drückt Button  <br> 2. System überprüft ob alles ausgefühlt wurde <br> 3. System speichert die Daten in einder Datenbank <br> |
| __Erweiterungen:__ |  2a. Das Formular wurde nicht ganz ausgefühlt <br> 2a1. Das Sytem merkt das Daten Fehlen <br> 2a2. Das System gibt eine Fehlermeldung aus <br>
| __Kommentare:__ | ~ ||

[Funktionale Anforderungen](fallstudie/woche6.md#_9-button-zum-speichern-drücken)

<br>
<br>