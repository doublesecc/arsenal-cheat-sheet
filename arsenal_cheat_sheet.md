# nmap
% nmap

#platform/linux #target/remote #cat/RECON #tag/scan

## nmap - full tcp syn, service version and default scripts, output to file.
```
sudo nmap -v -sS -sV -sC -T4 -p- -oA <output_file|nmap/tcp_full_scan> <ip>
```

# semgrep
% code_review

#platform/linux #target/local #cat/code_review #tag/scan

## semgrep - webapp  local code review
```
semgrep --config "p/security-audit" --config "p/owasp-top-ten" --config "p/javascript" --metrics off <source_code>
```

# xfreerdp
% rdp, windows, 3389

#platform/linux #target/remote #protocol/rdp #port/3389 #cat/ATTACK/CONNECT

## xfreerdp - share clipboard
```
xfreerdp /v:<ip> /u:<user> /p:<password> /cert-ignore +clipboard
```

# john
% password recovery, password cracking

#plateform/linux #target/local #cat/CRACKING/PASSWORD

## Convert RAR to crackable hash:
```bash
rar2john <rar_file> > <hash_to_be_cracked>
```
