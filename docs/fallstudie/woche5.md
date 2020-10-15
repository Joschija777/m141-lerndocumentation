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
| __Vorbedingung:__ | Kann eingereist werden |
| __Essentielle Schritte:__ | 1. Der Benutzer öffnet die angegebene Webseite  <br> 2. Neue Reiseantrag eröffnen <br> 3. Vorname eingeben <br> 4. Nachname eingeben <br>  |
| __Erweiterungen:__ |  3a. Der Vorname wird nicht eingegeben <br> 3a1. Das Sytem merkt das kein Vorname eingegeben wurde <br> 3a2. Das System gibt eine Fehlermeldung aus <br><br> 4a. Der Nachname wird nicht eingegeben <br> 4a1. Das Sytem merkt das kein Nachname eingegeben wurde <br> 4a2. Das System gibt eine Fehlermeldung aus|
| __Kommentare:__ | ~ ||

<br>
<br>

## Reisezweck wählen 

<br>

| Name: | Reisezweck wählen  | 
|----------------------------|-----------------------------------|
| __Nummer:__ | 04 |
| __Ziel im Kontext:__ | User erfasst seine Personeninformationen |
| __Akteure:__ | Benutzer |
| __Trigger:__ | Der Benutzer trägt seine eigene Personeninformationen <br> in ein online Resiseantrag Formular ein |
| __Vorbedingung:__ | Internetzugriff |
| __Essentielle Schritte:__ | 1. Der Benutzer öffnet die angegebene Webseite  <br> 2. Neue Reiseantrag eröffnen <br> 3. Vorname eingeben <br> 4. Nachname eingeben <br>  |
| __Erweiterungen:__ |  3a. Der Vorname wird nicht eingegeben <br> 3a1. Das Sytem merkt das kein Vorname eingegeben wurde <br> 3a2. Das System gibt eine Fehlermeldung aus <br><br> 4a. Der Nachname wird nicht eingegeben <br> 4a1. Das Sytem merkt das kein Nachname eingegeben wurde <br> 4a2. Das System gibt eine Fehlermeldung aus|
| __Kommentare:__ | ~ ||

<br>
<br>

## Reisemittel herausfiltern 

<br>

| Name: | Reisemittel herausfiltern  | 
|----------------------------|-----------------------------------|
| __Nummer:__ | 05 |
| __Ziel im Kontext:__ | User erfasst seine Personeninformationen |
| __Akteure:__ | Benutzer |
| __Trigger:__ | Der Benutzer trägt seine eigene Personeninformationen <br> in ein online Resiseantrag Formular ein |
| __Vorbedingung:__ | Internetzugriff |
| __Essentielle Schritte:__ | 1. Der Benutzer öffnet die angegebene Webseite  <br> 2. Neue Reiseantrag eröffnen <br> 3. Vorname eingeben <br> 4. Nachname eingeben <br>  |
| __Erweiterungen:__ |  3a. Der Vorname wird nicht eingegeben <br> 3a1. Das Sytem merkt das kein Vorname eingegeben wurde <br> 3a2. Das System gibt eine Fehlermeldung aus <br><br> 4a. Der Nachname wird nicht eingegeben <br> 4a1. Das Sytem merkt das kein Nachname eingegeben wurde <br> 4a2. Das System gibt eine Fehlermeldung aus|
| __Kommentare:__ | ~ ||

<br>
<br>

## Öffentliche Verkehrsmittel auswählen 

<br>

| Name: | Öffentliche Verkehrsmittel auswählen | 
|----------------------------|-----------------------------------|
| __Nummer:__ | 06 |
| __Ziel im Kontext:__ | User erfasst seine Personeninformationen |
| __Akteure:__ | Benutzer |
| __Trigger:__ | Der Benutzer trägt seine eigene Personeninformationen <br> in ein online Resiseantrag Formular ein |
| __Vorbedingung:__ | Internetzugriff |
| __Essentielle Schritte:__ | 1. Der Benutzer öffnet die angegebene Webseite  <br> 2. Neue Reiseantrag eröffnen <br> 3. Vorname eingeben <br> 4. Nachname eingeben <br>  |
| __Erweiterungen:__ |  3a. Der Vorname wird nicht eingegeben <br> 3a1. Das Sytem merkt das kein Vorname eingegeben wurde <br> 3a2. Das System gibt eine Fehlermeldung aus <br><br> 4a. Der Nachname wird nicht eingegeben <br> 4a1. Das Sytem merkt das kein Nachname eingegeben wurde <br> 4a2. Das System gibt eine Fehlermeldung aus|
| __Kommentare:__ | ~ ||

<br>
<br>

## Flugzeuginformationen erfassen 

<br>

| Name: | Flugzeuginformationen erfassen  | 
|----------------------------|-----------------------------------|
| __Nummer:__ | 07 |
| __Ziel im Kontext:__ | User erfasst seine Personeninformationen |
| __Akteure:__ | Benutzer |
| __Trigger:__ | Der Benutzer trägt seine eigene Personeninformationen <br> in ein online Resiseantrag Formular ein |
| __Vorbedingung:__ | Internetzugriff |
| __Essentielle Schritte:__ | 1. Der Benutzer öffnet die angegebene Webseite  <br> 2. Neue Reiseantrag eröffnen <br> 3. Vorname eingeben <br> 4. Nachname eingeben <br>  |
| __Erweiterungen:__ |  3a. Der Vorname wird nicht eingegeben <br> 3a1. Das Sytem merkt das kein Vorname eingegeben wurde <br> 3a2. Das System gibt eine Fehlermeldung aus <br><br> 4a. Der Nachname wird nicht eingegeben <br> 4a1. Das Sytem merkt das kein Nachname eingegeben wurde <br> 4a2. Das System gibt eine Fehlermeldung aus|
| __Kommentare:__ | ~ ||

<br>
<br>

## Farzeug aussuchen

<br>

| Name: | Farzeug aussuchen | 
|----------------------------|-----------------------------------|
| __Nummer:__ | 08 |
| __Ziel im Kontext:__ | User erfasst seine Personeninformationen |
| __Akteure:__ | Benutzer |
| __Trigger:__ | Der Benutzer trägt seine eigene Personeninformationen <br> in ein online Resiseantrag Formular ein |
| __Vorbedingung:__ | Internetzugriff |
| __Essentielle Schritte:__ | 1. Der Benutzer öffnet die angegebene Webseite  <br> 2. Neue Reiseantrag eröffnen <br> 3. Vorname eingeben <br> 4. Nachname eingeben <br>  |
| __Erweiterungen:__ |  3a. Der Vorname wird nicht eingegeben <br> 3a1. Das Sytem merkt das kein Vorname eingegeben wurde <br> 3a2. Das System gibt eine Fehlermeldung aus <br><br> 4a. Der Nachname wird nicht eingegeben <br> 4a1. Das Sytem merkt das kein Nachname eingegeben wurde <br> 4a2. Das System gibt eine Fehlermeldung aus|
| __Kommentare:__ | ~ ||

<br>
<br>
