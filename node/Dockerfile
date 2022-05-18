FROM node:12-alpine

RUN apk add git zip ruby-dev build-base ruby-rdoc && \
    npm set progress=false && \
    npm config set depth 0

WORKDIR /var/www/html

COPY package*.json ./

COPY bower*.json ./

RUN gem install compass

RUN apk update && apk upgrade && apk add bash

RUN npm install

RUN npm install -g bower

CMD ["npm install && bower install && node_modules/grunt/bin/grunt"]