------ This document describes a backup Service Level Agreement (SLA) ------

Backup coverage

Services that can be restored using manual restoration from backup of ansibe playbooks:
- Web services (Nginx) - covered by ansible repository
- App services (Agama application) - covered by ansible repository
- Database services (InfluxDB, MySQL) - backed up daily 
- DNS services (Bind9) - covered by ansible repository
- Monitoring services - grafana dashboard and exporters are covered by ansible repository
- Ansible repository itself - backed up by github

------------------------------

RPO (recovery point objective)<br>
The backup will restore the database to an identical point no more than one day in the past.

------------------------

Versioning and retention<br>
Local backup is made once a day at 03:00 in the morning. Includes: InfluxDB, MySQL.
Local backups are deleted once a day right before new backup is made.

Full backup is made every Sunday at 03:30 in the morning. Includes: InfluxDB, MySQL.
Full backups are kept for one month.

Incremental backup is made at 03:30 on every day-of-week from Monday through Saturday. Includes: InfluxDB, MySQL.
Incremental backups are kept for one week.

----------------

Usability checks<br>
Backup recovery can be verified by using administration tools on virtual environment comparing database dump to live database. 

--------------------

Restoration criteria<br>
Restoration occurs only at the time when there is an actual problem with the service that could not be reversed. 
These include: files deleted by an accident, damaged files, data loss, security breach (malware, ransomware).

-----------------------------

RTO (recovery time objective)<br>
Since our infrastructure is pretty small - restoring of a backup will take no longer than 2 hours to guarantee minimal process downtimes.
