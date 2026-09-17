# Attack 1 (Phase 2): SMB Enumeration and Unauthenticated login

Since the major service that's running on the NAS is Samba, it is the most relevant service to attempt an attack on.

## Step 1: Unauthenticated Attacker test
- In this step, I tested whether an unauthenticated attacker can discover the Samba shares on the NAS. To do this, the following command was utilized:

***smbclient -L // 192.168.1.xx -N***

<img width="762" height="232" alt="smb_enum_1" src="https://github.com/user-attachments/assets/182357df-a597-4dcc-a962-ffaab9469f31" />


- It is clear from the output that the Kali VM was able to **enumerate** the shares without providing a **password**.
- Even though the Kali VM's IP address is **trusted** in the server's UFW rules, it should only be allowed to attempt to connect but it **shouldn't** be permitted to enumerate the Samba shares without authentication.

## Step 2: Unauthenticated Samba share access
- In this step, I checked whether the shares are accessible without providing credentials. To do this, the following command was executed:

  ***smbclient //192.168.1.xx/NAS -N***

<img width="372" height="125" alt="smb_access_test" src="https://github.com/user-attachments/assets/a7a389a7-9d9d-4760-ba05-c92717223156" />

- The ***NT_STATUS_ACCESS_DENIED*** indicates that the **guest ok = no** parameter in the Samba configuration file (i.e. smb.conf) is working as intended. The **guest ok = no** ensures that users must authenticate before accessing the share. 

## Findings from this Attack
- Attacker was able to enumerate share names without credentials, but could not access the protected shares.
- **Severity:** Low
- **Remediation goal:** Prevent unauthenticated share enumeration. [Remediation for Attack 1](remediation_attack_1.md)
