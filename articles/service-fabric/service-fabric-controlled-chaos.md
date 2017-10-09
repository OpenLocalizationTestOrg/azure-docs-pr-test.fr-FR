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
# <a name="induce-controlled-chaos-in-service-fabric-clusters"></a>Induire un chaos contrôlé dans les clusters Service Fabric
Les systèmes distribués à grande échelle, comme les infrastructures cloud, sont par définition peu fiables. Azure Service Fabric permet aux développeurs toowrite distribuée des services fiables sur une infrastructure fiable. toowrite des services distribués fiables sur une infrastructure fiable, les développeurs doivent stabilité de hello toobe tootest en mesure de leurs services pendant hello sous-jacent infrastructure non fiable par le biais de transitions d’état compliquée toofaults échéance.

Hello [injection d’erreurs et le Service de Cluster Analysis](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-testability-overview) (également appelé Service d’analyse de panne hello) permet aux développeurs hello tooinduce erreurs tootest leurs services. Ces ciblés simulée des erreurs, comme [le redémarrage d’une partition](https://docs.microsoft.com/en-us/powershell/module/servicefabric/start-servicefabricpartitionrestart?view=azureservicefabricps), peuvent aider à tester les transitions d’état courantes hello. Toutefois, les erreurs simulées ciblées sont biaisées par définition, et peuvent donc manquer des bogues qui se présentent uniquement dans une séquence longue, compliquée et difficile à prédire de transitions d’état. Pour un test non biaisé, vous pouvez utiliser Chaos.

Chaos simule les erreurs périodiques, entrelacés (progressif et anormal) dans l’ensemble de cluster de hello sur de longues périodes. Une fois que vous avez configuré le Chaos taux de hello et de type hello d’erreurs, vous pouvez démarrer Chaos via c# ou Powershell API toostart génération des erreurs dans le cluster de hello et vos services. Vous pouvez configurer Chaos toorun pour une période de temps (par exemple, pour une heure), après laquelle Chaos s’arrête automatiquement, ou vous pouvez appeler des API StopChaos (c# ou Powershell) toostop à tout moment.

> [!NOTE]
> Dans sa forme actuelle, Chaos induit erreurs uniquement sans échec, ce qui implique qu’en absence de hello d’erreurs externes une perte de quorum, ou une perte de données ne se produit jamais.
>

Pendant l’exécution de Chaos, il génère des événements qui capturent l’état hello Hello exécuter moment hello. Par exemple, un ExecutingFaultsEvent contient toutes les erreurs de hello que Chaos a décidé tooexecute dans cette itération. Un ValidationFailedEvent contient les détails de hello d’un échec de validation (problèmes d’intégrité ou de stabilité) qui a été trouvé lors de la validation de cluster de hello hello. Vous pouvez appeler hello GetChaosReport API (c# ou Powershell) tooget hello rapport sur les séries de Chaos. Ces événements sont rendus persistants dans un [dictionnaire fiable](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-reliable-collections), qui a une stratégie de troncation dictée par deux configurations : **MaxStoredChaosEventCount** (la valeur par défaut est 25 000) et **StoredActionCleanupIntervalInSeconds** (la valeur par défaut est 3 600). Chaque *StoredActionCleanupIntervalInSeconds* les vérifications de Chaos et tous les mais hello plus récente *MaxStoredChaosEventCount* , les événements sont purgés de dictionnaire fiable de hello.

## <a name="faults-induced-in-chaos"></a>Erreurs introduites dans le chaos
Chaos génère des erreurs sur l’intégralité du cluster Service Fabric hello et compresse les erreurs qui sont visibles dans les mois ou années en quelques heures. combinaison Hello d’erreurs entrelacées avec un taux d’erreur élevé hello recherche les cas qui peuvent manquer dans le cas contraire. Cet exercice de Chaos entraîne une amélioration significative de tooa dans la qualité du code hello du service de hello.

Chaos déclenche des erreurs de hello suivant des catégories :

* Redémarrer un nœud
* Redémarrer un package de code déployé
* Supprimer un réplica
* Redémarrer un réplica
* Déplacer un réplica principal (configurable)
* Déplacer un réplica secondaire (configurable)

Le chaos s’exécute dans de nombreuses itérations. Chaque itération se compose des erreurs et la validation du cluster pour hello spécifié période. Vous pouvez configurer hello temps pour hello cluster toostabilize et toosucceed de validation. Si une défaillance se trouve dans la validation du cluster, Chaos génère et persiste une ValidationFailedEvent avec hello UTC timestamp et les détails de l’échec hello. Par exemple, considérez une instance de Chaos définie toorun pour une heure avec un maximum de trois défaillances simultanées. Chaos induit trois erreurs, puis valide l’intégrité du cluster hello. Il itère au sein hello précédente passe de l’étape jusqu'à ce qu’il soit explicitement arrêté via hello StopChaosAsync API ou une heure. Si le cluster de hello devient non intègre dans les itérations (autrement dit, il ne pas stabiliser dans hello MaxClusterStabilizationTimeout passé dans), Chaos génère un ValidationFailedEvent. Cet événement indique qu’une erreur est survenue et qu’un examen approfondi est peut-être nécessaire.

tooget qui Chaos induites par des erreurs, vous pouvez utiliser les API GetChaosReport (powershell ou c#). Hello API Obtient le segment suivant de hello du rapport de Chaos hello en fonction de jeton de continuation transmis hello ou hello passé dans intervalle de temps. Vous pouvez spécifier hello segment suivant hello tooget ContinuationToken du rapport de Chaos hello ou vous pouvez spécifier la plage de temps hello via StartTimeUtc et EndTimeUtc, mais vous ne pouvez pas spécifier hello ContinuationToken et intervalle de temps hello Bonjour même appel. Lorsqu’il y a plus de 100 événements Chaos, hello rapport de Chaos est retourné dans les segments où un segment contient des événements Chaos pas plus de 100.

## <a name="important-configuration-options"></a>Options de configuration importantes
* **TimeToRun** : durée totale d’exécution du chaos jusqu’à sa fin. Vous pouvez arrêter le Chaos préalablement à l’exécution pour la période de TimeToRun hello via hello StopChaos API.

* **MaxClusterStabilizationTimeout**: durée maximale hello toowait de temps pour toobecome de cluster hello sain avant de produire un ValidationFailedEvent. Ce délai est de charge de hello tooreduce sur le cluster de hello lors de la récupérer. vérifications de Hello sont :
  * Si l’intégrité du cluster hello est OK
  * Si l’intégrité du service hello est OK
  * Si la taille du jeu de réplicas de cible de hello est obtenue de la partition de service hello
  * Aucun réplica InBuild n’existe
* **MaxConcurrentFaults**: hello nombre maximal d’erreurs simultanées induites dans chaque itération. valeur supérieure hello Hello, hello plus agressive Chaos est et hello basculements et hello état transition combinaisons hello cluster traverse sont également plus complexes. 

> [!NOTE]
> Quel que soit une valeur élevée comment *MaxConcurrentFaults* a, Chaos garantit - en absence de hello d’erreurs externes - aucune perte de quorum ou une perte de données.
>

* **EnableMoveReplicaFaults**: Active ou désactive les défauts de hello qui entraînent des toomove de réplicas principaux ou secondaires hello. Ces erreurs sont désactivées par défaut.
* **WaitTimeBetweenIterations**: durée hello toowait de temps entre les itérations. Autrement dit, hello temps que chaos suspend après avoir exécuté un arrondi des défaillances et avoir terminé la validation correspondante hello d’intégrité hello du cluster de hello. Hello plus la valeur hello, hello inférieur est le taux d’injection de code hello erreur moyenne.
* **WaitTimeBetweenFaults**: durée hello toowait de temps entre deux erreurs consécutives dans une seule itération. Hello plus la valeur hello, hello inférieur concurrence hello de (ou hello chevauchement) erreurs.
* **ClusterHealthPolicy**: stratégie de contrôle d’intégrité du Cluster est utilisé toovalidate hello intégrité cluster hello entre les itérations de Chaos. Si l’intégrité du cluster hello est erroné ou si une exception inattendue se produit pendant l’exécution de pannes, Chaos attendra 30 minutes avant de hello suivant de contrôle d’intégrité - cluster de hello tooprovide avec certaines toorecuperate de temps.
* **Contexte** : une collection de paires clé-valeur de type (string, string). mappage de Hello peut être utilisé toorecord informations hello Chaos exécuter. Il ne peut pas y avoir plus de 100 de ces paires et chaque chaîne (clé ou valeur) peut comporter au maximum 4095 caractères. Ce mappage est défini par starter hello du contexte de hello hello Chaos exécuter toooptionally magasin sur hello spécifique s’exécuter.

## <a name="how-toorun-chaos"></a>Comment toorun Chaos

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
