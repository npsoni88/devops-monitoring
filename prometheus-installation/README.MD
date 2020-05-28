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