### checklist Windows ###
  
**Hostname:** hostname  
**Infos utilisateur:** whoami /all  
**infos IP:** ipconfig /all  
**liste des connexions:** netstat -ano  
**infos system:** systeminfo  
**powershell-history:** type C:\Users\[user]\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt  
  
**lister user/groupe en powershell:**  
Get-LocalUser  
net user [user]  
Get-LocalGroup  
Get-LocalGroupMember adminteam 
  
**process:** Get-Process  
**Logiciels installés:**  
Get-ItemProperty "HKLM:\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\*" | select displayname  
Get-ItemProperty "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\*" | select displayname  
