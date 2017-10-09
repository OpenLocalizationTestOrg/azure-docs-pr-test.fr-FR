---
title: aaaCreate chaos et basculement de tests pour Azure microservices | Documents Microsoft
description: "À l’aide de basculement et test de chaos hello Service Fabric erreurs tooinduce de scénarios de test et vérifier la fiabilité hello de vos services."
services: service-fabric
documentationcenter: .net
author: motanv
manager: rsinha
editor: toddabel
ms.assetid: 8eee7e89-404a-4605-8f00-7e4d4fb17553
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: motanv
ms.openlocfilehash: 1cac4f9e0e4a6c8416d5220d1537b5110decd1f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="testability-scenarios"></a>Scénarios de testabilité
Les grands systèmes distribués, comme les infrastructures cloud, sont par définition peu fiables. Azure Service Fabric permet aux développeurs hello capacité toowrite services toorun au-dessus des infrastructures non fiables. Dans l’ordre toowrite des services de qualité, les développeurs doivent tooinduce en mesure de toobe stabilité de hello tootest telle infrastructure non fiable de leurs services.

Hello erreur Analysis Service offre aux développeurs services tootest des actions de pannes hello capacité tooinduce en présence de hello d’échecs. Toutefois, les erreurs simulées ciblées présentent une efficacité limitée. hello tootake test en outre, vous pouvez utiliser des scénarios de test hello dans Service Fabric : un test chaos et un test de basculement. Ces scénarios de simulent continues erreurs entrelacées, normale et anormal, dans l’ensemble de cluster hello sur de longues périodes. Une fois qu’un test est configuré avec un taux de hello et du type d’erreurs, il peut être démarré par le biais des API c# ou PowerShell, toogenerate des erreurs dans le cluster de hello et votre service.

> [!WARNING]
> ChaosTestScenario est remplacé par un chaos plus robuste, basé sur le service. Reportez-vous toohello nouvel article [contrôlé le Chaos](service-fabric-controlled-chaos.md) pour plus d’informations.
> 
> 

## <a name="chaos-test"></a>Test chaos
scénario de chaos Hello génère des erreurs sur l’intégralité du cluster Service Fabric hello. scénario de Hello compresse les erreurs généralement visibles dans les mois ou années tooa quelques heures. combinaison Hello d’erreurs entrelacées avec un taux d’erreur élevé hello recherche les cas qui sont omis dans le cas contraire. Cela entraîne une amélioration importante tooa dans la qualité du code hello du service de hello.

### <a name="faults-simulated-in-hello-chaos-test"></a>Erreurs simulées dans le test de chaos hello
* Redémarrer un nœud
* Redémarrer un package de code déployé
* Supprimer un réplica
* Redémarrer un réplica
* Déplacer un réplica principal (principal)
* Déplacer un réplica secondaire (facultatif)

test de chaos Hello exécute plusieurs itérations d’erreurs et les validations de cluster pour hello spécifié laps de temps. Hello temps passé pour hello cluster toostabilize et toosucceed de validation est également configurable. scénario de Hello échoue lorsque vous atteignez une défaillance de la validation du cluster.

Par exemple, considérez qu'un test définie toorun pendant une heure avec un maximum de trois défaillances simultanées. test de Hello sera induire des erreurs de trois et puis de valider l’intégrité du cluster hello. test de Hello effectue une itération à l’étape précédente de hello jusqu'à ce que le cluster de hello devient non intègre ou passe d’une heure. Si le cluster de hello devient non intègre dans une itération, autrement dit, ne pas stabiliser pendant la durée configurée, test de hello échoue avec une exception. Cette exception indique qu’une erreur est survenue et qu’un examen approfondi est nécessaire.

Dans sa forme actuelle du moteur de génération de pannes hello dans le test de chaos hello induit erreurs uniquement sans échec. Cela signifie qu’en absence de hello d’erreurs externes, une quorum ou perte de données ne se produira.

### <a name="important-configuration-options"></a>Options de configuration importantes
* **TimeToRun**: durée totale de ce test hello exécutera avant de terminer avec succès. test de Hello peut terminer plus tôt à la place d’un échec de validation.
* **MaxClusterStabilizationTimeout**: quantité maximale de toowait de temps pour toobecome de cluster hello sain avant l’échec du test de hello. Hello vérifications effectuées sont si l’intégrité du cluster est OK, l’intégrité du service est OK, taille du jeu de réplica cible hello est obtenue de la partition de service hello et aucun réplicas InBuild n’existent.
* **MaxConcurrentFaults** : nombre maximal d’erreurs simultanées introduites dans chaque itération. Hello plus grand nombre de hello, hello plus agressive test hello, par conséquent, ce qui entraîne des basculements plus complexes et les combinaisons de transition. test de Hello garantit qu’en l’absence d’erreurs externes aucun ne sera une quorum ou perte de données, quel que soit la manière dont cette configuration est.
* **EnableMoveReplicaFaults**: Active ou désactive les erreurs hello qui sont à l’origine de déplacement hello Hello réplicas principaux ou secondaires. Ces erreurs sont désactivées par défaut.
* **WaitTimeBetweenIterations**: quantité de toowait de temps entre les itérations, par exemple, après un arrondi des défaillances et de validation correspondante.

### <a name="how-toorun-hello-chaos-test"></a>Comment tester les chaos de hello toorun
Exemple de code C#

```csharp
using System;
using System.Fabric;
using System.Fabric.Testability.Scenario;
using System.Threading;
using System.Threading.Tasks;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";

        Console.WriteLine("Starting Chaos Test Scenario...");
        try
        {
            RunChaosTestScenarioAsync(clusterConnection).Wait();
        }
        catch (AggregateException ae)
        {
            Console.WriteLine("Chaos Test Scenario did not complete: ");
            foreach (Exception ex in ae.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("Chaos Test Scenario completed.");
        return 0;
    }

    static async Task RunChaosTestScenarioAsync(string clusterConnection)
    {
        TimeSpan maxClusterStabilizationTimeout = TimeSpan.FromSeconds(180);
        uint maxConcurrentFaults = 3;
        bool enableMoveReplicaFaults = true;

        // Create FabricClient with connection and security information here.
        FabricClient fabricClient = new FabricClient(clusterConnection);

        // hello chaos test scenario should run at least 60 minutes or until it fails.
        TimeSpan timeToRun = TimeSpan.FromMinutes(60);
        ChaosTestScenarioParameters scenarioParameters = new ChaosTestScenarioParameters(
          maxClusterStabilizationTimeout,
          maxConcurrentFaults,
          enableMoveReplicaFaults,
          timeToRun);

        // Other related parameters:
        // Pause between two iterations for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenIterations = TimeSpan.FromSeconds(30);
        // Pause between concurrent actions for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenFaults = TimeSpan.FromSeconds(10);

        // Create hello scenario class and execute it asynchronously.
        ChaosTestScenario chaosScenario = new ChaosTestScenario(fabricClient, scenarioParameters);

        try
        {
            await chaosScenario.ExecuteAsync(CancellationToken.None);
        }
        catch (AggregateException ae)
        {
            throw ae.InnerException;
        }
    }
}
```

PowerShell

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricChaosTestScenario -TimeToRunMinute $timeToRun -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -MaxConcurrentFaults $concurrentFaults -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec
```


## <a name="failover-test"></a>Test de basculement
scénario de test de basculement Hello est une version de scénario de test de chaos hello qui cible une partition de service spécifique. Il teste effet hello de basculement sur une partition de service spécifique en laissant d’autres services hello pas affectées. Une fois qu’il est configuré avec les informations de partition cible hello et d’autres paramètres, elle s’exécute comme un outil côté client qui utilise l’API c# ou PowerShell défauts de toogenerate pour une partition de service. scénario de Hello effectue une itération dans une séquence d’erreurs simulés et validation de service pendant l’exécution de votre logique métier sur hello côté tooprovide une charge de travail. Un échec de validation de service indique une erreur nécessitant un examen approfondi.

### <a name="faults-simulated-in-hello-failover-test"></a>Erreurs simulées dans le test de basculement hello
* Redémarrer un package de code déployé où la partition de hello est hébergée
* Supprimez une instance sans état ou un réplica principal/secondaire
* Redémarrez un réplica principal/secondaire (en cas de service persistant)
* Déplacez un réplica principal
* Déplacez un réplica secondaire
* Redémarrez la partition de hello

test de basculement Hello induit une erreur choisie, puis exécute la validation sur hello service tooensure sa stabilité. test de basculement Hello induit uniquement une erreur au niveau d’un toopossible de temps, par opposition plusieurs erreurs dans le test de chaos hello. Si la partition de service hello ne stabiliser pas dans le délai d’attente hello configuré après chaque erreur, hello échoue. test de Hello induit uniquement les erreurs sans échec. Cela signifie qu’en l’absence de défaillances externes, aucune perte de données ni de quorum ne survient.

### <a name="important-configuration-options"></a>Options de configuration importantes
* **PartitionSelector**: objet de sélecteur qui spécifie la partition d’hello toobe ciblé.
* **TimeToRun**: durée totale de ce test hello exécutera avant la fin.
* **MaxServiceStabilizationTimeout**: quantité maximale de toowait de temps pour toobecome de cluster hello sain avant l’échec du test de hello. Hello vérifications effectuées sont si l’intégrité du service est OK, taille du jeu de réplica cible hello est réalisée pour toutes les partitions et aucun réplicas InBuild n’existent.
* **WaitTimeBetweenFaults**: quantité de toowait de temps entre chaque cycle d’erreur et de validation.

### <a name="how-toorun-hello-failover-test"></a>Comment tester les toorun hello basculement
**C#**

```csharp
using System;
using System.Fabric;
using System.Fabric.Testability.Scenario;
using System.Threading;
using System.Threading.Tasks;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";
        Uri serviceName = new Uri("fabric:/samples/PersistentToDoListApp/PersistentToDoListService");

        Console.WriteLine("Starting Chaos Test Scenario...");
        try
        {
            RunFailoverTestScenarioAsync(clusterConnection, serviceName).Wait();
        }
        catch (AggregateException ae)
        {
            Console.WriteLine("Chaos Test Scenario did not complete: ");
            foreach (Exception ex in ae.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("Chaos Test Scenario completed.");
        return 0;
    }

    static async Task RunFailoverTestScenarioAsync(string clusterConnection, Uri serviceName)
    {
        TimeSpan maxServiceStabilizationTimeout = TimeSpan.FromSeconds(180);
        PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);

        // Create FabricClient with connection and security information here.
        FabricClient fabricClient = new FabricClient(clusterConnection);

        // hello chaos test scenario should run at least 60 minutes or until it fails.
        TimeSpan timeToRun = TimeSpan.FromMinutes(60);
        FailoverTestScenarioParameters scenarioParameters = new FailoverTestScenarioParameters(
          randomPartitionSelector,
          timeToRun,
          maxServiceStabilizationTimeout);

        // Other related parameters:
        // Pause between two iterations for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenIterations = TimeSpan.FromSeconds(30);
        // Pause between concurrent actions for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenFaults = TimeSpan.FromSeconds(10);

        // Create hello scenario class and execute it asynchronously.
        FailoverTestScenario failoverScenario = new FailoverTestScenario(fabricClient, scenarioParameters);

        try
        {
            await failoverScenario.ExecuteAsync(CancellationToken.None);
        }
        catch (AggregateException ae)
        {
            throw ae.InnerException;
        }
    }
}
```


**PowerShell**

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$waitTimeBetweenFaultsSec = 10
$serviceName = "fabric:/SampleApp/SampleService"

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricFailoverTestScenario -TimeToRunMinute $timeToRun -MaxServiceStabilizationTimeoutSec $maxStabilizationTimeSecs -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ServiceName $serviceName -PartitionKindSingleton
```
