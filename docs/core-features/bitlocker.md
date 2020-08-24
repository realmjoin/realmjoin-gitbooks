# BitLocker

### BitLocker enforcement

It is possible to force BitLocker encryption for OS volumes. The configuration file \(see chapter [Settings](settings.md#policies-requiresecurityfeatures-bitlockerenabled)\) allows to set the switch **BitlockerEnabled** to **true**. If the device is equipped with a **ready state** TPM chip the encryption is activated.

### BitLocker recovery key

To allow the BitLocker enforcement, the following registry key

```text
HKLM\SYSTEM\CurrentControlSet\Control\BitLocker:PreventDeviceEncryption
```

is set to **false**.

For virtual machines, the encryption is only enforced, if the virtual machines variables are:

```text
$env:RjDisableVmDetection=1
```

If the client device is Azure AD joined, RealmJoin uploads the BitLocker recovery key to Azure AD. If the upload is not successful on the first try, it will be retried. If the upload cannot be performed successfully, the RealmJoin rollout fails. In the case of a **non-AAD-joined** device, the BitLocker recovery key is not saved anywhere.

