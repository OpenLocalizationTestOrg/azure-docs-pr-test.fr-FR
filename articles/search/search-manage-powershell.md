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
# <a name="manage-your-azure-search-service-with-powershell"></a>Gérer votre service Azure Search avec PowerShell
> [!div class="op_single_selector"]
> * [Portail](search-manage.md)
> * [PowerShell](search-manage-powershell.md)
> 
> 

Cette rubrique décrit tooperform de commandes PowerShell hello des tâches de gestion hello pour les services Azure Search. Nous allons étudier la création d’un service de recherche, sa mise à l’échelle et la gestion de ses clés d’API.
Ces commandes en parallèle les options de gestion hello disponibles dans hello [API REST de gestion Azure Search](http://msdn.microsoft.com/library/dn832684.aspx).

## <a name="prerequisites"></a>Composants requis
* Vous devez disposer d’Azure PowerShell 1.0 ou versions ultérieures. Pour obtenir des instructions, consultez la rubrique [Installation et configuration d'Azure PowerShell](/powershell/azure/overview).
* Vous devez être connecté en tooyour abonnement Azure dans PowerShell, comme décrit ci-dessous.

Vous devez tout d’abord, tooAzure de connexion avec cette commande :

    Login-AzureRmAccount

Spécifiez l’adresse de messagerie de hello de votre compte Azure et son mot de passe dans la boîte de dialogue de connexion hello Microsoft Azure.

Vous pouvez également [vous connecter de manière non interactive avec un principal de service](../azure-resource-manager/resource-group-authenticate-service-principal.md).

Si vous avez plusieurs abonnements Azure, vous devez tooset votre abonnement Azure. toosee une liste de vos abonnements en cours, exécutez la commande.

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

abonnement de hello toospecify, exécutez hello commande suivante. Dans l’exemple suivant de hello, nom de l’abonnement hello est `ContosoSubscription`.

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

## <a name="commands-toohelp-you-get-started"></a>Toohelp de commandes que vous prise en main
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

## <a name="next-steps"></a>Étapes suivantes
Maintenant que votre service est créé, vous pouvez prendre des mesures de suivant hello : générer un [index](search-what-is-an-index.md), [interroger un index](search-query-overview.md)et enfin créer et gérer votre propre application de recherche qui utilise Azure Search.

* [Créer un index Azure Search Bonjour portail Azure](search-create-index-portal.md)
* [Interroger un index Azure Search à l’aide de l’Explorateur de recherche Bonjour portail Azure](search-explorer.md)
* [Programme d’installation un indexeur tooload de données à partir d’autres services](search-indexer-overview.md)
* [Comment effectuer une recherche toouse Azure dans .NET](search-howto-dotnet-sdk.md)
* [Analyse du trafic Azure Search](search-traffic-analytics.md)

