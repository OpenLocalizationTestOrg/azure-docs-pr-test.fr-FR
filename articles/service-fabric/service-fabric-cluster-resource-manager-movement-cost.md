---
title: "Gestionnaire des ressources de cluster Service Fabric : coût du déplacement | Microsoft Docs"
description: "Présentation du coût du mouvement pour les services Service Fabric"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: f022f258-7bc0-4db4-aa85-8c6c8344da32
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 65d4ac73efffcf7b25b1e95da6f9012a9238cb75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-movement-cost"></a>Coût du déplacement de services
Un facteur qui hello du Gestionnaire de ressources du Cluster Service Fabric prend en compte lors de la tentative de toodetermine quel cluster de tooa toomake modifications est coût hello de ces modifications. notion Hello de « coût » est échangée hors tension par rapport à la quantité cluster hello peut être améliorée. Le coût est pris en compte lors du déplacement de services à des fins d’équilibrage, de défragmentation ou autres. Hello vise toomeet les exigences de hello Bonjour moins moyen d’interruption ou coûteuse. 

Le déplacement de services coûte au minimum du temps processeur et de la bande passante réseau. Pour les services avec état, il requiert la copie état hello de ces services, l’utilisation du disque et mémoire supplémentaire. En réduisant les coûts de hello de solutions que hello Gestionnaire de ressources de Cluster Azure Service Fabric s’affiche avec permet de s’assurer que les ressources du cluster hello ne sont pas inutilement passées. Toutefois, vous n’également tooignore solutions sont d’améliorer considérablement l’allocation des ressources de cluster de hello hello.

Hello, Gestionnaire de ressources de Cluster de deux façons de coûts informatiques et en les limitant pendant qu’il essaie de cluster de hello toomanage. mécanisme de première Hello est simplement le comptage chaque déplacement serait. Si les deux solutions sont générées avec sur hello même équilibrer (score), puis hello Gestionnaire du Cluster de ressource préféré hello une avec hello plus faible coût (nombre total de déplacements).

Cette stratégie fonctionne bien. Mais, comme avec les charges par défaut ou statiques, il est peu probable dans n’importe quel système complexe que tous les déplacements soient égaux. Certaines sont probablement toobe beaucoup plus onéreuse.

## <a name="setting-move-costs"></a>Définir les coûts de déplacement 
Vous pouvez spécifier le coût du déplacement hello par défaut pour un service lors de sa création :

PowerShell :

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -DefaultMoveCost Medium
```

C# : 

```csharp
FabricClient fabricClient = new FabricClient();
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
//set up hello rest of hello ServiceDescription
serviceDescription.DefaultMoveCost = MoveCost.Medium;
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

Vous pouvez également spécifier ou mettre à jour MoveCost dynamiquement pour un service après que hello service a été créé : 

PowerShell : 

```posh
Update-ServiceFabricService -Stateful -ServiceName "fabric:/AppName/ServiceName" -DefaultMoveCost High
```

C# :

```csharp
StatefulServiceUpdateDescription updateDescription = new StatefulServiceUpdateDescription();
updateDescription.DefaultMoveCost = MoveCost.High;
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/AppName/ServiceName"), updateDescription);
```

## <a name="dynamically-specifying-move-cost-on-a-per-replica-basis"></a>Spécifier dynamiquement le coût de déplacement pour chaque réplica

Hello des extraits de code précédents sont tous pour la spécification MoveCost pour un service entier en une seule fois à partir de service externe hello proprement dit. Toutefois, déplacez le coût est plus utile est lorsque coût du déplacement d’un objet de service spécifique hello change au fil de sa durée de vie. Puisque hello services eux-mêmes probablement judicieux de hello coût se toomove un moment donné, il est une API pour tooreport services leur propres mouvement coût pendant l’exécution. 

C# :

```csharp
this.Partition.ReportMoveCost(MoveCost.Medium);
```

## <a name="impact-of-move-cost"></a>Impact du coût de déplacement
MoveCost a quatre niveaux : zéro, faible, moyen et élevé. MoveCosts sont relatif tooeach autre, à l’exception de zéro. Aucun coût de déplacement signifie que le déplacement des sont gratuit et ne doivent pas compter sur le score hello de solution de hello. Paramètre que vous déplacez votre coût tooHigh est *pas* garantit que le réplica hello reste dans un seul emplacement.

<center>
![Coût du déplacement comme facteur de sélection des réplicas pour les déplacements][Image1]
</center>

MoveCost vous permet de trouver des solutions hello que cause hello globale des minimiser les interruptions et tooachieve plus simple lors toujours arrivant au solde équivalent. Notion d’un service de coût peut être réduire relatif. Hello facteurs courants dans le calcul du coût du déplacement sont :

- quantité de Hello d’état ou les données que le service de hello a toomove.
- coût de Hello de déconnexion des clients. Déplacement d’un réplica principal est généralement plus coûteuse que coût hello de déplacement d’un réplica secondaire.
- coût Hello d’interruption d’une opération en cours. Certaines opérations sur les données de salutation stocker au niveau du ou des opérations dans l’appel de réponse tooa client sont coûteuses. Après un certain point, vous ne souhaitez pas toostop les si vous n’êtes pas obligé. Par conséquent, pendant les opération hello, vous augmentez coût du déplacement de cette probabilité hello tooreduce objet service qui il déplace hello. Lors de l’opération de hello, vous définissez toonormal arrière du coût hello.

## <a name="enabling-move-cost-in-your-cluster"></a>Activer le coût de déplacement dans un cluster
Dans l’ordre pour hello plus granulaire MoveCosts toobe pris en compte, MoveCost doit être activé dans votre cluster. Sans ce paramètre, le mode par défaut hello de comptage des déplacements est utilisé pour calculer MoveCost et MoveCost États sont ignorés.


ClusterManifest.xml :

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="UseMoveCostReports" Value="true" />
        </Section>
```

via ClusterConfig.json pour les déploiements autonomes ou Template.json pour les clusters hébergés sur Azure :

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "UseMoveCostReports",
          "value": "true"
      }
    ]
  }
]
```

## <a name="next-steps"></a>Étapes suivantes
- Gestionnaire de ressources du Cluster service Fabric utilise la capacité et la consommation de métriques toomanage dans un cluster de hello. toolearn plus d’informations sur les métriques et comment tooconfigure, extraire [la gestion de la consommation des ressources et les charge dans l’infrastructure de Service avec les mesures de](service-fabric-cluster-resource-manager-metrics.md).
- toolearn sur comment hello Gestionnaire de ressources de Cluster gère et équilibre la charge du cluster de hello, extraire [votre cluster Service Fabric d’équilibrage](service-fabric-cluster-resource-manager-balancing.md).

[Image1]:./media/service-fabric-cluster-resource-manager-movement-cost/service-most-cost-example.png
