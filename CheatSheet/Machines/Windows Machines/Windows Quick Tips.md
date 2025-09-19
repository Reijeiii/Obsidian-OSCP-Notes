https://github.com/samratashok/nishang The repository contains a useful set of scripts for initial access, enumeration and privilege escalation

# USING POWERSHELL IN REVERSE SHELL! IMPORTANT
``` bash
# if we want to use powershell cmds we need to use oneliners. Atleast I Don't know how to change to PS without shell crashing
powershell -ExecutionPolicy Bypass -Command "<CMD>"
#Example
powershell -ExecutionPolicy Bypass -Command ". .\PowerUp.ps1; Invoke-AllChecks"
```