---
title: aaaScale une infrastructure de Service de cluster ou de sortie | Documents Microsoft
description: "Faire évoluer un cluster Service Fabric ou d’annuler la demande de toomatch en définissant des règles à l’échelle automatique pour chaque nœud type/Virtual Machines identiques. Ajouter ou supprimer le cluster de nœuds tooa Service Fabric"
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: aeb76f63-7303-4753-9c64-46146340b83d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/22/2017
ms.author: chackdan
ms.openlocfilehash: 37cfeaf80edc016cf6de017d1c2dc6fbcb8acc2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-service-fabric-cluster-in-or-out-using-auto-scale-rules"></a>Augmenter ou diminuer la taille des instances d’un cluster Service Fabric à l’aide de règles de mise à l’échelle automatique
Machines virtuelles identiques constituent une ressource de calcul Azure que vous pouvez utiliser toodeploy et gérer une collection d’ordinateurs virtuels en tant qu’ensemble. Chaque type de nœud qui est défini dans un cluster Service Fabric est configuré en tant que groupe de machines virtuelles identiques distinct. Chaque type de nœud peut ensuite faire l’objet d’une augmentation ou d’une diminution de la taille des instances de manière indépendante, avoir différents jeux de ports ouverts et présenter différentes métriques de capacité. En savoir plus sur dans hello [Service Fabric nodetypes](service-fabric-cluster-nodetypes.md) document. Étant donné que les types de nœud de Service Fabric hello dans votre cluster sont constitués de machines virtuelles identiques à hello principal, vous devez tooset des règles de l’échelle automatique pour chaque nœud type/Virtual Machines identiques.

> [!NOTE]
> Votre abonnement doit avoir suffisamment tooadd cœurs hello de nouveaux ordinateurs virtuels qui composent ce cluster. Il n’existe aucune validation du modèle actuellement, donc vous obtenez une erreur de temps de déploiement, si une des limites de quota hello sont atteints.
> 
> 

## <a name="choose-hello-node-typevirtual-machine-scale-set-tooscale"></a>Choisissez le nœud type/virtuel échelle de machines hello tooscale
Actuellement, vous n’êtes pas toospecify en mesure de règles de l’échelle automatique hello pour les machines virtuelles identiques à l’aide du portail de hello, donc nous permettent d’utiliser des types de nœuds Azure PowerShell (1.0 +) toolist hello et puis ajoutez toothem de règles à l’échelle automatique.

liste de hello tooget de Machine virtuelle ensemble d’échelle qui composent votre cluster, exécutez hello suivant d’applets de commande :

```powershell
Get-AzureRmResource -ResourceGroupName <RGname> -ResourceType Microsoft.Compute/VirtualMachineScaleSets

Get-AzureRmVmss -ResourceGroupName <RGname> -VMScaleSetName <Virtual Machine scale set name>
```

## <a name="set-auto-scale-rules-for-hello-node-typevirtual-machine-scale-set"></a>Définir des règles à l’échelle automatique pour l’ensemble d’échelle hello nœud type/Virtual Machine
Si votre cluster a plusieurs types de nœud, puis répétez ces étapes pour chaque nœud virtuel/types de montée en puissance de l’ordinateur définit que vous souhaitez tooscale (entrant ou sortant). Tenir numéro hello de nœuds que vous devez disposer avant de configurer la mise à l’échelle automatique. nombre minimal de Hello de nœuds que vous devez posséder pour le type de nœud principal hello est piloté par le niveau de fiabilité hello que vous avez choisi. En savoir plus sur les [niveaux de fiabilité](service-fabric-cluster-capacity.md).

> [!NOTE]
> Mise à l’échelle vers le bas accessible sans type de nœud principal hello que ce nombre minimal de hello rendre le cluster de hello instable ou mettez-le vers le bas. Cela peut entraîner une perte de données pour vos applications et services de système de hello.
> 
> 

Actuellement fonctionnalité à l’échelle automatique de hello n’est pas pilotée par les charges hello que vos applications peuvent signaler tooService l’ensemble fibre optique. Par conséquent, à ce hello temps vous obtenez à l’échelle automatique est purement piloté par les compteurs de performance hello qui sont émis par chacune des instances de jeu de mise à l’échelle de Machine virtuelle hello.  

Suivez ces instructions [tooset à l’échelle automatique pour chaque ensemble d’échelle de Machine virtuelle](../virtual-machine-scale-sets/virtual-machine-scale-sets-autoscale-overview.md).

> [!NOTE]
> Dans une mise à l’échelle vers le bas du scénario, à moins que votre type de nœud possède un niveau de durabilité d’argent ou or vous devez toocall hello [applet de commande Remove-ServiceFabricNodeState](https://msdn.microsoft.com/library/azure/mt125993.aspx) avec le nom de nœud approprié hello.
> 
> 

## <a name="manually-add-vms-tooa-node-typevirtual-machine-scale-set"></a>Ajouter manuellement des machines virtuelles tooa nœud type/Virtual Machines identiques
Suivez l’exemple hello/instructions hello [galerie de modèles de démarrage rapide](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing) nombre de hello toochange d’ordinateurs virtuels dans chaque Nodetype. 

> [!NOTE]
> Ajout de machines virtuelles du temps, donc n’attendent ne pas hello ajouts toobe instantanée. Par conséquent, planifier la capacité de tooadd bien dans le temps, tooallow plus de 10 minutes avant de hello capacité de machine virtuelle est disponible pour les réplicas de hello / tooget instances placé de service.
> 
> 

## <a name="manually-remove-vms-from-hello-primary-node-typevirtual-machine-scale-set"></a>Supprimer manuellement les ordinateurs virtuels à partir de l’ensemble d’échelle hello nœud principal type/Virtual Machine
> [!NOTE]
> services de système de l’infrastructure de service Hello exécutent dans le type de nœud principal hello dans votre cluster. Par conséquent, ne doit jamais arrêter ou nombre hello d’instances qui des types de nœud à l’échelle inférieure à quel niveau de fiabilité hello justifie. Consultez trop[hello plus d’informations sur les niveaux de fiabilité ici](service-fabric-cluster-capacity.md). 
> 
> 

Vous devez tooexecute suivant de hello étapes d’une instance de machine virtuelle à la fois. Ainsi, les services système hello (et vos services avec état) toobe s’arrête sur l’instance de machine virtuelle hello à supprimer et les nouveaux réplicas créés sur d’autres nœuds.

1. Exécutez [Disable-ServiceFabricNode](https://msdn.microsoft.com/library/mt125852.aspx) avec intention nœud de hello toodisable « RemoveNode » que vous allez tooremove (instance la plus élevée dans ce type de nœud hello).
2. Exécutez [Get-ServiceFabricNode](https://msdn.microsoft.com/library/mt125856.aspx) toomake que ce nœud hello est passée en effet toodisabled. Si ce n’est pas le cas, attendez que le nœud de hello est désactivé. Vous ne pouvez pas accélérer cette étape.
3. Suivez l’exemple hello/instructions hello [galerie de modèles de démarrage rapide](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing) toochange hello plusieurs ordinateurs virtuels d’une unité à ce Nodetype. instance Hello supprimé est instance de machine virtuelle la plus élevée hello. 
4. Répétez les étapes 1 à 3, en fonction des besoins, mais jamais à l’échelle nombre hello d’instances dans les types de nœud principal de hello inférieur à quel niveau de fiabilité hello justifient ou non. Consultez trop[hello plus d’informations sur les niveaux de fiabilité ici](service-fabric-cluster-capacity.md). 

## <a name="manually-remove-vms-from-hello-non-primary-node-typevirtual-machine-scale-set"></a>Supprimez manuellement les ordinateurs virtuels à partir d’un nœud principal hello type/Virtual Machines identiques
> [!NOTE]
> Pour un service avec état, vous avez besoin un certain nombre de nœuds toobe toujours toomaintain disponibilité et conserver l’état de votre service. Hello minimum, vous devez hello nombre de nœuds égale toohello cible réplica ensemble de service/partition hello. 
> 
> 

Vous devez hello exécuter hello suivant d’une instance de machine virtuelle comme suit à la fois. Ainsi, toobe s’arrête sur hello instance de machine virtuelle à supprimer les services système hello (et vos services avec état) et nouveaux réplicas créé where else.

1. Exécutez [Disable-ServiceFabricNode](https://msdn.microsoft.com/library/mt125852.aspx) avec intention nœud de hello toodisable « RemoveNode » que vous allez tooremove (instance la plus élevée dans ce type de nœud hello).
2. Exécutez [Get-ServiceFabricNode](https://msdn.microsoft.com/library/mt125856.aspx) toomake que ce nœud hello est passée en effet toodisabled. Si ce n’est pas le cas, attendez que le nœud de hello est désactivé. Vous ne pouvez pas accélérer cette étape.
3. Suivez l’exemple hello/instructions hello [galerie de modèles de démarrage rapide](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing) toochange hello plusieurs ordinateurs virtuels d’une unité à ce Nodetype. Cela va supprimer instance de machine virtuelle la plus élevée hello. 
4. Répétez les étapes 1 à 3, en fonction des besoins, mais jamais à l’échelle nombre hello d’instances dans les types de nœud principal de hello inférieur à quel niveau de fiabilité hello justifient ou non. Consultez trop[hello plus d’informations sur les niveaux de fiabilité ici](service-fabric-cluster-capacity.md).

## <a name="behaviors-you-may-observe-in-service-fabric-explorer"></a>Comportements que vous pouvez observer dans Service Fabric Explorer
Lors de la montée en puissance un Bonjour cluster Service Fabric Explorer reflétera nombre hello de nœuds (ensemble d’échelle de Machine virtuelle instances) qui font partie du cluster de hello.  Toutefois, lorsque vous redimensionnez un cluster, vous verrez instance de nœud/VM hello supprimé affiché dans un état non intègre sauf si vous appelez [Remove-ServiceFabricNodeState cmd](https://msdn.microsoft.com/library/mt125993.aspx) avec le nom de nœud approprié hello.   

Voici une explication hello pour ce comportement.

nœuds répertoriés dans le Service Fabric Explorer Hello sont une réflexion de quels services de système de Service Fabric hello (FM spécifiquement) connaît le nombre de hello du cluster de hello nœuds attendu/a. Lorsque vous faites évoluer hello échelle de machines virtuelles vers le bas, hello machine virtuelle a été supprimé, mais le service système FM considère toujours que reviendra de ce nœud hello (qui a été mappé toohello machine virtuelle qui a été supprimé). Par conséquent, Service Fabric Explorer continue toodisplay ce nœud (même si l’état d’intégrité hello peut-être erreur ou inconnu).

Dans l’ordre les toomake sûr qu’un nœud est supprimé lorsqu’une machine virtuelle est supprimée, vous avez deux options :

1) Choisissez un niveau de durabilité d’argent ou OR (disponible prochainement) pour les types de nœud hello dans votre cluster, qui vous permet de hello d’intégration de l’infrastructure. Qui puis supprimera automatiquement les nœuds hello de notre état services (FM) du système lorsque vous mettez à l’échelle vers le bas.
Consultez trop[hello plus d’informations sur les niveaux de durabilité ici](service-fabric-cluster-capacity.md)

2) Une fois que l’instance de machine virtuelle hello a été mis à l’échelle vers le bas, vous devez toocall hello [applet de commande Remove-ServiceFabricNodeState](https://msdn.microsoft.com/library/mt125993.aspx).

> [!NOTE]
> Les clusters service Fabric nécessitent un certain nombre de nœuds toobe à tout le temps hello dans ordre toomaintain disponibilité et conserver l’état - tooas référencé « gestion de quorum ». Par conséquent, il est généralement unsafe tooshut vers le bas de tous les ordinateurs hello dans un cluster de hello, sauf si vous avez effectué tout d’abord un [une sauvegarde complète de l’état](service-fabric-reliable-services-backup-restore.md).
> 
> 

## <a name="next-steps"></a>Étapes suivantes
Hello en lecture suivant tooalso en savoir plus sur la planification de la capacité du cluster, la mise à niveau un cluster et un partitionnement des services :

* [Planification de la capacité de votre cluster](service-fabric-cluster-capacity.md)
* [Mise à niveau des clusters](service-fabric-cluster-upgrade.md)
* [Partitionnement des services avec état pour une mise à l’échelle maximale](service-fabric-concepts-partitioning.md)

<!--Image references-->
[BrowseServiceFabricClusterResource]: ./media/service-fabric-cluster-scale-up-down/BrowseServiceFabricClusterResource.png
[ClusterResources]: ./media/service-fabric-cluster-scale-up-down/ClusterResources.png
