# Customer Tasks

If you are interested in AnyDesk send a request to [Glück & Kanja \(GK\)](mailto:support@glueckkanja.com). GK sends you two different URLs:

* A user client URL
* A supporter client URL

These URLs are important for the following configurations and settings.

## AnyDesk Group Settings for User Client

Use a [JSON policy](../../packages/json-backgrounder.md) to configure AnyDesk in the RealmJoin [Group Settings](../../rj-portal/groups-and-group-settings.md#group-settings). There are three different policies to configure AnyDesk.

The following JSON contains all configurations:

**Key** = Integration  
**Value** = {"AnyDesk: { "Enabled": true, "BootstrapperUrl": "[https://.../.../AnyDesk.exe](https://.../.../AnyDesk.exe)", "Ui": {TrayMenuTextEnglish": "Start remote session} } }

{% hint style="info" %}
The BootstrapperUrl is your **user client URL**.
{% endhint %}

It is also possible to split this single JSON from above, in three different JSON policies:

**Key** = Integration.AnyDesk.Enabled  
**Value** = true

and

**Key** = Integration.AnyDesk.BootstrapperUrl  
**Value** = "[https://.../.../AnyDesk.exe](https://.../.../AnyDesk.exe)"

and

**Key** = Integration.AnyDesk.UI.TrayMenuTextEnglish  
**Value** = "Start remote session"

The following JSON is possible as well:

**Key** = Integration.AnyDesk  
**Value** = {"Enabled":true, BootstrapperUrl": "[https://.../.../AnyDesk.exe](https://.../.../AnyDesk.exe)", "UI":{"TrayMenuTextEnglish": "Start remote session"} }

## Back-End Integration

After you configure your user client, AnyDesk will send you an email. This email contains your **Contract ID**, your **License ID** and your **API Password**. Send these IDs and the password to the [Glück & Kanja suppor](mailto:support@glueckkanja.com)t. If you do so, GK will integrate a AnyDesk API in your RealmJoin portal.

![](../../.gitbook/assets/anydesk9%20%281%29%20%281%29.png)

### AnyDesk Supporter Client Setup Launcher

To allow a supporter to connect to a desktop, you have to assign the **AnyDesk Supporter Client Setup Launcher** to a supporter.

![](../../.gitbook/assets/anydesk_setuplauncher.png)

For this assignment you need your supporter client URL.

Read our [App Store article](../../rj-portal/app-store.md#app-subscribtion) for details about package subscription and read our [Software Packages article](../../rj-portal/software-packages.md#package-assignment) for details about package assignment.

## Start a Remote Session via RealmJoin Tray Menu

| Task | Image |
| :--- | :--- |
| 1. Open the RealmJoin tray menu |  |
| 2. Click **Start remote session** | [![RJtraymenu](../../.gitbook/assets/anydesk1%20%281%29%20%281%29.png)](https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/anydesk1.png) |
| 3. The AnyDesk client starts and its current address will be pushed to RealmJoin backend in the background. Also,, it's visible in the UI. | [![RJanydesksession](../../.gitbook/assets/anydesk2%20%281%29.png)](https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/anydesk2.png) |
| 4. This client address will be displayed in RealmJoin portal at the corresponding client and the support staff can initiate the session via clicking **Connect** | [![AnyDeskConnect](../../.gitbook/assets/anydesk3.png)](https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/anydesk3.png) |
| 5. This will automatically start the AnyDesk client |  |
| 6. Subsequently, the end user needs to accept the incoming remote session request | [![RJremoterequest](../../.gitbook/assets/anydesk4.png)](https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/anydesk4.png) |
| 7. The Connection is established and the support staff can perform his tasks remotely |  |
| 8. When the job is finished, please **disconnect** from the remote session |  |

#### Get Elevated Rights

For special support scenarios, administrative rights will be needed. A normal remote session starts with standard rights. That requires to elevate the permissions:

| Task | Image |
| :--- | :--- |
| 1. Click the **lightning icon** |  |
| 2. Select **Request elevation** | [![Request elevation](../../.gitbook/assets/anydesk5.png)](https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/anydesk5.png) |
| 3. In the new appearing window \(Request elevation\) choose to **Transmit authentication data** |  |
| 4. Insert corresponding credentials |  |
| 5. Then, click **OK** | [![Credentials](../../.gitbook/assets/anydesk6%20%281%29.png)](https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/anydesk6.png) |
| 5. On the remote client, a new window **User Account Control** will appear |  |
| 6. Confirm it |  |
| 7. The support staff is now able to perform administrative tasks. |  |

## Additional Sessions

When setting up AnyDesk for the first time, you will receive a single license from Glück & Kanja. This single license allows one remote session. Further simultaneous sessions by other supporters are not possible, additional licenses are necessary.

If you need more licenses, [contact Glück & Kanja ](mailto:support@glueckkanja.com)for more details.

