FROM node:5.3
#we need npm install here to aws micro instance unable to build some libraries (lwip e.g.)
RUN mkdir /flaper.api && \
    git clone https://github.com/flaper/api.git /flaper.api --depth 1 && echo 1 > /dev/null && \
    cd /flaper.api && npm install && \
    npm install pm2 -g
WORKDIR /flaper.api
#temp.log workaround to run server constantly
#after cp should be ";" as it generate an error when directory not exist
CMD git pull && \
 cp /config/flaper/api/* . -r 2>/dev/null ; \
 npm install  && \
 touch /var/log/temp.log && npm run prestart && pm2 start dist/server/server.js && tail -f /var/log/temp.log
