# GAP-1
Prometeus Grafana Alerting

apt install docker

mkdir /opt/GAP-1
nano /opt/GAP-1/prometheus.yml 
  

docker run -d -p 9090:9090 -v /opt/GAP-1/prometheus.yml:/etc/prometheus/prometheus.yml \
        -v /opt/GAP-1/alert.rules:/etc/prometheus/alert.rules \
        sredna/prometheus



Victoria

docker pull victoriametrics/victoria-metrics:latest
docker run -it --rm -v `pwd`/victoria-metrics-data:/victoria-metrics-data -p 8428:8428 victoriametrics/victoria-metrics:latest

