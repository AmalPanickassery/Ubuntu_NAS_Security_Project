# Attack 1 (Phase 2): SMB Enumeration and Unauthenticated login

Since the major service that's running on the NAS is Samba, it is the most relevant service to attempt an attack on.

## Step 1: Unauthenticated Attacker test
- In this step, I tested whether an unauthenticated attacker can discover the Samba shares on the NAS. To do this, the following command was utilized:

***smbclient -L // 192.168.1.xx -N***

- ***Screenshot***

- It is clear from the output that the Kali VM was able to enumerate the shares without providing a password.
- Even though the Kali VM's IP address is trusted in the server's UFW rules, it should only be allowed to attempt to connect but it shouldn't be permitted to enumerate the Samba shares without authentication.

## Step 2: Attempt login
