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
# <a name="azure-key-vault-storage-account-keys"></a><span data-ttu-id="023a1-103">Clés de compte de stockage Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="023a1-103">Azure Key Vault Storage Account Keys</span></span>

<span data-ttu-id="023a1-104">Avant de clés de compte de stockage Azure clé de coffre, les développeurs avaient toomanage leurs propres clés de compte de stockage Azure (ASA) et les faire pivoter manuellement ou via une automatisation externe.</span><span class="sxs-lookup"><span data-stu-id="023a1-104">Before Azure Key Vault Storage Account Keys, developers had toomanage their own Azure Storage Account (ASA) keys and rotate them manually or through an external automation.</span></span> <span data-ttu-id="023a1-105">À présent, les clés de compte de stockage Key Vault sont implémentées sous forme de [secrets Key Vault](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) pour l’authentification avec un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="023a1-105">Now, Key Vault Storage Account Keys are implemented as [Key Vault secrets](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) for authenticating with an Azure Storage Account.</span></span> 

<span data-ttu-id="023a1-106">fonctionnalité de clé ASA Hello gère rotation secret pour vous et exonère hello votre contact direct avec une clé ASA en offrant l’accès partagé des Signatures (SAS) en tant que méthode.</span><span class="sxs-lookup"><span data-stu-id="023a1-106">hello ASA key feature manages secret rotation for you and removes hello need for your direct contact with an ASA key by offering Shared Access Signatures (SAS) as a method.</span></span> 

<span data-ttu-id="023a1-107">Pour plus d’informations générales sur les comptes de stockage Azure, consultez la page [À propos des comptes de stockage Azure](https://docs.microsoft.com/azure/storage/storage-create-storage-account).</span><span class="sxs-lookup"><span data-stu-id="023a1-107">For more general information on Azure Storage Accounts, see [About Azure storage accounts](https://docs.microsoft.com/azure/storage/storage-create-storage-account).</span></span>

## <a name="supporting-interfaces"></a><span data-ttu-id="023a1-108">Prise en charge des interfaces</span><span class="sxs-lookup"><span data-stu-id="023a1-108">Supporting interfaces</span></span>

<span data-ttu-id="023a1-109">Hello fonctionnalités clés de compte de stockage Azure sont disponible via hello REST, .NET / C# et PowerShell d’interfaces.</span><span class="sxs-lookup"><span data-stu-id="023a1-109">hello Azure Storage Account keys feature is initially available through hello REST, .NET/C# and PowerShell interfaces.</span></span> <span data-ttu-id="023a1-110">Pour plus d’informations, consultez la page [Informations de référence Key Vault](https://docs.microsoft.com/azure/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="023a1-110">For more information, see [Key Vault Reference](https://docs.microsoft.com/azure/key-vault/).</span></span>


## <a name="storage-account-keys-behavior"></a><span data-ttu-id="023a1-111">Comportement des clés de compte de stockage</span><span class="sxs-lookup"><span data-stu-id="023a1-111">Storage account keys behavior</span></span>

### <a name="what-key-vault-manages"></a><span data-ttu-id="023a1-112">Ce que gère Key Vault</span><span class="sxs-lookup"><span data-stu-id="023a1-112">What Key Vault manages</span></span>

<span data-ttu-id="023a1-113">Key Vault exécute plusieurs fonctions de gestion interne à votre place lorsque vous utilisez des clés de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="023a1-113">Key Vault performs several internal management functions on your behalf when you use Storage Account Keys.</span></span>

1. <span data-ttu-id="023a1-114">Azure Key Vault gère les clés d’un compte de stockage Azure (ASA).</span><span class="sxs-lookup"><span data-stu-id="023a1-114">Azure Key Vault manages keys of an Azure Storage Account (ASA).</span></span> 
    - <span data-ttu-id="023a1-115">En interne, Azure Key Vault peut lister (synchroniser) les clés avec un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="023a1-115">Internally, Azure Key Vault can list (sync) keys with an Azure Storage Account.</span></span>  
    - <span data-ttu-id="023a1-116">Azure Key Vault régénère (pivote) hello clés périodiquement.</span><span class="sxs-lookup"><span data-stu-id="023a1-116">Azure Key Vault regenerates (rotates) hello keys periodically.</span></span> 
    - <span data-ttu-id="023a1-117">Valeurs de clés ne sont jamais retournés dans la réponse toocaller.</span><span class="sxs-lookup"><span data-stu-id="023a1-117">Key values are never returned in response toocaller.</span></span> 
    - <span data-ttu-id="023a1-118">Azure Key Vault gère les clés des comptes de stockage ainsi que des comptes de stockage Classic.</span><span class="sxs-lookup"><span data-stu-id="023a1-118">Azure Key Vault manages keys of both Storage Accounts and Classic Storage Accounts.</span></span> 
2. <span data-ttu-id="023a1-119">Coffre de clés Azure permet de vous, propriétaire de l’archivage/objet hello, définitions de toocreate SAS (compte ou service SAS).</span><span class="sxs-lookup"><span data-stu-id="023a1-119">Azure Key Vault allows you, hello vault/object owner, toocreate SAS (account or service SAS) definitions.</span></span> 
    - <span data-ttu-id="023a1-120">Hello valeur de SAP, créé à l’aide de la définition de SAS, est retourné en tant que secret via le chemin d’accès de hello URI REST.</span><span class="sxs-lookup"><span data-stu-id="023a1-120">hello SAS value, created using SAS definition, is returned as a secret via hello REST URI path.</span></span> <span data-ttu-id="023a1-121">Pour plus d’informations, consultez la page [Opérations du compte de stockage Azure Key Vault](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations).</span><span class="sxs-lookup"><span data-stu-id="023a1-121">For more information, see [Azure Key Vault storage account operations](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations).</span></span>

### <a name="naming-guidance"></a><span data-ttu-id="023a1-122">Aide pour l’affectation de noms</span><span class="sxs-lookup"><span data-stu-id="023a1-122">Naming guidance</span></span>

<span data-ttu-id="023a1-123">Les noms des comptes de stockage doivent comporter entre 3 et 24 caractères, uniquement des lettres minuscules et des chiffres.</span><span class="sxs-lookup"><span data-stu-id="023a1-123">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span>  
 
<span data-ttu-id="023a1-124">Un nom de définition de SAP doit avoir une longueur comprise entre 1 et 102 caractères, composés uniquement de 0-9, a-z et A-Z.</span><span class="sxs-lookup"><span data-stu-id="023a1-124">A SAS definition name must be 1-102 characters in length containing only 0-9, a-z, A-Z.</span></span>

## <a name="developer-experience"></a><span data-ttu-id="023a1-125">Expérience de développement</span><span class="sxs-lookup"><span data-stu-id="023a1-125">Developer experience</span></span> 

### <a name="before-azure-key-vault-storage-keys"></a><span data-ttu-id="023a1-126">Avant l’apparition des clés de stockage Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="023a1-126">Before Azure Key Vault Storage Keys</span></span> 

<span data-ttu-id="023a1-127">Les développeurs utilisaient hello de toodo tooneed pratiques avec un compte tooget clé accès tooAzure de stockage.</span><span class="sxs-lookup"><span data-stu-id="023a1-127">Developers used tooneed toodo hello following practices with a storage account key tooget access tooAzure storage.</span></span> 
 
 ```
//create storage account using connection string containing account name 
// and hello storage key 

var storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));
var blobClient = storageAccount.CreateCloudBlobClient();
 ```
 
### <a name="after-azure-key-vault-storage-keys"></a><span data-ttu-id="023a1-128">Après l’apparition des clés de stockage Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="023a1-128">After Azure Key Vault Storage Keys</span></span> 

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
 
 ### <a name="developer-best-practices"></a><span data-ttu-id="023a1-129">Meilleures pratiques de développement</span><span class="sxs-lookup"><span data-stu-id="023a1-129">Developer best practices</span></span> 

- <span data-ttu-id="023a1-130">Autoriser uniquement le coffre de clés toomanage vos clés ASA.</span><span class="sxs-lookup"><span data-stu-id="023a1-130">Only allow Key Vault toomanage your ASA keys.</span></span> <span data-ttu-id="023a1-131">N’essayez pas de toomanage les vous-même, vous n’interférera avec les processus du coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="023a1-131">Do not attempt toomanage them yourself, you will interfere with Key Vault's processes.</span></span> 
- <span data-ttu-id="023a1-132">N’autorisez pas ASA toobe de clés géré par plusieurs objets de coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="023a1-132">Do not allow ASA keys toobe managed by more than one Key Vault object.</span></span> 
- <span data-ttu-id="023a1-133">Si vous avez besoin toomanually régénérer vos clés ASA, nous vous recommandons de les régénérer via le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="023a1-133">If you need toomanually regenerate your ASA keys, we recommend that you regenerate them via Key Vault.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="023a1-134">Prise en main</span><span class="sxs-lookup"><span data-stu-id="023a1-134">Getting started</span></span>

### <a name="setup-for-role-based-access-control-rbac-permissions"></a><span data-ttu-id="023a1-135">Configuration des autorisations de contrôle d’accès en fonction des permissions (RBAC)</span><span class="sxs-lookup"><span data-stu-id="023a1-135">Setup for role-based access control (RBAC) permissions</span></span>

<span data-ttu-id="023a1-136">Le coffre de clés a besoin d’autorisations trop*liste* et *régénérer* clés pour un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="023a1-136">Key Vault needs permissions too*list* and *regenerate* keys for a storage account.</span></span> <span data-ttu-id="023a1-137">Vous pouvez configurer ces autorisations à l’aide de hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="023a1-137">Set up these permissions using hello following steps:</span></span>

- <span data-ttu-id="023a1-138">Récupérez la valeur ObjectId de Key Vault :</span><span class="sxs-lookup"><span data-stu-id="023a1-138">Get ObjectId of Key Vault:</span></span> 

    `Get-AzureRmADServicePrincipal -SearchString "AzureKeyVault"`

- <span data-ttu-id="023a1-139">Affecter tooAzure du rôle opérateur de clé de stockage identité de coffre de clé :</span><span class="sxs-lookup"><span data-stu-id="023a1-139">Assign Storage Key Operator role tooAzure Key Vault Identity:</span></span> 

    `New-AzureRmRoleAssignment -ObjectId <objectId of AzureKeyVault from previous command> -RoleDefinitionName 'Storage Account Key Operator Service Role' -Scope '<azure resource id of storage account>'`

    >[!NOTE]
    > <span data-ttu-id="023a1-140">Pour un type de compte classique, définir un paramètre de rôle hello trop*« Classique stockage compte clé Service de rôle d’opérateur »*.</span><span class="sxs-lookup"><span data-stu-id="023a1-140">For a classic account type, set hello role parameter too*"Classic Storage Account Key Operator Service Role"*.</span></span>

### <a name="storage-account-onboarding"></a><span data-ttu-id="023a1-141">Intégration des comptes de stockage</span><span class="sxs-lookup"><span data-stu-id="023a1-141">Storage account onboarding</span></span> 

<span data-ttu-id="023a1-142">Exemple : En tant que propriétaire d’un objet de coffre de clés vous ajoutez un stockage compte objet tooyour Azure Key Vault tooonboard un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="023a1-142">Example: As a Key Vault object owner you add a storage account object tooyour Azure Key Vault tooonboard a storage account.</span></span>

<span data-ttu-id="023a1-143">Lors de l’intégration, le coffre de clés doit tooverify qu’identité hello du compte de l’intégration de hello dispose des autorisations trop*liste* et trop*régénérer* clés de stockage.</span><span class="sxs-lookup"><span data-stu-id="023a1-143">During onboarding, Key Vault needs tooverify that hello identity of hello onboarding account has permissions too*list* and too*regenerate* storage keys.</span></span> <span data-ttu-id="023a1-144">Dans commande tooverify ces autorisations, le coffre de clés Obtient un OBO (à la place de) jeton à partir du service d’authentification hello, audience tooAzure Gestionnaire de ressources et rend un *liste* service de stockage Azure toohello appel de clé.</span><span class="sxs-lookup"><span data-stu-id="023a1-144">In order tooverify these permissions, Key Vault gets an OBO (On Behalf Of) token from hello authentication service, audience set tooAzure Resource Manager, and makes a *list* key call toohello Azure Storage service.</span></span> <span data-ttu-id="023a1-145">Si hello *liste* appel échoue, hello de création de l’objet échoue avec un code d’état HTTP de coffre de clés *interdit*.</span><span class="sxs-lookup"><span data-stu-id="023a1-145">If hello *list* call fails, hello Key Vault object creation fails with a HTTP status code of *Forbidden*.</span></span> <span data-ttu-id="023a1-146">les clés de Hello répertoriées de cette manière sont mis en cache avec le stockage de votre entité de coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="023a1-146">hello keys listed in this fashion are cached with your key vault entity storage.</span></span> 

<span data-ttu-id="023a1-147">Le coffre de clés doit vérifier que les identités hello a *régénérer* autorisations avant de prendre possession de régénérer vos clés.</span><span class="sxs-lookup"><span data-stu-id="023a1-147">Key Vault must verify that hello identity has *regenerate* permissions before it can take ownership of regenerating your keys.</span></span> <span data-ttu-id="023a1-148">tooverify hello identité, via le jeton OBO, ainsi que hello première identité de tiers le coffre de clés dispose de ces autorisations :</span><span class="sxs-lookup"><span data-stu-id="023a1-148">tooverify that hello identity, via OBO token, as well as hello Key Vault first party identity has these permissions:</span></span>

- <span data-ttu-id="023a1-149">Le coffre de clés répertorie les autorisations de RBAC sur la ressource de compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="023a1-149">Key Vault lists RBAC permissions on hello storage account resource.</span></span>
- <span data-ttu-id="023a1-150">Le coffre de clés valide réponse hello via des actions et les actions non correspondance d’expression régulière.</span><span class="sxs-lookup"><span data-stu-id="023a1-150">Key Vault validates hello response via regular expression matching of actions and non-actions.</span></span> 

<span data-ttu-id="023a1-151">Recherchez des exemples de prise en charge dans la section relative aux [exemples de clés de comptes de stockage gérés de Key Vault](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167).</span><span class="sxs-lookup"><span data-stu-id="023a1-151">Find some supporting examples at [Key Vault - Managed Storage Account Keys Samples](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167).</span></span>

<span data-ttu-id="023a1-152">Si l’identité de hello n’est pas *régénérer* autorisations ou si la première identité de tiers du coffre de clés n’a pas *liste* ou *régénérer* autorisation, puis l’intégration de hello demande échouera et retournera un code d’erreur approprié et un message.</span><span class="sxs-lookup"><span data-stu-id="023a1-152">If hello identity does not have *regenerate* permissions or if Key Vault's first party identity doesn’t have *list* or *regenerate* permission, then hello onboarding request fails returning an appropriate error code and message.</span></span> 

<span data-ttu-id="023a1-153">jeton OBO Hello fonctionne uniquement lorsque vous utilisez internes, les applications clientes natives de PowerShell ou CLI.</span><span class="sxs-lookup"><span data-stu-id="023a1-153">hello OBO token will only work when you use first-party, native client applications of either PowerShell or CLI.</span></span>

## <a name="other-applications"></a><span data-ttu-id="023a1-154">Autres applications</span><span class="sxs-lookup"><span data-stu-id="023a1-154">Other applications</span></span>

- <span data-ttu-id="023a1-155">Jetons SAP, construits à l’aide de clés de compte de stockage de coffre de clés, fournissent davantage un accès contrôlé tooan compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="023a1-155">SAS tokens, constructed using Key Vault storage account keys, provide even more controlled access tooan Azure storage account.</span></span> <span data-ttu-id="023a1-156">Pour plus d’informations, consultez [Utilisation des signatures d’accès partagé](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).</span><span class="sxs-lookup"><span data-stu-id="023a1-156">For more information, see [Using shared access signatures](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).</span></span>

## <a name="see-also"></a><span data-ttu-id="023a1-157">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="023a1-157">See also</span></span>

- [<span data-ttu-id="023a1-158">Présentation des clés, des secrets et des certificats</span><span class="sxs-lookup"><span data-stu-id="023a1-158">About keys, secrets, and certificates</span></span>](https://docs.microsoft.com/rest/api/keyvault/)
- [<span data-ttu-id="023a1-159">Blog de l’équipe Key Vault</span><span class="sxs-lookup"><span data-stu-id="023a1-159">Key Vault Team Blog</span></span>](https://blogs.technet.microsoft.com/kv/)
