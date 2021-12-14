# Software Report

**Software Report** contains an overview of all software that is in use. Additionally you can see which user, group or client is using a software.

### Overview

![](<../.gitbook/assets/software-report1 (1).png>)

When you open the menu you will see a complete list of all software in use. This list is sorted alphabetically. The following software attributes are listed:

| Attribut      | Explanation                                                                                                                                                         |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Type**      | <p>There are two in RealmJoin:<br></p><ul><li>Windows Installer</li><li>Windows Store</li></ul>                                                                     |
| **Known as**  | 'Known as' corresponds to a RealmJoin package ID. Even if the package was not purchased via RealmJoin, RealmJoin still tries to map an existing ID to this package. |
| **Publisher** | Publisher of the Software                                                                                                                                           |
| **Version**   | Version of the installed software                                                                                                                                   |
| **Clients**   | Count of using clients                                                                                                                                              |
| **User**      | Count of users                                                                                                                                                      |
| **Licenses**  | Count of existing licenses                                                                                                                                          |

### Details

![](<../.gitbook/assets/software-report2 (1).png>)

In this submenu you see the details of a software.

In the upper left corner you can see the name of the software, if it is available through RealmJoin and the corresponding package ID.

**Deployed on Active Clients** shows you the package version and the corresponding ID. You can also see how many clients (**Client Count**) and users (**User Count**) use the package. **Last Seen** shows you when RealmJoin last checked Client Count and User Count.

Below 'Deployed on Active Clients' you can see a list of all installed software versions. This list offers the following attributes:

| Attribut      | Explanation                                                                                     |
| ------------- | ----------------------------------------------------------------------------------------------- |
| **Type**      | <p>There are two in RealmJoin:<br></p><ul><li>Windows Installer</li><li>Windows Store</li></ul> |
| **Name**      | Software name                                                                                   |
| **Publisher** | Publisher of the Software                                                                       |
| **Version**   | Version of the installed software                                                               |
| **Clients**   | Count of using clients (for more details see [Client Report](software-report.md#client-report)) |
| **Users**     | Count of users (for more details see [Users Report](software-report.md#users-report))           |
| **Licenses**  | Count of existing licenses                                                                      |

In the upper right corner is a short description of the software or package.

### Client Report

If you click a number that is listed under 'Client' in the detail view, you will get to the menu **Clients that have \[Software name] installed.**

![](<../.gitbook/assets/software-report3 (1).png>)

The existing list shows the following attributes:

| Attribute            | Explanation                                                                                                      |
| -------------------- | ---------------------------------------------------------------------------------------------------------------- |
| **Name (latest)**    | The latest client name                                                                                           |
| **Primary User**     | The primary user of the client                                                                                   |
| **Version (latest)** | The latest RealmJoin version                                                                                     |
| **ID**               | Client ID number                                                                                                 |
| **First Seen**       | The first connection to RealmJoin                                                                                |
| **Last Contact**     | The last connection to RealmJoin                                                                                 |
| **Us**               | The count of the client's users (for more details see [Users of a Client](software-report.md#users-of-a-client)) |

#### Users of a Client

If you select one of the numbers in the **Us** column, you will get an overview of all users of a client:

![](<../.gitbook/assets/software-report4 (1).png>)

You will see the following information about each user:

| Attribute        | Explanation                                                                                 |
| ---------------- | ------------------------------------------------------------------------------------------- |
| **Name**         | <p>User name</p><ul><li>Black icon = Primary user</li><li>White icon = Guest user</li></ul> |
| **ID**           | User ID number                                                                              |
| **First Seen**   | First connection to RealmJoin                                                               |
| **Last Contact** | Last connection to RealmJoin                                                                |
| **Gr**           | Count of group memberships of the user                                                      |
| **Pa**           | Count of owning software packages                                                           |
| **Cl**           | Count of owning clients                                                                     |
| **Se**           | Count of configured settings                                                                |

### Users Report

If you click a number that is listed under 'User' in the detail view, you will get to the menu **Users that have \[Software name] installed.**

![](<../.gitbook/assets/software-report5 (1).png>)

The existing list shows the following attributes:

| Attribute        | Explanation                            |
| ---------------- | -------------------------------------- |
| **Name**         | User name                              |
| **ID**           | User ID number                         |
| **First Seen**   | First connection to RealmJoin          |
| **Last Contact** | Last connection to RealmJoin           |
| **Gr**           | Count of group memberships of the user |
| **Pa**           | Count of owning software packages      |
| **Cl**           | Count of owning clients                |
| **Se**           | Count of configured settings           |
