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
# <a name="placement-policies-for-service-fabric-services"></a><span data-ttu-id="d19cc-103">Stratégies de positionnement pour les services Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d19cc-103">Placement policies for service fabric services</span></span>
<span data-ttu-id="d19cc-104">Stratégies de positionnement sont des règles supplémentaires qui peuvent être utilisés toogovern placement du service dans certains scénarios spécifiques, moins courants.</span><span class="sxs-lookup"><span data-stu-id="d19cc-104">Placement policies are additional rules that can be used toogovern service placement in some specific, less-common scenarios.</span></span> <span data-ttu-id="d19cc-105">Voici quelques exemples de ces scénarios :</span><span class="sxs-lookup"><span data-stu-id="d19cc-105">Some examples of those scenarios are:</span></span>

- <span data-ttu-id="d19cc-106">Votre cluster Service Fabric s’étend sur différentes zones géographiques, par exemple avec plusieurs centres de données locaux ou dans différentes régions Azure</span><span class="sxs-lookup"><span data-stu-id="d19cc-106">Your Service Fabric cluster spans geographic distances, such as multiple on-premises datacenters or across Azure regions</span></span>
- <span data-ttu-id="d19cc-107">Votre environnement s’étend sur plusieurs zones du contrôle géopolitique ou légale ou certains autres cas où vous avez des limites de stratégie vous devez tooenforce</span><span class="sxs-lookup"><span data-stu-id="d19cc-107">Your environment spans multiple areas of geopolitical or legal control, or some other case where you have policy boundaries you need tooenforce</span></span>
- <span data-ttu-id="d19cc-108">Considérations de performances ou la latence de communication toolarge distances ou l’utilisation de liaisons de réseau plus lentes ou peu fiable</span><span class="sxs-lookup"><span data-stu-id="d19cc-108">There are communication performance or latency considerations due toolarge distances or use of slower or less reliable network links</span></span>
- <span data-ttu-id="d19cc-109">Vous devez tookeep certaine charges de travail colocalisée comme une meilleure possibilité, avec les autres charges de travail ou de proximité toocustomers</span><span class="sxs-lookup"><span data-stu-id="d19cc-109">You need tookeep certain workloads collocated as a best effort, either with other workloads or in proximity toocustomers</span></span>

<span data-ttu-id="d19cc-110">La plupart de ces exigences s’aligner avec la disposition physique de hello du cluster hello, représentée comme hello domaines de défaillance de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="d19cc-110">Most of these requirements align with hello physical layout of hello cluster, represented as hello fault domains of hello cluster.</span></span> 

<span data-ttu-id="d19cc-111">Hello avancée des stratégies de positionnement qui contribuent à résoudre que ces scénarios sont :</span><span class="sxs-lookup"><span data-stu-id="d19cc-111">hello advanced placement policies that help address these scenarios are:</span></span>

1. <span data-ttu-id="d19cc-112">Domaines non valides</span><span class="sxs-lookup"><span data-stu-id="d19cc-112">Invalid domains</span></span>
2. <span data-ttu-id="d19cc-113">Domaines requis</span><span class="sxs-lookup"><span data-stu-id="d19cc-113">Required domains</span></span>
3. <span data-ttu-id="d19cc-114">Domaines par défaut</span><span class="sxs-lookup"><span data-stu-id="d19cc-114">Preferred domains</span></span>
4. <span data-ttu-id="d19cc-115">Désactivation de la compression de réplica</span><span class="sxs-lookup"><span data-stu-id="d19cc-115">Disallowing replica packing</span></span>

<span data-ttu-id="d19cc-116">La plupart des hello les contrôles peut être configurée via les propriétés de nœud et les contraintes de placement, mais certaines sont plus complexes.</span><span class="sxs-lookup"><span data-stu-id="d19cc-116">Most of hello following controls could be configured via node properties and placement constraints, but some are more complicated.</span></span> <span data-ttu-id="d19cc-117">toomake les choses plus simples, hello Gestionnaire de ressources du Cluster Service Fabric fournit ces stratégies de positionnement supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="d19cc-117">toomake things simpler, hello Service Fabric Cluster Resource Manager provides these additional placement policies.</span></span> <span data-ttu-id="d19cc-118">Les stratégies de positionnement sont configurées pour chaque instance de service nommée.</span><span class="sxs-lookup"><span data-stu-id="d19cc-118">Placement policies are configured on a per-named service instance basis.</span></span> <span data-ttu-id="d19cc-119">Elles peuvent également être mises à jour dynamiquement.</span><span class="sxs-lookup"><span data-stu-id="d19cc-119">They can also be updated dynamically.</span></span>

## <a name="specifying-invalid-domains"></a><span data-ttu-id="d19cc-120">Spécification de domaines non valides</span><span class="sxs-lookup"><span data-stu-id="d19cc-120">Specifying invalid domains</span></span>
<span data-ttu-id="d19cc-121">Hello **InvalidDomain** stratégie de positionnement vous permet de toospecify qu’un domaine d’erreur particulier n’est pas valide pour un service spécifique.</span><span class="sxs-lookup"><span data-stu-id="d19cc-121">hello **InvalidDomain** placement policy allows you toospecify that a particular Fault Domain is invalid for a specific service.</span></span> <span data-ttu-id="d19cc-122">Cette stratégie garantit qu’un service particulier ne s’exécute jamais dans une zone particulière, par exemple pour des raisons de stratégie géopolitiques ou d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="d19cc-122">This policy ensures that a particular service never runs in a particular area, for example for geopolitical or corporate policy reasons.</span></span> <span data-ttu-id="d19cc-123">Vous pouvez spécifier plusieurs domaines non valides par le biais de différentes stratégies.</span><span class="sxs-lookup"><span data-stu-id="d19cc-123">Multiple invalid domains may be specified via separate policies.</span></span>

<span data-ttu-id="d19cc-124"><center>
![Exemple de domaine non valide][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="d19cc-124"><center>
![Invalid Domain Example][Image1]
</center></span></span>

<span data-ttu-id="d19cc-125">Code :</span><span class="sxs-lookup"><span data-stu-id="d19cc-125">Code:</span></span>

```csharp
ServicePlacementInvalidDomainPolicyDescription invalidDomain = new ServicePlacementInvalidDomainPolicyDescription();
invalidDomain.DomainName = "fd:/DCEast"; //regulations prohibit this workload here
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

<span data-ttu-id="d19cc-126">PowerShell :</span><span class="sxs-lookup"><span data-stu-id="d19cc-126">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("InvalidDomain,fd:/DCEast”)
```
## <a name="specifying-required-domains"></a><span data-ttu-id="d19cc-127">Spécification de domaines obligatoires</span><span class="sxs-lookup"><span data-stu-id="d19cc-127">Specifying required domains</span></span>
<span data-ttu-id="d19cc-128">Hello requis la stratégie de positionnement de domaine nécessite que le service de hello est présent uniquement dans le domaine spécifié de hello.</span><span class="sxs-lookup"><span data-stu-id="d19cc-128">hello required domain placement policy requires that hello service is present only in hello specified domain.</span></span> <span data-ttu-id="d19cc-129">Vous pouvez spécifier plusieurs domaines obligatoires par le biais de différentes stratégies.</span><span class="sxs-lookup"><span data-stu-id="d19cc-129">Multiple required domains can be specified via separate policies.</span></span>

<span data-ttu-id="d19cc-130"><center>
![Exemple de domaine requis][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="d19cc-130"><center>
![Required Domain Example][Image2]
</center></span></span>

<span data-ttu-id="d19cc-131">Code :</span><span class="sxs-lookup"><span data-stu-id="d19cc-131">Code:</span></span>

```csharp
ServicePlacementRequiredDomainPolicyDescription requiredDomain = new ServicePlacementRequiredDomainPolicyDescription();
requiredDomain.DomainName = "fd:/DC01/RK03/BL2";
serviceDescription.PlacementPolicies.Add(requiredDomain);
```

<span data-ttu-id="d19cc-132">PowerShell :</span><span class="sxs-lookup"><span data-stu-id="d19cc-132">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomain,fd:/DC01/RK03/BL2")
```

## <a name="specifying-a-preferred-domain-for-hello-primary-replicas-of-a-stateful-service"></a><span data-ttu-id="d19cc-133">Spécification d’un domaine par défaut pour les réplicas de hello principal d’un service avec état</span><span class="sxs-lookup"><span data-stu-id="d19cc-133">Specifying a preferred domain for hello primary replicas of a stateful service</span></span>
<span data-ttu-id="d19cc-134">Hello principal de domaine par défaut spécifie hello erreur domaine tooplace hello principal dans.</span><span class="sxs-lookup"><span data-stu-id="d19cc-134">hello Preferred Primary Domain specifies hello fault domain tooplace hello Primary in.</span></span> <span data-ttu-id="d19cc-135">Hello principal finit dans ce domaine lorsque tout fonctionne correctement.</span><span class="sxs-lookup"><span data-stu-id="d19cc-135">hello Primary ends up in this domain when everything is healthy.</span></span> <span data-ttu-id="d19cc-136">Si le domaine de hello ou le réplica principal de hello échoue ou s’arrête, hello principal déplace toosome tout autre emplacement, dans l’idéal, dans hello même domaine.</span><span class="sxs-lookup"><span data-stu-id="d19cc-136">If hello domain or hello Primary replica fails or shuts down, hello Primary moves toosome other location, ideally in hello same domain.</span></span> <span data-ttu-id="d19cc-137">Si cet emplacement n’est pas dans le domaine par défaut de hello, hello se déplace du Gestionnaire de ressources de Cluster à nouveau domaine par défaut de toohello dès que possible.</span><span class="sxs-lookup"><span data-stu-id="d19cc-137">If this new location isn't in hello preferred domain, hello Cluster Resource Manager moves it back toohello preferred domain as soon as possible.</span></span> <span data-ttu-id="d19cc-138">Naturellement, ce paramètre convient uniquement aux services avec état.</span><span class="sxs-lookup"><span data-stu-id="d19cc-138">Naturally this setting only makes sense for stateful services.</span></span> <span data-ttu-id="d19cc-139">Cette stratégie est particulièrement utile dans les clusters qui sont répartis entre plusieurs centres de données ou régions Azure, mais vous préférez que des services soient placés dans un emplacement donné.</span><span class="sxs-lookup"><span data-stu-id="d19cc-139">This policy is most useful in clusters that are spanned across Azure regions or multiple datacenters but have services that prefer placement in a certain location.</span></span> <span data-ttu-id="d19cc-140">Conservation indistinctement ferme tootheir utilisateurs ou autres services offre une latence plus faible, en particulier pour les lectures, qui sont gérées par des couleurs primaires par défaut.</span><span class="sxs-lookup"><span data-stu-id="d19cc-140">Keeping Primaries close tootheir users or other services helps provide lower latency, especially for reads, which are handled by Primaries by default.</span></span>

<span data-ttu-id="d19cc-141"><center>
![Basculement et domaines principaux préférés][Image3]
</center></span><span class="sxs-lookup"><span data-stu-id="d19cc-141"><center>
![Preferred Primary Domains and Failover][Image3]
</center></span></span>

```csharp
ServicePlacementPreferPrimaryDomainPolicyDescription primaryDomain = new ServicePlacementPreferPrimaryDomainPolicyDescription();
primaryDomain.DomainName = "fd:/EastUS/";
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

<span data-ttu-id="d19cc-142">PowerShell :</span><span class="sxs-lookup"><span data-stu-id="d19cc-142">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("PreferredPrimaryDomain,fd:/EastUS")
```

## <a name="requiring-replica-distribution-and-disallowing-packing"></a><span data-ttu-id="d19cc-143">Nécessite une distribution des réplicas et l’interdiction de la compression</span><span class="sxs-lookup"><span data-stu-id="d19cc-143">Requiring replica distribution and disallowing packing</span></span>
<span data-ttu-id="d19cc-144">Les réplicas sont _normalement_ distribué sur plusieurs domaines d’erreur et de mise à niveau lorsque le cluster de hello est sain.</span><span class="sxs-lookup"><span data-stu-id="d19cc-144">Replicas are _normally_ distributed across fault and upgrade domains when hello cluster is healthy.</span></span> <span data-ttu-id="d19cc-145">Toutefois, il peut arriver que plusieurs réplicas d’une partition donnée finissent par être temporairement compressés dans un domaine unique.</span><span class="sxs-lookup"><span data-stu-id="d19cc-145">However, there are cases where more than one replica for a given partition may end up temporarily packed into a single domain.</span></span> <span data-ttu-id="d19cc-146">Par exemple, supposons que ce cluster hello a neuf nœuds dans trois domaines d’erreur, fd : / 0, fd : / 1 et fd : / 2.</span><span class="sxs-lookup"><span data-stu-id="d19cc-146">For example, let's say that hello cluster has nine nodes in three fault domains, fd:/0, fd:/1, and fd:/2.</span></span> <span data-ttu-id="d19cc-147">Supposons également que votre service comporte trois réplicas.</span><span class="sxs-lookup"><span data-stu-id="d19cc-147">Let's also say that your service has three replicas.</span></span> <span data-ttu-id="d19cc-148">Supposons que hello nœuds qui ont été utilisés pour les réplicas dans fd : / 1 et fd : / 2 s’est arrêté.</span><span class="sxs-lookup"><span data-stu-id="d19cc-148">Let's say that hello nodes that were being used for those replicas in fd:/1 and fd:/2 went down.</span></span> <span data-ttu-id="d19cc-149">Normalement hello Gestionnaire de ressources du Cluster préférez des autres nœuds dans ces domaines d’erreur même.</span><span class="sxs-lookup"><span data-stu-id="d19cc-149">Normally hello Cluster Resource Manager would prefer other nodes in those same fault domains.</span></span> <span data-ttu-id="d19cc-150">Dans ce cas, supposons qu’en raison de problèmes de toocapacity aucun Hello autres nœuds dans ces domaines sont valides.</span><span class="sxs-lookup"><span data-stu-id="d19cc-150">In this case, let's say due toocapacity issues none of hello other nodes in those domains were valid.</span></span> <span data-ttu-id="d19cc-151">Si hello Gestionnaire de ressources de Cluster génère des remplacements pour ces réplicas, cela aurait toochoose nœuds fd : / 0.</span><span class="sxs-lookup"><span data-stu-id="d19cc-151">If hello Cluster Resource Manager builds replacements for those replicas, it would have toochoose nodes in fd:/0.</span></span> <span data-ttu-id="d19cc-152">Toutefois, en effectuant _qui_ crée une situation où hello contrainte de domaine d’erreur est violée.</span><span class="sxs-lookup"><span data-stu-id="d19cc-152">However, doing _that_ creates a situation where hello Fault Domain constraint is violated.</span></span> <span data-ttu-id="d19cc-153">Compression augmente de réplicas risques hello hello du jeu de réplicas entier peut tomber en panne ou être perdues.</span><span class="sxs-lookup"><span data-stu-id="d19cc-153">Packing replicas increases hello chance that hello whole replica set could go down or be lost.</span></span> 

> [!NOTE]
> <span data-ttu-id="d19cc-154">Pour plus d’informations sur les contraintes et les priorités de contraintes en général, consultez [cette rubrique](service-fabric-cluster-resource-manager-management-integration.md#constraint-priorities).</span><span class="sxs-lookup"><span data-stu-id="d19cc-154">For more information on constraints and constraint priorities generally, check out [this topic](service-fabric-cluster-resource-manager-management-integration.md#constraint-priorities).</span></span>
>

<span data-ttu-id="d19cc-155">Si vous avez déjà vu un message d’intégrité comme « `hello Load Balancer has detected a Constraint Violation for this Replica:fabric:/<some service name> Secondary Partition <some partition ID> is violating hello Constraint: FaultDomain` », vous avez rencontré cette situation ou quelque chose de semblable.</span><span class="sxs-lookup"><span data-stu-id="d19cc-155">If you've ever seen a health message such as "`hello Load Balancer has detected a Constraint Violation for this Replica:fabric:/<some service name> Secondary Partition <some partition ID> is violating hello Constraint: FaultDomain`", then you've hit this condition or something like it.</span></span> <span data-ttu-id="d19cc-156">En général, un ou deux réplicas sont temporairement compressés ensemble.</span><span class="sxs-lookup"><span data-stu-id="d19cc-156">Usually only one or two replicas are packed together temporarily.</span></span> <span data-ttu-id="d19cc-157">Tant qu’il y a moins de répliquas que le quorum d’un domaine donné, vous êtes en sécurité.</span><span class="sxs-lookup"><span data-stu-id="d19cc-157">So long as there are fewer than a quorum of replicas in a given domain, you're safe.</span></span> <span data-ttu-id="d19cc-158">Compression est rare, mais il peut se produire, et ces situations sont généralement transitoires dans la mesure où les nœuds hello reviennent.</span><span class="sxs-lookup"><span data-stu-id="d19cc-158">Packing is rare, but it can happen, and usually these situations are transient since hello nodes come back.</span></span> <span data-ttu-id="d19cc-159">Si les nœuds hello restent bas et hello Gestionnaire de ressources du Cluster doit toobuild remplacements, généralement sont autres nœuds disponibles dans des domaines d’erreur idéale hello.</span><span class="sxs-lookup"><span data-stu-id="d19cc-159">If hello nodes do stay down and hello Cluster Resource Manager needs toobuild replacements, usually there are other nodes available in hello ideal fault domains.</span></span>

<span data-ttu-id="d19cc-160">Certaines charges de travail choix disposer en permanence nombre cible de hello de réplicas, même si elles sont empaquetés dans moins de domaines.</span><span class="sxs-lookup"><span data-stu-id="d19cc-160">Some workloads would prefer always having hello target number of replicas, even if they are packed into fewer domains.</span></span> <span data-ttu-id="d19cc-161">Ces charges de travail sont supposent que des pannes de domaine simultanées totales ne surviendront pas, et peuvent généralement récupérer l’état local.</span><span class="sxs-lookup"><span data-stu-id="d19cc-161">These workloads are betting against total simultaneous permanent domain failures and can usually recover local state.</span></span> <span data-ttu-id="d19cc-162">Autres charges de travail seraient plutôt planifier hello temps d’arrêt antérieure à l’exactitude des risques ou des pertes de données.</span><span class="sxs-lookup"><span data-stu-id="d19cc-162">Other workloads would rather take hello downtime earlier than risk correctness or loss of data.</span></span> <span data-ttu-id="d19cc-163">La plupart des charges de travail s’exécutent avec plus de trois réplicas, plus de trois domaines d’erreur et plusieurs nœuds valides par domaine d’erreur.</span><span class="sxs-lookup"><span data-stu-id="d19cc-163">Most production workloads run with more than three replicas, more than three fault domains, and many valid nodes per fault domain.</span></span> <span data-ttu-id="d19cc-164">Pour cette raison, par défaut hello permet la compression de domaine par défaut.</span><span class="sxs-lookup"><span data-stu-id="d19cc-164">Because of this, hello default behavior allows domain packing by default.</span></span> <span data-ttu-id="d19cc-165">comportement par défaut de Hello permet l’équilibrage et basculement toohandle ces cas extrêmes, même si cela implique la livraison de domaine temporaire.</span><span class="sxs-lookup"><span data-stu-id="d19cc-165">hello default behavior allows normal balancing and failover toohandle these extreme cases, even if that means temporary domain packing.</span></span>

<span data-ttu-id="d19cc-166">Si vous souhaitez toodisable ce type de compression pour une charge de travail donné, vous pouvez spécifier hello `RequireDomainDistribution` stratégie sur hello service.</span><span class="sxs-lookup"><span data-stu-id="d19cc-166">If you want toodisable such packing for a given workload, you can specify hello `RequireDomainDistribution` policy on hello service.</span></span> <span data-ttu-id="d19cc-167">Lorsque cette stratégie est définie, hello Gestionnaire de ressources de Cluster ne garantit aucune deux réplicas de hello même partition exécuter Bonjour même d’erreur ou à mettre à niveau du domaine.</span><span class="sxs-lookup"><span data-stu-id="d19cc-167">When this policy is set, hello Cluster Resource Manager ensures no two replicas from hello same partition run in hello same fault or upgrade domain.</span></span>

<span data-ttu-id="d19cc-168">Code :</span><span class="sxs-lookup"><span data-stu-id="d19cc-168">Code:</span></span>

```csharp
ServicePlacementRequireDomainDistributionPolicyDescription distributeDomain = new ServicePlacementRequireDomainDistributionPolicyDescription();
serviceDescription.PlacementPolicies.Add(distributeDomain);
```

<span data-ttu-id="d19cc-169">PowerShell :</span><span class="sxs-lookup"><span data-stu-id="d19cc-169">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomainDistribution")
```

<span data-ttu-id="d19cc-170">À présent, il serait être toouse possible de ces configurations pour les services dans un cluster qui n’était pas géographiquement fractionnés ?</span><span class="sxs-lookup"><span data-stu-id="d19cc-170">Now, would it be possible toouse these configurations for services in a cluster that was not geographically spanned?</span></span> <span data-ttu-id="d19cc-171">Oui, mais il n’y a pas de bonne raison de le faire.</span><span class="sxs-lookup"><span data-stu-id="d19cc-171">You could, but there’s not a great reason too.</span></span> <span data-ttu-id="d19cc-172">Hello configurations de domaine requis, non valide et par défaut doivent être évitées, sauf si les scénarios de hello ont besoin.</span><span class="sxs-lookup"><span data-stu-id="d19cc-172">hello required, invalid, and preferred domain configurations should be avoided unless hello scenarios require them.</span></span> <span data-ttu-id="d19cc-173">Il ne rend pas une charge de travail donnée de toorun tout tooforce tootry de sens dans un seul rack ou tooprefer plusieurs segments de votre cluster local vers un autre.</span><span class="sxs-lookup"><span data-stu-id="d19cc-173">It doesn't make any sense tootry tooforce a given workload toorun in a single rack, or tooprefer some segment of your local cluster over another.</span></span> <span data-ttu-id="d19cc-174">Différentes configurations matérielles doivent être réparties sur plusieurs domaines d’erreur et gérées par les contraintes de placement et les propriétés de nœud normales.</span><span class="sxs-lookup"><span data-stu-id="d19cc-174">Different hardware configurations should be spread across fault domains and handled via normal placement constraints and node properties.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d19cc-175">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d19cc-175">Next steps</span></span>
- <span data-ttu-id="d19cc-176">Pour plus d’informations sur la configuration des services, consultez la rubrique [En savoir plus sur la configuration des services](service-fabric-cluster-resource-manager-configure-services.md)</span><span class="sxs-lookup"><span data-stu-id="d19cc-176">For more information on configuring services, [Learn about configuring Services](service-fabric-cluster-resource-manager-configure-services.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-invalid-placement-domain.png
[Image2]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-required-placement-domain.png
[Image3]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-preferred-primary-domain.png
