# PowerShell prompts for configuring NTP time server on Server 2022

Set server as NTP source

```text
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\W32Time\Config" -Name "AnnounceFlags" -Value 5
```

Enable NTP server service

```text
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\NtpServer" -Name "Enabled" -Value 1
```

Restart the time service

```text
Restart-Service w32time
```

Enable NTP through the Windows firewall

```text
New-NetFirewallRule -Name "Allow_NTP_In" -DisplayName "Allow NTP (UDP 123)" -Direction Inbound -Protocol UDP -LocalPort 123 -Action Allow
```
