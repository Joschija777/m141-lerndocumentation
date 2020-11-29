# Vergleich PPS & traditionellem Zugrif 

## Prepared Statement

### PHP Code:

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



> [!NOTE|style:flat]
Die Prepared abfrage sollte schneller schneller sein als der traditionelle Zugriff, zudem ist er Sicherer da man die Daten nicht einfach manipulieren kann.

<br>
<br>

## Traditioneller Zugriff

### PHP Code:

```php
$sql = "INSERT INTO `reiseantrag` (`id`, `vorname`, `nachname`, `userid`, `hinreise`, `rueckreise`, `reiseziel`, `reisezweck`, `refFlugzeug`, `refFahrzeug`, `refOev`, `status`)
VALUES ('3', 'Test', 'TestUser', '2', '2020-12-12', '2020-12-12', 'Bern', 'Schulung', '1', NULL, NULL, '0');
```


