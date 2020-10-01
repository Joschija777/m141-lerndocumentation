# Schulwoche 5
##### 7. September - 13. September

<br>
<br>
<br>


## Was haben wir gemacht?
Zu beginn der Lektion haben wir eine Repetition von PHP gemacht. Wo man 9 verschiedene Aufgaben lösen musste:
- [Aufgabe 1 - Gültige Variablen](#_1-Gültige-Variablen)
- [Aufgabe 2 - Syntax](#_2-Syntax)
- [Aufgabe 3 - Syntax](#_3-Syntax)
- [Aufgabe 4 - Syntax](#_4-Syntax)
- [Aufgabe 5 - Syntax](#_5-Syntax)
- [Aufgabe 6 - Syntax](#_6-Syntax)
- [Aufgabe 7 - Syntax](#_7-Syntax)
- [Aufgabe 8 - Arrays](#_8-Arrays)
- [Aufgabe 9 - Mathe](#_9-Mathe)

<br>

Danach mussten wir uns in das Thema [Objekt orientiertes Programieren](#Object-orientiertes-Programmieren) einlesen. In dem wir als Hausaufgabe auch 5 Punkte beschreiben musste:
1. [Wie wird in PHP instanziert?](#_1-Wie-wird-in-PHP-instanziert)
2. [Was bedeutet der Pfeil?](#_2-Was-bedeutet-der-Pfeil)
3. [Was bedeutet this?](#_3-Was-bedeutet-this)
4. [Welche Möglichkeiten an Zugriffsmodifizierer kennt PHP?](#_4-Welche-Möglichkeiten-an-Zugriffsmodifizierer-kennt-PHP)
5. [Dokumentieren Sie Beispiele zu Konstruktoren, Methoden, Klassen…](#_5-Dokumentieren-Sie-Beispiele-zu-Konstruktoren-Methoden-Klassen…)

Als letzter Abschnitt mussten wir uns noch in das Thema [MVC](#Model-View-Controller) einlesen

<br>
<br>
<br>

## Wie war es?

Der heutige Tag war abwechlungsreich gestaltet mit thorie und Praxis. Aber der Schwerpunkt war schon mehr auf der Thorie. Die Zeitlichen Abstände stimmten und soweit passte mir alles.

<br>
<br>
<br>



## Wie ist es mir ergangen?

Die wiederholungen von den PHP-Aufgaben waren mir sehr gut gelungen und ich hatte nur 1 Fehler. Aber obwohl wir in der Schule Objekt orientiertes Programmieren in Javsa hatten. Machte es mir trotzdem noch Probleme alle Syntax und Methoden, Funktionen zu verstehen.

Als neues Thema durfte ich MVC lernen. Da die Strucktur oder besser gesagt, der ganze Aufbau übersichtlicher macht.

<br>
<br>
<br>





## Was habe ich gelernt?

### PHP Syntax

#### 1. Gültige Variablen

__Auftrag:__

Welche Variablen sind gültig?

```PHP
$preis
$1preis
$_preis
$else
$gesamtpreis12
$gesamt-preis
$MeNg
```

<br>

__Lösung:__

```PHP
$preis
$_preis
$else
$gesamtpreis12 = (ist gültig aber nicht schlau gewählt mit nummer drin)
$MeNg
```
<br>
<br>


#### 2. Syntax

__Auftrag:__

Was ist die Ausgabe von:

```PHP
$j = "Hallo";
$k = "$j \"Onkel\" ";
echo $k;
```

<br>

__Lösung:__

```
Hallo "Onkel"
```
<br>
<br>




#### 3. Syntax

__Auftrag:__

Was ist die Ausgabe von:

```PHP
$a = "Hallo ";
$a .= "Welt";
echo $a;
```

<br>

__Lösung:__

```
Hallo Welt
```
<br>
<br>





#### 4. Syntax

__Auftrag:__

Was ist die Ausgabe von:

```PHP
$a = "Hallo";
$b = "Welt";
echo $a." ".$b."<br />"
```

<br>

__Lösung:__

```
Hallo Welt

```
<br>
<br>




#### 5. Syntax

__Auftrag:__

Was ist die Ausgabe von:

```PHP
$preis = 49.90;
echo "Die Variable $preis enthält den Wert: $preis";

```

<br>

__Lösung:__

```
Die Variable 49.90 enthält den Wert: 49.90
```
<br>
<br>


#### 6. Syntax

__Auftrag:__

Was ist die Ausgabe von:

```PHP
$preis = 49.90;
echo 'Die Variable $preis enthält den Wert: $preis';

```

<br>

__Lösung:__

```
Die Variable $preis enthält den Wert: $preis
```
<br>
<br>



#### 7. Syntax

__Auftrag:__

Was ist die Ausgabe von:

```PHP
$preis = 49.90;
echo 'Die Variable $preis enthält den Wert:' .$preis;

```

<br>

__Lösung:__

```
Die Variable $preis enthält den Wert: 49.90
```
<br>
<br>




#### 8. Arrays

__Auftrag:__

Was ist die Ausgabe von:

```PHP
$familie = array("Vater", "Mutter", "Tochter", "Sohn");
echo "$familie[3]<br />";
echo "$familie[1]<br />";
echo "$familie[0]<br />";
echo "$familie[4]<br />";
echo "$familie[2]<br />";
```

<br>

__Lösung:__

```
Sohn
Mutter
Vater

Tochter
```
<br>
<br>



#### 9. Mathe

__Auftrag:__

Was ist die Ausgabe von:

```PHP
$n = 5;
$o = 8;
echo $n + $o;
echo $n - $o;
echo $n * $o;
echo $n / $o;
echo $n % $o;
```

<br>

__Lösung:__

```PHP
13
-3
40
0.625
5
```
<br>
<br>

### Model-View-Controller

#### Was ist MVC?
MVC steht für Model, View, Controller. Eine kurze Antwort auf die Frage, was unter den drei Begriffen verstanden wird, könnte wie folgt lauten:

#### Model:
Das Model hat die Aufgabe, die Webanwendung mit Daten aus der Datenbank (oder von wo auch immer) zu versorgen und die Daten, wenn gewünscht, zu speichern.

#### View:
Die View beinhaltet die Verwaltung der Templates, und generiert die HTML-Ausgabe.

#### Controller:
Der Kontroller entscheidet, was mit den übergebenen Parametern anzufangen ist, und steuert die Anwendung.

<br>
<br>
<br>

## Was ist noch offen?

Die verschiedenen Syntaxe Funktionen und Methoden im OOP!!


### Object orientiertes Programmieren

#### 1. Wie wird in PHP instanziert

__Klasse: User__
```PHP
//Definition der Klasse User
class User {
	//Definition der Eigenschaften name, email und password
	public $name;
	public $email;
	public $password;
}
```

<br>

__Instanz:__

```
$max = new User();
```

> [!NOTE|style:flat]
Nach der Klassendefinition erstellen wir nun ein Objekt von der Klasse oder anders ausgedrückt wir erstellen eine Instanz der Klasse

<br>
<br>

#### 2. Was bedeutet der Pfeil

```
Mit dem Pfeil-Operator kannst Du auf die Funktionen oder Variablen
einer Klasse zugreifen.
```
<br>
<br>

#### 3. Was bedeutet this

```
Es ist eine Referenz auf das aktuelle Objekt
```
<br>
<br>

#### 4. Welche Möglichkeiten an Zugriffsmodifizierer kennt PHP

```
$public
$private
$protectet
```
<br>
<br>

#### 5. Dokumentieren Sie Beispiele zu Konstruktoren, Methoden, Klassen…

__Klassen:__
```
Klassen:
class User {
	public $erstellungsdatum;
	public $name;
	public $email;
		}
}
```
> [!NOTE|style:flat]
Die klasse User mit den 3 Atributen wurden erstellt.

<br>

__Konstruktoren:__
```
class User {
	public $erstellungsdatum;
	public $name;
	public $email;

	public function __construct($name, $email = "") {
		$this->name = $name;
		$this->email = $email;
		$this->erstellungsdatum = date("d.m.Y H:i:s");
	}
}
```

__Instanz mit Konstruktor:__

```
$max = new User("Max Mustermann", "max@muster.de");
echo "Das Objekt von $max->name wurde erstellt am $max->erstellungsdatum";
```

__Ausgabe:__

```
Das Objekt von Max Mustermann wurde erstellt am 10.09.2020 10:42:48
```

<br>

__Methoden:__

```PHP
class User {
 function methode1() { //Public Methode ohne Parameter
 }

 public function methode2($parmater) { //Public Methode mit Paramter
 }

 protected function methode2($parmater1, $parameter2) { //Protected Methode mit zwei Paramtern
 }

 private function methode3() { //Private Methode ohne Paramter
 }
}
```

__Beispiele:__

```PHP
public function setEmail($newEmail) {
		if($this->isValidEmail($newEmail)) {
			$this->email = $newEmail;
		}
	}

```

```PHP
public function getEmail() {
  return $this->email;
}
```

```PHP
public function setRandomPassword() {
		$randomPassword = strval(rand(1,10)); //Dies ist nicht sonderlich sicher
		$this->password = $this->hashPassword($randomPassword);
		return $randomPassword;
	}
```

<br>
<br>

#### 6. Dokumentieren Sie die Beispiele zur Vererbung mit PHP…

```PHP
class Saeugetier
{
  protected $geschlecht;  
  protected function setzGeschlecht($value)
  {
    $this -> geschlecht = $value;
  }
}
class Mensch extends Saeugetier
{
  ...
}
class Hund extends Saeugetier
{
  ...
}
```

> [!NOTE|style:flat]
extends
Damit haben wir nun den Kindklassen Mensch und Hund die Methoden und Eigenschaften der Elternklasse Saeugetier vererbt. Aus didaktischen Gründen habe ich diese mal als protected definiert. Das bedeutet, dass in diesem Fall(!) nur die eigene Klasse und die Kindklassen(!) darauf zugreifen können.

<br>
<br>
<br>
