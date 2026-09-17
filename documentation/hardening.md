# Security Hardening
This section elaborates on the security hardening practices performed on the NAS to improve it's security posture and as a result reduce the attack surface of the system.
The hardening process involved the following steps:
1. Documenting the base system
2. Updating the system
3. Removal of unnecessary packages and services
4. Improving SSH security
5. Configuring the UFW
6. Securing Samba

## Documenting the base system
The base system was documented in the [security baseline](security_baseline.md) by recording the version and kernel of Ubuntu Server that was utilized, services that are running, open ports and the default UFW configuration.

## Updating the system
- Using the ***sudo apt update*** command, the list of available software packages was updated. These updates were then installed using the ***sudo apt upgrade*** command.
- The command ***sudo apt autoremove*** was used to remove packages that were automatically installed as dependencies but are no longer required.

## Removal of Unnecessary Packages and Services
- The ***apt-mark showmanual*** command was run to display all the explicitly installed packages.
- All of these packages are essential and hence should not be removed.
- The services whose utility required investigation in [Services](security_baseline.md#Services) are mentioned below:
### ModemManager
  - ModemManager is a system daemon in Linux that controls mobile broadband devices. It provides a unified way to configure and manage cellular modems.
  - The network connection for the NAS is provided by the **VirtualBox** virtual Ethernet adapter. Therefore, ModemManager is **not required**.
  - The presence of a cellular modem was also checked by running the ***mmcli -L*** command which resulted in ***No modems were found***.

  <img width="375" height="78" alt="image" src="https://github.com/user-attachments/assets/c17fb58f-0239-48a7-abfe-9e6cd40191a5" />

  
  - Due to these reasons, the ModemManager service was **disabled**.

### multipathd
  - multipathd is a system daemon that manages multiple paths to the same storage device. It is typically used with enterprise SAN/storage systems.
  - The Ubuntu server only uses a single disk setup and the presence of multipath devices was checked by running the ***sudo multipath -ll*** which resulted in no output being printed (which implies that no multipath storage devices were detected)


  <img width="492" height="55" alt="image" src="https://github.com/user-attachments/assets/e2f20fae-90a4-4cda-bf94-d4cb7906d8e8" />

    
  - Due to these reasons, the multipathd service was **disabled**.

### networkd-dispatcher
  - networkd-dispatcher is a system daemon in Linux that automatically runs scripts in response to network state changes.
  - Network connections are handled by systemd, so networkd-dispatcher isn't required and hence networkd-disptacher was **disabled**.

### udisks2
  - It is a headless backend daemon that manages USB devices, external hard drives, and SD cards effortlessly.
  - Allows for safe Ejecting and Unmounting from the desktop interface and hence left it **enabled**.


## SSH setup for Server admin user
- In order to reduce the risk of an attacker logging into the **amaljp** admin account with stolen credentials, I created a ssh key pair for the Windows machine using the ***ssh-keygen -t ed25519 -C "amalp@windows"*** command.
- During the key generation process, I was prompted to provide a passphrase.
- The ssh key generation produces a public and private key which is far more secure than normal password authentication.
- The Ubuntu server encrypts a **challenge string** using the Windows machine's public key. This string can only be decrypted by the corresponding private key.
- Once the challenge string is successfully **decrypted**, the connection is **established**.
- In the off chance that the keys or the machine that contains the keys is apprehended, the **passphrase** comes to the rescue. The passphrase must be entered to decrypt the encrypted private key before it is used on the challenge string.
- The public key was copied and stored in the newly created ***~/.ssh/authorized_keys*** directory on the Ubuntu server. The permissions for the ***~/.ssh*** was set to **700**. This means that the owner (which is the root) has **rwx** ***(Read, Write, Execute)*** privileges, whereas groups and other users have none.
- The permissions for ***/authorized_keys*** was set to 600. This means that the owner has **rw** ***(Read, Write)*** privileges, whereas groups, and other users have none.

## Configuring SSH
The following modifications were made to the ***/etc/ssh/sshd_config*** after making a copy of it:
  1. **PermitRootLogin** no:

  - Prevents the root account from logging in directly through SSH.
  - This way an attacker can't directly target a highly privileged root account. They have to first compromise a regular account and then obtain elevated privileges to access it.
  - Adds an additional security barrier.
  
  3. **PasswordAuthentication** yes:

  - Allows for password authentication (required for the standard user accounts i.e. **alice** and **bob**)
  
  4. **PubkeyAuthentication** yes:

  - Enables authentication using SSH public/private key pairs (required for authenticating the **amaljp** admin account)
  
  5. **X11Forwarding** no:

  - Prevents the SSH sessions from forwarding X11 graphical applications through the connection. This feature of the SSH isn't required since the NAS is running headless.
  - Reduces the number of SSH features available for misuse.
  
  6. **MaxAuthTries** 3:

  - It limits each SSH connection to three failed authentication attempts. This prevents **brute force** attacks.
  
  7. **LoginGraceTime** 30:

  - Gives the client 30 seconds to successfully authenticate before SSH terminates the connection.
  - This limits how long unauthenticated connections can remain open.
  - This helps prevent attackers from repeatedly opening SSH connections in order to consume server resources.
  
  8. **PermitEmptyPasswords** no:

  - Ensures that an account can't be accessed through SSH simply because it has no password configured.
  - It provides a safeguard against insecure account configurations.
  
  9. **PermitUserEnvironment** no:

  - Prevents users from supplying environment variables through SSH user-environment files.
  - This helps reduce the ability for users to influence the environment of their SSH sessions.
    
  10. **PrintMotd** no:

  - Prevents SSH from displaying the system's **Message of the Day** after login.
  - The **MOTD** might contain system details and network information and displaying this to every SSH user could provide attackers with information that would aid them in an attack.
    
  10. **MaxSessions** 2:

  - Limits each SSH connection to a maximum of two concurrent sessions. Just like **LoginGraceTime** it helps prevent excessive resource usage.
 
## Configuring the UFW
- The default incoming policy was set to **deny** if no rule matches. This was done by executing ***sudo ufw default deny incoming***.
- The default outgoing policy was set to **allow** if no rule matches. This was done by executing ***sudo ufw default allow outgoing***. Blocking all outgoing traffic would make basic administration difficult.
- Two rules were configured which allowed for tcp traffic from the **Windows Host** machine and the **Kali VM**:

  ***sudo ufw allow from <Windows_IP> to any port 22 proto tcp***
  
  ***sudo ufw allow from <Kali_IP> to any port 22 proto tcp***


## Securing Samba
- The UFW controls who can reach Samba. In order to control what that user is allowed to do once they reach Samba, we have to modify ***smb.conf**, which is Samba's configuration file.
- First, the configuration file was opened using the ***sudo nano /etc/samba/smb.conf*** command.
- The following edits were made to it:
  - **guest ok** = no
  - **valid users** = family
  - **hide unreadable** = yes
  - **create mask** = 0660
  - **directory mask** = 0770
  - **host allow** = 192.168.1.
 
- Here is a brief description of the purpose of each parameter:
  - **guest ok**: When this is set to ***no***, a user has to pass authentication before accessing the NAS.
  - **valid users**: Only the users mentioned will be allowed to access the NAS. We have set the value to ***family***, which is the group that has **amaljp**, **alice**, and **bob** as members. Hence, **amaljp**, **alice**, and **bob** will be granted access.
  - **hide unreadable**: Hides files from users if they don't have permission to read them.
 
  Insert Diagram of example here

  Let's say ***amal_private.txt*** was created by **amaljp** and has the permissions **700**. Since the second and third digits of the permission configuartion is set to **0**, that means that no group or other user can read, write or execute the file. So when **hide unreadable** is set to ***yes***, the file won't be visible to the users **alice** and **bob**. This adds a level of security since user's that don't have any privileges on a file won't even it see it appear on the shared folder on the NAS.

- **create mask**: When it is set to ***0660***, all newly created files will automatically have the ***0660*** permissions configuration. For example, if you create a new file named ***new_file.txt*** it's permissions will be set to **0660**. **0660** implies that the **owner** and permitted **group** can ***Read*** and ***Write***, but all other users can no permissions.
- **directory mask**: When it is set to ***0770***, all newly created directories will automatically have the ***0770*** permissions configuration. For example, if you create a new directory named ***new_dir*** it's permissions will be set to **0770**. **0770** implies that the **owner** and permitted **group** can ***Read***, ***Write***, and ***Execute***, but all other users have no permissions.
- **host allow**: When it is set to ***192.168.1.***, only clients whose IP address begins with **192.168.1.** can connect to this Samba service. This adds an extra level of security since only devices on the LAN can connect and access the shares.





