# Connecting a Tenant

To connect a tenant to the Glück & Kanja RealmJoin back-end, a **Hello Token** is needed. This token can be requested from Glück & Kanja. A RealmJoin administrator group has to be created upfront in AAD with the name **cfg-RealmJoin Admin** and all dedicated RealmJoin administrators should be added to it. The **Connect Wizard** is located under the URL [RealmJoin connect](https://realmjoin-web.azurewebsites.net/global/graph). The token and the tenant name are to be entered and the request submitted.

{% hint style="info" %}
Sometimes if a new tab is used, the RealmJoin portal needs to log the admin user in first. This leads to the page reloading. In this case, open the link [RealmJoin connect](https://realmjoin-web.azurewebsites.net/global/graph) in the **same** browser  tab again.
{% endhint %}

![](../.gitbook/assets/rj-connect-tenant.png)

A tenant administrator has to give consent to RealmJoin. The Connect Wizard creates the necessary entries in Intune. After completion, it is important to revisit the first tab/browser window and the **Check&Install** option to be executed.

### RealmJoin Permissions

The following permissions are admitted by the administrator consent and set in Azure via the GraphAPI:

![](../.gitbook/assets/rj-realmjoin-permissions.png)

### Default configuration for new tenants

After successful connection the following software packages are provided as default in RealmJoin portal:

| Default Tenant Packages |
| :--- |
| Choco Extension RealmJoin Core |
| Google Chrome |
| Microsoft Office 365 ProPlus |
| MS Office with user settings and proofing tools |
| Microsoft Teams |
| RealmJoin Core Extension |
| RealmJoin Win10 Core Settings System |
| RealmJoin Win10 Remove Suggested Apps |
| RealmJoin Win10 Update Start Layout |
| RealmJoin Win10 Pin Unpin |
| RealmJoin Win10 Remove Provisioned Apps |
| Generic RealmJoin Configure OneDrive |
| Genereic Windows Activation |
| 7-Zip |
| GlueckKanja RealmJoin Publish State Computer System Information |
| GlueckKanja RealmJoin Publish State Speculation Control Settings |

