---
title: "aaaSmart - détection des anomalies de performances | Documents Microsoft"
description: "Application Insights réalise une analyse télémétrique intelligente de votre application et vous avertit des éventuels problèmes de performances. Cette fonctionnalité ne nécessite aucune configuration."
services: application-insights
documentationcenter: windows
author: antonfrMSFT
manager: carmonm
ms.assetid: 6acd41b9-fbf0-45b8-b83b-117e19062dd2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 5/04/2017
ms.author: bwren
ms.openlocfilehash: 60f10612188920330030129f7464e2f398ef1f2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="smart-detection---performance-anomalies"></a>Détection intelligente - anomalies de performances

[Application Insights](app-insights-overview.md) automatiquement analyse hello les performances de votre application web et peut vous avertir de problèmes potentiels. Vous pouvez lire ceci parce que vous avez reçu une de nos notifications de détection intelligente.

Cette fonctionnalité ne requiert aucune configuration spéciale, sauf la configuration de votre application pour Application Insights (sur [ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md) ou [Node.js](app-insights-nodejs.md) et dans le [code de page web](app-insights-javascript.md)). Elle est active lorsque votre application génère suffisamment de données de télémétrie.

## <a name="when-would-i-get-a-smart-detection-notification"></a>Quand pouvez-vous recevoir une notification de détection intelligente ?

Application Insights a détecté que hello les performances de votre application se sont dégradées dans une des manières suivantes :

* **Une dégradation des temps de réponse** -votre application a démarré répond toorequests plus lentement que celui qu’elle est utilisée pour. modification de Hello ont été rapide, par exemple, car il était une régression dans votre déploiement les plus récentes. Ou ils peuvent avoir été progressifs, probablement du fait d’une fuite de mémoire. 
* **Dégradation de durée de dépendance** -votre application effectue des appels tooa REST API, de base de données ou d’autre dépendance. dépendance de Hello répond plus lentement qu’auparavant.
* **Modèle de ralentissement des performances** -votre application s’affiche toohave performances problème qui affecte uniquement certaines demandes. Par exemple, les pages se chargent plus lentement dans un type de navigateur que dans d’autres, ou les demandes sont traitées plus lentement à partir d’un serveur particulier. À l’heure actuelle, nos algorithmes examinent le temps de chargement des pages, le temps de réponse aux demandes et le temps de réponse des dépendances.  

Active la détection nécessite au moins 8 jours de télémétrie à un volume exploitable dans l’ordre tooestablish une ligne de base des performances normales. Par conséquent, lorsque votre application a été exécutée pendant cette période, tout problème significatif entraîne une notification.


## <a name="does-my-app-definitely-have-a-problem"></a>Mon application rencontre-t-elle vraiment un problème ?

Non, une notification ne signifie pas que votre application rencontre réellement un problème. Il est simplement une suggestion à propos de quelque chose que vous pourriez toolook au plus près.

## <a name="how-do-i-fix-it"></a>Comment la corriger ?

les notifications de Hello contiennent des informations de diagnostic. Voici un exemple :


![Voici un exemple de détection Dégradation du temps de réponse du serveur](./media/app-insights-proactive-diagnostics/server_response_time_degradation.png)

1. **Tri**. notification de Hello montre combien d’utilisateurs ou le nombre d’opérations est affecté. Vous pouvez attribuer un problème de toohello de priorité.
2. **Portée**. Problème de hello affecte tout le trafic, ou uniquement certaines pages ? Est informatique limité tooparticular navigateurs ou des emplacements ? Ces informations peuvent être obtenues à partir de la notification de hello.
3. **Diagnostic**. Souvent, les informations de diagnostic hello dans la notification de hello suggère la nature hello de problème de hello. Par exemple, si le temps de réponse ralentit lorsque le taux de demandes est élevé, cela suggère que votre serveur ou les dépendances sont surchargés. 

    Dans le cas contraire, ouvrez le panneau de performances hello dans Application Insights. Vous y trouverez des données de [Profileur](app-insights-profiler.md). Si les exceptions sont levées, vous pouvez aussi essayer hello [débogueur de l’instantané](app-insights-snapshot-debugger.md).



## <a name="configure-email-notifications"></a>Configurer les notifications par courrier électronique

Les notifications de détection actives sont activées par défaut et envoyées toothose ayant [propriétaires, collaborateurs et les lecteurs, accéder aux ressources d’Application Insights toohello](app-insights-resources-roles-access-control.md). toochange cela, cliquez sur **configurer** hello notification par courrier électronique ou ouvrir des paramètres de détection actives dans Application Insights. 
  
  ![Paramètres de détection intelligente](./media/app-insights-proactive-diagnostics/smart_detection_configuration.png)
  
  * Vous pouvez utiliser hello **vous désabonner** lien dans hello détection actives par courrier électronique toostop recevoir des notifications par courrier électronique de hello.

Des messages électroniques relatifs des anomalies de performances détections actives sont messagerie tooone limité par jour par la ressource Application Insights. e-mail de Hello est envoyé uniquement s’il existe au moins un nouveau problème qui a été détecté pour ce jour. Vous n’obtiendrez pas plusieurs fois le même message. 

## <a name="faq"></a>Forum Aux Questions

* *Mais alors, vous examinez mes données ?*
  * Non. service de Hello est entièrement automatique. Vous obtenez uniquement les notifications hello. Vos données sont [privées](app-insights-data-retention-privacy.md).
* *Vous analysez de toutes les données hello collectées par Application Insights ?*
  * Pas à l'heure actuelle. Actuellement, nous analysons le temps de réponse des demandes, le temps de réponse des dépendances et le temps de chargement des pages. L’analyse d’autres métriques se trouve sur notre liste de travaux en souffrance.

* À quels types d’applications cela s’applique-t-il ?
  * Ces dégradations sont détectées dans toute application qui génère des données de télémétrie hello approprié. Si vous avez installé Application Insights dans votre application web, les demandes et les dépendances sont automatiquement suivies. Mais dans les services principaux ou d’autres applications, si vous avez inséré des appels trop[TrackRequest()](app-insights-api-custom-events-metrics.md#trackrequest) ou [TrackDependency](app-insights-api-custom-events-metrics.md#trackdependency), détection intelligente fonctionnera Bonjour même façon.

* *Puis-je créer mes propres règles de détection d’anomalies ou personnaliser des règles existantes ?*

  * Pas encore, mais vous pouvez :
    * [configurer des alertes](app-insights-alerts.md) qui vous indiquent qu'une métrique dépasse un seuil ;
    * [Exporter les données de télémétrie](app-insights-export-telemetry.md) tooa [base de données](app-insights-code-sample-export-sql-stream-analytics.md) ou [tooPowerBI](app-insights-export-power-bi.md), où vous pouvez les analyser vous-même.
* *La fréquence à laquelle l’analyse de hello est effectuée ?*

  * Nous exécutez hello analyse quotidiennement sur les données de télémétrie hello de hello jour précédent (jour complet dans le fuseau horaire UTC).
* *Cela remplace-t-il les [alertes de métrique](app-insights-alerts.md)?*
  * Non.  Nous ne validez pas toodetecting chaque comportement que vous pouvez envisager anormale.


* *Si vous ne faites rien dans la réponse tooa notification, sera recevoir un rappel ?*
  * Non, vous ne recevez qu’un message pour chaque problème. Si le problème de hello persiste, il mettra à jour Bonjour que détection intelligente flux panneau.
* *J’ai perdu par courrier électronique hello. Où puis-je trouver des notifications de hello dans le portail de hello ?*
  * Dans la vue d’ensemble des Application Insights hello de votre application, cliquez sur hello **détection intelligente** vignette. Il vous serez en mesure de toofind que too90 jours toutes les notifications de sauvegarde.

## <a name="how-can-i-improve-performance"></a>Comment améliorer les performances ?
Réponses lentes et ayant échouées sont un des plus frustrant lors de hello pour les utilisateurs du site web, comme vous le savez à partir de votre propre expérience. Par conséquent, il est important de tooaddress hello problèmes.

### <a name="triage"></a>Tri
Tout d’abord, est-il important ? Si une page est toujours lente tooload, mais uniquement de 1 % des utilisateurs de votre site jamais avoir toolook dessus, vous disposez peut-être plus importante toothink de choses sur. Sur hello autre part, si une seule ouvrez-le 1 % des utilisateurs, mais il lève des exceptions chaque fois, ce qui peut être intéressant d’examen.

Utiliser la déclaration d’impact hello (utilisateurs affectés ou % du trafic) en règle générale, mais gardez à l’esprit qu’il n’est pas tout hello. Rassemblez les autres tooconfirm de preuve.

Prendre en compte les paramètres hello du problème de hello. Si le problème est lié à la géographie, configurez des [tests de disponibilité](app-insights-monitor-web-app-availability.md) incluant la région. Il se peut qu’il y ait un problème de réseau dans la zone.

### <a name="diagnose-slow-page-loads"></a>Diagnostiquer des chargements de page lents
Où est le problème de hello ? Est toorespond lente du serveur hello, est page hello très long, ou hello browser a toodo une grande quantité de travail toodisplay il ?

Ouvrez le panneau de mesure des navigateurs hello. Hello segmentée affichage du navigateur page charge temps indique où va durée hello time. 

* Si **envoyer la durée de la demande** est élevée, des serveurs hello répond lentement ou demande de hello est une demande post avec une grande quantité de données. Examinez hello [des métriques de performances](app-insights-web-monitor-performance.md#metrics) tooinvestigate les temps de réponse.
* Configurer [le suivi des dépendances](app-insights-asp-net-dependencies.md) toosee si la lenteur de hello est tooexternal services ou de votre base de données.
* Si la **réception de réponse** est prédominante, votre page et ses composants dépendants (JavaScript, CSS, images, etc., mais pas de données chargées de manière asynchrone) sont longs. Configurer un [test de disponibilité](app-insights-monitor-web-app-availability.md), et être tooset que des composants dépendants hello option tooload. Lorsque vous obtenez des résultats, ouvrez détail hello d’un résultat et développez-le toosee hello temps de différents fichiers de chargement.
* Des **durées de traitement du client** prolongées suggèrent que l'exécution des scripts est lente. Si le motif de hello n’est pas évident, envisagez d’ajouter du code de minutage et envoyer des temps de hello dans les appels de trackMetric.

### <a name="improve-slow-pages"></a>Améliorer les pages lentes
Il existe un site web complet des conseils sur l’amélioration de vos réponses du serveur et le temps de chargement de page, et nous tenterons toorepeat tout ici. Voici quelques conseils que vous connaissez sans doute déjà, tooget simplement vous envisagez :

* Lentes à charger en raison de fichiers volumineux : charger les scripts hello et autres parties de façon asynchrone. Utiliser le regroupement de scripts. Saut de page principal de hello dans les widgets qui chargent leurs données séparément. Ne pas envoyer de HTML ancien standard pour les tables long : utiliser un script toorequest hello de données en tant que JSON ou un autre format compact, puis remplissez la table hello en place. Il n’y a toohelp infrastructures excellent avec tout cela. (Elles aussi comportent des scripts volumineux, bien sûr.)
* Ralentir les dépendances de serveur : envisagez hello emplacements géographiques de vos composants. Par exemple, si vous utilisez Azure, assurez-vous hello web server et la base de données hello sont Bonjour même région. Les requêtes récupèrent-elles plus d’informations que nécessaire ? La mise en mémoire cache ou en lot peut-elle aider ?
* Problèmes de capacité : examinez les métriques de serveur hello de temps de réponse et le nombre de requêtes. Si les temps de réponse présentent des pics disproportionnés en termes de nombre de requêtes, vos serveurs sont étirés.


## <a name="server-response-time-degradation"></a>Dégradation du temps de réponse du serveur

notification une dégradation des temps de réponse à Hello indique :

* temps de réponse Hello comparées toonormal le temps de réponse pour cette opération.
* Le nombre d’utilisateurs affectés.
* Temps de réponse moyen et le temps de réponse 90e centile pour cette opération jour-là hello de détection de hello et 7 jours avant. 
* Nombre de demandes de cette opération jour hello de détection de hello et 7 jours avant.
* Corrélation entre la dégradation de cette opération et les dégradations de dépendances associées. 
* Toohelp des liens vous diagnostiquez le problème de hello.
  * Effectue le suivi du Générateur de profils toohelp vous permet d’afficher où la durée de l’opération est passée (hello lien est disponible si les exemples de trace du Générateur de profils ont été collectés pour cette opération pendant la période de détection hello). 
  * Rapports de performance dans l’Explorateur de mesures, dans lequel vous pouvez segmenter et traiter une plage de temps/des filtres pour cette opération.
  * Les appels de recherche pour ce tooview les propriétés des appels spécifiques.
  * Signale un échec - si count > 1, cela signifie que des échecs dans cette opération qui ont pu contribuer tooperformance dégradation.

## <a name="dependency-duration-degradation"></a>Dégradation de la durée de dépendance

Application moderne adopter plus l’approche de conception de services micro conduisant dans de nombreux cas tooheavy fiabilité sur des services externes. Par exemple, si votre application s’appuie sur une plateforme de données ou si vous générez votre propre robot de service vous sera probablement relais sur certaines tooenable de fournisseur de services cognitifs votre toointeract robots manières plus humaine et certaines données de stocker pour hello toopull de robot de service à partir des réponses.  

Exemple de notification de dégradation de dépendance :

![Voici un exemple de détection de la dégradation de la durée de dépendance](./media/app-insights-proactive-diagnostics/dependency_duration_degradation.png)

Notez qu’il vous indique :

* durée de Hello comparées toonormal le temps de réponse pour cette opération
* Le nombre d’utilisateurs affectés
* Durée moyenne et 90e centile durée de cette dépendance jour hello de détection de hello et 7 jours avant
* Nombre de dépendance appelle hello au jour de la détection de hello et 7 jours avant
* Toohelp des liens vous diagnostiquez le problème de hello
  * Rapports de performances dans l’Explorateur de mesures de cette dépendance
  * Recherche de cette dépendance appelle tooview propriétés des appels
  * Rapports d’échec - si count > 1, ce qui signifie qu’il existait des échecs de dépendance appelle pendant hello détection période qui ont pu contribuer tooduration dégradation. 
  * Ouverture de la fonctionnalité Analytics permettant de calculer cette durée de dépendance et un nombre  

## <a name="smart-detection-of-slow-performing-patterns"></a>Détection intelligente de modèles de performances lentes 

Application Insights recherche les problèmes de performances pouvant toucher uniquement une partie de vos utilisateurs ou bien l’ensemble des utilisateurs mais dans certains cas de figure seulement. Par exemple, une notification sur des pages qui se chargent plus lentement dans un type de navigateur que dans d’autres types de navigateurs ou si les demandes sont traitées plus lentement à partir d’un serveur particulier. Elle peut aussi détecter les problèmes liés à des combinaisons de propriétés, tels que des pages qui se chargent lentement dans une zone géographique pour des clients utilisant un système d’exploitation particulier.  

Anomalies telles sont très difficile toodetect suffit d’inspecter les données de salutation, mais sont plus courantes que vous ne le pensez. Souvent, elles sont révélées par les plaintes des clients. À ce moment-là, il est trop tard : les utilisateurs de hello affecté sont déjà de commutation tooyour concurrents !

Actuellement, nos algorithmes examiner les temps de chargement de page, les temps de réponse de demande sur le serveur de hello et les temps de réponse de dépendance.  

Vous n’avez tooset tous les seuils ou configurer des règles. Apprentissage et les algorithmes d’exploration de données sont toodetect utilisé les modèles anormaux.

![À partir de l’alerte par courrier électronique de hello, cliquez sur hello lien tooopen hello rapport de diagnostics dans Azure](./media/app-insights-proactive-performance-diagnostics/03.png)

* **Lorsque** indique hello durée hello problème a été détecté.
* **Quoi** (What) décrit :

  * problème de Hello qui a été détectée ;
  * caractéristiques de Hello Hello jeu d’événements que nous avons trouvé affiché problème hello.
* tableau de Hello compare le jeu de peu performante hello avec un comportement moyenne de tous les autres événements hello.

Cliquez sur hello liens tooopen métrique Explorer et recherche sur les rapports appropriés, filtrés sur les temps de hello et les propriétés de hello lente effectuant ensemble.

Modifier hello temps plage et les filtres tooexplore hello données de télémétrie.

## <a name="next-steps"></a>Étapes suivantes
Ces outils de diagnostic vous aident à inspecter les données de télémétrie hello à partir de votre application :

* [Profileur](app-insights-profiler.md) 
* [Débogueur de capture instantanée](app-insights-snapshot-debugger.md)
* [Analytics](app-insights-analytics-tour.md)
* [Diagnostics intelligents Analytics](app-insights-analytics-diagnostics.md)

Les détections intelligentes sont entièrement automatiques. Mais peut-être voudriez-vous tooset certaines alertes plus ?

* [Alertes de mesures configurées manuellement](app-insights-alerts.md)
* [Tests web de disponibilité](app-insights-monitor-web-app-availability.md)
