### **1. Take a Step Back**

- Reread the **room description** and any questions

### **2. Re-Enumerate Thoroughly**

- Double-check your `nmap` results — missed ports?
- Run a **full port scan** if you haven’t
- Look at **robots.txt**, source code, headers, cookies
- add ip to /etc/hosts
- Did you find any info in webpage? 
```
  THM room silverplatter. Found info about project silverpeas. so navigater to url silverplatter:8080/silverpeas and found login
```

### **3. Enumerate the Services You Ignored**

- Did you skip SMB, FTP, or SSH?
- Try tools like:
    - `enum4linux` for SMB
    - `ftp [IP]` and try anonymous
    - `hydra` for brute-force (if allowed)

### **4. Google the Service or Version**

- Look up banners or versions from nmap:
    nginx
    CopyEdit
    `searchsploit apache 2.4.49`
- Google errors, strange outputs, or keywords

### **5. Try What-Ifs and Wild Ideas**

- What if you try `admin:admin`?
- What if you tamper with a cookie?
- What if that filename is an LFI?
- Sometimes the simplest things work

### **6. Use Automated Tools (Smartly)**

- `linpeas.sh`, `winpeas.exe`, `nmap scripts`
- Burp Suite, wfuzz, sqlmap (as applicable)

### **7. Take a Break**

- Seriously. Get up, stretch, walk.
- Come back with fresh eyes and you'll often spot something immediately.


### Bonus Pro-Tip:

Keep a "stuck journal" — every time you get stuck, write:
- What you’ve done
- What you ruled out
- What you’re assuming