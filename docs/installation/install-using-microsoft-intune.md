# Install Using Microsoft Intune

RealmJoin has to deploy through Microsoft Intune by deploying the MSI as a Line-of-Business app.

### Azure Intune Portal

The deployment of RealmJoin using Intune requires only the .MSI installer to be configured. If the RealmJoin app in the desired release version is not registered in Intune, it can be added as a Line-of-Business app via the Azure Portal blades:

1. Navigate to **Intune**
2. Click **Client Apps**
3. Click **Apps**
4. Then click **Add**

[![RJ Intune Deploy](../.gitbook/assets/rj-intune-deploy.png)](https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/rj-intune-deploy.png)

In the configuration tab basic and advanced information can be provided.

[![RJ Intune Deploy2](../.gitbook/assets/rj-intune-deploy2.png)](https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/rj-intune-deploy2.png)

{% hint style="info" %}
Like any other application in Intune, ReamJoin then can be assigned to the desired user groups as \(required\) software. It is not necessary to install additional software on the client devices to run RealmJoin. RealmJoin will be deployed on the client devices on next Azure sync.
{% endhint %}

### Windows Defender Exceptions

RealmJoin might be recognized by **Windows Defender** as a possible threat. While this behaviour is not certain, it is recommended to implement some Windows Defender exceptions. Create a new device configuration profile, type **Device restriction**, or edit your existing profile and add the following **Windows Defender Antivirus Exceptions**:

* Files and folders  
  * `%ProgramFiles%\RealmJoin`  
* Processes
  * `%ProgramFiles%\RealmJoin\RealmJoin.exe`
  * `%ProgramFiles%\RealmJoin\RealmJoinService.exe`
  * `%ProgramFiles%\RealmJoin\RealmJoinUpdate.exe`

