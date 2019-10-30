# AnyDesk

The RealmJoin Enterprise License contains an single session licens of the remote desktop tool **AnyDesk**. It allows the access to client devices including the option to elevate rights by using the RealmJoin LAPS feature. AnyDesk can be installed on Windows and macOS.

AnyDesk uses ID numbers to establish connections between two computers. Share your ID number with an other user \(this user needs AnyDesk as well\). This user has to enter the ID number in the AnyDesk menu. When you accept the request, the other user will have access to your desktop.

RealmJoin skips the whole ID number sharing process, because every AnyDesk ID numbers in an organization are linked to single users. An Administrator just needs to know the user and can request for access to the computer. Still the user has to accept this request.

{% hint style="info" %}
When you use the AnyDesk feature \(via RealmJoin\), it is not possible to start a remote session with external AnyDesk users.
{% endhint %}

## AnyDesk deployment

Before you can start with a AnyDesk session, you have to do few settings.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Task</th>
      <th style="text-align:left">Image</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">1. Log in to <a href="https://my.anydesk.com/login">AnyDesk</a>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">2. Customize your AnyDesk client</td>
      <td style="text-align:left"><a href="https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/anydesk7.png"><img src="../.gitbook/assets/anydesk7.png" alt="Customize AnyDesk client"/></a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">3. Select <b>Make download link publicly available</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">3. Click <b>Save</b> to confirm your settings</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">4. The <b>Custom Client Details</b> page will appear</td>
      <td style="text-align:left"><a href="https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/anydesk8.png"><img src="../.gitbook/assets/anydesk8 (1).png" alt="Custom Client Details"/></a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">5. Select the following <b>Options</b>:</td>
      <td style="text-align:left">
        <p></p>
        <p>
          <img src="../.gitbook/assets/anydesk8_2 (1).png" alt/>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <ul>
          <li>Disable settings</li>
          <li>Disable address book</li>
          <li>Disable TCP listen port</li>
          <li>Automatically register alias</li>
          <li>Assign to license</li>
          <li>Access control list</li>
        </ul>
      </td>
      <td style="text-align:left">
        <p></p>
        <p></p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">6. Copy or save the <b>Public Download</b> URL. You need it for <b>AnyDesk Group Settings</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>## AnyDesk Group Settings

Use a JSON policy to configure AnyDesk in RealmJoin backend \(**Group Settings**\). There are three different policies to configure AnyDesk.

The following JSON contains all configurations:

**Key** = Integration  
**Value** = {"AnyDesk: { "Enabled": true, "BootstrapperUrl": "[https://.../.../AnyDesk.exe](https://.../.../AnyDesk.exe)", "Ui": {TrayMenuTextEnglish": "Start remote session} } }

{% hint style="info" %}
The BootstrapperUrl is your **Public Download Url** from AnyDesk Custom Client Details.
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

## Backend Integration

After you customize your Client, AnyDesk will send you an email. This mail contains your **Contract ID**, your **License ID** and your **API Password**. Send these IDs and the password to the [Glück & Kanja support](mailto:support@glueckkanja.com). If you do so, Glück & Kanja will integrate a AnyDesk API in your RealmJoin Portal.

[![Backend Integration](../.gitbook/assets/anydesk9.png)](https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/anydesk9.png)

## Start a remote session via RealmJoin tray menu

| Task | Image |
| :--- | :--- |
| 1. Open the RealmJoin tray menu |  |
| 2. Click **Start remote session** | [![RJtraymenu](../.gitbook/assets/anydesk1%20%281%29.png)](https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/anydesk1.png) |
| 3. The AnyDesk client starts and its current address will be pushed to RealmJoin backend in background. In addition, its visible in the UI. | [![RJanydesksession](../.gitbook/assets/anydesk2.png)](https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/anydesk2.png) |
| 4. This client address will be displayed in RealmJoin portal at the corresponding client and the support staff can initiate the session via clicking **Connect** | [![AnyDeskConnect](../.gitbook/assets/anydesk3.png)](https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/anydesk3.png) |
| 5. This will automatically start the AnyDesk client |  |
| 6. Subsequently, the end user needs to accept the incoming remote session request | [![RJremoterequest](../.gitbook/assets/anydesk4.png)](https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/anydesk4.png) |
| 7. The Connection is established and the support staff can perform his tasks remotely |  |
| 8. When the job is finished, please **disconnect** from the remote session |  |

### Get elevated rights

For special support scenarios administrative rights will be needed. A normal remote session starts with standard rights. That requires to elevate the permissions:

| Task | Image |
| :--- | :--- |
| 1. Click the **lightning icon** |  |
| 2. Select **Request elevation** | [![Request elevation](../.gitbook/assets/anydesk5.png)](https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/anydesk5.png) |
| 3. In the new appearing window \(Request elevation\) choose **Transmit authentication data** |  |
| 4. Insert corresponding credentials |  |
| 5. Then, click **OK** | [![Credentials](../.gitbook/assets/anydesk6%20%281%29.png)](https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/anydesk6.png) |
| 5. On the remote client, a new window **User Account Control** will appear |  |
| 6. Confirm it |  |
| 7. The support staff is now able to perform administrative tasks. |  |

