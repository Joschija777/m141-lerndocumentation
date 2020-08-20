# Schulwoche 2

### A1: Hello World ausführen

#### A1.1: Führen Sie den Hello World-Container aus

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

#### A1.2: Bringen Sie einen Wahl dazu, Ihren Namen zu sagen

```
 docker run docker/whalesay cowsay joschija
 ```

 ```
 __________
< joschija >
----------
   \
    \
     \     
                   ##        .            
             ## ## ##       ==            
          ## ## ## ##      ===            
      /""""""""""""""""___/ ===        
 ~~~ {~~ ~~~~ ~~~ ~~~~ ~~ ~ /  ===- ~~~   
      \______ o          __/            
       \    \        __/             
         \____\______/   
```

### A2:
```
docker pull mysql
```

```
Using default tag: latest
latest: Pulling from library/mysql
bf5952930446: Pull complete
8254623a9871: Pull complete
938e3e06dac4: Pull complete
ea28ebf28884: Pull complete
f3cef38785c2: Pull complete
894f9792565a: Pull complete
1d8a57523420: Pull complete
6c676912929f: Pull complete
ff39fdb566b4: Pull complete
fff872988aba: Pull complete
4d34e365ae68: Pull complete
7886ee20621e: Pull complete
Digest: sha256:c358e72e100ab493a0304bda35e6f239db2ec8c9bb836d8a427ac34307d074ed
Status: Downloaded newer image
```


```
docker images
```


```
REPOSITORY                 TAG                 IMAGE ID            CREATED             SIZE
docsify-starter_docsify    latest              46f341a5da0f        6 days ago          899MB
node                       10-buster           072a515fb11a        2 weeks ago         879MB
mysql                      latest              0d64f46acfd1        2 weeks ago         544MB
plantuml/plantuml-server   jetty               6ee17d4a519c        3 weeks ago         438MB
hello-world                latest              bf756fb1ae65        7 months ago        13.3kB
docker/whalesay            latest              6b362a9f73eb        5 years ago         247MB
```



```
docker run --name mysql -e MYSQL_ROOT_PASSWORD=test mysql:latest
```


```
2020-08-20 07:45:47+00:00 [Note] [Entrypoint]: Entrypoint script for MySQL Server 8.0.21-1debian10 started.
2020-08-20 07:45:48+00:00 [Note] [Entrypoint]: Switching to dedicated user 'mysql'
2020-08-20 07:45:48+00:00 [Note] [Entrypoint]: Entrypoint script for MySQL Server 8.0.21-1debian10 started.
2020-08-20 07:45:48+00:00 [ERROR] [Entrypoint]: Database is uninitialized and password option is not specified
	You need to specify one of MYSQL_ROOT_PASSWORD, MYSQL_ALLOW_EMPTY_PASSWORD and MYSQL_RANDOM_ROOT_PASSWORD
```

### A3

```
docker images
```


```
REPOSITORY                 TAG                 IMAGE ID            CREATED             SIZE
docsify-starter_docsify    latest              46f341a5da0f        6 days ago          899MB
node                       10-buster           072a515fb11a        2 weeks ago         879MB
mysql                      latest              0d64f46acfd1        2 weeks ago         544MB
plantuml/plantuml-server   jetty               6ee17d4a519c        3 weeks ago         438MB
hello-world                latest              bf756fb1ae65        7 months ago        13.3kB
docker/whalesay            latest              6b362a9f73eb        5 years ago         247MB
```

### A4

```
docker ps
```

```
docker container ls
```

```
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
1aa9a378abe4        mysql:latest        "docker-entrypoint.s…"   3 minutes ago       Up 3 minutes        3306/tcp, 33060/tcp   mysql
```

Stopen:

```
docker stop 1aa9a378abe4
````

### A5

```
docker run -i --name mysql -e MYSQL_ROOT_PASSWORD=test mysql:latest /bin/bash
```
