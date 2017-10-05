---
title: "Mise à l’échelle d’Azure Service Fabric par programmation | Microsoft Docs"
description: "Faire évoluer un cluster Azure Service Fabric par programmation, selon des déclencheurs personnalisés"
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
ms.openlocfilehash: 46b0b62f92abbac57bc27bbcdd5821eafedf5519
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="scale-a-service-fabric-cluster-programmatically"></a><span data-ttu-id="796a3-103">Mettre à l’échelle un cluster Service Fabric par programmation</span><span class="sxs-lookup"><span data-stu-id="796a3-103">Scale a Service Fabric cluster programmatically</span></span> 

<span data-ttu-id="796a3-104">Les principes de base de mise à l’échelle d’un cluster Service Fabric dans Azure sont décrits dans la documentation sur la [mise à l’échelle du cluster](./service-fabric-cluster-scale-up-down.md).</span><span class="sxs-lookup"><span data-stu-id="796a3-104">Fundamentals of scaling a Service Fabric cluster in Azure are covered in documentation on [cluster scaling](./service-fabric-cluster-scale-up-down.md).</span></span> <span data-ttu-id="796a3-105">Cet article décrit comment les clusters Service Fabric s’appuient sur des groupes de machines virtuelles identiques et peuvent être mis à l’échelle manuellement ou avec des règles automatiques.</span><span class="sxs-lookup"><span data-stu-id="796a3-105">That article covers how Service Fabric clusters are built on top of virtual machine scale sets and can be scaled either manually or with auto-scale rules.</span></span> <span data-ttu-id="796a3-106">Ce document examine les méthodes de programmation pour coordonner les opérations de mise à l’échelle Azure dans les scénarios plus avancés.</span><span class="sxs-lookup"><span data-stu-id="796a3-106">This document looks at programmatic methods of coordinating Azure scaling operations for more advanced scenarios.</span></span> 

## <a name="reasons-for-programmatic-scaling"></a><span data-ttu-id="796a3-107">Motifs d’une mise à l’échelle par programmation</span><span class="sxs-lookup"><span data-stu-id="796a3-107">Reasons for programmatic scaling</span></span>
<span data-ttu-id="796a3-108">Dans de nombreux scénarios, la mise à l’échelle manuelle ou via des règles automatiques est une bonne solution.</span><span class="sxs-lookup"><span data-stu-id="796a3-108">In many scenarios, scaling manually or via auto-scale rules are good solutions.</span></span> <span data-ttu-id="796a3-109">Cependant, dans d’autres cas de figure, ces deux possibilités ne sont pas indiquées.</span><span class="sxs-lookup"><span data-stu-id="796a3-109">In other scenarios, though, they may not be the right fit.</span></span> <span data-ttu-id="796a3-110">Les inconvénients potentiels de ces approches sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="796a3-110">Potential drawbacks to these approaches include:</span></span>

- <span data-ttu-id="796a3-111">La mise à l’échelle manuelle vous oblige à ouvrir une session et à demander explicitement des opérations de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="796a3-111">Manually scaling requires you to log in and explicitly request scaling operations.</span></span> <span data-ttu-id="796a3-112">Si les opérations de mise à l’échelle sont requises fréquemment ou à des moments imprévisibles, cette approche n’est probablement pas la bonne.</span><span class="sxs-lookup"><span data-stu-id="796a3-112">If scaling operations are required frequently or at unpredictable times, this approach may not be a good solution.</span></span>
- <span data-ttu-id="796a3-113">Lorsque les règles de mise à l’échelle automatique suppriment une instance d’un groupe de machines virtuelles identiques, elles ne suppriment pas automatiquement les connaissances de ce nœud du cluster Service Fabric associé, sauf si le nœud a un niveau de durabilité agent ou or.</span><span class="sxs-lookup"><span data-stu-id="796a3-113">When auto-scale rules remove an instance from a virtual machine scale set, they do not automatically remove knowledge of that node from the associated Service Fabric cluster unless the node type has a durability level of Silver or Gold.</span></span> <span data-ttu-id="796a3-114">Comme les règles de mise à l’échelle automatique fonctionnent au niveau du groupe de machines virtuelles (et non au niveau de Service Fabric), elles peuvent supprimer des nœuds Service Fabric sans les arrêter en douceur.</span><span class="sxs-lookup"><span data-stu-id="796a3-114">Because auto-scale rules work at the scale set level (rather than at the Service Fabric level), auto-scale rules can remove Service Fabric nodes without shutting them down gracefully.</span></span> <span data-ttu-id="796a3-115">Cette suppression brutale laisse l’état de nœud Service Fabric « ghost » derrière elle, après les opérations de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="796a3-115">This rude node removal will leave 'ghost' Service Fabric node state behind after scale-in operations.</span></span> <span data-ttu-id="796a3-116">Une personne (ou un service) doit nettoyer régulièrement l’état du nœud supprimé dans le cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="796a3-116">An individual (or a service) would need to periodically clean up removed node state in the Service Fabric cluster.</span></span>
  - <span data-ttu-id="796a3-117">Notez qu’un nœud ayant un niveau de durabilité argent ou or nettoie automatiquement les nœuds supprimés.</span><span class="sxs-lookup"><span data-stu-id="796a3-117">Note that a node type with a durability level of Gold or Silver will automatically clean up removed nodes.</span></span>  
- <span data-ttu-id="796a3-118">Bien que les règles de mise à l’échelle automatique prennent en charge [plusieurs mesures](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md), ce groupe reste limité.</span><span class="sxs-lookup"><span data-stu-id="796a3-118">Although there are [many metrics](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md) supported by auto-scale rules, it is still a limited set.</span></span> <span data-ttu-id="796a3-119">Si votre scénario requiert une mise à l’échelle en fonction d’une mesure non incluse dans ce groupe, les règles de mise à l’échelle automatique ne sont peut-être pas la bonne solution.</span><span class="sxs-lookup"><span data-stu-id="796a3-119">If your scenario calls for scaling based on some metric not covered in that set, then auto-scale rules may not be a good option.</span></span>

<span data-ttu-id="796a3-120">Face à ces limitations, vous pouvez mettre en œuvre des modèles personnalisés de mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="796a3-120">Based on these limitations, you may wish to implement more customized automatic scaling models.</span></span> 

## <a name="scaling-apis"></a><span data-ttu-id="796a3-121">API de mise à l’échelle</span><span class="sxs-lookup"><span data-stu-id="796a3-121">Scaling APIs</span></span>
<span data-ttu-id="796a3-122">Il existe des API Azure qui permettent aux applications de travailler par programmation avec les groupes de machines virtuelles identiques et des clusters Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="796a3-122">Azure APIs exist which allow applications to programmatically work with virtual machine scale sets and Service Fabric clusters.</span></span> <span data-ttu-id="796a3-123">Si les options de mise à l’échelle automatique existantes ne conviennent pas à votre scénario, ces API permettent de mettre en œuvre une logique de mise à l’échelle personnalisée.</span><span class="sxs-lookup"><span data-stu-id="796a3-123">If existing auto-scale options don't work for your scenario, these APIs make it possible to implement custom scaling logic.</span></span> 

<span data-ttu-id="796a3-124">Cette fonctionnalité de mise à l’échelle automatique personnalisée permet d’ajouter un service sans état à l’application Service Fabric pour gérer les opérations de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="796a3-124">One approach to implementing this 'home-made' auto-scaling functionality is to add a new stateless service to the Service Fabric application to manage scaling operations.</span></span> <span data-ttu-id="796a3-125">Dans la méthode `RunAsync` du service, un ensemble de déclencheurs peut déterminer si la mise à l’échelle est requise (avec vérification de paramètres tels que la taille maximale des clusters et de mise à l’échelle de recharges).</span><span class="sxs-lookup"><span data-stu-id="796a3-125">Within the service's `RunAsync` method, a set of triggers can determine if scaling is required (including checking parameters such as maximum cluster size and scaling cooldowns).</span></span>   

<span data-ttu-id="796a3-126">L’API utilisée pour les interactions des groupes de machines virtuelles identiques (afin de vérifier et de modifier le nombre actuel d’instances de machines virtuelles) est la [bibliothèque Fluent Azure Management Compute](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/).</span><span class="sxs-lookup"><span data-stu-id="796a3-126">The API used for virtual machine scale set interactions (both to check the current number of virtual machine instances and to modify it) is the [fluent Azure Management Compute library](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/).</span></span> <span data-ttu-id="796a3-127">Cette bibliothèque de calcul fluide fournit une API conviviale pour interagir avec les groupes de machines virtuelles identiques.</span><span class="sxs-lookup"><span data-stu-id="796a3-127">The fluent compute library provides an easy-to-use API for interacting with virtual machine scale sets.</span></span>

<span data-ttu-id="796a3-128">Pour interagir avec le cluster Service Fabric, utilisez [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).</span><span class="sxs-lookup"><span data-stu-id="796a3-128">To interact with the Service Fabric cluster itself, use [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).</span></span>

<span data-ttu-id="796a3-129">Bien sûr, le code de mise à l’échelle n’a pas besoin de s’exécuter comme un service dans le cluster à mettre à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="796a3-129">Of course, the scaling code doesn't need to run as a service in the cluster to be scaled.</span></span> <span data-ttu-id="796a3-130">`IAzure` et `FabricClient` peuvent se connecter à leurs ressources Azure associées à distance. Donc, le service de mise à l’échelle peut être une application console ou un service Windows exécuté hors de l’application Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="796a3-130">Both `IAzure` and `FabricClient` can connect to their associated Azure resources remotely, so the scaling service could easily be a console application or Windows service running from outside the Service Fabric application.</span></span> 

## <a name="credential-management"></a><span data-ttu-id="796a3-131">Gestion des informations d’identification</span><span class="sxs-lookup"><span data-stu-id="796a3-131">Credential management</span></span>
<span data-ttu-id="796a3-132">Un service chargé de gérer la mise à l’échelle doit pouvoir accéder aux ressources d’un groupe de machines virtuelles identiques, sans ouverture de session interactive.</span><span class="sxs-lookup"><span data-stu-id="796a3-132">One challenge of writing a service to handle scaling is that the service must be able to access virtual machine scale set resources without an interactive login.</span></span> <span data-ttu-id="796a3-133">L’accès au cluster Service Fabric est simple si le service de mise à l’échelle modifie sa propre application Service Fabric, mais des informations d’identification sont nécessaires pour accéder au groupe identique.</span><span class="sxs-lookup"><span data-stu-id="796a3-133">Accessing the Service Fabric cluster is easy if the scaling service is modifying its own Service Fabric application, but credentials are needed to access the scale set.</span></span> <span data-ttu-id="796a3-134">Pour vous connecter, vous pouvez utiliser un [principal de service](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) créé avec [Azure CLI 2.0](https://github.com/azure/azure-cli).</span><span class="sxs-lookup"><span data-stu-id="796a3-134">To log in, you can use a [service principal](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) created with the [Azure CLI 2.0](https://github.com/azure/azure-cli).</span></span>

<span data-ttu-id="796a3-135">Pour créer un principal de service, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="796a3-135">A service principal can be created with the following steps:</span></span>

1. <span data-ttu-id="796a3-136">Connectez-vous à l’interface Azure CLI (`az login`) en tant qu’utilisateur ayant accès au groupe de machines virtuelles identiques.</span><span class="sxs-lookup"><span data-stu-id="796a3-136">Log in to the Azure CLI (`az login`) as a user with access to the virtual machine scale set</span></span>
2. <span data-ttu-id="796a3-137">Créez le principal de service avec `az ad sp create-for-rbac`</span><span class="sxs-lookup"><span data-stu-id="796a3-137">Create the service principal with `az ad sp create-for-rbac`</span></span>
    1. <span data-ttu-id="796a3-138">Notez l’ID d’application (appelé ID client ailleurs), le nom, le mot de passe et le client en vue d’une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="796a3-138">Make note of the appId (called 'client ID' elsewhere), name, password, and tenant for later use.</span></span>
    2. <span data-ttu-id="796a3-139">Vous aurez également besoin de votre ID d’abonnement, que vous pouvez afficher avec `az account list`.</span><span class="sxs-lookup"><span data-stu-id="796a3-139">You will also need your subscription ID, which can be viewed with `az account list`</span></span>

<span data-ttu-id="796a3-140">La bibliothèque de calcul Fluent peut se connecter avec ces informations d’identification de la façon suivante (notez que les principaux types Azure Fluent, par exemple `IAzure`, se trouvent dans le package [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/)) :</span><span class="sxs-lookup"><span data-stu-id="796a3-140">The fluent compute library can log in using these credentials as follows (note that core fluent Azure types like `IAzure` are in the [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) package):</span></span>

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
    ServiceEventSource.Current.ServiceMessage(Context, "ERROR: Failed to login to Azure");
}
```

<span data-ttu-id="796a3-141">Une fois celle-ci connectée, le nombre d’instances de groupes identiques peut être interrogée avec `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.</span><span class="sxs-lookup"><span data-stu-id="796a3-141">Once logged in, scale set instance count can be queried via `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.</span></span>

## <a name="scaling-out"></a><span data-ttu-id="796a3-142">Montée en charge</span><span class="sxs-lookup"><span data-stu-id="796a3-142">Scaling out</span></span>
<span data-ttu-id="796a3-143">Le Kit de développement logiciel (SDK) Azure Compute permet d’ajouter des instances au groupe de machines virtuelles identiques, moyennant quelques appels seulement.</span><span class="sxs-lookup"><span data-stu-id="796a3-143">Using the fluent Azure compute SDK, instances can be added to the virtual machine scale set with just a few calls -</span></span>

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);
var newCapacity = (int)Math.Min(MaximumNodeCount, scaleSet.Capacity + 1);
scaleSet.Update().WithCapacity(newCapacity).Apply(); 
``` 

<span data-ttu-id="796a3-144">Il est également possible de gérer la taille des groupes de machines virtuelles identiques avec des applets de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="796a3-144">Alternatively, virtual machine scale set size can also be managed with PowerShell cmdlets.</span></span> <span data-ttu-id="796a3-145">[`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss) peut récupérer l’objet groupe de machines virtuelles identiques.</span><span class="sxs-lookup"><span data-stu-id="796a3-145">[`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss) can retrieve the virtual machine scale set object.</span></span> <span data-ttu-id="796a3-146">La capacité actuelle sera stockée dans la propriété `.sku.capacity`.</span><span class="sxs-lookup"><span data-stu-id="796a3-146">The current capacity will be stored in the `.sku.capacity` property.</span></span> <span data-ttu-id="796a3-147">Une fois la capacité fixée à la valeur souhaitée, il est possible de mettre à jour le groupe de machines virtuelles identiques dans Azure avec la commande [`Update-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss).</span><span class="sxs-lookup"><span data-stu-id="796a3-147">After changing the capacity to the desired value, the virtual machine scale set in Azure can be updated with the [`Update-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss) command.</span></span>

<span data-ttu-id="796a3-148">Lorsque vous ajoutez manuellement un nœud, l’ajout d’une instance de groupe identique doit suffire pour démarrer un nouveau nœud Service Fabric, car le modèle de groupe identique contient des extensions pour ajouter automatiquement des instances au cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="796a3-148">As when adding a node manually, adding a scale set instance should be all that's needed to start a new Service Fabric node since the scale set template includes extensions to automatically join new instances to the Service Fabric cluster.</span></span> 

## <a name="scaling-in"></a><span data-ttu-id="796a3-149">Mise à l'échelle</span><span class="sxs-lookup"><span data-stu-id="796a3-149">Scaling in</span></span>

<span data-ttu-id="796a3-150">La mise à l’échelle est similaire à la montée en charge.</span><span class="sxs-lookup"><span data-stu-id="796a3-150">Scaling in is similar to scaling out.</span></span> <span data-ttu-id="796a3-151">Les modifications d’un groupe de machines virtuelles identiques sont pratiquement identiques.</span><span class="sxs-lookup"><span data-stu-id="796a3-151">The actual virtual machine scale set changes are practically the same.</span></span> <span data-ttu-id="796a3-152">Mais, comme nous l’avons déjà vu, Service Fabric ne nettoie automatiquement que les nœuds supprimés ayant une durabilité de niveau or ou argent.</span><span class="sxs-lookup"><span data-stu-id="796a3-152">But, as was discussed previously, Service Fabric only automatically cleans up removed nodes with a durability of Gold or Silver.</span></span> <span data-ttu-id="796a3-153">Par conséquent, dans le cas d’une mise à l’échelle avec une durabilité de niveau bronze, il est nécessaire d’interagir avec le cluster Service Fabric pour arrêter le nœud à supprimer, puis de supprimer son état.</span><span class="sxs-lookup"><span data-stu-id="796a3-153">So, in the Bronze-durability scale-in case, it's necessary to interact with the Service Fabric cluster to shut down the node to be removed and then to remove its state.</span></span>

<span data-ttu-id="796a3-154">La préparation du nœud à l’arrêt consiste à trouver le nœud à supprimer (le dernier nœud ajouté) et à le désactiver.</span><span class="sxs-lookup"><span data-stu-id="796a3-154">Preparing the node for shutdown involves finding the node to be removed (the most recently added node) and deactivating it.</span></span> <span data-ttu-id="796a3-155">Pour les nœuds non racines, les nœuds plus récents sont accessibles en comparant le `NodeInstanceId`.</span><span class="sxs-lookup"><span data-stu-id="796a3-155">For non-seed nodes, newer nodes can be found by comparing `NodeInstanceId`.</span></span> 

```C#
using (var client = new FabricClient())
{
    var mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync())
        .Where(n => n.NodeType.Equals(NodeTypeToScale, StringComparison.OrdinalIgnoreCase))
        .Where(n => n.NodeStatus == System.Fabric.Query.NodeStatus.Up)
        .OrderByDescending(n => n.NodeInstanceId)
        .FirstOrDefault();
```

<span data-ttu-id="796a3-156">N’oubliez pas que les nœuds *racines* ne semblent pas toujours respecter la convention selon laquelle les ID d’instance supérieurs sont supprimés en premier.</span><span class="sxs-lookup"><span data-stu-id="796a3-156">Be aware that *seed* nodes don't seem to always follow the convention that greater instance IDs are removed first.</span></span>

<span data-ttu-id="796a3-157">Une fois le nœud à supprimer trouvé, il peut être désactivé et supprimé à l’aide de la même instance `FabricClient` et de l’instance `IAzure` précédente.</span><span class="sxs-lookup"><span data-stu-id="796a3-157">Once the node to be removed is found, it can be deactivated and removed using the same `FabricClient` instance and the `IAzure` instance from earlier.</span></span>

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);

// Remove the node from the Service Fabric cluster
ServiceEventSource.Current.ServiceMessage(Context, $"Disabling node {mostRecentLiveNode.NodeName}");
await client.ClusterManager.DeactivateNodeAsync(mostRecentLiveNode.NodeName, NodeDeactivationIntent.RemoveNode);

// Wait (up to a timeout) for the node to gracefully shutdown
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

<span data-ttu-id="796a3-158">Comme pour la montée en charge, des cmdlets e PowerShell de modification de la capacité des groupes de machines virtuelles identiques peuvent également être utilisées ici si une approche par scripts est préférable.</span><span class="sxs-lookup"><span data-stu-id="796a3-158">As with scaling out, PowerShell cmdlets for modifying virtual machine scale set capacity can also be used here if a scripting approach is preferable.</span></span> <span data-ttu-id="796a3-159">Une fois l’instance de machine virtuelle supprimée, l’état du nœud Service Fabric peut être supprimé.</span><span class="sxs-lookup"><span data-stu-id="796a3-159">Once the virtual machine instance is removed, Service Fabric node state can be removed.</span></span>

```C#
await client.ClusterManager.RemoveNodeStateAsync(mostRecentLiveNode.NodeName);
```

## <a name="potential-drawbacks"></a><span data-ttu-id="796a3-160">Inconvénients potentiels</span><span class="sxs-lookup"><span data-stu-id="796a3-160">Potential drawbacks</span></span>

<span data-ttu-id="796a3-161">Comme nous l’avons vu dans les extraits de code précédents, créer votre propre service de mise à l’échelle optimise le niveau de contrôle et de personnalisation du comportement de mise à l’échelle de votre application.</span><span class="sxs-lookup"><span data-stu-id="796a3-161">As demonstrated in the preceding code snippets, creating your own scaling service provides the highest degree of control and customizability over your application's scaling behavior.</span></span> <span data-ttu-id="796a3-162">Cela peut être utile dans les cas qui requièrent un contrôle précis sur le moment ou les modalités de la mise à l’échelle ou la montée en charge d’une application.</span><span class="sxs-lookup"><span data-stu-id="796a3-162">This can be useful for scenarios requiring precise control over when or how an application scales in or out.</span></span> <span data-ttu-id="796a3-163">Toutefois, ce contrôle complique le code.</span><span class="sxs-lookup"><span data-stu-id="796a3-163">However, this control comes with a tradeoff of code complexity.</span></span> <span data-ttu-id="796a3-164">Cette approche signifie que vous devez posséder votre propre code de mise à l’échelle, ce qui n’est pas négligeable.</span><span class="sxs-lookup"><span data-stu-id="796a3-164">Using this approach means that you need to own scaling code, which is non-trivial.</span></span>

<span data-ttu-id="796a3-165">Le mode de mise à l’échelle de Service Fabric dépend de votre cas de figure.</span><span class="sxs-lookup"><span data-stu-id="796a3-165">How you should approach Service Fabric scaling depends on your scenario.</span></span> <span data-ttu-id="796a3-166">Si la mise à l’échelle est rare, la possibilité d’ajouter ou de supprimer des nœuds manuellement est probablement suffisante.</span><span class="sxs-lookup"><span data-stu-id="796a3-166">If scaling is uncommon, the ability to add or remove nodes manually is probably sufficient.</span></span> <span data-ttu-id="796a3-167">Dans les scénarios plus complexes, les règles de mise à l’échelle automatique et les kits de développement logiciel (SDK) qui assurent la mise à l’échelle par programmation offrent des alternatives puissantes.</span><span class="sxs-lookup"><span data-stu-id="796a3-167">For more complex scenarios, auto-scale rules and SDKs exposing the ability to scale programmatically offer powerful alternatives.</span></span>

## <a name="next-steps"></a><span data-ttu-id="796a3-168">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="796a3-168">Next steps</span></span>

<span data-ttu-id="796a3-169">Pour commencer à implémenter votre propre logique de mise à l’échelle automatique, vous devez vous familiariser avec les API utiles et les concepts suivants :</span><span class="sxs-lookup"><span data-stu-id="796a3-169">To get started implementing your own auto-scaling logic, familiarize yourself with the following concepts and useful APIs:</span></span>

- [<span data-ttu-id="796a3-170">Augmenter ou diminuer la taille des instances d’un cluster Service Fabric à l’aide de règles de mise à l’échelle automatique</span><span class="sxs-lookup"><span data-stu-id="796a3-170">Scaling manually or with auto-scale rules</span></span>](./service-fabric-cluster-scale-up-down.md)
- <span data-ttu-id="796a3-171">[Bibliothèques Azure Management fluides pour .NET](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (utiles pour interagir avec les groupes de machines virtuelles identiques sous-jacents d’un cluster Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="796a3-171">[Fluent Azure Management Libraries for .NET](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (useful for interacting with a Service Fabric cluster's underlying virtual machine scale sets)</span></span>
- <span data-ttu-id="796a3-172">[System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (utile pour interagir avec un cluster Service Fabric et ses nœuds)</span><span class="sxs-lookup"><span data-stu-id="796a3-172">[System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (useful for interacting with a Service Fabric cluster and its nodes)</span></span>
