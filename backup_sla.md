This document describes a backup Service Level Agreement (SLA).

---------------
Backup coverage

Services that can be restored using manual restoration from backup of ansibe playbooks:
- Web services (Nginx) - covered by ansible repository
- App services (Agama application) - covered by ansible repository
- Database services (InfluxDB, MySQL) - backed up daily 
- DNS services (Bind9) - covered by ansible repository
- Monitoring services - grafana dashboard and exporters are covered by ansible repository
- Ansible repository itself - backed up by github

------------------------------
RPO (recovery point objective)
The backup will restore the database to an identical point no more than one day in the past.

------------------------
Versioning and retention
Local backup is made once a day at 3:30 in the morning. Includes: InfluxDB, MySQL and ansible repository.
Local backups are deleted once a day right before new backup is made. Includes: InfluxDB, MySQL and ansible repository.

Full backup is made every Sunday at 3:30 in the morning. Includes: InfluxDB, MySQL and ansible repository.
Full backups are kept for one month. Includes: InfluxDB, MySQL and ansible repository.

----------------
Usability checks
Backup recovery can be verified by using administration tools on virtual environment comparing database dump to live database. 

--------------------
Restoration criteria
Restoration occurs only at the time when there is an actual problem with the service that could not be reversed. 
These include: files deleted by an accident, damaged files, data loss, security breach (malware, ransomware).

-----------------------------
RTO (recovery time objective)
Since our infrastructure is pretty small - restoring of a backup will take no longer than 2 hours to guarantee minimal process downtimes.