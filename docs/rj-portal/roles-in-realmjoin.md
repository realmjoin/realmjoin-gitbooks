# Roles in RealmJoin

During the initial installation of a tenant, RealmJoin automatically searches for roles and stores their IDs. All groups containing the following strings are automatically searched for:

* RealmJoin Admin
* RealmJoin Auditor
* RealmJoin Supporter
* RealmJoin Software Agent
* RealmJoin Notification Agent

{% hint style="warning" %}
To be considered during sychronization, these groups must start with the prefix \*\*CFG - :

For Example:\*\*  
CFG - RealmJoin Admin
{% endhint %}

## Administrator

A RealmJoin administrator has full rights within the RealmJoin portal.

## Auditor

An auditor has read-only rights within the RealmJoin portal and has access to all settings and assignments.

## Software Agent

A software agent can assign software to users and can change it as well and the software agent can subscribe to apps in RealmJoin App Store. Additionally, a software agent has access to users, clients, groups, software, and app store. With this role, it is not possible to use AnyDesk and LAPS and it is not possible to reassign primary users.

## Supporter

A supporter can not manage RealmJoin software. A supporter has access to users, clients, and groups \(reassign primary users as well\). Furthermore, a supporter has the possibility to use AnyDesk and LAPS.

## Notification Agent

A notification agent may create, manage and assign RealmJoin notifications to all user groups.

