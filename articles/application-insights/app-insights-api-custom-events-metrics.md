---
title: "aaaApplication API d’aperçu pour les événements personnalisés et les métriques | Documents Microsoft"
description: "Insérer quelques lignes de code dans votre utilisation tootrack périphérique ou application de bureau, page Web ou service et diagnostiquer les problèmes."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 80400495-c67b-4468-a92e-abf49793a54d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/17/2017
ms.author: bwren
ms.openlocfilehash: f3d207a47bb4825efda806a19dd0c26540db7bdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-api-for-custom-events-and-metrics"></a>API Application Insights pour les événements et les mesures personnalisés

Insérer quelques lignes de code dans votre toofind d’application à ce que les utilisateurs sont en servent, ou toohelp diagnostiquer les problèmes. Vous pouvez envoyer la télémétrie depuis des applications de périphérique et de bureau, des clients web et des serveurs web. Hello d’utilisation [Azure Application Insights](app-insights-overview.md) vos propres versions de télémétrie standard et des métriques et des événements personnalisés de toosend API de télémétrie de base. Cette API est hello même API standard hello utilisent des collecteurs de données d’Application Insights.

## <a name="api-summary"></a>Résumé des API
Hello API est uniforme sur toutes les plateformes, indépendamment des quelques légères variantes.

| Méthode | Utilisé pour |
| --- | --- |
| [`TrackPageView`](#page-views) |Pages, écrans, panneaux ou formes. |
| [`TrackEvent`](#trackevent) |Actions de l’utilisateur et autres événements. Tootrack utilisé toomonitor comportement ou les performances de l’utilisateur. |
| [`TrackMetric`](#trackmetric) |Les mesures de performances telles que les files d’attente les événements de toospecific pas associés. |
| [`TrackException`](#trackexception) |Exceptions de journal pour des diagnostics. Suivi lorsqu’ils se produisent dans les événements de relation tooother et examinez les traces de pile. |
| [`TrackRequest`](#trackrequest) |Fréquence de hello et la durée des demandes de serveur pour l’analyse des performances de la journalisation. |
| [`TrackTrace`](#tracktrace) |Messages du journal de diagnostic Vous pouvez également capturer des journaux tiers. |
| [`TrackDependency`](#trackdependency) |Durée hello de journalisation et la fréquence des composants de tooexternal d’appels qui dépend de votre application. |

Vous pouvez [attacher des propriétés et des mesures](#properties) toomost de ces appels de télémétrie.

## <a name="prep"></a>Avant de commencer
Si vous n’avez pas encore de référence sur le kit SDK Application Insights :

* Ajouter hello Application Insights SDK tooyour projet :

  * [Projet ASP.NET](app-insights-asp-net.md)
  * [Projet Java](app-insights-java-get-started.md)
  * [JavaScript dans chaque page web](app-insights-javascript.md) 
* Ajoutez au code de votre périphérique ou de votre serveur web :

    *C# :*`using Microsoft.ApplicationInsights;`

    *Visual Basic :*`Imports Microsoft.ApplicationInsights`

    *Java:*`import com.microsoft.applicationinsights.TelemetryClient;`

## <a name="constructing-a-telemetryclient-instance"></a>Construction d’une instance de TelemetryClient
Construisez une instance de `TelemetryClient` (sauf en JavaScript dans les pages web) :

*C#*

    private TelemetryClient telemetry = new TelemetryClient();

*Visual Basic*

    Private Dim telemetry As New TelemetryClient

*Java*

    private TelemetryClient telemetry = new TelemetryClient();

TelemetryClient est thread-safe.

Nous vous recommandons d’utiliser une instance de TelemetryClient pour chaque module de votre application. Par exemple, vous avez peut-être une seule instance TelemetryClient dans vos requêtes HTTP entrantes tooreport web service et l’autre dans un intergiciel (middleware) classe tooreport business les événements de logique. Vous pouvez définir des propriétés telles que `TelemetryClient.Context.User.Id` tootrack utilisateurs et des sessions, ou `TelemetryClient.Context.Device.Id` machine de hello tooidentify. Ces informations sont les événements attachés tooall hello envoie d’instance.

## <a name="trackevent"></a>TrackEvent
Dans Application Insights, un *événement personnalisé* est un point de données que vous pouvez afficher dans [Metrics Explorer](app-insights-metrics-explorer.md) en tant que nombre agrégé et dans [Recherche de diagnostic](app-insights-diagnostic-search.md) en tant qu’occurrences individuelles. (Il n’est pas tooMVC connexe ou autres framework « événements ».)

Insérer `TrackEvent` appelle dans votre code toocount différents événements. Par exemple, la fréquence à laquelle les utilisateurs choisissent une fonctionnalité particulière, la fréquence à laquelle ils atteignent des objectifs particuliers ou à laquelle ils commettent éventuellement des types d’erreurs particuliers.

Par exemple, dans une application de jeu, vous devez envoyer un événement chaque fois qu’un utilisateur wins jeu de hello :

*JavaScript*

    appInsights.trackEvent("WinGame");

*C#*

    telemetry.TrackEvent("WinGame");

*Visual Basic*

    telemetry.TrackEvent("WinGame")

*Java*

    telemetry.trackEvent("WinGame");

### <a name="view-your-events-in-hello-microsoft-azure-portal"></a>Afficher les événements dans le portail de Microsoft Azure hello
toosee un nombre de vos événements, ouvrez un [Metrics Explorer](app-insights-metrics-explorer.md) panneau, ajouter un nouveau graphique, puis sélectionnez **événements**.  

![Afficher un nombre d’événements personnalisés](./media/app-insights-api-custom-events-metrics/01-custom.png)

nombres de hello toocompare d’événements, définir le type de graphique hello trop**grille**et de groupe par le nom de l’événement :

![Définir le type de graphique de hello et regroupement](./media/app-insights-api-custom-events-metrics/07-grid.png)

Sur la grille de hello, cliquez sur un événement nom toosee des occurrences individuelles de cet événement. toosee plus de détails - cliquez sur n’importe quelle occurrence dans la liste de hello.

![Extraire les événements hello](./media/app-insights-api-custom-events-metrics/03-instances.png)

toofocus sur des événements spécifiques dans la recherche ou Metrics Explorer, toohello événement les noms des filtres du panneau ensemble hello qui vous intéresse :

![Ouvrez Filtres, développez Nom de l'événement et sélectionnez une ou plusieurs valeurs](./media/app-insights-api-custom-events-metrics/06-filter.png)

### <a name="custom-events-in-analytics"></a>Événements personnalisés dans l’analytique

les données de télémétrie Hello est disponible dans hello `customEvents` table [Application Insights Analytique](app-insights-analytics.md). Chaque ligne représente un appel trop`trackEvent(..)` dans votre application. 

Si [échantillonnage](app-insights-sampling.md) est en opération, la propriété itemCount hello affiche une valeur supérieure à 1. Pour exemple itemCount == 10 signifie que de 10 appels tootrackEvent(), processus d’échantillonnage hello transmises uniquement un d’eux. tooget un nombre correct d’événements personnalisés, vous devez utiliser par conséquent utiliser du code comme `customEvent | summarize sum(itemCount)`.


## <a name="trackmetric"></a>TrackMetric

Application Insights peuvent graphique des métriques qui ne sont pas attachés tooparticular événements. Par exemple, vous pouvez analyser la longueur d’une file d'attente à des intervalles réguliers. Avec des mesures, des mesures individuelles hello sont moins importantes que les variations hello et les tendances et graphiques par conséquent, les statistiques sont utiles.

Dans commande toosend métriques tooApplication Insights, vous pouvez utiliser hello `TrackMetric(..)` API. Il existe deux façons toosend une mesure de : 

* Valeur unique. Chaque fois que vous effectuez une mesure dans votre application, vous envoyez valeur hello tooApplication Insights. Par exemple, supposons que vous disposez d’une mesure de nombre hello d’éléments dans un conteneur. Pendant une période donnée, vous commencez par mettre trois éléments dans le conteneur de hello, puis vous supprimez deux éléments. En conséquence, vous appelez `TrackMetric` à deux reprises : tout d’abord en passant la valeur de hello `3` et puis hello valeur `-2`. Application Insights stocke les deux valeurs pour votre compte. 

* Agrégation. Quand vous travaillez avec des métriques, chaque mesure individuelle est rarement intéressante. Au lieu de cela, un récapitulatif de ce qui s’est passé au cours d’une période donnée est important. Un tel récapitulatif est appelé _agrégation_. Bonjour exemple ci-dessus, hello métrique somme pour cette période est `1` et hello de valeurs de mesure hello est `2`. Lorsque vous utilisez l’approche d’agrégation hello, vous appelez uniquement `TrackMetric` une fois toutes les valeurs d’agrégation hello envoi et de période de temps. Il s’agit de hello approche recommandée étant donné qu’elle peut réduire considérablement le coût de hello et performances surcharge par envoi de données moins tooApplication Insights, lors de la collecte de toujours toutes les informations pertinentes.

### <a name="examples"></a>Exemples :

#### <a name="single-values"></a>Valeurs uniques

toosend une valeur métrique unique :

*JavaScript*

 ```Javascript
     appInsights.trackMetric("queueLength", 42.0);
 ```

*C#, Java*

```C#
    var sample = new MetricTelemetry();
    sample.Name = "metric name";
    sample.Value = 42.3;
    telemetryClient.TrackMetric(sample);
```

#### <a name="aggregating-metrics"></a>Agrégation des métriques

Il est recommandé de métriques de tooaggregate avant de les envoyer à partir de votre application, de la bande passante tooreduce, de coût et tooimprove les performances.
Voici un exemple de code d’agrégation :

*C#*

```C#
using System;
using System.Threading;
using System.Threading.Tasks;

using Microsoft.ApplicationInsights;
using Microsoft.ApplicationInsights.DataContracts;

namespace MetricAggregationExample
{
    /// <summary>
    /// Aggregates metric values for a single time period.
    /// </summary>
    internal class MetricAggregator
    {
        private SpinLock _trackLock = new SpinLock();

        public DateTimeOffset StartTimestamp    { get; }
        public int Count                        { get; private set; }
        public double Sum                       { get; private set; }
        public double SumOfSquares              { get; private set; }
        public double Min                       { get; private set; }
        public double Max                       { get; private set; }
        public double Average                   { get { return (Count == 0) ? 0 : (Sum / Count); } }
        public double Variance                  { get { return (Count == 0) ? 0 : (SumOfSquares / Count)
                                                                                  - (Average * Average); } }
        public double StandardDeviation         { get { return Math.Sqrt(Variance); } }

        public MetricAggregator(DateTimeOffset startTimestamp)
        {
            this.StartTimestamp = startTimestamp;
        }

        public void TrackValue(double value)
        {
            bool lockAcquired = false;

            try
            {
                _trackLock.Enter(ref lockAcquired);

                if ((Count == 0) || (value < Min))  { Min = value; }
                if ((Count == 0) || (value > Max))  { Max = value; }
                Count++;
                Sum += value;
                SumOfSquares += value * value;
            }
            finally
            {
                if (lockAcquired)
                {
                    _trackLock.Exit();
                }
            }
        }
    }   // internal class MetricAggregator

    /// <summary>
    /// Accepts metric values and sends hello aggregated values at 1-minute intervals.
    /// </summary>
    public sealed class Metric : IDisposable
    {
        private static readonly TimeSpan AggregationPeriod = TimeSpan.FromSeconds(60);

        private bool _isDisposed = false;
        private MetricAggregator _aggregator = null;
        private readonly TelemetryClient _telemetryClient;

        public string Name { get; }

        public Metric(string name, TelemetryClient telemetryClient)
        {
            this.Name = name ?? "null";
            this._aggregator = new MetricAggregator(DateTimeOffset.UtcNow);
            this._telemetryClient = telemetryClient ?? throw new ArgumentNullException(nameof(telemetryClient));

            Task.Run(this.AggregatorLoopAsync);
        }

        public void TrackValue(double value)
        {
            MetricAggregator currAggregator = _aggregator;
            if (currAggregator != null)
            {
                currAggregator.TrackValue(value);
            }
        }

        private async Task AggregatorLoopAsync()
        {
            while (_isDisposed == false)
            {
                try
                {
                    // Wait for end end of hello aggregation period:
                    await Task.Delay(AggregationPeriod).ConfigureAwait(continueOnCapturedContext: false);

                    // Atomically snap hello current aggregation:
                    MetricAggregator nextAggregator = new MetricAggregator(DateTimeOffset.UtcNow);
                    MetricAggregator prevAggregator = Interlocked.Exchange(ref _aggregator, nextAggregator);

                    // Only send anything is at least one value was measured:
                    if (prevAggregator != null && prevAggregator.Count > 0)
                    {
                        // Compute hello actual aggregation period length:
                        TimeSpan aggPeriod = nextAggregator.StartTimestamp - prevAggregator.StartTimestamp;
                        if (aggPeriod.TotalMilliseconds < 1)
                        {
                            aggPeriod = TimeSpan.FromMilliseconds(1);
                        }

                        // Construct hello metric telemetry item and send:
                        var aggregatedMetricTelemetry = new MetricTelemetry(
                                Name,
                                prevAggregator.Count,
                                prevAggregator.Sum,
                                prevAggregator.Min,
                                prevAggregator.Max,
                                prevAggregator.StandardDeviation);
                        aggregatedMetricTelemetry.Properties["AggregationPeriod"] = aggPeriod.ToString("c");

                        _telemetryClient.Track(aggregatedMetricTelemetry);
                    }
                }
                catch(Exception ex)
                {
                    // log ex as appropriate for your application
                }
            }
        }

        void IDisposable.Dispose()
        {
            _isDisposed = true;
            _aggregator = null;
        }
    }   // public sealed class Metric
}
```

### <a name="custom-metrics-in-metrics-explorer"></a>Métriques personnalisées dans Metrics Explorer

résultats de hello toosee, ouvrez l’Explorateur de métriques et ajouter un nouveau graphique. Modifier hello graphique tooshow votre mesure.

> [!NOTE]
> Votre métrique personnalisée peut prendre plusieurs minutes tooappear liste hello de métriques disponibles.
>

![Ajouter un nouveau graphique ou sélectionnez un graphique et sélectionnez votre métrique sous Personnalisé](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

### <a name="custom-metrics-in-analytics"></a>Métriques personnalisées dans Analytics

les données de télémétrie Hello est disponible dans hello `customMetrics` table [Application Insights Analytique](app-insights-analytics.md). Chaque ligne représente un appel trop`trackMetric(..)` dans votre application.
* `valueSum`-C’est la somme de hello des mesures de hello. valeur moyenne tooget hello, de division par `valueCount`.
* `valueCount`-hello du nombre de mesures qui ont été regroupés dans ce `trackMetric(..)` appeler.

## <a name="page-views"></a>Affichages de page
Dans un périphérique ou une application de page web, la télémétrie d'affichage de page est envoyée par défaut lorsque chaque écran ou page est chargé. Mais vous pouvez modifier les vues de cette page tootrack à des moments supplémentaires ou différents. Par exemple, dans une application qui affiche les onglets ou les panneaux, vous pourriez tootrack une page chaque fois que l’utilisateur de hello ouvre un nouveau panneau.

![Filtre d'utilisation dans le panneau Vue d'ensemble](./media/app-insights-api-custom-events-metrics/appinsights-47usage-2.png)

Les données utilisateur et la session sont envoyées comme propriétés ainsi que les vues de page, hello donc graphiques utilisateur et session vivantes lors de la télémétrie des consultations de page.

### <a name="custom-page-views"></a>Affichages de pages personnalisées
*JavaScript*

    appInsights.trackPageView("tab1");

*C#*

    telemetry.TrackPageView("GameReviewPage");

*Visual Basic*

    telemetry.TrackPageView("GameReviewPage")


Si vous avez plusieurs onglets dans différentes pages HTML, vous pouvez spécifier des URL de hello trop :

    appInsights.trackPageView("tab1", "http://fabrikam.com/page1.htm");

### <a name="timing-page-views"></a>Affichages de la page de durée
Par défaut, les temps de hello déclarés en tant que **temps de chargement de Page vue** sont mesurées à partir de lorsque le navigateur de hello envoie la demande de hello, jusqu'à ce que l’événement de chargement de page du navigateur hello est appelée.

Au lieu de cela, vous pouvez :

* Définir une durée explicite dans hello [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) appeler : `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.
* Utiliser les appels de minutage hello page vue `startTrackPage` et `stopTrackPage`.

*JavaScript*

    // toostart timing a page:
    appInsights.startTrackPage("Page1");

...

    // toostop timing and log hello page:
    appInsights.stopTrackPage("Page1", url, properties, measurements);

Hello nom que vous utilisez comme premier paramètre de hello associe le début de hello et arrêter des appels. Nom de la page actuelle toohello la valeur par défaut.

intervalle hello entre hello proviennent des durées affichées dans Metrics Explorer le chargement des pages qui en résulte Hello démarrer et arrêter des appels. C’est tooyou quel intervalle de temps réellement.

### <a name="page-telemetry-in-analytics"></a>Télémétrie des pages dans Analytique

Dans [Analytique](app-insights-analytics.md), deux tables affichent les données des opérations du navigateur :

* Hello `pageViews` table contient des données sur le titre de page et les URL de hello
* Hello `browserTimings` table contient des données sur les performances du client, telles que hello durée tooprocess hello les données entrantes

toofind combien de navigateur de hello prend tooprocess différentes pages :

```
browserTimings | summarize avg(networkDuration), avg(processingDuration), avg(totalDuration) by name 
```

toodiscover popularities de hello de différents navigateurs :

```
pageViews | summarize count() by client_Browser
```

appels de tooAJAX tooassociate page vues, joindre avec des dépendances :

```
pageViews | join (dependencies) on operation_Id 
```

## <a name="trackrequest"></a>TrackRequest
le serveur de Hello SDK utilise les requêtes HTTP TrackRequest toolog.

Vous pouvez également l’appeler vous-même si vous souhaitez que les demandes de toosimulate dans un contexte où vous n’avez pas hello web service module en cours.

Toutefois, hello recommandé est de télémétrie des requêtes de façon toosend où la demande de hello agit comme un <a href="#operation-context">contexte d’opération</a>.

## <a name="operation-context"></a>Contexte de l’opération
Vous pouvez associer des éléments de télémétrie ensemble en attachant toothem un ID d’opération courantes. module de suivi des demandes standard Hello effectue cette opération pour les exceptions et les autres événements qui sont envoyées pendant le traitement d’une requête HTTP. Dans [recherche](app-insights-diagnostic-search.md) et [Analytique](app-insights-analytics.md), vous pouvez utiliser hello ID tooeasily rechercher tous les événements associés à la demande de hello.

ID de Hello plus simple façon tooset hello est tooset un contexte d’opération à l’aide de ce modèle :

*C#*

```C#
// Establish an operation context and associated telemetry item:
using (var operation = telemetry.StartOperation<RequestTelemetry>("operationName"))
{
    // Telemetry sent in here will use hello same operation ID.
    ...
    telemetry.TrackTrace(...); // or other Track* calls
    ...
    // Set properties of containing telemetry item--for example:
    operation.Telemetry.ResponseCode = "200";

    // Optional: explicitly send telemetry item:
    telemetry.StopOperation(operation);

} // When operation is disposed, telemetry item is sent.
```

Outre la définition d’un contexte d’opération, `StartOperation` crée un élément de données de télémétrie de type hello que vous spécifiez. Il envoie des données de télémétrie hello élément lorsque vous supprimez l’opération de hello, ou si vous appelez explicitement `StopOperation`. Si vous utilisez `RequestTelemetry` comme type de données de télémétrie hello, sa durée est définie à intervalle toohello a dépassé le délai entre le début et de fin.

Les contextes de l’opération ne peuvent pas être imbriqués. Si un contexte d’opération existe déjà, son ID est associé à tous les éléments hello contenu, y compris les élément hello créé avec `StartOperation`.

Dans la recherche, contexte d’opération hello est utilisé toocreate hello **éléments connexes** liste :

![Éléments connexes](./media/app-insights-api-custom-events-metrics/21.png)

Pour plus d’informations sur le suivi des opérations personnalisées, consultez [application-insights-custom-operations-tracking.md].

### <a name="requests-in-analytics"></a>Requêtes dans Analytique 

Dans [Application Insights Analytique](app-insights-analytics.md), afficher les demandes des Bonjour `requests` table.

Si [échantillonnage](app-insights-sampling.md) est en opération, la propriété itemCount hello affichera une valeur supérieure à 1. Pour exemple itemCount == 10 signifie que de 10 appels tootrackRequest(), processus d’échantillonnage hello transmises uniquement un d’eux. tooget un nombre correct de demandes et la durée moyenne segmentés par des noms de la demande, utilisez un code tel que :

```AIQL
requests | summarize count = sum(itemCount), avgduration = avg(duration) by name
```


## <a name="trackexception"></a>TrackException
Envoyer les exceptions tooApplication Insights :

* trop[les compter](app-insights-metrics-explorer.md), comme une indication de la fréquence de hello d’un problème.
* trop[examiner des occurrences individuelles](app-insights-diagnostic-search.md).

les rapports de Hello incluent les traces de pile hello.

*C#*

    try
    {
        ...
    }
    catch (Exception ex)
    {
       telemetry.TrackException(ex);
    }

*JavaScript*

    try
    {
       ...
    }
    catch (ex)
    {
       appInsights.trackException(ex);
    }

Kits de développement logiciel Hello interceptent de nombreuses exceptions automatiquement, donc vous n’avez toujours pas toocall TrackException explicitement.

* ASP.NET : [écrire du code toocatch exceptions](app-insights-asp-net-exceptions.md).
* J2EE : [les exceptions sont interceptées automatiquement](app-insights-java-get-started.md#exceptions-and-request-failures).
* JavaScript : les exceptions sont interceptées automatiquement. Si vous souhaitez collecte automatique des toodisable, ajoutez un extrait de code toohello ligne que vous insérez dans vos pages Web :

    ```
    ({
      instrumentationKey: "your key"
      , disableExceptionTracking: true
    })
    ```

### <a name="exceptions-in-analytics"></a>Exceptions dans Analytique

Dans [Application Insights Analytique](app-insights-analytics.md), exceptions s’afficheront dans hello `exceptions` table.

Si [échantillonnage](app-insights-sampling.md) est en opération, hello `itemCount` propriété indique une valeur supérieure à 1. Pour exemple itemCount == 10 signifie que de 10 appels tootrackException(), processus d’échantillonnage hello transmises uniquement un d’eux. tooget un nombre correct d’exceptions segmentées par type d’exception, utilisez un code tel que :

```
exceptions | summarize sum(itemCount) by type
```

La plupart des hello en important les informations de pile sont déjà extrait dans des variables distinctes, mais vous pouvez extraire hello éloigné `details` tooget structure plus. Étant donné que cette structure est dynamique, vous devez effectuer un cast de type de toohello hello résultat escompté. Par exemple :

```AIQL
exceptions
| extend method2 = tostring(details[0].parsedStack[1].method)
```

exceptions tooassociate avec leurs demandes associées, utilisez une jointure :

```
exceptions
| join (requests) on operation_Id 
```

## <a name="tracktrace"></a>TrackTrace
Utilisez TrackTrace toohelp diagnostiquer les problèmes en envoyant une tooApplication « cheminement de navigation » Insights. Vous pouvez envoyer des blocs de données de diagnostic et les examiner dans la [Recherche de diagnostic](app-insights-diagnostic-search.md).

[Connecter des adaptateurs](app-insights-asp-net-trace-logs.md) utiliser ce portail de toohello API toosend les journaux tierce.

*C#*

    telemetry.TrackTrace(message, SeverityLevel.Warning, properties);


Vous pouvez effectuer une recherche dans le contenu du message, mais (contrairement aux valeurs de propriété), vous ne pouvez pas les filtrer.

limite de taille Hello sur `message` est plus importante que la limite de hello sur les propriétés.
L’avantage de TrackTrace est que vous pouvez placer des données relativement longues dans le message de type hello. Par exemple, vous pourriez y encoder des données POST.  

En outre, vous pouvez ajouter un message tooyour au niveau de gravité. Et, comme les autres données de télémétrie, vous pouvez ajouter toohelp de valeurs de propriété que vous filtrez ou de recherche pour différents ensembles de traces. Par exemple :

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

Dans [recherche](app-insights-diagnostic-search.md), vous pouvez ensuite facilement filtrer tous les messages hello d’un niveau de gravité spécifique qui se rapportent tooa la base de données particulière.


### <a name="traces-in-analytics"></a>Traces dans Analytique

Dans [Application Insights Analytique](app-insights-analytics.md), appelle tooTrackTrace afficher Bonjour `traces` table.

Si [échantillonnage](app-insights-sampling.md) est en opération, la propriété itemCount hello affiche une valeur supérieure à 1. Pour exemple itemCount == 10 signifie que 10 appelle trop`trackTrace()`, processus d’échantillonnage hello transmis uniquement un d’eux. tooget un nombre approprié de suivi des appels, vous devez utiliser par conséquent code tel que `traces | summarize sum(itemCount)`.

## <a name="trackdependency"></a>TrackDependency
Hello d’utilisation TrackDependency appeler le temps de réponse tootrack hello et taux de réussite de la partie externe de tooan appelle du code. résultats de Hello s’affichent dans les graphiques de dépendance hello dans le portail de hello.

```C#
var success = false;
var startTime = DateTime.UtcNow;
var timer = System.Diagnostics.Stopwatch.StartNew();
try
{
    success = dependency.Call();
}
finally
{
    timer.Stop();
    telemetry.TrackDependency("myDependency", "myCall", startTime, timer.Elapsed, success);
}
```

N’oubliez pas de ce serveur hello kits de développement incluent un [module de dépendance](app-insights-asp-net-dependencies.md) qui détecte et effectue le suivi de certains appels de dépendance automatiquement--par exemple, toodatabases et API REST. Vous avez tooinstall un agent sur le module de hello toomake serveur fonctionne. Vous utilisez cet appel si vous voulez n’intercepte pas les appels tootrack hello suivi automatique, ou si vous ne souhaitez pas l’agent de tooinstall hello.

tooturn off hello standard dépendance-module de suivi, modifier [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) et supprimer la référence de hello trop`DependencyCollector.DependencyTrackingTelemetryModule`.

### <a name="dependencies-in-analytics"></a>Dépendances dans Analytique

Dans [Application Insights Analytique](app-insights-analytics.md), trackDependency appels apparaissent dans hello `dependencies` table.

Si [échantillonnage](app-insights-sampling.md) est en opération, la propriété itemCount hello affiche une valeur supérieure à 1. Pour exemple itemCount == 10 signifie que de 10 appels tootrackDependency(), processus d’échantillonnage hello transmises uniquement un d’eux. tooget un nombre correct de dépendances segmentées par le composant cible, utilisez un code tel que :

```
dependencies | summarize sum(itemCount) by target
```

dépendances de tooassociate avec leurs requêtes connexes, utilisez une jointure :

```
dependencies
| join (requests) on operation_Id 
```

## <a name="flushing-data"></a>Vidage des données
Normalement, hello Kit de développement logiciel envoie des données à des moments choisies un impact hello toominimize sur utilisateur de hello. Toutefois, dans certains cas, vous pourriez tooflush mémoire tampon de hello--par exemple, si vous utilisez hello SDK dans une application s’arrête.

*C#*

    telemetry.Flush();

    // Allow some time for flushing before shutdown.
    System.Threading.Thread.Sleep(1000);

Notez que la fonction hello est asynchrone pour hello [canal de télémétrie serveur](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).

## <a name="authenticated-users"></a>Utilisateurs authentifiés
Dans une application web, les utilisateurs sont identifiés par des cookies par défaut. Un utilisateur peut être compté plusieurs fois s’il accède à votre application à partir d’un autre ordinateur ou navigateur, ou s’il supprime des cookies.

Si les utilisateurs se connectent tooyour application, vous pouvez obtenir un nombre plus précis en définissant des ID d’utilisateur hello authentifié dans le code hello navigateur :

*JavaScript*

```JS
// Called when my app has identified hello user.
function Authenticated(signInId) {
    var validatedId = signInId.replace(/[,;=| ]+/g, "_");
    appInsights.setAuthenticatedUserContext(validatedId);
    ...
}
```

Dans une application MVC Web ASP.NET, par exemple :

*Razor*

        @if (Request.IsAuthenticated)
        {
            <script>
                appInsights.setAuthenticatedUserContext("@User.Identity.Name
                   .Replace("\\", "\\\\")"
                   .replace(/[,;=| ]+/g, "_"));
            </script>
        }

Il n’est pas le nom de connexion réel de l’utilisateur nécessaire toouse hello. Il ne possède que toobe un ID unique toothat utilisateur. Il ne doit pas inclure des espaces ou les caractères de hello `,;=|`.

ID d’utilisateur Hello est également défini dans un cookie de session et envoyé toohello serveur. Si le serveur hello SDK est installé, hello les ID est envoyé en tant que partie des propriétés de contexte hello de télémétrie de client et le serveur de l’utilisateur authentifié. Vous pouvez ensuite filtrer et rechercher dessus.

Si votre application regroupe les utilisateurs dans des comptes, vous pouvez également passer un identificateur pour le compte de hello (hello avec les mêmes restrictions de caractères).

      appInsights.setAuthenticatedUserContext(validatedId, accountId);

Dans [Metrics Explorer](app-insights-metrics-explorer.md), vous pouvez créer un graphique qui compte les **Utilisateurs authentifiés** et les **Comptes d’utilisateur**.

Vous pouvez également [rechercher](app-insights-diagnostic-search.md) les points de données client avec des comptes et des noms d'utilisateur spécifiques.

## <a name="properties"></a>Filtrage, recherche et segmentation de vos données à l’aide des propriétés
Vous pouvez joindre des propriétés et des mesures tooyour événements (et également toometrics, vues de page, des exceptions et autres données de télémétrie).

*Propriétés* sont des valeurs de chaîne que vous pouvez utiliser toofilter votre télémétrie dans les rapports d’utilisation hello. Par exemple, si votre application fournit plusieurs jeux, vous pouvez attacher nom hello d’événement de jeu tooeach hello afin que vous pouvez voir les jeux sont plus populaires.

Il existe une limite de 8 192 sur la longueur de la chaîne hello. (Si vous souhaitez toosend de grandes quantités de données, utilisez le paramètre de message hello de [TrackTrace](#track-trace).)

*mesures* sont des valeurs numériques qui peuvent être représentées sous forme graphique. Par exemple, vous pourriez toosee s’il existe une augmentation progressive de scores de hello votre joueurs atteindre. graphiques de Hello peuvent être segmentées par hello séparer les propriétés qui sont envoyées avec les événements de hello, qui vous pouvez d’obtenir ou empilées graphiques pour jeux différents.

Pour toobe de valeurs de mesure affiché correctement, ils doivent être too0 égal ou supérieur.

Il existe quelques [limites nombre hello de propriétés, les valeurs de propriété et les métriques](#limits) que vous pouvez utiliser.

*JavaScript*

    appInsights.trackEvent
      ("WinGame",
         // String properties:
         {Game: currentGame.name, Difficulty: currentGame.difficulty},
         // Numeric metrics:
         {Score: currentGame.score, Opponents: currentGame.opponentCount}
         );

    appInsights.trackPageView
        ("page name", "http://fabrikam.com/pageurl.html",
          // String properties:
         {Game: currentGame.name, Difficulty: currentGame.difficulty},
         // Numeric metrics:
         {Score: currentGame.score, Opponents: currentGame.opponentCount}
         );


*C#*

    // Set up some properties and metrics:
    var properties = new Dictionary <string, string>
       {{"game", currentGame.Name}, {"difficulty", currentGame.Difficulty}};
    var metrics = new Dictionary <string, double>
       {{"Score", currentGame.Score}, {"Opponents", currentGame.OpponentCount}};

    // Send hello event:
    telemetry.TrackEvent("WinGame", properties, metrics);


*Visual Basic*

    ' Set up some properties:
    Dim properties = New Dictionary (Of String, String)
    properties.Add("game", currentGame.Name)
    properties.Add("difficulty", currentGame.Difficulty)

    Dim metrics = New Dictionary (Of String, Double)
    metrics.Add("Score", currentGame.Score)
    metrics.Add("Opponents", currentGame.OpponentCount)

    ' Send hello event:
    telemetry.TrackEvent("WinGame", properties, metrics)


*Java*

    Map<String, String> properties = new HashMap<String, String>();
    properties.put("game", currentGame.getName());
    properties.put("difficulty", currentGame.getDifficulty());

    Map<String, Double> metrics = new HashMap<String, Double>();
    metrics.put("Score", currentGame.getScore());
    metrics.put("Opponents", currentGame.getOpponentCount());

    telemetry.trackEvent("WinGame", properties, metrics);


> [!NOTE]
> Prenez soin toolog pas les informations personnelles dans les propriétés.
>
>

*Si vous avez utilisé des métriques*, ouvrez Metrics Explorer et sélectionnez des mesures de hello de hello **personnalisé** groupe :

![Ouvrez l’Explorateur de métriques, graphique de hello select et sélectionnez hello métrique](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

> [!NOTE]
> Si votre métrique n’apparaît pas, ou si hello **personnalisé** en-tête n’est pas présent, panneau de sélection de fermer hello et réessayez ultérieurement. Métriques peuvent parfois prendre une heure toobe agrégées via le pipeline de hello.

*Si vous avez utilisé des propriétés et des mesures*, segment métrique de hello par la propriété de hello :

![Définir le regroupement, puis sélectionnez la propriété hello sous Group by](./media/app-insights-api-custom-events-metrics/04-segment-metric-event.png)

*Dans la recherche de Diagnostic*, vous pouvez afficher les propriétés de hello et les métriques des occurrences individuelles d’un événement.

![Sélectionnez une instance, puis sélectionnez « ... »](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-4.png)

Hello d’utilisation **recherche** champ toosee des occurrences d’événements qui ont une valeur de propriété particulière.

![Tapez un terme dans Rechercher](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-5.png)

[En savoir plus sur les expressions de recherche](app-insights-diagnostic-search.md).

### <a name="alternative-way-tooset-properties-and-metrics"></a>Mesures et les propriétés de tooset autre moyen
S’il est plus pratique, vous pouvez collecter les paramètres d’un événement dans un objet séparé hello :

    var event = new EventTelemetry();

    event.Name = "WinGame";
    event.Metrics["processingTime"] = stopwatch.Elapsed.TotalMilliseconds;
    event.Properties["game"] = currentGame.Name;
    event.Properties["difficulty"] = currentGame.Difficulty;
    event.Metrics["Score"] = currentGame.Score;
    event.Metrics["Opponents"] = currentGame.Opponents.Length;

    telemetry.TrackEvent(event);

> [!WARNING]
> Ne réutilisez pas hello même instance d’élément de données de télémétrie (`event` dans cet exemple) toocall Track*() plusieurs fois. Cela peut entraîner des toobe de télémétrie envoyé avec une configuration incorrecte.
>
>

### <a name="custom-measurements-and-properties-in-analytics"></a>Mesures et propriétés personnalisées dans Analytique

Dans [Analytique](app-insights-analytics.md), affichent les mesures personnalisées et les propriétés Bonjour `customMeasurements` et `customDimensions` les attributs de chaque enregistrement de données de télémétrie.

Par exemple, si vous avez ajouté une propriété nommée « jeu » tooyour télémétrie des requêtes, cette requête compte les occurrences de hello de différentes valeurs de « jeu » et afficher moyenne hello Hello métrique personnalisé « score » :

```
requests
| summarize sum(itemCount), avg(todouble(customMeasurements.score)) by tostring(customDimensions.game) 
```

Notez que :

* Lorsque vous extrayez une valeur de hello customDimensions ou customMeasurements JSON, il a le type dynamique, et par conséquent, vous devez effectuer un cast `tostring` ou `todouble`.
* compte tootake de possibilité de hello de [échantillonnage](app-insights-sampling.md), vous devez utiliser `sum(itemCount)`, et non `count()`.



## <a name="timed"></a> Événements de durée
Vous pouvez souhaiter que toochart la durée pendant laquelle il effectue tooperform une action. Par exemple, vous pourriez tooknow la durée pendant laquelle les utilisateurs prennent tooconsider choix dans un jeu. Vous pouvez utiliser le paramètre de mesure hello pour cela.

*C#*

    var stopwatch = System.Diagnostics.Stopwatch.StartNew();

    // ... perform hello timed action ...

    stopwatch.Stop();

    var metrics = new Dictionary <string, double>
       {{"processingTime", stopwatch.Elapsed.TotalMilliseconds}};

    // Set up some properties:
    var properties = new Dictionary <string, string>
       {{"signalSource", currentSignalSource.Name}};

    // Send hello event:
    telemetry.TrackEvent("SignalProcessed", properties, metrics);



## <a name="defaults"></a>Propriétés par défaut pour la télémétrie personnalisée
Si vous souhaitez que les valeurs de propriété par défaut tooset pour certaines des événements personnalisés hello que vous écrivez, vous pouvez les définir dans une instance de TelemetryClient. Ils sont des éléments de télémétrie tooevery jointe qui sont envoyé à partir de ce client.

*C#*

    using Microsoft.ApplicationInsights.DataContracts;

    var gameTelemetry = new TelemetryClient();
    gameTelemetry.Context.Properties["Game"] = currentGame.Name;
    // Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame");

*Visual Basic*

    Dim gameTelemetry = New TelemetryClient()
    gameTelemetry.Context.Properties("Game") = currentGame.Name
    ' Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame")

*Java*

    import com.microsoft.applicationinsights.TelemetryClient;
    import com.microsoft.applicationinsights.TelemetryContext;
    ...


    TelemetryClient gameTelemetry = new TelemetryClient();
    TelemetryContext context = gameTelemetry.getContext();
    context.getProperties().put("Game", currentGame.Name);

    gameTelemetry.TrackEvent("WinGame");



Appels de télémétrie individuels peuvent remplacer des valeurs de par défaut de hello dans les dictionnaires de leurs propriétés.

*Pour les clients Web JavaScript*, [utilisez des initialiseurs de télémétrie JavaScript](#js-initializer).

*données de télémétrie tooadd propriétés tooall*, y compris les données hello à partir des modules de collection standard, [implémenter `ITelemetryInitializer` ](app-insights-api-filtering-sampling.md#add-properties).

## <a name="sampling-filtering-and-processing-telemetry"></a>Échantillonnage, filtrage et traitement de la télémétrie
Vous pouvez écrire tooprocess de code de votre télémétrie avant d’être envoyée à partir de hello SDK. le traitement de Hello comprend des données envoyées à partir de modules de télémétrie standard hello, telles que la collection de requêtes HTTP et de la collection de dépendances.

[Ajouter des propriétés](app-insights-api-filtering-sampling.md#add-properties) tootelemetry en implémentant `ITelemetryInitializer`. Par exemple, vous pouvez ajouter des numéros de version ou des valeurs calculées à partir d'autres propriétés.

[Le filtrage](app-insights-api-filtering-sampling.md#filtering) peut modifier ou ignorer les données de télémétrie avant d’être envoyée à partir de hello SDK en implémentant `ITelemetryProcesor`. Vous contrôlez ce qui est envoyé ou rejeté, mais vous avez tooaccount pour effet de hello sur vos mesures. En fonction de la façon dont vous ignorez les éléments, vous risquez de perdre toonavigate de capacité hello entre des éléments connexes.

[Échantillonnage](app-insights-api-filtering-sampling.md) est un volume de hello tooreduce offre groupée de données qui sont envoyés à partir de votre portail toohello d’application. Il le fait sans affecter les métriques hello affiché. Et il le fait sans affecter vos problèmes de toodiagnose de capacité en naviguant entre les éléments connexes tels que les exceptions, les demandes et les vues de page.

[En savoir plus](app-insights-api-filtering-sampling.md).

## <a name="disabling-telemetry"></a>Désactivation de la télémétrie
trop*dynamiquement arrêter et démarrer* hello collecte et transmission des données de télémétrie :

*C#*

```C#

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```

trop*désactiver les collecteurs standards sélectionnés*--par exemple, les compteurs de performance, les requêtes HTTP ou dépendances--supprimer ou commenter les lignes concernées hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Vous pouvez cela, par exemple, si vous souhaitez toosend vos propres données TrackRequest.

## <a name="debug"></a>Mode Développeur :
Pendant le débogage, il est utile toohave votre télémétrie expédié via le pipeline de hello afin que vous pouvez voir immédiatement les résultats. Vous get également des messages supplémentaires qui vous permettent de suivi des problèmes avec les données de télémétrie hello. Désactivez-les lors de la production, car ils peuvent ralentir votre application.

*C#*

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = true;

*Visual Basic*

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = True


## <a name="ikey"></a>Définition de clé d’instrumentation de hello pour une télémétrie personnalisée sélectionnée
*C#*

    var telemetry = new TelemetryClient();
    telemetry.InstrumentationKey = "---my key---";
    // ...


## <a name="dynamic-ikey"></a> Clé d'instrumentation dynamique
tooavoid mélange de télémétrie de développement, de test et environnements de production, vous pouvez [créer des ressources Application Insights distinctes](app-insights-create-new-resource.md) et modifier leurs clés, en fonction de l’environnement de hello.

Au lieu d’obtenir la clé d’instrumentation hello hello fichier de configuration, vous pouvez la définir dans votre code. Clé d’ensemble hello dans une méthode d’initialisation, par exemple global.aspx.cs dans un service ASP.NET :

*C#*

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      ...

*JavaScript*

    appInsights.config.instrumentationKey = myKey;



Dans les pages Web, vous pourriez tooset à partir du serveur hello web état, plutôt que par codage il littéralement dans le script de hello. Par exemple, dans une page web générée dans une application ASP.NET :

*JavaScript dans Razor*

    <script type="text/javascript">
    // Standard Application Insights webpage script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      @Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="telemetrycontext"></a>TelemetryContext
TelemetryClient a une propriété de contexte contenant les valeurs qui sont envoyées avec toutes les données de télémétrie. Ils sont normalement définies par les modules de télémétrie standard hello, mais vous pouvez également les définir vous-même. Par exemple :

    telemetry.Context.Operation.Name = "MyOperationName";

Si vous définissez une de ces valeurs vous-même, envisagez de supprimer la ligne hello pertinentes [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), de sorte que vos valeurs et hello standard ne pas dérouter.

* **Composant**: hello application et sa version.
* **APPAREIL**: les données sur l’appareil hello où l’application hello est en cours d’exécution. (Dans les applications web, voici hello serveur ou dispositif envoyées par les données de télémétrie hello.)
* **InstrumentationKey**: hello ressource Application Insights dans Azure où apparaissent les données de télémétrie hello. Elle est généralement récupérée dans ApplicationInsights.config.
* **Emplacement**: hello emplacement géographique de hello appareil.
* **Opération**: dans les applications web, hello la requête HTTP actuelle. Dans d’autres types d’application, vous pouvez définir cette événements toogroup ensemble.
  * **ID**: une valeur générée qui met en relation différents événements de manière à ce que vous trouviez les « Éléments associés » lorsque vous inspectez un événement dans la Recherche de diagnostic.
  * **Nom**: un identificateur, généralement hello URL de demande de hello HTTP.
  * **SyntheticSource**: si non null ou vide, une chaîne indiquant que cette source de hello de demande de hello a été identifiée comme un test web ou le robot. Par défaut, elle est exclue des calculs dans Metrics Explorer.
* **Propriétés** : ce sont les propriétés qui sont envoyées avec toutes les données de télémétrie. Elles peuvent être remplacées dans les appels Track* individuels.
* **Session**: hello session utilisateur. Hello ID a la valeur tooa généré, ce qui est modifiée lorsque l’utilisateur de hello n’a pas été active pendant un certain temps.
* **Utilisateur** : Informations utilisateur.

## <a name="limits"></a>limites
[!INCLUDE [application-insights-limits](../../includes/application-insights-limits.md)]

tooavoid atteint la limite de débit hello, utilisez [échantillonnage](app-insights-sampling.md).

toodetermine comment les données de type long sont conservées, consultez [rétention des données et confidentialité](app-insights-data-retention-privacy.md).

## <a name="reference-docs"></a>Documents de référence
* [Référence ASP.NET](https://msdn.microsoft.com/library/dn817570.aspx)
* [Référence Java](http://dl.windowsazure.com/applicationinsights/javadoc/)
* [Référence JavaScript](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md)
* [Kit de développement logiciel Android](https://github.com/Microsoft/ApplicationInsights-Android)
* [Kit de développement logiciel (SDK) iOS](https://github.com/Microsoft/ApplicationInsights-iOS)

## <a name="sdk-code"></a>Code de Kit de développement logiciel (SDK)
* [Kit de développement logiciel (SDK) principal ASP.NET](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [ASP.NET 5](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [Packages Windows Server](https://github.com/Microsoft/applicationInsights-dotnet-server)
* [Kit SDK Java](https://github.com/Microsoft/ApplicationInsights-Java)
* [Kit de développement logiciel (SDK) JavaScript](https://github.com/Microsoft/ApplicationInsights-JS)
* [Toutes les plateformes](https://github.com/Microsoft?utf8=%E2%9C%93&query=applicationInsights)

## <a name="questions"></a>Questions
* *Quelles exceptions peuvent être lancées par les appels Track_() ?*

    Aucune. Vous n’avez pas besoin de toowrap dans les clauses try-catch. Si le Kit de développement logiciel de hello rencontre des problèmes, il enregistrera les messages dans la sortie de console de débogage hello et--si hello messages obtenir via--dans la recherche de Diagnostic.
* *Existe-t-il un tooget de données API REST à partir du portail de hello ?*

    Oui, hello [API d’accès aux données](https://dev.applicationinsights.io/). Incluent d’autres données tooextract [exporter à partir de l’Analytique tooPower BI](app-insights-export-power-bi.md) et [exportation continue](app-insights-export-telemetry.md).

## <a name="next"></a>Étapes suivantes
* [Recherche d’événements et de journaux](app-insights-diagnostic-search.md)

* [Dépannage](app-insights-troubleshoot-faq.md)


