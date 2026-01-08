# Scheduler in Linux:

In linux , a scheduler job is a task(command or script) that you set to run automatically at a specific time or 
interval.

 There are two main tools: 

at- run a job once at a specific time 

cron- run job repeatedly at fixed time or intervals.

1. at commands(one-time scheduling)

used when you want a job to run only once in the future.

SYNTAX:

`at 1030 (type command after prompt)`

`at > mkdir test/tmp/test`

`at > ctrl+d`

This will run at 10:30 today and create directory in /tmp/test

# List Scheduled Jobs:

`at -l`

`atq`

# check job file content:

`at -c "job id"`

# remove a job:

`atrm "job id"`

# at job creation path:

`cd/var/spool/at`

2. Cron Command(Repeated Scheduling)

used for tasks that need to run regularly(daily,weekly,hourly etc)

SYNTAX:

`crontab -e`

This open cron editor add job in this format 

MIN HOUR DAY MONTH DAYOFWEEK COMMAND

#Time field explained:

.1st field MIN - 0-59

.2nd field HOUR - 0-23

.3rd field DAY - 1-31

.4th field MONTH - 1-12

.5th field DAYOFWEEK - 0-6(0-SUNDAY)

.6th field COMMAND 

.7th field output 

EXAMPLES:

1. Run script every day at 5am 

`05 * * * /home/user/backup.sh`

2. Run every monday at 9am

`09 * * * /home/user/report.sh`

3. Run every 10 minutes

`*/10 * * * * /home/user/check.sh`

4. Run every day at midnight and redirect output

`00 * * * echo "daily job run at midnight" >> /tmp/cron.log`

# Command to manage cron:

1) Edit jobs

`crontab -e`

2) List jobs

`crontab -l` 

3) Remove jobs

`crontab -r`

# cron job file path:

`cd /var/spool/cron`

# cron services status for rhel 7/8/9:

.`systemctl crond status`

.`systemctl crond start`

.`systemctl crond stop`

.`systemctl crond restart`

# So in short:

.use at if you want something to run only once in the future 

.use CRON if you want something to run again and again at fixed time.
