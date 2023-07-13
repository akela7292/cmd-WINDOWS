# cmd-WINDOWS
cmd WINDOWS
Remotely determine logged in user

wmic /node:remotecomputer computersystem get username
List running processes

wmic process list brief
Kill a process

wmic process where name="cmd.exe" delete
Determine open shares

net share
wmic share list brief
Determine IP address

ipconfig
Get a new IP address

ipconfig /release
ipconfig /renew
Remotely display machine’s MAC address

wmic /node:machinename nic get macaddress
Remotely list running processes every second

wmic /node:machinename process list brief /every:1
Remotely display System Info

wmic /node:machinename computersystem list full
Disk drive information

wmic diskdrive list full
wmic partition list full
Bios info

wmic bios list full
List all patches

wmic qfe
Look for a particular patch

wmic qfe where hotfixid="KB958644" list full
Remotely List Local Enabled Accounts

wmic /node:machinename USERACCOUNT WHERE "Disabled=0 AND LocalAccount=1" GET Name
Start a service remotely

wmic /node:machinename 4 service lanmanserver CALL Startservice
sc \\machinename start lanmanserver
List services

wmic service list brief
sc \\machinename query
Disable startup service

sc config example disabled
List user accounts

wmic useraccount list brief
Enable RDP remotely

wmic /node:"machinename 4" path Win32_TerminalServiceSetting where AllowTSConnections=“0” call SetAllowTSConnections “1”
List number of times a user logged on

wmic netlogin where (name like "%adm%") get numberoflogons
Query active RDP sessions

qwinsta /server:192.168.1.1
Remove active RDP session ID 2

rwinsta /server:192.168.1.1 2
Remotely query registry for last logged in user

reg query "\\computername\HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\WinLogon" /v DefaultUserName
List all computers in domain “blah”

dsquery computer "OU=example,DC=blah" -o rdn -limit 6000 &gt; output.txt
Reboot

shutdown /r /t 0
Shutdown

shutdown /s /t 0
Remotely reboot machine

shutdown /m \\192.168.1.1 /r /t 0 /f
Copy entire folder and its contents from a remote source to local machine

xcopy /s \\remotecomputer\directory c:\local
Find location of file with string “blah” in file name

dir c:\ /s /b | find "blah"
Spawn a new command prompt

start cmd
Determine name of a machine with known IP

nbtstat -A 192.168.1.1
Find directory named blah

dir c:\ /s /b /ad | find "blah"
Command line history

F7
Determine the current user (aka whoami Linux equivalent)

echo %USERNAME%
Determine who is apart of the administrators group

net localgroup administrators
Add a user where travis is the username and password is blah

net user travis blah /add
Add user travis to administrators group

net localgroup administrators travis /add
List user accounts

net user
Map a network share with a given drive letter of T:

net use T: \\serverNameOrIP\shareName
List network connections and the programs that are making those connections

netstat -nba
Display contents of file text.txt

type text.txt
Edit contents of file text.txt

edit text.txt
Determine PC name

hostname
Run cmd.exe as administrator user

runas /user:administrator cmd
Uninstall a program, Symantec in this case ;-}

wmic product where “description=’Symantec’ ” uninstall
Determine whether a system is 32 or 64 bit

wmic cpu get DataWidth /format:list
Powershell one liner download file

(new-object System.Net.WebClient).Downloadfile("http://example.com/file.txt", "C:\Users\Travis\file.txt")
Information about OS version and other useful system information

systeminformation
Startup applications

wmic startup get caption,command
Recursively unzip all zip folders, you’ll need unzip.exe for this

FOR /R %a (*.zip) do unzip -d unzipDir "%a"
Query status of Windows Defender

sc query WinDefend
Powershell one liner to determine if Windows Defender and other services are running

Get-MpComputerStatus
Validate credentials against Active Directory

net use \\%userdnsdomain% /user:domain\user *
Delete net use connection

net use \\%userdnsdomain% /del
