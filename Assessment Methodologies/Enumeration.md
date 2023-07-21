# Enumeration
### Enumerating servers and services
##### ***Note: the 10.10.10.10 IP address is used as an example here and you can change it to your desired IP address.*** 
#### SMB:
 - Windows implementation of file share
 - Server Message Block
 - port 445
 - smb enumeration using Nmap Scripts
 - $ nmap -p 445 --script smb-protocols 10.10.10.10
 - $ nmap -p445 --script smb-security-mode 10.10.10.10
 - $ nmap -p445 --script smb-enum-sessions 10.10.10.10
 - $ nmap -p445 --script smb-enum-sessions --script-args smbusername=administrator,smbpassword=smbserver_771 10.10.10.10
 - enumerate shares --> $ nmap -p445 --script smb-enum-shares 10.10.10.10
 - $ nmap -p445 --script smb-enum-shares --script-args smbusername=administrator,smbpassword=smbserver_771 10.10.10.10 
 - enumerate users  --> $ nmap -p445 --script smb-enum-users --script-args smbusername=administrator,smbpassword=smbserver_771 10.10.10.10 
 - check the Nmap Scripts documentation for more SMB scripts that can be useful for penetration testing
 - tool used - SMBMap
 - $ smbmap -u guest -p "" -ed . -H 10.10.10.10
 - running a command using SMBMap --> $ smbmap -H 10.10.10.10 -u administrator -p smbserver_771 -x 'ipconfig'
 - check the -help and documentation for more commands  
 - you can connect, enumerate, upload, and download files using the SMBMap 
 - $ smbmap -H 10.10.10.10 -u administrator -p smbserver_771 --download 'c$\flag.txt'

#### SMB - Samba
- Samba is the SMB version of the Linux
- can also use Metasploit  by using --> auxiliary(scanner/smb/smb_version)
- connect via smbclient and rpcclient --> These tools are preinstalled in Kali Linux
- enum4linux  --> great tool

#### FTP
- File Transfer Protocol
- port 21
- check for usernames using hydra --> $ hydra -L /usr/share/merasploit-framework/data/wordlists/common_users.txt -P /usr/share/merasploit-framework/data/wordlists/unix_passwords.txt 10.10.10.10 ftp
- we can also do it via Nmap Scripts --> nmap 10.10.10.10 --script ftp-brute --script-args userdb=/root/users -p 21  --> users in this argument is the list of users 
- connet via ftp  --> ftp 10.10.10.10
- anonymous Login --> nmap 10.10.10.10 -p 21 --script ftp-anon <--> If anonymous login was allowed, connect using FTP and enter anonymous for the user and no password

#### SSH
- Secure Shell
- port 22
- how to connect :- $ ssh root@10.10.10.10
- $ nc 10.10.10.10 22
- $ nmap 10.10.10.10 -p 22 --script ssh2-enum-algos  --> to check which algorithms is being used
- nmap 10.10.10.10 -p 22 --script ssh-hostkey --script-arg ssh_hostkey=full --> pull rsa host key
- check for weak passwords - $ nmap 10.10.10.10 -p 22 --script ssh-auth-methods --script-args="ssh.user=student" --> student can be admin or any user
- SSH Dictionary attack -- for poor passwords and poor misconfiguration
- $ hydra -l student -P /usr/share/passwordlists/rockyou.txt 
- $ nmap 10.10.10.10 -p 22 --script ssh-brute --script-args user=administrator ***or can be a list of users and can be specified by -- userdb=/root/users***
- we can also use Metasploit to perform a brute force 
- metasploit command --> use auxiliary/scanner/ssh/ssh_login -- configure the options and run

#### HTTP
- for hosting websites
- $ whatweb 10.10.10.10
- $ http 10.10.10.10
- $ dirb http://10.10.10.10
- $ browsh --startup-url http://10.10.10.10/Default.aspx  --> a good tool if you have access to just the terminal, it will help you see somehow the actual webpage
- Nmap scripts --> nmap 10.10.10.10 -sV -p 80 --script http-enum 
- $ nmap 10.10.10.10 -sV -p 80 --script http-headers
- $ nmap 10.10.10.10 -sV -p 80 --script http-methods --script-args http-methods.url-path=/webdav/
- the above commands are an example of how to enumerate an HTTP with Nmap Scripts 
- for Linux/Unix OS
- nmap 10.10.10.10 -p 80 -sV -script banner
- using Metasploit --> use auxuilary/scanner/http/http_version --> configure all options
- wget "http://10.10.10.10/index"  --> will download the webpage
- also browsh 
- Metasploit again --> use auxiliary/scabber/http/brute_dirbs 
- dirb http://10.10.10.10 <passwordlist path>
- robots.txt --> use auxiliary/scanner/http/robots_txt

#### SQL
- $ nmap 10.10.10.10 -p 3306 --script=mysql-empty-password --> check the Nmap documentation for more scripts for MySQL
- $ mysql -h 10.10.10.10 -u root 
- once inside -- show databases 
- and then -- use books; 
- using Metasploit 
- use auxiliary/scanner/mysql/mysql_writeable_dirs
- use auxiliary/scanner/mysql/mysql_hashdump  --> another Metasploit auxiliary that can be used
- $ nmap 10.10.10.10 -p 3306 --script=mysql-empty-password
- dictionary attack using Metasploit --> use auxiliary/scanner/mysql/mysql_login
- or by hydra --> $ hydra -l root -P < **password list path**> 10.10.10.10 mysql

#### MSSQL -- Windows version
- Nmap script fo MSSQL --> nmap 10.10.10.10 -p 1433 --script ms-sql-info 
- $ nmap 10.10.10.10 -p 1433 --script ms-sql-ntlm-info --script-args mssql.instance-port=1433
- $ nmap 10.10.10.10 -p 1433 --script ms-sql-brute --script-args userdb=< **users list path**>,password=< **pass list path**>
- check for empty passwords --> $ nmap 10.10.10.10 -p 1433 --script ms-sql-empty-password
-  $ nmap 10.10.10.10 -p 1433 --script ms-sql-query --script-args mssql.username=admin,mssql.password=anamaria,ms-sql-query.query="SELECT * FROM master..syslogins" -oN output.txt
- $ $ nmap 10.10.10.10 -p 1433 --script ms-sql-dump-hashes --script-args mssql.username=admin,mssql.password=anamaria
- $ nmap 10.10.10.10 -p 1433 --script ms-sql-xp-cmdshell --script-args mssql.username=admin,mssql.password=anamaria,ms-sql-xp-cmdshell.cmd="ipconfig" --> running a command 
- Metasploit 
- $ use auxiliary/scanner/mssql/mssql_login  --> configure all options
- $ use auxiliary/admin/mssql/mssql_enum 
- $ use auxiliary/admin/mssql/mssql_enum_sql_logins
- $ use auxiliary/admin/mssql/mssql_exec -- set cmd whoami
- $ use auxiliary/admin/mssql/mssql_enum_domain_accounts
- For all the above Metasploit commands, do complete all the options that are required with a yes
