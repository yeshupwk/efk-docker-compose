# Introduction to Fluentd
1. you need to create a  dockerfile with fluentd ,plugin fluent-plugin-elasticsearch and copy the cri-o_example.log file into the tmp location of the docker image.

FROM fluent/fluentd:v1.11-debian

USER root
RUN gem install elasticsearch -v 7.6
RUN gem install fluent-plugin-elasticsearch
COPY cri-o_example.log/tmp/
 
2. Build the image and push it to dockerhub.

## Collecting logs from files

1. Reading logs from a file cri-o_example.log 

2. In containers-fluent.conf: file 
It reads the contents of the log file cri-o_example.log from starting  using tail plugin and passes it to the  match block in  elastic-fluent.conf file. 
3. On high level ,fluentd passes the log contents to the elasticsearch.

## Displaying the logs in kibana
1. As the docker-compose file is provided with elasticsearch and kibana ,have included fluentd service with all the requirments.

2. once the above steps are done , you should be able to browse http:localhost:5601 and you should be able to create a index pattern with fluentd* and  click on discover in kibana , all logs of cri-o_example.logs are displayed. 

3. For creating a index pattern you can use (./create-index-kibana.sh) by running sh create-index-kibana.sh in gitbash from the file location.

