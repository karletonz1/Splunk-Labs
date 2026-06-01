# The UFW Configuration

References: <https://help.splunk.com/en/splunk-enterprise/administer/inherit-a-splunk-deployment/10.4/inherited-deployment-tasks/components-and-their-relationship-with-the-network>

All Ubuntu Servers (Global)

```text
sudo ufw default deny incoming

sudo ufw default allow outgoing

sudo ufw allow from 192.168.1.100 to any port 22

sudo ufw allow 8089/tcp

sudo ufw enable
```

Management Host

```text
Global Rules +

sudo ufw allow 8000/tcp
```

Search Head

```text
Global Rules +

sudo ufw allow 8000/tcp

sudo ufw allow 8191/tcp
```

Indexers

```text
Global Rules +

sudo ufw allow 9997/tcp

sudo ufw allow 9887/tcp 
```

Heavy Forwarder

```text
Global Rules +

sudo ufw allow 9997/tcp
```

Check the status of the UFW - `sudo ufw status`

Check rules with numbers - `sudo ufw status numbered`

Remove rules by numbers - `sudo ufw delete [number]`

Remove rules by protocol - `sudo ufw delete allow 8089/tcp`