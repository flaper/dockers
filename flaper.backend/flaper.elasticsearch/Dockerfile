FROM elasticsearch:5.0
RUN apt-get update && apt-get install -y -q --no-install-recommends \
    python-pip vim curl\
     && rm -rf /var/lib/apt/lists/*
RUN pip install mongo-connector elastic2-doc-manager
WORKDIR /flaper/es
COPY index.json  index.json
COPY mongo-connect.config  mongo-connect.config
RUN sed -i '/sysctl -q -w vm.max_map_count/ s/^#*/true\n#/' /etc/init.d/elasticsearch
RUN sed -i 's/MAX_OPEN_FILES=.*/MAX_OPEN_FILES=1000/' /etc/init.d/elasticsearch
RUN sed -i 's/#\?ES_JAVA_OPTS=.*/ES_JAVA_OPTS="-Xms256m -Xmx256m"/' /etc/init.d/elasticsearch
RUN echo "http.host: 0.0.0.0" >> /etc/elasticsearch/elasticsearch.yml
CMD (chown -R elasticsearch:elasticsearch /var/log/elasticsearch /var/lib/elasticsearch ;\
  /etc/init.d/elasticsearch start && sleep 20s &&\
  curl -XPUT localhost:9200/flaper -d @index.json --header "Content-Type: application/json" && \
  mongo-connector -c mongo-connect.config) || \
  touch /var/log/temp.log && tail -f /var/log/temp.log

