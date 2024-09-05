# Forensic
Forensic testing notes

Windows Event Logs (via Command Line)

List all event logs
•	C:\> wevtutil el
o	Examples of important logs to retrieve are shown below, but consider reviewing and exporting others if time permits 

Export System, Security, Application, PowerShell, and RDP session logs, and save each .evtx file to C:\Temp (or change C:\Temp to desired output location)
•	C:\> wevtutil epl System C:\Temp\system_log.evtx
•	C:\> wevtutil epl Security C:\Temp\security_log.evtx
•	C:\> wevtutil epl Application C:\Temp\application_log.evtx
•	C:\> wevtutil epl “Windows PowerShell” C:\Temp\powershell_log.evtx
•	C:\> wevtutil epl "Microsoft-Windows-TerminalServices-LocalSessionManager/Operational" C:\Temp\rdpsession_log.evtx


Web Browser History

Firefox
•	C:\Users\<Username>\AppData\Roaming\Mozilla\Firefox\Profiles
o	Back up the entire ‘Profiles’ folder for analysis

Chrome
•	C:\Users\<Username>\AppData\Local\Google\Chrome\User Data\Default
o	Back up the entire ‘Default’ folder for analysis

Edge
•	C:\Users\<Username>\AppData\Local\Microsoft\Edge\User Data\Profile 1
•	Alternatively, ‘Profile 1’ may be named ‘Default’ or ‘Profile 2’ or something else…
o	Back up the entire ‘Default’ or ‘Profile #’ folder for analysis


Windows Defender

Log Path
•	C:\ProgramData\Microsoft\Windows Defender
o	Consider backing up entire folder for analysis


Windows Firewall

Log Path (if logging is enabled, but may not be)
•	C:\Windows\System32\LogFiles\Firewall\pfirewall.log
Outlook PST/Data Files

Data Path
•	C:\Users\<Username>\AppData\Local\Microsoft\Outlook
o	Filetype may be .pst, .ost, or .nst (retrieve all if needed)
o	If this path is wrong, do the following
1.	Open Outlook
2.	Go to File (top left) > Account Settings > Account Settings
3.	Click the “Data Files” tab
4.	Review the path in the “Location” field for the appropriate mailbox


General Data Collection (via Command Line)

View all active connections (ports, IPs) and save to C:\Temp
•	C:\> netstat -a > C:\Temp\netstat_export.txt
o	May appear to hang for several minutes. Netstat can take some time to run completely

View scheduled tasks and save to C:\Temp
•	C:\> schtasks > E:\Temp\scheduledtasks_export.txt

Get running processes, save to C:\Temp
•	C:\> wmic /output:E:\Temp\process_export.txt process get Caption,Description,Processid,ParentProcessID,Commandline,ReadOperationCount,WriteOperationCount
o	More verbose results via WMIC
•	C:\> tasklist > E:\Temp\tasklist_export.txt
o	Easier to read at a glance

Get all installed software, save to C:\Temp
•	C:\> wmic /output:E:\Temp\software_export.txt product get name,version

Get system information, save to C:\Temp
•	C:\> systeminfo > E:\Temp\systeminfo_export.txt

Get current user’s information, group memberships, privileges
•	C:\> whoami /all > E:\Temp\whoami_export.txt
•	C:\> net user “username” > E:\Temp\userinfo_export.txt
o	Useful for reviewing current user’s info, or other user’s info

Get local user and group information, save to C:\Temp
•	C:\> net user > E:\Temp\localuser_export.txt
•	C:\> net localgroup > E:\Temp\localgroups_export.txt
•	C:\> net localgroup administrators > E:\Temp\localadmin_export.txt
o	Consider reviewing/exporting group memberships of other interesting groups
1.	Backup Operators
2.	Remote Desktop Users
•	C:\> set > E:\Temp\set_export.txt
o	Gets user environment variables, useful for identifying suspicious files added to PATH or others

Get domain user and group information, save to C:\Temp
•	C:\> net user /domain > E:\Temp\domainusers_export.txt
•	C:\> net group /domain > E:\Temp\domaingroups_export.txt
•	C:\> net group “Domain Admins” /domain > E:\Temp\domainadmin_export.txt
o	Consider exporting group memberships of other interesting domain groups
