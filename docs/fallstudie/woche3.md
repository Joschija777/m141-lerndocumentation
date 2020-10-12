# SSR & CSR

## Server Side Rendering



### PlantUML
```plantuml

@startuml

actor Joschija
participant WebBrowser
participant WebServer
participant PHP


Joschija -> WebBrowser : Webbrowser öffnen
activate WebBrowser
WebBrowser -> WebServer : HTTP/POST - index.html
activate WebServer
WebServer -> PHP : Erkennt PHP / an Interpreter
activate PHP
PHP -> PHP : Führt PHP aus
PHP -> WebServer: Liefert Ausgabe an webserver zurück
deactivate PHP
WebServer -> WebBrowser : Liefert HTML an Browser aus 
deactivate WebServer
WebBrowser -> Joschija : Seite ist jetzt sichtbar 
deactivate WebBrowser

@enduml

```


## Client Side Rendering


### PlantUML
```plantuml

@startuml

actor Joschija
participant WebBrowser
participant WebServer
participant JSON


Joschija -> WebBrowser : Webbrowser öffnen
activate WebBrowser
WebBrowser -> WebServer : HTTP/POST - index.html
activate WebServer
WebServer -> WebBrowser : Browser lädt Javascript... herunter
deactivate WebServer
WebBrowser -> JSON : zB. addButton (ajax js daten anfordern)
activate JSON
JSON -> WebBrowser : z.B Tabelle generieren
deactivate JSON
WebBrowser -> WebBrowser : Browser führt Reaktionen aus (Rendern)
WebBrowser -> Joschija : Seite ist jetzt sichtbar und interaktiv
deactivate WebBrowser

@enduml

```

<br>

#### Vorteile:
- Schnelles Rendern der Website nach dem ersten Laden.
- Ideal für Webanwendungen.
- Robuste Auswahl an JavaScript-Bibliotheken.

#### Nachteile:
- Geringe SEO, wenn nicht richtig implementiert.
- Das anfängliche Laden erfordert möglicherweise mehr Zeit.
- In den meisten Fällen ist eine externe Bibliothek erforderlich.