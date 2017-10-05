---
title: "Filtrage et prétraitement dans le Kit de développement logiciel (SDK) Azure Application Insights | Microsoft Docs"
description: "Écrivez des processeurs de télémétrie et des initialiseurs de télémétrie que le Kit de développement logiciel (SDK) doit filtrer ou ajoutez des propriétés aux données avant que la télémétrie ne soit envoyée au portail Application Insights."
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
ms.openlocfilehash: 17e66775dd2cd1c858594102f1ddb32e2fbbccc8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="filtering-and-preprocessing-telemetry-in-the-application-insights-sdk"></a><span data-ttu-id="d3aa9-103">Filtrage et pré-traitement de la télémétrie dans le Kit de développement logiciel (SDK) Application Insights</span><span class="sxs-lookup"><span data-stu-id="d3aa9-103">Filtering and preprocessing telemetry in the Application Insights SDK</span></span>


<span data-ttu-id="d3aa9-104">Vous pouvez écrire et configurer des plug-ins pour le Kit de développement logiciel (SDK) Application Insights afin de personnaliser la capture et le traitement des données de télémétrie avant leur envoi au service Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-104">You can write and configure plug-ins for the Application Insights SDK to customize how telemetry is captured and processed before it is sent to the Application Insights service.</span></span>

* <span data-ttu-id="d3aa9-105">[échantillonnage](app-insights-sampling.md) réduit le volume des données de télémétrie sans affecter les statistiques.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-105">[Sampling](app-insights-sampling.md) reduces the volume of telemetry without affecting your statistics.</span></span> <span data-ttu-id="d3aa9-106">Il maintient ensemble les points de données liés de sorte que vous pouvez naviguer entre eux pour diagnostiquer un problème.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-106">It keeps together related data points so that you can navigate between them when diagnosing a problem.</span></span> <span data-ttu-id="d3aa9-107">Dans le portail, les nombres totaux sont multipliés pour compenser l'échantillonnage.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-107">In the portal, the total counts are multiplied to compensate for the sampling.</span></span>
* <span data-ttu-id="d3aa9-108">Le filtrage avec des processeurs de télémétrie [pour ASP.NET](#filtering) ou [Java](app-insights-java-filter-telemetry.md) vous permet de sélectionner ou de modifier la télémétrie dans le Kit de développement logiciel (SDK) avant l’envoi au serveur.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-108">Filtering with Telemetry Processors [for ASP.NET](#filtering) or [Java](app-insights-java-filter-telemetry.md) lets you select or modify telemetry in the SDK before it is sent to the server.</span></span> <span data-ttu-id="d3aa9-109">Par exemple, vous pouvez réduire le volume de la télémétrie en excluant les demandes émanant de robots.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-109">For example, you could reduce the volume of telemetry by excluding requests from robots.</span></span> <span data-ttu-id="d3aa9-110">Mais le filtrage est une approche plus simple que l’échantillonnage pour réduire le trafic.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-110">But filtering is a more basic approach to reducing traffic than sampling.</span></span> <span data-ttu-id="d3aa9-111">Cela vous permet de mieux contrôler ce qui est transmis, mais vous devez être conscient que cela affecte vos statistiques ; par exemple, si vous filtrez toutes les demandes réussies.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-111">It allows you more control over what is transmitted, but you have to be aware that it affects your statistics - for example, if you filter out all successful requests.</span></span>
* <span data-ttu-id="d3aa9-112">[Les initialiseurs de télémétrie ajoutent des propriétés](#add-properties) à n’importe quelle télémétrie envoyée à partir de votre application, notamment les données de télémétrie fournies par les modules standard.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-112">[Telemetry Initializers add properties](#add-properties) to any telemetry sent from your app, including telemetry from the standard modules.</span></span> <span data-ttu-id="d3aa9-113">Par exemple, vous pouvez ajouter des valeurs calculées ou des numéros de version permettant de filtrer les données dans le portail.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-113">For example, you could add calculated values; or version numbers by which to filter the data in the portal.</span></span>
* <span data-ttu-id="d3aa9-114">[L'API SDK](app-insights-api-custom-events-metrics.md) est utilisée pour envoyer des événements et des mesures personnalisés.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-114">[The SDK API](app-insights-api-custom-events-metrics.md) is used to send custom events and metrics.</span></span>

<span data-ttu-id="d3aa9-115">Avant de commencer :</span><span class="sxs-lookup"><span data-stu-id="d3aa9-115">Before you start:</span></span>

* <span data-ttu-id="d3aa9-116">Installez le [SDK Application Insights pour ASP.NET](app-insights-asp-net.md) ou le [SDK pour Java](app-insights-java-get-started.md) dans votre application.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-116">Install the Application Insights [SDK for ASP.NET](app-insights-asp-net.md) or [SDK for Java](app-insights-java-get-started.md) in your app.</span></span>

<a name="filtering"></a>

## <a name="filtering-itelemetryprocessor"></a><span data-ttu-id="d3aa9-117">Filtrage : ITelemetryProcessor</span><span class="sxs-lookup"><span data-stu-id="d3aa9-117">Filtering: ITelemetryProcessor</span></span>
<span data-ttu-id="d3aa9-118">Cette technique vous offre un contrôle plus direct sur ce qui est inclus ou exclu du flux de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-118">This technique gives you more direct control over what is included or excluded from the telemetry stream.</span></span> <span data-ttu-id="d3aa9-119">Vous pouvez l'utiliser conjointement avec l'échantillonnage, ou séparément.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-119">You can use it in conjunction with Sampling, or separately.</span></span>

<span data-ttu-id="d3aa9-120">Pour filtrer la télémétrie, vous écrivez un processeur de télémétrie et l'enregistrez avec le Kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="d3aa9-120">To filter telemetry, you write a telemetry processor and register it with the SDK.</span></span> <span data-ttu-id="d3aa9-121">Toute la télémétrie passe par votre processeur et vous pouvez choisir de la supprimer du flux ou d'ajouter des propriétés.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-121">All telemetry goes through your processor, and you can choose to drop it from the stream, or add properties.</span></span> <span data-ttu-id="d3aa9-122">Cela inclut les données de télémétrie fournies par les modules standard tels que le collecteur de demandes HTTP et le collecteur de dépendances, ainsi que les données de télémétrie que vous avez écrites vous-même.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-122">This includes telemetry from the standard modules such as the HTTP request collector and the dependency collector, as well as telemetry you have written yourself.</span></span> <span data-ttu-id="d3aa9-123">Vous pouvez, par exemple, exclure la télémétrie concernant les demandes émanant de robots ou les appels de dépendance réussis.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-123">You can, for example, filter out telemetry about requests from robots, or successful dependency calls.</span></span>

> [!WARNING]
> <span data-ttu-id="d3aa9-124">Filtrer la télémétrie envoyée depuis le Kit de développement logiciel (SDK) à l’aide de processeurs peut fausser les statistiques que vous voyez dans le portail et rendre difficile le suivi des éléments associés.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-124">Filtering the telemetry sent from the SDK using processors can skew the statistics that you see in the portal, and make it difficult to follow related items.</span></span>
>
> <span data-ttu-id="d3aa9-125">Envisagez plutôt d'utiliser l' [échantillonnage](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="d3aa9-125">Instead, consider using [sampling](app-insights-sampling.md).</span></span>
>
>

### <a name="create-a-telemetry-processor-c"></a><span data-ttu-id="d3aa9-126">Créer un processeur de télémétrie (C#)</span><span class="sxs-lookup"><span data-stu-id="d3aa9-126">Create a telemetry processor (C#)</span></span>
1. <span data-ttu-id="d3aa9-127">Vérifiez que la version du SDK Application Insights dans votre projet est la version 2.0.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-127">Verify that the Application Insights SDK in your project is  version 2.0.0 or later.</span></span> <span data-ttu-id="d3aa9-128">Cliquez avec le bouton droit sur votre projet dans l'explorateur de solutions Visual Studio, puis sélectionnez Gérer les packages NuGet.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-128">Right-click your project in Visual Studio Solution Explorer and choose Manage NuGet Packages.</span></span> <span data-ttu-id="d3aa9-129">Dans le Gestionnaire de package NuGet, cochez Microsoft.ApplicationInsights.Web.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-129">In NuGet package manager, check Microsoft.ApplicationInsights.Web.</span></span>
2. <span data-ttu-id="d3aa9-130">Pour créer un filtre, déployez ITelemetryProcessor.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-130">To create a filter, implement ITelemetryProcessor.</span></span> <span data-ttu-id="d3aa9-131">Il s’agit d’un autre point d’extensibilité, à l’instar d’un module de télémétrie, d’un initialiseur de télémétrie et d’un canal de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-131">This is another extensibility point like telemetry module, telemetry initializer, and telemetry channel.</span></span>

    <span data-ttu-id="d3aa9-132">Notez que les processeurs de télémétrie construisent une chaîne de traitement.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-132">Notice that Telemetry Processors construct a chain of processing.</span></span> <span data-ttu-id="d3aa9-133">Lorsque vous instanciez un processeur de télémétrie, vous transmettez un lien au processeur suivant dans la chaîne.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-133">When you instantiate a telemetry processor, you pass a link to the next processor in the chain.</span></span> <span data-ttu-id="d3aa9-134">Lorsqu’un point de données de télémétrie est transmis à la méthode de traitement, il effectue son travail, puis appelle le processeur de télémétrie suivant dans la chaîne.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-134">When a telemetry data point is passed to the Process method, it does its work and then calls the next Telemetry Processor in the chain.</span></span>

    ``` C#

    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.Extensibility;

    public class SuccessfulDependencyFilter : ITelemetryProcessor
      {

        private ITelemetryProcessor Next { get; set; }

        // You can pass values from .config
        public string MyParamFromConfigFile { get; set; }

        // Link processors to each other in a chain.
        public SuccessfulDependencyFilter(ITelemetryProcessor next)
        {
            this.Next = next;
        }
        public void Process(ITelemetry item)
        {
            // To filter out an item, just return
            if (!OKtoSend(item)) { return; }
            // Modify the item if required
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
1. <span data-ttu-id="d3aa9-135">Insérez-la dans ApplicationInsights.config :</span><span class="sxs-lookup"><span data-stu-id="d3aa9-135">Insert this in ApplicationInsights.config:</span></span>

```XML

    <TelemetryProcessors>
      <Add Type="WebApplication9.SuccessfulDependencyFilter, WebApplication9">
         <!-- Set public property -->
         <MyParamFromConfigFile>2-beta</MyParamFromConfigFile>
      </Add>
    </TelemetryProcessors>

```

<span data-ttu-id="d3aa9-136">(Il s’agit de la section dans laquelle vous initialisez un filtre d’échantillonnage.)</span><span class="sxs-lookup"><span data-stu-id="d3aa9-136">(This is the same section where you initialize a sampling filter.)</span></span>

<span data-ttu-id="d3aa9-137">Vous pouvez transférer des valeurs de chaîne depuis le fichier .config en fournissant des propriétés publiques nommées dans votre classe.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-137">You can pass string values from the .config file by providing public named properties in your class.</span></span>

> [!WARNING]
> <span data-ttu-id="d3aa9-138">Veillez à faire correspondre le nom de type et les noms de propriété dans le fichier .config aux noms de classe et de propriété dans le code.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-138">Take care to match the type name and any property names in the .config file to the class and property names in the code.</span></span> <span data-ttu-id="d3aa9-139">Si le fichier .config fait référence à un type ou à une propriété qui n'existe pas, le kit de développement peut échouer lors de l'envoi d'une télémétrie quelconque.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-139">If the .config file references a non-existent type or property, the SDK may silently fail to send any telemetry.</span></span>
>
>

<span data-ttu-id="d3aa9-140">**également** initialiser le filtre dans le code.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-140">**Alternatively,** you can initialize the filter in code.</span></span> <span data-ttu-id="d3aa9-141">Dans une classe d’initialisation appropriée (par exemple, AppStart dans Global.asax.cs), insérez votre processeur dans la chaîne :</span><span class="sxs-lookup"><span data-stu-id="d3aa9-141">In a suitable initialization class - for example AppStart in Global.asax.cs - insert your processor into the chain:</span></span>

```C#

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;
    builder.Use((next) => new SuccessfulDependencyFilter(next));

    // If you have more processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="d3aa9-142">Les clients de télémétrie créés après ce point utiliseront vos processeurs.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-142">TelemetryClients created after this point will use your processors.</span></span>

### <a name="example-filters"></a><span data-ttu-id="d3aa9-143">Exemples de filtres</span><span class="sxs-lookup"><span data-stu-id="d3aa9-143">Example filters</span></span>
#### <a name="synthetic-requests"></a><span data-ttu-id="d3aa9-144">Demandes synthétiques</span><span class="sxs-lookup"><span data-stu-id="d3aa9-144">Synthetic requests</span></span>
<span data-ttu-id="d3aa9-145">Excluez les robots et les tests web.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-145">Filter out bots and web tests.</span></span> <span data-ttu-id="d3aa9-146">Bien que Metrics Explorer vous donne la possibilité d’exclure les sources synthétiques, cette option réduit le trafic en les filtrant au niveau du Kit de développement (SDK).</span><span class="sxs-lookup"><span data-stu-id="d3aa9-146">Although Metrics Explorer gives you the option to filter out synthetic sources, this option reduces traffic by filtering them at the SDK.</span></span>

``` C#

    public void Process(ITelemetry item)
    {
      if (!string.IsNullOrEmpty(item.Context.Operation.SyntheticSource)) {return;}

      // Send everything else:
      this.Next.Process(item);
    }

```

#### <a name="failed-authentication"></a><span data-ttu-id="d3aa9-147">Échec d’authentification</span><span class="sxs-lookup"><span data-stu-id="d3aa9-147">Failed authentication</span></span>
<span data-ttu-id="d3aa9-148">Excluez les demandes avec une réponse de type « 401 ».</span><span class="sxs-lookup"><span data-stu-id="d3aa9-148">Filter out requests with a "401" response.</span></span>

```C#

public void Process(ITelemetry item)
{
    var request = item as RequestTelemetry;

    if (request != null &&
    request.ResponseCode.Equals("401", StringComparison.OrdinalIgnoreCase))
    {
        // To filter out an item, just terminate the chain:
        return;
    }
    // Send everything else:
    this.Next.Process(item);
}

```

#### <a name="filter-out-fast-remote-dependency-calls"></a><span data-ttu-id="d3aa9-149">Excluez les appels de dépendance à distance rapides.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-149">Filter out fast remote dependency calls</span></span>
<span data-ttu-id="d3aa9-150">Si vous souhaitez uniquement diagnostiquer les appels lents, excluez les appels rapides.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-150">If you only want to diagnose calls that are slow, filter out the fast ones.</span></span>

> [!NOTE]
> <span data-ttu-id="d3aa9-151">Cela faussera les statistiques que vous voyez dans le portail.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-151">This will skew the statistics you see on the portal.</span></span> <span data-ttu-id="d3aa9-152">Le graphique de dépendance s’affichera comme si les appels de dépendance avaient tous échoué.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-152">The dependency chart will look as if the dependency calls are all failures.</span></span>
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

#### <a name="diagnose-dependency-issues"></a><span data-ttu-id="d3aa9-153">Diagnostiquer les problèmes de dépendance</span><span class="sxs-lookup"><span data-stu-id="d3aa9-153">Diagnose dependency issues</span></span>
<span data-ttu-id="d3aa9-154">[Ce blog](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) décrit un projet pour diagnostiquer les problèmes de dépendance en envoyant automatiquement des requêtes ping régulières aux dépendances.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-154">[This blog](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) describes a project to diagnose dependency issues by automatically sending regular pings to dependencies.</span></span>


<a name="add-properties"></a>

## <a name="add-properties-itelemetryinitializer"></a><span data-ttu-id="d3aa9-155">Ajouter des propriétés : ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="d3aa9-155">Add properties: ITelemetryInitializer</span></span>
<span data-ttu-id="d3aa9-156">Utilisez des initialiseurs de télémétrie pour définir des propriétés globales qui sont envoyées avec toute la télémétrie ; et pour substituer le comportement sélectionné des modules standard de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-156">Use telemetry initializers to define global properties that are sent with all telemetry; and to override selected behavior of the standard telemetry modules.</span></span>

<span data-ttu-id="d3aa9-157">Par exemple, le package Application Insights pour le Web collecte la télémétrie sur les requêtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-157">For example, the Application Insights for Web package collects telemetry about HTTP requests.</span></span> <span data-ttu-id="d3aa9-158">Il indique par défaut l’échec de toute requête à l’aide d’un code de réponse supérieur ou égal à 400.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-158">By default, it flags as failed any request with a response code >= 400.</span></span> <span data-ttu-id="d3aa9-159">Toutefois, si 400 vous convient, vous pouvez fournir un initialiseur de télémétrie qui définit la propriété Success.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-159">But if you want to treat 400 as a success, you can provide a telemetry initializer that sets the Success property.</span></span>

<span data-ttu-id="d3aa9-160">Si vous fournissez un initialiseur de télémétrie, celui-ci est appelé chaque fois qu'une des méthodes Track*() est appelée.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-160">If you provide a telemetry initializer, it is called whenever any of the Track*() methods is called.</span></span> <span data-ttu-id="d3aa9-161">Cela inclut les méthodes appelées par les modules de télémétrie standard.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-161">This includes methods called by the standard telemetry modules.</span></span> <span data-ttu-id="d3aa9-162">Par convention, ces modules ne définissent aucune propriété déjà définie par un initialiseur.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-162">By convention, these modules do not set any property that has already been set by an initializer.</span></span>

<span data-ttu-id="d3aa9-163">**Définir votre initialiseur**</span><span class="sxs-lookup"><span data-stu-id="d3aa9-163">**Define your initializer**</span></span>

<span data-ttu-id="d3aa9-164">*C#*</span><span class="sxs-lookup"><span data-stu-id="d3aa9-164">*C#*</span></span>

```C#

    using System;
    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.DataContracts;
    using Microsoft.ApplicationInsights.Extensibility;

    namespace MvcWebRole.Telemetry
    {
      /*
       * Custom TelemetryInitializer that overrides the default SDK
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
                // If we set the Success property, the SDK won't change it:
                requestTelemetry.Success = true;
                // Allow us to filter these requests in the portal:
                requestTelemetry.Context.Properties["Overridden400s"] = "true";
            }
            // else leave the SDK to set the Success property      
        }
      }
    }
```

<span data-ttu-id="d3aa9-165">**Charger votre initialiseur**</span><span class="sxs-lookup"><span data-stu-id="d3aa9-165">**Load your initializer**</span></span>

<span data-ttu-id="d3aa9-166">Dans ApplicationInsights.config :</span><span class="sxs-lookup"><span data-stu-id="d3aa9-166">In ApplicationInsights.config:</span></span>

    <ApplicationInsights>
      <TelemetryInitializers>
        <!-- Fully qualified type name, assembly name: -->
        <Add Type="MvcWebRole.Telemetry.MyTelemetryInitializer, MvcWebRole"/>
        ...
      </TelemetryInitializers>
    </ApplicationInsights>

<span data-ttu-id="d3aa9-167">*également* instancier l'initialiseur dans le code, par exemple dans Global.aspx.cs :</span><span class="sxs-lookup"><span data-stu-id="d3aa9-167">*Alternatively,* you can instantiate the initializer in code, for example in Global.aspx.cs:</span></span>

```C#
    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```


[<span data-ttu-id="d3aa9-168">Voir l’intégralité de cet exemple.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-168">See more of this sample.</span></span>](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/MvcWebRole)

<a name="js-initializer"></a>

### <a name="javascript-telemetry-initializers"></a><span data-ttu-id="d3aa9-169">Initialiseurs de télémétrie JavaScript</span><span class="sxs-lookup"><span data-stu-id="d3aa9-169">JavaScript telemetry initializers</span></span>
<span data-ttu-id="d3aa9-170">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="d3aa9-170">*JavaScript*</span></span>

<span data-ttu-id="d3aa9-171">Insérer un initialiseur de télémétrie immédiatement après le code d’initialisation obtenu à partir du portail :</span><span class="sxs-lookup"><span data-stu-id="d3aa9-171">Insert a telemetry initializer immediately after the initialization code that you got from the portal:</span></span>

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

                // To check the telemetry item’s type - for example PageView:
                if (envelope.name == Microsoft.ApplicationInsights.Telemetry.PageView.envelopeType) {
                    // this statement removes url from all page view documents
                    telemetryItem.url = "URL CENSORED";
                }

                // To set custom properties:
                telemetryItem.properties = telemetryItem.properties || {};
                telemetryItem.properties["globalProperty"] = "boo";

                // To set custom metrics:
                telemetryItem.measurements = telemetryItem.measurements || {};
                telemetryItem.measurements["globalMetric"] = 100;
            });
        });

        // End of inserted code.

        appInsights.trackPageView();
    </script>
```

<span data-ttu-id="d3aa9-172">Pour obtenir un résumé des propriétés non personnalisées disponibles dans le telemetryItem, consultez le [modèle d’exportation de données Application Insights](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="d3aa9-172">For a summary of the non-custom properties available on the telemetryItem, see [Application Insights Export Data Model](app-insights-export-data-model.md).</span></span>

<span data-ttu-id="d3aa9-173">Vous pouvez ajouter autant d'initialiseurs que vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-173">You can add as many initializers as you like.</span></span>

## <a name="itelemetryprocessor-and-itelemetryinitializer"></a><span data-ttu-id="d3aa9-174">ITelemetryProcessor et ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="d3aa9-174">ITelemetryProcessor and ITelemetryInitializer</span></span>
<span data-ttu-id="d3aa9-175">Quelle est la différence entre les processeurs de télémétrie et les initialiseurs de télémétrie ?</span><span class="sxs-lookup"><span data-stu-id="d3aa9-175">What's the difference between telemetry processors and telemetry initializers?</span></span>

* <span data-ttu-id="d3aa9-176">Leurs utilisations se recoupent partiellement : les deux peuvent être utilisés pour ajouter des propriétés à la télémétrie.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-176">There are some overlaps in what you can do with them: both can be used to add properties to telemetry.</span></span>
* <span data-ttu-id="d3aa9-177">Les TelemetryInitializers sont toujours exécutés avant les TelemetryProcessors.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-177">TelemetryInitializers always run before TelemetryProcessors.</span></span>
* <span data-ttu-id="d3aa9-178">Les TelemetryProcessors permettent de remplacer ou supprimer complètement un élément de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-178">TelemetryProcessors allow you to completely replace or discard a telemetry item.</span></span>
* <span data-ttu-id="d3aa9-179">Les TelemetryProcessors ne traitent pas la télémétrie du compteur de performances.</span><span class="sxs-lookup"><span data-stu-id="d3aa9-179">TelemetryProcessors don't process performance counter telemetry.</span></span>


## <a name="reference-docs"></a><span data-ttu-id="d3aa9-180">Documents de référence</span><span class="sxs-lookup"><span data-stu-id="d3aa9-180">Reference docs</span></span>
* [<span data-ttu-id="d3aa9-181">Présentation de l’API</span><span class="sxs-lookup"><span data-stu-id="d3aa9-181">API Overview</span></span>](app-insights-api-custom-events-metrics.md)
* [<span data-ttu-id="d3aa9-182">Référence ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d3aa9-182">ASP.NET reference</span></span>](https://msdn.microsoft.com/library/dn817570.aspx)

## <a name="sdk-code"></a><span data-ttu-id="d3aa9-183">Code du Kit de développement logiciel (SDK)</span><span class="sxs-lookup"><span data-stu-id="d3aa9-183">SDK Code</span></span>
* [<span data-ttu-id="d3aa9-184">Kit de développement logiciel (SDK) principal ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d3aa9-184">ASP.NET Core SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [<span data-ttu-id="d3aa9-185">ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="d3aa9-185">ASP.NET 5</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [<span data-ttu-id="d3aa9-186">Kit de développement logiciel (SDK) JavaScript</span><span class="sxs-lookup"><span data-stu-id="d3aa9-186">JavaScript SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-JS)

## <span data-ttu-id="d3aa9-187"><a name="next"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d3aa9-187"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="d3aa9-188">Recherche d’événements et de journaux</span><span class="sxs-lookup"><span data-stu-id="d3aa9-188">Search events and logs</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="d3aa9-189">Échantillonnage</span><span class="sxs-lookup"><span data-stu-id="d3aa9-189">Sampling</span></span>](app-insights-sampling.md)
* [<span data-ttu-id="d3aa9-190">Dépannage</span><span class="sxs-lookup"><span data-stu-id="d3aa9-190">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)
