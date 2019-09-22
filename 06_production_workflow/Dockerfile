FROM node:alpine as builder
WORKDIR '/opt/frontend'
COPY package.json .
RUN npm install
COPY . .
RUN npm run build

FROM nginx
COPY --from=builder /opt/frontend/build /usr/share/nginx/html