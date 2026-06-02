# IP Addressing and Subnets

This document defines the logical architecture and IP addressing scheme.

## Network Subnets

| Subnet | Purpose |  
| ------ | ------- |
| 10.10.1.0/24 | Enterprise Services Network |
| 10.10.2.0/24 | Splunk Cluster - Management Network |
| 10.10.3.0/24 | Splunk Cluster - Primary Indexer Network |
| 10.10.4.0/24 | Splunk Cluster - Secondary Indexer Network |
| 10.10.5.0/24 | Splunk Cluster - Search Head Network |
| 10.10.6.0/24 | Point-to-Point Network |
| 10.20.20.0/24 | Remote Network |
| 192.168.1.0/24 | WAN and Management Network |

## IP Address Allocations

### Central Switch IP Addresses

| Hostname | GNS3 Port | Network Address | Address Type | IP Address | Broadcast Address | MTU | Description |
| -------- | --------- | --------------- | ------------ | ---------- | ----------------- | --- | ---- |
| karlo-central-switch | eth1 | 192.168.1.0/24 | Static | 192.168.1.96/24 | 192.168.1.255 | 1500 | PTP link between karlo-central-switch and management1 |
| karlo-central-switch | eth7 | 10.10.1.0/24 | Static | 10.10.1.1/24 | 10.10.1.255 | 1500 | PTP link between karlo-central-switch and karlo-splunk-dc |
| karlo-central-switch | eth2 | 10.10.2.0/24 | Static | 10.10.2.1/24 | 10.10.2.255 | 1500 | PTP link between karlo-central-switch and karlo-splunk-mgmt |
| karlo-central-switch | eth3 | 10.10.3.0/24 | Static | 10.10.3.1/24 | 10.10.3.255 | 1500 | PTP link between karlo-central-switch and karlo-splunk-indexer01 |
| karlo-central-switch | eth4 | 10.10.4.0/24 | Static | 10.10.4.1/24 | 10.10.4.255 | 1500 | PTP link between karlo-central-switch and karlo-splunk-indexer02 |
| karlo-central-switch | eth5 | 10.10.5.0/24 | Static | 10.10.5.1/24 | 10.10.5.255 | 1500 | PTP link between karlo-central-switch and karlo-splunk-sh |
| karlo-central-switch | eth6 | 10.10.6.0/24 | Static | 10.10.6.1/24 | 10.10.6.255 | 1500 | PTP link between karlo-central-switch and karlo-remote-router |

### Server and Endpoint IP Addresses

| Hostname | GNS3 Port | Network Address | Address Type | IP Address | Gateway | MTU | Description |
| -------- | --------- | --------------- | ------------ | ---------- | ----------------- | --- | ---- |
| Management1 | NIC1 | 192.168.1.0/24 | DHCP | 192.168.1.100/24 | 192.168.1.96 | 1500 | PTP link between karlo-central-switch and Management1 |
| karlo-splunk-dc | NIC1 | 10.10.1.0/24 | Static | 10.10.1.2/24 | 10.10.1.1 | 1500 | PTP link between karlo-central-switch and karlo-splunk-dc |
| karlo-splunk-mgmt | e0 | 10.10.2.0/24 | DHCP | 10.10.2.10/24 | 10.10.2.1 | 1500 | PTP link between karlo-central-switch and karlo-splunk-mgmt |
| karlo-splunk-indexer01 | e0 | 10.10.3.0/24 | DHCP | 10.10.3.10/24 | 10.10.3.1 | 1500 | PTP link between karlo-central-switch and karlo-splunk-indexer01 |
| karlo-splunk-indexer02 | e0 | 10.10.4.0/24 | DHCP | 10.10.4.10/24 | 10.10.4.1 | 1500 | PTP link between karlo-central-switch and karlo-splunk-indexer02 |
| karlo-splunk-sh | e0 | 10.10.5.0/24 | DHCP | 10.10.5.10/24 | 10.10.5.1 | 1500 | PTP link between karlo-central-switch and karlo-splunk-sh |
| karlo-remote-router | eth0 | 10.10.6.0/24 | DHCP | 10.10.6.11/24 | 10.10.6.1 | 1500 | PTP link between karlo-central-switch and karlo-remote-router |
| karlo-remote-router | eth1 | 10.20.20.0/24 | Static | 10.20.20.1/24 | N/A | 1500 | PTP link between karlo-remote-router and karlo-splunk-kvm |
| karlo-splunk-kvm | e0 | 10.20.20.0/24 | DHCP | 10.20.20.10/24 | 10.20.20.1 | 1500 | PTP link between karlo-splunk-kvm and karlo-remote-router |
