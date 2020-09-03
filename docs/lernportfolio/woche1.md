# Schulwoche 1
##### 10. August - 16. August



<br>

## Was ist Container-Virtualisierung?
<img width="50%" src='./bilder/Virtualisierung.png'></img>

Containervirtualisierung ist eine Methode, um mehrere Instanzen eines Betriebssystems isoliert voneinander auf einem Hostsystem zu betreiben. Im Gegensatz zur Virtualisierung mittels eines Hypervisors hat Containervirtualisierung zwar einige Einschränkungen in der Art ihrer Gäste, gilt aber als besonders ressourcenschonend.

<br>



## Wofür wird Docker verwendet?
Docker ist ein Open-Source-Projekt zur automatisierten Bereitstellung von Applikationen, die in einem Container organisiert sind. Es nutzt hierzu die Eigenschaften des Linux-Kernel. Ressourcen wie Prozessor, RAM, Netzwerk oder Block-Speicher lassen sich so ohne den Start einer einzigen virtuellen Maschine voneinander isolieren. Weiterhin können Applikationen vollständig von der jeweiligen Umgebung inklusive der Prozesse, Dateisysteme oder des Netzwerks getrennt und damit autonom betrieben werden. Mit dem Aufheben von externen Abhängigkeiten lassen sich Applikationen autonom über Systeme hinweg verschieben. Docker kapselt dafür die eigentliche Anwendung und ihre notwendigen Abhängigkeiten wie Bibliotheken in einen virtuellen Container, welcher dann auf jedem beliebigen Linux- und Windows-System ausführbar ist. Dies erhöht den Portabilitätsgrad und die Flexibilität.

<br>

## Docker Hello World
Am besten ein Verzeichnis erstellen wo man das Images Hello World ausführen möchte.



__Eingabe__
```bash
docker run hello-world
```

__Ausgabe__
```
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
0e03bdcc26d7: Pull complete
Digest: sha256:7f0a9f93b4aa3022c3a4c147a449bf11e0941a1fd0bf4a8e6c9408b2600777c5
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

<br>

#### Überprüfen

__Eingabe__
```bash
docker ps -a
```

__Ausgabe__
```
CONTAINER ID        IMAGE                            COMMAND                  CREATED             STATUS                       PORTS                                           
bc34523c9bea        hello-world                      "/hello"                 19 seconds ago      Exited (0) 17 seconds ago                                                        
1396e81418e0        plantuml/plantuml-server:jetty   "/docker-entrypoint.…"   4 days ago          Exited (255) 2 minutes ago   0.0.0.0:10001->8080/tcp                             
5b1e4f262e4e        docsify-starter_docsify          "docker-entrypoint.s…"   4 days ago          Exited (255) 2 minutes ago   0.0.0.0:10000->10000/tcp, 0.0.0.0:35729->35729/tcp   

```
