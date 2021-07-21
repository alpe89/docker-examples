# Lo step iniziale solitamente è partire da una immagine, in questo caso
# inizio con una immagine di base di nodejs versione 14
# questa immagine è hostata su dockerhub
FROM node:14
# Imposto la working directory dove andrò a copiare i file che serviranno alla mia 
# app
WORKDIR /project/fe
# Imposto i permessi per le cartelle per l'utente che voglio usare
RUN chown -R node /project
# Imposto l'utente che userò per eseguire le operazioni nel container
USER node
# Copio i file per la gestione delle dipendenze della mia app così da sfruttare la 
# cache al meglio
COPY --chown=node package.json .
COPY --chown=node yarn.lock .
# Avvio l'installazione delle dipendenze tramite yarn
RUN ["yarn", "install"]
# Copio i restanti file nel container
COPY --chown=node . .
# Eseguo la build
RUN ["yarn", "build"]