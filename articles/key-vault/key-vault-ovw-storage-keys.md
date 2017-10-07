---
ms.assetid: 
title: "aaaAzure clés de compte de stockage de coffre de clé"
description: "Clés de compte de stockage fournissent une intégration transparent entre Azure Key Vault et l’accès en fonction de la clé tooAzure compte de stockage."
ms.topic: article
services: key-vault
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/25/2017
ms.openlocfilehash: becdf97798a08164c48d3a7a14aea6ca54085c9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-storage-account-keys"></a>Clés de compte de stockage Azure Key Vault

Avant de clés de compte de stockage Azure clé de coffre, les développeurs avaient toomanage leurs propres clés de compte de stockage Azure (ASA) et les faire pivoter manuellement ou via une automatisation externe. À présent, les clés de compte de stockage Key Vault sont implémentées sous forme de [secrets Key Vault](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) pour l’authentification avec un compte de stockage Azure. 

fonctionnalité de clé ASA Hello gère rotation secret pour vous et exonère hello votre contact direct avec une clé ASA en offrant l’accès partagé des Signatures (SAS) en tant que méthode. 

Pour plus d’informations générales sur les comptes de stockage Azure, consultez la page [À propos des comptes de stockage Azure](https://docs.microsoft.com/azure/storage/storage-create-storage-account).

## <a name="supporting-interfaces"></a>Prise en charge des interfaces

Hello fonctionnalités clés de compte de stockage Azure sont disponible via hello REST, .NET / C# et PowerShell d’interfaces. Pour plus d’informations, consultez la page [Informations de référence Key Vault](https://docs.microsoft.com/azure/key-vault/).


## <a name="storage-account-keys-behavior"></a>Comportement des clés de compte de stockage

### <a name="what-key-vault-manages"></a>Ce que gère Key Vault

Key Vault exécute plusieurs fonctions de gestion interne à votre place lorsque vous utilisez des clés de compte de stockage.

1. Azure Key Vault gère les clés d’un compte de stockage Azure (ASA). 
    - En interne, Azure Key Vault peut lister (synchroniser) les clés avec un compte de stockage Azure.  
    - Azure Key Vault régénère (pivote) hello clés périodiquement. 
    - Valeurs de clés ne sont jamais retournés dans la réponse toocaller. 
    - Azure Key Vault gère les clés des comptes de stockage ainsi que des comptes de stockage Classic. 
2. Coffre de clés Azure permet de vous, propriétaire de l’archivage/objet hello, définitions de toocreate SAS (compte ou service SAS). 
    - Hello valeur de SAP, créé à l’aide de la définition de SAS, est retourné en tant que secret via le chemin d’accès de hello URI REST. Pour plus d’informations, consultez la page [Opérations du compte de stockage Azure Key Vault](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations).

### <a name="naming-guidance"></a>Aide pour l’affectation de noms

Les noms des comptes de stockage doivent comporter entre 3 et 24 caractères, uniquement des lettres minuscules et des chiffres.  
 
Un nom de définition de SAP doit avoir une longueur comprise entre 1 et 102 caractères, composés uniquement de 0-9, a-z et A-Z.

## <a name="developer-experience"></a>Expérience de développement 

### <a name="before-azure-key-vault-storage-keys"></a>Avant l’apparition des clés de stockage Azure Key Vault 

Les développeurs utilisaient hello de toodo tooneed pratiques avec un compte tooget clé accès tooAzure de stockage. 
 
 ```
//create storage account using connection string containing account name 
// and hello storage key 

var storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));
var blobClient = storageAccount.CreateCloudBlobClient();
 ```
 
### <a name="after-azure-key-vault-storage-keys"></a>Après l’apparition des clés de stockage Azure Key Vault 

```
//Please make sure tooset storage permissions appropriately on your key vault
Set-AzureRmKeyVaultAccessPolicy -VaultName 'yourVault' -ObjectId yourObjectId -PermissionsToStorage all

//Use PowerShell command tooget Secret URI 

Set-AzureKeyVaultManagedStorageSasDefinition -Service Blob -ResourceType Container,Service -VaultName yourKV  
-AccountName msak01 -Name blobsas1 -Protocol HttpsOnly -ValidityPeriod ([System.Timespan]::FromDays(1)) -Permission Read,List

//Get SAS token from Key Vault

var secret = await kv.GetSecretAsync("SecretUri");

// Create new storage credentials using hello SAS token. 

var accountSasCredential = new StorageCredentials(secret.Value); 

// Use credentials and hello Blob storage endpoint toocreate a new Blob service client. 

var accountWithSas = new CloudStorageAccount(accountSasCredential, new Uri ("https://myaccount.blob.core.windows.net/"), null, null, null); 

var blobClientWithSas = accountWithSas.CreateCloudBlobClient(); 
 
// If SAS token is about tooexpire then Get sasToken again from Key Vault and update it.

accountSasCredential.UpdateSASToken(sasToken);

  ```
 
 ### <a name="developer-best-practices"></a>Meilleures pratiques de développement 

- Autoriser uniquement le coffre de clés toomanage vos clés ASA. N’essayez pas de toomanage les vous-même, vous n’interférera avec les processus du coffre de clés. 
- N’autorisez pas ASA toobe de clés géré par plusieurs objets de coffre de clés. 
- Si vous avez besoin toomanually régénérer vos clés ASA, nous vous recommandons de les régénérer via le coffre de clés. 

## <a name="getting-started"></a>Prise en main

### <a name="setup-for-role-based-access-control-rbac-permissions"></a>Configuration des autorisations de contrôle d’accès en fonction des permissions (RBAC)

Le coffre de clés a besoin d’autorisations trop*liste* et *régénérer* clés pour un compte de stockage. Vous pouvez configurer ces autorisations à l’aide de hello comme suit :

- Récupérez la valeur ObjectId de Key Vault : 

    `Get-AzureRmADServicePrincipal -SearchString "AzureKeyVault"`

- Affecter tooAzure du rôle opérateur de clé de stockage identité de coffre de clé : 

    `New-AzureRmRoleAssignment -ObjectId <objectId of AzureKeyVault from previous command> -RoleDefinitionName 'Storage Account Key Operator Service Role' -Scope '<azure resource id of storage account>'`

    >[!NOTE]
    > Pour un type de compte classique, définir un paramètre de rôle hello trop*« Classique stockage compte clé Service de rôle d’opérateur »*.

### <a name="storage-account-onboarding"></a>Intégration des comptes de stockage 

Exemple : En tant que propriétaire d’un objet de coffre de clés vous ajoutez un stockage compte objet tooyour Azure Key Vault tooonboard un compte de stockage.

Lors de l’intégration, le coffre de clés doit tooverify qu’identité hello du compte de l’intégration de hello dispose des autorisations trop*liste* et trop*régénérer* clés de stockage. Dans commande tooverify ces autorisations, le coffre de clés Obtient un OBO (à la place de) jeton à partir du service d’authentification hello, audience tooAzure Gestionnaire de ressources et rend un *liste* service de stockage Azure toohello appel de clé. Si hello *liste* appel échoue, hello de création de l’objet échoue avec un code d’état HTTP de coffre de clés *interdit*. les clés de Hello répertoriées de cette manière sont mis en cache avec le stockage de votre entité de coffre de clés. 

Le coffre de clés doit vérifier que les identités hello a *régénérer* autorisations avant de prendre possession de régénérer vos clés. tooverify hello identité, via le jeton OBO, ainsi que hello première identité de tiers le coffre de clés dispose de ces autorisations :

- Le coffre de clés répertorie les autorisations de RBAC sur la ressource de compte de stockage hello.
- Le coffre de clés valide réponse hello via des actions et les actions non correspondance d’expression régulière. 

Recherchez des exemples de prise en charge dans la section relative aux [exemples de clés de comptes de stockage gérés de Key Vault](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167).

Si l’identité de hello n’est pas *régénérer* autorisations ou si la première identité de tiers du coffre de clés n’a pas *liste* ou *régénérer* autorisation, puis l’intégration de hello demande échouera et retournera un code d’erreur approprié et un message. 

jeton OBO Hello fonctionne uniquement lorsque vous utilisez internes, les applications clientes natives de PowerShell ou CLI.

## <a name="other-applications"></a>Autres applications

- Jetons SAP, construits à l’aide de clés de compte de stockage de coffre de clés, fournissent davantage un accès contrôlé tooan compte de stockage Azure. Pour plus d’informations, consultez [Utilisation des signatures d’accès partagé](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).

## <a name="see-also"></a>Voir aussi

- [Présentation des clés, des secrets et des certificats](https://docs.microsoft.com/rest/api/keyvault/)
- [Blog de l’équipe Key Vault](https://blogs.technet.microsoft.com/kv/)
