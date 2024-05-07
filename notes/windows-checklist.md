# Checklist Windows
  
**Hostname:** hostname  
**Infos utilisateur:** whoami /all  
**infos IP:** ipconfig /all  
**liste des connexions:** netstat -ano  
**infos system:** systeminfo  
**powershell-history:** type C:\Users\[user]\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt  
  
**list connected user:**  
query user  
  
**users and localgroups:**  
net users  
net localgroups  

**More info about a specific user:**  
net user [user]  
  
**View Domain Groups:**  
net group /domain  
  
**View Members of Domain Group:**  
net group /domain [Group Name]  

**lister user/groupe en powershell:**  
Get-LocalUser  
Get-LocalGroup  
Get-LocalGroupMember adminteam  
  
**process:**  
Get-Process  
tasklist /v  
  
**Logiciels installés:**  
Get-ItemProperty "HKLM:\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\*" | select displayname  
Get-ItemProperty "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\*" | select displayname  
  
**Firewall:**  
netsh firewall show state  
netsh firewall show config  

## Cleartext Passwords  
findstr /si password *.txt  
findstr /si password *.xml  
findstr /si password *.ini  
  
**Find all those strings in config files.**  
dir /s *pass* == *cred* == *vnc* == *.config*  
  
**Find all passwords in all files.**  
findstr /spin "password" *.*  
findstr /spin "password" *.*  

Some source: https://chryzsh.gitbooks.io/pentestbook/content/privilege_escalation_windows.html  
