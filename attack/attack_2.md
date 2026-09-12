# Attack 2 (Bypass Admin Account SSH)
- In this scenario, the attacker is in possession of the credentials of the **amaljp** account, which is an admin account on the Ubuntu server that hosts the NAS.
- As the attacker, I used the Kali VM (which is a trusted IP) to utilize the credentials to gain access in order to conduct malicious activity.
- First and foremost as the attacker, I checked whether the Kali VM was able to reach the SSH service by executing the following command:

  ***nmap -p 22 -sV 192.168.1.xx**

- **nmap**: Scans the target machine
- **-p 22**: Scans only TCP port 22, which is the standard SSH port.
- **-sV**: Used to identify the service and it's version that's running on the port.

- ***Screenshot***

- After this I attempted to login to the **amaljp** account via the Kali VM by using the stolen credentials. The purpose of setting up the SSH keys for the Windows host machine was to ensure that the user can only login to the **amaljp** account using the SSH key on the Windows machine. A passphrase was also implemented in case the SSH were compromised (which is unlikely but the risk is never 0).
- I used the following command in Kali to attempt to SSH into the Ubuntu server:

  ***ssh amaljp@192.168.1.xx***

- ***Screenshot***

- As you can see, the user is prompted to enter the **amaljp** account's password. Hence, the SSH keys aren't being utilized for authentication as we have intended in order to increase the security on the admin account.
- This must be remediated as it undermines the security measures we established in order increase admin security.
