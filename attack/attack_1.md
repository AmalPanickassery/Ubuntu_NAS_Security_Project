# Attack 1 (Network Reconnaissance)
The following steps elaborate the Attack 1 process:

## Step 1: Determine that the Kali VM can reach the NAS
- For the sake of the attack phase, the Kali VM is allowed to reach the NAS in this project.
- Elaborate more on this and add a few screenshots. Might remove this part. Not sure yet.

## Step 2: Test the connectivity between Kali VM and the NAS
- In order to test whether the Kali VM can connect to the NAS, I executed the following command:

  ***ping -c 4 192.168.1.xx***

- The **-c** stands for count and it is a flag that tells the **ping** utility to stop after sending a specific number of packets (in this scenario that number is **4**) to the IP address 192.168.1.xx.
- ***Screenshot***
- All the packets that were transmitted were received. Hence, the **Kali VM** can reach the **NAS**.

## Step 3: Check the open ports and services
- In this step, I checked the all the open ports and the services that run on them.
- The following command was executed to do so:

  ***nmap 192.168.1.xx***

- ***Screenshot***

