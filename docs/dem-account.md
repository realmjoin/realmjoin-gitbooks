# Multi-User Devices

Multi-User Devices allow an administrator to provision devices intended to be used by more than one user. A tool for Multi-User Devices is **Device Enrollment Manager** (short DEM).

DEM is an Intune permission that can be applied to an Azure Active Directory user account and lets the user enroll up to 1,000 devices. A DEM account is useful for scenarios where devices are enrolled and prepared before handing them out to the users of the devices.

## Licenses

Devices enrolled by DEM accounts need to be licensed. Therefore, each DEM account needs an Intune user or device license assigned.

Example:

* Enterprise Mobility + Security (user license) or
* A simple device license

![](<.gitbook/assets/dem1 (1) (1) (2).png>)

## Preparations

Before you can start with a device enrollment you have to do some preparations.

### Create DEM User

Create a generic user account that is not assigned to a real person. Please make sure that this account never gets deleted. In that case, enrolled devices will not stay under management anymore. Assign a suitable Intune license as described before.

![](<.gitbook/assets/dem2 (1) (1) (2).png>)

### Create User Group for DEM Accounts

A new user group is necessary that contains all DEM users. Ad one (e.g. **CFG - All multi-user device accounts DEM**) and assign the previously created user.

![](<.gitbook/assets/dem3 (1) (1) (1) (2).png>)

### Prepare Group

In **Intune** the following actions are necessary for that group:

* Assign compliance policies and device configurations (that should apply for these devices)
* Assign Intune distributed apps (e. g. RealmJoin Installer)
* Check if DEM group can enroll and register new devices in Tune/Azure AD (e. g. enrollment restrictions and Azure AD Join)

The following steps must be done in **RealmJoin**

* Add RealmJoin configuration policies to that group
* Add Software packages (that should be installed when the device is set up by DEM account)
* Let Glück & Kanja mark this group as **Primary Users** (obtain Azure AD Object ID)

## Device Setup

A new and clean device will be set up with the DEM user account created before:

![](<.gitbook/assets/dem5 (1) (1) (2).png>)

Depending on configuration second factor authentication will be enforced:

![](<.gitbook/assets/dem6 (1) (1) (2).png>)

Device enrollment and provisioning will start:

![](<.gitbook/assets/dem7 (1) (1) (1) (1) (1) (1) (2).png>)

Prompt for Windows Hello setup appears (depending on configuration):

![](<.gitbook/assets/dem8 (1) (1) (1) (2).png>)

After that, RealmJoin will start and install the defined set of software for the DEM account:

![](<.gitbook/assets/dem9 (1) (1) (2).png>)

When logging in via DEM account (primary user) the software should be installed:

![](<.gitbook/assets/dem10 (1) (1) (2).png>)

## Secondary User Experience

Secondary users are now able to log in::

![](<.gitbook/assets/dem11 (1) (1) (2).png>)

Software assigned and installed by DEM account should be available

Additional software can be installed by this secondary user (see **Software Packages**):

![](<.gitbook/assets/dem13 (1) (1) (2).png>)

![](<.gitbook/assets/dem14 (1) (1) (2).png>)

![](<.gitbook/assets/dem15 (1) (1) (2).png>)
