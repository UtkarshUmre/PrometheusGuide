### prometheus server setup

1. create user prometheus

```bash
  sudo useradd --no-create-home --shell /bin/false prometheus
```

2. create a folder promtheus in /etc directory, to store the prometheus.yaml file

```bash
sudo mkdir /etc/prometheus
```

3. create another folder prometheus in /var/lib to store all data, time series database going to reside in this folder

```bash
sudo mkdir /var/lib/prometheus
```

4. update permissions, so that those two folders are owned by the promtheus user and the prometheus group

```bash
sudo chown prometheus:prometheus /etc/prometheus

sudo chown prometheus:prometheus /var/lib/prometheus
```

5. copy prometheus executable to /usr/local/bin/

```bash
sudo cp prometheus /usr/local/bin/
```

6. copy promtool executable to usr/local/bin/

```bash
sudo cp promtool /usr/local/bin/
```

7. update the permissions of both the files so promethes user owns both files

```bash
sudo  chown prometheus:prometheus /usr/local/bin/prometheus

sudo chown prometheus:prometheus /usr/local/bin/promtool
```

8. copy the consoles and console_libraries folder to /etc/prometheus

```bash
sudo cp -r consoles /etc/prometheus

sudo cp -r console_libraries /etc/prometheus
```

9. update permissions

```bash
 sudo chown -R prometheus:prometheus /etc/prometheus/consoles

 sudo chown -R prometheus:prometheus /etc/prometheus/console_libraries
```

10. copy prometheus.yaml file into /etc/prometheus folder

```bash
sudo cp prometheus.yaml /etc/prometheus
```

11. update permissions

```bash
sudo chown prometheus:prometheus /etc/prometheus/prometheus.yaml
```

12. create unit service file for prometheus server service

```bash
sudo nano /etc/systemd/system/prometheus.service
```

13. prometheus.service file

```bash
[Unit]
Description=Prometheus
Wants=network-online.target
After=network-online.target

[Service]
User=prometheus
Group=prometheus
Type=simple
ExecStart=/usr/local/bin/prometheus \
--config.file=/etc/prometheus/prometheus.yml \
--storage.tsdb.path=/var/lib/prometheus/ \
--web.console.templates=/etc/prometheus/consoles \
--web.console.libraries=/etc/prometheus/console_libraries



[Install]
WantedBy=multi-user.target
```

14. reload the systemd manager configuration

```bash
 sudo systemctl daemon-reload
```

15. start the Prometheus service

```bash
sudo systemctl start prometheus
```

16. check the status of the Prometheus service

```bash
sudo systemctl status prometheus
```

17. enable the Prometheus service to start automatically when the system boots up

```bash
sudo systemctl enable prometheus
```
