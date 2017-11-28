---
title: "Signaler et contrôler l’intégrité avec Azure Service Fabric | Microsoft Docs"
description: "Découvrez comment envoyer des rapports d’intégrité à partir de votre code de service et comment contrôler l’intégrité de votre service avec les outils de contrôle d’intégrité fournis par Azure Service Fabric."
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
ms.openlocfilehash: 83981d5bec14c06c509f1a8a4153dc23298f5ce0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="report-and-check-service-health"></a><span data-ttu-id="dd131-103">Signaler et contrôler l’intégrité du service</span><span class="sxs-lookup"><span data-stu-id="dd131-103">Report and check service health</span></span>
<span data-ttu-id="dd131-104">Lorsque vos services rencontrent des problèmes, votre capacité à réagir et à résoudre les incidents et les pannes induits dépend de votre capacité à détecter les problèmes rapidement.</span><span class="sxs-lookup"><span data-stu-id="dd131-104">When your services encounter problems, your ability to respond to and fix incidents and outages depends on your ability to detect the issues quickly.</span></span> <span data-ttu-id="dd131-105">En signalant les problèmes et les pannes au gestionnaire de contrôle d’intégrité Azure Service Fabric à partir de votre code de service, vous pouvez utiliser les outils standard de contrôle d’intégrité fournis par Service Fabric pour contrôler l’état d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="dd131-105">If you report problems and failures to the Azure Service Fabric health manager from your service code, you can use standard health monitoring tools that Service Fabric provides to check the health status.</span></span>

<span data-ttu-id="dd131-106">Il existe trois méthodes pour signaler l’intégrité à partir du service :</span><span class="sxs-lookup"><span data-stu-id="dd131-106">There are three ways that you can report health from the service:</span></span>

* <span data-ttu-id="dd131-107">Utilisez les objets [Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) ou [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext).</span><span class="sxs-lookup"><span data-stu-id="dd131-107">Use [Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) or [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext) objects.</span></span>  
  <span data-ttu-id="dd131-108">Les objets `Partition` et `CodePackageActivationContext` peuvent vous servir à signaler l’intégrité d’éléments qui font partie du contexte actuel.</span><span class="sxs-lookup"><span data-stu-id="dd131-108">You can use the `Partition` and `CodePackageActivationContext` objects to report the health of elements that are part of the current context.</span></span> <span data-ttu-id="dd131-109">Par exemple, le code s’exécutant dans le cadre d’un réplica ne peut signaler l’intégrité que sur ce réplica, la partition à laquelle il appartient et l’application dont il fait partie.</span><span class="sxs-lookup"><span data-stu-id="dd131-109">For example, code that runs as part of a replica can report health only on that replica, the partition that it belongs to, and the application that it is a part of.</span></span>
* <span data-ttu-id="dd131-110">Utilisez `FabricClient`.</span><span class="sxs-lookup"><span data-stu-id="dd131-110">Use `FabricClient`.</span></span>   
  <span data-ttu-id="dd131-111">Vous ne pouvez pas utiliser `FabricClient` pour signaler l’intégrité à partir du code de service si le cluster n’est pas [sécurisé](service-fabric-cluster-security.md) ou si le service s’exécute avec des privilèges d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="dd131-111">You can use `FabricClient` to report health from the service code if the cluster is not [secure](service-fabric-cluster-security.md) or if the service is running with admin privileges.</span></span> <span data-ttu-id="dd131-112">La plupart des scénarios réels n’utilisent pas de clusters non sécurisés et ne fournissent pas de privilèges Administrateur.</span><span class="sxs-lookup"><span data-stu-id="dd131-112">Most real-world scenarios do not use unsecured clusters, or provide admin privileges.</span></span> <span data-ttu-id="dd131-113">Avec `FabricClient`, vous pouvez signaler l’intégrité de toute entité qui fait partie du cluster.</span><span class="sxs-lookup"><span data-stu-id="dd131-113">With `FabricClient`, you can report health on any entity that is a part of the cluster.</span></span> <span data-ttu-id="dd131-114">Toutefois, dans l’idéal, le code de service n’est censé envoyer que des rapports liés à sa propre intégrité.</span><span class="sxs-lookup"><span data-stu-id="dd131-114">Ideally, however, service code should only send reports that are related to its own health.</span></span>
* <span data-ttu-id="dd131-115">Utilisez les API REST au niveau du cluster, de l’application, de l’application déployée, du service, du package de service, de la partition, du réplica ou du nœud.</span><span class="sxs-lookup"><span data-stu-id="dd131-115">Use the REST APIs at the cluster, application, deployed application, service, service package, partition, replica, or node levels.</span></span> <span data-ttu-id="dd131-116">Cela peut servir pour générer des rapports sur l’état d’un conteneur.</span><span class="sxs-lookup"><span data-stu-id="dd131-116">This can be used to report health from within a container.</span></span>

<span data-ttu-id="dd131-117">Cet article vous présente un exemple de rapports d’intégrité du code de service.</span><span class="sxs-lookup"><span data-stu-id="dd131-117">This article walks you through an example that reports health from the service code.</span></span> <span data-ttu-id="dd131-118">L’exemple montre également comment les outils fournis par Service Fabric peuvent être utilisés pour vérifier l’état d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="dd131-118">The example also shows how the tools provided by Service Fabric can be used to check the health status.</span></span> <span data-ttu-id="dd131-119">Cet article constitue une présentation rapide des fonctionnalités de contrôle d’intégrité de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="dd131-119">This article is intended to be a quick introduction to the health monitoring capabilities of Service Fabric.</span></span> <span data-ttu-id="dd131-120">Pour plus d’informations, vous pouvez lire la série d’articles détaillés sur l’intégrité, à commencer par le lien situé à la fin de cet article.</span><span class="sxs-lookup"><span data-stu-id="dd131-120">For more detailed information, you can read the series of in-depth articles about health that start with the link at the end of this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dd131-121">Composants requis</span><span class="sxs-lookup"><span data-stu-id="dd131-121">Prerequisites</span></span>
<span data-ttu-id="dd131-122">Les éléments suivants doivent être installés :</span><span class="sxs-lookup"><span data-stu-id="dd131-122">You must have the following installed:</span></span>

* <span data-ttu-id="dd131-123">Visual Studio 2015 ou Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="dd131-123">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="dd131-124">SDK Service Fabric</span><span class="sxs-lookup"><span data-stu-id="dd131-124">Service Fabric SDK</span></span>

## <a name="to-create-a-local-secure-dev-cluster"></a><span data-ttu-id="dd131-125">Pour créer un cluster local de développement sécurisé</span><span class="sxs-lookup"><span data-stu-id="dd131-125">To create a local secure dev cluster</span></span>
* <span data-ttu-id="dd131-126">Ouvrez PowerShell avec des privilèges Administrateur et exécutez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="dd131-126">Open PowerShell with admin privileges, and run the following commands:</span></span>

![Commandes montrant comment créer un cluster de développement sécurisé](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-secure-dev-cluster.png)

## <a name="to-deploy-an-application-and-check-its-health"></a><span data-ttu-id="dd131-128">Pour déployer une application et contrôler son intégrité</span><span class="sxs-lookup"><span data-stu-id="dd131-128">To deploy an application and check its health</span></span>
1. <span data-ttu-id="dd131-129">Ouvrez Visual Studio en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="dd131-129">Open Visual Studio as an administrator.</span></span>
2. <span data-ttu-id="dd131-130">Créez un projet à l’aide du modèle **Service avec état** .</span><span class="sxs-lookup"><span data-stu-id="dd131-130">Create a project by using the **Stateful Service** template.</span></span>
   
    ![Créer une application Service Fabric avec des services avec état](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-stateful-service-application-dialog.png)
3. <span data-ttu-id="dd131-132">Appuyez sur **F5** pour exécuter l’application en mode débogage.</span><span class="sxs-lookup"><span data-stu-id="dd131-132">Press **F5** to run the application in debug mode.</span></span> <span data-ttu-id="dd131-133">L’application est déployée sur le cluster local.</span><span class="sxs-lookup"><span data-stu-id="dd131-133">The application is deployed to the local cluster.</span></span>
4. <span data-ttu-id="dd131-134">Une fois que l’application est en cours d’exécution, cliquez avec le bouton droit sur l’icône du gestionnaire de cluster local dans la zone de notification et sélectionnez **Gérer le cluster local** dans le menu contextuel pour ouvrir Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="dd131-134">After the application is running, right-click the Local Cluster Manager icon in the notification area and select **Manage Local Cluster** from the shortcut menu to open Service Fabric Explorer.</span></span>
   
    ![Ouvrez Service Fabric Explorer à partir de la zone de notification](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/LaunchSFX.png)
5. <span data-ttu-id="dd131-136">L’intégrité de l’application doit s’afficher comme dans cette image.</span><span class="sxs-lookup"><span data-stu-id="dd131-136">The application health should be displayed as in this image.</span></span> <span data-ttu-id="dd131-137">À ce stade, l’application doit être saine et sans erreurs.</span><span class="sxs-lookup"><span data-stu-id="dd131-137">At this time, the application should be healthy with no errors.</span></span>
   
    ![Application saine dans l’Explorateur Service Fabric](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-healthy-app.png)
6. <span data-ttu-id="dd131-139">Vous pouvez également contrôler l’intégrité à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dd131-139">You can also check the health by using PowerShell.</span></span> <span data-ttu-id="dd131-140">Vous pouvez utiliser ```Get-ServiceFabricApplicationHealth``` pour vérifier l’intégrité d’une application et ```Get-ServiceFabricServiceHealth``` pour vérifier l’intégrité d’un service.</span><span class="sxs-lookup"><span data-stu-id="dd131-140">You can use ```Get-ServiceFabricApplicationHealth``` to check an application's health, and you can use ```Get-ServiceFabricServiceHealth``` to check a service's health.</span></span> <span data-ttu-id="dd131-141">Le rapport d’intégrité pour la même application dans PowerShell figure dans cette image.</span><span class="sxs-lookup"><span data-stu-id="dd131-141">The health report for the same application in PowerShell is in this image.</span></span>
   
    ![Application saine dans PowerShell](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/ps-healthy-app-report.png)

## <a name="to-add-custom-health-events-to-your-service-code"></a><span data-ttu-id="dd131-143">Pour ajouter des événements d’intégrité personnalisés à votre code de service</span><span class="sxs-lookup"><span data-stu-id="dd131-143">To add custom health events to your service code</span></span>
<span data-ttu-id="dd131-144">Les modèles de projet Visual Studio de Service Fabric contiennent des exemples de code.</span><span class="sxs-lookup"><span data-stu-id="dd131-144">The Service Fabric project templates in Visual Studio contain sample code.</span></span> <span data-ttu-id="dd131-145">Les étapes suivantes montrent comment vous pouvez créer des rapports sur des événements d’intégrité personnalisés à partir de votre code de service.</span><span class="sxs-lookup"><span data-stu-id="dd131-145">The following steps show how you can report custom health events from your service code.</span></span> <span data-ttu-id="dd131-146">Ces rapports s’affichent automatiquement dans les outils standard de surveillance de l’intégrité fournis par Service Fabric, tels que Service Fabric Explorer, la vue d’intégrité du portail Azure et PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dd131-146">Such reports show up automatically in the standard tools for health monitoring that Service Fabric provides, such as Service Fabric Explorer, Azure portal health view, and PowerShell.</span></span>

1. <span data-ttu-id="dd131-147">Rouvrez l’application créée précédemment dans Visual Studio ou créez une application à l’aide du modèle **Service avec état** de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dd131-147">Reopen the application that you created previously in Visual Studio, or create a new application by using the **Stateful Service** Visual Studio template.</span></span>
2. <span data-ttu-id="dd131-148">Ouvrez le fichier Stateful1.cs, puis recherchez l’appel `myDictionary.TryGetValueAsync` dans la méthode `RunAsync`.</span><span class="sxs-lookup"><span data-stu-id="dd131-148">Open the Stateful1.cs file, and find the `myDictionary.TryGetValueAsync` call in the `RunAsync` method.</span></span> <span data-ttu-id="dd131-149">La méthode renvoie un `result` contenant la valeur actuelle du compteur, car la logique principale de cette application est de tenir un décompte.</span><span class="sxs-lookup"><span data-stu-id="dd131-149">You can see that this method returns a `result` that holds the current value of the counter because the key logic in this application is to keep a count running.</span></span> <span data-ttu-id="dd131-150">S’il s’agissait d’une application réelle et que l’absence de résultat représentait un échec, il faudrait marquer cet événement.</span><span class="sxs-lookup"><span data-stu-id="dd131-150">If this were a real application, and if the lack of result represented a failure, you would want to flag that event.</span></span>
3. <span data-ttu-id="dd131-151">Pour signaler un événement d’état quand l’absence de résultat représente un échec, ajoutez les étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="dd131-151">To report a health event when the lack of result represents a failure, add the following steps.</span></span>
   
    <span data-ttu-id="dd131-152">a.</span><span class="sxs-lookup"><span data-stu-id="dd131-152">a.</span></span> <span data-ttu-id="dd131-153">Ajoutez l’espace de noms `System.Fabric.Health` au fichier Stateful1.cs.</span><span class="sxs-lookup"><span data-stu-id="dd131-153">Add the `System.Fabric.Health` namespace to the Stateful1.cs file.</span></span>
   
    ```csharp
    using System.Fabric.Health;
    ```
   
    <span data-ttu-id="dd131-154">b.</span><span class="sxs-lookup"><span data-stu-id="dd131-154">b.</span></span> <span data-ttu-id="dd131-155">Ajoutez le code suivant après l’appel `myDictionary.TryGetValueAsync`</span><span class="sxs-lookup"><span data-stu-id="dd131-155">Add the following code after the `myDictionary.TryGetValueAsync` call</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
    <span data-ttu-id="dd131-156">Nous signalons l’intégrité du réplica, car il provient d’un service avec état.</span><span class="sxs-lookup"><span data-stu-id="dd131-156">We report replica health because it's being reported from a stateful service.</span></span> <span data-ttu-id="dd131-157">Le paramètre `HealthInformation` stocke les informations relatives au problème d’intégrité signalé.</span><span class="sxs-lookup"><span data-stu-id="dd131-157">The `HealthInformation` parameter stores information about the health issue that's being reported.</span></span>
   
    <span data-ttu-id="dd131-158">Si vous aviez créé un service sans état, utilisez le code suivant</span><span class="sxs-lookup"><span data-stu-id="dd131-158">If you had created a stateless service, use the following code</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
    ```
4. <span data-ttu-id="dd131-159">Si votre service s’exécute avec des privilèges d’administrateur ou que le cluster n’est pas [sécurisé`FabricClient`, vous pouvez également utiliser ](service-fabric-cluster-security.md) pour signaler l’intégrité comme indiqué dans les étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="dd131-159">If your service is running with admin privileges or if the cluster is not [secure](service-fabric-cluster-security.md), you can also use `FabricClient` to report health as shown in the following steps.</span></span>  
   
    <span data-ttu-id="dd131-160">a.</span><span class="sxs-lookup"><span data-stu-id="dd131-160">a.</span></span> <span data-ttu-id="dd131-161">Créez l’instance `FabricClient` après la déclaration `var myDictionary`.</span><span class="sxs-lookup"><span data-stu-id="dd131-161">Create the `FabricClient` instance after the `var myDictionary` declaration.</span></span>
   
    ```csharp
    var fabricClient = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });
    ```
   
    <span data-ttu-id="dd131-162">b.</span><span class="sxs-lookup"><span data-stu-id="dd131-162">b.</span></span> <span data-ttu-id="dd131-163">Ajoutez le code suivant après l’appel `myDictionary.TryGetValueAsync` :</span><span class="sxs-lookup"><span data-stu-id="dd131-163">Add the following code after the `myDictionary.TryGetValueAsync` call.</span></span>
   
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
5. <span data-ttu-id="dd131-164">Simulons cette panne et voyons comment elle s’affiche dans les outils de contrôle d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="dd131-164">Let's simulate this failure and see it show up in the health monitoring tools.</span></span> <span data-ttu-id="dd131-165">Pour simuler la panne, commentez la première ligne dans le code de rapport d’intégrité ajouté précédemment.</span><span class="sxs-lookup"><span data-stu-id="dd131-165">To simulate the failure, comment out the first line in the health reporting code that you added earlier.</span></span> <span data-ttu-id="dd131-166">Une fois le commentaire ajouté à la première ligne, le code se présente comme suit.</span><span class="sxs-lookup"><span data-stu-id="dd131-166">After you comment out the first line, the code will look like the following example.</span></span>
   
    ```csharp
    //if(!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
   <span data-ttu-id="dd131-167">Ce code déclenche le rapport d’intégrité à chaque exécution de `RunAsync`.</span><span class="sxs-lookup"><span data-stu-id="dd131-167">This code fires the health report each time `RunAsync` executes.</span></span> <span data-ttu-id="dd131-168">Après avoir apporté la modification, appuyez sur **F5** pour exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="dd131-168">After you make the change, press **F5** to run the application.</span></span>
6. <span data-ttu-id="dd131-169">Une fois que l’application est en cours d’exécution, ouvrez Service Fabric Explorer pour vérifier l’intégrité de l’application.</span><span class="sxs-lookup"><span data-stu-id="dd131-169">After the application is running, open Service Fabric Explorer to check the health of the application.</span></span> <span data-ttu-id="dd131-170">Cette fois-ci, Service Fabric Explorer affiche un problème d’intégrité de l’application.</span><span class="sxs-lookup"><span data-stu-id="dd131-170">This time, Service Fabric Explorer shows that the application is unhealthy.</span></span> <span data-ttu-id="dd131-171">Ceci est dû à l’erreur signalée à partir du code que nous avons ajouté précédemment.</span><span class="sxs-lookup"><span data-stu-id="dd131-171">This is because of the error that was reported from the code that we added previously.</span></span>
   
    ![Application non saine dans l’Explorateur Service Fabric](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-unhealthy-app.png)
7. <span data-ttu-id="dd131-173">Si vous sélectionnez le réplica principal dans l’arborescence de Service Fabric Explorer, vous verrez que l’ **état d’intégrité** indique également une erreur.</span><span class="sxs-lookup"><span data-stu-id="dd131-173">If you select the primary replica in the tree view of Service Fabric Explorer, you will see that **Health State** indicates an error, too.</span></span> <span data-ttu-id="dd131-174">Service Fabric Explorer affiche également les détails du rapport d’intégrité qui ont été ajoutés au paramètre `HealthInformation` dans le code.</span><span class="sxs-lookup"><span data-stu-id="dd131-174">Service Fabric Explorer also displays the health report details that were added to the `HealthInformation` parameter in the code.</span></span> <span data-ttu-id="dd131-175">Vous pouvez voir les mêmes rapports d’intégrité dans PowerShell, ainsi que dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="dd131-175">You can see the same health reports in PowerShell and the Azure portal.</span></span>
   
    ![Intégrité du réplica dans l’Explorateur Service Fabric](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/replica-health-error-report-sfx.png)

<span data-ttu-id="dd131-177">Ce rapport est conservé dans Health Manager tant qu’il n’est pas remplacé par un autre rapport ou que ce réplica n’est pas supprimé.</span><span class="sxs-lookup"><span data-stu-id="dd131-177">This report remains in the health manager until it is replaced by another report or until this replica is deleted.</span></span> <span data-ttu-id="dd131-178">Étant donné que nous n’avons pas défini `TimeToLive` pour ce rapport d’intégrité dans l’objet `HealthInformation`, le rapport n’expire jamais.</span><span class="sxs-lookup"><span data-stu-id="dd131-178">Because we did not set `TimeToLive` for this health report in the `HealthInformation` object, the report never expires.</span></span>

<span data-ttu-id="dd131-179">Il est recommandé que l’intégrité soit signalée au niveau le plus granulaire, qui dans ce cas est le réplica.</span><span class="sxs-lookup"><span data-stu-id="dd131-179">We recommend that health should be reported on the most granular level, which in this case is the replica.</span></span> <span data-ttu-id="dd131-180">Vous pouvez également signaler l’intégrité sur `Partition`.</span><span class="sxs-lookup"><span data-stu-id="dd131-180">You can also report health on `Partition`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
this.Partition.ReportPartitionHealth(healthInformation);
```

<span data-ttu-id="dd131-181">Pour créer un rapport d’intégrité sur `Application`, `DeployedApplication` et `DeployedServicePackage`, utilisez `CodePackageActivationContext`.</span><span class="sxs-lookup"><span data-stu-id="dd131-181">To report health on `Application`, `DeployedApplication`, and `DeployedServicePackage`, use  `CodePackageActivationContext`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
var activationContext = FabricRuntime.GetActivationContext();
activationContext.ReportApplicationHealth(healthInformation);
```

## <a name="next-steps"></a><span data-ttu-id="dd131-182">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dd131-182">Next steps</span></span>
* [<span data-ttu-id="dd131-183">Présentation approfondie de l’intégrité de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="dd131-183">Deep dive on Service Fabric health</span></span>](service-fabric-health-introduction.md)
* [<span data-ttu-id="dd131-184">API REST pour les rapports d’intégrité du service</span><span class="sxs-lookup"><span data-stu-id="dd131-184">REST API for reporting service health</span></span>](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service)
* [<span data-ttu-id="dd131-185">API REST pour les rapports d’intégrité de l’application</span><span class="sxs-lookup"><span data-stu-id="dd131-185">REST API for reporting application health</span></span>](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-an-application)

