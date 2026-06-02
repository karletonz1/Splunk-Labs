`sudo nano /etc/systemd/timesyncd.conf`

[Time]
NTP=10.10.1.2

sudo systemctl restart systemd-timesyncd

verification - `timedatectl status`

verification - `systemctl status systemd-timesyncd`
