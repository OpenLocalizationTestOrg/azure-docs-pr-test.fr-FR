---
title: "contrôle d’intégrité aaaReport et vérification avec Azure Service Fabric | Documents Microsoft"
description: "Découvrez comment l’intégrité de toosend les rapports à partir de votre code de service et comment le contrôle d’intégrité de hello toocheck de votre service à l’aide des outils de surveillance de la santé hello que Azure Service Fabric fournit."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: mfussell
editor: 
ms.assetid: 7c712c22-d333-44bc-b837-d0b3603d9da8
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: dekapur
ms.openlocfilehash: bcb838fefe3f2054447e1731d709e455560260e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="report-and-check-service-health"></a><span data-ttu-id="bf7f5-103">Signaler et contrôler l’intégrité du service</span><span class="sxs-lookup"><span data-stu-id="bf7f5-103">Report and check service health</span></span>
<span data-ttu-id="bf7f5-104">Lorsque vos services rencontrent des problèmes, votre capacité toorespond tooand correctif incidents et les pannes dépend de vos problèmes de hello toodetect capacité rapidement.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-104">When your services encounter problems, your ability toorespond tooand fix incidents and outages depends on your ability toodetect hello issues quickly.</span></span> <span data-ttu-id="bf7f5-105">Si vous signalez des problèmes et des défaillances du Gestionnaire de contrôle d’intégrité toohello Azure Service Fabric à partir de votre code de service, vous pouvez utiliser que le Service Fabric fournit l’état d’intégrité toocheck hello des outils d’analyse d’état standard.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-105">If you report problems and failures toohello Azure Service Fabric health manager from your service code, you can use standard health monitoring tools that Service Fabric provides toocheck hello health status.</span></span>

<span data-ttu-id="bf7f5-106">Il existe trois méthodes que vous pouvez signaler l’intégrité du service de hello :</span><span class="sxs-lookup"><span data-stu-id="bf7f5-106">There are three ways that you can report health from hello service:</span></span>

* <span data-ttu-id="bf7f5-107">Utilisez les objets [Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) ou [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext).</span><span class="sxs-lookup"><span data-stu-id="bf7f5-107">Use [Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) or [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext) objects.</span></span>  
  <span data-ttu-id="bf7f5-108">Vous pouvez utiliser hello `Partition` et `CodePackageActivationContext` objets de contrôle d’intégrité de hello tooreport d’éléments qui font partie du contexte actuel de hello.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-108">You can use hello `Partition` and `CodePackageActivationContext` objects tooreport hello health of elements that are part of hello current context.</span></span> <span data-ttu-id="bf7f5-109">Par exemple, le code qui s’exécute en tant que partie d’un réplica peut signaler d’intégrité uniquement sur ce réplica, partition hello auquel il appartient et application hello dont il fait partie de.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-109">For example, code that runs as part of a replica can report health only on that replica, hello partition that it belongs to, and hello application that it is a part of.</span></span>
* <span data-ttu-id="bf7f5-110">Utilisez `FabricClient`.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-110">Use `FabricClient`.</span></span>   
  <span data-ttu-id="bf7f5-111">Vous pouvez utiliser `FabricClient` intégrité tooreport à partir du code de service hello si hello cluster n’est pas [sécurisé](service-fabric-cluster-security.md) ou si le service de hello est en cours d’exécution avec des privilèges d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-111">You can use `FabricClient` tooreport health from hello service code if hello cluster is not [secure](service-fabric-cluster-security.md) or if hello service is running with admin privileges.</span></span> <span data-ttu-id="bf7f5-112">La plupart des scénarios réels n’utilisent pas de clusters non sécurisés et ne fournissent pas de privilèges Administrateur.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-112">Most real-world scenarios do not use unsecured clusters, or provide admin privileges.</span></span> <span data-ttu-id="bf7f5-113">Avec `FabricClient`, vous pouvez signaler l’intégrité de toute entité qui fait partie du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-113">With `FabricClient`, you can report health on any entity that is a part of hello cluster.</span></span> <span data-ttu-id="bf7f5-114">Dans l’idéal, toutefois, code de service doit uniquement envoyer des rapports qui sont la santé propres tooits connexes.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-114">Ideally, however, service code should only send reports that are related tooits own health.</span></span>
* <span data-ttu-id="bf7f5-115">Utilisez hello API REST au cluster de hello, application, application déployée, service, package de service, partition, réplicas ou les niveaux de nœud.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-115">Use hello REST APIs at hello cluster, application, deployed application, service, service package, partition, replica, or node levels.</span></span> <span data-ttu-id="bf7f5-116">Cela peut être l’intégrité tooreport utilisé dans un conteneur.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-116">This can be used tooreport health from within a container.</span></span>

<span data-ttu-id="bf7f5-117">Cet article vous guide dans un exemple où les rapports d’intégrité à partir de code de service hello.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-117">This article walks you through an example that reports health from hello service code.</span></span> <span data-ttu-id="bf7f5-118">Hello montre également comment outils hello fournies par l’infrastructure de Service peuvent être l’état d’intégrité utilisées toocheck hello.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-118">hello example also shows how hello tools provided by Service Fabric can be used toocheck hello health status.</span></span> <span data-ttu-id="bf7f5-119">Cet article est prévue toobe un brève introduction toohello d’analyse du fonctionnement fonctionnalités du Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-119">This article is intended toobe a quick introduction toohello health monitoring capabilities of Service Fabric.</span></span> <span data-ttu-id="bf7f5-120">Pour plus d’informations, vous pouvez lire série hello des articles détaillés sur le contrôle d’intégrité qui commencent par un lien de hello en fin de hello de cet article.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-120">For more detailed information, you can read hello series of in-depth articles about health that start with hello link at hello end of this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bf7f5-121">Composants requis</span><span class="sxs-lookup"><span data-stu-id="bf7f5-121">Prerequisites</span></span>
<span data-ttu-id="bf7f5-122">Vous devez disposer de hello installé :</span><span class="sxs-lookup"><span data-stu-id="bf7f5-122">You must have hello following installed:</span></span>

* <span data-ttu-id="bf7f5-123">Visual Studio 2015 ou Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="bf7f5-123">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="bf7f5-124">SDK Service Fabric</span><span class="sxs-lookup"><span data-stu-id="bf7f5-124">Service Fabric SDK</span></span>

## <a name="toocreate-a-local-secure-dev-cluster"></a><span data-ttu-id="bf7f5-125">toocreate un cluster local développement sécurisé</span><span class="sxs-lookup"><span data-stu-id="bf7f5-125">toocreate a local secure dev cluster</span></span>
* <span data-ttu-id="bf7f5-126">Ouvrez PowerShell avec des privilèges d’administrateur et exécutez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="bf7f5-126">Open PowerShell with admin privileges, and run hello following commands:</span></span>

![Commandes qui montrent comment toocreate un cluster de développement sécurisé](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-secure-dev-cluster.png)

## <a name="toodeploy-an-application-and-check-its-health"></a><span data-ttu-id="bf7f5-128">toodeploy une application et vérifier son état d’intégrité</span><span class="sxs-lookup"><span data-stu-id="bf7f5-128">toodeploy an application and check its health</span></span>
1. <span data-ttu-id="bf7f5-129">Ouvrez Visual Studio en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-129">Open Visual Studio as an administrator.</span></span>
2. <span data-ttu-id="bf7f5-130">Créer un projet à l’aide de hello **avec état Service** modèle.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-130">Create a project by using hello **Stateful Service** template.</span></span>
   
    ![Créer une application Service Fabric avec des services avec état](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-stateful-service-application-dialog.png)
3. <span data-ttu-id="bf7f5-132">Appuyez sur **F5** application hello de toorun en mode débogage.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-132">Press **F5** toorun hello application in debug mode.</span></span> <span data-ttu-id="bf7f5-133">Hello application est déployée toohello local.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-133">hello application is deployed toohello local cluster.</span></span>
4. <span data-ttu-id="bf7f5-134">Après l’application hello est en cours d’exécution, cliquez sur icône du Gestionnaire du Cluster Local hello dans la zone de notification hello et sélectionnez **gérer un Cluster Local** de tooopen de menu contextuel hello Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-134">After hello application is running, right-click hello Local Cluster Manager icon in hello notification area and select **Manage Local Cluster** from hello shortcut menu tooopen Service Fabric Explorer.</span></span>
   
    ![Ouvrez Service Fabric Explorer à partir de la zone de notification](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/LaunchSFX.png)
5. <span data-ttu-id="bf7f5-136">intégrité des applications Hello doit être affichée comme dans cette image.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-136">hello application health should be displayed as in this image.</span></span> <span data-ttu-id="bf7f5-137">À ce stade, l’application hello doit être saine sans erreurs.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-137">At this time, hello application should be healthy with no errors.</span></span>
   
    ![Application saine dans l’Explorateur Service Fabric](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-healthy-app.png)
6. <span data-ttu-id="bf7f5-139">Vous pouvez également vérifier l’intégrité de hello à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-139">You can also check hello health by using PowerShell.</span></span> <span data-ttu-id="bf7f5-140">Vous pouvez utiliser ```Get-ServiceFabricApplicationHealth``` toocheck contrôle d’intégrité d’une application et vous pouvez utiliser ```Get-ServiceFabricServiceHealth``` toocheck contrôle d’intégrité d’un service.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-140">You can use ```Get-ServiceFabricApplicationHealth``` toocheck an application's health, and you can use ```Get-ServiceFabricServiceHealth``` toocheck a service's health.</span></span> <span data-ttu-id="bf7f5-141">Hello rapport d’intégrité pour hello même application dans PowerShell est dans cette image.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-141">hello health report for hello same application in PowerShell is in this image.</span></span>
   
    ![Application saine dans PowerShell](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/ps-healthy-app-report.png)

## <a name="tooadd-custom-health-events-tooyour-service-code"></a><span data-ttu-id="bf7f5-143">code de service tooadd l’intégrité personnalisée événements tooyour</span><span class="sxs-lookup"><span data-stu-id="bf7f5-143">tooadd custom health events tooyour service code</span></span>
<span data-ttu-id="bf7f5-144">modèles de projet de Service Fabric Hello dans Visual Studio contiennent un exemple de code.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-144">hello Service Fabric project templates in Visual Studio contain sample code.</span></span> <span data-ttu-id="bf7f5-145">Hello étapes suivantes montrent comment vous pouvez signaler des événements d’état personnalisé à partir de votre code de service.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-145">hello following steps show how you can report custom health events from your service code.</span></span> <span data-ttu-id="bf7f5-146">Ces rapports s’affichent automatiquement dans les outils standard hello pour que l’infrastructure de Service fournit, telles que le Service Fabric Explorer, vue de contrôle d’intégrité du portail Azure et PowerShell d’analyse du fonctionnement.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-146">Such reports show up automatically in hello standard tools for health monitoring that Service Fabric provides, such as Service Fabric Explorer, Azure portal health view, and PowerShell.</span></span>

1. <span data-ttu-id="bf7f5-147">Rouvrez l’application hello que vous avez créé précédemment dans Visual Studio, ou créez une application à l’aide de hello **avec état Service** modèle Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-147">Reopen hello application that you created previously in Visual Studio, or create a new application by using hello **Stateful Service** Visual Studio template.</span></span>
2. <span data-ttu-id="bf7f5-148">Ouvrez le fichier de Stateful1.cs hello et recherche hello `myDictionary.TryGetValueAsync` appeler Bonjour `RunAsync` (méthode).</span><span class="sxs-lookup"><span data-stu-id="bf7f5-148">Open hello Stateful1.cs file, and find hello `myDictionary.TryGetValueAsync` call in hello `RunAsync` method.</span></span> <span data-ttu-id="bf7f5-149">Vous pouvez voir que cette méthode retourne un `result` que contient hello la valeur actuelle du compteur de hello, car il est logique de clé hello dans cette application est tookeep en cours d’exécution un nombre.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-149">You can see that this method returns a `result` that holds hello current value of hello counter because hello key logic in this application is tookeep a count running.</span></span> <span data-ttu-id="bf7f5-150">S’il s’agissait d’une application réelle, et si un manque de hello du résultat représenté une défaillance, vous souhaiteriez tooflag cet événement.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-150">If this were a real application, and if hello lack of result represented a failure, you would want tooflag that event.</span></span>
3. <span data-ttu-id="bf7f5-151">tooreport un événement de contrôle d’intégrité en cas de manque de hello de résultat représente une erreur, ajoutez hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-151">tooreport a health event when hello lack of result represents a failure, add hello following steps.</span></span>
   
    <span data-ttu-id="bf7f5-152">a.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-152">a.</span></span> <span data-ttu-id="bf7f5-153">Ajouter hello `System.Fabric.Health` espace de noms toohello Stateful1.cs fichier.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-153">Add hello `System.Fabric.Health` namespace toohello Stateful1.cs file.</span></span>
   
    ```csharp
    using System.Fabric.Health;
    ```
   
    <span data-ttu-id="bf7f5-154">b.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-154">b.</span></span> <span data-ttu-id="bf7f5-155">Ajouter hello après le code après hello `myDictionary.TryGetValueAsync` appeler</span><span class="sxs-lookup"><span data-stu-id="bf7f5-155">Add hello following code after hello `myDictionary.TryGetValueAsync` call</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
    <span data-ttu-id="bf7f5-156">Nous signalons l’intégrité du réplica, car il provient d’un service avec état.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-156">We report replica health because it's being reported from a stateful service.</span></span> <span data-ttu-id="bf7f5-157">Hello `HealthInformation` paramètre stocke des informations sur le problème d’intégrité hello signalée.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-157">hello `HealthInformation` parameter stores information about hello health issue that's being reported.</span></span>
   
    <span data-ttu-id="bf7f5-158">Si vous aviez créé un service sans état, utiliser hello suivant de code</span><span class="sxs-lookup"><span data-stu-id="bf7f5-158">If you had created a stateless service, use hello following code</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
    ```
4. <span data-ttu-id="bf7f5-159">Si votre service s’exécute avec des privilèges d’administrateur ou si hello cluster n’est pas [sécurisé](service-fabric-cluster-security.md), vous pouvez également utiliser `FabricClient` intégrité tooreport comme indiqué dans hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-159">If your service is running with admin privileges or if hello cluster is not [secure](service-fabric-cluster-security.md), you can also use `FabricClient` tooreport health as shown in hello following steps.</span></span>  
   
    <span data-ttu-id="bf7f5-160">a.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-160">a.</span></span> <span data-ttu-id="bf7f5-161">Créer hello `FabricClient` instance après hello `var myDictionary` déclaration.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-161">Create hello `FabricClient` instance after hello `var myDictionary` declaration.</span></span>
   
    ```csharp
    var fabricClient = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });
    ```
   
    <span data-ttu-id="bf7f5-162">b.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-162">b.</span></span> <span data-ttu-id="bf7f5-163">Ajouter hello après le code après hello `myDictionary.TryGetValueAsync` appeler.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-163">Add hello following code after hello `myDictionary.TryGetValueAsync` call.</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
       var replicaHealthReport = new StatefulServiceReplicaHealthReport(
            this.Context.PartitionId,
            this.Context.ReplicaId,
            new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error));
        fabricClient.HealthManager.ReportHealth(replicaHealthReport);
    }
    ```
5. <span data-ttu-id="bf7f5-164">Nous allons simuler cette panne et la faire apparaître dans les outils de contrôle d’intégrité hello.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-164">Let's simulate this failure and see it show up in hello health monitoring tools.</span></span> <span data-ttu-id="bf7f5-165">Échec de hello toosimulate, commentez hello de première ligne dans le contrôle d’intégrité hello signale le code que vous avez ajouté précédemment.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-165">toosimulate hello failure, comment out hello first line in hello health reporting code that you added earlier.</span></span> <span data-ttu-id="bf7f5-166">Une fois que vous mettez en commentez hello première ligne, code de hello ressemblera à hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-166">After you comment out hello first line, hello code will look like hello following example.</span></span>
   
    ```csharp
    //if(!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
   <span data-ttu-id="bf7f5-167">Ce code déclenche rapport d’intégrité de hello chaque fois `RunAsync` s’exécute.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-167">This code fires hello health report each time `RunAsync` executes.</span></span> <span data-ttu-id="bf7f5-168">Dès que vous modifiez hello, appuyez sur **F5** application hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-168">After you make hello change, press **F5** toorun hello application.</span></span>
6. <span data-ttu-id="bf7f5-169">Après que l’application hello est en cours d’exécution, ouvrez le contrôle d’intégrité de Service Fabric Explorer toocheck hello de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-169">After hello application is running, open Service Fabric Explorer toocheck hello health of hello application.</span></span> <span data-ttu-id="bf7f5-170">Cette fois-ci, Service Fabric Explorer montre que l’application hello est défectueux.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-170">This time, Service Fabric Explorer shows that hello application is unhealthy.</span></span> <span data-ttu-id="bf7f5-171">Il s’agit en raison de l’erreur hello qui a été signalée à partir du code hello que nous avons ajouté précédemment.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-171">This is because of hello error that was reported from hello code that we added previously.</span></span>
   
    ![Application non saine dans l’Explorateur Service Fabric](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-unhealthy-app.png)
7. <span data-ttu-id="bf7f5-173">Si vous sélectionnez le réplica principal de hello dans arborescence hello de Service Fabric Explorer, vous verrez que **l’état d’intégrité** indique une erreur de trop.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-173">If you select hello primary replica in hello tree view of Service Fabric Explorer, you will see that **Health State** indicates an error, too.</span></span> <span data-ttu-id="bf7f5-174">Service Fabric Explorer affiche également le rapport d’intégrité de hello détails qui ont été ajoutés toohello `HealthInformation` paramètre dans le code hello.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-174">Service Fabric Explorer also displays hello health report details that were added toohello `HealthInformation` parameter in hello code.</span></span> <span data-ttu-id="bf7f5-175">Vous pouvez voir hello même rapports d’intégrité dans PowerShell et hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-175">You can see hello same health reports in PowerShell and hello Azure portal.</span></span>
   
    ![Intégrité du réplica dans l’Explorateur Service Fabric](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/replica-health-error-report-sfx.png)

<span data-ttu-id="bf7f5-177">Ce rapport reste dans le Gestionnaire de contrôle d’intégrité hello jusqu'à ce qu’il est remplacé par un autre rapport, ou jusqu'à ce que ce réplica est supprimé.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-177">This report remains in hello health manager until it is replaced by another report or until this replica is deleted.</span></span> <span data-ttu-id="bf7f5-178">Étant donné que nous n’avez pas défini `TimeToLive` pour ce rapport d’intégrité Bonjour `HealthInformation` de l’objet, les rapports hello n’expire jamais.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-178">Because we did not set `TimeToLive` for this health report in hello `HealthInformation` object, hello report never expires.</span></span>

<span data-ttu-id="bf7f5-179">Il est recommandé que le contrôle d’intégrité doit être signalé sur un niveau plus granulaire de hello, qui dans ce cas est le réplica de hello.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-179">We recommend that health should be reported on hello most granular level, which in this case is hello replica.</span></span> <span data-ttu-id="bf7f5-180">Vous pouvez également signaler l’intégrité sur `Partition`.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-180">You can also report health on `Partition`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
this.Partition.ReportPartitionHealth(healthInformation);
```

<span data-ttu-id="bf7f5-181">contrôle d’intégrité tooreport sur `Application`, `DeployedApplication`, et `DeployedServicePackage`, utilisez `CodePackageActivationContext`.</span><span class="sxs-lookup"><span data-stu-id="bf7f5-181">tooreport health on `Application`, `DeployedApplication`, and `DeployedServicePackage`, use  `CodePackageActivationContext`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
var activationContext = FabricRuntime.GetActivationContext();
activationContext.ReportApplicationHealth(healthInformation);
```

## <a name="next-steps"></a><span data-ttu-id="bf7f5-182">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bf7f5-182">Next steps</span></span>
* [<span data-ttu-id="bf7f5-183">Présentation approfondie de l’intégrité de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="bf7f5-183">Deep dive on Service Fabric health</span></span>](service-fabric-health-introduction.md)
* [<span data-ttu-id="bf7f5-184">API REST pour les rapports d’intégrité du service</span><span class="sxs-lookup"><span data-stu-id="bf7f5-184">REST API for reporting service health</span></span>](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service)
* [<span data-ttu-id="bf7f5-185">API REST pour les rapports d’intégrité de l’application</span><span class="sxs-lookup"><span data-stu-id="bf7f5-185">REST API for reporting application health</span></span>](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-an-application)

