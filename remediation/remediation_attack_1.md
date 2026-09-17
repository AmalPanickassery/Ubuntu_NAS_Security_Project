# Remediation for Attack 1
- In order to perform the remediation we need to edit the **smb.conf** file, which is the Samba configuration. The configuration file is opened for editing using the following command:

  ***sudo nano /etc/samba/smb.conf***

- Under the **[NAS]** section of the configuration file, the following parameter is added:

  ***access based share enum = yes***

  <img width="447" height="335" alt="remediation1_scsht_1" src="https://github.com/user-attachments/assets/d54a995b-8aa2-4f19-a6d0-8bd8fc3996f9" />


- This parameter tells Samba to hide the share during enumeration when the connecting user isn't authorized to access it.
- Now to test whether the change has created the desired effect, the following command is executed:

  ***smbclient -L //192.168.1.xx -N***
  

<img width="642" height="161" alt="image" src="https://github.com/user-attachments/assets/840bb57b-87f0-44a8-8337-0d3a6499a934" />

 
- It is clear that the share is no longer visible without providing credentials. To test whether 
