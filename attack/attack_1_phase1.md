# Attack 1 (Phase 1): Network Reconnaissance 
The following steps elaborate the Attack 1 process:

## Step 1: Test the connectivity between Kali VM and the NAS
- In order to test whether the Kali VM can connect to the NAS, I executed the following command:

  ***ping -c 4 192.168.1.xx***

- The **-c** stands for count and it is a flag that tells the **ping** utility to stop after sending a specific number of packets (in this scenario that number is **4**) to the IP address 192.168.1.xx.

<img width="515" height="177" alt="ping_kali" src="https://github.com/user-attachments/assets/71db04b7-0a9f-4ac7-991b-fcec64d68387" />

- All the packets that were transmitted were received. Hence, the **Kali VM** can reach the **NAS**.

## Step 2: Check the open ports and services
- In this step, I checked the all the open ports and the services that run on them.
- The following command was executed to do so:

  ***nmap 192.168.1.xx***

<img width="531" height="217" alt="nmap" src="https://github.com/user-attachments/assets/a783ae4b-3ac8-4f7e-b7a8-9857f3c8b3d6" />


- Now we need to check the services that are running along with their version using the following command:

***nmap -sC -sV 192.168.1.xx***

<img width="782" height="205" alt="nmapsCsV" src="https://github.com/user-attachments/assets/8ef50d72-1d17-49d0-a715-c27bc6bb24b2" />


- From the result it is clear that Samba seems to be the one possible entry point since it is the major service running on the server.

