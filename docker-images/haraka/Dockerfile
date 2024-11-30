# Builder
FROM node:lts-alpine AS builder

ARG version=3.0.5
ARG haraka_plugin_version=5.8.15

# Instalar dependencias necesarias
RUN apk update && apk add --no-cache git python3 make g++
RUN apk add npm

# Directorio de trabajo
WORKDIR /app

# Clonar el repositorio con la versión específica
RUN echo "Cloning Haraka version: ${version}" && \
    git clone https://github.com/haraka/Haraka.git ./ --branch v"${version}" --depth 1

# Instalar dependencias del proyecto
RUN npm install && npm ci --omit=dev
RUN npm install haraka-plugin-wildduck@${haraka_plugin_version}

# App
FROM node:lts-alpine AS app

# Definir variable de entorno
ENV NODE_ENV=production

# Instalar tini
RUN apk add --no-cache tini

# Configurar directorio de trabajo
WORKDIR /app

# Copiar la app desde el builder
COPY --from=builder /app /app

# Configurar entrada
ENTRYPOINT ["/sbin/tini", "--", "node", "haraka.js"]
