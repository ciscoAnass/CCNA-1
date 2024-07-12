## 1- STATIC Route

| Command                                      | Description                                                            | Example                                                        |
|----------------------------------------------|------------------------------------------------------------------------|----------------------------------------------------------------|
| `ip route <destination-network> <subnet-mask> <next-hop-ip>` | Define a static route to a specific destination network.               | `ip route 192.168.30.0 255.255.255.0 192.168.1.1`              |



## 2-  PPP (PAP)

| Command                                              | Description                                                             | Example                                                                  |
|------------------------------------------------------|-------------------------------------------------------------------------|--------------------------------------------------------------------------|
| `username <name> password <password>`                | Create a local username and password for PPP authentication.            | `username R1 password cisco`                                             |
| `interface <interface>`                              | Enter interface configuration mode.                                     | `int s0/0/0`                                                             |
| `encapsulation ppp`                                  | Set the encapsulation method to PPP.                                    | `encapsulation ppp`                                                      |
| `ppp authentication pap`                             | Enable PAP authentication on the PPP link.                              | `ppp authentication pap`                                                 |
| `ppp pap sent-username <username> password <password>` | Configure PAP to use a specific username and password for authentication. | `ppp pap sent-username R2 password cisco` (connects to the user on router R2) |


## 3- PPP (CHAP)
| Command                                      | Description                                                             | Example                                                        |
|----------------------------------------------|-------------------------------------------------------------------------|----------------------------------------------------------------|
| `interface <interface>`                      | Enter interface configuration mode.                                     | `interface s0/0/0`                                              |
| `encapsulation ppp`                          | Set the encapsulation method to PPP.                                    | `encapsulation ppp`                                             |
| `ppp authentication chap`                    | Enable CHAP authentication on the PPP link.                             | `ppp authentication chap`                                       |
| `exit`                                       | Exit interface configuration mode.                                      | `exit`                                                          |
| `username <name> password <password>`        | Create a local username and password for PPP authentication.            | `username R2 password cisco` (the name of the router we want to connect to) |



## 4- RIPV2

| Command                                      | Description                                                             | Example                                                        |
|----------------------------------------------|-------------------------------------------------------------------------|----------------------------------------------------------------|
| `router rip`                                 | Enter RIP routing protocol configuration mode.                          | `router rip`                                                   |
| `version 2`                                  | Enable RIP version 2.                                                   | `version 2`                                                    |
| `network <network>`                          | Specify the directly connected networks to include in RIP updates.      | `network 192.168.1.0`<br>`network 172.16.1.0`                  |
| `no auto-summary`                            | Disable automatic summarization of subnet routes.                       | `no auto-summary`                                              |
| `default-information originate`              | Advertise a default route if one exists (e.g., static route).           | `default-information originate`                                |


## 5- BGP

| Command                                      | Description                                                            | Example                                                        |
|----------------------------------------------|------------------------------------------------------------------------|----------------------------------------------------------------|
| `router bgp <AS-number>`                     | Enter BGP configuration mode for a specific Autonomous System (AS).    | `router bgp 100`                                               |
| `network <network>`                          | Advertise a network in BGP.                                            | `network 192.168.0.0`                                          |
| `neighbor <IP-address> remote-as <AS-number>`| Define a BGP neighbor with its remote AS number.                       | `neighbor 10.10.10.2 remote-as 200`<br>`neighbor 10.10.20.2 remote-as 300`|
| `no synchronization`                         | Disable BGP synchronization (no syn).                                  | `no synchronization`                                           |



## 6- EIGRP

| Command                                      | Description                                                             | Example                                                        |
|----------------------------------------------|-------------------------------------------------------------------------|----------------------------------------------------------------|
| `router eigrp <AS-number>`                   | Enter EIGRP routing protocol configuration mode for a specific Autonomous System (AS). | `router eigrp 100`                                             |
| `network <network> [wildcard-mask]`          | Specify the networks to include in EIGRP updates.                       | `network 192.168.1.0 0.0.0.255`<br>`network 172.16.1.0 0.0.0.255` |
| `no auto-summary`                            | Disable automatic summarization of subnet routes.                       | `no auto-summary`                                              |
| `default-information originate`              | Advertise a default route if one exists.                                | `default-information originate`                                |
| `exit`                                       | Exit EIGRP configuration mode.                                          | `exit`                                                         |
| `show ip eigrp neighbors`                    | Display EIGRP neighbors.                                                | `show ip eigrp neighbors`                                      |
| `show ip eigrp topology`                     | Display the EIGRP topology table.                                        | `show ip eigrp topology`                                       |

## 7- OSPF

| Command                                      | Description                                                             | Example                                                        |
|----------------------------------------------|-------------------------------------------------------------------------|----------------------------------------------------------------|
| `router ospf <process-id>`                    | Enter OSPF routing process configuration mode with a specified process ID. | `router ospf 1`                                                |
| `network <network> <wildcard-mask> area <area-id>` | Specify networks to include in OSPF updates and their associated area.  | `network 192.168.1.0 0.0.0.255 area 0`                         |
| `passive-interface <interface>`              | Configure an interface to not send OSPF hello packets (passive mode).   | `passive-interface GigabitEthernet0/0`                         |
| `default-information originate`              | Advertise a default route into OSPF if one exists.                      | `default-information originate`                                |
| `exit`                                       | Exit OSPF configuration mode.                                           | `exit`                                                         |
| `show ip ospf neighbor`                      | Display OSPF neighbor relationships.                                    | `show ip ospf neighbor`                                        |
| `show ip ospf database`                      | Display OSPF link-state database information.                           | `show ip ospf database`                                        |


## 8- Difference between Routing Protocols

| Feature          | Static Route                           | PPP                                     | RIPv2                                   | BGP                                      | EIGRP                                   | OSPF                                    |
|------------------|----------------------------------------|-----------------------------------------|-----------------------------------------|------------------------------------------|-----------------------------------------|-----------------------------------------|
| **Protocol Type**| Routing protocol                       | Data-link protocol                      | Distance vector routing protocol        | Path vector routing protocol              | Advanced distance vector routing protocol | Link-state routing protocol              |
| **Purpose**      | Manually configured path                | Point-to-Point Protocol                 | Exchange routing information dynamically within a network | Exchange routing information between Autonomous Systems (AS) | Exchange routing information dynamically within a network | Exchange routing information within a single Autonomous System (AS) |
| **Operation**    | Static, manually configured routes     | Provides point-to-point connection over serial links | Sends periodic updates about routing tables to neighboring routers | Uses AS_PATH to prevent routing loops     | Uses DUAL algorithm for faster convergence | Uses SPF algorithm for path calculation  |
| **Complexity**   | Simple to configure and manage         | Configuration involves authentication and negotiation | Simple setup with basic configuration   | Complex setup, supports complex policy controls | Moderate complexity, supports more features than RIP | Moderate to complex, supports large networks and advanced features |
| **Scalability**  | Not scalable for large networks       | Limited to point-to-point connections   | Limited scalability due to periodic updates | Highly scalable, suitable for large networks and ISPs | Scalable for medium and large networks    | Highly scalable, suitable for large networks and complex topologies |
| **Convergence**  | Slow convergence, manual intervention required | Fast, efficient for point-to-point links | Moderate convergence time               | Fast convergence, suited for large networks | Fast convergence, suited for medium and large networks | Fast convergence, suited for medium and large networks |
| **Flexibility**  | Limited flexibility, requires manual updates | Limited to point-to-point scenarios     | Limited flexibility in network design   | Highly flexible, supports complex policy routing | Flexible, supports multiple protocols and advanced features | Flexible, supports multiple areas and complex network topologies |
| **Use Cases**    | Small networks, static routes           | Point-to-point WAN connections          | Small to medium-sized networks          | Large-scale networks, ISPs, multi-homed connections | Medium to large enterprise networks     | Medium to large enterprise networks, ISPs |
| **Example Cisco Command** | `ip route 192.168.1.0 255.255.255.0 10.0.0.1` | `int s0/0/0`<br>`encapsulation ppp`<br>`ppp authentication chap` | `router rip`<br>`network 192.168.1.0` | `router bgp 65000`<br>`network 192.168.1.0 mask 255.255.255.0` | `router eigrp 100`<br>`network 192.168.1.0 0.0.0.255` | `router ospf 1`<br>`network 192.168.1.0 0.0.0.255 area 0` |

