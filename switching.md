## 1- Basic Configuration
| Command                | Description                                                                                   |
|------------------------|-----------------------------------------------------------------------------------------------|
| `enable`               | Enter privileged mode for full access to configuration commands.                              |
| `conf t`               | Enter global configuration mode to make device-wide changes.                                  |
| `no ip domain-lookup`  | Disable DNS lookup to prevent command interpretation errors.                                  |
| `hostname S1`          | Set the device hostname to 'S1' for network identification.                                   |
| `enable secret class`  | Set an encrypted password 'class' for privileged mode access.                                  |
| `line con 0`           | Configure settings for the console port (console 0) used for local access.                     |
| `password cisco`       | Set the console port password to 'cisco' for local access security.                            |
| `login`                | Enable login authentication on the console port.                                               |
| `line vty 0 15`        | Configure settings for virtual terminal (vty) lines 0 to 15 for remote access.                 |
| `password cisco`       | Set the VTY password to 'cisco' for remote access security.                                    |
| `login`                | Enable login authentication on the VTY lines.                                                  |
| `end`                  | Exit configuration mode and return to privileged EXEC mode.                                    |

***
## 2- Vlan Creation
| Command         | Description                                                                                      |
|-----------------|--------------------------------------------------------------------------------------------------|
| `conf t`        | Enter global configuration mode to make device-wide changes.                                      |
| `VLAN 10`       | Create VLAN 10.                                                                                  |
| `name Tech` | Assign the name "Tech" to VLAN 10.                                                         |
| `vlan 99`       | Create VLAN 99.                                                                                  |
| `name admin`    | Assign the name "admin" to VLAN 99.                                                               |

## 3- VTP

| Command                     | Description                                                                                      |
|-----------------------------|--------------------------------------------------------------------------------------------------|
| `vtp mode {server | client | transparent}` | Set the VTP mode for the device. Choices are server, client, or transparent.                    |
| `vtp domain <domain-name>`  | Set the VTP domain name for VLAN synchronization across switches.                                |
| `vtp password <password>`   | Set a password for VTP domain information to ensure secure synchronization.                      |
| `vtp version <1 | 2 | 3>`    | Set the VTP version. Choices are 1, 2, or 3.                                                      |
| `vtp pruning`               | Enable VTP pruning to restrict VLAN information propagation to only trunk links where VLAN is active. |
| `show vtp status`           | Display the current VTP configuration and operational status.                                     |

## 4- Interfaces Management (Trunking , Switchport)

| Command                      | Description                                                           |
|------------------------------|-----------------------------------------------------------------------|
| `int range f0/1-21`          | Configure interfaces FastEthernet 0/1 to 0/21.                        |
| `switchport mode access`     | Set interfaces to access mode.                                         |
| `int f0/1-4`                 | Access to the interface range f0/1-4.                                  |
| `switchport access vlan 99`  | Assign VLAN 99 to interfaces FastEthernet 0/1 to 0/4.                  |
| `int f0/5-10`                 | Access to the interface range f0/5-10.                                |
| `switchport access vlan 20`  | Assign VLAN 20 to interfaces FastEthernet 0/5 to 0/10.                 |
| `int f0/11-14`                 | Access to the interface range f0/11-14.                              |
| `switchport access vlan 30`  | Assign VLAN 30 to interfaces FastEthernet 0/11 to 0/14.                |
| `int f0/15-21`                 | Access to the interface range f0/15-21.                              |
| `switchport access vlan 40`  | Assign VLAN 40 to interfaces FastEthernet 0/15 to 0/21.                |
| `int range f0/22-24`         | Configure interfaces FastEthernet 0/22 to 0/24.                        |
| `switchport mode trunk`      | Set interfaces to trunk mode.                                          |
| `switchport trunk native vlan 50` | Set native VLAN to 50 on trunk interfaces.                        |
| `no shutdown`                | Enable all configured interfaces.                                      |
| `int range g0/1-2`           | Configure interfaces GigabitEthernet 0/1 and 0/2.                      |
| `switchport mode trunk`      | Set interfaces to trunk mode.                                          |
| `switchport trunk native vlan 50` | Set native VLAN to 50 on trunk interfaces.                        |

## 5- VLAN IP Configuration

| Command                            | Description                                               |
|------------------------------------|-----------------------------------------------------------|
| `int vlan 99`                      | Enter VLAN interface configuration mode for VLAN 99.       |
| `ip address 192.168.99.4 255.255.255.0` | Assign IP address 192.168.99.4 with subnet mask 255.255.255.0 to VLAN interface. |
| `ip default-gateway 192.168.99.1`  | Set the default gateway for VLAN 99 to 192.168.99.1.       |

## 6- Port Security Configuration

| Command                                   | Description                                                          |
|-------------------------------------------|----------------------------------------------------------------------|
| `int range f0/1-21`                       | Configure interfaces FastEthernet 0/1 to 0/21.                       |
| `switchport mode access`                  | Set interfaces to access mode.                                        |
| `switchport port-security`                | Enable port security on the interfaces.                               |
| `switchport port-security maximum 2`      | Set maximum number of secure MAC addresses to 2 per interface.        |
| `switchport port-security mac-address sticky` | Enable sticky MAC address learning for port security.              |
| `switchport port-security violation shutdown` | Set action to shutdown interface on security violation.            |
| `no shutdown`                             | Enable all configured interfaces.                                     |


## 7- SSH
| Command                               | Description                                                          |
|---------------------------------------|----------------------------------------------------------------------|
| `service password-encryption`         | Encrypts plaintext passwords in the configuration.                   |
| `username anass password H!ghly$3cureP@ssw0rd2024#`       | Creates a local user 'anass' with password 'H!ghly$3cureP@ssw0rd2024#'.                  |
| `line vty 0 15`                       | Enters line configuration mode for virtual terminal (vty) lines 0 to 15. |
| `login local`                         | Enables local authentication for vty lines, using locally configured usernames and passwords. |
| `transport input ssh`                 | Restricts vty lines to accept SSH connections only.                   |
| `exit`                                | Exits line configuration mode.                                        |
| `ip domain-name ejemplo.es`           | Configures the domain name 'ejemplo.es' for SSH key generation.       |
| `crypto key generate rsa`            | Generates RSA cryptographic keys for SSH connections.                 |

## 8- Etherchannel

| Command                                    | Description                                                          |
|--------------------------------------------|----------------------------------------------------------------------|
| `interface range g0/1-2`                   | Enter configuration mode for multiple interfaces simultaneously.     |
| `channel-group 1 mode on`                  | Configure individual interfaces to participate in an EtherChannel bundle. |
| `no shutdown`                              | Enable the interfaces participating in the EtherChannel.              |
| `show etherchannel summary`                | Display summary information about configured EtherChannels.           |
| `show etherchannel <number>`               | Display detailed information about a specific EtherChannel bundle.    |

## 9- Router on Stick
| Command                            | Description                                                          |
|------------------------------------|----------------------------------------------------------------------|
| `int g0/1`                         | Enter interface configuration mode for GigabitEthernet 0/1.           |
| `no ip address`                    | Remove any existing IP addresses from the interface.                  |
| `no shutdown`                      | Enable the interface.                                                 |
| `int g0/1.40`                      | Enter subinterface configuration mode for VLAN 40 on GigabitEthernet 0/1. |
| `encapsulation dot1Q 40`           | Set the subinterface encapsulation to IEEE 802.1Q for VLAN 40.        |
| `ip address 192.168.40.1 255.255.255.0` | Assign IP address 192.168.40.1 with subnet mask 255.255.255.0 to the subinterface. |
| `no shutdown`                      | Enable the subinterface.                                              |

