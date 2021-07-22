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
# Avvio l'installazione delle dipendenze tramite npm
RUN npm install
# Comando di default da eseguire all'avvio del container
CMD ["npm", "start"]
# Informo il container di esporre la porta 3000
EXPOSE 3000