---
title: "Filtrer les données de télémétrie d’Azure Application Insights dans votre application web Java | Microsoft Docs"
description: "Réduisez le trafic de télémétrie en excluant les événements que vous n’avez pas besoin de surveiller."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: bwren
ms.openlocfilehash: 5f6d6d4ad590b85810c42e9f9520850024c5446a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="filter-telemetry-in-your-java-web-app"></a>Filtrer la télémétrie dans votre application web Java

Les filtres offrent un moyen de sélectionner les données de télémétrie que votre [application web Java envoie à Application Insights](app-insights-java-get-started.md). Vous pouvez utiliser certains filtres prêts à l’emploi, et également écrire vos propres filtres personnalisés.

Les filtres prêts à l’emploi incluent :

* Niveau de gravité de trace
* URL, mots clés ou codes de réponse spécifiques
* Réponses rapides, autrement dit, les demandes auxquelles votre application a répondu rapidement
* Noms des événements spécifiques

> [!NOTE]
> Les filtres faussent les mesures de votre application. Par exemple, vous pouvez décider que, pour diagnostiquer les réponses lentes, vous allez définir un filtre permettant d’ignorer les temps de réponse rapides. Toutefois, vous devez être conscient que les temps de réponse moyens signalés par Application Insights seront plus lents que la vitesse réelle, et que le nombre de demandes sera inférieur au nombre réel.
> Si cela pose problème, utilisez plutôt [l’échantillonnage](app-insights-sampling.md).

## <a name="setting-filters"></a>Définition de filtres

Dans ApplicationInsights.xml, ajoutez une section `TelemetryProcessors` comme dans cet exemple :


```XML

    <ApplicationInsights>
      <TelemetryProcessors>

        <BuiltInProcessors>
           <Processor type="TraceTelemetryFilter">
                  <Add name="FromSeverityLevel" value="ERROR"/>
           </Processor>

           <Processor type="RequestTelemetryFilter">
                  <Add name="MinimumDurationInMS" value="100"/>
                  <Add name="NotNeededResponseCodes" value="200-400"/>
           </Processor>

           <Processor type="PageViewTelemetryFilter">
                  <Add name="DurationThresholdInMS" value="100"/>
                  <Add name="NotNeededNames" value="home,index"/>
                  <Add name="NotNeededUrls" value=".jpg,.css"/>
           </Processor>

           <Processor type="TelemetryEventFilter">
                  <!-- Names of events we don't want to see -->
                  <Add name="NotNeededNames" value="Start,Stop,Pause"/>
           </Processor>

           <!-- Exclude telemetry from availability tests and bots -->
           <Processor type="SyntheticSourceFilter">
                <!-- Optional: specify which synthetic sources,
                     comma-separated
                     - default is all synthetics -->
                <Add name="NotNeededSources" value="Application Insights Availability Monitoring,BingPreview"
           </Processor>

        </BuiltInProcessors>

        <CustomProcessors>
          <Processor type="com.fabrikam.MyFilter">
            <Add name="Successful" value="false"/>
          </Processor>
        </CustomProcessors>

      </TelemetryProcessors>
    </ApplicationInsights>

```




[Inspectez l’ensemble complet des processeurs intégrés](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor).

## <a name="built-in-filters"></a>Filtres intégrés

### <a name="metric-telemetry-filter"></a>Filtre Télémétrie des mesures

```XML

           <Processor type="MetricTelemetryFilter">
                  <Add name="NotNeeded" value="metric1,metric2"/>
           </Processor>
```

* `NotNeeded` : liste séparée par des virgules de noms de mesures personnalisées.


### <a name="page-view-telemetry-filter"></a>Filtre Télémétrie d’affichage de page

```XML

           <Processor type="PageViewTelemetryFilter">
                  <Add name="DurationThresholdInMS" value="500"/>
                  <Add name="NotNeededNames" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```

* `DurationThresholdInMS` : la durée correspond au temps nécessaire pour charger la page. Si ce paramètre est défini, les pages qui se sont chargées plus rapidement que cette durée ne sont pas signalées.
* `NotNeededNames` : liste séparée par des virgules de noms de pages.
* `NotNeededUrls` : liste séparée par des virgules de fragments d’URL. Par exemple, `"home"` exclut toutes les pages contenant « home » dans l’URL.


### <a name="request-telemetry-filter"></a>Filtre Télémétrie des demandes


```XML

           <Processor type="RequestTelemetryFilter">
                  <Add name="MinimumDurationInMS" value="500"/>
                  <Add name="NotNeededResponseCodes" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```



### <a name="synthetic-source-filter"></a>Filtre Sources synthétiques

Exclut toutes les données de télémétrie présentant des valeurs dans la propriété SyntheticSource. Cela inclut notamment les demandes des robots, les robots et les tests de disponibilité.

Exclure les données de télémétrie pour toutes les demandes synthétiques :


```XML

           <Processor type="SyntheticSourceFilter" />
```

Exclure les données de télémétrie pour des sources synthétiques spécifiques :


```XML

           <Processor type="SyntheticSourceFilter" >
                  <Add name="NotNeeded" value="source1,source2"/>
           </Processor>
```

* `NotNeeded` : liste séparée par des virgules de noms de sources synthétiques.

### <a name="telemetry-event-filter"></a>Filtre Événements de télémétrie

Filtre les événements personnalisés (consignés à l’aide de [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)).


```XML

           <Processor type="TelemetryEventFilter" >
                  <Add name="NotNeededNames" value="event1, event2"/>
           </Processor>
```


* `NotNeededNames` : liste séparée par des virgules de noms d’événements.


### <a name="trace-telemetry-filter"></a>Filtre Télémétrie des traces

Filtre les traces de journaux (consignés à l’aide de [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) ou d’un [collecteur framework de journalisation](app-insights-java-trace-logs.md)).

```XML

           <Processor type="TraceTelemetryFilter">
                  <Add name="FromSeverityLevel" value="ERROR"/>
           </Processor>
```

* Les valeurs autorisées `FromSeverityLevel` sont :
 *  OFF             - Exclure TOUTES les traces
 *  TRACE           - Aucun filtrage. équivaut au niveau Trace
 *  INFO            - Exclure le niveau TRACE
 *  WARN            - Exclure TRACE et INFO
 *  ERROR           - Exclure WARN, INFO, TRACE
 *  CRITICAL        - Exclure tout sauf CRITICAL


## <a name="custom-filters"></a>Filtres personnalisés

### <a name="1-code-your-filter"></a>1. Codez votre filtre

Dans votre code, créez une classe qui implémente `TelemetryProcessor`:

```Java

    package com.fabrikam.MyFilter;
    import com.microsoft.applicationinsights.extensibility.TelemetryProcessor;
    import com.microsoft.applicationinsights.telemetry.Telemetry;

    public class SuccessFilter implements TelemetryProcessor {

       /* Any parameters that are required to support the filter.*/
       private final String successful;

       /* Initializers for the parameters, named "setParameterName" */
       public void setNotNeeded(String successful)
       {
          this.successful = successful;
       }

       /* This method is called for each item of telemetry to be sent.
          Return false to discard it.
          Return true to allow other processors to inspect it. */
       @Override
       public boolean process(Telemetry telemetry) {
        if (telemetry == null) { return true; }
        if (telemetry instanceof RequestTelemetry)
        {
            RequestTelemetry requestTelemetry = (RequestTelemetry)telemetry;
            return request.getSuccess() == successful;
        }
        return true;
       }
    }

```


### <a name="2-invoke-your-filter-in-the-configuration-file"></a>2. Appeler votre filtre dans le fichier de configuration

Dans ApplicationInsights.xml :

```XML


    <ApplicationInsights>
      <TelemetryProcessors>
        <CustomProcessors>
          <Processor type="com.fabrikam.SuccessFilter">
            <Add name="Successful" value="false"/>
          </Processor>
        </CustomProcessors>
      </TelemetryProcessors>
    </ApplicationInsights>

```

## <a name="troubleshooting"></a>Résolution des problèmes

*Mon filtre ne fonctionne pas.*

* Vérifiez que vous avez fourni des valeurs de paramètres valides. Par exemple, les durées doivent être des entiers. En cas de valeurs non valides, le filtre est ignoré. Si votre filtre personnalisé lève une exception à partir d’un constructeur ou d’une méthode définie, il sera ignoré.

## <a name="next-steps"></a>Étapes suivantes

* [Échantillonnage](app-insights-sampling.md) : envisagez l’échantillonnage comme une possibilité ne faussant pas vos mesures.
