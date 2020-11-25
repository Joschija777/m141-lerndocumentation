# Prepared-Statements 

## Was ist das?
Ein Prepared Statement ist eine sogenannte vorbereitete Anweisung für ein Datenbanksystem. Im Gegensatz zu gewöhnlichen Statements enthält es noch keine Parameterwerte. Stattdessen werden dem Datenbanksystem Platzhalter übergeben.

## Wofür braucht man das?
Der entscheidende Grund dafür, in Datenbankmanagementsystemen wie MySQL mit Prepared Statements zu arbeiten, ist der Aspekt Sicherheit. Das wohl größte Problem an standardmäßigen Zugriffen auf Datenbanken mit SQL-Sprachhintergrund ist nämlich die Tatsache, dass diese sich leicht manipulieren lassen. Man spricht in diesem Fall von einer SQL-Injection, bei der Code hinzugefügt oder angepasst wird, um an sensible Daten zu gelangen oder gar gänzlich die Kontrolle über das Datenbanksystem zu erlangen. 


## Beispiel

### Code von meinen Projekt

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
Sozusagen nehme ich mit z.B :vorname den Array $data['vorname'] anstatt direkt eine Wert reinschreiben.

<br>
<br>

### Ohne Prepare Statement

```sql
INSERT INTO `reiseantrag` (`id`, `vorname`, `nachname`, `userid`, `hinreise`, `rueckreise`, `reiseziel`, `reisezweck`, `refFlugzeug`, `refFahrzeug`, `refOev`, `status`)
VALUES ('3', 'Test', 'TestUser', '2', '2020-12-12', '2020-12-12', 'Bern', 'Schulung', '1', NULL, NULL, '0');
```