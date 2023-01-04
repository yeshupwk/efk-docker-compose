## Prerequisites 
We need a Kubernetes cluster
docker installation and kuernetes
 docker desktop is installed in my local machine which has docker 20.10.21 and kubernetes 1.25.2 installed in it 

## Fluentd Manifests
Have dowbloaded the fluentd manifests from fluentd github official page and modified accordingly 
cd .\monitoring\logging\fluentd\kubernetes\

Have copied the log file in the fluentd-docker image and Build the image 
docker build . -t yeshupwku/fluentd-demo:1 and pushed the image to dockerhub
docker push yeshupwku/fluentd-demo:1

## Fluentd Namespace

Let's create a `fluentd` namespace: <br/>
kubectl create ns fluentd

## Fluentd Configmap

`fluentd-configmap.yaml` : Have moved all the contents of the log file to the elasticsearch 
kubectl apply -f fluentd-configmap.yaml

## Fluentd Daemonset

Let's deploy our `daemonset`:
kubectl apply -f fluentd-rbac.yaml 
kubectl apply -f fluentd.yaml
kubectl -n fluentd get pods


## Demo ElasticSearch and Kibana

create a new namespace kubectl create ns elastic-kibana and run the below commands

# deploy elastic search
kubectl -n elastic-kibana apply -f elastic\elastic-demo.yaml
kubectl -n elastic-kibana get pods

# deploy kibana
kubectl -n elastic-kibana apply -f elastic\kibana-demo.yaml
kubectl -n elastic-kibana get pods
```
## Kibana
kubectl -n elastic-kibana port-forward svc/kibana 5601
once the above steps are done , you should be able to browse https:localhost:5601 and you should be able to create a index pattern with fluentd* and all logs of cri-o_example.logs are displayed 
and for creating a index pattern you can use (./create-index-kibana.sh) by running sh create-index-kibana.sh from the location.