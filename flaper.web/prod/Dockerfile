FROM nginx
# Replace shell with bash so we can source files
RUN rm /bin/sh && ln -s /bin/bash /bin/sh
# Set debconf to run non-interactively
RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections
# allow aliases

RUN  apt-get update && apt-get install -y -q --no-install-recommends \
    vim python2.7 curl unzip \
     && rm -rf /var/lib/apt/lists/*

WORKDIR /usr/share/nginx/html
RUN curl -O https://bootstrap.pypa.io/get-pip.py && /usr/bin/python2.7 get-pip.py
RUN pip install awscli
COPY default.conf /etc/nginx/conf.d/default.conf

RUN echo "shopt -s expand_aliases" >> ~/.bashrc
RUN echo "alias s3update=\"aws s3 cp s3://flaper . --region eu-central-1 --recursive --no-sign-request && unzip -o dist.zip\"" >> ~/.bashrc
COPY update.sh /root/update.sh
RUN chmod +x ~/update.sh
RUN ~/update.sh

CMD ~/update.sh && touch /var/log/temp.log && nginx && tail -f /var/log/temp.log
