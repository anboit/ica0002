**------ Backup restore instruction ------**

Run Ansible playbook to install all the necessary configurations, run this command from the ica0002 on your machine.<br>
```ansible-playbook```

----------------------------------------

To restore **MySQL** database you will have to run commands on the virtual machine where our MySQL service configuration is made. 

First one restores the backup from the server, run this command as backup user:<br>
```sudo su - backup``` <br>
```duplicity --no-encryption restore rsync://anboit@backup.reily.tech//home/anboit /home/backup/restore```

Second uploads the restore backup onto the machine, run this command from root user:<br>
```cd```<br>
```mysql agama < /home/backup/mysql/agama.sql```

----------------------------------------

To restore **InfluxDB** database you will have to run commands as root on the first virtual machine where our InfluxDB configuration is made.

First one restores the backup from the server, run this command as backup user:<br>
```sudo su - backup```<br>
```duplicity --no-encryption restore rsync://anboit@backup.reily.tech//home/anboit /home/backup/restore```

To restore the backup you will need to delete existing telegraf database first. It also makes sense to stop the Telegraf service so that it doesn't recreate the database before you could restore it, run these commands from root user:<br>
```cd```<br>
```service telegraf stop```<br>
```influx -execute 'DROP DATABASE telegraf'```<br>
```influxd restore -portable -database telegraf /home/backup/influxdb```

----------------------------------------

After you have verified that backup was restored successfully, run this command from the ica0002 on your machine,
it will start the telegraf service again:<br>
```ansible-playbook infra.yaml```
