---
title: "échantillonnage aaaTelemetry dans Azure Application Insights | Documents Microsoft"
description: "Comment tookeep hello volume de données de télémétrie sous contrôle de code."
services: application-insights
documentationcenter: windows
author: vgorbenko
manager: carmonm
ms.assetid: 015ab744-d514-42c0-8553-8410eef00368
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bwren
ms.openlocfilehash: e19c350d0a5f16736c100322a9922fcfbf5d7b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sampling-in-application-insights"></a>Échantillonnage dans Application Insights


L’échantillonnage est une fonctionnalité dans [Azure Application Insights](app-insights-overview.md). Il est recommandé de hello le trafic de façon tooreduce télémétrie et le stockage, tout en conservant une analyse statistique correcte des données d’application. filtre de Hello sélectionne les éléments associés, afin que vous pouvez naviguer entre des éléments lorsque vous effectuez des investigations en matière de diagnostic.
Lorsque les nombres de métriques sont présentés tooyou dans le portail de hello, ils sont renormalisés compte tootake Hello d’échantillonnage, toominimize un effet sur les statistiques de hello.

L’échantillonnage réduit les coûts du trafic et des données, et vous aide à éviter les limitations.

## <a name="in-brief"></a>En bref :
* Échantillonnage conserve 1 dans  *n*  enregistre et ignore le reste de hello. Par exemple, il peut conserver 1 événement sur 5, soit un taux d’échantillonnage de 20 %. 
* L’échantillonnage s’effectue automatiquement si votre application envoie de nombreuses données de télémétrie, dans les applications de serveur web ASP.NET.
* Vous pouvez également définir d’échantillonnage manuellement, soit en hello portail sur hello tarification page ; ou dans le Kit de développement ASP.NET dans le fichier .config de hello de hello, tooalso réduire le trafic réseau de hello.
* Si vous consignez des événements personnalisés et que vous souhaitez toomake sûr qu’un jeu d’événements est conservé ou ignoré ensemble, assurez-vous qu’ils ont hello même valeur OperationId.
* diviseur d’échantillonnage de Hello  *n*  est signalée dans chaque enregistrement de la propriété de hello `itemCount`, qui, dans la recherche s’affiche sous hello nom convivial « nombre de demande » ou « nombre d’événements ». Lorsque l’échantillonnage n’est pas en cours d’utilisation, `itemCount==1`.
* Si vous écrivez des requêtes Analytics, vous devez [tenir compte de l’échantillonnage](app-insights-analytics-tour.md#counting-sampled-data). En particulier, au lieu de compter simplement les enregistrements, vous devez utiliser `summarize sum(itemCount)`.

## <a name="types-of-sampling"></a>Types d’échantillonnage
Il existe trois autres méthodes d’échantillonnage :

* **Échantillonnage Adaptive** ajuste automatiquement le volume hello de télémétrie envoyé à partir du Kit de développement logiciel de hello dans votre application ASP.NET. Il s’agit du comportement par défaut depuis la version 2.0.0-beta3 du Kit de développement logiciel (SDK). Actuellement uniquement disponible pour la télémétrie ASP.NET côté serveur. 
* **Échantillonnage de taux fixe** réduit le volume de hello de télémétrie envoyé depuis votre serveur ASP.NET ou à partir de navigateurs de vos utilisateurs. Vous définissez des taux de hello. Hello client et serveur synchronisera les échantillonnages donc, de recherche, vous pouvez naviguer entre les vues de page associée et des demandes.
* **Échantillonnage de l’ingestion** fonctionne Bonjour portail Azure. Il ignore certaines des données de télémétrie hello qui arrive à partir de votre application, à une fréquence que vous définissez. Le trafic des données de télémétrie n’est pas réduit, mais cela vous permet de respecter votre quota mensuel. Hello présente l’avantage d’échantillonnage d’ingestion est que vous pouvez le définir sans redéployer votre application et uniformément fonctionne pour tous les clients et serveurs. 

Si un échantillonnage de débit adaptatif ou fixe est en cours d’utilisation, l’échantillonnage d’ingestion est désactivé.

## <a name="ingestion-sampling"></a>échantillonnage d’ingestion
Cette forme d’échantillonnage fonctionne au point hello où télémétrie hello à partir de votre serveur web, les navigateurs et périphériques atteint le point de terminaison de service hello Application Insights. Bien qu’elle ne réduit pas le trafic de télémétrie de hello envoyé à partir de votre application, elle réduit hello traitées et conservées (et facturé pour) par Application Insights.

Utilisez ce type d’échantillonnage si votre application dépasse souvent son quota mensuel et que vous ne pouvez hello à l’aide d’un des types de basée sur le Kit de développement logiciel hello d’échantillonnage. 

Définir le taux d’échantillonnage de hello Bonjour Quotas et panneau de tarification :

![À partir du Panneau de vue d’ensemble d’applications de hello, cliquez sur paramètres, des quotas, des échantillons, puis un taux d’échantillonnage et cliquez sur la mise à jour.](./media/app-insights-sampling/04.png)

Comme d’autres types d’échantillonnage, algorithme de hello conserve les éléments de télémétrie connexes. Par exemple, lorsque que vous examinez les données de télémétrie hello dans la recherche, vous serez en mesure de demande de hello toofind liés tooa des exception particulière. Les données de mesure telles que les taux de demandes et le taux d’exceptions sont correctement conservées.

Les points de données ignorés par l’échantillonnage ne sont disponibles dans aucune fonctionnalité Application Insights, par exemple l’ [exportation continue](app-insights-export-telemetry.md).

L’échantillonnage d’ingestion ne fonctionne pas pendant qu’une opération d’échantillonnage adaptatif ou taux fixe basé sur un Kit de développement logiciel (SDK) est en cours d’exécution. Si le taux d’échantillonnage hello hello SDK est inférieure à 100 %, puis hello taux d’échantillonnage de réception que vous définissez est ignoré.

> [!WARNING]
> valeur de Hello affichée sur la vignette de hello valeur hello que vous définissez pour l’échantillonnage de l’ingestion. Il ne représente le taux d’échantillonnage réelle de hello si l’échantillonnage SDK est en opération.
> 
> 

## <a name="adaptive-sampling-at-your-web-server"></a>Échantillonnage adaptatif sur votre serveur web
Échantillonnage adaptatif est disponible pour hello Application Insights SDK pour ASP.NET v 2.0.0-beta3 et versions ultérieures et est activé par défaut. 

Échantillonnage Adaptive affecte volume hello de télémétrie envoyé à partir de votre toohello application du serveur web service Application Insights. Hello volume est ajusté automatiquement tookeep au sein d’un taux maximum spécifié de trafic.

Il ne fonctionne pas quand les volumes de données de télémétrie sont bas ; ainsi, une application en mode débogage ou un site web faiblement utilisé ne sont pas affectés.

volume cible tooachieve hello, certaines des données de télémétrie hello générée est ignoré. Mais comme les autres types d’échantillonnage, algorithme de hello conserve les éléments de télémétrie connexes. Par exemple, lorsque que vous examinez les données de télémétrie hello dans la recherche, vous serez en mesure de demande de hello toofind liés tooa des exception particulière. 

Mesure de compte, telles que les taux de demande et exception sont toocompensate ajustée pour hello taux d’échantillonnage, afin qu’elles affichent des valeurs correctes environ dans l’Explorateur de métrique.

**Mettre à jour NuGet de votre projet** packages toohello dernière *préliminaires* version d’Application Insights : avec le bouton droit de projet hello dans l’Explorateur de solutions, cliquez sur Gérer les Packages NuGet, vérifiez **Include version préliminaire** et recherchez Microsoft.ApplicationInsights.Web. 

Dans [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), vous pouvez ajuster les paramètres plusieurs Bonjour `AdaptiveSamplingTelemetryProcessor` nœud. chiffres Hello indiqués sont les valeurs par défaut hello :

* `<MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>`
  
    Hello taux cible hello algorithme adaptatif judicieuse s’adresse aux **sur chaque hôte du serveur**. Si votre application web s’exécute sur plusieurs hôtes, réduisez cette valeur ainsi en tooremain au sein de votre taux de cible de trafic sur le portail d’Application Insights hello.
* `<EvaluationInterval>00:00:15</EvaluationInterval>` 
  
    intervalle de salutation à quels hello taux actuel de télémétrie est réévaluée. L’évaluation est effectuée sous forme de moyenne mobile. Vous pourriez tooshorten cet intervalle si vos données de télémétrie sont toosudden susceptibles de pics d’activité.
* `<SamplingPercentageDecreaseTimeout>00:02:00</SamplingPercentageDecreaseTimeout>`
  
    Lorsque les modifications de valeurs de pourcentage d’échantillonnage, combien de temps après sont nous autorisée toolower à nouveau l’échantillonnage pourcentage toocapture moins de données.
* `<SamplingPercentageIncreaseTimeout>00:15:00</SamplingPercentageIncreaseTimeout>`
  
    Lorsque les modifications de valeurs de pourcentage d’échantillonnage, combien de temps après sont nous autorisé tooincrease à nouveau l’échantillonnage pourcentage toocapture davantage de données.
* `<MinSamplingPercentage>0.1</MinSamplingPercentage>`
  
    Comme l’échantillonnage du pourcentage varie, ce qui est valeur minimale de hello nous sommes autorisés tooset.
* `<MaxSamplingPercentage>100.0</MaxSamplingPercentage>`
  
    Comme l’échantillonnage du pourcentage varie, ce qui est valeur maximale de hello nous sommes autorisés tooset.
* `<MovingAverageRatio>0.25</MovingAverageRatio>` 
  
    Dans le calcul hello Hello moyenne mobile, poids de hello affecté toohello valeur la plus récente. Utilisez un tooor égale de valeur inférieure à 1. Plus petites valeurs Modifier algorithme de hello moins réactifs toosudden.
* `<InitialSamplingPercentage>100</InitialSamplingPercentage>`
  
    valeur Hello affectée lors de l’application hello vient juste de démarrer. Ne diminuez pas cette valeur pendant le débogage. 

* `<ExcludedTypes>Trace;Exception</ExcludedTypes>`
  
    Un point-virgule liste délimitée par des types que vous ne voulez pas toobe échantillonnée. Les types reconnus sont : Dependency, Event, Exception, PageView, Request et Trace. Toutes les instances de hello spécifié de types sont transmis ; types Hello qui ne sont pas spécifiés sont échantillonnés.

* `<IncludedTypes>Request;Dependency</IncludedTypes>`
  
    Une liste délimitée par des points-virgules des types que vous souhaitez toobe échantillonnée. Les types reconnus sont : Dependency, Event, Exception, PageView, Request et Trace. Hello spécifié de types sont échantillonnés ; toutes les instances de hello autres types sont toujours transmis.


**tooswitch hors** échantillonnage adaptive, AdaptiveSamplingTelemetryProcessor hello supprimer un nœud à partir d’applicationinsights-config.

### <a name="alternative-configure-adaptive-sampling-in-code"></a>Solution alternative : configurer l’échantillonnage adaptatif dans le code
Au lieu d’échantillonnage dans le fichier .config de hello, vous pouvez utiliser le code. Cela vous permet de toospecify une fonction de rappel qui est appelée chaque fois que le taux d’échantillonnage de hello est réévaluée. Vous pouvez l’utiliser, par exemple, toofind les taux d’échantillonnage est utilisé.

Supprimer hello `AdaptiveSamplingTelemetryProcessor` nœud à partir du fichier .config de hello.

*C#*

```C#

    using Microsoft.ApplicationInsights;
    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.Channel.Implementation;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var adaptiveSamplingSettings = new SamplingPercentageEstimatorSettings();

    // Optional: here you can adjust hello settings from their defaults.

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;

    builder.UseAdaptiveSampling(
         adaptiveSamplingSettings,

        // Callback on rate re-evaluation:
        (double afterSamplingTelemetryItemRatePerSecond,
         double currentSamplingPercentage,
         double newSamplingPercentage,
         bool isSamplingPercentageChanged,
         SamplingPercentageEstimatorSettings s
        ) =>
        {
          if (isSamplingPercentageChanged)
          {
             // Report hello sampling rate.
             telemetryClient.TrackMetric("samplingPercentage", newSamplingPercentage);
          }
      });

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

([En savoir plus sur les processeurs de télémétrie](app-insights-api-filtering-sampling.md#filtering).)

<a name="other-web-pages"></a>

## <a name="sampling-for-web-pages-with-javascript"></a>Échantillonnage pour les pages web avec JavaScript
Vous pouvez configurer des pages Web pour l’échantillonnage à débit fixe à partir de n’importe quel serveur. 

Lorsque vous [configurer des pages web hello pour Application Insights](app-insights-javascript.md), modifier l’extrait de code hello que vous obtenez à partir du portail d’Application Insights hello. (Dans les applications ASP.NET, extrait de code hello passe généralement dans _Layout.cshtml.)  Insérer une ligne telle que `samplingPercentage: 10,` avant la clé d’instrumentation hello :

    <script>
    var appInsights= ... 
    }({ 


    // Value must be 100/N where N is an integer.
    // Valid examples: 50, 25, 20, 10, 5, 1, 0.1, ...
    samplingPercentage: 10, 

    instrumentationKey:...
    }); 

    window.appInsights=appInsights; 
    appInsights.trackPageView(); 
    </script> 

Pourcentage d’échantillonnage de hello, choisissez un pourcentage de fermer too100/N où N est un entier.  L’échantillonnage ne prend actuellement en charge aucune autre valeur.

Si vous activez également d’échantillonnage de taux fixe sur le serveur de hello, serveur et clients de hello synchronise donc, de recherche, vous pouvez naviguer entre les vues de page associée et des demandes.

## <a name="fixed-rate-sampling-for-aspnet-web-sites"></a>Échantillonnage à débit fixe pour les sites web ASP.NET
Taux fixe échantillonnage réduit le trafic de hello envoyé à partir de votre serveur web et les navigateurs web. À la différence de l’échantillonnage adaptatif, il réduit les données de télémétrie à un débit fixe choisi par vos soins. Il synchronise également les clients de hello et échantillonnage du serveur afin que les éléments associés sont conservés - par exemple, afin que si vous examinez un affichage de page dans la recherche, vous pouvez rechercher sa requête connexe.

algorithme d’échantillonnage de Hello conserve les éléments associés. Pour chaque événement de requête HTTP, celui-ci et ses événements associés sont ignorés ou transmis. 

Dans Metrics Explorer, taux telles que des nombres de demande et de l’exception sont multipliés par un toocompensate de facteur de taux d’échantillonnage de hello, afin qu’ils soient environ corrects.

1. **Mettre à jour les packages NuGet de votre projet** toohello dernière *préliminaires* version d’Application Insights. Cliquez sur projet hello dans l’Explorateur de solutions, cliquez sur Gérer les Packages NuGet, vérifiez **inclure la version préliminaire** et recherchez Microsoft.ApplicationInsights.Web. 
2. **Désactiver l’échantillonnage adaptive**: dans [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), supprimez ou commentez hello `AdaptiveSamplingTelemetryProcessor` nœud.
   
    ```xml
   
    <TelemetryProcessors>
   
    <!-- Disabled adaptive sampling:
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    -->

    ```

1. **Activer le module d’échantillonnage de taux fixe hello.** Ajoutez cet extrait de code trop[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):
   
    ```XML
   
    <TelemetryProcessors>
     <Add  Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
   
      <!-- Set a percentage close too100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
      <SamplingPercentage>10</SamplingPercentage>
      </Add>
    </TelemetryProcessors>
   
    ```

> [!NOTE]
> Pourcentage d’échantillonnage de hello, choisissez un pourcentage de fermer too100/N où N est un entier.  L’échantillonnage ne prend actuellement en charge aucune autre valeur.
> 
> 

### <a name="alternative-enable-fixed-rate-sampling-in-your-server-code"></a>Solution alternative : activez l’échantillonnage à taux fixe dans le code serveur
Au lieu de définir le paramètre d’échantillonnage hello dans le fichier .config de hello, vous pouvez utiliser le code. 

*C#*

```C#

    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var builder = TelemetryConfiguration.Active.GetTelemetryProcessorChainBuilder();
    builder.UseSampling(10.0); // percentage

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

([En savoir plus sur les processeurs de télémétrie](app-insights-api-filtering-sampling.md#filtering).)

## <a name="when-toouse-sampling"></a>Lors de l’échantillonnage toouse ?
Échantillonnage adaptative est activée automatiquement si vous utilisez hello ASP.NET SDK version 2.0.0-beta3 ou version ultérieure. Quelle que soit la version du Kit de développement logiciel (SDK) que vous utilisez, vous pouvez utiliser l’échantillonnage d’ingestion (sur notre serveur).

L’échantillonnage n’est pas utile pour la plupart des applications de taille petite à moyenne. les informations de diagnostic Hello plus utiles et des statistiques plus précises sont obtenus en collectant des données sur vos activités de l’utilisateur. 

principaux avantages de Hello d’échantillonnage sont :

* Si le service Application Insights supprime (« limite ») des points de données lorsque votre application envoie un taux de télémétrie très élevé dans un court laps de temps. 
* tookeep dans hello [quota](app-insights-pricing.md) de points de données pour votre niveau tarifaire. 
* tooreduce du trafic réseau à partir de la collection hello de télémétrie. 

### <a name="which-type-of-sampling-should-i-use"></a>Quel type d’échantillonnage dois-je utiliser ?
**Utiliser l’échantillonnage d’ingestion dans les situations suivantes :**

* Vous dépassez souvent votre quota mensuel de données de télémétrie.
* Vous utilisez une version de hello SDK qui ne prennent en charge d’échantillonnage - par exemple, hello Kit de développement logiciel Java ou les versions d’ASP.NET antérieures à 2.
* Vous obtenez un volume élevé de données de télémétrie des navigateurs web de vos utilisateurs.

**Utilisez l’échantillonnage à débit fixe si :**

* Vous utilisez hello Application Insights SDK pour la version de services web ASP.NET 2.0.0 ou version ultérieure, et
* Vous souhaitez un échantillonnage synchronisés entre client et serveur, afin que, lorsque vous recherchez des événements dans [recherche](app-insights-diagnostic-search.md), vous pouvez naviguer entre les événements connexes sur le client de hello et de serveur, telles que les vues de page et de requêtes http.
* Vous êtes certain de pourcentage d’échantillonnage approprié de hello pour votre application. Il doit être suffisamment élevée tooget des mesures précises, mais ci-dessous hello taux dépasse votre quota de tarification et hello limites. 

**Utilisez l’échantillonnage adaptatif :**

Dans le cas contraire, nous vous recommandons d’utiliser l’échantillonnage adaptatif. Cette option est activée par défaut sur un serveur d’ASP.NET hello SDK, version 2.0.0-beta3 ou version ultérieure. Comme il ne réduit pas le trafic jusqu’à un certain débit minimum, il n’affecte pas un site peu utilisé.

## <a name="how-do-i-know-whether-sampling-is-in-operation"></a>Comment savoir si l’échantillonnage est utilisé ?
hello toodiscover réel d’échantillonnage taux, quel que soit l’où il a été appliqué, utilisez un [les requête Analytique](app-insights-analytics.md) comme celui-ci :

    requests | where timestamp > ago(1d)
    | summarize 100/avg(itemCount) by bin(timestamp, 1h) 
    | render areachart 

Chaque enregistrement, conservé `itemCount` indique nombre hello d’origine enregistrements qu’elle représente, too1 égal + nombre de hello d’anciens enregistrements rejetés. 

## <a name="how-does-sampling-work"></a>Comment fonctionne l’échantillonnage ?
Taux fixe et échantillonnage adapté sont une fonctionnalité de hello SDK dans les versions ASP.NET à partir de 2.0.0 et versions ultérieures. Échantillonnage de réception est une fonctionnalité de hello service Application Insights et peut être dans l’opération si hello SDK n’effectue pas d’échantillonnage. 

algorithme d’échantillonnage de Hello décide quelle toodrop d’éléments de télémétrie et le tookeep celles (s’il s’agit dans le Kit de développement logiciel de hello ou dans le service Application Insights hello). la décision d’échantillonnage de Hello repose sur plusieurs règles visant toopreserve intact, en conservant une expérience de diagnostic dans Application Insights exploitables et fiable même avec un jeu de données réduit tous les points de données reliées entre elles. En cas d’échec d’une requête, par exemple, si votre application envoie d’autres éléments de télémétrie (tels que les exceptions et les traces enregistrées à partir de cette requête), l’échantillonnage ne fractionnera ni cette requête ni les autres éléments de télémétrie. Il les conservera ou supprimera ensemble. Par conséquent, lorsque vous examinez les détails de la demande hello dans Application Insights, vous voyez toujours demande hello, ainsi que ses éléments de télémétrie associée. 

Pour les applications qui définissent le « utilisateur » (autrement dit, les applications web les plus typiques), la décision d’échantillonnage de hello repose sur hachage hello de pseudo hello, ce qui signifie que toutes les données de télémétrie pour un utilisateur spécifique sont conservée ou supprimée. Pour les types d’applications que vous ne définissent pas les utilisateurs (tels que les services web) hello la décision d’échantillonnage de hello est basée sur l’id de l’opération de demande de hello hello. Enfin, pour les éléments de télémétrie hello qui n’ont des id utilisateur ni d’opération (pour les exemples d’éléments de télémétrie signalés par les threads asynchrones sans contexte http) échantillonnage capture simplement un pourcentage d’éléments de télémétrie de chaque type. 

Lors de la présentation tooyou arrière de télémétrie, hello Application Insights service ajuste les métriques de hello en hello même pourcentage d’échantillonnage qui a été utilisé au moment de hello de collection, toocompensate pourquoi les points de données manquants. Par conséquent, lorsque vous examinez la télémétrie hello dans Application Insights, hello infligés aux utilisateurs des approximations statistique correctes qui sont des nombres réels toohello très proche.

précision Hello de rapprochement de hello dépend en grande partie de pourcentage d’échantillonnage de hello configuré. En outre, une précision hello augmente pour les applications qui gèrent un grand nombre de demandes généralement semblables à partir d’un grand nombre d’utilisateurs. Sur hello autre part, pour les applications qui ne fonctionnent pas avec une charge importante, l’échantillonnage n’est pas nécessaire que ces applications peuvent envoyer généralement toutes leurs données de télémétrie tout en restant dans le quota de hello, sans entraîner de perte de données à partir de la limitation. 

Notez que Application Insights ne pas échantillonner des Sessions et les métriques des types de télémétrie, depuis pour ces types, la réduction de la précision de hello peut être souhaitable. 

### <a name="adaptive-sampling"></a>échantillonnage adaptatif
Échantillonnage Adaptive ajoute un composant cette vitesse de transmission pour les analyses hello actuelle hello SDK et ajuste hello d’échantillonnage pourcentage tootry toostay au sein de la vitesse maximale de hello cible. l’ajustement Hello est recalculé à intervalles réguliers et est basé sur une moyenne mobile de hello vitesse de transmission de sortie.

## <a name="sampling-and-hello-javascript-sdk"></a>Échantillonnage et hello SDK JavaScript
Hello côté client (JavaScript) SDK participe échantillonnage taux fixe en conjonction avec hello côté serveur SDK. pages de Hello instrumenté n’envoie les données de télémétrie côté client de hello aux mêmes utilisateurs pour le hello côté serveur fait son choix trop « sample dans. » Cette logique est intégrité toomaintain conçu d’une session utilisateur entre les côtés client et serveur. En partant de n’importe quel élément de télémétrie dans Application Insights, vous retrouverez donc tous les autres éléments de télémétrie associés à l’utilisateur ou à la session en question. 

*Mes données de télémétrie côté client et côté serveur n’affichent pas les échantillons coordonnés que vous décrivez ci-dessus.*

* Vérifiez que vous avez activé l’échantillonnage à débit fixe à la fois sur le serveur et sur le client.
* Assurez-vous que cette version du Kit de développement logiciel hello est 2.0 ou version ultérieure.
* Vérifiez que vous définissez hello même d’échantillonnage du pourcentage de hello client et le serveur.

## <a name="frequently-asked-questions"></a>Forum Aux Questions (FAQ)
*Pourquoi l’échantillonnage ne permet-il pas simplement de « collecter X % de chaque type de télémétrie » ?*

* Alors que cette approche d’échantillonnage peuvent fournir une très haute précision des approximations de métriques, il compromettrait capacité toocorrelate des données de diagnostic par l’utilisateur, de session et de demande, ce qui est essentiel pour les diagnostics. L’échantillonnage est donc plus efficace lorsqu’il revient à « collecter tous les éléments de télémétrie pour X % des utilisateurs de l’application » ou à « collecter tous les éléments de télémétrie pour X % des requêtes de l’application ». Pour les éléments de télémétrie hello ne pas associés aux demandes de hello (par exemple, le traitement asynchrone d’en arrière-plan) font partie de hello est trop « collecter X % de tous les éléments pour chaque type de données de télémétrie. » 

*Pourcentage d’échantillonnage hello permettre changer au fil du temps ?*

* Oui, l’échantillonnage adaptive progressivement modifie hello d’échantillonnage, basées sur des pourcentages sur hello actuellement observée volume de données de télémétrie hello.

*Si vous utilisez l’échantillonnage taux fixe, comment puis-je savoir quel échantillonnage pourcentage fonctionnera hello mieux à mon application ?*

* Une façon est toostart avec échantillonnage adaptive, découvrez ce que le taux règle sur (voir hello question ci-dessus), puis commutateur toofixed-taux d’échantillonnage à l’aide de ce taux. 
  
    Dans le cas contraire, vous avez tooguess. Analyser votre utilisation actuelle de la télémétrie dans AI, observez une limitation qui est en cours et estimation hello volume de télémétrie de hello collectée. Ces trois entrées, ainsi que le niveau tarifaire sélectionné, suggèrent combien vous pourriez volume de hello tooreduce de télémétrie de hello collectée. Toutefois, l’augmentation nombre hello de vos utilisateurs ou certaines autres MAJ volume hello de télémétrie peut invalider votre estimation.

*Que se passe-t-il si je configure le pourcentage d’échantillonnage à un niveau trop faible ?*

* Le pourcentage d’échantillonnage excessivement basse (échantillonnage over-aggressive) réduit la précision hello des approximations de hello, lors de l’Application Insights tente de visualisation de hello toocompensate de données hello hello données réduction de volume. En outre, expérience de diagnostic peut-être être réduite, car certaines de hello rarement échouent ou lente aux demandes peuvent être échantillonnés.

*Que se passe-t-il si je configure un pourcentage d’échantillonnage trop élevé ?*

* Configuration d’échantillonnage trop élevée pourcentage (pas agressif suffisamment) entraîne une réduction insuffisante dans le volume hello Hello collectées télémétrie. Vous pouvez rencontrer une perte de données liées toothrottling et hello le coût de l’utilisation d’Application Insights peuvent être plus élevée que prévu en raison des frais toooverage de télémétrie.

*Sur quelles plates-formes puis-je utiliser l’échantillonnage ?*

* Échantillonnage de réception peut se produire automatiquement pour toutes les données de télémétrie au-dessus d’un certain volume si hello SDK n’effectue pas d’échantillonnage. Cela fonctionne, par exemple, si votre application utilise un serveur Java, ou si vous utilisez une version antérieure de hello Kit de développement ASP.NET.
* Si vous utilisez des versions du Kit de développement ASP.NET 2.0.0 et versions ultérieures (hébergé dans Azure ou sur votre propre serveur), vous obtenez adaptative d’échantillonnage par défaut, mais vous pouvez basculer le taux de toofixed comme décrit ci-dessus. Avec un taux fixe échantillonnage, le navigateur hello SDK synchronise automatiquement toosample des événements connexes. 

*Il existe certains événements rares que je veux toujours toosee. Comment puis-je obtenir les au-delà de module d’échantillonnage de hello ?*

* Initialiser une instance distincte de TelemetryClient avec une nouveau TelemetryConfiguration (pas hello par défaut actif). Utilisez ce toosend vos événements rares.

## <a name="next-steps"></a>Étapes suivantes
* [filtrage](app-insights-api-filtering-sampling.md) peut fournir un contrôle plus strict de ce que le Kit de développement logiciel (SDK) envoie.

