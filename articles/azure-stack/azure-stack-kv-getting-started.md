---
title: "Mise en route avec le coffre de clés dans la pile de Azure | Documents Microsoft"
description: "Commencer à l’aide de la pile d’Azure Key Vault"
services: azure-stack
documentationcenter: 
author: rlfmendes
manager: natmack
editor: 
ms.assetid: b973be33-2fc1-4ee6-976a-84ed270e7254
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/23/2017
ms.author: ricardom
ms.openlocfilehash: 32fad3ce17c877db661573e67c9cb5948b3c78fa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-key-vault"></a>Mise en route avec le coffre de clés
Cette section décrit les étapes pour créer un coffre, gérer les clés et les clés secrètes ainsi que pour autoriser des utilisateurs ou des applications pour appeler des opérations dans le coffre dans la pile de Azure. Les étapes suivantes supposent un abonnement locataire existe et KeyVault service est enregistré au sein de cet abonnement. Tous les exemples de commandes sont basées sur les applets de commande KeyVault disponibles dans le cadre du kit SDK Azure PowerShell.

## <a name="enabling-the-tenant-subscription-for-vault-operations"></a>L’activation de l’abonnement du client pour les opérations d’archivage
Avant de pouvoir émettre des opérations par rapport à un coffre-fort, vous devez vous assurer que votre abonnement est activé pour les opérations d’archivage. Vous pouvez confirmer qu’en émettant la commande PowerShell suivante :

    Get-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault | ft -AutoSize

La sortie de la commande ci-dessus doit signaler les « Enregistré » pour l’état « Registration » de chaque ligne.

    ProviderNamespace RegistrationState ResourceTypes Locations
    Microsoft.KeyVault Registered {operations} {local}
    Microsoft.KeyVault Registered {vaults} {local}
    Microsoft.KeyVault Registered {vaults/secrets} {local}


 Si tel n’est pas le cas, vous devez appeler la commande suivante pour inscrire le service KeyVault dans votre abonnement :

    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault

Et ce qui suit est la sortie de la commande :

    ProviderNamespace : Microsoft.KeyVault
    RegistrationState : Registered
    ResourceTypes : {operations, vaults, vaults/secrets}
    Locations : {local}


> [!NOTE]
> Si vous obtenez l’erreur : «*l’abonnement n’est pas inscrit auprès d’Azure Key Vault*» lors de l’appel des applets de commande KeyVault, vérifiez que vous avez activé le fournisseur de ressources KeyVault par les instructions ci-dessus.
> 
> 

## <a name="creating-a-hardened-container-a-vault-in-azure-stack-to-store-and-manage-cryptographic-keys-and-secrets"></a>Création d’un conteneur de sécurisation renforcé (un coffre) dans la pile de Azure pour stocker et gérer des clés de chiffrement et des clés secrètes
Pour créer un coffre, un locataire devez d’abord créer un groupe de ressources. Les commandes PowerShell créent un groupe de ressources, puis un coffre dans ce groupe de ressources. L’exemple inclut également les sorties à partir de cette applet de commande.

### <a name="creating-a-resource-group"></a>Création d’un groupe de ressources :
    New-AzureRmResourceGroup -Name vaultrg010 -Location local -Verbose -Force

Output:

    VERBOSE: Performing the operation "Replacing resource group ..." on target "".
    VERBOSE: 12:52:51 PM - Created resource group 'vaultrg010' in location 'local'
    ResourceGroupName : vaultrg010
    Location : local
    ProvisioningState : Succeeded
    Tags :
    ResourceId : /subscriptions/fa881715-3802-42cc-a54e-a06adf61584d/resourceGroups/vaultrg010


### <a name="creating-a-vault"></a>Création d’un coffre :
    New-AzureRmKeyVault -VaultName vault010 -ResourceGroupName vaultrg010 -Location local -Verbose

Output:

    VaultUri : https://vault010.vault.local.azurestack.global
    TenantId : 5454420b-2e38-4b9e-8b56-1712d321cf33
    TenantName : 5454420b-2e38-4b9e-8b56-1712d321cf33
    Sku : Standard
    EnabledForDeployment : False
    EnabledForTemplateDeployment : False
    EnabledForDiskEncryption : False
    AccessPolicies : {5454420b-2e38-4b9e-8b56-1712d321cf33}
    AccessPoliciesText :
    Tenant ID : 5454420b-2e38-4b9e-8b56-1712d321cf33
    Object ID : ca342e90-f6aa-435b-a11c-dfe5ef0bfeeb
    Application ID :
    Display Name : Tenant Admin (tenantadmin1@msazurestack.onmicrosoft.com)
    Permissions to Keys : get, create, delete, list, update, import, backup, restore
    Permissions to Secrets : all
    OriginalVault : Microsoft.Azure.Management.KeyVault.Vault
    ResourceId : /subscriptions/fa881715-3802-42cc-a54e-a06adf61584d/resourceGroups/vaultrg010/providers/Microsoft.KeyVault/vaults/vault010
    VaultName : vault010
    ResourceGroupName : vaultrg010
    Location : local
    Tags : {}
    TagsTable :

La sortie de cette applet de commande affiche les propriétés du coffre de clés que vous venez de créer. Les deux propriétés les plus importantes sont :

* **Nom de coffre**: dans l’exemple, il s’agit de **vault010**. Vous allez utiliser ce nom pour les autres applets de commande Key Vault.
* **URI de coffre**: dans l’exemple, il s’agit d’https://vault010.vault.local.azurestack.global. Les applications qui utilisent votre coffre via son API REST doivent utiliser cet URI.

Votre compte Azure est pour l’instant le seul autorisé à effectuer des opérations sur ce coffre de clés.

## <a name="operating-on-keys-and-secrets"></a>Fonctionne sur les clés et les clés secrètes
Après avoir créé un coffre, suivez les étapes ci-dessous pour créer, gérer les clés et les secrets :

### <a name="creating-a-key"></a>Création d’une clé
Pour créer une clé, utilisez la **Add-AzureKeyVaultKey** par l’exemple ci-dessous. Après la création réussie de la clé, l’applet de commande affiche les détails de la clé nouvellement créées.

    Add-AzureKeyVaultKey -VaultName \$vaultName -Name\$keyVaultKeyName -Verbose -Destination Software

Voici la sortie de la *Add-AzureKeyVaultKey* applet de commande :

    Attributes : Microsoft.Azure.Commands.KeyVault.Models.KeyAttributes
    Key : {"kid":"https://vault010.vault.local.azurestack.global/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff","kty":"RSA","key\_ops":\["encrypt"
    ,"decrypt","sign","verify","wrapKey","unwrapKey"\],"n":"nDkcBQCyyLnXtbwFMnXOWzPDqWKiyjf0G3QTxvuN\_MansEn9X-91q4\_WFmRBCd5zWBqz671iuZO\_D4r0P25
    Fe2lAq\_3T1gATVNGR7LTEU9W5h8AoY10bmt4e0y66Jn2vUV-UTCz4\_vtKSKoiuNXHFR\_tGZ-6YX-frqKIiC8pbE4Qvz1x-c7E-eM\_Cpu87koL95n-Hl3wQRQRPXEPRR6gcHR5E74D1
    gLEFCWKySTo4nXtLoeBMNK5QYEBZIAS61ACbR4czjHn6ty-tZeVTc7hyK\_UO2EbJovQIAhyayfq018uNtCBzjjkqJKnY34kviVCPoTQqOdpHa0FHrloe5FeIw","e":"AQAB"}
    VaultName : vault010
    Name : keyVaultKeyName001
    Version : 86062b02b10342688f3b0b3713e343ff
    Id : https://vault010.vault.local.azurestack.global:443/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff

Vous pouvez maintenant référencer cette clé que vous avez créée ou téléchargée dans Azure Key Vault à l’aide de son URI. Utilisez **https://vault010.vault.local.azurestack.global:443/clés/keyVaultKeyName001** pour obtenir la version actuelle ; toujours utiliser **https://vault010.vault.local.azurestack.global:443/clés keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff** pour obtenir cette version spécifique.

### <a name="retrieving-a-key"></a>La récupération d’une clé
Utilisez le **Get-AzureKeyVaultKey** pour récupérer une clé et ses détails par l’exemple suivant :

    Get-AzureKeyVaultKey -VaultName vault010 -Name keyVaultKeyName001

Voici la sortie de Get-AzureKeyVaultKey

    Attributes : Microsoft.Azure.Commands.KeyVault.Models.KeyAttributes
    Key : {"kid":"https://vault010.vault.local.azurestack.global/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff","kty":"RSA","key\_ops":\["encrypt"
    ,"decrypt","sign","verify","wrapKey","unwrapKey"\],"n":"nDkcBQCyyLnXtbwFMnXOWzPDqWKiyjf0G3QTxvuN\_MansEn9X-91q4\_WFmRBCd5zWBqz671iuZO\_D4r0P25
    Fe2lAq\_3T1gATVNGR7LTEU9W5h8AoY10bmt4e0y66Jn2vUV-UTCz4\_vtKSKoiuNXHFR\_tGZ-6YX-frqKIiC8pbE4Qvz1x-c7E-eM\_Cpu87koL95n-Hl3wQRQRPXEPRR6gcHR5E74D1
    gLEFCWKySTo4nXtLoeBMNK5QYEBZIAS61ACbR4czjHn6ty-tZeVTc7hyK\_UO2EbJovQIAhyayfq018uNtCBzjjkqJKnY34kviVCPoTQqOdpHa0FHrloe5FeIw","e":"AQAB"}
    VaultName : vault010
    Name : keyVaultKeyName001
    Version : 86062b02b10342688f3b0b3713e343ff
    Id : https://vault010.vault.local.azurestack.global:443/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff

### <a name="setting-a-secret"></a>Définition d’une clé secrète
    $secretvalue = ConvertTo-SecureString 'User@123' -AsPlainText -Force
    Set-AzureKeyVaultSecret -Name MySecret-VaultName vault010 -SecretValue $secretvalue

Sortie

    Vault Name : vault010
    Name : MySecret
    Version : 65a387f2ed4a416180e852b970846f5b
    Id : https://vault010.vault.local.azurestack.global:443/secrets/MySecret/65a387f2ed4a416180e852b970846f5b
    Enabled : True
    Expires :
    Not Before :
    Created : 8/17/2016 10:49:52 PM
    Updated : 8/17/2016 10:49:52 PM
    Content Type :
    Tags : 

### <a name="retrieving-a-secret"></a>La récupération d’une clé secrète
    Get-AzureKeyVaultSecret -VaultName vault010

Sortie

    Vault Name : vault010
    Name : MySecret
    Version :
    Id : https://vault010.vault.local.azurestack.global:443/secrets/MySecret
    Enabled : True
    Expires :
    Not Before :
    Created : 8/17/2016 10:49:52 PM
    Updated : 8/17/2016 10:49:52 PM
    Content Type :
    Tags :

À présent, votre coffre de clés et la clé/le secret sont prêts à être utilisés par les applications
qui doivent recevoir les autorisations adéquates.

## <a name="authorize-the-application-to-use-the-key-or-secret"></a>Autorisation de l’application à utiliser la clé ou le secret
Pour autoriser l’application d’accéder à la clé ou le secret dans le coffre, utilisez la commande Set -**AzureRmKeyVaultAccessPolicy** applet de commande.

Par exemple, si le nom de votre coffre est *ContosoKeyVault* et dispose de l’application que vous souhaitez autoriser un *ID Client* de *8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed*et que vous vous souhaitez autoriser l’application pour déchiffrer et vous connecter avec des clés dans le coffre, exécutez la commande suivante :

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToKeys decrypt,sign

Si vous souhaitez autoriser cette même application à lire les éléments secrets de votre coffre, exécutez la commande suivante :

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToSecrets Get


## <a name="next-steps"></a>Étapes suivantes
[Déployer une machine virtuelle avec un mot de passe Key Vault](azure-stack-kv-deploy-vm-with-secret.md)

[Déployer une machine virtuelle avec un certificat Key Vault](azure-stack-kv-push-secret-into-vm.md)

