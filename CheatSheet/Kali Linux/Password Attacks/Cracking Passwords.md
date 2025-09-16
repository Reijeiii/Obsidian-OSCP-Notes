### John The Ripper

basic password crack:
```
john <pswd-file>
```

wordlist path and hash format:
```
john <passwordFile> --wordlist=/usr/share/wordlists/rockyou.txt --format=Raw-SHA256
```

### Hashcat
```
hashcat -m 0 -a 0 hash.txt /usr/share/wordlists/rockyou.txt
```

check hash format from: https://www.tunnelsup.com/hash-analyzer/
or with hashid 
```
hashid '<hash>'
```