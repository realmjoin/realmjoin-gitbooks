# Connecting a Tenant

To a connect a tenant to the Glück & Kanja RealmJoin back-end, a **Hello Token** is needed. This token might be requested from Glück & Kanja. A RealmJoin administrator group has to be created upfront in AAD with the name **cfg-RealmJoin Admin** and all dedicated RealmJoin administrators should be added to it. The **Connect Wizard** is located under the URL [RealmJoin connect](https://realmjoin-web.azurewebsites.net/global/graph). The token and the tenant name are to be entered and the request submitted.

[![RJ connection interface](../.gitbook/assets/rj-connect-tenant.png)](https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/rj-connect-tenant.png)

A tenant administrator has to give consent to RealmJoin. The Connect Wizard creates the necessary entries in Intune. After the success, it is important to revisit the first tab/browser window and the **Check&Install** option as to be executed.

### RealmJoin Permissions

The following permissions are admitted by the administrator consent and set in Azure via the GraphAPI:

[![RJ azure permissions](../.gitbook/assets/rj-realmjoin-permissions.png)](https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/rj-realmjoin-permissions.png)

### Default software for new tenants

After successful connection the following software packages are provided as default in RealmJoin portal:

* Choco Extension RealmJoin Core
* Google Chrome
* Microsoft Office 365 ProPlus
* Microsoft Teams
* Mozilla Firefox
* RealmJoin Core Extension
* RealmJoin Win10 Core Settings System
* RealmJoin Win10 Remove Suggested Apps
* RealmJoin Win10 Update Start Layout
* RealmJoin Win10 Pin Unpin
* RealmJoin Win10 Remove Provisioned Apps
* Generic RealmJoin Configure OneDrive
* Genereic Windows Activation
* MS Office with user settings and proofing tools  
* 7-Zip
* GlueckKanja RealmJoin Publish State Computer System Information
* GlueckKanja RealmJoin Publish State Speculation Control Settings

In addition, the following policies are part of a tenant for all RJ Users:

* Environment.Channel \(beta\)
* Integration.AnyDesk
* LocalAdminManagement
* Policies.ExplorShortcuts
* Policies.DisableNetworkLocationWizard
* WebLinks

