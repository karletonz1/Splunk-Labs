# Physical Port Addressing

This document defines the physical architecture and port mapping scheme.

## Central Switch Port Map

| Source Hostname | Source Interface Name | Interface Description | Speed | Duplex | MTU | Destination Hostname | Destination Interface Name |
| --------------- | --------------------- | --------------------- | ----- | ------ | --- | -------------------- | -------------------------- |
| karlo-central-switch | eth1 | To User Endpoint | 1000 | Full | 1500 | Management1 | NIC1 |  
| karlo-central-switch | eth2 | To Server Port | 1000 | Full | 1500 | karlo-splunk-mgmt | e0 |  
| karlo-central-switch | eth3 | To Server Port | 1000 | Full | 1500 | karlo-splunk-indexer01 | e0 |  
| karlo-central-switch | eth4 | To Server Port | 1000 | Full | 1500 | karlo-splunk-indexer02 | e0 |  
| karlo-central-switch | eth5 | To Server Port | 1000 | Full | 1500 | karlo-splunk-sh | e0 |  
| karlo-central-switch | eth6 | To Router PTP link | 1000 | Full | 1500 | karlo-remote-router | eth0 |  
| karlo-central-switch | eth7 | To Server Port | 1000 | Full | 1500 | karlo-splunk-dc | NIC1 |  

## Server Port Map

| Source Hostname | Source Interface Name | Interface Description | Speed | Duplex | MTU | Destination Hostname | Destination Interface Name |
| --------------- | --------------------- | --------------------- | ----- | ------ | --- | -------------------- | -------------------------- |
| karlo-splunk-dc | NIC1 | To Distribution Switch Port | 1000 | Full | 1500 | karlo-central-switch | eth7 |  
| karlo-splunk-mgmt | e0 | To Distribution Switch Port | 1000 | Full | 1500 | karlo-central-switch | eth2 |  
| karlo-splunk-indexer01 | e0 | To Distribution Switch Port | 1000 | Full | 1500 | karlo-central-switch | eth3 |  
| karlo-splunk-indexer02 | e0 | To Distribution Switch Port | 1000 | Full | 1500 | karlo-central-switch | eth4 |  
| karlo-splunk-sh | e0 | To Distribution Switch Port | 1000 | Full | 1500 | karlo-central-switch | eth5 |  
| karlo-splunk-kvm | e0 | To Router Port | 1000 | Full | 1500 | karlo-remote-router | eth1 |  

## Router Port Map

| Source Hostname | Source Interface Name | Interface Description | Speed | Duplex | MTU | Destination Hostname | Destination Interface Name |
| --------------- | --------------------- | --------------------- | ----- | ------ | --- | -------------------- | -------------------------- |
| karlo-remote-router | eth0 | To Distribution Switch Port | 1000 | Full | 1500 | karlo-central-switch | eth6 |  
| karlo-remote-router | eth1 | To Server Port | 1000 | Full | 1500 | karlo-splunk-kvm | e0 |  

## User Endpoint Port Map

| Source Hostname | Source Interface Name | Interface Description | Speed | Duplex | MTU | Destination Hostname | Destination Interface Name |
| --------------- | --------------------- | --------------------- | ----- | ------ | --- | -------------------- | -------------------------- |
| Management1 | NIC1 | To Distribution Switch Port | 1000 | Full | 1500 | karlo-central-switch | eth1 |  
