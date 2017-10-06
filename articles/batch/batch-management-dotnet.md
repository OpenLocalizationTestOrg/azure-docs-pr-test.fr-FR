---
title: "ressources de compte de traitement par lots aaaManage avec la bibliothèque cliente de hello pour .NET - Azure | Documents Microsoft"
description: "Créer, supprimer et modifier des ressources de compte Azure Batch avec la bibliothèque de Batch Management .NET hello."
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
ms.openlocfilehash: 638d8129f3841ffcfb2e10f5d531a319bcbb7701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-accounts-and-quotas-with-hello-batch-management-client-library-for-net"></a><span data-ttu-id="d7422-103">Gérer les quotas avec la bibliothèque cliente de gestion par lots hello et comptes Batch pour .NET</span><span class="sxs-lookup"><span data-stu-id="d7422-103">Manage Batch accounts and quotas with hello Batch Management client library for .NET</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d7422-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="d7422-104">Azure portal</span></span>](batch-account-create-portal.md)
> * [<span data-ttu-id="d7422-105">Gestion de lots .NET</span><span class="sxs-lookup"><span data-stu-id="d7422-105">Batch Management .NET</span></span>](batch-management-dotnet.md)
> 
> 

<span data-ttu-id="d7422-106">Vous pouvez diminuer maintenance surcharge dans vos applications de traitement par lots Azure à l’aide de hello [Batch Management .NET] [ api_mgmt_net] la création du compte de traitement par lots bibliothèque tooautomate, la suppression, la gestion de clés et découverte de quota.</span><span class="sxs-lookup"><span data-stu-id="d7422-106">You can lower maintenance overhead in your Azure Batch applications by using hello [Batch Management .NET][api_mgmt_net] library tooautomate Batch account creation, deletion, key management, and quota discovery.</span></span>

* <span data-ttu-id="d7422-107">**Créez et supprimez des comptes Batch** dans n'importe quelle région.</span><span class="sxs-lookup"><span data-stu-id="d7422-107">**Create and delete Batch accounts** within any region.</span></span> <span data-ttu-id="d7422-108">Si, par exemple, comme un éditeur de logiciels indépendant (ISV) vous fournissez un service à vos clients dans lequel chaque est affectée d’un compte de traitement par lots distinct pour la facturation, vous pouvez ajouter la création et la suppression des fonctionnalités tooyour client portail du compte.</span><span class="sxs-lookup"><span data-stu-id="d7422-108">If, as an independent software vendor (ISV) for example, you provide a service for your clients in which each is assigned a separate Batch account for billing purposes, you can add account creation and deletion capabilities tooyour customer portal.</span></span>
* <span data-ttu-id="d7422-109">**Récupérez et régénérez des clés de compte** par programme pour tous vos comptes Batch.</span><span class="sxs-lookup"><span data-stu-id="d7422-109">**Retrieve and regenerate account keys** programmatically for any of your Batch accounts.</span></span> <span data-ttu-id="d7422-110">Cela est pratique pour maintenir la conformité aux stratégies de sécurité appliquant une substitution ou une expiration périodique des clés de compte.</span><span class="sxs-lookup"><span data-stu-id="d7422-110">This can help you comply with security policies that enforce periodic rollover or expiry of account keys.</span></span> <span data-ttu-id="d7422-111">Lorsque vous avez plusieurs comptes Batch dans différentes régions Azure, l’automatisation de ce processus de substitution augmente l’efficacité de votre solution.</span><span class="sxs-lookup"><span data-stu-id="d7422-111">When you have several Batch accounts in various Azure regions, automation of this rollover process increases your solution's efficiency.</span></span>
* <span data-ttu-id="d7422-112">**Vérifiez les quotas de compte** et prendre hello essai et erreur incertitudes en déterminant les comptes de traitement par lots ont les limites.</span><span class="sxs-lookup"><span data-stu-id="d7422-112">**Check account quotas** and take hello trial-and-error guesswork out of determining which Batch accounts have what limits.</span></span> <span data-ttu-id="d7422-113">En vérifiant les quotas de vos comptes avant de commencer les travaux, de créer des pools ou d’ajouter des nœuds de calcul, vous pouvez ajuster de façon proactive l’endroit et le moment où ces ressources de calcul sont créées.</span><span class="sxs-lookup"><span data-stu-id="d7422-113">By checking your account quotas before starting jobs, creating pools, or adding compute nodes, you can proactively adjust where or when these compute resources are created.</span></span> <span data-ttu-id="d7422-114">Vous pouvez déterminer quels comptes requièrent des augmentations de quota avant d’allouer des ressources supplémentaires à ces comptes.</span><span class="sxs-lookup"><span data-stu-id="d7422-114">You can determine which accounts require quota increases before allocating additional resources in those accounts.</span></span>
* <span data-ttu-id="d7422-115">**Combiner les fonctionnalités d’autres services Azure** pour une expérience de gestion complète, à l’aide de Batch Management .NET, [Azure Active Directory][aad_about]et hello [Azure Le Gestionnaire de ressources] [ resman_overview] hello dans la même application.</span><span class="sxs-lookup"><span data-stu-id="d7422-115">**Combine features of other Azure services** for a full-featured management experience--by using Batch Management .NET, [Azure Active Directory][aad_about], and hello [Azure Resource Manager][resman_overview] together in hello same application.</span></span> <span data-ttu-id="d7422-116">À l’aide de ces fonctionnalités et leurs API, vous pouvez fournir une expérience d’authentification sans friction, hello toocreate de capacité et supprimer des groupes de ressources et des fonctions de hello décrites ci-dessus pour une solution de gestion de bout en bout.</span><span class="sxs-lookup"><span data-stu-id="d7422-116">By using these features and their APIs, you can provide a frictionless authentication experience, hello ability toocreate and delete resource groups, and hello capabilities that are described above for an end-to-end management solution.</span></span>

> [!NOTE]
> <span data-ttu-id="d7422-117">Alors que cet article se concentre sur la gestion par programme de hello de vos comptes, les clés et les quotas de lot, vous pouvez effectuer la plupart de ces activités à l’aide de hello [portail Azure][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="d7422-117">While this article focuses on hello programmatic management of your Batch accounts, keys, and quotas, you can perform many of these activities by using hello [Azure portal][azure_portal].</span></span> <span data-ttu-id="d7422-118">Pour plus d’informations, consultez [créer un compte Azure Batch hello portail Azure](batch-account-create-portal.md) et [Quotas et limites pour hello service Azure Batch](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="d7422-118">For more information, see [Create an Azure Batch account using hello Azure portal](batch-account-create-portal.md) and [Quotas and limits for hello Azure Batch service](batch-quota-limit.md).</span></span>
> 
> 

## <a name="create-and-delete-batch-accounts"></a><span data-ttu-id="d7422-119">Créez et supprimez des comptes Batch</span><span class="sxs-lookup"><span data-stu-id="d7422-119">Create and delete Batch accounts</span></span>
<span data-ttu-id="d7422-120">Comme indiqué, une des principales fonctionnalités de hello Hello API de gestion de traitement par lots est toocreate et supprimer des comptes de traitement par lots dans une région Azure.</span><span class="sxs-lookup"><span data-stu-id="d7422-120">As mentioned, one of hello primary features of hello Batch Management API is toocreate and delete Batch accounts in an Azure region.</span></span> <span data-ttu-id="d7422-121">toodo donc utiliser [BatchManagementClient.Account.CreateAsync] [ net_create] et [DeleteAsync][net_delete], ou leurs équivalents synchrones.</span><span class="sxs-lookup"><span data-stu-id="d7422-121">toodo so, use [BatchManagementClient.Account.CreateAsync][net_create] and [DeleteAsync][net_delete], or their synchronous counterparts.</span></span>

<span data-ttu-id="d7422-122">Hello extrait de code suivant crée un compte, obtient hello qui vient d’être créé le compte à partir de hello service Batch, puis le supprime.</span><span class="sxs-lookup"><span data-stu-id="d7422-122">hello following code snippet creates an account, obtains hello newly created account from hello Batch service, and then deletes it.</span></span> <span data-ttu-id="d7422-123">Dans cet extrait de code et d’autres hello dans cet article, `batchManagementClient` est une instance complètement initialisée de [BatchManagementClient][net_mgmt_client].</span><span class="sxs-lookup"><span data-stu-id="d7422-123">In this snippet and hello others in this article, `batchManagementClient` is a fully initialized instance of [BatchManagementClient][net_mgmt_client].</span></span>

```csharp
// Create a new Batch account
await batchManagementClient.Account.CreateAsync("MyResourceGroup",
    "mynewaccount",
    new BatchAccountCreateParameters() { Location = "West US" });

// Get hello new account from hello Batch service
AccountResource account = await batchManagementClient.Account.GetAsync(
    "MyResourceGroup",
    "mynewaccount");

// Delete hello account
await batchManagementClient.Account.DeleteAsync("MyResourceGroup", account.Name);
```

> [!NOTE]
> <span data-ttu-id="d7422-124">Applications qui utilisent la bibliothèque de Batch Management .NET hello et sa classe BatchManagementClient nécessitent **administrateur de service** ou **coadministrator** toohello abonnement propriétaire hello d’accès Traitement par lots toobe compte géré.</span><span class="sxs-lookup"><span data-stu-id="d7422-124">Applications that use hello Batch Management .NET library and its BatchManagementClient class require **service administrator** or **coadministrator** access toohello subscription that owns hello Batch account toobe managed.</span></span> <span data-ttu-id="d7422-125">Pour plus d’informations, consultez hello [Azure Active Directory](#azure-active-directory) section et hello [AccountManagement] [ acct_mgmt_sample] exemple de code.</span><span class="sxs-lookup"><span data-stu-id="d7422-125">For more information, see hello [Azure Active Directory](#azure-active-directory) section and hello [AccountManagement][acct_mgmt_sample] code sample.</span></span>
> 
> 

## <a name="retrieve-and-regenerate-account-keys"></a><span data-ttu-id="d7422-126">Récupérez et régénérez des clés de compte</span><span class="sxs-lookup"><span data-stu-id="d7422-126">Retrieve and regenerate account keys</span></span>
<span data-ttu-id="d7422-127">Récupérez les clés primaires et secondaires de n’importe quel compte Batch de votre abonnement avec [ListKeysAsync][net_list_keys].</span><span class="sxs-lookup"><span data-stu-id="d7422-127">Obtain primary and secondary account keys from any Batch account within your subscription by using [ListKeysAsync][net_list_keys].</span></span> <span data-ttu-id="d7422-128">Vous pouvez régénérer ces clés à l’aide de [RegenerateKeyAsync][net_regenerate_keys].</span><span class="sxs-lookup"><span data-stu-id="d7422-128">You can regenerate those keys by using [RegenerateKeyAsync][net_regenerate_keys].</span></span>

```csharp
// Get and print hello primary and secondary keys
BatchAccountListKeyResult accountKeys =
    await batchManagementClient.Account.ListKeysAsync(
        "MyResourceGroup",
        "mybatchaccount");
Console.WriteLine("Primary key:   {0}", accountKeys.Primary);
Console.WriteLine("Secondary key: {0}", accountKeys.Secondary);

// Regenerate hello primary key
BatchAccountRegenerateKeyResponse newKeys =
    await batchManagementClient.Account.RegenerateKeyAsync(
        "MyResourceGroup",
        "mybatchaccount",
        new BatchAccountRegenerateKeyParameters() {
            KeyName = AccountKeyType.Primary
            });
```

> [!TIP]
> <span data-ttu-id="d7422-129">Vous pouvez créer un flux de travail de connexion rationalisé pour vos applications de gestion.</span><span class="sxs-lookup"><span data-stu-id="d7422-129">You can create a streamlined connection workflow for your management applications.</span></span> <span data-ttu-id="d7422-130">Tout d’abord, obtenir une clé de compte pour le compte de traitement par lots hello vous souhaitez toomanage avec [ListKeysAsync][net_list_keys].</span><span class="sxs-lookup"><span data-stu-id="d7422-130">First, obtain an account key for hello Batch account you wish toomanage with [ListKeysAsync][net_list_keys].</span></span> <span data-ttu-id="d7422-131">Ensuite, utilisez cette clé lors de l’initialisation de la bibliothèque hello Batch .NET [BatchSharedKeyCredentials] [ net_sharedkeycred] (classe), qui est utilisé lors de l’initialisation [BatchClient] [net_batch_client].</span><span class="sxs-lookup"><span data-stu-id="d7422-131">Then, use this key when initializing hello Batch .NET library's [BatchSharedKeyCredentials][net_sharedkeycred] class, which is used when initializing [BatchClient][net_batch_client].</span></span>
> 
> 

## <a name="check-azure-subscription-and-batch-account-quotas"></a><span data-ttu-id="d7422-132">Vérifier les quotas d'un abonnement Azure et d'un compte Batch</span><span class="sxs-lookup"><span data-stu-id="d7422-132">Check Azure subscription and Batch account quotas</span></span>
<span data-ttu-id="d7422-133">Abonnements Azure et hello différents services Azure tels que tous les lots ont des quotas par défaut qui limitent le nombre de hello de certaines entités au sein de celles-ci.</span><span class="sxs-lookup"><span data-stu-id="d7422-133">Azure subscriptions and hello individual Azure services like Batch all have default quotas that limit hello number of certain entities within them.</span></span> <span data-ttu-id="d7422-134">Pour les quotas par défaut de hello pour les abonnements Azure, consultez [abonnement Azure et limites de service, quotas et contraintes](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="d7422-134">For hello default quotas for Azure subscriptions, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span> <span data-ttu-id="d7422-135">Pour les quotas par défaut de hello Hello service Batch, consultez [Quotas et limites pour hello service Azure Batch](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="d7422-135">For hello default quotas of hello Batch service, see [Quotas and limits for hello Azure Batch service](batch-quota-limit.md).</span></span> <span data-ttu-id="d7422-136">En utilisant la bibliothèque de hello Batch Management .NET, vous pouvez vérifier ces quotas dans vos applications.</span><span class="sxs-lookup"><span data-stu-id="d7422-136">By using hello Batch Management .NET library, you can check these quotas in your applications.</span></span> <span data-ttu-id="d7422-137">Cela permet les décisions de répartition toomake avant d’ajouter des comptes ou de ressources, telles que les pools de calcul et de nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="d7422-137">This enables you toomake allocation decisions before you add accounts or compute resources like pools and compute nodes.</span></span>

### <a name="check-an-azure-subscription-for-batch-account-quotas"></a><span data-ttu-id="d7422-138">Vérifier les quotas d'un compte Batch dans un abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="d7422-138">Check an Azure subscription for Batch account quotas</span></span>
<span data-ttu-id="d7422-139">Avant de créer un compte de traitement par lots dans une région, vous pouvez vérifier votre toosee abonnement Azure si vous êtes en mesure de tooadd un compte dans cette région.</span><span class="sxs-lookup"><span data-stu-id="d7422-139">Before creating a Batch account in a region, you can check your Azure subscription toosee whether you are able tooadd an account in that region.</span></span>

<span data-ttu-id="d7422-140">Dans l’extrait de code hello ci-dessous, nous avons tout d’abord utiliser [BatchManagementClient.Account.ListAsync] [ net_mgmt_listaccounts] tooget une collection de tous les comptes de traitement par lots qui se trouvent dans un abonnement.</span><span class="sxs-lookup"><span data-stu-id="d7422-140">In hello code snippet below, we first use [BatchManagementClient.Account.ListAsync][net_mgmt_listaccounts] tooget a collection of all Batch accounts that are within a subscription.</span></span> <span data-ttu-id="d7422-141">Une fois que nous avons obtenu de cette collection, nous déterminer le nombre de comptes dans la région cible hello.</span><span class="sxs-lookup"><span data-stu-id="d7422-141">Once we've obtained this collection, we determine how many accounts are in hello target region.</span></span> <span data-ttu-id="d7422-142">Ensuite, nous utilisons [BatchManagementClient.Subscriptions] [ net_mgmt_subscriptions] tooobtain hello quota de comptes Batch et déterminer le nombre de comptes (le cas échéant) peut être créé dans cette région.</span><span class="sxs-lookup"><span data-stu-id="d7422-142">Then we use [BatchManagementClient.Subscriptions][net_mgmt_subscriptions] tooobtain hello Batch account quota and determine how many accounts (if any) can be created in that region.</span></span>

```csharp
// Get a collection of all Batch accounts within hello subscription
BatchAccountListResponse listResponse =
        await batchManagementClient.Account.ListAsync(new AccountListParameters());
IList<AccountResource> accounts = listResponse.Accounts;
Console.WriteLine("Total number of Batch accounts under subscription id {0}:  {1}",
    creds.SubscriptionId,
    accounts.Count);

// Get a count of all accounts within hello target region
string region = "westus";
int accountsInRegion = accounts.Count(o => o.Location == region);

// Get hello account quota for hello specified region
SubscriptionQuotasGetResponse quotaResponse = await batchManagementClient.Subscriptions.GetSubscriptionQuotasAsync(region);
Console.WriteLine("Account quota for {0} region: {1}", region, quotaResponse.AccountQuota);

// Determine how many accounts can be created in hello target region
Console.WriteLine("Accounts in {0}: {1}", region, accountsInRegion);
Console.WriteLine("You can create {0} accounts in hello {1} region.", quotaResponse.AccountQuota - accountsInRegion, region);
```

<span data-ttu-id="d7422-143">Dans l’extrait de code hello ci-dessus, `creds` est une instance de [TokenCloudCredentials][azure_tokencreds].</span><span class="sxs-lookup"><span data-stu-id="d7422-143">In hello snippet above, `creds` is an instance of [TokenCloudCredentials][azure_tokencreds].</span></span> <span data-ttu-id="d7422-144">toosee un exemple de création de cet objet, consultez hello [AccountManagement] [ acct_mgmt_sample] exemple de code sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="d7422-144">toosee an example of creating this object, see hello [AccountManagement][acct_mgmt_sample] code sample on GitHub.</span></span>

### <a name="check-a-batch-account-for-compute-resource-quotas"></a><span data-ttu-id="d7422-145">Vérifier les quotas de ressources de calcul dans un compte Batch</span><span class="sxs-lookup"><span data-stu-id="d7422-145">Check a Batch account for compute resource quotas</span></span>
<span data-ttu-id="d7422-146">Avant d’augmenter les ressources de calcul dans votre solution de traitement par lots, vous pouvez vérifier tooensure hello ressources tooallocate ne dépassent les quotas du compte hello.</span><span class="sxs-lookup"><span data-stu-id="d7422-146">Before increasing compute resources in your Batch solution, you can check tooensure hello resources you want tooallocate won't exceed hello account's quotas.</span></span> <span data-ttu-id="d7422-147">Dans l’extrait de code hello ci-dessous, nous imprimer les informations de quota de hello pour hello compte Batch nommé `mybatchaccount`.</span><span class="sxs-lookup"><span data-stu-id="d7422-147">In hello code snippet below, we print hello quota information for hello Batch account named `mybatchaccount`.</span></span> <span data-ttu-id="d7422-148">Dans votre application, vous pouvez utiliser toodetermine de ces informations si le compte de hello peut gérer hello des ressources supplémentaires toobe est créé.</span><span class="sxs-lookup"><span data-stu-id="d7422-148">In your own application, you could use such information toodetermine whether hello account can handle hello additional resources toobe created.</span></span>

```csharp
// First obtain hello Batch account
BatchAccountGetResponse getResponse =
    await batchManagementClient.Account.GetAsync("MyResourceGroup", "mybatchaccount");
AccountResource account = getResponse.Resource;

// Now print hello compute resource quotas for hello account
Console.WriteLine("Core quota: {0}", account.Properties.CoreQuota);
Console.WriteLine("Pool quota: {0}", account.Properties.PoolQuota);
Console.WriteLine("Active job and job schedule quota: {0}", account.Properties.ActiveJobAndJobScheduleQuota);
```

> [!IMPORTANT]
> <span data-ttu-id="d7422-149">Bien qu’il existe des quotas par défaut pour les services et abonnements Azure, la plupart de ces limites peuvent être déclenchés en émettant une requête Bonjour [portail Azure][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="d7422-149">While there are default quotas for Azure subscriptions and services, many of these limits can be raised by issuing a request in hello [Azure portal][azure_portal].</span></span> <span data-ttu-id="d7422-150">Par exemple, consultez [Quotas et limites pour hello service Azure Batch](batch-quota-limit.md) pour obtenir des instructions sur l’augmentation de votre compte les quotas de lot.</span><span class="sxs-lookup"><span data-stu-id="d7422-150">For example, see [Quotas and limits for hello Azure Batch service](batch-quota-limit.md) for instructions on increasing your Batch account quotas.</span></span>
> 
> 

## <a name="use-azure-ad-with-batch-management-net"></a><span data-ttu-id="d7422-151">Utiliser Azure AD avec Batch Management .NET</span><span class="sxs-lookup"><span data-stu-id="d7422-151">Use Azure AD with Batch Management .NET</span></span>

<span data-ttu-id="d7422-152">bibliothèque de Batch Management .NET Hello est un client de fournisseur de ressources Azure et est utilisée conjointement avec [Azure Resource Manager] [ resman_overview] toomanage compte de ressources par programme.</span><span class="sxs-lookup"><span data-stu-id="d7422-152">hello Batch Management .NET library is an Azure resource provider client, and is used together with [Azure Resource Manager][resman_overview] toomanage account resources programmatically.</span></span> <span data-ttu-id="d7422-153">Azure AD est tooauthenticate requis les demandes effectuées via n’importe quel client de fournisseur de ressources Azure, y compris hello Batch Management .NET bibliothèque et [Azure Resource Manager][resman_overview].</span><span class="sxs-lookup"><span data-stu-id="d7422-153">Azure AD is required tooauthenticate requests made through any Azure resource provider client, including hello Batch Management .NET library, and through [Azure Resource Manager][resman_overview].</span></span> <span data-ttu-id="d7422-154">Pour plus d’informations sur l’utilisation d’Azure AD avec la bibliothèque de Batch Management .NET hello, consultez [solutions de lot tooauthenticate utilisation d’Azure Active Directory](batch-aad-auth.md).</span><span class="sxs-lookup"><span data-stu-id="d7422-154">For information about using Azure AD with hello Batch Management .NET library, see [Use Azure Active Directory tooauthenticate Batch solutions](batch-aad-auth.md).</span></span> 

## <a name="sample-project-on-github"></a><span data-ttu-id="d7422-155">Exemple de projet sur GitHub</span><span class="sxs-lookup"><span data-stu-id="d7422-155">Sample project on GitHub</span></span>

<span data-ttu-id="d7422-156">toosee Batch Management .NET en action, consultez hello [AccountManagment] [ acct_mgmt_sample] exemple de projet sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="d7422-156">toosee Batch Management .NET in action, check out hello [AccountManagment][acct_mgmt_sample] sample project on GitHub.</span></span> <span data-ttu-id="d7422-157">Hello AccountManagment exemple d’application montre hello opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="d7422-157">hello AccountManagment sample application demonstrates hello following operations:</span></span>

1. <span data-ttu-id="d7422-158">Acquérir un jeton de sécurité d’Azure AD avec [ADAL][aad_adal].</span><span class="sxs-lookup"><span data-stu-id="d7422-158">Acquire a security token from Azure AD by using [ADAL][aad_adal].</span></span> <span data-ttu-id="d7422-159">Si l’utilisateur de hello n’est pas déjà inscrit, ils sont invité à entrer leurs informations d’identification Azure.</span><span class="sxs-lookup"><span data-stu-id="d7422-159">If hello user is not already signed in, they are prompted for their Azure credentials.</span></span>
2. <span data-ttu-id="d7422-160">Jeton de sécurité hello obtenu d’Azure AD, de créer un [SubscriptionClient] [ resman_subclient] tooquery Azure pour obtenir la liste d’abonnements associés au compte de hello.</span><span class="sxs-lookup"><span data-stu-id="d7422-160">With hello security token obtained from Azure AD, create a [SubscriptionClient][resman_subclient] tooquery Azure for a list of subscriptions associated with hello account.</span></span> <span data-ttu-id="d7422-161">utilisateur de Hello pouvez sélectionner un abonnement à partir de la liste de hello si elle contient plus d’un abonnement.</span><span class="sxs-lookup"><span data-stu-id="d7422-161">hello user can select a subscription from hello list if it contains more than one subscription.</span></span>
3. <span data-ttu-id="d7422-162">Obtenir des informations d’identification associées d’abonnement de hello sélectionné.</span><span class="sxs-lookup"><span data-stu-id="d7422-162">Get credentials associated with hello selected subscription.</span></span>
4. <span data-ttu-id="d7422-163">Créer un [ResourceManagementClient] [ resman_client] objet à l’aide des informations d’identification hello.</span><span class="sxs-lookup"><span data-stu-id="d7422-163">Create a [ResourceManagementClient][resman_client] object by using hello credentials.</span></span>
5. <span data-ttu-id="d7422-164">Utilisez un [ResourceManagementClient] [ resman_client] toocreate un groupe de ressources de l’objet.</span><span class="sxs-lookup"><span data-stu-id="d7422-164">Use a [ResourceManagementClient][resman_client] object toocreate a resource group.</span></span>
6. <span data-ttu-id="d7422-165">Utilisez un [BatchManagementClient] [ net_mgmt_client] objet tooperform plusieurs opérations de compte de traitement par lots :</span><span class="sxs-lookup"><span data-stu-id="d7422-165">Use a [BatchManagementClient][net_mgmt_client] object tooperform several Batch account operations:</span></span>
   * <span data-ttu-id="d7422-166">Créez un compte de traitement par lots dans le nouveau groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="d7422-166">Create a Batch account in hello new resource group.</span></span>
   * <span data-ttu-id="d7422-167">Obtenir hello qui vient d’être créé le compte à partir de hello service Batch.</span><span class="sxs-lookup"><span data-stu-id="d7422-167">Get hello newly created account from hello Batch service.</span></span>
   * <span data-ttu-id="d7422-168">Imprimer les clés de compte hello pour le nouveau compte de hello.</span><span class="sxs-lookup"><span data-stu-id="d7422-168">Print hello account keys for hello new account.</span></span>
   * <span data-ttu-id="d7422-169">Régénérer une nouvelle clé primaire pour le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="d7422-169">Regenerate a new primary key for hello account.</span></span>
   * <span data-ttu-id="d7422-170">Imprimer les informations de quota hello pour le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="d7422-170">Print hello quota information for hello account.</span></span>
   * <span data-ttu-id="d7422-171">Imprimer les informations de quota hello pour l’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="d7422-171">Print hello quota information for hello subscription.</span></span>
   * <span data-ttu-id="d7422-172">Imprimer tous les comptes d’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="d7422-172">Print all accounts within hello subscription.</span></span>
   * <span data-ttu-id="d7422-173">Supprimer le compte créé</span><span class="sxs-lookup"><span data-stu-id="d7422-173">Delete newly created account.</span></span>
7. <span data-ttu-id="d7422-174">Supprimer le groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="d7422-174">Delete hello resource group.</span></span>

<span data-ttu-id="d7422-175">Avant de supprimer le groupe de comptes et de ressources de lot hello nouvellement créé, vous pouvez les afficher dans hello [portail Azure][azure_portal]:</span><span class="sxs-lookup"><span data-stu-id="d7422-175">Before deleting hello newly created Batch account and resource group, you can view them in hello [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="d7422-176">application d’exemple hello toorun avec succès, vous devez tout d’abord l’inscrire auprès de votre client Azure AD Bonjour Azure portal et accordez les autorisations toohello API Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d7422-176">toorun hello sample application successfully, you must first register it with your Azure AD tenant in hello Azure portal and grant permissions toohello Azure Resource Manager API.</span></span> <span data-ttu-id="d7422-177">Suivez les étapes de hello fournies dans [des solutions de gestion de traitement par lots s’authentifier avec Active Directory](batch-aad-auth-management.md).</span><span class="sxs-lookup"><span data-stu-id="d7422-177">Follow hello steps provided in [Authenticate Batch Management solutions with Active Directory](batch-aad-auth-management.md).</span></span>


[aad_about]: ../active-directory/active-directory-whatis.md "Qu’est-ce qu’Azure Active Directory ?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Scénarios d’authentification pour Azure AD"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Intégration d’applications dans Azure Active Directory"
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
