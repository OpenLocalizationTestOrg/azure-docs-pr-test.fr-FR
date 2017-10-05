---
title: "Utiliser PowerShell pour gérer les ressources Azure Event Hubs | Microsoft Docs"
description: "Utiliser le module PowerShell pour créer et gérer Event Hubs"
services: event-hubs
documentationcenter: .NET
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 2b49c01153b1104612e6ebf9c88566fc40d1f635
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="use-powershell-to-manage-event-hubs-resources"></a><span data-ttu-id="9588d-103">Utiliser PowerShell pour gérer des ressources Event Hubs</span><span class="sxs-lookup"><span data-stu-id="9588d-103">Use PowerShell to manage Event Hubs resources</span></span>

<span data-ttu-id="9588d-104">Microsoft Azure PowerShell est un environnement de création de scripts vous permettant de contrôler et d'automatiser le déploiement et la gestion des services Azure.</span><span class="sxs-lookup"><span data-stu-id="9588d-104">Microsoft Azure PowerShell is a scripting environment that you can use to control and automate the deployment and management of Azure services.</span></span> <span data-ttu-id="9588d-105">Cet article explique comment utiliser le [module PowerShell du Gestionnaire de ressources Event Hubs](/powershell/module/azurerm.eventhub) pour approvisionner et gérer les entités Event Hubs (espaces de noms, concentrateurs d’événements individuels et groupes de consommateurs) à l’aide d’une console Azure PowerShell locale ou d’un script.</span><span class="sxs-lookup"><span data-stu-id="9588d-105">This article describes how to use the [Event Hubs Resource Manager PowerShell module](/powershell/module/azurerm.eventhub) to provision and manage Event Hubs entities (namespaces, individual event hubs, and consumer groups) using a local Azure PowerShell console or script.</span></span>

<span data-ttu-id="9588d-106">Vous pouvez également gérer les ressources Event Hubs avec des modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9588d-106">You can also manage Event Hubs resources using Azure Resource Manager templates.</span></span> <span data-ttu-id="9588d-107">Pour plus d’informations, consultez l’article [Créer un espace de noms Event Hubs avec un concentrateur d’événements et un groupe de consommateurs à l’aide d’un modèle Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub.md).</span><span class="sxs-lookup"><span data-stu-id="9588d-107">For more information, see the article [Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9588d-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9588d-108">Prerequisites</span></span>

<span data-ttu-id="9588d-109">Avant de débuter, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="9588d-109">Before you begin, you'll need the following:</span></span>

* <span data-ttu-id="9588d-110">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="9588d-110">An Azure subscription.</span></span> <span data-ttu-id="9588d-111">Pour plus d’informations sur la façon de se procurer un abonnement, consultez les [options d’achat][purchase options], les [offres spéciales membres][member offers] ou découvrez comment créer un [compte gratuit][free account].</span><span class="sxs-lookup"><span data-stu-id="9588d-111">For more information about obtaining a subscription, see [purchase options][purchase options], [member offers][member offers], or [free account][free account].</span></span>
* <span data-ttu-id="9588d-112">Un ordinateur sur lequel est installé Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9588d-112">A computer with Azure PowerShell.</span></span> <span data-ttu-id="9588d-113">Pour obtenir des instructions, consultez la page [Bien démarrer avec les applets de commande Azure PowerShell](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="9588d-113">For instructions, see [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps).</span></span>
* <span data-ttu-id="9588d-114">Des connaissances générales sur les scripts PowerShell, les packages NuGet et .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="9588d-114">A general understanding of PowerShell scripts, NuGet packages, and the .NET Framework.</span></span>

## <a name="get-started"></a><span data-ttu-id="9588d-115">Prise en main</span><span class="sxs-lookup"><span data-stu-id="9588d-115">Get started</span></span>

<span data-ttu-id="9588d-116">La première étape consiste à utiliser PowerShell pour vous connecter à votre compte Azure et à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="9588d-116">The first step is to use PowerShell to log in to your Azure account and Azure subscription.</span></span> <span data-ttu-id="9588d-117">Suivez les instructions décrites dans [Prise en main des applets de commande Azure PowerShell](/powershell/azure/get-started-azureps) pour vous connecter à votre compte Azure, puis récupérez les ressources de votre abonnement Azure et accédez à celles-ci.</span><span class="sxs-lookup"><span data-stu-id="9588d-117">Follow the instructions in [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps) to log in to your Azure account, then retrieve and access the resources in your Azure subscription.</span></span>

## <a name="provision-an-event-hubs-namespace"></a><span data-ttu-id="9588d-118">Approvisionner un espace de noms Event Hubs</span><span class="sxs-lookup"><span data-stu-id="9588d-118">Provision an Event Hubs namespace</span></span>

<span data-ttu-id="9588d-119">Lorsque vous travaillez avec des espaces de noms Event Hubs, vous pouvez utiliser les applets de commande [Get-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/get-azurermeventhubnamespace), [New-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/new-azurermeventhubnamespace), [Remove-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/remove-azurermeventhubnamespace) et [Set-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/set-azurermeventhubnamespace).</span><span class="sxs-lookup"><span data-stu-id="9588d-119">When working with Event Hubs namespaces, you can use the [Get-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/get-azurermeventhubnamespace), [New-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/new-azurermeventhubnamespace), [Remove-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/remove-azurermeventhubnamespace), and [Set-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/set-azurermeventhubnamespace) cmdlets.</span></span>

<span data-ttu-id="9588d-120">Cet exemple crée quelques variables locales dans le script ; `$Namespace` et `$Location`.</span><span class="sxs-lookup"><span data-stu-id="9588d-120">This example creates a few local variables in the script; `$Namespace` and `$Location`.</span></span>

* <span data-ttu-id="9588d-121">`$Namespace` est le nom de l’espace de noms Event Hubs que nous allons utiliser.</span><span class="sxs-lookup"><span data-stu-id="9588d-121">`$Namespace` is the name of the Event Hubs namespace with which we want to work.</span></span>
* <span data-ttu-id="9588d-122">`$Location` identifie le centre de données dans lequel nous allons approvisionner l'espace de noms.</span><span class="sxs-lookup"><span data-stu-id="9588d-122">`$Location` identifies the data center in which will we provision the namespace.</span></span>
* <span data-ttu-id="9588d-123">`$CurrentNamespace` stocke l'espace de noms de référence récupéré (ou créé).</span><span class="sxs-lookup"><span data-stu-id="9588d-123">`$CurrentNamespace` stores the reference namespace that we retrieve (or create).</span></span>

<span data-ttu-id="9588d-124">Dans un script réel, les variables `$Namespace` et `$Location` peuvent être transmises en tant que paramètres.</span><span class="sxs-lookup"><span data-stu-id="9588d-124">In an actual script, `$Namespace` and `$Location` can be passed as parameters.</span></span>

<span data-ttu-id="9588d-125">Cette partie du script effectue les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="9588d-125">This part of the script does the following:</span></span>

1. <span data-ttu-id="9588d-126">Il tente de récupérer un espace de noms Event Hubs portant le nom spécifié.</span><span class="sxs-lookup"><span data-stu-id="9588d-126">Attempts to retrieve an Event Hubs namespace with the specified name.</span></span>
2. <span data-ttu-id="9588d-127">S'il trouve l'espace de noms recherché, il signale qu'il l'a trouvé.</span><span class="sxs-lookup"><span data-stu-id="9588d-127">If the namespace is found, it reports what was found.</span></span>
3. <span data-ttu-id="9588d-128">S'il ne trouve pas l'espace de noms recherché, il le crée, puis il récupère le nouvel espace de noms.</span><span class="sxs-lookup"><span data-stu-id="9588d-128">If the namespace is not found, it creates the namespace and then retrieves the newly created namespace.</span></span>

    ```powershell
    # Query to see if the namespace currently exists
    $CurrentNamespace = Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
   
    # Check if the namespace already exists or needs to be created
    if ($CurrentNamespace)
    {
        Write-Host "The namespace $Namespace already exists in the $Location region:"
        # Report what was found
        Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
    }
    else
    {
        Write-Host "The $Namespace namespace does not exist."
        Write-Host "Creating the $Namespace namespace in the $Location region..."
        New-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace -Location $Location
        $CurrentNamespace = Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
        Write-Host "The $Namespace namespace in Resource Group $ResGrpName in the $Location region has been successfully created."
    }
    ```

## <a name="create-an-event-hub"></a><span data-ttu-id="9588d-129">Création d'un concentrateur d'événements</span><span class="sxs-lookup"><span data-stu-id="9588d-129">Create an event hub</span></span>

<span data-ttu-id="9588d-130">Pour créer un concentrateur d’événements, vérifiez l’espace de noms à l’aide du script décrit dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="9588d-130">To create an event hub, perform a namespace check using the script in the previous section.</span></span> <span data-ttu-id="9588d-131">Ensuite, utilisez l’applet de commande [New-AzureRmEventHub](/powershell/module/azurerm.eventhub/new-azurermeventhub) pour créer le concentrateur d’événements :</span><span class="sxs-lookup"><span data-stu-id="9588d-131">Then, use the [New-AzureRmEventHub](/powershell/module/azurerm.eventhub/new-azurermeventhub) cmdlet to create the event hub:</span></span>

```powershell
# Check if event hub already exists
$CurrentEH = Get-AzureRMEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName

if($CurrentEH)
{
    Write-Host "The event hub $EventHubName already exists in the $Location region:"
    # Report what was found
    Get-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
}
else
{
    Write-Host "The $EventHubName event hub does not exist."
    Write-Host "Creating the $EventHubName event hub in the $Location region..."
    New-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -Location $Location -MessageRetentionInDays 3
    $CurrentEH = Get-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
    Write-Host "The $EventHubName event hub in Resource Group $ResGrpName in the $Location region has been successfully created."
}
```

### <a name="create-a-consumer-group"></a><span data-ttu-id="9588d-132">Créer un groupe de consommateurs</span><span class="sxs-lookup"><span data-stu-id="9588d-132">Create a consumer group</span></span>

<span data-ttu-id="9588d-133">Pour créer un groupe de consommateurs au sein d’un concentrateur d’événements, vérifiez l’espace de noms et l’instance Event Hub à l’aide des scripts de la section précédente.</span><span class="sxs-lookup"><span data-stu-id="9588d-133">To create a consumer group within an event hub, perform the namespace and event hub checks using the scripts in the previous section.</span></span> <span data-ttu-id="9588d-134">Ensuite, utilisez l’applet de commande [New-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/new-azurermeventhubconsumergroup) pour créer le groupe de consommateurs dans le concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="9588d-134">Then, use the [New-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/new-azurermeventhubconsumergroup) cmdlet to create the consumer group within the event hub.</span></span> <span data-ttu-id="9588d-135">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="9588d-135">For example:</span></span>

```powershell
# Check if consumer group already exists
$CurrentCG = Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -ErrorAction Ignore

if($CurrentCG)
{
    Write-Host "The consumer group $ConsumerGroupName in event hub $EventHubName already exists in the $Location region:"
    # Report what was found
    Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
}
else
{
    Write-Host "The $ConsumerGroupName consumer group does not exist."
    Write-Host "Creating the $ConsumerGroupName consumer group in the $Location region..."
    New-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
    $CurrentCG = Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
    Write-Host "The $ConsumerGroupName consumer group in event hub $EventHubName in Resource Group $ResGrpName in the $Location region has been successfully created."
}
```

#### <a name="set-user-metadata"></a><span data-ttu-id="9588d-136">Définir les métadonnées utilisateur</span><span class="sxs-lookup"><span data-stu-id="9588d-136">Set user metadata</span></span>

<span data-ttu-id="9588d-137">Après avoir exécuté les scripts des sections précédentes, vous pourrez utiliser l’applet de commande [Set-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/set-azurermeventhubconsumergroup) pour mettre à jour les propriétés d’un groupe de consommateurs, comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="9588d-137">After executing the scripts in the preceding sections, you can use the [Set-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/set-azurermeventhubconsumergroup) cmdlet to update the properties of a consumer group, as in the following example:</span></span>

```powershell
# Set some user metadata on the CG
Write-Host "Setting the UserMetadata field to 'Testing'"
Set-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -UserMetadata "Testing"
# Show result
Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
```

## <a name="remove-event-hub"></a><span data-ttu-id="9588d-138">Supprimer un concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="9588d-138">Remove event hub</span></span>

<span data-ttu-id="9588d-139">Pour supprimer les concentrateur d’événements que vous avez créés, vous pouvez utiliser les applets de commande `Remove-*`, comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="9588d-139">To remove the event hubs you created, you can use the `Remove-*` cmdlets, as in the following example:</span></span>

```powershell
# Clean up
Remove-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
Remove-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
Remove-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
```

## <a name="next-steps"></a><span data-ttu-id="9588d-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9588d-140">Next steps</span></span>

- <span data-ttu-id="9588d-141">Consultez la documentation complète du module PowerShell du Gestionnaire de ressources Event Hubs [ici](/powershell/module/azurerm.eventhub).</span><span class="sxs-lookup"><span data-stu-id="9588d-141">See the complete Event Hubs Resource Manager PowerShell module documentation [here](/powershell/module/azurerm.eventhub).</span></span> <span data-ttu-id="9588d-142">Cette page liste toutes les applets de commande disponibles.</span><span class="sxs-lookup"><span data-stu-id="9588d-142">This page lists all available cmdlets.</span></span>
- <span data-ttu-id="9588d-143">Pour plus d’informations sur les modèles Azure Resource Manager, consultez l’article [Créer un espace de noms Event Hubs avec Event Hub et un groupe de consommateurs à l’aide d’un modèle Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub.md).</span><span class="sxs-lookup"><span data-stu-id="9588d-143">For information about using Azure Resource Manager templates, see the article [Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub.md).</span></span>
- <span data-ttu-id="9588d-144">Informations sur les [bibliothèques de gestion .NET Event Hubs](event-hubs-management-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="9588d-144">Information about [Event Hubs .NET management libraries](event-hubs-management-libraries.md).</span></span>

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
