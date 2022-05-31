
# list of software need to install for a CentOS server

1. net core

follow this guide
https://docs.microsoft.com/en-gb/dotnet/core/install/linux?WT.mc_id=dotnet-35129-website


for CentOS 9 Stream version

https://docs.microsoft.com/en-gb/dotnet/core/install/linux-rhel#centos-stream-9-

install runtime only. No need to install SDK

by command

sudo dnf install aspnetcore-runtime-6.0


2. Intall nginx Web server

step 1: make sure everything is up to date
sudo dnf update

step 2: Install nginx 

3. Install MariaDB

step 1: install command

sudo dnf install mariadb-server

step 2: Start mariadb, enable to make a service

sudo systemctl start mariadb
sudo systemctl enable mariadb
sudo systemctl status mariadb

step 3: set secure
mysql_secure_installation


4. Install fpt server for upload source code
step 1: Install VSFTPD


step 2. Make directory for website

mkdir [folder name]
chmod -R [permission] [folder name]

step 3: set full access for vsftpd
setsebool -P allow_ftpd_full_access on

step 4: remember turn off vsftp after use


5. Setup a service to run dotnet as a CentOS service
guideline: https://docs.microsoft.com/en-us/aspnet/core/host-and-deploy/linux-nginx?view=aspnetcore-6.0

create service like this
`
[Unit]
Description=Example .NET Web API App running on Ubuntu

[Service]
WorkingDirectory=/var/www/helloapp
ExecStart=/usr/bin/dotnet /var/www/helloapp/helloapp.dll
Restart=always
# Restart service after 10 seconds if the dotnet service crashes:
RestartSec=10
KillSignal=SIGINT
SyslogIdentifier=dotnet-example
User=www-data
Environment=ASPNETCORE_ENVIRONMENT=Production
Environment=DOTNET_PRINT_TELEMETRY_MESSAGE=false

[Install]
WantedBy=multi-user.target
`

setup nginx config file 
server {
    listen        80;
    server_name   example.com *.example.com;
    location / {
        proxy_pass         http://127.0.0.1:5000;
        proxy_http_version 1.1;
        proxy_set_header   Upgrade $http_upgrade;
        proxy_set_header   Connection keep-alive;
        proxy_set_header   Host $host;
        proxy_cache_bypass $http_upgrade;
        proxy_set_header   X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header   X-Forwarded-Proto $scheme;
    }
}

