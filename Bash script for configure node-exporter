#!/bin/bash -xe

# Create node_exporter user
useradd --no-create-home --shell /bin/false node_exporter

# Install wget if missing
yum install -y wget || apt-get update && apt-get install -y wget

# Go to tmp
cd /tmp/

# Download Node Exporter
wget https://github.com/prometheus/node_exporter/releases/download/v1.3.1/node_exporter-1.3.1.linux-amd64.tar.gz

# Extract
tar -xvf node_exporter-1.3.1.linux-amd64.tar.gz

cd node_exporter-1.3.1.linux-amd64

# Move binary
mv node_exporter /usr/local/bin/

# Set ownership
chown node_exporter:node_exporter /usr/local/bin/node_exporter

# Create systemd service
cat <<EOF > /etc/systemd/system/node_exporter.service
[Unit]
Description=Node Exporter
After=network.target

[Service]
User=node_exporter
Group=node_exporter
Type=simple
ExecStart=/usr/local/bin/node_exporter

[Install]
WantedBy=multi-user.target
EOF

# Reload systemd and start service
systemctl daemon-reload
systemctl enable node_exporter
systemctl start node_exporter

echo "Node Exporter installed and running"
