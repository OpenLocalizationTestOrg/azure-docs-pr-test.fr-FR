---
title: "Utiliser PowerShell pour gérer les ressources Azure Service Bus | Microsoft Docs"
description: "Utiliser le module PowerShell pour créer et gérer les ressources Service Bus"
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
ms.openlocfilehash: 1205f9fcabf5788c970fbce257aa5ad04f32cddc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-manage-service-bus-resources"></a><span data-ttu-id="635d2-103">Utiliser PowerShell pour gérer les ressources Service Bus</span><span class="sxs-lookup"><span data-stu-id="635d2-103">Use PowerShell to manage Service Bus resources</span></span>

<span data-ttu-id="635d2-104">Microsoft Azure PowerShell est un environnement de création de scripts vous permettant de contrôler et d'automatiser le déploiement et la gestion des services Azure.</span><span class="sxs-lookup"><span data-stu-id="635d2-104">Microsoft Azure PowerShell is a scripting environment that you can use to control and automate the deployment and management of Azure services.</span></span> <span data-ttu-id="635d2-105">Cet article explique comment utiliser le [module PowerShell du Gestionnaire de ressources Service Bus](/powershell/module/azurerm.servicebus) pour approvisionner et gérer les entités Service Bus (espaces de noms, files d’attente, rubriques et abonnements) à l’aide d’une console Azure PowerShell locale ou d’un script.</span><span class="sxs-lookup"><span data-stu-id="635d2-105">This article describes how to use the [Service Bus Resource Manager PowerShell module](/powershell/module/azurerm.servicebus) to provision and manage Service Bus entities (namespaces, queues, topics, and subscriptions) using a local Azure PowerShell console or script.</span></span>

<span data-ttu-id="635d2-106">Vous pouvez également gérer les entités Service Bus à l’aide de modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="635d2-106">You can also manage Service Bus entities using Azure Resource Manager templates.</span></span> <span data-ttu-id="635d2-107">Pour plus d’informations, consultez l’article [Création de ressources Service Bus à l’aide de modèles Azure Resource Manager](service-bus-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="635d2-107">For more information, see the article [Create Service Bus resources using Azure Resource Manager templates](service-bus-resource-manager-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="635d2-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="635d2-108">Prerequisites</span></span>

<span data-ttu-id="635d2-109">Avant de débuter, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="635d2-109">Before you begin, you'll need the following:</span></span>

* <span data-ttu-id="635d2-110">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="635d2-110">An Azure subscription.</span></span> <span data-ttu-id="635d2-111">Pour plus d’informations sur la façon de se procurer un abonnement, consultez les [options d’achat][purchase options], les [offres spéciales membres][member offers] ou découvrez comment créer un [compte gratuit][free account].</span><span class="sxs-lookup"><span data-stu-id="635d2-111">For more information about obtaining a subscription, see [purchase options][purchase options], [member offers][member offers], or [free account][free account].</span></span>
* <span data-ttu-id="635d2-112">Un ordinateur sur lequel est installé Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="635d2-112">A computer with Azure PowerShell.</span></span> <span data-ttu-id="635d2-113">Pour obtenir des instructions, consultez la page [Bien démarrer avec les applets de commande Azure PowerShell](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="635d2-113">For instructions, see [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps).</span></span>
* <span data-ttu-id="635d2-114">Des connaissances générales sur les scripts PowerShell, les packages NuGet et .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="635d2-114">A general understanding of PowerShell scripts, NuGet packages, and the .NET Framework.</span></span>

## <a name="get-started"></a><span data-ttu-id="635d2-115">Prise en main</span><span class="sxs-lookup"><span data-stu-id="635d2-115">Get started</span></span>

<span data-ttu-id="635d2-116">La première étape consiste à utiliser PowerShell pour vous connecter à votre compte Azure et à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="635d2-116">The first step is to use PowerShell to log in to your Azure account and Azure subscription.</span></span> <span data-ttu-id="635d2-117">Suivez les instructions décrites dans [Prise en main des applets de commande Azure PowerShell](/powershell/azure/get-started-azureps) pour vous connecter à votre compte Azure et récupérer les ressources de votre abonnement Azure ainsi qu’accéder à celles-ci.</span><span class="sxs-lookup"><span data-stu-id="635d2-117">Follow the instructions in [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps) to log in to your Azure account, and retrieve and access the resources in your Azure subscription.</span></span>

## <a name="provision-a-service-bus-namespace"></a><span data-ttu-id="635d2-118">Approvisionner un espace de noms Service Bus</span><span class="sxs-lookup"><span data-stu-id="635d2-118">Provision a Service Bus namespace</span></span>

<span data-ttu-id="635d2-119">Lorsque vous travaillez avec des espaces de noms Service Bus, vous pouvez utiliser les applets de commande [Get-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace), [New-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace), [Remove-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace) et [Set-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace).</span><span class="sxs-lookup"><span data-stu-id="635d2-119">When working with Service Bus namespaces, you can use the [Get-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace), [New-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace), [Remove-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace), and [Set-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace) cmdlets.</span></span>

<span data-ttu-id="635d2-120">Cet exemple crée quelques variables locales dans le script ; `$Namespace` et `$Location`.</span><span class="sxs-lookup"><span data-stu-id="635d2-120">This example creates a few local variables in the script; `$Namespace` and `$Location`.</span></span>

* <span data-ttu-id="635d2-121">`$Namespace` est le nom de l’espace de noms Service Bus que nous allons utiliser.</span><span class="sxs-lookup"><span data-stu-id="635d2-121">`$Namespace` is the name of the Service Bus namespace with which we want to work.</span></span>
* <span data-ttu-id="635d2-122">`$Location` identifie le centre de données dans lequel nous allons approvisionner l'espace de noms.</span><span class="sxs-lookup"><span data-stu-id="635d2-122">`$Location` identifies the data center in which will we provision the namespace.</span></span>
* <span data-ttu-id="635d2-123">`$CurrentNamespace` stocke l'espace de noms de référence récupéré (ou créé).</span><span class="sxs-lookup"><span data-stu-id="635d2-123">`$CurrentNamespace` stores the reference namespace that we retrieve (or create).</span></span>

<span data-ttu-id="635d2-124">Dans un script réel, les variables `$Namespace` et `$Location` peuvent être transmises en tant que paramètres.</span><span class="sxs-lookup"><span data-stu-id="635d2-124">In an actual script, `$Namespace` and `$Location` can be passed as parameters.</span></span>

<span data-ttu-id="635d2-125">Cette partie du script effectue les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="635d2-125">This part of the script does the following:</span></span>

1. <span data-ttu-id="635d2-126">Elle tente de récupérer un espace de noms Service Bus portant le nom spécifié.</span><span class="sxs-lookup"><span data-stu-id="635d2-126">Attempts to retrieve a Service Bus namespace with the specified name.</span></span>
2. <span data-ttu-id="635d2-127">S'il trouve l'espace de noms recherché, il signale qu'il l'a trouvé.</span><span class="sxs-lookup"><span data-stu-id="635d2-127">If the namespace is found, it reports what was found.</span></span>
3. <span data-ttu-id="635d2-128">S'il ne trouve pas l'espace de noms recherché, il le crée, puis il récupère le nouvel espace de noms.</span><span class="sxs-lookup"><span data-stu-id="635d2-128">If the namespace is not found, it creates the namespace and then retrieves the newly created namespace.</span></span>
   
    ``` powershell
    # Query to see if the namespace currently exists
    $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
   
    # Check if the namespace already exists or needs to be created
    if ($CurrentNamespace)
    {
        Write-Host "The namespace $Namespace already exists in the $Location region:"
        # Report what was found
        Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
    }
    else
    {
        Write-Host "The $Namespace namespace does not exist."
        Write-Host "Creating the $Namespace namespace in the $Location region..."
        New-AzureRmServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace -Location $Location
        $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
        Write-Host "The $Namespace namespace in Resource Group $ResGrpName in the $Location region has been successfully created."
                
    }
    ```

### <a name="create-a-namespace-authorization-rule"></a><span data-ttu-id="635d2-129">Créer une règle d’autorisation d’espace de noms</span><span class="sxs-lookup"><span data-stu-id="635d2-129">Create a namespace authorization rule</span></span>

<span data-ttu-id="635d2-130">L’exemple suivant montre comment gérer les règles d’autorisation d’espace de noms à l’aide des applets de commande [New-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule), [Get-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule), [Set-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule) et [applets de commande Remove-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule).</span><span class="sxs-lookup"><span data-stu-id="635d2-130">The following example shows how to manage namespace authorization rules using the [New-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule), [Get-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule), [Set-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule), and [Remove-AzureRmServiceBusNamespaceAuthorizationRule cmdlets](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule).</span></span>

```powershell
# Query to see if rule exists
$CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

# Check if the rule already exists or needs to be created
if ($CurrentRule)
{
    Write-Host "The $AuthRule rule already exists for the namespace $Namespace."
}
else
{
    Write-Host "The $AuthRule rule does not exist."
    Write-Host "Creating the $AuthRule rule for the $Namespace namespace..."
    New-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule -Rights @("Listen","Send")
    $CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
    Write-Host "The $AuthRule rule for the $Namespace namespace has been successfully created."

    Write-Host "Setting rights on the namespace"
    $authRuleObj = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

    Write-Host "Remove Send rights"
    $authRuleObj.Rights.Remove("Send")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj

    Write-Host "Add Send and Manage rights to the namespace"
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

## <a name="create-a-queue"></a><span data-ttu-id="635d2-131">Créer une file d’attente</span><span class="sxs-lookup"><span data-stu-id="635d2-131">Create a queue</span></span>

<span data-ttu-id="635d2-132">Pour créer une file d’attente ou une rubrique, vérifiez l’espace de noms à l’aide du script décrit dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="635d2-132">To create a queue or topic, perform a namespace check using the script in the previous section.</span></span> <span data-ttu-id="635d2-133">Ensuite, créez la file d’attente :</span><span class="sxs-lookup"><span data-stu-id="635d2-133">Then, create the queue:</span></span>

```powershell
# Check if queue already exists
$CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName

if($CurrentQ)
{
    Write-Host "The queue $QueueName already exists in the $Location region:"
}
else
{
    Write-Host "The $QueueName queue does not exist."
    Write-Host "Creating the $QueueName queue in the $Location region..."
    New-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -EnablePartitioning $True
    $CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName
    Write-Host "The $QueueName queue in Resource Group $ResGrpName in the $Location region has been successfully created."
}
```

### <a name="modify-queue-properties"></a><span data-ttu-id="635d2-134">Modifier les propriétés de la file d’attente</span><span class="sxs-lookup"><span data-stu-id="635d2-134">Modify queue properties</span></span>

<span data-ttu-id="635d2-135">Après l’exécution du script de la manière décrite dans la section précédente, vous pouvez utiliser l’applet de commande [Set-AzureRmServiceBusQueue](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) pour mettre à jour les propriétés d’une file d’attente, comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="635d2-135">After executing the script in the preceding section, you can use the [Set-AzureRmServiceBusQueue](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) cmdlet to update the properties of a queue, as in the following example:</span></span>

```powershell
$CurrentQ.DeadLetteringOnMessageExpiration = $True
$CurrentQ.MaxDeliveryCount = 7
$CurrentQ.MaxSizeInMegabytes = 2048
$CurrentQ.EnableExpress = $True

Set-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -QueueObj $CurrentQ
```

## <a name="provisioning-other-service-bus-entities"></a><span data-ttu-id="635d2-136">Approvisionne d'autres entités Service Bus</span><span class="sxs-lookup"><span data-stu-id="635d2-136">Provisioning other Service Bus entities</span></span>

<span data-ttu-id="635d2-137">Vous pouvez utiliser le [module PowerShell de Service Bus](/powershell/module/azurerm.servicebus) pour approvisionner d’autres entités, telles que des rubriques et abonnements.</span><span class="sxs-lookup"><span data-stu-id="635d2-137">You can use the [Service Bus PowerShell module](/powershell/module/azurerm.servicebus) to provision other entities, such as topics and subscriptions.</span></span> <span data-ttu-id="635d2-138">La syntaxe de ces applets de commande est similaire à celle des applets de commande de création de file d’attente décrites dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="635d2-138">These cmdlets are syntactically similar to the queue creation cmdlets demonstrated in the previous section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="635d2-139">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="635d2-139">Next steps</span></span>

- <span data-ttu-id="635d2-140">Consultez la documentation complète du module PowerShell du Gestionnaire de ressources Service Bus [ici](/powershell/module/azurerm.servicebus).</span><span class="sxs-lookup"><span data-stu-id="635d2-140">See the complete Service Bus Resource Manager PowerShell module documentation [here](/powershell/module/azurerm.servicebus).</span></span> <span data-ttu-id="635d2-141">Cette page répertorie toutes les applets de commande disponibles.</span><span class="sxs-lookup"><span data-stu-id="635d2-141">This page lists all available cmdlets.</span></span>
- <span data-ttu-id="635d2-142">Pour plus d’informations sur l’utilisation des modèles Azure Resource Manager, consultez l’article [Création de ressources Service Bus à l’aide de modèles Azure Resource Manager](service-bus-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="635d2-142">For information about using Azure Resource Manager templates, see the article [Create Service Bus resources using Azure Resource Manager templates](service-bus-resource-manager-overview.md).</span></span>
- <span data-ttu-id="635d2-143">Informations sur les [bibliothèques de gestion Service Bus .NET](service-bus-management-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="635d2-143">Information about [Service Bus .NET management libraries](service-bus-management-libraries.md).</span></span>

<span data-ttu-id="635d2-144">D’autres manières de gérer les entités Service Bus sont décrites dans les billets de blog suivants :</span><span class="sxs-lookup"><span data-stu-id="635d2-144">There are some alternate ways to manage Service Bus entities, as described in these blog posts:</span></span>

* [<span data-ttu-id="635d2-145">Comment créer des files d'attente, des rubriques et des abonnements Service Bus à l'aide d'un script PowerShell</span><span class="sxs-lookup"><span data-stu-id="635d2-145">How to create Service Bus queues, topics and subscriptions using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [<span data-ttu-id="635d2-146">Comment créer un espace de noms Service Bus et un Event Hub à l’aide d’un script PowerShell</span><span class="sxs-lookup"><span data-stu-id="635d2-146">How to create a Service Bus Namespace and an Event Hub using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)
* [<span data-ttu-id="635d2-147">Scripts PowerShell pour Service Bus</span><span class="sxs-lookup"><span data-stu-id="635d2-147">Service Bus PowerShell Scripts</span></span>](https://code.msdn.microsoft.com/Service-Bus-PowerShell-a46b7059)

<!--Anchors-->

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
