---
title: applications de Docker aaaMonitor dans Azure Application Insights | Documents Microsoft
description: "Exceptions, événements et compteurs de performance docker peuvent être affichées sur Application Insights, ainsi que les données de télémétrie hello à partir d’applications de hello placées dans des conteneurs."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 27a3083d-d67f-4a07-8f3c-4edb65a0a685
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 9aaf1076bae25485a396db1bb3dcd13bccd87c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-docker-applications-in-application-insights"></a>Analyse des applications Docker dans Application Insights
Les événements de cycle de vie et les compteurs de performances provenant de conteneurs [Docker](https://www.docker.com/) peuvent être représentés dans Application Insights. Installer hello [Application Insights](app-insights-overview.md) image dans un conteneur dans votre hôte et il affiche les compteurs de performance pour l’hôte de hello, que bien que pour hello autres images.

Avec Docker, vous distribuez vos applications dans des conteneurs légers avec toutes les dépendances. Elles s’exécuteront sur n’importe quelle machine hôte exécutant un moteur Docker.

Lorsque vous exécutez hello [image d’Application Insights](https://hub.docker.com/r/microsoft/applicationinsights/) sur l’hôte Docker, vous obtenez ces avantages :

* Cycle de vie des données de télémétrie sur tous les conteneurs hello en cours d’exécution sur l’ordinateur hôte de hello - Démarrer, arrêter et ainsi de suite.
* Compteurs de performances pour tous les conteneurs hello. Processeur, mémoire, utilisation du réseau, et bien plus encore.
* Si vous [installé le Kit de développement Application Insights pour Java](app-insights-java-live.md) dans les applications hello en cours d’exécution dans des conteneurs de hello, toutes les données de télémétrie hello de ces applications ont des propriétés supplémentaires identifiant le conteneur de hello et l’ordinateur hôte. Par exemple, si vous avez des instances d’une application en cours d’exécution dans plusieurs hôtes, vous pouvez facilement filtrer la télémétrie d’application par hôte.

![exemple](./media/app-insights-docker/00.png)

## <a name="set-up-your-application-insights-resource"></a>Configuration de votre ressource Application Insights
1. Connectez-vous à [portail Microsoft Azure](https://azure.com) et ouvrir la ressource d’Application Insights hello pour votre application ; ou [créer un nouveau](app-insights-create-new-resource.md). 
   
    *Quelle ressource dois-je utiliser ?* Si des applications hello qui vous sont en cours d’exécution sur votre ordinateur hôte ont été développées par quelqu'un d’autre, vous devez trop[créer une ressource Application Insights](app-insights-create-new-resource.md). Il s’agit où vous permet d’afficher et analysez les données de télémétrie hello. (Sélectionnez « Général » pour le type d’application hello).
   
    Mais si vous êtes développeur hello des applications de hello, puis nous espérons que vous [ajouté Application Insights SDK](app-insights-java-live.md) tooeach d'entre eux. S’ils sont tous les composants réellement d’une application métier unique, puis vous pouvez configurer toutes les ressources de tooone toosend télémétrie, et vous utilisez ces même ressource toodisplay hello Docker du cycle de vie et les performances des données. 
   
    Un troisième scénario est que vous avez développé la plupart des applications de hello, mais que vous utilisez des ressources distinctes toodisplay leurs données de télémétrie. Dans ce cas, vous probablement aussi que vous souhaitez toocreate une ressource distincte pour hello des données de Docker. 
2. Ajouter une vignette Docker hello : choisissez **ajouter vignette**, faites glisser de la vignette de Docker hello à partir de la galerie de hello, puis cliquez sur **fait**. 
   
    ![exemple](./media/app-insights-docker/03.png)
3. Cliquez sur hello **Essentials** liste déroulante et copiez la clé d’Instrumentation de hello. Vous utilisez ce Kit de développement logiciel de hello tootell où toosend ses données de télémétrie.

    ![exemple](./media/app-insights-docker/02-props.png)

Gardez cette fenêtre de navigateur pratique, que vous y reviendrons tooit bientôt toolook au niveau de votre télémétrie.

## <a name="run-hello-application-insights-monitor-on-your-host"></a>Exécuter le moniteur de Application Insights hello sur votre ordinateur hôte
Maintenant que vous avez quelque part télémétrie de hello toodisplay, vous pouvez définir l’application en conteneur hello qui recueille et envoyez-le.

1. Connecter l’hôte de Docker tooyour. 
2. Modifiez la clé d'instrumentation par cette commande, puis exécutez-la :
   
   ```
   
   docker run -v /var/run/docker.sock:/docker.sock -d microsoft/applicationinsights ikey=000000-1111-2222-3333-444444444
   ```

Une seule image Application Insights est requise par hôte Docker. Si votre application est déployée sur plusieurs hôtes de Docker, puis répétez la commande hello sur chaque hôte.

## <a name="update-your-app"></a>Mise à jour de votre application
Si votre application est instrumentée avec hello [Application Insights SDK pour Java](app-insights-java-get-started.md), ajouter hello ligne suivante dans fichier de ApplicationInsights.xml hello dans votre projet, sous hello `<TelemetryInitializers>` élément :

```xml

    <Add type="com.microsoft.applicationinsights.extensibility.initializer.docker.DockerContextInitializer"/> 
```

Cela ajoute des informations de Docker comme conteneur hôte id tooevery télémétrie élément et envoyé à partir de votre application.

## <a name="view-your-telemetry"></a>Affichage de vos données de télémétrie
Retournez une ressource d’Application Insights tooyour Bonjour portail Azure.

Cliquez dans la vignette de Docker hello.

Vous verrez peu de temps des données en provenance de l’application de Docker hello, surtout si vous avez d’autres conteneurs exécutés sur votre moteur Docker.

Voici certaines des vues hello que vous pouvez obtenir.

### <a name="perf-counters-by-host-activity-by-image"></a>Compteurs de performances par hôte, activité par image
![exemple](./media/app-insights-docker/10.png)

![exemple](./media/app-insights-docker/11.png)

Cliquez sur le nom d'un hôte ou d'une image pour plus de détails.

toocustomize hello, cliquez sur n’importe quel graphique, la grille hello titre ou ajouter un graphique. 

[En savoir plus sur Metrics Explorer](app-insights-metrics-explorer.md).

### <a name="docker-container-events"></a>Événements du conteneur Docker
![exemple](./media/app-insights-docker/13.png)

tooinvestigate des événements individuels, cliquez sur [recherche](app-insights-diagnostic-search.md). Rechercher et filtrer les événements de hello toofind souhaités. Cliquez sur n’importe quel tooget événement plus en détail.

### <a name="exceptions-by-container-name"></a>Exceptions par nom de conteneur
![exemple](./media/app-insights-docker/14.png)

### <a name="docker-context-added-tooapp-telemetry"></a>Contexte de docker ajouté tooapp télémétrie
Télémétrie des requêtes envoyée à partir de l’application hello instrumentée avec le Kit de développement logiciel AI, enrichie avec le contexte de Docker :

![exemple](./media/app-insights-docker/16.png)

Temps du processeur et compteurs de performance mémoire disponible, enrichis et regroupés par nom de conteneur Docker :

![exemple](./media/app-insights-docker/15.png)

## <a name="q--a"></a>Questions et réponses
*Quelles sont les fonctionnalités d’Application Insights qui ne sont pas disponibles dans Docker ?*

* Analyse détaillée des compteurs de performances par conteneur et par image.
* Intégration des données de conteneur et d’application dans un tableau de bord.
* [Exporter les données de télémétrie](app-insights-export-telemetry.md) pour l’autre base de données analysis tooa, Power BI ou tableau de bord.

*Comment obtenir des données de télémétrie à partir de l’application hello proprement dit ?*

* Installez hello Application Insights SDK dans l’application hello. Découvrez comment faire pour : les [applications web Java](app-insights-java-get-started.md), les [applications web Windows](app-insights-asp-net.md).

## <a name="video"></a>Vidéo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Étapes suivantes

* [Application Insights pour Java](app-insights-java-get-started.md)
* [Application Insights pour Node.js](app-insights-nodejs.md)
* [Application Insights pour ASP.NET](app-insights-asp-net.md)
