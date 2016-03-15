FROM node:5.3
#we need npm install here to aws micro instance unable to build some libraries (lwip e.g.)
RUN npm install pm2 -g
#increase number near echo to rebuild
RUN mkdir /flaper.render && \
    git clone https://github.com/flaper/render.git /flaper.render --depth 1 &&  \
    cd /flaper.render && npm install && \
    echo 2 > /dev/null

WORKDIR /flaper.render
#temp.log workaround to run server constantly
#after cp should be ";" as it generate an error when directory not exist
CMD git pull && \
 touch /var/log/temp.log && pm2 start app.js && tail -f /var/log/temp.log
