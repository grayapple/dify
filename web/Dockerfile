FROM node:18.17.0-alpine

LABEL maintainer="takatost@gmail.com"

ENV NODE_ENV=production
ENV EDITION SELF_HOSTED
ENV DEPLOY_ENV PRODUCTION
ENV CONSOLE_API_URL http://127.0.0.1:5001
ENV APP_API_URL http://127.0.0.1:5001

EXPOSE 3000

WORKDIR /app/web

COPY package.json /app/web/package.json

RUN npm install pm2 -g

RUN npm install --only=prod

COPY . /app/web/

RUN npm run build

COPY docker/pm2.json /app/web/pm2.json
COPY docker/entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

ARG COMMIT_SHA
ENV COMMIT_SHA ${COMMIT_SHA}

ENTRYPOINT ["/bin/sh", "/entrypoint.sh"]
