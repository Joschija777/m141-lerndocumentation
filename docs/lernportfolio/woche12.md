# Schulwoche 12
##### 9. November - 15. November

<br>
<br>
<br>


## Was haben wir gemacht?
Heute haben wir zuerst die Abgabe 2 angeschaut. 

Danach haben wir angeschaut was wir in Abgabe 3 machen müssen:

15% Funktionale Sicherheitsanforderungen berücksichtigt
-  Dokumentation : Prepared-Statements (Nachforschungen im Tutorial)
-  Vergleich von Prepared-Statments und “traditionellem Zugriff
-  Abgelegt im Lernportfolio
-  Umsetzung : DB-Verbindung mit Prepared-Statements auf Models
-  Umsetzung : Arbeiten mit Übergabeparameter nach Vorlage und Beispielen
-  Fehlerbehandlung angewendet

~20% Teilsysteme / Schnittstellen sinnvoll gewählt (DB)
-  (DB-)-Tabellen den funktionalen Anforderungen folgend angewendet
-  (DB-)-Datentypen den funktionalen Anforderungen folgendangewendet (< oder sinnvoll begründet)
-  Anwendung sql-Scripts in der Dokumentation beschrieben
-  Export der Beispieltabellen konsquent gemacht
-  Export der Beispieldaten-Imports konsquent gemacht





<br>
<br>
<br>

## Wie war es?
Es war intressant gestaltet, aber mit schon zuviel Informationen.
Zu kompliziert Gestalten mit MYSQL, könnte man viel besser erklären.

<br>
<br>
<br>

## Wie ist es mir ergangen?
Heute bin ich gut vorwärts gekommen, da ich ja beide Lektionen Zeit hatte daran zuarbeiten.

<br>
<br>
<br>

## Was habe ich gelernt?


```php
class OrderModel extends BaseModel
{

    /**
     * insertOrderDB - Übernimmt den data-Array und inserted es in die DB
     *
     * @param  mixed $data - Data Array aus der GUI
     *
     * @return boolean - Erfolgsfall oder nicht
     */
    public function insertOrderDB($data)
    {
        $this->db->query("INSERT INTO `orders` 
        (`userid`, `username`, `email`, `comment`, `refmenue`, `status`, `dateorder`)
        VALUES (:userid, :username, :email, :comment, :refmenue, :status, now())");

        $this->db->bind(':userid',$data['userid']);
        $this->db->bind(':username',$data['username']);
        $this->db->bind(':email',$data['email']);
        $this->db->bind(':comment',$data['comment']);
        $this->db->bind(':refmenue',$data['refmenue']);
        $this->db->bind(':status',0); // Neue Bestellung, Status ist immer 0

        return $this->db->execute(); // Gibt True im Erfolgsfall, False im Fehlerfall
    }
```



```php
    /**
     * changeStatusDB - Ändert den Status für eine Bestellung auf der DB. Wird benutzt vom Admin-Controller aus
     *
     * @param  mixed $orderID - Order ID
     * @param  mixed $status - Status der gesetzt werden soll (TinyInt)
     *
     * @return boolean - Erfolg oder nicht
     */
    public function changeStatusDB($orderID, $status)
    {
        $this->db->query("UPDATE orders SET status = :status WHERE id = :oderid");
        $this->db->bind(':oderid',$orderID);
        $this->db->bind(':status',$status);


        // Wenn man gucken will was da gebaut wurde, Debug-Methode aufrufen!

        return $this->db->execute(); // Gibt True im Erfolgsfall, False im Fehlerfall
    }

    /**
     * getOrderData - Holt die Liste aller Bestellungen aus der Datenbank
     *
     * @return $results - Array aus Bestellungen
     */
    public function getOrderData()
    {
        $this->db->query("SELECT * FROM `orders`");
        $results = $this->db->resultSet();

        return $results;
    }
```
