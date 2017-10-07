---
title: "aaaService Gestionnaire de ressources de Cluster de l’ensemble fibre optique - stratégies de positionnement | Documents Microsoft"
description: "Vue d’ensemble des autres règles et stratégies de positionnement pour les services Service Fabric"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 5c2d19c6-dd40-4c4b-abd3-5c5ec0abed38
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: bb58642520085ab3000f3929cf9aea7a8f6e3070
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="placement-policies-for-service-fabric-services"></a>Stratégies de positionnement pour les services Service Fabric
Stratégies de positionnement sont des règles supplémentaires qui peuvent être utilisés toogovern placement du service dans certains scénarios spécifiques, moins courants. Voici quelques exemples de ces scénarios :

- Votre cluster Service Fabric s’étend sur différentes zones géographiques, par exemple avec plusieurs centres de données locaux ou dans différentes régions Azure
- Votre environnement s’étend sur plusieurs zones du contrôle géopolitique ou légale ou certains autres cas où vous avez des limites de stratégie vous devez tooenforce
- Considérations de performances ou la latence de communication toolarge distances ou l’utilisation de liaisons de réseau plus lentes ou peu fiable
- Vous devez tookeep certaine charges de travail colocalisée comme une meilleure possibilité, avec les autres charges de travail ou de proximité toocustomers

La plupart de ces exigences s’aligner avec la disposition physique de hello du cluster hello, représentée comme hello domaines de défaillance de cluster de hello. 

Hello avancée des stratégies de positionnement qui contribuent à résoudre que ces scénarios sont :

1. Domaines non valides
2. Domaines requis
3. Domaines par défaut
4. Désactivation de la compression de réplica

La plupart des hello les contrôles peut être configurée via les propriétés de nœud et les contraintes de placement, mais certaines sont plus complexes. toomake les choses plus simples, hello Gestionnaire de ressources du Cluster Service Fabric fournit ces stratégies de positionnement supplémentaires. Les stratégies de positionnement sont configurées pour chaque instance de service nommée. Elles peuvent également être mises à jour dynamiquement.

## <a name="specifying-invalid-domains"></a>Spécification de domaines non valides
Hello **InvalidDomain** stratégie de positionnement vous permet de toospecify qu’un domaine d’erreur particulier n’est pas valide pour un service spécifique. Cette stratégie garantit qu’un service particulier ne s’exécute jamais dans une zone particulière, par exemple pour des raisons de stratégie géopolitiques ou d’entreprise. Vous pouvez spécifier plusieurs domaines non valides par le biais de différentes stratégies.

<center>
![Exemple de domaine non valide][Image1]
</center>

Code :

```csharp
ServicePlacementInvalidDomainPolicyDescription invalidDomain = new ServicePlacementInvalidDomainPolicyDescription();
invalidDomain.DomainName = "fd:/DCEast"; //regulations prohibit this workload here
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

PowerShell :

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("InvalidDomain,fd:/DCEast”)
```
## <a name="specifying-required-domains"></a>Spécification de domaines obligatoires
Hello requis la stratégie de positionnement de domaine nécessite que le service de hello est présent uniquement dans le domaine spécifié de hello. Vous pouvez spécifier plusieurs domaines obligatoires par le biais de différentes stratégies.

<center>
![Exemple de domaine requis][Image2]
</center>

Code :

```csharp
ServicePlacementRequiredDomainPolicyDescription requiredDomain = new ServicePlacementRequiredDomainPolicyDescription();
requiredDomain.DomainName = "fd:/DC01/RK03/BL2";
serviceDescription.PlacementPolicies.Add(requiredDomain);
```

PowerShell :

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomain,fd:/DC01/RK03/BL2")
```

## <a name="specifying-a-preferred-domain-for-hello-primary-replicas-of-a-stateful-service"></a>Spécification d’un domaine par défaut pour les réplicas de hello principal d’un service avec état
Hello principal de domaine par défaut spécifie hello erreur domaine tooplace hello principal dans. Hello principal finit dans ce domaine lorsque tout fonctionne correctement. Si le domaine de hello ou le réplica principal de hello échoue ou s’arrête, hello principal déplace toosome tout autre emplacement, dans l’idéal, dans hello même domaine. Si cet emplacement n’est pas dans le domaine par défaut de hello, hello se déplace du Gestionnaire de ressources de Cluster à nouveau domaine par défaut de toohello dès que possible. Naturellement, ce paramètre convient uniquement aux services avec état. Cette stratégie est particulièrement utile dans les clusters qui sont répartis entre plusieurs centres de données ou régions Azure, mais vous préférez que des services soient placés dans un emplacement donné. Conservation indistinctement ferme tootheir utilisateurs ou autres services offre une latence plus faible, en particulier pour les lectures, qui sont gérées par des couleurs primaires par défaut.

<center>
![Basculement et domaines principaux préférés][Image3]
</center>

```csharp
ServicePlacementPreferPrimaryDomainPolicyDescription primaryDomain = new ServicePlacementPreferPrimaryDomainPolicyDescription();
primaryDomain.DomainName = "fd:/EastUS/";
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

PowerShell :

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("PreferredPrimaryDomain,fd:/EastUS")
```

## <a name="requiring-replica-distribution-and-disallowing-packing"></a>Nécessite une distribution des réplicas et l’interdiction de la compression
Les réplicas sont _normalement_ distribué sur plusieurs domaines d’erreur et de mise à niveau lorsque le cluster de hello est sain. Toutefois, il peut arriver que plusieurs réplicas d’une partition donnée finissent par être temporairement compressés dans un domaine unique. Par exemple, supposons que ce cluster hello a neuf nœuds dans trois domaines d’erreur, fd : / 0, fd : / 1 et fd : / 2. Supposons également que votre service comporte trois réplicas. Supposons que hello nœuds qui ont été utilisés pour les réplicas dans fd : / 1 et fd : / 2 s’est arrêté. Normalement hello Gestionnaire de ressources du Cluster préférez des autres nœuds dans ces domaines d’erreur même. Dans ce cas, supposons qu’en raison de problèmes de toocapacity aucun Hello autres nœuds dans ces domaines sont valides. Si hello Gestionnaire de ressources de Cluster génère des remplacements pour ces réplicas, cela aurait toochoose nœuds fd : / 0. Toutefois, en effectuant _qui_ crée une situation où hello contrainte de domaine d’erreur est violée. Compression augmente de réplicas risques hello hello du jeu de réplicas entier peut tomber en panne ou être perdues. 

> [!NOTE]
> Pour plus d’informations sur les contraintes et les priorités de contraintes en général, consultez [cette rubrique](service-fabric-cluster-resource-manager-management-integration.md#constraint-priorities).
>

Si vous avez déjà vu un message d’intégrité comme « `hello Load Balancer has detected a Constraint Violation for this Replica:fabric:/<some service name> Secondary Partition <some partition ID> is violating hello Constraint: FaultDomain` », vous avez rencontré cette situation ou quelque chose de semblable. En général, un ou deux réplicas sont temporairement compressés ensemble. Tant qu’il y a moins de répliquas que le quorum d’un domaine donné, vous êtes en sécurité. Compression est rare, mais il peut se produire, et ces situations sont généralement transitoires dans la mesure où les nœuds hello reviennent. Si les nœuds hello restent bas et hello Gestionnaire de ressources du Cluster doit toobuild remplacements, généralement sont autres nœuds disponibles dans des domaines d’erreur idéale hello.

Certaines charges de travail choix disposer en permanence nombre cible de hello de réplicas, même si elles sont empaquetés dans moins de domaines. Ces charges de travail sont supposent que des pannes de domaine simultanées totales ne surviendront pas, et peuvent généralement récupérer l’état local. Autres charges de travail seraient plutôt planifier hello temps d’arrêt antérieure à l’exactitude des risques ou des pertes de données. La plupart des charges de travail s’exécutent avec plus de trois réplicas, plus de trois domaines d’erreur et plusieurs nœuds valides par domaine d’erreur. Pour cette raison, par défaut hello permet la compression de domaine par défaut. comportement par défaut de Hello permet l’équilibrage et basculement toohandle ces cas extrêmes, même si cela implique la livraison de domaine temporaire.

Si vous souhaitez toodisable ce type de compression pour une charge de travail donné, vous pouvez spécifier hello `RequireDomainDistribution` stratégie sur hello service. Lorsque cette stratégie est définie, hello Gestionnaire de ressources de Cluster ne garantit aucune deux réplicas de hello même partition exécuter Bonjour même d’erreur ou à mettre à niveau du domaine.

Code :

```csharp
ServicePlacementRequireDomainDistributionPolicyDescription distributeDomain = new ServicePlacementRequireDomainDistributionPolicyDescription();
serviceDescription.PlacementPolicies.Add(distributeDomain);
```

PowerShell :

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomainDistribution")
```

À présent, il serait être toouse possible de ces configurations pour les services dans un cluster qui n’était pas géographiquement fractionnés ? Oui, mais il n’y a pas de bonne raison de le faire. Hello configurations de domaine requis, non valide et par défaut doivent être évitées, sauf si les scénarios de hello ont besoin. Il ne rend pas une charge de travail donnée de toorun tout tooforce tootry de sens dans un seul rack ou tooprefer plusieurs segments de votre cluster local vers un autre. Différentes configurations matérielles doivent être réparties sur plusieurs domaines d’erreur et gérées par les contraintes de placement et les propriétés de nœud normales.

## <a name="next-steps"></a>Étapes suivantes
- Pour plus d’informations sur la configuration des services, consultez la rubrique [En savoir plus sur la configuration des services](service-fabric-cluster-resource-manager-configure-services.md)

[Image1]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-invalid-placement-domain.png
[Image2]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-required-placement-domain.png
[Image3]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-preferred-primary-domain.png
