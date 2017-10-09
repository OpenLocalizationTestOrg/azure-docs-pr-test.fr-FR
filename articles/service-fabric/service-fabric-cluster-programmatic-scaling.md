---
title: "aaaAzure Service Fabric par programmation mise à l’échelle | Documents Microsoft"
description: "Mettre à l’échelle d’un cluster Azure Service Fabric ou par programme, selon les déclencheurs toocustom"
services: service-fabric
documentationcenter: .net
author: mjrousos
manager: jonjung
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: mikerou
ms.openlocfilehash: a0c6499b1a143a173006248cf8a15380632637e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-service-fabric-cluster-programmatically"></a><span data-ttu-id="f9efe-103">Mettre à l’échelle un cluster Service Fabric par programmation</span><span class="sxs-lookup"><span data-stu-id="f9efe-103">Scale a Service Fabric cluster programmatically</span></span> 

<span data-ttu-id="f9efe-104">Les principes de base de mise à l’échelle d’un cluster Service Fabric dans Azure sont décrits dans la documentation sur la [mise à l’échelle du cluster](./service-fabric-cluster-scale-up-down.md).</span><span class="sxs-lookup"><span data-stu-id="f9efe-104">Fundamentals of scaling a Service Fabric cluster in Azure are covered in documentation on [cluster scaling](./service-fabric-cluster-scale-up-down.md).</span></span> <span data-ttu-id="f9efe-105">Cet article décrit comment les clusters Service Fabric s’appuient sur des groupes de machines virtuelles identiques et peuvent être mis à l’échelle manuellement ou avec des règles automatiques.</span><span class="sxs-lookup"><span data-stu-id="f9efe-105">That article covers how Service Fabric clusters are built on top of virtual machine scale sets and can be scaled either manually or with auto-scale rules.</span></span> <span data-ttu-id="f9efe-106">Ce document examine les méthodes de programmation pour coordonner les opérations de mise à l’échelle Azure dans les scénarios plus avancés.</span><span class="sxs-lookup"><span data-stu-id="f9efe-106">This document looks at programmatic methods of coordinating Azure scaling operations for more advanced scenarios.</span></span> 

## <a name="reasons-for-programmatic-scaling"></a><span data-ttu-id="f9efe-107">Motifs d’une mise à l’échelle par programmation</span><span class="sxs-lookup"><span data-stu-id="f9efe-107">Reasons for programmatic scaling</span></span>
<span data-ttu-id="f9efe-108">Dans de nombreux scénarios, la mise à l’échelle manuelle ou via des règles automatiques est une bonne solution.</span><span class="sxs-lookup"><span data-stu-id="f9efe-108">In many scenarios, scaling manually or via auto-scale rules are good solutions.</span></span> <span data-ttu-id="f9efe-109">Toutefois, dans d’autres scénarios, ils peuvent être pas hello ajuster à droite.</span><span class="sxs-lookup"><span data-stu-id="f9efe-109">In other scenarios, though, they may not be hello right fit.</span></span> <span data-ttu-id="f9efe-110">Approches de toothese inconvénients possibles sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="f9efe-110">Potential drawbacks toothese approaches include:</span></span>

- <span data-ttu-id="f9efe-111">Mise à l’échelle manuelle nécessite que vous toolog dans et explicitement les opérations de mise à l’échelle de la demande.</span><span class="sxs-lookup"><span data-stu-id="f9efe-111">Manually scaling requires you toolog in and explicitly request scaling operations.</span></span> <span data-ttu-id="f9efe-112">Si les opérations de mise à l’échelle sont requises fréquemment ou à des moments imprévisibles, cette approche n’est probablement pas la bonne.</span><span class="sxs-lookup"><span data-stu-id="f9efe-112">If scaling operations are required frequently or at unpredictable times, this approach may not be a good solution.</span></span>
- <span data-ttu-id="f9efe-113">Lorsque les règles à l’échelle automatique supprimer une instance d’un ensemble d’échelle de machine virtuelle, ils ne suppriment pas automatiquement connaissance de ce nœud de cluster du Service Fabric hello associé, sauf si le type de nœud hello a un niveau de durabilité d’argent ou OR.</span><span class="sxs-lookup"><span data-stu-id="f9efe-113">When auto-scale rules remove an instance from a virtual machine scale set, they do not automatically remove knowledge of that node from hello associated Service Fabric cluster unless hello node type has a durability level of Silver or Gold.</span></span> <span data-ttu-id="f9efe-114">Étant donné que les règles à l’échelle automatique de travail à définir le niveau de la montée en puissance hello (plutôt qu’à hello au niveau de l’infrastructure de Service), les règles à l’échelle automatique peuvent supprimer des nœuds de l’infrastructure de Service sans arrêter normalement.</span><span class="sxs-lookup"><span data-stu-id="f9efe-114">Because auto-scale rules work at hello scale set level (rather than at hello Service Fabric level), auto-scale rules can remove Service Fabric nodes without shutting them down gracefully.</span></span> <span data-ttu-id="f9efe-115">Cette suppression brutale laisse l’état de nœud Service Fabric « ghost » derrière elle, après les opérations de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="f9efe-115">This rude node removal will leave 'ghost' Service Fabric node state behind after scale-in operations.</span></span> <span data-ttu-id="f9efe-116">Une personne (ou un service) devez tooperiodically état du nœud supprimé du cluster Service Fabric de hello de nettoyage.</span><span class="sxs-lookup"><span data-stu-id="f9efe-116">An individual (or a service) would need tooperiodically clean up removed node state in hello Service Fabric cluster.</span></span>
  - <span data-ttu-id="f9efe-117">Notez qu’un nœud ayant un niveau de durabilité argent ou or nettoie automatiquement les nœuds supprimés.</span><span class="sxs-lookup"><span data-stu-id="f9efe-117">Note that a node type with a durability level of Gold or Silver will automatically clean up removed nodes.</span></span>  
- <span data-ttu-id="f9efe-118">Bien que les règles de mise à l’échelle automatique prennent en charge [plusieurs mesures](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md), ce groupe reste limité.</span><span class="sxs-lookup"><span data-stu-id="f9efe-118">Although there are [many metrics](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md) supported by auto-scale rules, it is still a limited set.</span></span> <span data-ttu-id="f9efe-119">Si votre scénario requiert une mise à l’échelle en fonction d’une mesure non incluse dans ce groupe, les règles de mise à l’échelle automatique ne sont peut-être pas la bonne solution.</span><span class="sxs-lookup"><span data-stu-id="f9efe-119">If your scenario calls for scaling based on some metric not covered in that set, then auto-scale rules may not be a good option.</span></span>

<span data-ttu-id="f9efe-120">En fonction de ces limitations, vous souhaiterez peut-être tooimplement plus automatique mise à l’échelle des modèles personnalisés.</span><span class="sxs-lookup"><span data-stu-id="f9efe-120">Based on these limitations, you may wish tooimplement more customized automatic scaling models.</span></span> 

## <a name="scaling-apis"></a><span data-ttu-id="f9efe-121">API de mise à l’échelle</span><span class="sxs-lookup"><span data-stu-id="f9efe-121">Scaling APIs</span></span>
<span data-ttu-id="f9efe-122">API Azure existe qui permettent d’applications tooprogrammatically les machines virtuelles identiques et clusters Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f9efe-122">Azure APIs exist which allow applications tooprogrammatically work with virtual machine scale sets and Service Fabric clusters.</span></span> <span data-ttu-id="f9efe-123">Si les options à l’échelle automatique existantes ne fonctionnent pas pour votre scénario, ces API rendre possible tooimplement logique de mise à l’échelle personnalisée.</span><span class="sxs-lookup"><span data-stu-id="f9efe-123">If existing auto-scale options don't work for your scenario, these APIs make it possible tooimplement custom scaling logic.</span></span> 

<span data-ttu-id="f9efe-124">Tooimplementing une approche Ceci 'accueil-rendu' mise à l’échelle des fonctionnalités est tooadd un toomanage nouvelle d’application Service Fabric toohello service sans état opérations de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="f9efe-124">One approach tooimplementing this 'home-made' auto-scaling functionality is tooadd a new stateless service toohello Service Fabric application toomanage scaling operations.</span></span> <span data-ttu-id="f9efe-125">Au sein du service hello `RunAsync` méthode, un ensemble de déclencheurs peut déterminer si la mise à l’échelle est requis (y compris les paramètres telles que la taille maximale des clusters de vérification et mise à l’échelle cooldowns).</span><span class="sxs-lookup"><span data-stu-id="f9efe-125">Within hello service's `RunAsync` method, a set of triggers can determine if scaling is required (including checking parameters such as maximum cluster size and scaling cooldowns).</span></span>   

<span data-ttu-id="f9efe-126">Hello API utilisée pour les interactions de machine virtuelle mise à l’échelle ensemble (à la fois nombre actuel de hello toocheck des instances de machine virtuelle et toomodify elle) est hello [fluent bibliothèque calcul de gestion Azure](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/).</span><span class="sxs-lookup"><span data-stu-id="f9efe-126">hello API used for virtual machine scale set interactions (both toocheck hello current number of virtual machine instances and toomodify it) is hello [fluent Azure Management Compute library](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/).</span></span> <span data-ttu-id="f9efe-127">bibliothèque de calcul fluent Hello fournit une API de facile à utiliser pour interagir avec les machines virtuelles identiques.</span><span class="sxs-lookup"><span data-stu-id="f9efe-127">hello fluent compute library provides an easy-to-use API for interacting with virtual machine scale sets.</span></span>

<span data-ttu-id="f9efe-128">toointeract avec cluster de Service Fabric hello lui-même, utilisez [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).</span><span class="sxs-lookup"><span data-stu-id="f9efe-128">toointeract with hello Service Fabric cluster itself, use [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).</span></span>

<span data-ttu-id="f9efe-129">Bien entendu, hello code de mise à l’échelle n’a pas besoin toorun en tant que service dans hello toobe de cluster à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="f9efe-129">Of course, hello scaling code doesn't need toorun as a service in hello cluster toobe scaled.</span></span> <span data-ttu-id="f9efe-130">Les deux `IAzure` et `FabricClient` peuvent se connecter tootheir associé des ressources Azure à distance, afin de hello service de mise à l’échelle peut être facilement une application console ou un service Windows en cours d’exécution à partir de l’application de Service Fabric hello en dehors.</span><span class="sxs-lookup"><span data-stu-id="f9efe-130">Both `IAzure` and `FabricClient` can connect tootheir associated Azure resources remotely, so hello scaling service could easily be a console application or Windows service running from outside hello Service Fabric application.</span></span> 

## <a name="credential-management"></a><span data-ttu-id="f9efe-131">Gestion des informations d’identification</span><span class="sxs-lookup"><span data-stu-id="f9efe-131">Credential management</span></span>
<span data-ttu-id="f9efe-132">Un des défis de l’écriture d’un service mise à l’échelle toohandle sont que service de hello doit être tooaccess en mesure de machine virtuelle l’échelle ensemble les ressources sans une connexion interactive.</span><span class="sxs-lookup"><span data-stu-id="f9efe-132">One challenge of writing a service toohandle scaling is that hello service must be able tooaccess virtual machine scale set resources without an interactive login.</span></span> <span data-ttu-id="f9efe-133">L’accès à hello Service Fabric cluster est facile si hello à l’échelle service modifie sa propre application Service Fabric, mais les informations d’identification sont nécessaires tooaccess hello ensemble d’échelle.</span><span class="sxs-lookup"><span data-stu-id="f9efe-133">Accessing hello Service Fabric cluster is easy if hello scaling service is modifying its own Service Fabric application, but credentials are needed tooaccess hello scale set.</span></span> <span data-ttu-id="f9efe-134">toolog dans, vous pouvez utiliser un [principal du service](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) créé par hello [Azure CLI 2.0](https://github.com/azure/azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f9efe-134">toolog in, you can use a [service principal](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) created with hello [Azure CLI 2.0](https://github.com/azure/azure-cli).</span></span>

<span data-ttu-id="f9efe-135">Un principal de service peut être créé avec hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f9efe-135">A service principal can be created with hello following steps:</span></span>

1. <span data-ttu-id="f9efe-136">Connectez-vous à toohello CLI d’Azure (`az login`) en tant qu’utilisateur avec une échelle de machine virtuelle accès toohello définie</span><span class="sxs-lookup"><span data-stu-id="f9efe-136">Log in toohello Azure CLI (`az login`) as a user with access toohello virtual machine scale set</span></span>
2. <span data-ttu-id="f9efe-137">Créer le service de hello principal avec`az ad sp create-for-rbac`</span><span class="sxs-lookup"><span data-stu-id="f9efe-137">Create hello service principal with `az ad sp create-for-rbac`</span></span>
    1. <span data-ttu-id="f9efe-138">Prenez note de l’appId hello (appelé d’ailleurs 'ID client'), nom, mot de passe et le client pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="f9efe-138">Make note of hello appId (called 'client ID' elsewhere), name, password, and tenant for later use.</span></span>
    2. <span data-ttu-id="f9efe-139">Vous aurez également besoin de votre ID d’abonnement, que vous pouvez afficher avec `az account list`.</span><span class="sxs-lookup"><span data-stu-id="f9efe-139">You will also need your subscription ID, which can be viewed with `az account list`</span></span>

<span data-ttu-id="f9efe-140">Hello calcul fluent bibliothèque peut se connecter à l’aide de ces informations d’identification comme suit (Notez que les types Azure fluent de principaux, tels que `IAzure` sont Bonjour [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) package) :</span><span class="sxs-lookup"><span data-stu-id="f9efe-140">hello fluent compute library can log in using these credentials as follows (note that core fluent Azure types like `IAzure` are in hello [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) package):</span></span>

```C#
var credentials = new AzureCredentials(new ServicePrincipalLoginInformation {
                ClientId = AzureClientId,
                ClientSecret = 
                AzureClientKey }, AzureTenantId, AzureEnvironment.AzureGlobalCloud);
IAzure AzureClient = Azure.Authenticate(credentials).WithSubscription(AzureSubscriptionId);

if (AzureClient?.SubscriptionId == AzureSubscriptionId)
{
    ServiceEventSource.Current.ServiceMessage(Context, "Successfully logged into Azure");
}
else
{
    ServiceEventSource.Current.ServiceMessage(Context, "ERROR: Failed toologin tooAzure");
}
```

<span data-ttu-id="f9efe-141">Une fois celle-ci connectée, le nombre d’instances de groupes identiques peut être interrogée avec `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.</span><span class="sxs-lookup"><span data-stu-id="f9efe-141">Once logged in, scale set instance count can be queried via `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.</span></span>

## <a name="scaling-out"></a><span data-ttu-id="f9efe-142">Montée en charge</span><span class="sxs-lookup"><span data-stu-id="f9efe-142">Scaling out</span></span>
<span data-ttu-id="f9efe-143">À l’aide de hello fluent Kit de développement logiciel de calcul Azure, instances peuvent être ajoutées à l’échelle de machine virtuelle toohello avec seulement quelques appels-</span><span class="sxs-lookup"><span data-stu-id="f9efe-143">Using hello fluent Azure compute SDK, instances can be added toohello virtual machine scale set with just a few calls -</span></span>

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);
var newCapacity = (int)Math.Min(MaximumNodeCount, scaleSet.Capacity + 1);
scaleSet.Update().WithCapacity(newCapacity).Apply(); 
``` 

<span data-ttu-id="f9efe-144">Il est également possible de gérer la taille des groupes de machines virtuelles identiques avec des applets de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f9efe-144">Alternatively, virtual machine scale set size can also be managed with PowerShell cmdlets.</span></span> <span data-ttu-id="f9efe-145">[`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss)peut récupérer l’objet de jeu de mise à l’échelle de machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="f9efe-145">[`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss) can retrieve hello virtual machine scale set object.</span></span> <span data-ttu-id="f9efe-146">capacité actuelle de Hello est stockée dans hello `.sku.capacity` propriété.</span><span class="sxs-lookup"><span data-stu-id="f9efe-146">hello current capacity will be stored in hello `.sku.capacity` property.</span></span> <span data-ttu-id="f9efe-147">Une fois la modification hello capacité toohello, valeur souhaitée, échelle de machines virtuelles hello dans Azure permettre être mis à jour avec hello [ `Update-AzureRmVmss` ](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss) commande.</span><span class="sxs-lookup"><span data-stu-id="f9efe-147">After changing hello capacity toohello desired value, hello virtual machine scale set in Azure can be updated with hello [`Update-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss) command.</span></span>

<span data-ttu-id="f9efe-148">Comme lorsque vous ajoutez un nœud manuellement, l’ajout d’une échelle de définie l’instance doit être tous les de toostart nécessaire à un nouveau nœud de l’infrastructure de Service, car le modèle de jeu de mise à l’échelle hello inclut extensions tooautomatically joindre cluster Service Fabric de nouvelles instances toohello.</span><span class="sxs-lookup"><span data-stu-id="f9efe-148">As when adding a node manually, adding a scale set instance should be all that's needed toostart a new Service Fabric node since hello scale set template includes extensions tooautomatically join new instances toohello Service Fabric cluster.</span></span> 

## <a name="scaling-in"></a><span data-ttu-id="f9efe-149">Mise à l'échelle</span><span class="sxs-lookup"><span data-stu-id="f9efe-149">Scaling in</span></span>

<span data-ttu-id="f9efe-150">Mise à l’échelle dans est similaire tooscaling out. ensemble d’échelle de machine virtuelle Hello modifications sont pratiquement hello identiques.</span><span class="sxs-lookup"><span data-stu-id="f9efe-150">Scaling in is similar tooscaling out. hello actual virtual machine scale set changes are practically hello same.</span></span> <span data-ttu-id="f9efe-151">Mais, comme nous l’avons déjà vu, Service Fabric ne nettoie automatiquement que les nœuds supprimés ayant une durabilité de niveau or ou argent.</span><span class="sxs-lookup"><span data-stu-id="f9efe-151">But, as was discussed previously, Service Fabric only automatically cleans up removed nodes with a durability of Gold or Silver.</span></span> <span data-ttu-id="f9efe-152">Dans les cas de mise à l’échelle dans hello Bronze-durabilité, il est donc nécessaire toointeract avec hello Service Fabric cluster tooshut hello toobe de nœud supprimé vers le bas, puis tooremove son état.</span><span class="sxs-lookup"><span data-stu-id="f9efe-152">So, in hello Bronze-durability scale-in case, it's necessary toointeract with hello Service Fabric cluster tooshut down hello node toobe removed and then tooremove its state.</span></span>

<span data-ttu-id="f9efe-153">Préparation du nœud de hello pour arrêt implique la recherche hello nœud toobe supprimé (hello plus récemment ajoutée nœud) et les désactiver.</span><span class="sxs-lookup"><span data-stu-id="f9efe-153">Preparing hello node for shutdown involves finding hello node toobe removed (hello most recently added node) and deactivating it.</span></span> <span data-ttu-id="f9efe-154">Pour les nœuds non racines, les nœuds plus récents sont accessibles en comparant le `NodeInstanceId`.</span><span class="sxs-lookup"><span data-stu-id="f9efe-154">For non-seed nodes, newer nodes can be found by comparing `NodeInstanceId`.</span></span> 

```C#
using (var client = new FabricClient())
{
    var mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync())
        .Where(n => n.NodeType.Equals(NodeTypeToScale, StringComparison.OrdinalIgnoreCase))
        .Where(n => n.NodeStatus == System.Fabric.Query.NodeStatus.Up)
        .OrderByDescending(n => n.NodeInstanceId)
        .FirstOrDefault();
```

<span data-ttu-id="f9efe-155">N’oubliez pas que *seed* nœuds semblent ne pas tooalways respectent la convention de hello qu’un ID d’instance supérieur est supprimé en premier.</span><span class="sxs-lookup"><span data-stu-id="f9efe-155">Be aware that *seed* nodes don't seem tooalways follow hello convention that greater instance IDs are removed first.</span></span>

<span data-ttu-id="f9efe-156">Une fois hello toobe de nœud supprimé est trouvé, il peut être désactivé et supprimé à l’aide de même hello `FabricClient` instance et hello `IAzure` instance précédemment.</span><span class="sxs-lookup"><span data-stu-id="f9efe-156">Once hello node toobe removed is found, it can be deactivated and removed using hello same `FabricClient` instance and hello `IAzure` instance from earlier.</span></span>

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);

// Remove hello node from hello Service Fabric cluster
ServiceEventSource.Current.ServiceMessage(Context, $"Disabling node {mostRecentLiveNode.NodeName}");
await client.ClusterManager.DeactivateNodeAsync(mostRecentLiveNode.NodeName, NodeDeactivationIntent.RemoveNode);

// Wait (up tooa timeout) for hello node toogracefully shutdown
var timeout = TimeSpan.FromMinutes(5);
var waitStart = DateTime.Now;
while ((mostRecentLiveNode.NodeStatus == System.Fabric.Query.NodeStatus.Up || mostRecentLiveNode.NodeStatus == System.Fabric.Query.NodeStatus.Disabling) &&
        DateTime.Now - waitStart < timeout)
{
    mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync()).FirstOrDefault(n => n.NodeName == mostRecentLiveNode.NodeName);
    await Task.Delay(10 * 1000);
}

// Decrement VMSS capacity
var newCapacity = (int)Math.Max(MinimumNodeCount, scaleSet.Capacity - 1); // Check min count 

scaleSet.Update().WithCapacity(newCapacity).Apply(); 
```

<span data-ttu-id="f9efe-157">Comme pour la montée en charge, des cmdlets e PowerShell de modification de la capacité des groupes de machines virtuelles identiques peuvent également être utilisées ici si une approche par scripts est préférable.</span><span class="sxs-lookup"><span data-stu-id="f9efe-157">As with scaling out, PowerShell cmdlets for modifying virtual machine scale set capacity can also be used here if a scripting approach is preferable.</span></span> <span data-ttu-id="f9efe-158">Une fois que l’instance de machine virtuelle hello est supprimé, l’état du nœud Service Fabric peut être supprimée.</span><span class="sxs-lookup"><span data-stu-id="f9efe-158">Once hello virtual machine instance is removed, Service Fabric node state can be removed.</span></span>

```C#
await client.ClusterManager.RemoveNodeStateAsync(mostRecentLiveNode.NodeName);
```

## <a name="potential-drawbacks"></a><span data-ttu-id="f9efe-159">Inconvénients potentiels</span><span class="sxs-lookup"><span data-stu-id="f9efe-159">Potential drawbacks</span></span>

<span data-ttu-id="f9efe-160">Comme illustré dans hello précédant les extraits de code, la création de votre propre service de mise à l’échelle fournit hello plus haut degré de contrôle et de personnalisation sur votre application de mise à l’échelle comportement.</span><span class="sxs-lookup"><span data-stu-id="f9efe-160">As demonstrated in hello preceding code snippets, creating your own scaling service provides hello highest degree of control and customizability over your application's scaling behavior.</span></span> <span data-ttu-id="f9efe-161">Cela peut être utile dans les cas qui requièrent un contrôle précis sur le moment ou les modalités de la mise à l’échelle ou la montée en charge d’une application. Toutefois, ce contrôle complique le code.</span><span class="sxs-lookup"><span data-stu-id="f9efe-161">This can be useful for scenarios requiring precise control over when or how an application scales in or out. However, this control comes with a tradeoff of code complexity.</span></span> <span data-ttu-id="f9efe-162">À l’aide de cette approche signifie que vous devez tooown mise à l’échelle de code, qui est non trivial.</span><span class="sxs-lookup"><span data-stu-id="f9efe-162">Using this approach means that you need tooown scaling code, which is non-trivial.</span></span>

<span data-ttu-id="f9efe-163">Le mode de mise à l’échelle de Service Fabric dépend de votre cas de figure.</span><span class="sxs-lookup"><span data-stu-id="f9efe-163">How you should approach Service Fabric scaling depends on your scenario.</span></span> <span data-ttu-id="f9efe-164">Si la mise à l’échelle est rare, les nœuds hello capacité tooadd ou supprimez manuellement suffit probablement.</span><span class="sxs-lookup"><span data-stu-id="f9efe-164">If scaling is uncommon, hello ability tooadd or remove nodes manually is probably sufficient.</span></span> <span data-ttu-id="f9efe-165">Pour des scénarios plus complexes, les règles à l’échelle automatique et les kits de développement logiciel exposition hello capacité tooscale par programmation offrent de puissantes alternatives.</span><span class="sxs-lookup"><span data-stu-id="f9efe-165">For more complex scenarios, auto-scale rules and SDKs exposing hello ability tooscale programmatically offer powerful alternatives.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9efe-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f9efe-166">Next steps</span></span>

<span data-ttu-id="f9efe-167">tooget commencé à implémenter votre propre logique de mise à l’échelle, familiarisez-vous avec hello suivant des concepts et des API utiles :</span><span class="sxs-lookup"><span data-stu-id="f9efe-167">tooget started implementing your own auto-scaling logic, familiarize yourself with hello following concepts and useful APIs:</span></span>

- [<span data-ttu-id="f9efe-168">Augmenter ou diminuer la taille des instances d’un cluster Service Fabric à l’aide de règles de mise à l’échelle automatique</span><span class="sxs-lookup"><span data-stu-id="f9efe-168">Scaling manually or with auto-scale rules</span></span>](./service-fabric-cluster-scale-up-down.md)
- <span data-ttu-id="f9efe-169">[Bibliothèques Azure Management fluides pour .NET](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (utiles pour interagir avec les groupes de machines virtuelles identiques sous-jacents d’un cluster Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="f9efe-169">[Fluent Azure Management Libraries for .NET](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (useful for interacting with a Service Fabric cluster's underlying virtual machine scale sets)</span></span>
- <span data-ttu-id="f9efe-170">[System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (utile pour interagir avec un cluster Service Fabric et ses nœuds)</span><span class="sxs-lookup"><span data-stu-id="f9efe-170">[System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (useful for interacting with a Service Fabric cluster and its nodes)</span></span>
