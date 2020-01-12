FROM node:10.16-alpine

WORKDIR /home/www/app-example

COPY package.json *.lock .

RUN npm install

COPY . .

EXPOSE 3000

CMD [ "node", "./app.js" ]
