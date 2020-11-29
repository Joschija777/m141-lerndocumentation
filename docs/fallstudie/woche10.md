# Anwendung sql-Scripts


## MYSQL Database
<img width="100%" src='./bilder/Tabellen.png'></img>

> [!NOTE|style:flat]
Hier habe ich meine Tabellen angelegt localhost:8080

### Export Tabeller erstellen
<img width="100%" src='./bilder/export.png'></img>


### Export Beispieldaten erstellen
<img width="100%" src='./bilder/export2.png'></img>


### Beispiel Daten & Strucktur
<img width="100%" src='./bilder/beispieldaten.png'></img>

### Schnell Tabelle erstellen
<img width="100%" src='./bilder/tabelleEr.png'></img>


<br>
<br>
<br>


## User anlegen

### Config Datei

```PHP
// DB-Params (die Werte sind im Docker-Compose definiert)
define('DB_HOST', 'mysql');
define('DB_USER', 'reiseUser');
define('DB_PASS', 'userpass');
define('DB_NAME', 'reisen');


// Unsere APP-Root
define('APPROOT', dirname(dirname(__FILE__)));

// Unsere URL-Root
define('URLROOT', 'http://localhost:8000');
```

### docker-compose.yml
```yml
version: '3'

volumes:
  mysqldata:
  mysqlinit:
  app:


services:
  php:
    build: ./php
    ports:
      - 8000:80
    volumes:
      - ./app:/var/www/html

  mysql:
    image: mysql:5.7
    ports:
      - 3306:3306
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_USER: reiseUser
      MYSQL_PASSWORD: userpass
      MYSQL_DATABASE: reisen
    volumes:
      - ./mysql/initscripts:/docker-entrypoint-initdb.d
      - ./mysql/mysqldata:/var/lib/mysql/

  adminer:
    image: adminer
    ports:
      - 8080:8080
```

### Benutzer erstellen
<img width="100%" src='./bilder/mysqlUser.png'></img>

> [!NOTE|style:flat]
Wichtig ist das man den richtigen username (yml & config File) und die Richtige Datenbank verbindet.


<br>
<br>
<br>

## Funktionen um zu Verbinden

### Reiseantrag-Liste

#### Model:
```php
public function getReiseantragData()
{
    $this->db->query("SELECT * FROM `reiseantrag`");
    $results = $this->db->resultSet();

    return $results;
}
```

#### Controller:
```PHP
public function index($pagename = 'Reiseantrag - Admin')
   {
       $reiseantragModel = $this->model('ReiseantragModel');
       $flugzeugModel = $this->model('FlugzeugModel');
       $fahrzeugModel = $this->model('FahrzeugModel');
       $oevModel = $this->model('OEVModel');
       $reiseantragArray = $reiseantragModel->getReiseantragData();
       $flugzeugArray = $flugzeugModel->getFlugzeuge();
       $fahrzeugArray = $fahrzeugModel->getFahrzeuge();
       $oevArray = $oevModel->getOEVs();


       // Fipseln uns einen Array zusammen, der dann gut auf der GUI funktioniert
       $data = $reiseantragModel->renderReiseantragList4GUI($reiseantragArray, $flugzeugArray, $fahrzeugArray, $oevArray);

       echo $this->twig->render('reiseantragadmin/index.twig.html', ['title' => $pagename, 'urlroot' => URLROOT, 'data' => $data] );                
   }
```

#### Browser:
<img width="100%" src='./bilder/liste.png'></img>

<br>
<br>

### Reiseantrag-Formular

#### Model:
```php
public function insertReisenDB($data)
{
    $this->db->query("INSERT INTO `reiseantrag`
    (`vorname`, `nachname`, `userid`, `hinreise`, `rueckreise`, `reiseziel`, `reisezweck`, `refFlugzeug`, `refFahrzeug`, `refOev`, `status`)
    VALUES (:vorname, :nachname, :userid, :hinreise, :rueckreise, :reiseziel, :reisezweck, :refFlugzeug, :refFahrzeug, :refOev, :status )");

    $this->db->bind(':vorname',$data['vorname']);
    $this->db->bind(':nachname',$data['nachname']);
    $this->db->bind(':userid',$data['userid']);
    $this->db->bind(':hinreise',$data['hinreise']);
    $this->db->bind(':rueckreise',$data['rueckreise']);
    $this->db->bind(':reiseziel',$data['reiseziel']);
    $this->db->bind(':reisezweck',$data['reisezweck']);
    $this->db->bind(':refFlugzeug',$data['refFlugzeug']);
    $this->db->bind(':refFahrzeug',$data['refFahrzeug']);
    $this->db->bind(':refOev',$data['refOev']);
    $this->db->bind(':status',0); // Neue Bestellung, Status ist immer 0

    return $this->db->execute(); // Gibt True im Erfolgsfall, False im Fehlerfall
}
```

#### Controller:
```PHP
if ($reiseantragModel->insertReisenDB($data))
               {
                   // Erfolgsfall
                   // Umleiten auf Liste meiner Bestellungen
                   redirect('Reiseantrag/listreiseantrag');
               } else
               {
                   echo "Fehler bein hinzufügen 1";
               }

```

#### Browser:
<img width="100%" src='./bilder/form.png'></img>
