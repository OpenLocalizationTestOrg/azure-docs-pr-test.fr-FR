---
title: "Gestion des ressources de compte Batch avec la bibliothèque client pour .NET - Azure | Microsoft Docs"
description: "Créez, supprimez et modifiez des ressources de compte Azure Batch avec la bibliothèque Batch Management .NET."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 16279b23-60ff-4b16-b308-5de000e4c028
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/24/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: eafde9258222a2ab09ade2e366f9cc595a303dec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-batch-accounts-and-quotas-with-the-batch-management-client-library-for-net"></a><span data-ttu-id="e5b6f-103">Gérer les quotas et comptes Batch avec la bibliothèque cliente Batch Management pour .NET</span><span class="sxs-lookup"><span data-stu-id="e5b6f-103">Manage Batch accounts and quotas with the Batch Management client library for .NET</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e5b6f-104">portail Azure</span><span class="sxs-lookup"><span data-stu-id="e5b6f-104">Azure portal</span></span>](batch-account-create-portal.md)
> * [<span data-ttu-id="e5b6f-105">Gestion de lots .NET</span><span class="sxs-lookup"><span data-stu-id="e5b6f-105">Batch Management .NET</span></span>](batch-management-dotnet.md)
> 
> 

<span data-ttu-id="e5b6f-106">Vous pouvez réduire la surcharge de maintenance dans vos applications Azure Batch avec la bibliothèque [Batch Management .NET][api_mgmt_net] en automatisant la création et la suppression de comptes Batch, la gestion des clés et la détection des quotas.</span><span class="sxs-lookup"><span data-stu-id="e5b6f-106">You can lower maintenance overhead in your Azure Batch applications by using the [Batch Management .NET][api_mgmt_net] library to automate Batch account creation, deletion, key management, and quota discovery.</span></span>

* <span data-ttu-id="e5b6f-107">**Créez et supprimez des comptes Batch** dans n'importe quelle région.</span><span class="sxs-lookup"><span data-stu-id="e5b6f-107">**Create and delete Batch accounts** within any region.</span></span> <span data-ttu-id="e5b6f-108">Si, par exemple, en tant qu'éditeur de logiciels indépendant (ISV) vous fournissez un service à vos clients dans lequel un compte Batch distinct est affecté à chacun à des fins de facturation, vous pouvez ajouter des fonctionnalités de création et de suppression de comptes à votre portail client.</span><span class="sxs-lookup"><span data-stu-id="e5b6f-108">If, as an independent software vendor (ISV) for example, you provide a service for your clients in which each is assigned a separate Batch account for billing purposes, you can add account creation and deletion capabilities to your customer portal.</span></span>
* <span data-ttu-id="e5b6f-109">**Récupérez et régénérez des clés de compte** par programme pour tous vos comptes Batch.</span><span class="sxs-lookup"><span data-stu-id="e5b6f-109">**Retrieve and regenerate account keys** programmatically for any of your Batch accounts.</span></span> <span data-ttu-id="e5b6f-110">Cela est pratique pour maintenir la conformité aux stratégies de sécurité appliquant une substitution ou une expiration périodique des clés de compte.</span><span class="sxs-lookup"><span data-stu-id="e5b6f-110">This can help you comply with security policies that enforce periodic rollover or expiry of account keys.</span></span> <span data-ttu-id="e5b6f-111">Lorsque vous avez plusieurs comptes Batch dans différentes régions Azure, l’automatisation de ce processus de substitution augmente l’efficacité de votre solution.</span><span class="sxs-lookup"><span data-stu-id="e5b6f-111">When you have several Batch accounts in various Azure regions, automation of this rollover process increases your solution's efficiency.</span></span>
* <span data-ttu-id="e5b6f-112">**Vérifiez les quotas des comptes** et déterminez quels comptes Batch possèdent quelles limites sans avoir à tâtonner.</span><span class="sxs-lookup"><span data-stu-id="e5b6f-112">**Check account quotas** and take the trial-and-error guesswork out of determining which Batch accounts have what limits.</span></span> <span data-ttu-id="e5b6f-113">En vérifiant les quotas de vos comptes avant de commencer les travaux, de créer des pools ou d’ajouter des nœuds de calcul, vous pouvez ajuster de façon proactive l’endroit et le moment où ces ressources de calcul sont créées.</span><span class="sxs-lookup"><span data-stu-id="e5b6f-113">By checking your account quotas before starting jobs, creating pools, or adding compute nodes, you can proactively adjust where or when these compute resources are created.</span></span> <span data-ttu-id="e5b6f-114">Vous pouvez déterminer quels comptes requièrent des augmentations de quota avant d’allouer des ressources supplémentaires à ces comptes.</span><span class="sxs-lookup"><span data-stu-id="e5b6f-114">You can determine which accounts require quota increases before allocating additional resources in those accounts.</span></span>
* <span data-ttu-id="e5b6f-115">**Combinez les fonctionnalités d’autres services Azure** pour une expérience de gestion complète en utilisant conjointement Batch Management .NET, [Azure Active Directory][aad_about] et [Azure Resource Manager][resman_overview] dans la même application.</span><span class="sxs-lookup"><span data-stu-id="e5b6f-115">**Combine features of other Azure services** for a full-featured management experience--by using Batch Management .NET, [Azure Active Directory][aad_about], and the [Azure Resource Manager][resman_overview] together in the same application.</span></span> <span data-ttu-id="e5b6f-116">En utilisant ces fonctionnalités et leurs API, vous pouvez fournir une expérience d’authentification transparente, une fonction de création et de suppression des groupes de ressources ainsi que les fonctionnalités décrites ci-dessus, pour une solution de gestion de bout en bout.</span><span class="sxs-lookup"><span data-stu-id="e5b6f-116">By using these features and their APIs, you can provide a frictionless authentication experience, the ability to create and delete resource groups, and the capabilities that are described above for an end-to-end management solution.</span></span>

> [!NOTE]
> <span data-ttu-id="e5b6f-117">Si cet article se concentre sur la gestion par programme de vos comptes, clés et quotas Batch, vous pouvez effectuer la plupart de ces activités avec le [Portail Azure][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="e5b6f-117">While this article focuses on the programmatic management of your Batch accounts, keys, and quotas, you can perform many of these activities by using the [Azure portal][azure_portal].</span></span> <span data-ttu-id="e5b6f-118">Pour plus d’informations, consultez [Création d’un compte Azure Batch à l’aide du portail Azure](batch-account-create-portal.md) et [Quotas et limites pour le service Azure Batch](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="e5b6f-118">For more information, see [Create an Azure Batch account using the Azure portal](batch-account-create-portal.md) and [Quotas and limits for the Azure Batch service](batch-quota-limit.md).</span></span>
> 
> 

## <a name="create-and-delete-batch-accounts"></a><span data-ttu-id="e5b6f-119">Créez et supprimez des comptes Batch</span><span class="sxs-lookup"><span data-stu-id="e5b6f-119">Create and delete Batch accounts</span></span>
<span data-ttu-id="e5b6f-120">Comme mentionné ci-dessus, l’une des principales fonctionnalités de l’API Batch Management consiste à créer et à supprimer des comptes Batch dans une région Azure.</span><span class="sxs-lookup"><span data-stu-id="e5b6f-120">As mentioned, one of the primary features of the Batch Management API is to create and delete Batch accounts in an Azure region.</span></span> <span data-ttu-id="e5b6f-121">Pour ce faire, utilisez [BatchManagementClient.Account.CreateAsync][net_create] et [DeleteAsync][net_delete], ou leurs équivalents synchrones.</span><span class="sxs-lookup"><span data-stu-id="e5b6f-121">To do so, use [BatchManagementClient.Account.CreateAsync][net_create] and [DeleteAsync][net_delete], or their synchronous counterparts.</span></span>

<span data-ttu-id="e5b6f-122">L’extrait de code suivant crée un compte, récupère le compte créé à partir du service Batch, puis le supprime.</span><span class="sxs-lookup"><span data-stu-id="e5b6f-122">The following code snippet creates an account, obtains the newly created account from the Batch service, and then deletes it.</span></span> <span data-ttu-id="e5b6f-123">Dans cet extrait de code et les autres extraits de cet article, `batchManagementClient` est une instance entièrement initialisée de [BatchManagementClient][net_mgmt_client].</span><span class="sxs-lookup"><span data-stu-id="e5b6f-123">In this snippet and the others in this article, `batchManagementClient` is a fully initialized instance of [BatchManagementClient][net_mgmt_client].</span></span>

```csharp
// Create a new Batch account
await batchManagementClient.Account.CreateAsync("MyResourceGroup",
    "mynewaccount",
    new BatchAccountCreateParameters() { Location = "West US" });

// Get the new account from the Batch service
AccountResource account = await batchManagementClient.Account.GetAsync(
    "MyResourceGroup",
    "mynewaccount");

// Delete the account
await batchManagementClient.Account.DeleteAsync("MyResourceGroup", account.Name);
```

> [!NOTE]
> <span data-ttu-id="e5b6f-124">Les applications qui utilisent la bibliothèque Batch Management .NET et sa classe BatchManagementClient nécessitent un accès **administrateur de services fédérés** ou **coadministrateur** à l’abonnement qui possède le compte Batch à gérer.</span><span class="sxs-lookup"><span data-stu-id="e5b6f-124">Applications that use the Batch Management .NET library and its BatchManagementClient class require **service administrator** or **coadministrator** access to the subscription that owns the Batch account to be managed.</span></span> <span data-ttu-id="e5b6f-125">Pour plus d’informations, consultez la section [Azure Active Directory](#azure-active-directory) et l’exemple de code [AccountManagement][acct_mgmt_sample].</span><span class="sxs-lookup"><span data-stu-id="e5b6f-125">For more information, see the [Azure Active Directory](#azure-active-directory) section and the [AccountManagement][acct_mgmt_sample] code sample.</span></span>
> 
> 

## <a name="retrieve-and-regenerate-account-keys"></a><span data-ttu-id="e5b6f-126">Récupérez et régénérez des clés de compte</span><span class="sxs-lookup"><span data-stu-id="e5b6f-126">Retrieve and regenerate account keys</span></span>
<span data-ttu-id="e5b6f-127">Récupérez les clés primaires et secondaires de n’importe quel compte Batch de votre abonnement avec [ListKeysAsync][net_list_keys].</span><span class="sxs-lookup"><span data-stu-id="e5b6f-127">Obtain primary and secondary account keys from any Batch account within your subscription by using [ListKeysAsync][net_list_keys].</span></span> <span data-ttu-id="e5b6f-128">Vous pouvez régénérer ces clés à l’aide de [RegenerateKeyAsync][net_regenerate_keys].</span><span class="sxs-lookup"><span data-stu-id="e5b6f-128">You can regenerate those keys by using [RegenerateKeyAsync][net_regenerate_keys].</span></span>

```csharp
// Get and print the primary and secondary keys
BatchAccountListKeyResult accountKeys =
    await batchManagementClient.Account.ListKeysAsync(
        "MyResourceGroup",
        "mybatchaccount");
Console.WriteLine("Primary key:   {0}", accountKeys.Primary);
Console.WriteLine("Secondary key: {0}", accountKeys.Secondary);

// Regenerate the primary key
BatchAccountRegenerateKeyResponse newKeys =
    await batchManagementClient.Account.RegenerateKeyAsync(
        "MyResourceGroup",
        "mybatchaccount",
        new BatchAccountRegenerateKeyParameters() {
            KeyName = AccountKeyType.Primary
            });
```

> [!TIP]
> <span data-ttu-id="e5b6f-129">Vous pouvez créer un flux de travail de connexion rationalisé pour vos applications de gestion.</span><span class="sxs-lookup"><span data-stu-id="e5b6f-129">You can create a streamlined connection workflow for your management applications.</span></span> <span data-ttu-id="e5b6f-130">Commencez par récupérer une clé du compte Batch que vous souhaitez gérer avec [ListKeysAsync][net_list_keys].</span><span class="sxs-lookup"><span data-stu-id="e5b6f-130">First, obtain an account key for the Batch account you wish to manage with [ListKeysAsync][net_list_keys].</span></span> <span data-ttu-id="e5b6f-131">Utilisez ensuite cette clé lors de l’initialisation de la classe [BatchSharedKeyCredentials][net_sharedkeycred] de la bibliothèque Batch .NET, qui est utilisée lors de l’initialisation de [BatchClient][net_batch_client].</span><span class="sxs-lookup"><span data-stu-id="e5b6f-131">Then, use this key when initializing the Batch .NET library's [BatchSharedKeyCredentials][net_sharedkeycred] class, which is used when initializing [BatchClient][net_batch_client].</span></span>
> 
> 

## <a name="check-azure-subscription-and-batch-account-quotas"></a><span data-ttu-id="e5b6f-132">Vérifier les quotas d'un abonnement Azure et d'un compte Batch</span><span class="sxs-lookup"><span data-stu-id="e5b6f-132">Check Azure subscription and Batch account quotas</span></span>
<span data-ttu-id="e5b6f-133">Les abonnements Azure et les services Azure, comme Batch, ont tous des quotas par défaut qui limitent le nombre de certaines entités.</span><span class="sxs-lookup"><span data-stu-id="e5b6f-133">Azure subscriptions and the individual Azure services like Batch all have default quotas that limit the number of certain entities within them.</span></span> <span data-ttu-id="e5b6f-134">Pour connaître les quotas par défaut des abonnements Azure, consultez [Abonnement Azure et limites, quotas et contraintes du service](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="e5b6f-134">For the default quotas for Azure subscriptions, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span> <span data-ttu-id="e5b6f-135">Pour obtenir les quotas par défaut du service Batch, consultez [Quotas et limites pour le service Azure Batch](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="e5b6f-135">For the default quotas of the Batch service, see [Quotas and limits for the Azure Batch service](batch-quota-limit.md).</span></span> <span data-ttu-id="e5b6f-136">La bibliothèque Batch Management .NET vous permet de vérifier ces quotas dans vos applications.</span><span class="sxs-lookup"><span data-stu-id="e5b6f-136">By using the Batch Management .NET library, you can check these quotas in your applications.</span></span> <span data-ttu-id="e5b6f-137">Vous pouvez ainsi plus facilement décider des allocations avant d’ajouter des comptes ou des ressources de calcul comme les pools et nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="e5b6f-137">This enables you to make allocation decisions before you add accounts or compute resources like pools and compute nodes.</span></span>

### <a name="check-an-azure-subscription-for-batch-account-quotas"></a><span data-ttu-id="e5b6f-138">Vérifier les quotas d'un compte Batch dans un abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="e5b6f-138">Check an Azure subscription for Batch account quotas</span></span>
<span data-ttu-id="e5b6f-139">Avant de créer un compte Batch dans une région, vous pouvez vérifier dans votre abonnement Azure que vous êtes en mesure d'ajouter un compte dans cette région.</span><span class="sxs-lookup"><span data-stu-id="e5b6f-139">Before creating a Batch account in a region, you can check your Azure subscription to see whether you are able to add an account in that region.</span></span>

<span data-ttu-id="e5b6f-140">Dans l’extrait de code ci-dessous, nous utilisons tout d’abord [BatchManagementClient.Account.ListAsync][net_mgmt_listaccounts] pour obtenir la liste de tous les comptes Batch d’un abonnement.</span><span class="sxs-lookup"><span data-stu-id="e5b6f-140">In the code snippet below, we first use [BatchManagementClient.Account.ListAsync][net_mgmt_listaccounts] to get a collection of all Batch accounts that are within a subscription.</span></span> <span data-ttu-id="e5b6f-141">Une fois que nous avons obtenu cette collection, nous pouvons déterminer le nombre de comptes qui se trouvent dans la région cible.</span><span class="sxs-lookup"><span data-stu-id="e5b6f-141">Once we've obtained this collection, we determine how many accounts are in the target region.</span></span> <span data-ttu-id="e5b6f-142">Nous utilisons ensuite [BatchManagementClient.Subscriptions][net_mgmt_subscriptions] pour obtenir le quota de comptes Batch et déterminer le nombre de comptes (le cas échéant) pouvant être créés dans cette région.</span><span class="sxs-lookup"><span data-stu-id="e5b6f-142">Then we use [BatchManagementClient.Subscriptions][net_mgmt_subscriptions] to obtain the Batch account quota and determine how many accounts (if any) can be created in that region.</span></span>

```csharp
// Get a collection of all Batch accounts within the subscription
BatchAccountListResponse listResponse =
        await batchManagementClient.Account.ListAsync(new AccountListParameters());
IList<AccountResource> accounts = listResponse.Accounts;
Console.WriteLine("Total number of Batch accounts under subscription id {0}:  {1}",
    creds.SubscriptionId,
    accounts.Count);

// Get a count of all accounts within the target region
string region = "westus";
int accountsInRegion = accounts.Count(o => o.Location == region);

// Get the account quota for the specified region
SubscriptionQuotasGetResponse quotaResponse = await batchManagementClient.Subscriptions.GetSubscriptionQuotasAsync(region);
Console.WriteLine("Account quota for {0} region: {1}", region, quotaResponse.AccountQuota);

// Determine how many accounts can be created in the target region
Console.WriteLine("Accounts in {0}: {1}", region, accountsInRegion);
Console.WriteLine("You can create {0} accounts in the {1} region.", quotaResponse.AccountQuota - accountsInRegion, region);
```

<span data-ttu-id="e5b6f-143">Dans l’extrait ci-dessus, `creds` est une instance de [TokenCloudCredentials][azure_tokencreds].</span><span class="sxs-lookup"><span data-stu-id="e5b6f-143">In the snippet above, `creds` is an instance of [TokenCloudCredentials][azure_tokencreds].</span></span> <span data-ttu-id="e5b6f-144">Pour voir un exemple de création de cet objet, consultez l’exemple de code [AccountManagement][acct_mgmt_sample] sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="e5b6f-144">To see an example of creating this object, see the [AccountManagement][acct_mgmt_sample] code sample on GitHub.</span></span>

### <a name="check-a-batch-account-for-compute-resource-quotas"></a><span data-ttu-id="e5b6f-145">Vérifier les quotas de ressources de calcul dans un compte Batch</span><span class="sxs-lookup"><span data-stu-id="e5b6f-145">Check a Batch account for compute resource quotas</span></span>
<span data-ttu-id="e5b6f-146">Avant d’augmenter les ressources de calcul dans votre solution Batch, vous pouvez vous assurer que les ressources que vous souhaitez allouer ne dépasseront pas les quotas de comptes.</span><span class="sxs-lookup"><span data-stu-id="e5b6f-146">Before increasing compute resources in your Batch solution, you can check to ensure the resources you want to allocate won't exceed the account's quotas.</span></span> <span data-ttu-id="e5b6f-147">Dans l’extrait de code ci-dessous, nous imprimons les informations de quota pour le compte Batch nommé `mybatchaccount`.</span><span class="sxs-lookup"><span data-stu-id="e5b6f-147">In the code snippet below, we print the quota information for the Batch account named `mybatchaccount`.</span></span> <span data-ttu-id="e5b6f-148">Dans votre application, vous pouvez utiliser ces informations pour déterminer si le compte peut ou non gérer les ressources supplémentaires à créer.</span><span class="sxs-lookup"><span data-stu-id="e5b6f-148">In your own application, you could use such information to determine whether the account can handle the additional resources to be created.</span></span>

```csharp
// First obtain the Batch account
BatchAccountGetResponse getResponse =
    await batchManagementClient.Account.GetAsync("MyResourceGroup", "mybatchaccount");
AccountResource account = getResponse.Resource;

// Now print the compute resource quotas for the account
Console.WriteLine("Core quota: {0}", account.Properties.CoreQuota);
Console.WriteLine("Pool quota: {0}", account.Properties.PoolQuota);
Console.WriteLine("Active job and job schedule quota: {0}", account.Properties.ActiveJobAndJobScheduleQuota);
```

> [!IMPORTANT]
> <span data-ttu-id="e5b6f-149">Bien qu’il y ait des quotas par défaut pour les abonnements et services Azure, la plupart de ces limites peuvent être relevées en émettant une demande dans le [Portail Azure][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="e5b6f-149">While there are default quotas for Azure subscriptions and services, many of these limits can be raised by issuing a request in the [Azure portal][azure_portal].</span></span> <span data-ttu-id="e5b6f-150">Par exemple, consultez [Quotas et limites du service Azure Batch](batch-quota-limit.md) pour obtenir des instructions sur l’augmentation des quotas de vos comptes Batch.</span><span class="sxs-lookup"><span data-stu-id="e5b6f-150">For example, see [Quotas and limits for the Azure Batch service](batch-quota-limit.md) for instructions on increasing your Batch account quotas.</span></span>
> 
> 

## <a name="use-azure-ad-with-batch-management-net"></a><span data-ttu-id="e5b6f-151">Utiliser Azure AD avec Batch Management .NET</span><span class="sxs-lookup"><span data-stu-id="e5b6f-151">Use Azure AD with Batch Management .NET</span></span>

<span data-ttu-id="e5b6f-152">La bibliothèque Batch Management .NET est un client de fournisseur de ressources Azure. Elle est utilisée avec [Azure Resource Manager][resman_overview] pour gérer les ressources de compte par programme.</span><span class="sxs-lookup"><span data-stu-id="e5b6f-152">The Batch Management .NET library is an Azure resource provider client, and is used together with [Azure Resource Manager][resman_overview] to manage account resources programmatically.</span></span> <span data-ttu-id="e5b6f-153">Azure AD est requis pour authentifier les demandes effectuées par le biais des clients de fournisseur de ressources Azure, y compris la bibliothèque Batch Management .NET et d’[Azure Resource Manager][resman_overview].</span><span class="sxs-lookup"><span data-stu-id="e5b6f-153">Azure AD is required to authenticate requests made through any Azure resource provider client, including the Batch Management .NET library, and through [Azure Resource Manager][resman_overview].</span></span> <span data-ttu-id="e5b6f-154">Pour plus d’informations sur l’utilisation d’Azure AD avec la bibliothèque Batch Management .NET, consultez [Utiliser Azure Active Directory pour authentifier des solutions Batch](batch-aad-auth.md).</span><span class="sxs-lookup"><span data-stu-id="e5b6f-154">For information about using Azure AD with the Batch Management .NET library, see [Use Azure Active Directory to authenticate Batch solutions](batch-aad-auth.md).</span></span> 

## <a name="sample-project-on-github"></a><span data-ttu-id="e5b6f-155">Exemple de projet sur GitHub</span><span class="sxs-lookup"><span data-stu-id="e5b6f-155">Sample project on GitHub</span></span>

<span data-ttu-id="e5b6f-156">Pour voir la bibliothèque Batch Management .NET en pratique, découvrez l’exemple de projet [AccountManagment][acct_mgmt_sample] sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="e5b6f-156">To see Batch Management .NET in action, check out the [AccountManagment][acct_mgmt_sample] sample project on GitHub.</span></span> <span data-ttu-id="e5b6f-157">L’exemple d’application AccountManagement illustre les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="e5b6f-157">The AccountManagment sample application demonstrates the following operations:</span></span>

1. <span data-ttu-id="e5b6f-158">Acquérir un jeton de sécurité d’Azure AD avec [ADAL][aad_adal].</span><span class="sxs-lookup"><span data-stu-id="e5b6f-158">Acquire a security token from Azure AD by using [ADAL][aad_adal].</span></span> <span data-ttu-id="e5b6f-159">Si l’utilisateur n’est pas encore connecté, il est invité à entrer ses informations d’identification Azure.</span><span class="sxs-lookup"><span data-stu-id="e5b6f-159">If the user is not already signed in, they are prompted for their Azure credentials.</span></span>
2. <span data-ttu-id="e5b6f-160">Avec le jeton de sécurité obtenu à partir d’Azure AD, créez une classe [SubscriptionClient][resman_subclient] pour demander à Azure la liste des abonnements associés au compte.</span><span class="sxs-lookup"><span data-stu-id="e5b6f-160">With the security token obtained from Azure AD, create a [SubscriptionClient][resman_subclient] to query Azure for a list of subscriptions associated with the account.</span></span> <span data-ttu-id="e5b6f-161">L’utilisateur peut sélectionner un abonnement à partir de la liste si celle-ci en contient plusieurs.</span><span class="sxs-lookup"><span data-stu-id="e5b6f-161">The user can select a subscription from the list if it contains more than one subscription.</span></span>
3. <span data-ttu-id="e5b6f-162">Obtenez les informations d’identification associées à l’abonnement sélectionné.</span><span class="sxs-lookup"><span data-stu-id="e5b6f-162">Get credentials associated with the selected subscription.</span></span>
4. <span data-ttu-id="e5b6f-163">Créez un objet [ResourceManagementClient][resman_client] avec les informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="e5b6f-163">Create a [ResourceManagementClient][resman_client] object by using the credentials.</span></span>
5. <span data-ttu-id="e5b6f-164">Utilisez un objet [ResourceManagementClient][resman_client] pour créer un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="e5b6f-164">Use a [ResourceManagementClient][resman_client] object to create a resource group.</span></span>
6. <span data-ttu-id="e5b6f-165">Utilisez un objet [BatchManagementClient][net_mgmt_client] pour effectuer un certain nombre d’opérations de compte Batch :</span><span class="sxs-lookup"><span data-stu-id="e5b6f-165">Use a [BatchManagementClient][net_mgmt_client] object to perform several Batch account operations:</span></span>
   * <span data-ttu-id="e5b6f-166">Créez un compte Batch dans le nouveau groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="e5b6f-166">Create a Batch account in the new resource group.</span></span>
   * <span data-ttu-id="e5b6f-167">Récupérer le compte créé dans le service Batch</span><span class="sxs-lookup"><span data-stu-id="e5b6f-167">Get the newly created account from the Batch service.</span></span>
   * <span data-ttu-id="e5b6f-168">Imprimer les clés du nouveau compte</span><span class="sxs-lookup"><span data-stu-id="e5b6f-168">Print the account keys for the new account.</span></span>
   * <span data-ttu-id="e5b6f-169">Régénérer une nouvelle clé primaire pour le compte</span><span class="sxs-lookup"><span data-stu-id="e5b6f-169">Regenerate a new primary key for the account.</span></span>
   * <span data-ttu-id="e5b6f-170">Imprimer les informations de quota du compte</span><span class="sxs-lookup"><span data-stu-id="e5b6f-170">Print the quota information for the account.</span></span>
   * <span data-ttu-id="e5b6f-171">Imprimer les informations de quota de l’abonnement</span><span class="sxs-lookup"><span data-stu-id="e5b6f-171">Print the quota information for the subscription.</span></span>
   * <span data-ttu-id="e5b6f-172">Imprimer tous les comptes de l’abonnement</span><span class="sxs-lookup"><span data-stu-id="e5b6f-172">Print all accounts within the subscription.</span></span>
   * <span data-ttu-id="e5b6f-173">Supprimer le compte créé</span><span class="sxs-lookup"><span data-stu-id="e5b6f-173">Delete newly created account.</span></span>
7. <span data-ttu-id="e5b6f-174">Supprimez le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="e5b6f-174">Delete the resource group.</span></span>

<span data-ttu-id="e5b6f-175">Avant de supprimer le compte Batch et le groupe de ressources qui viennent d’être créés, vous pouvez les afficher tous les deux dans le [Portail Azure][azure_portal] :</span><span class="sxs-lookup"><span data-stu-id="e5b6f-175">Before deleting the newly created Batch account and resource group, you can view them in the [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="e5b6f-176">Pour exécuter l’exemple d’application, vous devez tout d’abord l’inscrire auprès de votre locataire Azure AD sur le portail Azure et accorder des autorisations à l’API Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e5b6f-176">To run the sample application successfully, you must first register it with your Azure AD tenant in the Azure portal and grant permissions to the Azure Resource Manager API.</span></span> <span data-ttu-id="e5b6f-177">Suivez les étapes indiquées dans [Authentifier des solutions de gestion Batch avec Active Directory](batch-aad-auth-management.md).</span><span class="sxs-lookup"><span data-stu-id="e5b6f-177">Follow the steps provided in [Authenticate Batch Management solutions with Active Directory](batch-aad-auth-management.md).</span></span>


<span data-ttu-id="e5b6f-178">[aad_about]: ../active-directory/active-directory-whatis.md "Qu’est-ce qu’Azure Active Directory ?"</span><span class="sxs-lookup"><span data-stu-id="e5b6f-178">[aad_about]: ../active-directory/active-directory-whatis.md "What is Azure Active Directory?"</span></span>
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
<span data-ttu-id="e5b6f-179">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Scénarios d’authentification pour Azure AD"</span><span class="sxs-lookup"><span data-stu-id="e5b6f-179">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Authentication Scenarios for Azure AD"</span></span>
<span data-ttu-id="e5b6f-180">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Intégration d’applications dans Azure Active Directory"</span><span class="sxs-lookup"><span data-stu-id="e5b6f-180">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrating Applications with Azure Active Directory"</span></span>
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_mgmt_net]: https://msdn.microsoft.com/library/azure/mt463120.aspx
[azure_portal]: http://portal.azure.com
[azure_storage]: https://azure.microsoft.com/services/storage/
[azure_tokencreds]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.tokencloudcredentials.aspx
[batch_explorer_project]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[net_batch_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_list_keys]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.listkeysasync.aspx
[net_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.createasync.aspx
[net_delete]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.deleteasync.aspx
[net_regenerate_keys]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.regeneratekeyasync.aspx
[net_sharedkeycred]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.auth.batchsharedkeycredentials.aspx
[net_mgmt_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.batchmanagementclient.aspx
[net_mgmt_subscriptions]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.batchmanagementclient.subscriptions.aspx
[net_mgmt_listaccounts]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.iaccountoperations.listasync.aspx
[resman_api]: https://msdn.microsoft.com/library/azure/mt418626.aspx
[resman_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.resources.resourcemanagementclient.aspx
[resman_subclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.subscriptions.subscriptionclient.aspx
[resman_overview]: ../azure-resource-manager/resource-group-overview.md

[1]: ./media/batch-management-dotnet/portal-01.png
[2]: ./media/batch-management-dotnet/portal-02.png
[3]: ./media/batch-management-dotnet/portal-03.png
