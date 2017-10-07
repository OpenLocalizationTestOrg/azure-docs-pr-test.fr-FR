---
title: "aaaTroubleshoot avec les rapports d’intégrité système | Documents Microsoft"
description: "Décrit les rapports de contrôle d’intégrité hello envoyés par les composants d’infrastructure de Service Azure et leur utilisation pour la résolution des problèmes de cluster ou de problèmes liés aux applications."
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
ms.openlocfilehash: c77a6cdd0440ce5d354cd8760f40151f674a3529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-system-health-reports-tootroubleshoot"></a><span data-ttu-id="672fd-103">Utilisez tootroubleshoot de rapports d’intégrité système</span><span class="sxs-lookup"><span data-stu-id="672fd-103">Use system health reports tootroubleshoot</span></span>
<span data-ttu-id="672fd-104">Azure Service Fabric composants rapport prédéfinies hello sur toutes les entités dans un cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="672fd-104">Azure Service Fabric components report out of hello box on all entities in hello cluster.</span></span> <span data-ttu-id="672fd-105">Hello [magasin de contrôle d’intégrité](service-fabric-health-introduction.md#health-store) crée et supprime les entités en fonction des rapports sur le système hello.</span><span class="sxs-lookup"><span data-stu-id="672fd-105">hello [health store](service-fabric-health-introduction.md#health-store) creates and deletes entities based on hello system reports.</span></span> <span data-ttu-id="672fd-106">Il les organise au sein d’une hiérarchie qui tient compte des interactions entre les entités.</span><span class="sxs-lookup"><span data-stu-id="672fd-106">It also organizes them in a hierarchy that captures entity interactions.</span></span>

> [!NOTE]
> <span data-ttu-id="672fd-107">concepts relatifs à l’état de toounderstand, en savoir plus sur [modèle de contrôle d’intégrité de l’infrastructure de Service](service-fabric-health-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="672fd-107">toounderstand health-related concepts, read more at [Service Fabric health model](service-fabric-health-introduction.md).</span></span>
> 
> 

<span data-ttu-id="672fd-108">Les rapports d’intégrité du système procurent une visibilité sur les fonctionnalités du cluster et des applications, et signalent les problèmes d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="672fd-108">System health reports provide visibility into cluster and application functionality and flag issues through health.</span></span> <span data-ttu-id="672fd-109">Pour les applications et services, rapports d’intégrité système Vérifiez que les entités sont implémentées et sont comportent correctement à partir de hello perspective de l’infrastructure de Service.</span><span class="sxs-lookup"><span data-stu-id="672fd-109">For applications and services, system health reports verify that entities are implemented and are behaving correctly from hello Service Fabric perspective.</span></span> <span data-ttu-id="672fd-110">rapports de Hello ne fournissent pas de n’importe quel contrôle d’intégrité de la logique métier de hello du service de hello ou détection de processus bloqués.</span><span class="sxs-lookup"><span data-stu-id="672fd-110">hello reports do not provide any health monitoring of hello business logic of hello service or detection of hung processes.</span></span> <span data-ttu-id="672fd-111">Services de l’utilisateur peuvent enrichir les données de contrôle d’intégrité de hello avec une logique spécifique tootheir plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="672fd-111">User services can enrich hello health data with information specific tootheir logic.</span></span>

> [!NOTE]
> <span data-ttu-id="672fd-112">Agents de surveillance des rapports d’intégrité sont visibles uniquement *après* composants du système hello créent une entité.</span><span class="sxs-lookup"><span data-stu-id="672fd-112">Watchdogs health reports are visible only *after* hello system components create an entity.</span></span> <span data-ttu-id="672fd-113">Lorsqu’une entité est supprimée, magasin de contrôle d’intégrité hello supprime automatiquement tous les rapports d’intégrité associées.</span><span class="sxs-lookup"><span data-stu-id="672fd-113">When an entity is deleted, hello health store automatically deletes all health reports associated with it.</span></span> <span data-ttu-id="672fd-114">Hello même a la valeur true lors de la création d’une nouvelle instance de l’entité de hello (par exemple, une nouvelle instance de réplica de service rendues persistantes avec état est créée).</span><span class="sxs-lookup"><span data-stu-id="672fd-114">hello same is true when a new instance of hello entity is created (for example, a new stateful persisted service replica instance is created).</span></span> <span data-ttu-id="672fd-115">Tous les rapports associés avec l’ancienne instance de hello sont supprimés et supprimés du magasin de hello.</span><span class="sxs-lookup"><span data-stu-id="672fd-115">All reports associated with hello old instance are deleted and cleaned up from hello store.</span></span>
> 
> 

<span data-ttu-id="672fd-116">rapports sur les composants système Hello sont identifiés par source de hello, qui commence par hello »**système.**»</span><span class="sxs-lookup"><span data-stu-id="672fd-116">hello system component reports are identified by hello source, which starts with hello "**System.**"</span></span> <span data-ttu-id="672fd-117">.</span><span class="sxs-lookup"><span data-stu-id="672fd-117">prefix.</span></span> <span data-ttu-id="672fd-118">Agents de surveillance ne peut pas utiliser hello même préfixe de leurs sources, comme des rapports avec des paramètres non valides sont rejetées.</span><span class="sxs-lookup"><span data-stu-id="672fd-118">Watchdogs can't use hello same prefix for their sources, as reports with invalid parameters are rejected.</span></span>
<span data-ttu-id="672fd-119">Nous allons examiner certains rapports toounderstand ce qui déclenche les et comment toocorrect hello éventuels problèmes qu’ils représentent.</span><span class="sxs-lookup"><span data-stu-id="672fd-119">Let's look at some system reports toounderstand what triggers them and how toocorrect hello possible issues they represent.</span></span>

> [!NOTE]
> <span data-ttu-id="672fd-120">Service Fabric continue tooadd des rapports sur les conditions d’intérêt qui améliorent la visibilité de ce qui se passe dans l’application et du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="672fd-120">Service Fabric continues tooadd reports on conditions of interest that improve visibility into what is happening in hello cluster and application.</span></span> <span data-ttu-id="672fd-121">Les rapports existants peuvent également être améliorées avec plus de détails toohelp dépannage hello plus rapidement.</span><span class="sxs-lookup"><span data-stu-id="672fd-121">Existing reports can also be enhanced with more details toohelp troubleshoot hello problem faster.</span></span>
> 
> 

## <a name="cluster-system-health-reports"></a><span data-ttu-id="672fd-122">Rapports d’intégrité du système sur le cluster</span><span class="sxs-lookup"><span data-stu-id="672fd-122">Cluster system health reports</span></span>
<span data-ttu-id="672fd-123">entité de contrôle d’intégrité de cluster Hello est créée automatiquement dans le magasin de contrôle d’intégrité hello.</span><span class="sxs-lookup"><span data-stu-id="672fd-123">hello cluster health entity is created automatically in hello health store.</span></span> <span data-ttu-id="672fd-124">Si tout fonctionne correctement, elle ne présente pas de rapport système.</span><span class="sxs-lookup"><span data-stu-id="672fd-124">If everything works properly, it doesn't have a system report.</span></span>

### <a name="neighborhood-loss"></a><span data-ttu-id="672fd-125">Perte de voisinage</span><span class="sxs-lookup"><span data-stu-id="672fd-125">Neighborhood loss</span></span>
<span data-ttu-id="672fd-126">**System.Federation** indique une erreur s’il détecte une perte de voisinage.</span><span class="sxs-lookup"><span data-stu-id="672fd-126">**System.Federation** reports an error when it detects a neighborhood loss.</span></span> <span data-ttu-id="672fd-127">rapport de Hello est à partir des nœuds individuels, et ID de nœud hello est inclus dans le nom de la propriété hello.</span><span class="sxs-lookup"><span data-stu-id="672fd-127">hello report is from individual nodes, and hello node ID is included in hello property name.</span></span> <span data-ttu-id="672fd-128">Si un cercle est perdue au cours de l’anneau de Service Fabric entière hello, vous verrez généralement deux événements (les deux côtés du rapport d’écart hello).</span><span class="sxs-lookup"><span data-stu-id="672fd-128">If one neighborhood is lost in hello entire Service Fabric ring, you can typically expect two events (both sides of hello gap report).</span></span> <span data-ttu-id="672fd-129">Si plusieurs voisinages sont perdus, d’autres d’événements ont lieu.</span><span class="sxs-lookup"><span data-stu-id="672fd-129">If more neighborhoods are lost, there are more events.</span></span>

<span data-ttu-id="672fd-130">rapport de Hello Spécifie le délai d’attente de hello bail global comme heure hello toolive.</span><span class="sxs-lookup"><span data-stu-id="672fd-130">hello report specifies hello global lease timeout as hello time toolive.</span></span> <span data-ttu-id="672fd-131">rapport de Hello est renvoyée à chaque semestre de durée de vie hello pour tant que condition de hello demeure active.</span><span class="sxs-lookup"><span data-stu-id="672fd-131">hello report is resent every half of hello TTL duration for as long as hello condition remains active.</span></span> <span data-ttu-id="672fd-132">événement de Hello est automatiquement supprimé lorsqu’il arrive à expiration.</span><span class="sxs-lookup"><span data-stu-id="672fd-132">hello event is automatically removed when it expires.</span></span> <span data-ttu-id="672fd-133">Supprimer lorsque le comportement expirée permet de s’assurer que les rapports de hello sont nettoyées à partir du magasin de contrôle d’intégrité hello correctement, même si le nœud de création de rapports hello est arrêté.</span><span class="sxs-lookup"><span data-stu-id="672fd-133">Remove when expired behavior ensures that hello report is cleaned up from hello health store correctly, even if hello reporting node is down.</span></span>

* <span data-ttu-id="672fd-134">**SourceId**: System.Federation.</span><span class="sxs-lookup"><span data-stu-id="672fd-134">**SourceId**: System.Federation</span></span>
* <span data-ttu-id="672fd-135">**Property** : commence par **Neighborhood** et inclut des informations sur le nœud.</span><span class="sxs-lookup"><span data-stu-id="672fd-135">**Property**: Starts with **Neighborhood** and includes node information</span></span>
* <span data-ttu-id="672fd-136">**Étapes suivantes**: recherchez pourquoi le voisinage de hello est perdue (par exemple, la communication de hello cocher entre les nœuds de cluster).</span><span class="sxs-lookup"><span data-stu-id="672fd-136">**Next steps**: Investigate why hello neighborhood is lost (for example, check hello communication between cluster nodes).</span></span>

## <a name="node-system-health-reports"></a><span data-ttu-id="672fd-137">Rapports d’intégrité du système sur les nœuds</span><span class="sxs-lookup"><span data-stu-id="672fd-137">Node system health reports</span></span>
<span data-ttu-id="672fd-138">**System.FM**, qui représente le service de gestionnaire de basculement hello, est l’autorité hello qui gère des informations sur les nœuds de cluster.</span><span class="sxs-lookup"><span data-stu-id="672fd-138">**System.FM**, which represents hello Failover Manager service, is hello authority that manages information about cluster nodes.</span></span> <span data-ttu-id="672fd-139">Un rapport System.FM indiquant son état doit être alloué à chaque nœud.</span><span class="sxs-lookup"><span data-stu-id="672fd-139">Each node should have one report from System.FM showing its state.</span></span> <span data-ttu-id="672fd-140">entités de nœud de Hello sont supprimées lors de l’état du nœud hello est supprimé (consultez [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).</span><span class="sxs-lookup"><span data-stu-id="672fd-140">hello node entities are removed when hello node state is removed (see [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).</span></span>

### <a name="node-updown"></a><span data-ttu-id="672fd-141">Nœud activé/désactivé</span><span class="sxs-lookup"><span data-stu-id="672fd-141">Node up/down</span></span>
<span data-ttu-id="672fd-142">System.FM signale comme OK lorsque le nœud de hello joint anneau hello (il est en cours d’exécution).</span><span class="sxs-lookup"><span data-stu-id="672fd-142">System.FM reports as OK when hello node joins hello ring (it's up and running).</span></span> <span data-ttu-id="672fd-143">Il signale une erreur lors de l’anneau de hello de départ du nœud de hello (elle est activée, la mise à niveau ou simplement, car il a échoué).</span><span class="sxs-lookup"><span data-stu-id="672fd-143">It reports an error when hello node departs hello ring (it's down, either for upgrading or simply because it has failed).</span></span> <span data-ttu-id="672fd-144">hiérarchie de contrôle d’intégrité Hello généré par le magasin de contrôle d’intégrité hello entreprend des actions sur les entités déployées en corrélation avec les rapports de nœuds System.FM.</span><span class="sxs-lookup"><span data-stu-id="672fd-144">hello health hierarchy built by hello health store takes action on deployed entities in correlation with System.FM node reports.</span></span> <span data-ttu-id="672fd-145">Il considère que le nœud de hello virtuel parent de toutes les entités déployés.</span><span class="sxs-lookup"><span data-stu-id="672fd-145">It considers hello node a virtual parent of all deployed entities.</span></span> <span data-ttu-id="672fd-146">entités Hello déployé sur ce nœud sont exposées via des requêtes si le nœud de hello est signalée comme par System.FM, avec hello même l’instance comme instance hello associée aux entités de hello.</span><span class="sxs-lookup"><span data-stu-id="672fd-146">hello deployed entities on that node are exposed through queries if hello node is reported as up by System.FM, with hello same instance as hello instance associated with hello entities.</span></span> <span data-ttu-id="672fd-147">Lorsque System.FM signale ce nœud hello est arrêté ou redémarré (une nouvelle instance), magasin de contrôle d’intégrité hello nettoie automatiquement les entités hello déployé qui peuvent exister uniquement sur hello nœud vers le bas ou sur l’instance précédente de hello du nœud de hello.</span><span class="sxs-lookup"><span data-stu-id="672fd-147">When System.FM reports that hello node is down or restarted (a new instance), hello health store automatically cleans up hello deployed entities that can exist only on hello down node or on hello previous instance of hello node.</span></span>

* <span data-ttu-id="672fd-148">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="672fd-148">**SourceId**: System.FM</span></span>
* <span data-ttu-id="672fd-149">**Property**: State</span><span class="sxs-lookup"><span data-stu-id="672fd-149">**Property**: State</span></span>
* <span data-ttu-id="672fd-150">**Étapes suivantes**: si le nœud de hello est arrêté pour une mise à niveau, il doit s’afficher dans une fois qu’il a été mis à niveau.</span><span class="sxs-lookup"><span data-stu-id="672fd-150">**Next steps**: If hello node is down for an upgrade, it should come back up once it has been upgraded.</span></span> <span data-ttu-id="672fd-151">Dans ce cas, l’état d’intégrité hello doit basculer tooOK précédent.</span><span class="sxs-lookup"><span data-stu-id="672fd-151">In this case, hello health state should switch back tooOK.</span></span> <span data-ttu-id="672fd-152">Si le nœud de hello ne revenez ou il échoue, problème de hello doit investigations plus poussées.</span><span class="sxs-lookup"><span data-stu-id="672fd-152">If hello node doesn't come back or it fails, hello problem needs more investigation.</span></span>

<span data-ttu-id="672fd-153">Hello exemple suivant montre hello System.FM événement avec un état d’intégrité de OK pour le nœud :</span><span class="sxs-lookup"><span data-stu-id="672fd-153">hello following example shows hello System.FM event with a health state of OK for node up:</span></span>

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


### <a name="certificate-expiration"></a><span data-ttu-id="672fd-154">Expiration du certificat</span><span class="sxs-lookup"><span data-stu-id="672fd-154">Certificate expiration</span></span>
<span data-ttu-id="672fd-155">**System.FabricNode** émet un avertissement quand les certificats utilisés par le nœud de hello sont arrivant à expiration.</span><span class="sxs-lookup"><span data-stu-id="672fd-155">**System.FabricNode** reports a warning when certificates used by hello node are near expiration.</span></span> <span data-ttu-id="672fd-156">Chaque nœud comporte trois certificats associés : **Certificate_cluster**, **Certificate_server** et **Certificate_default_client**.</span><span class="sxs-lookup"><span data-stu-id="672fd-156">There are three certificates per node: **Certificate_cluster**, **Certificate_server**, and **Certificate_default_client**.</span></span> <span data-ttu-id="672fd-157">Lorsque le délai d’expiration de la hello est au moins deux semaines, état d’intégrité de rapport hello est OK.</span><span class="sxs-lookup"><span data-stu-id="672fd-157">When hello expiration is at least two weeks away, hello report health state is OK.</span></span> <span data-ttu-id="672fd-158">Lorsque le délai d’expiration de hello est dans les deux semaines, le type de rapport hello est un avertissement.</span><span class="sxs-lookup"><span data-stu-id="672fd-158">When hello expiration is within two weeks, hello report type is a warning.</span></span> <span data-ttu-id="672fd-159">Durée de vie de ces événements est infinie, et ils sont supprimés quand un nœud quitte hello cluster.</span><span class="sxs-lookup"><span data-stu-id="672fd-159">TTL of these events is infinite, and they are removed when a node leaves hello cluster.</span></span>

* <span data-ttu-id="672fd-160">**SourceId**: System.FabricNode</span><span class="sxs-lookup"><span data-stu-id="672fd-160">**SourceId**: System.FabricNode</span></span>
* <span data-ttu-id="672fd-161">**Propriété**: commence par **certificat** et contient plus d’informations sur le type de certificat hello</span><span class="sxs-lookup"><span data-stu-id="672fd-161">**Property**: Starts with **Certificate** and contains more information about hello certificate type</span></span>
* <span data-ttu-id="672fd-162">**Étapes suivantes**: mettre à jour les certificats hello s’ils sont arrivant à expiration.</span><span class="sxs-lookup"><span data-stu-id="672fd-162">**Next steps**: Update hello certificates if they are near expiration.</span></span>

### <a name="load-capacity-violation"></a><span data-ttu-id="672fd-163">Violation de capacité de charge</span><span class="sxs-lookup"><span data-stu-id="672fd-163">Load capacity violation</span></span>
<span data-ttu-id="672fd-164">Hello équilibrage de charge de l’infrastructure de Service émet un avertissement lorsqu’il détecte une violation de capacité de nœud.</span><span class="sxs-lookup"><span data-stu-id="672fd-164">hello Service Fabric Load Balancer reports a warning when it detects a node capacity violation.</span></span>

* <span data-ttu-id="672fd-165">**SourceId**: System.PLB</span><span class="sxs-lookup"><span data-stu-id="672fd-165">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="672fd-166">**Property** : commence par **Capacity**</span><span class="sxs-lookup"><span data-stu-id="672fd-166">**Property**: Starts with **Capacity**</span></span>
* <span data-ttu-id="672fd-167">**Étapes suivantes**: vérification fournies capacité actuelle de métriques et vue hello sur le nœud de hello.</span><span class="sxs-lookup"><span data-stu-id="672fd-167">**Next steps**: Check provided metrics and view hello current capacity on hello node.</span></span>

## <a name="application-system-health-reports"></a><span data-ttu-id="672fd-168">Rapports d’intégrité du système sur les applications</span><span class="sxs-lookup"><span data-stu-id="672fd-168">Application system health reports</span></span>
<span data-ttu-id="672fd-169">**System.CM**, qui représente le service de gestionnaire du Cluster de hello, est l’autorité hello qui gère les informations relatives à une application.</span><span class="sxs-lookup"><span data-stu-id="672fd-169">**System.CM**, which represents hello Cluster Manager service, is hello authority that manages information about an application.</span></span>

### <a name="state"></a><span data-ttu-id="672fd-170">State</span><span class="sxs-lookup"><span data-stu-id="672fd-170">State</span></span>
<span data-ttu-id="672fd-171">System.CM signale comme OK lorsque l’application hello a été créée ou mis à jour.</span><span class="sxs-lookup"><span data-stu-id="672fd-171">System.CM reports as OK when hello application has been created or updated.</span></span> <span data-ttu-id="672fd-172">Il informe magasin de contrôle d’intégrité hello lors de l’application hello a été supprimée, afin qu’il peut être supprimé de la banque.</span><span class="sxs-lookup"><span data-stu-id="672fd-172">It informs hello health store when hello application has been deleted, so that it can be removed from store.</span></span>

* <span data-ttu-id="672fd-173">**SourceId**: System.CM</span><span class="sxs-lookup"><span data-stu-id="672fd-173">**SourceId**: System.CM</span></span>
* <span data-ttu-id="672fd-174">**Property**: State</span><span class="sxs-lookup"><span data-stu-id="672fd-174">**Property**: State</span></span>
* <span data-ttu-id="672fd-175">**Étapes suivantes**: si l’application hello a été créée ou mis à jour, elle doit inclure un rapport de contrôle d’intégrité hello Gestionnaire du Cluster.</span><span class="sxs-lookup"><span data-stu-id="672fd-175">**Next steps**: If hello application has been created or updated, it should include hello Cluster Manager health report.</span></span> <span data-ttu-id="672fd-176">Vous pouvez aussi consulter état hello de l’application hello en émettant une requête (par exemple, hello applet de commande PowerShell **ServiceFabricApplication de Get - ApplicationName *applicationName***).</span><span class="sxs-lookup"><span data-stu-id="672fd-176">Otherwise, check hello state of hello application by issuing a query (for example, hello PowerShell cmdlet **Get-ServiceFabricApplication -ApplicationName *applicationName***).</span></span>

<span data-ttu-id="672fd-177">Hello suivant montre l’événement d’état hello sur hello **fabric : / WordCount** application :</span><span class="sxs-lookup"><span data-stu-id="672fd-177">hello following example shows hello state event on hello **fabric:/WordCount** application:</span></span>

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

## <a name="service-system-health-reports"></a><span data-ttu-id="672fd-178">Rapports d’intégrité du système sur les services</span><span class="sxs-lookup"><span data-stu-id="672fd-178">Service system health reports</span></span>
<span data-ttu-id="672fd-179">**System.FM**, qui représente le service de gestionnaire de basculement hello, est l’autorité hello qui gère les informations sur les services.</span><span class="sxs-lookup"><span data-stu-id="672fd-179">**System.FM**, which represents hello Failover Manager service, is hello authority that manages information about services.</span></span>

### <a name="state"></a><span data-ttu-id="672fd-180">State</span><span class="sxs-lookup"><span data-stu-id="672fd-180">State</span></span>
<span data-ttu-id="672fd-181">System.FM signale comme OK lorsque hello service a été créé.</span><span class="sxs-lookup"><span data-stu-id="672fd-181">System.FM reports as OK when hello service has been created.</span></span> <span data-ttu-id="672fd-182">Supprime les entités hello à partir du magasin de contrôle d’intégrité hello lorsque hello service a été supprimé.</span><span class="sxs-lookup"><span data-stu-id="672fd-182">It deletes hello entity from hello health store when hello service has been deleted.</span></span>

* <span data-ttu-id="672fd-183">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="672fd-183">**SourceId**: System.FM</span></span>
* <span data-ttu-id="672fd-184">**Property**: State</span><span class="sxs-lookup"><span data-stu-id="672fd-184">**Property**: State</span></span>

<span data-ttu-id="672fd-185">Hello suivant montre l’événement d’état hello sur le service de hello **fabric : / WordCount/WordCountWebService**:</span><span class="sxs-lookup"><span data-stu-id="672fd-185">hello following example shows hello state event on hello service **fabric:/WordCount/WordCountWebService**:</span></span>

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

### <a name="service-correlation-error"></a><span data-ttu-id="672fd-186">Erreur de corrélation de services</span><span class="sxs-lookup"><span data-stu-id="672fd-186">Service correlation error</span></span>
<span data-ttu-id="672fd-187">**System.PLB** signale une erreur lorsqu’il détecte que la mise à jour d’un toobe de service mis en corrélation avec un autre service crée une chaîne d’affinité.</span><span class="sxs-lookup"><span data-stu-id="672fd-187">**System.PLB** reports an error when it detects that updating a service toobe correlated with another service creates an affinity chain.</span></span> <span data-ttu-id="672fd-188">rapport de Hello est désactivée lors de la mise à jour réussie se produit.</span><span class="sxs-lookup"><span data-stu-id="672fd-188">hello report is cleared when successful update happens.</span></span>

* <span data-ttu-id="672fd-189">**SourceId**: System.PLB</span><span class="sxs-lookup"><span data-stu-id="672fd-189">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="672fd-190">**Property** : ServiceDescription</span><span class="sxs-lookup"><span data-stu-id="672fd-190">**Property**: ServiceDescription</span></span>
* <span data-ttu-id="672fd-191">**Étapes suivantes**: hello de vérification mis en corrélation les descriptions de service.</span><span class="sxs-lookup"><span data-stu-id="672fd-191">**Next steps**: Check hello correlated service descriptions.</span></span>

## <a name="partition-system-health-reports"></a><span data-ttu-id="672fd-192">Rapports d’intégrité du système sur les partitions</span><span class="sxs-lookup"><span data-stu-id="672fd-192">Partition system health reports</span></span>
<span data-ttu-id="672fd-193">**System.FM**, qui représente le service de gestionnaire de basculement hello, est l’autorité hello qui gère les informations sur les partitions de service.</span><span class="sxs-lookup"><span data-stu-id="672fd-193">**System.FM**, which represents hello Failover Manager service, is hello authority that manages information about service partitions.</span></span>

### <a name="state"></a><span data-ttu-id="672fd-194">State</span><span class="sxs-lookup"><span data-stu-id="672fd-194">State</span></span>
<span data-ttu-id="672fd-195">System.FM signale comme OK lors de la partition de hello a été créée et est intègre.</span><span class="sxs-lookup"><span data-stu-id="672fd-195">System.FM reports as OK when hello partition has been created and is healthy.</span></span> <span data-ttu-id="672fd-196">Supprime les entités hello à partir du magasin de contrôle d’intégrité hello lorsque hello partition est supprimée.</span><span class="sxs-lookup"><span data-stu-id="672fd-196">It deletes hello entity from hello health store when hello partition is deleted.</span></span>

<span data-ttu-id="672fd-197">Si la partition de hello est inférieur à nombre de réplicas minimale hello, il signale une erreur.</span><span class="sxs-lookup"><span data-stu-id="672fd-197">If hello partition is below hello minimum replica count, it reports an error.</span></span> <span data-ttu-id="672fd-198">Si la partition de hello n’est pas sous le nombre de réplicas minimale hello, mais il est sous le nombre de réplicas cible hello, il émet un avertissement.</span><span class="sxs-lookup"><span data-stu-id="672fd-198">If hello partition is not below hello minimum replica count, but it is below hello target replica count, it reports a warning.</span></span> <span data-ttu-id="672fd-199">Si la partition de hello est une perte de quorum, System.FM signale une erreur.</span><span class="sxs-lookup"><span data-stu-id="672fd-199">If hello partition is in quorum loss, System.FM reports an error.</span></span>

<span data-ttu-id="672fd-200">Autres événements importants incluent un avertissement lors de la reconfiguration de hello prend plus de temps que prévu, et lors de la génération de hello prend plus longtemps que prévu.</span><span class="sxs-lookup"><span data-stu-id="672fd-200">Other important events include a warning when hello reconfiguration takes longer than expected and when hello build takes longer than expected.</span></span> <span data-ttu-id="672fd-201">fois Hello attendu pour la génération de hello et la reconfiguration sont configurables selon les scénarios de service.</span><span class="sxs-lookup"><span data-stu-id="672fd-201">hello expected times for hello build and reconfiguration are configurable based on service scenarios.</span></span> <span data-ttu-id="672fd-202">Par exemple, si un service dispose d’un téraoctet d’état, telles que de la base de données SQL, génération de hello prend plue d’un service avec une petite quantité d’état.</span><span class="sxs-lookup"><span data-stu-id="672fd-202">For example, if a service has a terabyte of state, such as SQL Database, hello build takes longer than for a service with a small amount of state.</span></span>

* <span data-ttu-id="672fd-203">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="672fd-203">**SourceId**: System.FM</span></span>
* <span data-ttu-id="672fd-204">**Property**: State</span><span class="sxs-lookup"><span data-stu-id="672fd-204">**Property**: State</span></span>
* <span data-ttu-id="672fd-205">**Étapes suivantes**: si l’état d’intégrité hello n’est pas OK, il est possible que certains réplicas n’ont pas été promue, créé ou ouvert tooprimary ou base de données secondaire correctement.</span><span class="sxs-lookup"><span data-stu-id="672fd-205">**Next steps**: If hello health state is not OK, it's possible that some replicas have not been created, opened, or promoted tooprimary or secondary correctly.</span></span> <span data-ttu-id="672fd-206">Dans de nombreux cas, la cause première hello est un bogue de service dans hello ouverte ou l’implémentation de la modification du rôle.</span><span class="sxs-lookup"><span data-stu-id="672fd-206">In many instances, hello root cause is a service bug in hello open or change-role implementation.</span></span>

<span data-ttu-id="672fd-207">Bonjour à l’exemple suivant montre une partition intègre :</span><span class="sxs-lookup"><span data-stu-id="672fd-207">hello following example shows a healthy partition:</span></span>

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

<span data-ttu-id="672fd-208">Hello suivant montre la santé d’une partition qui est sous le nombre de réplicas cible hello.</span><span class="sxs-lookup"><span data-stu-id="672fd-208">hello following example shows hello health of a partition that is below target replica count.</span></span> <span data-ttu-id="672fd-209">étape suivante de Hello est tooget hello description de la partition, ce qui indique la façon dont il est configuré : **MinReplicaSetSize** est trois et **TargetReplicaSetSize** est sept.</span><span class="sxs-lookup"><span data-stu-id="672fd-209">hello next step is tooget hello partition description, which shows how it is configured: **MinReplicaSetSize** is three and **TargetReplicaSetSize** is seven.</span></span> <span data-ttu-id="672fd-210">Puis obtenir nombre hello de nœuds de cluster de hello : cinq.</span><span class="sxs-lookup"><span data-stu-id="672fd-210">Then get hello number of nodes in hello cluster: five.</span></span> <span data-ttu-id="672fd-211">Par conséquent, dans ce cas, deux réplicas ne peut pas être placés, car le nombre de cibles hello de réplicas est supérieur au numéro de hello de nœuds disponibles.</span><span class="sxs-lookup"><span data-stu-id="672fd-211">So in this case, two replicas can't be placed because hello target number of replicas is higher than hello number of nodes available.</span></span>

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
                        Description           : hello Load Balancer was unable toofind a placement for one or more of hello Service's Replicas:
                        Secondary replica could not be placed due toohello following constraints and properties:  
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

### <a name="replica-constraint-violation"></a><span data-ttu-id="672fd-212">Violation des contraintes de réplicas</span><span class="sxs-lookup"><span data-stu-id="672fd-212">Replica constraint violation</span></span>
<span data-ttu-id="672fd-213">**System.PLB** indique un avertissement s’il détecte une violation des contraintes de réplicas et qu’il ne peut pas placer tous les réplicas de la partition.</span><span class="sxs-lookup"><span data-stu-id="672fd-213">**System.PLB** reports a warning if it detects a replica constraint violation and can't place all partition replicas.</span></span> <span data-ttu-id="672fd-214">affichent les détails du rapport Hello les contraintes et les propriétés empêchent le positionnement de réplica hello.</span><span class="sxs-lookup"><span data-stu-id="672fd-214">hello report details show which constraints and properties prevent hello replica placement.</span></span>

* <span data-ttu-id="672fd-215">**SourceId**: System.PLB</span><span class="sxs-lookup"><span data-stu-id="672fd-215">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="672fd-216">**Property** : commence par **ReplicaConstraintViolation**</span><span class="sxs-lookup"><span data-stu-id="672fd-216">**Property**: Starts with **ReplicaConstraintViolation**</span></span>

## <a name="replica-system-health-reports"></a><span data-ttu-id="672fd-217">Rapports d’intégrité du système sur les réplicas</span><span class="sxs-lookup"><span data-stu-id="672fd-217">Replica system health reports</span></span>
<span data-ttu-id="672fd-218">**System.RA**, qui représente le composant de l’agent de reconfiguration hello, est l’autorité hello pour l’état du réplica hello.</span><span class="sxs-lookup"><span data-stu-id="672fd-218">**System.RA**, which represents hello reconfiguration agent component, is hello authority for hello replica state.</span></span>

### <a name="state"></a><span data-ttu-id="672fd-219">State</span><span class="sxs-lookup"><span data-stu-id="672fd-219">State</span></span>
<span data-ttu-id="672fd-220">**System.RA** indique OK lorsque hello réplica a été créé.</span><span class="sxs-lookup"><span data-stu-id="672fd-220">**System.RA** reports OK when hello replica has been created.</span></span>

* <span data-ttu-id="672fd-221">**SourceId**: System.RA</span><span class="sxs-lookup"><span data-stu-id="672fd-221">**SourceId**: System.RA</span></span>
* <span data-ttu-id="672fd-222">**Property**: State</span><span class="sxs-lookup"><span data-stu-id="672fd-222">**Property**: State</span></span>

<span data-ttu-id="672fd-223">Bonjour à l’exemple suivant montre un réplica intègre :</span><span class="sxs-lookup"><span data-stu-id="672fd-223">hello following example shows a healthy replica:</span></span>

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

### <a name="replica-open-status"></a><span data-ttu-id="672fd-224">État d’ouverture du réplica</span><span class="sxs-lookup"><span data-stu-id="672fd-224">Replica open status</span></span>
<span data-ttu-id="672fd-225">description de Hello de ce rapport d’intégrité contient l’heure de début de hello (temps universel) lors de l’appel de hello API a été appelé.</span><span class="sxs-lookup"><span data-stu-id="672fd-225">hello description of this health report contains hello start time (Coordinated Universal Time) when hello API call was invoked.</span></span>

<span data-ttu-id="672fd-226">**System.RA** émet un avertissement si le réplica hello ouvrir dure plus longtemps que la période de hello configuré (par défaut : 30 minutes).</span><span class="sxs-lookup"><span data-stu-id="672fd-226">**System.RA** reports a warning if hello replica open takes longer than hello configured period (default: 30 minutes).</span></span> <span data-ttu-id="672fd-227">Si hello API a un impact sur la disponibilité du service, les rapports hello sont émise beaucoup plus rapidement (un intervalle peut être configuré avec une valeur par défaut de 30 secondes).</span><span class="sxs-lookup"><span data-stu-id="672fd-227">If hello API impacts service availability, hello report is issued much faster (a configurable interval, with a default of 30 seconds).</span></span> <span data-ttu-id="672fd-228">Durée Hello mesuré inclut temps hello réplicateur hello ouvert et service hello ouvert.</span><span class="sxs-lookup"><span data-stu-id="672fd-228">hello time measured includes hello time taken for hello replicator open and hello service open.</span></span> <span data-ttu-id="672fd-229">tooOK de modifications de propriété Hello si hello ouvrez se termine.</span><span class="sxs-lookup"><span data-stu-id="672fd-229">hello property changes tooOK if hello open completes.</span></span>

* <span data-ttu-id="672fd-230">**SourceId**: System.RA</span><span class="sxs-lookup"><span data-stu-id="672fd-230">**SourceId**: System.RA</span></span>
* <span data-ttu-id="672fd-231">**Property**: **ReplicaOpenStatus**</span><span class="sxs-lookup"><span data-stu-id="672fd-231">**Property**: **ReplicaOpenStatus**</span></span>
* <span data-ttu-id="672fd-232">**Étapes suivantes**: si l’état d’intégrité hello n’est pas OK, recherchez pourquoi le réplica hello ouvrir prend plus longtemps que prévu.</span><span class="sxs-lookup"><span data-stu-id="672fd-232">**Next steps**: If hello health state is not OK, investigate why hello replica open takes longer than expected.</span></span>

### <a name="slow-service-api-call"></a><span data-ttu-id="672fd-233">Appel lent d’API de service</span><span class="sxs-lookup"><span data-stu-id="672fd-233">Slow service API call</span></span>
<span data-ttu-id="672fd-234">**System.RAP** et **System.Replicator** signaler un avertissement si un code de service appel toohello utilisateur prend plu de temps de hello configuré.</span><span class="sxs-lookup"><span data-stu-id="672fd-234">**System.RAP** and **System.Replicator** report a warning if a call toohello user service code takes longer than hello configured time.</span></span> <span data-ttu-id="672fd-235">Avertissement de Hello est désactivée lors de la fin de l’appel hello.</span><span class="sxs-lookup"><span data-stu-id="672fd-235">hello warning is cleared when hello call completes.</span></span>

* <span data-ttu-id="672fd-236">**SourceId**: System.RAP ou System.Replicator</span><span class="sxs-lookup"><span data-stu-id="672fd-236">**SourceId**: System.RAP or System.Replicator</span></span>
* <span data-ttu-id="672fd-237">**Propriété**: nom hello de l’API de lentes hello.</span><span class="sxs-lookup"><span data-stu-id="672fd-237">**Property**: hello name of hello slow API.</span></span> <span data-ttu-id="672fd-238">description de Hello fournit plus de détails sur hello de temps hello API a été en attente.</span><span class="sxs-lookup"><span data-stu-id="672fd-238">hello description provides more details about hello time hello API has been pending.</span></span>
* <span data-ttu-id="672fd-239">**Étapes suivantes**: recherchez pourquoi l’appel de hello prend plus de temps que prévu.</span><span class="sxs-lookup"><span data-stu-id="672fd-239">**Next steps**: Investigate why hello call takes longer than expected.</span></span>

<span data-ttu-id="672fd-240">Hello, l’exemple suivant montre une partition de perte de quorum et hello enquête étapes faits toofigure pourquoi.</span><span class="sxs-lookup"><span data-stu-id="672fd-240">hello following example shows a partition in quorum loss, and hello investigation steps done toofigure out why.</span></span> <span data-ttu-id="672fd-241">Un des réplicas de hello a un état d’avertissement, vous obtenir son intégrité.</span><span class="sxs-lookup"><span data-stu-id="672fd-241">One of hello replicas has a warning health state, so you get its health.</span></span> <span data-ttu-id="672fd-242">Il indique qu’opération de service hello l'prend plus longtemps que prévu, un événement signalé par System.RAP.</span><span class="sxs-lookup"><span data-stu-id="672fd-242">It shows that hello service operation takes longer than expected, an event reported by System.RAP.</span></span> <span data-ttu-id="672fd-243">Une fois ces informations sont reçues, étape suivante de hello est toolook au code de service hello et examinez il.</span><span class="sxs-lookup"><span data-stu-id="672fd-243">After this information is received, hello next step is toolook at hello service code and investigate there.</span></span> <span data-ttu-id="672fd-244">Dans ce cas, hello **RunAsync** implémentation d’un service avec état hello lève une exception non gérée.</span><span class="sxs-lookup"><span data-stu-id="672fd-244">For this case, hello **RunAsync** implementation of hello stateful service throws an unhandled exception.</span></span> <span data-ttu-id="672fd-245">les réplicas Hello sont recyclage, donc vous ne pouvez pas voir tous les réplicas dans un état d’avertissement hello.</span><span class="sxs-lookup"><span data-stu-id="672fd-245">hello replicas are recycling, so you may not see any replicas in hello warning state.</span></span> <span data-ttu-id="672fd-246">Vous pouvez réessayer de l’état d’intégrité hello lors de l’obtention et voir les différences dans l’ID de réplica hello.</span><span class="sxs-lookup"><span data-stu-id="672fd-246">You can retry getting hello health state and look for any differences in hello replica ID.</span></span> <span data-ttu-id="672fd-247">Dans certains cas, les tentatives de hello peuvent vous donner des indices.</span><span class="sxs-lookup"><span data-stu-id="672fd-247">In certain cases, hello retries can give you clues.</span></span>

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

<span data-ttu-id="672fd-248">Lorsque vous démarrez application défectueux hello sous le débogueur de hello, windows des événements de diagnostic hello affichent hello une exception à partir de RunAsync :</span><span class="sxs-lookup"><span data-stu-id="672fd-248">When you start hello faulty application under hello debugger, hello diagnostic events windows show hello exception thrown from RunAsync:</span></span>

![Événements de diagnostic Visual Studio 2015 : Échec de RunAsync dans la structure : /HelloWorldStatefulApplication.][1]

<span data-ttu-id="672fd-250">Événements de diagnostic Visual Studio 2015 : Échec de RunAsync dans la **structure : /HelloWorldStatefulApplication**.</span><span class="sxs-lookup"><span data-stu-id="672fd-250">Visual Studio 2015 diagnostic events: RunAsync failure in **fabric:/HelloWorldStatefulApplication**.</span></span>

[1]: ./media/service-fabric-understand-and-troubleshoot-with-system-health-reports/servicefabric-health-vs-runasync-exception.png


### <a name="replication-queue-full"></a><span data-ttu-id="672fd-251">File d’attente de réplication complète</span><span class="sxs-lookup"><span data-stu-id="672fd-251">Replication queue full</span></span>
<span data-ttu-id="672fd-252">**System.Replicator** émet un avertissement lors de la file d’attente de réplication hello est plein.</span><span class="sxs-lookup"><span data-stu-id="672fd-252">**System.Replicator** reports a warning when hello replication queue is full.</span></span> <span data-ttu-id="672fd-253">Sur hello principal, file d’attente de réplication généralement est saturé, car un ou plusieurs réplicas secondaires sont des opérations de tooacknowledge lente.</span><span class="sxs-lookup"><span data-stu-id="672fd-253">On hello primary, replication queue usually becomes full because one or more secondary replicas are slow tooacknowledge operations.</span></span> <span data-ttu-id="672fd-254">Sur hello secondaire, cela se produit généralement lorsque les service hello est tooapply lentes hello operations.</span><span class="sxs-lookup"><span data-stu-id="672fd-254">On hello secondary, this usually happens when hello service is slow tooapply hello operations.</span></span> <span data-ttu-id="672fd-255">Avertissement de Hello est désactivée lors de la file d’attente hello n’est plus complète.</span><span class="sxs-lookup"><span data-stu-id="672fd-255">hello warning is cleared when hello queue is no longer full.</span></span>

* <span data-ttu-id="672fd-256">**SourceId**: System.Replicator</span><span class="sxs-lookup"><span data-stu-id="672fd-256">**SourceId**: System.Replicator</span></span>
* <span data-ttu-id="672fd-257">**Propriété**: **PrimaryReplicationQueueStatus** ou **SecondaryReplicationQueueStatus**, en fonction du rôle de réplica hello</span><span class="sxs-lookup"><span data-stu-id="672fd-257">**Property**: **PrimaryReplicationQueueStatus** or **SecondaryReplicationQueueStatus**, depending on hello replica role</span></span>

### <a name="slow-naming-operations"></a><span data-ttu-id="672fd-258">Opérations de nommage lentes</span><span class="sxs-lookup"><span data-stu-id="672fd-258">Slow Naming operations</span></span>
<span data-ttu-id="672fd-259">**System.NamingService** signale l’intégrité sur son réplica principal quand une opération de nommage prend trop de temps.</span><span class="sxs-lookup"><span data-stu-id="672fd-259">**System.NamingService** reports health on its primary replica when a Naming operation takes longer than acceptable.</span></span> <span data-ttu-id="672fd-260">[CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) et [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) sont des exemples d’opérations de nommage.</span><span class="sxs-lookup"><span data-stu-id="672fd-260">Examples of Naming operations are [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) or [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync).</span></span> <span data-ttu-id="672fd-261">D’autres méthodes se trouvent sous FabricClient, par exemple dans les [méthodes de gestion de service](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) ou les [méthodes de gestion de propriété](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).</span><span class="sxs-lookup"><span data-stu-id="672fd-261">More methods can be found under FabricClient, for example under [service management methods](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) or [property management methods](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).</span></span>

> [!NOTE]
> <span data-ttu-id="672fd-262">Hello Naming service résout l’emplacement de tooa de noms de service dans un cluster de hello et permet les propriétés et les noms de service toomanage les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="672fd-262">hello Naming service resolves service names tooa location in hello cluster and enables users toomanage service names and properties.</span></span> <span data-ttu-id="672fd-263">Il s’agit d’un service persistant partitionné Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="672fd-263">It is a Service Fabric partitioned persisted service.</span></span> <span data-ttu-id="672fd-264">Une des partitions de hello représente hello Authority Owner, qui contient des métadonnées sur tous les services et les noms de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="672fd-264">One of hello partitions represents hello Authority Owner, which contains metadata about all Service Fabric names and services.</span></span> <span data-ttu-id="672fd-265">noms de Service Fabric Hello sont des partitions de toodifferent mappé, appelées partitions du nom du propriétaire, le service hello est extensible.</span><span class="sxs-lookup"><span data-stu-id="672fd-265">hello Service Fabric names are mapped toodifferent partitions, called Name Owner partitions, so hello service is extensible.</span></span> <span data-ttu-id="672fd-266">En savoir plus sur le [service de nommage](service-fabric-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="672fd-266">Read more about [Naming service](service-fabric-architecture.md).</span></span>
> 
> 

<span data-ttu-id="672fd-267">Quand une opération d’affectation de noms prend plus longtemps que prévu, l’opération de hello est marquée avec un état d’avertissement sur hello *réplica principal de hello d’affectation de noms partition de service qui sert d’opération de hello*.</span><span class="sxs-lookup"><span data-stu-id="672fd-267">When a Naming operation takes longer than expected, hello operation is flagged with a Warning report on hello *primary replica of hello Naming service partition that serves hello operation*.</span></span> <span data-ttu-id="672fd-268">Si l’opération de hello est correctement exécutée, hello avertissement est désactivé.</span><span class="sxs-lookup"><span data-stu-id="672fd-268">If hello operation completes successfully, hello Warning is cleared.</span></span> <span data-ttu-id="672fd-269">Si l’opération de hello est terminée avec une erreur hello d’intégrité inclut des détails sur les erreurs hello.</span><span class="sxs-lookup"><span data-stu-id="672fd-269">If hello operation completes with an error, hello health report includes details about hello error.</span></span>

* <span data-ttu-id="672fd-270">**SourceId**: System.NamingService</span><span class="sxs-lookup"><span data-stu-id="672fd-270">**SourceId**: System.NamingService</span></span>
* <span data-ttu-id="672fd-271">**Propriété**: commence par le préfixe **Duration_** et identifie les opération lente hello et nom de Service Fabric hello sur quel hello opération est appliquée.</span><span class="sxs-lookup"><span data-stu-id="672fd-271">**Property**: Starts with prefix **Duration_** and identifies hello slow operation and hello Service Fabric name on which hello operation is applied.</span></span> <span data-ttu-id="672fd-272">Par exemple, si créer un service à l’ensemble fibre optique de nom : / MyApp/MyService prend trop de temps, la propriété de hello est Duration_AOCreateService.fabric:/MyApp/MyService.</span><span class="sxs-lookup"><span data-stu-id="672fd-272">For example, if create service at name fabric:/MyApp/MyService takes too long, hello property is Duration_AOCreateService.fabric:/MyApp/MyService.</span></span> <span data-ttu-id="672fd-273">Rôle de toohello AO points Hello partition d’affectation de noms pour ce nom et l’opération.</span><span class="sxs-lookup"><span data-stu-id="672fd-273">AO points toohello role of hello Naming partition for this name and operation.</span></span>
* <span data-ttu-id="672fd-274">**Étapes suivantes**: vérification pourquoi hello d’affectation de noms opération échoue.</span><span class="sxs-lookup"><span data-stu-id="672fd-274">**Next steps**: Check why hello Naming operation fails.</span></span> <span data-ttu-id="672fd-275">Chaque opération peut avoir différentes causes principales.</span><span class="sxs-lookup"><span data-stu-id="672fd-275">Each operation can have different root causes.</span></span> <span data-ttu-id="672fd-276">Par exemple, supprimez service peut se bloquer sur un nœud, car l’hôte d’application hello conserve en panne sur un nœud en raison du bogue d’utilisateur tooa dans le code de service hello.</span><span class="sxs-lookup"><span data-stu-id="672fd-276">For example, delete service may be stuck on a node because hello application host keeps crashing on a node due tooa user bug in hello service code.</span></span>

<span data-ttu-id="672fd-277">Bonjour à l’exemple suivant montre une opération de service de création.</span><span class="sxs-lookup"><span data-stu-id="672fd-277">hello following example shows a create service operation.</span></span> <span data-ttu-id="672fd-278">opération de Hello a duré plus longtemps que durée de hello configuré.</span><span class="sxs-lookup"><span data-stu-id="672fd-278">hello operation took longer than hello configured duration.</span></span> <span data-ttu-id="672fd-279">AO nouvelle tentative et envoie le travail tooNO.</span><span class="sxs-lookup"><span data-stu-id="672fd-279">AO retries and sends work tooNO.</span></span> <span data-ttu-id="672fd-280">AUCUNE opération dernière hello terminé avec délai d’attente.</span><span class="sxs-lookup"><span data-stu-id="672fd-280">NO completed hello last operation with Timeout.</span></span> <span data-ttu-id="672fd-281">Dans ce cas, hello même réplica est principal pour hello AO et aucun rôle.</span><span class="sxs-lookup"><span data-stu-id="672fd-281">In this case, hello same replica is primary for both hello AO and NO roles.</span></span>

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
                        Description           : hello AOCreateService started at 2016-04-29 20:39:08.677 is taking longer than 30.000.
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
                        Description           : hello NOCreateService started at 2016-04-29 20:39:08.689 completed with FABRIC_E_TIMEOUT in more than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM
```

## <a name="deployedapplication-system-health-reports"></a><span data-ttu-id="672fd-282">Rapports d’intégrité du système sur les applications déployées</span><span class="sxs-lookup"><span data-stu-id="672fd-282">DeployedApplication system health reports</span></span>
<span data-ttu-id="672fd-283">**System.Hosting** est autorité hello sur les entités déployées.</span><span class="sxs-lookup"><span data-stu-id="672fd-283">**System.Hosting** is hello authority on deployed entities.</span></span>

### <a name="activation"></a><span data-ttu-id="672fd-284">Activation</span><span class="sxs-lookup"><span data-stu-id="672fd-284">Activation</span></span>
<span data-ttu-id="672fd-285">System.Hosting signale comme OK quand une application a été activée avec succès sur le nœud de hello.</span><span class="sxs-lookup"><span data-stu-id="672fd-285">System.Hosting reports as OK when an application has been successfully activated on hello node.</span></span> <span data-ttu-id="672fd-286">Dans le cas contraire, il indique une erreur.</span><span class="sxs-lookup"><span data-stu-id="672fd-286">Otherwise, it reports an error.</span></span>

* <span data-ttu-id="672fd-287">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="672fd-287">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="672fd-288">**Propriété**: l’Activation, y compris la version de déploiement hello</span><span class="sxs-lookup"><span data-stu-id="672fd-288">**Property**: Activation, including hello rollout version</span></span>
* <span data-ttu-id="672fd-289">**Étapes suivantes**: si l’application hello est défectueux, recherchez pourquoi l’activation hello a échoué.</span><span class="sxs-lookup"><span data-stu-id="672fd-289">**Next steps**: If hello application is unhealthy, investigate why hello activation failed.</span></span>

<span data-ttu-id="672fd-290">Hello exemple suivant illustre l’activation réussie :</span><span class="sxs-lookup"><span data-stu-id="672fd-290">hello following example shows successful activation:</span></span>

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
                                     Description           : hello application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a><span data-ttu-id="672fd-291">Télécharger</span><span class="sxs-lookup"><span data-stu-id="672fd-291">Download</span></span>
<span data-ttu-id="672fd-292">**System.Hosting** signale une erreur si le téléchargement de package d’application hello échoue.</span><span class="sxs-lookup"><span data-stu-id="672fd-292">**System.Hosting** reports an error if hello application package download fails.</span></span>

* <span data-ttu-id="672fd-293">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="672fd-293">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="672fd-294">**Property** : **Download:*RolloutVersion***</span><span class="sxs-lookup"><span data-stu-id="672fd-294">**Property**: **Download:*RolloutVersion***</span></span>
* <span data-ttu-id="672fd-295">**Étapes suivantes**: recherchez pourquoi le téléchargement de hello a échoué sur le nœud de hello.</span><span class="sxs-lookup"><span data-stu-id="672fd-295">**Next steps**: Investigate why hello download failed on hello node.</span></span>

## <a name="deployedservicepackage-system-health-reports"></a><span data-ttu-id="672fd-296">Rapports d’intégrité du système sur le package de service déployé</span><span class="sxs-lookup"><span data-stu-id="672fd-296">DeployedServicePackage system health reports</span></span>
<span data-ttu-id="672fd-297">**System.Hosting** est autorité hello sur les entités déployées.</span><span class="sxs-lookup"><span data-stu-id="672fd-297">**System.Hosting** is hello authority on deployed entities.</span></span>

### <a name="service-package-activation"></a><span data-ttu-id="672fd-298">Activation du package de service</span><span class="sxs-lookup"><span data-stu-id="672fd-298">Service package activation</span></span>
<span data-ttu-id="672fd-299">System.Hosting signale comme OK si l’activation du package service hello sur le nœud de hello a réussi.</span><span class="sxs-lookup"><span data-stu-id="672fd-299">System.Hosting reports as OK if hello service package activation on hello node is successful.</span></span> <span data-ttu-id="672fd-300">Dans le cas contraire, il indique une erreur.</span><span class="sxs-lookup"><span data-stu-id="672fd-300">Otherwise, it reports an error.</span></span>

* <span data-ttu-id="672fd-301">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="672fd-301">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="672fd-302">**Property**: Activation</span><span class="sxs-lookup"><span data-stu-id="672fd-302">**Property**: Activation</span></span>
* <span data-ttu-id="672fd-303">**Étapes suivantes**: recherchez pourquoi l’activation hello a échoué.</span><span class="sxs-lookup"><span data-stu-id="672fd-303">**Next steps**: Investigate why hello activation failed.</span></span>

### <a name="code-package-activation"></a><span data-ttu-id="672fd-304">Activation du package de code</span><span class="sxs-lookup"><span data-stu-id="672fd-304">Code package activation</span></span>
<span data-ttu-id="672fd-305">**System.Hosting** signale comme OK pour chaque package de code si hello activation a réussi.</span><span class="sxs-lookup"><span data-stu-id="672fd-305">**System.Hosting** reports as OK for each code package if hello activation is successful.</span></span> <span data-ttu-id="672fd-306">Si l’activation de hello échoue, il émet un avertissement, tel que configuré.</span><span class="sxs-lookup"><span data-stu-id="672fd-306">If hello activation fails, it reports a warning as configured.</span></span> <span data-ttu-id="672fd-307">Si **CodePackage** tooactivate d’échoue ou se termine avec une erreur supérieure hello configuré **CodePackageHealthErrorThreshold**, hébergement signale une erreur.</span><span class="sxs-lookup"><span data-stu-id="672fd-307">If **CodePackage** fails tooactivate or terminates with an error greater than hello configured **CodePackageHealthErrorThreshold**, hosting reports an error.</span></span> <span data-ttu-id="672fd-308">Si un package de service contient plusieurs packages de code, un rapport d’activation est généré pour chacun d’entre eux.</span><span class="sxs-lookup"><span data-stu-id="672fd-308">If a service package contains multiple code packages, an activation report is generated for each one.</span></span>

* <span data-ttu-id="672fd-309">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="672fd-309">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="672fd-310">**Propriété**: préfixe de hello utilise **CodePackageActivation** et contient le nom hello de package de code hello et le point d’entrée hello en tant que  **CodePackageActivation :* CodePackageName*:*SetupEntryPoint/EntryPoint*** (par exemple, **CodePackageActivation:Code:SetupEntryPoint**)</span><span class="sxs-lookup"><span data-stu-id="672fd-310">**Property**: Uses hello prefix **CodePackageActivation** and contains hello name of hello code package and hello entry point as **CodePackageActivation:*CodePackageName*:*SetupEntryPoint/EntryPoint*** (for example, **CodePackageActivation:Code:SetupEntryPoint**)</span></span>

### <a name="service-type-registration"></a><span data-ttu-id="672fd-311">Inscription du type de service</span><span class="sxs-lookup"><span data-stu-id="672fd-311">Service type registration</span></span>
<span data-ttu-id="672fd-312">**System.Hosting** signale comme OK si le type de service hello a été correctement enregistré.</span><span class="sxs-lookup"><span data-stu-id="672fd-312">**System.Hosting** reports as OK if hello service type has been registered successfully.</span></span> <span data-ttu-id="672fd-313">Il signale une erreur si l’inscription de hello n’était pas terminée dans le temps (tel que configuré à l’aide de **ServiceTypeRegistrationTimeout**).</span><span class="sxs-lookup"><span data-stu-id="672fd-313">It reports an error if hello registration wasn't done in time (as configured by using **ServiceTypeRegistrationTimeout**).</span></span> <span data-ttu-id="672fd-314">Si l’exécution de hello est fermée, le type de service hello est plus inscrit dans le nœud de hello et hébergement émet un avertissement.</span><span class="sxs-lookup"><span data-stu-id="672fd-314">If hello runtime is closed, hello service type is unregistered from hello node and Hosting reports a warning.</span></span>

* <span data-ttu-id="672fd-315">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="672fd-315">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="672fd-316">**Propriété**: préfixe de hello utilise **ServiceTypeRegistration** et contient le nom de type hello service (par exemple, **ServiceTypeRegistration:FileStoreServiceType**)</span><span class="sxs-lookup"><span data-stu-id="672fd-316">**Property**: Uses hello prefix **ServiceTypeRegistration** and contains hello service type name (for example, **ServiceTypeRegistration:FileStoreServiceType**)</span></span>

<span data-ttu-id="672fd-317">Bonjour à l’exemple suivant montre un package de service déployé intègre :</span><span class="sxs-lookup"><span data-stu-id="672fd-317">hello following example shows a healthy deployed service package:</span></span>

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
                             Description           : hello ServicePackage was activated successfully.
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
                             Description           : hello CodePackage was activated successfully.
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
                             Description           : hello ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a><span data-ttu-id="672fd-318">Télécharger</span><span class="sxs-lookup"><span data-stu-id="672fd-318">Download</span></span>
<span data-ttu-id="672fd-319">**System.Hosting** signale une erreur si le téléchargement du package hello service échoue.</span><span class="sxs-lookup"><span data-stu-id="672fd-319">**System.Hosting** reports an error if hello service package download fails.</span></span>

* <span data-ttu-id="672fd-320">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="672fd-320">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="672fd-321">**Property** : **Download:*RolloutVersion***</span><span class="sxs-lookup"><span data-stu-id="672fd-321">**Property**: **Download:*RolloutVersion***</span></span>
* <span data-ttu-id="672fd-322">**Étapes suivantes**: recherchez pourquoi le téléchargement de hello a échoué sur le nœud de hello.</span><span class="sxs-lookup"><span data-stu-id="672fd-322">**Next steps**: Investigate why hello download failed on hello node.</span></span>

### <a name="upgrade-validation"></a><span data-ttu-id="672fd-323">Validation de mise à niveau</span><span class="sxs-lookup"><span data-stu-id="672fd-323">Upgrade validation</span></span>
<span data-ttu-id="672fd-324">**System.Hosting** signale une erreur si la validation pendant la mise à niveau hello échoue ou si hello mise à niveau échoue sur le nœud de hello.</span><span class="sxs-lookup"><span data-stu-id="672fd-324">**System.Hosting** reports an error if validation during hello upgrade fails or if hello upgrade fails on hello node.</span></span>

* <span data-ttu-id="672fd-325">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="672fd-325">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="672fd-326">**Propriété**: préfixe de hello utilise **FabricUpgradeValidation** et contient la version de mise à niveau hello</span><span class="sxs-lookup"><span data-stu-id="672fd-326">**Property**: Uses hello prefix **FabricUpgradeValidation** and contains hello upgrade version</span></span>
* <span data-ttu-id="672fd-327">**Description**: erreur toohello de pointe</span><span class="sxs-lookup"><span data-stu-id="672fd-327">**Description**: Points toohello error encountered</span></span>

## <a name="next-steps"></a><span data-ttu-id="672fd-328">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="672fd-328">Next steps</span></span>
[<span data-ttu-id="672fd-329">Affichage rapports d’intégrité de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="672fd-329">View Service Fabric health reports</span></span>](service-fabric-view-entities-aggregated-health.md)

[<span data-ttu-id="672fd-330">Comment tooreport et vérification du service d’intégrité</span><span class="sxs-lookup"><span data-stu-id="672fd-330">How tooreport and check service health</span></span>](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[<span data-ttu-id="672fd-331">Surveiller et diagnostiquer les services localement</span><span class="sxs-lookup"><span data-stu-id="672fd-331">Monitor and diagnose services locally</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="672fd-332">Mise à niveau des applications Service Fabric</span><span class="sxs-lookup"><span data-stu-id="672fd-332">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

