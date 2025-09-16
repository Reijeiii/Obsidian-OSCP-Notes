### Basic Nmap scan

``` bash
sudo nmap -T4 -sC -sV -p- $IP --open -oN nmap-tcp.txt -v
```
- `-sC`: Runs default scripts (like version checking, vuln scans, etc.)
- `-sV`: Version detection
- `-O`: OS fingerprinting
- `-Pn`: Skip host discovery (assumes host is up — good for labs/firewalls)
- `-T4`: Speeds up the scan (balanced speed and reliability)

#### Nmap Scan (Quick)
```
nmap -sC -sV 10.10.10.10
```

### Identify running services and check for know vulnerabilities:
``` bash
nmap -sV -vv --script vuln <TARGET_IP>
```

### Scan all ports with details:
``` bash
nmap -T4 -p- -A <IP>
```

### Most common ports

```shell
nmap -sT <target>
```

### OS Fingerprint

```shell
nmap -O <target>
```

Try to guess the operating system behind the server, based on how the server is responding. This is effective because the TCP/IP stack is implemeted differently in the Operating Systems. The result fingreprint is then matched with a list of fingerprint of many OS. Adding **--osscan-guess** we get a guess of the OS.

### Server Banners

```shell
nmap -sV <target>
```

In order to have a better understanding of the service we can try to read the server fingerprint for that port. This increase the traffic for the scan.

#### Other nmap scan useful during exam

```
nmap -sV -Pn -T4 -A -p- -iL hosts.nmap -oN ports.nmap
nmap --script vuln --script-args=unsafe=1 -iL hosts.nmap
```

