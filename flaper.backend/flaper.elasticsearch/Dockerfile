FROM elasticsearch:5.0
RUN sed -i '/sysctl -q -w vm.max_map_count/ s/^#*/true\n#/' /etc/init.d/elasticsearch
# CMD sudo sysctl -w vm.max_map_count=262144 && \
# Define default command.
RUN apt-get update && apt-get install -y -q --no-install-recommends \
    python-pip vim curl\
     && rm -rf /var/lib/apt/lists/*
RUN pip install mongo-connector elastic2-doc-manager
WORKDIR /flaper/es
COPY index.json  index.json
COPY mongo-connect.config  mongo-connect.config
CMD /etc/init.d/elasticsearch start && sleep 20s &&\
  curl -XPUT localhost:9200/flaper -d @index.json --header "Content-Type: application/json" && \
  mongo-connector -c mongo-connect.config && \
  touch /var/log/temp.log && tail -f /var/log/temp.log

