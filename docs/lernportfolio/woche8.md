# Schulwoche 8
##### 28. September - 4. October

<br>
<br>
<br>


## Was haben wir gemacht?

Heute haben wir den Aufbau von der LB angesehen:

- 10% Architekturkonzept dokumentiert
- 30% Korrekte Umsetzung der funktionale Anforderungen
- 15% Funktionale Sicherheitsanforderungen berücksichtigt
- 10% Clean Code Konventionen berücksichtigt
- 20% Teilsysteme / Schnittstellen sinnvoll gewählt
- 10% Testszenario mit Testfällen wurde erarbeitet / Testergebnissefestgehalten
- 5% Zeitliche Vorgaben eingehalten


<br>
<br>
<br>

## Wie war es?
Heute war es gut eingeplat. Am Anfang haben wir angeschut wie die LBs aussehen mit dem Anfordernungen und Nach dem wir das gemacht haben wie die Themen funktional Anforderungen, Use-Case und Testszenario sind. Am Schluss konten wir noch mit der ersten Lb Abgabe anfangen.

<br>
<br>
<br>

## Wie ist es mir ergangen?
Am Anfang hatte ich noch mühe um die LB Abgabe Punkte richtig zu intepretieren und verstehen, aber nach dem Googlen und Nachfragen wurden mir die wenigen Punkten auch noch klar. Zudem kam ich gut voran muss aber trozdem noch einiges in den Ferien erlediegen.

<br>
<br>
<br>

## Was habe ich gelernt?
Ich habe gelernt was USE-Case sind und wie diese am besten Beschrieben werden. Zudem für was die FunktionaleAnforderung und Testszenario gut sind.


### Use-Case

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

### FunktionaleAnforderung:   Personeninformationen erfassen

- Die Software muss warnen, wenn die Vorname nicht mitgegeben wurde.
- Die Software muss warnen, wenn der Nachname nicht mitgegeben wurde.
- Das Formular muss die Eingabe von dem Vornamen an die Datenbank weitergeben : Speicher Button
- Das Formular muss die Eingabe von dem Nachnamen an die Datenbank weitergeben : Speicher Button
- Das Formular muss die Eingabe von den Zahlen in den Personalinformationen abfangen.
- Das Formular muss die Eingebe von Sonderzeichen abfangen.

<br>
<br>


### Szenario:   Personeninformationen erfassen

Er geht auf die Hompage klickt auf das Text Imput Feld das oben mit Vornamen beschriftet ist und gibt sein Vornamen ein. Danach klickt auf das Text Imput Feld das oben mit Nachnamen beschriftet ist und gibt sein Nachnamen ein und folgt dem Flow bis zu den Reisedaten.
