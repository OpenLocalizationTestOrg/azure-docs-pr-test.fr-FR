---
title: "aaaSmart détection - échec anomalies, dans Application Insights | Documents Microsoft"
description: "Vous informe des modifications toounusual taux hello de demandes ayant échoué tooyour web app et fournit une analyse de diagnostic. Aucune configuration n’est nécessaire."
services: application-insights
documentationcenter: 
author: yorac
manager: carmonm
ms.assetid: ea2a28ed-4cd9-4006-bd5a-d4c76f4ec20b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: bwren
ms.openlocfilehash: dfd178ca9546294be91f27b0c1b846d519539b77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="smart-detection---failure-anomalies"></a>Détection intelligente des anomalies de type échec
[Application Insights](app-insights-overview.md) automatiquement vous avertit en temps quasi réel si votre application web rencontre une élévation anormale du taux de hello d’échecs de demandes de. Il détecte une augmentation inhabituelle taux hello de requêtes HTTP ou d’appels de dépendance qui sont signalées comme ayant échoué. Les demandes ayant échoué sont généralement celles dont le code de réponse est supérieur ou égal à 400. toohelp trier et de diagnostiquer le problème de hello, une analyse des caractéristiques de hello des échecs de hello et de la télémétrie associée est fournie dans la notification de hello. Il existe également un portail d’Application Insights toohello des liens pour un diagnostic plus poussé. Hello fonctionnalité doit sans configuration ni la configuration, car il utilise l’apprentissage algorithmes toopredict hello normal taux d’échec.

Cette fonctionnalité fonctionne pour les applications web Java et ASP.NET, hébergées dans le cloud de hello ou sur vos serveurs. Elle sert également pour n’importe quelle application qui génère de la télémétrie de demande ou de dépendance : par exemple, si vous avez un rôle de travail qui appelle [TrackRequest()](app-insights-api-custom-events-metrics.md#trackrequest) ou [TrackDependency()](app-insights-api-custom-events-metrics.md#trackdependency).

Après avoir configuré [Application Insights pour votre projet](app-insights-overview.md), et autant de votre application génère une certaine quantité minimale de télémétrie, Active la détection des anomalies de défaillance prend comportement normal de hello toolearn de votre application, avant qu’il des dernières 24 heures est sous tension et peut envoyer des alertes.

Voici un exemple d’alerte.

![Exemple d’alerte de détection intelligente affichant l’analyse du cluster au moment de l’échec](./media/app-insights-proactive-failure-diagnostics/013.png)

> [!NOTE]
> Par défaut, vous obtenez un format de message plus court que dans cet exemple. Toutefois, vous pouvez [format détaillé de commutateur toothis](#configure-alerts).
>
>

Notez qu’il vous indique :

* taux d’échec Hello par rapport à un comportement toonormal des applications.
* Combien d’utilisateurs est affectés : afin de connaître la quantité tooworry.
* Un modèle de caractéristiques associé avec des erreurs de hello. Cet exemple contient un code de réponse, un nom de demande (opération) et une version de l’application spécifiques. Immédiatement, vous indique où toostart recherche dans votre code. Les autres possibilités peuvent être un type de navigateur ou un système d’exploitation client spécifique ;
* l’exception Hello, suivis de journal et Échec de la dépendance (bases de données ou d’autres composants externes) qui s’affichent toobe associé hello caractérisent les échecs.
* Lie directement recherches toorelevant télémétrie hello dans Application Insights.

## <a name="benefits-of-smart-detection"></a>Avantages de la détection intelligente
Les [alertes de mesure](app-insights-alerts.md) ordinaires vous indiquent un problème potentiel. Mais détection intelligente démarre le travail de diagnostic hello pour vous, qui effectue un grand nombre d’analyse hello vous devriez toodo vous-même. Vous obtenez hello soigneusement empaquetés, en vous permettant de tooget rapidement des résultats racine toohello de problème de hello.

## <a name="how-it-works"></a>Fonctionnement
Détection intelligente analyse télémétrie hello reçue à partir de votre application et de taux d’échec hello particulier. Cette règle dénombre hello de demandes pour le hello `Successful request` propriété a la valeur false, et nombre de hello de dépendance appelle pour quels hello `Successful call` propriété a la valeur false. Pour les demandes, par défaut, `Successful request == (resultCode < 400)` (sauf si vous avez écrit du code personnalisé trop[filtre](app-insights-api-filtering-sampling.md#filtering) ou générer vos propres [TrackRequest](app-insights-api-custom-events-metrics.md#trackrequest) appels). 

Les performances de votre application présentent un modèle de comportement typique. Certaines requêtes ou les appels de dépendance seront plus enclines toofailure que d’autres ; et hello taux d’échec global peut monter en charge augmente. Active la détection utilise apprentissage toofind ces anomalies.

Comme données de télémétrie arrive dans Application Insights à partir de votre application web, détection intelligente compare comportement actuel de hello avec des modèles de hello vu sur hello quelques jours. Si une augmentation anormale du taux d’échec est observée par rapport aux performances précédentes, une analyse est déclenchée.

Lorsqu’une analyse est déclenchée, service de hello effectue une analyse de cluster sur les demandes ayant échoué hello, tootry tooidentify une séquence de valeurs qui caractérisent les échecs de hello. Dans l’exemple hello ci-dessus, l’analyse de hello a découvert que la plupart des échecs sont sur un code de résultat spécifique, nom de la demande, hôte de l’URL du serveur et instance de rôle. En revanche, les analyse hello a découvert que la propriété du système d’exploitation client hello est répartie sur plusieurs valeurs, et par conséquent, il n’est pas répertorié.

Lorsque votre service est instrumenté avec ces appels de télémétrie, analyseur de hello recherche une exception et une erreur de dépendance qui sont associées aux requêtes dans le cluster hello qu'a identifiés, ainsi que d’un exemple de toutes les journaux de suivi associés avec ces demandes.

analyse Hello est envoyée tooyou en tant qu’alerte, sauf si vous l’avez pas configuré.

Comme hello [vous définir manuellement des alertes](app-insights-alerts.md), vous pouvez inspecter l’état hello d’alerte de hello et le configurer dans le panneau des alertes hello de votre ressource Application Insights. Mais contrairement à d’autres alertes, vous n’avez besoin tooset ou configurer la détection de Smart. Si vous le souhaitez, vous pouvez la désactiver ou changer l’adresse de messagerie électronique cible.

## <a name="configure-alerts"></a>Configurer des alertes
Vous pouvez désactiver la détection intelligente, modifier des destinataires de courrier électronique hello, créer un webhook ou participer toomore détaillée les messages d’alerte.

Ouvrez la page des alertes hello. Échec Anomalies est inclus avec toutes les alertes que vous avez défini manuellement, et vous pouvez déterminer s’il est actuellement dans l’état de l’alerte hello.

![Sur la page de vue d’ensemble de hello, cliquez sur mosaïque d’alertes. ou sur n’importe quelle page de mesures, cliquez sur le bouton Alertes.](./media/app-insights-proactive-failure-diagnostics/021.png)

Cliquez sur tooconfigure d’alerte hello il.

![Configuration](./media/app-insights-proactive-failure-diagnostics/032.png)

Notez que vous pouvez désactiver la détection intelligente, mais pas la supprimer (ni en créer une autre).

#### <a name="detailed-alerts"></a>Alertes détaillées
Si vous sélectionnez « Obtenir des diagnostics plus détaillés », par courrier électronique hello contient des informations de diagnostic. Vous serez parfois problème de hello toodiagnose en mesure uniquement à partir de données hello par courrier électronique hello.

Il existe un léger risque hello plus détaillé d’alerte peut contenir des informations sensibles, car il inclut des messages d’exception et trace. Toutefois, cela se produit uniquement si votre code autorise que ces informations sensibles soient incluses dans ces messages.

## <a name="triaging-and-diagnosing-an-alert"></a>Triage et diagnostic d’une alerte
Une alerte indique qu’une élévation anormale du taux de demandes ayant échoué hello d’a été détectée. Il est probable que votre application ou son environnement rencontre un problème.

À partir du pourcentage de hello de demandes et le nombre d’utilisateurs affectés, vous pouvez décider comment urgente problème de hello est. Dans l’exemple hello ci-dessus, les taux d’échec hello 22.5 % compare avec un taux normal de 1 %, indique que quelque chose se passe. Sur hello autre part, les 11 utilisateurs ont été affectés. S’il s’agissait de votre application, vous serez en mesure de tooassess l’importance est.

Dans de nombreux cas, vous serez problème de hello toodiagnose en mesure de rapidement à partir de nom de la demande hello, exception, données de défaillance et la trace de la dépendance fournies.

Il existe certains autres indices. Par exemple, le taux d’échec de dépendance hello dans cet exemple est hello identique hello taux d’exception (89.3 %). Il est possible que les exceptions hello survient directement à partir de l’échec de la dépendance hello - ce qui vous donne une idée précise de l’emplacement toostart recherche dans votre code.

tooinvestigate en outre, les liens hello dans chaque section vous conduira droite tooa [page de recherche](app-insights-diagnostic-search.md) filtrée toohello les demandes appropriées, exception, dépendance ou des traces. Vous pouvez aussi ouvrir hello [portail Azure](https://portal.azure.com), parcourir les ressources d’Application Insights toohello pour votre application et ouvrir le panneau des échecs de hello.

Dans cet exemple, en cliquant sur hello ' dépendance échecs lien Afficher les détails » ouvre le panneau de recherche d’Application Insights hello. Il montre l’instruction SQL hello qui comporte un exemple de la cause première hello : les valeurs NULL ont été fournis à des champs obligatoires et n’a pas réussi la validation pendant hello opération d’enregistrement.

![Recherche de diagnostic](./media/app-insights-proactive-failure-diagnostics/051.png)

## <a name="review-recent-alerts"></a>Consulter les alertes récentes

Cliquez sur **détection intelligente** alerte plus récente de tooget toohello :

![Résumé des alertes](./media/app-insights-proactive-failure-diagnostics/070.png)


## <a name="whats-hello-difference-"></a>Qu’est la différence de hello...
La détection intelligente des anomalies de type échec vient compléter d’autres fonctionnalités d’Application Insights similaires, mais distinctes.

* [Metric Alerts](app-insights-alerts.md) , qui peuvent surveiller un large éventail de mesures telles que l’occupation du processeur, les taux de demandes, les temps de chargement de page, etc. Vous pouvez les utiliser toowarn vous, par exemple, si vous avez besoin de tooadd davantage de ressources. En revanche, Active la détection des anomalies de défaillance couvre un toonotify petite plage métriques critiques (actuellement uniquement des demandes ayant échoué taux), conçue vous dans près de manière en temps réel une fois augmente considérablement la vitesse des demandes ayant échoué de votre application web par rapport à l’application tooweb comportement normal.

    Détection intelligente ajuste automatiquement son seuil dans les conditions de tooprevailing de réponse.

    Détection intelligente démarre le travail de diagnostic hello pour vous.
* [Active la détection des anomalies de performances](app-insights-proactive-performance-diagnostics.md) également utilise machine intelligence toodiscover inhabituelles dans vos métriques, et aucune configuration en vous est requise. Mais contrairement à Active la détection d’anomalies de défaillance, hello Active la détection des anomalies de performances vise toofind segments de votre collecteur d’utilisation qui peut être mal fournie, par exemple par des pages spécifiques sur un type spécifique de navigateur. analyse de Hello est effectué quotidiennement, et si des résultats sont trouvé, il est probable toobe beaucoup moins urgent à une alerte. En revanche, analyse hello pour les anomalies de défaillance est effectuée en permanence télémétrie entrant, et vous serez averti dans les minutes si le taux de défaillance de serveur sont plus que prévu.

## <a name="if-you-receive-a-smart-detection-alert"></a>Si vous recevez une alerte de la détection intelligente
*Pourquoi ai-je reçu cette alerte ?*

* Nous avons détecté une élévation anormale dans des demandes ayant échoué fréquence par rapport toohello normal ligne de base de hello précédant la période. Après l’analyse des échecs de hello et télémétrie associée, nous pensons qu’il existe un problème que vous devez examiner.

*Notification de hello signifie que faire sans aucun doute un problème ?*

* Nous essayons tooalert sur l’interruption de l’application ou une dégradation, mais uniquement bien comprendre la sémantique hello et l’impact de hello application hello ou les utilisateurs.

*Mais alors, vous examinez mes données ?*

* Non. service de Hello est entièrement automatique. Vous obtenez uniquement les notifications hello. Vos données sont [privées](app-insights-data-retention-privacy.md).

*Alerte de toothis toosubscribe ai-je besoin ?*

* Non. Chaque application envoie demande de télémétrie a une règle d’alerte actives détection hello.

*Puis-je annuler l’abonnement ou obtenir des notifications de hello envoyées à la place des collègues de toomy ?*

* Oui, les règles dans l’alerte, cliquez sur tooconfigure de règle de détection actives hello il. Vous pouvez désactiver l’alerte de hello ou modifier des destinataires pour l’alerte de hello.

*J’ai perdu par courrier électronique hello. Où puis-je trouver des notifications de hello dans le portail de hello ?*

* Dans les journaux d’activité hello. Dans Azure, ouvrez la ressource d’Application Insights hello pour votre application, puis sélectionnez les journaux d’activité.

*Certaines des alertes de hello sur les problèmes connus et je ne souhaite pas tooreceive les.*

* Notre backlog comporte la suppression de l’alerte.

## <a name="next-steps"></a>Étapes suivantes
Ces outils de diagnostic vous aident à inspecter les données de télémétrie hello à partir de votre application :

* [Metrics Explorer](app-insights-metrics-explorer.md)
* [Navigateur de recherche](app-insights-diagnostic-search.md)
* [Analytics : un puissant langage de requête](app-insights-analytics-tour.md)

Les détections intelligentes sont entièrement automatiques. Mais peut-être voudriez-vous tooset certaines alertes plus ?

* [Alertes de mesures configurées manuellement](app-insights-alerts.md)
* [Tests web de disponibilité](app-insights-monitor-web-app-availability.md)
