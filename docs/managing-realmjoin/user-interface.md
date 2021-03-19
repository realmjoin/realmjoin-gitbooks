# User Interface

![](../.gitbook/assets/rj-ui1%20%282%29%20%281%29.png)

RealmJoin uses the **user identity** and checks with it at a Cloud-Service for an **Extended Policy** and optionally for a **Secondary Identity**, then the RealmJoin Security Assessment **checks if the system is qualified** \(Encryption, Patch Level, Firewall, Anti-Virus, etc. - optionally, an Intune-Health-Check may be sufficient\). If the user's device is eligible **software- and configuration-Policy** will be applied \(Mandatory Applications, etc.\).

The following screen shows the RealmJoin toast notification. It appears in the Windows notification center:

![](../.gitbook/assets/rj-ui2.png)

This screen shows a customizable **hero image** \(for more information about hero images, click [here](https://docs.microsoft.com/en-us/windows/uwp/design/shell/tiles-and-notifications/adaptive-interactive-toasts#hero-image)\)

Below this hero image you can see information on packages and a comment when the update will start.

You also see a progress bar and an **Auto Install...** countdown. You can snooze the installation or start it immediately. How often a user can snooze the installation depends on a configured deadline. If this deadline has expired, RealmJoin will install the required updates automatically.

This deadline is configured in the package. So this deadline can be different from package to package.

