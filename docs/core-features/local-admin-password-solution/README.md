# Local Admin Password Solution
Our Local Administrator Password Solution (LAPS) was built to solve the issue of using identical accounts in your environment for user support or privilege escalation. LAPS creates strong passwords for local accounts which are stored securely in *your own* [Azure Key Vault](keyvault.md). For auditing, you also have to provide an [Application Insights](application-insights.md) instance, though we are transitioning to using Log Analytics workspaces directly.


## Pre-requirements
Before you can start with LAPS you have to meet the following pre-requirements:

* You have to have set up Application Insights
* You have to explicitly enable LAPS account types using group (or user) settings

We'll look at both of them below.


## Application Insights
Application Insights play an important role when using LAPS. The password requests triggered by LAPS are logged by RealmJoin and piped to Application Insights. This way you have complete insight into who is retrieving passwords.

More details can be found in our [Application Insight article](application-insights.md).


## Group settings
LAPS supports the follow global settings.
| Settings Key | Default Value | Description |
| ------------ | ------------- | ----------- |
| LocalAdminManagement.Inactive | `false` | Set to `true` to force this feature off |
| LocalAdminManagement.CheckInterval | `"01:00"` | Interval for internal config checks, does not influence the creation time of support accounts.  ([HH:mm](https://docs.microsoft.com/en-us/dotnet/standard/base-types/standard-timespan-format-strings)) |

The following account types are supported.
| Settings Key | Default Value |
| ------------ | ------------- |
| LocalAdminManagement.EmergencyAccount | `undefined` (*inactive*) |
| LocalAdminManagement.SupportAccount | `undefined` (*inactive*) |
| LocalAdminManagement.PrivilegedAccount | `undefined` (*inactive*) |


Each account type may be configured independently using the following common settings. Some types have special settings described in their respective section.

{% hint style="info" %}
In the following table `$` represents any of the three `Account` JSON object from above.
{% endhint %}

| Settings Key | Default Value | Description |
| ------------ | ------------- | ----------- |
| $.NamePattern | `"ADM-{HEX:8}"` | Account name. Dynamic tokens supported, see [Conflict avoidance](#conflict-avoidance). |
| $.DisplayName | `"RealmJoin Local Administrator"` | Display name |
| $.PasswordCharSet | `"!#%+23456789:=?@ABCDEFGHJKLMNPRSTUVWXYZabcdefghijkmnopqrstuvwxyz"` | Charset for the password generator (excludes lookalikes) |
| $.PasswordLength | `20` | Password length |
| $.PasswordPreset | `0` | Preset password templates, see [Password generation](#password-generation). |
| $.MaxStaleness | Special. See [Account recreation](#account-recreation). | Time after an account will be refreshed after use ([d.HH:mm](https://docs.microsoft.com/en-us/dotnet/standard/base-types/standard-timespan-format-strings)) |
| $.OnDemand | Special. See [Support account](#support-account). | Enable on-demand mode for SupportAccount |
| $.Expiration | Special. See [Privileged account](#privileged-account). | Fixed account expiration date (ISO-8601 format) |
| $.PasswordRenewals | Special. See [Privileged account](#privileged-account). | List (JSON array) of parameters |


## Password generation
By default truly random passwords will be generated based on the settings `PasswordCharSet` and `PasswordLength`. The default charset was chosen to exclude similar looking characters like `I1l` and `O0`. Windows' cryptographic random number generator is used to provide high quality randomness for generation.

{% hint style="info" %}
RealmJoin will automatically handle issues with Windows' complexity requirements on account creation. As with all truly random passwords sometimes generated passwords might not satisfy the complexity requirements. If this happens RealmJoin will do up to three rounds of passwords generation until a viable passwords is generated. There is a remaining statistically small probability that all retries will be exceeded. In this case you will see a message in the service log file similar to `All retries exceeded`. The complete process will restart in the next run of the internal config checks (see setting `CheckInterval`).
{% endhint %}

Truly random passwords can be painful to work with, which is why special preset templates are also supported.
* Preset 1 ⇒ `[1 upper][3 lower][4 digit]`
  * `Tuci9324`
  * `Lnso5050`
  * `Khwn2174`
* Preset 2 ⇒ `Key-[6 digit]-[6 digit]-[6 digit]-[6 digit]-[6 digit]-[6 digit]-[6 digit]-[6 digit]`
  * PasswordLength setting is supported! The setting determines the number of digit blocks.
  * `Key-012993-230956-976475` (PasswordLength = 3)
  * `Key-497254-679158-631224-278319` (PasswordLength = 4)
  * `Key-506179-861369-706482-613244-730371-097689-404350-340073` (default)
* Preset 3 ⇒ `[word]-[word]-[word]-[word]-[word]-[word]` generated from [Eff Long List](https://www.eff.org/files/2016/07/18/eff_large_wordlist.txt)
  * PasswordLength setting is supported! The setting determines the number of words.
  * `Exciting-Unearth-Cried-87` (PasswordLength = 3)
  * `Neurology-Astute-Debate-Marshy-15` (PasswordLength = 4)
  * `Marshy-Darkened-Undertake-Reset-Shrouded-Wise-26` (default)


## Account recreation
After an account was used, that is after sign out of the local user, RealmJoin can be configured to delete and recreate the account using the `MaxStaleness` setting. This way accounts will always be pristine. If not configured accounts will never be recreated and will stay around indefinitely.

{% hint style="danger" %}
RealmJoin will delete the account and its profile. ALL FILES WILL BE PERMANENTLY DELETED.
{% endhint %}


## Conflict avoidance
Even though RealmJoin tries its best to avoid naming conflicts when managing the accounts on a device, there is always the possibility that accounts might already exist on a device causing conflicts. This is why the `NamePattern` setting supports these tokens with special meaning to RealmJoin. The tokens will be transformed by the specified function and its length parameter following the colon.
* `{HEX:8}` ⇒ `F4D027EF`, `B3C4F74E`, ... (random hexadecimal characters)
* `{DEC:6}` ⇒ `506453`, `066946`, ... (random decimal characters)
* `{COUNT:2}` ⇒ `01`, `02`, ... (counter, will stay `01` if no conflicts exist)


## Emergency account
This account type is supposed to be your backup access to the device should it fail catastrophically. It will be created proactively. This way you will always have access for recovery. We recommend configuring it for [account recreation](#account-recreation).

_Example_  
Key `LocalAdminManagement.EmergencyAccount` (for common settings see [group settings](#group-settings))
```json
{
  "NamePattern": "ADM-Emergency-{HEX:4}",
  "DisplayName": "Emergency Access",
  "MaxStaleness": "04:00",
  "PasswordPreset": 2
}
```


## Support account
This account type can be configured for on-demand creation. It is designed for use in a limited time window of 12 hours in on-demand mode. After triggered via the RJ portal, the account will be created with the next sync to the backend. 

{% hint style="danger" %}
Support accounts and their profiles will be deleted 12 hours after requesting the account regardless of usage (after the support user has signed out). ALL FILES WILL BE PERMANENTLY DELETED.
{% endhint %}

{% hint style="danger" %}
When using on-demand mode account recreation (`MaxStaleness`) *should not be used*. It might interfere with your support workflow.
{% endhint %}

Requirements for the on-demand workflow:

1. The mode is enabled by setting `"OnDemand": true`.
1. A user is signed in
1. The RealmJoin agent is running
1. The device is connected to the internet
1. The device can reach the RealmJoin backend

{% hint style="tip" %}
It might take up to 30 minutes for the RealmJoin agent to notice the request. The signed-in user may speed up this progress by choosing "Sync this device" from the RealmJoin tray menu.
{% endhint %}

When not in on-demand mode it will be created proactively.

_Example_  
Key `LocalAdminManagement.SupportAccount` (for common settings see [group settings](#group-settings))
```json
{
  "NamePattern": "ADM-Support-User-{HEX:2}",
  "DisplayName": "Support User",
  "OnDemand": true,
  "PasswordPreset": 1
}
```


## Privileged account
This account type is designed to be used by power users that need regular but controlled admin privileges on their own devices. A fixed account expiration date can be specified (`Expiration`).

{% hint style="danger" %}
For this type account recreation (`MaxStaleness`) *should not be used*. The whole point is to have a persistent account for your users.
{% endhint %}

Forced password rotations are supported:
1. `2021-11-20T12:34:56+01:00`: any explicit timestamp in ISO8601. Multiple timestamps can be specified.
1. `DayAfterCreate`: after the account has been created the account's password will be changed. This is useful when users are supposed to set up Windows Hello for additional sign-in options.
1. `Monthly` or `Weekly`: Weekly takes preference over Monthly. If no more conditions are specified, defaults are "1st day of month" for Monthly or "Monday" for Weekly. All seven weekday can be specified. So if `Wednesday` and `Weekly` are specified, the password will be changed every Wednesday. If `Wednesday` and `Monthly` are specified, the password will be changed on the first Wednesday each month.

_Example_  
Key `LocalAdminManagement.PrivilegedAccount` (for common settings see [group settings](#group-settings))
```json
{
  "NamePattern": "Privileged-User-{COUNT:1}",
  "DisplayName": "Privileged User",
  "PasswordRenewals": ["DayAfterCreate", "Monthly", "Thursday"],
  "PasswordPreset": 3,
  "PasswordLength": 3
}
```


## Accessing passwords
Use the RealmJoin Portal to access the passwords. It will appears similar to this.
<img src="../../media/rj-laps-table-complete.png" />


## Enable self-service
Users may access accounts created on their _own_ devices (they are "PrimaryUser") when enabled using the _RealmJoin Portal_ starting with version `2022.5.1`. To enable, define a setting using the key `Allow.SelfLAPS`. This setting may be defined on groups and users. As with all settings prefixed with `Allow.*` they are AND-joined across the user and all of their groups.

```json
{
  "EmergencyAccount": true,
  "SupportAccount": true,
  "PrivilegedAccount": true
}
```

The value can also be pure boolean `true`/`false`. This may be used as a wildcard and encompasses every current and future account type. Please note that this is only recommended for disabling access (`false`).

{% hint style="info" %}
In the past it was recommended to set this setting to `true`. However, as we continue to expand RealmJoin, new account types will be added. It is therefore strongly recommended to migrate all `true` values to the more explicit object notation.
{% endhint %}

A sample configuration may look like this:
| Group | Value | Comment |
| ----- | ----- | ------- |
| All remote workers | `{ "EmergencyAccount": true }` | Remote workers may access their own devices emergency account. |
| All developers | `{ "EmergencyAccount": true, "PrivilegedAccount": true }` | Developers may access their emergency account and their privileged account—no matter whether they are remote workers or not. |
| All trainees | `false` | Trainees must never have access to any of the three account types **and** all future types, even if they are remote workers or developers. |
