# Étape de construction de l'application Angular
FROM node:14 AS build

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .
RUN npm run build --prod

# Étape de production avec Nginx
FROM nginx:alpine

COPY ./nginx.conf /etc/nginx/nginx.conf

COPY --from=build /app/dist/bobapp /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]