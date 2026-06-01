# Project Splunk Labs | Proof of Concept Development Sandbox

This is an active repository for a proof-of-concept deployment of a distributed Splunk model using a small enterprise, single search head with multiple indexer, architecture.

## Overview

Splunk Labs was designed to record the outcome of deploying a simple distributed Splunk architecture using minimal and lightweight resources in order to simulate and configure as many components as possible within the confines of my PC's resources.

The repository has been created to simulate the level of details and documentation that I would use when deploying infrastructure in a production environment. The document is intended to simulate a real document for a production environment but is a work-in-progress due to the limited scope of the project's goals, which focusses on the Splunk application as opposed to equally simulating a complex enterprise environment.  

Limitations of virtualizing a lab within GNS3 should be kept in mind as well as the condensed timeline given to the project.  

Key objectives:

:white_check_mark: Demonstrate design and documentation skills  
:white_check_mark: Deploy Splunk 10.4 and associated infrastructure and servers needed to achieve a working proof-of-concept model.  
:white_check_mark: Provide evidence that a Linux and Windows server can both forward logs using a distributed Splunk Cluster.  

## Lab Devices & Applications

Network

| Network Device | Purpose |
| ------------ | ------- |
| Arista vEOS Core Layer 3 Switch | Single switch to physically connect all devices together and route between networks |
| VyOS Router | Edge router to simulate ingesting logs from a separate network area |

| Server Nodes | Purpose |
| ------------ | ------- |
| Windows 2022 server | Hosts the Domain Controller needed to provide enterprise services such as DHCP and DNS |
| Ubuntu 24.04 LTS server | Host for installing Splunk Enterprise |

| Client Nodes | Purpose |
| ------------ | ------- |
| Windows 10 client | Management PC for accessing the Splunk web GUI |

Applications and Virtual Machines

| Application and Virtual Machines | Component | Purpose |
| ----------- | --------- | ------- |
| Splunk | License Manager | Tracks daily ingestion limits and licensing |
| | Agent Management | For monitoring and Universal Forwarder management |
| | Monitoring Console | Dashboard for monitoring the cluster health |
| | Cluster Manager | Dashboard for monitoring the Indexer cluster |
| | Indexer | Provides data processing and storage for local and remote data |
| | Search Head | Distributes searches to Indexers and can run searches based off these ingested logs |
| | Forwarders | Universal Forwarders installed on Windows and Linux endpoints for log gathering and sending to Indexers |
| Windows Server 2022 | Active Directory |
| | NTP | Central time keeping to ensure all events correlate across all devices within the lab |
| | DNS | Resolve IP address to names |
| | DHCP | Assignment of IP addresses |
| | LDAP | Access control and authentication |
| | Certificate Authority | Root CA authority |

## Repository Structure

- [01_design_documentation](01_design_documentation) | High level network design documentation including appendices for topologies, IP addressing, and verification documentation.
- [02_configurations](02_configurations) | Copy of configuration files for network devices and servers.

## How to Explore

1. Open the [lab_design_document](01_design_documentation/1_1_lab_design/lab_design_document.md) which is the main document for Splunk Labs that describes the high level decisions made.  

2. You can also find appendices under the 'verification and testing' directory which includes the master [IP addressing table](01_design_documentation/1_1_lab_design/appendices/appendix_c_logical_addressing.md) for all the IP addresses used as well simple [physical](01_design_documentation/1_1_lab_design/appendices/appendix_a_physical_topology.md) and [logical](01_design_documentation/1_1_lab_design/appendices/appendix_c_logical_addressing.md) topologies and other verficiation pages with screenshots.

2. Review the configuration documents for reference  
   Open [02_configurations](02_configurations) to see device configuration files.

3. Check the verification screenshots for successful proof-of-concept and deployment of Splunk on GNS3.  
   Open [appendix_e_splunk](01_design_documentation/1_2_verification_and_testing/appendix_e_splunk.md) to see screenshots of various configuration and deployment milestones.

## Success Criteria

The following screenshots are the culmination of various steps and prerequisites that were configured in order to successfully achieve the goal of Splunk Labs. To build a simple cross platform lab that proves the ability to forward logs from endpoints to a distributed cluster environment.

### Windows 2022 Server

![alt text](03_assets/3_1_images/splunk_ui/windows_forwarder_logs_final.png)  

### Ubuntu 24.04 LTS Server

![alt text](03_assets/3_1_images/splunk_ui/linux_forwarder_logs_final.png)  

### Windows 2022 and Ubuntu 24 Server

![alt text](03_assets/3_1_images/splunk_ui/windows_linux_forwarders_logs_final.png)  

To see other configurations within this lab, please refer to the separate [appendices](../1_2_verification_and_testing).
