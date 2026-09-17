# Remediation for Attack 2
- The security risk exposed in **Attack 2** was likely due to the fact that there isn't a special rule in place for the **amaljp** account in regards to user authentication in the SSH configuration.
- In order to investigate the SSH configuration, the following command was executed to open the **sshd_config** for editing:

  ***sudo nano /etc/ssh/sshd_config***


<img width="769" height="77" alt="remediation2_scsht_1" src="https://github.com/user-attachments/assets/07779fb8-2f6f-4401-899c-fff0ac97ed43" />



- As is clearly stated in the configuration file, ***PasswordAuthentication*** is set to ***yes***. Hence, globally the SSH policy for user authentication is that **PasswordAuthentication** is a possible option.
- Because of this, the Ubuntu password associated with the **amaljp** admin account can be used to gain access it.
- In order to remediate this security risk, a **specific rule** must be established for **amaljp**. At the bottom of the **sshd_config** after the Subsystem and global settings, the following is added:


<img width="645" height="337" alt="remediation2_scsht_2" src="https://github.com/user-attachments/assets/71173605-d7bc-479e-ae09-cf3c860e627b" />


- To test whether the specific authentication settings we established for **amaljp** the following command is executed in the Kail Terminal:

  ***ssh amaljp@192.168.1.xx***


<img width="437" height="60" alt="remediation2_scsht_3" src="https://github.com/user-attachments/assets/05d34d31-c83a-4cec-a48f-f42b425faf49" />


- Now to ensure that the **alice** and **bob** user accounts utilize the **globally defined** authentication settings the following commands are executed:
 
***ssh alice@192.168.1.xx***


<img width="551" height="77" alt="remediation2_scsht_4" src="https://github.com/user-attachments/assets/05b60f79-5301-45ee-8313-555633351c90" />


***ssh bob@192.168.1.xx***


<img width="527" height="76" alt="remediation2_scsht_5" src="https://github.com/user-attachments/assets/43a5db68-61a9-4f74-85a2-e16739c1cb2d" />


- It is clear that **amaljp** has the **SSH key only** authentication set up and the **alice** and **bob** accounts follow the globally enforced **password authentication** policy.
