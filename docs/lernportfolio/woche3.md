# Schulwoche 3
##### 24. August - 30. August

<br>
<br>
<br>

## Array

### Assozative Arrays
Bei großen Arrays wird es irgendwann umständlich zu wissen, welche Nummer/Index zu welchem Wert gehört, darum gibt es assoziative Arrays. Das heißt, man kann für einen Wert einen Schlüssel (auch Key genannt) zuweisen, dies kann z.B. eine andere Zeichenkette sein. Die Zuweisung erfolgt per =>

```php
$namen = array(
"jg" => "Joschija Gruss",
"ss" => "Stefan Schmid",
"dg" => "Domenik Gafner");

echo $namen["jg"];
```


__Ausgabe__

```
Joschija Gruss
```

<br>

### Arrays in Strings konvertieren
Eine sehr nützliche Funktion ist implode($trennzeichen, $array) . Hiermit könnt ihr die Elemente eines Arrays zu einem String verbinden. Mittels der Variable $trennzeichen könnt ihr spezifizieren, welches Verbindungselement zwischen den Elementen erscheinen soll. Diese Funktion ist sehr nützlich, um so z.B. formatierte Listen auszugeben.

```php
$namen = array("Januar", "Februar", "Maerz", "April");
$namenStr = implode(", ", $namen);
echo $namenStr;
```

__Ausgabe__

```
Januar, Februar, März, April, Mai
```

<br>
<br>

## Programmieraufträge
### Auftrag 2:

__Aufgabe__
```
Erstellen Sie ein PHP-Script mit welches ein Formular ausgibt. Wenn
man das Formular mit dem Button bedient, wird die Eingabe wieder in
der HTML-Page ausgegeben.
```


<br>

### Aufbau Docker:
<img width="40%" src='./bilder/aufbau2.png'></img>

<br>

#### HTML File - formular.html
```html
<form action="testfor.php" method="post">
    Vorname: <input type="text" name="vorname" /><br />
    Namename: <input type="text" name="nachname" /><br />
    <input type="Submit" value="Absenden" />
</form>
```

<br>

#### PHP File - testfor.php

```php

$vorname = $_POST["vorname"];
$nachname = $_POST["nachname"];
echo "Hallo $vorname $nachname";

```
<br>

### Browser:

#### Formular
<img width="70%" src='./bilder/formular.png'></img>


#### Ausgabe
<img width="70%" src='./bilder/f_ausgabe.png'></img>


<br>
<br>

## GET & POST

### GET:

- GET-Anforderungen können zwischengespeichert werden
- GET-Anfragen bleiben im Browserverlauf
- GET-Anfragen können mit Lesezeichen versehen werden
- GET-Anforderungen sollten niemals im Umgang mit vertraulichen Daten verwendet werden
- GET-Anforderungen unterliegen Längenbeschränkungen
- GET-Anforderungen werden nur zum Anfordern von Daten verwendet (nicht geändert).

<br>

#### Beispiel:

#### formular.php
```
<?php

$vorname = $_GET["vorname"];
$nachname = $_GET["nachname"];
echo "Hallo $vorname $nachname \n";

?>

<form action="formular.php" method="get">
    Vorname: <input type="text" name="vorname" /><br />
    Namename: <input type="text" name="nachname" /><br />
    <input type="Submit" value="Absenden" />
</form>
```

<br>

#### Browser

##### Formular
<img width="70%" src='./bilder/getStart.png'></img>


##### Ausgabe
<img width="83%" src='./bilder/getFertig.png'></img>


<br>


### POST:

- POST-Anfragen werden niemals zwischengespeichert
- POST-Anfragen bleiben nicht im Browserverlauf
- POST-Anfragen können nicht mit Lesezeichen versehen werden
- POST-Anforderungen unterliegen keinen Einschränkungen hinsichtlich der Datenlänge

<br>

#### Beispiel:

#### formular.php
```
<?php

$vorname = $_POST["vorname"];
$nachname = $_POST["nachname"];
echo "Hallo $vorname $nachname \n";

?>

<form action="formular.php" method="POST">
    Vorname: <input type="text" name="vorname" /><br />
    Namename: <input type="text" name="nachname" /><br />
    <input type="Submit" value="Absenden" />
</form>
```

<br>

#### Browser

##### Formular
<img width="70%" src='./bilder/postStart.png'></img>


##### Ausgabe
<img width="80%" src='./bilder/postFertig.png'></img>


## Bierformular

### Auftrag:

```
Für die Firma Brauerei Locher müssen Sie ein Interessen-Formular erstellen, welches folgenden Inhalt abdeckt:

- Anrede (Radiobutton: Mann, Frau, undefiniert)
- Name, Adresse
- Mailadresse
- Auswahl der Interessen an Produkten:
    - Nicht alkoholische Getränke
    - Schnäpse
    - Bier
- Freitextfeld für Bemerkungen
```

<br>

### Aufbau:

<img width="35%" src='./bilder/bierAufbau.png'></img>

<br>

### bierformular.html

```HTML
<form action="bier_ausgabe.php" method="POST">


    <fieldset>
        <legend>Brauerrei Locher:</legend>
        <label for="gender"> Anrede: </label><br>
        <input type="radio" id="male" name="gender" value="Herr">
        <label for="male">Herr</label><br>
        <input type="radio" id="female" name="gender" value="Frau">
        <label for="female">Frau</label><br>
        <input type="radio" id="other" name="gender" value="Andere">
        <label for="other">Andere</label><br><br>

        <label for="vorname">Vorname: </label><br>
        <input type="text" name="vorname" ><br><br>
        <label for="nachname">Nachname: </label><br>
        <input type="text" name="nachname"><br><br>

        <label for="email">Email: </label><br>
        <input type="email" name="email" ><br><br><br>

        <label for="produkte">Auswahl der Interessen an Produkten: </label><br>
        <input type="checkbox" id="nalk" name="nalk" value="Nicht Alkoholisch">
        <label for="nalk"> Nicht alkohlische Getraenke</label><br>
        <input type="checkbox" id="schnaps" name="schnaps" value="Schnaps">
        <label for="schnaps"> Schnaepse</label><br>
        <input type="checkbox" id="bier" name="bier" value="Bier">
        <label for="bier"> Bier</label><br><br>

        <label for="bemerkung">Bemerkungen: </label><br>
        <textarea name="message" style="width:600px; height:300px;"></textarea><br><br>
        <input type="Submit" value="absenden" /><br><br>

    </fieldset>

</form>
```
<br>

### bier_ausgabe.php

```
<?php

$anrede = $_POST["gender"];
$vorname = $_POST["vorname"];
$nachname = $_POST["nachname"];
$email = $_POST["email"];
$produkte = $_POST["produkte"];
$bemerkung = $_POST["message"];

?>

<h1>Herzlichen Dank!</h1>
<br>

<h4>Stimmen ihre Angaben?</h4>
<p>Anrede: <?php echo $anrede?></p>
<p>Vorname: <?php echo $vorname?></p>
<p>Nachname: <?php echo $nachname?></p>
<br>
<p>Email: <?php echo $email?></p>
<br>
<p>Auswahl: <br>
    <?php
        if(isset($_POST["nalk"])){
            echo "- ". $_POST["nalk"] . "<br>";
        }
        if(isset($_POST["schnaps"])){
            echo "- ". $_POST["schnaps"] . "<br>";
        }
        if(isset($_POST["bier"])){
            echo "- ". $_POST["bier"] . "<br>";
        }
    ?>
<br>
<p>Bemerkung: <?php echo $bemerkung?><br>
</p>

```

<br>

### Browser:

#### Bierformular
<img width="70%" src='./bilder/bierformular.png'></img>

<br>

#### Ausgabe
<img width="70%" src='./bilder/bier_ausgabe.png'></img>

<br>
<br>

## Tipps Formulare

### Überprüfen von Variablen

```
isset (Variable) // true / false
// Überprüft, ob eine Variable vorhanden ist
```

```
empty (Variable) // true / false
// Überprüft, ob eine Variable keinen Inhalt hat
```

<br>

#### Beispeil

__Formular - 2 Buttons__
```html
<table>
      <tr><td>Erste Zahl:</td><td><input type="text" name="zahl1"></td></tr
      <tr><td>Zweite Zahl:</td><td><input type="text" name="zahl2"></td></t
      <tr><td><input type="submit" name="mal" value="Zahlen multiplizieren"
      <td><input type="submit" name="plus" value="Zahlen addieren"></td></t
</table>
```
__PHP - isset__

```php
echo "<h3>Rechenergebnis</h3>";
if (isset($_POST["mal"]))
{
$ergebnis = $_POST["zahl1"] * $_POST["zahl2"];
echo $_POST["zahl1"] ." mal " .$_POST["zahl2"] . " ist gleich $ergebn
}
if (isset($_POST["plus"]))
{
$ergebnis = $_POST["zahl1"] + $_POST["zahl2"];
echo $_POST["zahl1"] ." plus " .$_POST["zahl2"] . " ist gleich $ergeb
}
```

<br>

### POST Testen

```
print_r ($_POST)
// Zeigt den Inhalt einer Variable in lesbarer Form
```

```
var_dump ($_POST)
// Zeigt den Inhalt mehrerer Variablen in lesbarer Form ganz detaillier
```
