### prometheus yaml

```yaml
# My global config
global:
  scrape_interval: 15s # Set the scrape interval to every 15 seconds. Default is every 1 minute.
  evaluation_interval: 15s # Evaluate rules every 15 seconds. The default is every 1 minute.

# Alertmanager configuration
alerting:
  alertmanagers:
    - static_configs:
        # Uncomment and configure if you are using an Alertmanager
        # - targets: ["alertmanager:9093"]

# Load rules once and periodically evaluate them according to the global 'evaluation_interval'.
rule_files:
  # Uncomment and configure if you are using Prometheus rules
  # - "first_rules.yml"
  # - "second_rules.yml"

# Scrape configuration for scraping Prometheus itself (already configured)
scrape_configs:
  # Scrape job for Prometheus itself
  - job_name: "prometheus"
    static_configs:
      - targets: ["localhost:9090"]

  # Scrape configuration for node_exporter running on two Google Cloud VMs
  - job_name: "node_exporter"
    scrape_interval: 15s # Scrape every 15 seconds from each node_exporter
    static_configs:
      - targets:
          - "YOUR_VM_INSTANCE_IP:9100" # External IP of VM 1
          - "YOUR_VM_INSTANCE_IP:9100" # External IP of VM 2
```

After making changes to the `prometheus.yaml` file, Prometheus does not automatically apply the new configurations. To apply the changes, you need to restart the Prometheus process.

```bash
sudo systemctl restart prometheus
```
