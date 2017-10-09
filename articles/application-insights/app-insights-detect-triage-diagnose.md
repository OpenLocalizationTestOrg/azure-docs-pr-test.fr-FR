---
title: aaaOverview de Azure Application Insights pour DevOps | Documents Microsoft
description: "Découvrez comment toouse Application Insights dans un environnement de développement Ops."
author: CFreemanwa
services: application-insights
documentationcenter: 
manager: carmonm
ms.assetid: 6ccab5d4-34c4-4303-9d3b-a0f1b11e6651
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: bwren
ms.openlocfilehash: 42139f4645e815f26378726f4716a9bfbdc78551
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-application-insights-for-devops"></a>Vue d’ensemble d’Application Insights pour DevOps

Avec [Application Insights](app-insights-overview.md), vous avez la possibilité de connaître rapidement les performances et l’utilisation de votre application active. S’il existe un problème, il vous permet de savoir qu’il vous aide à vous évaluez l’impact de hello et vous aide à déterminer les causes de hello.

Voici le compte d'une équipe qui développe des applications web :

* *« Il y a quelques jours, nous avons déployé un correctif secondaire. Nous n’avez pas exécuter un test d’étendue, mais malheureusement, des modifications inattendues ont été fusionnées dans la charge utile de hello, provoquant l’incompatibilité entre le début de hello et back-end. Immédiatement, exceptions du serveur forcées, notre alerte déclenchée, et nous avons été informés de situation de hello. Quelques clics immédiatement sur le portail Application Insights de hello, obtenue suffisamment d’informations à toonarrow de pile des appels d’exception problème de hello. Nous restaurées immédiatement et limité les dommages hello. Application Insights a effectué cette partie de hello devops cycle très facile et exploitables. »*

Dans cet article, nous suivons une équipe dans la banque de Fabrikam qui développe hello toosee système (répartition) l’utilisation de banque en ligne Application Insights tooquickly toocustomers de répondre et mettre à jour.  

Hello équipe l’exécute un cycle DevOps mentionné dans hello après l’illustration :

![Cycle DevOps](./media/app-insights-detect-triage-diagnose/00-devcycle.png)

Les exigences alimentent leur backlog de développement (liste des tâches). Elles fonctionnent en bref sprints, qui souvent fournir des logiciels opérationnels - généralement sous forme de hello d’améliorations et extensions toohello d’application existante. application en temps réel de Hello est fréquemment mis à jour avec les nouvelles fonctionnalités. S’il est dynamique, équipe de hello l’analyse des performances et d’utilisation à l’aide de hello de Application Insights. Les données de gestion des performances des applications alimentent leur backlog de développement.

équipe de Hello utilise Application Insights toomonitor hello dynamique d’application web en étroite collaboration pour :

* Les performances. Ils veulent toounderstand comment les temps de réponse varient selon le nombre de requêtes ; Comment beaucoup l’UC, de réseau, de disque et d’autres ressources sont utilisés ; et où les goulots d’étranglement hello.
* Les échecs. S’il existe des exceptions ou des demandes ayant échoué, ou si un compteur de performance est en dehors de sa plage à l’aise, hello équipe besoins tooknow rapidement afin qu’ils peuvent prendre des mesures.
* L’utilisation. Chaque fois qu’une nouvelle fonctionnalité est publiée, hello équipe tooknow toowhat étendue est qu’il est utilisé, et si les utilisateurs ont des difficultés avec lui.

Concentrons-nous sur la partie de commentaires de hello du cycle de hello :

![Détection-tri-diagnostic](./media/app-insights-detect-triage-diagnose/01-pipe1.png)

## <a name="detect-poor-availability"></a>Détecter une faible disponibilité
Marcela Markova est un développeur senior de l’équipe de répartition hello et prend prospect hello sur la surveillance des performances en ligne. Elle configure plusieurs [tests de disponibilité](app-insights-monitor-web-app-availability.md) :

* Un test par URL unique pour la page d’accueil hello pour l’application hello, http://fabrikambank.com/onlinebanking/. Elle définit des critères de code HTTP 200 et le texte « Bienvenue ! Si ce test échoue, il est gravement erroné avec hello réseau ou des serveurs de hello ou peut-être un problème de déploiement. (Ou un utilisateur a modifié hello Bienvenue ! message sur la page hello sans en avertir son connus).
* Un test en plusieurs étapes plus en profondeur, qui se connecte et obtient la liste des comptes actuels, en vérifiant quelques détails importants sur chaque page. Ce test vérifie que l’utilisation de cette base de données des comptes toohello hello lien. Elle utilise un ID de client fictif : elle en conserve quelques-uns pour ses tests.

Avec les tests de configuration, Marcela est assuré que l’équipe hello rapidement connaissent toute coupure de courant.  

Erreurs qui s’affichent sous forme de points rouges sur le graphique de test web hello :

![Affichage des tests web qui ont été exécutées sur hello précédant la période](./media/app-insights-detect-triage-diagnose/04-webtests.png)

Mais plus important encore, une alerte sur tout échec est par courrier électronique équipe de développement toohello. De cette façon, elles savent avant de quasiment tous hello clients.

## <a name="monitor-performance"></a>Analyser les performances
Sur la page de vue d’ensemble de hello dans Application Insights, il est un graphique qui affiche diverses [clé métriques](app-insights-web-monitor-performance.md).

![Différentes mesures](./media/app-insights-detect-triage-diagnose/05-perfMetrics.png)

Le temps de chargement de la page du navigateur provient de la télémétrie envoyée directement depuis vos pages web. Temps de réponse de serveur, nombre de demandes de serveur et le nombre de demandes ayant échoué sont tous mesurés dans le serveur web de hello et envoyés tooApplication Insights à partir de là.

Marcela est légèrement concerné avec le graphique de réponse du serveur hello. Ce graphique montre la durée moyenne de hello entre lorsque le serveur de hello reçoit une requête HTTP à partir du navigateur de l’utilisateur, et lorsqu’il retourne la réponse de hello. Il n’est pas inhabituel toosee une variation dans ce graphique, comme la charge sur le système de hello. Mais dans ce cas, il semble que toobe une corrélation entre la petite augmente dans hello nombre de demandes et big augmente dans le temps de réponse hello. Cela peut indiquer que hello système fonctionne uniquement au niveau de ses limites.

Elle ouvre des graphiques de serveurs hello :

![Différentes mesures](./media/app-insights-detect-triage-diagnose/06.png)

Il peut paraître toobe aucun signe de limitation de ressources, afin de rendre des irrégularités hello maybe graphiques de réponse de serveur hello simplement une coïncidence.

## <a name="set-alerts-toomeet-goals"></a>Définir des alertes toomeet objectifs
Toutefois, elle souhaite que tookeep un œil sur les temps de réponse hello. Si elles sont trop élevées, elle souhaite tooknow concernant immédiatement.

Elle définit alors une [alerte](app-insights-metrics-explorer.md) si les temps de réponse dépassent un seuil standard. Ainsi, elle est certaine d’être avertie en cas de temps de réponse lents.

![Ajouter un panneau d'alerte](./media/app-insights-detect-triage-diagnose/07-alerts.png)

Des alertes peuvent être définies sur une grande variété d’autres mesures. Par exemple, vous pouvez recevoir des messages électroniques si le nombre d’exceptions hello devient importante, ou la mémoire disponible hello est faible, ou s’il existe un pic dans les demandes des clients.

## <a name="stay-informed-with-smart-detection-alerts"></a>Rester informé grâce aux alertes de détection intelligentes
Le jour suivant, un message électronique d’alerte est généré depuis Application Insights. Mais quand elle s’ouvre, elle trouve qu'il n’est pas d’alerte du temps de réponse hello elle définies. Au lieu de cela, elle lui indique qu’il y a eu une augmentation soudaine du nombre de demandes ayant échoué (autrement dit, les demandes qui ont renvoyé des codes d’erreur d’au moins 500).

Requêtes ayant échoué sont où les utilisateurs connaissent une erreur - généralement après une exception levée dans le code hello. Peut-être ont-ils vu un message indiquant « Nous ne pouvons pas mettre à jour vos informations maintenant » Ou, au pire de gênant absolu, un vidage de pile s’affiche sur l’écran de l’utilisateur hello, avec l’autorisation de serveur web de hello.

Cette alerte est une surprise, car hello dernière, elle a examiné, hello des demandes ayant échoué nombre était approcher faible. Un petit nombre d’échecs est toobe attendu dans un serveur occupé.

Il était également un peu de surprenant pour son travail, car elle n’a pas tooconfigure cette alerte. Application Insights intègre la détection intelligente. Il ajuste automatiquement le motif d’échec habituel tooyour de l’application et les échecs « obtient utilisé pour » sur une page particulière, ou sous une charge élevée, ou les métriques tooother lié. Il déclenche une alerte de hello uniquement s’il existe une hausse au-dessus de ce qu’il vient tooexpect.

![e-mail de diagnostic proactif](./media/app-insights-detect-triage-diagnose/21.png)

Il s’agit d’un e-mail très utile. Il ne génère pas seulement une alarme : Il effectue beaucoup de travail de diagnostic et de triage de hello trop.

Il indique le nombre de clients, les pages web ou des opérations affectés. Marcela pouvez décider si elle doit tooget hello ensemble de l’équipe travaille sur cela comme un incendie, ou si elle peut être ignoré jusqu'à ce que la semaine suivante.

messagerie de Hello montre également qu’une exception particulière s’est produite, et - plus intéressant - échec hello est associé à des échecs d’appels tooa base de données. Cela explique pourquoi les pannes hello soudainement est apparue même si l’équipe de Marcela n’a pas déployé les mises à jour récemment.

Marcella pings hello leader hello équipe de base de données en fonction de ce courrier électronique. Il apprend qu’ils publié un correctif logiciel Bonjour dernière moitié heure ; et Oups, peut-être qu’il peut avoir été une modification de schéma secondaire...

Problème de hello est donc hello toobeing de manière fixé, même avant d’examiner les journaux et dans les 15 minutes de celui-ci résultant. Toutefois, Marcela clique hello lien tooopen Application Insights. Il s’ouvre directement sur une demande ayant échoué, et qu’elle peut voir la base de données a échoué à appeler dans la liste associée de hello d’appels de dépendance.

![Suivi des demandes ayant échoué](./media/app-insights-detect-triage-diagnose/23.png)

## <a name="detect-exceptions"></a>Détecter les exceptions
Avec un peu de l’installation, [exceptions](app-insights-asp-net-exceptions.md) sont signalée tooApplication Insights automatiquement. Ils peuvent également être capturés explicitement en insérant des appels trop[TrackException()](app-insights-api-custom-events-metrics.md#trackexception) dans le code de hello :  

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

       // Send hello exception telemetry:
       telemetry.TrackException(ex, properties, measurements);
    }


équipe de Fabrikam Bank Hello a évolué pratique hello de toujours envoyer les données de télémétrie sur une exception, sauf s’il existe une récupération évidente.  

En fait, leur stratégie est encore plus large que celle : ils envoient la télémétrie dans tous les cas où les clients hello ne sont pas satisfait dans quel ils voulaient toodo, si elle correspond exception tooan dans le code hello ou non. Par exemple, si le système de transfert Inter-bank externe hello renvoie un message « Impossible de terminer cette opération » pour une raison quelconque (aucune erreur de client de hello), opérationnelle elles suivent cet événement.

    var successCode = AttemptTransfer(transferAmount, ...);
    if (successCode < 0)
    {
       var properties = new Dictionary <string, string>
            {{ "Code", returnCode, ... }};
       var measurements = new Dictionary <string, double>
         {{"Value", transferAmount}};
       telemetry.TrackEvent("transfer failed", properties, measurements);
    }

TrackException est utilisé tooreport exceptions, car il envoie une copie de la pile de hello. TrackEvent est utilisé tooreport autres événements. Vous pouvez joindre toutes les propriétés qui peuvent être utiles au diagnostic.

Exceptions et les événements apparaissent dans hello [recherche Diagnostic](app-insights-diagnostic-search.md) panneau. Vous pouvez explorer les propriétés supplémentaires de toosee hello et trace de la pile.

![Dans la recherche de Diagnostic, utiliser des filtres tooshow certains types de données](./media/app-insights-detect-triage-diagnose/appinsights-333facets.png)


## <a name="monitor-proactively"></a>Surveiller de manière proactive
Marcela ne reste pas les bras croisés à attendre les alertes. Peu après chaque redéploiement, elle examine les [temps de réponse](app-insights-web-monitor-performance.md) : les deux hello globale figure et compte de la table hello de demandes les plus lents, ainsi que les exceptions.  

![Graphique des temps de réponse et grille des temps de réponse du serveur.](./media/app-insights-detect-triage-diagnose/09-dependencies.png)

Elle peut évaluer incidence sur les performances de chaque déploiement, hello généralement comparaison dernier chaque semaine par hello. S’il existe une aggravation soudaine, elle déclenche qui avec les développeurs pertinentes hello.

## <a name="triage-issues"></a>Problèmes de triage
Triage - évaluation de niveau de gravité hello et l’étendue d’un problème - est hello première étape après la détection. Étudions que nous appelons à l’équipe de hello à minuit ? Ou bien, il peut être conservé jusqu'à ce que l’intervalle de pratique suivant hello des travaux en souffrance de hello ? Le tri pose certaines questions importantes.

La fréquence à laquelle se passe-t-il ? graphiques Hello sur le panneau de vue d’ensemble de hello donner à un problème de tooa de perspective. Par exemple, hello Fabrikam application générant des alertes de test web quatre une nuit. Examinez le graphique de hello matin de hello, hello équipe peut voir qu’il y avait en effet, certains points rouges, si toujours la plupart des tests de hello étaient verte. L’exploration dans le graphique de disponibilité hello, il était clair que tous ces problèmes intermittents proviennent d’un emplacement pour un test. Il s'agissait d'un problème réseau affectant un seul itinéraire, qui disparaîtra probablement de lui-même.  

En revanche, une augmentation considérable et stable dans le graphique de hello du nombre d’exceptions ou de temps de réponse est à l’évidence un élément toopanic sur.

Une bonne tactique de tri est le test réel. Si vous rencontrez hello même problème, vous savez qu’il est de type real.

Quelle est la proportion d’utilisateurs sont affectés ? tooobtain une réponse approximative, divisez le taux d’échec hello par le nombre de sessions hello.

![Graphique des demandes et des sessions ayant échoué](./media/app-insights-detect-triage-diagnose/10-failureRate.png)

Lorsqu’il existe des réponses lentes, comparez table hello de ne répond plus lente des requêtes avec une fréquence d’utilisation hello de chaque page.

L’importance est le scénario de hello bloqué ? S'agit-il d'un problème fonctionnel qui bloque un parcours utilisateur particulier et est-il important ? Si les clients ne peuvent pas payer leurs factures, c'est grave. S'ils ne peuvent simplement pas changer les préférences de couleur d'écran, peut-être que le problème peut attendre. Hello détail de l’événement de hello ou d’une exception, ou l’identité de hello de lent des pages hello, vous indique où les clients rencontrent des problèmes.

## <a name="diagnose-issues"></a>Diagnostiquer les problèmes
Diagnostic n’est pas assez hello identique au débogage. Avant de commencer le suivi via le code de hello, doit avoir une idée approximative de la raison pour laquelle, où et quand le problème de hello se produit.

**Quand il se produit-il ?**  hello historiques fournies par les graphiques d’événement et la métrique hello facilitent les effets toocorrelate facile avec les causes possibles. S’il existe des pics intermittents taux de réponse temps ou une exception, examinez de nombre de demandes hello : si elle est optimale lorsque hello même temps, puis il ressemble à un problème de ressources. Vous devez tooassign plus d’UC ou de mémoire ? Ou bien, il y a une dépendance qui ne peut pas gérer la charge de hello ?

**Le problème vient-il de nous ?**  Si vous avez une chute soudaine des performances d’un type particulier de demande - par exemple lorsque hello client souhaite un relevé de compte - il est possible, il peut être un sous-système externe au lieu de votre application web. Dans Metrics Explorer, sélectionnez le taux d’échec de la dépendance hello et taux de durée de la dépendance et comparer leurs historiques sur hello au-delà de quelques heures ou jours avec problème de hello que vous détecté. Si il corrélation sont des modifications, un sous-système externe peut être tooblame.  

![Graphiques de l’échec de la dépendance et la durée des appels toodependencies](./media/app-insights-detect-triage-diagnose/11-dependencies.png)

Certains problèmes de dépendances lentes sont dus à des problèmes de géolocalisation. La banque Fabrikam utilise des machines virtuelles Azure et l'équipe a découvert que leur serveur web et le compte de ce serveur avaient été placés par inadvertance dans des pays différents. La migration d'un de ces deux éléments a apporté des améliorations considérables.

**Qu'avons-nous fait ?** Si le problème de hello n’apparaît pas toobe une dépendance, et si elle n’était pas toujours il, il est probablement dû à une modification récente. Hello perspective historique fournie par les graphiques de métriques et les événements hello rend toocorrelate facilement les changements soudains dans des déploiements. Cela réduit la recherche hello pour problème de hello.

**Que se passe-t-il ?** Certains problèmes se produisent rarement et peuvent être difficile tootrack vers le bas en le testant hors connexion. Tout ce que nous pouvons faire est bogue de hello tootry toocapture lorsqu’il se produit en temps réel. Vous pouvez inspecter les vidages de pile hello dans les rapports d’exception. En outre, vous pouvez écrire les appels de suivi, soit avec votre infrastructure de journalisation favorite, soit avec TrackTrace() ou TrackEvent().  

Fabrikam avait un problème intermittent avec les transferts entre comptes, mais uniquement avec certains types de compte. toounderstand mieux que s’est-il passé, ils inséré TrackTrace() appels à des points clés dans le code hello, attachement hello type de compte comme un appel de tooeach de propriété. Il était facile toofilter out uniquement les traces dans la recherche de Diagnostic. Ils attachés également les valeurs de paramètre en tant qu’appels de trace toohello propriétés et les mesures.

## <a name="respond-toodiscovered-issues"></a>Répondre toodiscovered problèmes
Une fois que vous avez diagnostiqué le problème de hello, vous pouvez rendre un plan toofix il. Éventuellement, vous devez tooroll retour une modification récente, ou vous pouvez simplement continuez et corrigez-le. Une fois que le correctif de hello est terminé, Application Insights vous indique si vous a réussi.  

Équipe de développement de la banque de Fabrikam prendre une mesure de tooperformance d’approche plus structurée plus toobefore ils utilisé Application Insights.

* Ils définir des objectifs de performances en termes de mesures spécifiques dans la page de vue d’ensemble d’Application Insights hello.
* Concevoir des mesures de performances dans une application hello du début hello, telles que les métriques hello qui mesurent la progression de l’utilisateur via 'Entonnoirs'.  


## <a name="monitor-user-activity"></a>Surveiller les activités des utilisateurs
Lorsque le temps de réponse est généralement correct et il existe quelques exceptions près, équipe de développement hello peut déplacer sur toousability. Ils peuvent imaginer comment tooimprove hello expérience des utilisateurs, et comment tooencourage hello de tooachieve plus d’utilisateurs souhaité objectifs.

Application Insights peuvent également être utilisé toolearn faire de ce que les utilisateurs avec une application. Une fois qu’il s’exécute correctement, hello aimerait tooknow les fonctionnalités qui sont hello plus populaire, ce que les utilisateurs comme ou ayant des difficultés avec, et la fréquence à laquelle les rapatrier. Ces données permettront de hiérarchiser le travail à venir. Et prévoyez de réussite de hello toomeasure de chaque fonctionnalité dans le cadre du cycle de développement hello. 

Par exemple, un trajet utilisateur classique via le site web de hello a un clair » en entonnoir. » De nombreux clients rechercher tarifs hello de différents types de prêt. Un nombre plus petit, allez sur toofill sous forme de guillemets hello. Les personnes qui reçoivent une citation, quelques continuez de contracter hello prêt.

![Nombre d’affichages de page](./media/app-insights-detect-triage-diagnose/12-funnel.png)

En considérant où disparaître hello de plus grand nombre de clients, business de hello peuvent élaborer comment tooget plus d’utilisateurs par le biais bas toohello Hello en entonnoir. Dans certains cas, il peut y avoir un échec de l’expérience utilisateur - par exemple, le bouton « suivant » hello est toofind dur ou les instructions hello ne sont pas évidentes. Plus vraisemblablement, il existe des raisons professionnelles plus importantes pour phénomène : peut-être le taux de prêt de hello sont trop élevés.

Quelque raison hello, les données de salutation aident hello équipe à déterminer ce que font les utilisateurs. Plus le suivi des appels peuvent être insérées toowork davantage de détails. TrackEvent() peut être utilisé toocount toutes les actions utilisateur, à partir des détails de hello d’individuels clics, réalisations toosignificant telles que de payer un prêt.

équipe de Hello est mise en route toohaving utilisé plus d’informations sur l’activité utilisateur. Aujourd'hui, chaque fois qu'ils conçoivent une nouvelle fonctionnalité, ils anticipent les avis qu’ils pourraient obtenir sur celle-ci. Concevoir des appels de suivi dans la fonction hello du début de hello. Ils utilisent la fonctionnalité de hello commentaires tooimprove hello dans chaque cycle de développement.

[En savoir plus sur le suivi de l’utilisation](app-insights-usage-overview.md).

## <a name="apply-hello-devops-cycle"></a>Appliquer le cycle de DevOps hello
C’est une team utilisez Application Insights toofix pas simplement individuels des problèmes, mais tooimprove leur cycle de vie de développement. J’espère que ceci vous a donné quelques idées sur la façon dont Application Insights peut vous aider dans vos propres applications avec la gestion des performances des applications.

## <a name="video"></a>Vidéo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Étapes suivantes
Vous pouvez commencer de différentes façons, selon les caractéristiques de hello de votre application. Choisissez ce qui vous convient le mieux :

* [Application web ASP.NET](app-insights-asp-net.md)
* [Application web Java](app-insights-java-get-started.md)
* [Application web Node.js](app-insights-nodejs.md)
* Applications déjà déployées, hébergées sur [IIS](app-insights-monitor-web-app-availability.md), [J2EE](app-insights-java-live.md) ou [Azure](app-insights-azure.md).
* [Pages Web](app-insights-javascript.md) -application Page unique ou ordinaire de la page web - utiliser sur son propre ou dans tooany Ajout hello des options de serveur.
* [Tests de disponibilité](app-insights-monitor-web-app-availability.md) tootest votre application à partir de hello internet public.
