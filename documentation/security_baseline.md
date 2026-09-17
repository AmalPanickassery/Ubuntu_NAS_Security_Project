The following information contains the details on the baseline security stance of the NAS before security hardening practices were implemented.

# OS Version and Kernel
The version of Ubuntu Server was **26.04 LTS** with the **Linux 7.0.0-27-generic** kernel

# Users
The server only had three users: **amaljp** ***(administrative account)***, **alice** ***(standard NAS user)***, and **bob** ***(standard NAS user)***. A lower user count helps minimize the attack surface and hence lowers the risk of a threat attacker gaining access via stolen credentials.

# Services
The following is a list of all the services on the server:
- **chrony**: Ensures that the system clock is synchronized using NTP ***(Essential)***
- **cron**: Responsible for scheduled/background tasks ***(Essential)***
- **dbus**: Allows system applications/services to communicate with eachother ***(Essential)***
- **getty@tty1**: Provides the local text login console ***(Essential)***
- **ModemManager**: Manages cellular/mobile broadband modems ***(Necessity Requires Investigation)***
- **multipathd**: Manages multiple paths to the same storage device ***(Necessity Requires Investigation)***
- **networkd-dispatcher**: Runs scripts in response to network state changes ***(Necessity Requires Investigation)***
- **polkit**: Controls authorization for certain privileged operations ***(Essential)***
- **rsyslog**: System logging ***(Essential)***
- **smbd**: Samba file-sharing server ***(Essential)***
- **ssh**: SSH server for remote administration ***(Essential)***
- **systemd-journald**: Collects system logs ***(Essential)***
- **systemd-resolved**: Responsible for DNS resolution ***(Essential)***
- **systemd-udevd**: Detects/manages hardware devices ***(Essential)***
- **udisks2**: Manages storage devices/disks ***(Necessity Requires Investigation)***
- **unattended-upgrades**: Handles automatic package updates ***(Essential)***
- **user@1000**: User manager for UID 1000 ***(Essential)***


# Open Ports
The following is a list of all the open ports and their use cases:
- **22/tcp**: Used for remote administration via SSH.
- **139/tcp**: Required for **netbios-ssn** which is a legacy network protocol used by Windows machines to share files over a local network. This allows legacy machines to use the NAS for file sharing.
- **445/tcp**: Required for **microsoft-ds**, the modern network protocol used by Windows and Linux systems to share files, folders over a local network.

# Firewall
The Ubuntu server utilizes a UFW (Uncomplicated Firewall). UFW allows you to secure your system using simple, human-readable commands instead of complicated syntax.
- **Status**: Active
- **Default incoming**: Denied
- **Default outgoing**: Allowed
- **SSH**: tcp 22 
- **Samba**: tcp 445 




  
