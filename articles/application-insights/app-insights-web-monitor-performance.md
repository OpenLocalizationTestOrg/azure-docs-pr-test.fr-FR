---
title: "aaaMonitor de votre application l’intégrité et l’utilisation avec Application Insights"
description: Prise en main d'Application Insights. Analyze usage, availability and performance of your on-premises or Microsoft Azure applications.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 40650472-e860-4c1b-a589-9956245df307
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/25/2015
ms.author: bwren
ms.openlocfilehash: 9230a6e65e5afb00c36122ff1d1de01ba19cd7f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-performance-in-web-applications"></a>Analyse des performances dans les applications web


Assurez-vous que votre application fonctionne correctement et identifiez rapidement toutes les défaillances éventuelles. [Application Insights] [ start] sera vous indiquent des problèmes de performances et des exceptions, et les aident à identifier et de diagnostiquer hello causes.

Application Insights peut surveiller les services WCF, ainsi que les applications et services web Java et ASP.NET. Ils peuvent être hébergés localement, sur des machines virtuelles, ou en tant que sites web Microsoft Azure. 

Côté client de hello, Application Insights peut prendre de télémétrie à partir des pages web et un large éventail de périphériques, notamment iOS, Android et les applications du Windows Store.

>[!Note]
> Nous proposons une nouvelle expérience pour identifier les pages qui ralentissent votre application web. Si vous n’avez pas accès tooit, activez-le en configurant les options de votre version d’évaluation avec hello [panneau d’aperçu](app-insights-previews.md). En savoir plus sur cette nouvelle expérience dans [rechercher et résoudre les goulots d’étranglement de performances avec un examen des performances interactif de hello](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation).

## <a name="setup"></a>Configurer la surveillance des performances
Si vous n’avez pas encore ajouté Application Insights tooyour (autrement dit, s’il n’a pas ApplicationInsights.config) du projet, choisissez une des manières suivantes tooget démarré :

* [Applications web ASP.NET](app-insights-asp-net.md)
  * [Ajout de la surveillance des exceptions](app-insights-asp-net-exceptions.md)
  * [Ajout de la surveillance des dépendances](app-insights-monitor-performance-live-website-now.md)
* [Applications web J2EE](app-insights-java-get-started.md)
  * [Ajout de la surveillance des dépendances](app-insights-java-agent.md)

## <a name="view"></a>Exploration des mesures de performances
Dans [hello portail Azure](https://portal.azure.com), recherchez la ressource Application Insights toohello que vous avez configurée pour votre application. Panneau de vue d’ensemble de Hello affiche des données de performances de base :

Cliquez sur n’importe quel toosee graphique plus en détail et les résultats de toosee pour une période plus longue. Par exemple, cliquez sur la vignette de demandes hello, puis sélectionnez une plage de temps :

![Parcourez les données toomore et sélectionnez une plage de temps](./media/app-insights-web-monitor-performance/appinsights-48metrics.png)

Cliquez sur un graphique toochoose les métriques, il s’affiche, ou ajouter un nouveau graphique et sélectionnez ses mesures :

![Cliquez sur une métrique de toochoose graphique](./media/app-insights-web-monitor-performance/appinsights-61perfchoices.png)

> [!NOTE]
> **Désactivez toutes les métriques hello** sélection complète toosee hello qui est disponible. métriques de Hello sont répartis en groupes ; Lorsqu’un membre d’un groupe est sélectionné, seuls hello autres membres de ce groupe s’affichent.

## <a name="metrics"></a>Signification Vignettes de performances et rapports
Vous pouvez obtenir plusieurs indicateurs de performance. Commençons par ceux qui s’affichent par défaut sur le panneau des applications hello.

### <a name="requests"></a>Requests
nombre de Hello de requêtes HTTP reçues pendant la période spécifiée. Comparer avec les résultats de hello en autres toosee rapports comment votre application se comporte comme hello charge varie.

Les demandes HTTP incluent toutes les demandes GET ou POST de pages, données et images.

Cliquez sur le nombre de tooget vignette hello d’URL spécifiques.

### <a name="average-response-time"></a>Temps de réponse moyen
Mesure le temps hello entre une demande web entrant dans votre réponse d’application et hello qui est retourné.

points de Hello indiquent le déplacement d’une moyenne. S’il existe un grand nombre de requêtes, il peut certaines écarter moyenne hello sans un pic évident ou plonger dans le graphique de hello.

Recherchez les pics inhabituels. En règle générale, vous attendre toorise de temps de réponse avec une augmentation des demandes. Si l’augmentation de hello est disproportionnée, votre application peut être en appuyant sur une limite de ressource telles que de la capacité d’UC ou de hello d’un service, qu'il utilise.

Cliquez sur heures de tooget hello vignette d’URL spécifiques.

![](./media/app-insights-web-monitor-performance/appinsights-42reqs.png)

### <a name="slowest-requests"></a>Demandes les plus lentes
![](./media/app-insights-web-monitor-performance/appinsights-44slowest.png)

Indique les demandes dont les performances doivent probablement être améliorées.

### <a name="failed-requests"></a>Demandes ayant échoué
![](./media/app-insights-web-monitor-performance/appinsights-46failed.png)

Décompte des demandes qui ont généré des exceptions non interceptées.

Cliquez sur hello vignette toosee hello détails des erreurs spécifiques, puis sélectionnez un toosee demande individuelle ses détails. 

Seul un échantillon représentatif des échecs est prélevé pour chaque inspection individuelle.

### <a name="other-metrics"></a>Autres métriques
toosee les autres métriques que vous pouvez afficher et cliquez sur un graphique, puis désélectionnez hello métriques toosee hello disponible définis. Cliquez sur (i) toosee les définition de chaque mesure.

![Désélectionnez l’option jeu toutes les métriques toosee hello entier](./media/app-insights-web-monitor-performance/appinsights-62allchoices.png)

En sélectionnant les hello métrique désactive d’autres qui ne peut pas apparaître sur hello même graphique.

## <a name="set-alerts"></a>Définir des alertes
toobe informé par courrier électronique de valeurs inhabituelles de toute mesure, ajouter une alerte. Vous pouvez choisir des administrateurs de comptes toohello toosend hello par courrier électronique, ou d’adresses de messagerie toospecific.

![](./media/app-insights-web-monitor-performance/appinsights-413setMetricAlert.png)

Ressource hello hello avant de définir d’autres propriétés. Ne choisissez pas les ressources de test Web hello si vous souhaitez que les alertes tooset sur les performances ou métriques d’utilisation.

Être prudent toonote unités de hello dans lequel vous êtes invité à valeur de seuil tooenter hello.

*Je ne vois pas bouton alerte de hello ajouter.* -S’agit-il d’un toowhich de compte de groupe vous avez accès en lecture seule ? Consultez l’administrateur de compte hello.

## <a name="diagnosis"></a>Problèmes de diagnostic
Voici quelques conseils pour identifier et diagnostiquer les problèmes de performances :

* Configurer [tests web] [ availability] toobe averti si votre site web tombe en panne ou répond lentement ou de façon incorrecte. 
* Comparer le nombre de demandes hello avec d’autres toosee de métriques si les échecs ou les temps de réponse sont tooload connexe.
* [Insérer et rechercher les instructions de trace] [ diagnostic] dans votre code toohelp identifie les problèmes.
* Surveillez votre application Web en cours avec le [Flux de métriques temps réel][livestream].
* Capturer l’état hello de votre application .net avec [instantané débogueur][snapshot].

## <a name="find-and-fix-performance-bottlenecks-with-an-interactive-performance-investigation"></a>Rechercher et corriger les goulots d’étranglement avec une analyse de performances interactive

Vous pouvez utiliser hello nouvelle Application Insights interactif enquête toolocate domaines de performances de votre application Web qui ralentissent les performances globales. Vous pouvez rapidement rechercher des pages spécifiques qui sont ralentir et utilisent hello [outil de profilage](app-insights-profiler.md) toosee s’il existe une corrélation entre ces pages.

### <a name="create-a-list-of-slow-performing-pages"></a>Créer la liste des pages lentes 

première étape de Hello pour détecter les problèmes de performances est tooget une liste de hello lente à répondre de pages. Hello capture d’écran ci-dessous illustre l’utilisation de hello performances panneau tooget une liste de potentiels tooinvestigate pages supplémentaires. Vous pouvez rapidement voir à partir de cette page qu’il a été un ralentissement hello temps de réponse de l’application hello à environ 6 h 00 et à nouveau à environ 10 PM. Vous pouvez également voir que l’opération de client/détails hello GET a rencontré quelques opérations longues avec un temps de réponse médian de 507.05 millisecondes. 

![Performances interactives d’Application Insights](./media/app-insights-web-monitor-performance/performance1.png)

### <a name="drill-down-on-specific-pages"></a>Examen approfondi de pages

Dès que vous avez un instantané des performances de votre application, vous pouvez obtenir plus d’informations sur les certaines opérations lentes. Cliquez sur une quelconque opération hello liste toosee hello détails comme indiqué ci-dessous. Graphique de hello, vous pouvez voir si les performances de hello était basée sur une dépendance. Vous pouvez également voir combien hello expérimentés d’utilisateurs différents temps de réponse. 

![Panneau des opérations d’Application Insights](./media/app-insights-web-monitor-performance/performance5.png)

### <a name="drill-down-on-a-specific-time-period"></a>Examen approfondi d’une période

Après avoir identifié une limite dans le temps tooinvestigate, descendez encore plu toolook à des opérations spécifiques hello ayant pu causer un ralentissement des performances hello. Lorsque vous cliquez sur un point spécifique dans le temps vous obtenez les détails de hello de page hello comme indiqué ci-dessous. Bonjour exemple ci-dessous, vous pouvez voir les opérations hello répertoriées pour une période donnée, ainsi que les codes de réponse du serveur hello et la durée d’une opération hello. Vous avez également hello url pour l’ouverture d’un élément de travail TFS si vous avez besoin toosend cette équipe de développement tooyour plus d’informations.

![Tranche horaire d’Application Insights](./media/app-insights-web-monitor-performance/performance2.png)

### <a name="drill-down-on-a-specific-operation"></a>Examen approfondi d’une opération

Après avoir identifié une limite dans le temps tooinvestigate, descendez encore plu toolook à des opérations spécifiques hello ayant pu causer un ralentissement des performances hello. Cliquez sur une opération de hello répertorier toosee hello les détails de l’opération hello comme indiqué ci-dessous. Dans cet exemple, que vous pouvez voir que hello opération a échoué, et Application Insights a fourni les informations de hello Hello a généré l’application de hello d’exception. Là encore, vous pouvez facilement créer un élément de travail TFS à partir de ce panneau.

![Panneau des opérations d’Application Insights](./media/app-insights-web-monitor-performance/performance3.png)


## <a name="next"></a>Étapes suivantes
[Tests Web] [ availability] -demandes web ont envoyés tooyour application à intervalles réguliers à partir de monde hello.

[Capturer et rechercher les traces de diagnostic] [ diagnostic] - insérer le suivi des appels et passer en revue les problèmes de toopinpoint résultats hello.

[Suivi de l’utilisation][usage] : découvrez comment ce que les utilisateurs font avec votre application.

[Résolution des problèmes][qna] et Questions et réponses



<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
[usage]: app-insights-web-track-usage.md
[livestream]: app-insights-live-stream.md
[snapshot]: app-insights-snapshot-debugger.md



