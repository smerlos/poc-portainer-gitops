FROM node:lts-alpine
RUN apk update && apk add --no-cache tini
RUN mkdir -p /app /app/www && chown node:node /app /app/www
WORKDIR /app
USER node
COPY --chown=node:node package.json package-lock.json ./
RUN npm ci --only=production && npm cache clean --force
COPY --chown=node:node . .
ENV APP_PORT=3003
EXPOSE ${APP_PORT}
ENTRYPOINT ["/sbin/tini", "--"]
CMD ["node", "index.js"]
