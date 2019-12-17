# Domain Connect

The following settings are necessary:

DomainConnect.Domain = "intranet.contoso.com"  
DomainConnect.NetBIOS = "CONTOSO"  
DomainConnect.CredentialName = "RealmJoin \(domain\)"

We recommend to set a CredentialName.

### User Setting - CredentialManager

You need a CredentialManager to query the above settings.

**Key** = CredentialManager  
**Value** =  
\[  
{  
"Type": "ntlm",  
"Target": "intranet.contoso.com",  
"CredentialName": "RealmJoin \(domain\)"  
}  
{

{% hint style="info" %}
Make sure that the **"CredentialName": "RealmJoin \(domain\)"** string is equal to the **DomainConnect.CredentialName = "RealmJoin \(domain\)"** string.
{% endhint %}

## Domain Password Expiry

RealmJoin uses the OnPrem AD attribute   
  
`msDS-UserPasswordExpiryTimeComputed`

to check if the user password is expired.  


