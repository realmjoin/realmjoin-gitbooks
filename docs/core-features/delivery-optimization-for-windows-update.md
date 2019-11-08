# Delivery Optimization for Windows Update

**Windows Update Delivery Optimization** \(WUDO\) is a self-organized solution for distributed caches for Windows Updates. In default mode, WUDO identifies peers as part of a WAN based on their external IP. In case of stretched out WANs with just one breakout point, this leads to a high network load and a bottleneck.  
To improve the handling, Microsoft Intune can be used to set WUDO to **DownloadMode=2**, where peers are grouped by a groupID. The ID \(GUID\) is set for each device using network fingerprinting and the MAC address of the default gateway and therefore creating a more localized group. RealmJoin can be used to set the groupID for each client.

The following registry key is set to define the DOGroupID:

### Network-Fingerprint-GUID in Reg-Key

```text
HKLM\SOFTWARE\Policies\Microsoft\Windows\DeliveryOptimization\DOGroupId
HKLM\SOFTWARE\Policies\Microsoft\Windows\DeliveryOptimization\GroupId
```

Remember to set the Download Mode to **Group** via Windows Update settings in Intune:

```text
Delivery optimization download mode: 
HTTP blended with peering across private group
```

This is effectively **DownloadMode=2**. Opting-out of setting the groupID via RealmJoin can be done by setting the [Policies.SetNetworkOptimizationID](http://docs.realmjoin.com/policies.html#policies) to **false**.

For more on WUDO see the [Microsoft WUDO documentation \(DE\)](https://docs.microsoft.com/de-de/windows/deployment/update/waas-delivery-optimization).

