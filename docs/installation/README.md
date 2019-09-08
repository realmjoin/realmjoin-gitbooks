# Installation

RealmJoin can be deployed on a device using one of multiple ways, depending on the individual scenario. As a first step, download the RealmJoin installer of your choice and precede to the desired installation method.

Stable release:  
[RealmJoin Release Version](https://gkrealmjoin.s3.amazonaws.com/win-release/RealmJoin.msi)

Beta Channel \(near to stable, for long time testing\):  
[RealmJoin Beta Version](https://gkrealmjoin.s3.amazonaws.com/win-beta/RealmJoin.msi)

Canary Channel \(Experimental, first testing\):  
[RealmJoin Canary Version](https://gkrealmjoin.s3.amazonaws.com/win-canary/RealmJoin.msi)

## Front-End \(Client\)

The front-end component of RealmJoin is a RealmJoin client, which is installed on the Windows 10 device. With the installed RealmJoin client an individual user is able to access and install provided software in self service. Packages assigned as **required** by the administrator are installed automatically on the first Logon after assignment. RealmJoin is responsible for two different processes running on the device:

* The **realmjoin.exe** process is started up automatically on Logon. The process is always running and sends upstream data \(compare to chapter [RealmJoin Portal](../rj-portal.md#States) every 15 minutes.
* The **realmjoinservice.exe** is called when a package requires the **SYSTEM mode** to be processed. It is not running by default.

## Pre-Requirements

The following pre-requirements are necessary for RealmJoin:

* Microsoft Azure with Azure AD
* Windows 10
* Microsoft Intune

RealmJoin runs on every Windows 10 device. A Windows 10 certified device with TPM chip is recommended to ensure BitLocker initialization.

