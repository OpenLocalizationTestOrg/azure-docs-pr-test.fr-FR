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
# <a name="testability-scenarios"></a><span data-ttu-id="ca293-103">Scénarios de testabilité</span><span class="sxs-lookup"><span data-stu-id="ca293-103">Testability scenarios</span></span>
<span data-ttu-id="ca293-104">Les grands systèmes distribués, comme les infrastructures cloud, sont par définition peu fiables.</span><span class="sxs-lookup"><span data-stu-id="ca293-104">Large distributed systems like cloud infrastructures are inherently unreliable.</span></span> <span data-ttu-id="ca293-105">Azure Service Fabric permet aux développeurs hello capacité toowrite services toorun au-dessus des infrastructures non fiables.</span><span class="sxs-lookup"><span data-stu-id="ca293-105">Azure Service Fabric gives developers hello ability toowrite services toorun on top of unreliable infrastructures.</span></span> <span data-ttu-id="ca293-106">Dans l’ordre toowrite des services de qualité, les développeurs doivent tooinduce en mesure de toobe stabilité de hello tootest telle infrastructure non fiable de leurs services.</span><span class="sxs-lookup"><span data-stu-id="ca293-106">In order toowrite high-quality services, developers need toobe able tooinduce such unreliable infrastructure tootest hello stability of their services.</span></span>

<span data-ttu-id="ca293-107">Hello erreur Analysis Service offre aux développeurs services tootest des actions de pannes hello capacité tooinduce en présence de hello d’échecs.</span><span class="sxs-lookup"><span data-stu-id="ca293-107">hello Fault Analysis Service gives developers hello ability tooinduce fault actions tootest services in hello presence of failures.</span></span> <span data-ttu-id="ca293-108">Toutefois, les erreurs simulées ciblées présentent une efficacité limitée.</span><span class="sxs-lookup"><span data-stu-id="ca293-108">However, targeted simulated faults will get you only so far.</span></span> <span data-ttu-id="ca293-109">hello tootake test en outre, vous pouvez utiliser des scénarios de test hello dans Service Fabric : un test chaos et un test de basculement.</span><span class="sxs-lookup"><span data-stu-id="ca293-109">tootake hello testing further, you can use hello test scenarios in Service Fabric: a chaos test and a failover test.</span></span> <span data-ttu-id="ca293-110">Ces scénarios de simulent continues erreurs entrelacées, normale et anormal, dans l’ensemble de cluster hello sur de longues périodes.</span><span class="sxs-lookup"><span data-stu-id="ca293-110">These scenarios simulate continuous interleaved faults, both graceful and ungraceful, throughout hello cluster over extended periods of time.</span></span> <span data-ttu-id="ca293-111">Une fois qu’un test est configuré avec un taux de hello et du type d’erreurs, il peut être démarré par le biais des API c# ou PowerShell, toogenerate des erreurs dans le cluster de hello et votre service.</span><span class="sxs-lookup"><span data-stu-id="ca293-111">Once a test is configured with hello rate and kind of faults, it can be started through either C# APIs or PowerShell, toogenerate faults in hello cluster and your service.</span></span>

> [!WARNING]
> <span data-ttu-id="ca293-112">ChaosTestScenario est remplacé par un chaos plus robuste, basé sur le service.</span><span class="sxs-lookup"><span data-stu-id="ca293-112">ChaosTestScenario is being replaced by a more resilient, service-based Chaos.</span></span> <span data-ttu-id="ca293-113">Reportez-vous toohello nouvel article [contrôlé le Chaos](service-fabric-controlled-chaos.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="ca293-113">Please refer toohello new article [Controlled Chaos](service-fabric-controlled-chaos.md) for more details.</span></span>
> 
> 

## <a name="chaos-test"></a><span data-ttu-id="ca293-114">Test chaos</span><span class="sxs-lookup"><span data-stu-id="ca293-114">Chaos test</span></span>
<span data-ttu-id="ca293-115">scénario de chaos Hello génère des erreurs sur l’intégralité du cluster Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="ca293-115">hello chaos scenario generates faults across hello entire Service Fabric cluster.</span></span> <span data-ttu-id="ca293-116">scénario de Hello compresse les erreurs généralement visibles dans les mois ou années tooa quelques heures.</span><span class="sxs-lookup"><span data-stu-id="ca293-116">hello scenario compresses faults generally seen in months or years tooa few hours.</span></span> <span data-ttu-id="ca293-117">combinaison Hello d’erreurs entrelacées avec un taux d’erreur élevé hello recherche les cas qui sont omis dans le cas contraire.</span><span class="sxs-lookup"><span data-stu-id="ca293-117">hello combination of interleaved faults with hello high fault rate finds corner cases that are otherwise missed.</span></span> <span data-ttu-id="ca293-118">Cela entraîne une amélioration importante tooa dans la qualité du code hello du service de hello.</span><span class="sxs-lookup"><span data-stu-id="ca293-118">This leads tooa significant improvement in hello code quality of hello service.</span></span>

### <a name="faults-simulated-in-hello-chaos-test"></a><span data-ttu-id="ca293-119">Erreurs simulées dans le test de chaos hello</span><span class="sxs-lookup"><span data-stu-id="ca293-119">Faults simulated in hello chaos test</span></span>
* <span data-ttu-id="ca293-120">Redémarrer un nœud</span><span class="sxs-lookup"><span data-stu-id="ca293-120">Restart a node</span></span>
* <span data-ttu-id="ca293-121">Redémarrer un package de code déployé</span><span class="sxs-lookup"><span data-stu-id="ca293-121">Restart a deployed code package</span></span>
* <span data-ttu-id="ca293-122">Supprimer un réplica</span><span class="sxs-lookup"><span data-stu-id="ca293-122">Remove a replica</span></span>
* <span data-ttu-id="ca293-123">Redémarrer un réplica</span><span class="sxs-lookup"><span data-stu-id="ca293-123">Restart a replica</span></span>
* <span data-ttu-id="ca293-124">Déplacer un réplica principal (principal)</span><span class="sxs-lookup"><span data-stu-id="ca293-124">Move a primary replica (optional)</span></span>
* <span data-ttu-id="ca293-125">Déplacer un réplica secondaire (facultatif)</span><span class="sxs-lookup"><span data-stu-id="ca293-125">Move a secondary replica (optional)</span></span>

<span data-ttu-id="ca293-126">test de chaos Hello exécute plusieurs itérations d’erreurs et les validations de cluster pour hello spécifié laps de temps.</span><span class="sxs-lookup"><span data-stu-id="ca293-126">hello chaos test runs multiple iterations of faults and cluster validations for hello specified period of time.</span></span> <span data-ttu-id="ca293-127">Hello temps passé pour hello cluster toostabilize et toosucceed de validation est également configurable.</span><span class="sxs-lookup"><span data-stu-id="ca293-127">hello time spent for hello cluster toostabilize and for validation toosucceed is also configurable.</span></span> <span data-ttu-id="ca293-128">scénario de Hello échoue lorsque vous atteignez une défaillance de la validation du cluster.</span><span class="sxs-lookup"><span data-stu-id="ca293-128">hello scenario fails when you hit a single failure in cluster validation.</span></span>

<span data-ttu-id="ca293-129">Par exemple, considérez qu'un test définie toorun pendant une heure avec un maximum de trois défaillances simultanées.</span><span class="sxs-lookup"><span data-stu-id="ca293-129">For example, consider a test set toorun for one hour with a maximum of three concurrent faults.</span></span> <span data-ttu-id="ca293-130">test de Hello sera induire des erreurs de trois et puis de valider l’intégrité du cluster hello.</span><span class="sxs-lookup"><span data-stu-id="ca293-130">hello test will induce three faults, and then validate hello cluster health.</span></span> <span data-ttu-id="ca293-131">test de Hello effectue une itération à l’étape précédente de hello jusqu'à ce que le cluster de hello devient non intègre ou passe d’une heure.</span><span class="sxs-lookup"><span data-stu-id="ca293-131">hello test will iterate through hello previous step till hello cluster becomes unhealthy or one hour passes.</span></span> <span data-ttu-id="ca293-132">Si le cluster de hello devient non intègre dans une itération, autrement dit, ne pas stabiliser pendant la durée configurée, test de hello échoue avec une exception.</span><span class="sxs-lookup"><span data-stu-id="ca293-132">If hello cluster becomes unhealthy in any iteration, i.e. it does not stabilize within a configured time, hello test will fail with an exception.</span></span> <span data-ttu-id="ca293-133">Cette exception indique qu’une erreur est survenue et qu’un examen approfondi est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="ca293-133">This exception indicates that something has gone wrong and needs further investigation.</span></span>

<span data-ttu-id="ca293-134">Dans sa forme actuelle du moteur de génération de pannes hello dans le test de chaos hello induit erreurs uniquement sans échec.</span><span class="sxs-lookup"><span data-stu-id="ca293-134">In its current form, hello fault generation engine in hello chaos test induces only safe faults.</span></span> <span data-ttu-id="ca293-135">Cela signifie qu’en absence de hello d’erreurs externes, une quorum ou perte de données ne se produira.</span><span class="sxs-lookup"><span data-stu-id="ca293-135">This means that in hello absence of external faults, a quorum or data loss will never occur.</span></span>

### <a name="important-configuration-options"></a><span data-ttu-id="ca293-136">Options de configuration importantes</span><span class="sxs-lookup"><span data-stu-id="ca293-136">Important configuration options</span></span>
* <span data-ttu-id="ca293-137">**TimeToRun**: durée totale de ce test hello exécutera avant de terminer avec succès.</span><span class="sxs-lookup"><span data-stu-id="ca293-137">**TimeToRun**: Total time that hello test will run before finishing with success.</span></span> <span data-ttu-id="ca293-138">test de Hello peut terminer plus tôt à la place d’un échec de validation.</span><span class="sxs-lookup"><span data-stu-id="ca293-138">hello test can finish earlier in lieu of a validation failure.</span></span>
* <span data-ttu-id="ca293-139">**MaxClusterStabilizationTimeout**: quantité maximale de toowait de temps pour toobecome de cluster hello sain avant l’échec du test de hello.</span><span class="sxs-lookup"><span data-stu-id="ca293-139">**MaxClusterStabilizationTimeout**: Maximum amount of time toowait for hello cluster toobecome healthy before failing hello test.</span></span> <span data-ttu-id="ca293-140">Hello vérifications effectuées sont si l’intégrité du cluster est OK, l’intégrité du service est OK, taille du jeu de réplica cible hello est obtenue de la partition de service hello et aucun réplicas InBuild n’existent.</span><span class="sxs-lookup"><span data-stu-id="ca293-140">hello checks performed are whether cluster health is OK, service health is OK, hello target replica set size is achieved for hello service partition, and no InBuild replicas exist.</span></span>
* <span data-ttu-id="ca293-141">**MaxConcurrentFaults** : nombre maximal d’erreurs simultanées introduites dans chaque itération.</span><span class="sxs-lookup"><span data-stu-id="ca293-141">**MaxConcurrentFaults**: Maximum number of concurrent faults induced in each iteration.</span></span> <span data-ttu-id="ca293-142">Hello plus grand nombre de hello, hello plus agressive test hello, par conséquent, ce qui entraîne des basculements plus complexes et les combinaisons de transition.</span><span class="sxs-lookup"><span data-stu-id="ca293-142">hello higher hello number, hello more aggressive hello test, hence resulting in more complex failovers and transition combinations.</span></span> <span data-ttu-id="ca293-143">test de Hello garantit qu’en l’absence d’erreurs externes aucun ne sera une quorum ou perte de données, quel que soit la manière dont cette configuration est.</span><span class="sxs-lookup"><span data-stu-id="ca293-143">hello test guarantees that in absence of external faults there will not be a quorum or data loss, irrespective of how high this configuration is.</span></span>
* <span data-ttu-id="ca293-144">**EnableMoveReplicaFaults**: Active ou désactive les erreurs hello qui sont à l’origine de déplacement hello Hello réplicas principaux ou secondaires.</span><span class="sxs-lookup"><span data-stu-id="ca293-144">**EnableMoveReplicaFaults**: Enables or disables hello faults that are causing hello move of hello primary or secondary replicas.</span></span> <span data-ttu-id="ca293-145">Ces erreurs sont désactivées par défaut.</span><span class="sxs-lookup"><span data-stu-id="ca293-145">These faults are disabled by default.</span></span>
* <span data-ttu-id="ca293-146">**WaitTimeBetweenIterations**: quantité de toowait de temps entre les itérations, par exemple, après un arrondi des défaillances et de validation correspondante.</span><span class="sxs-lookup"><span data-stu-id="ca293-146">**WaitTimeBetweenIterations**: Amount of time toowait between iterations, i.e. after a round of faults and corresponding validation.</span></span>

### <a name="how-toorun-hello-chaos-test"></a><span data-ttu-id="ca293-147">Comment tester les chaos de hello toorun</span><span class="sxs-lookup"><span data-stu-id="ca293-147">How toorun hello chaos test</span></span>
<span data-ttu-id="ca293-148">Exemple de code C#</span><span class="sxs-lookup"><span data-stu-id="ca293-148">C# sample</span></span>

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

<span data-ttu-id="ca293-149">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ca293-149">PowerShell</span></span>

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricChaosTestScenario -TimeToRunMinute $timeToRun -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -MaxConcurrentFaults $concurrentFaults -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec
```


## <a name="failover-test"></a><span data-ttu-id="ca293-150">Test de basculement</span><span class="sxs-lookup"><span data-stu-id="ca293-150">Failover test</span></span>
<span data-ttu-id="ca293-151">scénario de test de basculement Hello est une version de scénario de test de chaos hello qui cible une partition de service spécifique.</span><span class="sxs-lookup"><span data-stu-id="ca293-151">hello failover test scenario is a version of hello chaos test scenario that targets a specific service partition.</span></span> <span data-ttu-id="ca293-152">Il teste effet hello de basculement sur une partition de service spécifique en laissant d’autres services hello pas affectées.</span><span class="sxs-lookup"><span data-stu-id="ca293-152">It tests hello effect of failover on a specific service partition while leaving hello other services unaffected.</span></span> <span data-ttu-id="ca293-153">Une fois qu’il est configuré avec les informations de partition cible hello et d’autres paramètres, elle s’exécute comme un outil côté client qui utilise l’API c# ou PowerShell défauts de toogenerate pour une partition de service.</span><span class="sxs-lookup"><span data-stu-id="ca293-153">Once it's configured with hello target partition information and other parameters, it runs as a client-side tool that uses either C# APIs or PowerShell toogenerate faults for a service partition.</span></span> <span data-ttu-id="ca293-154">scénario de Hello effectue une itération dans une séquence d’erreurs simulés et validation de service pendant l’exécution de votre logique métier sur hello côté tooprovide une charge de travail.</span><span class="sxs-lookup"><span data-stu-id="ca293-154">hello scenario iterates through a sequence of simulated faults and service validation while your business logic runs on hello side tooprovide a workload.</span></span> <span data-ttu-id="ca293-155">Un échec de validation de service indique une erreur nécessitant un examen approfondi.</span><span class="sxs-lookup"><span data-stu-id="ca293-155">A failure in service validation indicates an issue that needs further investigation.</span></span>

### <a name="faults-simulated-in-hello-failover-test"></a><span data-ttu-id="ca293-156">Erreurs simulées dans le test de basculement hello</span><span class="sxs-lookup"><span data-stu-id="ca293-156">Faults simulated in hello failover test</span></span>
* <span data-ttu-id="ca293-157">Redémarrer un package de code déployé où la partition de hello est hébergée</span><span class="sxs-lookup"><span data-stu-id="ca293-157">Restart a deployed code package where hello partition is hosted</span></span>
* <span data-ttu-id="ca293-158">Supprimez une instance sans état ou un réplica principal/secondaire</span><span class="sxs-lookup"><span data-stu-id="ca293-158">Remove a primary/secondary replica or stateless instance</span></span>
* <span data-ttu-id="ca293-159">Redémarrez un réplica principal/secondaire (en cas de service persistant)</span><span class="sxs-lookup"><span data-stu-id="ca293-159">Restart a primary secondary replica (if a persisted service)</span></span>
* <span data-ttu-id="ca293-160">Déplacez un réplica principal</span><span class="sxs-lookup"><span data-stu-id="ca293-160">Move a primary replica</span></span>
* <span data-ttu-id="ca293-161">Déplacez un réplica secondaire</span><span class="sxs-lookup"><span data-stu-id="ca293-161">Move a secondary replica</span></span>
* <span data-ttu-id="ca293-162">Redémarrez la partition de hello</span><span class="sxs-lookup"><span data-stu-id="ca293-162">Restart hello partition</span></span>

<span data-ttu-id="ca293-163">test de basculement Hello induit une erreur choisie, puis exécute la validation sur hello service tooensure sa stabilité.</span><span class="sxs-lookup"><span data-stu-id="ca293-163">hello failover test induces a chosen fault and then runs validation on hello service tooensure its stability.</span></span> <span data-ttu-id="ca293-164">test de basculement Hello induit uniquement une erreur au niveau d’un toopossible de temps, par opposition plusieurs erreurs dans le test de chaos hello.</span><span class="sxs-lookup"><span data-stu-id="ca293-164">hello failover test induces only one fault at a time, as opposed toopossible multiple faults in hello chaos test.</span></span> <span data-ttu-id="ca293-165">Si la partition de service hello ne stabiliser pas dans le délai d’attente hello configuré après chaque erreur, hello échoue.</span><span class="sxs-lookup"><span data-stu-id="ca293-165">If hello service partition does not stabilize within hello configured timeout after each fault, hello test fails.</span></span> <span data-ttu-id="ca293-166">test de Hello induit uniquement les erreurs sans échec.</span><span class="sxs-lookup"><span data-stu-id="ca293-166">hello test induces only safe faults.</span></span> <span data-ttu-id="ca293-167">Cela signifie qu’en l’absence de défaillances externes, aucune perte de données ni de quorum ne survient.</span><span class="sxs-lookup"><span data-stu-id="ca293-167">This means that in absence of external failures, a quorum or data loss will not occur.</span></span>

### <a name="important-configuration-options"></a><span data-ttu-id="ca293-168">Options de configuration importantes</span><span class="sxs-lookup"><span data-stu-id="ca293-168">Important configuration options</span></span>
* <span data-ttu-id="ca293-169">**PartitionSelector**: objet de sélecteur qui spécifie la partition d’hello toobe ciblé.</span><span class="sxs-lookup"><span data-stu-id="ca293-169">**PartitionSelector**: Selector object that specifies hello partition that needs toobe targeted.</span></span>
* <span data-ttu-id="ca293-170">**TimeToRun**: durée totale de ce test hello exécutera avant la fin.</span><span class="sxs-lookup"><span data-stu-id="ca293-170">**TimeToRun**: Total time that hello test will run before finishing.</span></span>
* <span data-ttu-id="ca293-171">**MaxServiceStabilizationTimeout**: quantité maximale de toowait de temps pour toobecome de cluster hello sain avant l’échec du test de hello.</span><span class="sxs-lookup"><span data-stu-id="ca293-171">**MaxServiceStabilizationTimeout**: Maximum amount of time toowait for hello cluster toobecome healthy before failing hello test.</span></span> <span data-ttu-id="ca293-172">Hello vérifications effectuées sont si l’intégrité du service est OK, taille du jeu de réplica cible hello est réalisée pour toutes les partitions et aucun réplicas InBuild n’existent.</span><span class="sxs-lookup"><span data-stu-id="ca293-172">hello checks performed are whether service health is OK, hello target replica set size is achieved for all partitions, and no InBuild replicas exist.</span></span>
* <span data-ttu-id="ca293-173">**WaitTimeBetweenFaults**: quantité de toowait de temps entre chaque cycle d’erreur et de validation.</span><span class="sxs-lookup"><span data-stu-id="ca293-173">**WaitTimeBetweenFaults**: Amount of time toowait between every fault and validation cycle.</span></span>

### <a name="how-toorun-hello-failover-test"></a><span data-ttu-id="ca293-174">Comment tester les toorun hello basculement</span><span class="sxs-lookup"><span data-stu-id="ca293-174">How toorun hello failover test</span></span>
<span data-ttu-id="ca293-175">**C#**</span><span class="sxs-lookup"><span data-stu-id="ca293-175">**C#**</span></span>

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


<span data-ttu-id="ca293-176">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="ca293-176">**PowerShell**</span></span>

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$waitTimeBetweenFaultsSec = 10
$serviceName = "fabric:/SampleApp/SampleService"

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricFailoverTestScenario -TimeToRunMinute $timeToRun -MaxServiceStabilizationTimeoutSec $maxStabilizationTimeSecs -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ServiceName $serviceName -PartitionKindSingleton
```
