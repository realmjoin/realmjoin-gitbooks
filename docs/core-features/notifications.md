# Notifications

With the help of the notification feature it is possible to notify users and clients very quickly. Whether it is general information or important issues.

### Overview

![](../.gitbook/assets/rj-notification-list.png)

The notification menu shows all notifications that have been created. What the individual values and parameters in this overview mean is described in this article.

### Group Setting

In order to use this feature Glück & Kanja has to enable this feature in Group Settings.

### Create a new Notification

To create a new notification click **+ Add Notification** in the upper right corner of the notification menu.

![](../.gitbook/assets/rj-notification-add-notification.png)

The following window appears:

![](../.gitbook/assets/rj-notification-add-notification2.png)

#### Category

![](../.gitbook/assets/rj-notification-category.png)

The first parameter you can choose is **Category**. Here you have the choice between **Default, Info** and **Alert**. Depending on what you choose, the color of the notification will change.

#### Start and End

![](../.gitbook/assets/rj-notification-start-end.png)



Next, you need to specify when the notification should be published and when it should no longer be displayed. There are three values available for this configuration:

* Date
* Time **UTC**
* Time offset

#### Target and Ignore

Then you can select which groups should receive your notification \(Target\) and which groups should not receive it \(Ignore\).

To choose a target, click **Select groups** under **Target**. A search box appears where you can search for groups.

![](../.gitbook/assets/rj-notification-target.png)

To choose groups to be excluded from notifications, click **Select groups** under **Ignore**. A search box appears where you can search for groups.

![](../.gitbook/assets/rj-notification-ignore.png)

In the following example, one group was selected as **Target** and one as **Ignore**:

![](../.gitbook/assets/rj-notification-target-ignore.png)

#### Content

**Content** is the main part of your notification. In the field **Title** you enter the title of the notification. In the field **Body** you enter the text of your notification.  
  
Here is an example of a notification:

![](../.gitbook/assets/rj-notification-content.png)

If you want to add translations to your notification, click **Add Translation**. A further content block with **Language**, **Title** and **Body** will appear.

In the field **Language** you enter an IETF language tag. For example **de-DE**.

In the field **Title** enter the German title of your notification and in the field **Body** a German translation of your English notification text.

### Notification in Use

Once you have created your notification, the target groups will receive a notification at the scheduled time. This notification appears on the desktop of a client.

![](../.gitbook/assets/rj-notification-prompt.png)

