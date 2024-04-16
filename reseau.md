<img src="https://github.com/florianges/Simple-OSCP-cheat-sheet/assets/64069514/2b1a86a8-565a-48c7-909f-4f1725583655" height="180">

## Scan nmap :
nmap -A [IP]  
-O : Essaye de déterminer le système d'exploitation  
-sV : Essaye de déterminer les versions les logiciels installés  
-sC : Utilise des script par défaut  
--traceroute : Essaye de déterminer les différents sauts IP entre l'attaquant et le serveur  
-A : Cette option regroupe toutes ces options: -O -sV -sC --traceroute  
-sU : scan UDP  
-sS : Cette option ne termine pas les demandes de connexion -sS TCP (plus discret)  
-p 1-1000 : Spécifie une plage de port (-p- spécifie tout les port)  
-script [nom du script] : utilise un script  
-oN/-oX/-oS/-oG [fichier] : Génère un fichier xml avec les résultats du scan  

## Énumération DNS :
•	dnsenum [IP]  
•	Transfert de zone: dig AXFR dommaine @serveur_DNS  
•	récupérer fichier txt: host -t txt [domaine ] 

## Création de serveur :
•	http: python -m SimpleHTTPServer [port]  
•	ftp: python -m pyftpdlib -p [port]  
•	smb (avec authentification): smbserver.py -smb2support -username guest -password guest share ./  
•	smb (sans authentification): smbserver.py -smb2support share ./  

## Decouvrir les serveurs DHCP sur le réseau :
nmap --script broadcast-dhcp-discover  

## Enumération LDAP:
nmap -p 389 --script ldap-* [IP] : script nmap pour découvir les DC, trouver si des login anonymous sont accepté...  
ldapsearch -h [IP] -x -s base : Information sur le serveur LDAP, DC, currentTime...  
ldapsearch -h [IP] -x -b "DC=XXXX,DC=XXXX" : Récupération de l'arborescence du LDAP  

## Enumération SMTP (mail server):
bruteforce usser: smtp-user-enum.pl -M VRFY -U users.txt -t [IP]  (https://pentestmonkey.net/tools/user-enumeration/smtp-user-enum)
