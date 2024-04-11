<img src="https://github.com/florianges/Simple-OSCP-cheat-sheet/assets/64069514/6ada07ef-1fa7-4bad-83ff-78d636d8a6b5" width="450">

## Énumération des pages web :
dirb http://[IP] -X .php,.html,.txt  
gobuster –url [IP] dir –wordlist /usr/share/wordlists/dirb/big.txt -x php,txt,html  
## Identification de CMS :
whatweb [URL]  
python3 cmseek.py -u [URL]  
## Recherche des paramettres GET :
wfuzz --hh=[SIZE] -w [WORDLIST] [URL].php?[PARAM_NAME]=test  
## Recherche des fichiers backup :
dirb http://[fichier a tester] /usr/share/wordlists/dirb/mutations_common.txt -t
## Injection SQL :
sqlmap -u [URL] (--dbs / --tables -D [DATABASE] / --columns -D [DATABASE] -T [TABLENAME])  
sqlmap -r [FILE] (--dbs / --tables -D [DATABASE] / --columns -D [DATABASE] -T [TABLENAME])   
A la main: http://192.168.1.50/wordpress/sql-injection-cheat-sheet/  
 
