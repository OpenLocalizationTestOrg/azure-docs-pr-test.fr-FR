---
title: "rôles serveur et de travail d’Application Insights pour Windows aaaAzure | Documents Microsoft"
description: "Ajouter manuellement des performances, la disponibilité et l’utilisation des hello Application Insights SDK tooyour ASP.NET applications tooanalyze."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 106ba99b-b57a-43b8-8866-e02f626c8190
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: 64643ef637195d10f87fc6020a77169bca66c1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manually-configure-application-insights-for-net-applications"></a>Configurer manuellement Application Insights pour des applications .NET

Vous pouvez configurer [Application Insights](app-insights-overview.md) toomonitor une grande variété d’applications ou les rôles d’application, les composants ou microservices. Pour les services et applications web, Visual Studio permet un [configuration en une seule étape](app-insights-asp-net.md). Pour les autres types d’application .NET, telles que les rôles de serveur principal ou les applications de bureau, vous pouvez configurer Application Insights manuellement.

![Exemples de graphiques d’analyse des performances](./media/app-insights-windows-services/10-perf.png)

#### <a name="before-you-start"></a>Avant de commencer

Ce dont vous avez besoin :

* Un abonnement trop[Microsoft Azure](http://azure.com). Si votre équipe ou organisation dispose d’un abonnement Azure, propriétaire de hello vous pouvez ajouter des tooit, à l’aide de votre [compte Microsoft](http://live.com).
* Visual Studio 2013 ou une version ultérieure.

## <a name="add"></a>1. Choix d’une ressource Application Insights

Hello « ressource » est où vos données sont collectées et affichées dans hello portail Azure. Vous devez toodecide si toocreate un, ou partager un existant.

### <a name="part-of-a-larger-app-use-existing-resource"></a>Partie d’une application plus volumineuse : utiliser des ressources existantes

Si votre application web comporte plusieurs composants - par exemple, une application web frontal et un ou plusieurs services back-end - puis doit envoyer la télémétrie toohello de composants hello tous les mêmes ressources. Cela active les toobe affichée sur un seul mappage d’Application et rendre possible tootrace une demande à partir d’un composant tooanother.

Par conséquent, si vous êtes déjà analyse des autres composants de cette application, puis utilisez simplement hello même ressource.

Ouvrir la ressource de hello Bonjour [portail Azure](https://portal.azure.com/). 

### <a name="self-contained-app-create-a-new-resource"></a>Application autonome : créer une nouvelle ressource

Si les applications non liées tooother n’est hello nouvelle application, il doit avoir sa propre ressource.

Connectez-vous à toohello [portail Azure](https://portal.azure.com/)et créer une nouvelle ressource Application Insights. Choisissez ASP.NET en tant que type de l’application hello.

![Cliquez sur Nouveau > Application Insights](./media/app-insights-windows-services/01-new-asp.png)

choix de Hello du type d’application définit le contenu par défaut hello de panneaux de ressource hello.

## <a name="2-copy-hello-instrumentation-key"></a>2. Copiez la clé d’Instrumentation de hello
clé de Hello identifie les ressources hello. Vous allez l’installer dès Bonjour SDK, dans la ressource de toohello commande toodirect données.

![Cliquez sur Propriétés, sélectionnez la clé de hello et appuyez sur ctrl + C](./media/app-insights-windows-services/02-props-asp.png)

## <a name="sdk"></a>3. Installer le package d’Application Insights hello dans votre application
Installation et configuration hello Application Insights package varie selon la plateforme hello sur lequel vous travaillez. 

1. Dans Visual Studio, cliquez avec le bouton droit sur votre projet et choisissez **Gérer les packages NuGet**.
   
    ![Droit hello projet, puis sélectionnez Gérer les Packages Nuget](./media/app-insights-windows-services/03-nuget.png)
2. Installer le package d’Application Insights hello pour les applications Windows server, « Microsoft.ApplicationInsights.WindowsServer. »
   
    ![Recherchez « Application Insights »](./media/app-insights-windows-services/04-ai-nuget.png)
   
    *Quelle version ?*

    Vérifiez **inclure la version préliminaire** si vous souhaitez tootry nos dernières fonctionnalités. les documents correspondants Hello ou blogs Notez si vous avez besoin d’une version préliminaire.
    
    *Puis-je utiliser d’autres packages ?*
   
    Oui. Choisissez « Microsoft.ApplicationInsights » si vous souhaitez uniquement toouse hello API toosend vos propres données de télémétrie. Hello Windows Server inclut hello API et plusieurs autres packages tels que la collecte des compteurs de performances et l’analyse de dépendance. 

### <a name="tooupgrade-toofuture-package-versions"></a>versions de package tooupgrade toofuture
Nous libérer une nouvelle version de hello SDK à partir de tootime de temps.

tooupgrade tooa [nouvelle version de package de hello](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/), ouvrez le Gestionnaire de package NuGet à nouveau et filtrer sur les packages installés. Sélectionnez **Microsoft.ApplicationInsights.WindowsServer** et choisissez **Mettre à niveau**.

Si vous avez apporté des personnalisations tooApplicationInsights.config, enregistrer une copie de celui-ci avant de mettre à niveau et par la suite de fusionner vos modifications dans la nouvelle version de hello.

## <a name="4-send-telemetry"></a>4. Envoyer des données de télémétrie
**Si vous avez installé le package de hello API uniquement :**

* Valeur de clé d’instrumentation hello dans le code, par exemple `main()`: 
  
    `TelemetryConfiguration.Active.InstrumentationKey = "`*votre clé*`";` 
* [Écrire vos propres données de télémétrie à l’aide des API de hello](app-insights-api-custom-events-metrics.md#ikey).

**Si vous avez installé d’autres packages d’Application Insights,** vous pouvez, si vous préférez, utiliser clé d’instrumentation hello hello .config fichier tooset :

* Modifier ApplicationInsights.config (qui a été ajouté par hello NuGet installer). Insérez ce juste avant la balise de fermeture de hello :
  
    `<InstrumentationKey>`*clé d’instrumentation hello vous avez copié*`</InstrumentationKey>`
* Assurez-vous que les propriétés de hello de ApplicationInsights.config dans l’Explorateur de solutions sont définies trop**Build Action = le contenu, copie tooOutput Directory = copie**.

Il est la clé d’instrumentation hello tooset utiles dans le code si vous souhaitez trop[clé hello de commutateur pour différentes configurations de build](app-insights-separate-resources.md). Si vous définissez la clé de hello dans le code, vous n’avez pas tooset dans hello `.config` fichier.

## <a name="run"></a> Exécution de votre projet
Hello d’utilisation **F5** toorun votre application et essayez-la : ouvrir différentes pages toogenerate certaines données de télémétrie.

Dans Visual Studio, vous verrez un nombre d’événements de hello qui ont été envoyés.

![Nombre d’événements dans Visual Studio](./media/app-insights-windows-services/appinsights-09eventcount.png)

## <a name="monitor"></a> Affichage de vos données de télémétrie
Retourner toohello [portail Azure](https://portal.azure.com/) et parcourir les ressources d’Application Insights tooyour.

Rechercher des données dans les graphiques en vue d’ensemble de hello. Au début, seuls un ou deux points s'affichent. Par exemple :

![Parcourez les données toomore](./media/app-insights-windows-services/12-first-perf.png)

Cliquez sur via n’importe quel toosee graphique plus des métriques. [En savoir plus sur les mesures.](app-insights-web-monitor-performance.md)

### <a name="no-data"></a>Pas de données ?
* Utilisez l’application hello, ouvrir des pages différentes, afin qu’il génère des données de télémétrie.
* Ouvrez hello [recherche](app-insights-diagnostic-search.md) vignette, toosee des événements individuels. Il prend événements parfois un peu longtemps tooget via le pipeline de métriques hello.
* Attendez quelques secondes, puis cliquez sur **Actualiser**. Graphiques eux-mêmes actualiser régulièrement, mais vous pouvez actualiser manuellement si vous vous attendez tooshow de certaines données.
* Consultez la rubrique [Résolution des problèmes](app-insights-troubleshoot-faq.md).

## <a name="publish-your-app"></a>Publier votre application
Déployer maintenant votre serveur d’applications tooyour ou tooAzure et Espion hello s’accumulent des données.

![Utiliser Visual Studio toopublish votre application](./media/app-insights-windows-services/15-publish.png)

Lorsque vous exécutez en mode débogage, la télémétrie s’effectue via le pipeline de hello, afin que vous devez voir les données figurant dans les secondes. Quand vous déployez votre application dans la configuration Release, les données s’accumulent plus lentement.

### <a name="no-data-after-you-publish-tooyour-server"></a>Aucune donnée après la publication tooyour serveur ?
Ouvrez les ports pour le trafic sortant dans le pare-feu de votre serveur. Consultez [cette page](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses) pour la liste d’adresses requises hello 

### <a name="trouble-on-your-build-server"></a>Vous rencontrez des problèmes sur votre serveur de builds ?
Consultez cet article de [résolution des problèmes](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild).

> [!NOTE]
> Si votre application génère un grand nombre de télémétrie, module d’échantillonnage adaptive hello réduira automatiquement volume hello envoyé toohello portail en envoyant qu’une fraction représentative d’événements. Toutefois, les événements qui sont associée toohello même demande sera sélectionné ou désélectionné en tant que groupe, afin que vous pouvez naviguer entre les événements connexes. 
> [En savoir plus sur l'échantillonnage](app-insights-sampling.md).
> 
> 

## <a name="video"></a>Vidéo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Étapes suivantes
* [Ajouter des données de télémétrie plus](app-insights-asp-net-more.md) tooget hello vue 360 degrés de votre application.

