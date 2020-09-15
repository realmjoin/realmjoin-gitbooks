# Core Extension

## Core Extension

### Ensure Core Extension in RealmJoin portal

To ensure the extensions are correctly deployed on all clients, please add the core extensions Chocolatey package to the back-end with **order 1** and assign it to the global core group.

### Enable extension CmdLets in Craft packages

Out of Chocolatey packages, the usage of the extension CmdLets has to be enabled:

```text
Import-Module (Get-ItemPropertyValue -Path "Registry::HKLM\SOFTWARE\RealmJoin\Variables" -Name RealmjoinCraftSupportModulePath)
```

### Useable RealmJoin variables

#### Chocolatey variables

* $packagePrefix = flavour prefix of this package
* $packageName = name of this package
* $packageVersion = version of this package
* $packageVersionObject = \[System.Version\]$env:packageVersion
* $packageVersionNoRevisionObject = New-Object System.Version -ArgumentList $packageVersionObject.Major, $packageVersionObject.Minor, $packageVersionObject.Build
* $packageParameters = parameters as specified in the assignment arguments
* $packageFolder = folder in which the package is extracted
* $packageToolsFolder = sub directory "tools" of a Chocolatey package, contains the install script. Defined as: Join-Path $env:packageFolder "tools"
* $packageTempDir = temp directory which is used for the package. Defined as: Join-Path $env:TEMP \(Join-Path $env:chocolateyPackageName $env:chocolateyPackageVersion\)
* $PackageID = unique ID of the package

**Environment variables**

* $env:RJ\_Version
* $env:RJ\_UserSID = SID of the user who started this package installation. Can be used in system crafts if parameters are initialized
* $env:RJ\_ChocolateyPackage = glueckkanja-test-choco
* $env:RJ\_InstalledVersion = 1.0.0.1
* $envRJ\_PackageID = glueckkanja-test-choco
* $env:RJ\_DeploymentPhase = contains information on the installation.  
  Can be:

  ```text
  Blank

  RunningFirstDeployment
  RunningFirstDeploymentAuto
   - Now the installations start
  CompletedFirstDeployment

  RunningDeployment
   - Now the installations start
  CompletedDeployment

  ManualDeployment
   - Now the installations start
  ```

{% hint style="warning" %}
**Important**  
  
In order to keep the following sections easy to read und clear, a lot of extensions are based only on Chocolatey. Of course these extensions are also usable for Craft. Therefore you have to remove '**Chocolatey**' from an extension to make it valid for '**Craft**'.  
  
For example:  
  
Chocolatey extension =`Get-ChocolateyRealmjoinLocaleId`  
Craft extension =`Get-RealmjoinLocaleId`
{% endhint %}

### AppV Packages

#### Enable-ChocolateyRealmjoinAppv

This command will enable AppV on current client with BranchCache as supported.

**Syntax**

```text
Enable-ChocolateyRealmjoinAppv
```

#### Install-ChocolateyRealmjoinAppvPackage

This command will add and publish an AppV package

**Syntax**

```text
Install-ChocolateyRealmjoinAppvPackage [[-fileName] <string>] [[-fileChecksum] <string>] [[-DynamicDeploymentConfiguration] <string>] [<CommonParameters>]
```

**Parameters**

```text
Name                           Aliases Description Required? Pipeline Input? Default Value
----                           ------- ----------- --------- --------------- -------------
DynamicDeploymentConfiguration None                false     false                        
fileChecksum                   None                false     false                        
fileName                       None                false     false
```

#### Uninstall-ChocolateyRealmjoinAppvPackage

This command stops and removes an AppV Package.

{% hint style="info" %}
If needed a used connection group will also be stopped upfront.
{% endhint %}

**Syntax**

```text
Uninstall-ChocolateyRealmjoinAppvPackage [[-name] <string>] [<CommonParameters>]
```

**Parameters**

```text
Name Aliases Description Required? Pipeline Input? Default Value
---- ------- ----------- --------- --------------- -------------
name None                false     false
```

#### Get-ChocolateyRealmjoinAppvPackageVfsPath

**Syntax**

```text
Get-ChocolateyRealmjoinAppvPackageVfsPath [[-appvPackage] <Object>] [<CommonParameters>]
```

**Parameters**

```text
Name        Aliases Description Required? Pipeline Input? Default Value
----        ------- ----------- --------- --------------- -------------
appvPackage None                false     false
```

#### Install-ChocolateyRealmjoinAppvConnectionGroup

This command adds and enables a connection group by a xml-based definition given as its filename

**Syntax**

```text
Install-ChocolateyRealmjoinAppvConnectionGroup 
```

**Parameters**

```text

```

#### Uninstall-ChocolateyRealmjoinAppvConnectionGroup

This command removes a connection group for AppV packages

**Syntax**

```text
Uninstall-ChocolateyRealmjoinAppvConnectionGroup
```

**Parameters**

```text

```

### Logs and Transforms

#### Get-ChocolateyRealmjoinLocaleId

Returns the corresponding LocaleID of a given locale string \(e. g. en-US or de-De\)

{% hint style="info" %}
If the translation fails, the default localeID 1033 \(en-US\) is returned. Can be overwritten with a custom default value.
{% endhint %}

**Syntax**

```text
Get-ChocolateyRealmjoinLocaleId [[-localeString] <string>] [[-defaultLocaleId] <int>] [<CommonParameters>]
```

**Parameters**

```text
Name            Aliases Description Required? Pipeline Input? Default Value
----            ------- ----------- --------- --------------- -------------
defaultLocaleId None                false     false                        
localeString    None                false     false
```

#### Get-ChocolateyRealmjoinLocaleMsiTransform

Based on the given LocaleID this command will return the path of the localized transform file.

By default the file is supposed to be located in package root folder. A parent folder for localed file can provided as a parameter \(**localeTransformsFolder**\).

{% hint style="info" %}
* The root folder for any file reference inside the scripts are always **tools**.
* For using locale string \(e. g. de-de\) as input the command be combinded output from **Get-ChocolateyRealmjoinLocaleId.**
{% endhint %}

**Syntax**

```text
Get-ChocolateyRealmjoinLocaleMsiTransform [[-localeString] <string>] [[-localeTransformsFolder] <string>] [[-defaultLocaleId] <int>] [<CommonParameters>]
```

**Parameters**

```text
Name                   Aliases Description Required? Pipeline Input? Default Value
----                   ------- ----------- --------- --------------- -------------
defaultLocaleId        None                false     false                        
localeString           None                false     false                        
localeTransformsFolder None                false     false
```

#### Get-ChocolateyRealmjoinLogFilePath

This command will return the realmjoin-specific logfile path including a package-specific logfile depending on the execution context.

**Syntax**

```text
Get-ChocolateyRealmjoinLogFilePath [[-operation] <string>] [[-target] <string>] [<CommonParameters>]
```

**Parameters**

```text
Name      Aliases Description Required? Pipeline Input? Default Value
----      ------- ----------- --------- --------------- -------------
operation None                false     false                        
target    None                false     false
```

### Chocolatey Packages

#### Install-ChocolateyRealmjoinPackage

This command will install a software \(installer file from cloud blob storage\).

**Syntax**

```text
Install-ChocolateyRealmjoinPackage [[-installerFileName] <string>] [[-installerFileChecksum] <string>] [[-msiTransforms] <string[]>] [[-msiTransformsCabs] <string[]>] [[-additionalArgs] <string[]>] [[-silentArgs] <string[]>] [[-validExitCodes] <int[]>] [[-installers] <psobject[]>] [[-preActions] <scriptblock>] [[-postActions] <scriptblock>] [[-installPackage] <bool>] [[-noInstallMessage] <string>] [-installerFileNameIsLocalPath] [<CommonParameters>]
```

**Parameters**

```text
Name                         Aliases Description Required? Pipeline Input? Default Value
----                         ------- ----------- --------- --------------- -------------
additionalArgs               None                false     false                        
installPackage               None                false     false                        
installerFileChecksum        None                false     false                        
installerFileName            None                false     false                        
installerFileNameIsLocalPath None                false     false                        
installers                   None                false     false                        
msiTransforms                None                false     false                        
msiTransformsCabs            None                false     false                        
noInstallMessage             None                false     false                        
postActions                  None                false     false                        
preActions                   None                false     false                        
silentArgs                   None                false     false                        
validExitCodes               None                false     false
```

#### Uninstall-ChocolateyRealmjoinPackage

This command uninstalls a software package.

By default MSI based installer is performed with the most common silent parameters. The valid exitcodes for success are set to 0, 1641, 3010 for MSI and EXE based installer.

Optionally args for a silent uninstallation, valid exitcodes for success and post-installation actions as a PowerShell `scriptblock` \(e. g. deleting a desktop shortcut\) can be provided.

{% hint style="info" %}
* The parameter **additionalArgs** is populated with args from the given uninstall info \(object\) and can **not** be overwritten. Use **silentsArgs** to apply additional parameter\(s\) for a silent uninstallation.
* If parameters from uninstall info \(object\) are not suitable for a successful \(silent\) uninstallation, you can provide the uninstall info manually as parameters. You have to provide a uninstaller executable file \(**uninstallerFile**\), uninstall args \(**additionalArgs**\) and a package name \(**subPackageName**\) for product to be uninstalled.
{% endhint %}

**Syntax**

```text
Uninstall-ChocolateyRealmjoinPackage [[-uninstallerFile] <string>] [[-additionalArgs] <string[]>] [[-silentArgs] <string[]>] [[-validExitCodes] <int[]>] [[-subPackageName] <string>] [[-uninstallers] <psobject[]>] [[-uninstallInfo] <Object>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

**Parameters**

```text
Name            Aliases Description Required? Pipeline Input? Default Value
----            ------- ----------- --------- --------------- -------------
Confirm         cf                  false     false                        
WhatIf          wi                  false     false                        
additionalArgs  None                false     false                        
silentArgs      None                false     false                        
subPackageName  None                false     false                        
uninstallInfo   None                false     true (ByValue)               
uninstallerFile None                false     false                        
uninstallers    None                false     false                        
validExitCodes  None                false     false
```

#### Import-ChocolateyRealmjoinPackageParameters

Retrieves the package parameter given provided by the RealmJoin Portal \(package or user assignment\). Those parameters will become available inside the  scripting as prefixed variable \(**packParam**\). A parameter like **/Language:de-de** will be provided as the variable **$packParamLanguage** with the string value of **de-de**.

**Syntax**

```text
Import-ChocolateyRealmjoinPackageParameters [[-params] <string>] [-setVariables] [-clearVariables] [-returnKeyValuePairs] [-returnParameterHashset] [<CommonParameters>]
```

**Parameters**

```text
Name                   Aliases Description Required? Pipeline Input? Default Value
----                   ------- ----------- --------- --------------- -------------
clearVariables         None                false     false                        
params                 None                false     false                        
returnKeyValuePairs    None                false     false                        
returnParameterHashset None                false     false                        
setVariables           None                false     false
```

#### Test-ChocolateyRealmjoinRegistryUninstallExists

With this command you can test if a software exist on your system. This test based on the uninstall info from **Get-ChocolateyRealmjoinRegistryUninstallInfo**.

**Syntax**

```text
Test-ChocolateyRealmjoinRegistryUninstallExists [[-keyNameFilter] <string>] [[-displayNameFilter] <string>] [[-publisherFilter] <string>] [[-versionGe] <version>] [[-versionGt] <version>] [[-versionLe] <version>] [[-versionLt] <version>] [[-filterScriptblock] <scriptblock>] [<CommonParameters>]
```

**Parameters**

```text
Name              Aliases Description Required? Pipeline Input? Default Value
----              ------- ----------- --------- --------------- -------------
displayNameFilter None                false     false                        
filterScriptblock None                false     false                        
keyNameFilter     None                false     false                        
publisherFilter   None                false     false                        
versionGe         None                false     false                        
versionGt         None                false     false                        
versionLe         None                false     false                        
versionLt         None                false     false
```

#### Get-ChocolateyRealmjoinRegistryUninstallInfo

With this command you can get the common uninstall infos as PSObject of all items.

**Syntax**

```text
Get-ChocolateyRealmjoinRegistryUninstallInfo [[-keyNameFilter] <string>] [[-displayNameFilter] <string>] [[-publisherFilter] <string>] [[-versionGe] <version>] [[-versionGt] <version>] [[-versionLe] <version>] [[-versionLt] <version>] [[-filterScriptblock] <scriptblock>] [<CommonParameters>]
```

**Parameters**

```text
Name              Aliases Description Required? Pipeline Input? Default Value
----              ------- ----------- --------- --------------- -------------
displayNameFilter None                false     false                        
filterScriptblock None                false     false                        
keyNameFilter     None                false     false                        
publisherFilter   None                false     false                        
versionGe         None                false     false                        
versionGt         None                false     false                        
versionLe         None                false     false                        
versionLt         None                false     false
```

#### Get-ChocolateyRealmjoinRegistryUninstallStrings

With this command you will get an object with key name, file and arguments of an uninstall info match. You will get this info from **Get-ChocolateyRealmjoinRegistryUninstallInfo**.

**Syntax**

```text
Get-ChocolateyRealmjoinRegistryUninstallStrings [-uninstallKeyNameFilter] <string> [<CommonParameters>]
```

**Parameters**

```text
Name                   Aliases Description Required? Pipeline Input? Default Value
----                   ------- ----------- --------- --------------- -------------
uninstallKeyNameFilter None                true      false
```

#### Get-ChocolateyRealmjoinWebFile

Downloads given filename \(archive\) from cloud blob storage.

**Syntax**

```text
Get-ChocolateyRealmjoinWebFile [[-fileName] <string>] [[-fileChecksum] <string>] [[-remoteFileName] <string>] [-extractArchive] [<CommonParameters>]
```

**Parameters**

```text
Name           Aliases Description Required? Pipeline Input? Default Value
----           ------- ----------- --------- --------------- -------------
extractArchive None                false     false                        
fileChecksum   None                false     false                        
fileName       None                false     false                        
remoteFileName None                false     false
```

#### Invoke-RealmjoinChocoPackageInstallation

**Syntax**

```text
Invoke-RealmjoinChocoPackageInstallation [[-packageName] <string>] [[-params] <hashtable>] [<CommonParameters>]
```

**Parameters**

```text
Name        Aliases Description Required? Pipeline Input? Default Value
----        ------- ----------- --------- --------------- -------------
packageName None                false     false                        
params      None                false     false
```

### Command line

#### Join-RealmjoinCommandLine

**Syntax**

```text
Join-RealmjoinCommandLine [[-CommandOnly] <string>] [[-ArgumentsOnly] <string>] [<CommonParameters>]
```

**Parameters**

```text
Name          Aliases Description Required? Pipeline Input? Default Value
----          ------- ----------- --------- --------------- -------------
ArgumentsOnly None                false     false                        
CommandOnly   None                false     false
```

#### Split-RealmjoinCommandLine

**Syntax**

```text
Split-RealmjoinCommandLine [[-CommandLine] <string>] [<CommonParameters>]
```

**Parameters**

```text
Name        Aliases Description Required? Pipeline Input? Default Value
----        ------- ----------- --------- --------------- -------------
CommandLine None                false     false
```

#### Get-RealmjoinCommandLineWithLauncher

**Syntax**

```text
Get-RealmjoinCommandLineWithLauncher [[-CommandLine] <string>] [[-CommandOnly] <string>] [[-ArgumentsOnly] <string>] [-ReturnSplit] [<CommonParameters>]
```

**Parameters**

```text
Name          Aliases Description Required? Pipeline Input? Default Value
----          ------- ----------- --------- --------------- -------------
ArgumentsOnly None                false     false                        
CommandLine   None                false     false                        
CommandOnly   None                false     false                        
ReturnSplit   None                false     false
```

#### Restart-RealmjoinComputer

A system restart can be initiated. By default with a delay of 10 seconds, which can be overwritten by the corresponding parameter. Optional you can provide a message by parameter. Behind the scene, a scheduled task is created which performs a shutdown with a parameter for restart.

**Syntax**

```text
Restart-RealmjoinComputer [[-Delay] <timespan>] [[-Message] <string>] [<CommonParameters>]
```

**Parameters**

```text
Name    Aliases Description Required? Pipeline Input? Default Value
----    ------- ----------- --------- --------------- -------------
Delay   None                false     false                        
Message None                false     false
```

#### Get-RealmjoinComputerSystemBiosVersion

**Syntax**

```text
Get-RealmjoinComputerSystemBiosVersion
```

#### Get-RealmjoinComputerSystemModel

**Syntax**

```text
Get-RealmjoinComputerSystemModel [-IncludeDebugInfoIfUnsure] [<CommonParameters>]
```

**Parameters**

```text
Name                     Aliases Description Required? Pipeline Input? Default Value
----                     ------- ----------- --------- --------------- -------------
IncludeDebugInfoIfUnsure None                false     false
```

### Custom States

#### Out-RealmjoinCustomState

This command creates a custom state with a mandatory name and input object.

**Syntax**

```text
Out-RealmjoinCustomState [-Name] <string> [[-InputObject] <Object>] [<CommonParameters>]
```

**Parameters**

```text
Name        Aliases Description Required? Pipeline Input? Default Value
----        ------- ----------- --------- --------------- -------------
InputObject None                false     true (ByValue)               
Name        None                true      false
```

#### Remove-RealmjoinCustomState

This command removes a custom state

**Syntax**

```text
Remove-RealmjoinCustomState [-Name] <string> [<CommonParameters>]
```

**Parameters**

```text
Name Aliases Description Required? Pipeline Input? Default Value
---- ------- ----------- --------- --------------- -------------
Name None                true      false
```

### Scheduled Tasks

Using predefined RealmJoin cmdlets, it is possible to register scheduled tasks in system or user scope. The cmdlet provides an XML template, that is modified following the used parameters. Tasks also might be unscheduled.

#### Register-RealmjoinCustomStateScheduledTask

This command registers a scheduled task with package title a its name for creation. By default with a repetition interval of one day and a mandatory PowerShell script \(**publishState.ps1**\) in the current script dir.

Optionally the parameters **PublishStateScriptFile** can be overwritten.

**Syntax**

```text
Register-RealmjoinCustomStateScheduledTask [[-RepetitionInterval] <timespan>] [[-TaskName] <string>] [[-PublishStateScriptFile] <string>]
```

**Parameters**

```text
Name                   Aliases Description Required? Pipeline Input? Default Value
----                   ------- ----------- --------- --------------- -------------
PublishStateScriptFile None                false     false           ".\publishState.ps1"                        
RepetitionInterval     None                false     false           "1.00:00:00"             
TaskName               None                false     false           $env:packageTitle
```

#### Unregister-RealmjoinCustomStateScheduledTask

This command removes the custom state scheduled task by its name - typically the package title.

**Syntax**

```text
Unregister-RealmjoinCustomStateScheduledTask [[-TaskName] <string>] [[-PublishStateScriptFile] <string>]
```

**Parameters**

```text
Name                   Aliases Description Required? Pipeline Input? Default Value
----                   ------- ----------- --------- --------------- -------------
PublishStateScriptFile None                false     false                        
TaskName               None                false     false
```

#### Get-RealmjoinInvocationParameters

**Syntax**

```text
Get-RealmjoinInvocationParameters [[-Invocation] <InvocationInfo>] [<CommonParameters>]
```

**Parameters**

```text
Name       Aliases Description Required? Pipeline Input? Default Value
----       ------- ----------- --------- --------------- -------------
Invocation None                false     false
```

#### Get-RealmjoinPathRooted

**Syntax**

```text
Get-RealmjoinPathRooted [[-Path] <string>] [<CommonParameters>]
```

**Parameters**

```text
Name Aliases Description Required? Pipeline Input? Default Value
---- ------- ----------- --------- --------------- -------------
Path None                false     false
```

#### New-RealmjoinScheduledTaskBootTrigger

This command will create a boot scheduled task trigger

**Syntax**

```text
New-RealmjoinScheduledTaskBootTrigger [[-Enabled] <bool>] [[-StartBoundary] <datetime>] [[-EndBoundary] <datetime>] [[-RepetitionInterval] <timespan>] [[-RepetitionDuration] <timespan>] [[-Delay] <timespan>] [<CommonParameters>]
```

**Parameters**

```text
Name               Aliases Description Required? Pipeline Input? Default Value
----               ------- ----------- --------- --------------- -------------
Delay              None                false     false                        
Enabled            None                false     false                        
EndBoundary        None                false     false                        
RepetitionDuration None                false     false                        
RepetitionInterval None                false     false                        
StartBoundary      None                false     false
```

#### New-RealmjoinScheduledTaskDailyTrigger

This command will create a daily scheduled task trigger

**Syntax**

```text
New-RealmjoinScheduledTaskDailyTrigger [[-Enabled] <bool>] [[-StartBoundary] <datetime>] [[-EndBoundary] <datetime>] [[-RepetitionInterval] <timespan>] [[-RepetitionDuration] <timespan>] [[-RandomDelay] <timespan>] [[-DaysInterval] <uint32>] [<CommonParameters>]
```

**Parameters**

```text
Name               Aliases Description Required? Pipeline Input? Default Value
----               ------- ----------- --------- --------------- -------------
DaysInterval       None                false     false                        
Enabled            None                false     false                        
EndBoundary        None                false     false                        
RandomDelay        None                false     false                        
RepetitionDuration None                false     false                        
RepetitionInterval None                false     false                        
StartBoundary      None                false     false
```

#### New-RealmjoinScheduledTaskLogonTrigger

This command will create a logon scheduled task trigger.

**Syntax**

```text
New-RealmjoinScheduledTaskLogonTrigger [[-Enabled] <bool>] [[-StartBoundary] <datetime>] [[-EndBoundary] <datetime>] [[-RepetitionInterval] <timespan>] [[-RepetitionDuration] <timespan>] [[-Delay] <timespan>] [<CommonParameters>]
```

**Parameters**

```text
Name               Aliases Description Required? Pipeline Input? Default Value
----               ------- ----------- --------- --------------- -------------
Delay              None                false     false                        
Enabled            None                false     false                        
EndBoundary        None                false     false                        
RepetitionDuration None                false     false                        
RepetitionInterval None                false     false                        
StartBoundary      None                false     false
```

#### New-RealmjoinScheduledTaskTimeTrigger

This command will create a custom scheduled task trigger.

**Syntax**

```text
New-RealmjoinScheduledTaskTimeTrigger [[-DelayFromNow] <timespan>] [[-Enabled] <bool>] [[-StartBoundary] <datetime>] [[-EndBoundary] <datetime>] [[-RepetitionInterval] <timespan>] [[-RepetitionDuration] <timespan>] [[-RandomDelay] <timespan>] [<CommonParameters>]
```

**Parameters**

```text
Name               Aliases Description Required? Pipeline Input? Default Value
----               ------- ----------- --------- --------------- -------------
DelayFromNow       None                false     false                        
Enabled            None                false     false                        
EndBoundary        None                false     false                        
RandomDelay        None                false     false                        
RepetitionDuration None                false     false                        
RepetitionInterval None                false     false                        
StartBoundary      None                false     false
```

#### New-RealmjoinScheduledTaskXml

This command creates \(and optionally registers\) a scheduled task with a given action and trigger, e. g. loggon trigger.

By default its only returns the XML content for a scheduled task, enabled with `user` as principal and a execution time limit of 15 minutes. To optionally register the task the parameter **Register** and a mandatory task name \(**TaskName**\) must be provided.

{% hint style="info" %}
Optional `switch`parameters to start the task once after creation \(**StartOnce**\) or for deleting the task after its first run \(**DeleteAfterFirstRun**\) can be set.
{% endhint %}

**Syntax**

```text
New-RealmjoinScheduledTaskXml [[-Principal] <ScheduledTaskPrincipal>] [[-Action] <Object[]>] [[-Trigger] <Object[]>] [[-Enabled] <bool>] [[-ExecutionTimeLimit] <timespan>] [[-TaskName] <string>] [-DeleteAfterFirstRun] [-Register] [-StartOnce] [<CommonParameters>]
```

**Parameters**

```text
Name                Aliases Description Required? Pipeline Input? Default Value
----                ------- ----------- --------- --------------- -------------
Action              None                false     false                        
DeleteAfterFirstRun None                false     false                        
Enabled             None                false     false                        
ExecutionTimeLimit  None                false     false                        
Principal           None                false     false                        
Register            None                false     false                        
StartOnce           None                false     false                        
TaskName            None                false     false                        
Trigger             None                false     false
```

### Shortcuts

The following cmdlets allow to remove, create or modify shortcuts ot/on the desktop or the global start menu.

#### New-RealmjoinShortcut

This command will create shortcuts. If you do so, this shortcut will follow a defined **TargetPath** and a defined **shortcutPath**

**Syntax**

```text
New-RealmjoinShortcut [-shortcutPath] <string> [-targetPath] <string> [[-targetArguments] <string>] [[-workingDirectory] <string>] [[-description] <string>] [[-iconLocation] <string>] [[-hotKey] <string>] [[-windowStyle] <int>] [-forCurrentUser] [-onDesktop] [<CommonParameters>]
```

**Parameters**

```text
Name             Aliases Description Required? Pipeline Input? Default Value
----             ------- ----------- --------- --------------- -------------
description      None                false     false                        
forCurrentUser   None     Shortcuts are enabled for current user           false     false                        
hotKey           None                false     false                        
iconLocation     None                false     false                        
onDesktop        None     Path will create on the desktop           false     false                        
shortcutPath     None                true      false                        
targetArguments  None                false     false                        
targetPath       None                true      false                        
windowStyle      None                false     false                        
workingDirectory None                false     false
```

#### Remove-RealmjoinShortcut

This command will remove shortcuts

**Syntax**

```text
Remove-RealmjoinShortcut [-shortcutPath] <string> [-forCurrentUser] [-onDesktop] [<CommonParameters>]
```

**Parameters**

```text
Name           Aliases Description Required? Pipeline Input? Default Value
----           ------- ----------- --------- --------------- -------------
forCurrentUser None      Remove and disable a shortcut for current user          false     false                        
onDesktop      None      Remove a shortcut from desktop          false     false                        
shortcutPath   None                true      false
```

#### Format-RealmjoinShortcutPath

**Syntax**

```text
Format-RealmjoinShortcutPath [-shortcutPath] <string> [-forCurrentUser] [-onDesktop] [-doNotCheckCreateFolder] [<CommonParameters>]
```

**Parameters**

```text
Name                   Aliases Description Required? Pipeline Input? Default Value
----                   ------- ----------- --------- --------------- -------------
doNotCheckCreateFolder None                false     false                        
forCurrentUser         None                false     false                        
onDesktop              None                false     false                        
shortcutPath           None                true      false
```

#### Start-RealmjoinSoftwarePackageInstallation

**Syntax**

```text
Start-RealmjoinSoftwarePackageInstallation [[-packageName] <string>] [<CommonParameters>]
```

**Parameters**

```text
Name        Aliases Description Required? Pipeline Input? Default Value
----        ------- ----------- --------- --------------- -------------
packageName None                false     false
```

#### Add-RealmjoinExeToTaskbar

This command attaches a given path to the Windows taskbar.

{% hint style="info" %}
Only the extension types `.exe`and `.lnk`are supported.
{% endhint %}

**Syntax**

```text
Add-RealmjoinExeToTaskbar
```

**Parameters**

```text

```

### Fonts

tbd

#### Add-RealmjoinFont

This command adds and registers a font to the system by a given path to the font file.

**Syntax**

```text
Add-RealmjoinFont
```

**Parameters**

```text

```

#### Remove-RealmjoinFont

This command removes a font from the system.

{% hint style="info" %}
If you only know the file path, you can provide the mandatory name by using the PowerShell pipeline with the output of command **Get-RealmjoinFontName**.
{% endhint %}

**Syntax**

```text
Remove-RealmjoinFont
```

**Parameters**

```text

```

#### Get-RealmjoinFontName

This command returns the font name of a given font file.

{% hint style="info" %}
The output can typically used to remove a font without knowing the font name and using the command **Remove-RealmjoinFont**.
{% endhint %}

**Syntax**

```text
Get-RealmjoinFontName
```

**Parameters**

```text

```

### Registry

tbd

#### Get-RealmjoinRegistryValue

Returns the value of one or more registry entries. Will return $null \(or hashtable with entries set to $null\) of the registry key or any entries are missing, but will not fail. If only one registry entry is requested, its value will be returned directly. If more than one registry entry is requested, a hashtable will be returned.

**Syntax**

```text
Get-RealmJoinRegistryValue [-Path] <string> [-Name] <string[]> [<CommonParameters>]
```

**Parameters**

```text

```

#### Update-RealmjoinRegistryValue

This command sets a registry to a specific value or removes the entry \(if value is $null\). It will also create the registry key of it does not exist.

**Syntax**

```text
Update-RealmJoinRegistryValue [-Path] <string> [-Name] <string> [[-Value] <Object>] [[-ValueKind] <RegistryValueKind>] [-ReturnTrueOnChange] [<CommonParameters>]
```

**Parameters**

```text

```

### INI Files

tbd

#### Get-RealmjoinIniFileValue

This command returns the value of an entry in the given section of the specific ini-file.

Optionally a default value will be return, if key name is not found, can be provided.

**Syntax**

```text
Get-RealmjoinIniFileValue [-IniFilePath] <string> [-SectionName] <string> [-KeyName] <string> [[-DefaultValue] <string>] [<CommonParameters>]
```

**Parameters**

```text

```

#### Update-RealmjoinIniFileValue

This command sets a given value of an entry in the given section of the specific ini-file.

{% hint style="info" %}
* Any **existing** value will be overwritten.
* Providing `$null`for section, key name or value will be removes itself from the file.
{% endhint %}

**Syntax**

```text
Update-RealmjoinIniFileValue [-IniFilePath] <string> [-SectionName] <string> [[-KeyName] <Object>] [[-Value] <Object>] [<CommonParameters>]
```

**Parameters**

```text

```

### Logging

tbd

#### Copy-RealmjoinExternalLogFiles

This command copies product-specific logfiles from a given location to the common RealmJoin-specific location. By default every file with a last write time greater or equal then 5 seconds before script start will be collected.

Optionally a filename filter \(e.g. \*.log\), in- or exluding filename\(s\) can be provided. Optional `switch` parameters for deletion after copy \(**DeleteAfterCopy**\), creation time prefixing \(**PrefixWithCreationTime**\) and a recursivley copy including subfolders \(**Recurse**\) can be set.

{% hint style="info" %}
The parameter **NotBefore** can be overwritten with a custom value of type`[DateTime]`. Alternatively for more specific filtering with a powershell `scriptblock`, used as a criteria for **Where-Object**, can be given.
{% endhint %}

**Syntax**

```text
Copy-RealmjoinExternalLogFiles [[-Path] <string[]>] [[-Filter] <string>] [[-Exclude] <string[]>] [[-Include] <string[]>] [[-NotBefore] <datetime>] [[-FilterScriptblock] <scriptblock>] [[-Destination] <string>] [-Recurse] [-PrefixWithCreationTime] [-DeleteAfterCopy] [<CommonParameters>]
```

**Parameters**

```text

```

#### Get-ChocolateyRealmjoinLogFilePath

This command returns a RealmJoin-specific log file path including a package-specific log file depending on the script execution context. Optionally a operation \(e.g. `<scriptname>`\) and a target \(e.g. `start_licenseactivation.exe`\) can be provided.

{% hint style="info" %}
In absence of parameter **Operation** it will be set to an empty string, if the executing script name is **chocolateyInstall.ps1**, **chocolateyUninstall.ps1** or **rj\_install.ps1**. Otherwise the executing script name without its extension will used as value for parameter.
{% endhint %}

**Syntax**

```text
Get-ChocolateyRealmjoinLogFilePath [[-Target] <string>]
```

**Parameters**

```text

```

#### Get-RealmjoinLogFilePath

Internal function for command for **Get-ChocolateyRealmjoinLogFilePath**

#### Get-RealmjoinPackageLogDir

This command returns a RealmJoin-specific location for log files depending on the script execution context.

**Syntax**

```text
Get-RealmjoinPackageLogDir [[-RealmjoinPackageName] <string>] [<CommonParameters>]
```

**Parameters**

```text

```

### Firewall

tbd

#### Disable-RealmjoinFirewallPopup

This command adds a firewall rule with the given executable path. The package name will set as the display name for the rule.

**Syntax**

```text
Disable-RealmjoinFirewallPopup [[-exePath] <string>] [<CommonParameters>]
```

**Parameters**

```text

```

#### Disable-RealmjoinFirewallPopupJava

This command applies a firewall rule by adding the common java executables \(java.exe, javaw.exe, jnlplauncher.exe\) to the given path of Java.

Optionally the java executable file\(s\) can be overwritten by the parameter **exeFiles** \(e. g. javaw.exe\)

**Syntax**

```text
Disable-RealmjoinFirewallPopupJava [[-javaRootFolder] <string>] [[-exeFiles] <string[]>] [<CommonParameters>]
```

**Parameters**

```text

```

#### Disable-RealmjoinFirewallPopupJavaAppV

This command applies a firewall rule by adding the common **appv - specific** java executables \(java.exe, javaw.exe, jnlplauncher.exe\) to the given **AppV package**. 

Optionally the java executable file\(s\) can be overwritten by the parameter "exeFiles" \(e.g. javaw.exe\).

**Syntax**

```text
Disable-RealmjoinFirewallPopupJavaAppV [[-appvPackage] <Object>] [[-exeFiles] <string[]>] [<CommonParameters>]
```

**Parameters**

```text

```

#### Remove-RealmjoinFirewallRules

This command removes a firewall rule by its display name, typically the package name.

**Syntax**

```text
Remove-RealmjoinFirewallRules
```

**Parameters**

```text

```

### Specials

tbd

#### Remove-RealmjoinFileAtReboot

A given file will be marked to be **deleted after rebooting** the system.

**Syntax**

```text
Remove-RealmjoinFileAtReboot [-LiteralPath] <string[]> [<CommonParameters>]
```

**Parameters**

```text

```

#### Get-RealmjoinWrpFileProtectionState

This command returns a boolean with the value `$True`, if the file protected. Typically a helper for command **Remove-RealmjoinFileAtReboot**.

**Syntax**

```text
Get-RealmjoinWrpFileProtectionState [-LiteralPath] <string> [<CommonParameters>]
```

**Parameters**

```text

```

#### Update-RealmjoinHostsFile

This command adds one or more entries to the `hosts`file of the system. Behind the scene these entries are added as a block with RealmJoin - specific comments.

For an update you must always provide **all \(including previous\) entries**. By providing the `switch`parameter **CleanUp** the whole RealmJoin - specific block of entries will be removed from the file.

**Syntax**

```text
Update-RealmjoinHostsFile [[-entries] <string[]>] [-cleanup] [<CommonParameters>]
```

**Parameters**

```text

```

#### Convert-RealmjoinStringToBoolean

Convert boolean related **strings** like '1', 'true', '0' and 'false' to its corresponding and valid boolean type. The default return value, if conversion failed is `$false`.

{% hint style="info" %}
The default return value can be overwritten to  `$true` or `$null`
{% endhint %}

**Syntax**

```text
Convert-RealmjoinStringToBoolean [-InputObject] <string> [[-DefaultValue] <bool>] [<CommonParameters>]
```

**Parameters**

```text

```

#### Wait-RealmjoinCondition

This command loops and waits for a given condition provided as a PowerShell `scriptblock`.

By default with **0.5 minutes timeout**, the condition as display name and final throw of a exception by reaching the timeout. The parameter 'TimeOutMinutes', 'TimeOutSeconds', 'DisplayName' and final action 'OnTimeout' can be overwritten.

**Syntax**

```text
Wait-RealmjoinCondition [-Condition] <scriptblock> [[-TimeOutMinutes] <double>] [[-TimeOutSeconds] <int>] [[-DisplayName] <string>] [[-OnTimeout] <scriptblock>] [<CommonParameters>]
```

**Parameters**

```text

```

#### Invoke-RealmjoinWithRetry

This command invoke a given action \(defined as `scriptblock`\) with retries and also executes a fail and a final fail action.

By default with maximal **4** retries and an delay of **1** seconds increased by **1.5** seconds each retry. Optionally a fail \('OnErrorRetry'\) and a **final** fail \('OnErrorFinal'\) action can be provided as a `scriptblock`.

The parameters 'RetryDelaySeconds', 'MaxRetries' can be overwritten. The increment of the delay can be suppressed by providing the `switch` parameter 'DoNotIncreaseDelay'.

**Syntax**

```text
Invoke-RealmjoinWithRetry [-ScriptBlock] <scriptblock> [[-RetryDelaySeconds] <int>] [[-MaxRetries] <int>] [[-OnErrorRetryPrefix] <string>] [[-OnErrorRetry] <scriptblock>] [[-OnErrorFinal] <scriptblock>] [-DoNotIncreaseDelay] [<CommonParameters>]
```

**Parameters**

```text

```

#### Invoke-RealmjoinChocoPackageInstallation

tbd

**Syntax**

```text
Invoke-RealmjoinChocoPackageInstallation [[-packageName] <string>] [[-params] <hashtable>] [-allowFromIntune] [<CommonParameters>]
```

**Parameters**

```text

```

#### Invoke-RealmjoinChocoPackage**Uninstall**

tbd

**Syntax**

```text
Invoke-RealmjoinChocoPackageUninstall [[-packageName] <string>] [-allowFromIntune] [-returnPriorState] [<CommonParameters>]
```

**Parameters**

```text

```

#### Invoke-RealmjoinDevChocoScript

tbd

**Syntax**

```text
Invoke-RealmjoinDevChocoScript [[-scriptToRun] <string>] [[-params] <Object>] [-uninstall] [-copyBlobs]
```

**Parameters**

```text

```

#### Restart-RealmjoinComputer

This command initiates a system restart.

By default with a delay of **10 seconds**, which can be overwritten by the parameter 'Delay'.

Optionally a message can be provided by the parameter 'Message'. Behind the scene a scheduled task is created which performs a shutdown with parameter for restart.

**Syntax**

```text
Restart-RealmjoinComputer [[-Delay] <timespan>] [[-Message] <string>] [<CommonParameters>]
```

**Parameters**

```text

```

#### Enable-ChocolateyRealmjoinAppv

This command enables AppV service on current client with BranchCache as supported. For enabling the **Package Scripts** support the optional parameter 'enablePackageScripts' can be used.

{% hint style="info" %}
Publishing is only allow with **administrative permissons.**
{% endhint %}

**Syntax**

```text
Enable-ChocolateyRealmjoinAppv
```

**Parameters**

```text

```

#### Get-RealmjoinJavaAppvRootFolder

This command returns the **root AppV path** \(Vfs\) of Java Runtime Environment by giving any existing AppV package.

**Syntax**

```text
Get-RealmjoinJavaAppvRootFolder [[-appvPackage] <Object>] [<CommonParameters>]
```

**Parameters**

```text

```

