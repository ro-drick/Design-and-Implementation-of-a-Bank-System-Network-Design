# Radeon Company Ltd. Network Design and Implementation

## Project Overview

This project involves designing and implementing a robust and scalable network for **Radeon Company Ltd.**, a US-based organization that specializes in banking and insurance services. As the company seeks to expand into Africa, their first branch will be established in Nairobi, Kenya. The building assigned for their operations spans four stories, each floor housing multiple departments, as detailed below.

I was tasked with planning and setting up a network that would cater to both wired and wireless users in all departments, while ensuring secure, efficient, and reliable communication across the network.

<img src= "https://github.com/ro-drick/Design-and-Implementation-of-a-Bank-System-Network-Design/blob/main/bank-network.png"/>

## Case Study Requirements

Radeon Company Ltd. outlined the following key requirements for their network setup:

- **Network Hierarchical Design**: The network must follow a hierarchical design, ensuring scalability, manageability, and performance.
- **Simulation**: Cisco Packet Tracer was used to simulate the design and implementation.
- **Routing Protocol**: OSPF (Open Shortest Path First) will be configured to advertise routes.
- **Wireless Connectivity**: Each department should have wireless access to accommodate mobile and non-wired devices.
- **Dynamic IP Allocation**: A dedicated DHCP server will dynamically assign IP addresses to hosts across all departments.
- **VLAN Segmentation**: Each department is to be segmented into its own VLAN, ensuring network isolation and improved security.
- **Server Setup**: HTTP, DHCP, and Email servers will be deployed to handle internal communication and services.
- **Remote Access**: Secure Shell (SSH) must be configured on all routers to enable secure remote login.
- **Port Security**: Port security must be implemented on switches using sticky MAC and shutdown violation mode to secure access points.
- **Basic Configuration**: Standard device configurations will include hostname settings, password encryption, banners, and disabling DNS lookup.
- **Inter-VLAN Routing**: Routing between VLANs will be handled by multilayer switches configured with Switch Virtual Interfaces (SVIs).

## Network Topology

The network topology is structured hierarchically across four floors, with each floor hosting different departments as detailed in the table below:

### Floor-wise Department Layout:

| **Floor**     | **Departments**         | **No. of PCs** | **No. of Printers** | **No. of Servers** |
|---------------|-------------------------|----------------|---------------------|--------------------|
| First Floor   | Management, Research, HR | 20 per dept.   | 4 per dept.         | -                  |
| Second Floor  | Marketing, Accounting, Finance | 20 per dept. | 4 per dept. | - |
| Third Floor   | Logistics, Customer Care, Guest Area | 20 each (40 for Guest) | 4 each (2 for Guest) | - |
| Fourth Floor  | Administration, ICT, Server Room | 20 each (2 admin PCs in Server Room) | 2 each | 3 (DHCP, HTTP, Email) |

### VLAN Assignments:

Each department is assigned its own VLAN to ensure network segmentation:

| **VLAN ID** | **Department**        | **Subnet**             | **IP Range**                | **Broadcast Address** |
|-------------|-----------------------|------------------------|-----------------------------|-----------------------|
| 10          | Management            | 192.168.10.0/26         | 192.168.10.1 – 192.168.10.62 | 192.168.10.63         |
| 20          | Research              | 192.168.10.64/26        | 192.168.10.65 – 192.168.10.126 | 192.168.10.127       |
| 30          | HR                    | 192.168.10.128/26       | 192.168.10.129 – 192.168.10.190 | 192.168.10.191       |
| 40          | Marketing             | 192.168.10.192/26       | 192.168.10.193 – 192.168.10.254 | 192.168.10.255       |
| 50          | Accounting            | 192.168.11.0/26         | 192.168.11.1 – 192.168.11.62 | 192.168.11.63         |
| 60          | Finance               | 192.168.11.64/26        | 192.168.11.65 – 192.168.11.126 | 192.168.11.127       |
| 70          | Logistics             | 192.168.11.128/26       | 192.168.11.129 – 192.168.11.190 | 192.168.11.191       |
| 80          | Customer Care         | 192.168.11.192/26       | 192.168.11.193 – 192.168.11.254 | 192.168.11.255       |
| 90          | Guest Area            | 192.168.12.0/26         | 192.168.12.1 – 192.168.12.62 | 192.168.12.63         |
| 100         | Admin                 | 192.168.12.64/26        | 192.168.12.65 – 192.168.12.126 | 192.168.12.127       |
| 110         | ICT                   | 192.168.12.128/26       | 192.168.12.129 – 192.168.12.190 | 192.168.12.191       |
| 120         | Server Room           | 192.168.12.192/26       | 192.168.12.193 – 192.168.12.254 | 192.168.12.255       |

### IP Addressing and Subnetting:

The base network address is 192.168.10.0, and subnetting has been done based on the number of hosts required per department. Each department has been allocated a separate subnet with the correct subnet mask to accommodate all hosts (wired and wireless devices). Below is the addressing scheme for each department.

- **Management (VLAN 10)**: 192.168.10.0/26, usable IPs: 192.168.10.1 – 192.168.10.62
- **Research (VLAN 20)**: 192.168.10.64/26, usable IPs: 192.168.10.65 – 192.168.10.126
- **HR (VLAN 30)**: 192.168.10.128/26, usable IPs: 192.168.10.129 – 192.168.10.190
- **And so on…**

### Network Implementation

1. **VLAN Configuration**: Each department is assigned a unique VLAN. Switch ports are configured and assigned to their respective VLANs.
2. **IP Addressing**: Hosts are assigned dynamic IP addresses via DHCP, with the server located on the fourth floor in the server room.
3. **OSPF Configuration**: OSPF is used as the routing protocol for all subnets. OSPF ensures dynamic route advertisement across the network.
4. **SSH**: Secure remote access is enabled through SSH configuration on all routers.
5. **Port Security**: Implemented on switch ports to prevent unauthorized devices from accessing the network. Sticky MAC addresses are used to dynamically learn the MAC addresses, and the violation mode is set to "shutdown."
6. **Wireless Network**: Wireless Access Points are deployed in each department, allowing seamless connectivity for mobile devices.

### Device Configurations:

- **Routers**: Each router is configured with hostname, OSPF routing, SSH for remote management, and basic security settings.
- **Switches**: VLANs, port security, and switchport settings are configured on each switch to manage the wired network.
- **Servers**: DHCP, HTTP, and Email services are configured to manage dynamic IP allocation, internal web services, and communication across the company.

### Testing and Verification:

To ensure the network is operating as expected, various testing methods were employed:

- **Ping Test**: Communication between devices across different VLANs was tested using ping.
- **DHCP Test**: Devices were checked to verify they could automatically obtain IP addresses from the DHCP server.
- **SSH Test**: Verified that SSH was working properly by remotely logging into routers.
- **Port Security Test**: Attempts to connect unauthorized devices resulted in port shutdown as expected.

## Technologies and Features Used:

- **Cisco Packet Tracer** for simulation.
- **Hierarchical Network Design**.
- **OSPF Routing**.
- **VLAN Configuration and Inter-VLAN Routing**.
- **DHCP for Dynamic IP Allocation**.
- **SSH for Secure Remote Management**.
- **Switchport Security**.
- **Wireless Networks** (WLAN with Access Points).
- **Testing and Troubleshooting** using Cisco tools.


## How to Run

1. **Open the Network Simulation File**: Launch the Cisco Packet Tracer or GNS3 software and open the project file.

2. **Verify Device Configurations**:
   - Confirm the VLANs, IP addressing scheme, and basic configurations on all network devices (switches, routers, access points).
   - Ensure that SSH, DHCP, and OSPF configurations are active.

3. **Access Network Devices**:
   - To log into any router or switch, use the password `cisco` for console, VTY (SSH), and enable mode.

4. **Test Network Connectivity**:
   - Ping devices from different VLANs to ensure successful inter-VLAN routing.
   - Check if all devices are obtaining their IP addresses dynamically via DHCP.
   - Test remote access to routers via SSH using the password `cisco`.

5. **Test Servers**:
   - Open a browser on any end device and access the HTTP server using the appropriate IP address.
   - Configure an email client on any device to connect to the Email server for testing.

6. **Monitor Security**:
   - Check the port-security settings by examining the active ports on the switches to ensure MAC address sticky configurations and security violations are in place. 

With the configuration complete, the network should now be fully operational and secure, with seamless communication between all departments.

<img src="https://github.com/ro-drick/Design-and-Implementation-of-a-Bank-System-Network-Design/blob/main/bank-network-cisco-packet-tracer.png"/>

## Conclusion

The successful design and implementation of the network for **Radeon Company Ltd.** provides a scalable, secure, and efficient communication infrastructure tailored to their needs. By utilizing VLAN segmentation, OSPF routing, and port security, I ensured both network performance and security. The incorporation of dynamic IP allocation via DHCP and secure remote access through SSH further enhances the usability and manageability of the network. Wireless access points across all floors allow for flexible connectivity, ensuring that both wired and wireless devices can seamlessly communicate. This project demonstrates the power of hierarchical network design in an enterprise setting, meeting the organization's current operational requirements while ensuring the network is capable of handling future growth. Testing and verification have confirmed that the network operates smoothly, with all departments and services functioning as expected. The project sets a solid foundation for the company's expansion and its move into the African market.

---
