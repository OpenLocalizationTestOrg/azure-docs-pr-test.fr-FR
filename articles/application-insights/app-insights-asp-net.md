---
title: "aaaSet d’analytique d’application web ASP.NET avec Azure Application Insights | Documents Microsoft"
description: "Configurez les performances, la disponibilité et l’analyse de l’utilisation de votre site web ASP.NET, hébergé en local ou dans Azure."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d0eee3c0-b328-448f-8123-f478052751db
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: 61a3cdce68da48bfb9450b1d296acc1535f50a38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-application-insights-for-your-aspnet-website"></a>Configurer Application Insights pour votre site web ASP.NET

Cette procédure configure votre toohello de télémétrie ASP.NET web application toosend [Azure Application Insights](app-insights-overview.md) service. Il fonctionne pour les applications ASP.NET qui sont hébergées dans votre propre serveur IIS ou dans hello Cloud. Vous obtenez des graphiques et un langage de requête puissante qui vous aident à comprendre les performances hello de votre application et d’utilisation, ainsi que des alertes automatiques sur les échecs ou les problèmes de performances. De nombreux développeurs trouvent ces fonctionnalités très comme ils le sont, mais vous pouvez également étendre et personnaliser les données de télémétrie hello si vous avez besoin.

L’installation se fait en seulement quelques clics dans Visual Studio. Vous avez des frais de tooavoid option hello en limitant le volume hello de télémétrie. Cela vous permet de tooexperiment et de débogage ou toomonitor un site avec pas de nombreux utilisateurs. Lorsque vous décidez de vous le souhaitez toogo avance et surveillez votre site de production, il est plus tard limite de hello tooraise facile.

## <a name="before-you-start"></a>Avant de commencer
Ce dont vous avez besoin :

* Visual Studio 2013 Update 3 ou version ultérieure. Il est préférable d’utiliser une version ultérieure.
* Un abonnement trop[Microsoft Azure](http://azure.com). Si votre équipe ou organisation dispose d’un abonnement Azure, hello propriétaire peut ajouter vous tooit, à l’aide de votre [compte Microsoft](http://live.com).

Il existe des toolook d’autres rubriques à si vous êtes intéressé par :

* [Instrumentation d’une application web au moment de l’exécution](app-insights-monitor-performance-live-website-now.md)
* [Azure Cloud Services](app-insights-cloudservices.md)

## <a name="ide"></a>Étape 1 : Ajouter hello Application Insights SDK

Cliquez avec le bouton droit sur votre projet d’application web dans l’Explorateur de solutions et sélectionnez **Ajouter** > **Application Insights Telemetry...** ou **Configurer Application Insights**.

![Capture d’écran de l’Explorateur de solutions, avec l’option Ajouter Application Insights Telemetry en surbrillance](./media/app-insights-asp-net/appinsights-03-addExisting.png)

(Dans Visual Studio 2015, il existe également une option de tooadd Application Insights dans la boîte de dialogue Nouveau projet hello.)

Continuer la page de configuration d’Application Insights toohello :

![Capture d’écran de la page Inscrire votre application auprès d’Application Insights](./media/app-insights-asp-net/visual-studio-register-dialog.png)

**a.** Sélectionnez le compte de hello et l’abonnement que vous utilisez tooaccess Azure.

**b.** Sélectionnez les ressources hello dans Azure où vous souhaitez les données de salutation toosee à partir de votre application. En règle générale :

* Utilisez une [seule ressource pour les différents composants](app-insights-monitor-multi-role-apps.md) d’une application unique. 
* Créez des ressources distinctes pour les applications non liées.
 
Si vous souhaitez tooset hello ressource groupe ou hello l’emplacement où sont stockées vos données, cliquez sur **configurer les paramètres**. Groupes de ressources sont utilisées toocontrol accès toodata. Par exemple, si vous avez plusieurs applications qui font partie de hello même système, vous pouvez placer leurs données d’Application Insights hello du même groupe de ressources.

**c.** Limite de volume de données libre hello, tooavoid frais, définissez une limite. Application Insights est Libérez tooa certain volume de données de télémétrie. Après la création de la ressource de hello, vous pouvez modifier votre sélection dans le portail de hello en ouvrant **fonctionnalités + tarification** > **gestion des volumes de données** > **quotidienne extrémité de volume**.

**d.** Cliquez sur **inscrire** toogo avance et configurer Application Insights pour votre application web. Télémétrie sera envoyée toohello [portail Azure](https://portal.azure.com), pendant le débogage et une fois que vous avez publié votre application.

**e.** Si vous ne souhaitez portal de toohello toosend télémétrie pendant le débogage, juste ajouter hello Application Insights SDK tooyour application mais ne configurez pas une ressource dans le portail de hello. Vous serez en mesure de toosee de données de télémétrie de Visual Studio pendant le débogage. Plus tard, vous pouvez retourner la page de configuration toothis, ou vous pouvez attendre après avoir déployé votre application et [passer des données télémétriques fournies au moment de l’exécution](app-insights-monitor-performance-live-website-now.md).


## <a name="run"></a> Étape 2 : exécution de votre application
Exécutez votre application en appuyant sur F5. Ouvrir des pages différentes toogenerate certaines données de télémétrie.

Dans Visual Studio, vous consultez un nombre d’événements de hello qui ont été enregistrés.

![Capture d’écran de Visual Studio. bouton d’Application Insights Hello s’affiche pendant le débogage.](./media/app-insights-asp-net/54.png)

## <a name="step-3-see-your-telemetry"></a>Étape 3 : afficher vos données de télémétrie
Vous pouvez voir votre télémétrie dans Visual Studio ou dans le portail web hello Application Insights. Rechercher les données de télémétrie dans Visual Studio toohelp vous déboguez votre application. Surveiller les performances et l’utilisation dans le portail web hello lorsque votre système est dynamique. 

### <a name="see-your-telemetry-in-visual-studio"></a>Afficher vos données de télémétrie dans Visual Studio

Dans Visual Studio, ouvrez la fenêtre d’Application Insights hello. Cliquez sur hello **Application Insights** bouton, ou avec le bouton droit de votre projet dans l’Explorateur de solutions, sélectionnez **Application Insights**, puis cliquez sur **recherche Live télémétrie**.

Dans la fenêtre de recherche de Visual Studio Application Insights hello, consultez hello **les données à partir de la session de débogage** vue de télémétrie généré côté serveur hello votre application. Faire des essais avec des filtres hello, puis cliquez sur n’importe quel toosee d’événement de plus en détail.

![Capture d’écran de hello de vue de données à partir de la session de débogage dans la fenêtre d’Application Insights hello.](./media/app-insights-asp-net/55.png)

> [!NOTE]
> Si vous ne voyez pas toutes les données, assurez-vous que plage de temps hello est correct, cliquez sur icône de recherche hello.

[En savoir plus sur les outils Application Insights dans Visual Studio](app-insights-visual-studio.md).

<a name="monitor"></a>
### <a name="see-telemetry-in-web-portal"></a>Afficher les données de télémétrie dans le portail web

Vous pouvez également voir les données de télémétrie dans le portail web hello Application Insights (sauf si vous avez choisi hello uniquement de tooinstall SDK). portail de Hello a plusieurs graphiques, des outils d’analyse et vues entre composants de Visual Studio. portail de Hello fournit également des alertes.

Ouvrez votre ressource Application Insights. Soit vous connecter toohello [portail Azure](https://portal.azure.com/) rechercher celui-ci ou avec le bouton hello projet dans Visual Studio et il permettent d’y accéder.

![Capture d’écran de Visual Studio, montrant comment tooopen hello portail Application Insights](./media/app-insights-asp-net/appinsights-04-openPortal.png)

> [!NOTE]
> Si vous obtenez une erreur d’accès : vous avez plus d’un jeu d’informations d’identification de Microsoft, et si vous êtes connecté avec un jeu incorrect hello ? Dans le portail hello, déconnectez-vous et reconnectez-vous.

portail de Hello s’ouvre sur une vue de données de télémétrie hello à partir de votre application.

![Capture d’écran de la page de présentation Application Insights](./media/app-insights-asp-net/66.png)

Dans le portail hello, cliquez sur n’importe quel toosee vignette ou un graphique plus en détail.

[En savoir plus sur l’utilisation d’Application Insights Bonjour Azure portal](app-insights-dashboards.md).

## <a name="step-4-publish-your-app"></a>Étape 4 : publication de votre application
Publier le serveur IIS application tooyour des tooAzure. Espion [flux Live de métriques](app-insights-metrics-explorer.md#live-metrics-stream) toomake que tout fonctionne correctement.

Votre télémétrie construit dans le portail Application Insights hello, où vous pouvez surveiller les mesures, rechercher vos données de télémétrie et configurer [tableaux de bord](app-insights-dashboards.md). Vous pouvez également utiliser hello puissant [de langage de requête Analytique de journal](https://docs.loganalytics.io/) tooanalyze toofind et les performances ou l’utilisation des événements spécifiques.

Vous pouvez également continuer tooanalyze vos données de télémétrie de [Visual Studio](app-insights-visual-studio.md), avec des outils, tels que la recherche de diagnostic et [les tendances](app-insights-visual-studio-trends.md).

> [!NOTE]
> Si votre application envoie suffisamment hello tooapproach de télémétrie [limites](app-insights-pricing.md#limits-summary)automatique [échantillonnage](app-insights-sampling.md) bascule. Échantillonnage réduit la quantité de hello de télémétrie envoyé à partir de votre application, tout en conservant les données mises en corrélation pour établir un diagnostic.
>
>

## <a name="land"></a> Vous êtes prêt.

Félicitations ! Vous dans votre application le package d’Application Insights hello installé et configuré de service d’Application Insights toosend télémétrie toohello sur Azure.

![Diagramme du mouvement des données de télémétrie](./media/app-insights-asp-net/01-scheme.png)

Hello ressource Azure qui reçoit les données de télémétrie de votre application est identifiée par un *clé d’instrumentation*. Vous trouverez cette clé dans le fichier ApplicationInsights.config de hello.


## <a name="upgrade-toofuture-sdk-versions"></a>Mise à niveau des versions du Kit de développement logiciel toofuture
tooupgrade tooa [nouvelle version du Kit de développement logiciel de hello](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases), ouvrez hello **Gestionnaire de package NuGet** à nouveau et filtre sur les packages installés. Sélectionnez **Microsoft.ApplicationInsights.Web** et choisissez **Mettre à niveau**.

Si vous avez apporté des personnalisations tooApplicationInsights.config, enregistrez une copie de mettre à niveau. Ensuite, fusionnez vos modifications dans la nouvelle version de hello.

## <a name="video"></a>Vidéo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Étapes suivantes

### <a name="more-telemetry"></a>Données de télémétrie supplémentaires

* **[Données de navigateur et de chargement de page](app-insights-javascript.md)** : insérez un extrait de code dans vos pages web.
* **[Obtenir des dépendances et une analyse des exceptions plus détaillées](app-insights-monitor-performance-live-website-now.md)** : installez Status Monitor sur votre serveur.
* **[Événements personnalisés de code](app-insights-api-custom-events-metrics.md)**  toocount, d’heure ou de mesurer les actions de l’utilisateur.
* **[Obtenir des données de journalisation](app-insights-asp-net-trace-logs.md)** : corrélez les données de journalisation avec vos données de télémétrie.

### <a name="analysis"></a>Analyse

* **[Utilisation d’Application Insights dans Visual Studio](app-insights-visual-studio.md)**<br/>Inclut des informations sur le débogage avec les données de télémétrie, recherche de diagnostic et d’extraction toocode.
* **[Utilisation de portail d’Application Insights hello](app-insights-dashboards.md)**<br/> Inclut des informations sur les tableaux de bord, les puissants outils de diagnostic et d’analyse, les alertes, le mappage direct des dépendances de votre application et l’exportation des données de télémétrie.
* **[Analytique](app-insights-analytics-tour.md)**  -hello du langage de requête puissantes.

### <a name="alerts"></a>Alertes

* [Tests de disponibilité](app-insights-monitor-web-app-availability.md): créer des tests toomake que votre site est visible sur le web de hello.
* [Smart diagnostics](app-insights-proactive-diagnostics.md): ces tests exécutés automatiquement, vous n’avez donc toodo n’est pas défini tooset de. Ils vous indiquent si votre application affiche un taux inhabituel de demandes ayant échoué.
* [Alertes métriques](app-insights-alerts.md): définir ces toowarn si une métrique dépasse un seuil. Vous pouvez définir des mesures personnalisées que vous codez dans votre application.

### <a name="automation"></a>Automatisation

* [Automatisation de la création d’une ressource Application Insights](app-insights-powershell.md)
