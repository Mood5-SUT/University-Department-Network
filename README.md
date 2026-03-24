# University Department Network with Guest Wi-Fi & Secure VLANs

## Project Overview

This project designs and implements a secure, segmented network for a university IT department. The network supports three internal user groups—faculty, students, and administration—along with a separate guest Wi-Fi network. The guest network provides internet access only, with no connectivity to internal systems, ensuring security and compliance with institutional policies.

The implementation includes VLAN segmentation, inter-VLAN routing, DHCP, access control lists (ACLs), and network address translation (NAT). A monitoring dashboard is also developed to visualize guest network usage and generate alerts for unusual activity.

---

## Scenario

The university’s IT department requires:

- A **secure internal network** for faculty, students, and administrative staff.
- A **guest Wi-Fi** network that offers internet access but is completely isolated from internal systems.

---

## Objectives

- Implement VLANs to segment network traffic by user group.
- Configure inter-VLAN routing using router-on-a-stick.
- Set up DHCP for automatic IP address assignment.
- Apply ACLs to enforce security policies and isolate the guest network.
- Implement NAT for internet access.
- Build a dashboard to monitor guest network usage and trigger alerts for misuse.

---

## Learning Focus

- VLAN and DHCP configuration
- Router-on-a-stick inter-VLAN routing
- ACLs for network security policies
- Guest network isolation and monitoring
- Network visualization and dashboarding

---

## Network Design

### VLAN & Subnet Plan

| VLAN ID | Network       | Subnet          | User Group     |
|---------|---------------|-----------------|----------------|
| 10      | Faculty       | 192.168.10.0/24 | Faculty        |
| 20      | Students      | 192.168.20.0/24 | Students       |
| 30      | Admin         | 192.168.30.0/24 | Administration |
| 40      | Guest         | 192.168.40.0/24 | Guest Wi-Fi    |

### DHCP Pools

Each VLAN is assigned a DHCP pool for dynamic IP allocation:

- **Faculty VLAN 10:** 192.168.10.100 – 192.168.10.200  
- **Students VLAN 20:** 192.168.20.100 – 192.168.20.200  
- **Admin VLAN 30:** 192.168.30.100 – 192.168.30.200  
- **Guest VLAN 40:** 192.168.40.100 – 192.168.40.200  

### ACL Policy Design

- **Guest VLAN:** Deny access to internal VLANs (10, 20, 30); allow only internet traffic.
- **Internal VLANs:** Allow full inter-VLAN communication as needed for faculty, students, and admin.
- **Internet Access:** Permitted for all VLANs except Guest is limited to HTTP/HTTPS.

---

## Implementation

### Router-on-a-Stick Configuration

- Single trunk link between router and switch.
- Subinterfaces configured for each VLAN with 802.1Q encapsulation.

### DHCP Configuration

- DHCP pools configured on the router for each VLAN.
- DHCP relay configured if needed for client-side DHCP requests.

### ACL Implementation

- Extended ACL applied to Guest VLAN subinterface to block traffic to internal networks.
- Optional ACLs to restrict access between internal VLANs if required.

### NAT Configuration

- PAT (Port Address Translation) configured on the router to allow all VLANs to access the internet.

---

## Dashboard Plan

The monitoring dashboard tracks:

- **Per-VLAN utilization:** Bandwidth usage for faculty, students, admin, and guest networks.
- **Guest network activity:** Top talkers, session duration, and bandwidth consumption.
- **Alerts:** Notifications triggered by excessive bandwidth usage, unusual connection patterns, or attempts to access internal IP ranges from the guest VLAN.

### Dashboard Tools (Suggested)

- **PRTG Network Monitor** or **Zabbix** for real-time graphing.
- **NetFlow/sFlow** for traffic analysis.
- **Custom scripts** with Grafana for visualization.

---

## Testing Results

| Test Case                          | Expected Result                                    | Status |
|------------------------------------|----------------------------------------------------|--------|
| Guest connects to Wi-Fi            | Assigned IP from 192.168.40.0/24                   | ✅     |
| Guest accesses internal IP         | Blocked by ACL                                     | ✅     |
| Guest browses internet             | Allowed (HTTP/HTTPS)                               | ✅     |
| Faculty/Student/Admin access internet | Allowed                                         | ✅     |
| Internal VLANs communicate         | Allowed as per policy                              | ✅     |
| Dashboard displays guest usage     | Real-time graphs and alerts active                 | ✅     |

---

## Expected Results

- ✅ Guest VLAN fully isolated from internal systems  
- ✅ DHCP automatically assigns IPs to all user groups  
- ✅ Internet access granted only to authorized networks  
- ✅ Dashboard provides real-time monitoring of guest bandwidth  
- ✅ Alerts triggered for guest network misuse or anomalies  

---

## Deliverables

### Phase 1: Design
- VLAN and subnet plan  
- DHCP pools and ACL policy design  
- Dashboard plan with metrics and alert logic  

### Phase 2: Implementation & Testing
- Router-on-a-stick configuration  
- DHCP and ACL implementation  
- Dashboard graphs showing guest usage  
- Testing results confirming guest isolation and internet access  

---

## Tools & Technologies

- **Cisco Packet Tracer** or **GNS3** for simulation  
- **Cisco IOS** (routers and switches)  
- **PRTG / Zabbix / Grafana** for dashboarding  
- **NetFlow / sFlow** for traffic monitoring  

---

## Author

**Mahmoud Hany Hussien**  
*IT & Networking Enthusiast*

---

## Acknowledgments

- Cisco Networking Academy  
- Huawei ICT Academy  
- E& Egypt Summer Internship Program
