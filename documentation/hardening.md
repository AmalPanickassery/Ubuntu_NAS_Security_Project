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
  - Due to these reasons, the ModemManager service was **disabled**.

### multipathd
  - multipathd is a system daemon that manages multiple paths to the same storage device. It is typically used with enterprise SAN/storage systems.
  - The server only uses a single disk setup and the presence of multipath devices was checked by running the ***sudo multipath -ll*** which resulted in ***No multipath devices found***.
  - Due to these reasons, the multipathd service was **disabled**.

### networkd-dispatcher
  - networkd-dispatcher is a system daemon in Linux that automatically runs scripts in response to network state changes.
  - Network connections are handled by systemd, so networkd-dispatcher isn't required and hence networkd-disptacher was **disabled**.

### udisks2
  - It is a headless backend daemon that manages USB devices, external hard drives, and SD cards effortlessly.
  - Allows for safe Ejecting and Unmounting from the desktop interface and hence left it **enabled**.


## Improving SSH security
- In order to reduce the risk of stolen credentials when logging into the **amaljp** Linux admin account via the Windows host machine, I created a ssh key pair for the Windows machine using the ***ssh-keygen -t ed25519 -C "amalp@windows"*** command.
- During the key generation process, I was prompted to provide a passphrase.
- The ssh key generation produces a public and private key which is far more secure than normal password authentication.
- The server encrypts a **challenge string** using the public key. This string can only be decrypted by the corresponding private key.
- Once the challenge string is successfully **decrypted**, the connection is **established**.
- In the off chance that the keys or the machine that contains the keys is apprehended, the **passphrase** comes to the rescue. The passphrase must be entered to decrypt the encrypted private key before it is used on the challenge string.

## Configuring the UFW

## Securing Samba




