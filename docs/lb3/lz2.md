# Views 



## Views anzeigen

```mysql
show full tables where table_type = 'View';
```

<img width="80%" src='./bilder/showView.png'></img>


<br>
<br>


## Beispiele 

##### Beispiel 1: Alle Customers anzeigen

```mysql
create view v_cust as select * from customers;
```

```mysql
select * from v_cust;
```

<img width="100%" src='./bilder/Views.png'></img>


<br>
<br>


##### Beispiel 2: Attributname ändern
Sie wollen in der views Anrede als anr und Vorname als vn haben


```mysql
create view test_v 
as Select Anrede AS anr, Vorname AS vn, From Kunden;
```

```mysql
create View test_v (anr, vn)
AS Select Anrede, Vorname FROM Kunden;
```


<br>
<br>


##### Beispiel 2: Attributname ändern
Sie wollen in der views Anrede als anr und Vorname als vn haben


```mysql
create view test_v 
as Select Anrede AS anr, Vorname AS vn, From Kunden;
```

```mysql
create View test_v (anr, vn)
AS Select Anrede, Vorname FROM Kunden;
```



<br>
<br>


##### Beispiel 3: Join
stellen Sie eine View, die von allen “employees” den Vor- und Nachnamen ausgibt. Zusätzlich
soll noch der “titles” für den Employee angezeigt werden.

<img width="70%" src='./bilder/viewBeispiel.png'></img>

```mysql
create view show_V 
SELECT employees.first_name, employees.last_name, titles.title
FROM employees
LEFT JOIN titles ON employees.emp_no = titles.emp_no
ORDER BY employees.first_name;
```



