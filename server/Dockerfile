FROM node:8.16.0-alpine
ENV NODE_ENV=production \
  PORT=3000 \
  DB_CONNECTION_URL=mongodb://localhost/test \
  JWT_SECRET=shared-secret
WORKDIR /app
COPY package.json package.json ./
RUN apk --no-cache --virtual build-dependencies add \
    python \
    make \
    g++ \
    tini \
    && npm install \
    && npm cache clean --force \
    && apk del build-dependencies
RUN apk add --no-cache tini
COPY . .
ENTRYPOINT ["/sbin/tini", "--"]
CMD ["node", "app.js"]
