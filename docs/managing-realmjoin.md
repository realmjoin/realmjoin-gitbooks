# RealmJoin Windows Client

The RealmJoin Windows client is enrolled on every Windows 10 device. RealmJoin seamlessly fits into the modern workplace with its focus on user self-service and mobility. Using the RealmJoin client module, the user may install provided software, get basic information on the device and membership in the tenant domain without the need of contact an IT administrative.

## Initial Start since RealmJoin v4.15

Since the release of version 4.15, RealmJoin skips the email-based discovery process that user goes through on the sign in page, leading to a slightly more streamlined user experience \(RealmJoin still based on the AAD workflow - AAD sign-in and OAuth-protocol\).

{% hint style="info" %}
In rare cases it can happen that the user has to enter username and password manually, as a result of failures or incompatible settings.
{% endhint %}

To see information about the Initial Start before version 4.15, navigate to the [Appendix](appendix.md#Initial-Start-before-RJ-v4.15)

## RealmJoin User Interface and Client menu

### User Interface

![](.gitbook/assets/rj-ui1.png)

RealmJoin uses the **user identity** and checks with it at a Cloud-Service for an **Extended Policy** and optionally for a **Secondary Identity**, then the RealmJoin Security Assessment **checks if the system is qualifies** \(Encryption, Patch Level, Firewall, Anti-Virus, etc. - optionally, an Intune-Health-Check may be sufficient\). If the user's device is eligible **software- and configuration-Policy** will be applied \(Mandatory Applications, etc.\).

The following screen shows the RealmJoin toast notification. It appears in the Windows notification center:

![](.gitbook/assets/rj-ui2.png)

This screen shows a customizable **hero image** \(for more information about hero images, click [here](https://docs.microsoft.com/en-us/windows/uwp/design/shell/tiles-and-notifications/adaptive-interactive-toasts#hero-image)\)

Below this hero image you can see information on packages and a comment when the update will start.

You also see a progress bar and an **Auto Install...** countdown. You can snooze the installation or start it immediately. How often a user can snooze the installation depends on a configured deadline. If this deadline has expired, RealmJoin will install the required updates automatically.

This deadline is configured in the package. So this deadline can be different from package to package.

### Client menu

After being successfully installed, RealmJoin is automatically started on the user login and is permanent active in the background. It is represented with an ID card icon. Clicking on the icon opens up the RealmJoin client menu. It contains basic information in the lower part and a number of links in the upper part. These links are ordered in two different sections - **Web Links** and **Software Packages**.

![](.gitbook/assets/rj-ui3.png)

**Web Links** contains customizable web links. For example, Google. When a user click the web link **Google**, RealmJoin opens the Google Search  automatically.

Software Packages contains customizable software categories. For example, **Browser** contains links to Mozilla Firefox or Google Chrome. With a click on a link, RealmJoin starts automatically an installation or an updating process \(if the software is already installed\).

Furthermore RealmJoin offers a remote function \(**Start remote session**\). For more information read our [AnyDesk article](anydesk.md).

A further useful feature is **Sync this device**.

![](.gitbook/assets/rj-ui3.2.png)

When you click **Sync this device** RealmJoin will install or update mandatory packages. Furthermore **Sync this device** helps to speed up background processes \(e. g. waiting for new weblinks or waiting for an admin account\).

