---
title: Linux Daemon
parent: CertificateBot
nav_order: 3
---

# RCL CertificateBot for Linux

RCL CertificateBot runs as a **Daemon** in a Linux Server. The daemon will run every four (4) days to automatically renew and save TLS/SSL certificate from a user's subscription in the **RCL Portal** to a Linux Server.

## Automatically Renew TLS/SSL Certificates

You can use RCL CertificateBot to automatically renew TLS/SSL certificates created in the **RCL Portal** using the the following creation options :

- Azure DNS (including SAN) - Recommended
- Azure Key Vault (including SAN)

**'Stand Alone' certificates are not supported by RCL CertificateBot.**


## Download and Extract the Daemon Files to the Linux Server

- You will download the files from the RCL CertificateBot GitHub Project Page in the [Releases](https://github.com/rcl-letsencrypt-auto-ssl/RCL.LetsEncrypt.CertBot/releases) section; and extract it to your Linux Server in the ``/usr/sbin`` folder:

- In your Linux server, navigate to the ``/usr/sbin`` folder

```bash
cd /usr/sbin
```

- Run the command in the folder to download and extract the ``linux-x64`` files:

```bash
wget -c https://github.com/rcl-letsencrypt-auto-ssl/RCL.LetsEncrypt.CertBot/releases/download/v2/rclcertbot-linux-x64.tar.gz -O - | sudo tar -xz
```

or ``linux-arm`` files :

```bash
wget -c https://github.com/rcl-letsencrypt-auto-ssl/RCL.LetsEncrypt.CertBot/releases/download/v2/rclcertbot-linux-arm.tar.gz -O - | sudo tar -xz
```

## Configure the Daemon

### Register an AAD Application

An Azure Active Directory (AAD) application must be registered to obtain permission to access a user's Azure resources and to make authorized requests to the [RCL API](../api/api). 

Please refer to the following link to register an AAD application:

- [Registering an AAD Application](../authorization/aad-application)

### Set Access Control for the AAD Application

Access control must be set for the AAD application to access resources in a user's Azure subscription. Please refer to the following link to set access control :

- [Setting Access Control for the AAD Application](../authorization/access-control-app)

### Get the AAD Application Credentials 

Please refer to the following link to get the AAD Application credentials to configure the daemon :

- [Get the AAD Application Credentials](../authorization/aad-application#get-the-aad-application-credentials)

### Add the Configuration variables

- Navigate to the folder you downloaded and extracted the daemon files :

```bash
cd /usr/sbin/rclcertbot-linux-x64
```

or for ``arm``

```bash
cd /usr/sbin/rclcertbot-linux-arm
```

- Use nano (or other text editor) to edit the **appsettings.json** file in the folder

```bash
sudo nano appsettings.json
```

- Add the credentials for the AAD Application in the **Auth** section
  - client_id
  - client_secret
  - tenantId

- In the **CertBot** section, set a folder path to save the TLS/SSL certificates. Recommended path : /etc/ssl/rclcertbot

  - saveCertificatePath

- Create the folder in the server and ensure it has read/write permissions so that the certificates can be saved to it. 

```bash
sudo mkdir /etc/ssl/rclcertbot
```

- The ``includeCertificates`` settings will allow for including specific certificates by its name 
(eg: [ "contoso.com" ] or ["contoso.com, *.contoso.com"] for SAN) as an array of strings in the renewal operation. Multiple certificates can be also be set (eg: [ "contoso.com", "acme.com", "fabricam.com, *.fabricam.com" ]). To include all certificates in the renewal operation, leave the settings as [ "all" ]

- The ``serverIdentifier`` setting should be used to identify the server in which the daemon is being installed

```
{
  "Auth": {
    "client_id": "3434354ere455-6464-5456",
    "client_secret": "~irjhfyyr-6653gfghf",
    "tenantId": "47735-477635-46534"
  },
  "CertBot": {
    "saveCertificatePath": "/etc/ssl/rclcertbot",
     "includeCertificates": ["all"],
     "serverIdentifier": "default",
     "bindings": []
  },
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft": "Warning",
      "Microsoft.Hosting.Lifetime": "Information"
    },
    "EventLog": {
      "LogLevel": {
        "Default": "Information",
        "Microsoft.Hosting.Lifetime": "Information"
      }
    }
  },
  "LetsEncryptSDK": {
    "apiEndPoint": "https://letsencryptapi.azure-api.net",
    "armResource": "https://management.core.windows.net",
    "keyVaultResource": "https://vault.azure.net"
  }
}
```
- Save the updated **appsettings.json** file when you are done

# Add the Linux Daemon

## Create the Daemon

- Navigate to the **/etc/systemd/system** folder

```bash
cd /etc/systemd/system
```

- Create the daemon file

```bash
sudo touch rclcertbot.service
```

- Use nano (or other text editor) to edit the service file 

```bash
sudo nano rclcertbot.service
```

- Add the following code to the file

```bash
[Unit]
Description=RCL CertificateBot

[Service]
Type=notify
WorkingDirectory=/usr/sbin/rclcertbot-linux-x64
ExecStart=/usr/sbin/rclcertbot-linux-x64/RCL.LetsEncrypt.Certbot.LinuxDaemon

[Install]
WantedBy=multi-user.target

```

If you installed the ``arm`` version, change the directory to the arm path ``/usr/sbin/rclcertbot-linux-arm`` instead of ``/usr/sbin/rclcertbot-linux-x64`` in the 'WorkingDirectory' and 'ExecStart' settings

## Reload the Daemon

- Reload the daemon anytime you make changes to the service file

```bash
sudo systemctl daemon-reload
```

## Start the Daemon

- Run the code to start the daemon

```bash
sudo systemctl start rclcertbot
```

## View the Status of the Daemon

- Run the code to view the status of the daemon

```bash
sudo systemctl status rclcertbot
```

- You will see the status of the daemon. The most recent logs will also be displayed. 

- Ensure that there are no errors in the logs. If there are errors, the daemon is misconfigured and will not function

## View the Detailed Logs

- Run the command to view the daemon's detailed logs

```bash
sudo journalctl -u rclcertbot
```

## When you need to Stop the Daemon

- Run the code when you need to stop the daemon. When the daemon is stopped CertBot will discontinue certificate renewals and installation in the server.

```bash
sudo systemctl stop rclcertbot
```

# Fixing Errors

If you encounter errors in the logs for the daemon, please stop the daemon. Ensure the 'appsettings' configuration is correct for the AAD Application credentials and the certificate save path settings. The folder to save the certificate must have read/write access. Reload and restart the daemon after you make changes and check if the errors were resolved.

# Installing Certificates in Web Servers

RCL CertificateBot will save renewed TLS/SSL certificate files to a folder in the server. You should then configure the web server to use these files to implement SSL/TLS in your website.

Please follow the links below to configure your web server:

- [Installing TLS/SSL Certificates in Apache Server](../installations/apache)
- [Installing TLS/SSL Certificates in Apache Tomcat](../installations/apache-tomcat)
- [Installing TLS/SSL Certificates in NGINX](../installations/nginx)


