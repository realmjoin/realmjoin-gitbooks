# Troubleshooting

## Possible reasons why a software package might not install

**1. The software package is not properly assigned to the user**

* In Azure AD: Is there a software distribution group for this software and is the user member of this group?  
* In RealmJoin Admin Portal: Is there a package for this software and is this package assigned to the correct Azure AD group?  
* Is the software package assigned for automatic or manual install?  

**2. The software is assigned but the assignment is not received by the client**

* Is RealmJoin running?
* Is the RealmJoin configuration up to date?
* Is the RealmJoin version up to date?
* Are there any errors in the RealmJoin logs?

**3. The assignment reaches the client but the installation is not started or fails**

* Is the software assigned for manual installation?
* Is it possible to start the installation manually and are there any errors shown?
* Check RealmJoin logs and software installation logs if available?

## Review installed & available software

Find the RealmJoin icon in your taskbar.

[![Tray](.gitbook/assets/rj-tray.png)](https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/rj-tray.png)

Click the RealmJoin icon and click **Software Packages**. Check if the software is listed and which status is displayed. Grayed-out indicated software is already installed. 'Black Text' \(ready to install\) indicates software is not installed. In this case the installation failed or the software package is configured for manual installation.

[![Tray-Menu](.gitbook/assets/rj-tray-menu.png)](https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/rj-tray-menu.png)

Click the software if it is shown as ready to install. This should start the software installation. Click **Show Details**

[![Install-Citrix](.gitbook/assets/rj-install-citrix.png)](https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/rj-install-citrix.png)

Select and copy everything in the details if the software installation fails. Attach this information to the incident ticket.

[![Install-Citrix-Details](.gitbook/assets/rj-install-citrix-details.png)](https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/rj-install-citrix-details.png)

## RealmJoin Log Files

### Logging

RealmJoin records all event data into log files. Those can easily be accessed on the client device using the Windows Event Viewer \(eventvwr.msc\). RealmJoin logs can be found under **Event Viewer \(Local\) / Windows Logs / Application**.

To troubleshoot package execution problems or RealmJoin Problems there are several Log Files available:

System Context Installations and other system tasks: `C:\Windows\Logs\realmjoin.log`

[![Log](.gitbook/assets/rj-log-one.png)](https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/rj-log-one.png)

User Context Installations and other tray component tasks: `%LocalAppData%\RealmJoin\tray.log`

[![Log](.gitbook/assets/rj-log-two.png)](https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/rj-log-two.png)

RealmJoin Service events in the application eventlog.

[![Log](.gitbook/assets/rj-event-log.png)](https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/rj-event-log.png)

Chocolatey Install Logfiles: `C:\ProgramData\chocolatey\logs\chocolatey.log`

[![Log](.gitbook/assets/rj-choco-log.png)](https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/rj-choco-log.png)

MSI Installations logs.

[![Log](.gitbook/assets/rj-msi-log.png)](https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/rj-msi-log.png)

Alternatively the logs can be automatically collected and save to the current users desktop via the debug window \(see section below\).

## Debug Mode

To open the tray debug \(and enter the debug mode\) click **STRG + SHIFT + Click on the RealmJoin Icon**. The Client menu will open but with a further entry at the end of the menu: **Show Debug Window**.

Client menu:

[![RJclientmenu2](.gitbook/assets/rj-ui4.png)](https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/rj-ui4.png)

Tray debug:

[![RJtraydebug](.gitbook/assets/rj-ui5.png)](https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/rj-ui5.png)

Show Debug Window contains seven different diagnostic tools. If a device is not able to be addressed by the server or can not connect to the back-end, this tool will provide the user with the tools for the first steps of diagnosis.

You can ping the RealmJoin back-end to check connectivity.

[![Advanced](.gitbook/assets/rjx-debug-menu-two.png)](https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/rjx-debug-menu-two.png)

You can check if the client version is up to date.

[![Advanced](.gitbook/assets/rjx-debug-menu-three.png)](https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/rjx-debug-menu-three.png)

You can check if the user configuration is up to date. This includes the assigned software packages.

[![Advanced](.gitbook/assets/rjx-debug-menu-four.png)](https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/rjx-debug-menu-four.png)

If a new user configuration is available you can update the configuration.

[![Advanced](.gitbook/assets/rjx-debug-menu-five.png)](https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/rjx-debug-menu-five.png)

You can reset the user configuration. After this is done it is required to update the user configuration with **Check Config**

[![Advanced](.gitbook/assets/rjx-debug-menu-six.png)](https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/rjx-debug-menu-six.png)

You can collect the RealmJoin log files automatically.

[![Advanced](.gitbook/assets/rjx-debug-menu-seven.png)](https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/rjx-debug-menu-seven.png)

## Verify Group Membership in Office 365 Admin Center

You need to know the software Distribution Group to which the software should be deployed.

Open Office 365 Admin Center Group management at: [Office 365 Admin Center](https://portal.office.com/adminportal/home#/groups)

[![O365 Portal](.gitbook/assets/o365-portal-one.png)](https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/o365-portal-one.png)

Select appropriate software distribution group and verify if the user is member of this group.

[![O365 Portal](.gitbook/assets/o365-portal-two.png)](https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/o365-portal-two.png)

## Token Error

There are several possible approaches to repair token errors.

### Delete Token.dat

To trigger a new token request, delete the file  
`C:\Users\username\AppData\Local\RealmJoin\token.dat`  
and restart your device. Newer RealmJoin \(starting with v4.10\) versions that detect broken tokens may repair them automatically.

### Reconnect to Domain

In the RealmJoin tray, you might use the **Reconnect to Domain** or **Change Domain Password** options to reinstate the connection authentication.

## RealmJoin Back-end

Replaced with Admin Console!

Go to RealmJoin back-end admin portal at: [RealmJoin back-end Portal](https://realmjoin-backend.azurewebsites.net)

[![RealmJoin Portal](.gitbook/assets/rjserver-one.png)](https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/rjserver-one.png)

In **Software** select the required software package. At the right users and groups are visible which have been assigned to this software package. In this example it has not been assigned to any individual user but to 2 groups. Assignments for automatic installation are shown in bold letters.

[![RealmJoin Portal](.gitbook/assets/rjserver-two.png)](https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/rjserver-two.png)

## Corrupted Chocolatey installation

If the installation of software packages produce error messages hinting to a corrupt Chocolatey installation, it is possible to reenforce the automatic Chocolatey installation through RealmJoin.  
To do so, remove the _%chocolatey%_ environment variable and enforce a reboot of the client machine and the RealmJoin agent. This will trigger a reinstallation of Chocolatey.

## How can I remove the RealmJoin application from a client?

It is not supported to remove the RealmJoin application from a client.  
However, for test scenarios, there are two ways to remove the application from a client.

1. Reimage the client.
2. Delete manually.

Manual deletion instruction:

* Stop all running RealmJoin processes
* Remove the service, execute "sc delete realmjoin"
* Remove the executables from C:\Program Files\RealmJoin
* Delete registry hive HKLM and HKCU\SOFTWARE\RealmJoin
* Delete folder %LocalAppData%\RealmJoin
* Delete folder C:\ProgramData\RealmJoin
* Uninstalling Chocolatey \([https://chocolatey.org/docs/uninstallation](https://chocolatey.org/docs/uninstallation)\)

## Where does RealmJoin file the package scripts on the client?

You may find the data as follows:

* Chocolatey install scripts: %PROGRAMDATA%\chocolatey\lib\\tools\chocolateyInstall.ps1  
* Chocolatey blobs:  Windows\Temp\chocolatey\\
* Craft scripts are cleaned up after the execution  

## How can I send feedback to the RealmJoin team?

Please use the official user voice website:  
[https://realmjoin.canny.io/features](https://realmjoin.canny.io/features)

## Where is the changelog located?

[https://headwayapp.co/realmjoin-platform-changelog](https://headwayapp.co/realmjoin-platform-changelog)

