FROM node:18-bullseye as builder

WORKDIR /bitcore-node-builder

COPY ./package*.json ./
COPY ./tsconfig.json ./
COPY . ./

RUN npm i && npm run compile

FROM node:18-bullseye-slim as runner

WORKDIR /bitcore-node

COPY --from=builder /bitcore-node-builder/build/src/ ./build
COPY --from=builder /bitcore-node-builder/node_modules/ ./node_modules

CMD ["node", "/bitcore-node/build/server.js"]
