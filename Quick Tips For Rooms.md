- add ip to /etc/hosts

### export variables for re-use
```
export LHOST="<local_ip>";
export RHOST="<TARGET_IP>";
```
### Enumeration:
``` bash
#autorecon runs all scans for all ports and vulnerabilities. Very heavy
sudo autorecon <TARGET_IP>

#NmapAutomator. 
nmapautomator.sh <TARGET_IP> --type port #shows open ports
nmapautomator.sh <TARGET_IP> --type recon #runs basic recon
nmapautomator.sh <TARGET_IP> --type script #runs script scan
nmapautomator.sh <TARGET_IP> --type vulns #runs vuln scan

#Basic nmap
sudo nmap -T4 -sC -sV -p- $IP --open -oN nmap-tcp.txt -v
```

#### SMB 445
- check for mounts
- `Smbclient, enum4linux, smbmap`

#### 80 HTTP
- Gobuster for directories
``` bash
gobuster dir -u http://<TARGET_IP>:<PORT> -w /usr/share/wordlists/dirbuster/directory-list-1.0.txt 
```
- check robots.txt for hidden folders
- check page source

#### 21 FTP
- anonymous login?
- test admin creds admin/admin; root/root; admin/password

#### 22 SSH 
- version
- bruteforce?
- test admin/admin; root/root; admin/password