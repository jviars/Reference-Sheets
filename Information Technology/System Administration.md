# System Administration Reference Sheet

## Linux System Administration

### User Management
```bash
# User Operations
useradd [username]            # Create new user
userdel [username]            # Delete user
usermod [options] [username]  # Modify user
passwd [username]             # Change password

# Group Operations
groupadd [groupname]         # Create new group
groupdel [groupname]         # Delete group
groupmod [options] [group]   # Modify group
gpasswd [options] [group]    # Administer groups

# Access Control
chown user:group file        # Change ownership
chmod permissions file       # Change permissions
sudo command                 # Execute as superuser
su - username               # Switch user
```

### File System Management
```bash
# Disk Operations
df -h                       # Show disk usage
du -sh directory           # Directory size
mount device mountpoint    # Mount filesystem
umount mountpoint         # Unmount filesystem
fsck device               # Check filesystem

# File Operations
ls -la                     # List files with details
cp source destination     # Copy files
mv source destination     # Move/rename files
rm [-r] file/directory    # Remove files/directories
find / -name filename    # Find files
grep pattern files       # Search in files

# Permissions
chmod 755 file           # rwx r-x r-x
chmod 644 file           # rw- r-- r--
chmod +x file            # Add execute permission
chown user:group file    # Change ownership
```

### Process Management
```bash
# Process Monitoring
ps aux                    # List all processes
top                       # Dynamic process viewer
htop                      # Enhanced top
kill pid                  # Kill process
killall processname       # Kill by name
nice -n value command    # Run with priority
renice value pid         # Change priority

# Service Management (SystemD)
systemctl start service
systemctl stop service
systemctl restart service
systemctl status service
systemctl enable service
systemctl disable service
```

### Network Management
```bash
# Network Configuration
ip addr show             # Show IP addresses
ip link set dev up/down  # Enable/disable interface
ip route show            # Show routing table
ifconfig                 # Show/configure interfaces
netstat -tuln           # Show listening ports
ss -tuln                # Modern netstat

# Firewall (iptables/nftables)
iptables -L             # List rules
iptables -A INPUT       # Append rule
iptables -D INPUT       # Delete rule
iptables-save          # Save rules
iptables-restore       # Restore rules

# Network Troubleshooting
ping host              # Test connectivity
traceroute host       # Show route
dig domain           # DNS lookup
nslookup domain      # DNS lookup
tcpdump              # Packet capture
```

### Package Management

#### Debian/Ubuntu (APT)
```bash
apt update              # Update package lists
apt upgrade             # Upgrade packages
apt install package    # Install package
apt remove package     # Remove package
apt purge package      # Remove package & config
apt autoremove         # Remove unused packages
dpkg -i package.deb   # Install local package
```

#### Red Hat/CentOS (YUM/DNF)
```bash
yum update             # Update packages
yum install package   # Install package
yum remove package    # Remove package
yum search keyword    # Search packages
rpm -i package.rpm    # Install local package
dnf update            # DNF equivalent
```

### Log Management
```bash
# System Logs
journalctl                    # SystemD journal
tail -f /var/log/syslog      # Follow syslog
grep pattern /var/log/auth.log # Search auth log
less /var/log/messages       # View messages

# Log Rotation
logrotate -f /etc/logrotate.conf # Force rotation
```

### Backup and Recovery
```bash
# Backup Commands
tar -czf backup.tar.gz directory  # Create archive
tar -xzf backup.tar.gz           # Extract archive
rsync -av source destination    # Sync files
dd if=/dev/sda of=disk.img      # Disk image

# System Backup
dump -0uf /dev/tape /          # Full backup
restore -if /dev/tape          # Restore backup
```

## Windows System Administration

### PowerShell Commands
```powershell
# User Management
New-LocalUser "username"                # Create user
Remove-LocalUser "username"             # Delete user
Add-LocalGroupMember "group" "user"     # Add to group
Get-LocalUser                          # List users

# Service Management
Get-Service                           # List services
Start-Service servicename            # Start service
Stop-Service servicename             # Stop service
Restart-Service servicename          # Restart service

# Process Management
Get-Process                          # List processes
Stop-Process -Name processname      # Kill process
Get-Process | Sort-Object CPU -Desc # Sort by CPU
```

### Windows Server Management
```powershell
# Active Directory
Add-ADUser                           # Create AD user
Remove-ADUser                        # Delete AD user
Get-ADGroup                         # List AD groups
New-ADGroup                        # Create AD group

# File System
Get-ChildItem                      # List files
Copy-Item source destination      # Copy files
Move-Item source destination     # Move files
Remove-Item path                # Delete files
```

### Group Policy
```powershell
# GPO Management
New-GPO "name"                    # Create GPO
Get-GPO -All                     # List all GPOs
Set-GPLink                      # Link GPO
gpupdate /force                # Force update
```

## Security Administration

### SSL/TLS Management
```bash
# Certificate Operations
openssl req -new -key private.key -out cert.csr   # Create CSR
openssl x509 -req -in cert.csr -signkey key.pem   # Self-sign
openssl x509 -in cert.pem -text                   # View cert
```

### Security Monitoring
```bash
# Intrusion Detection
aide --check                     # Check file integrity
rkhunter --check                # Check rootkits
chkrootkit                      # Another rootkit check

# Security Scanning
nmap -sS target                 # Port scan
nikto -h target                # Web vulnerability scan
```

## Virtualization Management

### Docker
```bash
# Container Management
docker ps                       # List containers
docker images                  # List images
docker build -t name .        # Build image
docker run image             # Run container
docker stop container       # Stop container
docker rm container        # Remove container

# Docker Compose
docker-compose up         # Start services
docker-compose down      # Stop services
```

### Virtual Machines
```bash
# VirtualBox CLI
VBoxManage list vms              # List VMs
VBoxManage startvm "name"        # Start VM
VBoxManage controlvm "name" stop # Stop VM

# KVM/QEMU
virsh list                       # List VMs
virsh start domain              # Start VM
virsh shutdown domain          # Stop VM
```

## Monitoring and Maintenance

### System Monitoring
```bash
# Resource Monitoring
free -h                         # Memory usage
vmstat                         # Virtual memory stats
iostat                        # IO statistics
sar                          # System activity
```

### Performance Tuning
```bash
# System Configuration
sysctl -a                      # Show all parameters
ulimit -a                     # Show resource limits
nice -n value command        # Set process priority
```

### Automation and Scripting
```bash
# Cron Jobs
crontab -e                    # Edit cron jobs
crontab -l                   # List cron jobs

# Shell Scripting
#!/bin/bash
if [ condition ]; then
    command
fi

for item in items; do
    command
done
```

## Cloud Administration

### AWS CLI
```bash
# EC2 Management
aws ec2 describe-instances
aws ec2 start-instances
aws ec2 stop-instances

# S3 Operations
aws s3 ls
aws s3 cp source destination
aws s3 sync source destination
```

### Azure CLI
```bash
# Resource Management
az group list
az vm list
az vm start --name --resource-group
az vm stop --name --resource-group
```

## Database Administration

### MySQL/MariaDB
```sql
-- User Management
CREATE USER 'username'@'host' IDENTIFIED BY 'password';
GRANT privileges ON database.table TO 'username'@'host';
REVOKE privileges ON database.table FROM 'username'@'host';

-- Backup and Recovery
mysqldump -u user -p database > backup.sql
mysql -u user -p database < backup.sql
```

### PostgreSQL
```sql
-- User Management
CREATE USER username WITH PASSWORD 'password';
GRANT privileges ON DATABASE database TO username;
REVOKE privileges ON DATABASE database FROM username;

-- Backup and Recovery
pg_dump dbname > backup.sql
psql dbname < backup.sql
```
