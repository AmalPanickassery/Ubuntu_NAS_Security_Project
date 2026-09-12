# Remediation for Attack 1
- In order to perform the remediation we need to edit the **smb.conf** file, which is the Samba configuration. The configuration file is opened for editing using the following command:

  ***sudo nano /etc/samba/smb.conf***

- Under the **[NAS]** section of the configuration file, the following parameter is added:

  ***access based share enum = yes***

- This parameter tells Samba to hide the share during enumeration when the connecting user isn't authorized to access it.
- Now to test whether the change has created the desired effect, the following command is executed:

  ***smbclient -L //192.168.1.xx -N***

- ***Screenshot***
- It is clear that the share is no longer visible without providing credentials. To test whether 
