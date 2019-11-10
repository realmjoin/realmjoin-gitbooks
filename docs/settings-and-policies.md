# Settings & Policies

## Settings

Comments on the individual settings in _italics_.

* Key: "Environment"

```text
   "UpdateCheckInterval": "01:00"
   "ConfigCheckInterval": "00:30"
```

_Set as "hh:mm"_

* Key: "FirstRun"

```text
"EnableSecureDesktop": true
```

_Enable the Windows secure desktop_ feature

* Key: "Realm"  


  ```text
   "Domain": "glueckkanja.net"
   "NetBIOS": "GLUECKKANJA"
  ```

* Key: "DomainConnect"  


  ```text
   "Domain": "glueckkanja.net",
   "NetBIOS": "GLUECKKANJA",
   "CheckInterval": "01:00"  
  ```

* Key: "CredentialManager":  


  ```text
  "Type": "wlan",  
      * "Target": "GKEnterprise" 
  "Type": "ntlm",
      * "Target": "identity.glueckkanja.net",
  "Type": "smb",  
      * "Target": "files.glueckkanja.net",
      * "Share": "Filestore"  
  ```

_Allows to configure WAN/LAN connections and manage authentication_

* Key: "IpSec":

```text
    "Rules":
       * "Name": "Domain Controller - glueckkanja.net",
       * "Targets": "glueckkanja.net",
       * "Protocol": "tcp",
       * "Range": "135,389,445,30000-30400",
       * "RangeOSX": "135,389,445",
       * "Key": "xxxxxxxxxxxxxxxxxxxxx"  
```

* Key: "Branchbox":

```text
    "RescanInterval": "00:15",  
    "Rules": 
       * "Name": "Branchbox",
       * "Target": "files.glueckkanja.net",
       * "IPs": "172.27.0.20",
       * "CheckPort": 63069,
       * "CN": "*.glueckkanja.net"  
```

* Key: "CloudVPN":

```text
   "Gateway": "cloudvpn.gkdatacenter.net",
   "Username": "",
   "Password": ""  
```

* Key: "WebLinks":

```text
    "Name": "GK Help",
    "Target": "https://help.glueckkanja.net/",
    "Platform": "any"  
```

{% hint style="info" %}
It is possible to direct the link to a specific application or process to be started with. To do so, the target has to be set to the process and optional args can be provided. Additionally, for edge, the protocol handler can be used.
{% endhint %}

* Key: "WebLinks" \(directing to process\):

```text
   {
"Name": "Citrix-Applikationen",
"Target": "iexplore",
"Args": "https://url.net",
"Platform": "any"
},
{
"Name": "Citrix-Applikationen",
"Target": "microsoft-edge:https://url.net",
"Platform": "any"
}
```

* Key: "BranchCache":

```text
 "Mode": "Distributed"  
```

* Key: "Chocolatey":

```text
   { "Version": "0.10.3",  
    "Sources":
    "Name": "gkpackages",
    "Source": "https://packages.gkdatacenter.net/nuget",
    "User": "packages",
    "Password": "xxxxxxxxxxxxxxxxxxxxx",
    "Priority": 10
   }
```

* Key: "SoftwarePackages":

```text
    "Package": "bcurl",
    "ID": "bcurl",
    "Platform": "winchoco",
    "Version": "1.0.11",
    "Args": "",
    "Name": "BcUrl",
    "Order": 500,
    "PreRelease": false,
    "AllowReinstall": false,
    "DependsOn": [],
    "AutoUpgrade": true,
    "AutoUpgradeStaggered": "",
    "GroupName": "Development",
    "Hidden": false,
    "Mandatory": false  
```

* Key:

```text
"Location": "https://packages.gkdatacenter.net/blobs/v1.0.0.0.zip",
  * "Hash": "46298d7dfe399cc46bd62ee359ab983771f5bcf1",
  * "Scope": "user",
  * "ID": "glueckkanja-core-settings-wlan-gkenterprise",
  * "Platform": "win",
  * "Version": "1.0.0.0",
  * "Args": "",
  * "Name": "GK WLAN (GKEnterprise)",
  * "Order": 999999,
  * "PreRelease": false,
  * "AllowReinstall": false,
  * "DependsOn": [],
  * "AutoUpgrade": true,
  * "AutoUpgradeStaggered": "",
  * "GroupName": "Glueckkanja",
  * "Hidden": false,
  * "Mandatory": false  
```

## Policies

Comments on the individual settings in _italics_

* Key: "Policies":

```text
  * "SMimeEnabled": false,
  * "OsActivationEnabled": false,
  * "SetTimeserver": ["time.windows.com", "time.apple.com"],
  * "TrustedSites": ["file://glueckkanja.net", "https://glueckkanja.net"],
```

* Key: "RequireSecurityFeatures"

```text
    * "WinVersion": "Win7",
    * "BitlockerEnabled": null,  
         
          Entry: *PreventDeviceEncryption*;
          Value: *null* / *false*
         * The BitLocker key is synced to AAD if the client is AAD-joined, otherwise no backup will be made.
    * "FirewallEnabled": true,
    * "AvEnabled": null,
    * "EnvironmentCheck": null  
```

If set to **true**, BitLocker will be enforced if the device has a TPM.  
  
The following key-value is changed to allow BitLocker force:  
 `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\BitLocker`

* Key: "SetCurrentUserAdministrator": null  


  _Recommended setting: Set to **false** for all users. This removes the administrator privileges for all users. Set to **true** for all users that should have local admin privileges. The privileges are only granted to users on clients where they are the primary user/device owner._  

* Key: "SetNetworkOptimizationID": null  _Opt-out from using a DOGroupID from Realmjoin_ 
* Key: "AwsAccess":

```text
 "AccessKey": "AKIAIHFASK3VCX4EWCAA",
 "SecretKey": "xxxxxxxxxxxxxxxxxxxxx"
```

* Key: "DisableExplorerLibraries": true 
* Key: "Rms":

```text
     "Enabled": null,
     "Hostname": "12323815-123c-123a-1230-123aab12ba3a.rms.eu.aadrm.com"
```

* Key: "OneDrive":

```text
     "Enabled": false,
     "DisplayName": "OneDrive Business",
     "FolderRedirection": false,
     "DisableOneDrivePersonal": false,
     "DisableStartupShortcut": false
```

* Key: "Office":

```text
     "NoDomainKey": false,
     "SetGenericCredentials": false,
     "SetLyncUsername": false
```

## Clients

* Key: "Client":

```text
    "IsPrimaryOfUser": true
```

### Autogenerated by the Server

The **IsPrimaryOfUser** attribute is set when the RealmJoin client on the device contacts the back-end for the first time. The user who is signed on during this process is registered as a primary user of the device.  
  
Mandatory packages will only be installed when the primary user is logged in. If the **makeAdmin** property is set in the user/group settings, the primary user is promoted to the administrator. It is possible to manually set another user to the primary of the device. If a device is decommissioned and given another user without changing the primary, the old primary user might persist in the back-end.

## Signatures

RealmJoin provides Outlook with signature files. Those files can be found in:

* %userprofile%\AppData\Roaming\Microsoft\Signatures
  * .\anyname.txt
  * .\anyname.htm

The following fields for signatures are extracted from the Microsoft Graph API and may be used:

```text
Graph_User_BusinessPhone  
Graph_User_City  
Graph_User_CompanyName  
Graph_User_Country  
Graph_User_Department  
Graph_User_DisplayName  
Graph_User_GivenName  
Graph_User_Id  
Graph_User_JobTitle  
Graph_User_Mail  
Graph_User_MobilePhone  
Graph_User_OfficeLocation  
Graph_User_PostalCode  
Graph_User_State  
Graph_User_StreetAddress  
Graph_User_Surname  
```

