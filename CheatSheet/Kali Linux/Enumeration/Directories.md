### Ffuf
``` bash
ffuf -c -w /usr/share/seclists/Discovery/Web-Content/raft-large-directories-lowercase.txt -u http://<TARGET_IP>/FUZZ
```

### Gobuster

``` bash
gobuster dir -u http://10.10.48.44:3333 -w /usr/share/wordlists/dirbuster/directory-list-1.0.txt 

```

