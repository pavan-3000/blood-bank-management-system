FROM node:18-alpine AS build-stage

WORKDIR /app

COPY package*.json ./
COPY vite.config.js ./
COPY src/ src/
COPY public/ public/
COPY components.json ./
COPY index.html ./
COPY eslint.config.js ./

RUN npm install --production && npm run build

FROM nginx:alpine AS production-stage

COPY --from=build-stage /app/dist /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]