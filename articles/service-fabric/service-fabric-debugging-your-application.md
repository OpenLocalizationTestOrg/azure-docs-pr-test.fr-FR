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
# <a name="debug-your-service-fabric-application-by-using-visual-studio"></a>Débogage de votre application Service Fabric à l’aide de Visual Studio
> [!div class="op_single_selector"]
> * [Visual Studio/CSharp](service-fabric-debugging-your-application.md) 
> * [Eclipse/Java](service-fabric-debugging-your-application-java.md)
>


## <a name="debug-a-local-service-fabric-application"></a>Débogage d’une application Service Fabric locale
Vous pouvez économiser du temps et de l’argent en déployant et déboguant votre application Azure Service Fabric dans un cluster de développement d’ordinateur local. Visual Studio 2017 ou Visual Studio 2015 peut déployer le cluster local du toohello application hello et se connecter automatiquement les instances de tooall hello débogueur de votre application.

1. Démarrer un cluster de développement local en suivant les étapes de hello dans [configuration de votre environnement de développement Service Fabric](service-fabric-get-started.md).
2. Appuyez sur **F5** ou cliquez sur **Déboguer** > **Démarrer le débogage**.
   
    ![Démarrer le débogage d'une application][startdebugging]
3. Définir des points d’arrêt dans votre code et les étapes à l’application hello en cliquant sur les commandes Bonjour **déboguer** menu.
   
   > [!NOTE]
   > Visual Studio attache tooall des instances de votre application. Pendant le parcours du code, les points d’arrêt peuvent être visités par plusieurs processus résultant de sessions simultanées. Essayez de désactiver des points d’arrêt hello après qu’ils vous atteint, faisant de chaque point d’arrêt conditionnel sur l’ID de thread hello ou à l’aide d’événements de diagnostic.
   > 
   > 
4. Hello **des événements de Diagnostic** fenêtre s’ouvre automatiquement afin que vous puissiez afficher des événements de diagnostic en temps réel.
   
    ![Afficher les événements de diagnostic en temps réel][diagnosticevents]
5. Vous pouvez également ouvrir hello **des événements de Diagnostic** fenêtre dans l’Explorateur de Cloud.  Sous **Service Fabric**, cliquez avec le bouton droit sur n’importe quel nœud et choisissez **Afficher les traces de diffusion en continu**.
   
    ![Fenêtre des événements de diagnostic hello ouvert][viewdiagnosticevents]
   
    Si vous souhaitez toofilter votre service de traces tooa spécifique ou d’une application, activez simplement la diffusion en continu des traces sur cette application ou un service particulier.
6. les événements de diagnostic Hello peuvent être consultés dans hello généré automatiquement **ServiceEventSource.cs** de fichiers et sont appelées à partir de code d’application.
   
    ```csharp
    ServiceEventSource.Current.ServiceMessage(this, "My ServiceMessage with a parameter {0}", result.Value.ToString());
    ```
7. Hello **des événements de Diagnostic** fenêtre prend en charge le filtrage, la suspension et l’inspection des événements en temps réel.  filtre de Hello est une recherche de chaîne simple hello message d’événement, y compris son contenu.
   
    ![Filtrer, suspendre et reprendre ou examiner des événements en temps réel][diagnosticeventsactions]
8. Les services de débogage ont la même fonction que le débogage de toute autre application. Les points d’arrêt sont définis normalement via Visual Studio pour faciliter le débogage. Bien que les Reliable Collections sont répliquées sur plusieurs nœuds, elles implémentent toujours IEnumerable. Cela signifie que vous pouvez utiliser hello affichage des résultats dans Visual Studio pendant le débogage toosee ce que vous avez stocké à l’intérieur. Définissez simplement un point d’arrêt n’importe où dans votre code.
   
    ![Démarrer le débogage d'une application][breakpoint]

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="debug-a-remote-service-fabric-application"></a>Débogage d’une application Service Fabric à distance
Si vos applications de Service Fabric sont exécutent sur un cluster Service Fabric dans Azure, vous ne pouvez tooremotely déboguer ces, directement à partir de Visual Studio.

> [!NOTE]
> fonctionnalité de Hello requiert [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) et [Azure SDK pour .NET 2.9](https://azure.microsoft.com/downloads/).    
> 
> 

<!-- -->
> [!WARNING]
> Débogage à distance est destiné aux scénarios de développement/test et toobe pas les utiliser dans les environnements de production, en raison de l’impact hello sur hello applications en cours d’exécution.
> 
> 

1. Accédez cluster tooyour dans **Cloud Explorer**, avec le bouton droit et choisissez **activer le débogage**
   
    ![Activer le débogage à distance][enableremotedebugging]
   
    Cela lancera hors processus hello d’activation hello extension sur vos nœuds de cluster du débogage distant, ainsi que des configurations de réseau requises.
2. Nœud de cluster avec le bouton hello dans **Cloud Explorer**, puis choisissez **attacher le débogueur**
   
    ![Attacher le débogueur][attachdebugger]
3. Bonjour **attacher tooprocess** boîte de dialogue, sélectionnez hello processus que vous souhaitez toodebug, puis cliquez sur **attacher**
   
    ![Choisir le processus][chooseprocess]
   
    nom de Hello du processus de hello vous tooattach à, égal à hello nom de l’assembly du projet de service.
   
    débogueur de Hello attachera nœuds tooall en cours d’exécution des processus de hello.
   
   * Dans les cas de hello où vous déboguez un service sans état, toutes les instances de service hello sur tous les nœuds font partie de la session de débogage de hello.
   * Si vous déboguez un service avec état, uniquement hello réplica principal d’une partition sera par conséquent interceptée par le débogueur de hello et active. Si le réplica principal de hello se déplace pendant la session de débogage de hello, traitement hello de ce réplica sera toujours partie de la session de débogage de hello.
   * Dans des partitions concernées ordre tooonly catch ou des instances d’un service donné, vous pouvez utiliser des points d’arrêt conditionnels tooonly saut une partition spécifique ou instance.
     
     ![Point d’arrêt conditionnel][conditionalbreakpoint]
     
     > [!NOTE]
     > Actuellement nous ne pas en charge un cluster Service Fabric avec plusieurs instances de hello de débogage même nom de service exécutable.
     > 
     > 
4. Une fois que vous avez terminé de déboguer votre application, vous pouvez désactiver l’extension de débogage distant hello en double-cliquant sur le cluster hello dans **Cloud Explorer** et choisissez **désactiver le débogage**
   
    ![Désactiver le débogage à distance][disableremotedebugging]

## <a name="streaming-traces-from-a-remote-cluster-node"></a>Traces de diffusion en continu à partir d’un nœud de cluster à distance
Vous êtes également en mesure de toostream des traces directement à partir d’un tooVisual de nœud de cluster distant Studio. Cette fonctionnalité vous permet d’événements de trace ETW toostream, générés sur un nœud de cluster Service Fabric.

> [!NOTE]
> Cette fonctionnalité nécessite le [Kit de développement logiciel (SDK) Service Fabric 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) et le [Kit de développement logiciel (SDK) Azure pour .NET 2.9](https://azure.microsoft.com/downloads/).
> Cette fonctionnalité prend uniquement en charge les clusters exécutés dans Azure.
> 
> 

<!-- -->
> [!WARNING]
> Diffusion en continu des traces est destinée aux scénarios de développement/test et de toobe pas les utiliser dans les environnements de production, en raison de l’impact hello sur hello applications en cours d’exécution.
> Dans un scénario de production, vous devez utiliser le transfert d’événements à l’aide d’Azure Diagnostics.
> 
> 

1. Accédez cluster tooyour dans **Cloud Explorer**, avec le bouton droit et choisissez **activer les Traces de diffusion en continu**
   
    ![Activer les traces de diffusion en continu à distance][enablestreamingtraces]
   
    Cela lancera hors processus hello d’activation hello de diffusion en continu d’extension de traces sur vos nœuds de cluster, ainsi que des configurations de réseau requises.
2. Développez hello **nœuds** élément **Cloud Explorer**, nœud de hello avec le bouton toostream des traces à partir de puis choisissez **des Traces de diffusion en continu de la vue**
   
    ![Afficher les traces de diffusion en continu à distance][viewremotestreamingtraces]
   
    Répétez l’étape 2 pour autant de nœuds que vous le souhaitez toosee des traces à partir de. Chaque flux de nœud s’affiche dans une fenêtre dédiée.
   
    Vous êtes maintenant toosee en mesure de traces de hello émis par l’infrastructure de Service et vos services. Si vous souhaitez toofilter hello événements tooonly afficher une application spécifique, tapez simplement nom hello d’application hello dans le filtre de hello.
   
    ![Afficher les traces de diffusion en continu][viewingstreamingtraces]
3. Une fois que vous avez terminé les traces de diffusion en continu à partir de votre cluster, vous pouvez désactiver les traces de diffusion en continu à distance, en double-cliquant sur le cluster hello dans **Cloud Explorer** et choisissez **désactiver les Traces de diffusion en continu**
   
    ![Désactiver les traces de diffusion en continu à distance][disablestreamingtraces]

## <a name="next-steps"></a>Étapes suivantes
* [Tester un service Service Fabric](service-fabric-testability-overview.md).
* [Gérer vos applications Service Fabric dans Visual Studio](service-fabric-manage-application-in-visual-studio.md).

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
