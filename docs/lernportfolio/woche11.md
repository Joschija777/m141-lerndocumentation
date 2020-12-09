# Schulwoche 11
##### 2. November - 8. November

<br>
<br>
<br>


## Was haben wir gemacht?

Am heutigen Tag haben wir nichts neues angeschaut, wir durften an der 2ten LB Abgabe weiter Arbeiten. 

Was ich eigentlich ereichen wollte:
- Fake Daten
- Rendern Funktion von externen Klassen
- View fast fertig

<br>
<br>
<br>

## Wie war es?
Da es selbständige Arbeit war, musst man den Ablauf selber planen. 

<br>
<br>
<br>

## Wie ist es mir ergangen?
Heute bin ich gut vorwärts gekommen, da ich ja beide Lektionen Zeit hatte daran zuarbeiten. 
Da ich aber noch viel für die Abgabe 2 machen mustte hatte ich ein bisschen Stress


<br>
<br>
<br>

## Was habe ich gelernt?
Ich habe Arrays mit Fake Daten erstellt

### Model 
```php
 public function getFakeOrderData()
    {
        $data = [
            ['id' => '2', 'userid' => '', 'username' => 'TestBenutzer1','email' => 'test1@test.ch','comment' => 'TestKommentar1','refmenue' => '1','status' => '0','dateorder' => ''],
            ['id' => '3', 'userid' => '', 'username' => 'TestBenutzer2','email' => 'test2@test.ch','comment' => 'TestKommentar2','refmenue' => '2','status' => '1','dateorder' => ''],
            ['id' => '4', 'userid' => '', 'username' => 'TestBenutzer3','email' => 'test3@test.ch','comment' => 'TestKommentar3','refmenue' => '1','status' => '2','dateorder' => ''],
            ['id' => '5', 'userid' => '', 'username' => 'TestBenutzer4','email' => 'test4@test.ch','comment' => 'TestKommentar4','refmenue' => '3','status' => '0','dateorder' => '']
        ];

        return $data;
    }

    /**
     * TestMethode die einfach nur Fake-Daten liefert, solange man noch keine DB hat
     *
     * @param  mixed $userid
     *
     * @return $data : Liste aus Orders
     */
    public function getFakeOrderDataForUserID($userid)
    {
        $data = [
            ['id' => '2', 'userid' => '1','username' => 'TestBenutzer1','email' => 'test1@test.ch','comment' => 'TestKommentar1','refmenue' => '1','status' => '1','dateorder' => '']
        ];

        return $data;
    }
```
<br>

### Controller

```php
$menueArray = $menueModel->getFakeMenueDataArray(); 
$orderArray = $orderModel->getFakeOrderDataForUserID($userid);
```