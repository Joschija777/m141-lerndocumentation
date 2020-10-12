# Template Engine Twig

## Was ist Twig?
Twig ist eine Template-Engine für die Programmiersprache PHP. Die Syntax wurde von der Template-Engine Jinja sowie der des Django-Frameworks beeinflusst.

<br>

## Wofür braucht man Twig?
Twig braucht man um das PHP aus dem HTMl zu rauszuhalten.
Da es vorallem nicht sicher ist wenn man PHP in den HTML, wegen dem Manipulieren der Werte.
Und da es nicht besonders schön ist wenn man PHP in HTML hat. 

<br>

## Syntax

```html
{{ ... }}   =  um den Inhalt einer Variable oder das Ergebnis eines Ausdrucks auszugeben.
```

```html
{# ... #}   =  für Kommentare, die nicht weiter verarbeitet werden
```

```html
{% ... %}    =  für Kommandos und Kontrollstrukturen durch z. B. Schleifen oder Verzweigungen
```

<br>

## Beispiel 

### Aufbau:
<img width="20%" src='./bilder/aufbau-flugzeug.png'></img>

#### base
In dem Verzeichnis base sind Twig Sites drin die immmer wieder vorkommen wie zum Beispiel der Footer und der Header.
Ansonstens müsste man das ganze immer wieder von neuem schreiben.

__Footer__

Im Footer kommt halt die Angaben hinein die man in der Fusszeile möchte

__Header__

In die Kopfzeile kommen so Sachen wie das Nav-bar.

__Core__

Da ist die einbindung von JavaScript etc.

__Layout__

Im Layout werden alle Seiten eingebunden:

```HTML
<body>

  <!-- Include der Navbar -->
  {{ include('base/header.twig.html') }}


  <!-- Begin page content -->
  <main role="main" class="container">

    <!-- Der Content Block kann von Subtemplates überschrieben werden -->
    {% block content %}

    <h1>Index</h1>
    <p class="important">
      Das ist Default-Text auf dem Layout, falls der Content-Block nicht von Sub-Templates überschrieben wird
    </p>

    {% endblock %}

  </main>


  <!-- Include Footer -->
  {{ include('base/footer.twig.html') }}

  <!-- Include von js-Imports -->
  {{ include('base/corejs.twig.html') }}
</body>
```

<br>
<br>

### Index - Flugzeug

#### Dropdown

```HTML
<table border="1" style="width: 80%;">

    <select class="form-control">
        {% for flugzeug in flugzeuge %}
        <option value="{{ flugzeug.type }}{{ flugzeug.geschwindigkeit }}" >{{ flugzeug.type }}{{ flugzeug.geschwindigkeit }}</option>
    {% endfor %}
    </select>

</table>
```

<img width="60%" src='./bilder/dropdown.png'></img>

<br>

#### Array:

```HTML
{{ dump(flugzeuge) }}
```
<img width="50%" src='./bilder/array-flugzeug.png'></img>