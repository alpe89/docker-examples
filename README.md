# Esempi di utilizzo di Docker per il Frontend

> Semplici esempi per iniziare con lo sviluppo di applicazioni Dockerizzate

## Istruzioni

Clonare il repository ed entrare nella cartella react-app

```bash
git clone https://github.com/alpe89/docker-examples.git && cd docker-examples/react-app
```

## Uso dell'immagine base

Posizionarsi nella branch `creazione-immagine` ed avviare la build dell'immagine

```bash
git checkout creazione-immagine && docker build -t docker-example-fe:creazione-immagine .
```

Una volta terminata la build possiamo utilizzare questa immagine per avviare un container

```docker
docker run -d --rm -p 3000:5000 --name react-app docker-example-fe:creazione-immagine
```

Possiamo quindi aprire nel browser `localhost:3000` ed avremo la nostra app react esposta nella sua build di produzione.

## Uso di Docker per lo sviluppo

Rimanendo sempre nella stessa branch di sviluppo possiamo sfruttare la stessa immagine (o crearne una dedicata volendo) per sviluppare direttamente all'interno di un container. Il comando per avviare un container `di sviluppo` è

```docker
docker run -d --rm -p 3000:3000 -v "$(pwd):/project/fe/" --name dev-container docker-example-app:creazione-immagine npm start
```

> Attenzione: per questa sezione il comando potrebbe non funzionare correttamente sotto windows, specialmente se Docker è impostato nell'utilizzo di Linux Containers.

## Uso della multi stage build

Cambiando la branch in `multi-stage-build` o `master` possiamo eseguire la build del nuovo Dockerfile che sfrutta le multi stage build.

```bash
docker build -t docker-example-fe:multi-stage .
```
Successivamente possiamo eseguire il container risultante
```docker
docker run -d --rm -p 8080:80 --name nginx-app docker-example-fe:multi-stage
```