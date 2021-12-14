# Install Using Microsoft Intune

RealmJoin has to deploy through Microsoft Intune by deploying the MSI as a Line-of-Business app. The following article is a step-by-step guide to deploy RealmJoin.

### Azure Intune Portal

Use the following instructions to deploy RealmJoin:

1. Log in to your [Azure portal](https://portal.azure.com)
2. Navigate to **Microsoft Intune** and select **Client apps**

![](<../.gitbook/assets/install-rj-azure-portal1 (1).png>)

1. Then select **Apps** and click **+Add**

![](<../.gitbook/assets/install-rj-azure-portal2 (1).png>)

1. Under **Other** choose **Line-of-business-app** and click **Select**

![](<../.gitbook/assets/install-rj-azure-portal3 (1).png>)

1. Next click **Select app package file**
2. As **App package file** browse for **RealmJoin.msi** on your device

![](<../.gitbook/assets/install-rj-azure-portal4 (1).png>)

1. Then, click **OK**
2. Under **App information** fill in all required fields and set **Ignore app version** to **Yes**

![](<../.gitbook/assets/install-rj-azure-portal5 (1).png>)

1. Under **Assignments** add groups and users for your RealmJoin app

![](<../.gitbook/assets/install-rj-azure-portal6 (1).png>)

1. Under **Review + create** check all your settings

![](<../.gitbook/assets/install-rj-azure-portal7 (1).png>)

1. Finally click **Create**

{% hint style="warning" %}
Like any other application in Intune, ReamJoin can be assigned to the desired user groups as (required) software. It is not necessary to install additional software on the client devices to run RealmJoin. RealmJoin will be deployed on the client devices on the next Azure sync.
{% endhint %}

### Windows Defender Exceptions

RealmJoin has worked with the Microsoft Defender Team to be whitelisted from malware detection. Since Defender is using more and more machine learning mechanisms to identify potential threats and RealmJoin has several features like cloud downloaded application installations, RealmJoin might be recognized by **Windows Defender** as a possible threat.

While this behavior is not certain, it is recommended to implement additional Windows Defender exceptions. Create a new device configuration profile, type **Device restriction**, or edit your existing profile and add the following **Windows Defender Antivirus Exceptions**:

| Defender Exceptions                             |
| ----------------------------------------------- |
| **Files and Folders**                           |
| `%ProgramFiles%\RealmJoin`                      |
| `%ProgramFiles%\RealmJoin\RealmJoin.exe`        |
| `%ProgramFiles%\RealmJoin\RealmJoinService.exe` |
| `%ProgramFiles%\RealmJoin\RealmJoinUpdate.exe`  |
| **Processes**                                   |
| `%ProgramFiles%\RealmJoin`                      |
| `%ProgramFiles%\RealmJoin\RealmJoin.exe`        |
| `%ProgramFiles%\RealmJoin\RealmJoinService.exe` |
| `%ProgramFiles%\RealmJoin\RealmJoinUpdate.exe`  |

{% hint style="info" %}
It\`s important to configure the same path in **Files and Folders** and **Processes**. In some cases, Microsoft only checks one of this Defender Exceptions.
{% endhint %}
