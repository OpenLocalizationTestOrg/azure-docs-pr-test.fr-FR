---
title: les applications web aaaAzure Application Insights pour JavaScript | Documents Microsoft
description: "Obtention des décomptes de sessions et d’affichages de pages, des données de client web et suivi des modèles d’utilisation. Détection des problèmes de performances et des exceptions dans les pages Web JavaScript."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 3b710d09-6ab4-4004-b26a-4fa840039500
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 986db3c3776471f9f8556f4e09f2d02aad022549
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-web-pages"></a>Application Insights pour les pages web
Découvrez les performances de hello et d’utilisation de votre page web ou d’une application. Si vous ajoutez [Application Insights](app-insights-overview.md) tooyour script de page, vous obtenez le minutage de chargement de page et les appels AJAX, les nombres et détails des exceptions du navigateur et les échecs d’AJAX, ainsi que les utilisateurs et les nombres de la session. Toutes ces données peuvent être segmentées par page, par version de système d’exploitation ou de navigateur client, par emplacement géographique et en fonction d’autres aspects. Vous pouvez définir des alertes en cas de dépassement d’un certain nombre d’échecs ou de ralentissement du chargement des pages. Et en insérant des appels de trace dans votre code JavaScript, vous pouvez suivre l’utilisation des hello différentes fonctionnalités de votre application de la page web.

Vous pouvez utiliser Application Insights avec toutes les pages web ; il vous suffit pour cela d’ajouter un court extrait de code JavaScript. Si votre service web est [Java](app-insights-java-get-started.md) ou [ASP.NET](app-insights-asp-net.md), vous pouvez intégrer les données de télémétrie de votre serveur et de vos clients.

![Dans portal.azure.com, ouvrez les ressources de votre application, puis cliquez sur Navigateur](./media/app-insights-javascript/03.png)

Vous avez besoin d’un abonnement trop[Microsoft Azure](https://azure.com). Si votre équipe dispose d’un abonnement d’organisation, vous pouvez demander hello propriétaire tooadd votre tooit Account Microsoft. Le développement et l’utilisation à petite échelle ne coûtent rien.

## <a name="set-up-application-insights-for-your-web-page"></a>Configurer Application Insights pour votre page web
Ajouter hello chargeur code extrait tooyour des pages web, comme suit.

### <a name="open-or-create-application-insights-resource"></a>Ouverture ou création d’une ressource Application Insights dans Azure
Hello ressource Application Insights est où les données sur les performances et d’utilisation de votre page s’affiche. 

Connectez-vous au [portail Azure](https://portal.azure.com).

Si vous avez déjà défini la surveillance pour le côté du serveur hello de votre application, vous disposez déjà d’une ressource :

![Cliquez sur Parcourir, Services de développement, Application Insights.](./media/app-insights-javascript/01-find.png)

Si vous n'en avez pas, créez-la.

![Cliquez sur Nouveau, Services de développement, Application Insights.](./media/app-insights-javascript/01-create.png)

*Vous avez déjà des questions ?* [Plus d’informations sur la création d’une ressource](app-insights-create-new-resource.md).

### <a name="add-hello-sdk-script-tooyour-app-or-web-pages"></a>Ajouter une application de tooyour script hello SDK ou des pages web
Dans le démarrage rapide, obtenir le script de hello pour les pages web :

![Sur votre Panneau de vue d’ensemble des applications, sélectionnez Démarrage rapide, obtenir code toomonitor Mes pages web. Copiez le script de hello.](./media/app-insights-javascript/02-monitor-web-page.png)

Insérer un script hello juste avant hello `</head>` balise de chaque page, vous souhaitez tootrack. Si votre site Web dispose d’une page maître, vous pouvez placer les script hello il. Par exemple :

* Dans un projet ASP.NET MVC, vous devez placer le script dans `View\Shared\_Layout.cshtml`
* Dans un site SharePoint, dans le panneau de configuration hello, ouvrez [paramètres du Site / Page maître](app-insights-sharepoint.md).

script de Hello contient la clé d’instrumentation hello qui dirige la ressource d’Application Insights hello données tooyour. 

([Une explication plus approfondie du script de hello. ](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))

*(Si vous utilisez une infrastructure de page web connue, cherchez des adaptateurs Application Insights. Par exemple, il existe [un module AngularJS](http://ngmodules.org/modules/angular-appinsights).)*

## <a name="detailed-configuration"></a>Configuration détaillée
Bien que vous puissiez définir plusieurs [paramètres](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) , vous ne devriez pas avoir besoin de le faire dans la plupart des cas. Par exemple, vous pouvez désactiver ou limiter le nombre de hello des appels Ajax signalées par l’affichage de page (trafic tooreduce). Ou bien, vous pouvez définir debug mode toohave télémétrie déplacer rapidement au pipeline de hello sans être traités par lot.

tooset ces paramètres, recherchez la ligne dans l’extrait de code hello et ajouter davantage d’éléments séparés par des virgules :

    })({
      instrumentationKey: "..."
      // Insert here
    });

Hello [paramètres disponibles](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) incluent :

    // Send telemetry immediately without batching.
    // Remember tooremove this when no longer required, as it
    // can affect browser performance.
    enableDebug: boolean,

    // Don't log browser exceptions.
    disableExceptionTracking: boolean,

    // Don't log ajax calls.
    disableAjaxTracking: boolean,

    // Limit number of Ajax calls logged, tooreduce traffic.
    maxAjaxCallsPerView: 10, // default is 500

    // Time page load up tooexecution of first trackPageView().
    overridePageViewDuration: boolean,

    // Set these dynamically for an authenticated user.
    appUserId: string,
    accountId: string,



## <a name="run"></a>Exécution de votre application
Exécuter votre application web, utiliser un lors de la télémétrie de toogenerate et patientez quelques secondes. Vous pouvez exécuter à l’aide de hello **F5** clés sur votre ordinateur de développement, ou publier et permettre aux utilisateurs de le manipuler.

Si vous souhaitez que les données de télémétrie toocheck hello qu’une application web envoie tooApplication Insights, utilisez les outils de débogage de votre navigateur (**F12** sur de nombreux navigateurs). Données sont envoyées toodc.services.visualstudio.com.

## <a name="explore-your-browser-performance-data"></a>Exploration de vos données de performances dans les navigateurs
Ouvrez hello navigateur panneau tooshow agrégée les données de performances à partir de navigateurs de vos utilisateurs.

![Dans portal.azure.com, ouvrez les ressources de votre application, puis cliquez sur Paramètres, Navigateur.](./media/app-insights-javascript/03.png)

*Pas de données pour le moment ? Cliquez sur **Actualiser** en hello haut hello. Toujours rien ? Consultez la rubrique [Résolution des problèmes](app-insights-troubleshoot-faq.md).*

Panneau de navigateur Hello est un [panneau Metrics Explorer](app-insights-metrics-explorer.md) avec des filtres prédéfinis et les sélections de graphique. Vous pouvez modifier la plage de temps hello, de filtres et de configuration des graphiques si vous le souhaitez et enregistrez le résultat de hello en tant que favori. Cliquez sur **restaurer les valeurs par défaut** configuration du panneau tooget toohello arrière d’origine.

## <a name="page-load-performance"></a>Performances de chargement des pages
À hello haut est un graphique segmenté de temps de chargement de page. hauteur totale de Hello du graphique de hello représente des pages de tooload et l’affichage de la durée moyenne hello à partir de votre application dans les navigateurs de vos utilisateurs. temps de Hello est mesuré à partir de lorsque le navigateur de hello envoie la requête HTTP initiale de hello jusqu'à ce que la charge synchrone tous les événements ont été traités, y compris la mise en page et d’exécution de scripts. Elle n’inclut pas les tâches asynchrones telles que le chargement des composants web à partir des appels AJAX.

graphique de Hello segmente les temps de chargement du nombre total de pages hello en hello [minutages standards définis par le W3C](http://www.w3.org/TR/navigation-timing/#processing-model). 

![](./media/app-insights-javascript/08-client-split.png)

Notez que hello *de connexion réseau* heure est souvent inférieure à ce que vous pourriez vous attendre, car elle est une moyenne de toutes les demandes d’hello navigateur toohello le serveur. Nombre de requêtes individuelles ont une durée de connexion 0, car il existe déjà un serveur de toohello de connexion active.

### <a name="slow-loading"></a>Le chargement est lent ?
Les pages qui mettent du temps à se charger constituent une source de mécontentement majeure pour vos utilisateurs. Si le graphique de hello indique le chargement de page lente, il est facile toodo des recherches de diagnostic.

graphique de Hello montre toutes les charges de page moyenne hello dans votre application. toosee si le problème de hello est limitée tooparticular pages, plus détaillée de panneau de hello, dans lequel il existe une grille segmentée par une URL de la page :

![](./media/app-insights-javascript/09-page-perf.png)

Notez le nombre de vues de page hello et l’écart. Si le nombre de pages hello est très faible, puis problème de hello n’est pas affecter d’utilisateurs beaucoup. Un écart type élevé (moyenne toohello comparables lui-même) indique un grand nombre de variation entre des mesures individuelles.

**Zoomez sur une URL et un affichage de page.** Cliquez sur n’importe quel toosee de nom de page une lame de navigateur graphiques filtrés toothat simplement URL ; puis sur une instance d’un affichage de page.

![](./media/app-insights-javascript/35.png)

Cliquez sur `...` pour une liste complète des propriétés pour cet événement, ou examiner les appels Ajax hello et événements connexes. Appels Ajax lents affectent hello page global des temps de chargement s’ils sont synchrones. Liées événements incluent des requêtes au serveur pour hello même URL (si vous avez configuré Application Insights sur votre serveur web).

**Historique des performances de la page.** Revenir au panneau de navigateurs hello, transformer grille de temps de chargement de Page vue hello une toosee graphique de ligne s’il y a des pics à des moments :

![Cliquez sur en-tête hello de grille de hello et sélectionnez un nouveau type de graphique](./media/app-insights-javascript/10-page-perf-area.png)

**Segmentation en fonction d’autres aspects.** Peut-être que vos pages sont tooload plus lent sur un emplacement spécifique de navigateur, du système d’exploitation client ou utilisateur ? Ajouter un nouveau graphique et faire des essais avec hello **Group by** dimension.

![](./media/app-insights-javascript/21.png)

## <a name="ajax-performance"></a>Performances AJAX
Assurez-vous que tous les appels AJAX dans vos pages web fonctionnent correctement. Il s’agit souvent utilisé toofill des parties de votre page de façon asynchrone. Bien que hello page globale peut charger rapidement, vos utilisateurs pourraient confrontés veut WebPart vide, en attente de tooappear de données dans les.

Appels AJAX effectuées à partir de votre page web sont affichés sur le panneau de navigateurs hello en tant que dépendances.

Il existe des graphiques de résumé dans la partie supérieure de hello du Panneau de hello :

![](./media/app-insights-javascript/31.png)

et des grilles détaillées plus bas :

![](./media/app-insights-javascript/33.png)

Cliquez sur n’importe quelle ligne pour obtenir des détails spécifiques.

> [!NOTE]
> Si vous supprimez le filtre de navigateurs hello sur le panneau de hello, serveur et dépendances AJAX sont inclus dans ces graphiques. Cliquez sur le filtre de hello tooreconfigure de paramètres par défaut.
> 
> 

**toodrill dans des échecs d’appels Ajax** défiler la grille de défaillances de dépendance toohello, puis cliquez sur une instance spécifique de toosee de ligne.

![](./media/app-insights-javascript/37.png)


Cliquez sur `...` de télémétrie complète de hello pour un appel Ajax.

### <a name="no-ajax-calls-reported"></a>Aucun appel Ajax n’est signalé ?
Appels AJAX incluent tous les appels HTTP/HTTPS effectuées à partir du script hello de votre page web. Si vous ne voyez pas les signalé, vérifiez hello ne définit pas cet extrait de code hello `disableAjaxTracking` ou `maxAjaxCallsPerView` [paramètres](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).

## <a name="browser-exceptions"></a>Exceptions du navigateur
Dans Panneau de navigateurs hello, il existe un graphique de synthèse des exceptions et une grille des types d’exception plus bas le panneau de hello.

![](./media/app-insights-javascript/39.png)

Si vous ne voyez pas les exceptions de navigateur signalées, vérifiez hello ne définit pas cet extrait de code hello `disableExceptionTracking` [paramètre](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).

## <a name="inspect-individual-page-view-events"></a>Inspection des événements d’affichage de page individuels

La télémétrie de l'affichage de page est généralement analysée par Application Insights, et vous ne consultez que des rapports cumulés, avec une moyenne entre tous les utilisateurs. Toutefois, à des fins de débogage, vous pouvez également consulter des événements d'affichage de page individuels.

Dans le panneau de recherche Diagnostic hello, définir les filtres tooPage vue.

![](./media/app-insights-javascript/12-search-pages.png)

Sélectionnez n’importe quel toosee événement plus en détail. Dans la page de détails de hello, cliquez sur «... » toosee encore plus de détails.

> [!NOTE]
> Si vous utilisez [recherche](app-insights-diagnostic-search.md), notez que vous disposez des mots entiers toomatch : « Ropos » et « à propos de » ne correspondent pas « About ».
> 
> 

Vous pouvez également utiliser hello puissant [de langage de requête Analytique de journal](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) toosearch les vues de page.

### <a name="page-view-properties"></a>Propriétés d'affichage de la page
* **Durée d’affichage de la page** 
  
  * Par défaut, hello fois qu’il prend tooload hello page, à partir du client demande toofull charger (y compris les fichiers auxiliaires mais à l’exclusion des tâches asynchrones tels que les appels Ajax). 
  * Si vous définissez `overridePageViewDuration` Bonjour [configuration de la page](#detailed-configuration), hello intervalle entre tooexecution de demande client Hello tout d’abord `trackPageView`. Si vous avez déplacé trackPageView depuis sa position habituelle après l’initialisation de hello du script de hello, il reflète une valeur différente.
  * Si `overridePageViewDuration` est défini et une durée d’argument est fourni dans hello `trackPageView()` appeler, puis de la valeur de l’argument hello est utilisée à la place. 

## <a name="custom-page-counts"></a>Compteurs de page personnalisés
Par défaut, un nombre de pages se produit chaque fois qu'une nouvelle page est chargée dans le navigateur du client hello.  Toutefois, vous pouvez toocount les vues de page supplémentaires. Par exemple, une page peut afficher son contenu dans les onglets et vous toocount une page lorsque les utilisateur hello bascule onglets. Ou le code JavaScript dans la page de hello peut charger de nouveau contenu sans modifier l’URL du navigateur hello.

Insérer un appel JavaScript comme suit à point hello dans votre code client :

    appInsights.trackPageView(myPageName);

nom de la page Hello peut contenir hello même caractères en tant qu’URL, mais n’est pas défini après « # » ou « ? » est ignoré.

## <a name="usage-tracking"></a>Suivi de l’utilisation
Vous souhaitez toofind les opérations de vos utilisateurs avec votre application ?

* [En savoir plus sur le suivi de l’utilisation](app-insights-web-track-usage.md)
* [En savoir plus sur les événements personnalisés et les API de métriques](app-insights-api-custom-events-metrics.md).

## <a name="video"></a> Vidéo


> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]



## <a name="next"></a> Étapes suivantes
* [Suivi de l'utilisation](app-insights-web-track-usage.md)
* [Mesures et événements personnalisés](app-insights-api-custom-events-metrics.md)
* [Développer-mesurer-apprendre](app-insights-web-track-usage.md)

