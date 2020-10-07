# Schulwoche 7
##### 21. September - 27. September

<br>
<br>
<br>


## Was haben wir gemacht?
Am Anfang der ersten Lektion haben wir unsere Lerndokumentation angeschaut und was wir alles verbessern können. Ich habe Leider vergessen diese 5 Fragen zu beantworten.
- Was haben wir gemacht?
- Wie war es?
- Wie ist es mir ergangen?
- Was habe ich gelernt?
- Was ist noch offen?

<br>

Zum anderen haben wir nochmal ein MVC Beispiel durchgemacht. Das ganze mit den MVC-TWIG Beispiel.
Als erstes mussten wir das eine neue Entität Flugzeug erstellen.

- [Model - Flugzeug](#Model)
- [Controller - Flugzeug](#Controller)


Am Schluss mussten wir noch ein MVC Projekt (die View mittels TWIG) analysieren und eine neue Seite erstellen.


<br>
<br>
<br>

## Wie war es?


<br>
<br>
<br>

## Wie ist es mir ergangen?

<br>
<br>
<br>

## Was habe ich gelernt?

Durch das ständige wiederholen der Aufgabe bekomme ich mehr vesrtändnis der Funktionen!!

<br>

### MVC-TwIG Projekt - Flugzeug

#### Model
 ```PHP
 class AutoModel
 {
     public $type;
     public $marke;

 }

 ```

<br>

#### Controller

 ```PHP
 class Flugzeug extends Controller
 {

     private $flugzeugArray = array();

     public function index($name = '')
     {
         $this->addFlugzeug("Airbus", "360");
         $this->addFlugzeug("Blabla", "test");
         $this->addFlugzeug("Irgendwas", "ff");

         //var_dump($this->FlugzeugArray);

         echo $this->twig->render('flugzeug/index.twig.html', ['title' => "Flugzeug / Index", 'flugzeuge' => $this->flugzeugArray] );                
     }

     public function add($marke = 'dummyMarke', $typ = 'dummyType')
     {
         // Hier müsste jetzt die Logik für die DB kommen...
         //$this->addFlugzeug($typ, $marke);

         // Aus der Helper-Klasse unter helpers/url_helper.php
         redirect('flugzeug/index');
     }


     private function addFlugzeug($typ, $marke)
     {
         $flugzeug = $this->model('FlugzeugModel');
         $flugzeug->type = $typ;
         $flugzeug->marke = $marke;

         array_push($this->flugzeugArray, $flugzeug);
     }
 }
 ```

<br>
<br>
<br>

## Was ist noch offen?

### TWIG

#### Was ist TWIG

Twig ist eine Template-Engine für die Programmiersprache PHP. Die Syntax wurde von der Template-Engine Jinja sowie der des Django-Frameworks beeinflusst. Twig ist eine freie Software,

<br>

#### Aufbau:
<img width="30%" src='./bilder/aufbau-flugzeug.png'></img>

##### base
In dem Verzeichnis base sind Twig Sites drin die immmer wieder vorkommen wie zum Beispiel der Footer und der Header.
Ansonstens müsste man das ganze immer wieder von neuem schreiben.
