FROM elasticsearch:5.0
RUN sed -i '/sysctl -q -w vm.max_map_count/ s/^#*/true\n#/' /etc/init.d/elasticsearch
# CMD sudo sysctl -w vm.max_map_count=262144 && \
# Define default command.
RUN apt-get update && apt-get install -y -q --no-install-recommends \
    python-pip vim curl\
     && rm -rf /var/lib/apt/lists/*
RUN pip install mongo-connector elastic2-doc-manager
COPY index.json  /flaper/index.json
CMD /etc/init.d/elasticsearch start && sleep 20s &&\
  curl -XPUT localhost:9200/flaper -d @/flaper/index.json --header "Content-Type: application/json" && \
  mongo-connector -m mongo:27017 -t localhost:9200 -d elastic2_doc_manager && \
  touch /var/log/temp.log && tail -f /var/log/temp.log

