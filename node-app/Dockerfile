# I had to use a newer version than 9.9 because of deprecation warning when downloading git
# Debian Jessie's repositories are outdated and packages very archived and 404 error was happening
FROM node:14-buster

RUN apt-get update && apt-get install -y git

WORKDIR /usr/src
RUN git clone https://github.com/kkenan/basic-microservices.git

WORKDIR /usr/src/basic-microservices/node-app

RUN npm install

EXPOSE 8081

CMD ["node", "index.js"]
