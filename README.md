# GAP-1
Prometeus Grafana Alerting

apt install docker

mkdir /opt/GAP-1
nano /opt/GAP-1/prometheus.yml 
  


# Create persistent volume for your data
docker volume create prometheus-data
# Start Prometheus container
docker run \
    -p 9090:9090 \
    -v /opt/GAP-1/prometheus.yml:/etc/prometheus/prometheus.yml \
    -v prometheus-data:/prometheus \
    --name prometeus
    prom/prometheus
    




Victoria

docker pull victoriametrics/victoria-metrics:latest
docker volume create victoria-metrics-data
docker run -d -v victoria-metrics-data:/victoria-metrics-data -p 8428:8428 --name victoria-metrics victoriametrics/victoria-metrics:latest 

