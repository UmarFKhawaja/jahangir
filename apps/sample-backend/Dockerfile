FROM docker.io/node:lts-alpine

ENV HOST=0.0.0.0
ENV PORT=80

WORKDIR /app

COPY dist ./lib
COPY package.json .
COPY package-lock.json .

RUN npm clean-install

CMD [ "node", "lib/index.js" ]
