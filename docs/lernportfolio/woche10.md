# Schulwoche 10
##### 26. October - 1. November

<br>
<br>
<br>


## Was haben wir gemacht?
Da letzten Sonntag, die Abgabe1 vom Projekt war haben wir heute die ganze Abgabe 2 angeschaut und was Sie beinhaltet.

Projekt:
- Model, View, Controller Programmieren
- HTML Webseite mittels Twig
- Fake Daten (noch kein SQL)

Wir haben seine Vorlage (200 FS FunktAnforderungen FakeDaten Vorlage LB1 T2) angeschaut mit den ganze Funktionen. 



<br>
<br>
<br>

## Wie war es?
Es war intressant gestaltet, aber mit schon zuviel Informationen.
Das ganze Projekt ist am anfang unübersichtlich, da ich ja noch nie vorher mit MVC Programmiert habe. 


<br>
<br>
<br>

## Wie ist es mir ergangen?
Es war anstrengend mit dem ganzen mitzukommen. Einige Sachen habe ich Verstanden anderes muss ich kommende Woche noch anschauen.

<br>
<br>
<br>

## Was habe ich gelernt?
Beim Formular gibt es ein Button damit man die ganzen Daten jetzt noch mit fake Array ($menueArray = $menueModel->getFakeMenueDataArray();) und später direkt in die Datenbank.

Sobald man den Button drückt wird die funktinon add im Controller aufgeruffen
```html
<form action="{{ urlroot }}/Orders/add" method="post">
```


```php
public function add($pagename = 'Order - Add')
    {
        $orderModel = $this->model('OrderModel');
        $menueModel = $this->model('MenueModel');
        $menueArray = $menueModel->getFakeMenueDataArray();

        if ($_SERVER['REQUEST_METHOD'] == 'POST') {
            // Process Form -> weil Post-Aufruf

            // Zuerst mal trimen und filtern auf gesunde Daten
            $username = trim(
                filter_input(INPUT_POST, 'username', FILTER_SANITIZE_STRING)
            );
            $comment = trim(
                filter_input(INPUT_POST, 'comment', FILTER_SANITIZE_STRING)
            );
            $email = trim(
                filter_input(INPUT_POST, 'email', FILTER_SANITIZE_EMAIL)
            );
            $refmenue = trim(
                filter_input(INPUT_POST, 'refmenue', FILTER_SANITIZE_NUMBER_INT)
            );

            // Daten setzen
            $data = [
                'username' => $username,       // Form-Feld-Daten
                'username_err' => '',   // Feldermeldung für Attribute
                'email' => $email,          // Form-Feld-Daten
                'email_err' => '',      // Feldermeldung für Attribute
                'refmenue' => $refmenue,       // Form-Feld-Daten
                'refmenue_err' => '',   // Feldermeldung für Attribute
                'comment' => $comment       // Form-Feld-Daten
            ];


            // Gucken ob die Daten plausibel sind
            // Da müsste man aber noch mehr machen
            
            if(empty($data['username']))
            {
                $data['username_err'] = 'Bitte Name angeben';
            }

            if(empty($data['email']))
            {
                $data['email_err'] = 'Bitte Email angeben';
            }

            if(empty($data['refmenue']))
            {
                $data['refmenue_err'] = 'Bitte Menü auswählen';
            }

            // Keine Errors vorhanden
            if (empty($data['username_err']) && empty($data['email_err']) && empty($data['refmenue_err']))
            {
                // Alles gut, keine Fehler vorhanden
                // Späteres TODO: Auf DB schreiben

                $orderModel->fakewriteData($data);
            }
            else {
                // Fehler vorhanden - Fehler anzeigen
                // View laden mit Fehlern

                echo $this->twig->render('order/add.twig.html', ['title' => $pagename, 'urlroot' => URLROOT, 'data' => $data, 'menues' => $menueArray]);
            }

        } else {
            // Init Form mit Default-Daten, weil Get-Aufruf

            $data = [
                'username' => '',       // Form-Feld-Daten
                'username_err' => '',   // Feldermeldung für Attribute
                'email' => '',          // Form-Feld-Daten
                'email_err' => '',      // Feldermeldung für Attribute
                'refmenue' => '',       // Form-Feld-Daten
                'refmenue_err' => '',    // Feldermeldung für Attribute
                'comment' => ''       // Form-Feld-Daten
            ];

            echo $this->twig->render('order/add.twig.html', ['title' => "Order - Add", 'urlroot' => URLROOT, 'data' => $data, 'menues' => $menueArray]);
        }
    }
```

> [!NOTE|style:flat]
1. Werden die einzelen Attribute getrimmt und auf den richtigen Typ gesetzt.
2. Werden die Daten gesetzt.
3. Werden Fehlermeldungen (Satz) bei den Daten die mann ausfüllen muss geschrieben und kontrolliert.
4. Wenn keine Error Vorhanden sind dann werden Fakedaten ausgegen die wir im Model erstellt haben.
5. Bei Fehler auf der Seite bleiben und anzeigen was man noch ausfülllen muss.