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
# <a name="filter-telemetry-in-your-java-web-app"></a><span data-ttu-id="d9558-103">Filtrer la télémétrie dans votre application web Java</span><span class="sxs-lookup"><span data-stu-id="d9558-103">Filter telemetry in your Java web app</span></span>

<span data-ttu-id="d9558-104">Les filtres offrent un moyen de sélectionner les données de télémétrie que votre [application web Java envoie à Application Insights](app-insights-java-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d9558-104">Filters provide a way to select the telemetry that your [Java web app sends to Application Insights](app-insights-java-get-started.md).</span></span> <span data-ttu-id="d9558-105">Vous pouvez utiliser certains filtres prêts à l’emploi, et également écrire vos propres filtres personnalisés.</span><span class="sxs-lookup"><span data-stu-id="d9558-105">There are some out-of-the-box filters that you can use, and you can also write your own custom filters.</span></span>

<span data-ttu-id="d9558-106">Les filtres prêts à l’emploi incluent :</span><span class="sxs-lookup"><span data-stu-id="d9558-106">The out-of-the-box filters include:</span></span>

* <span data-ttu-id="d9558-107">Niveau de gravité de trace</span><span class="sxs-lookup"><span data-stu-id="d9558-107">Trace severity level</span></span>
* <span data-ttu-id="d9558-108">URL, mots clés ou codes de réponse spécifiques</span><span class="sxs-lookup"><span data-stu-id="d9558-108">Specific URLs, keywords or response codes</span></span>
* <span data-ttu-id="d9558-109">Réponses rapides, autrement dit, les demandes auxquelles votre application a répondu rapidement</span><span class="sxs-lookup"><span data-stu-id="d9558-109">Fast responses - that is, requests to which your app responded to quickly</span></span>
* <span data-ttu-id="d9558-110">Noms des événements spécifiques</span><span class="sxs-lookup"><span data-stu-id="d9558-110">Specific event names</span></span>

> [!NOTE]
> <span data-ttu-id="d9558-111">Les filtres faussent les mesures de votre application.</span><span class="sxs-lookup"><span data-stu-id="d9558-111">Filters skew the metrics of your app.</span></span> <span data-ttu-id="d9558-112">Par exemple, vous pouvez décider que, pour diagnostiquer les réponses lentes, vous allez définir un filtre permettant d’ignorer les temps de réponse rapides.</span><span class="sxs-lookup"><span data-stu-id="d9558-112">For example, you might decide that, in order to diagnose slow responses, you will set a filter to discard fast response times.</span></span> <span data-ttu-id="d9558-113">Toutefois, vous devez être conscient que les temps de réponse moyens signalés par Application Insights seront plus lents que la vitesse réelle, et que le nombre de demandes sera inférieur au nombre réel.</span><span class="sxs-lookup"><span data-stu-id="d9558-113">But you must be aware that the average response times reported by Application Insights will then be slower than the true speed, and the count of requests will be smaller than the real count.</span></span>
> <span data-ttu-id="d9558-114">Si cela pose problème, utilisez plutôt [l’échantillonnage](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="d9558-114">If this is a concern, use [Sampling](app-insights-sampling.md) instead.</span></span>

## <a name="setting-filters"></a><span data-ttu-id="d9558-115">Définition de filtres</span><span class="sxs-lookup"><span data-stu-id="d9558-115">Setting filters</span></span>

<span data-ttu-id="d9558-116">Dans ApplicationInsights.xml, ajoutez une section `TelemetryProcessors` comme dans cet exemple :</span><span class="sxs-lookup"><span data-stu-id="d9558-116">In ApplicationInsights.xml, add a `TelemetryProcessors` section like this example:</span></span>


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




<span data-ttu-id="d9558-117">[Inspectez l’ensemble complet des processeurs intégrés](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor).</span><span class="sxs-lookup"><span data-stu-id="d9558-117">[Inspect the full set of built-in processors](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor).</span></span>

## <a name="built-in-filters"></a><span data-ttu-id="d9558-118">Filtres intégrés</span><span class="sxs-lookup"><span data-stu-id="d9558-118">Built-in filters</span></span>

### <a name="metric-telemetry-filter"></a><span data-ttu-id="d9558-119">Filtre Télémétrie des mesures</span><span class="sxs-lookup"><span data-stu-id="d9558-119">Metric Telemetry filter</span></span>

```XML

           <Processor type="MetricTelemetryFilter">
                  <Add name="NotNeeded" value="metric1,metric2"/>
           </Processor>
```

* <span data-ttu-id="d9558-120">`NotNeeded` : liste séparée par des virgules de noms de mesures personnalisées.</span><span class="sxs-lookup"><span data-stu-id="d9558-120">`NotNeeded` - Comma-separated list of custom metric names.</span></span>


### <a name="page-view-telemetry-filter"></a><span data-ttu-id="d9558-121">Filtre Télémétrie d’affichage de page</span><span class="sxs-lookup"><span data-stu-id="d9558-121">Page View Telemetry filter</span></span>

```XML

           <Processor type="PageViewTelemetryFilter">
                  <Add name="DurationThresholdInMS" value="500"/>
                  <Add name="NotNeededNames" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```

* <span data-ttu-id="d9558-122">`DurationThresholdInMS` : la durée correspond au temps nécessaire pour charger la page.</span><span class="sxs-lookup"><span data-stu-id="d9558-122">`DurationThresholdInMS` - Duration refers to the time taken to load the page.</span></span> <span data-ttu-id="d9558-123">Si ce paramètre est défini, les pages qui se sont chargées plus rapidement que cette durée ne sont pas signalées.</span><span class="sxs-lookup"><span data-stu-id="d9558-123">If this is set, pages that loaded faster than this time are not reported.</span></span>
* <span data-ttu-id="d9558-124">`NotNeededNames` : liste séparée par des virgules de noms de pages.</span><span class="sxs-lookup"><span data-stu-id="d9558-124">`NotNeededNames` - Comma-separated list of page names.</span></span>
* <span data-ttu-id="d9558-125">`NotNeededUrls` : liste séparée par des virgules de fragments d’URL.</span><span class="sxs-lookup"><span data-stu-id="d9558-125">`NotNeededUrls` - Comma-separated list of URL fragments.</span></span> <span data-ttu-id="d9558-126">Par exemple, `"home"` exclut toutes les pages contenant « home » dans l’URL.</span><span class="sxs-lookup"><span data-stu-id="d9558-126">For example, `"home"` filters out all pages that have "home" in the URL.</span></span>


### <a name="request-telemetry-filter"></a><span data-ttu-id="d9558-127">Filtre Télémétrie des demandes</span><span class="sxs-lookup"><span data-stu-id="d9558-127">Request Telemetry Filter</span></span>


```XML

           <Processor type="RequestTelemetryFilter">
                  <Add name="MinimumDurationInMS" value="500"/>
                  <Add name="NotNeededResponseCodes" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```



### <a name="synthetic-source-filter"></a><span data-ttu-id="d9558-128">Filtre Sources synthétiques</span><span class="sxs-lookup"><span data-stu-id="d9558-128">Synthetic Source filter</span></span>

<span data-ttu-id="d9558-129">Exclut toutes les données de télémétrie présentant des valeurs dans la propriété SyntheticSource.</span><span class="sxs-lookup"><span data-stu-id="d9558-129">Filters out all telemetry that have values in the SyntheticSource property.</span></span> <span data-ttu-id="d9558-130">Cela inclut notamment les demandes des robots, les robots et les tests de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="d9558-130">These include requests from bots, spiders and availability tests.</span></span>

<span data-ttu-id="d9558-131">Exclure les données de télémétrie pour toutes les demandes synthétiques :</span><span class="sxs-lookup"><span data-stu-id="d9558-131">Filter out telemetry for all synthetic requests:</span></span>


```XML

           <Processor type="SyntheticSourceFilter" />
```

<span data-ttu-id="d9558-132">Exclure les données de télémétrie pour des sources synthétiques spécifiques :</span><span class="sxs-lookup"><span data-stu-id="d9558-132">Filter out telemetry for specific synthetic sources:</span></span>


```XML

           <Processor type="SyntheticSourceFilter" >
                  <Add name="NotNeeded" value="source1,source2"/>
           </Processor>
```

* <span data-ttu-id="d9558-133">`NotNeeded` : liste séparée par des virgules de noms de sources synthétiques.</span><span class="sxs-lookup"><span data-stu-id="d9558-133">`NotNeeded` - Comma-separated list of synthetic source names.</span></span>

### <a name="telemetry-event-filter"></a><span data-ttu-id="d9558-134">Filtre Événements de télémétrie</span><span class="sxs-lookup"><span data-stu-id="d9558-134">Telemetry Event filter</span></span>

<span data-ttu-id="d9558-135">Filtre les événements personnalisés (consignés à l’aide de [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)).</span><span class="sxs-lookup"><span data-stu-id="d9558-135">Filters custom events (logged using [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)).</span></span>


```XML

           <Processor type="TelemetryEventFilter" >
                  <Add name="NotNeededNames" value="event1, event2"/>
           </Processor>
```


* <span data-ttu-id="d9558-136">`NotNeededNames` : liste séparée par des virgules de noms d’événements.</span><span class="sxs-lookup"><span data-stu-id="d9558-136">`NotNeededNames` - Comma-separated list of event names.</span></span>


### <a name="trace-telemetry-filter"></a><span data-ttu-id="d9558-137">Filtre Télémétrie des traces</span><span class="sxs-lookup"><span data-stu-id="d9558-137">Trace Telemetry filter</span></span>

<span data-ttu-id="d9558-138">Filtre les traces de journaux (consignés à l’aide de [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) ou d’un [collecteur framework de journalisation](app-insights-java-trace-logs.md)).</span><span class="sxs-lookup"><span data-stu-id="d9558-138">Filters log traces (logged using [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) or a [logging framework collector](app-insights-java-trace-logs.md)).</span></span>

```XML

           <Processor type="TraceTelemetryFilter">
                  <Add name="FromSeverityLevel" value="ERROR"/>
           </Processor>
```

* <span data-ttu-id="d9558-139">Les valeurs autorisées `FromSeverityLevel` sont :</span><span class="sxs-lookup"><span data-stu-id="d9558-139">`FromSeverityLevel` valid values are:</span></span>
 *  <span data-ttu-id="d9558-140">OFF             - Exclure TOUTES les traces</span><span class="sxs-lookup"><span data-stu-id="d9558-140">OFF             - Filter out ALL traces</span></span>
 *  <span data-ttu-id="d9558-141">TRACE           - Aucun filtrage.</span><span class="sxs-lookup"><span data-stu-id="d9558-141">TRACE           - No filtering.</span></span> <span data-ttu-id="d9558-142">équivaut au niveau Trace</span><span class="sxs-lookup"><span data-stu-id="d9558-142">equals to Trace level</span></span>
 *  <span data-ttu-id="d9558-143">INFO            - Exclure le niveau TRACE</span><span class="sxs-lookup"><span data-stu-id="d9558-143">INFO            - Filter out TRACE level</span></span>
 *  <span data-ttu-id="d9558-144">WARN            - Exclure TRACE et INFO</span><span class="sxs-lookup"><span data-stu-id="d9558-144">WARN            - Filter out TRACE and INFO</span></span>
 *  <span data-ttu-id="d9558-145">ERROR           - Exclure WARN, INFO, TRACE</span><span class="sxs-lookup"><span data-stu-id="d9558-145">ERROR           - Filter out WARN, INFO, TRACE</span></span>
 *  <span data-ttu-id="d9558-146">CRITICAL        - Exclure tout sauf CRITICAL</span><span class="sxs-lookup"><span data-stu-id="d9558-146">CRITICAL        - filter out all but CRITICAL</span></span>


## <a name="custom-filters"></a><span data-ttu-id="d9558-147">Filtres personnalisés</span><span class="sxs-lookup"><span data-stu-id="d9558-147">Custom filters</span></span>

### <a name="1-code-your-filter"></a><span data-ttu-id="d9558-148">1. Codez votre filtre</span><span class="sxs-lookup"><span data-stu-id="d9558-148">1. Code your filter</span></span>

<span data-ttu-id="d9558-149">Dans votre code, créez une classe qui implémente `TelemetryProcessor`:</span><span class="sxs-lookup"><span data-stu-id="d9558-149">In your code, create a class that implements `TelemetryProcessor`:</span></span>

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


### <a name="2-invoke-your-filter-in-the-configuration-file"></a><span data-ttu-id="d9558-150">2. Appeler votre filtre dans le fichier de configuration</span><span class="sxs-lookup"><span data-stu-id="d9558-150">2. Invoke your filter in the configuration file</span></span>

<span data-ttu-id="d9558-151">Dans ApplicationInsights.xml :</span><span class="sxs-lookup"><span data-stu-id="d9558-151">In ApplicationInsights.xml:</span></span>

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

## <a name="troubleshooting"></a><span data-ttu-id="d9558-152">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="d9558-152">Troubleshooting</span></span>

<span data-ttu-id="d9558-153">*Mon filtre ne fonctionne pas.*</span><span class="sxs-lookup"><span data-stu-id="d9558-153">*My filter isn't working.*</span></span>

* <span data-ttu-id="d9558-154">Vérifiez que vous avez fourni des valeurs de paramètres valides.</span><span class="sxs-lookup"><span data-stu-id="d9558-154">Check that you have provided valid parameter values.</span></span> <span data-ttu-id="d9558-155">Par exemple, les durées doivent être des entiers.</span><span class="sxs-lookup"><span data-stu-id="d9558-155">For example, durations should be integers.</span></span> <span data-ttu-id="d9558-156">En cas de valeurs non valides, le filtre est ignoré.</span><span class="sxs-lookup"><span data-stu-id="d9558-156">Invalid values will cause the filter to be ignored.</span></span> <span data-ttu-id="d9558-157">Si votre filtre personnalisé lève une exception à partir d’un constructeur ou d’une méthode définie, il sera ignoré.</span><span class="sxs-lookup"><span data-stu-id="d9558-157">If your custom filter throws an exception from a constructor or set method, it will be ignored.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9558-158">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d9558-158">Next steps</span></span>

* <span data-ttu-id="d9558-159">[Échantillonnage](app-insights-sampling.md) : envisagez l’échantillonnage comme une possibilité ne faussant pas vos mesures.</span><span class="sxs-lookup"><span data-stu-id="d9558-159">[Sampling](app-insights-sampling.md) - Consider sampling as an alternative that does not skew your metrics.</span></span>
