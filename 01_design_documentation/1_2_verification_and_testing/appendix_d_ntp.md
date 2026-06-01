# Splunk Labs NTP server Confirmation  

## Domain Controller Settings

![alt text](<../../03_assets/3_1_images/NTP/NTP Domain Controller.png>)

## Ubuntu Server Verification

Commands

Configuration File - `sudo nano /etc/systemd/timesyncd.conf`  
Restart Time Engine - `sudo systemctl restart systemd-timesyncd`  
Verify NTP Source - `systemctl status systemd-timesyncd`  
Check Time Status - `timedatectl status`  

## karlo-splunk-mgmt  

![alt text](../../03_assets/3_1_images/NTP/splunk-mgmt-ntp.png)

![alt text](../../03_assets/3_1_images/NTP/splunk-mgmt-ntp-source.png)

## karlo-splunk-kvm  

![alt text](../../03_assets/3_1_images/NTP/splunk-kvm-ntp.png)  

![alt text](../../03_assets/3_1_images/NTP/splunk-mgmt-ntp-source.png)  

## karlo-splunk-indexer01

![alt text](../../03_assets/3_1_images/NTP/splunk-indexer1-ntp.png)  

![alt text](../../03_assets/3_1_images/NTP/splunk-indexer1-ntp-source.png)  

## karlo-splunk-indexer02

![alt text](../../03_assets/3_1_images/NTP/splunk-indexer2-ntp.png)  

![alt text](../../03_assets/3_1_images/NTP/splunk-indexer2-ntp-source.png)  

## karlo-splunk-sh

![alt text](../../03_assets/3_1_images/NTP/splunk-sh-ntp.png)  

![alt text](../../03_assets/3_1_images/NTP/splunk-sh-ntp-source.png)  

## karlo-remote-router

![alt text](../../03_assets/3_1_images/NTP/remote-router-ntp.png)  

## karlo-central-switch

![alt text](../../03_assets/3_1_images/NTP/central-switch-ntp.png)  
