# Settings

The following article describes important settings for RealmJoin.

## BrancheCache.Mode

**Value**

```text
"Distributed"|"Undefinied"
```

**Description**

This setting changes BranchCache mode for **new** clients.

## **DomainConnect.CredentialName**

**Value**

```text
"RealmJoin (domain)"
```

**Description**

For more details about domain connect read the '[Domain Connect website](https://www.domainconnect.org/)'.

## DomainConnect.Domain

**Value**

```text
"domain.contoso.net"
```

**Description**

For more details about domain connect read the '[Domain Connect website](https://www.domainconnect.org/)'.

## DomainConnect.NetBIOS

**Value**

```text
"contoso"
```

**Description**

For more details about domain connect read the '[Domain Connect website](https://www.domainconnect.org/)'.

## Environment.Channel

**Value**

```text
"release" | "beta" | "canary"
```

**Description**

With this setting the user group switch channel on next auto-update.

## FirstRun.AfterSuccessAction

**Value**

```text
"none" | "logoff" | "restart"
```

**Description**

Action to perform after initial deployment screen \(default is _restart_\).

## FirstRun.EnableSecure Desktop

**Value**

```text
true | false
```

**Description**

Show deployment screen on restricted and secure desktop \(default is _true_\).

## Integration.AnyDesk

**Value**

```text
{
"Enabled": true, | false,
"BootstrapperUrl":"https://get.anydesk.com/GENERATED_LINK_TOKEN/RJAnyDesk.exe"
}
```

**Descritpion**

This setting enables or disables the AnyDesk feature**.**

## **Integration.ExecutionMonitor**

**Value**

```text
{
"Enabled": true, | false,
"UpdateInterval": "08:00"
}
```

**Description**

This setting enables or disables the ExecutionMonitor Feature.

## **Integration.Notification**

**Value**

```text
{
"Enabled": true, | false,
"SourceUrl": "URL_PROVIDED_BY_GKGAB",
"FallbackCulture": "en"
}
```

**Description**

This setting enables or disables the Notifier feature and it also activates or deactivates the editor UI.

## LocalAdminManagement.CheckInterval

**Value**

```text
"00:05"
```

**Description**

With this setting you confiure the interval for configuration checks \(hh:ss\).

## LocalAdminManagement.EmergencyAccount

**Value**

```text
{
    "MaxStaleness": "00:45",
    "NamePattern": "ADM-{HEX:4},
    "Display": "Local Emergency Account",
    "PasswordCharSet": "1234567890ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz",
    "PasswordLength": 14
}
```

**Description**

With this setting you can configure an emergency account. For more details about local admin management read our corresponding ['Local Admin Password Solution' article](local-admin-password-solution/). 

## LocalAdminManagement.SupportAccount

**Value**

LocalAdminManagement.SupportAccount

```text
{
    "MaxStaleness": "00:45",
    "NamePattern": "ADM-{HEX:4}",
    "DisplayName": "Local Support Administrator",
    "PasswordCharSet": "1234567890ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz",
    "PasswordLength": 14,
    "OnDemand": true | false
}
```

**Description**

With this setting you can configure a support account. For more details about local admin management read our corresponding ['Local Admin Password Solution' article](local-admin-password-solution/).

## LocalAdminManagement.Inactive

**Value**

```text
false
```

**Description**

This setting activates or deactivates local administrator management. For more details about local admin management read our corresponding ['Local Admin Password Solution' article](local-admin-password-solution/).

## Policies.DisableNetworkLocationWizard

**Value**

```text
true | false
```

**Description**

With this setting you can activate or deactivate the network location wizard.

## Policies.RequireSecurityFeatures.BitlockerEnabled

**Value**

```text
true | false
```

**Description**

With this setting you can enable or disable Bitlocker.

## Policies.SetCurrentUserAdministrator

**Value**

```text
true | false
```

**Description**

This policy sets the current user as administrator.

## Policies.SetTimeserver

**Value**

```text
"pool.ntp.org"
```

**Description**

With this setting the current time is available via NTP. For more information about it, read the [pool.ntp.org documentation](https://www.pool.ntp.org/en/).

## Restrict.LAPS

**Value**

```text
{
"Admin": [
    "5c9e9c23-7b14-4d97-90d0-4841f2d4b520",
    "4508f67c-d85e-4c15-82f1-ec5e4adb7c6c"
    ],
"Deny":[
    "a5baa9d5-5545-41d7-aea8-19058b29b182"
    ]
}
```

{% hint style="warning" %}
Attach Restrict. \*keys to target user group
{% endhint %}

## WebLinks

**Value**

```text
[
  {
    "Name": "My Azure Account",
    "Target": "https://account.activedirectory.windowsazure.com/r/#/profile",
    "Platform": "any"
  },
  {
    "Name": "Outlook Web Access",
    "Target": "https://outlook.office365.com/owa/?realm=contoso.onmicrosoft.com",
    "Platform": "any"
  }
]
```

**Description**

With this setting you can add weblinks to the tray menu of RealmJoin.



### 

