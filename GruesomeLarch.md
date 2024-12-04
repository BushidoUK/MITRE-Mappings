# GruesomeLarch
- Publicly known as APT28, Forest Blizzard, Sofacy, Fancy Bear, among other names
- Publicly attributed to Russian GRU Unit 26165

| ATT&CK ID |	Activity Description | Observables | 
|---|---|---|
| T1110.003: Password Spraying | The attacker used password spraying attacks against a public-facing service to validate credentials. | N/A | 
| T1078: Valid Accounts | The attacker used valid domain usernames and passwords to authenticate to Wi-Fi networks and/or VPN networks. | N/A | 
| T102: Remote Services | The attacker used the credentials validated from password spraying to authenticate to the target’s VPN, which did not have MFA enabled. | N/A |
| T1560: Archive Collected Data | The attacker used PowerShell commands indicating in-line compression of files. 	| Compress-Archive -DestinationPath C:\ProgramData\out.zip” |
| T1068: Exploitation for Privilege Escalation | The attacker used a post-compromise tool named GooseEgg the exploits the Windows Print Spooler service. | Servtask.bat, Wayzgoose52.dll, DefragmentSrv.exe |
| T1006: Direct Volume Access | The attacker created a volume shadow copy to steal the active directory database. | vssadmin create shadow /for C: /quiet |
| T1003.003: OS Credential Dumping: NTDS | The attacker stole the active directory database by copying the NTDS.dit file. | copy NTDS.dit |
| T1074.002: Data Staged: Remote Data Staging | The attacker staged data in directories on a public-facing webserver before downloading it. | N/A |
| T1016.002: System Network Configuration Discovery: Wi-Fi Discovery | The attacker used a custom PowerShell script to examine the available networks within range of its wireless. | Wlanapi.dll |
| T1562.004: Impair Defenses: Disable or Modify System Firewall | The attacker used the Windows utility netsh to set up a series of port-forwards that allowed them to reach the target systems. | cmd.exe /C netsh advfirewall firewall add rule name="Remote Event Log Management SMB" | 
| T1561.001: Disk Wipe: Disk Content Wipe | During the intrusion, the attacker removed files they created, making use of an inbuilt Windows tool, Cipher.exe. | cmd.exe /c cipher /W:C |

### References:
- https://www.volexity.com/blog/2024/11/22/the-nearest-neighbor-attack-how-a-russian-apt-weaponized-nearby-wi-fi-networks-for-covert-access/
- https://github.com/volexity/threat-intel/blob/main/2024/2024-11-22%20GruesomeLarch/wifi_ps1_redacted.cs
- https://www.wired.com/story/russia-gru-apt28-wifi-daisy-chain-breach/
- https://www.microsoft.com/en-us/security/blog/2024/04/22/analyzing-forest-blizzards-custom-post-compromise-tool-for-exploiting-cve-2022-38028-to-obtain-credentials/
- https://attack.mitre.org/groups/G0007/
