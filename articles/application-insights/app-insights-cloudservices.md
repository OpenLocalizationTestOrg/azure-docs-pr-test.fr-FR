---
title: aaaApplication Insights pour les Services de cloud computing Azure | Documents Microsoft
description: "Surveillance efficace de vos rôles Web et de travail avec Application Insights"
services: application-insights
documentationcenter: 
keywords: WAD2AI, Azure Diagnostics
author: CFreemanwa
manager: carmonm
editor: alancameronwills
ms.assetid: 5c7a5b34-329e-42b7-9330-9dcbb9ff1f88
ms.service: application-insights
ms.devlang: na
ms.tgt_pltfrm: ibiza
ms.topic: get-started-article
ms.workload: tbd
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: 6956ce423eea1e2cf387bd98250bae32d9501ed0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-azure-cloud-services"></a>Application Insights pour Services cloud Azure
[Les applications de service cloud Microsoft Azure](https://azure.microsoft.com/services/cloud-services/) peuvent être surveillées par [Application Insights][start] pour la disponibilité, les performances, les défaillances et l’utilisation en combinant les données des kits de développement logiciel (SDK) d’Application Insights avec les données [Azure Diagnostics](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/azure-diagnostics) de vos services cloud. Avec commentaires hello que vous obtenez sur les performances de hello et l’efficacité de votre application Bonjour générique, vous pouvez rendre des décisions avisées sur la direction hello de conception de hello dans chaque cycle de vie de développement.

![Exemple](./media/app-insights-cloudservices/sample.png)

## <a name="before-you-start"></a>Avant de commencer
Vous devez disposer des éléments suivants :

* Un abonnement à [Microsoft Azure](http://azure.com). Connectez-vous avec un compte Microsoft, que vous pouvez avoir pour Windows, XBox Live ou d’autres services cloud de Microsoft. 
* Microsoft Azure Tools 2.9 ou version ultérieure
* Developer Analytics Tools 7.10 ou version ultérieure

## <a name="quick-start"></a>Démarrage rapide
Bonjour toomonitor rapidement et facilement que votre service cloud avec Application Insights est toochoose option lorsque vous publiez votre tooAzure de service.

![Exemple](./media/app-insights-cloudservices/azure-cloud-application-insights.png)

Instruments de cette option votre application en cours d’exécution, ce qui vous donne toutes les données de télémétrie hello vous devez toomonitor demandes, les exceptions et les dépendances dans votre rôle web, ainsi que les performances des compteurs à partir de vos rôles de travail. Toutes les traces de diagnostic générés par votre application sont également envoyés tooApplication Insights.

Si tout ceci vous suffit, vous avez terminé ! Les étapes suivantes consistent à [afficher les métriques de votre application](app-insights-metrics-explorer.md), à [interroger vos données avec Analytics](app-insights-analytics.md) et éventuellement à configurer un [tableau de bord](app-insights-dashboards.md). Vous pourriez tooset des [les tests de disponibilité](app-insights-monitor-web-app-availability.md) et [ajouter des pages de codes tooyour web](app-insights-javascript.md) toomonitor les performances dans le navigateur de hello.

Mais vous pouvez aussi obtenir plus d’options :

* Envoyer des données à partir de différents composants et configurations de build tooseparate ressources.
* Ajouter une télémétrie personnalisée à partir de votre application.

Si ces options sont d’intérêt tooyou, lisez la suite.

## <a name="sample-application-instrumented-with-application-insights"></a>Exemple d’application instrumentée avec Application Insights
Examinons cela [exemple d’application](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService) dans lequel Application Insights est ajouté le service cloud tooa avec deux rôles de travail hébergés dans Azure. 

Ce qui suit vous indique comment tooadapt votre propre service de cloud de projet Bonjour identique.

## <a name="plan-resources-and-resource-groups"></a>Planifier des ressources et des groupes de ressources
télémétrie Hello à partir de votre application est stockée, analysée et affichée dans une ressource Azure de type Application Insights. 

Chaque ressource appartient le groupe de ressources tooa. Groupes de ressources sont utilisées pour gérer les coûts, pour accorder l’accès à des membres tooteam, et toodeploy mises à jour dans une seule transaction coordonnée. Par exemple, vous pouvez [écrire un script toodeploy](../azure-resource-manager/resource-group-template-deploy.md) un Service Cloud Azure et son Application Insights analyse des ressources en une seule opération.

### <a name="resources-for-components"></a>Ressources pour les composants
Hello recommandé de schéma est toocreate une ressource distincte pour chaque composant de votre application : autrement dit, chaque rôle web et le rôle de travail. Vous pouvez analyser chaque composant séparément, mais vous pouvez créer un [tableau de bord](app-insights-dashboards.md) qui réunit les graphiques clés hello à partir de tous les composants de hello, afin que vous pouvez comparer et analyser les ensemble. 

Un autre système est la télémétrie de hello toosend à partir de plusieurs rôles toohello même ressource, mais [ajouter un élément de données de télémétrie de dimension propriété tooeach](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer) qui identifie son rôle de la source. Dans ce schéma, métriques graphiques tels que les exceptions affichent normalement une agrégation des nombres hello de hello différents rôles, mais vous pouvez segmenter le graphique de hello par identificateur de rôle hello à la demande. Les recherches peuvent également être filtrés par hello même dimension. Cette solution rend un peu plus facile tooview tout à hello en même temps, mais peut également entraîner toosome confusion entre les rôles de hello.

Données de télémétrie de navigateur sont généralement incluse dans hello mêmes ressources que son rôle web côté serveur.

Placez les ressources d’Application Insights hello pour les différents composants de hello dans un groupe de ressources. Il est ainsi facile toomanage ensemble. 

### <a name="separating-development-test-and-production"></a>Séparation du développement, des tests et de la production
Si vous développez des événements personnalisés pour votre fonctionnalité suivante lors de la version précédente de hello est dynamique, vous souhaitez le ressource de Application Insights distinct de toosend hello développement télémétrie tooa. Sinon, il est difficile toofind votre test de télémétrie parmi tous les hello le trafic à partir du site en ligne hello.

tooavoid cette situation, créer des ressources distinctes pour chaque configuration de build ou un « tampon » (développement, test, production,...) de votre système. Placez les ressources hello pour chaque configuration de build dans un groupe de ressources distinct. 

toosend hello télémétrie toohello ressources appropriées, vous pouvez configurer hello Application Insights SDK afin qu’il récupère une clé d’instrumentation différents en fonction de la configuration de build hello. 

## <a name="create-an-application-insights-resource-for-each-role"></a>Création d’une ressource Application Insights pour chaque rôle
Si vous avez décidé de toocreate une ressource distincte pour chaque rôle - et éventuellement une séparée définie pour chaque configuration de build -, il est plus simple toocreate les portail Application Insights de hello. (Si vous créez un lot des ressources, vous pouvez [automatiser les processus hello](app-insights-powershell.md).

1. Bonjour [portail Azure][portal], créez une ressource Application Insights. Choisissez ASP.NET comme type d’application. 

    ![Cliquez sur Nouveau > Application Insights](./media/app-insights-cloudservices/01-new.png)
2. Notez que chaque ressource est identifiée par une clé d’instrumentation. Vous devrez peut-être cela ultérieurement si vous souhaitez toomanually configurez ou vérifiez la configuration de hello Hello SDK.

    ![Cliquez sur Propriétés, sélectionnez la clé de hello et appuyez sur ctrl + C](./media/app-insights-cloudservices/02-props.png) 

## <a name="set-up-azure-diagnostics-for-each-role"></a>Configurer Diagnostics Azure pour chaque rôle
Définissez cette option toomonitor votre application avec Application Insights. Pour les rôles web, vous bénéficierez d’alertes, de diagnostics et d’une surveillance des performances, ainsi que de l’analyse de l’utilisation. Pour d’autres rôles, vous pouvez rechercher et contrôler les diagnostics Azure telles que le redémarrage, les compteurs de performance et les appels tooSystem.Diagnostics.Trace. 

1. Dans l’Explorateur de solutions Visual Studio, sous &lt;YourCloudService&gt;, rôles, ouvrez les propriétés de hello de chaque rôle.
2. Dans **Configuration**, définissez **envoyer des données de diagnostics tooApplication Insights** et sélectionnez hello ressources Application Insights approprié que vous avez créé précédemment.

Si vous avez décidé de toouse une ressource Application Insights distincte pour chaque configuration de build, sélectionnez d’abord la configuration de hello.

![Dans Propriétés de hello de chaque rôle Azure, configurer Application Insights](./media/app-insights-cloudservices/configure-azure-diagnostics.png)

Cela a pour effet hello d’insertion de vos clés d’instrumentation Application Insights dans les fichiers hello nommés `ServiceConfiguration.*.cscfg`. ([Exemple de code](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/AzureEmailService/ServiceConfiguration.Cloud.cscfg)).

Si vous souhaitez que le niveau de hello toovary des informations de diagnostic envoyées tooApplication Insights, vous pouvez le faire [en modifiant hello `.cscfg` directement les fichiers](app-insights-azure-diagnostics.md).

## <a name="sdk"></a>Installer hello SDK dans chaque projet.
Cette option ajoute hello capacité tooadd personnalisé télémétrie tooany rôle d’entreprise, pour une analyse plus approfondie de la façon dont votre application est utilisée et qu’il exécute.

Dans Visual Studio, configurez hello Application Insights SDK pour chaque projet d’application cloud.

1. **Rôles Web**: droit hello projet, puis choisissez **configurer Application Insights** ou **Ajouter > données de télémétrie Application Insights**.

2. **Rôles de travail** : 
 * Droit hello projet, puis sélectionnez **gérer les Packages Nuget**.
 * Ajoutez [Application Insights pour les serveurs Windows](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/).

    ![Recherchez « Application Insights »](./media/app-insights-cloudservices/04-ai-nuget.png)

3. Configurer hello SDK toosend données toohello ressource Application Insights.

    Dans une fonction de démarrage appropriée, définir la clé d’instrumentation hello à partir du paramètre de configuration hello dans le fichier .cscfg de hello :
 
    ```C#
   
     TelemetryConfiguration.Active.InstrumentationKey = RoleEnvironment.GetConfigurationSettingValue("APPINSIGHTS_INSTRUMENTATIONKEY");
    ```
   
    Faites cela pour chaque rôle de votre application. Consultez les exemples hello :
   
   * [Rôle Web](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/Global.asax.cs#L27)
   * [Rôle de travail](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/WorkerRoleA.cs#L232)
   * [Pour les pages Web](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/Views/Shared/_Layout.cshtml#L13) 
4. Ensemble hello ApplicationInsights.config fichier toobe copié toujours répertoire de sortie toohello. 
   
    (Dans le fichier .config de hello, vous verrez message demandant vous tooplace hello clé d’instrumentation il. Toutefois, pour les applications cloud, il est mieux tooset à partir du fichier .cscfg de hello. Cela garantit que hello rôle est correctement identifié dans le portail de hello.)

#### <a name="run-and-publish-hello-app"></a>Exécuter et publier l’application hello
Exécutez votre application et connectez-vous à Azure. Ressources d’Application Insights hello ouverts que vous avez créé, et vous verrez des points de données individuels apparaissant dans [recherche](app-insights-diagnostic-search.md), et les données agrégées dans [métrique Explorer](app-insights-metrics-explorer.md). 

Ajouter plus de télémétrie : voir les sections de hello ci-dessous - et puis publier votre application tooget dynamique diagnostic et utilisation des commentaires. 

#### <a name="no-data"></a>Pas de données ?
* Ouvrez hello [recherche] [ diagnostic] vignette, toosee des événements individuels.
* Utilisez l’application hello, ouvrir des pages différentes, afin qu’il génère des données de télémétrie.
* Attendez quelques secondes, puis cliquez sur Actualiser.
* Consultez la rubrique [Résolution des problèmes][qna].

## <a name="view-azure-diagnostic-events"></a>Affichage des événements Azure Diagnostics
Où toofind hello [Azure Diagnostics](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/azure-diagnostics) informations dans Application Insights :

* Les compteurs de performances s’affichent comme mesures personnalisées. 
* Les journaux des événements Windows s’affichent comme traces et événements personnalisés.
* Les journaux des applications, les journaux ETW et tous les journaux d’infrastructure des diagnostics s’affichent comme traces.

les compteurs de performances toosee et décomptes d’événements, ouvrez [Metrics Explorer](app-insights-metrics-explorer.md) et ajouter un nouveau graphique :

![Données de diagnostics Azure](./media/app-insights-cloudservices/23-wad.png)

Utilisez [recherche](app-insights-diagnostic-search.md) ou [les requête Analytique](app-insights-analytics-tour.md) toosearch entre hello différents journaux envoyés par les Diagnostics Azure de suivi. Par exemple, supposons que vous disposez d’une exception non gérée qui a provoqué un rôle toocrash et le recyclage. Ces informations sont inscrive dans hello Application canal de journal des événements Windows. Vous pouvez utiliser recherche toolook à hello erreur du journal des événements Windows et obtenir une trace de la pile complète hello pour exception de hello. Qui vous aideront à trouver hello cause première du problème de hello.

![Recherche de diagnostics Azure](./media/app-insights-cloudservices/25-wad.png)

## <a name="more-telemetry"></a>Données de télémétrie supplémentaires
Hello sections ci-dessous montrent comment tooget de télémétrie supplémentaires à partir de différents aspects de votre application.

## <a name="track-requests-from-worker-roles"></a>Suivi des demandes des rôles de travail
Dans les rôles web, module de demandes hello collecte automatiquement des données sur les requêtes HTTP. Consultez hello [exemple MVCWebRole](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/MvcWebRole) pour obtenir des exemples de comment vous pouvez substituer le comportement de regroupement par défaut hello. 

Vous pouvez capturer des performances hello des rôles de tooworker d’appels en effectuant le suivi dans hello même façon que les requêtes HTTP. Dans Application Insights, type de données de télémétrie hello demande mesure une unité de travail côté serveur nommé qui soit chronométré indépendamment vous réussissent ou échouent. Alors que les requêtes HTTP sont automatiquement capturés par hello SDK, vous pouvez insérer vos propres rôles de tooworker code tootrack demandes.

Consultez hello deux exemples de travail rôles tooreport instrumenté demandes : [WorkerRoleA](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/WorkerRoleA) et [WorkerRoleB](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/WorkerRoleB)

## <a name="exceptions"></a>Exceptions
Consultez la rubrique [Analyse des exceptions dans Application Insights](app-insights-asp-net-exceptions.md) pour découvrir comment collecter des exceptions non gérées depuis différents types d'applications Web.

rôle de web d’exemple Hello a MVC5 et API Web 2 contrôleurs. Hello des exceptions non gérées à partir de hello deux sont capturées par hello suivant gestionnaires :

* [AiHandleErrorAttribute](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/Telemetry/AiHandleErrorAttribute.cs) configuré [ici](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/App_Start/FilterConfig.cs#L12) pour les contrôleurs MVC5
* [AiWebApiExceptionLogger](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/Telemetry/AiWebApiExceptionLogger.cs) configuré [ici](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/App_Start/WebApiConfig.cs#L25) pour les contrôleurs de l’API Web 2

Pour les rôles de travail, voici deux façons tootrack exceptions :

* TrackException(ex)
* Si vous avez ajouté le package NuGet écouteur hello Application Insights trace, vous pouvez utiliser **System.Diagnostics.Trace** toolog exceptions. [Exemple de code.](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/WorkerRoleA.cs#L107)

## <a name="performance-counters"></a>Compteurs de performance
Hello suivant les compteurs est recueillis par défaut :

    * \Processus(??APP_WIN32_PROC??)\% Temps processeur
    * \Memory\Octets disponibles
    * \.Exceptions .NET CLR(??APP_CLR_PROC??)\# Nombre d'exceptions levées/s
    * \Processus(??APP_WIN32_PROC??)\Octets privés
    * \Processus(??APP_WIN32_PROC??)\Nombre d’octets de données E/S par s
    * \Processus(_Total)\% Temps processeur

Pour les rôles web, ces compteurs sont également collectés :

    * \Applications ASP.NET(??APP_W3SVC_PROC??)\Demandes/s
    * \Applications ASP.NET (??APP_W3SVC_PROC??)\Durée d’exécution de la demande
    * \Applications ASP.NET (??APP_W3SVC_PROC??)\Demandes dans la file d’attente d’application

Vous pouvez spécifier des compteurs personnalisés ou d’autres compteurs de performances Windows en modifiant ApplicationInsights.config [comme dans cet exemple](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/ApplicationInsights.config#L14).

  ![Compteurs de performances](./media/app-insights-cloudservices/OLfMo2f.png)

## <a name="correlated-telemetry-for-worker-roles"></a>Télémétrie liée aux rôles de travail
Il est une expérience enrichie de diagnostic, lorsque vous voyez les DEL tooa a échoué ou la demande d’une latence élevée. Avec les rôles web, hello entre que SDK configure automatiquement la corrélation une télémétrie associée. Pour les rôles de travail, vous pouvez utiliser un tooset d’initialiseur de télémétrie personnalisée un attribut de contexte Operation.Id commun pour toutes les tooachieve de télémétrie hello ce cela. Cela vous permet de toosee si hello était dû latence/échec en raison de la dépendance de tooa ou de votre code en un clin de œil ! 

Voici comment procéder :

* Définir l’Id de corrélation hello dans un CallContext comme [ici](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/WorkerRoleA.cs#L36). Dans ce cas, nous utilisons hello ID de la demande en tant qu’id de corrélation hello
* Ajouter une implémentation personnalisée de TelemetryInitializer, tooset hello Operation.Id toohello correlationId ci-dessus. Voici un exemple : [ItemCorrelationTelemetryInitializer](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/Telemetry/ItemCorrelationTelemetryInitializer.cs#L13)
* Ajouter un initialiseur de télémétrie personnalisée hello. Vous pouvez le faire dans le fichier ApplicationInsights.config de hello, ou dans le code comme indiqué [ici](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/WorkerRoleA.cs#L233)

Et voilà ! utilisation du portail Hello est déjà associée toohelp que vous voyez toutes les données de télémétrie en un coup de œil :

![Télémétrie corrélée](./media/app-insights-cloudservices/bHxuUhd.png)

## <a name="client-telemetry"></a>Télémétrie client
[Ajouter hello des pages web SDK JavaScript tooyour] [ client] tooget basée sur navigateur télémétrie telles que les chiffres de consultation de page, les temps de chargement de page, les exceptions de script et toolet vous écrivez une télémétrie personnalisée dans vos scripts de la page.

## <a name="availability-tests"></a>Tests de disponibilité
[Configurer des tests web] [ availability] toomake que votre application reste en direct et réactives.

## <a name="display-everything-together"></a>Afficher tous les éléments ensemble
tooget une vue d’ensemble de votre système, vous pouvez intégrer des graphiques d’analyse ensemble sur l’une clés de hello [tableau de bord](app-insights-dashboards.md). Par exemple, vous pourriez épingler les demande hello et décompte des échecs de chaque rôle. 

Si votre système utilise d’autres services Azure tels que Stream Analytics, incluez également leurs graphiques de surveillance. 

Si vous avez une application mobile client, insérer certains événements personnalisés toosend de code sur les opérations de clé utilisateur et créer un [HockeyApp pont](app-insights-hockeyapp-bridge-app.md). Créer des requêtes dans [Analytique](app-insights-analytics.md) toodisplay hello du nombre d’événements et les épingler un tableau de bord toohello.

## <a name="example"></a>Exemple
[exemple de Hello](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService) surveille un service qui a un rôle web et deux rôles de travail.

## <a name="exception-method-not-found-on-running-in-azure-cloud-services"></a>Exception « méthode introuvable » lors de l’exécution dans Services cloud Azure
Avez-vous effectué une génération pour .NET 4.6 ? 4.6 n’est pas automatiquement pris en charge dans les rôles Azure Cloud Services. [Installez la version 4.6 sur chaque rôle](../cloud-services/cloud-services-dotnet-install-dotnet.md) avant d’exécuter votre application.

## <a name="video"></a>Vidéo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Étapes suivantes
* [Configurer l’envoi de Diagnostics Azure tooApplication Insights](app-insights-azure-diagnostics.md)
* [Automatiser la création des ressources Application Insights](app-insights-powershell.md)
* [Automatiser les diagnostics Azure](app-insights-powershell-azure-diagnostics.md)
* [Azure Functions](https://github.com/christopheranderson/azure-functions-app-insights-sample)

[api]: app-insights-api-custom-events-metrics.md
[availability]: app-insights-monitor-web-app-availability.md
[azure]: app-insights-azure.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[netlogs]: app-insights-asp-net-trace-logs.md
[portal]: http://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md 
