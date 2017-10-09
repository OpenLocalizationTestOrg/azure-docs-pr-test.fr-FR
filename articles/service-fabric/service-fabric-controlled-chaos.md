---
title: clusters de Chaos dans Service Fabric aaaInduce | Documents Microsoft
description: "À l’aide d’injection d’erreurs et les API de Service de Cluster Analysis toomanage Chaos dans un cluster de hello."
services: service-fabric
documentationcenter: .net
author: motanv
manager: anmola
editor: motanv
ms.assetid: 2bd13443-3478-4382-9a5a-1f6c6b32bfc9
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: motanv
ms.openlocfilehash: 7e87cae22645fc4ba52e258471d8f3a4ffdb1cce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="induce-controlled-chaos-in-service-fabric-clusters"></a><span data-ttu-id="af85e-103">Induire un chaos contrôlé dans les clusters Service Fabric</span><span class="sxs-lookup"><span data-stu-id="af85e-103">Induce controlled Chaos in Service Fabric clusters</span></span>
<span data-ttu-id="af85e-104">Les systèmes distribués à grande échelle, comme les infrastructures cloud, sont par définition peu fiables.</span><span class="sxs-lookup"><span data-stu-id="af85e-104">Large-scale distributed systems like cloud infrastructures are inherently unreliable.</span></span> <span data-ttu-id="af85e-105">Azure Service Fabric permet aux développeurs toowrite distribuée des services fiables sur une infrastructure fiable.</span><span class="sxs-lookup"><span data-stu-id="af85e-105">Azure Service Fabric enables developers toowrite reliable distributed services on top of an unreliable infrastructure.</span></span> <span data-ttu-id="af85e-106">toowrite des services distribués fiables sur une infrastructure fiable, les développeurs doivent stabilité de hello toobe tootest en mesure de leurs services pendant hello sous-jacent infrastructure non fiable par le biais de transitions d’état compliquée toofaults échéance.</span><span class="sxs-lookup"><span data-stu-id="af85e-106">toowrite robust distributed services on top of an unreliable infrastructure, developers need toobe able tootest hello stability of their services while hello underlying unreliable infrastructure is going through complicated state transitions due toofaults.</span></span>

<span data-ttu-id="af85e-107">Hello [injection d’erreurs et le Service de Cluster Analysis](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-testability-overview) (également appelé Service d’analyse de panne hello) permet aux développeurs hello tooinduce erreurs tootest leurs services.</span><span class="sxs-lookup"><span data-stu-id="af85e-107">hello [Fault Injection and Cluster Analysis Service](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-testability-overview) (also known as hello Fault Analysis Service) gives developers hello ability tooinduce faults tootest their services.</span></span> <span data-ttu-id="af85e-108">Ces ciblés simulée des erreurs, comme [le redémarrage d’une partition](https://docs.microsoft.com/en-us/powershell/module/servicefabric/start-servicefabricpartitionrestart?view=azureservicefabricps), peuvent aider à tester les transitions d’état courantes hello.</span><span class="sxs-lookup"><span data-stu-id="af85e-108">These targeted simulated faults, like [restarting a partition](https://docs.microsoft.com/en-us/powershell/module/servicefabric/start-servicefabricpartitionrestart?view=azureservicefabricps), can help exercise hello most common state transitions.</span></span> <span data-ttu-id="af85e-109">Toutefois, les erreurs simulées ciblées sont biaisées par définition, et peuvent donc manquer des bogues qui se présentent uniquement dans une séquence longue, compliquée et difficile à prédire de transitions d’état.</span><span class="sxs-lookup"><span data-stu-id="af85e-109">However targeted simulated faults are biased by definition and thus may miss bugs that show up only in hard-to-predict, long and complicated sequence of state transitions.</span></span> <span data-ttu-id="af85e-110">Pour un test non biaisé, vous pouvez utiliser Chaos.</span><span class="sxs-lookup"><span data-stu-id="af85e-110">For an unbiased testing, you can use Chaos.</span></span>

<span data-ttu-id="af85e-111">Chaos simule les erreurs périodiques, entrelacés (progressif et anormal) dans l’ensemble de cluster de hello sur de longues périodes.</span><span class="sxs-lookup"><span data-stu-id="af85e-111">Chaos simulates periodic, interleaved faults (both graceful and ungraceful) throughout hello cluster over extended periods of time.</span></span> <span data-ttu-id="af85e-112">Une fois que vous avez configuré le Chaos taux de hello et de type hello d’erreurs, vous pouvez démarrer Chaos via c# ou Powershell API toostart génération des erreurs dans le cluster de hello et vos services.</span><span class="sxs-lookup"><span data-stu-id="af85e-112">Once you have configured Chaos with hello rate and hello kind of faults, you can start Chaos through C# or Powershell API toostart generating faults in hello cluster and in your services.</span></span> <span data-ttu-id="af85e-113">Vous pouvez configurer Chaos toorun pour une période de temps (par exemple, pour une heure), après laquelle Chaos s’arrête automatiquement, ou vous pouvez appeler des API StopChaos (c# ou Powershell) toostop à tout moment.</span><span class="sxs-lookup"><span data-stu-id="af85e-113">You can configure Chaos toorun for a specified time period (for example, for one hour), after which Chaos stops automatically, or you can call StopChaos API (C# or Powershell) toostop it at any time.</span></span>

> [!NOTE]
> <span data-ttu-id="af85e-114">Dans sa forme actuelle, Chaos induit erreurs uniquement sans échec, ce qui implique qu’en absence de hello d’erreurs externes une perte de quorum, ou une perte de données ne se produit jamais.</span><span class="sxs-lookup"><span data-stu-id="af85e-114">In its current form, Chaos induces only safe faults, which implies that in hello absence of external faults a quorum loss, or data loss never occurs.</span></span>
>

<span data-ttu-id="af85e-115">Pendant l’exécution de Chaos, il génère des événements qui capturent l’état hello Hello exécuter moment hello.</span><span class="sxs-lookup"><span data-stu-id="af85e-115">While Chaos is running, it produces different events that capture hello state of hello run at hello moment.</span></span> <span data-ttu-id="af85e-116">Par exemple, un ExecutingFaultsEvent contient toutes les erreurs de hello que Chaos a décidé tooexecute dans cette itération.</span><span class="sxs-lookup"><span data-stu-id="af85e-116">For example, an ExecutingFaultsEvent contains all hello faults that Chaos has decided tooexecute in that iteration.</span></span> <span data-ttu-id="af85e-117">Un ValidationFailedEvent contient les détails de hello d’un échec de validation (problèmes d’intégrité ou de stabilité) qui a été trouvé lors de la validation de cluster de hello hello.</span><span class="sxs-lookup"><span data-stu-id="af85e-117">A ValidationFailedEvent contains hello details of a validation failure (health or stability issues) that was found during hello validation of hello cluster.</span></span> <span data-ttu-id="af85e-118">Vous pouvez appeler hello GetChaosReport API (c# ou Powershell) tooget hello rapport sur les séries de Chaos.</span><span class="sxs-lookup"><span data-stu-id="af85e-118">You can invoke hello GetChaosReport API (C# or Powershell) tooget hello report of Chaos runs.</span></span> <span data-ttu-id="af85e-119">Ces événements sont rendus persistants dans un [dictionnaire fiable](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-reliable-collections), qui a une stratégie de troncation dictée par deux configurations : **MaxStoredChaosEventCount** (la valeur par défaut est 25 000) et **StoredActionCleanupIntervalInSeconds** (la valeur par défaut est 3 600).</span><span class="sxs-lookup"><span data-stu-id="af85e-119">These events get persisted in a [reliable dictionary](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-reliable-collections), which has a truncation policy dictated by two configurations: **MaxStoredChaosEventCount** (default value is 25000) and **StoredActionCleanupIntervalInSeconds** (default value is 3600).</span></span> <span data-ttu-id="af85e-120">Chaque *StoredActionCleanupIntervalInSeconds* les vérifications de Chaos et tous les mais hello plus récente *MaxStoredChaosEventCount* , les événements sont purgés de dictionnaire fiable de hello.</span><span class="sxs-lookup"><span data-stu-id="af85e-120">Every *StoredActionCleanupIntervalInSeconds* Chaos checks and all but hello most recent *MaxStoredChaosEventCount* events, are purged from hello reliable dictionary.</span></span>

## <a name="faults-induced-in-chaos"></a><span data-ttu-id="af85e-121">Erreurs introduites dans le chaos</span><span class="sxs-lookup"><span data-stu-id="af85e-121">Faults induced in Chaos</span></span>
<span data-ttu-id="af85e-122">Chaos génère des erreurs sur l’intégralité du cluster Service Fabric hello et compresse les erreurs qui sont visibles dans les mois ou années en quelques heures.</span><span class="sxs-lookup"><span data-stu-id="af85e-122">Chaos generates faults across hello entire Service Fabric cluster and compresses faults that are seen in months or years into a few hours.</span></span> <span data-ttu-id="af85e-123">combinaison Hello d’erreurs entrelacées avec un taux d’erreur élevé hello recherche les cas qui peuvent manquer dans le cas contraire.</span><span class="sxs-lookup"><span data-stu-id="af85e-123">hello combination of interleaved faults with hello high fault rate finds corner cases that may otherwise be missed.</span></span> <span data-ttu-id="af85e-124">Cet exercice de Chaos entraîne une amélioration significative de tooa dans la qualité du code hello du service de hello.</span><span class="sxs-lookup"><span data-stu-id="af85e-124">This exercise of Chaos leads tooa significant improvement in hello code quality of hello service.</span></span>

<span data-ttu-id="af85e-125">Chaos déclenche des erreurs de hello suivant des catégories :</span><span class="sxs-lookup"><span data-stu-id="af85e-125">Chaos induces faults from hello following categories:</span></span>

* <span data-ttu-id="af85e-126">Redémarrer un nœud</span><span class="sxs-lookup"><span data-stu-id="af85e-126">Restart a node</span></span>
* <span data-ttu-id="af85e-127">Redémarrer un package de code déployé</span><span class="sxs-lookup"><span data-stu-id="af85e-127">Restart a deployed code package</span></span>
* <span data-ttu-id="af85e-128">Supprimer un réplica</span><span class="sxs-lookup"><span data-stu-id="af85e-128">Remove a replica</span></span>
* <span data-ttu-id="af85e-129">Redémarrer un réplica</span><span class="sxs-lookup"><span data-stu-id="af85e-129">Restart a replica</span></span>
* <span data-ttu-id="af85e-130">Déplacer un réplica principal (configurable)</span><span class="sxs-lookup"><span data-stu-id="af85e-130">Move a primary replica (configurable)</span></span>
* <span data-ttu-id="af85e-131">Déplacer un réplica secondaire (configurable)</span><span class="sxs-lookup"><span data-stu-id="af85e-131">Move a secondary replica (configurable)</span></span>

<span data-ttu-id="af85e-132">Le chaos s’exécute dans de nombreuses itérations.</span><span class="sxs-lookup"><span data-stu-id="af85e-132">Chaos runs in multiple iterations.</span></span> <span data-ttu-id="af85e-133">Chaque itération se compose des erreurs et la validation du cluster pour hello spécifié période.</span><span class="sxs-lookup"><span data-stu-id="af85e-133">Each iteration consists of faults and cluster validation for hello specified period.</span></span> <span data-ttu-id="af85e-134">Vous pouvez configurer hello temps pour hello cluster toostabilize et toosucceed de validation.</span><span class="sxs-lookup"><span data-stu-id="af85e-134">You can configure hello time spent for hello cluster toostabilize and for validation toosucceed.</span></span> <span data-ttu-id="af85e-135">Si une défaillance se trouve dans la validation du cluster, Chaos génère et persiste une ValidationFailedEvent avec hello UTC timestamp et les détails de l’échec hello.</span><span class="sxs-lookup"><span data-stu-id="af85e-135">If a failure is found in cluster validation, Chaos generates and persists a ValidationFailedEvent with hello UTC timestamp and hello failure details.</span></span> <span data-ttu-id="af85e-136">Par exemple, considérez une instance de Chaos définie toorun pour une heure avec un maximum de trois défaillances simultanées.</span><span class="sxs-lookup"><span data-stu-id="af85e-136">For example, consider an instance of Chaos that is set toorun for an hour with a maximum of three concurrent faults.</span></span> <span data-ttu-id="af85e-137">Chaos induit trois erreurs, puis valide l’intégrité du cluster hello.</span><span class="sxs-lookup"><span data-stu-id="af85e-137">Chaos induces three faults, and then validates hello cluster health.</span></span> <span data-ttu-id="af85e-138">Il itère au sein hello précédente passe de l’étape jusqu'à ce qu’il soit explicitement arrêté via hello StopChaosAsync API ou une heure.</span><span class="sxs-lookup"><span data-stu-id="af85e-138">It iterates through hello previous step until it is explicitly stopped through hello StopChaosAsync API or one-hour passes.</span></span> <span data-ttu-id="af85e-139">Si le cluster de hello devient non intègre dans les itérations (autrement dit, il ne pas stabiliser dans hello MaxClusterStabilizationTimeout passé dans), Chaos génère un ValidationFailedEvent.</span><span class="sxs-lookup"><span data-stu-id="af85e-139">If hello cluster becomes unhealthy in any iteration (that is, it does not stabilize within hello passed-in MaxClusterStabilizationTimeout), Chaos generates a ValidationFailedEvent.</span></span> <span data-ttu-id="af85e-140">Cet événement indique qu’une erreur est survenue et qu’un examen approfondi est peut-être nécessaire.</span><span class="sxs-lookup"><span data-stu-id="af85e-140">This event indicates that something has gone wrong and might need further investigation.</span></span>

<span data-ttu-id="af85e-141">tooget qui Chaos induites par des erreurs, vous pouvez utiliser les API GetChaosReport (powershell ou c#).</span><span class="sxs-lookup"><span data-stu-id="af85e-141">tooget which faults Chaos induced, you can use GetChaosReport API (powershell or C#).</span></span> <span data-ttu-id="af85e-142">Hello API Obtient le segment suivant de hello du rapport de Chaos hello en fonction de jeton de continuation transmis hello ou hello passé dans intervalle de temps.</span><span class="sxs-lookup"><span data-stu-id="af85e-142">hello API gets hello next segment of hello Chaos report based on hello passed-in continuation token or hello passed-in time-range.</span></span> <span data-ttu-id="af85e-143">Vous pouvez spécifier hello segment suivant hello tooget ContinuationToken du rapport de Chaos hello ou vous pouvez spécifier la plage de temps hello via StartTimeUtc et EndTimeUtc, mais vous ne pouvez pas spécifier hello ContinuationToken et intervalle de temps hello Bonjour même appel.</span><span class="sxs-lookup"><span data-stu-id="af85e-143">You can either specify hello ContinuationToken tooget hello next segment of hello Chaos report or you can specify hello time-range through StartTimeUtc and EndTimeUtc, but you cannot specify both hello ContinuationToken and hello time-range in hello same call.</span></span> <span data-ttu-id="af85e-144">Lorsqu’il y a plus de 100 événements Chaos, hello rapport de Chaos est retourné dans les segments où un segment contient des événements Chaos pas plus de 100.</span><span class="sxs-lookup"><span data-stu-id="af85e-144">When there are more than 100 Chaos events, hello Chaos report is returned in segments where a segment contains no more than 100 Chaos events.</span></span>

## <a name="important-configuration-options"></a><span data-ttu-id="af85e-145">Options de configuration importantes</span><span class="sxs-lookup"><span data-stu-id="af85e-145">Important configuration options</span></span>
* <span data-ttu-id="af85e-146">**TimeToRun** : durée totale d’exécution du chaos jusqu’à sa fin.</span><span class="sxs-lookup"><span data-stu-id="af85e-146">**TimeToRun**: Total time that Chaos runs before it finishes with success.</span></span> <span data-ttu-id="af85e-147">Vous pouvez arrêter le Chaos préalablement à l’exécution pour la période de TimeToRun hello via hello StopChaos API.</span><span class="sxs-lookup"><span data-stu-id="af85e-147">You can stop Chaos before it has run for hello TimeToRun period through hello StopChaos API.</span></span>

* <span data-ttu-id="af85e-148">**MaxClusterStabilizationTimeout**: durée maximale hello toowait de temps pour toobecome de cluster hello sain avant de produire un ValidationFailedEvent.</span><span class="sxs-lookup"><span data-stu-id="af85e-148">**MaxClusterStabilizationTimeout**: hello maximum amount of time toowait for hello cluster toobecome healthy before producing a ValidationFailedEvent.</span></span> <span data-ttu-id="af85e-149">Ce délai est de charge de hello tooreduce sur le cluster de hello lors de la récupérer.</span><span class="sxs-lookup"><span data-stu-id="af85e-149">This wait is tooreduce hello load on hello cluster while it is recovering.</span></span> <span data-ttu-id="af85e-150">vérifications de Hello sont :</span><span class="sxs-lookup"><span data-stu-id="af85e-150">hello checks performed are:</span></span>
  * <span data-ttu-id="af85e-151">Si l’intégrité du cluster hello est OK</span><span class="sxs-lookup"><span data-stu-id="af85e-151">If hello cluster health is OK</span></span>
  * <span data-ttu-id="af85e-152">Si l’intégrité du service hello est OK</span><span class="sxs-lookup"><span data-stu-id="af85e-152">If hello service health is OK</span></span>
  * <span data-ttu-id="af85e-153">Si la taille du jeu de réplicas de cible de hello est obtenue de la partition de service hello</span><span class="sxs-lookup"><span data-stu-id="af85e-153">If hello target replica set size is achieved for hello service partition</span></span>
  * <span data-ttu-id="af85e-154">Aucun réplica InBuild n’existe</span><span class="sxs-lookup"><span data-stu-id="af85e-154">That no InBuild replicas exist</span></span>
* <span data-ttu-id="af85e-155">**MaxConcurrentFaults**: hello nombre maximal d’erreurs simultanées induites dans chaque itération.</span><span class="sxs-lookup"><span data-stu-id="af85e-155">**MaxConcurrentFaults**: hello maximum number of concurrent faults that are induced in each iteration.</span></span> <span data-ttu-id="af85e-156">valeur supérieure hello Hello, hello plus agressive Chaos est et hello basculements et hello état transition combinaisons hello cluster traverse sont également plus complexes.</span><span class="sxs-lookup"><span data-stu-id="af85e-156">hello higher hello number, hello more aggressive Chaos is and hello failovers and hello state transition combinations that hello cluster goes through are also more complex.</span></span> 

> [!NOTE]
> <span data-ttu-id="af85e-157">Quel que soit une valeur élevée comment *MaxConcurrentFaults* a, Chaos garantit - en absence de hello d’erreurs externes - aucune perte de quorum ou une perte de données.</span><span class="sxs-lookup"><span data-stu-id="af85e-157">Regardless how high a value *MaxConcurrentFaults* has, Chaos guarantees - in hello absence of external faults - there is no quorum loss or data loss.</span></span>
>

* <span data-ttu-id="af85e-158">**EnableMoveReplicaFaults**: Active ou désactive les défauts de hello qui entraînent des toomove de réplicas principaux ou secondaires hello.</span><span class="sxs-lookup"><span data-stu-id="af85e-158">**EnableMoveReplicaFaults**: Enables or disables hello faults that cause hello primary or secondary replicas toomove.</span></span> <span data-ttu-id="af85e-159">Ces erreurs sont désactivées par défaut.</span><span class="sxs-lookup"><span data-stu-id="af85e-159">These faults are disabled by default.</span></span>
* <span data-ttu-id="af85e-160">**WaitTimeBetweenIterations**: durée hello toowait de temps entre les itérations.</span><span class="sxs-lookup"><span data-stu-id="af85e-160">**WaitTimeBetweenIterations**: hello amount of time toowait between iterations.</span></span> <span data-ttu-id="af85e-161">Autrement dit, hello temps que chaos suspend après avoir exécuté un arrondi des défaillances et avoir terminé la validation correspondante hello d’intégrité hello du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="af85e-161">That is, hello amount of time Chaos will pause after having executed a round of faults and having finished hello corresponding validation of hello health of hello cluster.</span></span> <span data-ttu-id="af85e-162">Hello plus la valeur hello, hello inférieur est le taux d’injection de code hello erreur moyenne.</span><span class="sxs-lookup"><span data-stu-id="af85e-162">hello higher hello value, hello lower is hello average fault injection rate.</span></span>
* <span data-ttu-id="af85e-163">**WaitTimeBetweenFaults**: durée hello toowait de temps entre deux erreurs consécutives dans une seule itération.</span><span class="sxs-lookup"><span data-stu-id="af85e-163">**WaitTimeBetweenFaults**: hello amount of time toowait between two consecutive faults in a single iteration.</span></span> <span data-ttu-id="af85e-164">Hello plus la valeur hello, hello inférieur concurrence hello de (ou hello chevauchement) erreurs.</span><span class="sxs-lookup"><span data-stu-id="af85e-164">hello higher hello value, hello lower hello concurrency of (or hello overlap between) faults.</span></span>
* <span data-ttu-id="af85e-165">**ClusterHealthPolicy**: stratégie de contrôle d’intégrité du Cluster est utilisé toovalidate hello intégrité cluster hello entre les itérations de Chaos.</span><span class="sxs-lookup"><span data-stu-id="af85e-165">**ClusterHealthPolicy**: Cluster health policy is used toovalidate hello health of hello cluster in between Chaos iterations.</span></span> <span data-ttu-id="af85e-166">Si l’intégrité du cluster hello est erroné ou si une exception inattendue se produit pendant l’exécution de pannes, Chaos attendra 30 minutes avant de hello suivant de contrôle d’intégrité - cluster de hello tooprovide avec certaines toorecuperate de temps.</span><span class="sxs-lookup"><span data-stu-id="af85e-166">If hello cluster health is in error or if an unexpected exception happens during fault execution, Chaos will wait for 30 minutes before hello next health-check - tooprovide hello cluster with some time toorecuperate.</span></span>
* <span data-ttu-id="af85e-167">**Contexte** : une collection de paires clé-valeur de type (string, string).</span><span class="sxs-lookup"><span data-stu-id="af85e-167">**Context**: A collection of (string, string) type key-value pairs.</span></span> <span data-ttu-id="af85e-168">mappage de Hello peut être utilisé toorecord informations hello Chaos exécuter.</span><span class="sxs-lookup"><span data-stu-id="af85e-168">hello map can be used toorecord information about hello Chaos run.</span></span> <span data-ttu-id="af85e-169">Il ne peut pas y avoir plus de 100 de ces paires et chaque chaîne (clé ou valeur) peut comporter au maximum 4095 caractères.</span><span class="sxs-lookup"><span data-stu-id="af85e-169">There cannot be more than 100 such pairs and each string (key or value) can be at most 4095 characters long.</span></span> <span data-ttu-id="af85e-170">Ce mappage est défini par starter hello du contexte de hello hello Chaos exécuter toooptionally magasin sur hello spécifique s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="af85e-170">This map is set by hello starter of hello Chaos run toooptionally store hello context about hello specific run.</span></span>

## <a name="how-toorun-chaos"></a><span data-ttu-id="af85e-171">Comment toorun Chaos</span><span class="sxs-lookup"><span data-stu-id="af85e-171">How toorun Chaos</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Threading.Tasks;
using System.Fabric;

using System.Diagnostics;
using System.Fabric.Chaos.DataStructures;

class Program
{
    private class ChaosEventComparer : IEqualityComparer<ChaosEvent>
    {
        public bool Equals(ChaosEvent x, ChaosEvent y)
        {
            return x.TimeStampUtc.Equals(y.TimeStampUtc);
        }

        public int GetHashCode(ChaosEvent obj)
        {
            return obj.TimeStampUtc.GetHashCode();
        }
    }

    static void Main(string[] args)
    {
        var clusterConnectionString = "localhost:19000";
        using (var client = new FabricClient(clusterConnectionString))
        {
            var startTimeUtc = DateTime.UtcNow;
            var stabilizationTimeout = TimeSpan.FromSeconds(30.0);
            var timeToRun = TimeSpan.FromMinutes(60.0);
            var maxConcurrentFaults = 3;

            var parameters = new ChaosParameters(
                stabilizationTimeout,
                maxConcurrentFaults,
                true, /* EnableMoveReplicaFault */
                timeToRun);

            try
            {
                client.TestManager.StartChaosAsync(parameters).GetAwaiter().GetResult();
            }
            catch (FabricChaosAlreadyRunningException)
            {
                Console.WriteLine("An instance of Chaos is already running in hello cluster.");
            }

            var filter = new ChaosReportFilter(startTimeUtc, DateTime.MaxValue);

            var eventSet = new HashSet<ChaosEvent>(new ChaosEventComparer());

            while (true)
            {
                var report = client.TestManager.GetChaosReportAsync(filter).GetAwaiter().GetResult();

                foreach (var chaosEvent in report.History)
                {
                    if (eventSet.Add(chaosEvent))
                    {
                        Console.WriteLine(chaosEvent);
                    }
                }

                // When Chaos stops, a StoppedEvent is created.
                // If a StoppedEvent is found, exit hello loop.
                var lastEvent = report.History.LastOrDefault();

                if (lastEvent is StoppedEvent)
                {
                    break;
                }

                Task.Delay(TimeSpan.FromSeconds(1.0)).GetAwaiter().GetResult();
            }
        }
    }
}
```

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

$events = @{}
$now = [System.DateTime]::UtcNow

Start-ServiceFabricChaos -TimeToRunMinute $timeToRun -MaxConcurrentFaults $concurrentFaults -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec

while($true)
{
    $stopped = $false
    $report = Get-ServiceFabricChaosReport -StartTimeUtc $now -EndTimeUtc ([System.DateTime]::MaxValue)

    foreach ($e in $report.History) {

        if(-Not ($events.Contains($e.TimeStampUtc.Ticks)))
        {
            $events.Add($e.TimeStampUtc.Ticks, $e)
            if($e -is [System.Fabric.Chaos.DataStructures.ValidationFailedEvent])
            {
                Write-Host -BackgroundColor White -ForegroundColor Red $e
            }
            else
            {
                if($e -is [System.Fabric.Chaos.DataStructures.StoppedEvent])
                {
                    $stopped = $true
                }

                Write-Host $e
            }
        }
    }

    if($stopped -eq $true)
    {
        break
    }

    Start-Sleep -Seconds 1
}

Stop-ServiceFabricChaos
```
