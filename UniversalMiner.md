# UniversalMiner

| ATT&CK ID | Activity Description | Observables |
|---|---|---|
| T1091: Replication Through Removable Media | The malware’s infection chain starts with a .LNK file on a USB drive, which the user manually executes. | D:\<USB_Name>.lnk |
| T1204.002: User Execution: Malicious File	| The .LNK file is manually executed by the user, requiring user interaction.	| D:\<USB_Name>.lnk |
| T1059.005: Command and Scripting Interpreter: Visual Basic | The .LNK file executes a .VBS file, which drops another four files: two .DAT files (which are really .DLL files), one .VBS file, and one .BAT file. | "C:\Windows\System32\WScript.exe" "D:\rootdir\<*.VBS>" |
| T1036.005: Masquerading: Match Legitimate Name or Location | The .BAT file creates a new folder, masqueraded as Windows System32, but with a space character in the file path. | mkdir "\\?\C:\Windows \System32" |
| T1574.002: Hijack Execution Flow: DLL Side-Loading | The malware copies the printui.exe file from the original Windows System32 folder to the newly created fake folder as well as one of the .DAT files. Then, it renames the .DAT file to printui.dll and executes using printui.exe. |	xcopy "C:\Windows\System32\printui.exe" "C:\Windows \System32" /Y | 
| T1547.001: Boot or Logon Autostart Execution: Registry Run Keys / Startup Folder | The malware uses a registry key and adds the name of the .DAT file as a newly created service.	| `reg add HKLM\SYSTEM\CurrentControlSet\services\<*.DAT>\Parameters /v ServiceDll /t REG_EXPAND_SZ /d "C:\Windows\System32\<*.DAT>" /f` | 
| T1569.002: System Services: Service Execution	|The .DAT file is added as a newly created service using sc.exe so that it restarts if the system is rebooted. | `sc create <*.DAT> binPath = "C:\Windows\System32\svchost.exe -k DcomLaunch" type= own start= auto` |
| T1053: Scheduled Task/Job	| The malware runs a file called console_zero.exe in the Windows System32 folder and adds it as a scheduled task.	| console_zero.exe |
| T1016: System Network Configuration Discovery	| The malware performs an HTTP request to the site IPinfo[.]io to gather the system's network configuration. | hxxps://ipinfo[.]io/json |
| T1105: Ingress Tool Transfer | This malware checks if the .DAT file is running. If it is not, it will download another copy from either GitHub or an adversary-created domain using Curl.	| libcurl.dll |
| T1068: Exploitation for Privilege Escalation | The malware also drops and exploits a vulnerability in the kernel driver for Windows for privilege escalation before loading the cryptocurrency miner. This trick is known as Bring-Your-Own-Vulnerable-Driver (BYOVD).	| WinRing0x64.sys |
| T1496.001: Resource Hijacking: Compute Hijacking | The final step of this multi-stage infection chain is to download the XMRig cryptocurrency mining program.	| xmrig.exe |

### References:
- https://mrl.cert.gov.az/az/articles/view/125
- https://x.com/ShanHolo/status/1851528395315630273
