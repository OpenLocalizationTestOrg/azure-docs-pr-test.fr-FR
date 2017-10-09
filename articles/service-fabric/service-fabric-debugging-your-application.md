---
title: aaaDebug votre application dans Visual Studio | Documents Microsoft
description: "Améliorer la fiabilité de hello et les performances de vos services en développant et en leur débogage dans Visual Studio sur un cluster de développement local."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: cb888532-bcdb-4e47-95e4-bfbb1f644da4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: vturecek;mikhegn
ms.openlocfilehash: 8d08689e82195d09f57b462631ad04fd237bc4fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-service-fabric-application-by-using-visual-studio"></a><span data-ttu-id="2e279-103">Débogage de votre application Service Fabric à l’aide de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2e279-103">Debug your Service Fabric application by using Visual Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2e279-104">Visual Studio/CSharp</span><span class="sxs-lookup"><span data-stu-id="2e279-104">Visual Studio/CSharp</span></span>](service-fabric-debugging-your-application.md) 
> * [<span data-ttu-id="2e279-105">Eclipse/Java</span><span class="sxs-lookup"><span data-stu-id="2e279-105">Eclipse/Java</span></span>](service-fabric-debugging-your-application-java.md)
>


## <a name="debug-a-local-service-fabric-application"></a><span data-ttu-id="2e279-106">Débogage d’une application Service Fabric locale</span><span class="sxs-lookup"><span data-stu-id="2e279-106">Debug a local Service Fabric application</span></span>
<span data-ttu-id="2e279-107">Vous pouvez économiser du temps et de l’argent en déployant et déboguant votre application Azure Service Fabric dans un cluster de développement d’ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="2e279-107">You can save time and money by deploying and debugging your Azure Service Fabric application in a local computer development cluster.</span></span> <span data-ttu-id="2e279-108">Visual Studio 2017 ou Visual Studio 2015 peut déployer le cluster local du toohello application hello et se connecter automatiquement les instances de tooall hello débogueur de votre application.</span><span class="sxs-lookup"><span data-stu-id="2e279-108">Visual Studio 2017 or Visual Studio 2015 can deploy hello application toohello local cluster and automatically connect hello debugger tooall instances of your application.</span></span>

1. <span data-ttu-id="2e279-109">Démarrer un cluster de développement local en suivant les étapes de hello dans [configuration de votre environnement de développement Service Fabric](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2e279-109">Start a local development cluster by following hello steps in [Setting up your Service Fabric development environment](service-fabric-get-started.md).</span></span>
2. <span data-ttu-id="2e279-110">Appuyez sur **F5** ou cliquez sur **Déboguer** > **Démarrer le débogage**.</span><span class="sxs-lookup"><span data-stu-id="2e279-110">Press **F5** or click **Debug** > **Start Debugging**.</span></span>
   
    ![Démarrer le débogage d'une application][startdebugging]
3. <span data-ttu-id="2e279-112">Définir des points d’arrêt dans votre code et les étapes à l’application hello en cliquant sur les commandes Bonjour **déboguer** menu.</span><span class="sxs-lookup"><span data-stu-id="2e279-112">Set breakpoints in your code and step through hello application by clicking commands in hello **Debug** menu.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="2e279-113">Visual Studio attache tooall des instances de votre application.</span><span class="sxs-lookup"><span data-stu-id="2e279-113">Visual Studio attaches tooall instances of your application.</span></span> <span data-ttu-id="2e279-114">Pendant le parcours du code, les points d’arrêt peuvent être visités par plusieurs processus résultant de sessions simultanées.</span><span class="sxs-lookup"><span data-stu-id="2e279-114">While you're stepping through code, breakpoints may get hit by multiple processes resulting in concurrent sessions.</span></span> <span data-ttu-id="2e279-115">Essayez de désactiver des points d’arrêt hello après qu’ils vous atteint, faisant de chaque point d’arrêt conditionnel sur l’ID de thread hello ou à l’aide d’événements de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="2e279-115">Try disabling hello breakpoints after they're hit, by making each breakpoint conditional on hello thread ID or by using diagnostic events.</span></span>
   > 
   > 
4. <span data-ttu-id="2e279-116">Hello **des événements de Diagnostic** fenêtre s’ouvre automatiquement afin que vous puissiez afficher des événements de diagnostic en temps réel.</span><span class="sxs-lookup"><span data-stu-id="2e279-116">hello **Diagnostic Events** window will automatically open so you can view diagnostic events in real time.</span></span>
   
    ![Afficher les événements de diagnostic en temps réel][diagnosticevents]
5. <span data-ttu-id="2e279-118">Vous pouvez également ouvrir hello **des événements de Diagnostic** fenêtre dans l’Explorateur de Cloud.</span><span class="sxs-lookup"><span data-stu-id="2e279-118">You can also open hello **Diagnostic Events** window in Cloud Explorer.</span></span>  <span data-ttu-id="2e279-119">Sous **Service Fabric**, cliquez avec le bouton droit sur n’importe quel nœud et choisissez **Afficher les traces de diffusion en continu**.</span><span class="sxs-lookup"><span data-stu-id="2e279-119">Under **Service Fabric**, right-click any node and choose **View Streaming Traces**.</span></span>
   
    ![Fenêtre des événements de diagnostic hello ouvert][viewdiagnosticevents]
   
    <span data-ttu-id="2e279-121">Si vous souhaitez toofilter votre service de traces tooa spécifique ou d’une application, activez simplement la diffusion en continu des traces sur cette application ou un service particulier.</span><span class="sxs-lookup"><span data-stu-id="2e279-121">If you want toofilter your traces tooa specific service or application, simply enable streaming traces on that specific service or application.</span></span>
6. <span data-ttu-id="2e279-122">les événements de diagnostic Hello peuvent être consultés dans hello généré automatiquement **ServiceEventSource.cs** de fichiers et sont appelées à partir de code d’application.</span><span class="sxs-lookup"><span data-stu-id="2e279-122">hello diagnostic events can be seen in hello automatically generated **ServiceEventSource.cs** file and are called from application code.</span></span>
   
    ```csharp
    ServiceEventSource.Current.ServiceMessage(this, "My ServiceMessage with a parameter {0}", result.Value.ToString());
    ```
7. <span data-ttu-id="2e279-123">Hello **des événements de Diagnostic** fenêtre prend en charge le filtrage, la suspension et l’inspection des événements en temps réel.</span><span class="sxs-lookup"><span data-stu-id="2e279-123">hello **Diagnostic Events** window supports filtering, pausing, and inspecting events in real time.</span></span>  <span data-ttu-id="2e279-124">filtre de Hello est une recherche de chaîne simple hello message d’événement, y compris son contenu.</span><span class="sxs-lookup"><span data-stu-id="2e279-124">hello filter is a simple string search of hello event message, including its contents.</span></span>
   
    ![Filtrer, suspendre et reprendre ou examiner des événements en temps réel][diagnosticeventsactions]
8. <span data-ttu-id="2e279-126">Les services de débogage ont la même fonction que le débogage de toute autre application.</span><span class="sxs-lookup"><span data-stu-id="2e279-126">Debugging services is like debugging any other application.</span></span> <span data-ttu-id="2e279-127">Les points d’arrêt sont définis normalement via Visual Studio pour faciliter le débogage.</span><span class="sxs-lookup"><span data-stu-id="2e279-127">You will normally set Breakpoints through Visual Studio for easy debugging.</span></span> <span data-ttu-id="2e279-128">Bien que les Reliable Collections sont répliquées sur plusieurs nœuds, elles implémentent toujours IEnumerable.</span><span class="sxs-lookup"><span data-stu-id="2e279-128">Even though Reliable Collections replicate across multiple nodes, they still implement IEnumerable.</span></span> <span data-ttu-id="2e279-129">Cela signifie que vous pouvez utiliser hello affichage des résultats dans Visual Studio pendant le débogage toosee ce que vous avez stocké à l’intérieur.</span><span class="sxs-lookup"><span data-stu-id="2e279-129">This means that you can use hello Results View in Visual Studio while debugging toosee what you've stored inside.</span></span> <span data-ttu-id="2e279-130">Définissez simplement un point d’arrêt n’importe où dans votre code.</span><span class="sxs-lookup"><span data-stu-id="2e279-130">Simply set a breakpoint anywhere in your code.</span></span>
   
    ![Démarrer le débogage d'une application][breakpoint]

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="debug-a-remote-service-fabric-application"></a><span data-ttu-id="2e279-132">Débogage d’une application Service Fabric à distance</span><span class="sxs-lookup"><span data-stu-id="2e279-132">Debug a remote Service Fabric application</span></span>
<span data-ttu-id="2e279-133">Si vos applications de Service Fabric sont exécutent sur un cluster Service Fabric dans Azure, vous ne pouvez tooremotely déboguer ces, directement à partir de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2e279-133">If your Service Fabric applications are running on a Service Fabric cluster in Azure, you are able tooremotely debug these, directly from Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="2e279-134">fonctionnalité de Hello requiert [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) et [Azure SDK pour .NET 2.9](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="2e279-134">hello feature requires [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) and [Azure SDK for .NET 2.9](https://azure.microsoft.com/downloads/).</span></span>    
> 
> 

<!-- -->
> [!WARNING]
> <span data-ttu-id="2e279-135">Débogage à distance est destiné aux scénarios de développement/test et toobe pas les utiliser dans les environnements de production, en raison de l’impact hello sur hello applications en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="2e279-135">Remote debugging is meant for dev/test scenarios and not toobe used in production environments, because of hello impact on hello running applications.</span></span>
> 
> 

1. <span data-ttu-id="2e279-136">Accédez cluster tooyour dans **Cloud Explorer**, avec le bouton droit et choisissez **activer le débogage**</span><span class="sxs-lookup"><span data-stu-id="2e279-136">Navigate tooyour cluster in **Cloud Explorer**, right-click and choose **Enable Debugging**</span></span>
   
    ![Activer le débogage à distance][enableremotedebugging]
   
    <span data-ttu-id="2e279-138">Cela lancera hors processus hello d’activation hello extension sur vos nœuds de cluster du débogage distant, ainsi que des configurations de réseau requises.</span><span class="sxs-lookup"><span data-stu-id="2e279-138">This will kick off hello process of enabling hello remote debugging extension on your cluster nodes, as well as required network configurations.</span></span>
2. <span data-ttu-id="2e279-139">Nœud de cluster avec le bouton hello dans **Cloud Explorer**, puis choisissez **attacher le débogueur**</span><span class="sxs-lookup"><span data-stu-id="2e279-139">Right-click hello cluster node in **Cloud Explorer**, and choose **Attach Debugger**</span></span>
   
    ![Attacher le débogueur][attachdebugger]
3. <span data-ttu-id="2e279-141">Bonjour **attacher tooprocess** boîte de dialogue, sélectionnez hello processus que vous souhaitez toodebug, puis cliquez sur **attacher**</span><span class="sxs-lookup"><span data-stu-id="2e279-141">In hello **Attach tooprocess** dialog, choose hello process you want toodebug, and click **Attach**</span></span>
   
    ![Choisir le processus][chooseprocess]
   
    <span data-ttu-id="2e279-143">nom de Hello du processus de hello vous tooattach à, égal à hello nom de l’assembly du projet de service.</span><span class="sxs-lookup"><span data-stu-id="2e279-143">hello name of hello process you want tooattach to, equals hello name of your service project assembly name.</span></span>
   
    <span data-ttu-id="2e279-144">débogueur de Hello attachera nœuds tooall en cours d’exécution des processus de hello.</span><span class="sxs-lookup"><span data-stu-id="2e279-144">hello debugger will attach tooall nodes running hello process.</span></span>
   
   * <span data-ttu-id="2e279-145">Dans les cas de hello où vous déboguez un service sans état, toutes les instances de service hello sur tous les nœuds font partie de la session de débogage de hello.</span><span class="sxs-lookup"><span data-stu-id="2e279-145">In hello case where you are debugging a stateless service, all instances of hello service on all nodes are part of hello debug session.</span></span>
   * <span data-ttu-id="2e279-146">Si vous déboguez un service avec état, uniquement hello réplica principal d’une partition sera par conséquent interceptée par le débogueur de hello et active.</span><span class="sxs-lookup"><span data-stu-id="2e279-146">If you are debugging a stateful service, only hello primary replica of any partition will be active and therefore caught by hello debugger.</span></span> <span data-ttu-id="2e279-147">Si le réplica principal de hello se déplace pendant la session de débogage de hello, traitement hello de ce réplica sera toujours partie de la session de débogage de hello.</span><span class="sxs-lookup"><span data-stu-id="2e279-147">If hello primary replica moves during hello debug session, hello processing of that replica will still be part of hello debug session.</span></span>
   * <span data-ttu-id="2e279-148">Dans des partitions concernées ordre tooonly catch ou des instances d’un service donné, vous pouvez utiliser des points d’arrêt conditionnels tooonly saut une partition spécifique ou instance.</span><span class="sxs-lookup"><span data-stu-id="2e279-148">In order tooonly catch relevant partitions or instances of a given service, you can use conditional breakpoints tooonly break a specific partition or instance.</span></span>
     
     ![Point d’arrêt conditionnel][conditionalbreakpoint]
     
     > [!NOTE]
     > <span data-ttu-id="2e279-150">Actuellement nous ne pas en charge un cluster Service Fabric avec plusieurs instances de hello de débogage même nom de service exécutable.</span><span class="sxs-lookup"><span data-stu-id="2e279-150">Currently we do not support debugging a Service Fabric cluster with multiple instances of hello same service executable name.</span></span>
     > 
     > 
4. <span data-ttu-id="2e279-151">Une fois que vous avez terminé de déboguer votre application, vous pouvez désactiver l’extension de débogage distant hello en double-cliquant sur le cluster hello dans **Cloud Explorer** et choisissez **désactiver le débogage**</span><span class="sxs-lookup"><span data-stu-id="2e279-151">Once you finish debugging your application, you can disable hello remote debugging extension by right-clicking hello cluster in **Cloud Explorer** and choose **Disable Debugging**</span></span>
   
    ![Désactiver le débogage à distance][disableremotedebugging]

## <a name="streaming-traces-from-a-remote-cluster-node"></a><span data-ttu-id="2e279-153">Traces de diffusion en continu à partir d’un nœud de cluster à distance</span><span class="sxs-lookup"><span data-stu-id="2e279-153">Streaming traces from a remote cluster node</span></span>
<span data-ttu-id="2e279-154">Vous êtes également en mesure de toostream des traces directement à partir d’un tooVisual de nœud de cluster distant Studio.</span><span class="sxs-lookup"><span data-stu-id="2e279-154">You are also able toostream traces directly from a remote cluster node tooVisual Studio.</span></span> <span data-ttu-id="2e279-155">Cette fonctionnalité vous permet d’événements de trace ETW toostream, générés sur un nœud de cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2e279-155">This feature allows you toostream ETW trace events, produced on a Service Fabric cluster node.</span></span>

> [!NOTE]
> <span data-ttu-id="2e279-156">Cette fonctionnalité nécessite le [Kit de développement logiciel (SDK) Service Fabric 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) et le [Kit de développement logiciel (SDK) Azure pour .NET 2.9](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="2e279-156">This feature requires [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) and [Azure SDK for .NET 2.9](https://azure.microsoft.com/downloads/).</span></span>
> <span data-ttu-id="2e279-157">Cette fonctionnalité prend uniquement en charge les clusters exécutés dans Azure.</span><span class="sxs-lookup"><span data-stu-id="2e279-157">This feature only supports clusters running in Azure.</span></span>
> 
> 

<!-- -->
> [!WARNING]
> <span data-ttu-id="2e279-158">Diffusion en continu des traces est destinée aux scénarios de développement/test et de toobe pas les utiliser dans les environnements de production, en raison de l’impact hello sur hello applications en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="2e279-158">Streaming traces is meant for dev/test scenarios and not toobe used in production environments, because of hello impact on hello running applications.</span></span>
> <span data-ttu-id="2e279-159">Dans un scénario de production, vous devez utiliser le transfert d’événements à l’aide d’Azure Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="2e279-159">In a production scenario, you should rely on forwarding events using Azure Diagnostics.</span></span>
> 
> 

1. <span data-ttu-id="2e279-160">Accédez cluster tooyour dans **Cloud Explorer**, avec le bouton droit et choisissez **activer les Traces de diffusion en continu**</span><span class="sxs-lookup"><span data-stu-id="2e279-160">Navigate tooyour cluster in **Cloud Explorer**, right-click and choose **Enable Streaming Traces**</span></span>
   
    ![Activer les traces de diffusion en continu à distance][enablestreamingtraces]
   
    <span data-ttu-id="2e279-162">Cela lancera hors processus hello d’activation hello de diffusion en continu d’extension de traces sur vos nœuds de cluster, ainsi que des configurations de réseau requises.</span><span class="sxs-lookup"><span data-stu-id="2e279-162">This will kick off hello process of enabling hello streaming traces extension on your cluster nodes, as well as required network configurations.</span></span>
2. <span data-ttu-id="2e279-163">Développez hello **nœuds** élément **Cloud Explorer**, nœud de hello avec le bouton toostream des traces à partir de puis choisissez **des Traces de diffusion en continu de la vue**</span><span class="sxs-lookup"><span data-stu-id="2e279-163">Expand hello **Nodes** element in **Cloud Explorer**, right-click hello node you want toostream traces from and choose **View Streaming Traces**</span></span>
   
    ![Afficher les traces de diffusion en continu à distance][viewremotestreamingtraces]
   
    <span data-ttu-id="2e279-165">Répétez l’étape 2 pour autant de nœuds que vous le souhaitez toosee des traces à partir de.</span><span class="sxs-lookup"><span data-stu-id="2e279-165">Repeat step 2 for as many nodes as you want toosee traces from.</span></span> <span data-ttu-id="2e279-166">Chaque flux de nœud s’affiche dans une fenêtre dédiée.</span><span class="sxs-lookup"><span data-stu-id="2e279-166">Each nodes stream will show up in a dedicated window.</span></span>
   
    <span data-ttu-id="2e279-167">Vous êtes maintenant toosee en mesure de traces de hello émis par l’infrastructure de Service et vos services.</span><span class="sxs-lookup"><span data-stu-id="2e279-167">You are now able toosee hello traces emitted by Service Fabric, and your services.</span></span> <span data-ttu-id="2e279-168">Si vous souhaitez toofilter hello événements tooonly afficher une application spécifique, tapez simplement nom hello d’application hello dans le filtre de hello.</span><span class="sxs-lookup"><span data-stu-id="2e279-168">If you want toofilter hello events tooonly show a specific application, simply type in hello name of hello application in hello filter.</span></span>
   
    ![Afficher les traces de diffusion en continu][viewingstreamingtraces]
3. <span data-ttu-id="2e279-170">Une fois que vous avez terminé les traces de diffusion en continu à partir de votre cluster, vous pouvez désactiver les traces de diffusion en continu à distance, en double-cliquant sur le cluster hello dans **Cloud Explorer** et choisissez **désactiver les Traces de diffusion en continu**</span><span class="sxs-lookup"><span data-stu-id="2e279-170">Once you are done streaming traces from your cluster, you can disable remote streaming traces, by right-clicking hello cluster in **Cloud Explorer** and choose **Disable Streaming Traces**</span></span>
   
    ![Désactiver les traces de diffusion en continu à distance][disablestreamingtraces]

## <a name="next-steps"></a><span data-ttu-id="2e279-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2e279-172">Next steps</span></span>
* <span data-ttu-id="2e279-173">[Tester un service Service Fabric](service-fabric-testability-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2e279-173">[Test a Service Fabric service](service-fabric-testability-overview.md).</span></span>
* <span data-ttu-id="2e279-174">[Gérer vos applications Service Fabric dans Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="2e279-174">[Manage your Service Fabric applications in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span></span>

<!--Image references-->
[startdebugging]: ./media/service-fabric-debugging-your-application/startdebugging.png
[diagnosticevents]: ./media/service-fabric-debugging-your-application/diagnosticevents.png
[viewdiagnosticevents]: ./media/service-fabric-debugging-your-application/viewdiagnosticevents.png
[diagnosticeventsactions]: ./media/service-fabric-debugging-your-application/diagnosticeventsactions.png
[breakpoint]: ./media/service-fabric-debugging-your-application/breakpoint.png
[enableremotedebugging]: ./media/service-fabric-debugging-your-application/enableremotedebugging.png
[attachdebugger]: ./media/service-fabric-debugging-your-application/attachdebugger.png
[chooseprocess]: ./media/service-fabric-debugging-your-application/chooseprocess.png
[conditionalbreakpoint]: ./media/service-fabric-debugging-your-application/conditionalbreakpoint.png
[disableremotedebugging]: ./media/service-fabric-debugging-your-application/disableremotedebugging.png
[enablestreamingtraces]: ./media/service-fabric-debugging-your-application/enablestreamingtraces.png
[viewingstreamingtraces]: ./media/service-fabric-debugging-your-application/viewingstreamingtraces.png
[viewremotestreamingtraces]: ./media/service-fabric-debugging-your-application/viewremotestreamingtraces.png
[disablestreamingtraces]: ./media/service-fabric-debugging-your-application/disablestreamingtraces.png
