# Labsession

Stappenplan
1. Setup databases
2. Setup carbon-relay
3. Setup telegraf
4. Setup Grafana


## Setup database

Betrokken servers: db1 en db2

```
sudo yum install influxdb
cd /etc/influxdb
```

* Voeg onder aan de file het grahite blok toe
```
[[graphite]]
  # Telegraf metrics
  enabled = true
  database = "telegraf"
  bind-address = ":2003"
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
  
* Start de database

```
systemctl start influxdb
systemctl enable influxdb
```
* Controleer of de poort naar de graphite interface open staat.


## Setup carbon-relay

Betrokken server: relay
```
# cd /opt
# mkdir relay && cd $_
# wget https://github.com/theo-bot/Labsession/raw/master/carbon-relay-ng
# wget ...
# useradd -s /bin/false carbon
# cd /etc/systemd/system
# wget ...
# systemctl start carbon
# systemctl enable carbon



