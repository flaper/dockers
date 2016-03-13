FROM node:5.3
#we need npm install here to aws micro instance unable to build some libraries (lwip e.g.)
RUN npm install sails -g
RUN mkdir /flaper.render && \
    git clone https://github.com/flaper/render.git /flaper.render && \
    cd /flaper.render && npm install
WORKDIR /flaper.render
#temp.log workaround to run server constantly
#after cp should be ";" as it generate an error when directory not exist
CMD git pull && \
 cp /config/flaper/api/* . -r 2>/dev/null ; \
 npm install  && \
 touch /var/log/temp.log && sails lift && tail -f /var/log/temp.log
