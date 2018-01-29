---
title: "Vue d’ensemble d’Azure Application Insights pour DevOps | Microsoft Docs"
description: "Découvrez comment utiliser Application Insights dans un environnement DevOps."
author: mrbullwinkle
services: application-insights
documentationcenter: 
manager: carmonm
ms.assetid: 6ccab5d4-34c4-4303-9d3b-a0f1b11e6651
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.custom: mvc
ms.topic: overview
ms.date: 06/26/2017
ms.author: mbullwin
ms.openlocfilehash: b83d08b9dac4fccc033ad4537afd343a6fbe02c2
ms.sourcegitcommit: e462e5cca2424ce36423f9eff3a0cf250ac146ad
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2017
---
# <a name="overview-of-application-insights-for-devops"></a>Vue d’ensemble d’Application Insights pour DevOps

Avec [Application Insights](app-insights-overview.md), vous avez la possibilité de connaître rapidement les performances et l’utilisation de votre application active. Il vous informe en cas de problème, vous permet d’évaluer son impact et vous aide à en déterminer la cause.

Voici le compte d'une équipe qui développe des applications web :

* *« Il y a quelques jours, nous avons déployé un correctif secondaire. Nous n'avons pas effectué de tests complets, mais malheureusement certaines modifications inattendues ont été ajoutées à la charge utile, ce qui a créé une incompatibilité entre le début et la fin. Immédiatement, des exceptions sont apparues sur le serveur, nos alertes se sont déclenchées et nous avons été mis au fait de la situation. En quelques clics sur le portail Application Insights, nous avons obtenu suffisamment d'informations dans la pile des appels d'exception pour cerner le problème. Nous avons immédiatement restauré la version précédente et limité les dégâts. Application Insights facilite et simplifie cette partie du cycle des opérations de développement. »*

Dans cet article, nous suivons une équipe de la banque Fabrikam qui développe le système d’opérations bancaires en ligne, dans le but de voir comment elle utilise Application Insights pour répondre rapidement aux clients et effectuer des mises à jour.  

L’équipe travaille selon un cycle DevOps décrit dans l’illustration suivante :

![Cycle DevOps](./media/app-insights-detect-triage-diagnose/00-devcycle.png)

Les exigences alimentent leur backlog de développement (liste des tâches). Ils travaillent en sprints courts, qui permettent souvent de livrer des logiciels fonctionnels, généralement sous la forme d'améliorations et d'extensions d'une application existante. L'application active est fréquemment mise à jour avec de nouvelles fonctionnalités. Lorsqu'elle est active, l'équipe analyse ses performances et son utilisation à l'aide d'Application Insights. Les données de gestion des performances des applications alimentent leur backlog de développement.

L'équipe utilise Application Insights pour surveiller de l'application web active en termes pour :

* Les performances. Elle cherche à comprendre comment les temps de réponse varient en fonction du nombre de demandes, quelles ressources de l’UC, de réseau, de disque et autres sont utilisées, quel code d’application a ralenti les performances et où se trouvent les goulots d’étranglement.
* Les échecs. S'il existe des exceptions ou des demandes ayant échoué, ou si un compteur de performances dépasse sa plage de confort, l'équipe doit en être rapidement informée pour pouvoir prendre des mesures.
* L’utilisation. Lorsqu'une nouvelle fonctionnalité est disponible, l'équipe souhaite savoir dans quelle mesure elle est utilisée et si les utilisateurs rencontrent des difficultés avec elle.

Penchons-nous à présent sur la partie rétroaction du cycle :

![Détection-tri-diagnostic](./media/app-insights-detect-triage-diagnose/01-pipe1.png)

## <a name="detect-poor-availability"></a>Détecter une faible disponibilité
Marcela Markova est développeur senior de l'équipe OBS et elle est responsable de la surveillance des performances en ligne. Elle configure plusieurs [tests de disponibilité](app-insights-monitor-web-app-availability.md) :

* Un test d’URL unique pour la page d’accueil principale de l’application, http://fabrikambank.com/onlinebanking/. Elle définit des critères de code HTTP 200 et le texte « Bienvenue ! ». Si ce test échoue, il y a un sérieux problème de réseau ou un problème sur les serveurs, voire un problème de déploiement. (Ou bien quelqu'un a modifié sans l'informer le message de bienvenue sur la page d'accueil.)
* Un test en plusieurs étapes plus en profondeur, qui se connecte et obtient la liste des comptes actuels, en vérifiant quelques détails importants sur chaque page. Ce test vérifie que le lien vers la base de données des comptes fonctionne. Elle utilise un ID de client fictif : elle en conserve quelques-uns pour ses tests.

Une fois ces tests configurés, Marcela sait que l'équipe sera rapidement avertie en cas d'interruption.  

Les défaillances sont indiquées par des points rouge dans le graphique de test web :

![Affichage des tests web exécutés sur la période précédente](./media/app-insights-detect-triage-diagnose/04-webtests.png)

Mais, surtout, une alerte est envoyée à l’équipe de développement en cas de défaillance. De cette façon, ils en sont informés presque avant tous les clients.

## <a name="monitor-performance"></a>Analyser les performances
Dans la page Vue d’ensemble d’Application Insights, un graphique montre une série de [mesures clés](app-insights-web-monitor-performance.md).

![Différentes mesures](./media/app-insights-detect-triage-diagnose/05-perfMetrics.png)

Le temps de chargement de la page du navigateur provient de la télémétrie envoyée directement depuis vos pages web. Le temps de réponse du serveur, le nombre de demandes au serveur et le nombre de demandes ayant échoué sont mesurés dans le serveur web puis envoyés à Application Insights à partir de là.

Marcela est légèrement préoccupée par le graphique de réponse du serveur. Ce graphique affiche la durée moyenne entre le moment où le serveur reçoit une demande HTTP depuis le navigateur d’un utilisateur et le moment où il renvoie la réponse. Il n’est pas rare de voir une variation dans ce graphique, car la charge sur le système varie. Mais, dans ce cas, il semble y avoir une corrélation entre une légère augmentation du nombre de demandes et une augmentation conséquente du temps de réponse. Cela peut indiquer que le système a atteint ses limites de fonctionnement.

Elle ouvre les graphiques Serveurs (Serveurs)  :

![Différentes mesures](./media/app-insights-detect-triage-diagnose/06.png)

Il semble n’y avoir aucun signe de limitation de ressources. L’augmentation des temps de réponse du serveur sur le graphique est peut-être en fait tout simplement une coïncidence.

## <a name="set-alerts-to-meet-goals"></a>Définir des alertes pour atteindre les objectifs
Néanmoins, elle souhaite continuer à surveiller les temps de réponse. Elle souhaite être avertie immédiatement s’ils sont trop élevés.

Elle définit alors une [alerte](app-insights-metrics-explorer.md) si les temps de réponse dépassent un seuil standard. Ainsi, elle est certaine d’être avertie en cas de temps de réponse lents.

![Ajouter un panneau d'alerte](./media/app-insights-detect-triage-diagnose/07-alerts.png)

Des alertes peuvent être définies sur une grande variété d’autres mesures. Par exemple, vous pouvez recevoir des courriers électroniques si le nombre d'exceptions est trop élevé ou si la mémoire disponible est faible, ou bien s'il existe un pic dans les demandes des clients.

## <a name="stay-informed-with-smart-detection-alerts"></a>Rester informé grâce aux alertes de détection intelligentes
Le jour suivant, un message électronique d’alerte est généré depuis Application Insights. Mais, lorsqu’elle l’ouvre, elle se rend compte qu’il ne s’agit pas de l’alerte de temps de réponse qu’elle a définie. Au lieu de cela, elle lui indique qu’il y a eu une augmentation soudaine du nombre de demandes ayant échoué (autrement dit, les demandes qui ont renvoyé des codes d’erreur d’au moins 500).

Les demandes ayant échoué sont celles dans lesquelles les utilisateurs ont vu une erreur, généralement suite à une exception levée dans le code. Peut-être ont-ils vu un message indiquant « Nous ne pouvons pas mettre à jour vos informations maintenant » ou, dans le pire des cas, le vidage de la pile sur l'écran de l'utilisateur, via le serveur web.

Cette alerte est une surprise, car, au dernier contrôle, le nombre de demandes ayant échoué était relativement peu élevé. Un petit nombre d’échecs est à prévoir dans un serveur très sollicité.

Mais elle est également un peu surprise de ne pas avoir eu à configurer cette alerte. Application Insights intègre la détection intelligente. Il s’ajuste automatiquement au schéma d’échec habituel de votre application et « s’habitue » aux échecs sur une page spécifique, ou en cas de charge élevée ou liée à d’autres mesures. Il génère l’alarme uniquement si l’augmentation dépasse la mesure attendue.

![e-mail de diagnostic proactif](./media/app-insights-detect-triage-diagnose/21.png)

Il s’agit d’un e-mail très utile. Il ne génère pas seulement une alarme : il effectue également une grande partie du travail de triage et de diagnostic.

Il indique le nombre de clients, les pages web ou des opérations affectés. Marcela peut décider si l’ensemble de l’équipe doit travailler à « éteindre l’incendie » ou si l’alerte peut être ignorée jusqu’à la semaine prochaine.

L’e-mail indique également qu’une exception particulière s’est produite et, ce qui est encore plus intéressant, que la défaillance est associée à des appels d’une base de données spécifique ayant échoué. Ceci explique pourquoi l’erreur est apparue soudainement alors que l’équipe de Marcela n’a pas déployé de mises à jour récemment.

Marcella interroge le responsable de l’équipe qui gère la base de données sur cet e-mail. Elle apprend qu’ils ont publié un correctif il y a moins d’une demi-heure. Il se peut donc qu’une modification mineure du schéma se soit produite...

Par conséquent, le problème est en cours de résolution, même avant l’examen des journaux et dans les 15 minutes suivant son apparition. Toutefois, Marcela clique sur le lien pour ouvrir Application Insights. Il s’ouvre directement sur une demande ayant échoué, et elle peut voir l’appel de base de données ayant échoué dans la liste d’appels de dépendance associée.

![Suivi des demandes ayant échoué](./media/app-insights-detect-triage-diagnose/23.png)

## <a name="detect-exceptions"></a>Détecter les exceptions
Après quelques configurations, les [exceptions](app-insights-asp-net-exceptions.md) sont signalées automatiquement à Application Insights. Elles peuvent également être capturées explicitement en insérant des appels à [TrackException()](app-insights-api-custom-events-metrics.md#trackexception) dans le code :  

    var telemetry = new TelemetryClient();
    ...
    try
    { ...
    }
    catch (Exception ex)
    {
       // Set up some properties:
       var properties = new Dictionary <string, string>
         {{"Game", currentGame.Name}};

       var measurements = new Dictionary <string, double>
         {{"Users", currentGame.Users.Count}};

       // Send the exception telemetry:
       telemetry.TrackException(ex, properties, measurements);
    }


L'équipe de la banque Fabrikam a pour règle de toujours envoyer la télémétrie en cas d'exception, sauf s'il existe une solution évidente.  

En fait, la stratégie de l'équipe est encore plus large : elle envoie la télémétrie dans tous les cas où le client ne peut pas faire ce qu'il veut, que cela corresponde à une exception dans le code ou non. Par exemple, si le système de transfert interbancaire externe renvoie un message « Impossible d'effectuer cette transaction » pour une raison quelconque (aucune erreur du client), cet événement est suivi.

    var successCode = AttemptTransfer(transferAmount, ...);
    if (successCode < 0)
    {
       var properties = new Dictionary <string, string>
            {{ "Code", returnCode, ... }};
       var measurements = new Dictionary <string, double>
         {{"Value", transferAmount}};
       telemetry.TrackEvent("transfer failed", properties, measurements);
    }

TrackException est utilisé pour signaler les exceptions, car il envoie une copie de la pile. TrackEvent est utilisé pour signaler les autres événements. Vous pouvez joindre toutes les propriétés qui peuvent être utiles au diagnostic.

Les exceptions et les événements apparaissent dans le panneau [Recherche de diagnostic](app-insights-diagnostic-search.md). Vous pouvez afficher plus de détails dans les propriétés supplémentaires et dans le suivi de la pile.

![Dans Recherche de diagnostic, utilisez les filtres pour afficher certains types de données.](./media/app-insights-detect-triage-diagnose/appinsights-333facets.png)


## <a name="monitor-proactively"></a>Surveiller de manière proactive
Marcela ne reste pas les bras croisés à attendre les alertes. Après chaque redéploiement, elle examine les [temps de réponse](app-insights-web-monitor-performance.md), à savoir les chiffres globaux aussi bien que la table des demandes les plus lentes, ainsi que le nombre d’exceptions.  

![Graphique des temps de réponse et grille des temps de réponse du serveur.](./media/app-insights-detect-triage-diagnose/09-dependencies.png)

Elle peut évaluer l'effet de chaque déploiement sur les performances, en comparant chaque semaine avec la précédente. Si l'état s'aggrave soudainement, elle le signale aux développeurs responsables du composant affecté.

## <a name="triage-issues"></a>Problèmes de triage
Tri : évaluation de la gravité et de l'étendue d'un problème. Première étape après la détection. Est-il nécessaire d'appeler l'équipe à minuit ? Ou est-il possible de laisser le problème de côté en attendant que l'équipe ait un peu de temps pour s'y attaquer ? Le tri pose certaines questions importantes.

Le problème se pose-t-il souvent ? Les graphiques du panneau Vue d'ensemble mettent le problème en perspective. Par exemple, l'application Fabrikam a généré en une nuit quatre alertes de test web. En examinant le graphique le matin, l'équipe a constaté qu'il y avait effectivement des points rouges, bien que la plupart des tests soient encore en vert. En ouvrant les détails du graphique de disponibilité, il était clair que tous ces problèmes intermittents venaient d'un emplacement de test. Il s'agissait d'un problème réseau affectant un seul itinéraire, qui disparaîtra probablement de lui-même.  

En revanche, une augmentation importante et constante dans le graphique du nombre d'exceptions ou des temps de réponse est évidemment source de panique.

Une bonne tactique de tri est le test réel. Si vous rencontrez le même problème, vous savez qu'il est bel et bien réel.

Quelle est la part des utilisateurs affectés ? Pour obtenir une réponse approximative, divisez le taux d'échec par le nombre de sessions.

![Graphique des demandes et des sessions ayant échoué](./media/app-insights-detect-triage-diagnose/10-failureRate.png)

En cas de réponses lentes, comparez la table des requêtes ayant reçu la réponse la moins rapide avec la fréquence d’utilisation de chaque page.

Quelle est l'importance du scénario bloqué ? S'agit-il d'un problème fonctionnel qui bloque un parcours utilisateur particulier et est-il important ? Si les clients ne peuvent pas payer leurs factures, c'est grave. S'ils ne peuvent simplement pas changer les préférences de couleur d'écran, peut-être que le problème peut attendre. Les détails de l'événement ou de l'exception, ou l'identité de la page qui présente un temps de chargement trop long, vous indiquent où les clients rencontrent des difficultés.

## <a name="diagnose-issues"></a>Diagnostiquer les problèmes
Le diagnostic n'est pas tout à fait la même chose que le débogage. Avant de commencer le suivi via le code, vous devez avoir une idée du pourquoi, du quand et du où le problème se produit.

**Quand cela se produit-il ?** La vue historique fournie par les graphiques des événements et des mesures facilite la mise en corrélation des effets avec les causes possibles. S'il y a des pics intermittents dans les temps de réponse ou les taux d'exceptions, examinez le nombre de demandes : si elle augmente en même temps, il peut s'agir d'un problème de ressources. Est-il nécessaire d'allouer davantage de processeur ou de mémoire ? Ou s'agit-il d'une dépendance qui ne peut pas gérer la charge ?

**Le problème vient-il de nous ?**  Si vous constatez une chute soudaine des performances d'un type de demande particulier, par exemple lorsque le client souhaite obtenir un relevé de compte, il est possible que le problème vienne d'un sous-système externe plutôt que de votre application web. Dans Metrics Explorer, sélectionnez les taux d'échec de dépendance et les taux de durée de la dépendance et consultez leur historique sur quelques heures ou jours avec en tête le problème que vous avez détecté. S'il y a une corrélation dans les changements, un sous-système externe peut être à l'origine du problème.  


![Graphiques des échecs des dépendances et durée des appels aux dépendances](./media/app-insights-detect-triage-diagnose/11-dependencies.png)

Certains problèmes de dépendances lentes sont dus à des problèmes de géolocalisation. La banque Fabrikam utilise des machines virtuelles Azure et l'équipe a découvert que leur serveur web et le compte de ce serveur avaient été placés par inadvertance dans des pays différents. La migration d'un de ces deux éléments a apporté des améliorations considérables.

**Qu'avons-nous fait ?** Si le problème ne paraît pas venir d'une dépendance, et s’il n'a pas toujours été là, il est probablement dû à une modification récente. La perspective historique fournie par les graphiques des mesures et des événements facilite la mise en corrélation de changements soudains avec les déploiements. Cela permet de réduire le champ de la recherche du problème. Pour identifier les lignes du code d’application à l’origine du ralentissement des performances, activez Application Insights Profiler. Reportez-vous à [Profilage des applications web dynamiques Azure avec Application Insights](./app-insights-profiler.md). Une fois Application Insights Profiler activé, vous verrez une trace semblable à la suivante. Dans cet exemple, on remarque facilement que la méthode *GetStorageTableData* a provoqué le problème.  

![Trace d’Application Insights Profiler](./media/app-insights-detect-triage-diagnose/AppInsightsProfiler.png)

**Que se passe-t-il ?** Certains problèmes se produisent rarement et peuvent être difficiles à détecter en cas de test hors connexion. Tout ce que nous pouvons faire, c'est essayer de capturer le bogue lorsqu'il se produit en temps réel. Vous pouvez inspecter les vidages de pile dans les rapports d'exceptions. En outre, vous pouvez écrire les appels de suivi, soit avec votre infrastructure de journalisation favorite, soit avec TrackTrace() ou TrackEvent().  

Fabrikam avait un problème intermittent avec les transferts entre comptes, mais uniquement avec certains types de compte. Pour mieux comprendre ce qui se produisait, ils ont inséré des appels TrackTrace() à des points clés du code, en joignant le type de compte en tant que propriété à chaque appel. Cela a permis de filtrer plus facilement le suivi dans la recherche de diagnostic. Ils ont aussi joint les valeurs des paramètres en tant que propriétés, ainsi que des mesures pour les appels de trace.

## <a name="respond-to-discovered-issues"></a>Réagir aux problèmes détectés
Une fois que vous avez diagnostiqué le problème, vous pouvez mettre en place les mesures nécessaires pour le résoudre. Peut-être devrez-vous annuler une modification récente ou peut-être pouvez-vous simplement résoudre le problème. Une fois la correction appliquée, Application Insights vous indique si vous avez réussi.  

L'équipe de développement de la banque Fabrikam adopte une approche plus structurée de la mesure des performances qu'avant l'utilisation d'Application Insights.

* Elle définit des objectifs de performances sur des mesures spécifiques dans la page Vue d'ensemble Application Insights.
* Elle intègre dès le départ des mesures de performances dans l'application, par exemple des indicateurs qui mesurent la progression de l'utilisateur dans certains segments.  


## <a name="monitor-user-activity"></a>Surveiller les activités des utilisateurs
Lorsque le temps de réponse reste satisfaisant et qu’il existe quelques exceptions, l’équipe de développement peut passer à la facilité d’utilisation. Elle peut réfléchir à la façon d’améliorer l’expérience des utilisateurs et d’encourager davantage d’utilisateurs à atteindre leurs objectifs.

Application Insights peut également servir à apprendre ce que les utilisateurs font avec une application. Une fois que cette dernière s'exécute correctement, l'équipe souhaite savoir quelles sont les fonctionnalités les plus populaires, ce que les utilisateurs ont comme difficultés et s'ils reviennent souvent. Ces données permettront de hiérarchiser le travail à venir. Et l'équipe peut prévoir de mesurer la réussite de chaque fonctionnalité dans le cadre du cycle de développement.

Par exemple, le parcours typique d’un utilisateur sur un site web s’effectue via un « entonnoir » bien défini. De nombreux clients consultent les taux de différents types de prêt. Un petit nombre d’entre eux décident de remplir le formulaire de devis. Parmi ceux qui reçoivent le devis, quelques-uns poursuivent jusqu’à la finalisation du prêt.

![Nombre d’affichages de page](./media/app-insights-detect-triage-diagnose/12-funnel.png)

En regardant à quel moment le plus grand nombre de clients s’est désintéressé, l’entreprise peut réfléchir à un moyen pour encourager davantage d’utilisateurs à aller plus loin dans leur exploration du site. Dans certains cas, il peut y avoir une défaillance de l'expérience utilisateur : par exemple, le bouton « suivant » est difficile de trouver ou les instructions ne sont pas claires. Toutefois, il est plus probable que ce désintéressement soit lié à des raisons commerciales : le taux du prêt est peut-être trop élevé.

Quelque soit les raisons, les données permettent à l’équipe de comprendre ce que font les utilisateurs. Plusieurs appels de suivi peuvent être insérées afin d’obtenir davantage de détails. TrackEvent() peut être utilisé pour compter toutes les actions d’un utilisateur, des moindres détails relatifs aux clics sur un bouton aux résultats les plus significatifs tels que le remboursement d’un prêt.

L'équipe est habituée à recevoir des informations sur l’activité d’un utilisateur. Aujourd'hui, chaque fois qu'ils conçoivent une nouvelle fonctionnalité, ils anticipent les avis qu’ils pourraient obtenir sur celle-ci. Ils conçoivent de zéro des appels de suivi dans la fonctionnalité. Ils exploitent les avis afin d’améliorer la fonctionnalité pour chaque cycle de développement.

[En savoir plus sur le suivi de l’utilisation](app-insights-usage-overview.md).

## <a name="apply-the-devops-cycle"></a>Appliquer le cycle DevOps
Voici donc une équipe qui utilise Application Insights non seulement pour résoudre les problèmes, mais aussi pour améliorer le cycle de développement. J’espère que ceci vous a donné quelques idées sur la façon dont Application Insights peut vous aider dans vos propres applications avec la gestion des performances des applications.

## <a name="video"></a>Vidéo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Étapes suivantes
Vous pouvez commencer de plusieurs façons, selon les caractéristiques de votre application. Choisissez ce qui vous convient le mieux :

* [Application web ASP.NET](app-insights-asp-net.md)
* [Application web Java](app-insights-java-get-started.md)
* [Application web Node.js](app-insights-nodejs.md)
* Applications déjà déployées, hébergées sur [IIS](app-insights-monitor-web-app-availability.md), [J2EE](app-insights-java-live.md) ou [Azure](app-insights-azure.md).
* [Pages web](app-insights-javascript.md) (application à page unique ou page web ordinaire) : utilisez cette option seule ou en plus des options de serveur.
* [Tests de disponibilité](app-insights-monitor-web-app-availability.md) pour tester votre application à partir de l’Internet public.
