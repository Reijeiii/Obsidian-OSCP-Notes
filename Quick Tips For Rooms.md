- add ip to /etc/hosts

### export variables for re-use
```
export LHOST="<local_ip>";
export RHOST="<TARGET_IP>";
```
### Enumeration:
Start with autorecon to scan for Open ports and known vulnerabilities
``` bash
sudo autorecon <TARGET_IP>
```
or with basic nmap
``` bash
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