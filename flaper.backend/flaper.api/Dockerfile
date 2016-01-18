FROM node:5.3
RUN mkdir /flaper.api && \
 git clone https://github.com/flaper/api.git /flaper.api && \
 cd /flaper.api && npm install && npm install pm2 -g
WORKDIR /flaper.api
#temp.log workaround to run server constantly
CMD touch /var/log/temp.log && npm run prestart && pm2 start dist/server/server.js && tail -f /var/log/temp.log
