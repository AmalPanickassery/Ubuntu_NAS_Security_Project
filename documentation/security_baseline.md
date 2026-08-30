The following information contains the details on the baseline security stance of the NAS before security hardening practices were implemented.

# OS Version and Kernel
The version of Ubuntu Server was **26.04 LTS** with the **Linux 7.0.0-27-generic** kernel

# Users
The server only had three users: **amaljp**, **alice**, and **bob**. A lower user count helps minimize the attack surface and hence lowers the risk of a threat attacker gaining access via stolen credentials.

# Services
The following is a list of all the services on the server:
- **chrony**: Ensures that the system clock is synchronized using NTP ***(Essential)***
- **cron**: Responsible for scheduled/background tasks ***(Essential)***
- **dbus**: Allows system applications/services to communicate with eachother ***(Essential)***
- **getty@tty1**: Provides the local text login console ***(Essential)***
- **ModemManager**: Manages cellular/mobile broadband modems ***(Utility Requires Investigation)***
- **multipathd**: Manages multiple paths to the same storage device ***(Use Requires Investigation)***
- **networkd-dispatcher**: Runs scripts in response to network state changes ***(Use Requires Investigation)***
- **polkit**: Controls authorization for certain privileged operations ***(Essential)***
- **rsyslog**: System logging ***(Essential)***
- **smbd**: Samba file-sharing server ***(Essential)***
- **ssh**: SSH server for remote administration ***(Essential)***
- **systemd-journald**: Collects system logs ***(Essential)***
- **systemd-resolved**: Responsible for DNS resolution ***(Essential)***
- **systemd-udevd**: Detects/manages hardware devices ***(Essential)***
- **udisks2**: Manages storage devices/disks ***(Use Requires Investigation)***

# Service Requirement Investigation Results
The following are the findings and conclusions drawn from the investigation into whether certain services are actually essential or not. Disabling non-essential services ensures that vulnerabilities aren't introduced due to the presence of non-essential services on the system.

## ModemManager
- ModemManager is a system daemon in Linux that controls mobile broadband devices. It provides a unified way to configure and manage cellular modems.
- The network connection for the NAS is provided by the **VirtualBox** virtual Ethernet adapter. Therefore, ModemManager is **not required**.
- The presence of a cellular modem was also checked by running the ***mmcli -L*** command which resulted in ***No modems were found***.
- Due to these reasons, the ModemManager service was **disabled**.

## multipathd
- multipathd is a system daemon that manages multiple paths to the same storage device. It is typically used with enterprise SAN/storage systems.
- The server only uses a single disk setup and the presence of multipath devices was checked by running the ***sudo multipath -ll*** which resulted in ***No multipath devices found***.
- Due to these reasons, the multipathd service was **disabled**.

  
