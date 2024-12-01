FROM node:lts-alpine AS builder

ARG version=3.10.0
ARG plugin_version=1.3.15

RUN apk update && apk add --no-cache git python make g++

WORKDIR /app

RUN git clone https://github.com/zone-eu/zone-mta-template ./

RUN npm install zone-mta@${version}
RUN npm install && npm ci --omit=dev
RUN npm install zonemta-wildduck@${plugin_version}

FROM node:lts-alpine AS app

ENV NODE_ENV=production

RUN apk add --no-cache tini

WORKDIR /app
COPY --from=builder /app /app

ENTRYPOINT ["/sbin/tini", "--", "node", "index.js"]
CMD ["--config=config/zonemta.toml"]
