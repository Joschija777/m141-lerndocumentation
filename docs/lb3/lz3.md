# Stored Procedures


## Alle SP anzeigen von DB
```
SHOW PROCEDURE STATUS WHERE Db = 'classicmodels';
```



show fields from orders;

<br>
<br>


## Einlesen und Counten
Erstellen Sie nun eine SP, welche den Bestellungsstatus einlesen kann und die Anzahl der Bestellungen, die diesem Status entsprechen, in eine Ausgabevariable speichert.


```
DELIMITER //
CREATE PROCEDURE sp (IN bStatus VARCHAR(12))
BEGIN 
    SELECT COUNT(*) FROM orders WHERE status = bStatus;
END//
DELIMITER ;
```


```
call sp('Shipped');
```

<br>
<br>


## DB befüllen
```
DELIMITER //
CREATE PROCEDURE simpleproc (IN name varchar(50),IN user_name varchar(50),IN branch varchar(50))
BEGIN
    insert into student (name,user_name,branch) values (name ,user_name,branch);
END//
DELIMITER ;
```



<br>
<br>

## INOUT Example

```
CREATE PROCEDURE p (OUT ver_param VARCHAR(25), INOUT incr_param INT)
BEGIN
  # Set value of OUT parameter
  SELECT VERSION() INTO ver_param;
  # Increment value of INOUT parameter
  SET incr_param = incr_param + 1;
END;
```

https://www.mysqltutorial.org/stored-procedures-parameters.aspx#:~:text=An%20INOUT%20parameter%20is%20a,back%20to%20the%20calling%20program.