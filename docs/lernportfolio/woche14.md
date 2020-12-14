# Schulwoche 14
##### 23. November - 29. November

<br>
<br>
<br>

## Was haben wir gemacht?

Heute haben heute  Session und Cookies angeschaut und ein Besispiel gemacht.


#### Session
HTTP ist ein zustandsloses Protokoll, das bedeutet, Informationen werden zwischen den verschiedenen Aufrufen eines Besuchers nicht zwischengespeichert. Dies ist natürlich unpraktisch wenn wir gewisse Informationen zu einem Besucher speichern müssen, beispielsweise mit welchem Benutzernamen sich dieser eingeloggt hat. Um dies zu lösen, verwendet man in PHP Sessions

<br>

#### Cookies
Mit Cookies hat man genau so die Möglichkeit, wie bei Sessions, bestimmte Daten während einer Folge von Aufrufen einer Website festzuhalten.
Allerdings kann man mit Cookies auch Daten über die Sitzung hinaus speichern (z.B. 100 Tage nach der Speicherung), denn Cookies werden als Datei auf dem Computer des Besuchers gespeichert.
Allerdings kann der Besucher uns natürlich verbieten, auf seinem Computer einen Cookie zu speichern, darum verwendet man nur für die Speicherung von Daten während einer Folge von Aufrufen einer Website lieber Sessions.



<br>
<br>
<br>

## Wie war es?
Es war mal etwas neues da ich die Begriffe schonmal gefört habe aber nicht gewusst habe für was das gut ist.

<br>
<br>
<br>

## Wie ist es mir ergangen?
Ich fand es schwer und hatte mühe beim Programieren

<br>
<br>
<br>

## Was habe ich gelernt?

#### Session

__Session-Start__

```php
session_start();
```

__Werte auf Sessions setzen__

```php
$_SESSION['name'] = "wert";
```

__Sessionslöschen__

```php
session_destroy(); // Session löschen...alles
unset($_SESSION['name']); // Wert löschen
```

__Komplettes Beispiel__

```php
 session_start(); //Ganz wichtig
 if(!isset($_SESSION['username'])) {die("Bitte erst einloggen"); //Mit die() beenden wir den weiteren Scriptablauf 
 //In $name den Wert der Session speichern      
 $name = $_SESSION['username'];//Text ausgeben
 echo"Du heißt immer noch: $name      
 <a href=\"logout.php\">Logout</a>";
```

<br>

#### Cookies

__Cookie setzen__

```php
setcookie("username","Max",0);  // Gültig bis Ende der Sitzung      
setcookie("username","Max",time()+(3600*24));
```

__Cookie auslesen__

```php
$cookie = $_COOKIE["username"]; 
echo"Der Inhalt des Cookies: $cookie";
```

__Cookie löschen__

```php
setcookie("username","",time() - 3600);
```
