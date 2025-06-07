# System Enumeration

**History Files & Path**
```
history
env
echo $PATH
cat ~/.bashrc
cat ~/.zshrc
cat ~/.bash_history
```
**System & Kernel Version**
```
uname -a
cat /etc/issue
cat /etc/os-release
uname -r
arch
```
**CPU Type & Version**
```
lscpu
```
**Drives & Shares**
```
lsblk
cat /etc/fstab
mount
```
**Device Drivers & Kernel Modules**
```
lsmod 
sbin/modinfo <module_name>
```

<br>

# Network Enumeration

**Interfaces**
```
ip a 
ifconfig
```
**Routing Information**
```
routel
route
netstat -rn
ip route
```
**Active Connections & Listening Ports**
```
netstat -anp
netstat -tua     #service names, not ports
netstat -tuna    #port numbers, not service names
ss -anp
ps aux          #users running commands
```
**Firewall Rules**
```
cat /etc/iptables/rules.v4
```
**ARP Tables**
```
arp -a 
ip neigh
```
**Last Logins**
```
lastlog
w
```

<br>

# User Enumeration

**User(s) & System Context**
```
id <username>
sudo -l
sudo -V
ls -lah /home
hostname
cat /etc/passwd
```
**Group Context**
```
groups <username>
getent group <group_name>      #get-localgroupmember
```

<br>

# Installed Applications & Scheduled Tasks

**Installed Applications**
```
dpkg -l
rpm -l
```
**Additional Information about Compiled Programs**
```
ls -l /bin /usr/bin/ /usr/sbin/
ls /usr/bin/python* 
```
**Scheduled Tasks**
```
ls -lah /etc/cron*
crontab -l           #unprivileged attempt
sudo crontab -l      #if privileges allow it
grep "CRON" /var/log/syslog
ls -lah /path/to/cron/file.sh
```

<br>

# Files & Directories

**Insecure File Permissions**
```
find / -writable -type d 2>/dev/null
```
**SUID-marked Binaries**
```
find / -perm -u=s -type f 2>/dev/null
```
**Binaries with Capabilities**
```
/usr/sbin/getcap -r / 2>/dev/null
```
**Configuration Files**
```
find / -type f \( -name *.conf -o -name *.config \) -exec ls -l {} \; 2>/dev/null
```
**.sh Scripts**
```
find / -type f -name "*.sh" 2>/dev/null | grep -v "src\|snap\|share"
```
**History Files Created by Programs/Scripts**
```
find / -type f \( -name *_hist -o -name *_history \) -exec ls -l {} \; 2>/dev/null
```
**Misc. File/Directory Types**
```
find / -path /proc -prune -o -type f -perm -o+w 2>/dev/null    #writeable files
find / -type f -name ".*" -exec ls -l {} \; 2>/dev/null | grep <keyword>   #hidden files
find / -type d -name ".*" -ls 2>/dev/null     #hidden directories
find / -path /proc -prune -o -type d -perm -o+w 2>/dev/null    #writeable directories
```
