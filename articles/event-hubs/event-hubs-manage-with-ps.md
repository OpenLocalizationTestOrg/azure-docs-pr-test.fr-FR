---
title: "ressources d’Azure Event Hubs aaaUse PowerShell toomanage | Documents Microsoft"
description: "Utilisez PowerShell module toocreate et gérer les Hubs d’événements"
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
ms.openlocfilehash: d79cb307c2b4a031d059ce6ca67117ffc0b4600b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomanage-event-hubs-resources"></a><span data-ttu-id="186ce-103">Utiliser les ressources de concentrateurs d’événements toomanage PowerShell</span><span class="sxs-lookup"><span data-stu-id="186ce-103">Use PowerShell toomanage Event Hubs resources</span></span>

<span data-ttu-id="186ce-104">Microsoft Azure PowerShell est un environnement de script que vous pouvez utiliser toocontrol et automatiser le déploiement de hello et la gestion des services Azure.</span><span class="sxs-lookup"><span data-stu-id="186ce-104">Microsoft Azure PowerShell is a scripting environment that you can use toocontrol and automate hello deployment and management of Azure services.</span></span> <span data-ttu-id="186ce-105">Cet article décrit comment toouse hello [module PowerShell de gestionnaire de ressources de concentrateurs événement](/powershell/module/azurerm.eventhub) tooprovision et de gérer les entités de concentrateurs d’événements (espaces de noms, les concentrateurs d’événements individuels et les groupes de consommateurs) à l’aide d’une console Azure PowerShell locale ou script.</span><span class="sxs-lookup"><span data-stu-id="186ce-105">This article describes how toouse hello [Event Hubs Resource Manager PowerShell module](/powershell/module/azurerm.eventhub) tooprovision and manage Event Hubs entities (namespaces, individual event hubs, and consumer groups) using a local Azure PowerShell console or script.</span></span>

<span data-ttu-id="186ce-106">Vous pouvez également gérer les ressources Event Hubs avec des modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="186ce-106">You can also manage Event Hubs resources using Azure Resource Manager templates.</span></span> <span data-ttu-id="186ce-107">Pour plus d’informations, voir l’article hello [créer un espace de noms de concentrateurs d’événements avec le groupe d’événements concentrateur et le consommateur à l’aide d’un modèle Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub.md).</span><span class="sxs-lookup"><span data-stu-id="186ce-107">For more information, see hello article [Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="186ce-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="186ce-108">Prerequisites</span></span>

<span data-ttu-id="186ce-109">Avant de commencer, vous devez suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="186ce-109">Before you begin, you'll need hello following:</span></span>

* <span data-ttu-id="186ce-110">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="186ce-110">An Azure subscription.</span></span> <span data-ttu-id="186ce-111">Pour plus d’informations sur la façon de se procurer un abonnement, consultez les [options d’achat][purchase options], les [offres spéciales membres][member offers] ou découvrez comment créer un [compte gratuit][free account].</span><span class="sxs-lookup"><span data-stu-id="186ce-111">For more information about obtaining a subscription, see [purchase options][purchase options], [member offers][member offers], or [free account][free account].</span></span>
* <span data-ttu-id="186ce-112">Un ordinateur sur lequel est installé Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="186ce-112">A computer with Azure PowerShell.</span></span> <span data-ttu-id="186ce-113">Pour obtenir des instructions, consultez la page [Bien démarrer avec les applets de commande Azure PowerShell](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="186ce-113">For instructions, see [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps).</span></span>
* <span data-ttu-id="186ce-114">Une compréhension générale de scripts PowerShell, les packages NuGet et hello .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="186ce-114">A general understanding of PowerShell scripts, NuGet packages, and hello .NET Framework.</span></span>

## <a name="get-started"></a><span data-ttu-id="186ce-115">Prise en main</span><span class="sxs-lookup"><span data-stu-id="186ce-115">Get started</span></span>

<span data-ttu-id="186ce-116">première étape de Hello est toolog de PowerShell toouse dans tooyour compte Azure et d’abonnement Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="186ce-116">hello first step is toouse PowerShell toolog in tooyour Azure account and Azure subscription.</span></span> <span data-ttu-id="186ce-117">Suivez les instructions de hello dans [prise en main des applets de commande Azure PowerShell](/powershell/azure/get-started-azureps) toolog dans tooyour compte Azure, puis récupérer et accéder aux ressources hello dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="186ce-117">Follow hello instructions in [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps) toolog in tooyour Azure account, then retrieve and access hello resources in your Azure subscription.</span></span>

## <a name="provision-an-event-hubs-namespace"></a><span data-ttu-id="186ce-118">Approvisionner un espace de noms Event Hubs</span><span class="sxs-lookup"><span data-stu-id="186ce-118">Provision an Event Hubs namespace</span></span>

<span data-ttu-id="186ce-119">Lorsque vous travaillez avec des espaces de noms de concentrateurs d’événements, vous pouvez utiliser hello [Get-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/get-azurermeventhubnamespace), [New-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/new-azurermeventhubnamespace), [Remove-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/remove-azurermeventhubnamespace) , et [Set-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/set-azurermeventhubnamespace) applets de commande.</span><span class="sxs-lookup"><span data-stu-id="186ce-119">When working with Event Hubs namespaces, you can use hello [Get-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/get-azurermeventhubnamespace), [New-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/new-azurermeventhubnamespace), [Remove-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/remove-azurermeventhubnamespace), and [Set-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/set-azurermeventhubnamespace) cmdlets.</span></span>

<span data-ttu-id="186ce-120">Cet exemple crée quelques variables locales dans le script de hello ; `$Namespace` et `$Location`.</span><span class="sxs-lookup"><span data-stu-id="186ce-120">This example creates a few local variables in hello script; `$Namespace` and `$Location`.</span></span>

* <span data-ttu-id="186ce-121">`$Namespace`est le nom hello d’espace de noms de concentrateurs d’événements hello avec lequel nous souhaitons toowork.</span><span class="sxs-lookup"><span data-stu-id="186ce-121">`$Namespace` is hello name of hello Event Hubs namespace with which we want toowork.</span></span>
* <span data-ttu-id="186ce-122">`$Location`identifie le centre de données hello dans lequel nous configurera hello espace de noms.</span><span class="sxs-lookup"><span data-stu-id="186ce-122">`$Location` identifies hello data center in which will we provision hello namespace.</span></span>
* <span data-ttu-id="186ce-123">`$CurrentNamespace`stocke l’espace de noms hello référence nous récupérer (ou créer).</span><span class="sxs-lookup"><span data-stu-id="186ce-123">`$CurrentNamespace` stores hello reference namespace that we retrieve (or create).</span></span>

<span data-ttu-id="186ce-124">Dans un script réel, les variables `$Namespace` et `$Location` peuvent être transmises en tant que paramètres.</span><span class="sxs-lookup"><span data-stu-id="186ce-124">In an actual script, `$Namespace` and `$Location` can be passed as parameters.</span></span>

<span data-ttu-id="186ce-125">Cette partie du script de hello hello suivant :</span><span class="sxs-lookup"><span data-stu-id="186ce-125">This part of hello script does hello following:</span></span>

1. <span data-ttu-id="186ce-126">Tentatives tooretrieve concentrateurs d’événements d’un espace de noms avec hello spécifié de nom.</span><span class="sxs-lookup"><span data-stu-id="186ce-126">Attempts tooretrieve an Event Hubs namespace with hello specified name.</span></span>
2. <span data-ttu-id="186ce-127">Si l’espace de noms hello est trouvé, il signale ce qui a été trouvé.</span><span class="sxs-lookup"><span data-stu-id="186ce-127">If hello namespace is found, it reports what was found.</span></span>
3. <span data-ttu-id="186ce-128">Si l’espace de noms hello n’est trouvé, il crée l’espace de noms hello, puis récupère hello nouvellement créé espace de noms.</span><span class="sxs-lookup"><span data-stu-id="186ce-128">If hello namespace is not found, it creates hello namespace and then retrieves hello newly created namespace.</span></span>

    ```powershell
    # Query toosee if hello namespace currently exists
    $CurrentNamespace = Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
   
    # Check if hello namespace already exists or needs toobe created
    if ($CurrentNamespace)
    {
        Write-Host "hello namespace $Namespace already exists in hello $Location region:"
        # Report what was found
        Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
    }
    else
    {
        Write-Host "hello $Namespace namespace does not exist."
        Write-Host "Creating hello $Namespace namespace in hello $Location region..."
        New-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace -Location $Location
        $CurrentNamespace = Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
        Write-Host "hello $Namespace namespace in Resource Group $ResGrpName in hello $Location region has been successfully created."
    }
    ```

## <a name="create-an-event-hub"></a><span data-ttu-id="186ce-129">Création d'un concentrateur d'événements</span><span class="sxs-lookup"><span data-stu-id="186ce-129">Create an event hub</span></span>

<span data-ttu-id="186ce-130">toocreate un concentrateur d’événements, effectuer une vérification de l’espace de noms à l’aide du script de hello dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="186ce-130">toocreate an event hub, perform a namespace check using hello script in hello previous section.</span></span> <span data-ttu-id="186ce-131">Ensuite, utilisez hello [New-AzureRmEventHub](/powershell/module/azurerm.eventhub/new-azurermeventhub) concentrateur d’événements d’applet de commande toocreate hello :</span><span class="sxs-lookup"><span data-stu-id="186ce-131">Then, use hello [New-AzureRmEventHub](/powershell/module/azurerm.eventhub/new-azurermeventhub) cmdlet toocreate hello event hub:</span></span>

```powershell
# Check if event hub already exists
$CurrentEH = Get-AzureRMEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName

if($CurrentEH)
{
    Write-Host "hello event hub $EventHubName already exists in hello $Location region:"
    # Report what was found
    Get-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
}
else
{
    Write-Host "hello $EventHubName event hub does not exist."
    Write-Host "Creating hello $EventHubName event hub in hello $Location region..."
    New-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -Location $Location -MessageRetentionInDays 3
    $CurrentEH = Get-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
    Write-Host "hello $EventHubName event hub in Resource Group $ResGrpName in hello $Location region has been successfully created."
}
```

### <a name="create-a-consumer-group"></a><span data-ttu-id="186ce-132">Créer un groupe de consommateurs</span><span class="sxs-lookup"><span data-stu-id="186ce-132">Create a consumer group</span></span>

<span data-ttu-id="186ce-133">toocreate un groupe de consommateurs dans un concentrateur d’événements, vérification hello espace de noms et les événements concentrateur à l’aide de scripts de hello dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="186ce-133">toocreate a consumer group within an event hub, perform hello namespace and event hub checks using hello scripts in hello previous section.</span></span> <span data-ttu-id="186ce-134">Ensuite, utilisez hello [New-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/new-azurermeventhubconsumergroup) groupe de consommateurs toocreate hello applet de commande dans le concentrateur d’événements hello.</span><span class="sxs-lookup"><span data-stu-id="186ce-134">Then, use hello [New-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/new-azurermeventhubconsumergroup) cmdlet toocreate hello consumer group within hello event hub.</span></span> <span data-ttu-id="186ce-135">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="186ce-135">For example:</span></span>

```powershell
# Check if consumer group already exists
$CurrentCG = Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -ErrorAction Ignore

if($CurrentCG)
{
    Write-Host "hello consumer group $ConsumerGroupName in event hub $EventHubName already exists in hello $Location region:"
    # Report what was found
    Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
}
else
{
    Write-Host "hello $ConsumerGroupName consumer group does not exist."
    Write-Host "Creating hello $ConsumerGroupName consumer group in hello $Location region..."
    New-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
    $CurrentCG = Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
    Write-Host "hello $ConsumerGroupName consumer group in event hub $EventHubName in Resource Group $ResGrpName in hello $Location region has been successfully created."
}
```

#### <a name="set-user-metadata"></a><span data-ttu-id="186ce-136">Définir les métadonnées utilisateur</span><span class="sxs-lookup"><span data-stu-id="186ce-136">Set user metadata</span></span>

<span data-ttu-id="186ce-137">Après l’exécution de scripts de hello Bonjour sections précédentes, vous pouvez utiliser hello [Set-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/set-azurermeventhubconsumergroup) propriétés de hello tooupdate applet de commande d’un groupe de consommateurs, comme dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="186ce-137">After executing hello scripts in hello preceding sections, you can use hello [Set-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/set-azurermeventhubconsumergroup) cmdlet tooupdate hello properties of a consumer group, as in hello following example:</span></span>

```powershell
# Set some user metadata on hello CG
Write-Host "Setting hello UserMetadata field too'Testing'"
Set-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -UserMetadata "Testing"
# Show result
Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
```

## <a name="remove-event-hub"></a><span data-ttu-id="186ce-138">Supprimer un concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="186ce-138">Remove event hub</span></span>

<span data-ttu-id="186ce-139">concentrateurs d’événements hello tooremove vous avez créé, vous pouvez utiliser hello `Remove-*` applets de commande, comme dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="186ce-139">tooremove hello event hubs you created, you can use hello `Remove-*` cmdlets, as in hello following example:</span></span>

```powershell
# Clean up
Remove-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
Remove-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
Remove-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
```

## <a name="next-steps"></a><span data-ttu-id="186ce-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="186ce-140">Next steps</span></span>

- <span data-ttu-id="186ce-141">Consultez la documentation du module hello complète événement concentrateurs Resource Manager PowerShell [ici](/powershell/module/azurerm.eventhub).</span><span class="sxs-lookup"><span data-stu-id="186ce-141">See hello complete Event Hubs Resource Manager PowerShell module documentation [here](/powershell/module/azurerm.eventhub).</span></span> <span data-ttu-id="186ce-142">Cette page liste toutes les applets de commande disponibles.</span><span class="sxs-lookup"><span data-stu-id="186ce-142">This page lists all available cmdlets.</span></span>
- <span data-ttu-id="186ce-143">Pour plus d’informations sur l’utilisation de modèles Azure Resource Manager, voir l’article hello [créer un espace de noms de concentrateurs d’événements avec le groupe d’événements concentrateur et le consommateur à l’aide d’un modèle Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub.md).</span><span class="sxs-lookup"><span data-stu-id="186ce-143">For information about using Azure Resource Manager templates, see hello article [Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub.md).</span></span>
- <span data-ttu-id="186ce-144">Informations sur les [bibliothèques de gestion .NET Event Hubs](event-hubs-management-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="186ce-144">Information about [Event Hubs .NET management libraries](event-hubs-management-libraries.md).</span></span>

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
