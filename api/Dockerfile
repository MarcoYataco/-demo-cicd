# Etapa 1: instalar dependencias de produccion.
FROM node:22-alpine AS builder

WORKDIR /app
COPY package*.json ./
RUN npm ci --omit=dev

# Etapa 2: imagen final sin npm.
FROM node:22-alpine

ENV NODE_ENV=production
WORKDIR /app

USER root
RUN rm -rf /usr/local/lib/node_modules/npm \
    /usr/local/bin/npm \
    /usr/local/bin/npx

COPY --from=builder /app/node_modules ./node_modules
COPY app.js server.js ./

USER 1000
EXPOSE 3000

HEALTHCHECK --interval=10s --timeout=3s --start-period=5s --retries=3 \
  CMD ["wget", "-qO-", "http://127.0.0.1:3000/api/health"]

CMD ["node", "server.js"]
