# SUID-marked Binaries & Sudo Right Abuse
Check **GTFOBins.** Sometimes it is necessary to specify the absolute path of the binary with sudo privileges instead of the relative path. 

**1. Special Permission Enumeration**
```
find / -perm -u=s -type f 2>/dev/null
find / -user root -perm -4000 -exec ls -ldb {} \; 2>/dev/null

find / -uid 0 -perm -6000 -type f 2>/dev/null
find / -perm -u=s -type f 2>/dev/null
find / -user root -perm -6000 -exec ls -ldb {} \; 2>/dev/null
```
**2. Sudo Rights Enumeration**
```
sudo -l
```
**3. Check Audit Daemon:** If any privilege escalation attempts fail, check the syslog.
```
cat /var/log/syslog | grep <program_name>
```

<br>

# Privileged Groups
lorem ipsum



<br>

# Capabilities
Check **GTFOBins.** Sometimes it is necessary to specify the absolute path of the binary with sudo privileges instead of the relative path. 

**1. Enumerate Binaries with Misconfigured Capabilities**
```
/usr/sbin/getcap -r / 2>/dev/null
find /usr/bin /usr/sbin /usr/local/bin /usr/local/sbin -type f -exec getcap {} \;
```
