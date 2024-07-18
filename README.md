# Design-and-Implementation-of-a-Small-Office-Home-Office-Network--SOHO-Project-2-
### Project #2: Design and Implementation of a Small Office Home Office Network (SOHO)

#### Case Study and Requirements

1. **Network Design**:
   - One router and one switch (all CISCO products).
   - 3 departments: Admin/IT, Finance/HR, and Customer Service/Reception.
   - Each department in different VLANs.
   - Each department has a wireless network.
   - Host devices obtain IPv4 addresses automatically.
   - Devices in all departments must communicate with each other.
   - Base network: 192.168.1.0

#### Technologies Implemented

1. **Creating a Simple Network using a Router and Access Layer Switch**:
   - Use one router and one switch to set up the network.
   
2. **Connecting Networking Devices with Correct Cabling**:
   - Use straight-through cables to connect the router to the switch and PCs to the switch.

3. **Creating VLANs and Assigning Ports VLAN Numbers**:
   - Create VLANs for each department on the switch.

4. **Subnetting and IP Addressing**:
   - Subnet the given network 192.168.1.0/24 to accommodate VLANs.
   
5. **Configuring Inter-VLAN Routing (Router on a Stick)**:
   - Use a router with sub-interfaces to enable communication between VLANs.

6. **Configuring DHCP Server (Router as the DHCP Server)**:
   - Configure the router to act as a DHCP server, assigning IP addresses to devices in each VLAN.

7. **Configuring WLAN or Wireless Network (Cisco Access Point)**:
   - Set up wireless networks for each VLAN.

8. **Host Device Configurations**:
   - Ensure all host devices are configured to receive IP addresses via DHCP.

9. **Testing and Verifying Network Communication**:
   - Test connectivity within and between VLANs.

#### Detailed Pointwise Implementation

1. **Setting Up the Devices**:
   - Drag and drop the required devices in Cisco Packet Tracer: one router, one switch, three access points, and host devices.

2. **Connecting the Devices**:
   - Use straight-through cables to connect the router to the switch.
   - Connect each PC to the switch with straight-through cables.
   - Connect access points to the switch.

3. **Configuring VLANs**:
   - Access the switch CLI and create VLANs:
     ```bash
     Switch> enable
     Switch# configure terminal
     Switch(config)# vlan 10
     Switch(config-vlan)# name Admin_IT
     Switch(config-vlan)# vlan 20
     Switch(config-vlan)# name Finance_HR
     Switch(config-vlan)# vlan 30
     Switch(config-vlan)# name Customer_Service_Reception
     ```
   - Assign switch ports to VLANs:
     ```bash
     Switch(config)# interface range fastEthernet 0/1-5
     Switch(config-if-range)# switchport mode access
     Switch(config-if-range)# switchport access vlan 10
     Switch(config)# interface range fastEthernet 0/6-10
     Switch(config-if-range)# switchport mode access
     Switch(config-if-range)# switchport access vlan 20
     Switch(config)# interface range fastEthernet 0/11-15
     Switch(config-if-range)# switchport mode access
     Switch(config-if-range)# switchport access vlan 30
     ```

4. **Subnetting and IP Addressing**:
   - Subnet 192.168.1.0/24 into smaller subnets for each VLAN:
     - Admin/IT (VLAN 10): 192.168.1.0/26
     - Finance/HR (VLAN 20): 192.168.1.64/26
     - Customer Service/Reception (VLAN 30): 192.168.1.128/26

5. **Configuring Inter-VLAN Routing (Router on a Stick)**:
   - Configure router sub-interfaces for each VLAN:
     ```bash
     Router> enable
     Router# configure terminal
     Router(config)# interface gigabitEthernet 0/0.10
     Router(config-subif)# encapsulation dot1Q 10
     Router(config-subif)# ip address 192.168.1.1 255.255.255.192
     Router(config)# interface gigabitEthernet 0/0.20
     Router(config-subif)# encapsulation dot1Q 20
     Router(config-subif)# ip address 192.168.1.65 255.255.255.192
     Router(config)# interface gigabitEthernet 0/0.30
     Router(config-subif)# encapsulation dot1Q 30
     Router(config-subif)# ip address 192.168.1.129 255.255.255.192
     ```

6. **Configuring DHCP Server (Router as the DHCP Server)**:
   - Configure the router to provide DHCP services:
     ```bash
     Router(config)# ip dhcp pool VLAN10
     Router(dhcp-config)# network 192.168.1.0 255.255.255.192
     Router(dhcp-config)# default-router 192.168.1.1
     Router(dhcp-config)# ip dhcp pool VLAN20
     Router(dhcp-config)# network 192.168.1.64 255.255.255.192
     Router(dhcp-config)# default-router 192.168.1.65
     Router(dhcp-config)# ip dhcp pool VLAN30
     Router(dhcp-config)# network 192.168.1.128 255.255.255.192
     Router(dhcp-config)# default-router 192.168.1.129
     ```

7. **Configuring WLAN or Wireless Network (Cisco Access Point)**:
   - Configure access points for each VLAN:
     - Access Point for Admin/IT:
       ```bash
       AccessPoint> enable
       AccessPoint# configure terminal
       AccessPoint(config)# interface dot11Radio 0
       AccessPoint(config-if)# ssid Admin_IT_WLAN
       AccessPoint(config-if-ssid)# vlan 10
       ```
     - Repeat similar steps for Finance/HR and Customer Service/Reception.

8. **Host Device Configurations**:
   - Ensure all PCs and wireless devices are set to obtain IP addresses automatically via DHCP.

9. **Testing Network Communication**:
   - Use the ping command to test connectivity:
     - Ping between devices within the same VLAN.
     - Ping between devices in different VLANs to ensure inter-VLAN routing is working.

By following these steps, you will have a functional network that meets the requirements of XYZ company's new branch, with proper VLAN segmentation, wireless network access, and DHCP configuration, enabling seamless communication within and between departments.
