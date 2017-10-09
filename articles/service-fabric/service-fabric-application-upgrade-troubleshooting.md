---
title: "mises à niveau des applications aaaTroubleshooting | Documents Microsoft"
description: "Cet article aborde certains problèmes courants autour de la mise à niveau une application de Service Fabric et comment tooresolve les."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 19ad152e-ec50-4327-9f19-065c875c003c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 0f56fa61db9b4e32824623f162dc1bfe7fda0f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-application-upgrades"></a><span data-ttu-id="daff1-103">Résoudre les problèmes de mise à niveau d'application</span><span class="sxs-lookup"><span data-stu-id="daff1-103">Troubleshoot application upgrades</span></span>
<span data-ttu-id="daff1-104">Cet article décrit certains des problèmes courants de hello autour de la mise à niveau une application Azure Service Fabric et comment tooresolve les.</span><span class="sxs-lookup"><span data-stu-id="daff1-104">This article covers some of hello common issues around upgrading an Azure Service Fabric application and how tooresolve them.</span></span>

## <a name="troubleshoot-a-failed-application-upgrade"></a><span data-ttu-id="daff1-105">Résoudre les problèmes liés à l'échec de la mise à niveau d'une application</span><span class="sxs-lookup"><span data-stu-id="daff1-105">Troubleshoot a failed application upgrade</span></span>
<span data-ttu-id="daff1-106">Lorsqu’une mise à niveau échoue, sortie hello Hello **Get-ServiceFabricApplicationUpgrade** commande contient des informations supplémentaires pour le débogage d’échec de hello.</span><span class="sxs-lookup"><span data-stu-id="daff1-106">When an upgrade fails, hello output of hello **Get-ServiceFabricApplicationUpgrade** command contains additional information for debugging hello failure.</span></span>  <span data-ttu-id="daff1-107">Hello liste suivante indique comment les informations supplémentaires de hello peuvent être utilisées :</span><span class="sxs-lookup"><span data-stu-id="daff1-107">hello following list specifies how hello additional information can be used:</span></span>

1. <span data-ttu-id="daff1-108">Identifier le type d’échec hello.</span><span class="sxs-lookup"><span data-stu-id="daff1-108">Identify hello failure type.</span></span>
2. <span data-ttu-id="daff1-109">Identifiez la raison de l’échec hello.</span><span class="sxs-lookup"><span data-stu-id="daff1-109">Identify hello failure reason.</span></span>
3. <span data-ttu-id="daff1-110">Isoler le ou les composants défectueux en vue d’un examen approfondi.</span><span class="sxs-lookup"><span data-stu-id="daff1-110">Isolate one or more failing components for further investigation.</span></span>

<span data-ttu-id="daff1-111">Ces informations sont disponibles lorsque le Service Fabric détecte l’échec de hello, indépendamment de si hello **FailureAction** tooroll DOS ou suspendre la mise à niveau hello.</span><span class="sxs-lookup"><span data-stu-id="daff1-111">This information is available when Service Fabric detects hello failure regardless of whether hello **FailureAction** is tooroll back or suspend hello upgrade.</span></span>

### <a name="identify-hello-failure-type"></a><span data-ttu-id="daff1-112">Identifier le type d’échec hello</span><span class="sxs-lookup"><span data-stu-id="daff1-112">Identify hello failure type</span></span>
<span data-ttu-id="daff1-113">Dans la sortie de hello de **Get-ServiceFabricApplicationUpgrade**, **FailureTimestampUtc** identifie hello horodateur (UTC) à laquelle un échec de mise à niveau a été détecté par l’infrastructure de Service et  **FailureAction** a été déclenchée.</span><span class="sxs-lookup"><span data-stu-id="daff1-113">In hello output of **Get-ServiceFabricApplicationUpgrade**, **FailureTimestampUtc** identifies hello timestamp (in UTC) at which an upgrade failure was detected by Service Fabric and **FailureAction** was triggered.</span></span> <span data-ttu-id="daff1-114">**Raison de l’échec** identifie l’un de trois causes principales de l’échec de hello :</span><span class="sxs-lookup"><span data-stu-id="daff1-114">**FailureReason** identifies one of three potential high-level causes of hello failure:</span></span>

1. <span data-ttu-id="daff1-115">UpgradeDomainTimeout - indique qu’un domaine de mise à niveau particulier a pris trop de temps toocomplete et **UpgradeDomainTimeout** a expiré.</span><span class="sxs-lookup"><span data-stu-id="daff1-115">UpgradeDomainTimeout - Indicates that a particular upgrade domain took too long toocomplete and **UpgradeDomainTimeout** expired.</span></span>
2. <span data-ttu-id="daff1-116">OverallUpgradeTimeout - indique que hello globale de mise à niveau a duré trop long toocomplete et **UpgradeTimeout** a expiré.</span><span class="sxs-lookup"><span data-stu-id="daff1-116">OverallUpgradeTimeout - Indicates that hello overall upgrade took too long toocomplete and **UpgradeTimeout** expired.</span></span>
3. <span data-ttu-id="daff1-117">Vérification de l’intégrité - indique qu’après la mise à niveau un domaine de mise à jour, application hello est restée défectueuse selon toohello spécifié des stratégies d’intégrité et **HealthCheckRetryTimeout** a expiré.</span><span class="sxs-lookup"><span data-stu-id="daff1-117">HealthCheck - Indicates that after upgrading an update domain, hello application remained unhealthy according toohello specified health policies and **HealthCheckRetryTimeout** expired.</span></span>

<span data-ttu-id="daff1-118">Ces entrées apparaissent seulement dans la sortie de hello lors de la mise à niveau hello échoue et démarre l’annulation.</span><span class="sxs-lookup"><span data-stu-id="daff1-118">These entries only show up in hello output when hello upgrade fails and starts rolling back.</span></span> <span data-ttu-id="daff1-119">Informations complémentaires sont affichées en fonction de type hello de défaillance de hello.</span><span class="sxs-lookup"><span data-stu-id="daff1-119">Further information is displayed depending on hello type of hello failure.</span></span>

### <a name="investigate-upgrade-timeouts"></a><span data-ttu-id="daff1-120">Examiner les dépassements de délai d'attente de mise à niveau</span><span class="sxs-lookup"><span data-stu-id="daff1-120">Investigate upgrade timeouts</span></span>
<span data-ttu-id="daff1-121">Les échecs de délai d'attente de mise à niveau sont généralement dus à des problèmes de disponibilité de service.</span><span class="sxs-lookup"><span data-stu-id="daff1-121">Upgrade timeout failures are most commonly caused by service availability issues.</span></span> <span data-ttu-id="daff1-122">sortie Hello ci-dessous est typique de mises à niveau si les réplicas de service ou les instances ne toostart dans la nouvelle version de code hello.</span><span class="sxs-lookup"><span data-stu-id="daff1-122">hello output following this paragraph is typical of upgrades where service replicas or instances fail toostart in hello new code version.</span></span> <span data-ttu-id="daff1-123">Hello **UpgradeDomainProgressAtFailure** champ capture un instantané de tout travail de mise à niveau en attente au moment de hello de défaillance.</span><span class="sxs-lookup"><span data-stu-id="daff1-123">hello **UpgradeDomainProgressAtFailure** field captures a snapshot of any pending upgrade work at hello time of failure.</span></span>

```
PS D:\temp> Get-ServiceFabricApplicationUpgrade fabric:/DemoApp

ApplicationName                : fabric:/DemoApp
ApplicationTypeName            : DemoAppType
TargetApplicationTypeVersion   : v2
ApplicationParameters          : {}
StartTimestampUtc              : 4/14/2015 9:26:38 PM
FailureTimestampUtc            : 4/14/2015 9:27:05 PM
FailureReason                  : UpgradeDomainTimeout
UpgradeDomainProgressAtFailure : MYUD1

                                 NodeName            : Node4
                                 UpgradePhase        : PostUpgradeSafetyCheck
                                 PendingSafetyChecks :
                                     WaitForPrimaryPlacement - PartitionId: 744c8d9f-1d26-417e-a60e-cd48f5c098f0

                                 NodeName            : Node1
                                 UpgradePhase        : PostUpgradeSafetyCheck
                                 PendingSafetyChecks :
                                     WaitForPrimaryPlacement - PartitionId: 4b43f4d8-b26b-424e-9307-7a7a62e79750
UpgradeState                   : RollingBackCompleted
UpgradeDuration                : 00:00:46
CurrentUpgradeDomainDuration   : 00:00:00
NextUpgradeDomain              :
UpgradeDomainsStatus           : { "MYUD1" = "Completed";
                                 "MYUD2" = "Completed";
                                 "MYUD3" = "Completed" }
UpgradeKind                    : Rolling
RollingUpgradeMode             : UnmonitoredAuto
ForceRestart                   : False
UpgradeReplicaSetCheckTimeout  : 00:00:00
```

<span data-ttu-id="daff1-124">Dans cet exemple, mise à niveau hello échec au niveau du domaine de mise à niveau *MYUD1* et deux partitions (*744c8d9f-1d26-417e-a60e-cd48f5c098f0* et *4b43f4d8-b26b-424e-9307-7a7a62e79750*) ont été bloqués.</span><span class="sxs-lookup"><span data-stu-id="daff1-124">In this example, hello upgrade failed at upgrade domain *MYUD1* and two partitions (*744c8d9f-1d26-417e-a60e-cd48f5c098f0* and *4b43f4d8-b26b-424e-9307-7a7a62e79750*) were stuck.</span></span> <span data-ttu-id="daff1-125">les partitions Hello ont été bloquées car hello runtime a été impossible de tooplace les réplicas principaux (*WaitForPrimaryPlacement*) sur les nœuds cibles *Node1* et *Node4*.</span><span class="sxs-lookup"><span data-stu-id="daff1-125">hello partitions were stuck because hello runtime was unable tooplace primary replicas (*WaitForPrimaryPlacement*) on target nodes *Node1* and *Node4*.</span></span>

<span data-ttu-id="daff1-126">Hello **Get-ServiceFabricNode** commande peut être utilisé tooverify que ces deux nœuds sont dans le domaine de mise à niveau *MYUD1*.</span><span class="sxs-lookup"><span data-stu-id="daff1-126">hello **Get-ServiceFabricNode** command can be used tooverify that these two nodes are in upgrade domain *MYUD1*.</span></span> <span data-ttu-id="daff1-127">Hello *UpgradePhase* indique que *PostUpgradeSafetyCheck*, ce qui signifie que ces contrôles de sécurité sont produisent une fois tous les nœuds dans le domaine de mise à niveau hello ont terminé la mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="daff1-127">hello *UpgradePhase* says *PostUpgradeSafetyCheck*, which means that these safety checks are occurring after all nodes in hello upgrade domain have finished upgrading.</span></span> <span data-ttu-id="daff1-128">Toutes ces informations pointant tooa le problème potentiel avec hello nouvelle version du code de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="daff1-128">All this information points tooa potential issue with hello new version of hello application code.</span></span> <span data-ttu-id="daff1-129">les problèmes les plus courants Hello des erreurs service hello open ou les chemins de code de promotion tooprimary.</span><span class="sxs-lookup"><span data-stu-id="daff1-129">hello most common issues are service errors in hello open or promotion tooprimary code paths.</span></span>

<span data-ttu-id="daff1-130">Un *UpgradePhase* de *PreUpgradeSafetyCheck* signifie problèmes de domaine de mise à niveau hello avant qu’il a été effectuée.</span><span class="sxs-lookup"><span data-stu-id="daff1-130">An *UpgradePhase* of *PreUpgradeSafetyCheck* means there were issues preparing hello upgrade domain before it was performed.</span></span> <span data-ttu-id="daff1-131">Dans ce cas, les problèmes les plus courants Hello sont erreurs service hello fermer ou de rétrogradation à partir des chemins de code principal.</span><span class="sxs-lookup"><span data-stu-id="daff1-131">hello most common issues in this case are service errors in hello close or demotion from primary code paths.</span></span>

<span data-ttu-id="daff1-132">Hello actuel **UpgradeState** est *RollingBackCompleted*, de sorte que la mise à niveau d’origine de hello doit avoir été effectuée avec une restauration **FailureAction**, qui automatiquement restaurée de la mise à niveau hello en cas d’échec.</span><span class="sxs-lookup"><span data-stu-id="daff1-132">hello current **UpgradeState** is *RollingBackCompleted*, so hello original upgrade must have been performed with a rollback **FailureAction**, which automatically rolled back hello upgrade upon failure.</span></span> <span data-ttu-id="daff1-133">Si une mise à niveau d’origine de hello a été effectuée d’une opération manuelle **FailureAction**, puis de la mise à niveau hello serait à la place dans un état suspendu de tooallow dynamique de débogage de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="daff1-133">If hello original upgrade was performed with a manual **FailureAction**, then hello upgrade would instead be in a suspended state tooallow live debugging of hello application.</span></span>

### <a name="investigate-health-check-failures"></a><span data-ttu-id="daff1-134">Examiner les échecs des contrôles d'intégrité</span><span class="sxs-lookup"><span data-stu-id="daff1-134">Investigate health check failures</span></span>
<span data-ttu-id="daff1-135">Des échecs de contrôle d’intégrité peuvent être déclenchés par divers problèmes qui peuvent se produire après la mise à niveau de tous les nœuds dans un domaine de mise à niveau et la réussite de tous les contrôles de sécurité.</span><span class="sxs-lookup"><span data-stu-id="daff1-135">Health check failures can be triggered by various issues that can happen after all nodes in an upgrade domain finish upgrading and passing all safety checks.</span></span> <span data-ttu-id="daff1-136">sortie Hello ci-dessous est typique d’un échec de mise à niveau en raison des contrôles d’intégrité de toofailed.</span><span class="sxs-lookup"><span data-stu-id="daff1-136">hello output following this paragraph is typical of an upgrade failure due toofailed health checks.</span></span> <span data-ttu-id="daff1-137">Hello **UnhealthyEvaluations** champ capture un instantané des contrôles d’intégrité qui a échoué lors de mise à niveau hello selon toohello spécifié hello [stratégie d’intégrité](service-fabric-health-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="daff1-137">hello **UnhealthyEvaluations** field captures a snapshot of health checks that failed at hello time of hello upgrade according toohello specified [health policy](service-fabric-health-introduction.md).</span></span>

```
PS D:\temp> Get-ServiceFabricApplicationUpgrade fabric:/DemoApp

ApplicationName                         : fabric:/DemoApp
ApplicationTypeName                     : DemoAppType
TargetApplicationTypeVersion            : v4
ApplicationParameters                   : {}
StartTimestampUtc                       : 4/24/2015 2:42:31 AM
UpgradeState                            : RollingForwardPending
UpgradeDuration                         : 00:00:27
CurrentUpgradeDomainDuration            : 00:00:27
NextUpgradeDomain                       : MYUD2
UpgradeDomainsStatus                    : { "MYUD1" = "Completed";
                                          "MYUD2" = "Pending";
                                          "MYUD3" = "Pending" }
UnhealthyEvaluations                    :
                                          Unhealthy services: 50% (2/4), ServiceType='PersistedServiceType', MaxPercentUnhealthyServices=0%.

                                          Unhealthy service: ServiceName='fabric:/DemoApp/Svc3', AggregatedHealthState='Error'.

                                              Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                              Unhealthy partition: PartitionId='3a9911f6-a2e5-452d-89a8-09271e7e49a8', AggregatedHealthState='Error'.

                                                  Error event: SourceId='Replica', Property='InjectedFault'.

                                          Unhealthy service: ServiceName='fabric:/DemoApp/Svc2', AggregatedHealthState='Error'.

                                              Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                              Unhealthy partition: PartitionId='744c8d9f-1d26-417e-a60e-cd48f5c098f0', AggregatedHealthState='Error'.

                                                  Error event: SourceId='Replica', Property='InjectedFault'.

UpgradeKind                             : Rolling
RollingUpgradeMode                      : Monitored
FailureAction                           : Manual
ForceRestart                            : False
UpgradeReplicaSetCheckTimeout           : 49710.06:28:15
HealthCheckWaitDuration                 : 00:00:00
HealthCheckStableDuration               : 00:00:10
HealthCheckRetryTimeout                 : 00:00:10
UpgradeDomainTimeout                    : 10675199.02:48:05.4775807
UpgradeTimeout                          : 10675199.02:48:05.4775807
ConsiderWarningAsError                  :
MaxPercentUnhealthyPartitionsPerService :
MaxPercentUnhealthyReplicasPerPartition :
MaxPercentUnhealthyServices             :
MaxPercentUnhealthyDeployedApplications :
ServiceTypeHealthPolicyMap              :
```

<span data-ttu-id="daff1-138">Enquête sur les échecs de vérification d’intégrité exige en premier lieu une présentation du modèle de contrôle d’intégrité de l’infrastructure de Service hello.</span><span class="sxs-lookup"><span data-stu-id="daff1-138">Investigating health check failures first requires an understanding of hello Service Fabric health model.</span></span> <span data-ttu-id="daff1-139">Mais même sans ces approfondies, nous pouvons voir que les deux services ne sont pas intègres : *fabric : / DemoApp/Svc3* et *fabric : / DemoApp/Svc2*, ainsi que les rapports d’intégrité erreur hello (« InjectedFault « Dans ce cas).</span><span class="sxs-lookup"><span data-stu-id="daff1-139">But even without such an in-depth understanding, we can see that two services are unhealthy: *fabric:/DemoApp/Svc3* and *fabric:/DemoApp/Svc2*, along with hello error health reports ("InjectedFault" in this case).</span></span> <span data-ttu-id="daff1-140">Dans cet exemple, deux des quatre services sont défectueux, ce qui est sous la cible par défaut de hello de 0 % défectueux (*MaxPercentUnhealthyServices*).</span><span class="sxs-lookup"><span data-stu-id="daff1-140">In this example, two out of four services are unhealthy, which is below hello default target of 0% unhealthy (*MaxPercentUnhealthyServices*).</span></span>

<span data-ttu-id="daff1-141">Hello mise à niveau a été suspendu lors de l’échec en spécifiant un **FailureAction** de manuelle lorsque démarrage hello mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="daff1-141">hello upgrade was suspended upon failing by specifying a **FailureAction** of manual when starting hello upgrade.</span></span> <span data-ttu-id="daff1-142">Ce mode permet tooinvestigate hello dynamique du système en état de hello a échoué avant toute autre action.</span><span class="sxs-lookup"><span data-stu-id="daff1-142">This mode allows us tooinvestigate hello live system in hello failed state before taking any further action.</span></span>

### <a name="recover-from-a-suspended-upgrade"></a><span data-ttu-id="daff1-143">Récupérer à partir d'une mise à niveau suspendue</span><span class="sxs-lookup"><span data-stu-id="daff1-143">Recover from a suspended upgrade</span></span>
<span data-ttu-id="daff1-144">Avec une restauration **FailureAction**, il n’existe aucune récupération n’est nécessaire car la mise à niveau hello restaure automatiquement sur l’échec.</span><span class="sxs-lookup"><span data-stu-id="daff1-144">With a rollback **FailureAction**, there is no recovery needed since hello upgrade automatically rolls back upon failing.</span></span> <span data-ttu-id="daff1-145">Si une opération **FailureAction**manuelle est définie, plusieurs options de récupération existent :</span><span class="sxs-lookup"><span data-stu-id="daff1-145">With a manual **FailureAction**, there are several recovery options:</span></span>

1.  <span data-ttu-id="daff1-146">Déclencher une restauration</span><span class="sxs-lookup"><span data-stu-id="daff1-146">trigger a rollback</span></span>
2. <span data-ttu-id="daff1-147">Suivez les étapes reste hello de mise à niveau hello manuellement</span><span class="sxs-lookup"><span data-stu-id="daff1-147">Proceed through hello remainder of hello upgrade manually</span></span>
3. <span data-ttu-id="daff1-148">Hello de CV analysée mise à niveau</span><span class="sxs-lookup"><span data-stu-id="daff1-148">Resume hello monitored upgrade</span></span>

<span data-ttu-id="daff1-149">Hello **ServiceFabricApplicationRollback de début** à n’importe quel toostart temps annulation application hello, vous pouvez utiliser la commande.</span><span class="sxs-lookup"><span data-stu-id="daff1-149">hello **Start-ServiceFabricApplicationRollback** command can be used at any time toostart rolling back hello application.</span></span> <span data-ttu-id="daff1-150">Une fois la commande hello est retournée avec succès, une requête rollback hello a été inscrit dans le système de hello et démarre peu de temps après.</span><span class="sxs-lookup"><span data-stu-id="daff1-150">Once hello command returns successfully, hello rollback request has been registered in hello system and starts shortly thereafter.</span></span>

<span data-ttu-id="daff1-151">Hello **Resume-ServiceFabricApplicationUpgrade** commande peut être utilisée tooproceed via reste hello Hello mise à niveau manuellement, un seul domaine de mise à niveau à la fois.</span><span class="sxs-lookup"><span data-stu-id="daff1-151">hello **Resume-ServiceFabricApplicationUpgrade** command can be used tooproceed through hello remainder of hello upgrade manually, one upgrade domain at a time.</span></span> <span data-ttu-id="daff1-152">Dans ce mode, les vérifications de sécurité uniquement effectuées par ce hello.</span><span class="sxs-lookup"><span data-stu-id="daff1-152">In this mode, only safety checks are performed by hello system.</span></span> <span data-ttu-id="daff1-153">Aucun contrôle d’intégrité supplémentaire n’est effectué.</span><span class="sxs-lookup"><span data-stu-id="daff1-153">No more health checks are performed.</span></span> <span data-ttu-id="daff1-154">Cette commande peut être utilisée uniquement lorsque hello *UpgradeState* montre *RollingForwardPending*, ce qui signifie que ce domaine de mise à niveau en cours hello a terminé la mise à niveau, mais hello ensuite une n’a pas démarré (en attente).</span><span class="sxs-lookup"><span data-stu-id="daff1-154">This command can only be used when hello *UpgradeState* shows *RollingForwardPending*, which means that hello current upgrade domain has finished upgrading but hello next one has not started (pending).</span></span>

<span data-ttu-id="daff1-155">Hello **mise à jour-ServiceFabricApplicationUpgrade** commande peut être mise à niveau de hello analysé tooresume utilisés avec les vérifications de sécurité et de santé en cours.</span><span class="sxs-lookup"><span data-stu-id="daff1-155">hello **Update-ServiceFabricApplicationUpgrade** command can be used tooresume hello monitored upgrade with both safety and health checks being performed.</span></span>

```
PS D:\temp> Update-ServiceFabricApplicationUpgrade fabric:/DemoApp -UpgradeMode Monitored

UpgradeMode                             : Monitored
ForceRestart                            :
UpgradeReplicaSetCheckTimeout           :
FailureAction                           :
HealthCheckWaitDuration                 :
HealthCheckStableDuration               :
HealthCheckRetryTimeout                 :
UpgradeTimeout                          :
UpgradeDomainTimeout                    :
ConsiderWarningAsError                  :
MaxPercentUnhealthyPartitionsPerService :
MaxPercentUnhealthyReplicasPerPartition :
MaxPercentUnhealthyServices             :
MaxPercentUnhealthyDeployedApplications :
ServiceTypeHealthPolicyMap              :

PS D:\temp>
```

<span data-ttu-id="daff1-156">mise à niveau de Hello continue à partir de domaine de mise à niveau hello dans laquelle il a été interrompu en dernier et hello utilisez même mettre à niveau les paramètres et stratégies d’intégrité en tant qu’avant.</span><span class="sxs-lookup"><span data-stu-id="daff1-156">hello upgrade continues from hello upgrade domain where it was last suspended and use hello same upgrade parameters and health policies as before.</span></span> <span data-ttu-id="daff1-157">Si nécessaire, un des paramètres de mise à niveau hello et stratégies d’intégrité illustrés hello précédant la sortie peut être modifié dans hello même commande lors de la mise à niveau hello reprend.</span><span class="sxs-lookup"><span data-stu-id="daff1-157">If needed, any of hello upgrade parameters and health policies shown in hello preceding output can be changed in hello same command when hello upgrade resumes.</span></span> <span data-ttu-id="daff1-158">Dans cet exemple, la mise à niveau hello a repris en mode surveillés, avec des paramètres de hello et de stratégies d’intégrité hello inchangées.</span><span class="sxs-lookup"><span data-stu-id="daff1-158">In this example, hello upgrade was resumed in Monitored mode, with hello parameters and hello health policies unchanged.</span></span>

## <a name="further-troubleshooting"></a><span data-ttu-id="daff1-159">Suite de la résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="daff1-159">Further troubleshooting</span></span>
### <a name="service-fabric-is-not-following-hello-specified-health-policies"></a><span data-ttu-id="daff1-160">L’infrastructure de service n’est pas les hello spécifié stratégies d’intégrité</span><span class="sxs-lookup"><span data-stu-id="daff1-160">Service Fabric is not following hello specified health policies</span></span>
<span data-ttu-id="daff1-161">Cause possible 1 :</span><span class="sxs-lookup"><span data-stu-id="daff1-161">Possible Cause 1:</span></span>

<span data-ttu-id="daff1-162">L’infrastructure de service se traduit par des pourcentages tous les chiffres réels d’entités (par exemple, les réplicas, partitions et les services) pour l’évaluation d’intégrité et arrondit toujours des entités de toowhole.</span><span class="sxs-lookup"><span data-stu-id="daff1-162">Service Fabric translates all percentages into actual numbers of entities (for example, replicas, partitions, and services) for health evaluation and always rounds up toowhole entities.</span></span> <span data-ttu-id="daff1-163">Par exemple, si hello maximale *MaxPercentUnhealthyReplicasPerPartition* est 21 % et il existe cinq réplicas, puis le Service Fabric permet des réplicas de fonctionnement anormal tootwo (autrement dit,`Math.Ceiling (5*0.21)`).</span><span class="sxs-lookup"><span data-stu-id="daff1-163">For example, if hello maximum *MaxPercentUnhealthyReplicasPerPartition* is 21% and there are five replicas, then Service Fabric allows up tootwo unhealthy replicas (that is,`Math.Ceiling (5*0.21)`).</span></span> <span data-ttu-id="daff1-164">Par conséquent, les stratégies de contrôle d’intégrité doivent être définies pour tenir compte de cela.</span><span class="sxs-lookup"><span data-stu-id="daff1-164">Thus, health policies should be set accordingly.</span></span>

<span data-ttu-id="daff1-165">Cause possible 2 :</span><span class="sxs-lookup"><span data-stu-id="daff1-165">Possible Cause 2:</span></span>

<span data-ttu-id="daff1-166">Les stratégies d'intégrité sont spécifiées en pourcentages du nombre total de services et non en instances de service spécifiques.</span><span class="sxs-lookup"><span data-stu-id="daff1-166">Health policies are specified in terms of percentages of total services and not specific service instances.</span></span> <span data-ttu-id="daff1-167">Par exemple, avant une mise à niveau, si une application possède quatre instances A, B, C et D, de service où service D n’est pas intègre, mais avec application de toohello faible impact.</span><span class="sxs-lookup"><span data-stu-id="daff1-167">For example, before an upgrade, if an application has four service instances A, B, C, and D, where service D is unhealthy but with little impact toohello application.</span></span> <span data-ttu-id="daff1-168">Nous souhaitons hello tooignore connue de service non intègre D lors de paramètre de mise à niveau et définissez hello *MaxPercentUnhealthyServices* toobe 25 %, en supposant seulement A, B et C doivent toobe sain.</span><span class="sxs-lookup"><span data-stu-id="daff1-168">We want tooignore hello known unhealthy service D during upgrade and set hello parameter *MaxPercentUnhealthyServices* toobe 25%, assuming only A, B, and C need toobe healthy.</span></span>

<span data-ttu-id="daff1-169">Toutefois, au cours de la mise à niveau de hello, D peut-être devenir intègre tandis que C devient non intègre.</span><span class="sxs-lookup"><span data-stu-id="daff1-169">However, during hello upgrade, D may become healthy while C becomes unhealthy.</span></span> <span data-ttu-id="daff1-170">mise à niveau Hello réussit toujours, car seuls 25 % de services de hello ne sont pas intègres.</span><span class="sxs-lookup"><span data-stu-id="daff1-170">hello upgrade would still succeed because only 25% of hello services are unhealthy.</span></span> <span data-ttu-id="daff1-171">Toutefois, cela peut entraîner des erreurs imprévues échéance tooC en cours défectueux de façon inattendue au lieu de D. Dans ce cas, D doit être modélisée comme un type de service différent de A, B et C. Étant donné que les stratégies d’intégrité sont spécifiés par le type de service, les seuils de pourcentage anormal différent peuvent être appliqué toodifferent services.</span><span class="sxs-lookup"><span data-stu-id="daff1-171">However, it might result in unanticipated errors due tooC being unexpectedly unhealthy instead of D. In this situation, D should be modeled as a different service type from A, B, and C. Since health policies are specified per service type, different unhealthy percentage thresholds can be applied toodifferent services.</span></span> 

### <a name="i-did-not-specify-a-health-policy-for-application-upgrade-but-hello-upgrade-still-fails-for-some-time-outs-that-i-never-specified"></a><span data-ttu-id="daff1-172">Je ne spécifiait pas une stratégie de contrôle d’intégrité pour la mise à niveau de l’application, mais la mise à niveau hello échoue pour des délais d’expiration spécifiée jamais</span><span class="sxs-lookup"><span data-stu-id="daff1-172">I did not specify a health policy for application upgrade, but hello upgrade still fails for some time-outs that I never specified</span></span>
<span data-ttu-id="daff1-173">Lorsque les stratégies d’intégrité ne sont pas fournis de demande de mise à niveau toohello, elles sont tirées de hello *ApplicationManifest.xml* de la version actuelle de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="daff1-173">When health policies aren't provided toohello upgrade request, they are taken from hello *ApplicationManifest.xml* of hello current application version.</span></span> <span data-ttu-id="daff1-174">Par exemple, si vous mettez à niveau X de l’Application à partir de la version 1.0 tooversion 2.0, les stratégies de contrôle d’intégrité d’application spécifiés pour la version 1.0 sont utilisés.</span><span class="sxs-lookup"><span data-stu-id="daff1-174">For example, if you're upgrading Application X from version 1.0 tooversion 2.0, application health policies specified for in version 1.0 are used.</span></span> <span data-ttu-id="daff1-175">Si une autre stratégie d’intégrité doit être utilisée pour la mise à niveau hello, stratégie de hello doit toobe spécifié dans le cadre de l’appel d’API hello application mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="daff1-175">If a different health policy should be used for hello upgrade, then hello policy needs toobe specified as part of hello application upgrade API call.</span></span> <span data-ttu-id="daff1-176">Hello stratégies spécifiées dans le cadre de l’appel d’API de hello s’appliquent uniquement au cours de la mise à niveau hello.</span><span class="sxs-lookup"><span data-stu-id="daff1-176">hello policies specified as part of hello API call only apply during hello upgrade.</span></span> <span data-ttu-id="daff1-177">Une fois la mise à niveau hello est terminée, les stratégies de hello spécifiées Bonjour *ApplicationManifest.xml* sont utilisés.</span><span class="sxs-lookup"><span data-stu-id="daff1-177">Once hello upgrade is complete, hello policies specified in hello *ApplicationManifest.xml* are used.</span></span>

### <a name="incorrect-time-outs-are-specified"></a><span data-ttu-id="daff1-178">Délais d’attente incorrects spécifiés</span><span class="sxs-lookup"><span data-stu-id="daff1-178">Incorrect time-outs are specified</span></span>
<span data-ttu-id="daff1-179">Vous vous demandez peut-être ce qui se passe lorsque les délais d’expiration sont définis de façon incohérente.</span><span class="sxs-lookup"><span data-stu-id="daff1-179">You may have wondered about what happens when time-outs are set inconsistently.</span></span> <span data-ttu-id="daff1-180">Par exemple, vous pouvez avoir un *UpgradeTimeout* qui est inférieur à hello *UpgradeDomainTimeout*.</span><span class="sxs-lookup"><span data-stu-id="daff1-180">For example, you may have an *UpgradeTimeout* that's less than hello *UpgradeDomainTimeout*.</span></span> <span data-ttu-id="daff1-181">les réponses Hello sont qu’une erreur est retournée.</span><span class="sxs-lookup"><span data-stu-id="daff1-181">hello answer is that an error is returned.</span></span> <span data-ttu-id="daff1-182">Les erreurs sont retournées si hello *UpgradeDomainTimeout* est inférieure à la somme de hello de *HealthCheckWaitDuration* et *HealthCheckRetryTimeout*, ou si  *UpgradeDomainTimeout* est inférieure à la somme de hello de *HealthCheckWaitDuration* et *HealthCheckStableDuration*.</span><span class="sxs-lookup"><span data-stu-id="daff1-182">Errors are returned if hello *UpgradeDomainTimeout* is less than hello sum of *HealthCheckWaitDuration* and *HealthCheckRetryTimeout*, or if *UpgradeDomainTimeout* is less than hello sum of *HealthCheckWaitDuration* and *HealthCheckStableDuration*.</span></span>

### <a name="my-upgrades-are-taking-too-long"></a><span data-ttu-id="daff1-183">Mes mises à niveau prennent trop de temps</span><span class="sxs-lookup"><span data-stu-id="daff1-183">My upgrades are taking too long</span></span>
<span data-ttu-id="daff1-184">temps de Hello pour une mise à niveau toocomplete dépend de vérifications d’intégrité de hello et délais d’expiration spécifiés.</span><span class="sxs-lookup"><span data-stu-id="daff1-184">hello time for an upgrade toocomplete depends on hello health checks and time-outs specified.</span></span> <span data-ttu-id="daff1-185">Contrôles d’intégrité et les délais d’expiration dépendent de la durée toocopy, déploiement et stabilisent application hello.</span><span class="sxs-lookup"><span data-stu-id="daff1-185">Health checks and time-outs depend on how long it takes toocopy, deploy, and stabilize hello application.</span></span> <span data-ttu-id="daff1-186">Se montrer trop sévère avec les délais d’attente peut induire plus d’échecs de mises à niveau ; nous vous recommandons donc de démarrer prudemment avec des délais d’attente plus longs.</span><span class="sxs-lookup"><span data-stu-id="daff1-186">Being too aggressive with time-outs might mean more failed upgrades, so we recommend starting conservatively with longer time-outs.</span></span>

<span data-ttu-id="daff1-187">Voici un rappel rapide sur l’interagissent des délais d’expiration hello tentatives de mise à niveau hello :</span><span class="sxs-lookup"><span data-stu-id="daff1-187">Here's a quick refresher on how hello time-outs interact with hello upgrade times:</span></span>

<span data-ttu-id="daff1-188">Les mises à niveau pour un domaine de mise à niveau ne peuvent pas prendre moins de temps que *HealthCheckWaitDuration* + *HealthCheckStableDuration*.</span><span class="sxs-lookup"><span data-stu-id="daff1-188">Upgrades for an upgrade domain cannot complete faster than *HealthCheckWaitDuration* + *HealthCheckStableDuration*.</span></span>

<span data-ttu-id="daff1-189">Un échec de mise à niveau ne peut pas se produire avant *HealthCheckWaitDuration* + *HealthCheckRetryTimeout*.</span><span class="sxs-lookup"><span data-stu-id="daff1-189">Upgrade failure cannot occur faster than *HealthCheckWaitDuration* + *HealthCheckRetryTimeout*.</span></span>

<span data-ttu-id="daff1-190">temps de mise à niveau pour un domaine de mise à niveau Hello est limitée par *UpgradeDomainTimeout*.</span><span class="sxs-lookup"><span data-stu-id="daff1-190">hello upgrade time for an upgrade domain is limited by *UpgradeDomainTimeout*.</span></span>  <span data-ttu-id="daff1-191">Si *HealthCheckRetryTimeout* et *HealthCheckStableDuration* sont différente de zéro et la santé de l’application hello hello conserve va-et-vient, puis mise à niveau hello finalement arrive à expiration sur  *UpgradeDomainTimeout*.</span><span class="sxs-lookup"><span data-stu-id="daff1-191">If *HealthCheckRetryTimeout* and *HealthCheckStableDuration* are both non-zero and hello health of hello application keeps switching back and forth, then hello upgrade eventually times out on *UpgradeDomainTimeout*.</span></span> <span data-ttu-id="daff1-192">*UpgradeDomainTimeout* démarre une fois le comptage vers le bas hello mise à niveau pour le domaine de mise à niveau actuel hello commence.</span><span class="sxs-lookup"><span data-stu-id="daff1-192">*UpgradeDomainTimeout* starts counting down once hello upgrade for hello current upgrade domain begins.</span></span>

## <a name="next-steps"></a><span data-ttu-id="daff1-193">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="daff1-193">Next steps</span></span>
<span data-ttu-id="daff1-194">[mise à niveau de votre application à l’aide de Visual Studio](service-fabric-application-upgrade-tutorial.md) vous guide à travers une mise à niveau de l’application à l’aide de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="daff1-194">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>

<span data-ttu-id="daff1-195">[mise à niveau de votre application à l’aide de PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) vous guide à travers une mise à niveau de l’application à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="daff1-195">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>

<span data-ttu-id="daff1-196">Contrôlez les mises à niveau de votre application à l'aide des [Paramètres de mise à niveau](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="daff1-196">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>

<span data-ttu-id="daff1-197">Rendre les mises à niveau de votre application compatible par learning comment toouse [sérialisation des données](service-fabric-application-upgrade-data-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="daff1-197">Make your application upgrades compatible by learning how toouse [Data Serialization](service-fabric-application-upgrade-data-serialization.md).</span></span>

<span data-ttu-id="daff1-198">Découvrez comment toouse des fonctionnalités avancées lors de la mise à niveau de votre application en vous reportant trop[rubriques avancées](service-fabric-application-upgrade-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="daff1-198">Learn how toouse advanced functionality while upgrading your application by referring too[Advanced Topics](service-fabric-application-upgrade-advanced.md).</span></span>
