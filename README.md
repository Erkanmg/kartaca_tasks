# kartaca_tasks
Error response from daemon: failed to create shim task: OCI runtime create failed: runc create failed: unable to start container process: error during container init: error mounting "/host_mnt/Users/emg/promgrafnode/prometheus/prometheus.yml" to rootfs at "/etc/prometheus/prometheus.yml": mount /host_mnt/Users/emg/promgrafnode/prometheus/prometheus.yml:/etc/prometheus/prometheus.yml (via /proc/self/fd/14), flags: 0x5000: not a directory: unknown: Are you trying to mount a directory onto a file (or vice-versa)? Check if the specified host path exists and is the expected type

Buna benzer bir hata alırsanız, prometheus.yml klasörünü silip sudo touch prometheus.yml yaptıktan sonra aşağıdaki konfigürasyon kodlarını yapıştırabilirsiniz.


global:
  scrape_interval: 1m

scrape_configs:
  - job_name: "prometheus"
    scrape_interval: 1m
    static_configs:
    - targets: ["localhost:9090"]

  - job_name: "node"
    static_configs:
    - targets: ["node-exporter:9100"]

  - job_name: "cadvisor"
    scrape_interval: 5s
    static_configs:
    - targets: ["10.1.149.19:8081"]

  - job_name: 'traefik'
    metrics_path: /metrics
    static_configs:
    - targets: ['traefik:8080']
