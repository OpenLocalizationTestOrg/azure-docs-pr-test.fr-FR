---
title: applications aaaDebug avec Azure Application Insights dans Visual Studio | Documents Microsoft
description: "Analyse des performances d’application web et diagnostics en phase de débogage et de production."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 2059802b-1131-477e-a7b4-5f70fb53f974
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/7/2017
ms.author: bwren
ms.openlocfilehash: 20491fbe4505bf719039e5d1c220b1afec01db25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-applications-with-azure-application-insights-in-visual-studio"></a>Débogage d’applications à l’aide d’Azure Application Insights dans Visual Studio
Visual Studio 2015 (et versions ultérieures) vous permet d’analyser les performances et de diagnostiquer les problèmes au niveau de votre application web ASP.NET aussi bien en phase de débogage qu’en production, à l’aide des données de télémétrie [d’Azure Application Insights](app-insights-overview.md).

Si vous avez créé votre application de web ASP.NET à l’aide de Visual Studio 2017 ou une version ultérieure, il a déjà hello Application Insights SDK. Sinon, si vous n’avez pas déjà fait, [ajouter Application Insights tooyour application](app-insights-asp-net.md).

toomonitor votre application lorsqu’il est dans un environnement de production, vous normalement Affichez les données de télémétrie Application Insights hello Bonjour [portail Azure](https://portal.azure.com), où vous pouvez définir des alertes et appliquer des outils d’analyse puissants. Mais, pour le débogage, vous pouvez également rechercher et analysez la télémétrie hello dans Visual Studio. Vous pouvez utiliser les données de télémétrie tooanalyze Visual Studio de votre site de production et de débogage s’exécute sur votre ordinateur de développement. Dans ce dernier cas de hello, vous pouvez analyser les séries de débogage même si vous n’avez pas encore configuré hello SDK toosend télémétrie toohello portail Azure. 

## <a name="run"></a> Débogage de votre projet
Exécutez votre application web en mode de débogage local à l’aide de la touche F5. Ouvrir des pages différentes toogenerate certaines données de télémétrie.

Dans Visual Studio, vous consultez un nombre d’événements de hello qui ont été consignés par le module d’Application Insights hello dans votre projet.

![Dans Visual Studio, le bouton d’Application Insights hello montre pendant le débogage.](./media/app-insights-visual-studio/appinsights-09eventcount.png)

Cliquez sur ce bouton toosearch votre télémétrie. 

## <a name="application-insights-search"></a>Recherche Application Insights
fenêtre de recherche Application Insights Hello présente les événements qui ont été enregistrés. (Si vous connecté tooAzure lorsque vous installez Application Insights, vous pouvez rechercher hello les mêmes événements Bonjour portail Azure.)

![Droit hello projet, puis choisissez Application Insights, recherche](./media/app-insights-visual-studio/34.png)

> [!NOTE] 
> Une fois que vous sélectionnez ou désélectionnez les filtres, cliquez sur le bouton de recherche hello à fin hello du champ de recherche de texte hello.
>

recherche en texte libre Hello fonctionne sur tous les champs dans les événements hello. Par exemple, rechercher une partie de l’URL de hello d’une page ; ou valeur hello d’une propriété telle que ville du client ; ou des mots spécifiques dans un journal des traces.

Cliquez sur n’importe quel toosee événement ses propriétés détaillées.

Pour les demandes tooyour web app, vous pouvez cliquer sur toohello code.

![Sous Détails de la demande, cliquez sur dans le code de toohello](./media/app-insights-visual-studio/31.png)

Vous pouvez également ouvrir des éléments connexes toohelp diagnostiquer les échecs de demandes ou des exceptions.

![Sous Détails de la demande, faites défiler la liste des éléments toorelated](./media/app-insights-visual-studio/41.png)

## <a name="view-exceptions-and-failed-requests"></a>Afficher les exceptions et les requêtes ayant échoué
Exception afficher de rapports dans la fenêtre de recherche hello. (Dans certains types plus anciens d’application ASP.NET, vous avez trop[configurer l’analyse des exceptions](app-insights-asp-net-exceptions.md) toosee les exceptions qui sont gérées par le framework de hello.)

Cliquez sur une exception de tooget une trace de pile. Si le code hello de l’application hello est ouvert dans Visual Studio, vous pouvez cliquer à partir de hello pile trace toohello ligne appropriée du code de hello.

![Arborescence des appels de procédure d’exception](./media/app-insights-visual-studio/17.png)

## <a name="view-request-and-exception-summaries-in-hello-code"></a>Afficher les récapitulatifs de demande et de l’exception dans le code hello
Dans la ligne de Code thématique au-dessus de chaque méthode de gestionnaire de hello, vous consultez un nombre de demandes de hello et exceptions consignées par Application Insights Bonjour dernières 24 heures.

![Arborescence des appels de procédure d’exception](./media/app-insights-visual-studio/21.png)

> [!NOTE] 
> Codelens affiche uniquement les données d’Application Insights si vous avez [configuré votre portail Application Insights toohello de télémétrie de toosend application](app-insights-asp-net.md).
>

[En savoir plus sur Application Insights dans le filtre Code](app-insights-visual-studio-codelens.md)

## <a name="trends"></a>Trends
Trends est un outil permettant de visualiser le comportement de votre application au fil du temps. 

Choisissez **Explorer les tendances de télémétrie** à partir de bouton de barre d’outils Application Insights hello ou recherche Application Insights. Choisissez une des cinq tooget de requêtes courantes a démarré. Vous pouvez analyser différents jeux de données en fonction des types de télémétrie, des intervalles de temps ainsi que d’autres propriétés. 

anomalies toofind dans vos données, choisissez une des options d’anomalie hello sous la liste déroulante du « Type d’affichage » hello. options de filtrage Hello bas hello de fenêtre hello qu’il soit facile toohone dans sur des sous-ensembles spécifiques de votre télémétrie.

![Trends](./media/app-insights-visual-studio/51.png)

[En savoir plus sur Tendances](app-insights-visual-studio-trends.md).

## <a name="local-monitoring"></a>Surveillance locale
(À partir de Visual Studio 2015 Update 2) Si vous n’avez pas configuré le portail Application Insights de hello SDK toosend télémétrie toohello (pour qu’il n’y a aucune clé d’instrumentation dans ApplicationInsights.config) puis hello diagnostics affiche télémétrie à partir de votre session de débogage plus récentes. 

C’est le comportement adéquat si vous avez déjà publié une version antérieure de votre application. Vous ne souhaitez pas que votre toobe de sessions de débogage télémétrie hello confondues télémétrie hello sur hello portail Application Insights à partir de l’application publiée hello.

Il est également utile si vous disposez d’un [une télémétrie personnalisée](app-insights-api-custom-events-metrics.md) que vous souhaitez toodebug avant d’envoyer le portail de toohello de télémétrie.

* *Dans un premier temps, j’ai configuré entièrement portail de toohello télémétrie Application Insights toosend. Mais maintenant je souhaite que les données de télémétrie toosee hello uniquement dans Visual Studio.*
  
  * Paramètres de la fenêtre de recherche hello, est une option toosearch local de diagnostic même si votre application envoie un portail toohello de télémétrie.
  * télémétrie toostop envoyée portail toohello, commentez la ligne de hello `<instrumentationkey>...` à partir de ApplicationInsights.config. Lorsque vous êtes à nouveau portail de toohello toosend prêt télémétrie, supprimez les commentaires.


## <a name="next-steps"></a>Étapes suivantes
|  |  |
| --- | --- |
| **[Ajouter des données](app-insights-asp-net-more.md)**<br/>Analysez l’utilisation, la disponibilité, les dépendances et les exceptions. Intégrer des traces à partir des frameworks de journalisation. Écrire des données de télémétrie personnalisées. |![Visual Studio](./media/app-insights-visual-studio/64.png) |
| **[Utilisation de portail d’Application Insights hello](app-insights-dashboards.md)**<br/>Affichez les tableaux de bord, les puissants outils de diagnostic et d’analyse, les alertes, le mappage direct des dépendances de votre application et les données de télémétrie exportées. |![Visual Studio](./media/app-insights-visual-studio/62.png) |

