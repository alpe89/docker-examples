FROM node:14 AS build-stage
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
RUN npm ci --silent
# Copio i restanti file nel container
COPY --chown=node . .
# Eseguo la build
RUN npm run build

FROM nginx:1.21.1-alpine
#copies React to the container directory
# Set working directory to nginx resources directory
WORKDIR /usr/share/nginx/html
# Remove default nginx static resources
RUN rm -rf ./*
# Copies static resources from builder stage
COPY --from=build-stage /project/fe/build .
# Containers run nginx with global directives and daemon off
ENTRYPOINT ["nginx", "-g", "daemon off;"]