# Example - Steps

Deploy Elasticsearch & Kibana (namespace: elasticsearch)

Deploy Fluentd (namespace: fluentd) - Event Log

Deploy APM (namespace: elasticsearch) - Distributed Tracing

Deploy Prometheus & Grafana - Metrics

Deploy App components - DB, API Service & Frontend

# Pre-requisites:

## Kubernetes cluster
Please refer vagrant setup inside vagrant folder

## Helm on Master node
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh

## Storage Class
Run `kubectl apply -f sc-default.yaml`

## Persistent Volumes
`mkdir -p /data/elasticsearch` directory on all the worker nodes and run `sudo chmod 777 -R /data/elasticsearch`
`mkdir -p /data/prometheus-server` directory on all the worker nodes and run `sudo chmod 777 -R /data/prometheus-server`
`mkdir -p /data/prometheus-alert-manager` directory on all the worker nodes and run `sudo chmod 777 -R /data/prometheus-alert-manager`

Run `kubectl apply -f pv-hostpath.yaml`

## Namespaces
kubectl create namespace elasticsearch
kubectl create namespace fluentd
kubectl create namespace monitoring
kubectl create namespace weather

# References
## Microservices
### Frontend
https://github.com/brainupgrade-in/weather/tree/metrics
### REST Service
https://github.com/brainupgrade-in/weather-service