# Ubuntu Server Configuration settings

## Server Hostname Change

```text
sudo hostnamectl set-hostname <target-hostname>

echo "127.0.1.1 $(hostname)" | sudo tee -a /etc/hosts

sudo reboot
```

## Local User Account Creation and Install

`sudo groupadd splunk`

`sudo useradd -m -g splunk -s /bin/bash splunk`

`sudo dpkg -i splunk*.deb`

`sudo chown -R splunk:splunk /opt/splunk`

`sudo -u splunk /opt/splunk/bin/splunk start --accept-license`

`sudo /opt/splunk/bin/splunk enable boot-start -user splunk`

(Non-Management Nodes only)  
`sudo -u splunk /opt/splunk/bin/splunk edit cluster-config -mode peer -manager_uri https://10.10.2.10:8089 -replication_port 9887 -secret [password]`

(Search Head only)  
`sudo -u splunk /opt/splunk/bin/splunk edit cluster-config -mode searchhead -manager_uri https://10.10.2.10:8089 -secret [password]`

## Disable Web GUI

`sudo /opt/splunk/bin/splunk disable webserver`

## Link Search Head with Indexer Peer

`sudo /opt/splunk/bin/splunk add search-server -host https://10.10.3.10:8089 -auth admin:[password]`

verify - `nc -vz 10.10.3.10 8089`

verify - `sudo ss -tulnp | grep 8089`

## Link forwarder to Management node

`sudo /opt/splunkforwarder/bin/splunk set deploy-poll 10.10.2.10:8089`

verify - `nc -vz 10.10.2.10 8089`

verify - `sudo ss -tulnp | grep 8089`

## Enable Specific Port Listening on Linux Server

`sudo -u splunk /opt/splunk/bin/splunk enable listen [ Port ]`

## LDAP Configuration File

```text
 [authentication]
authType = LDAP
authSettings = Splunk_Labs_AD

[Splunk_Labs_AD]
SSLEnabled = 0
bindDN = CN=splunk svc,CN=Users,DC=splunk,DC=labs
bindDNpassword = $7$8Z0hVGL1GkvNSsFNiB9gay6YNfPXmFHGOm2JeHpcq0KtzyXir35S9C6mMA==
host = 10.10.1.2
port = 389
realNameAttribute = displayName
userBaseDN = CN=Users,DC=splunk,DC=labs
userNameAttribute = sAMAccountName
groupBaseDN = DC=splunk,DC=labs
groupMappingAttribute = dn
groupMemberAttribute = member
groupNameAttribute = cn
nestedGroups = 1

[roleMap_Splunk_Labs_AD]
admin = Splunk_admins
user = Splunk_users
```

## Splunk Management/indexer/search head Node Shutdown/Maintenance Mode  

On the Manager: Turn on maintenance mode.  
`sudo /opt/splunk/bin/splunk enable maintenance-mode`  
`sudo /opt/splunk/bin/splunk disable maintenance-mode`  
`sudo /opt/splunk/bin/splunk show maintenance-mode`  

On BOTH Indexers: Stop the Splunk services. Wait for them to completely shut down before touching the Manager again.  
`sudo /opt/splunk/bin/splunk stop`

On the Manager: After Indexers are shutdown, stop the Manager's Splunk service.  
`sudo /opt/splunk/bin/splunk stop`  

On all three VMs: Finally, run the OS shutdown command to power them off.  
`sudo shutdown -h now`

> [!NOTE]
> Always shut the Indexers down first, and turn the Manager off last.

## Troubleshooting

Restarting Splunk and Forwarders  
`sudo -u splunk /opt/splunk/bin/splunk restart`  
`sudo /opt/splunkforwarder/bin/splunk restart`  
`sudo -u splunk /opt/splunk/bin/splunk reload deploy-server`  

Starting and Stopping Splunk and Forwarders  
`sudo /opt/splunkforwarder/bin/splunk stop`  
`sudo /opt/splunkforwarder/bin/splunk start`  
`sudo /opt/splunk/bin/splunk stop`  
`sudo /opt/splunk/bin/splunk start`  

Splunk and forwarder logs Commands  
`sudo -u splunk tail -f /opt/splunkforwarder/var/log/splunk/splunkd.log`  
`sudo -u splunk tail -f /opt/splunk/var/log/splunk/splunkd.log`  

Agent Manager Logs Commands  
`sudo -u splunk grep -i "deploy\|client\|phonehome" /opt/splunk/var/log/splunk/splunkd.log | tail -n 30`  

Check UF SSL Enforcement Commands  
`sudo -u splunkfwd /opt/splunkforwarder/bin/splunk btool server list sslConfig --debug | grep -i "requireClientCert\|sslVersions"`  

Check UF Global Password  Command  
`sudo -u splunkfwd /opt/splunkforwarder/bin/splunk btool server list general --debug | grep -i pass4SymmKey`  

SSH Connection test Commands  
`sudo tail -f /opt/splunkforwarder/var/log/splunk/splunkd.log | grep -i "deploymentclient"`  

`sudo -u splunk grep -i "deploymentclient\|handshake\|phonehome" /opt/splunkforwarder/var/log/splunk/splunkd.log | tail -n 20`  

verify - `nc -vz 10.10.2.10 8089`  

verify - `sudo ss -tulnp | grep 8089`  

Checking if server is sending logs to Indexers

`sudo nano /opt/splunkforwarder/etc/system/local/outputs.conf`

`sudo nano /opt/splunkforwarder/etc/system/local/inputs.conf`

`sudo /opt/splunkforwarder/bin/splunk list forward-server`

`sudo chown -R splunk:splunk /opt/splunkforwarder`

`sudo /opt/splunkforwarder/bin/splunk start`

## Deployment Server/Client Config  Commands

`sudo nano /opt/splunkforwarder/etc/system/local/deploymentclient.conf`  
`sudo nano /opt/splunk/etc/system/local/serverclass.conf`  
`sudo nano /opt/splunk/etc/system/local/outputs.conf`  

Troubleshooting  
`sudo -u splunk /opt/splunk/bin/splunk btool serverclass list --debug`  
`sudo -u splunk /opt/splunkforwarder/bin/splunk show deploy-poll`  

Verify deployment clients that have contact Agent Manager Command  
`sudo -u splunk /opt/splunk/bin/splunk list deploy-clients`  
