# RealmJoin Portal

Device provisioning and RealmJoin configuration is done with the RealmJoin Portal. Administrative users have access to the RealmJoin Portal. Designed to mirror the style of the new Microsoft administration services, it is the main tool for the management of RealmJoin clients and users. RealmJoin incorporates the same group based user and policy management experience and uses the Azure AD defined groups as a basis for software deployment.

The default interval for group synchronization between Azure AD and RealmJoin is 15 minutes, while only groups with a defined prefix are taken into consideration. Only groups with at least one assigned user are synchronized (synchronization interval can be adjusted).

Click one of these links to get to the RealmJoin Portal:

* [Web application](https://realmjoin-web.azurewebsites.net)
* [Beta version](https://realmjoin-web-staging.azurewebsites.net)

The dashboard provides a quick and beneficial overview. All sections can be accessed by either clicking on the corresponding number or selecting the section in the toolbar on the left.

![](<../.gitbook/assets/realmjoin-portal-overview (1).PNG>)

### RealmJoin Toolbar

As you can see, there are several icons listed in the toolbar. Here is a brief explanation of each icon (links to more detailed information are provided).

#### Clients

![](<../.gitbook/assets/rj-ac-clientsicon (1) (1).png>)

A click on the Clients icon gives you a transparent overview over all enrolled devices as well as the respective primary user. For more details read our [Clients article](clients.md).

#### Users

![](<../media/rj-ac-usersicon (1).png>)

The Users icon gives you a list of all users assigned to the tenant. For more details read our [Users and User Settings article](users-and-user-settings.md).

#### User Settings

![](<../.gitbook/assets/rj-ac-usersettingsicon (1) (1).png>)

Via the User Settings icon, you have the possibility to configure user settings and policies. For more details read our [Users and User Settings article](users-and-user-settings.md).

#### Groups

![](<../.gitbook/assets/rj-ac-groupsicon (1).png>)

Via the Groups icon, you can see all groups registered in this tenant. For more details read our [Groups and Group Settings article](groups-and-group-settings.md).

#### Group Settings

![](<../.gitbook/assets/rj-ac-groupsettingsicon (1) (1).png>)

Via the User Settings icon, you have the possibility to configure group settings and policies. For more details read our [Groups and Group Settings article](groups-and-group-settings.md).

#### App Store

![](<../.gitbook/assets/rj-ac-storeicon (1).png>)

This icon takes you to the RealmJoin application store. For more details read our [App Store article](app-store.md).

#### Software Packages

![](<../.gitbook/assets/rj-ac-packagesicon (1) (1).png>)

A click on this icon gives you a list of all added packages. For more details read our [Software Packages article](software-packages.md).

#### Notifications

![](<../.gitbook/assets/rj-notification-icon (1).png>)

Click on this icon to create new notifications and edit existing notifications. For more details read [our corresponding article](../core-features/notifications.md).

#### Software Report

![](<../.gitbook/assets/rj-software-report-icon (1).png>)

Click on this symbol to open the 'Software Report' menu. In this menu you can see which software is in use and which users, groups or clients are using it. For more details read [our corresponding article](../core-features/software-report.md).

#### Request Packages

![](<../.gitbook/assets/rj-ac-uploadicon (1).png>)

If an application is not listed in the App Store or is in need of customization, a packaging request can be sent to Glück & Kanja. For more details read our [Request Package article](request-package.md).

###
