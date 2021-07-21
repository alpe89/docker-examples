# Lo step iniziale solitamente è partire da una immagine, in questo caso
# inizio con una immagine di base di nodejs versione 14
# questa immagine è hostata su dockerhub.
# Solitamente il Dockerfile andrebbe all'interno della root del progetto, 
# essendo questo un esempio lo abbiamo in una cartella diversa e tramite il flag -f 
# possiamo dire a Docker dove si trova il Dockerfile di cui vogliamo eseguire 
# la build
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
COPY --chown=node package*.json .
# Avvio l'installazione delle dipendenze tramite yarn
RUN npm ci --silent
# Copio i restanti file nel container
COPY --chown=node . .
# Eseguo la build
RUN npm run build
# Comando di default da eseguire all'avvio del container
CMD ["npm", "run", "serve"]
# Informo il container di esporre la porta 5000
EXPOSE 5000