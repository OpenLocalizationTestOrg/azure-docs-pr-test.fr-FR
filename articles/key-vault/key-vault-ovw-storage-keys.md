---
ms.assetid: 
title: "Clés de compte de stockage Azure Key Vault"
description: "Les clés de compte de stockage assurent une intégration transparente entre Azure Key Vault et l’accès au compte de stockage Azure basé sur les clés."
ms.topic: article
services: key-vault
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/25/2017
ms.openlocfilehash: 3148088c88236c64e089fd25c98eb8ac7cdcbfea
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-key-vault-storage-account-keys"></a><span data-ttu-id="c99c5-103">Clés de compte de stockage Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="c99c5-103">Azure Key Vault Storage Account Keys</span></span>

<span data-ttu-id="c99c5-104">Avant l’apparition des clés de compte de stockage Azure Key Vault, les développeurs devaient gérer leurs propres clés de compte de stockage Azure (ASA) et les faire tourner manuellement ou par le biais d’une automatisation externe.</span><span class="sxs-lookup"><span data-stu-id="c99c5-104">Before Azure Key Vault Storage Account Keys, developers had to manage their own Azure Storage Account (ASA) keys and rotate them manually or through an external automation.</span></span> <span data-ttu-id="c99c5-105">À présent, les clés de compte de stockage Key Vault sont implémentées sous forme de [secrets Key Vault](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) pour l’authentification avec un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="c99c5-105">Now, Key Vault Storage Account Keys are implemented as [Key Vault secrets](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) for authenticating with an Azure Storage Account.</span></span> 

<span data-ttu-id="c99c5-106">La fonctionnalité de clé ASA gère le roulement des secrets à votre place et vous évite d’avoir à établir un contact direct avec une clé ASA en proposant les signatures d’accès partagé (SAP) sous forme de méthode.</span><span class="sxs-lookup"><span data-stu-id="c99c5-106">The ASA key feature manages secret rotation for you and removes the need for your direct contact with an ASA key by offering Shared Access Signatures (SAS) as a method.</span></span> 

<span data-ttu-id="c99c5-107">Pour plus d’informations générales sur les comptes de stockage Azure, consultez la page [À propos des comptes de stockage Azure](https://docs.microsoft.com/azure/storage/storage-create-storage-account).</span><span class="sxs-lookup"><span data-stu-id="c99c5-107">For more general information on Azure Storage Accounts, see [About Azure storage accounts](https://docs.microsoft.com/azure/storage/storage-create-storage-account).</span></span>

## <a name="supporting-interfaces"></a><span data-ttu-id="c99c5-108">Prise en charge des interfaces</span><span class="sxs-lookup"><span data-stu-id="c99c5-108">Supporting interfaces</span></span>

<span data-ttu-id="c99c5-109">La fonctionnalité de clés de compte de stockage Azure est pour le moment disponible sur les interfaces REST, .NET/C# et PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c99c5-109">The Azure Storage Account keys feature is initially available through the REST, .NET/C# and PowerShell interfaces.</span></span> <span data-ttu-id="c99c5-110">Pour plus d’informations, consultez la page [Informations de référence Key Vault](https://docs.microsoft.com/azure/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="c99c5-110">For more information, see [Key Vault Reference](https://docs.microsoft.com/azure/key-vault/).</span></span>


## <a name="storage-account-keys-behavior"></a><span data-ttu-id="c99c5-111">Comportement des clés de compte de stockage</span><span class="sxs-lookup"><span data-stu-id="c99c5-111">Storage account keys behavior</span></span>

### <a name="what-key-vault-manages"></a><span data-ttu-id="c99c5-112">Ce que gère Key Vault</span><span class="sxs-lookup"><span data-stu-id="c99c5-112">What Key Vault manages</span></span>

<span data-ttu-id="c99c5-113">Key Vault exécute plusieurs fonctions de gestion interne à votre place lorsque vous utilisez des clés de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="c99c5-113">Key Vault performs several internal management functions on your behalf when you use Storage Account Keys.</span></span>

1. <span data-ttu-id="c99c5-114">Azure Key Vault gère les clés d’un compte de stockage Azure (ASA).</span><span class="sxs-lookup"><span data-stu-id="c99c5-114">Azure Key Vault manages keys of an Azure Storage Account (ASA).</span></span> 
    - <span data-ttu-id="c99c5-115">En interne, Azure Key Vault peut lister (synchroniser) les clés avec un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="c99c5-115">Internally, Azure Key Vault can list (sync) keys with an Azure Storage Account.</span></span>  
    - <span data-ttu-id="c99c5-116">Azure Key Vault régénère (fait tourner) les clés régulièrement.</span><span class="sxs-lookup"><span data-stu-id="c99c5-116">Azure Key Vault regenerates (rotates) the keys periodically.</span></span> 
    - <span data-ttu-id="c99c5-117">Les valeurs de clés ne sont jamais retournées en réponse à l’appelant.</span><span class="sxs-lookup"><span data-stu-id="c99c5-117">Key values are never returned in response to caller.</span></span> 
    - <span data-ttu-id="c99c5-118">Azure Key Vault gère les clés des comptes de stockage ainsi que des comptes de stockage Classic.</span><span class="sxs-lookup"><span data-stu-id="c99c5-118">Azure Key Vault manages keys of both Storage Accounts and Classic Storage Accounts.</span></span> 
2. <span data-ttu-id="c99c5-119">Azure Key Vault permet au propriétaire du coffre / de l’objet (vous) de créer des définitions de SAP (de compte ou de service).</span><span class="sxs-lookup"><span data-stu-id="c99c5-119">Azure Key Vault allows you, the vault/object owner, to create SAS (account or service SAS) definitions.</span></span> 
    - <span data-ttu-id="c99c5-120">La valeur de la SAP, créée à l’aide de sa définition, est retournée sous forme de secret par le biais du chemin d’accès de l’URI REST.</span><span class="sxs-lookup"><span data-stu-id="c99c5-120">The SAS value, created using SAS definition, is returned as a secret via the REST URI path.</span></span> <span data-ttu-id="c99c5-121">Pour plus d’informations, consultez la page [Opérations du compte de stockage Azure Key Vault](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations).</span><span class="sxs-lookup"><span data-stu-id="c99c5-121">For more information, see [Azure Key Vault storage account operations](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations).</span></span>

### <a name="naming-guidance"></a><span data-ttu-id="c99c5-122">Aide pour l’affectation de noms</span><span class="sxs-lookup"><span data-stu-id="c99c5-122">Naming guidance</span></span>

<span data-ttu-id="c99c5-123">Les noms des comptes de stockage doivent comporter entre 3 et 24 caractères, uniquement des lettres minuscules et des chiffres.</span><span class="sxs-lookup"><span data-stu-id="c99c5-123">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span>  
 
<span data-ttu-id="c99c5-124">Un nom de définition de SAP doit avoir une longueur comprise entre 1 et 102 caractères, composés uniquement de 0-9, a-z et A-Z.</span><span class="sxs-lookup"><span data-stu-id="c99c5-124">A SAS definition name must be 1-102 characters in length containing only 0-9, a-z, A-Z.</span></span>

## <a name="developer-experience"></a><span data-ttu-id="c99c5-125">Expérience de développement</span><span class="sxs-lookup"><span data-stu-id="c99c5-125">Developer experience</span></span> 

### <a name="before-azure-key-vault-storage-keys"></a><span data-ttu-id="c99c5-126">Avant l’apparition des clés de stockage Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="c99c5-126">Before Azure Key Vault Storage Keys</span></span> 

<span data-ttu-id="c99c5-127">Les développeurs avaient besoin d’appliquer les pratiques suivantes avec une clé de compte de stockage pour obtenir un accès au stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="c99c5-127">Developers used to need to do the following practices with a storage account key to get access to Azure storage.</span></span> 
 
 ```
//create storage account using connection string containing account name 
// and the storage key 

var storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));
var blobClient = storageAccount.CreateCloudBlobClient();
 ```
 
### <a name="after-azure-key-vault-storage-keys"></a><span data-ttu-id="c99c5-128">Après l’apparition des clés de stockage Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="c99c5-128">After Azure Key Vault Storage Keys</span></span> 

```
//Please make sure to set storage permissions appropriately on your key vault
Set-AzureRmKeyVaultAccessPolicy -VaultName 'yourVault' -ObjectId yourObjectId -PermissionsToStorage all

//Use PowerShell command to get Secret URI 

Set-AzureKeyVaultManagedStorageSasDefinition -Service Blob -ResourceType Container,Service -VaultName yourKV  
-AccountName msak01 -Name blobsas1 -Protocol HttpsOnly -ValidityPeriod ([System.Timespan]::FromDays(1)) -Permission Read,List

//Get SAS token from Key Vault

var secret = await kv.GetSecretAsync("SecretUri");

// Create new storage credentials using the SAS token. 

var accountSasCredential = new StorageCredentials(secret.Value); 

// Use credentials and the Blob storage endpoint to create a new Blob service client. 

var accountWithSas = new CloudStorageAccount(accountSasCredential, new Uri ("https://myaccount.blob.core.windows.net/"), null, null, null); 

var blobClientWithSas = accountWithSas.CreateCloudBlobClient(); 
 
// If SAS token is about to expire then Get sasToken again from Key Vault and update it.

accountSasCredential.UpdateSASToken(sasToken);

  ```
 
 ### <a name="developer-best-practices"></a><span data-ttu-id="c99c5-129">Meilleures pratiques de développement</span><span class="sxs-lookup"><span data-stu-id="c99c5-129">Developer best practices</span></span> 

- <span data-ttu-id="c99c5-130">Autorisez uniquement Key Vault à gérer vos clés ASA.</span><span class="sxs-lookup"><span data-stu-id="c99c5-130">Only allow Key Vault to manage your ASA keys.</span></span> <span data-ttu-id="c99c5-131">N’essayez pas de les gérer vous-même, vous interféreriez avec les processus de Key Vault.</span><span class="sxs-lookup"><span data-stu-id="c99c5-131">Do not attempt to manage them yourself, you will interfere with Key Vault's processes.</span></span> 
- <span data-ttu-id="c99c5-132">Ne permettez pas que les clés ASA soient gérées par plusieurs objets Key Vault.</span><span class="sxs-lookup"><span data-stu-id="c99c5-132">Do not allow ASA keys to be managed by more than one Key Vault object.</span></span> 
- <span data-ttu-id="c99c5-133">Si vous devez régénérer manuellement vos clés ASA, nous vous recommandons de le faire avec Key Vault.</span><span class="sxs-lookup"><span data-stu-id="c99c5-133">If you need to manually regenerate your ASA keys, we recommend that you regenerate them via Key Vault.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="c99c5-134">Prise en main</span><span class="sxs-lookup"><span data-stu-id="c99c5-134">Getting started</span></span>

### <a name="setup-for-role-based-access-control-rbac-permissions"></a><span data-ttu-id="c99c5-135">Configuration des autorisations de contrôle d’accès en fonction des permissions (RBAC)</span><span class="sxs-lookup"><span data-stu-id="c99c5-135">Setup for role-based access control (RBAC) permissions</span></span>

<span data-ttu-id="c99c5-136">Key Vault a besoin d’autorisations pour *répertorier* et *régénérer* les clés d’un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="c99c5-136">Key Vault needs permissions to *list* and *regenerate* keys for a storage account.</span></span> <span data-ttu-id="c99c5-137">Configurez-les en suivant les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c99c5-137">Set up these permissions using the following steps:</span></span>

- <span data-ttu-id="c99c5-138">Récupérez la valeur ObjectId de Key Vault :</span><span class="sxs-lookup"><span data-stu-id="c99c5-138">Get ObjectId of Key Vault:</span></span> 

    `Get-AzureRmADServicePrincipal -SearchString "AzureKeyVault"`

- <span data-ttu-id="c99c5-139">Attribuez le rôle d’opérateur de clés de stockage à l’identité Azure Key Vault :</span><span class="sxs-lookup"><span data-stu-id="c99c5-139">Assign Storage Key Operator role to Azure Key Vault Identity:</span></span> 

    `New-AzureRmRoleAssignment -ObjectId <objectId of AzureKeyVault from previous command> -RoleDefinitionName 'Storage Account Key Operator Service Role' -Scope '<azure resource id of storage account>'`

    >[!NOTE]
    > <span data-ttu-id="c99c5-140">Pour un type de compte classique, réglez le paramètre de rôle sur *« Rôle de service d’opérateur de clés du compte de stockage Classic »*.</span><span class="sxs-lookup"><span data-stu-id="c99c5-140">For a classic account type, set the role parameter to *"Classic Storage Account Key Operator Service Role"*.</span></span>

### <a name="storage-account-onboarding"></a><span data-ttu-id="c99c5-141">Intégration des comptes de stockage</span><span class="sxs-lookup"><span data-stu-id="c99c5-141">Storage account onboarding</span></span> 

<span data-ttu-id="c99c5-142">Exemple : en tant que propriétaire d’un objet Key Vault, vous ajoutez un objet de compte de stockage à votre coffre Azure Key Vault pour intégrer un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="c99c5-142">Example: As a Key Vault object owner you add a storage account object to your Azure Key Vault to onboard a storage account.</span></span>

<span data-ttu-id="c99c5-143">Lors de l’intégration, Key Vault doit vérifier que l’identité du compte en cours d’intégration dispose des autorisations adéquates pour *répertorier* et *régénérer* les clés de stockage.</span><span class="sxs-lookup"><span data-stu-id="c99c5-143">During onboarding, Key Vault needs to verify that the identity of the onboarding account has permissions to *list* and to *regenerate* storage keys.</span></span> <span data-ttu-id="c99c5-144">Pour vérifier ces autorisations, Key Vault obtient un jeton OBO (On Behalf Of) de la part du service d’authentification, audience définie pour le gestionnaire de ressources Azure, et effectue un appel de la *liste* clé auprès du service de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="c99c5-144">In order to verify these permissions, Key Vault gets an OBO (On Behalf Of) token from the authentication service, audience set to Azure Resource Manager, and makes a *list* key call to the Azure Storage service.</span></span> <span data-ttu-id="c99c5-145">Si l’appel de la *liste* échoue, la création de l’objet Key Vault échoue avec le code d’état HTTP *Interdit*.</span><span class="sxs-lookup"><span data-stu-id="c99c5-145">If the *list* call fails, the Key Vault object creation fails with a HTTP status code of *Forbidden*.</span></span> <span data-ttu-id="c99c5-146">Les clés listées de cette manière sont mises en cache avec le stockage de votre entité de coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="c99c5-146">The keys listed in this fashion are cached with your key vault entity storage.</span></span> 

<span data-ttu-id="c99c5-147">Key Vault doit vérifier que l’identité a l’autorisation de *régénérer* pour pouvoir prendre possession de la régénération des clés.</span><span class="sxs-lookup"><span data-stu-id="c99c5-147">Key Vault must verify that the identity has *regenerate* permissions before it can take ownership of regenerating your keys.</span></span> <span data-ttu-id="c99c5-148">Pour vérifier que l’identité, par le biais du jeton OBO, ainsi que l’identité interne Key Vault disposent de ces autorisations :</span><span class="sxs-lookup"><span data-stu-id="c99c5-148">To verify that the identity, via OBO token, as well as the Key Vault first party identity has these permissions:</span></span>

- <span data-ttu-id="c99c5-149">Key Vault liste les autorisations de contrôle d’accès en fonction du rôle sur la ressource du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="c99c5-149">Key Vault lists RBAC permissions on the storage account resource.</span></span>
- <span data-ttu-id="c99c5-150">Key Vault valide la réponse par le rapprochement d’actions et d’inactions avec des expressions régulières.</span><span class="sxs-lookup"><span data-stu-id="c99c5-150">Key Vault validates the response via regular expression matching of actions and non-actions.</span></span> 

<span data-ttu-id="c99c5-151">Recherchez des exemples de prise en charge dans la section relative aux [exemples de clés de comptes de stockage gérés de Key Vault](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167).</span><span class="sxs-lookup"><span data-stu-id="c99c5-151">Find some supporting examples at [Key Vault - Managed Storage Account Keys Samples](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167).</span></span>

<span data-ttu-id="c99c5-152">Si l’identité n’a pas d’autorisation de *régénération* ou que l’identité interne de Key Vault n’a pas l’autorisation de *répertorier* ou de *régénérer* des éléments, la demande d’intégration échoue en renvoyant un message et un code d’erreur appropriés.</span><span class="sxs-lookup"><span data-stu-id="c99c5-152">If the identity does not have *regenerate* permissions or if Key Vault's first party identity doesn’t have *list* or *regenerate* permission, then the onboarding request fails returning an appropriate error code and message.</span></span> 

<span data-ttu-id="c99c5-153">Le jeton OBO ne fonctionne que si l’on utilise des applications clientes natives internes de PowerShell ou CLI.</span><span class="sxs-lookup"><span data-stu-id="c99c5-153">The OBO token will only work when you use first-party, native client applications of either PowerShell or CLI.</span></span>

## <a name="other-applications"></a><span data-ttu-id="c99c5-154">Autres applications</span><span class="sxs-lookup"><span data-stu-id="c99c5-154">Other applications</span></span>

- <span data-ttu-id="c99c5-155">Les jetons SAP, construits à l’aide de clés de compte de stockage Key Vault, assurent un accès encore plus contrôlé à un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="c99c5-155">SAS tokens, constructed using Key Vault storage account keys, provide even more controlled access to an Azure storage account.</span></span> <span data-ttu-id="c99c5-156">Pour plus d’informations, consultez la page [Utiliser des signatures d’accès partagé](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).</span><span class="sxs-lookup"><span data-stu-id="c99c5-156">For more information, see [Using shared access signatures](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).</span></span>

## <a name="see-also"></a><span data-ttu-id="c99c5-157">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="c99c5-157">See also</span></span>

- [<span data-ttu-id="c99c5-158">Présentation des clés, des secrets et des certificats</span><span class="sxs-lookup"><span data-stu-id="c99c5-158">About keys, secrets, and certificates</span></span>](https://docs.microsoft.com/rest/api/keyvault/)
- [<span data-ttu-id="c99c5-159">Blog de l’équipe Key Vault</span><span class="sxs-lookup"><span data-stu-id="c99c5-159">Key Vault Team Blog</span></span>](https://blogs.technet.microsoft.com/kv/)
