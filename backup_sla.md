# Backup services SLA

## Introduction

### Definition of SLA

This Service Level Agreement (this “SLA”) governs the backup Services. Operations and security teams may update, amend, modify or supplement this SLA from time to time. The terms and conditions of this SLA are applicable to the Managed Backup and Disaster Recovery Services only.  

### Structure of SLA

This SLA describes the backup approach for all services in the infrastructure:  

- Application services - **Nginx,Agama,MySQL**
- Internal services - **InfluxDB,Prometheus,Grafana,Telegraf**
- Other services - **Bind9**
- Infra as a Code - **Ansible** <https://github.com/ellawerthan/ica0002>

Descriptions of backup approaches contain information on specific backup attributes, such as:

- Backup coverage - what is backed up and what is not
- Backup RPO (recovery point objective) - acceptable data loss (time period)
- Versioning and retention - how many backup versions are stored and for how long
- Usability - how is the backup recovery verified (backup should be usable)
- Restoration criteria - when should backup be restored
- Backup RTO (recovery time objective) - how long will it take to restore the service

## Backup coverage

Backup service covers only the next services:

- User-driven database services - **MySQL**

**Explanation:**  
> Every service that contains users-inputed data (MySQL) will be stored fully. Some of logging information can be less prioritized as it will not ruin services running in case of disaster.

Other services do not include user provided information, thus it is decided that it will not in need of backup as all can be recovered by Ansible playbook. As all services are run by Ansible, Ansible repository itself will be stored in GitHub. 
https://github.com/ellawerthan/ica0002

## Backup RPO

Recovery point objective for:

|Service|RPO|
|---|---|
|MySQL|7 days|

**Time:** backups should be done automatically with full backup on Sundays and incremental backup on other days.

**Explanation:**  
For space-saving, full backups are done on Sundays. Other days will conduct incremental backups.

## Versioning and retention

All services will be stored for maximum 30 days with 4 full versions.

**Explanation:**  
all services must be restored before 30 days. And 4 Sundays with 4 full backups should pass in the past 30 days, thus 4 versions in total.

## Usability

All services will be checked every week on Wednesday, only in development environment.

**Explanation:**  
Things must be done with attention, thus all usability tests will be conducted in development environment to avoid any mistakes.

## Restoration criteria
- Backup restoration of the **MySQL** data should be done only if it was detected and confirmed that the stored data was corrupted, modified by the unauthorized 1st/3rd party, stolen or deleted.

**Explanation:**  
Backup restoration takes time and computing resources, there is no reason to use it, if the data it covers, was not corrupted.

## Backup RTO
- Backup service is expected to take maximum of **12 hours** to fully recover all the data.
- If the whole infrastructures should be restored, excepted maximum required time equals **24 hours**.

**Explanation:**  
There is only one backed-up data table, so it should not take too long to restore.