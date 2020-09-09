# Woche 1


```plantuml


@startuml

(Scripting-Sprachen) as (ScriptSprachen)
(PHP)
(HTML)
(Webapplikation) as (Web)
(Methoden)
(POST)
(GET)
(Formular)
(ISSET)
(EMPTY)
(print_r)
(var_dumb)
(Funktionen)










(Web) <--- (PHP)
(Web) <--- (HTML)
(ScriptSprachen) <---> (PHP)
(PHP) <--> (HTML)
(Formular) ---> (HTML)
(PHP) <--- (Methoden)
(PHP) <--- (Funktionen)
(Funktionen) <--- (print_r)
(Funktionen) <--- (var_dumb)
(Funktionen) <--- (ISSET)
(Funktionen) <--- (EMPTY)
(GET) ---> (Methoden)
(POST) ---> (Methoden)
(POST) <--> (GET)
(Formular) <--- (Methoden)
(POST) ...> (Formular)
(GET) ...> (Formular)






note right of (HTML)
  HTML ist eine textbasierte Auszeichnungssprache
  zur Strukturierung elektronischer Dokumente wie
  Texte mit Hyperlinks, Bildern und anderen Inhalten.
end note

note right of (PHP)
 PHP ist eine Scriptsprache
 die sich besonders für
 Webapplikationen eignet
end note

note right of (ISSET)
Überprüft, ob eine Variable
vorhanden ist
end note

note right of (EMPTY)
Überprüft, ob eine Variable
keinen Inhalt hat
end note

note right of (print_r)
Zeigt den Inhalt einer
Variable in lesbarer
Form
end note

note right of (var_dumb)
Zeigt den Inhalt
mehrerer Variablen in
lesbarer Form ganz
detaillier
end note

note right of (Funktionen)
Funktionen sind flapsig gesagt,
kleine Programme im großen Ablauf.
end note

note right of (GET)
ist ein Array welches alle Parameter
aus der vom Besucher aufgerufenen URL
enthält.
end note

note right of (POST)
Der Array $_POST[] enthält den Inhalt
von Variablen aus einem anderem Dokument,
und nutzt diesen dann in dem
vorhandenem Dokument.
end note







note "Wird für Webapps \n eingesetzt" as NWebapps
(ScriptSprachen) .. NWebapps
NWebapps .. (PHP)


note "Methode zum übertragen \n vom Variablen" as Mpoge
(POST) .. Mpoge
Mpoge .. (GET)

note "Methoden sind Funktionen, \n die innerhalb einer \n Klasse verwendet werden" as nMethoden
(Methoden) .. nMethoden
nMethoden .. (Funktionen)

@enduml

```
