[home](../README.md)

---

## SMB Enumeration with NMAP (INE)  

**smb-protocols** will check the versions (dialects) of SMB that the target machine uses<br>
```bash
nmap -p445 --script smb-protocols <IP>
```
**smb-security-mode** will check the security level of the SMB configuration<br>
```bash
nmap -p444 --script smb-security-mode <IP>
```
**--script-args** is optional for most of these but may not return any information if **guest** access is disabled or does not have enough permissions<br>
```bash
nmap -p445 --script smb-enum-domains --script-args smbusername=<username>,smbpassword=<password> <IP>

nmap -p445 --script smb-enum-shares --script-args smbusername=<username>,smbpassword=<password> <IP>

nmap -p445 --script smb-enum-users --script-args smbusername=<username>,smbpassword=<password> <IP>

nmap -p445 --script smb-enum-groups --script-args smbusername=<username>,smbpassword=<password> <IP>

nmap -p445 --script smb-enum-sessions --script-args smbusername=<username>,smbpassword=<password> <IP>

nmap -p445 --script smb-server-stats --script-args smbusername=<username>,smbpassword=<password> <IP>

nmap -p445 --script smb-enum-services --script-args smbusername=<username>,smbpassword=<password> <IP>

nmap -p445 --script smb-enum-shares,smb-ls --script-args smbusername=<username>,smbpassword=<password> <IP>
```

## Enumerating Samba

Checking default UDP ports (137,138) for **nmbd** service<br>
```bash
nmap -sU [-p port/portrange] <IP>
```
Checking OS and Samba version using **nmap**<br>
```bash
nmap -p445 --script smb-os-discovery <IP>
```
Checking Samba version using **msfconsole**
```bash
msfconsole
use auxiliary/scanner/smb/smb_version
set rhosts <IP>
run
```
Checking NetBIOS computer name using **nmblookup**<br>
[nmblookup output explained](https://superuser.com/questions/710304/how-to-interpret-output-of-nmblookup-a)
```bash
nmblookup -A <IP>
```
Checking for **NULL** sessions with **smbclient**<br>
If you get share information, then null session connection was successful<br>
```bash
smbclient -L <IP> -N
```
Checking for **NULL** sessions with **rpcclient**<br>
If you get "rpcclient $>" prompt, then run "?" for help<br>
```bash
rpcclient -U "" -N <IP>
rpcclient $> ?
```
Some helpful rpcclient commands
```bash
srvinfo
enumdomusers
enumdomgroups
lookupnames <username>
```
Checking OS version using **enum4linux**
```bash
enum4linux -o <IP>
```
Checking if SMBv2 is supported using **msfconsole**
```bash
msfconsole
use auxiliary/scanner/smb/smb2
set rhosts <IP>
run
```
Checking SMB users with **msfconsole**
```bash
msfconsle
use auxiliary/scanner/smb/smb_enumusers
set rhosts <IP>
run
```
Checking SMB users with **enum4linxu**
```bash
enum4linux -U <IP>
```
Checking SMB shares with **msfconsole**
```bash
msfconsole
use auxiliary/scanner/smb/smb_enumshares
set rhosts <IP>
run
```
Checking SMB shares with **enum4linux**
```bash
enum4linux -S <IP>
```
Checking SMB groups with **enum4linx**
```bash
enum4linux -G <IP>
```
Checking SMB printer configuration(s) with **enum4linux**
```bash
enum4linux -i <IP>
```
Brute force password for a user using **msfconsole**
```bash
msfconsole
use auxiliary/scanner/smb/smb_login
set pass_file </path/to/wordlists/passwords.txt>
set smbuser <username>
set rhosts <IP>
run
```
Brute force password for a user using **hydra**
```bash
hyrda -l <username> -P </path/to/wordlists/password.txt> <IP> <protocol>
hyrda -l admin -P </path/to/wordlists/password.txt> <IP> smb
```
Listing named pipes in SMB using **msfconsole**
```bash
msfconsole
use auxiliary/scanner/smb/pipe_aduitor
set smbuser <username>
set smbpass <password>
set rhosts <IP>
run
```
List the SID of users with RID cycling using **enum4linux**
```bash
enum4linux -r -u "<username>" -p "<password>" <IP>
```
Checking SMB shares with guest access using **smbmap**
```bash
smbmap -u guest -p "" -H <IP>
smbmap -u <admin> -p <password> -H <IP>
```
Execute a command using **smbmap**
```bash
smbmap -u <admin> -p <password> -H <IP> -x '<command>'
smbmap -u <admin> -p <password> -H <IP> -x 'ipconfig'
```
List all drives on specifice host using **smbmap**
```bash
smbmap -H <IP> -u <admin> -p <password> -L
```
List the contents of a specific drive using **smbmap**
```bash
smbmap -H <IP> -u <admin> -p <password> -r '<drive>'
smbmap -H <IP> -u <admin> -p <password> -r 'C$'
```
Misc. stuff with **smbmap**
```bash
smbmap -H <IP> -u <admin> -p <password> --upload '/path/to/backdoor.exe' 'C$\totally_normal_file.exe'

smbmap -H <IP> -u <admin> -p <password> --download 'C$\super_private_file.txt'
```

## References & Further Reading:
- [Samba](https://wiki.samba.org/index.php/Main_Page)
- [CIFS](http://www.ubiqx.org/cifs/)



---
[home](../README.md)
