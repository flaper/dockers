FROM nginx
# Replace shell with bash so we can source files
RUN rm /bin/sh && ln -s /bin/bash /bin/sh
# Set debconf to run non-interactively
RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections


RUN  apt-get update && apt-get install -y -q --no-install-recommends \
    git curl npm vim make g++ bzip2 \
     && rm -rf /var/lib/apt/lists/*
ENV NODE_VERSION 5.0.0
ENV NVM_DIR /usr/local/nvm
RUN curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.30.2/install.sh | bash \
    && source $NVM_DIR/nvm.sh \
    && nvm install $NODE_VERSION \
    && nvm alias default $NODE_VERSION \
    && nvm use default
ENV NODE_DIR $NVM_DIR/versions/node/v$NODE_VERSION
ENV NODE_PATH $NODE_DIR/lib/node_modules
ENV PATH      $NODE_DIR/bin:$PATH
COPY default.conf /etc/nginx/conf.d/default.conf

#echo just to update git cache at docker
RUN    rm /usr/share/nginx/html* -r && echo 2 > /dev/null && \
    git clone https://github.com/flaper/web.git --depth 1 /usr/share/nginx/html

#after npm should be ";" as it generate an error when directory not exist
RUN cd /usr/share/nginx/html && npm install ; \
    npm install bower typings -g && bower install --allow-root

WORKDIR /usr/share/nginx/html
COPY config.local.json  /usr/share/nginx/html/src/app/config/config.local.json

#temp.log workaround to run server constantly
#after cp should be ";" as it generate an error when directory not exist
RUN git pull && npm install && npm rebuild && bower install --allow-root && typings install && \
   npm run build:prod
CMD touch /var/log/temp.log && nginx && tail -f /var/log/temp.log
