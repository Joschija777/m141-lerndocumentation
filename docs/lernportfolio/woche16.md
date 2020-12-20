# Schulwoche 16
##### 07. Dezember - 13. Dezember

<br>
<br>
<br>


## Was haben wir gemacht?

Am heutigen Tag haben wir nichts neues angeschaut, wir durften an der letzten LB abgabe weiter Arbeiten.


<br>
<br>
<br>

## Wie war es?
Da es selbständige Arbeit war, musst man den Ablauf selber planen.
Zudem fand ich gut das man die LB in 4 Abgaben aufgeteilt hat und jede Abgabe mit Teilaufgaben unterteilt.

<br>
<br>
<br>

## Wie ist es mir ergangen?
Heute bin ich gut vorwärts gekommen, da ich ja beide Lektionen Zeit hatte daran zuarbeiten.

<br>
<br>
<br>

## Was habe ich gelernt?

#### UserModel

```PHP
class UserModel extends BaseModel
{

    /**
     * login - Funktion. Übernimmt die Email und das Passwort (Cleartext) und vergleicht auf den Hash aus der DB
     *
     * @param  mixed $email
     * @param  mixed $password
     *
     * @return void
     */
    public function login($email, $password)
    {
        $this->db->query('SELECT * FROM users WHERE email = :email');
        $this->db->bind(':email', $email);

        $row = $this->db->single();
        $hashed_pass = $row['password'];

        if (password_verify($password, $hashed_pass))
        {
            return $row;
        } else
        {
            return false;
        }
    }


    /**
     * registerUser - Nach der erfolgreichen Registrierung (Formular bestanden) wird der Benutzer auf der Datenbank gespeichert
     * Default Einstellung : user
     *
     * @param  mixed $data
     *
     * @return void
     */
    public function registerUser($data)
    {
        // Default Benutzer wird normaler User
        $obj = ["user"];
        $json = json_encode($obj);

        $this->db->query("INSERT INTO `users` (`name`, `email`, `password`, `created_at`, `roles`)
            VALUES (:name, :email, :password, now(), :json);");

        $this->db->bind(':name', $data['name']);
        $this->db->bind(':email', $data['email']);
        $this->db->bind(':password', $data['password']);
        $this->db->bind(':json', $json);

        if ($this->db->execute())
        {
            return true;
        } else
        {
            return false;
        }

    }

    /**
     * getUsers - Liste aller Benutzer
     *
     * @return $results - Resultset
     */
    public function getUsers()
    {
        $this->db->query("SELECT * FROM users");
        $results = $this->db->resultSet();

        return $results;
    }

    /**
     * getUsers - Liste aller Benutzer mit einer bestimmten Email, nur eine Antwort
     *
     * @return $row - Eine Datarow
     */
    public function getUserForEmail($email)
    {
        $this->db->query("SELECT * FROM users WHERE email = :email");
        $this->db->bind(':email', $email);

        $row = $this->db->single();

        return $row;
    }


    /**
     * checkUserForEmail - Wichtige Hilfsfunktion für Registrierung. Ziel: Gucken ob bereits eine Email besetzt ist.
     *
     * @param  mixed $email
     *
     * @return boolean
     */
    public function checkUserForEmail($email)
    {
        $this->db->query("SELECT * FROM users WHERE email = :email");
        $this->db->bind(':email', $email);

        $row = $this->db->single();

        if ($this->db->rowCount() > 0)
        {
            return true;
        } else {
            return false;
        }
    }

    /**
     * getUsersForRole - Hilfsfunktion: User listen mit einer bestimmten Rolle
     *
     * @param  mixed $role - String
     *
     * @return $results - Resultset
     */
    public function getUsersForRole($role)
    {

        $obj = [$role];
        $json = json_encode($obj);

        $this->db->query("SELECT * FROM users WHERE JSON_CONTAINS(roles, :json);");
        $this->db->bind(':json', $json);
        $results = $this->db->resultSet();

        return $results;
    }


    /**
     * getUserForID - Liste aller Benutzer mit einer bestimmten Email, nur eine Antwort
     *
     * @param  mixed $userid
     *
     * @return $row - DataRow
     */
    public function getUserForID($userid)
    {
        $this->db->query("SELECT * FROM users WHERE id = :id");
        $this->db->bind(':id', $userid);

        $row = $this->db->single();

        return $row;
    }
```
