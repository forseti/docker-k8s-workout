FROM node:alpine

WORKDIR /opt/visits

COPY package.json .
RUN npm install

COPY . .

CMD ["npm", "start"]