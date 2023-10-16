# GAP-1
## Prometeus Grafana Alerting

apt install docker.io

mkdir /opt/GAP-1

nano /opt/GAP-1/[prometheus.yml](https://github.com/CTPAyCCC/GAP-1/blob/main/prometeus.yml)
  


# Create persistent volume for your data
<pre><code>docker volume create prometheus-data</code></pre>
# Start Prometheus container
<pre><code>docker run -d\
    -p 9090:9090 \
    -v /opt/GAP-1/prometheus.yml:/etc/prometheus/prometheus.yml \
    -v prometheus-data:/prometheus \
    --name prometeus
    prom/prometheus</code></pre>
    

# Victoria metric

<pre><code>docker volume create victoria-metrics-data</code></pre>
<pre><code>docker run -d \
  -v victoria-metrics-data:/victoria-metrics-data \
  -p 8428:8428 \
  --name victoria-metrics \
  victoriametrics/victoria-metrics:latest </code></pre>

