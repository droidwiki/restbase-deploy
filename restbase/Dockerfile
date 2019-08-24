FROM node:alpine AS build

WORKDIR /restbase
RUN apk --no-cache add git python make g++
RUN git clone https://github.com/wikimedia/restbase.git .

RUN npm install

# https://phabricator.wikimedia.org/T231135
COPY ./patched_router.js /restbase/node_modules/hyperswitch/lib/router.js

FROM node:alpine

COPY --from=build /restbase /restbase

WORKDIR /restbase
ENV APP_BASE_PATH "/restbase"
EXPOSE 7231

CMD ["node", "/restbase/server.js"]
