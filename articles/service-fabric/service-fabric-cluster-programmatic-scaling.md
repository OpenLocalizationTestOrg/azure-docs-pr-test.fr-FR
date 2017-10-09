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
# <a name="scale-a-service-fabric-cluster-programmatically"></a>Mettre à l’échelle un cluster Service Fabric par programmation 

Les principes de base de mise à l’échelle d’un cluster Service Fabric dans Azure sont décrits dans la documentation sur la [mise à l’échelle du cluster](./service-fabric-cluster-scale-up-down.md). Cet article décrit comment les clusters Service Fabric s’appuient sur des groupes de machines virtuelles identiques et peuvent être mis à l’échelle manuellement ou avec des règles automatiques. Ce document examine les méthodes de programmation pour coordonner les opérations de mise à l’échelle Azure dans les scénarios plus avancés. 

## <a name="reasons-for-programmatic-scaling"></a>Motifs d’une mise à l’échelle par programmation
Dans de nombreux scénarios, la mise à l’échelle manuelle ou via des règles automatiques est une bonne solution. Toutefois, dans d’autres scénarios, ils peuvent être pas hello ajuster à droite. Approches de toothese inconvénients possibles sont les suivantes :

- Mise à l’échelle manuelle nécessite que vous toolog dans et explicitement les opérations de mise à l’échelle de la demande. Si les opérations de mise à l’échelle sont requises fréquemment ou à des moments imprévisibles, cette approche n’est probablement pas la bonne.
- Lorsque les règles à l’échelle automatique supprimer une instance d’un ensemble d’échelle de machine virtuelle, ils ne suppriment pas automatiquement connaissance de ce nœud de cluster du Service Fabric hello associé, sauf si le type de nœud hello a un niveau de durabilité d’argent ou OR. Étant donné que les règles à l’échelle automatique de travail à définir le niveau de la montée en puissance hello (plutôt qu’à hello au niveau de l’infrastructure de Service), les règles à l’échelle automatique peuvent supprimer des nœuds de l’infrastructure de Service sans arrêter normalement. Cette suppression brutale laisse l’état de nœud Service Fabric « ghost » derrière elle, après les opérations de mise à l’échelle. Une personne (ou un service) devez tooperiodically état du nœud supprimé du cluster Service Fabric de hello de nettoyage.
  - Notez qu’un nœud ayant un niveau de durabilité argent ou or nettoie automatiquement les nœuds supprimés.  
- Bien que les règles de mise à l’échelle automatique prennent en charge [plusieurs mesures](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md), ce groupe reste limité. Si votre scénario requiert une mise à l’échelle en fonction d’une mesure non incluse dans ce groupe, les règles de mise à l’échelle automatique ne sont peut-être pas la bonne solution.

En fonction de ces limitations, vous souhaiterez peut-être tooimplement plus automatique mise à l’échelle des modèles personnalisés. 

## <a name="scaling-apis"></a>API de mise à l’échelle
API Azure existe qui permettent d’applications tooprogrammatically les machines virtuelles identiques et clusters Service Fabric. Si les options à l’échelle automatique existantes ne fonctionnent pas pour votre scénario, ces API rendre possible tooimplement logique de mise à l’échelle personnalisée. 

Tooimplementing une approche Ceci 'accueil-rendu' mise à l’échelle des fonctionnalités est tooadd un toomanage nouvelle d’application Service Fabric toohello service sans état opérations de mise à l’échelle. Au sein du service hello `RunAsync` méthode, un ensemble de déclencheurs peut déterminer si la mise à l’échelle est requis (y compris les paramètres telles que la taille maximale des clusters de vérification et mise à l’échelle cooldowns).   

Hello API utilisée pour les interactions de machine virtuelle mise à l’échelle ensemble (à la fois nombre actuel de hello toocheck des instances de machine virtuelle et toomodify elle) est hello [fluent bibliothèque calcul de gestion Azure](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/). bibliothèque de calcul fluent Hello fournit une API de facile à utiliser pour interagir avec les machines virtuelles identiques.

toointeract avec cluster de Service Fabric hello lui-même, utilisez [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).

Bien entendu, hello code de mise à l’échelle n’a pas besoin toorun en tant que service dans hello toobe de cluster à l’échelle. Les deux `IAzure` et `FabricClient` peuvent se connecter tootheir associé des ressources Azure à distance, afin de hello service de mise à l’échelle peut être facilement une application console ou un service Windows en cours d’exécution à partir de l’application de Service Fabric hello en dehors. 

## <a name="credential-management"></a>Gestion des informations d’identification
Un des défis de l’écriture d’un service mise à l’échelle toohandle sont que service de hello doit être tooaccess en mesure de machine virtuelle l’échelle ensemble les ressources sans une connexion interactive. L’accès à hello Service Fabric cluster est facile si hello à l’échelle service modifie sa propre application Service Fabric, mais les informations d’identification sont nécessaires tooaccess hello ensemble d’échelle. toolog dans, vous pouvez utiliser un [principal du service](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) créé par hello [Azure CLI 2.0](https://github.com/azure/azure-cli).

Un principal de service peut être créé avec hello comme suit :

1. Connectez-vous à toohello CLI d’Azure (`az login`) en tant qu’utilisateur avec une échelle de machine virtuelle accès toohello définie
2. Créer le service de hello principal avec`az ad sp create-for-rbac`
    1. Prenez note de l’appId hello (appelé d’ailleurs 'ID client'), nom, mot de passe et le client pour une utilisation ultérieure.
    2. Vous aurez également besoin de votre ID d’abonnement, que vous pouvez afficher avec `az account list`.

Hello calcul fluent bibliothèque peut se connecter à l’aide de ces informations d’identification comme suit (Notez que les types Azure fluent de principaux, tels que `IAzure` sont Bonjour [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) package) :

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

Une fois celle-ci connectée, le nombre d’instances de groupes identiques peut être interrogée avec `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.

## <a name="scaling-out"></a>Montée en charge
À l’aide de hello fluent Kit de développement logiciel de calcul Azure, instances peuvent être ajoutées à l’échelle de machine virtuelle toohello avec seulement quelques appels-

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);
var newCapacity = (int)Math.Min(MaximumNodeCount, scaleSet.Capacity + 1);
scaleSet.Update().WithCapacity(newCapacity).Apply(); 
``` 

Il est également possible de gérer la taille des groupes de machines virtuelles identiques avec des applets de commande PowerShell. [`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss)peut récupérer l’objet de jeu de mise à l’échelle de machine virtuelle hello. capacité actuelle de Hello est stockée dans hello `.sku.capacity` propriété. Une fois la modification hello capacité toohello, valeur souhaitée, échelle de machines virtuelles hello dans Azure permettre être mis à jour avec hello [ `Update-AzureRmVmss` ](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss) commande.

Comme lorsque vous ajoutez un nœud manuellement, l’ajout d’une échelle de définie l’instance doit être tous les de toostart nécessaire à un nouveau nœud de l’infrastructure de Service, car le modèle de jeu de mise à l’échelle hello inclut extensions tooautomatically joindre cluster Service Fabric de nouvelles instances toohello. 

## <a name="scaling-in"></a>Mise à l'échelle

Mise à l’échelle dans est similaire tooscaling out. ensemble d’échelle de machine virtuelle Hello modifications sont pratiquement hello identiques. Mais, comme nous l’avons déjà vu, Service Fabric ne nettoie automatiquement que les nœuds supprimés ayant une durabilité de niveau or ou argent. Dans les cas de mise à l’échelle dans hello Bronze-durabilité, il est donc nécessaire toointeract avec hello Service Fabric cluster tooshut hello toobe de nœud supprimé vers le bas, puis tooremove son état.

Préparation du nœud de hello pour arrêt implique la recherche hello nœud toobe supprimé (hello plus récemment ajoutée nœud) et les désactiver. Pour les nœuds non racines, les nœuds plus récents sont accessibles en comparant le `NodeInstanceId`. 

```C#
using (var client = new FabricClient())
{
    var mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync())
        .Where(n => n.NodeType.Equals(NodeTypeToScale, StringComparison.OrdinalIgnoreCase))
        .Where(n => n.NodeStatus == System.Fabric.Query.NodeStatus.Up)
        .OrderByDescending(n => n.NodeInstanceId)
        .FirstOrDefault();
```

N’oubliez pas que *seed* nœuds semblent ne pas tooalways respectent la convention de hello qu’un ID d’instance supérieur est supprimé en premier.

Une fois hello toobe de nœud supprimé est trouvé, il peut être désactivé et supprimé à l’aide de même hello `FabricClient` instance et hello `IAzure` instance précédemment.

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

Comme pour la montée en charge, des cmdlets e PowerShell de modification de la capacité des groupes de machines virtuelles identiques peuvent également être utilisées ici si une approche par scripts est préférable. Une fois que l’instance de machine virtuelle hello est supprimé, l’état du nœud Service Fabric peut être supprimée.

```C#
await client.ClusterManager.RemoveNodeStateAsync(mostRecentLiveNode.NodeName);
```

## <a name="potential-drawbacks"></a>Inconvénients potentiels

Comme illustré dans hello précédant les extraits de code, la création de votre propre service de mise à l’échelle fournit hello plus haut degré de contrôle et de personnalisation sur votre application de mise à l’échelle comportement. Cela peut être utile dans les cas qui requièrent un contrôle précis sur le moment ou les modalités de la mise à l’échelle ou la montée en charge d’une application. Toutefois, ce contrôle complique le code. À l’aide de cette approche signifie que vous devez tooown mise à l’échelle de code, qui est non trivial.

Le mode de mise à l’échelle de Service Fabric dépend de votre cas de figure. Si la mise à l’échelle est rare, les nœuds hello capacité tooadd ou supprimez manuellement suffit probablement. Pour des scénarios plus complexes, les règles à l’échelle automatique et les kits de développement logiciel exposition hello capacité tooscale par programmation offrent de puissantes alternatives.

## <a name="next-steps"></a>Étapes suivantes

tooget commencé à implémenter votre propre logique de mise à l’échelle, familiarisez-vous avec hello suivant des concepts et des API utiles :

- [Augmenter ou diminuer la taille des instances d’un cluster Service Fabric à l’aide de règles de mise à l’échelle automatique](./service-fabric-cluster-scale-up-down.md)
- [Bibliothèques Azure Management fluides pour .NET](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (utiles pour interagir avec les groupes de machines virtuelles identiques sous-jacents d’un cluster Service Fabric)
- [System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (utile pour interagir avec un cluster Service Fabric et ses nœuds)
