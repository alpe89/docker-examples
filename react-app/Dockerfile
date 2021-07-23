FROM node:14 AS build-stage
WORKDIR /project/fe
RUN chown -R node /project
USER node
COPY --chown=node package*.json .
RUN npm ci --silent
COPY --chown=node . .
RUN npm run build

# Secondo stage
FROM nginx:1.21.1-alpine
# Setto la directory di lavoro su quella di nginx
WORKDIR /usr/share/nginx/html
# Cancello le risorse di default di nginx
RUN rm -rf ./*
# Copio il risultato della build dello step precedente
COPY --from=build-stage /project/fe/build .
# Script da avviare all'avvio del container (nginx)
ENTRYPOINT ["nginx", "-g", "daemon off;"]