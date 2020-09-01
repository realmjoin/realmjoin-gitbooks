# Interactive Installation

## Interactive Installation

If an administrator wants to install RealmJoin on a device without mass deployment or the Microsoft Intune infrastructure, he/she may download the MSI and do an interactive installation or copy one of the command lines below to download and run in a single step.

### Command Line Installation

You may download and install RealmJoin in a single step by using the following command lines. This may help especially when testing scenarios or new software packages in virtual machines.

#### Release Channel:

```text
@powershell -NoProfile -ExecutionPolicy unrestricted -Command "((new-object net.webclient).DownloadFile('https://gkrealmjoin.s3.amazonaws.com/win-release/RealmJoin.exe', 'realmjoin.exe'))" && .\realmjoin.exe
```

#### Beta Channel:

```text
@powershell -NoProfile -ExecutionPolicy unrestricted -Command "((new-object net.webclient).DownloadFile('https://gkrealmjoin.s3.amazonaws.com/win-beta/RealmJoin.exe', 'realmjoin.exe'))" && .\realmjoin.exe
```

#### Canary Channel:

```text
@powershell -NoProfile -ExecutionPolicy unrestricted -Command "((new-object net.webclient).DownloadFile('https://gkrealmjoin.s3.amazonaws.com/win-canary/RealmJoin.exe', 'realmjoin.exe'))" && .\realmjoin.exe
```

### Silent Installation

When installing RealmJoin during unattended OS installation or any other non-interactive deployment method you may decide not to have any UI interaction during installation. To install RealmJoin in such a scenario, use the silent installation option:

```text
reamjoin.exe -install
```

## 

