# Labsession

Stappenplan
1. Setup databases
2. Setup carbon-relay
3. Setup telegraf
4. Setup Grafana


## Setup database

```
sudo yum install influxdb
cd /etc/influxdb
```

Voeg onder aan de file het grahite blok toe
```
[[graphite]]
  # Telegraf metrics
  enabled = true
  database = "telegraf"
  bind-address = ":**2003**"
  protocol = "tcp"
  consistency-level = "one"
  separator = "."
  ignore-unnamed = true
  templates = [
      "telegraf.disk.* .measurement.host.device.fstype.mode.mount.field",
      "telegraf.procstat.* .measurement.host.process.exe.user.field",
      "telegraf.* .measurement.host.tags.field"
  ]
  ```
  
Start de database

```
systemctl start influxdb
systemctl enable influxdb
```

