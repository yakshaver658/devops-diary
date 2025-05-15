# Week 2 (May 10 – May 15, 2025)

## What I studied
- Bash scripting: variables, conditionals, loops, functions, arguments  
- Backup scripting with logging  
- Cron jobs for automation  
- rsync for remote file transfers  
- Monitoring tools: htop, iftop, ncdu  
- Linux logging systems (rsyslog, syslog-ng, journald)  
- Prometheus and Node Exporter installation and configuration  

## What I practiced

### Bash Scripting
- Created and executed basic Bash scripts using `#!/bin/bash` and `echo`  
- Used `chmod +x` to make scripts executable  
- Practiced using conditionals (`if`, `else`), `case`, `for`, and `while` loops  
- Created functions and used arguments in scripts  

Example script with conditional:
```bash
if [ "$age" -ge 18 ]; then
    echo "Adult"
else
    echo "Minor"
fi
```

### Backup Automation
- Wrote a script `etcbackup.sh` to copy and archive `/etc` directory  
- Enhanced the script with timestamped archive names using `$(date)`  
- Implemented logging to `/var/log/etcbackup.log`  
- Scheduled daily cron job at 20:30 with `crontab -e`  

Cron job:
```
30 20 * * * /home/server/etcbackupNC.sh
```

### rsync and SSH
- Set up a second Ubuntu VM for testing file transfers  
- Configured bridged networking and SSH access between VMs  
- Used `rsync -avz` to securely transfer archives between machines  

Example:
```bash
rsync -avz ~/testdir.tar.gz server@192.168.178.32:/home/server/
```

### Monitoring Tools
- Installed `htop`, `iftop`, and `ncdu`  
- Practiced viewing system resource usage, disk consumption, and network activity  
  - `htop` — process and CPU monitoring  
  - `iftop` — real-time network traffic  
  - `ncdu` — interactive disk usage analyzer  

### Linux Logging
- Explored `/var/log` directory and common log files  
- Learned about different logging systems:  
  - `rsyslog` — standard syslog daemon  
  - `syslog-ng` — advanced syslog alternative  
  - `journald` — systemd journal daemon  
- Reviewed log levels and formats of log messages  

### Prometheus and Node Exporter
- Installed Prometheus locally from official release  
- Configured `prometheus.yml` to scrape metrics from Node Exporter  
- Created systemd services for both Prometheus and Node Exporter  
- Verified that Prometheus could collect metrics at `http://localhost:9090/metrics`  

Prometheus scrape config example:
```yaml
scrape_configs:
  - job_name: 'node_exporter'
    static_configs:
      - targets: ['localhost:9100']
```

## Problems I solved
- Backup script initially required user input, which blocked cron job — removed prompt for non-interactive use  
- rsync failed due to SSH auth settings — temporarily enabled password login in `sshd_config`  
- Node Exporter didn't start until I correctly created a systemd service and reloaded daemon  
- Prometheus failed to start before adding proper permissions and ensuring `nobody` user could access files  

## Plans for next week
- Learn how to build and run Docker containers  
- Understand basic CI/CD concepts and pipeline structure  

