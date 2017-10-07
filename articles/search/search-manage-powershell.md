---
title: aaaManage Azure Search avec des scripts Powershell | Documents Microsoft
description: "Gérez votre service Azure Search avec des scripts PowerShell. Créez ou mettez à jour un service Azure Search et gérez les clés d’administration Azure Search"
services: search
documentationcenter: 
author: seansaleh
manager: mblythe
editor: 
tags: azure-resource-manager
ms.assetid: 9b3dc1f2-3619-4235-ba1f-d2d6f5c45dd5
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: powershell
ms.date: 08/15/2016
ms.author: seasa
ms.openlocfilehash: fc7fb4b025340c77717601e0aaee938be3e9230f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-azure-search-service-with-powershell"></a><span data-ttu-id="24ac3-104">Gérer votre service Azure Search avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="24ac3-104">Manage your Azure Search service with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="24ac3-105">Portail</span><span class="sxs-lookup"><span data-stu-id="24ac3-105">Portal</span></span>](search-manage.md)
> * [<span data-ttu-id="24ac3-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="24ac3-106">PowerShell</span></span>](search-manage-powershell.md)
> 
> 

<span data-ttu-id="24ac3-107">Cette rubrique décrit tooperform de commandes PowerShell hello des tâches de gestion hello pour les services Azure Search.</span><span class="sxs-lookup"><span data-stu-id="24ac3-107">This topic describes hello PowerShell commands tooperform many of hello management tasks for Azure Search services.</span></span> <span data-ttu-id="24ac3-108">Nous allons étudier la création d’un service de recherche, sa mise à l’échelle et la gestion de ses clés d’API.</span><span class="sxs-lookup"><span data-stu-id="24ac3-108">We will walk through creating a search service, scaling it, and managing its API keys.</span></span>
<span data-ttu-id="24ac3-109">Ces commandes en parallèle les options de gestion hello disponibles dans hello [API REST de gestion Azure Search](http://msdn.microsoft.com/library/dn832684.aspx).</span><span class="sxs-lookup"><span data-stu-id="24ac3-109">These commands parallel hello management options available in hello [Azure Search Management REST API](http://msdn.microsoft.com/library/dn832684.aspx).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24ac3-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="24ac3-110">Prerequisites</span></span>
* <span data-ttu-id="24ac3-111">Vous devez disposer d’Azure PowerShell 1.0 ou versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="24ac3-111">You must have Azure PowerShell 1.0 or greater.</span></span> <span data-ttu-id="24ac3-112">Pour obtenir des instructions, consultez la rubrique [Installation et configuration d'Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="24ac3-112">For instructions, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="24ac3-113">Vous devez être connecté en tooyour abonnement Azure dans PowerShell, comme décrit ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="24ac3-113">You must be logged in tooyour Azure subscription in PowerShell as described below.</span></span>

<span data-ttu-id="24ac3-114">Vous devez tout d’abord, tooAzure de connexion avec cette commande :</span><span class="sxs-lookup"><span data-stu-id="24ac3-114">First, you must login tooAzure with this command:</span></span>

    Login-AzureRmAccount

<span data-ttu-id="24ac3-115">Spécifiez l’adresse de messagerie de hello de votre compte Azure et son mot de passe dans la boîte de dialogue de connexion hello Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="24ac3-115">Specify hello email address of your Azure account and its password in hello Microsoft Azure login dialog.</span></span>

<span data-ttu-id="24ac3-116">Vous pouvez également [vous connecter de manière non interactive avec un principal de service](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="24ac3-116">Alternatively you can [login non-interactively with a service principal](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

<span data-ttu-id="24ac3-117">Si vous avez plusieurs abonnements Azure, vous devez tooset votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="24ac3-117">If you have multiple Azure subscriptions, you need tooset your Azure subscription.</span></span> <span data-ttu-id="24ac3-118">toosee une liste de vos abonnements en cours, exécutez la commande.</span><span class="sxs-lookup"><span data-stu-id="24ac3-118">toosee a list of your current subscriptions, run this command.</span></span>

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

<span data-ttu-id="24ac3-119">abonnement de hello toospecify, exécutez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="24ac3-119">toospecify hello subscription, run hello following command.</span></span> <span data-ttu-id="24ac3-120">Dans l’exemple suivant de hello, nom de l’abonnement hello est `ContosoSubscription`.</span><span class="sxs-lookup"><span data-stu-id="24ac3-120">In hello following example, hello subscription name is `ContosoSubscription`.</span></span>

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

## <a name="commands-toohelp-you-get-started"></a><span data-ttu-id="24ac3-121">Toohelp de commandes que vous prise en main</span><span class="sxs-lookup"><span data-stu-id="24ac3-121">Commands toohelp you get started</span></span>
    $serviceName = "your-service-name-lowercase-with-dashes"
    $sku = "free" # or "basic" or "standard" for paid services
    $location = "West US"
    # You can get a list of potential locations with
    # (Get-AzureRmResourceProvider -ListAvailable | Where-Object {$_.ProviderNamespace -eq 'Microsoft.Search'}).Locations
    $resourceGroupName = "YourResourceGroup" 
    # If you don't already have this resource group, you can create it with 
    # New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Register hello ARM provider idempotently. This must be done once per subscription
    Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Search"

    # Create a new search service
    # This command will return once hello service is fully created
    New-AzureRmResourceGroupDeployment `
        -ResourceGroupName $resourceGroupName `
        -TemplateUri "https://gallery.azure.com/artifact/20151001/Microsoft.Search.1.0.9/DeploymentTemplates/searchServiceDefaultTemplate.json" `
        -NameFromTemplate $serviceName `
        -Sku $sku `
        -Location $location `
        -PartitionCount 1 `
        -ReplicaCount 1

    # Get information about your new service and store it in $resource
    $resource = Get-AzureRmResource `
        -ResourceType "Microsoft.Search/searchServices" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19

    # View your resource
    $resource

    # Get hello primary admin API key
    $primaryKey = (Invoke-AzureRmResourceAction `
        -Action listAdminKeys `
        -ResourceId $resource.ResourceId `
        -ApiVersion 2015-08-19).PrimaryKey

    # Regenerate hello secondary admin API Key
    $secondaryKey = (Invoke-AzureRmResourceAction `
        -ResourceType "Microsoft.Search/searchServices/regenerateAdminKey" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19 `
        -Action secondary).SecondaryKey

    # Create a query key for read only access tooyour indexes
    $queryKeyDescription = "query-key-created-from-powershell"
    $queryKey = (Invoke-AzureRmResourceAction `
        -ResourceType "Microsoft.Search/searchServices/createQueryKey" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19 `
        -Action $queryKeyDescription).Key

    # View your query key
    $queryKey

    # Delete query key
    Remove-AzureRmResource `
        -ResourceType "Microsoft.Search/searchServices/deleteQueryKey/$($queryKey)" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19

    # Scale your service up
    # Note that this will only work if you made a non "free" service
    # This command will not return until hello operation is finished
    # It can take 15 minutes or more tooprovision hello additional resources
    $resource.Properties.ReplicaCount = 2
    $resource | Set-AzureRmResource

    # Delete your service
    # Deleting your service will delete all indexes and data in hello service
    $resource | Remove-AzureRmResource

## <a name="next-steps"></a><span data-ttu-id="24ac3-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="24ac3-122">Next Steps</span></span>
<span data-ttu-id="24ac3-123">Maintenant que votre service est créé, vous pouvez prendre des mesures de suivant hello : générer un [index](search-what-is-an-index.md), [interroger un index](search-query-overview.md)et enfin créer et gérer votre propre application de recherche qui utilise Azure Search.</span><span class="sxs-lookup"><span data-stu-id="24ac3-123">Now that your service is created, you can take hello next steps: build an [index](search-what-is-an-index.md), [query an index](search-query-overview.md), and finally create and manage your own search application that uses Azure Search.</span></span>

* [<span data-ttu-id="24ac3-124">Créer un index Azure Search Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="24ac3-124">Create an Azure Search index in hello Azure portal</span></span>](search-create-index-portal.md)
* [<span data-ttu-id="24ac3-125">Interroger un index Azure Search à l’aide de l’Explorateur de recherche Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="24ac3-125">Query an Azure Search index using Search Explorer in hello Azure portal</span></span>](search-explorer.md)
* [<span data-ttu-id="24ac3-126">Programme d’installation un indexeur tooload de données à partir d’autres services</span><span class="sxs-lookup"><span data-stu-id="24ac3-126">Setup an indexer tooload data from other services</span></span>](search-indexer-overview.md)
* [<span data-ttu-id="24ac3-127">Comment effectuer une recherche toouse Azure dans .NET</span><span class="sxs-lookup"><span data-stu-id="24ac3-127">How toouse Azure Search in .NET</span></span>](search-howto-dotnet-sdk.md)
* [<span data-ttu-id="24ac3-128">Analyse du trafic Azure Search</span><span class="sxs-lookup"><span data-stu-id="24ac3-128">Analyze your Azure Search traffic</span></span>](search-traffic-analytics.md)

