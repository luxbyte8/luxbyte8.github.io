# Notes for hacking

### SMB Enumeration (INE)
```bash
nmap -p445 --script smb-protocols <IP>

nmap -p444 --script smb-security-mode <IP>

nmap -p445 --script smb-enum-sessions <IP>

nmap -p445 --script smb-enum-sessions <IP> --script-args smbusername=<username>,smbpassword=<password> <IP>
```
