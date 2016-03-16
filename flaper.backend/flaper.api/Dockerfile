FROM node:5.3
#we need npm install here to aws micro instance unable to build some libraries (lwip e.g.)
RUN  apt-get update && apt-get install -y -q --no-install-recommends \
    vim zip curl cron\
     && rm -rf /var/lib/apt/lists/*
#set crontab for current user
COPY  cron.txt  /var/spool/cron/crontabs/root

RUN curl -O https://bootstrap.pypa.io/get-pip.py && /usr/bin/python2.7 get-pip.py
RUN pip install awscli

RUN mkdir /flaper.api && \
    git clone https://github.com/flaper/api.git /flaper.api --depth 1 && echo 1 > /dev/null && \
    cd /flaper.api && npm install && \
    npm install pm2 -g
WORKDIR /flaper.api
#temp.log workaround to run server constantly
#after cp should be ";" as it generate an error when directory not exist
RUN mkdir ~/.aws -p


CMD git pull && \
 cp /config/flaper/api/* . -r 2>/dev/null ; \
 cp /config/flaper/views/aws.config ~/.aws/config -r 2>/dev/null ; \
 npm install  && \
 touch /var/log/temp.log && npm run prestart && pm2 start dist/server/server.js && tail -f /var/log/temp.log
