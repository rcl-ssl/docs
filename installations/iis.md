---
title: Microsoft IIS
parent: Certificate Installations
nav_order: 4
---

# Installing TLS/SSL Certificates in IIS

This article assumes that you have experience with IIS.

# Get the Certificate Files Manually

You can download the files required to install the TLS/SSL certificate in IIS from the **RCL Portal** on the **Certificate Details** page.

## Files Required

The files required are :

- Certificate PFX file (.pfx)

On some operating systems, .pfx files may be downloaded with a .p12 extension. To resolve this issue, left click the link to download the file and click 'Save link as..'. In the save dialog, change the file extension to .pfx. You can also change the file extension from .p12 to .pfx, or vice versa, after the file is downloaded.

# How To Import The PFX (PKCS12) File Into Microsoft IIS

Importing a PFX (PKCS12) file into Windows IIS is generally a straight-forward process.

Step 1 : Click “Start” and choose “Run”.

Step 2 : In the “Run” dialogue box type “MMC” and click “OK”. The MMC should then appear.

Step 3 : Go to the File tab or menu and select “Add / Remove Snap-In”.

Step 4 : Click on “Certificates” and click “Add”.

Step 5 : Select “Computer Account” and click “Next”.

Step 6 : Select “Local Computer” and click “Finish”.

Step 7 : Click “OK” to close the “Add / Remove Snap-In” window.

Step 8 : Double click on “Certificates (Local Computer)” in the center window.

Step 9 : Right click on the “Personal Certificates Store” folder.

Step 10 : Choose “ALL TASKS” then select “Import”.

Step 11 : Follow the “Certificate Import Wizard” to import your “Primary Certificate” from the .PFX file.

Step 12 : Browse to the .PFX and enter the associated password when prompted. Enter the certificate password you assigned when creating the certificate in the RCL portal. You can find this password in the Certificate Details page (Certificate Password) of the RCL portal.

Step 13 : If desired, check the box to “Mark This Key As Exportable”. We recommend choosing this option.

Step 14 : When prompted, choose to automatically place the Certificates in the Certificate Stores based on the type of the Certificate.

Step 15 : Click “Finish” to close the Certificate Import Wizard.

Step 16 : Close the MMC console. It is not necessary to save any changes that you have made to the MMC console.

The SSL Certificate, Private Key and any Intermediate Certificates should now be imported into your server. You must now follow the instructions below to bind your SSL Certificate to your website profile.

# How To Bind An SSL Certificate In Microsoft IIS

Once the SSL Certificate has been imported it is important to now bind the SSL Certificate to your website so that the website functions correctly. Your SSL Certificate will not function until the following steps are completed.

Step 1 : Click “Start”, “Administrative Tools” and then choose Internet Information Services (IIS) Manager.

Step 2 : Click on the server name and expand the “Sites” folder.

Step 3 : Locate your website (usually this will be called “Default Web Site”) and click on it.

Step 4 : From the “Actions” menu (on the right) click on “Site Bindings” or similar.

Step 5. In the “Site Bindings” window, click “Add” or similar. This will open the “Add Site Binding” window.

Step 6 : Under “Type” choose https. The IP address should be the corresponding dedicated IP address of the site or “All Unassigned”. The “Port” which traffic will be secured by SSL is usually 443. The “SSL Certificate” field should specify the SSL Certificate that was installed during the import process above.

Step 7 : Click “OK”.

Step 8 : Your SSL Certificate should now be installed and functioning correctly in conjunction with your website. Occasionally a restart of IIS may be required before the new SSL Certificate is recognized.

# Automatically Installing Certificates with RCL CertificateBot

You can automate the certificate renewal and installation process for IIS by using RCL CertificateBot.

This article will provide instructions on how to install RCL CertificateBot in Windows :

[Installing RCL CertificateBot in Windows](../certbot/windows-service)

This article will provide instructions on how to configure RCL CertificateBot for IIS :

[Using RCL CertificateBot with Microsoft IIS](../certbot/iis)



