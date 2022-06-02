# KeyVault

Cloud applications and services use cryptographic keys and secrets to help keep information secure. Azure Key Vault safeguards these keys and secrets. When you use Key Vault, you can encrypt authentication keys, storage account keys, data encryption keys, .pfx files, and passwords by using keys that are protected by hardware security modules.

## Create KeyVault

The following table shows you the steps for Azure KeyVault Creation:

| Task                                                                                                                                                                             | Image                                              |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------- |
| 1. Open [Azure Portal](https://portal.azure.com)                                                                                                                                 |                                                    |
| 2. Start with **Create a resource**                                                                                                                                              | ![](<../../.gitbook/assets/keyvault1 (1).png>)     |
| 3. Type in **Key Vault** in the search field                                                                                                                                     | ![](<../../.gitbook/assets/keyvault2 (1) (1).png>) |
| 4. On the detail page click **Create**                                                                                                                                           |                                                    |
| <p>5. Fill out the required fields.<br><br>Please make sure to use a distinct naming scheme for the keyvault URL.<br><br>For example: <strong>rj-[tenant]-[service]</strong></p> | ![](<../../.gitbook/assets/keyvault3 (1).png>)     |
| 6. Click **Review + Create**                                                                                                                                                     |                                                    |
| 7. Review your settings and configurations and click **Create**                                                                                                                  |                                                    |
| 8. Wait for the successful deployment                                                                                                                                            |                                                    |
| 9. Click **Go to resource**                                                                                                                                                      |                                                    |
| 10. Navigate to **Access policies**                                                                                                                                              | ![](<../../.gitbook/assets/keyvault4 (1).png>)     |
| 11. Click **Add Access Policies**                                                                                                                                                |                                                    |
| 12. Select **Key, Secret & Certificate Management** as template and add RealmJoin as **Select principal**                                                                        | ![](<../../.gitbook/assets/keyvault5 (1).png>)     |
| 13. Click **Key permissions**                                                                                                                                                    |                                                    |
| 14. For **Cryptographic Operations** add Decrypt, Encrypt, Unwrap Key, Wrap Key, Verify and Sign                                                                                 | ![](<../../.gitbook/assets/keyvault6 (1).png>)     |
| 15. Click **Save** and then **OK**                                                                                                                                               |                                                    |
| 16. Finally, go to **Overview** and share the **DNS Name** with the [Glück & Kanja support](mailto:product.support@glueckkanja.com)                                              | ![](<../../.gitbook/assets/keyvault7 (1).png>)     |
| **Example Value**: https://example-rj-localadmin.vault.azure.net                                                                                                                 |                                                    |

## KeyVault Storage of Secrets

RealmJoin will not store the secret in any proprietary storage but instead create an **Azure KeyVault Secret** to store it in a secure and auditable way. 

The entry in KeyVault will be added with the device name as a key and the plain GUID as the secret value. See the following example screenshot:

[![CreateKeyVault](<../../.gitbook/assets/keyvault8 (1) (2).png>)](https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/keyvault8.png)

[![KeyVaultStorageofSecrets](<../../.gitbook/assets/keyvault9 (1) (1) (2).png>)](https://github.com/realmjoin/realmjoin-gitbooks/tree/3c2250fcc0d712e1b40ac535a1766b57ce01910c/docs/media/keyvault9.png)
