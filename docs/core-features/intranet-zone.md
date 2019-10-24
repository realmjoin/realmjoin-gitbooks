# Intranet Zone

## Intranet Zone

Site may be added to the **Intranet Zone** \(in Internet Options\) by specifying a setting with the key `Policies.TrustedSites` and an array of URLs. These URLs are parsed by RealmJoin and written to a registry key called **ZoneMap**.

One might specify the following JSON array:

```text
["file://example.com", "https://foo.example.com"]
```

* Windows will interpret a naked domain like `file://example.com` as `file://*.example.com`.
* RealmJoin does not allow for wildcard protocols. You must specify all protocols explicitly.
* RealmJoin will manage all protocols for a configured domain and remove any user added protocols.
* RealmJoin will not manage other domains which are not configured in this setting.

### Recommendations

Many customers have extensive Intranet Zone list. Clean it up! Investigate whether a site works without adding it to the Intranet Zone.

* Add a site using `https` protocol if it uses Integrated Windows Authentication or other legacy features like ActiveX.
* Add a server using `file` protocol if it is accessed using SMB.

