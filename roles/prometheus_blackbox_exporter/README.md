# prometheus_blackbox_exporter

Installs and configures the [Prometheus Blackbox Exporter](https://github.com/prometheus/blackbox_exporter) as a systemd service.

## Variables

| Variable | Default  | Description |
|---|----------|---|
| `blackbox_exporter_version` | `0.28.0` | Version to install |

## Modules

The default config (`/etc/blackbox_exporter/blackbox.yml`) provides a `tls_connect` module for TLS certificate checks via TCP probe on port 443.

The exporter listens on port `9115`.

## Example scrape config for Prometheus

```yaml
- job_name: 'tls_check'
  metrics_path: /probe
  params:
    module: [tls_connect]
  static_configs:
    - targets:
        - example.com:443
  relabel_configs:
    - source_labels: [__address__]
      target_label: __param_target
    - target_label: __address__
      replacement: localhost:9115
```
