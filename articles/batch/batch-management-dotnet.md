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
# <a name="manage-batch-accounts-and-quotas-with-hello-batch-management-client-library-for-net"></a>Gérer les quotas avec la bibliothèque cliente de gestion par lots hello et comptes Batch pour .NET

> [!div class="op_single_selector"]
> * [Portail Azure](batch-account-create-portal.md)
> * [Gestion de lots .NET](batch-management-dotnet.md)
> 
> 

Vous pouvez diminuer maintenance surcharge dans vos applications de traitement par lots Azure à l’aide de hello [Batch Management .NET] [ api_mgmt_net] la création du compte de traitement par lots bibliothèque tooautomate, la suppression, la gestion de clés et découverte de quota.

* **Créez et supprimez des comptes Batch** dans n'importe quelle région. Si, par exemple, comme un éditeur de logiciels indépendant (ISV) vous fournissez un service à vos clients dans lequel chaque est affectée d’un compte de traitement par lots distinct pour la facturation, vous pouvez ajouter la création et la suppression des fonctionnalités tooyour client portail du compte.
* **Récupérez et régénérez des clés de compte** par programme pour tous vos comptes Batch. Cela est pratique pour maintenir la conformité aux stratégies de sécurité appliquant une substitution ou une expiration périodique des clés de compte. Lorsque vous avez plusieurs comptes Batch dans différentes régions Azure, l’automatisation de ce processus de substitution augmente l’efficacité de votre solution.
* **Vérifiez les quotas de compte** et prendre hello essai et erreur incertitudes en déterminant les comptes de traitement par lots ont les limites. En vérifiant les quotas de vos comptes avant de commencer les travaux, de créer des pools ou d’ajouter des nœuds de calcul, vous pouvez ajuster de façon proactive l’endroit et le moment où ces ressources de calcul sont créées. Vous pouvez déterminer quels comptes requièrent des augmentations de quota avant d’allouer des ressources supplémentaires à ces comptes.
* **Combiner les fonctionnalités d’autres services Azure** pour une expérience de gestion complète, à l’aide de Batch Management .NET, [Azure Active Directory][aad_about]et hello [Azure Le Gestionnaire de ressources] [ resman_overview] hello dans la même application. À l’aide de ces fonctionnalités et leurs API, vous pouvez fournir une expérience d’authentification sans friction, hello toocreate de capacité et supprimer des groupes de ressources et des fonctions de hello décrites ci-dessus pour une solution de gestion de bout en bout.

> [!NOTE]
> Alors que cet article se concentre sur la gestion par programme de hello de vos comptes, les clés et les quotas de lot, vous pouvez effectuer la plupart de ces activités à l’aide de hello [portail Azure][azure_portal]. Pour plus d’informations, consultez [créer un compte Azure Batch hello portail Azure](batch-account-create-portal.md) et [Quotas et limites pour hello service Azure Batch](batch-quota-limit.md).
> 
> 

## <a name="create-and-delete-batch-accounts"></a>Créez et supprimez des comptes Batch
Comme indiqué, une des principales fonctionnalités de hello Hello API de gestion de traitement par lots est toocreate et supprimer des comptes de traitement par lots dans une région Azure. toodo donc utiliser [BatchManagementClient.Account.CreateAsync] [ net_create] et [DeleteAsync][net_delete], ou leurs équivalents synchrones.

Hello extrait de code suivant crée un compte, obtient hello qui vient d’être créé le compte à partir de hello service Batch, puis le supprime. Dans cet extrait de code et d’autres hello dans cet article, `batchManagementClient` est une instance complètement initialisée de [BatchManagementClient][net_mgmt_client].

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
> Applications qui utilisent la bibliothèque de Batch Management .NET hello et sa classe BatchManagementClient nécessitent **administrateur de service** ou **coadministrator** toohello abonnement propriétaire hello d’accès Traitement par lots toobe compte géré. Pour plus d’informations, consultez hello [Azure Active Directory](#azure-active-directory) section et hello [AccountManagement] [ acct_mgmt_sample] exemple de code.
> 
> 

## <a name="retrieve-and-regenerate-account-keys"></a>Récupérez et régénérez des clés de compte
Récupérez les clés primaires et secondaires de n’importe quel compte Batch de votre abonnement avec [ListKeysAsync][net_list_keys]. Vous pouvez régénérer ces clés à l’aide de [RegenerateKeyAsync][net_regenerate_keys].

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
> Vous pouvez créer un flux de travail de connexion rationalisé pour vos applications de gestion. Tout d’abord, obtenir une clé de compte pour le compte de traitement par lots hello vous souhaitez toomanage avec [ListKeysAsync][net_list_keys]. Ensuite, utilisez cette clé lors de l’initialisation de la bibliothèque hello Batch .NET [BatchSharedKeyCredentials] [ net_sharedkeycred] (classe), qui est utilisé lors de l’initialisation [BatchClient] [net_batch_client].
> 
> 

## <a name="check-azure-subscription-and-batch-account-quotas"></a>Vérifier les quotas d'un abonnement Azure et d'un compte Batch
Abonnements Azure et hello différents services Azure tels que tous les lots ont des quotas par défaut qui limitent le nombre de hello de certaines entités au sein de celles-ci. Pour les quotas par défaut de hello pour les abonnements Azure, consultez [abonnement Azure et limites de service, quotas et contraintes](../azure-subscription-service-limits.md). Pour les quotas par défaut de hello Hello service Batch, consultez [Quotas et limites pour hello service Azure Batch](batch-quota-limit.md). En utilisant la bibliothèque de hello Batch Management .NET, vous pouvez vérifier ces quotas dans vos applications. Cela permet les décisions de répartition toomake avant d’ajouter des comptes ou de ressources, telles que les pools de calcul et de nœuds de calcul.

### <a name="check-an-azure-subscription-for-batch-account-quotas"></a>Vérifier les quotas d'un compte Batch dans un abonnement Azure
Avant de créer un compte de traitement par lots dans une région, vous pouvez vérifier votre toosee abonnement Azure si vous êtes en mesure de tooadd un compte dans cette région.

Dans l’extrait de code hello ci-dessous, nous avons tout d’abord utiliser [BatchManagementClient.Account.ListAsync] [ net_mgmt_listaccounts] tooget une collection de tous les comptes de traitement par lots qui se trouvent dans un abonnement. Une fois que nous avons obtenu de cette collection, nous déterminer le nombre de comptes dans la région cible hello. Ensuite, nous utilisons [BatchManagementClient.Subscriptions] [ net_mgmt_subscriptions] tooobtain hello quota de comptes Batch et déterminer le nombre de comptes (le cas échéant) peut être créé dans cette région.

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

Dans l’extrait de code hello ci-dessus, `creds` est une instance de [TokenCloudCredentials][azure_tokencreds]. toosee un exemple de création de cet objet, consultez hello [AccountManagement] [ acct_mgmt_sample] exemple de code sur GitHub.

### <a name="check-a-batch-account-for-compute-resource-quotas"></a>Vérifier les quotas de ressources de calcul dans un compte Batch
Avant d’augmenter les ressources de calcul dans votre solution de traitement par lots, vous pouvez vérifier tooensure hello ressources tooallocate ne dépassent les quotas du compte hello. Dans l’extrait de code hello ci-dessous, nous imprimer les informations de quota de hello pour hello compte Batch nommé `mybatchaccount`. Dans votre application, vous pouvez utiliser toodetermine de ces informations si le compte de hello peut gérer hello des ressources supplémentaires toobe est créé.

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
> Bien qu’il existe des quotas par défaut pour les services et abonnements Azure, la plupart de ces limites peuvent être déclenchés en émettant une requête Bonjour [portail Azure][azure_portal]. Par exemple, consultez [Quotas et limites pour hello service Azure Batch](batch-quota-limit.md) pour obtenir des instructions sur l’augmentation de votre compte les quotas de lot.
> 
> 

## <a name="use-azure-ad-with-batch-management-net"></a>Utiliser Azure AD avec Batch Management .NET

bibliothèque de Batch Management .NET Hello est un client de fournisseur de ressources Azure et est utilisée conjointement avec [Azure Resource Manager] [ resman_overview] toomanage compte de ressources par programme. Azure AD est tooauthenticate requis les demandes effectuées via n’importe quel client de fournisseur de ressources Azure, y compris hello Batch Management .NET bibliothèque et [Azure Resource Manager][resman_overview]. Pour plus d’informations sur l’utilisation d’Azure AD avec la bibliothèque de Batch Management .NET hello, consultez [solutions de lot tooauthenticate utilisation d’Azure Active Directory](batch-aad-auth.md). 

## <a name="sample-project-on-github"></a>Exemple de projet sur GitHub

toosee Batch Management .NET en action, consultez hello [AccountManagment] [ acct_mgmt_sample] exemple de projet sur GitHub. Hello AccountManagment exemple d’application montre hello opérations suivantes :

1. Acquérir un jeton de sécurité d’Azure AD avec [ADAL][aad_adal]. Si l’utilisateur de hello n’est pas déjà inscrit, ils sont invité à entrer leurs informations d’identification Azure.
2. Jeton de sécurité hello obtenu d’Azure AD, de créer un [SubscriptionClient] [ resman_subclient] tooquery Azure pour obtenir la liste d’abonnements associés au compte de hello. utilisateur de Hello pouvez sélectionner un abonnement à partir de la liste de hello si elle contient plus d’un abonnement.
3. Obtenir des informations d’identification associées d’abonnement de hello sélectionné.
4. Créer un [ResourceManagementClient] [ resman_client] objet à l’aide des informations d’identification hello.
5. Utilisez un [ResourceManagementClient] [ resman_client] toocreate un groupe de ressources de l’objet.
6. Utilisez un [BatchManagementClient] [ net_mgmt_client] objet tooperform plusieurs opérations de compte de traitement par lots :
   * Créez un compte de traitement par lots dans le nouveau groupe de ressources hello.
   * Obtenir hello qui vient d’être créé le compte à partir de hello service Batch.
   * Imprimer les clés de compte hello pour le nouveau compte de hello.
   * Régénérer une nouvelle clé primaire pour le compte de hello.
   * Imprimer les informations de quota hello pour le compte de hello.
   * Imprimer les informations de quota hello pour l’abonnement de hello.
   * Imprimer tous les comptes d’abonnement de hello.
   * Supprimer le compte créé
7. Supprimer le groupe de ressources hello.

Avant de supprimer le groupe de comptes et de ressources de lot hello nouvellement créé, vous pouvez les afficher dans hello [portail Azure][azure_portal]:

application d’exemple hello toorun avec succès, vous devez tout d’abord l’inscrire auprès de votre client Azure AD Bonjour Azure portal et accordez les autorisations toohello API Azure Resource Manager. Suivez les étapes de hello fournies dans [des solutions de gestion de traitement par lots s’authentifier avec Active Directory](batch-aad-auth-management.md).


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
