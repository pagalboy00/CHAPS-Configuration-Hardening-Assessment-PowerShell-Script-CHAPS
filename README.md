# CHAPS-Configuration-Hardening-Assessment-PowerShell-Script-CHAPS.
# CHAPS Assessment Steps
Running CHAPS may be confusing. The following list is a simple process for running an assessment to obtain configuration / hardening information from a Windows workstation or server. The first set of steps are scripts that can be used to gather information about the system using Administrator privileges on the local system. None of these checks will trigger anti-virus as long as the PowerShell execution policy is set to ```bypass```. The steps marked **AV TRIGGER** will trigger Windows Defender and, possibly, other AV / EDR solutions. These steps should be run as a local user, NOT Administrator, to limit false positives for Elevation of Privilege (EoP) vulnerabilities.
# Start 
git clone https://github.com/cutaway-security/chaps.git
# 1. Run CHAPS
## Start Web Server

On Linux system with CHAPS and other tools installed, note the IP address and start a Python web server. For this example, all tools are installed in the user's home directory in a subdirectory named chaps.
```
cd ~/chaps
ip addr
python3 -m http.server 8181
```
2.In Window using wsl command
```
cd ~/Chaps
wsl
ip addr
python3 -m http.server 8181
```

## Start Powershell or Windows Terminal as Administrator

Locate PowerShell or Windows Terminal in start menu, hold shift, right click, and select "Run as administrator".

## Allow Powershell to run scripts

```Set-ExecutionPolicy Bypass -scope Process```

## Run Chaps 

```
IEX (New-Object Net.WebClient).DownloadString('http://<web server IP>:8181/chaps/chaps.ps1')

```
```
.\chaps-powersploit.ps1
```


## Review CHAPS Tool Output 
Check the user's AppData temp directory. In a Windows Explorer terminal, type the following in the address bar. Find the latest run of CHAPS and check output.
or
windows + r

```%temp%```


## Store and delete old runs

**DO NOT SKIP** Do not leave old CHAPS and tool runs on the system. This information is valuable for attackers. If they can download these files, they don't have to run the queries on the local system and the network again. We want to force attackers to gather this information because we can detect that activity in Windows Event logs and network traffic. **DO NOT SKIP** 
