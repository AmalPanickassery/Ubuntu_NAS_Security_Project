# Securtiy Testing
This section elaborates on the security testing/verification that was performed after the security hardening process in order to ensure that all the security changes have actually been implemented as expected. This is a very crucial step because without verifying the security measures, a system can not be deemed to be secure.

The following items were tested:
1. Shared directory permissions
2. Shared files permissions
3. Samba configuration
4. SSH configuration
5. SSH keys permissions
6. User home directories access

## Shared directory permissions
- The permissions of the shared NAS directory that had been created to store the files that uploaded to the NAS was checked by executing:
  
  ***ls -ld /srv/nas/shared***
  
  <img width="727" height="87" alt="Screenshot 2026-09-05 123145" src="https://github.com/user-attachments/assets/68234d51-f9d1-459e-afd3-4e8d5424eed9" />

- As expected after setting up the permissions, only **amaljp** and the users in the **family** group have complete access (i.e. rwx or rws)

## Shared files permissions
- The permissions of the files present on the shared NAS directory was checked by executing:

  ***ls -l /srv/nas/shared***

  <img width="776" height="191" alt="Screenshot 2026-09-05 123518" src="https://github.com/user-attachments/assets/19812a19-7528-4b24-9ce7-167c2cf09308" />

- Everything is as expected. The **owner** and permitted **group** have ***rw** access to the files and ***rwx*** and ***rws*** access to the directories on the NAS. 

## Samba configuration
- The permissions of the Samba configuration file was checked by executing:

  ***ls -l /etc/samba/smb.conf***

  <img width="755" height="45" alt="Screenshot 2026-09-05 160444" src="https://github.com/user-attachments/assets/fd40a0e1-b258-4d57-bc6e-ea98680773c0" />

- As expected, the permissions on the **smb.conf** file have been properly established. The **root** user is the only one that has ***rw*** rights, the **root** group and other users have only ***r***.


## SSH configuration
- The permissions of the SSH configuration file was checked by executing:

  ***ls -l /etc/ssh/sshd_config***

  <img width="747" height="45" alt="Screenshot 2026-09-05 160623" src="https://github.com/user-attachments/assets/ff72cc1a-3350-4602-8090-5feed4b7afa0" />

- As expected, the permissions for the **sshd_config** file have been properly established. The **root** user is the only one that has ***rw*** rights, the **root** group and other users have only ***r***.


## SSH keys
- The permissions of the hidden ssh directory was checked by executing:

  ***ls -l ~/.ssh***

  <img width="713" height="70" alt="Screenshot 2026-09-05 160808" src="https://github.com/user-attachments/assets/dd568746-3487-4338-8add-5e6add8e129f" />

- As expected only **amaljp** has **rw** access the ssh keys stored on the server. Every other user and group has no access. This helps reduce the chance of viewing or editing the keys by random users that aren't admins.


## User home directories
- The permissions of the user home directories was checked by executing:

  ***ls -ld /home/****

  <img width="701" height="95" alt="Screenshot 2026-09-05 160856" src="https://github.com/user-attachments/assets/9df5ccd9-88ba-4914-a857-cca9535fbe78" />

- As expected, the users have full access (i.e. ***rwx***) to their corresponding user home directory. This ensures other users can't view to edit another user's permissions etc.



  



  


