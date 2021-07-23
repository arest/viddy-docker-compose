FROM node:10

WORKDIR /var/www/html

COPY package*.json ./

RUN npm install

EXPOSE 3000

CMD ["npm", "run", "dev"]