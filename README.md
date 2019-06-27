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

* Voeg onder aan de file het graphite blok toe
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
sudo systemctl start influxdb
sudo systemctl enable influxdb
```

* Maak de database

```
$ influx
InfluxDB shell version: 1.7.6
Enter an InfluxQL query
> show databases
name: databases
name
----
> create database telegraf
> show databases
name: databases
name
----
_internal
telegraf
>
```

* Controleer of de poort naar de graphite interface open staat.


## Setup carbon-relay

Betrokken server: relay
```
# cd /opt
# mkdir relay && cd $_
# mkdir -p etc sbin var/run log
# cd sbin
# wget https://github.com/theo-bot/Labsession/raw/master/carbon-relay-ng
# cd ../etc
# wget https://raw.githubusercontent.com/theo-bot/Labsession/master/carbon-relay.ini
# useradd -s /bin/false carbon
# cd ../../
# chown -R carbon:carbon carbon
# chmod 750 /opt/carbon/sbin/carbon-relay-ng
# cd /etc/systemd/system
# wget https://raw.githubusercontent.com/theo-bot/Labsession/master/carbon.service
# cd /etc/xinetd.d

Enable de discard service tcp/9
# vi discard-stream
# systemctl start xinetd

# Start carbon relay
# systemctl start carbon
# systemctl enable carbon
```

## Setup telegraf

Betrokken servers: alle
```
# yum install telegraf
# vi /etc/telegraf/telegraf.conf
```

Configureer de graphite output zodat deze wijst naar de carbon relay
Configureer het blok:
- [[outputs.graphite]]

## Setup Grafana
Betrokken server: gui

```
# yum install grafana
```
Open de url: http:192.168.1.30:3000

Login met admin/admin

Voeg een influxdb datasource toe met url : http://db1:8086
Maak een dasboard aan voor cpu usage system/user en iowait

