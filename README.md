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
    --name prometeus \
    prom/prometheus</code></pre>
    

# Victoria metric

<pre><code>docker volume create victoria-metrics-data</code></pre>
<pre><code>docker run -d \
  -v victoria-metrics-data:/victoria-metrics-data \
  -p 8428:8428 \
  --name victoria-metrics \
  victoriametrics/victoria-metrics:latest </code></pre>

### Удаленная отправка метрик на Victoria
nano /opt/GAP-1/[prometheus.yml](https://github.com/CTPAyCCC/GAP-1/blob/main/prometeus.yml)
<pre><code>remote_write:
  - url: http://192.168.1.101:8428/api/v1/write
    queue_config:
      max_samples_per_send: 10000
      capacity: 20000
      max_shards: 30</code></pre>

<pre><code>docker restart prometheus</code></pre>

# Grafana
<pre><code>docker run -d -p 3000:3000 \
-e GF_INSTALL_PLUGINS=grafana-clock-panel,natel-discrete-panel,grafana-piechart-panel \
--name=grafana \
grafana/grafana-enterprise</code></pre>

# Alertmanager (*--volume поменять на свой путь)
<pre><code>
  docker run \
--detach \
--name=alertmanager \
--volume=/etc/prometheus/rules.yml:/etc/alertmanager/rules.yml \
--publish=9093:9093 \
prom/alertmanager
</code></pre>
