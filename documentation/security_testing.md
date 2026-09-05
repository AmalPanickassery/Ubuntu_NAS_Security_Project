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
- The permissions of the shared NAS directory that had been created to store the files that uploaded to the NAS was checked by executing the following command:
  
  ***ls -ld /srv/nas/shared***
  
  <img width="772" height="133" alt="Screenshot 2026-09-05 122842" src="https://github.com/user-attachments/assets/85a4d9d3-f5c2-49be-af87-2c70c6c48f73" />

  


