# Security Hardening
This section elaborates on the security hardening practices performed on the NAS to improve it's security posture and as a result reduce the attack surface of the system.
The hardening process involved the following steps:
1. Documenting the base system
2. Updating the system
3. Removal of unnecessary packages and services
4. Improving SSH security
5. Configuring the UFW
6. Securing Samba

## Documenting the base system
The base system was documented in the [security baseline](security_baseline.md) by recording the version and kernel of Ubuntu Server that was utilized, services that are running, open ports and the default UFW configuration.

## Updating the system
- Using the ***sudo apt update*** command, the list of available software packages was updated. These updates were then installed using the ***sudo apt upgrade*** command.
- The command ***sudo apt autoremove*** was used to remove packages that were automatically installed as dependencies but are no longer required.

## Removal of Unnecessary Packages and Services
- The ***apt-mark showmanual*** command was run to display all the explicitly installed packages.
- All of these packages are essential and hence should not be removed.
- The services whose utility required investigation in [Services](security_baseline.md#Services) are mentioned below:
  - 


