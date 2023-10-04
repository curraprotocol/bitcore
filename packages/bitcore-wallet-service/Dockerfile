FROM node:18-bullseye as builder

WORKDIR /bws

COPY ./package*.json ./
COPY ./tsconfig.json ./

COPY . ./

RUN npm i && npm run tsc

FROM node:18-bullseye-slim as runner

WORKDIR /bws

RUN npm install pm2 -g
COPY --from=builder /bws/ts_build/ ./
COPY --from=builder /bws/node_modules/ ./node_modules
COPY ./templates/ ./templates

CMD ["pm2-runtime", "./app.js", "--name", "bitcoin-wallet-service"]
