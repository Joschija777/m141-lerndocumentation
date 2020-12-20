# Testzenario

## Testfall 1:   Personeninformationen erfassen
1. Er gibt den Vornamen ein.
2. Er gibt den nachname ein.
3. Die Daten sollen übermittelt werden. (Sobald das ganze Formular ausgefühlt wurde.)

<img width="60%"  src='./bilder/Testfall1.png'></img>

<br>

<img width="60%"  src='./bilder/Testfall1_1.png'></img>
> [!TIP|style:flat]
Erfolgreich

<br>


### Testfall 1.2: Nichts eingetragen
1. Vornamen vergessen einzutragen
2. Nachnamen vergessen einzutragen
3. Fehlermeldung sollte kommen!!!

<img width="60%"  src='./bilder/Testfall1_3.png'></img>
> [!TIP|style:flat]
Erfolgreich

<br>

### Testfall 1.3: Zahlen eingetragen
1. Vornamen haben Zahlen oder Abstände drin
2. Nachnamen haben Zahlen oder Abstände drin
3. Sollte nicht funktionieren!!!

<img width="60%"  src='./bilder/Testfall1_4.png'></img>

> [!TIP|style:flat]
Erfolgreich




<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## Testfall 2:   Reisedaten erfassen
1. Er gibt das Hinreisedatum ein.
2. Er gibt das Rückreisedatum ein.
3. Die Daten sollen übermittelt werden. (Sobald das ganze Formular ausgefühlt wurde.)

<img width="60%"  src='./bilder/Testfall2.png'></img>

<br>

<img width="60%"  src='./bilder/Testfall2_1.png'></img>
> [!TIP|style:flat]
Erfolgreich

<br>


### Testfall 2.2: Nichts eingetragen
1. Hinreisedatum vergessen einzutragen
2. Rückreisdatum vergessen einzutragen
3. Fehlermeldung sollte kommen!!!

<img width="60%"  src='./bilder/Testfall2_2.png'></img>
> [!TIP|style:flat]
Erfolgreich

<br>

### Testfall 2.3: Beliebiges Datum eingetragen
1. Beliebiges Hinreisedatum (sogar Vergangenheit)
2. Beliebiges Rückreisedatum (sogar vor Hinreisedatum)
3. Sollte nicht funktionieren!!!

<img width="60%"  src='./bilder/Testfall2_3.png'></img>

> [!ATTENTION|style:flat]
Alle Daten Auswählbar


<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>



## Testfall 3:   Reiseinformationen erfassen
1. Er gibt das Reiseziel ein.
2. Er gibt das Reisezweck ein.
3. Die Daten sollen übermittelt werden. (Sobald das ganze Formular ausgefühlt wurde.)

<img width="60%"  src='./bilder/Testfall3.png'></img>

<br>

<img width="60%"  src='./bilder/Testfall3_1.png'></img>
> [!TIP|style:flat]
Erfolgreich

<br>


### Testfall 3.2: Nichts eingetragen
1. Reiseziel vergessen einzutragen
2. Reisezweck vergessen einzutragen
3. Fehlermeldung sollte kommen!!!

<img width="60%"  src='./bilder/Testfall3_2.png'></img>
> [!TIP|style:flat]
Erfolgreich

<br>

### Testfall 3.3: Zahlen im Reisezweck
1. Im Reiseziel darf man Zahlen verwenden
2. Reisezweck ohne Zahlen
3. Sollte nicht funktionieren!!!

<img width="60%"  src='./bilder/Testfall3_3.png'></img>

> [!TIP|style:flat]
Alle Daten Auswählbar


<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>


## Testfall 4:   Reisemittel erfassen
1. Er wählt das Reisemittel aus.
2. Er wählt die zusätzlichen Reisemittelinformationen aus.
3. Die Daten sollen übermittelt werden. (Sobald das ganze Formular ausgefühlt wurde.)

<img width="60%"  src='./bilder/Testfall4.png'></img>

<br>

<img width="60%"  src='./bilder/Testfall4_1.png'></img>
> [!TIP|style:flat]
Erfolgreich



<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>


## Testfall 5:   Benutzer erstellen
1. Er gibt den Namen ein.
2. Er gibt die Email ein.
3. Er gibt ein Passwort ein.
4. Der Benutzer sollte erstellt werden. (Sobald das ganze Formular ausgefühlt wurde.)

<img width="60%"  src='./bilder/Testfall5.png'></img>

<br>

<img width="60%"  src='./bilder/Testfall5_1.png'></img>
> [!TIP|style:flat]
Erfolgreich


<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## Testfall 6:   Als Benutzer einloggen
1. Er gibt den Benutzernamen ein.
2. Er gibt das gültige Password ein.
3. Ich sollte mich einloggen können. (Sobald das ganze Formular ausgefühlt wurde.)

<img width="60%"  src='./bilder/Testfall6.png'></img>

<br>

<img width="60%"  src='./bilder/Testfall6_1.png'></img>
> [!TIP|style:flat]
Erfolgreich

<br>


### Testfall 6.2: Als normaler User (Zugriff)
1. Versuch in die Adminliste zu gelangen
2. Versuch in die Userliste zu gelangen
3. Sollte nicht funktioniern

<img width="60%"  src='./bilder/Testfall6_2.png'></img>
> [!TIP|style:flat]
Erfolgreich


<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## Testfall 7:   Adminrechte vergeben
1. In Database User adminrechte vergeben
2. User sollte jetzt auch Admin sein

<img width="60%"  src='./bilder/Testfall7.png'></img>


> [!TIP|style:flat]
Erfolgreich

<br>


### Testfall 7.2: Als Admin (Zugriff)
1. Versuch in die Adminliste zu gelangen
2. Versuch in die Userliste zu gelangen
3. Sollte funktioniern!!

<img width="60%"  src='./bilder/Testfall7_1.png'></img>

<br>

<img width="60%"  src='./bilder/Testfall7_2.png'></img>
> [!TIP|style:flat]
Erfolgreich


<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## Testfall 8:  Status wechseln
1. Er gibt einen anderen Status ein
2. Er drückt auf den Button
3. Status sollte geändert sein

<img width="60%"  src='./bilder/Testfall8.png'></img>

<br>

<img width="60%"  src='./bilder/Testfall8_1.png'></img>

<br>

<img width="60%"  src='./bilder/Testfall8_2.png'></img>
> [!TIP|style:flat]
Erfolgreich

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## Testfall 9:  Reiseantrag löschen
1. Löschbutton drücken
2. Reiseantrag sollte gelöscht werden

<img width="60%"  src='./bilder/Testfall9.png'></img>

<br>

<img width="60%"  src='./bilder/Testfall9_1.png'></img>

> [!TIP|style:flat]
Erfolgreich

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
