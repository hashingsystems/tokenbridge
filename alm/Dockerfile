FROM node:12

WORKDIR /mono
COPY package.json .
COPY contracts/package.json ./contracts/
COPY commons/package.json ./commons/
COPY alm/package.json ./alm/
COPY yarn.lock .
RUN yarn install --production --frozen-lockfile

COPY ./contracts ./contracts
RUN yarn run compile:contracts
RUN mv ./contracts/build ./ && rm -rf ./contracts/* ./contracts/.[!.]* && mv ./build ./contracts/

COPY ./commons ./commons

COPY ./alm ./alm
ARG DOT_ENV_PATH=./alm/.env
COPY ${DOT_ENV_PATH} ./alm/.env

WORKDIR /mono/alm
CMD echo "To start the application run:" \
  "yarn start"
