# Build phase
FROM node:18-alpine AS build

USER node

RUN mkdir -p /home/node/app
WORKDIR /home/node/app

COPY --chown=node:node package.json .
RUN npm install
COPY --chown=node:node . .

RUN npm run build

# Run phase
FROM nginx
EXPOSE 3000
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
COPY --from=build /home/node/app/build /usr/share/nginx/html