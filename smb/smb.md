# Notes for hacking

### SMB Enumeration (INE)
```bash
nmap -p445 --script smb-protocols <IP>

nmap -p444 --script smb-security-mode <IP>

nmap -p445 --script smb-enum-domains --script-args smbusername=<username>,smbpassword=<password> <IP>

nmap -p445 --script smb-enum-shares --script-args smbusername=<username>,smbpassword=<password> <IP>

nmap -p445 --script smb-enum-users --script-args smbusername=<username>,smbpassword=<password> <IP>

nmap -p445 --script smb-enum-groups --script-args smbusername=<username>,smbpassword=<password> <IP>

nmap -p445 --script smb-enum-sessions --script-args smbusername=<username>,smbpassword=<password> <IP>

nmap -p445 --script smb-server-stats --script-args smbusername=<username>,smbpassword=<password> <IP>

nmap -p445 --script smb-enum-services --script-args smbusername=<username>,smbpassword=<password> <IP>

nmap -p445 --script smb-enum-shares,smb-ls --script-args smbusername=<username>,smbpassword=<password> <IP>

```



