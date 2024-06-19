ARG IMAGE_VERSION_BUILD=latest
ARG IMAGE_VERSION=18.14.2-bullseye-slim
ARG NODE_ENV=development

FROM node:${IMAGE_VERSION_BUILD} AS build
RUN apt-get update && apt-get install -y --no-install-recommends dumb-init

FROM node:${IMAGE_VERSION}
ENV NODE_ENV ${NODE_ENV}
COPY --from=build /usr/bin/dumb-init /usr/bin/dumb-init
RUN mkdir /usr/src/app
COPY ./app /usr/src/app
RUN chown node:node /usr/src/app && cd /usr/src/app && npm install
WORKDIR /usr/src/app
USER node
CMD ["dumb-init", "npm", "run", "start"]