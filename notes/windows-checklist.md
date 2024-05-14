# Checklist Windows
  
**Hostname:** hostname  
**Infos utilisateur:** whoami /all  
**infos IP:** ipconfig /all  
**liste des connexions:** netstat -ano  
**infos system:** systeminfo  
**powershell-history:** type C:\Users\[user]\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt  
to verify the path of ConsoleHost_history: (Get-PSReadlineOption).HistorySavePath  
  
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

**Kepass File**  
Get-ChildItem -Path C:\ -Include *.kdbx -File -Recurse -ErrorAction SilentlyContinue  
  
All doc file :
Get-ChildItem -Path C:\Users\ -Include *.txt,*.pdf,*.xls,*.xlsx,*.doc,*.docx -File -Recurse -ErrorAction SilentlyContinue

## mimikatz.exe cheat sheet
privilege::debug  -->  engage the SeDebugPrivlege  
token::elevate + lsadump::sam --> Dump from SAM database  
sekurlsa::logonpasswords --> Dump from Sekurlsa  
sekurlsa::tickets --> Dump cached tickets  
Some source: https://chryzsh.gitbooks.io/pentestbook/content/privilege_escalation_windows.html  

## démarer un service:  
sc.exe start audtiTracker  
