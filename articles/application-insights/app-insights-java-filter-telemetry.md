---
title: "aaaFilter télémétrie Azure Application Insights dans votre application de web Java | Documents Microsoft"
description: "Réduire le trafic de télémétrie en filtrant les événements de hello vous n’avez pas besoin toomonitor."
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
ms.openlocfilehash: 95713e11d5f86472777c67e4e7f3177fbf2cd0b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="filter-telemetry-in-your-java-web-app"></a><span data-ttu-id="d622d-103">Filtrer la télémétrie dans votre application web Java</span><span class="sxs-lookup"><span data-stu-id="d622d-103">Filter telemetry in your Java web app</span></span>

<span data-ttu-id="d622d-104">Filtres fournissent une télémétrie de hello tooselect façon dont votre [d’application web Java envoie tooApplication Insights](app-insights-java-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d622d-104">Filters provide a way tooselect hello telemetry that your [Java web app sends tooApplication Insights](app-insights-java-get-started.md).</span></span> <span data-ttu-id="d622d-105">Vous pouvez utiliser certains filtres prêts à l’emploi, et également écrire vos propres filtres personnalisés.</span><span class="sxs-lookup"><span data-stu-id="d622d-105">There are some out-of-the-box filters that you can use, and you can also write your own custom filters.</span></span>

<span data-ttu-id="d622d-106">les filtres out of box Hello incluent :</span><span class="sxs-lookup"><span data-stu-id="d622d-106">hello out-of-the-box filters include:</span></span>

* <span data-ttu-id="d622d-107">Niveau de gravité de trace</span><span class="sxs-lookup"><span data-stu-id="d622d-107">Trace severity level</span></span>
* <span data-ttu-id="d622d-108">URL, mots clés ou codes de réponse spécifiques</span><span class="sxs-lookup"><span data-stu-id="d622d-108">Specific URLs, keywords or response codes</span></span>
* <span data-ttu-id="d622d-109">Des réponses rapides - demande qui est, toowhich votre application a répondu tooquickly</span><span class="sxs-lookup"><span data-stu-id="d622d-109">Fast responses - that is, requests toowhich your app responded tooquickly</span></span>
* <span data-ttu-id="d622d-110">Noms des événements spécifiques</span><span class="sxs-lookup"><span data-stu-id="d622d-110">Specific event names</span></span>

> [!NOTE]
> <span data-ttu-id="d622d-111">Filtres d’inclinaison de métriques hello de votre application.</span><span class="sxs-lookup"><span data-stu-id="d622d-111">Filters skew hello metrics of your app.</span></span> <span data-ttu-id="d622d-112">Par exemple, vous pouvez décider que, dans l’ordre toodiagnose des réactions lentes, vous allez définir un filtre toodiscard un temps de réponse.</span><span class="sxs-lookup"><span data-stu-id="d622d-112">For example, you might decide that, in order toodiagnose slow responses, you will set a filter toodiscard fast response times.</span></span> <span data-ttu-id="d622d-113">Mais vous devez être conscient que les temps de réponse moyens hello signalés à Application Insights sera plus lents que la vitesse réelle de hello, et nombre hello de requêtes est inférieur au nombre réel de hello.</span><span class="sxs-lookup"><span data-stu-id="d622d-113">But you must be aware that hello average response times reported by Application Insights will then be slower than hello true speed, and hello count of requests will be smaller than hello real count.</span></span>
> <span data-ttu-id="d622d-114">Si cela pose problème, utilisez plutôt [l’échantillonnage](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="d622d-114">If this is a concern, use [Sampling](app-insights-sampling.md) instead.</span></span>

## <a name="setting-filters"></a><span data-ttu-id="d622d-115">Définition de filtres</span><span class="sxs-lookup"><span data-stu-id="d622d-115">Setting filters</span></span>

<span data-ttu-id="d622d-116">Dans ApplicationInsights.xml, ajoutez une section `TelemetryProcessors` comme dans cet exemple :</span><span class="sxs-lookup"><span data-stu-id="d622d-116">In ApplicationInsights.xml, add a `TelemetryProcessors` section like this example:</span></span>


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
                  <!-- Names of events we don't want toosee -->
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




<span data-ttu-id="d622d-117">[Inspecter le jeu complet de hello de processeurs intégrés](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor).</span><span class="sxs-lookup"><span data-stu-id="d622d-117">[Inspect hello full set of built-in processors](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor).</span></span>

## <a name="built-in-filters"></a><span data-ttu-id="d622d-118">Filtres intégrés</span><span class="sxs-lookup"><span data-stu-id="d622d-118">Built-in filters</span></span>

### <a name="metric-telemetry-filter"></a><span data-ttu-id="d622d-119">Filtre Télémétrie des mesures</span><span class="sxs-lookup"><span data-stu-id="d622d-119">Metric Telemetry filter</span></span>

```XML

           <Processor type="MetricTelemetryFilter">
                  <Add name="NotNeeded" value="metric1,metric2"/>
           </Processor>
```

* <span data-ttu-id="d622d-120">`NotNeeded` : liste séparée par des virgules de noms de mesures personnalisées.</span><span class="sxs-lookup"><span data-stu-id="d622d-120">`NotNeeded` - Comma-separated list of custom metric names.</span></span>


### <a name="page-view-telemetry-filter"></a><span data-ttu-id="d622d-121">Filtre Télémétrie d’affichage de page</span><span class="sxs-lookup"><span data-stu-id="d622d-121">Page View Telemetry filter</span></span>

```XML

           <Processor type="PageViewTelemetryFilter">
                  <Add name="DurationThresholdInMS" value="500"/>
                  <Add name="NotNeededNames" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```

* <span data-ttu-id="d622d-122">`DurationThresholdInMS`-Durée fait référence toohello durée de la page de hello tooload.</span><span class="sxs-lookup"><span data-stu-id="d622d-122">`DurationThresholdInMS` - Duration refers toohello time taken tooload hello page.</span></span> <span data-ttu-id="d622d-123">Si ce paramètre est défini, les pages qui se sont chargées plus rapidement que cette durée ne sont pas signalées.</span><span class="sxs-lookup"><span data-stu-id="d622d-123">If this is set, pages that loaded faster than this time are not reported.</span></span>
* <span data-ttu-id="d622d-124">`NotNeededNames` : liste séparée par des virgules de noms de pages.</span><span class="sxs-lookup"><span data-stu-id="d622d-124">`NotNeededNames` - Comma-separated list of page names.</span></span>
* <span data-ttu-id="d622d-125">`NotNeededUrls` : liste séparée par des virgules de fragments d’URL.</span><span class="sxs-lookup"><span data-stu-id="d622d-125">`NotNeededUrls` - Comma-separated list of URL fragments.</span></span> <span data-ttu-id="d622d-126">Par exemple, `"home"` exclut toutes les pages qui ont « accueil » dans l’URL de hello.</span><span class="sxs-lookup"><span data-stu-id="d622d-126">For example, `"home"` filters out all pages that have "home" in hello URL.</span></span>


### <a name="request-telemetry-filter"></a><span data-ttu-id="d622d-127">Filtre Télémétrie des demandes</span><span class="sxs-lookup"><span data-stu-id="d622d-127">Request Telemetry Filter</span></span>


```XML

           <Processor type="RequestTelemetryFilter">
                  <Add name="MinimumDurationInMS" value="500"/>
                  <Add name="NotNeededResponseCodes" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```



### <a name="synthetic-source-filter"></a><span data-ttu-id="d622d-128">Filtre Sources synthétiques</span><span class="sxs-lookup"><span data-stu-id="d622d-128">Synthetic Source filter</span></span>

<span data-ttu-id="d622d-129">Exclut toutes les données de télémétrie qui ont des valeurs Bonjour SyntheticSource propriété.</span><span class="sxs-lookup"><span data-stu-id="d622d-129">Filters out all telemetry that have values in hello SyntheticSource property.</span></span> <span data-ttu-id="d622d-130">Cela inclut notamment les demandes des robots, les robots et les tests de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="d622d-130">These include requests from bots, spiders and availability tests.</span></span>

<span data-ttu-id="d622d-131">Exclure les données de télémétrie pour toutes les demandes synthétiques :</span><span class="sxs-lookup"><span data-stu-id="d622d-131">Filter out telemetry for all synthetic requests:</span></span>


```XML

           <Processor type="SyntheticSourceFilter" />
```

<span data-ttu-id="d622d-132">Exclure les données de télémétrie pour des sources synthétiques spécifiques :</span><span class="sxs-lookup"><span data-stu-id="d622d-132">Filter out telemetry for specific synthetic sources:</span></span>


```XML

           <Processor type="SyntheticSourceFilter" >
                  <Add name="NotNeeded" value="source1,source2"/>
           </Processor>
```

* <span data-ttu-id="d622d-133">`NotNeeded` : liste séparée par des virgules de noms de sources synthétiques.</span><span class="sxs-lookup"><span data-stu-id="d622d-133">`NotNeeded` - Comma-separated list of synthetic source names.</span></span>

### <a name="telemetry-event-filter"></a><span data-ttu-id="d622d-134">Filtre Événements de télémétrie</span><span class="sxs-lookup"><span data-stu-id="d622d-134">Telemetry Event filter</span></span>

<span data-ttu-id="d622d-135">Filtre les événements personnalisés (consignés à l’aide de [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)).</span><span class="sxs-lookup"><span data-stu-id="d622d-135">Filters custom events (logged using [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)).</span></span>


```XML

           <Processor type="TelemetryEventFilter" >
                  <Add name="NotNeededNames" value="event1, event2"/>
           </Processor>
```


* <span data-ttu-id="d622d-136">`NotNeededNames` : liste séparée par des virgules de noms d’événements.</span><span class="sxs-lookup"><span data-stu-id="d622d-136">`NotNeededNames` - Comma-separated list of event names.</span></span>


### <a name="trace-telemetry-filter"></a><span data-ttu-id="d622d-137">Filtre Télémétrie des traces</span><span class="sxs-lookup"><span data-stu-id="d622d-137">Trace Telemetry filter</span></span>

<span data-ttu-id="d622d-138">Filtre les traces de journaux (consignés à l’aide de [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) ou d’un [collecteur framework de journalisation](app-insights-java-trace-logs.md)).</span><span class="sxs-lookup"><span data-stu-id="d622d-138">Filters log traces (logged using [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) or a [logging framework collector](app-insights-java-trace-logs.md)).</span></span>

```XML

           <Processor type="TraceTelemetryFilter">
                  <Add name="FromSeverityLevel" value="ERROR"/>
           </Processor>
```

* <span data-ttu-id="d622d-139">Les valeurs autorisées `FromSeverityLevel` sont :</span><span class="sxs-lookup"><span data-stu-id="d622d-139">`FromSeverityLevel` valid values are:</span></span>
 *  <span data-ttu-id="d622d-140">OFF             - Exclure TOUTES les traces</span><span class="sxs-lookup"><span data-stu-id="d622d-140">OFF             - Filter out ALL traces</span></span>
 *  <span data-ttu-id="d622d-141">TRACE           - Aucun filtrage.</span><span class="sxs-lookup"><span data-stu-id="d622d-141">TRACE           - No filtering.</span></span> <span data-ttu-id="d622d-142">niveau de tooTrace égal à</span><span class="sxs-lookup"><span data-stu-id="d622d-142">equals tooTrace level</span></span>
 *  <span data-ttu-id="d622d-143">INFO            - Exclure le niveau TRACE</span><span class="sxs-lookup"><span data-stu-id="d622d-143">INFO            - Filter out TRACE level</span></span>
 *  <span data-ttu-id="d622d-144">WARN            - Exclure TRACE et INFO</span><span class="sxs-lookup"><span data-stu-id="d622d-144">WARN            - Filter out TRACE and INFO</span></span>
 *  <span data-ttu-id="d622d-145">ERROR           - Exclure WARN, INFO, TRACE</span><span class="sxs-lookup"><span data-stu-id="d622d-145">ERROR           - Filter out WARN, INFO, TRACE</span></span>
 *  <span data-ttu-id="d622d-146">CRITICAL        - Exclure tout sauf CRITICAL</span><span class="sxs-lookup"><span data-stu-id="d622d-146">CRITICAL        - filter out all but CRITICAL</span></span>


## <a name="custom-filters"></a><span data-ttu-id="d622d-147">Filtres personnalisés</span><span class="sxs-lookup"><span data-stu-id="d622d-147">Custom filters</span></span>

### <a name="1-code-your-filter"></a><span data-ttu-id="d622d-148">1. Codez votre filtre</span><span class="sxs-lookup"><span data-stu-id="d622d-148">1. Code your filter</span></span>

<span data-ttu-id="d622d-149">Dans votre code, créez une classe qui implémente `TelemetryProcessor`:</span><span class="sxs-lookup"><span data-stu-id="d622d-149">In your code, create a class that implements `TelemetryProcessor`:</span></span>

```Java

    package com.fabrikam.MyFilter;
    import com.microsoft.applicationinsights.extensibility.TelemetryProcessor;
    import com.microsoft.applicationinsights.telemetry.Telemetry;

    public class SuccessFilter implements TelemetryProcessor {

       /* Any parameters that are required toosupport hello filter.*/
       private final String successful;

       /* Initializers for hello parameters, named "setParameterName" */
       public void setNotNeeded(String successful)
       {
          this.successful = successful;
       }

       /* This method is called for each item of telemetry toobe sent.
          Return false toodiscard it.
          Return true tooallow other processors tooinspect it. */
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


### <a name="2-invoke-your-filter-in-hello-configuration-file"></a><span data-ttu-id="d622d-150">2. Appeler votre filtre dans le fichier de configuration hello</span><span class="sxs-lookup"><span data-stu-id="d622d-150">2. Invoke your filter in hello configuration file</span></span>

<span data-ttu-id="d622d-151">Dans ApplicationInsights.xml :</span><span class="sxs-lookup"><span data-stu-id="d622d-151">In ApplicationInsights.xml:</span></span>

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

## <a name="troubleshooting"></a><span data-ttu-id="d622d-152">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="d622d-152">Troubleshooting</span></span>

<span data-ttu-id="d622d-153">*Mon filtre ne fonctionne pas.*</span><span class="sxs-lookup"><span data-stu-id="d622d-153">*My filter isn't working.*</span></span>

* <span data-ttu-id="d622d-154">Vérifiez que vous avez fourni des valeurs de paramètres valides.</span><span class="sxs-lookup"><span data-stu-id="d622d-154">Check that you have provided valid parameter values.</span></span> <span data-ttu-id="d622d-155">Par exemple, les durées doivent être des entiers.</span><span class="sxs-lookup"><span data-stu-id="d622d-155">For example, durations should be integers.</span></span> <span data-ttu-id="d622d-156">Valeurs non valides entraîne hello filtre toobe est ignoré.</span><span class="sxs-lookup"><span data-stu-id="d622d-156">Invalid values will cause hello filter toobe ignored.</span></span> <span data-ttu-id="d622d-157">Si votre filtre personnalisé lève une exception à partir d’un constructeur ou d’une méthode définie, il sera ignoré.</span><span class="sxs-lookup"><span data-stu-id="d622d-157">If your custom filter throws an exception from a constructor or set method, it will be ignored.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d622d-158">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d622d-158">Next steps</span></span>

* <span data-ttu-id="d622d-159">[Échantillonnage](app-insights-sampling.md) : envisagez l’échantillonnage comme une possibilité ne faussant pas vos mesures.</span><span class="sxs-lookup"><span data-stu-id="d622d-159">[Sampling](app-insights-sampling.md) - Consider sampling as an alternative that does not skew your metrics.</span></span>
