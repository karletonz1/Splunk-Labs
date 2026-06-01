# Network Configuration Commands

## Ubuntu Server DHCP settings
File location to change network settings: `sudo nano /etc/netplan/50-cloud-init.yaml`

```text
network:
  version: 2
  ethernets:
    ens3:
      dhcp4: true
```  
```text
network:
  version: 2
  ethernets:
    ens3:
      dhcp4: false
      addresses:
        - [ IP ] [CIDR]
      routes:
        - to: default
          via: [ IP ]
      nameservers:
        addresses:
          - 10.10.1.2
```

Apply the settings for it to take effect: `sudo netplan apply`  

Default static routes `sudo ip route add default via [IP address]`

## VyOS Router settings  

```text
set interfaces ethernet eth0 address dhcp  

set service ntp server 10.10.1.2  

set service dhcp-relay listen-interface eth1

set service dhcp-relay upstream-interface eth0

set service dhcp-relay server 10.10.1.2

commit  

save  
```  

```text
set protocols ospf area 0 network 10.20.20.0/24
set protocols ospf area 0 network 10.10.6.0/24
```

sudo ip route add default via 10.20.20.1 dev ens3