FROM node:14.0.0-alpine3.11 as build-stage
WORKDIR /app
COPY vue/app/package*.json ./
RUN npm install
COPY vue/app/ ./
RUN npm run build

FROM nginx:1.17.10-alpine as production-stage
RUN mkdir /app
COPY --from=build-stage /app/dist /app
COPY nginx/nginx.conf /etc/nginx/nginx.conf
COPY keys/localhost.key /etc/nginx/ssl/localhost.key
COPY keys/localhost.crt /etc/nginx/ssl/localhost.crt