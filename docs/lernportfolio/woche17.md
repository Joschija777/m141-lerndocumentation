# Schulwoche 16
##### 14. Dezember - 20. Dezember

<br>
<br>
<br>


## Was haben wir gemacht?

Es ist die letzte Woche vor der grossen Abgabe und wir durften nochmals selbständig weiter arbeiten.


<br>
<br>
<br>

## Wie war es?
Da selbständige Arbeit war fand ich gut da man nochmals vorwärts kommt.

<br>
<br>
<br>

## Wie ist es mir ergangen?
Ich habe das logout noch erreicht das ich erreicht haben wollte und bin somit praktisch fertig mit dem Projekt.

<br>
<br>
<br>

## Was habe ich gelernt?

### Logout

#### HTML
```html
{% if not session.user_id is defined %}
        <ul class="navbar-nav ml-auto">
          <li class="nav-item">
            <a class="nav-link" href="{{ urlroot }}/Users/register">Register</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="{{ urlroot }}/Users/login">Login</a>
          </li>
        </ul>
{% else %}
        <ul class="navbar-nav ml-auto">
            <li class="nav-item">
              <a class="nav-link" href="{{ urlroot }}/Users/logout">Logout</a>
            </li>
        </ul>  
{% endif %}
```

<br>


#### entweder - Controller.php
```php
$this->twig->addGlobal('session', $_SESSION);
```
Bei der Base in die Controller.php hinzufügen!!!

<br>

#### oder - Reiseantrag.php
```php
//alles was man noch mitgiebt
echo $this->twig->render('reiseantrag/list.twig.html', ['title' => $pagename, 'urlroot' => URLROOT, 'data' => $data, 'session' => $_SESSION]);
```
Bei jedem Render noch den Session Array mitgeben - das ganze ist so viel aufwendiger.
