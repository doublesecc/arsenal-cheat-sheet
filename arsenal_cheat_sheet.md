# nmap
% nmap

#plateform/linux #target/remote #cat/RECON #tag/scan

## nmap - full tcp syn, service version and default scripts, output to file
```
sudo nmap -v -sS -sV -sC -T4 -p- -oA <output_file|nmap/tcp_full_scan> <ip>
```

# SMB
% smb

#plateform/linux #target/remote #cat/ATTACK/CONNECT

## smbclient - list shares as anonymous user, just hit enter on password prompt
```
smbclient -L <ip>
```
## smbclient - list shares
```
smbclient -L //<ip> -U <user>
```

## smbclient - connect to share, to download files set recurse on 'RECURSE ON' and disable prompt 'PROMPT OFF' then 'mget*' to download
```
smbclient //<ip>/<share>
```

## smbmap - list shares with no authentication
```
smbmap -H <ip>
```

## smbmap - list shares with null authentication
```
smbmap -u null -p "" -H <ip>
```

## smbmap - list all contents of share with no authentication
```
smbmap -R <share> -H <ip>
```

## smbmap - download specific file from share (might not save to local dir, updatedb, locate file)
```
smbmap -R <share> -H <ip> -A '<file>' -q
```

## smbmap - download all files from share. Sometimes not all files are visible, connect via smbclient to confirm.
```
smbmap -R <share> -H <ip> -A '.' -q
```

# Crackmapexec
% crackmapexec
#plateform/linux #target/remote #cat/ATTACK/CONNECT

## crackmapexec - check password policy with null authentication, only works against pre windows compatibility group (domains upgraded from 2003)
```
crackmapexec smb <ip> --pass-pol -u '' -p ''
```

# rpc
% rpc

#plateform/linux #target/remote #cat/ATTACK/CONNECT

## rpcclient - null authentication
```
rpcclient -U '' <ip>
```

# Mount
% mount

#plateform/linux #target/remote #cat/ATTACK/CONNECT

## mount - mount share
```
mount -t cifs -o username=<user>,password=<password> //<ip>/"<share>" <local_dir>
```

# semgrep
% code_review

#platfeorm/linux #target/local #cat/code_review #tag/scan

## semgrep - webapp local code review
```
semgrep --config "p/security-audit" --config "p/owasp-top-ten" --config "p/javascript" --metrics off <source_code>
```

## semgrep - java webapp
```
semgrep --config "p/security-audit" --config "p/owasp-top-ten" --config "p/java" --config "p/secrets" --config "p/clientside-js" --config "p/sql-injection" --config "p/command-injection" --config "p/insecure-transport" -v --metrics off -o semgrep_<file>.md <source_code>
```

# xfreerdp
% rdp, windows, 3389

#plateform/linux #target/remote #protocol/rdp #port/3389 #cat/ATTACK/CONNECT

## xfreerdp - share clipboard
```
xfreerdp /v:<ip> /u:<user> /p:<password> /cert-ignore +clipboard
```

# Haiti
% password recovery, password cracking

#plateform/linux #target/local #cat/CRACKING/PASSWORD 

## Haiti - Identify hash from file
```
haiti -e $(cat <hash.txt|hash.txt>)
```

## Haiti - Identify hash from argument
```
haiti -e <hash|hash>
```

# Hashid
% password recovery, password cracking

#plateform/linux #target/local #cat/CRACKING/PASSWORD 

## Hashid - Identify hash
```
hashid <hash>
```

# john
% password recovery, password cracking

#plateform/linux #target/local #cat/CRACKING/PASSWORD

## John - Convert RAR to crackable hash
```
rar2john <rar_file> > <hash_to_be_cracked>
```

## John - Check formats
```
john --list=formats | grep -i <value>
```

## John - Standard crack no format
```
john --wordlist=<wordlist|/usr/share/wordlists/rockyou.txt> <hash>
```

## John - Standard crack with format
```
john --wordlist=<wordlist|/usr/share/wordlists/rockyou.txt> --format=<format> <hash>
```

## John - Show cracked passwords by current user that are stored in pot
```
cat ~/.john/john.pot
```

## John - Show cracked passwords via John for a specific hash file
```
john --show <hash_file>
```

## John - Convert /etc/shadow to crackable format (both /etc/passwd and /etc/shadow required)
```
unshadow <passwd_file> <shadow_file> > <output_file|unshadowed.txt>
```

## John - Crack /etc/shadow hashes
```
john --wordlist=<wordlist|/usr/share/wordlists/rockyou.txt> --format=sha512crypt <hash|unshadowed.txt>
```

## John - Convert zip file to crackable hash
```
zip2jhon <zipfile> > <zip_hash.txt|zip_hash.txt>
```

## John - Crack zip hash
```
john --wordlist=<wordlist|/usr/share/wordlists/rockyou.txt> <zip_hash.txt|zip_hash.txt>
```

## John - Convert SSH private key to hash to crack ssh key password
```
ssh2john <id_rsa|id_rsa> > <hash|id_rsa_hash.txt>
```

## SSH - SSH into target using key and cracked password
```
ssh -i <id_rsa_file> <user>@<ip>
#password: cracked_password
```

## John - Convert pfx file to crackable hash
```
pfx2john <pfx_file> > <pfx_hash.txt|pfx_hash.txt>
```

## John - Convert kirbi TGS to crackable hash
```
/usr/share/john/kirbi2john.py <hash.kirbi|hash.kirbi> > <outfile|kirbi_hash_to_crack>
```

## John - Crack kerberos TGS hash
```
john --wordlist=<wordlist|/usr/share/wordlists/rockyou.txt> --format=krb5tgs <hash.txt|kirbi_hash_to_crack>
```

## John - Crack NT Hash
```
john --wordlist=<wordlist|/usr/share/wordlists/rockyou.txt> --format=NT <hash.txt>
```

## John - Crack Kerberos AS-REP
```
john --wordlist=<wordlist|/usr/share/wordlists/rockyou.txt> --format=krb5asrep <as_rep_hashes_john|as_rep_hashes_john>
```

## John - Crack Kerberos TGS-REP
```
john --wordlist=<wordlist|/usr/share/wordlists/rockyou.txt> --format=krb5tgs <hash.txt>
```

# TGS Rep Crack
% password recovery, password cracking

#plateform/linux #target/local #cat/CRACKING/PASSWORD 

## TGS Rep Crack - Crack TGS Responses containing hashed service password
```
/usr/share/kerberoast/tgsrepcrack.py <wordlist|/usr/share/wordlists/rockyou.txt> <TGS_response|*kirbi_ticket>
```

# GPP
% password recovery, password cracking

#plateform/linux #target/local #cat/CRACKING/PASSWORD 
## GPP Decrypt - Decrypt Group Policy Preferences (GPP) encrypted strings
```
gpp-decrypt <string>
```

# Steghide
## Steghide - Show info on file
```
steghide info <file>
```

## Steghide - Extract data from file
```
steghide extract -sf <file>
```

# Stegsolve
## Stegsolve - Run stegsolve
```
java -jar stegsolve.jar
```

# Kerbrute
## Kerbrute -  user Enumeration
```
/opt/kerbrute/dist/kerbrute_linux_amd64 userenum --dc <DC> -d <domain> <wordlist|User.txt> -o <output_file>
```

# Impacket
## getuserspns - dump the Kerberos hash for all kerberoastable accounts it can find on the target domain 
```
python3 /usr/share/doc/python3-impacket/examples/GetUserSPNs.py <domain>/<user>:<password> -dc-ip <ip> -request -outputfile <spn_filename> 
```
## getnpusers - obtain TGT tickets for users with user wordlist and output in format for john
```
python3 /usr/share/doc/python3-impacket/examples/GetNPUsers.py -dc-ip <DC-IP> -usersfile <userlist_file> -outputfile <output_file|as_rep_hashes_john> -format john -no-pass <domain>/<ip>
```
## getnpusers - obtain TGT tickets for users and output in format for john
```
python3 /usr/share/doc/python3-impacket/examples/GetNPUsers.py -dc-ip <dc-ip|ip> -outputfile as_rep_hashes_john -format john <domain>/
```

## psexec - with username 
```
python3 /usr/share/doc/python3-impacket/examples/psexec.py <domain>/<user>:<password>@<ip>
```
