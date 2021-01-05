## APPLICATION SERVICES
### AGAMA
run on own device in EXAM directory

ansible-playbook infra.yaml -tagama

### MySQL Service
run on own device in EXAM directory

ansible-playbook infra.yaml -tmysql

Run the following queries on ellawerthan-2 mysql to finish setup:
 - STOP SLAVE;
 - CHANGE MASTER TO MASTER_HOST='ellawerthan-1.hitec.io',MASTER_USER='replication',MASTER_PASSWORD='my password (can print in debug if necessary)'
 - RESET SLAVE;
 - START SLAVE;
 - SHOW SLAVE STATUS\G

### MySQL Database restore
run on an application machine as backup

duplicity --no-encryption restore rsync://ellawerthan@backup.hitec.io//home/ellawerthan/ /home/backup/restore/

mysql agama < /home/backup/restore/agama.sql

### Nginx
run on own device in EXAM directory

ansible-playbook infra.yaml -tnginx

## INTERNAL SERVICES
### Prometheus
run on own device in EXAM directory

ansible-playbook infra.yaml -tprometheus

### Grafana
run on own device in EXAM directory

ansible-playbook infra.yaml -tgrafana

initial user/pass is admin/admin
dashboard json is available in EXAM directory for import
prometheus database is at http://prometheus.hitec.io:9090/prometheus
influx databases are at http://influxdb.hitec.io:8086

### Telegraf/Rsyslog/pinger/InfluxDB
run on own device in EXAM directory

ansible-playbook infra.yaml -tinflux

## BACKUP SERVICES

### Duplicity
run on own device in EXAM directory

ansible-playbook infra.yaml -tbackup

(could take some time to gain access to backup server)

### Cron
run on own device in EXAM directory

ansible-playbook infra.yaml -tbackup

### Bind9
run on own device in EXAM directory

ansible-playbook infra.yaml -tbind
