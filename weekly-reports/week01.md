# Week 1 (May 2 – May 9, 2025)

## What I studied

- Basic virtualization with VirtualBox
- Ubuntu Server installation and initial configuration
- SSH setup and key-based authentication
- User and permission management
- Localization, hostname, and timezone setup
- Service management with systemd and journalctl
- Basic firewall configuration with UFW
- Brute-force protection using fail2ban
- Disk mounting and `/etc/fstab` configuration
- Network tools: `ip`, `ping`, `ss`, `nmtui`

## What I practiced

### Server Setup and SSH
- Installed Ubuntu Server in VirtualBox
- Enabled and started `ssh` service using `systemctl`
- Set up port forwarding and connected via SSH from PowerShell
- Generated SSH key on host, copied to guest, and configured `authorized_keys`
- Disabled password login and root SSH access for better security

### User and System Configuration
- Created a new user with `adduser` and granted sudo rights
- Configured locale with `dpkg-reconfigure locales`
- Set hostname using `hostnamectl`
- Set timezone with `timedatectl set-timezone Europe/Moscow`

### Services and Logs
- Practiced starting and stopping services with `systemctl`
- Enabled auto-start for necessary services
- Used `journalctl` to view logs and debug service issues

### Firewall and Security
- Installed and enabled `ufw`
- Allowed essential ports: SSH (22), HTTP (80), HTTPS (443)
- Installed `fail2ban`, copied default config to `jail.local`
- Enabled `[sshd]` jail and configured `maxretry`
- Restarted `fail2ban` and verified it's working with `fail2ban-client status`

### Disk Management
- Installed VirtualBox Extension Pack to detect USB devices
- Identified USB drive with `lsblk`
- Mounted USB manually to `/mnt/usb`
- Found UUID with `blkid` and added to `/etc/fstab` for auto-mount

### Network Tools
- Viewed IP and interfaces with `ip a`
- Used `ping` to test connectivity to websites and DNS
- Installed and used `nmtui` for basic network configuration
- Compared legacy tools like `ifconfig` and `netstat` with modern ones like `ip` and `ss`

## Problems I solved

- Accidentally locked myself out of SSH — reopened port with UFW in recovery mode
- Misconfigured `fstab` initially — system failed to boot properly until UUID was corrected
- `fail2ban` didn’t start at first — forgot to set `enabled = true` in `[sshd]` section

## Plans for next week
- Learn the basics of Bash scripting
- Try automating routine server tasks (e.g., service checks, backups)
- Explore simple monitoring tools like `htop`, `top`, `df`, and `uptime`
- etc.

This is my first weekly DevOps learning report. The goal is to document my journey and track progress each week.

