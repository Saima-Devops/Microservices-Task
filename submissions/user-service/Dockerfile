FROM node:20-alpine

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

ENV NODE_ENV=prod123

EXPOSE 3000

CMD ["node", "app.js"]
