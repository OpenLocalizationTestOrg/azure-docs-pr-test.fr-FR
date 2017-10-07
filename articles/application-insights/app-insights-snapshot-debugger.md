---
title: "aaaAzure Application Insights instantané débogueur pour les applications .NET | Documents Microsoft"
description: "Des captures instantanées de débogage sont collectées automatiquement lorsque des exceptions sont levées dans des applications .NET de production"
services: application-insights
documentationcenter: 
author: qubitron
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: bwren
ms.openlocfilehash: f0173a752b5795d934fbab1bd53eb077433edc90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-snapshots-on-exceptions-in-net-apps"></a>Captures instantanées de débogage sur exceptions levées dans des applications .NET

Quand une exception se produit, vous pouvez collecter automatiquement une capture instantanée de débogage à partir de votre application web dynamique. l’instantané Hello affiche état hello du code source et les variables à l’exception de hello moment hello a été levée. Hello instantané débogueur (version préliminaire) dans [Azure Application Insights](app-insights-overview.md) surveille la télémétrie des exceptions à partir de votre application web. Il collecte des captures instantanées sur vos exceptions levées en haut afin que les informations hello problèmes toodiagnose en production. Inclure hello [package NuGet de collecteur instantané](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) dans votre application et éventuellement configurer les paramètres de collecte dans [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Instantanés apparaissent sur [exceptions](app-insights-asp-net-exceptions.md) portail Application Insights de hello.

Vous pouvez afficher des instantanés de débogage dans la pile des appels hello toosee portail hello et inspecter des variables à chaque frame de pile des appels. tooget une expérience de débogage plus puissante avec code source, ouvrez instantanés avec Visual Studio 2017 Enterprise par [télécharger l’extension de débogueur de l’instantané hello pour Visual Studio](https://aka.ms/snapshotdebugger).

La collecte de captures instantanées est disponible pour :
* les applications .NET framework et ASP.NET exécutant .NET Framework 4.5 ou version ultérieure ;
* les applications .NET core 2.0 et ASP.NET Core 2.0 s’exécutant sous Windows.

### <a name="configure-snapshot-collection-for-aspnet-applications"></a>Configurer la collecte de captures instantanées pour les applications ASP.NET

1. Si vous ne l’avez pas encore fait, [Activez Application Insights dans votre application web](app-insights-asp-net.md).

2. Inclure hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) package NuGet dans votre application. 

3. Passez en revue les options par défaut hello hello package ajouté trop[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):

    ```xml
    <TelemetryProcessors>
        <Add Type="Microsoft.ApplicationInsights.SnapshotCollector.SnapshotCollectorTelemetryProcessor, Microsoft.ApplicationInsights.SnapshotCollector">
        <!-- hello default is true, but you can disable Snapshot Debugging by setting it toofalse -->
        <IsEnabled>true</IsEnabled>
        <!-- Snapshot Debugging is usually disabled in developer mode, but you can enable it by setting this tootrue. -->
        <!-- DeveloperMode is a property on hello active TelemetryChannel. -->
        <IsEnabledInDeveloperMode>false</IsEnabledInDeveloperMode>
        <!-- How many times we need toosee an exception before we ask for snapshots. -->
        <ThresholdForSnapshotting>5</ThresholdForSnapshotting>
        <!-- hello maximum number of examples we create for a single problem. -->
        <MaximumSnapshotsRequired>3</MaximumSnapshotsRequired>
        <!-- hello maximum number of problems that we can be tracking at any time. -->
        <MaximumCollectionPlanSize>50</MaximumCollectionPlanSize>
        <!-- How often tooreset problem counters. -->
        <ProblemCounterResetInterval>06:00:00</ProblemCounterResetInterval>
        <!-- hello maximum number of snapshots allowed in one minute. -->
        <SnapshotsPerMinuteLimit>2</SnapshotsPerMinuteLimit>
        <!-- hello maximum number of snapshots allowed per day. -->
        <SnapshotsPerDayLimit>50</SnapshotsPerDayLimit>
        </Add>
    </TelemetryProcessors>
    ```

4. Les instantanés sont collectés uniquement sur les exceptions qui sont signalés tooApplication Insights. Dans certains cas (par exemple, les anciennes versions de la plateforme .NET de hello), vous devrez peut-être trop[configurer la collection d’exceptions](app-insights-asp-net-exceptions.md#exceptions) exceptions toosee avec des instantanés dans le portail de hello.


### <a name="configure-snapshot-collection-for-aspnet-core-20-applications"></a>Configurer la collecte de captures instantanées pour les applications ASP.NET Core 2.0

1. Si vous ne l’avez pas encore fait, [Activez Application Insights dans votre application web ASP.NET Core](app-insights-asp-net-core.md).

2. Inclure hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) package NuGet dans votre application.

3. Modifier hello `ConfigureServices` méthode dans votre application `Startup` classe du processeur de télémétrie du collecteur instantané tooadd hello. code Hello que vous devez ajouter dépend de la version de référencé de hello Hello package NuGet de Microsoft.ApplicationInsights.ASPNETCore.

   Pour Microsoft.ApplicationInsights.AspNetCore 2.1.0, ajoutez :
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       // This method is called by hello runtime. Use it tooadd services toohello container.
       public void ConfigureServices(IServiceCollection services)
       {
           services.AddSingleton<Func<ITelemetryProcessor, ITelemetryProcessor>>(next => new SnapshotCollectorTelemetryProcessor(next));
           // TODO: Add any other services your application needs here.
       }
   }
   ```

   Pour Microsoft.ApplicationInsights.AspNetCore 2.1.1, ajoutez :
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       private class SnapshotCollectorTelemetryProcessorFactory : ITelemetryProcessorFactory
       {
           public ITelemetryProcessor Create(ITelemetryProcessor next) =>
               new SnapshotCollectorTelemetryProcessor(next);
       }

       // This method is called by hello runtime. Use it tooadd services toohello container.
       public void ConfigureServices(IServiceCollection services)
       {
            services.AddSingleton<ITelemetryProcessorFactory>(new SnapshotCollectorTelemetryProcessorFactory());
           // TODO: Add any other services your application needs here.
       }
   }
   ```

### <a name="configure-snapshot-collection-for-other-net-applications"></a>Configurer la collecte de captures instantanées pour d’autres applications .NET

1. Si votre application n’est pas déjà instrumentée avec Application Insights, commencez par [l’activation d’Application Insights et clé d’instrumentation paramètre hello](app-insights-windows-desktop.md).

2. Ajouter hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) package NuGet dans votre application.

3. Les instantanés sont collectés uniquement sur les exceptions qui sont signalés tooApplication Insights. Vous devrez peut-être toomodify tooreport de votre code les. code de gestion des exceptions de Hello dépend de la structure de hello de votre application, mais voici un exemple :
    ```C#
   TelemetryClient _telemetryClient = new TelemetryClient();

   void ExampleRequest()
   {
        try
        {
            // TODO: Handle hello request.
        }
        catch (Exception ex)
        {
            // Report hello exception tooApplication Insights.
            _telemetryClient.TrackException(ex);

            // TODO: Rethrow hello exception if desired.
        }
   }
    ```
    
## <a name="grant-permissions"></a>Accorder des autorisations

Les propriétaires de hello abonnement Azure peuvent inspecter des instantanés. Les autres utilisateurs doivent y être autorisés par un propriétaire.

autorisation toogrant, affecter hello `Application Insights Snapshot Debugger` toousers de rôle qui inspecte instantanés. Ce rôle peut être attribué tooindividual utilisateurs ou groupes de propriétaires d’abonnements pour la cible de hello ressource Application Insights ou son groupe de ressources ou l’abonnement.

1. Ouvrez le panneau de contrôle d’accès (IAM) hello.
1. Cliquez sur hello + bouton Ajouter.
1. Sélectionnez l’Application Insights instantané débogueur à partir de la liste déroulante de rôles hello.
1. Recherchez et entrez un nom pour hello utilisateur tooadd.
1. Cliquez sur le rôle d’utilisateur toohello hello hello enregistrer bouton tooadd.


[!IMPORTANT]
    Les captures instantanées des valeurs de variables et de paramètres peuvent contenir des informations personnelles ou sensibles.

## <a name="debug-snapshots-in-hello-application-insights-portal"></a>Déboguer des instantanés dans le portail Application Insights de hello

Si un instantané est disponible pour une exception donnée ou un ID de problème, un **ouvrir l’instantané déboguer** bouton s’affiche sur hello [exception](app-insights-asp-net-exceptions.md) portail Application Insights de hello.

![Bouton Ouvrir la capture instantanée de débogage sur l’exception](./media/app-insights-snapshot-debugger/snapshot-on-exception.png)

Bonjour déboguer un instantané, vous consultez une pile des appels et un volet variables. Lorsque vous sélectionnez les frames d’appel de hello de pile dans le volet de pile d’appel hello, vous pouvez afficher les variables locales et appellent des paramètres pour cette fonction dans le volet des variables hello.

![Afficher l’instantané de débogage dans le portail de hello](./media/app-insights-snapshot-debugger/open-snapshot-portal.png)

Les captures instantanées peuvent contenir des informations sensibles qui, par défaut, ne sont pas visibles. tooview des instantanés, vous devez avoir hello `Application Insights Snapshot Debugger` tooyou du rôle assigné.

## <a name="debug-snapshots-with-visual-studio-2017-enterprise"></a>Déboguer des captures instantanées avec Visual Studio 2017 Enterprise
1. Cliquez sur hello **télécharger un instantané** toodownload de bouton un `.diagsession` fichier, qui peut être ouverte par Visual Studio 2017 Enterprise. 

2. tooopen hello `.diagsession` fichier, vous devez d’abord [télécharger et installer l’extension de débogueur de l’instantané hello pour Visual Studio](https://aka.ms/snapshotdebugger).

3. Après avoir ouvert le fichier d’instantané hello, page de débogage de Minidump hello dans Visual Studio s’affiche. Cliquez sur **déboguer du Code managé** toostart instantané d’hello de débogage. instantané d’Hello ouvre ligne toohello de code où hello de l’exception afin que vous puissiez déboguer état actuel de hello du processus de hello.

    ![Afficher la capture instantanée de débogage dans Visual Studio](./media/app-insights-snapshot-debugger/open-snapshot-visualstudio.png)

les instantanés téléchargés Hello contient tous les fichiers de symboles qui ont été trouvées sur votre serveur d’applications web. Ces fichiers de symboles sont requis tooassociate les données d’instantané avec le code source. Pour les applications de Service d’applications, assurez-vous que déploiement de symbole tooenable lors de la publication de vos applications web.

## <a name="how-snapshots-work"></a>Fonctionnement des captures instantanées

Au démarrage de votre application, un processus distinct de chargeur de captures instantanées qui surveille les demandes de captures instantanées de votre application est créé. Lorsqu’un instantané est demandé, un cliché instantané d’hello processus en cours d’exécution est effectué dans les too20 environ 10 minutes. processus de clichés instantanés Hello est ensuite analysé et un instantané est créé sans interrompre le processus principal hello toorun et traiter le trafic toousers. Bonjour instantané est ensuite téléchargée tooApplication Insights, ainsi que tous les fichiers de symbole (.pdb) qui sont nécessaires tooview instantané d’hello.

## <a name="current-limitations"></a>Limitations actuelles

### <a name="publish-symbols"></a>Publier des symboles
Hello instantané débogueur requiert des fichiers de symboles sur les variables de toodecode de serveur de production hello et tooprovide une expérience de débogage dans Visual Studio. version de Hello 15,2 de Visual Studio 2017 publie des symboles pour les versions release par défaut lorsqu’il publie tooApp Service. Dans les versions antérieures, vous devez suivant de hello tooadd ligne tooyour le profil de publication `.pubxml` fichiers afin que les symboles sont publiés en mode release :

```xml
    <ExcludeGeneratedDebugSymbol>False</ExcludeGeneratedDebugSymbol>
```

Calcul Azure et d’autres types, assurez-vous que les fichiers de symboles hello sont hello même dossier du fichier .dll de principale de l’application hello (en règle générale, `wwwroot/bin`) ou sont disponibles sur le chemin d’accès actuel de hello.

### <a name="optimized-builds"></a>Optimisation des versions
Dans certains cas, les variables locales ne peut pas être affichés dans les versions release en raison d’optimisations qui sont appliquées au cours du processus de génération hello.

## <a name="troubleshooting"></a>Résolution des problèmes

Les conseils suivants vous aider à résoudre les problèmes de hello débogueur de l’instantané.

### <a name="verify-hello-instrumentation-key"></a>Vérifiez la clé d’instrumentation hello

Assurez-vous que vous utilisez une clé d’instrumentation correct hello dans votre application publiée. En règle générale, Application Insights lit clé d’instrumentation hello hello ApplicationInsights.config du fichier. Vérifiez que la valeur de hello même hello en tant que clé d’instrumentation hello pour la ressource d’Application Insights hello que vous voyez dans le portail de hello.

### <a name="check-hello-uploader-logs"></a>Vérifiez les journaux du téléchargeur hello

Une fois une capture instantanée créée, un fichier minidump (.dmp) est créé sur le disque. Un processus distinct du chargeur prend ce fichier minidump, télécharger, ainsi que toutes les fichiers pdb associé, tooApplication stockage du débogueur d’instantané Insights. Une fois les minidump hello a été téléchargé correctement, elle est supprimée à partir du disque. fichiers journaux Hello téléchargeur de minidump hello sont conservés sur le disque. Dans un environnement App Service, vous pouvez trouver ces fichiers journaux dans `D:\Home\LogFiles\Uploader_*.log`. Utiliser le site Administration Kudu hello pour le Service d’applications toofind ces fichiers journaux.

1. Bonjour portail Azure, ouvrez votre application de Service de l’application.

2. Sélectionnez hello **outils avancés** panneau ou recherchez **Kudu**.
3. Cliquez sur **Atteindre**.
4. Bonjour **console de débogage** zone de liste déroulante, sélectionnez **CMD**.
5. Cliquez sur **LogFiles**.

Vous devriez voir au moins un fichier dont le nom commence par `Uploader_` et dont l’extension est `.log`. Cliquez sur toodownload d’icône appropriée hello tous les fichiers journaux ou les ouvrir dans un navigateur.
nom de fichier Hello inclut le nom de l’ordinateur hello. Si votre instance App Service est hébergée sur plusieurs machines, il existe des fichiers journaux distincts pour chacune d’elles. Lorsque le Téléchargeur de hello détecte un fichier minidump, elle est enregistrée dans le fichier journal de hello. Voici un exemple chargement réussi :

```
MinidumpUploader.exe Information: 0 : Dump available 139e411a23934dc0b9ea08a626db16c5.dmp
    DateTime=2017-05-25T14:25:08.0349846Z
MinidumpUploader.exe Information: 0 : Uploading D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp, 329.12 MB
    DateTime=2017-05-25T14:25:16.0145444Z
MinidumpUploader.exe Information: 0 : Upload successful.
    DateTime=2017-05-25T14:25:42.9164120Z
MinidumpUploader.exe Information: 0 : Extracting PDB info from D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp.
    DateTime=2017-05-25T14:25:42.9164120Z
MinidumpUploader.exe Information: 0 : Matched 2 PDB(s) with local files.
    DateTime=2017-05-25T14:25:44.2310982Z
MinidumpUploader.exe Information: 0 : Stamp does not want any of our matched PDBs.
    DateTime=2017-05-25T14:25:44.5435948Z
MinidumpUploader.exe Information: 0 : Deleted D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp
    DateTime=2017-05-25T14:25:44.6095821Z
```

Dans l’exemple précédent de hello, clé d’instrumentation hello est `c12a605e73c44346a984e00000000000`. Cette valeur doit correspondre à clé d’instrumentation hello pour votre application.
minidump de Hello est associé à un instantané avec l’ID de hello `139e411a23934dc0b9ea08a626db16c5`. Vous pouvez utiliser cet ID ultérieure toolocate hello associés télémétrie des exceptions dans Application Insights Analytique.

Téléchargeur de Hello analyse les nouveaux fichiers PDB sur toutes les 15 minutes. Voici un exemple :

```
MinidumpUploader.exe Information: 0 : PDB rescan requested.
    DateTime=2017-05-25T15:11:38.8003886Z
MinidumpUploader.exe Information: 0 : Scanning D:\home\site\wwwroot\ for local PDBs.
    DateTime=2017-05-25T15:11:38.8003886Z
MinidumpUploader.exe Information: 0 : Scanning D:\local\Temporary ASP.NET Files\root\a6554c94\e3ad6f22\assembly\dl3\81d5008b\00b93cc8_dec5d201 for local PDBs.
    DateTime=2017-05-25T15:11:38.8160276Z
MinidumpUploader.exe Information: 0 : Local PDB scan complete. Found 2 PDB(s).
    DateTime=2017-05-25T15:11:38.8316450Z
MinidumpUploader.exe Information: 0 : Deleted PDB scan marker D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\.pdbscan.
    DateTime=2017-05-25T15:11:38.8316450Z
```

Pour les applications qui sont _pas_ hébergé dans le Service d’applications, les journaux téléchargeur hello sont Bonjour même dossier que les minidumps hello : `%TEMP%\Dumps\<ikey>` (où `<ikey>` est votre clé d’instrumentation).

### <a name="use-application-insights-search-toofind-exceptions-with-snapshots"></a>Utilisez Application Insights rechercher les exceptions toofind avec des instantanés

Lorsqu’un instantané est créé, hello lever exception est marqué avec un ID d’instantané. Lors de la télémétrie des exceptions hello est signalé tooApplication Insights, cet ID d’instantané est inclus comme une propriété personnalisée. Panneau de recherche hello dans Application Insights, vous pouvez rechercher toutes les données de télémétrie avec hello `ai.snapshot.id` propriété personnalisée.

1. Parcourir les ressources d’Application Insights tooyour Bonjour portail Azure.
2. Cliquez sur **Rechercher**.
3. Type `ai.snapshot.id` hello de zone de texte Rechercher et appuyez sur ENTRÉE.

![Recherche de télémétrie avec un ID d’instantané dans le portail de hello](./media/app-insights-snapshot-debugger/search-snapshot-portal.png)

Si cette recherche ne retourne aucun résultat, aucun instantané n’ont été Insights tooApplication signalé pour votre application dans la plage de temps hello sélectionné.

toosearch pour un instantané spécifique à partir de journaux de téléchargeur hello, tapez ce code dans la zone de recherche hello. Si vous ne trouvez la télémétrie d’une capture instantanée dont vous savez qu’elle a été chargée, procédez comme suit :

1. Vérifiez que vous envisagez d’utiliser les ressources Application Insights droite hello en vérifiant la clé d’instrumentation hello.

2. À l’aide d’horodatage hello du journal du téléchargeur hello, du filtre de plage de temps hello de hello recherche toocover régler cet intervalle de temps.

Si vous ne voyez pas une exception avec cet ID d’instantané, puis télémétrie des exceptions hello n’a pas été signalé tooApplication Insights. Cette situation peut se produire si votre application est tombé en panne après l’instantané d’hello nécessaire, mais avant qu’elles consignées télémétrie des exceptions hello. Dans ce cas, recherchez hello App Service se connecte sous `Diagnose and solve problems` toosee si elle existait inattendue redémarre ou les exceptions non gérées.

## <a name="next-steps"></a>Étapes suivantes

* [Définissez snappoints dans votre code](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) instantanés tooget sans attendre d’une exception.
* [Diagnostiquer des exceptions dans vos applications web](app-insights-asp-net-exceptions.md) explique comment toomake plusieurs exceptions tooApplication visible Insights. 
* [Détection intelligente](app-insights-proactive-diagnostics.md) permet de détecter automatiquement les anomalies relatives aux performances.
