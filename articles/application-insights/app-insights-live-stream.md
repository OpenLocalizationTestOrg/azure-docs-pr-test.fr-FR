---
title: "aaaLive métriques de flux de données avec des mesures personnalisées et des diagnostics dans Azure Application Insights | Documents Microsoft"
description: "Surveillez votre application web en temps réel avec des métriques personnalisées, et diagnostiquez les problèmes avec un flux temps réel des échecs, des traces et des événements."
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 1f471176-38f3-40b3-bc6d-3f47d0cbaaa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: bwren
ms.openlocfilehash: 68ddfbf387379ea778c20280c4ec96baa06d3273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="live-metrics-stream-monitor--diagnose-with-1-second-latency"></a>Flux de métriques temps réel : Surveiller et diagnostiquer avec une latence de 1 seconde 

Sonde de battements du coeur hello de votre application web dynamique et de production à l’aide de flux Live de métriques à partir de [Application Insights](app-insights-overview.md). Sélectionnez et toowatch de compteurs métriques et les performances en temps réel, sans n’importe quel service de tooyour perturbation de filtre. Inspectez les traces de pile à partir d’échantillons de demandes en échec et d’exceptions. En combinaison avec le [profileur](app-insights-profiler.md), le [débogueur d’instantané](app-insights-snapshot-debugger.md) et les [tests de performances](app-insights-monitor-web-app-availability.md#performance-tests), les flux de métriques temps réel constituent un outil de diagnostic puissant et non invasif pour votre site web dynamique.

Avec les flux de métriques temps réel, vous pouvez :

* Valider un correctif lors de sa publication, en observant les performances et les nombres d’échecs.
* Regardez effet hello du test de charge et de diagnostiquer les problèmes en direct. 
* Se concentrer sur les sessions de test particulier ou filtrer les problèmes connus, par sélection et filtrage des métriques hello toowatch.
* Obtenir les traces des exceptions quand elles se produisent.
* Essayez d’utiliser des filtres toofind hello des indicateurs de performance clés les plus pertinents.
* Surveiller en temps réel des compteurs de performances Windows.
* Identifiez un serveur qui rencontre des problèmes et facilement filtrer tous les hello actives/indicateur de performance clé flux toojust ce serveur.

[![Vidéo sur les flux de métriques temps réel](./media/app-insights-live-stream/youtube.png)](https://www.youtube.com/watch?v=zqfHf1Oi5PY)

Flux Live de métriques est actuellement disponible sur les applications ASP.NET s’exécutent localement ou dans le Cloud de hello. 

## <a name="get-started"></a>Prise en main

1. Si vous ne l’avez pas encore fait, [installez Application Insights](app-insights-asp-net.md) dans votre application web ASP.NET ou dans votre [application de serveur Windows](app-insights-windows-services.md). 
2. **Dernière version de mise à jour toohello** du package d’Application Insights hello. Dans Visual Studio, cliquez avec le bouton droit sur votre projet et choisissez **Gérer les packages NuGet**. Ouvrez hello **mises à jour** onglet, vérifiez **inclure la version préliminaire**, sélectionnez tous les packages de Microsoft.ApplicationInsights.* hello.

    Redéployez votre application.

3. Bonjour [portail Azure](https://portal.azure.com), ouvrir la ressource d’Application Insights hello pour votre application, puis ouvrez le flux Live.

4. [Canal de contrôle sécurisé hello](#secure-the-control-channel) si vous pouvez utiliser des données sensibles telles que les noms des clients dans vos filtres.


![Dans le panneau de vue d’ensemble de hello, cliquez sur le flux en direct](./media/app-insights-live-stream/live-stream-2.png)

### <a name="no-data-check-your-server-firewall"></a>Pas de données ? Vérifier le pare-feu de votre serveur

Vérifiez hello [sortant des ports pour les flux Live de métriques](app-insights-ip-addresses.md#outgoing-ports) sont ouverts dans le pare-feu hello de vos serveurs. 


## <a name="how-does-live-metrics-stream-differ-from-metrics-explorer-and-analytics"></a>En quoi les flux de métriques temps réel diffèrent-ils de Metrics Explorer et d’Analytique ?

| |Flux temps réel | Metrics Explorer et Analytique |
|---|---|---|
|Latence|Données affichées en une seconde|Agrégé sur plusieurs minutes|
|Pas de conservation|Elles sont conservées pendant que se trouve sur le graphique de hello et il est ensuite ignoré|[Données conservées pendant 90 jours](app-insights-data-retention-privacy.md#how-long-is-the-data-kept)|
|À la demande|Les données sont diffusées dès que vous ouvrez les métriques temps réel|Les données sont envoyées chaque fois que hello SDK est installé et activé|
|Gratuit|Pas de facturation pour les données du flux temps réel|L’objet trop[tarification](app-insights-pricing.md)
|échantillonnage|Tous les compteurs et métriques sélectionnés sont transmis. Les échecs et les traces de pile sont échantillonnés. Les processeurs de télémétrie ne sont pas appliqués.|Les événements peuvent être [échantillonnés](app-insights-api-filtering-sampling.md)|
|Canal de contrôle|Les signaux de contrôle de filtre sont envoyés toohello Kit de développement logiciel. Nous vous recommandons de [sécuriser ce canal](#secure-channel).|La communication est à sens unique, toohello portail|


## <a name="select-and-filter-your-metrics"></a>Sélectionner et filtrer vos métriques

(Disponible sur classique avec les applications ASP.NET hello dernière version du SDK.)

Vous pouvez surveiller les KPI personnalisé en direct en appliquant des filtres arbitraires sur toutes les données de télémétrie Application Insights à partir du portail de hello. Cliquez sur le contrôle de filtre hello montre lorsque vous la souris sur un des graphiques de hello. Hello suivant le graphique est tracé nombre demande KPI personnalisé avec des filtres sur les attributs d’URL et la durée. Valider vos filtres par hello section d’aperçu du flux de données qui montre un flux en direct de télémétrie qui correspond aux critères de hello que vous avez spécifié à n’importe quel point dans le temps. 

![Indicateur de performance clé (KPI) de demande personnalisé](./media/app-insights-live-stream/live-stream-filteredMetric.png)

Vous pouvez surveiller une valeur autre qu’un nombre. les options de Hello dépendent de type hello du flux, ce qui peut être n’importe quel télémétrie Application Insights : demandes, dépendances, exceptions, des traces, les événements ou métriques. Il peut s’agir d’une [mesure personnalisée](app-insights-api-custom-events-metrics.md#properties) :

![Options de valeur](./media/app-insights-live-stream/live-stream-valueoptions.png)

En outre tooApplication télémétrie Insights, vous pouvez également surveiller n’importe quel compteur de performances de Windows en sélectionnant qui à partir des options de flux hello et en fournissant le nom hello hello du compteur de performance.

Les métriques temps réel sont agrégées à deux endroits : localement sur chaque serveur, puis sur tous les serveurs. Vous pouvez modifier la valeur par défaut de hello en sélectionnant l’option autres options dans hello respectifs les zones déroulantes.

## <a name="sample-telemetry-custom-live-diagnostic-events"></a>Exemple de télémétrie : événements de diagnostic temps réel personnalisés
Par défaut, flux d’événements hello présente des exemples de demandes ayant échoué et les appels de dépendance, les exceptions, les événements et les traces. Cliquez sur critères hello filtre icône toosee hello appliquée à n’importe quel point dans le temps. 

![Flux temps réel par défaut](./media/app-insights-live-stream/live-stream-eventsdefault.png)

Comme avec les mesures, vous pouvez spécifier n’importe quel tooany critères arbitraire des types de données de télémétrie Application Insights hello. Dans cet exemple, nous sélectionnons des échecs de demande, des suivis et des événements spécifiques. Nous sélectionnons également toutes les exceptions et tous les échecs de dépendance.

![Flux temps réel personnalisé](./media/app-insights-live-stream/live-stream-events.png)

Remarque : Actuellement, pour les critères basés sur le message d’Exception, utilisez message d’exception extérieur hello. Bonjour précédent exemple, toofilter des exceptions sans gravité de hello avec le message d’exception interne (suit hello » <--« délimiteur) hello « client » déconnecté. utilisez un critère de message ne contenant pas « Erreur de lecture du contenu de la demande ».

Afficher les détails de hello d’un élément dans hello live flux en cliquant dessus. Vous pouvez suspendre hello flux soit en cliquant sur **suspendre** simplement le défilement vers le bas ou en cliquant sur un élément. Les flux Live reprend après le défilement arrière toohello haut, ou en cliquant sur le compteur hello d’éléments collectées pendant qu’il a été suspendu.

![Échecs dynamiques échantillonnés](./media/app-insights-live-stream/live-metrics-eventdetail.png)

## <a name="filter-by-server-instance"></a>Filtrer par instance de serveur

Si vous souhaitez toomonitor une instance de rôle de serveur spécifique, vous pouvez filtrer par serveur.

![Échecs dynamiques échantillonnés](./media/app-insights-live-stream/live-stream-filter.png)

## <a name="sdk-requirements"></a>Configuration requise du Kit de développement logiciel (SDK)
Le flux de métriques temps réel personnalisé est disponible avec la version 2.4.0-beta2 ou plus récente du [Kit de développement logiciel (SDK) Application Insights pour le web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/). N’oubliez pas d’option de « Inclure la version préliminaire » tooselect à partir du Gestionnaire de package NuGet.

## <a name="secure-hello-control-channel"></a>Sécuriser le canal de contrôle hello
vous spécifiez des critères filtres personnalisés Hello sont envoyés composant des métriques de Live toohello arrière Bonjour Application Insights SDK. filtres de Hello peut contenir potentiellement des informations sensibles telles que CustomerID. Vous pouvez apporter les canaux hello sécurisé avec une clé secrète d’API en outre toohello clé d’instrumentation.
### <a name="create-an-api-key"></a>Création d’une clé API

![Création d’une clé API](./media/app-insights-live-stream/live-metrics-apikeycreate.png)

### <a name="add-api-key-tooconfiguration"></a>Ajouter tooConfiguration clée d’API
Dans le fichier applicationinsights.config de hello, ajoutez hello AuthenticationApiKey toohello QuickPulseTelemetryModule :
``` XML

<Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.QuickPulse.QuickPulseTelemetryModule, Microsoft.AI.PerfCounterCollector">
      <AuthenticationApiKey>YOUR-API-KEY-HERE</AuthenticationApiKey>
</Add> 

```
Ou, dans le code, définissez-la sur hello QuickPulseTelemetryModule :

``` C#

    module.AuthenticationApiKey = "YOUR-API-KEY-HERE";

```

Toutefois, si vous reconnaissez et approuver que tout hello serveurs connectés, vous pouvez essayer des filtres personnalisés hello sans canal de hello authentifié. Cette option est disponible pour six mois. Ce remplacement est nécessaire à chaque nouvelle session, ou lorsqu’un nouveau serveur est en ligne.

![Options d’authentification de métriques temps réel](./media/app-insights-live-stream/live-stream-auth.png)

>[!NOTE]
>Nous vous recommandons vivement de configurer le canal de hello authentifié avant d’entrer des informations potentiellement sensibles, telles que CustomerID dans les critères de filtre hello.
>

## <a name="generating-a-performance-test-load"></a>Génération d’un test de performances de charge

Si vous souhaitez effet de hello toowatch d’une charge augmenter, panneau de Test de performances utilisation hello. Il simule des demandes à partir d’un certain nombre d’utilisateurs simultanés. Il peut s’exécuter soit « tests manuels » (tests de ping) d’une URL unique, ou il peut exécuter un [test de performances web de multi-step](app-insights-monitor-web-app-availability.md#multi-step-web-tests) que vous téléchargez (de hello la même façon que la disponibilité de test).

> [!TIP]
> Après avoir créé le test de performances de hello, ouvrez le test de hello et hello lame de flux Live dans des fenêtres distinctes. Vous pouvez voir lorsque le hello en file d’attente démarre de test de performances et les flux en direct à hello espion même temps.
>


## <a name="troubleshooting"></a>Résolution des problèmes

Pas de données ? Si votre application se trouve dans un réseau protégé : le Flux de métriques temps réel utilise des adresses IP différentes d’autres données de télémétrie Application Insights. Assurez-vous que [ces adresses IP](app-insights-ip-addresses.md) sont ouvertes dans votre pare-feu.



## <a name="next-steps"></a>Étapes suivantes
* [Surveillance de l’utilisation avec Application Insights](app-insights-web-track-usage.md)
* [Utilisation de Diagnostic Search](app-insights-diagnostic-search.md)
* [Profileur](app-insights-profiler.md)
* [Débogueur de capture instantanée](app-insights-snapshot-debugger.md)
