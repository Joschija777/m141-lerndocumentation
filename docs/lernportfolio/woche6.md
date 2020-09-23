# Schulwoche 6
##### 14. September - 20. September

<br>
<br>
<br>

## Klassendiagramm

```plantuml
@StartUML Cardatabase



package controllers <<Folder>> {

  class Home{
      + index($name = '')

  }


  class contact{
      + index(): echo 'contact/index'
      + test($param1 = '', $param2 = ''): echo $param1 = '', $param2 = ''
  }
}


package core <<Folder>> {

  class Controller{
      # model($model): new $model()
      # view($view, $data = [])
  }

  class APP{
      # $controller = 'home';
      # $method = 'index';
      # $params = [];

      + __construct()
      + parseUrl()
  }
}


package models <<Folder>> {

  class User{
    + $name;
  }
}


package  views <<Folder>> {

  interface index{

  }

}

Home --|> Controller : extends
contact --|> Controller : extends
Controller ..> APP
User ..> Home
index ..> Controller


@enduml



```

<br>
<br>

## Sequenzdiagramm

```plantuml

@startuml

actor Joschija
participant View
participant Controller
participant Model


View -> Joschija : wird wahrgenommen
Joschija -> Controller : URL wird ein Parameter mitgegeben oder ein Button wird gedrückt (interaktion)
activate Controller
Controller -> Model : Klasse wird mit den Attributen ausgelesen, erstellt, ... (Modifikation)
deactivate Controller
activate Model
Model -> View : informiert()
deactivate Model
View -> Joschija : wird wahrgenommen


@enduml

```



<br>
<br>

## MVC-Beispiel

### Controller

```php

class Home extends Controller
{
    public function index($marke = '', $modell = '')
    {
        $car = $this->model('Car');
        $car->marke = $marke;
        $car->modell = $modell;

        $this->view('home/index', ['marke' => $car->marke,
                                    'modell' => $car->modell]);
    }
}

```

<br>

### Model

```php
class Car{
    public $marke;
    public $modell;
}
```

<br>

### View

```html
Marke:  <?=$data['marke']?> <br>
Modell: <?=$data['modell']?>
```

<br>

### Browser
<img width="1000%" src='./bilder/mvc.png'></img>
