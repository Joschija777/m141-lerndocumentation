# SSR & CSR

## Server Side Rendering
Beim Server-seitigen Rendern werden die React-Komponenten auf dem Server gerendert. Die Ausgabe ist HTML-Inhalt. Das kann natürlich eine gewisse Geschwindigkeit bieten. Suchmaschinenoptimierte Seiten gehen deshalb lieber den SSR-Weg.

__Userfeeling:__ Das anfängliche Laden der Seite ist schneller als beim Client-seitigen Rendern. In Spitzenzeiten zahlreicher Anfragen leidet allerdings die Leistung der Website darunter. Geeignet eher für statische Seiten. 

<br>

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

#### Vorteile:
- deutliche Leistungsverbesserung (bei kleineren Anwendungen)
- Suchmaschinenoptimierung
- Leistungsbeeinträchtigung bei größeren Anwendungen

#### Nachteile:
- Erhöhte Antwortzeiten in Spitzenzeiten
- Erhöhte Komplexität der Anwendung


<br>
<br>
<br>

## Client Side Rendering
Beim Client-seitigen Rendern lädt der Browser eine minimale HTML-Seite. Es rendert das JavaScript und füllt den Inhalt darin.

__Userfeeling:__ Nach dem anfänglichen, langsamen Laden ist der Rest des Website-Renderings schneller. Die anfängliche Ladezeit kann aber frustrierend sein. Geeignet eher für interaktive Webanwendungen mit mehr statischem Inhalt. 

<br>

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