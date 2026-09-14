# Remediation for Attack 2
- The security risk exposed in **Attack 2** was likely due to the fact that there isn't a special rule in place for the **amaljp** account in regards to user authentication in the SSH configuration.
- In order to investigate the SSH configuration, the following command was executed to open the **sshd_config** for editing:

  ***sudo nano /etc/ssh/sshd_config***

- ***Screenshot***

- As is clearly stated in the configuration file, ***PasswordAuthentication*** is set to ***yes***. Hence, globally the SSH policy for user authentication is that **PasswordAuthentication** is a possible option.
- Because of this, the Ubuntu password associated with the **amaljp** admin account can be used to gain access it.
- In order to remediate this security risk, a specific rule must be established for **amaljp**. At the bottom of the **sshd_config** after the Subsystem and global settings, the following is added:

- ***Screenshot***
- To test whether the specific authentication settings we established for **amaljp** the following command is executed:

  ***COMMAND***

  - Now to ensure that the **alice** and **bob** user accounts utilize the globally defined authentication settings the following commands are executed:
 
    ***COMMAND FOR ALICE***
    - ***Screenshot***
    ***COMMAND FOR BOB***
    - ***SCreenshot***
   
    - It is clear that **amaljp** has the SSH only authentication set up and the **alice** and **bob** accounts follow the globally enforced authentication policy.
