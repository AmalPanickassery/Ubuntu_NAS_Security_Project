# Remediation for Attack 2
- The security risk exposed in **Attack 2** was likely due to the fact that there isn't a special rule in place for the **amaljp** account in regards to user authentication in the SSH configuration.
- In order to investigate the SSH configuration, the following command was executed to open the **sshd_config** for editing:

  ***sudo nano /etc/ssh/sshd_config***

- ***Screenshot***

- As is clearly stated in the configuration file, ***PasswordAuthentication*** is set to ***yes***. Hence, globally the SSH policy for user authentication is that **PasswordAuthentication** is a possible option.
- Because of this, a password can be utilized to login into the **amaljp** admin account.
