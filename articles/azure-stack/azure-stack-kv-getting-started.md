---
title: "aaaGetting a démarré avec le coffre de clés dans la pile de Azure | Documents Microsoft"
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
ms.openlocfilehash: 66ae55291951ee0c673ba2b50ea4aecb3df19a88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-key-vault"></a>Mise en route avec le coffre de clés
Cette section décrit hello étapes toocreate un coffre, gérer les clés et les clés secrètes ainsi autoriser des utilisateurs ou des applications opérations tooinvoke dans le coffre de hello dans la pile d’Azure. Hello suit supposent un abonnement locataire existe et KeyVault service est enregistré au sein de cet abonnement. Toutes les commandes d’exemple hello reposent sur hello KeyVault d’applets de commande disponibles dans le cadre de hello Kit de développement logiciel Azure PowerShell.

## <a name="enabling-hello-tenant-subscription-for-vault-operations"></a>L’activation d’abonnement du locataire hello pour les opérations d’archivage
Avant de pouvoir émettre des opérations par rapport à un coffre-fort, vous devez tooensure votre abonnement est activé pour les opérations de coffre. Vous pouvez confirmer qu’en émettant hello suivant de commande PowerShell :

    Get-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault | ft -AutoSize

sortie Hello Hello ci-dessus commande rapport « Enregistré » hello état « Registration » de chaque ligne.

    ProviderNamespace RegistrationState ResourceTypes Locations
    Microsoft.KeyVault Registered {operations} {local}
    Microsoft.KeyVault Registered {vaults} {local}
    Microsoft.KeyVault Registered {vaults/secrets} {local}


 Si tel n’est pas le cas de hello, vous devez appeler hello après commande tooregister hello KeyVault service au sein de votre abonnement :

    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault

Et hello suivants est sortie hello de commande hello :

    ProviderNamespace : Microsoft.KeyVault
    RegistrationState : Registered
    ResourceTypes : {operations, vaults, vaults/secrets}
    Locations : {local}


> [!NOTE]
> Si vous obtenez hello erreur : «*abonnement de hello n’est pas inscrit auprès d’Azure Key Vault*» lors de l’appel des applets de commande KeyVault, vérifiez que vous avez activé le fournisseur de ressources KeyVault hello par les instructions ci-dessus.
> 
> 

## <a name="creating-a-hardened-container-a-vault-in-azure-stack-toostore-and-manage-cryptographic-keys-and-secrets"></a>Création d’un conteneur de sécurisation renforcé (un coffre) dans la pile de Azure toostore et gérer les clés de chiffrement et les clés secrètes
Dans l’ordre toocreate un coffre, un locataire devez d’abord créer un groupe de ressources. Hello commandes PowerShell suivantes créent un groupe de ressources, puis un coffre dans ce groupe de ressources. Hello exemple inclut également la sortie de type hello à partir de cette applet de commande.

### <a name="creating-a-resource-group"></a>Création d’un groupe de ressources :
    New-AzureRmResourceGroup -Name vaultrg010 -Location local -Verbose -Force

Output:

    VERBOSE: Performing hello operation "Replacing resource group ..." on target "".
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
    Permissions tooKeys : get, create, delete, list, update, import, backup, restore
    Permissions tooSecrets : all
    OriginalVault : Microsoft.Azure.Management.KeyVault.Vault
    ResourceId : /subscriptions/fa881715-3802-42cc-a54e-a06adf61584d/resourceGroups/vaultrg010/providers/Microsoft.KeyVault/vaults/vault010
    VaultName : vault010
    ResourceGroupName : vaultrg010
    Location : local
    Tags : {}
    TagsTable :

sortie Hello de cette applet de commande affiche les propriétés du coffre de clés hello que vous venez de créer. propriétés les plus importantes Hello deux sont :

* **Nom de coffre**: dans l’exemple de hello, il s’agit **vault010**. Vous allez utiliser ce nom pour les autres applets de commande Key Vault.
* **URI de coffre**: dans l’exemple de hello, il s’agit https://vault010.vault.local.azurestack.global. Les applications qui utilisent votre coffre via son API REST doivent utiliser cet URI.

Votre compte Azure est désormais toutes les opérations sur cette clé de coffre tooperform autorisé. coffre de clés.

## <a name="operating-on-keys-and-secrets"></a>Fonctionne sur les clés et les clés secrètes
Après avoir créé un coffre, hello suivez ci-dessous les étapes toocreate gérer les clés et les secrets :

### <a name="creating-a-key"></a>Création d’une clé
Dans l’ordre toocreate une clé, utilisez hello **Add-AzureKeyVaultKey** par exemple hello ci-dessous. Après la création réussie de la clé, applet de commande hello produira hello nouvellement créé les détails de la clé.

    Add-AzureKeyVaultKey -VaultName \$vaultName -Name\$keyVaultKeyName -Verbose -Destination Software

Hello Voici la sortie hello Hello *Add-AzureKeyVaultKey* applet de commande :

    Attributes : Microsoft.Azure.Commands.KeyVault.Models.KeyAttributes
    Key : {"kid":"https://vault010.vault.local.azurestack.global/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff","kty":"RSA","key\_ops":\["encrypt"
    ,"decrypt","sign","verify","wrapKey","unwrapKey"\],"n":"nDkcBQCyyLnXtbwFMnXOWzPDqWKiyjf0G3QTxvuN\_MansEn9X-91q4\_WFmRBCd5zWBqz671iuZO\_D4r0P25
    Fe2lAq\_3T1gATVNGR7LTEU9W5h8AoY10bmt4e0y66Jn2vUV-UTCz4\_vtKSKoiuNXHFR\_tGZ-6YX-frqKIiC8pbE4Qvz1x-c7E-eM\_Cpu87koL95n-Hl3wQRQRPXEPRR6gcHR5E74D1
    gLEFCWKySTo4nXtLoeBMNK5QYEBZIAS61ACbR4czjHn6ty-tZeVTc7hyK\_UO2EbJovQIAhyayfq018uNtCBzjjkqJKnY34kviVCPoTQqOdpHa0FHrloe5FeIw","e":"AQAB"}
    VaultName : vault010
    Name : keyVaultKeyName001
    Version : 86062b02b10342688f3b0b3713e343ff
    Id : https://vault010.vault.local.azurestack.global:443/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff

Vous pouvez maintenant référencer cette clé que vous avez créé ou téléchargé tooAzure le coffre de clés, à l’aide de son URI. Utilisez **https://vault010.vault.local.azurestack.global:443/clés/keyVaultKeyName001** tooalways obtenir la version actuelle de hello ; et utiliser **https://vault010.vault.local.azurestack.global:443/clés keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff** tooget cette version spécifique.

### <a name="retrieving-a-key"></a>La récupération d’une clé
Hello d’utilisation **Get-AzureKeyVaultKey** tooretrieve une clé et ses détails par hello selon exemple :

    Get-AzureKeyVaultKey -VaultName vault010 -Name keyVaultKeyName001

Hello Voici la sortie de hello de Get-AzureKeyVaultKey

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

Votre coffre de clés et la clé ou le secret est maintenant prête pour les applications toouse.
Vous devez autoriser les applications toouse les.

## <a name="authorize-hello-application-toouse-hello-key-or-secret"></a>Autoriser hello application toouse hello clé ou le secret
tooauthorize hello application tooaccess hello clé ou le secret de coffre hello, hello d’utiliser Set -**AzureRmKeyVaultAccessPolicy** applet de commande.

Par exemple, si le nom de votre coffre est *ContosoKeyVault* , puis hello application tooauthorize a un *ID Client* de *8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed*et que vous choix tooauthorize hello application toodecrypt et connectez-vous avec des clés dans le coffre, exécutez hello suivante :

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToKeys decrypt,sign

Si vous souhaitez tooauthorize que secrets de tooread même application dans le coffre, exécutez suivante de hello :

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToSecrets Get


## <a name="next-steps"></a>Étapes suivantes
[Déployer une machine virtuelle avec un mot de passe Key Vault](azure-stack-kv-deploy-vm-with-secret.md)

[Déployer une machine virtuelle avec un certificat Key Vault](azure-stack-kv-push-secret-into-vm.md)

