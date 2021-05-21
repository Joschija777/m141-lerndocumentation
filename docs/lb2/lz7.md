# Datentypen anwenden

__Datentyp:__

Datentyp | Verwendung im Projekt  | Beschreibung  
:-------- | :---------- | :----------
VARCHAR |  E-Mail,  Telefonnummer(wegen 0 kein Double), Strasse, Stadt, Name,   |    Zeichenkette variabler Länge, Maximum ist M. Wertebereich für M: 0 bis 255.
INT |  Primary Key wie(ID), FOREIGN KEY   |    Ganzzahlen von 0 bis ~4,3 Mill. oder von -2.147.483.648 bis 2.147.483.647.
SMALLINT |  Kleine Zahlen wie(Postleizahl)   |    	Ganzzahlen von 0 bis 65.535 oder von -32.768 bis 32.767.
FLOAT |  Daten, Temperatur, BreiteKoordinaten, LaengeKoordinaten   |    	Fließkommazahl mit Vorzeichen. Wertebereich von -(3,402823466×1038) bis -(1,175494351×10-38)




__Alle:__

Datentyp | Speicherplatz | Beschreibung
:-------- | :---------- | :----------
TINYINT | 1 Byte | Ganzzahlen von 0 bis 255 oder von -128 bis 127.
SMALLINT | 2 Bytes | Ganzzahlen von 0 bis 65.535 oder von -32.768 bis 32.767.
MEDIUMINT | 3 Bytes | Ganzzahlen von 0 bis 16.777.215 oder von -8.388.608 bis 8.388.607.
INT | 4 Bytes | Ganzzahlen von 0 bis ~4,3 Mill. oder von -2.147.483.648 bis 2.147.483.647.
INTEGER | 4 Bytes | Alias für INT.
BIGINT | 8 Bytes | Ganzzahlen von 0 bis 2^64-1 oder von -(2^63) bis (2^63)-1.
FLOAT | 4 Bytes | Fließkommazahl mit Vorzeichen. Wertebereich von -(3,402823466×1038) bis -(1,175494351×10-38), 0 und 1,175494351×10-38 bis 3,402823466×1038.
DOUBLE | 8 Bytes | Fließkommazahl mit Vorzeichen. Wertebereich von -(1,79769×10308) bis -(2.22507×10-308), 0 und 2.22507×10-308 bis 1,79769×10308
REAL | 8 Bytes | Alias für DOUBLE.
DECIMAL | M+x Bytes | Fließkommazahl mit Vorzeichen. Speicherbedarf: x=1 wenn D=0, sonst x=2. Ab MySQL 5.1 binär gespeichert, zuvor als String.
NUMERIC | M+x Bytes | Alias für DECIMAL.
DATE | 3 Bytes | Datum im Format 'YYYY-MM-DD'. Wertebereich von 01.01.1000 bis 31.12.9999.
DATETIME | 8 Bytes | Datumsangabe im Format 'YYYY-MM-DD hh:mm:ss'. Wertebereich entspricht DATE.
TIMESTAMP | 4 Bytes | Zeitstempel. Wertebereich: 1.1.1970 bis 19.01.2038. Das Format variiert in den MySQL-Versionen.
TIME | 3 Bytes | Zeit zwischen -838:59:59 und 839:59:59. Ausgabe: hh:mm:ss.
YEAR | 1 Byte | Jahr zwischen 1901 bis 2155 bei (4) und zwischen 1970 bis 2069 bei (2).
CHAR | M Byte(s) | Zeichenkette fester Länge M. Wertebereich für M: 0 bis 255.
VARCHAR | L+1 Bytes | Zeichenkette variabler Länge, Maximum ist M. Wertebereich für M: 0 bis 255.
BINARY | M Bytes | Zum Speichern binärer Strings, unabhängig vom Zeichensatz. Wertebereich für M: 0 bis 255. Weiterer Typ: VARBINARY
BLOB | L+2 Bytes | Binäres Objekt mit variablen Daten. Weitere Typen: TINYBLOB, MEDIUMBLOB und LONGBLOB. M ist ab Version 4.1 definierbar.
TEXT | L+2 Bytes | Wie BLOB. Ignoriert beim Sortieren & Vergleichen Groß- und Kleinschreibung. Weitere Typen: TINYTEXT, MEDIUMTEXT, LONGTEXT. M ist ab Version 4.1 definierbar.
ENUM | 1 oder 2 Bytes | Liste von Werten (val1, val2, ...). 65.535 eineindeutige Elemente sind maximal möglich.
SET | x Bytes | String-Objekt mit verschiedenen Variablen. 64 sind maximal möglich. Speicherbedarf: x ist 1, 2, 3, 4 oder 8.