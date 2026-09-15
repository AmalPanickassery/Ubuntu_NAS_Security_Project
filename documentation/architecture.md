# Lab Architecture Diagram
The following is the project's architecture diagram:

<img width="1542" height="932" alt="NAS_Architecture_3_PNG drawio" src="https://github.com/user-attachments/assets/31cb8715-c49c-4a29-9e9c-7dc865a86e04" />


## Windows Host

- The Windows Host machine is the physical machine that runs **Oracle VirtualBox**.
- **VirtualBox** hosts two VM's, the **Ubuntu Server VM** (i.e. the NAS), and the **Kali Linux VM** which is used to perform simulated attacks on the NAS.

## NAS Users
- There are three users on the Ubuntu Server. The **amaljp** account is the only **admin** account, whereas **alice** and **bob** are **standard user** accounts.
- **amaljp** can only be accessed when using the **Windows** machine since it contains the **private key** linked to the account. Both the private key and the passphrase have to be entered in order to be authenticated.
- The **alice** and **bob** accounts can be accessed via the traditional **username** and **password** combination.

## Ubuntu Server VM

- The Ubuntu Server utilizes a UFW on which only the required services are running.
- The two main services that pertain to the NAS are: **Samba (SMB)** and **OpenSSH**.
- **Samba** is the service utilized to ensure that file sharing can be performed. It is essentially the backbone of the NAS. Only the users that are apart of the group called **family** can access the shared files.
- **OpenSSH** is the service that allows for the different NAS users to connect remotely.

## Shared Storage

- The **shared** directory that contains all the shared files and folders is **/srv/nas/shared**

## Connectivity and Exposure

- The NAS is not exposed to the internet and is hosted on the **LAN** (Local Area Network)


