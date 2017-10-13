---
title: "Déboguer votre application dans Visual Studio | Microsoft Docs"
description: "Améliorez la fiabilité et les performances de vos services en les développant et en procédant à leur débogage dans Visual Studio sur un cluster de développement local."
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
ms.openlocfilehash: 2459025899a7f5ffebf44fa104ed112c0eb99dfa
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="debug-your-service-fabric-application-by-using-visual-studio"></a>Débogage de votre application Service Fabric à l’aide de Visual Studio
> [!div class="op_single_selector"]
> * [Visual Studio/CSharp](service-fabric-debugging-your-application.md) 
> * [Eclipse/Java](service-fabric-debugging-your-application-java.md)
>


## <a name="debug-a-local-service-fabric-application"></a>Débogage d’une application Service Fabric locale
Vous pouvez économiser du temps et de l’argent en déployant et déboguant votre application Azure Service Fabric dans un cluster de développement d’ordinateur local. Visual Studio 2017 et Visual Studio 2015 peuvent déployer l’application sur le cluster local et connecter automatiquement le débogueur à toutes les instances de votre application.

1. Démarrez un cluster de développement local en suivant les étapes de la section [Configuration de votre environnement de développement Service Fabric](service-fabric-get-started.md).
2. Appuyez sur **F5** ou cliquez sur **Déboguer** > **Démarrer le débogage**.
   
    ![Démarrer le débogage d'une application][startdebugging]
3. Définissez des points d’arrêt dans votre code et parcourez l’application en cliquant sur les commandes du menu **Déboguer** .
   
   > [!NOTE]
   > Visual Studio s'attache à toutes les instances de votre application. Pendant le parcours du code, les points d’arrêt peuvent être visités par plusieurs processus résultant de sessions simultanées. Essayez de désactiver les points d’arrêt une fois qu’ils ont été atteints en définissant le point d’arrêt comme étant conditionnel sur l’ID de thread ou en utilisant les événements de diagnostic.
   > 
   > 
4. La fenêtre **Événements de diagnostic** s’ouvre automatiquement et affiche les événements de diagnostic en temps réel.
   
    ![Afficher les événements de diagnostic en temps réel][diagnosticevents]
5. Vous pouvez également ouvrir la fenêtre **Événements de diagnostic** dans Cloud Explorer.  Sous **Service Fabric**, cliquez avec le bouton droit sur n’importe quel nœud et choisissez **Afficher les traces de diffusion en continu**.
   
    ![Ouvrir la fenêtre des événements de diagnostic][viewdiagnosticevents]
   
    Si vous souhaitez filtrer les traces en fonction d’une application ou d’un service spécifique, activez simplement les traces de diffusion en continu pour ce service ou cette application spécifique.
6. Les événements de diagnostics peuvent être consultés dans le fichier **ServiceEventSource.cs** , généré automatiquement, et sont appelés à partir du code d’application.
   
    ```csharp
    ServiceEventSource.Current.ServiceMessage(this, "My ServiceMessage with a parameter {0}", result.Value.ToString());
    ```
7. La fenêtre **Événements de diagnostic** prend en charge le filtrage, la suspension et l’inspection des événements en temps réel.  Le filtre est une simple recherche de chaîne du message d'événement, y compris son contenu.
   
    ![Filtrer, suspendre et reprendre ou examiner des événements en temps réel][diagnosticeventsactions]
8. Les services de débogage ont la même fonction que le débogage de toute autre application. Les points d’arrêt sont définis normalement via Visual Studio pour faciliter le débogage. Bien que les Reliable Collections sont répliquées sur plusieurs nœuds, elles implémentent toujours IEnumerable. Cela signifie que vous pouvez utiliser l’affichage des résultats dans Visual Studio pendant le débogage pour voir ce que vous avez stocké à l’intérieur. Définissez simplement un point d’arrêt n’importe où dans votre code.
   
    ![Démarrer le débogage d'une application][breakpoint]

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->

## <a name="debug-a-remote-service-fabric-application"></a>Débogage d’une application Service Fabric à distance
Si vos applications Service Fabric sont exécutées sur un cluster Service Fabric dans Azure, vous êtes en mesure de les déboguer à distance, directement à partir de Visual Studio.

> [!NOTE]
> La fonctionnalité nécessite le [Kit de développement logiciel (SDK) Service Fabric 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) et le [Kit de développement logiciel (SDK) Azure pour .NET 2.9](https://azure.microsoft.com/downloads/).    
> 
> 

<!-- -->
> [!WARNING]
> Le débogage à distance est destiné aux scénarios de développement/test et ne doit pas être utilisé dans des environnements de production, en raison de l’impact sur les applications exécutées.
> 
> 

1. Accédez à votre cluster dans **Cloud Explorer**, cliquez avec le bouton droit, puis choisissez **Activer le débogage**.
   
    ![Activer le débogage à distance][enableremotedebugging]
   
    Cette opération démarre le processus d’activation de l’extension de débogage à distance sur vos nœuds de cluster, ainsi que les configurations réseau nécessaires.
2. Cliquez avec le bouton droit sur le nœud de cluster dans **Cloud Explorer**, puis choisissez **Attacher le débogueur**.
   
    ![Attacher le débogueur][attachdebugger]
3. Dans la boîte de dialogue **Attacher au processus**, choisissez le processus à déboguer, puis cliquez sur **Attacher**.
   
    ![Choisir le processus][chooseprocess]
   
    Le nom du processus auquel le débogage est attaché est identique au nom d’assembly de votre projet service.
   
    Le débogueur s’attache à tous les nœuds qui exécutent le processus.
   
   * Si vous déboguez un service sans état, toutes les instances du service sur tous les nœuds font partie de la session de débogage.
   * Si vous déboguez un service avec état, seul le réplica principal d’une partition sera actif et par conséquent capturé par le débogueur. Si le réplica principal se déplace pendant la session de débogage, le traitement de ce réplica fera toujours partie de la session de débogage.
   * Afin d’intercepter uniquement les partitions ou les instances concernées d’un service donné, vous pouvez utiliser des points d’arrêt conditionnels pour n’arrêter qu’une instance ou une partition spécifique.
     
     ![Point d’arrêt conditionnel][conditionalbreakpoint]
     
     > [!NOTE]
     > Actuellement, nous ne prenons pas en charge le débogage d’un cluster Service Fabric avec plusieurs instances du même nom d’exécutable de service.
     > 
     > 
4. Une fois que vous avez terminé de déboguer votre application, vous pouvez désactiver l’extension de débogage à distance en cliquant avec le bouton droit sur le cluster dans **Cloud Explorer** et en choisissant **Désactiver le débogage**.
   
    ![Désactiver le débogage à distance][disableremotedebugging]

## <a name="streaming-traces-from-a-remote-cluster-node"></a>Traces de diffusion en continu à partir d’un nœud de cluster à distance
Vous pouvez également diffuser en continu des traces directement à partir d’un nœud de cluster à distance vers Visual Studio. Cette fonctionnalité vous permet de diffuser des événements de trace ETW, générés sur un nœud de cluster Service Fabric.

> [!NOTE]
> Cette fonctionnalité nécessite le [Kit de développement logiciel (SDK) Service Fabric 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) et le [Kit de développement logiciel (SDK) Azure pour .NET 2.9](https://azure.microsoft.com/downloads/).
> Cette fonctionnalité prend uniquement en charge les clusters exécutés dans Azure.
> 
> 

<!-- -->
> [!WARNING]
> Les traces de diffusion en continu sont destinées aux scénarios de développement/test et ne doivent pas être utilisées dans des environnements de production, en raison de l’impact sur les applications exécutées.
> Dans un scénario de production, vous devez utiliser le transfert d’événements à l’aide d’Azure Diagnostics.
> 
> 

1. Accédez à votre cluster dans **Cloud Explorer**, cliquez avec le bouton droit, puis choisissez **Activer les traces de diffusion en continu**.
   
    ![Activer les traces de diffusion en continu à distance][enablestreamingtraces]
   
    Cette opération démarre le processus d’activation de l’extension des traces de diffusion en continu sur vos nœuds de cluster, ainsi que les configurations réseau nécessaires.
2. Développez l’élément **Nœuds** dans **Cloud Explorer**, cliquez avec le bouton droit sur le nœud à partir duquel diffuser les traces en continu, puis choisissez **Afficher les traces de diffusion en continu**.
   
    ![Afficher les traces de diffusion en continu à distance][viewremotestreamingtraces]
   
    Répétez l’étape 2 pour tous les nœuds pour lesquels vous voulez afficher les traces. Chaque flux de nœud s’affiche dans une fenêtre dédiée.
   
    Vous êtes maintenant en mesure de voir les traces émises par Service Fabric et vos services. Si vous souhaitez filtrer les événements pour afficher uniquement une application spécifique, tapez simplement le nom de l’application dans le filtre.
   
    ![Afficher les traces de diffusion en continu][viewingstreamingtraces]
3. Lorsque vous avez terminé de diffuser les traces à partir de votre cluster, vous pouvez désactiver les traces de diffusion en continu à distance, en cliquant avec le bouton droit sur le cluster dans **Cloud Explorer** et en choisissant **Désactiver les traces de diffusion en continu**.
   
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
