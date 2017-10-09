---
title: "aaaFiltering et le prétraitement dans hello Azure Application Insights SDK | Documents Microsoft"
description: "Écrire des processeurs de télémétrie et les initialiseurs de télémétrie pour hello SDK toofilter ou ajouter des données de toohello de propriétés avant de télémétrie de hello est envoyé de portail d’Application Insights toohello."
services: application-insights
documentationcenter: 
author: beckylino
manager: carmonm
ms.assetid: 38a9e454-43d5-4dba-a0f0-bd7cd75fb97b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 11/23/2016
ms.author: bwren
ms.openlocfilehash: 51b9db69b2375b8799718f1b0e1af77620dc2692
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="filtering-and-preprocessing-telemetry-in-hello-application-insights-sdk"></a>Le filtrage et le prétraitement des données de télémétrie de hello Application Insights SDK


Vous pouvez écrire et configurer des plug-ins pour hello Application Insights SDK toocustomize la télémétrie est capturée et traitée avant d’être envoyée toohello service Application Insights.

* [Échantillonnage](app-insights-sampling.md) réduit le volume de hello de télémétrie sans affecter vos statistiques. Il maintient ensemble les points de données liés de sorte que vous pouvez naviguer entre eux pour diagnostiquer un problème. Dans le portail hello, nombre total de hello est multiplié toocompensate pour l’échantillonnage de hello.
* Le filtrage avec des processeurs de télémétrie [pour ASP.NET](#filtering) ou [Java](app-insights-java-filter-telemetry.md) vous permet de sélectionner ou de modifier la télémétrie Bonjour SDK avant d’être envoyée toohello server. Par exemple, vous pouvez réduire le volume de hello de télémétrie en excluant les demandes de robots. Mais le filtrage est un trafic de tooreducing approche plus simple que l’échantillonnage. Il vous permet de mieux contrôler ce qui est transmis, mais vous avez toobe savoir qu’il affecte vos statistiques - par exemple, si vous filtrez toutes les demandes réussies.
* [Ajouter des initialiseurs de télémétrie propriétés](#add-properties) télémétrie tooany envoyé à partir de votre application, y compris les données de télémétrie à partir des modules standards hello. Par exemple, vous pouvez ajouter des valeurs calculées ; ou les numéros de version par les données de hello toofilter dans le portail de hello.
* [Hello API du Kit de développement logiciel](app-insights-api-custom-events-metrics.md) est toosend utilisé des événements personnalisés et des mesures.

Avant de commencer :

* Installer l’Application hello Insights [SDK pour ASP.NET](app-insights-asp-net.md) ou [SDK pour Java](app-insights-java-get-started.md) dans votre application.

<a name="filtering"></a>

## <a name="filtering-itelemetryprocessor"></a>Filtrage : ITelemetryProcessor
Cette technique vous donne un contrôle plus direct sur ce qui est inclus ou exclu des flux de données de télémétrie hello. Vous pouvez l'utiliser conjointement avec l'échantillonnage, ou séparément.

toofilter télémétrie, vous écrivez un processeur de télémétrie et l’inscrivez auprès de hello Kit de développement logiciel. Toutes les données de télémétrie passe par le processeur, et vous pouvez choisir toodrop à partir de hello diffuser en continu, ou ajouter des propriétés. Cela inclut les données de télémétrie à partir des modules standards hello telles que le collecteur de demande HTTP hello et le collecteur de dépendance hello, ainsi que la télémétrie que vous avez écrit vous-même. Vous pouvez, par exemple, exclure la télémétrie concernant les demandes émanant de robots ou les appels de dépendance réussis.

> [!WARNING]
> Le filtrage de télémétrie hello envoyé à partir de hello SDK à l’aide de processeurs peut déformer les statistiques de hello hello portail et de rendre difficile toofollow concernant les éléments.
>
> Envisagez plutôt d'utiliser l' [échantillonnage](app-insights-sampling.md).
>
>

### <a name="create-a-telemetry-processor-c"></a>Créer un processeur de télémétrie (C#)
1. Vérifiez que hello Application Insights SDK dans votre projet est la version 2.0.0 ou version ultérieure. Cliquez avec le bouton droit sur votre projet dans l'explorateur de solutions Visual Studio, puis sélectionnez Gérer les packages NuGet. Dans le Gestionnaire de package NuGet, cochez Microsoft.ApplicationInsights.Web.
2. toocreate un filtre, implémenter ITelemetryProcessor. Il s’agit d’un autre point d’extensibilité, à l’instar d’un module de télémétrie, d’un initialiseur de télémétrie et d’un canal de télémétrie.

    Notez que les processeurs de télémétrie construisent une chaîne de traitement. Lorsque vous instanciez un processeur de télémétrie, vous passez un processeur suivant toohello de lien dans la chaîne de hello. Lorsqu’un point de données de télémétrie est passé procédé toohello, il effectue son travail, et puis appelle hello processeur télémétrie suivant dans la chaîne de hello.

    ``` C#

    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.Extensibility;

    public class SuccessfulDependencyFilter : ITelemetryProcessor
      {

        private ITelemetryProcessor Next { get; set; }

        // You can pass values from .config
        public string MyParamFromConfigFile { get; set; }

        // Link processors tooeach other in a chain.
        public SuccessfulDependencyFilter(ITelemetryProcessor next)
        {
            this.Next = next;
        }
        public void Process(ITelemetry item)
        {
            // toofilter out an item, just return
            if (!OKtoSend(item)) { return; }
            // Modify hello item if required
            ModifyItem(item);

            this.Next.Process(item);
        }

        // Example: replace with your own criteria.
        private bool OKtoSend (ITelemetry item)
        {
            var dependency = item as DependencyTelemetry;
            if (dependency == null) return true;

            return dependency.Success != true;
        }

        // Example: replace with your own modifiers.
        private void ModifyItem (ITelemetry item)
        {
            item.Context.Properties.Add("app-version", "1." + MyParamFromConfigFile);
        }
    }

    ```
1. Insérez-la dans ApplicationInsights.config :

```XML

    <TelemetryProcessors>
      <Add Type="WebApplication9.SuccessfulDependencyFilter, WebApplication9">
         <!-- Set public property -->
         <MyParamFromConfigFile>2-beta</MyParamFromConfigFile>
      </Add>
    </TelemetryProcessors>

```

(Il s’agit de hello section même où vous initialisez un filtre d’échantillonnage.)

Vous pouvez passer des valeurs de chaîne à partir du fichier .config de hello en fournissant des propriétés nommées publiques dans votre classe.

> [!WARNING]
> Nom de type hello toomatch et que les noms de propriété dans une classe de toohello du fichier .config hello et des noms de propriété dans le code hello prennent en charge. Si le fichier .config de hello fait référence à un type inexistant ou une propriété, hello SDK en mode silencieux ne toosend toutes les données de télémétrie.
>
>

**Vous pouvez également** vous pouvez initialiser filtre hello dans le code. Dans une classe de l’initialisation approprié - par exemple AppStart dans Global.asax.cs - insérer votre processeur dans la chaîne de hello :

```C#

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;
    builder.Use((next) => new SuccessfulDependencyFilter(next));

    // If you have more processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

Les clients de télémétrie créés après ce point utiliseront vos processeurs.

### <a name="example-filters"></a>Exemples de filtres
#### <a name="synthetic-requests"></a>Demandes synthétiques
Excluez les robots et les tests web. Bien que l’offre de Metrics Explorer vous hello toofilter option des sources synthétiques, cette option réduit le trafic en les filtrant à hello Kit de développement logiciel.

``` C#

    public void Process(ITelemetry item)
    {
      if (!string.IsNullOrEmpty(item.Context.Operation.SyntheticSource)) {return;}

      // Send everything else:
      this.Next.Process(item);
    }

```

#### <a name="failed-authentication"></a>Échec d’authentification
Excluez les demandes avec une réponse de type « 401 ».

```C#

public void Process(ITelemetry item)
{
    var request = item as RequestTelemetry;

    if (request != null &&
    request.ResponseCode.Equals("401", StringComparison.OrdinalIgnoreCase))
    {
        // toofilter out an item, just terminate hello chain:
        return;
    }
    // Send everything else:
    this.Next.Process(item);
}

```

#### <a name="filter-out-fast-remote-dependency-calls"></a>Excluez les appels de dépendance à distance rapides.
Si vous ne souhaitez que les appels de toodiagnose qui sont lentes, filtrer ceux d’accélérée hello.

> [!NOTE]
> Cela ne fausse pas les statistiques hello que vous voyez sur le portail de hello. graphique de dépendance Hello aura l’aspect des appels de dépendance hello sont tous les échecs.
>
>

``` C#

public void Process(ITelemetry item)
{
    var request = item as DependencyTelemetry;

    if (request != null && request.Duration.TotalMilliseconds < 100)
    {
        return;
    }
    this.Next.Process(item);
}

```

#### <a name="diagnose-dependency-issues"></a>Diagnostiquer les problèmes de dépendance
[Ce billet de blog](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) décrit un problèmes de dépendance de projet toodiagnose en envoyant des commandes ping régulière toodependencies automatiquement.


<a name="add-properties"></a>

## <a name="add-properties-itelemetryinitializer"></a>Ajouter des propriétés : ITelemetryInitializer
Utiliser des données de télémétrie initialiseurs toodefine propriétés globales qui sont envoyées avec toutes les données de télémétrie ; et le comportement de toooverride sélectionné des modules de télémétrie standard hello.

Par exemple, hello Application Insights pour le package Web collecte une télémétrie sur les requêtes HTTP. Il indique par défaut l’échec de toute requête à l’aide d’un code de réponse supérieur ou égal à 400. Mais si vous souhaitez tootreat 400 comme un succès, vous pouvez fournir un initialiseur de télémétrie qui définit la propriété de réussite hello.

Si vous fournissez un initialiseur de télémétrie, elle est appelée chaque fois qu’un des hello Track*() méthodes est appelée. Cela inclut les méthodes appelées par les modules de télémétrie standard hello. Par convention, ces modules ne définissent aucune propriété déjà définie par un initialiseur.

**Définir votre initialiseur**

*C#*

```C#

    using System;
    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.DataContracts;
    using Microsoft.ApplicationInsights.Extensibility;

    namespace MvcWebRole.Telemetry
    {
      /*
       * Custom TelemetryInitializer that overrides hello default SDK
       * behavior of treating response codes >= 400 as failed requests
       *
       */
      public class MyTelemetryInitializer : ITelemetryInitializer
      {
        public void Initialize(ITelemetry telemetry)
        {
            var requestTelemetry = telemetry as RequestTelemetry;
            // Is this a TrackRequest() ?
            if (requestTelemetry == null) return;
            int code;
            bool parsed = Int32.TryParse(requestTelemetry.ResponseCode, out code);
            if (!parsed) return;
            if (code >= 400 && code < 500)
            {
                // If we set hello Success property, hello SDK won't change it:
                requestTelemetry.Success = true;
                // Allow us toofilter these requests in hello portal:
                requestTelemetry.Context.Properties["Overridden400s"] = "true";
            }
            // else leave hello SDK tooset hello Success property      
        }
      }
    }
```

**Charger votre initialiseur**

Dans ApplicationInsights.config :

    <ApplicationInsights>
      <TelemetryInitializers>
        <!-- Fully qualified type name, assembly name: -->
        <Add Type="MvcWebRole.Telemetry.MyTelemetryInitializer, MvcWebRole"/>
        ...
      </TelemetryInitializers>
    </ApplicationInsights>

*Vous pouvez également* vous pouvez instancier initialiseur hello dans le code, par exemple dans Global.aspx.cs :

```C#
    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```


[Voir l’intégralité de cet exemple.](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/MvcWebRole)

<a name="js-initializer"></a>

### <a name="javascript-telemetry-initializers"></a>Initialiseurs de télémétrie JavaScript
*JavaScript*

Insérer un initialiseur de télémétrie immédiatement après le code d’initialisation hello que vous avez obtenu à partir du portail de hello :

```JS

    <script type="text/javascript">
        // ... initialization code
        ...({
            instrumentationKey: "your instrumentation key"
        });
        window.appInsights = appInsights;


        // Adding telemetry initializer.
        // This is called whenever a new telemetry item
        // is created.

        appInsights.queue.push(function () {
            appInsights.context.addTelemetryInitializer(function (envelope) {
                var telemetryItem = envelope.data.baseData;

                // toocheck hello telemetry item’s type - for example PageView:
                if (envelope.name == Microsoft.ApplicationInsights.Telemetry.PageView.envelopeType) {
                    // this statement removes url from all page view documents
                    telemetryItem.url = "URL CENSORED";
                }

                // tooset custom properties:
                telemetryItem.properties = telemetryItem.properties || {};
                telemetryItem.properties["globalProperty"] = "boo";

                // tooset custom metrics:
                telemetryItem.measurements = telemetryItem.measurements || {};
                telemetryItem.measurements["globalMetric"] = 100;
            });
        });

        // End of inserted code.

        appInsights.trackPageView();
    </script>
```

Pour obtenir un résumé des propriétés de non-custom hello disponibles sur hello telemetryItem, consultez [modèle exporter des données d’Application Insights](app-insights-export-data-model.md).

Vous pouvez ajouter autant d'initialiseurs que vous le souhaitez.

## <a name="itelemetryprocessor-and-itelemetryinitializer"></a>ITelemetryProcessor et ITelemetryInitializer
Qu’est la différence de hello entre les processeurs de télémétrie et les initialiseurs de télémétrie ?

* Il existe des chevauchements dans ce que vous pouvez faire avec eux : les deux peuvent être utilisés tooadd propriétés tootelemetry.
* Les TelemetryInitializers sont toujours exécutés avant les TelemetryProcessors.
* TelemetryProcessors permettent toocompletely remplacer ou ignorer un élément de données de télémétrie.
* Les TelemetryProcessors ne traitent pas la télémétrie du compteur de performances.


## <a name="reference-docs"></a>Documents de référence
* [Présentation de l’API](app-insights-api-custom-events-metrics.md)
* [Référence ASP.NET](https://msdn.microsoft.com/library/dn817570.aspx)

## <a name="sdk-code"></a>Code du Kit de développement logiciel (SDK)
* [Kit de développement logiciel (SDK) principal ASP.NET](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [ASP.NET 5](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [Kit de développement logiciel (SDK) JavaScript](https://github.com/Microsoft/ApplicationInsights-JS)

## <a name="next"></a>Étapes suivantes
* [Recherche d’événements et de journaux](app-insights-diagnostic-search.md)
* [Échantillonnage](app-insights-sampling.md)
* [Dépannage](app-insights-troubleshoot-faq.md)
