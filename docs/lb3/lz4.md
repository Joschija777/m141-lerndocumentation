# Backup



##### warm, logisch & full

in Datei exportieren
```sql
mysqldump --single-transaction -u root -p --all-databases > dump.sql
```

importieren
```sql
mysql -u root -p < dump.sql
```

<br>
<br>

##  Übung 1 - Lokales Backup

Richten Sie auf Ihrem Server ein Backup-Script, gemäss der Vorlage von oben, ein. Testen Sie das Script aus ob der Export funktioniert und Sie die Daten auch wieder importieren können ("Niemand will Backup - alle wollen restore")

```terminal
sudo nano test.sh
```

```bash
#!/bin/bash
# Add the backup dir location, MySQL root password, MySQL and mysqldump location
DATE=$(date +%d-%m-%Y)
BACKUP_DIR="/tmp/test-backup"
MYSQLroot='root'
MYSQL_PASSWORD='Admin_123'
MYSQL=/usr/bin/mysql
MYSQLDUMP=/usr/bin/mysqldump

# To create a new directory in the backup directory location based on the date
mkdir -p $BACKUP_DIR/$DATE

# To get a list of databases
databases=`$MYSQL -u$MYSQL_USER -p$MYSQL_PASSWORD -e "SHOW DATABASES;" | grep -Ev "(Database|information_schema)"`

# To dump each database in a separate file
for db in $databases; do
echo $db
$MYSQLDUMP --single-transaction --force --opt --skip-lock-tables --user=$MYSQL_USER -p$MYSQL_PASSWORD --databases $db | gzip > "$BACKUP_DIR/$DATE/$db.sql.gz"
done

# Delete the files older than 10 days
find $BACKUP_DIR/* -mtime +10 -exec rm {} \;
```

```
bash test.sh
```

<br>
<br>


##  Übung 4 - Migration auf entfernten Server#

Vorbereitung:

1. Erstellen Sie einen Klon Ihrer MySQL-VM mit neuen MAC-Adressen
2. Verbinden Sie die orginale VM mit der geklonten VM in einem NAT-Network <- Testen Sie die Verbindung untereinander
3. Testen Sie die SSH-Verbindung zwischen den VMs

Verbindung ssh zu 192.168.10.4

```
ssh vagrant@192.168.10.4
```

```
apt-get install openssh-server openssh-client
```

<br>


Auftrag

Führen Sie einen entfernten Backup mittels SSH, gemäss den Anleitung von oben, durch. Nutzen Sie das Beispiel "Verbindung zwischen den Servern per SSH möglich".

Schrittweises Vorgehen:

1. SSH auf den Export-Server
2. Dump durchführen und Ausabe auf PIPE umleiten
3. die PIPE umleiten auf die SSH-Verbindung zum Import-Server


Version : Keine direkte Verbindung zwischen den Servern, der Datentraffic muss über den Laptop umgeleitet werden

```
ssh user@SERVER1 'mysqldump --single-transaction -u root -pPASS DBNAME' | ssh user@SERVER2 'mysql -u USER -pPASS NEWDB'
```


```
ssh vagrant@192.168.10.4 'mysqldump --single-transaction -u root -pAdmin_123 roehFix | gzip -9' | ssh vagrant@192.168.10.5 'gunzip | mysql -uroot -pAdmin_123 NewRoehfix'
```




mysqldump --single-transaction -uroot -pAdmin_123 roehFix -h localhost \ | mysql -uroot -pAdmin_123 -h 192.168.10.4 newRoehFix



## Migration import, dump

```
# Dump erstellen und direkt zippen
mysqldump --single-transaction -u root -p DB | gzip -9 > /tmp/DUMP_DB.sql.gz

# Files auf einen anderen Server kopieren, meistens über SSH
scp /tmp/DUMP_DB.sql.gz root@ANDERERSERVERIP:/tmp/

# Auf dem Zielserver neue NEUEDB erstellen

# Direktes Entzippen und importieren
gunzip < DUMP_DB.sql.gz | mysql -u root -p NEUEDB
```