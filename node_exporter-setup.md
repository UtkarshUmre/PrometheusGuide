### node_exporter setup

1. copy node_exporter executable to /usr/local/bin

```bash
 sudo cp node_exporter /usr/local/bin
```

2. create user node_exporter

```bash
sudo useradd --no-create-home --shell /bin/false node_exporter
```

3. change permission of node_exporter executable, so that node_exporter user owns it

```bash
sudo chown node_exporter:node_exporter /usr/local/bin/node_exporter
```

4. create node_exporter service

```bash
 sudo nano /etc/systemd/system/node_exporter.service
```

5.  node_exporter.service file

```bash
[Unit]
Description=Node Exporter
Wants=network-online.target
After=network.target

[Service]
User=node_exporter
Group=node_exporter
Type=simple
ExecStart=/usr/local/bin/node_exporter


[Install]
WantedBy=multi-user.target
```

6. reload the systemd manager configuration

```bash
 sudo systemctl daemon-reload
```

7. start the node_exporter service

```bash
sudo systemctl start node_exporter
```

8. check the status of the node_exporter service

```bash
sudo systemctl status node_exporter
```

9. enable the node_exporter service to start automatically when the system boots up

```bash
sudo systemctl enable node_exporter
```
