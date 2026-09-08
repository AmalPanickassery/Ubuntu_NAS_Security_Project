# Attack 1 (Phase 2): SMB Enumeration

Since the major service that's running on the NAS is Samba, it is the most relevant service to attempt an attack on.

## Step 1: Unauthenticated Attacker test
- In this step, I tested whether an unauthenticated attacker can discover the Samba shares on the NAS. To do this, the following command was utilized:

***smbclient -L // 192.168.1.xx -N***

- 
