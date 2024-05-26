# Deploy App as a Linux Service

## Description

The following commands and configuration details outline the process of deploying an ASP.NET Core application as a Linux service.

## Command: Copy Published Files

```bash

sudo cp -r aspdotnet/published dotnet

dotnet dotnet/published/aspdotnetcore.dll

dotnet /ubuntu/home/dotnet/published/aspdotnetcore.dll

```

## Service Configuration


```
[Unit]
Description=ASP.NET Core Application
After=network.target

[Service]
Type=simple
WorkingDirectory=/home/ubuntu/dotnet/published
ExecStart=/usr/bin/dotnet /home/ubuntu/dotnet/published/aspdotnetcore.dll
Restart=always
RestartSec=10
SyslogIdentifier=aspnetcoreapp
User=ubuntu
Group=ubuntu

[Install]
WantedBy=multi-user.target
```

## Commands for Service Management

```
sudo nano aspnet_app.service
sudo mv aspnet_app.service /etc/systemd/system/
sudo systemctl daemon-reload
sudo systemctl start aspnet_app
sudo systemctl enable aspnet_app
sudo systemctl status aspnet_app
sudo nano /etc/systemd/system/aspnet_app.service
```