# Windows Commands and WMI

## Command line

### Windows Registry

**Adding Keys and Values**

```powershell
C:>reg add [\TargetIPaddr][RegDomain][Key]
```

Add a key to the registry on machine [TargetIPaddr] within the registry domain [RegDomain] to location [Key].

If no remote machine is specified, the current machine is assumed.

**Export and Import**

```powershell
C:>reg export [RegDomain][Key] [FileName]
```

Export all subkeys and values located in the domain [RegDomain] under the location [Key] to the file [FileName]

```powershell
C:>reg import [FileName]
```

Import all registry entries from the file [FileName].

Import and export can only be done from or to the local machine.

Query for a specific Value of a Key

```powershell
C:>reg query [\TargetIPaddr][RegDomain][Key] /v [ValueName]
```

Query a key on machine [TargetIPaddr] within the registry domain [RegDomain] in location [Key] and get the specific value [ValueName] under that key.

Add /s to recurse all values.

### Processes and Services

List all processes currently running

```powershell
C:>tasklist
```

List all processes currently running and the DLLs each has loaded

```powershell
C:>tasklist /m
```

Lists all processes currently running which have the specified [dll] loaded

```powershell
C:>tasklist /m [dll]
```

List all processes currently running and the services hosted in those processes

```powershell
C:>tasklist /svc
```

Query brief status of all services

```powershell
C:>sc query
```

Query the configuration of a specific service

```powershell
C:>sc qc [ServiceName]
```

### File Search and Counting Lines

Search directory structure for a file in a specific directory

```powershell
C:>dir /b /s [Directory][FileName]
```

Count the number of lines on StandardOuy of [Command]

```powershell
C:>[Command] | find /c /v “”
```

Finds the count (/c) of lines that do not contain (/v) nothing (“”). 
Lines that do not have nothing are all lines, even blank lines, which contain CR/LF

### Command Line FOR loop

Counting Loop

```powershell
C:>for /L %i in([start],[step],[stop]) do [command]
```

Set %i to an initial value of [start] and increment it by [step] at every iteration until its value is equal to [stop].

For each iteration, run [command].

The iterator variable %i can be used anywhere in the command to represent its current value.

Iterate over file contents

```powershell
C:>for /F %i in ([file-set]) do[command]
```

Iterate through the contents of the file on a line-by-line basis. 

For each iteration, store the contents of the line into %i and run [command].

### Networking

Show all TCP and UDP port usage and process ID

```powershell
C:>netstat –nao
```

Look for usage of port [port] every [N] seconds

```powershell
C:>netstat –nao [N] | find [port]
```

Dump detailed protocol statistics

```powershell
C:>netstat –s –p [tcp|udp|ip|icmp]
```

Useful NETSH syntax

Turn off built-in Windows firewall

```powershell
C:>netsh firewall set opmode disable
```

Configure interface “Local Area Connection” with [IPaddr] [Netmask] [DefaultGW]

```powershell
C:>netsh interface ip set address local static [IPaddr] [Netmask] [DefaultGW] 1
```

Configure DNS server for “Local Area Connection”

```powershell
C:>netsh interface ip set dns local static [IPaddr]
```

Configure interface to use DHCP:

```powershell
C:>netsh interface ip set address local dhcp
```

### WMI

```powershell
C:>wmic [alias] [where clause] [verb clause]
```

**Useful [aliases]:**
- process
- service
- share
- nicconfig
- startup
- useraccount
- qfe (Quick Fix Engineering — shows patches)

**Example [where clauses]:**
- where name=”nc.exe”
- where (commandline like “%stuff”)
- where (name=”cmd.exe” and parentprocessid!=”[pid]”)

**Example [verb clauses]:**
- list [full|brief]
- get [attrib1,attrib2…]
- call [method]
- delete

Collect a list of groups on the local system using the following command

```powershell
wmic group list brief
```

which will return output similar to this

```powershell
Caption Domain Name SID

Lab7\Administrators Lab7 Administrators S-1–5–32–544

Lab7\Backup Operators Lab7 Backup Operators S-1–5–32–551

Lab7\Guests Lab7 Guests S-1–5–32–546

Lab7\Network Configuration Operators Lab7 Network Configuration Operators S-1–5–32–556

Lab7\Power Users Lab7 Power Users S-1–5–32–547

Lab7\Remote Desktop Users Lab7 Remote Desktop Users S-1–5–32–555

Lab7\Replicator Lab7 Replicator S-1–5–32–552

Lab7\Users Lab7 Users S-1–5–32–545

Lab7\Debugger Users Lab7 Debugger Users S-1–5–21–577561410–1864853564–3972553872–1006
```

The same command issued against a remote system in another domain looks like this

```powershell
wmic /user:"FOREIGN_DOMAIN\Admin" /password:"Password" /node:192.168.33.25 group list brief
```

and the output is

```powershell
Caption Domain Name SID

REMOTE-DESK\Administrators REMOTE-DESK Administrators S-1–5–32–544

REMOTE-DESK\Backup Operators REMOTE-DESK Backup Operators S-1–5–32–551

REMOTE-DESK\Guests REMOTE-DESK Guests S-1–5–32–546

REMOTE-DESK\Network Configuration Operators REMOTE-DESK Network Configuration Operators S-1–5–32–556

REMOTE-DESK\Power Users REMOTE-DESK Power Users S-1–5–32–547

REMOTE-DESK\Remote Desktop Users REMOTE-DESK Remote Desktop Users S-1–5–32–555

REMOTE-DESK\Replicator REMOTE-DESK Replicator S-1–5–32–552

REMOTE-DESK\Users REMOTE-DESK Users S-1–5–32–545

REMOTE-DESK\HelpServicesGroup REMOTE-DESK HelpServicesGroup S-1–5–21–789336058–1078081533–839522115–1001

REMOTE-DESK\__vmware__ REMOTE-DESK __vmware__ S-1–5–21–789336058–1078081533–839522115–1004

FOREIGN_DOMAIN\Cert Publishers FOREIGN_DOMAIN Cert Publishers S-1–5–21–1948120765-

2568877423–583830540–517

FOREIGN_DOMAIN\RAS and IAS Servers FOREIGN_DOMAIN RAS and IAS Servers S-1–5–21–1948120765-

2568877423–583830540–553

FOREIGN_DOMAIN\HelpServicesGroup FOREIGN_DOMAIN HelpServicesGroup S-1–5–21–1948120765-

2568877423–583830540–1000

FOREIGN_DOMAIN\TelnetClients FOREIGN_DOMAIN TelnetClients S-1–5–21–1948120765-2568877423–583830540–1002

FOREIGN_DOMAIN\DnsAdmins FOREIGN_DOMAIN DnsAdmins S-1–5–21–1948120765-2568877423–583830540–1117

FOREIGN_DOMAIN\DnsUpdateProxy FOREIGN_DOMAIN DnsUpdateProxy S-1–5–21–1948120765-2568877423–583830540–1118

FOREIGN_DOMAIN\Domain Admins FOREIGN_DOMAIN Domain Admins S-1–5–21–1948120765-2568877423–583830540–512

FOREIGN_DOMAIN\Domain Computers FOREIGN_DOMAIN Domain Computers S-1–5–21–1948120765-2568877423–583830540–515

FOREIGN_DOMAIN\Domain Controllers FOREIGN_DOMAIN Domain Controllers S-1–5–21–1948120765-2568877423–583830540–516

FOREIGN_DOMAIN\Domain Guests FOREIGN_DOMAIN Domain Guests S-1–5–21–1948120765-2568877423–583830540–514

FOREIGN_DOMAIN\Domain Users FOREIGN_DOMAIN Domain Users S-1–5–21–1948120765-2568877423–583830540–513

FOREIGN_DOMAIN\Enterprise Admins FOREIGN_DOMAIN Enterprise Admins S-1–5–21–1948120765-2568877423–583830540–519

FOREIGN_DOMAIN\Group Policy Creator Owners FOREIGN_DOMAIN Group Policy Creator Owners S-1–5–21–1948120765-2568877423–583830540–520

FOREIGN_DOMAIN\Schema Admins FOREIGN_DOMAIN Schema Admins S-1–5–21–1948120765-2568877423–583830540–518

FOREIGN_DOMAIN\Shared FOREIGN_DOMAIN Shared S-1–5–21–1948120765-2568877423–583830540–1113
```

#### Processes

WMIC can collect a list of the currently running processes similar to what you’d see in “Task Manager” using the following command

```powershell
wmic process list
```

Note that some of the WMIC built-ins can also be used in “brief” mode to display a less verbose output. The process built-in is one of these, so you could collect more refined output using the command

```powershell
wmic process list brief
```

Start an Application

```powershell
wmic process call create "calc.exe"
```

Terminate an Application

```powershell
wmic process where name="calc.exe" call terminate
```

Change Process Priority

```powershell
wmic process where name="explorer.exe" call setpriority 64
```

Get List of Process Identifiers

```powershell
wmic process where (Name='svchost.exe') get name,processid
```

Find a specific Process

```powershell
wmic process list brief find "cmd.exe"
```

#### System Information and Settings

You can collect a listing of the environment variables (including the PATH) with this command

```powershell
wmic environment list
```

OS/System Report HTML Formatted

```powershell
wmic /output:c:os.html os get /format:hform
```

Products/Programs Installed Report HTML Formatted

```powershell
wmic /output:c:product.html product get /format:hform
```

Turn on Remoted Desktop Remotely

```powershell
Wmic /node:"servername" /user:"user@domain" /password: "password" RDToggle where ServerName="server name" call SetAllowTSConnections 1
```

Get Server Drive Space Usage Remotely

```powershell
WMIC /Node:%%A LogicalDisk Where DriveType="3" Get DeviceID,FileSystem,FreeSpace,Size /Format:csv MORE /E +2 >> SRVSPACE.CSV
```

Get PC Serial Number

```powershell
wmic /node:"HOST" bios get serialnumber
```

Get PC Product Number

```powershell
wmic /node:"HOST" baseboard get product
```

Find stuff that starts on boot

```powershell
wmic STARTUP GET Caption, Command, User
```

Reboot or Shutdown

```powershell
wmic os where buildnumber="2600" call reboot
```

Get Startup List

```powershell
wmic startup list full
```

Information About Harddrives

```powershell
wmic logicaldisk where drivetype=3 get name, freespace, systemname, filesystem, size, volumeserialnumber
```

Information about os

```powershell
wmic os get bootdevice, buildnumber, caption, freespaceinpagingfiles, installdate, name, systemdrive, windowsdirectory /format:htable > c:osinfo.htm
```

Information about files

```powershell
wmic path cim_datafile where "Path='\windows\system32\wbem\' and FileSize>1784088" > c:wbemfiles.txt
```

#### User and Groups

Local user and group information can be obtained using these commands:

```powershell
wmic useraccount list
```

```powershell
wmic group list
```

```powershell
wmic sysaccount list
```

For domain controllers, this should provide a listing of all user accounts and groups in the domain. The “sysaccount” version provides you with system accounts built-in and otherwise,which is useful for any extra accounts that may have been added by rootkits.

Identify any local system accounts that are enabled (guest, etc.)

```powershell
wmic USERACCOUNT WHERE "Disabled=0 AND LocalAccount=1" GET Name
```

Number of Logons Per USERID

```powershell
wmic netlogin where (name like "%skodo") get numberoflogons
```

Get Domain Names And When Account PWD set to Expire

```powershell
WMIC UserAccount GET name,PasswordExpires /Value
```

#### Patch Management

Need to know if there are any missing patches on the system? WMIC can help you find out with this command

```powershell
wmic qfe list
```

The QFE here stands for “Quick Fix Engineering”.

The results also include the dates of install should that be needed from an auditing standpoint.

#### Shares

Enumeration of all of the local shares can be collected using the command

```powershell
wmic share list
```

The result will also include hidden shares (named with a $ at the end)

Find user-created shares (usually not hidden)

```powershell
wmic SHARE WHERE "NOT Name LIKE '%$'" GET Name, Path
```

#### Networking

Use the following command to extract a list of network adapters and IP address information

```powershell
wmic nicconfig list
```

Get Mac Address

```powershell
wmic nic get macaddress
```

Update static IP address

```powershell
wmic nicconfig where index=9 call enablestatic("192.168.16.4"), ("255.255.255.0")
```

Change network gateway

```powershell
wmic nicconfig where index=9 call setgateways("192.168.16.4", "192.168.16.5"),(1,2)
```

Enable DHCP

```powershell
wmic nicconfig where index=9 call enabledhcp
```

Get List of IP Interfaces

```powershell
wmic nicconfig where IPEnabled='true'
```

#### Services

WMIC can list all of the installed services and their configurations using this command

```powershell
wmic service list
```

the output will include the full command used for starting the service and its verbose description.

Service Management

```powershell
wmic service where caption="DHCP Client" call changestartmode "Disabled"
```

Look at services that are set to start automatically

```powershell
wmic SERVICE WHERE StartMode="Auto" GET Name, State
```

Services Report on a Remote Machine HTML Formatted

```powershell
wmic /output:c:services.htm /node:server1 service list full / format:htable
```

Get Startmode of Services

```powershell
Wmic service get caption, name, startmode, state
```

Change Start Mode of Service

```powershell
wmic service where (name like "Fax" OR name like "Alerter") CALL ChangeStartMode Disabled
```

Get Running Services Information

```powershell
Wmic service where (state="running") get caption, name, startmode, state
```

#### WMIC in Forensics

Record the run-time command executed and runtime configuration all in one XML file. A recorded session might look something like this.

```powershell
wmic /record:users_list.xml useraccount list
```

Obtain a Certain Kind of Event from Eventlog

```powershell
wmic ntevent where (message like "%logon%") list brief
```

Clear the Eventlog

```powershell
wmic nteventlog where (description like "%secevent%") call cleareventlog
```

Retrieve list of warning and error events not from system or security logs

```powershell
WMIC NTEVENT WHERE “EventType < 3 AND LogFile != ‘System’ AND LogFile != ‘Security’” GET LogFile, SourceName, EventType, Message, TimeGenerated /FORMAT:”htable.xsl”:” datatype = number”:” sortby = EventType” > c:appevent.htm
```
