---
title: analyse des performances des applications aaaWeb - Azure Application Insights | Documents Microsoft
description: "Comment Application Insights s’adapte à hello devOps cycle"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 479522a9-ff5c-471e-a405-b8fa221aedb3
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: bba2d6c59de1794adcbf8e298d0ef4f0dbaa700f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deep-diagnostics-for-web-apps-and-services-with-application-insights"></a>Diagnostic approfondi des applications et services web avec Application Insights
## <a name="why-do-i-need-application-insights"></a>Pourquoi ai-je besoin d’Application Insights ?
Application Insights surveille votre application web en cours d’exécution. En plus de signaler les défaillances et problèmes de performance, il permet d’analyser comment les clients utilisent votre application. Il fonctionne pour les applications qui s’exécutent sur de nombreuses plateformes (ASP.NET, J2EE, Node.js,...) et est hébergé dans hello Cloud ou local. 

![Aspects de la complexité hello de la livraison d’applications web](./media/app-insights-devops/010.png)

Il est essentiel toomonitor une application moderne pendant son exécution. Plus important encore, vous souhaitez que les échecs de toodetect avant de la plupart de vos clients. Vous souhaitez toodiscover et résoudre les problèmes de performances, lorsque pas grave, voire ralentissent ou désagréments tooyour utilisateurs. Et lors de système de hello est tooyour satisfaction, que vous souhaitez tooknow ce que les utilisateurs hello sont en servent : sont-elles à l’aide de la fonctionnalité la plus récente hello ? Sont-ils satisfaits par celle-ci ?

Les applications web modernes sont développées dans un cycle de livraison continue : libérer une nouvelle fonctionnalité ou l’amélioration du produit ; Observez comment il fonctionne pour les utilisateurs de hello ; Planifiez hello prochaine incrémentation de développement basé sur cette base de connaissances. Une partie essentielle de ce cycle est la phase d’observation hello. Application Insights fournit hello outils toomonitor une application web pour les performances et l’utilisation.

Hello plus important de ce processus est le diagnostic et diagnostic. Si l’application hello échoue, puis entreprise est en cours a perdu. Hello premier rôle d’une infrastructure d’analyse est par conséquent toodetect échecs fiable, informer immédiatement et toopresent des informations de hello problème de hello toodiagnose. C’est exactement ce que fait Application Insights.

### <a name="where-do-bugs-come-from"></a>D'où proviennent les bogues ?
Dans les systèmes web, les défaillances proviennent généralement de problèmes de configuration ou de mauvaises interactions entre les multiples composants. Hello première tâche lors de la résolution d’un incident de site actif est donc emplacement de hello de tooidentify des problème de hello : le composant ou la relation est la cause de hello ?

Les plus âgés d’entre nous se rappellent l’époque où un programme s’exécutait sur un ordinateur. les développeurs de Hello seraient tester de manière approfondie avant de le livrer ; et avoir fourni, serait consultez rarement ou penser à nouveau. les utilisateurs de Hello aient tooput bogues résiduelles de hello depuis de nombreuses années. 

Aujourd’hui, les choses sont bien différentes. Votre application possède une multitude de différents appareils toorun, et il peut être difficile de tooguarantee hello même comportement exact sur chacun d’eux. Hébergement d’applications dans le cloud de hello signifie peuvent être corrigés rapidement, mais il signifie également expectation concurrence et hello continue de nouvelles fonctionnalités à intervalles fréquents. 

Dans ces conditions, hello tookeep de façon seulement qu'un contrôle définitive sur le nombre de bogues hello est automatisée de tests unitaires. Il serait impossible toomanually Testez de nouveau tout le contenu de chaque remise. Test unitaire est à présent partie courants de hello les processus de génération. Aide des outils tels que hello Xamarin Test Cloud en fournissant l’interface utilisateur automatisés test sur plusieurs versions de navigateur. Ces régimes de test nous permettent de toohope ce taux hello de bogues trouvés à l’intérieur d’une application peut être conservé tooa minimale.

Les applications web classiques ont de nombreux composants actifs. Dans Ajout toohello client (situé dans une application de navigateur ou l’appareil) et serveur web de hello, est probablement toobe substantielle principal traitement. Hello principal est peut-être un pipeline de composants, ou une collection plus souple de pièces de collaboration. Et bon nombre de ces éléments ne seront pas sous votre contrôle. Il s’agit de services externes dont vous dépendez.

Dans les configurations telles que celles-ci, il peut être difficile et uneconomical tootest, ou prévoir, chaque mode de défaillance possibles, autre que Bonjour live système lui-même. 

### <a name="questions-"></a>Questions...
Voici quelques questions que nous nous posons lorsque nous développons un système web :

* Mon application se bloque-t-elle ? 
* Que s’est-il passé exactement ? -En cas d’échec une demande, je veux tooknow comment il est parvenu il. Nous avons d’un suivi des événements...
* Mon application est-elle assez rapide ? Combien de temps faut-il toorespond tootypical demandes ?
* Messages hello du handle hello serveur peut charger ? Lorsque le taux de hello de requêtes augmente, le temps de réponse hello contient stable ?
* La réactivité sont mes dépendances - hello API REST, bases de données et d’autres composants qui appelle de mon application. En particulier, si le système de hello est lente, il est de mon composant ou obtenez-vous des réponses lentes de quelqu'un d’autre ?
* Mon application fonctionne-t-elle ou pas ? Il montre autour Bonjour ? Signalez-moi tout dysfonctionnement...
* Quelle est la cause première hello ? Hello est survenue dans mon composant ou une dépendance ? Est-ce un problème de communication ?
* Combien d’utilisateurs en sont affectés ? Si j’ai plus d’un problème tootackle, qui est hello plus importante ?

## <a name="what-is-application-insights"></a>Présentation d’Application Insights
![Flux de travail de base d’Application Insights](./media/app-insights-devops/020.png)

1. Application Insights instrumente votre application et envoie télémétrie concernant pendant que l’application hello est en cours d’exécution. Vous pouvez générer hello Application Insights SDK dans l’application hello, ou vous pouvez appliquer instrumentation lors de l’exécution. méthode ancien Hello est plus souple, que vous pouvez ajouter vos propres modules standards toohello de télémétrie.
2. les données de télémétrie Hello sont envoyée portail Application Insights de toohello, où il est stocké et traité. (Bien qu’hébergé dans Microsoft Azure, Application Insights peut surveiller toutes les applications web, et pas seulement les applications Azure.)
3. les données de télémétrie Hello sont présentée tooyou sous forme de hello de graphiques et des tables d’événements.

Il existe deux principaux types de données télémétriques : les instances agrégées et les instances brutes. 

* Les données d’instance incluent, par exemple, un rapport d’une demande reçue par votre application web. Vous pouvez rechercher et obtenir des détails de hello d’une demande à l’aide d’outil de recherche hello portail Application Insights de hello. instance de Hello serait incluent des données telles que la durée pendant laquelle votre application a duré toorespond toohello demande, ainsi que hello URL demandée, emplacement approximatif de client de hello et autres données.
* Données agrégées incluent les nombres d’événements par unité de temps, afin que vous puissiez comparer les taux hello de requêtes avec un temps de réponse hello. Elles indiquent également des valeurs moyennes, comme le temps de réponse aux demandes.

Hello principales catégories de données sont :

* Demandes tooyour application (généralement des requêtes HTTP), avec des données sur l’URL, les temps de réponse et les succès ou échec.
* Dépendances - Appels REST et SQL effectués par votre application, avec l’URI, les temps de réponse et la réussite
* Exceptions, y compris les traces de pile.
* Page Afficher les données, qui proviennent de navigateurs des utilisateurs hello.
* Mesures, comme les compteurs de performance ou les mesures que vous écrivez vous-même. 
* Événements personnalisés que vous pouvez utiliser des événements commerciaux tootrack
* Traces de journal utilisées pour le débogage.

## <a name="case-study-real-madrid-fc"></a>Étude de cas : Real Madrid F.C.
Hello du service web de [réel Club de Football de Madrid](http://www.realmadrid.com/) sert environ 450 millions ventilateurs monde hello. Ventilateurs accéder via un navigateur et des applications mobiles du Club de hello. Les supporters n’achètent pas seulement des billets, ils consultent des informations et visionnent des vidéos sur les résultats, les joueurs et les prochains matchs. Ils peuvent effectuer des recherches avec des filtres, comme le nombre de buts marqués. Il existe également un support de toosocial de liens. l’expérience utilisateur Hello est extrêmement personnalisé et est conçu comme un ventilateurs tooengage de communication bidirectionnelle.

solution de Hello [est un système des services et applications sur Microsoft Azure](https://www.microsoft.com/en-us/enterprise/microsoftcloud/realmadrid.aspx). L’évolutivité est essentielle : le trafic, variable, peut atteindre des sommets avant, pendant et après les matchs.

Madrid réel, il s’agit de performances du système toomonitor vitales hello. Azure Application Insights offre une vue détaillée sur le système de hello, assurant un niveau de service fiable et haute. 

Hello Club obtient également approfondir votre compréhension de ses ventilateurs : là où ils sont (seulement 3 % sont en Espagne), quel intérêt ont dans les lecteurs, historique des résultats et des jeux à venir, et comment ils y répondent toomatch résultats.

La plupart de ces données de télémétrie sont automatiquement collectées sans code ajouté, qui simplifiée des solutions de hello et réduit la complexité opérationnelle.  Pour le Real Madrid, Application Insights gère 3,8 milliards de points de télémétrie par mois.

Real Madrid utilise hello Power BI module tooview leurs données de télémétrie.

![Vue Power BI des données télémétriques d’Application Insights](./media/app-insights-devops/080.png)

## <a name="smart-detection"></a>Détection intelligente
[Diagnostics proactifs](app-insights-proactive-diagnostics.md) est une fonctionnalité récente. Sans aucune configuration particulière, Application Insights détecte automatiquement et signale toute hausse inhabituelle du nombre de défaillances dans votre application. Il est assez intelligente tooignore un arrière-plan de défaillances occasionnelles, et également augmente est proportionnée simplement tooa augmentation des demandes. Par exemple, s’il existe une défaillance dans un des services hello que vous en avez besoin, ou si hello nouvelle build que vous venez de déployer ne fonctionne pas bien, puis vous devez savoir dès que vous examinez votre adresse de messagerie. (Et les webhooks vous permettent de déclencher d’autres applications.)

Un autre aspect de cette fonctionnalité effectue une analyse approfondie quotidienne de votre télémétrie, recherchez inhabituelles de performances qui sont toodiscover dur. Par exemple, elle peut identifier un faible niveau de performance dans une zone géographique ou avec une version particulière d’un navigateur.

Dans les deux cas, hello alerte indique non seulement vous hello symptômes, il est découvert, mais également permet de diagnostiquer les données, vous devez toohelp hello problème, tels que les rapports d’exception pertinente.

![E-mail issus des diagnostics proactifs](./media/app-insights-devops/030.png)

Notre client Samtec a déclaré : « Récemment, pendant une interruption du service, nous avons trouvé une base de données sous-dimensionnée qui atteignait la limite de ses ressources, provoquant des attentes. Alertes de détection proactive traversé littéralement que nous avons triage problème hello, très quasiment en temps réel comme publiés. Cette alerte associée à des alertes de plateforme Windows Azure hello nous ont permis de résoudre les problème de hello presque instantanément. Temps d’arrêt total < 10 minutes. »

## <a name="live-metrics-stream"></a>Live Metrics Stream (Flux continu de mesures)
Déployer la build la plus récente hello peut être une expérience inquiéter. S’il existe des problèmes, vous souhaitez tooknow à leur sujet immédiatement, afin que vous pouvez annuler si nécessaire. Live Metrics Stream (Flux continu de mesures) fournit des mesures clés avec une latence d’environ une seconde.

![Mesures actives](./media/app-insights-devops/040.png)

Et vous permet d’inspecter immédiatement un échantillon des échecs ou exceptions éventuels.

![Événements d’échec en direct](./media/app-insights-devops/live-stream-failures.png)

## <a name="application-map"></a>Plan de l’application
Mappage d’application détecte automatiquement la topologie de votre application, portant des informations sur les performances hello par-dessus, toolet vous identifiez facilement les goulots d’étranglement des performances et des flux problématiques dans votre environnement distribué. Il vous permet de dépendances des applications toodiscover sur les Services Azure. Vous pouvez triage des problème de hello à comprendre si elle est relative au code ou des dépendances liées et à partir d’un emplacement unique, explorez diagnostics connexes expérience. Par exemple, votre application en cas d’échec en raison de la dégradation de tooperformance dans le niveau SQL. Avec le mappage de l’application, vous pouvez voir immédiatement et explorez hello conseiller d’indexation SQL ou d’analyse des requêtes de l’expérience.

![Plan de l’application](./media/app-insights-devops/050.png)

## <a name="application-insights-analytics"></a>Application Insights Analytics
Avec [Analytics](app-insights-analytics.md), vous pouvez écrire des requêtes arbitraires dans un puissant langage de type SQL.  Il devient facile de diagnostic sur la pile d’application entière hello comme selon différentes perspectives se connecter et que vous pouvez demander hello toocorrelate de bonnes questions sur les performances du Service avec des mesures et l’expérience utilisateur. 

Vous pouvez interroger tous les votre instance de télémétrie et les données brutes métriques stockées dans le portail de hello. langage de Hello comprend des filtres, jointure, agrégation et autres opérations. Vous pouvez calculer des champs et effectuer une analyse statistique. Les visualisations peuvent être tabulaires ou graphiques.

![Graphique de l’interrogation d’analyse et des résultats](./media/app-insights-devops/025.png)

Par exemple, les opérations suivantes sont faciles :

* Demande de votre application par le client, les données de performances des niveaux de toounderstand leur expérience de segment.
* Rechercher des codes d’erreur spécifiques ou des noms d’événement personnalisés pendant l’analyse d’un site actif.
* Explorez l’utilisation des applications de clients spécifiques toounderstand hello comment les fonctionnalités qui sont acquis et adoptées.
* Effectuer le suivi des sessions et les temps de réponse pour des utilisateurs spécifiques tooenable prise en charge et opérations équipes tooprovide client instantanée.
* Déterminer les questions de définition des priorités application fréquemment utilisées fonctionnalités tooanswer fonctionnalité.

Client profonds DNN a dit : « Application Insights nous a fourni hello manque des équations hello pour être en mesure de toocombine, trier, requête et filtrer les données en fonction des besoins. Autoriser toouse de notre équipe leur propres toofind ingéniosité et expérience les données avec un langage de requête puissantes nous a permis de toofind insights et résoudre les problèmes que n’a pas savoir que nous avions. Un grand nombre de réponses intéressantes proviennent de questions hello commençant par *' I étonnant if...'.*»

## <a name="development-tools-integration"></a>Intégration d’outils de développement
### <a name="configuring-application-insights"></a>Configuration d'Application Insights
Visual Studio et Eclipse ont outils tooconfigure hello corrects packages SDK pour le projet hello que vous développez. Il existe un tooadd de commande de menu Application Insights.

Si vous vous trouvez toobe à l’aide d’une infrastructure de journalisation de suivi comme System.Diagnostics.Trace, NLog ou Log4N, vous obtenez hello option toosend hello journaux tooApplication Insights avec hello autres données de télémétrie, afin que vous pouvez facilement corréler des suivis de hello avec les requêtes , appels de dépendance et des exceptions.

### <a name="search-telemetry-in-visual-studio"></a>Recherche de données télémétriques dans Visual Studio
Lors du développement et une fonctionnalité de débogage, vous pouvez afficher et rechercher hello télémétrie directement dans Visual Studio, à l’aide de hello même rechercher des fonctionnalités comme dans le portail web hello.

Et lorsque l’Application Insights se connecte à une exception, vous pouvez afficher le point de données hello dans Visual Studio et passer le code approprié de toohello droites.

![Recherche Visual Studio](./media/app-insights-devops/060.png)

Pendant le débogage, vous avez télémétrie de hello option tookeep hello dans votre ordinateur de développement, affichage dans Visual Studio, mais sans l’envoyer toohello portal. Cela évite de mélanger le débogage avec les données télémétriques de production.

### <a name="build-annotations"></a>Annotations de build
Si vous utilisez Visual Studio Team Services toobuild et déployez votre application, les annotations de déploiement s’affichent dans les graphiques dans le portail de hello. Si votre dernière version avait aucun effet sur les métriques de hello, il devient évident.

![Annotations de build](./media/app-insights-devops/070.png)

### <a name="work-items"></a>Éléments de travail
Lorsqu’une alerte est émise, Application Insights peut automatiquement créer un élément de travail dans votre système de suivi du travail.

## <a name="but-what-about"></a>Mais qu’en est-il de... ?
* [Confidentialité et stockage](app-insights-data-retention-privacy.md) - Vos données télémétriques sont conservées sur des serveurs Azure sécurisés.
* Performances - impact de hello est très faible. Les données télémétriques sont traitées par lot.
* [Tarification](app-insights-pricing.md) - Vous pouvez démarrer gratuitement tant que votre volume reste faible.


## <a name="video"></a>Vidéo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Étapes suivantes
La prise en main d’Application Insights est simple. les options principales Hello sont :

* Instrumenter une application web déjà en cours d’exécution. Cela vous donne toutes les données de télémétrie hello performance intégrés. Elles sont disponibles pour [Java](app-insights-java-live.md) et les [serveurs IIS](app-insights-monitor-performance-live-website-now.md), ainsi que pour les [applications web Azure](app-insights-azure.md).
* Instrumenter votre projet pendant le développement. Vous pouvez effectuer cette tâche pour des applications [ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md) et [Node.js](app-insights-nodejs.md) et une multitude d’[autres types](app-insights-platforms.md). 
* Instrumenter [n’importe quelle page web](app-insights-javascript.md) en y ajoutant un court extrait de code.

