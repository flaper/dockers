FROM node:5.3
RUN mkdir /flaper.api && \
 git clone https://github.com/flaper/api.git /flaper.api && \
 cd /flaper.api && npm install
WORKDIR /flaper.api
CMD npm start
