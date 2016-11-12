FROM mongo:3.2
RUN apt-get update && apt-get install -y -q --no-install-recommends \
   vim\
     && rm -rf /var/lib/apt/lists/*
WORKDIR /flaper/mongo
COPY mongod.conf /opt/mongod.conf
CMD mongod --config /opt/mongod.conf &\
# /etc/hosts should be in CMD as aws can override it during deploy
  echo "127.0.0.1 mongo" >> /etc/hosts &\
  sleep 20s; \
  mongo --eval 'printjson(rs.initiate({_id: "rs0", members: [{_id: 0, host: "mongo:27017"}]}))' --quiet &&\
  touch /var/log/temp.log && tail -f /var/log/temp.log

