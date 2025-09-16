- add ip to /etc/hosts

- export variable so no need always to write whole ip
```
export LHOST="<local_ip>";
export RHOST="<TARGET_IP>";
```
### Enumeration: asdasd

Start with autorecon to scan for Open ports and known vulnerabilities
``` bash
sudo autorecon <TARGET_IP>
```
or with basic nmap
``` bash
sudo nmap -T4 -sC -sV -p- $IP --open -oN nmap-tcp.txt -v
```

If there is web server run gobuster
```
gobuster dir -u http://<TARGET_IP>:<PORT> -w /usr/share/wordlists/dirbuster/directory-list-1.0.txt 
```

#### SMB 445
- check for mounts
- `Smbclient, enum4linux, smbmap`

#### 80 HTTP
- Gobuster for directories
- robots.txt
- page source

#### 21 FTP
- anonymous login?

#### 22 SSH 
- version
- bruteforce?



### Privesc

check designated notes
[[Linux Privesc Enum]]
[[Windows PrivEsc Quick Tips]]