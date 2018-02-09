# Prometheus Setup with Node-Exporter

    * Systems monitoring and alerting toolkit
    * Node-Exporter - Exporter for machine metrics


# Steps to Configure Prometheus

    * sudo apt-get install nginx - Install Nginx

    * sudo useradd --no-create-home --shell /bin/false prometheus
    * sudo useradd --no-create-home --shell /bin/false node_exporter

    * sudo mkdir /etc/prometheus
    * sudo mkdir /var/lib/prometheus

    * sudo chown prometheus:prometheus /etc/prometheus
    * sudo chown prometheus:prometheus /var/lib/prometheus

    * curl -LO https://github.com/prometheus/prometheus/releases/download/v2.1.0/prometheus-2.1.0.linux-amd64.tar.gz
    * tar xvf prometheus-2.1.0.linux-amd64.tar.gz 

    * sudo cp prometheus-2.1.0.linux-amd64/prometheus /usr/local/bin/
    * sudo cp prometheus-2.1.0.linux-amd64/promtool /usr/local/bin/

    * sudo chown prometheus:prometheus /usr/local/bin/prometheus
    * sudo chown prometheus:prometheus /usr/local/bin/prometool

    * sudo cp -r prometheus-2.1.0.linux-amd64/consoles /etc/prometheus/
    * sudo cp -r prometheus-2.1.0.linux-amd64/console_libraries/ /etc/prometheus/

    * sudo chown -R prometheus:prometheus /etc/prometheus/consoles
    * sudo chown -R prometheus:prometheus /etc/prometheus/console_libraries/
    
    * sudo vi /etc/prometheus/prometheus.yml
    * sudo chown prometheus:prometheus /etc/prometheus/prometheus.yml

    *   sudo -u prometheus /usr/local/bin/prometheus \
        --config.file /etc/prometheus/prometheus.yaml \
        --storage.tsdb.path /var/lib/prometheus/ \
        --web.console.templates=/etc/prometheus/consoles \
        --web.console.libraries=/etc/prometheus/console_libraries

    * sudo vi /etc/systemd/system/prometheus.service
    * sudo systemctl daemon-reload
    * sudo systemctl start prometheus
    * sudo systemctl status prometheus
    * sudo systemctl enable prometheus

# Setup Node Exporter

    * curl -LO https://github.com/prometheus/node_exporter/releases/download/v0.15.2/node_exporter-0.15.2.linux-amd64.tar.gz

    * tar xvf node_exporter-0.15.2.linux-amd64.tar.gz
    * sudo cp node_exporter-0.15.2.linux-amd64/node_exporter /usr/local/bin/
    * sudo chown node_exporter:node_exporter /usr/local/bin/node_exporter

    * sudo vi /etc/systemd/system/node_exporter.service

    * sudo systemctl daemon-reload
    * sudo systemctl start node_exporter
    * sudo systemctl enable node_exporter

# Setup Grafana

    * curl -LO https://s3-us-west-2.amazonaws.com/grafana-releases/release/grafana_4.6.3_amd64.deb
    
    * sudo apt-get install -y adduser libfontconfig
    * sudo dpkg -i grafana_4.6.3_amd64.deb
    * sudo systemctl start grafana-server