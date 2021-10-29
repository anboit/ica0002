This document describes a Service Level Agreement (SLA).

Backup coverage

Database servers, InfluxDB, Ansible repository - backed up
Nginx, AGAMA, Grafana, Bind - not backed up
r 

RPO (recovery point objective)
One day - 

Versioning and retention -- how many backup versions are stored and for how long
In our infrastructure incremental way of backup will be used as a daily backup version. An incremental backup is one in which successive copies of the data contain only the portion that has changed since the preceding backup copy was made. Differential backup will be used once in a week

Usability checks -- how is backup usability verified


Restoration criteria -- when should backup be restored
Restoration occurs only at the time when there is an actual problem with the service that could not be reversed. 
These include: files deleted by an accident, damaged files.

RTO (recovery time objective)
Service restoration time is one hour