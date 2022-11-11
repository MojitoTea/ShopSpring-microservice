FROM node:14-alpine3.16 AS build
WORKDIR /app
COPY ["package.json","package-lock.json","/app/"]
RUN npm install
RUN npm install -g @angular/cli

COPY . /app
RUN ["ng","build","--prod"]

FROM nginx:1.13.3-alpine
COPY /nginx/default.conf /etc/nginx/conf.d/
RUN rm -rf /usr/share/nginx/html/*
COPY --from=build /app/dist/shop /usr/share/nginx/html
