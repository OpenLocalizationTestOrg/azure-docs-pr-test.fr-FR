---
title: "ressources d’Azure Service Bus aaaUse PowerShell toomanage | Documents Microsoft"
description: "Utilisez PowerShell module toocreate et gérer les ressources de Service Bus"
services: service-bus-messaging
documentationcenter: .NET
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/06/2017
ms.author: sethm
ms.openlocfilehash: 737044def913c5798e7e05fc4f1aeece76c8f4dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomanage-service-bus-resources"></a><span data-ttu-id="fded2-103">Utiliser les ressources de Service Bus PowerShell toomanage</span><span class="sxs-lookup"><span data-stu-id="fded2-103">Use PowerShell toomanage Service Bus resources</span></span>

<span data-ttu-id="fded2-104">Microsoft Azure PowerShell est un environnement de script que vous pouvez utiliser toocontrol et automatiser le déploiement de hello et la gestion des services Azure.</span><span class="sxs-lookup"><span data-stu-id="fded2-104">Microsoft Azure PowerShell is a scripting environment that you can use toocontrol and automate hello deployment and management of Azure services.</span></span> <span data-ttu-id="fded2-105">Cet article décrit comment toouse hello [module PowerShell de gestionnaire de ressources du Service Bus](/powershell/module/azurerm.servicebus) tooprovision et gérer des entités Service Bus (espaces de noms, les files d’attente, rubriques et abonnements) à l’aide d’une console Azure PowerShell locale ou script.</span><span class="sxs-lookup"><span data-stu-id="fded2-105">This article describes how toouse hello [Service Bus Resource Manager PowerShell module](/powershell/module/azurerm.servicebus) tooprovision and manage Service Bus entities (namespaces, queues, topics, and subscriptions) using a local Azure PowerShell console or script.</span></span>

<span data-ttu-id="fded2-106">Vous pouvez également gérer les entités Service Bus à l’aide de modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fded2-106">You can also manage Service Bus entities using Azure Resource Manager templates.</span></span> <span data-ttu-id="fded2-107">Pour plus d’informations, voir l’article hello [ressources créez Service Bus à l’aide de modèles Azure Resource Manager](service-bus-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fded2-107">For more information, see hello article [Create Service Bus resources using Azure Resource Manager templates](service-bus-resource-manager-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fded2-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="fded2-108">Prerequisites</span></span>

<span data-ttu-id="fded2-109">Avant de commencer, vous devez suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="fded2-109">Before you begin, you'll need hello following:</span></span>

* <span data-ttu-id="fded2-110">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="fded2-110">An Azure subscription.</span></span> <span data-ttu-id="fded2-111">Pour plus d’informations sur la façon de se procurer un abonnement, consultez les [options d’achat][purchase options], les [offres spéciales membres][member offers] ou découvrez comment créer un [compte gratuit][free account].</span><span class="sxs-lookup"><span data-stu-id="fded2-111">For more information about obtaining a subscription, see [purchase options][purchase options], [member offers][member offers], or [free account][free account].</span></span>
* <span data-ttu-id="fded2-112">Un ordinateur sur lequel est installé Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fded2-112">A computer with Azure PowerShell.</span></span> <span data-ttu-id="fded2-113">Pour obtenir des instructions, consultez la page [Bien démarrer avec les applets de commande Azure PowerShell](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="fded2-113">For instructions, see [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps).</span></span>
* <span data-ttu-id="fded2-114">Une compréhension générale de scripts PowerShell, les packages NuGet et hello .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="fded2-114">A general understanding of PowerShell scripts, NuGet packages, and hello .NET Framework.</span></span>

## <a name="get-started"></a><span data-ttu-id="fded2-115">Prise en main</span><span class="sxs-lookup"><span data-stu-id="fded2-115">Get started</span></span>

<span data-ttu-id="fded2-116">première étape de Hello est toolog de PowerShell toouse dans tooyour compte Azure et d’abonnement Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="fded2-116">hello first step is toouse PowerShell toolog in tooyour Azure account and Azure subscription.</span></span> <span data-ttu-id="fded2-117">Suivez les instructions de hello dans [prise en main des applets de commande Azure PowerShell](/powershell/azure/get-started-azureps) toolog dans tooyour compte Azure et de récupérer et accès aux ressources de hello dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="fded2-117">Follow hello instructions in [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps) toolog in tooyour Azure account, and retrieve and access hello resources in your Azure subscription.</span></span>

## <a name="provision-a-service-bus-namespace"></a><span data-ttu-id="fded2-118">Approvisionner un espace de noms Service Bus</span><span class="sxs-lookup"><span data-stu-id="fded2-118">Provision a Service Bus namespace</span></span>

<span data-ttu-id="fded2-119">Lorsque vous travaillez avec des espaces de noms Service Bus, vous pouvez utiliser hello [Get-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace), [New-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace), [Remove-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace), et [Set-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace) applets de commande.</span><span class="sxs-lookup"><span data-stu-id="fded2-119">When working with Service Bus namespaces, you can use hello [Get-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace), [New-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace), [Remove-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace), and [Set-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace) cmdlets.</span></span>

<span data-ttu-id="fded2-120">Cet exemple crée quelques variables locales dans le script de hello ; `$Namespace` et `$Location`.</span><span class="sxs-lookup"><span data-stu-id="fded2-120">This example creates a few local variables in hello script; `$Namespace` and `$Location`.</span></span>

* <span data-ttu-id="fded2-121">`$Namespace`est le nom hello d’espace de noms Service Bus hello avec lequel nous souhaitons toowork.</span><span class="sxs-lookup"><span data-stu-id="fded2-121">`$Namespace` is hello name of hello Service Bus namespace with which we want toowork.</span></span>
* <span data-ttu-id="fded2-122">`$Location`identifie le centre de données hello dans lequel nous configurera hello espace de noms.</span><span class="sxs-lookup"><span data-stu-id="fded2-122">`$Location` identifies hello data center in which will we provision hello namespace.</span></span>
* <span data-ttu-id="fded2-123">`$CurrentNamespace`stocke l’espace de noms hello référence nous récupérer (ou créer).</span><span class="sxs-lookup"><span data-stu-id="fded2-123">`$CurrentNamespace` stores hello reference namespace that we retrieve (or create).</span></span>

<span data-ttu-id="fded2-124">Dans un script réel, les variables `$Namespace` et `$Location` peuvent être transmises en tant que paramètres.</span><span class="sxs-lookup"><span data-stu-id="fded2-124">In an actual script, `$Namespace` and `$Location` can be passed as parameters.</span></span>

<span data-ttu-id="fded2-125">Cette partie du script de hello hello suivant :</span><span class="sxs-lookup"><span data-stu-id="fded2-125">This part of hello script does hello following:</span></span>

1. <span data-ttu-id="fded2-126">Nom spécifié par les tentatives tooretrieve un espace de noms Service Bus avec hello.</span><span class="sxs-lookup"><span data-stu-id="fded2-126">Attempts tooretrieve a Service Bus namespace with hello specified name.</span></span>
2. <span data-ttu-id="fded2-127">Si l’espace de noms hello est trouvé, il signale ce qui a été trouvé.</span><span class="sxs-lookup"><span data-stu-id="fded2-127">If hello namespace is found, it reports what was found.</span></span>
3. <span data-ttu-id="fded2-128">Si l’espace de noms hello n’est trouvé, il crée l’espace de noms hello, puis récupère hello nouvellement créé espace de noms.</span><span class="sxs-lookup"><span data-stu-id="fded2-128">If hello namespace is not found, it creates hello namespace and then retrieves hello newly created namespace.</span></span>
   
    ``` powershell
    # Query toosee if hello namespace currently exists
    $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
   
    # Check if hello namespace already exists or needs toobe created
    if ($CurrentNamespace)
    {
        Write-Host "hello namespace $Namespace already exists in hello $Location region:"
        # Report what was found
        Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
    }
    else
    {
        Write-Host "hello $Namespace namespace does not exist."
        Write-Host "Creating hello $Namespace namespace in hello $Location region..."
        New-AzureRmServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace -Location $Location
        $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
        Write-Host "hello $Namespace namespace in Resource Group $ResGrpName in hello $Location region has been successfully created."
                
    }
    ```

### <a name="create-a-namespace-authorization-rule"></a><span data-ttu-id="fded2-129">Créer une règle d’autorisation d’espace de noms</span><span class="sxs-lookup"><span data-stu-id="fded2-129">Create a namespace authorization rule</span></span>

<span data-ttu-id="fded2-130">Hello suivant montre comment les règles d’autorisation de toomanage espace de noms à l’aide de hello [New-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule), [Get-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule), [Set-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule), et [applets de commande Remove-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule).</span><span class="sxs-lookup"><span data-stu-id="fded2-130">hello following example shows how toomanage namespace authorization rules using hello [New-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule), [Get-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule), [Set-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule), and [Remove-AzureRmServiceBusNamespaceAuthorizationRule cmdlets](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule).</span></span>

```powershell
# Query toosee if rule exists
$CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

# Check if hello rule already exists or needs toobe created
if ($CurrentRule)
{
    Write-Host "hello $AuthRule rule already exists for hello namespace $Namespace."
}
else
{
    Write-Host "hello $AuthRule rule does not exist."
    Write-Host "Creating hello $AuthRule rule for hello $Namespace namespace..."
    New-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule -Rights @("Listen","Send")
    $CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
    Write-Host "hello $AuthRule rule for hello $Namespace namespace has been successfully created."

    Write-Host "Setting rights on hello namespace"
    $authRuleObj = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

    Write-Host "Remove Send rights"
    $authRuleObj.Rights.Remove("Send")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj

    Write-Host "Add Send and Manage rights toohello namespace"
    $authRuleObj.Rights.Add("Send")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj
    $authRuleObj.Rights.Add("Manage")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj

    Write-Host "Show value of primary key"
    $CurrentKey = Get-AzureRmServiceBusNamespaceKey -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
        
    Write-Host "Remove this authorization rule"
    Remove-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
}
```

## <a name="create-a-queue"></a><span data-ttu-id="fded2-131">Création d’une file d’attente</span><span class="sxs-lookup"><span data-stu-id="fded2-131">Create a queue</span></span>

<span data-ttu-id="fded2-132">toocreate une file d’attente ou rubrique, effectuer une vérification de l’espace de noms à l’aide du script de hello dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="fded2-132">toocreate a queue or topic, perform a namespace check using hello script in hello previous section.</span></span> <span data-ttu-id="fded2-133">Ensuite, créez la file d’attente de hello :</span><span class="sxs-lookup"><span data-stu-id="fded2-133">Then, create hello queue:</span></span>

```powershell
# Check if queue already exists
$CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName

if($CurrentQ)
{
    Write-Host "hello queue $QueueName already exists in hello $Location region:"
}
else
{
    Write-Host "hello $QueueName queue does not exist."
    Write-Host "Creating hello $QueueName queue in hello $Location region..."
    New-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -EnablePartitioning $True
    $CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName
    Write-Host "hello $QueueName queue in Resource Group $ResGrpName in hello $Location region has been successfully created."
}
```

### <a name="modify-queue-properties"></a><span data-ttu-id="fded2-134">Modifier les propriétés de la file d’attente</span><span class="sxs-lookup"><span data-stu-id="fded2-134">Modify queue properties</span></span>

<span data-ttu-id="fded2-135">Après avoir exécuté le script de hello Bonjour précédant la section, vous pouvez utiliser hello [Set-AzureRmServiceBusQueue](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) propriétés de hello tooupdate applet de commande d’une file d’attente, comme dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="fded2-135">After executing hello script in hello preceding section, you can use hello [Set-AzureRmServiceBusQueue](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) cmdlet tooupdate hello properties of a queue, as in hello following example:</span></span>

```powershell
$CurrentQ.DeadLetteringOnMessageExpiration = $True
$CurrentQ.MaxDeliveryCount = 7
$CurrentQ.MaxSizeInMegabytes = 2048
$CurrentQ.EnableExpress = $True

Set-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -QueueObj $CurrentQ
```

## <a name="provisioning-other-service-bus-entities"></a><span data-ttu-id="fded2-136">Approvisionne d'autres entités Service Bus</span><span class="sxs-lookup"><span data-stu-id="fded2-136">Provisioning other Service Bus entities</span></span>

<span data-ttu-id="fded2-137">Vous pouvez utiliser hello [module PowerShell de Service Bus](/powershell/module/azurerm.servicebus) tooprovision autres entités, telles que des rubriques et abonnements.</span><span class="sxs-lookup"><span data-stu-id="fded2-137">You can use hello [Service Bus PowerShell module](/powershell/module/azurerm.servicebus) tooprovision other entities, such as topics and subscriptions.</span></span> <span data-ttu-id="fded2-138">Ces applets de commande sont syntaxiquement similaire cmdlets de création de file d’attente toohello illustrée dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="fded2-138">These cmdlets are syntactically similar toohello queue creation cmdlets demonstrated in hello previous section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fded2-139">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fded2-139">Next steps</span></span>

- <span data-ttu-id="fded2-140">Consultez la documentation de module Gestionnaire de ressources du Service Bus PowerShell complète hello [ici](/powershell/module/azurerm.servicebus).</span><span class="sxs-lookup"><span data-stu-id="fded2-140">See hello complete Service Bus Resource Manager PowerShell module documentation [here](/powershell/module/azurerm.servicebus).</span></span> <span data-ttu-id="fded2-141">Cette page liste toutes les applets de commande disponibles.</span><span class="sxs-lookup"><span data-stu-id="fded2-141">This page lists all available cmdlets.</span></span>
- <span data-ttu-id="fded2-142">Pour plus d’informations sur l’utilisation de modèles Azure Resource Manager, voir l’article hello [ressources créez Service Bus à l’aide de modèles Azure Resource Manager](service-bus-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fded2-142">For information about using Azure Resource Manager templates, see hello article [Create Service Bus resources using Azure Resource Manager templates](service-bus-resource-manager-overview.md).</span></span>
- <span data-ttu-id="fded2-143">Informations sur les [bibliothèques de gestion Service Bus .NET](service-bus-management-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="fded2-143">Information about [Service Bus .NET management libraries](service-bus-management-libraries.md).</span></span>

<span data-ttu-id="fded2-144">Voici quelques-unes des autres toomanage des entités Service Bus, comme décrit dans ces billets de blog :</span><span class="sxs-lookup"><span data-stu-id="fded2-144">There are some alternate ways toomanage Service Bus entities, as described in these blog posts:</span></span>

* [<span data-ttu-id="fded2-145">Comment toocreate Service Bus files d’attente, rubriques et abonnements à l’aide d’un script PowerShell</span><span class="sxs-lookup"><span data-stu-id="fded2-145">How toocreate Service Bus queues, topics and subscriptions using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [<span data-ttu-id="fded2-146">Comment toocreate un Service Bus Namespace et qu’un concentrateur d’événements à l’aide d’un script PowerShell</span><span class="sxs-lookup"><span data-stu-id="fded2-146">How toocreate a Service Bus Namespace and an Event Hub using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)
* [<span data-ttu-id="fded2-147">Scripts PowerShell pour Service Bus</span><span class="sxs-lookup"><span data-stu-id="fded2-147">Service Bus PowerShell Scripts</span></span>](https://code.msdn.microsoft.com/Service-Bus-PowerShell-a46b7059)

<!--Anchors-->

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
