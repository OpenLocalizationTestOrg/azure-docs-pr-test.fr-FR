---
title: "Utilisation des rapports d’intégrité du système pour la résolution des problèmes | Microsoft Docs"
description: "Décrit les rapports d’intégrité envoyés par les composants Azure Service Fabric et leur utilisation pour la résolution des problèmes de cluster ou d’application."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: 52574ea7-eb37-47e0-a20a-101539177625
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: oanapl
ms.openlocfilehash: 54e20146b2f1e0ca6153b66319be70c6f7c2fb59
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="use-system-health-reports-to-troubleshoot"></a><span data-ttu-id="fd96a-103">Utiliser les rapports d’intégrité du système pour la résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="fd96a-103">Use system health reports to troubleshoot</span></span>
<span data-ttu-id="fd96a-104">Les composants Azure Service Fabric signalent sans configuration l’intégrité de toutes les entités du cluster.</span><span class="sxs-lookup"><span data-stu-id="fd96a-104">Azure Service Fabric components report out of the box on all entities in the cluster.</span></span> <span data-ttu-id="fd96a-105">Le [magasin d’intégrité](service-fabric-health-introduction.md#health-store) crée et supprime des entités en fonction des rapports du système.</span><span class="sxs-lookup"><span data-stu-id="fd96a-105">The [health store](service-fabric-health-introduction.md#health-store) creates and deletes entities based on the system reports.</span></span> <span data-ttu-id="fd96a-106">Il les organise au sein d’une hiérarchie qui tient compte des interactions entre les entités.</span><span class="sxs-lookup"><span data-stu-id="fd96a-106">It also organizes them in a hierarchy that captures entity interactions.</span></span>

> [!NOTE]
> <span data-ttu-id="fd96a-107">Pour mieux comprendre les concepts relatifs à l’intégrité, consultez la documentation relative au [modèle d’intégrité du Service Fabric](service-fabric-health-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fd96a-107">To understand health-related concepts, read more at [Service Fabric health model](service-fabric-health-introduction.md).</span></span>
> 
> 

<span data-ttu-id="fd96a-108">Les rapports d’intégrité du système procurent une visibilité sur les fonctionnalités du cluster et des applications, et signalent les problèmes d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="fd96a-108">System health reports provide visibility into cluster and application functionality and flag issues through health.</span></span> <span data-ttu-id="fd96a-109">Pour les applications et services, les rapports d’intégrité du système vérifient que les entités sont implémentées et qu’elles se comportent correctement du point de vue de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="fd96a-109">For applications and services, system health reports verify that entities are implemented and are behaving correctly from the Service Fabric perspective.</span></span> <span data-ttu-id="fd96a-110">Le rapport ne fournit aucune information sur l’intégrité de la logique métier du service ni sur la détection des processus bloqués.</span><span class="sxs-lookup"><span data-stu-id="fd96a-110">The reports do not provide any health monitoring of the business logic of the service or detection of hung processes.</span></span> <span data-ttu-id="fd96a-111">Les services utilisateur peuvent enrichir les données d’intégrité avec des informations spécifiques à leur logique.</span><span class="sxs-lookup"><span data-stu-id="fd96a-111">User services can enrich the health data with information specific to their logic.</span></span>

> [!NOTE]
> <span data-ttu-id="fd96a-112">Les rapports de surveillance d’intégrité sont visibles uniquement *après* que les composants système ont créé une entité.</span><span class="sxs-lookup"><span data-stu-id="fd96a-112">Watchdogs health reports are visible only *after* the system components create an entity.</span></span> <span data-ttu-id="fd96a-113">Lorsqu’une entité est supprimée, le magasin d’intégrité élimine automatiquement l’ensemble des rapports d’intégrité qui lui sont associés.</span><span class="sxs-lookup"><span data-stu-id="fd96a-113">When an entity is deleted, the health store automatically deletes all health reports associated with it.</span></span> <span data-ttu-id="fd96a-114">Cela vaut également quand une nouvelle instance de l’entité est créée (par exemple une nouvelle instance de réplica de service avec état persistant est créée).</span><span class="sxs-lookup"><span data-stu-id="fd96a-114">The same is true when a new instance of the entity is created (for example, a new stateful persisted service replica instance is created).</span></span> <span data-ttu-id="fd96a-115">Tous les rapports associés à l’ancienne instance sont supprimés et éliminés du magasin.</span><span class="sxs-lookup"><span data-stu-id="fd96a-115">All reports associated with the old instance are deleted and cleaned up from the store.</span></span>
> 
> 

<span data-ttu-id="fd96a-116">Les rapports sur les composants système sont identifiés par la source, qui commence par le préfixe « **System.** »</span><span class="sxs-lookup"><span data-stu-id="fd96a-116">The system component reports are identified by the source, which starts with the "**System.**"</span></span> <span data-ttu-id="fd96a-117">.</span><span class="sxs-lookup"><span data-stu-id="fd96a-117">prefix.</span></span> <span data-ttu-id="fd96a-118">Les pilotes de surveillance ne peuvent pas utiliser le même préfixe pour leurs sources, car les rapports dotés de paramètres non valides sont rejetés.</span><span class="sxs-lookup"><span data-stu-id="fd96a-118">Watchdogs can't use the same prefix for their sources, as reports with invalid parameters are rejected.</span></span>
<span data-ttu-id="fd96a-119">Examinons certains rapports du système et tâchons d’identifier les éléments déclencheurs et d’imaginer des moyens de corriger les problèmes potentiels qu’ils représentent.</span><span class="sxs-lookup"><span data-stu-id="fd96a-119">Let's look at some system reports to understand what triggers them and how to correct the possible issues they represent.</span></span>

> [!NOTE]
> <span data-ttu-id="fd96a-120">Service Fabric continue d’ajouter des rapports sur les domaines d’intérêt qui améliorent la visibilité sur les événements associés au cluster et aux applications.</span><span class="sxs-lookup"><span data-stu-id="fd96a-120">Service Fabric continues to add reports on conditions of interest that improve visibility into what is happening in the cluster and application.</span></span> <span data-ttu-id="fd96a-121">Les rapports existants peuvent également être améliorés en offrant plus de détails pour vous aider à résoudre le problème plus rapidement.</span><span class="sxs-lookup"><span data-stu-id="fd96a-121">Existing reports can also be enhanced with more details to help troubleshoot the problem faster.</span></span>
> 
> 

## <a name="cluster-system-health-reports"></a><span data-ttu-id="fd96a-122">Rapports d’intégrité du système sur le cluster</span><span class="sxs-lookup"><span data-stu-id="fd96a-122">Cluster system health reports</span></span>
<span data-ttu-id="fd96a-123">L’entité d’intégrité du cluster est créée automatiquement dans le magasin d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="fd96a-123">The cluster health entity is created automatically in the health store.</span></span> <span data-ttu-id="fd96a-124">Si tout fonctionne correctement, elle ne présente pas de rapport système.</span><span class="sxs-lookup"><span data-stu-id="fd96a-124">If everything works properly, it doesn't have a system report.</span></span>

### <a name="neighborhood-loss"></a><span data-ttu-id="fd96a-125">Perte de voisinage</span><span class="sxs-lookup"><span data-stu-id="fd96a-125">Neighborhood loss</span></span>
<span data-ttu-id="fd96a-126">**System.Federation** indique une erreur s’il détecte une perte de voisinage.</span><span class="sxs-lookup"><span data-stu-id="fd96a-126">**System.Federation** reports an error when it detects a neighborhood loss.</span></span> <span data-ttu-id="fd96a-127">Le rapport est issu de nœuds individuels ; l’ID de nœud est inclus dans le nom de propriété.</span><span class="sxs-lookup"><span data-stu-id="fd96a-127">The report is from individual nodes, and the node ID is included in the property name.</span></span> <span data-ttu-id="fd96a-128">Si un voisinage est perdu dans l’ensemble de l’anneau de Service Fabric, deux événements sont généralement signalés (les deux côtés de l’intervalle indiquent une erreur).</span><span class="sxs-lookup"><span data-stu-id="fd96a-128">If one neighborhood is lost in the entire Service Fabric ring, you can typically expect two events (both sides of the gap report).</span></span> <span data-ttu-id="fd96a-129">Si plusieurs voisinages sont perdus, d’autres d’événements ont lieu.</span><span class="sxs-lookup"><span data-stu-id="fd96a-129">If more neighborhoods are lost, there are more events.</span></span>

<span data-ttu-id="fd96a-130">Le rapport spécifie le délai d’expiration du bail globale comme durée de vie.</span><span class="sxs-lookup"><span data-stu-id="fd96a-130">The report specifies the global lease timeout as the time to live.</span></span> <span data-ttu-id="fd96a-131">Il est renvoyé lorsque la moitié de la durée de vie est atteinte, tant que la condition reste active.</span><span class="sxs-lookup"><span data-stu-id="fd96a-131">The report is resent every half of the TTL duration for as long as the condition remains active.</span></span> <span data-ttu-id="fd96a-132">L’événement arrivé à expiration est automatiquement supprimé.</span><span class="sxs-lookup"><span data-stu-id="fd96a-132">The event is automatically removed when it expires.</span></span> <span data-ttu-id="fd96a-133">Le comportement de suppression à expiration garantit le nettoyage approprié du rapport dans le magasin d’intégrité, même si le nœud de création de rapports est arrêté.</span><span class="sxs-lookup"><span data-stu-id="fd96a-133">Remove when expired behavior ensures that the report is cleaned up from the health store correctly, even if the reporting node is down.</span></span>

* <span data-ttu-id="fd96a-134">**SourceId**: System.Federation.</span><span class="sxs-lookup"><span data-stu-id="fd96a-134">**SourceId**: System.Federation</span></span>
* <span data-ttu-id="fd96a-135">**Property** : commence par **Neighborhood** et inclut des informations sur le nœud.</span><span class="sxs-lookup"><span data-stu-id="fd96a-135">**Property**: Starts with **Neighborhood** and includes node information</span></span>
* <span data-ttu-id="fd96a-136">**Étapes suivantes**: recherchez ce qui a provoqué la perte de voisinage (par exemple, vérifiez la communication entre les nœuds du cluster).</span><span class="sxs-lookup"><span data-stu-id="fd96a-136">**Next steps**: Investigate why the neighborhood is lost (for example, check the communication between cluster nodes).</span></span>

## <a name="node-system-health-reports"></a><span data-ttu-id="fd96a-137">Rapports d’intégrité du système sur les nœuds</span><span class="sxs-lookup"><span data-stu-id="fd96a-137">Node system health reports</span></span>
<span data-ttu-id="fd96a-138">**System.FM**, qui représente le service Failover Manager, est l’autorité qui gère les informations sur les nœuds de cluster.</span><span class="sxs-lookup"><span data-stu-id="fd96a-138">**System.FM**, which represents the Failover Manager service, is the authority that manages information about cluster nodes.</span></span> <span data-ttu-id="fd96a-139">Un rapport System.FM indiquant son état doit être alloué à chaque nœud.</span><span class="sxs-lookup"><span data-stu-id="fd96a-139">Each node should have one report from System.FM showing its state.</span></span> <span data-ttu-id="fd96a-140">Les entités de nœud sont supprimées lorsque l’état du nœud est supprimé (consultez [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).</span><span class="sxs-lookup"><span data-stu-id="fd96a-140">The node entities are removed when the node state is removed (see [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).</span></span>

### <a name="node-updown"></a><span data-ttu-id="fd96a-141">Nœud activé/désactivé</span><span class="sxs-lookup"><span data-stu-id="fd96a-141">Node up/down</span></span>
<span data-ttu-id="fd96a-142">System.FM consigne la valeur OK lorsque le nœud rejoint l’anneau (il est opérationnel).</span><span class="sxs-lookup"><span data-stu-id="fd96a-142">System.FM reports as OK when the node joins the ring (it's up and running).</span></span> <span data-ttu-id="fd96a-143">Il indique une erreur lorsque le nœud quitte l’anneau (il est inactif, en raison d’une mise à niveau ou simplement d’une défaillance).</span><span class="sxs-lookup"><span data-stu-id="fd96a-143">It reports an error when the node departs the ring (it's down, either for upgrading or simply because it has failed).</span></span> <span data-ttu-id="fd96a-144">La hiérarchie d’intégrité développée par le magasin d’intégrité agit sur les entités déployées en corrélation avec les rapports sur les nœuds de System.FM.</span><span class="sxs-lookup"><span data-stu-id="fd96a-144">The health hierarchy built by the health store takes action on deployed entities in correlation with System.FM node reports.</span></span> <span data-ttu-id="fd96a-145">Elle traite le nœud comme un parent virtuel de toutes les entités déployées.</span><span class="sxs-lookup"><span data-stu-id="fd96a-145">It considers the node a virtual parent of all deployed entities.</span></span> <span data-ttu-id="fd96a-146">Les entités déployées sur ce nœud sont exposées via des requêtes si le nœud est indiqué comme actif par System/FM, avec la même instance comme instance associée aux entités.</span><span class="sxs-lookup"><span data-stu-id="fd96a-146">The deployed entities on that node are exposed through queries if the node is reported as up by System.FM, with the same instance as the instance associated with the entities.</span></span> <span data-ttu-id="fd96a-147">Lorsque System.FM fait état de l’inactivité ou du redémarrage du nœud (nouvelle instance), le magasin d’intégrité nettoie automatiquement les entités déployées qui peuvent exister uniquement sur le nœud inactif ou sur l’instance précédente du nœud.</span><span class="sxs-lookup"><span data-stu-id="fd96a-147">When System.FM reports that the node is down or restarted (a new instance), the health store automatically cleans up the deployed entities that can exist only on the down node or on the previous instance of the node.</span></span>

* <span data-ttu-id="fd96a-148">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="fd96a-148">**SourceId**: System.FM</span></span>
* <span data-ttu-id="fd96a-149">**Property**: State</span><span class="sxs-lookup"><span data-stu-id="fd96a-149">**Property**: State</span></span>
* <span data-ttu-id="fd96a-150">**Étapes suivantes**: si le nœud est inactif en raison d’une mise à niveau, il doit redevenir actif une fois l’opération terminée.</span><span class="sxs-lookup"><span data-stu-id="fd96a-150">**Next steps**: If the node is down for an upgrade, it should come back up once it has been upgraded.</span></span> <span data-ttu-id="fd96a-151">Dans ce cas, l’état d’intégrité doit repasser sur OK.</span><span class="sxs-lookup"><span data-stu-id="fd96a-151">In this case, the health state should switch back to OK.</span></span> <span data-ttu-id="fd96a-152">Si le nœud ne redevient pas actif ou s’il échoue, le problème requiert un examen plus approfondi.</span><span class="sxs-lookup"><span data-stu-id="fd96a-152">If the node doesn't come back or it fails, the problem needs more investigation.</span></span>

<span data-ttu-id="fd96a-153">L’exemple suivant représente l’événement System.FM avec un état d’intégrité OK pour le nœud actif :</span><span class="sxs-lookup"><span data-stu-id="fd96a-153">The following example shows the System.FM event with a health state of OK for node up:</span></span>

```powershell
PS C:\> Get-ServiceFabricNodeHealth  _Node_0

NodeName              : _Node_0
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 8
                        SentAt                : 7/14/2017 4:54:51 PM
                        ReceivedAt            : 7/14/2017 4:55:14 PM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```


### <a name="certificate-expiration"></a><span data-ttu-id="fd96a-154">Expiration du certificat</span><span class="sxs-lookup"><span data-stu-id="fd96a-154">Certificate expiration</span></span>
<span data-ttu-id="fd96a-155">**System.FabricNode** indique un avertissement lorsque les certificats utilisés par le nœud sont sur le point d’arriver à expiration.</span><span class="sxs-lookup"><span data-stu-id="fd96a-155">**System.FabricNode** reports a warning when certificates used by the node are near expiration.</span></span> <span data-ttu-id="fd96a-156">Chaque nœud comporte trois certificats associés : **Certificate_cluster**, **Certificate_server** et **Certificate_default_client**.</span><span class="sxs-lookup"><span data-stu-id="fd96a-156">There are three certificates per node: **Certificate_cluster**, **Certificate_server**, and **Certificate_default_client**.</span></span> <span data-ttu-id="fd96a-157">Lorsque la date d’expiration est à au moins deux semaines, l’état d’intégrité du rapport est OK.</span><span class="sxs-lookup"><span data-stu-id="fd96a-157">When the expiration is at least two weeks away, the report health state is OK.</span></span> <span data-ttu-id="fd96a-158">Si elle a lieu dans les deux semaines qui suivent, le type de rapport est un avertissement.</span><span class="sxs-lookup"><span data-stu-id="fd96a-158">When the expiration is within two weeks, the report type is a warning.</span></span> <span data-ttu-id="fd96a-159">La durée de vie de ces événements est infinie, et ils sont supprimés lorsqu’un nœud quitte un cluster.</span><span class="sxs-lookup"><span data-stu-id="fd96a-159">TTL of these events is infinite, and they are removed when a node leaves the cluster.</span></span>

* <span data-ttu-id="fd96a-160">**SourceId**: System.FabricNode</span><span class="sxs-lookup"><span data-stu-id="fd96a-160">**SourceId**: System.FabricNode</span></span>
* <span data-ttu-id="fd96a-161">**Property** : commence par **Certificate** et contient des informations supplémentaires sur le type de certificat</span><span class="sxs-lookup"><span data-stu-id="fd96a-161">**Property**: Starts with **Certificate** and contains more information about the certificate type</span></span>
* <span data-ttu-id="fd96a-162">**Étapes suivantes**: mettez à jour les certificats sur le point d’arriver à expiration.</span><span class="sxs-lookup"><span data-stu-id="fd96a-162">**Next steps**: Update the certificates if they are near expiration.</span></span>

### <a name="load-capacity-violation"></a><span data-ttu-id="fd96a-163">Violation de capacité de charge</span><span class="sxs-lookup"><span data-stu-id="fd96a-163">Load capacity violation</span></span>
<span data-ttu-id="fd96a-164">L’équilibrage de charge de Service Fabric indique un avertissement quand il détecte une violation de la capacité du nœud.</span><span class="sxs-lookup"><span data-stu-id="fd96a-164">The Service Fabric Load Balancer reports a warning when it detects a node capacity violation.</span></span>

* <span data-ttu-id="fd96a-165">**SourceId**: System.PLB</span><span class="sxs-lookup"><span data-stu-id="fd96a-165">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="fd96a-166">**Property** : commence par **Capacity**</span><span class="sxs-lookup"><span data-stu-id="fd96a-166">**Property**: Starts with **Capacity**</span></span>
* <span data-ttu-id="fd96a-167">**Étapes suivantes**: contrôlez les mesures fournies et examinez la capacité actuelle sur le nœud.</span><span class="sxs-lookup"><span data-stu-id="fd96a-167">**Next steps**: Check provided metrics and view the current capacity on the node.</span></span>

## <a name="application-system-health-reports"></a><span data-ttu-id="fd96a-168">Rapports d’intégrité du système sur les applications</span><span class="sxs-lookup"><span data-stu-id="fd96a-168">Application system health reports</span></span>
<span data-ttu-id="fd96a-169">**System.CM**, qui représente le service Cluster Manager, est l’autorité qui gère les informations sur une application.</span><span class="sxs-lookup"><span data-stu-id="fd96a-169">**System.CM**, which represents the Cluster Manager service, is the authority that manages information about an application.</span></span>

### <a name="state"></a><span data-ttu-id="fd96a-170">State</span><span class="sxs-lookup"><span data-stu-id="fd96a-170">State</span></span>
<span data-ttu-id="fd96a-171">System.CM consigne la valeur OK lorsque l’application a été créée ou mise à jour.</span><span class="sxs-lookup"><span data-stu-id="fd96a-171">System.CM reports as OK when the application has been created or updated.</span></span> <span data-ttu-id="fd96a-172">Il informe le magasin d’intégrité lorsque l’application a été supprimée afin qu’elle puisse en être retirée.</span><span class="sxs-lookup"><span data-stu-id="fd96a-172">It informs the health store when the application has been deleted, so that it can be removed from store.</span></span>

* <span data-ttu-id="fd96a-173">**SourceId**: System.CM</span><span class="sxs-lookup"><span data-stu-id="fd96a-173">**SourceId**: System.CM</span></span>
* <span data-ttu-id="fd96a-174">**Property**: State</span><span class="sxs-lookup"><span data-stu-id="fd96a-174">**Property**: State</span></span>
* <span data-ttu-id="fd96a-175">**Étapes suivantes**: si l’application a été créée ou mise à jour, elle doit inclure le rapport d’intégrité du Gestionnaire du cluster.</span><span class="sxs-lookup"><span data-stu-id="fd96a-175">**Next steps**: If the application has been created or updated, it should include the Cluster Manager health report.</span></span> <span data-ttu-id="fd96a-176">Dans le cas contraire, vérifiez l’état de l’application en émettant une requête (par exemple, l’applet de commande PowerShell **Get-ServiceFabricApplication -ApplicationName *nom_application***).</span><span class="sxs-lookup"><span data-stu-id="fd96a-176">Otherwise, check the state of the application by issuing a query (for example, the PowerShell cmdlet **Get-ServiceFabricApplication -ApplicationName *applicationName***).</span></span>

<span data-ttu-id="fd96a-177">L’exemple suivant représente l’événement d’état sur l’application **fabric:/WordCount** :</span><span class="sxs-lookup"><span data-stu-id="fd96a-177">The following example shows the state event on the **fabric:/WordCount** application:</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationHealth fabric:/WordCount -ServicesFilter None -DeployedApplicationsFilter None -ExcludeHealthStatistics

ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Ok
ServiceHealthStates             : None
DeployedApplicationHealthStates : None
HealthEvents                    : 
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 282
                                  SentAt                : 7/13/2017 5:57:05 PM
                                  ReceivedAt            : 7/14/2017 4:55:10 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 7/13/2017 5:57:05 PM, LastWarning = 1/1/0001 12:00:00 AM
```

## <a name="service-system-health-reports"></a><span data-ttu-id="fd96a-178">Rapports d’intégrité du système sur les services</span><span class="sxs-lookup"><span data-stu-id="fd96a-178">Service system health reports</span></span>
<span data-ttu-id="fd96a-179">**System.FM**, qui représente le service Failover Manager, est l’autorité qui gère les informations sur les services.</span><span class="sxs-lookup"><span data-stu-id="fd96a-179">**System.FM**, which represents the Failover Manager service, is the authority that manages information about services.</span></span>

### <a name="state"></a><span data-ttu-id="fd96a-180">State</span><span class="sxs-lookup"><span data-stu-id="fd96a-180">State</span></span>
<span data-ttu-id="fd96a-181">System.FM consigne la valeur OK lorsque le service a été créé.</span><span class="sxs-lookup"><span data-stu-id="fd96a-181">System.FM reports as OK when the service has been created.</span></span> <span data-ttu-id="fd96a-182">Il supprime l’entité du magasin d’intégrité lorsque le service a été supprimé.</span><span class="sxs-lookup"><span data-stu-id="fd96a-182">It deletes the entity from the health store when the service has been deleted.</span></span>

* <span data-ttu-id="fd96a-183">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="fd96a-183">**SourceId**: System.FM</span></span>
* <span data-ttu-id="fd96a-184">**Property**: State</span><span class="sxs-lookup"><span data-stu-id="fd96a-184">**Property**: State</span></span>

<span data-ttu-id="fd96a-185">L’exemple suivant représente l’événement d’état sur le service **fabric:/WordCount/WordCountWebService** :</span><span class="sxs-lookup"><span data-stu-id="fd96a-185">The following example shows the state event on the service **fabric:/WordCount/WordCountWebService**:</span></span>

```powershell
PS C:\> Get-ServiceFabricServiceHealth fabric:/WordCount/WordCountWebService -ExcludeHealthStatistics


ServiceName           : fabric:/WordCount/WordCountWebService
AggregatedHealthState : Ok
PartitionHealthStates : 
                        PartitionId           : 8bbcd03a-3a53-47ec-a5f1-9b77f73c53b2
                        AggregatedHealthState : Ok
                        
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 14
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/14/2017 4:55:10 PM
                        TTL                   : Infinite
                        Description           : Service has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="service-correlation-error"></a><span data-ttu-id="fd96a-186">Erreur de corrélation de services</span><span class="sxs-lookup"><span data-stu-id="fd96a-186">Service correlation error</span></span>
<span data-ttu-id="fd96a-187">**System.PLB** signale une erreur lorsqu’il détecte que la mise à jour d’un service à mettre en corrélation avec un autre service crée une chaîne d’affinités.</span><span class="sxs-lookup"><span data-stu-id="fd96a-187">**System.PLB** reports an error when it detects that updating a service to be correlated with another service creates an affinity chain.</span></span> <span data-ttu-id="fd96a-188">Le rapport est effacé lorsque la mise à jour est réussie.</span><span class="sxs-lookup"><span data-stu-id="fd96a-188">The report is cleared when successful update happens.</span></span>

* <span data-ttu-id="fd96a-189">**SourceId** : System.PLB</span><span class="sxs-lookup"><span data-stu-id="fd96a-189">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="fd96a-190">**Property** : ServiceDescription</span><span class="sxs-lookup"><span data-stu-id="fd96a-190">**Property**: ServiceDescription</span></span>
* <span data-ttu-id="fd96a-191">**Étapes suivantes** : vérifiez les descriptions de service en corrélation.</span><span class="sxs-lookup"><span data-stu-id="fd96a-191">**Next steps**: Check the correlated service descriptions.</span></span>

## <a name="partition-system-health-reports"></a><span data-ttu-id="fd96a-192">Rapports d’intégrité du système sur les partitions</span><span class="sxs-lookup"><span data-stu-id="fd96a-192">Partition system health reports</span></span>
<span data-ttu-id="fd96a-193">**System.FM**, qui représente le service Failover Manager, est l’autorité qui gère les informations sur les partitions de service.</span><span class="sxs-lookup"><span data-stu-id="fd96a-193">**System.FM**, which represents the Failover Manager service, is the authority that manages information about service partitions.</span></span>

### <a name="state"></a><span data-ttu-id="fd96a-194">State</span><span class="sxs-lookup"><span data-stu-id="fd96a-194">State</span></span>
<span data-ttu-id="fd96a-195">System.FM consigne la valeur OK lorsque la partition créée est intègre.</span><span class="sxs-lookup"><span data-stu-id="fd96a-195">System.FM reports as OK when the partition has been created and is healthy.</span></span> <span data-ttu-id="fd96a-196">Il élimine l’entité du magasin d’intégrité lorsque la partition est supprimée.</span><span class="sxs-lookup"><span data-stu-id="fd96a-196">It deletes the entity from the health store when the partition is deleted.</span></span>

<span data-ttu-id="fd96a-197">Si la partition présente une valeur inférieure au nombre minimal de réplicas, une erreur est signalée.</span><span class="sxs-lookup"><span data-stu-id="fd96a-197">If the partition is below the minimum replica count, it reports an error.</span></span> <span data-ttu-id="fd96a-198">Si la partition présente une valeur non inférieure au nombre minimal de réplicas, mais inférieure au nombre cible de réplicas, un avertissement est signalé.</span><span class="sxs-lookup"><span data-stu-id="fd96a-198">If the partition is not below the minimum replica count, but it is below the target replica count, it reports a warning.</span></span> <span data-ttu-id="fd96a-199">Si la partition subit une perte de quorum, System.FM indique une erreur.</span><span class="sxs-lookup"><span data-stu-id="fd96a-199">If the partition is in quorum loss, System.FM reports an error.</span></span>

<span data-ttu-id="fd96a-200">Les autres événements importants incluent un avertissement quand la reconfiguration et la génération prennent plus de temps que prévu.</span><span class="sxs-lookup"><span data-stu-id="fd96a-200">Other important events include a warning when the reconfiguration takes longer than expected and when the build takes longer than expected.</span></span> <span data-ttu-id="fd96a-201">Les délais impartis pour la génération et la reconfiguration sont configurables en fonction des scénarios de service.</span><span class="sxs-lookup"><span data-stu-id="fd96a-201">The expected times for the build and reconfiguration are configurable based on service scenarios.</span></span> <span data-ttu-id="fd96a-202">Par exemple, si un service présente un état défini en téraoctet, par exemple une instance SQL Database, la génération prendra davantage de temps que celle d’un service affichant un état d’un volume moindre.</span><span class="sxs-lookup"><span data-stu-id="fd96a-202">For example, if a service has a terabyte of state, such as SQL Database, the build takes longer than for a service with a small amount of state.</span></span>

* <span data-ttu-id="fd96a-203">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="fd96a-203">**SourceId**: System.FM</span></span>
* <span data-ttu-id="fd96a-204">**Property**: State</span><span class="sxs-lookup"><span data-stu-id="fd96a-204">**Property**: State</span></span>
* <span data-ttu-id="fd96a-205">**Étapes suivantes**: si l’état d’intégrité n’est pas OK, il est possible que certains réplicas n’aient pas été créés, ouverts ou promus comme réplicas principaux ou secondaires de manière correcte.</span><span class="sxs-lookup"><span data-stu-id="fd96a-205">**Next steps**: If the health state is not OK, it's possible that some replicas have not been created, opened, or promoted to primary or secondary correctly.</span></span> <span data-ttu-id="fd96a-206">Dans de nombreux cas, la cause principale est un bogue de service dans l’implémentation du rôle d’ouverture ou de modification.</span><span class="sxs-lookup"><span data-stu-id="fd96a-206">In many instances, the root cause is a service bug in the open or change-role implementation.</span></span>

<span data-ttu-id="fd96a-207">L’exemple suivant représente une partition saine :</span><span class="sxs-lookup"><span data-stu-id="fd96a-207">The following example shows a healthy partition:</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountWebService | Get-ServiceFabricPartitionHealth -ExcludeHealthStatistics -ReplicasFilter None

PartitionId           : 8bbcd03a-3a53-47ec-a5f1-9b77f73c53b2
AggregatedHealthState : Ok
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 70
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/14/2017 4:55:10 PM
                        TTL                   : Infinite
                        Description           : Partition is healthy.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

<span data-ttu-id="fd96a-208">L’exemple suivant représente l’intégrité d’une partition qui présente un nombre de réplicas inférieur à la valeur cible.</span><span class="sxs-lookup"><span data-stu-id="fd96a-208">The following example shows the health of a partition that is below target replica count.</span></span> <span data-ttu-id="fd96a-209">Ensuite, il faut récupérer la description de la partition, qui indique la façon dont elle est configurée : **MinReplicaSetSize** est défini sur trois et **TargetReplicaSetSize** sur sept.</span><span class="sxs-lookup"><span data-stu-id="fd96a-209">The next step is to get the partition description, which shows how it is configured: **MinReplicaSetSize** is three and **TargetReplicaSetSize** is seven.</span></span> <span data-ttu-id="fd96a-210">Obtenez ensuite le nombre de nœuds dans le cluster : 5.</span><span class="sxs-lookup"><span data-stu-id="fd96a-210">Then get the number of nodes in the cluster: five.</span></span> <span data-ttu-id="fd96a-211">Par conséquent, dans ce cas, il n’est pas possible de placer deux réplicas, car le nombre cible de réplicas est supérieur au nombre de nœuds disponibles.</span><span class="sxs-lookup"><span data-stu-id="fd96a-211">So in this case, two replicas can't be placed because the target number of replicas is higher than the number of nodes available.</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricPartitionHealth -ReplicasFilter None -ExcludeHealthStatistics


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Warning
                        SequenceNumber        : 123
                        SentAt                : 7/14/2017 4:55:39 PM
                        ReceivedAt            : 7/14/2017 4:55:44 PM
                        TTL                   : Infinite
                        Description           : Partition is below target replica or instance count.
                        fabric:/WordCount/WordCountService 7 2 af2e3e44-a8f8-45ac-9f31-4093eb897600
                          N/S RD _Node_2 Up 131444422260002646
                          N/S RD _Node_4 Up 131444422293113678
                          N/S RD _Node_3 Up 131444422293113679
                          N/S RD _Node_1 Up 131444422293118720
                          N/P RD _Node_0 Up 131444422293118721
                          (Showing 5 out of 5 replicas. Total available replicas: 5.)
                        
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/14/2017 4:55:44 PM, LastOk = 1/1/0001 12:00:00 AM
                        
                        SourceId              : System.PLB
                        Property              : ServiceReplicaUnplacedHealth_Secondary_af2e3e44-a8f8-45ac-9f31-4093eb897600
                        HealthState           : Warning
                        SequenceNumber        : 131445250939703027
                        SentAt                : 7/14/2017 4:58:13 PM
                        ReceivedAt            : 7/14/2017 4:58:14 PM
                        TTL                   : 00:01:05
                        Description           : The Load Balancer was unable to find a placement for one or more of the Service's Replicas:
                        Secondary replica could not be placed due to the following constraints and properties:  
                        TargetReplicaSetSize: 7
                        Placement Constraint: N/A
                        Parent Service: N/A
                        
                        Constraint Elimination Sequence:
                        Existing Secondary Replicas eliminated 4 possible node(s) for placement -- 1/5 node(s) remain.
                        Existing Primary Replica eliminated 1 possible node(s) for placement -- 0/5 node(s) remain.
                        
                        Nodes Eliminated By Constraints:
                        
                        Existing Secondary Replicas -- Nodes with Partition's Existing Secondary Replicas/Instances:
                        --
                        FaultDomain:fd:/4 NodeName:_Node_4 NodeType:NodeType4 UpgradeDomain:4 UpgradeDomain: ud:/4 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/3 NodeName:_Node_3 NodeType:NodeType3 UpgradeDomain:3 UpgradeDomain: ud:/3 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/2 NodeName:_Node_2 NodeType:NodeType2 UpgradeDomain:2 UpgradeDomain: ud:/2 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/1 NodeName:_Node_1 NodeType:NodeType1 UpgradeDomain:1 UpgradeDomain: ud:/1 Deactivation Intent/Status: None/None
                        
                        Existing Primary Replica -- Nodes with Partition's Existing Primary Replica or Secondary Replicas:
                        --
                        FaultDomain:fd:/0 NodeName:_Node_0 NodeType:NodeType0 UpgradeDomain:0 UpgradeDomain: ud:/0 Deactivation Intent/Status: None/None
                        
                        
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/14/2017 4:56:14 PM, LastOk = 1/1/0001 12:00:00 AM

PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | select MinReplicaSetSize,TargetReplicaSetSize

MinReplicaSetSize TargetReplicaSetSize
----------------- --------------------
                2                    7                        

PS C:\> @(Get-ServiceFabricNode).Count
5
```

### <a name="replica-constraint-violation"></a><span data-ttu-id="fd96a-212">Violation des contraintes de réplicas</span><span class="sxs-lookup"><span data-stu-id="fd96a-212">Replica constraint violation</span></span>
<span data-ttu-id="fd96a-213">**System.PLB** indique un avertissement s’il détecte une violation des contraintes de réplicas et qu’il ne peut pas placer tous les réplicas de la partition.</span><span class="sxs-lookup"><span data-stu-id="fd96a-213">**System.PLB** reports a warning if it detects a replica constraint violation and can't place all partition replicas.</span></span> <span data-ttu-id="fd96a-214">Les détails du rapport montrent quelles contraintes et quelles propriétés empêchent le placement des réplicas.</span><span class="sxs-lookup"><span data-stu-id="fd96a-214">The report details show which constraints and properties prevent the replica placement.</span></span>

* <span data-ttu-id="fd96a-215">**SourceId**: System.PLB</span><span class="sxs-lookup"><span data-stu-id="fd96a-215">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="fd96a-216">**Property** : commence par **ReplicaConstraintViolation**</span><span class="sxs-lookup"><span data-stu-id="fd96a-216">**Property**: Starts with **ReplicaConstraintViolation**</span></span>

## <a name="replica-system-health-reports"></a><span data-ttu-id="fd96a-217">Rapports d’intégrité du système sur les réplicas</span><span class="sxs-lookup"><span data-stu-id="fd96a-217">Replica system health reports</span></span>
<span data-ttu-id="fd96a-218">**System.RA**, qui représente le composant Reconfiguration Agent, est l’autorité de l’état des réplicas.</span><span class="sxs-lookup"><span data-stu-id="fd96a-218">**System.RA**, which represents the reconfiguration agent component, is the authority for the replica state.</span></span>

### <a name="state"></a><span data-ttu-id="fd96a-219">État</span><span class="sxs-lookup"><span data-stu-id="fd96a-219">State</span></span>
<span data-ttu-id="fd96a-220">**System.RA** consigne la valeur OK lorsque le réplica a été créé.</span><span class="sxs-lookup"><span data-stu-id="fd96a-220">**System.RA** reports OK when the replica has been created.</span></span>

* <span data-ttu-id="fd96a-221">**SourceId**: System.RA</span><span class="sxs-lookup"><span data-stu-id="fd96a-221">**SourceId**: System.RA</span></span>
* <span data-ttu-id="fd96a-222">**Property**: State</span><span class="sxs-lookup"><span data-stu-id="fd96a-222">**Property**: State</span></span>

<span data-ttu-id="fd96a-223">L’exemple suivant représente un réplica sain :</span><span class="sxs-lookup"><span data-stu-id="fd96a-223">The following example shows a healthy replica:</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricReplica | where {$_.ReplicaRole -eq "Primary"} | Get-ServiceFabricReplicaHealth

PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422293118721
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131445248920273536
                        SentAt                : 7/14/2017 4:54:52 PM
                        ReceivedAt            : 7/14/2017 4:55:13 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_0
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/14/2017 4:55:13 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="replica-open-status"></a><span data-ttu-id="fd96a-224">État d’ouverture du réplica</span><span class="sxs-lookup"><span data-stu-id="fd96a-224">Replica open status</span></span>
<span data-ttu-id="fd96a-225">La description de ce rapport d’intégrité contient l’heure de début (temps universel coordonné) de l’appel d’API.</span><span class="sxs-lookup"><span data-stu-id="fd96a-225">The description of this health report contains the start time (Coordinated Universal Time) when the API call was invoked.</span></span>

<span data-ttu-id="fd96a-226">**System.RA** indique un avertissement si l’ouverture du réplica dure plus longtemps que la période configurée (valeur par défaut : 30 minutes).</span><span class="sxs-lookup"><span data-stu-id="fd96a-226">**System.RA** reports a warning if the replica open takes longer than the configured period (default: 30 minutes).</span></span> <span data-ttu-id="fd96a-227">Si l’API a une incidence sur la disponibilité du service, le rapport est émis plus rapidement (intervalle configurable avec une valeur de 30 secondes par défaut).</span><span class="sxs-lookup"><span data-stu-id="fd96a-227">If the API impacts service availability, the report is issued much faster (a configurable interval, with a default of 30 seconds).</span></span> <span data-ttu-id="fd96a-228">La durée inclut le temps nécessaire à l’ouverture du duplicateur et du service.</span><span class="sxs-lookup"><span data-stu-id="fd96a-228">The time measured includes the time taken for the replicator open and the service open.</span></span> <span data-ttu-id="fd96a-229">Lorsque l’ouverture se termine, la propriété affiche la valeur OK.</span><span class="sxs-lookup"><span data-stu-id="fd96a-229">The property changes to OK if the open completes.</span></span>

* <span data-ttu-id="fd96a-230">**SourceId**: System.RA</span><span class="sxs-lookup"><span data-stu-id="fd96a-230">**SourceId**: System.RA</span></span>
* <span data-ttu-id="fd96a-231">**Property**: **ReplicaOpenStatus**</span><span class="sxs-lookup"><span data-stu-id="fd96a-231">**Property**: **ReplicaOpenStatus**</span></span>
* <span data-ttu-id="fd96a-232">**Étapes suivantes**: si l’état d’intégrité ne présente pas la valeur OK, recherchez pourquoi l’ouverture du réplica prend plus de temps que prévu.</span><span class="sxs-lookup"><span data-stu-id="fd96a-232">**Next steps**: If the health state is not OK, investigate why the replica open takes longer than expected.</span></span>

### <a name="slow-service-api-call"></a><span data-ttu-id="fd96a-233">Appel lent d’API de service</span><span class="sxs-lookup"><span data-stu-id="fd96a-233">Slow service API call</span></span>
<span data-ttu-id="fd96a-234">**System.RAP** et **System.Replicator** indiquent un avertissement si un appel de code de service utilisateur prend plus de temps que la durée configurée.</span><span class="sxs-lookup"><span data-stu-id="fd96a-234">**System.RAP** and **System.Replicator** report a warning if a call to the user service code takes longer than the configured time.</span></span> <span data-ttu-id="fd96a-235">L’avertissement est effacé à l’exécution de l’appel.</span><span class="sxs-lookup"><span data-stu-id="fd96a-235">The warning is cleared when the call completes.</span></span>

* <span data-ttu-id="fd96a-236">**SourceId**: System.RAP ou System.Replicator</span><span class="sxs-lookup"><span data-stu-id="fd96a-236">**SourceId**: System.RAP or System.Replicator</span></span>
* <span data-ttu-id="fd96a-237">**Property**: nom de l’API lente.</span><span class="sxs-lookup"><span data-stu-id="fd96a-237">**Property**: The name of the slow API.</span></span> <span data-ttu-id="fd96a-238">La description fournit plus de détails sur le délai de mise en attente de l’API.</span><span class="sxs-lookup"><span data-stu-id="fd96a-238">The description provides more details about the time the API has been pending.</span></span>
* <span data-ttu-id="fd96a-239">**Étapes suivantes**: recherchez pourquoi l’appel prend plus de temps que prévu.</span><span class="sxs-lookup"><span data-stu-id="fd96a-239">**Next steps**: Investigate why the call takes longer than expected.</span></span>

<span data-ttu-id="fd96a-240">L’exemple suivant représente une partition affichant une perte de quorum et la procédure d’investigation exécutée pour identifier la raison.</span><span class="sxs-lookup"><span data-stu-id="fd96a-240">The following example shows a partition in quorum loss, and the investigation steps done to figure out why.</span></span> <span data-ttu-id="fd96a-241">L’un des réplicas présente un état d’intégrité d’avertissement ; vous êtes ainsi renseigné sur sa condition.</span><span class="sxs-lookup"><span data-stu-id="fd96a-241">One of the replicas has a warning health state, so you get its health.</span></span> <span data-ttu-id="fd96a-242">Le code montre que le service prend plus de temps que prévu ; il s’agit d’un événement signalé par System.RAP.</span><span class="sxs-lookup"><span data-stu-id="fd96a-242">It shows that the service operation takes longer than expected, an event reported by System.RAP.</span></span> <span data-ttu-id="fd96a-243">Une fois cette information reçue, il convient maintenant d’examiner le code de service et d’effectuer les recherches qui s’imposent.</span><span class="sxs-lookup"><span data-stu-id="fd96a-243">After this information is received, the next step is to look at the service code and investigate there.</span></span> <span data-ttu-id="fd96a-244">Dans ce cas, l’implémentation **RunAsync** du service avec état génère une exception non prise en charge.</span><span class="sxs-lookup"><span data-stu-id="fd96a-244">For this case, the **RunAsync** implementation of the stateful service throws an unhandled exception.</span></span> <span data-ttu-id="fd96a-245">Notez que les réplicas sont en cours de recyclage. Il est donc possible qu’aucun d’entre eux n’affiche l’état d’avertissement.</span><span class="sxs-lookup"><span data-stu-id="fd96a-245">The replicas are recycling, so you may not see any replicas in the warning state.</span></span> <span data-ttu-id="fd96a-246">Vous pouvez réessayer d’obtenir l’état d’intégrité et rechercher les éventuelles différences d’ID de réplica.</span><span class="sxs-lookup"><span data-stu-id="fd96a-246">You can retry getting the health state and look for any differences in the replica ID.</span></span> <span data-ttu-id="fd96a-247">Dans certains cas, les nouvelles tentatives peuvent vous donner des indices.</span><span class="sxs-lookup"><span data-stu-id="fd96a-247">In certain cases, the retries can give you clues.</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/HelloWorldStatefulApplication/HelloWorldStateful | Get-ServiceFabricPartitionHealth -ExcludeHealthStatistics

PartitionId           : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
AggregatedHealthState : Error
UnhealthyEvaluations  :
                        Error event: SourceId='System.FM', Property='State'.

ReplicaHealthStates   :
                        ReplicaId             : 130743748372546446
                        AggregatedHealthState : Ok

                        ReplicaId             : 130743746168084332
                        AggregatedHealthState : Ok

                        ReplicaId             : 130743746195428808
                        AggregatedHealthState : Warning

                        ReplicaId             : 130743746195428807
                        AggregatedHealthState : Ok

HealthEvents          :
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Error
                        SequenceNumber        : 182
                        SentAt                : 4/24/2015 7:00:17 PM
                        ReceivedAt            : 4/24/2015 7:00:31 PM
                        TTL                   : Infinite
                        Description           : Partition is in quorum loss.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Warning->Error = 4/24/2015 6:51:31 PM

PS C:\> Get-ServiceFabricPartition fabric:/HelloWorldStatefulApplication/HelloWorldStateful

PartitionId            : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
PartitionKind          : Int64Range
PartitionLowKey        : -9223372036854775808
PartitionHighKey       : 9223372036854775807
PartitionStatus        : InQuorumLoss
LastQuorumLossDuration : 00:00:13
MinReplicaSetSize      : 3
TargetReplicaSetSize   : 3
HealthState            : Error
DataLossNumber         : 130743746152927699
ConfigurationNumber    : 227633266688

PS C:\> Get-ServiceFabricReplica 72a0fb3e-53ec-44f2-9983-2f272aca3e38 130743746195428808

ReplicaId           : 130743746195428808
ReplicaAddress      : PartitionId: 72a0fb3e-53ec-44f2-9983-2f272aca3e38, ReplicaId: 130743746195428808
ReplicaRole         : Primary
NodeName            : Node.3
ReplicaStatus       : Ready
LastInBuildDuration : 00:00:01
HealthState         : Warning

PS C:\> Get-ServiceFabricReplicaHealth 72a0fb3e-53ec-44f2-9983-2f272aca3e38 130743746195428808

PartitionId           : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
ReplicaId             : 130743746195428808
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.RAP', Property='ServiceOpenOperationDuration', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 130743756170185892
                        SentAt                : 4/24/2015 7:00:17 PM
                        ReceivedAt            : 4/24/2015 7:00:33 PM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/24/2015 7:00:33 PM

                        SourceId              : System.RAP
                        Property              : ServiceOpenOperationDuration
                        HealthState           : Warning
                        SequenceNumber        : 130743756399407044
                        SentAt                : 4/24/2015 7:00:39 PM
                        ReceivedAt            : 4/24/2015 7:00:59 PM
                        TTL                   : Infinite
                        Description           : Start Time (UTC): 2015-04-24 19:00:17.019
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Warning = 4/24/2015 7:00:59 PM
```

<span data-ttu-id="fd96a-248">Lors du démarrage de l’application défaillante sous le débogueur, les fenêtres des événements de diagnostic affichent l’exception levée par RunAsync :</span><span class="sxs-lookup"><span data-stu-id="fd96a-248">When you start the faulty application under the debugger, the diagnostic events windows show the exception thrown from RunAsync:</span></span>

![Événements de diagnostic Visual Studio 2015 : Échec de RunAsync dans la structure : /HelloWorldStatefulApplication.][1]

<span data-ttu-id="fd96a-250">Événements de diagnostic Visual Studio 2015 : Échec de RunAsync dans la **structure : /HelloWorldStatefulApplication**.</span><span class="sxs-lookup"><span data-stu-id="fd96a-250">Visual Studio 2015 diagnostic events: RunAsync failure in **fabric:/HelloWorldStatefulApplication**.</span></span>

[1]: ./media/service-fabric-understand-and-troubleshoot-with-system-health-reports/servicefabric-health-vs-runasync-exception.png


### <a name="replication-queue-full"></a><span data-ttu-id="fd96a-251">File d’attente de réplication complète</span><span class="sxs-lookup"><span data-stu-id="fd96a-251">Replication queue full</span></span>
<span data-ttu-id="fd96a-252">**System.Replicator** indique un avertissement lorsque la file d’attente de réplication est pleine.</span><span class="sxs-lookup"><span data-stu-id="fd96a-252">**System.Replicator** reports a warning when the replication queue is full.</span></span> <span data-ttu-id="fd96a-253">Sur le rôle principal, la file d’attente de réplication se remplit généralement en raison de la lenteur d’un ou de plusieurs réplicas secondaires à accuser réception des opérations.</span><span class="sxs-lookup"><span data-stu-id="fd96a-253">On the primary, replication queue usually becomes full because one or more secondary replicas are slow to acknowledge operations.</span></span> <span data-ttu-id="fd96a-254">Sur le rôle secondaire, cela se produit habituellement lorsque le service prend trop de temps pour appliquer les opérations.</span><span class="sxs-lookup"><span data-stu-id="fd96a-254">On the secondary, this usually happens when the service is slow to apply the operations.</span></span> <span data-ttu-id="fd96a-255">L’avertissement est effacé une fois que la file d’attente n’est plus pleine.</span><span class="sxs-lookup"><span data-stu-id="fd96a-255">The warning is cleared when the queue is no longer full.</span></span>

* <span data-ttu-id="fd96a-256">**SourceId**: System.Replicator</span><span class="sxs-lookup"><span data-stu-id="fd96a-256">**SourceId**: System.Replicator</span></span>
* <span data-ttu-id="fd96a-257">**Property** : **PrimaryReplicationQueueStatus** ou **SecondaryReplicationQueueStatus**, en fonction du rôle de réplica</span><span class="sxs-lookup"><span data-stu-id="fd96a-257">**Property**: **PrimaryReplicationQueueStatus** or **SecondaryReplicationQueueStatus**, depending on the replica role</span></span>

### <a name="slow-naming-operations"></a><span data-ttu-id="fd96a-258">Opérations de nommage lentes</span><span class="sxs-lookup"><span data-stu-id="fd96a-258">Slow Naming operations</span></span>
<span data-ttu-id="fd96a-259">**System.NamingService** signale l’intégrité sur son réplica principal quand une opération de nommage prend trop de temps.</span><span class="sxs-lookup"><span data-stu-id="fd96a-259">**System.NamingService** reports health on its primary replica when a Naming operation takes longer than acceptable.</span></span> <span data-ttu-id="fd96a-260">[CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) et [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) sont des exemples d’opérations de nommage.</span><span class="sxs-lookup"><span data-stu-id="fd96a-260">Examples of Naming operations are [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) or [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync).</span></span> <span data-ttu-id="fd96a-261">D’autres méthodes se trouvent sous FabricClient, par exemple dans les [méthodes de gestion de service](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) ou les [méthodes de gestion de propriété](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).</span><span class="sxs-lookup"><span data-stu-id="fd96a-261">More methods can be found under FabricClient, for example under [service management methods](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) or [property management methods](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).</span></span>

> [!NOTE]
> <span data-ttu-id="fd96a-262">Le service d’affectation de noms résout les noms des services dans un emplacement du cluster et permet aux utilisateurs de gérer les propriétés et les noms des services.</span><span class="sxs-lookup"><span data-stu-id="fd96a-262">The Naming service resolves service names to a location in the cluster and enables users to manage service names and properties.</span></span> <span data-ttu-id="fd96a-263">Il s’agit d’un service persistant partitionné Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="fd96a-263">It is a Service Fabric partitioned persisted service.</span></span> <span data-ttu-id="fd96a-264">L’une des partitions représente le propriétaire de l’autorité, qui contient des métadonnées sur tous les noms et les services Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="fd96a-264">One of the partitions represents the Authority Owner, which contains metadata about all Service Fabric names and services.</span></span> <span data-ttu-id="fd96a-265">Les noms Service Fabric sont mappés à des partitions différentes, appelées partitions Propriétaire du nom. Ainsi, le service est extensible.</span><span class="sxs-lookup"><span data-stu-id="fd96a-265">The Service Fabric names are mapped to different partitions, called Name Owner partitions, so the service is extensible.</span></span> <span data-ttu-id="fd96a-266">En savoir plus sur le [service de nommage](service-fabric-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="fd96a-266">Read more about [Naming service](service-fabric-architecture.md).</span></span>
> 
> 

<span data-ttu-id="fd96a-267">Quand une opération de nommage prend plus longtemps que prévu, elle est marquée avec un Avertissement sur le *réplica principal de la partition de service d’affectation de noms qui effectue l’opération*.</span><span class="sxs-lookup"><span data-stu-id="fd96a-267">When a Naming operation takes longer than expected, the operation is flagged with a Warning report on the *primary replica of the Naming service partition that serves the operation*.</span></span> <span data-ttu-id="fd96a-268">Si l’opération se termine avec succès, l’avertissement est effacé.</span><span class="sxs-lookup"><span data-stu-id="fd96a-268">If the operation completes successfully, the Warning is cleared.</span></span> <span data-ttu-id="fd96a-269">Si l’opération se termine avec une erreur, le rapport d’intégrité inclut des détails sur l’erreur.</span><span class="sxs-lookup"><span data-stu-id="fd96a-269">If the operation completes with an error, the health report includes details about the error.</span></span>

* <span data-ttu-id="fd96a-270">**SourceId**: System.NamingService</span><span class="sxs-lookup"><span data-stu-id="fd96a-270">**SourceId**: System.NamingService</span></span>
* <span data-ttu-id="fd96a-271">**Property** : commence par le préfixe **Duration_** et identifie l’opération lente et le nom Service Fabric sur lequel l’opération est appliquée.</span><span class="sxs-lookup"><span data-stu-id="fd96a-271">**Property**: Starts with prefix **Duration_** and identifies the slow operation and the Service Fabric name on which the operation is applied.</span></span> <span data-ttu-id="fd96a-272">Par exemple, si la création de service au nom fabric:/MyApp/MyService prend trop de temps, la propriété est Duration_AOCreateService.fabric:/MyApp/MyService.</span><span class="sxs-lookup"><span data-stu-id="fd96a-272">For example, if create service at name fabric:/MyApp/MyService takes too long, the property is Duration_AOCreateService.fabric:/MyApp/MyService.</span></span> <span data-ttu-id="fd96a-273">AO pointe vers le rôle de la partition de nommage pour ce nom et cette opération.</span><span class="sxs-lookup"><span data-stu-id="fd96a-273">AO points to the role of the Naming partition for this name and operation.</span></span>
* <span data-ttu-id="fd96a-274">**Étapes suivantes**: vérifier pourquoi l’opération de nommage échoue.</span><span class="sxs-lookup"><span data-stu-id="fd96a-274">**Next steps**: Check why the Naming operation fails.</span></span> <span data-ttu-id="fd96a-275">Chaque opération peut avoir différentes causes principales.</span><span class="sxs-lookup"><span data-stu-id="fd96a-275">Each operation can have different root causes.</span></span> <span data-ttu-id="fd96a-276">Par exemple, une opération de suppression de service peut se bloquer sur un nœud car l’hôte d’application se bloque constamment sur un nœud à cause d’un bogue utilisateur dans le code de service.</span><span class="sxs-lookup"><span data-stu-id="fd96a-276">For example, delete service may be stuck on a node because the application host keeps crashing on a node due to a user bug in the service code.</span></span>

<span data-ttu-id="fd96a-277">L’exemple suivant illustre une opération de création de service.</span><span class="sxs-lookup"><span data-stu-id="fd96a-277">The following example shows a create service operation.</span></span> <span data-ttu-id="fd96a-278">L’opération a duré plus longtemps que la durée configurée.</span><span class="sxs-lookup"><span data-stu-id="fd96a-278">The operation took longer than the configured duration.</span></span> <span data-ttu-id="fd96a-279">AO réessaie et envoie le travail à NO.</span><span class="sxs-lookup"><span data-stu-id="fd96a-279">AO retries and sends work to NO.</span></span> <span data-ttu-id="fd96a-280">NO a terminé la dernière opération avec Timeout.</span><span class="sxs-lookup"><span data-stu-id="fd96a-280">NO completed the last operation with Timeout.</span></span> <span data-ttu-id="fd96a-281">Dans ce cas, le même réplica est principal pour les rôles AO et NO.</span><span class="sxs-lookup"><span data-stu-id="fd96a-281">In this case, the same replica is primary for both the AO and NO roles.</span></span>

```powershell
PartitionId           : 00000000-0000-0000-0000-000000001000
ReplicaId             : 131064359253133577
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.NamingService', Property='Duration_AOCreateService.fabric:/MyApp/MyService', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131064359308715535
                        SentAt                : 4/29/2016 8:38:50 PM
                        ReceivedAt            : 4/29/2016 8:39:08 PM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 4/29/2016 8:39:08 PM, LastWarning = 1/1/0001 12:00:00 AM

                        SourceId              : System.NamingService
                        Property              : Duration_AOCreateService.fabric:/MyApp/MyService
                        HealthState           : Warning
                        SequenceNumber        : 131064359526778775
                        SentAt                : 4/29/2016 8:39:12 PM
                        ReceivedAt            : 4/29/2016 8:39:38 PM
                        TTL                   : 00:05:00
                        Description           : The AOCreateService started at 2016-04-29 20:39:08.677 is taking longer than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM

                        SourceId              : System.NamingService
                        Property              : Duration_NOCreateService.fabric:/MyApp/MyService
                        HealthState           : Warning
                        SequenceNumber        : 131064360657607311
                        SentAt                : 4/29/2016 8:41:05 PM
                        ReceivedAt            : 4/29/2016 8:41:08 PM
                        TTL                   : 00:00:15
                        Description           : The NOCreateService started at 2016-04-29 20:39:08.689 completed with FABRIC_E_TIMEOUT in more than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM
```

## <a name="deployedapplication-system-health-reports"></a><span data-ttu-id="fd96a-282">Rapports d’intégrité du système sur les applications déployées</span><span class="sxs-lookup"><span data-stu-id="fd96a-282">DeployedApplication system health reports</span></span>
<span data-ttu-id="fd96a-283">**System.Hosting** est l’autorité régnant sur les entités déployées.</span><span class="sxs-lookup"><span data-stu-id="fd96a-283">**System.Hosting** is the authority on deployed entities.</span></span>

### <a name="activation"></a><span data-ttu-id="fd96a-284">Activation</span><span class="sxs-lookup"><span data-stu-id="fd96a-284">Activation</span></span>
<span data-ttu-id="fd96a-285">System.Hosting consigne la valeur OK lorsqu’une application a été activée sur le nœud.</span><span class="sxs-lookup"><span data-stu-id="fd96a-285">System.Hosting reports as OK when an application has been successfully activated on the node.</span></span> <span data-ttu-id="fd96a-286">Dans le cas contraire, il indique une erreur.</span><span class="sxs-lookup"><span data-stu-id="fd96a-286">Otherwise, it reports an error.</span></span>

* <span data-ttu-id="fd96a-287">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="fd96a-287">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="fd96a-288">**Property**: Activation, inclut la version de déploiement</span><span class="sxs-lookup"><span data-stu-id="fd96a-288">**Property**: Activation, including the rollout version</span></span>
* <span data-ttu-id="fd96a-289">**Étapes suivantes**: si l’application est défectueuse, rechercher la raison de l’échec de l’activation.</span><span class="sxs-lookup"><span data-stu-id="fd96a-289">**Next steps**: If the application is unhealthy, investigate why the activation failed.</span></span>

<span data-ttu-id="fd96a-290">L’exemple suivant représente une activation réussie :</span><span class="sxs-lookup"><span data-stu-id="fd96a-290">The following example shows successful activation:</span></span>

```powershell
PS C:\> Get-ServiceFabricDeployedApplicationHealth -NodeName _Node_1 -ApplicationName fabric:/WordCount -ExcludeHealthStatistics

ApplicationName                    : fabric:/WordCount
NodeName                           : _Node_1
AggregatedHealthState              : Ok
DeployedServicePackageHealthStates : 
                                     ServiceManifestName   : WordCountServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_1
                                     AggregatedHealthState : Ok
                                     
HealthEvents                       : 
                                     SourceId              : System.Hosting
                                     Property              : Activation
                                     HealthState           : Ok
                                     SequenceNumber        : 131445249083836329
                                     SentAt                : 7/14/2017 4:55:08 PM
                                     ReceivedAt            : 7/14/2017 4:55:14 PM
                                     TTL                   : Infinite
                                     Description           : The application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a><span data-ttu-id="fd96a-291">Télécharger</span><span class="sxs-lookup"><span data-stu-id="fd96a-291">Download</span></span>
<span data-ttu-id="fd96a-292">**System.Hosting** indique une erreur en cas d’échec du téléchargement du package d’application.</span><span class="sxs-lookup"><span data-stu-id="fd96a-292">**System.Hosting** reports an error if the application package download fails.</span></span>

* <span data-ttu-id="fd96a-293">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="fd96a-293">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="fd96a-294">**Property** : **Download:*RolloutVersion***</span><span class="sxs-lookup"><span data-stu-id="fd96a-294">**Property**: **Download:*RolloutVersion***</span></span>
* <span data-ttu-id="fd96a-295">**Étapes suivantes**: rechercher la raison de l’échec du téléchargement sur le nœud.</span><span class="sxs-lookup"><span data-stu-id="fd96a-295">**Next steps**: Investigate why the download failed on the node.</span></span>

## <a name="deployedservicepackage-system-health-reports"></a><span data-ttu-id="fd96a-296">Rapports d’intégrité du système sur le package de service déployé</span><span class="sxs-lookup"><span data-stu-id="fd96a-296">DeployedServicePackage system health reports</span></span>
<span data-ttu-id="fd96a-297">**System.Hosting** est l’autorité régnant sur les entités déployées.</span><span class="sxs-lookup"><span data-stu-id="fd96a-297">**System.Hosting** is the authority on deployed entities.</span></span>

### <a name="service-package-activation"></a><span data-ttu-id="fd96a-298">Activation du package de service</span><span class="sxs-lookup"><span data-stu-id="fd96a-298">Service package activation</span></span>
<span data-ttu-id="fd96a-299">System.Hosting consigne la valeur OK si l’activation du package de service sur le nœud est réussie.</span><span class="sxs-lookup"><span data-stu-id="fd96a-299">System.Hosting reports as OK if the service package activation on the node is successful.</span></span> <span data-ttu-id="fd96a-300">Dans le cas contraire, il indique une erreur.</span><span class="sxs-lookup"><span data-stu-id="fd96a-300">Otherwise, it reports an error.</span></span>

* <span data-ttu-id="fd96a-301">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="fd96a-301">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="fd96a-302">**Property**: Activation</span><span class="sxs-lookup"><span data-stu-id="fd96a-302">**Property**: Activation</span></span>
* <span data-ttu-id="fd96a-303">**Étapes suivantes**: examiner la raison de l’échec de l’activation.</span><span class="sxs-lookup"><span data-stu-id="fd96a-303">**Next steps**: Investigate why the activation failed.</span></span>

### <a name="code-package-activation"></a><span data-ttu-id="fd96a-304">Activation du package de code</span><span class="sxs-lookup"><span data-stu-id="fd96a-304">Code package activation</span></span>
<span data-ttu-id="fd96a-305">**System.Hosting** consigne la valeur OK pour chaque package de code en cas de réussite de l’activation.</span><span class="sxs-lookup"><span data-stu-id="fd96a-305">**System.Hosting** reports as OK for each code package if the activation is successful.</span></span> <span data-ttu-id="fd96a-306">En cas d’échec de l’activation, il indique un avertissement conformément à la configuration.</span><span class="sxs-lookup"><span data-stu-id="fd96a-306">If the activation fails, it reports a warning as configured.</span></span> <span data-ttu-id="fd96a-307">Si l’activation de **CodePackage** échoue, ou s’il se termine avec une erreur supérieure à la valeur **CodePackageHealthErrorThreshold** configurée, System.Hosting indique une erreur.</span><span class="sxs-lookup"><span data-stu-id="fd96a-307">If **CodePackage** fails to activate or terminates with an error greater than the configured **CodePackageHealthErrorThreshold**, hosting reports an error.</span></span> <span data-ttu-id="fd96a-308">Si un package de service contient plusieurs packages de code, un rapport d’activation est généré pour chacun d’entre eux.</span><span class="sxs-lookup"><span data-stu-id="fd96a-308">If a service package contains multiple code packages, an activation report is generated for each one.</span></span>

* <span data-ttu-id="fd96a-309">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="fd96a-309">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="fd96a-310">**Property** : utilise le préfixe **CodePackageActivation** et contient le nom du package de code et le point d’entrée **CodePackageActivation:*CodePackageName*:*SetupEntryPoint/EntryPoint*** (par exemple, **CodePackageActivation:Code:SetupEntryPoint**)</span><span class="sxs-lookup"><span data-stu-id="fd96a-310">**Property**: Uses the prefix **CodePackageActivation** and contains the name of the code package and the entry point as **CodePackageActivation:*CodePackageName*:*SetupEntryPoint/EntryPoint*** (for example, **CodePackageActivation:Code:SetupEntryPoint**)</span></span>

### <a name="service-type-registration"></a><span data-ttu-id="fd96a-311">Inscription du type de service</span><span class="sxs-lookup"><span data-stu-id="fd96a-311">Service type registration</span></span>
<span data-ttu-id="fd96a-312">**System.Hosting** consigne la valeur OK si le type de service a été inscrit correctement.</span><span class="sxs-lookup"><span data-stu-id="fd96a-312">**System.Hosting** reports as OK if the service type has been registered successfully.</span></span> <span data-ttu-id="fd96a-313">Il indique une erreur si l’inscription n’a pas été effectuée à temps (conformément à la configuration de **ServiceTypeRegistrationTimeout**).</span><span class="sxs-lookup"><span data-stu-id="fd96a-313">It reports an error if the registration wasn't done in time (as configured by using **ServiceTypeRegistrationTimeout**).</span></span> <span data-ttu-id="fd96a-314">Si le runtime est fermé, le type de service n’est pas inscrit à partir du nœud et Hosting signale un avertissement.</span><span class="sxs-lookup"><span data-stu-id="fd96a-314">If the runtime is closed, the service type is unregistered from the node and Hosting reports a warning.</span></span>

* <span data-ttu-id="fd96a-315">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="fd96a-315">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="fd96a-316">**Property** : utilise le préfixe **ServiceTypeRegistration** et contient le nom du type de service (par exemple, **ServiceTypeRegistration:FileStoreServiceType**)</span><span class="sxs-lookup"><span data-stu-id="fd96a-316">**Property**: Uses the prefix **ServiceTypeRegistration** and contains the service type name (for example, **ServiceTypeRegistration:FileStoreServiceType**)</span></span>

<span data-ttu-id="fd96a-317">L’exemple suivant représente un package de service déployé sain :</span><span class="sxs-lookup"><span data-stu-id="fd96a-317">The following example shows a healthy deployed service package:</span></span>

```powershell
PS C:\> Get-ServiceFabricDeployedServicePackageHealth -NodeName _Node_1 -ApplicationName fabric:/WordCount -ServiceManifestName WordCountServicePkg


ApplicationName            : fabric:/WordCount
ServiceManifestName        : WordCountServicePkg
ServicePackageActivationId : 
NodeName                   : _Node_1
AggregatedHealthState      : Ok
HealthEvents               : 
                             SourceId              : System.Hosting
                             Property              : Activation
                             HealthState           : Ok
                             SequenceNumber        : 131445249084026346
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : The ServicePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : CodePackageActivation:Code:EntryPoint
                             HealthState           : Ok
                             SequenceNumber        : 131445249084306362
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : The CodePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : ServiceTypeRegistration:WordCountServiceType
                             HealthState           : Ok
                             SequenceNumber        : 131445249088096842
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : The ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a><span data-ttu-id="fd96a-318">Télécharger</span><span class="sxs-lookup"><span data-stu-id="fd96a-318">Download</span></span>
<span data-ttu-id="fd96a-319">**System.Hosting** indique une erreur en cas d’échec du téléchargement du package de service.</span><span class="sxs-lookup"><span data-stu-id="fd96a-319">**System.Hosting** reports an error if the service package download fails.</span></span>

* <span data-ttu-id="fd96a-320">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="fd96a-320">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="fd96a-321">**Property** : **Download:*RolloutVersion***</span><span class="sxs-lookup"><span data-stu-id="fd96a-321">**Property**: **Download:*RolloutVersion***</span></span>
* <span data-ttu-id="fd96a-322">**Étapes suivantes**: rechercher la raison de l’échec du téléchargement sur le nœud.</span><span class="sxs-lookup"><span data-stu-id="fd96a-322">**Next steps**: Investigate why the download failed on the node.</span></span>

### <a name="upgrade-validation"></a><span data-ttu-id="fd96a-323">Validation de mise à niveau</span><span class="sxs-lookup"><span data-stu-id="fd96a-323">Upgrade validation</span></span>
<span data-ttu-id="fd96a-324">**System.Hosting** indique une erreur en cas d’échec de la validation lors la mise à niveau ou en cas d’échec de la mise à niveau sur le nœud.</span><span class="sxs-lookup"><span data-stu-id="fd96a-324">**System.Hosting** reports an error if validation during the upgrade fails or if the upgrade fails on the node.</span></span>

* <span data-ttu-id="fd96a-325">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="fd96a-325">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="fd96a-326">**Property** : utilise le préfixe **FabricUpgradeValidation** et contient la version de mise à niveau</span><span class="sxs-lookup"><span data-stu-id="fd96a-326">**Property**: Uses the prefix **FabricUpgradeValidation** and contains the upgrade version</span></span>
* <span data-ttu-id="fd96a-327">**Description**: désigne l’erreur rencontrée</span><span class="sxs-lookup"><span data-stu-id="fd96a-327">**Description**: Points to the error encountered</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd96a-328">Étapes suivantes </span><span class="sxs-lookup"><span data-stu-id="fd96a-328">Next steps</span></span>
[<span data-ttu-id="fd96a-329">Affichage rapports d’intégrité de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="fd96a-329">View Service Fabric health reports</span></span>](service-fabric-view-entities-aggregated-health.md)

[<span data-ttu-id="fd96a-330">Comment signaler et contrôler l’intégrité du service</span><span class="sxs-lookup"><span data-stu-id="fd96a-330">How to report and check service health</span></span>](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[<span data-ttu-id="fd96a-331">Surveiller et diagnostiquer les services localement</span><span class="sxs-lookup"><span data-stu-id="fd96a-331">Monitor and diagnose services locally</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="fd96a-332">Mise à niveau des applications Service Fabric</span><span class="sxs-lookup"><span data-stu-id="fd96a-332">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

