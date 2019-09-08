# Local Admin Password Solution

Local Administrator Password Solution \(short **LAPS**\) is a Microsoft tool which will solve the issue of using an identical account on every Windows computer in a domain environment. Currently there is no such solution available for Azure AD environments.

With RealmJoin it is possible to manage secure and individualized administrative accounts, either for local support or remote support, on a large scale.RealmJoin saves encrypted passwords in **Azure Key Vault** within the customers tenant and the Azure Audit records all accesses to these passwords.

## Prerequirements

### Application Insights

Application Insights is an important part of LAPS. Click [here](keyvault.md) to see details about Application Insights:

### Group Configuration

<table>
  <thead>
    <tr>
      <th style="text-align:left">
        <p><b>LocalAdminManagement.EmergencyAccount</b>
        </p>
        <p>Default Value / Sample Value / Description</p>
      </th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>.NamePattern</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">&quot;ADM-{HEX:8}&quot;</td>
      <td style="text-align:left">&quot;Admin-{HEX:4}&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">Pattern to create randomized accounts.</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>.DisplayName</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">&quot;RealmJoin Local Administrator&quot;</td>
      <td style="text-align:left">&quot;Local Emergency Admin&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">Display name of administrator account.</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>.PasswordCharSet</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">(See note below)</td>
      <td style="text-align:left">&quot;0123456789ABCDEFabcdef&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">Charset of the random generated password.</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>.PasswordLength</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">20</td>
      <td style="text-align:left">30</td>
    </tr>
    <tr>
      <td style="text-align:left">Length of password in characters.</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>.MaxStaleness</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">&quot;00:45&quot;</td>
      <td style="text-align:left">&quot;00:45&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left">Delete and recreate profile after last use.</td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>{% hint style="info" %}
Default Password Char Set excludes similar looking characters:  
  
`!#%+23456789:=?@ABCDEFGHJKLMNPRSTUVWXYZabcdefghijkmnopqrstuvwxyz`
{% endhint %}

## Access

When a support member needs to access a secret, RealmJoin will provide an interface to get account and password. When this happens, an update-secret command will be send to the client and the admin account will be recreated.

## Administrator Account Types

Two different account types are available. An **Emergency Administrator Account** and a **Support Administrator Account**

### Emergency Administrator Account

This account type will be created by default and is **available persistently** on the device. Thus, it is possible to get administrative access even when there is no internet connection available or when facing other connection problems.

A corresponding RealmJoin policy can trigger the creation of a persistent administrator account. The following process will be passed:

1. Starting point: Existing or new client with RealmJoin a\) Existing client \(Azure AD joined, Intune managed, RealmJoin agenda installed\) b\) New client \(initialization during OOBE, Azure AD join, Intune enrollment, installation of RealmJoin and deployed software\)
2. RealmJoin policy triggers RealmJoin agent to create a persistent administrator account on the client.
3. RealmJoin agent transfers the encrypted password to the RealmJoin backend.
4. RealmJoin backend stores the cyphertext into a customer owned [Azure Key Vault](keyvault.md).

A requirement for this process is a successful deployment of corresponding policy to the client.

#### Use in case of support

A support staff needs local administrative rights in field support \(e. g. for troubleshooting connectivity issues\). Therefore, he/she must go through the following steps:

1. The staff visits the RealmJoin WebUI. On the device details he/she will see the name of the administrator account and can request the password when clicking on the dotted text.

[![Request password for emergency admin](../.gitbook/assets/rj-laps1.png)](https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/rj-laps1.png)

1. RealmJoin pulls the password from Azure Key Vault and displays it.
2. The staff is now able to get elevated rights with entering this username and password in the UAC credential prompt or performing a re-login as an administrator.
3. When the staff has finished all tasks, he/she logs out of the account.
4. The previously used account will be deleted after a defined period and a new one will be generated \(following to steps already described\).

### Support Administrator Account

A support account will be generated **on demand** and is designed for **one-time use**.

A support staff can trigger the creation of a temporal administrator account. The following process will be passed:

1. Starting point: Existing or new client with RealmJoin a\) Existing client \(Azure AD joined, Intune managed, RealmJoin agent installed\) b\) New client \(initialization during OOBE, Azure AD join, Intune enrollment, installation of RealmJoin and deployed software\)
2. A Support staff requests a support account via RealmJoin WebUI
3. This triggers RealmJoin agent to create a temporal administrator account on the client.
4. RealmJoin agent transfers the encrypted password to the RealmJoin backend.
5. RealmJoin backend stores the cyphertext into customer owned [Azure Key Vault](keyvault.md).

Requirements for this process:

* Successful deployment of corresponding of client.
* User is logged in and RealmJoin agent is running.
* Internet connectivity.

#### Use in case of support

The support staff visits the RealmJoin WebUI again \(depends on the **Configuration check interval**\) and follows these steps:

1. On the device details he/she will see the name of the temporal administrator account. The account creation will be started when clicking on **Request**.

[![Request password for support admin](../.gitbook/assets/rj-laps2.png)](https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/rj-laps2.png)

{% hint style="info" %}
After a certain time, the credentials will appear. Click the dotted password field to request the password.
{% endhint %}

1. RealmJoin pulls the password from Azure Key Vault and displays it.

[![Request password for emergency admin](../.gitbook/assets/rj-laps3.png)](https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/rj-laps3.png)

1. The staff is now able to get elevated rights with entering this username and password in the UAC credential prompt or performing a re-login as an administrator.
2. When the staff has finished his tasks, he/she logs out of the account.
3. The previously used account will be deleted after a defined period

