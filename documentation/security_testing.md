# Securtiy Testing
This section elaborates on the security testing/verification that was performed after the security hardening process in order to ensure that all the security changes have actually been implemented as expected. This is a very crucial step because without verifying the security measures, a system can not be deemed to be secure.

The following items were tested:
1. Shared directory permissions
2. Shared files permissions
3. Parent directories permissions
4. Samba configuration
5. SSH configuration
6. SSH keys permissions
7. User home directories access

## Shared directory permissions
- The permissions of the shared NAS directory that had been created to store the files that uploaded to the NAS was checked by executing:
  
  ***ls -ld /srv/nas/shared***
  
  <img width="727" height="87" alt="Screenshot 2026-09-05 123145" src="https://github.com/user-attachments/assets/68234d51-f9d1-459e-afd3-4e8d5424eed9" />

## Shared files permissions
- The permissions of the files present on the shared NAS directory was checked by executing:

  ***ls -l /srv/nas/shared***

  <img width="776" height="191" alt="Screenshot 2026-09-05 123518" src="https://github.com/user-attachments/assets/19812a19-7528-4b24-9ce7-167c2cf09308" />

## Samba configuration
- The permissions of the Samba configuration file was checked by executing:

  ***ls -l /etc/samba/smb.conf***

## SSH configuration
- The permissions of the SSH configuration file was checked by executing:

  ***ls -l /etc/ssh/sshd_config***

## SSH keys
- The permissions of the hidden ssh directory was checked by executing:

  ***ls -l ~/.ssh***

## User home directories
- The permissions of the user home directories was checked by executing:

  ***ls -ld /home/****


  



  


