# Local Admin Password Solution

Local Administrator Password Solution \(short LAPS\) will solve the issue of using an identical account on every Windows computer in a domain environment. On its own, LAPS creates a randomly generated password for a local admin account.

With RealmJoin it is possible to manage secure and individualized administrative accounts, either for local support or remote support, on a large scale. RealmJoin saves encrypted passwords in [Azure Key Vault](keyvault.md) within the customer's tenant and the Azure Audit records all accesses to these passwords.

## Prerequirements

Before you can start with LAPS you have to meet the following prerequirements:

* You must use **Application Insights**
* You must have configured certain **policies**

We'll look at both of them below:

### Application Insights

Application Insights has a very important role when using LAPS. The password requests triggered by LAPS are logged by Application Insights. Thus it can be tracked at any time who has made a password request and when and where this request was made.

More details can be found in our [Application Insight article](application-insights.md).

### Configuration Policies

RealmJoin offers multiple policies to configure local administrator account management. These policies  are described in the following table: 

<table>
  <thead>
    <tr>
      <th style="text-align:left">Policy (Key)</th>
      <th style="text-align:left">Value (Sample)</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">LocalAdminManagement.Inactive</td>
      <td style="text-align:left">true/false</td>
      <td style="text-align:left">
        <p>Deactivates or activates local</p>
        <p>administrator management</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">LocalAdminManagement.CheckInterval</td>
      <td style="text-align:left">&quot;00:30&quot;</td>
      <td style="text-align:left">
        <p>Interval for configuration checks</p>
        <p>(hh:ss)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>LocalAdminManagement.</p>
        <p>[EmergencyAccount/SupportAccount].NamePattern</p>
      </td>
      <td style="text-align:left">&quot;ADM-(HEX:8)&quot;</td>
      <td style="text-align:left">Admin name. HEX:8 stands for 8-digit random hex-code</td>
    </tr>
    <tr>
      <td style="text-align:left">LocalAdminManagement.[EmergencyAccount/SupportAccount].DisplayName</td>
      <td
      style="text-align:left">&quot;RealmJoin Local Administrator&quot;</td>
        <td style="text-align:left">Display name of administrator account (appears on Windows)</td>
    </tr>
    <tr>
      <td style="text-align:left">LocalAdminManagement.[EmergencyAccount/SupportAccount].PasswordCharSet</td>
      <td
      style="text-align:left">&quot;!#%+23456789:=?@ABCDEFGHJK LMNPRSTUVWXYZabcdefghijkmn opqrstuvwxyz&quot;</td>
        <td
        style="text-align:left">Charset of the password</td>
    </tr>
    <tr>
      <td style="text-align:left">LocalAdminManagement.[EmergencyAccount/SupportAccount].PasswordLength</td>
      <td
      style="text-align:left">20</td>
        <td style="text-align:left">Password length</td>
    </tr>
    <tr>
      <td style="text-align:left">LocalAdminManagement.[EmergencyAccount/SupportAccount].PasswordPreset</td>
      <td
      style="text-align:left">1</td>
        <td style="text-align:left">Predefined password templates (PasswordCharSet and PasswordLength not
          necessary)</td>
    </tr>
    <tr>
      <td style="text-align:left">LocalAdminManagement.[EmergencyAccount/SupportAccount].MaxStaleness</td>
      <td
      style="text-align:left">12:00</td>
        <td style="text-align:left">Time after account will be removed/refreshed (when logged out after use)</td>
    </tr>
    <tr>
      <td style="text-align:left">LocalAdminManagement.SupportAccount.OnDemand</td>
      <td style="text-align:left">true/false</td>
      <td style="text-align:left">Create support account on demand (account will expire after 12 hours)</td>
    </tr>
  </tbody>
</table>

For example:

**Key:**   
`LocalAdminManagement.SupportAccount`  
**Value:**  
`{  
"CheckInterval": "00:30",  
"NamePattern": "ADM-(HEX:8)",  
"DisplayName": "RealmJoin Local Administrator",  
"OnDemand": true  
}`

#### Configuration Policies based on User Groups

It is possible to assign these policies based on user groups. For example, deactivate local administrator management for all users except a specific group:

| Key | Value | Groupname |
| :--- | :--- | :--- |
| Local.AdminManagement.Inactive | true | RealmJoin - All Users |
| Local.AdminManagement.Inactive | false | CFG - RealmJoin-EnableSupportAdmin |

## Access

When a support member needs to access a secret, RealmJoin will provide an interface to get account and password credentials. When this happens, an update-secret command will be sent to the client and the admin account will be recreated.

## Administrator Account Types

Two different account types are available. An **Emergency Administrator Account** and a **Support Administrator Account**

### Emergency Administrator Account

This account type will be created by default and is **available persistently** on the device. Thus, it is possible to get administrative access even when there is no internet connection available or when facing other connection problems.

A corresponding RealmJoin policy can trigger the creation of a persistent administrator account. The following process will be passed:

1. Starting point: Existing or new client with RealmJoin a\) Existing client \(Azure AD joined, Intune managed, RealmJoin agenda installed\) b\) New client \(initialization during OOBE, Azure AD join, Intune enrollment, installation of RealmJoin and deployed software\)
2. RealmJoin policy triggers RealmJoin agent to create a persistent administrator account on the client.
3. RealmJoin agent transfers the encrypted password to the RealmJoin backend.
4. RealmJoin backend stores the cyphertext into a customer-owned [Azure KeyVault](keyvault.md).

A requirement for this process is a successful deployment of corresponding policy to the client.

#### Use in case of support

Support staff needs local administrative rights in-field support \(e. g. for troubleshooting connectivity issues\). Therefore, he/she must go through the following steps:

1. The staff visits the RealmJoin WebUI. On the device details, he/she will see the name of the administrator account and can request the password when clicking on the dotted text.
2. RealmJoin pulls the password from Azure Key Vault and displays it.
3. The staff is now able to get elevated rights by entering this username and password in the UAC credential prompt or performing a re-login as an administrator.
4. When the staff has finished all tasks, he/she logs out of the account.
5. The previously used account will be deleted after a defined period and a new one will be generated \(following to steps already described\).

![](../../.gitbook/assets/rj-laps1.png)

### Support Administrator Account

A support account will be generated **on demand** and is designed for **one-time use**.

A support staff can trigger the creation of a temporal administrator account. The following process will be passed:

1. Starting point: Existing or new client with RealmJoin a\) Existing client \(Azure AD joined, Intune managed, RealmJoin agent installed\) b\) New client \(initialization during OOBE, Azure AD join, Intune enrollment, installation of RealmJoin and deployed software\)
2. A Support staff requests a support account via RealmJoin WebUI
3. This triggers RealmJoin agent to create a temporal administrator account on the client.
4. RealmJoin agent transfers the encrypted password to the RealmJoin backend.
5. RealmJoin backend stores the cyphertext into customer-owned [Azure KeyVault](keyvault.md). 

Requirements for this process:

* Successful deployment of corresponding of the client.
* The user is logged in and RealmJoin agent is running.
* Internet connectivity.

#### Use in case of support

The support staff visits the RealmJoin WebUI again \(depends on the **Configuration check interval**\) and follows these steps:

1. On the device details, he/she will see the name of the temporal administrator account. The account creation will be started when clicking on **Request**.

![](../../.gitbook/assets/rj-laps2.png)

{% hint style="info" %}
After a certain time, the credentials will appear. Click the dotted password field to request the password.
{% endhint %}

1. RealmJoin pulls the password from Azure Key Vault and displays it.
2. The staff is now able to get elevated rights by entering this username and password in the UAC credential prompt or performing a re-login as an administrator.
3. When the staff has finished his tasks, he/she logs out of the account.
4. The previously used account will be deleted after a defined period

![](../../.gitbook/assets/rj-laps3.png)

