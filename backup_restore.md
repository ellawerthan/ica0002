Web servers
---
App servers
---
    sudo su - backup duplicity --no-encryption restore rsync://ellawerthan@backup.hitec.io//home/ellawerthan/ /home/backup/restore/
    service agama stop
    rm -rf /opt/lib/agama/*
    cp -a /home/backup/restore/agama/* /opt/lib/agama/
    service agama start
Database servers
---
DNS servers
---
Monitoring servers 
(Prometheus, Grafana, Telegraf, InfluxDB)
---
Ansible repository
---
Duplicity
---