# Prometheus installation and configuration

```
useradd --no-create-home --shell /bin/false  prometheus
mkdir /etc/prometheus
mkdir /var/lib/prometheus
chown prometheus:prometheus /var/lib/prometheus/
cd /tmp
wget https://github.com/prometheus/prometheus/releases/download/v2.18.1/prometheus-2.18.1.linux-amd64.tar.gz
tar -xzf prometheus-2.18.1.linux-amd64.tar.gz
cd prometheus-2.18.1.linux-amd64/
mv console* /etc/prometheus/
mv prometheus.yml /etc/prometheus/
chown -R prometheus:prometheus /etc/prometheus/
mv prometheus /usr/local/bin/
mv promtool /usr/local/bin/
chown prometheus:prometheus /usr/local/bin/prom*

vim /etc/systemd/system/prometheus.servicee
find the file in the same repository and copy paste the content

systemctl daemon-reload
systemctl start prometheus
systemctl enable prometheus
systemctl status prometheus
```

## Install alert manager
```
useradd --no-create-home --shell /bin/false alertmanager
mkdir /etc/alertmanager
cd /tmp
wget https://github.com/prometheus/alertmanager/releases/download/v0.20.0/alertmanager-0.20.0.linux-amd64.tar.gz
tar -xzf tar -xzf alertmanager-0.20.0.linux-amd64.tar.gz
cd alertmanager-0.20.0.linux-amd64/
mv alertmanager /usr/local/bin/
mv amtool /usr/local/bin/
chown alertmanager:alertmanager /usr/local/bin/alertmanager
chown alertmanager:alertmanager /usr/local/bin/amtool
mv alertmanager.yml /etc/alertmanager/
chown -R alertmanager:alertmanager /etc/alertmanager/
cd /etc/systemd/system/
vim alertmanager.service
find the file in the same repository and copy paste the content
systemctl daemon-reload


### Update prometheus with the new alert manager's configuration

vim /etc/prometheus/prometheus.yml

It should look like this
alerting:
  alertmanagers:
  - static_configs:
    - targets:
      - localhost:9093

systemctl restart prometheus
systemctl start alertmanager
systemctl enable alertmanager

```

## Install node-exporter

```
useradd --no-create-home --shell /bin/false node_exporter
```