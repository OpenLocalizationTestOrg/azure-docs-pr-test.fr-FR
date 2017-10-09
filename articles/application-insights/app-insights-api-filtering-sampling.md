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
# <a name="filtering-and-preprocessing-telemetry-in-hello-application-insights-sdk"></a><span data-ttu-id="dc410-103">Le filtrage et le prétraitement des données de télémétrie de hello Application Insights SDK</span><span class="sxs-lookup"><span data-stu-id="dc410-103">Filtering and preprocessing telemetry in hello Application Insights SDK</span></span>


<span data-ttu-id="dc410-104">Vous pouvez écrire et configurer des plug-ins pour hello Application Insights SDK toocustomize la télémétrie est capturée et traitée avant d’être envoyée toohello service Application Insights.</span><span class="sxs-lookup"><span data-stu-id="dc410-104">You can write and configure plug-ins for hello Application Insights SDK toocustomize how telemetry is captured and processed before it is sent toohello Application Insights service.</span></span>

* <span data-ttu-id="dc410-105">[Échantillonnage](app-insights-sampling.md) réduit le volume de hello de télémétrie sans affecter vos statistiques.</span><span class="sxs-lookup"><span data-stu-id="dc410-105">[Sampling](app-insights-sampling.md) reduces hello volume of telemetry without affecting your statistics.</span></span> <span data-ttu-id="dc410-106">Il maintient ensemble les points de données liés de sorte que vous pouvez naviguer entre eux pour diagnostiquer un problème.</span><span class="sxs-lookup"><span data-stu-id="dc410-106">It keeps together related data points so that you can navigate between them when diagnosing a problem.</span></span> <span data-ttu-id="dc410-107">Dans le portail hello, nombre total de hello est multiplié toocompensate pour l’échantillonnage de hello.</span><span class="sxs-lookup"><span data-stu-id="dc410-107">In hello portal, hello total counts are multiplied toocompensate for hello sampling.</span></span>
* <span data-ttu-id="dc410-108">Le filtrage avec des processeurs de télémétrie [pour ASP.NET](#filtering) ou [Java](app-insights-java-filter-telemetry.md) vous permet de sélectionner ou de modifier la télémétrie Bonjour SDK avant d’être envoyée toohello server.</span><span class="sxs-lookup"><span data-stu-id="dc410-108">Filtering with Telemetry Processors [for ASP.NET](#filtering) or [Java](app-insights-java-filter-telemetry.md) lets you select or modify telemetry in hello SDK before it is sent toohello server.</span></span> <span data-ttu-id="dc410-109">Par exemple, vous pouvez réduire le volume de hello de télémétrie en excluant les demandes de robots.</span><span class="sxs-lookup"><span data-stu-id="dc410-109">For example, you could reduce hello volume of telemetry by excluding requests from robots.</span></span> <span data-ttu-id="dc410-110">Mais le filtrage est un trafic de tooreducing approche plus simple que l’échantillonnage.</span><span class="sxs-lookup"><span data-stu-id="dc410-110">But filtering is a more basic approach tooreducing traffic than sampling.</span></span> <span data-ttu-id="dc410-111">Il vous permet de mieux contrôler ce qui est transmis, mais vous avez toobe savoir qu’il affecte vos statistiques - par exemple, si vous filtrez toutes les demandes réussies.</span><span class="sxs-lookup"><span data-stu-id="dc410-111">It allows you more control over what is transmitted, but you have toobe aware that it affects your statistics - for example, if you filter out all successful requests.</span></span>
* <span data-ttu-id="dc410-112">[Ajouter des initialiseurs de télémétrie propriétés](#add-properties) télémétrie tooany envoyé à partir de votre application, y compris les données de télémétrie à partir des modules standards hello.</span><span class="sxs-lookup"><span data-stu-id="dc410-112">[Telemetry Initializers add properties](#add-properties) tooany telemetry sent from your app, including telemetry from hello standard modules.</span></span> <span data-ttu-id="dc410-113">Par exemple, vous pouvez ajouter des valeurs calculées ; ou les numéros de version par les données de hello toofilter dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="dc410-113">For example, you could add calculated values; or version numbers by which toofilter hello data in hello portal.</span></span>
* <span data-ttu-id="dc410-114">[Hello API du Kit de développement logiciel](app-insights-api-custom-events-metrics.md) est toosend utilisé des événements personnalisés et des mesures.</span><span class="sxs-lookup"><span data-stu-id="dc410-114">[hello SDK API](app-insights-api-custom-events-metrics.md) is used toosend custom events and metrics.</span></span>

<span data-ttu-id="dc410-115">Avant de commencer :</span><span class="sxs-lookup"><span data-stu-id="dc410-115">Before you start:</span></span>

* <span data-ttu-id="dc410-116">Installer l’Application hello Insights [SDK pour ASP.NET](app-insights-asp-net.md) ou [SDK pour Java](app-insights-java-get-started.md) dans votre application.</span><span class="sxs-lookup"><span data-stu-id="dc410-116">Install hello Application Insights [SDK for ASP.NET](app-insights-asp-net.md) or [SDK for Java](app-insights-java-get-started.md) in your app.</span></span>

<a name="filtering"></a>

## <a name="filtering-itelemetryprocessor"></a><span data-ttu-id="dc410-117">Filtrage : ITelemetryProcessor</span><span class="sxs-lookup"><span data-stu-id="dc410-117">Filtering: ITelemetryProcessor</span></span>
<span data-ttu-id="dc410-118">Cette technique vous donne un contrôle plus direct sur ce qui est inclus ou exclu des flux de données de télémétrie hello.</span><span class="sxs-lookup"><span data-stu-id="dc410-118">This technique gives you more direct control over what is included or excluded from hello telemetry stream.</span></span> <span data-ttu-id="dc410-119">Vous pouvez l'utiliser conjointement avec l'échantillonnage, ou séparément.</span><span class="sxs-lookup"><span data-stu-id="dc410-119">You can use it in conjunction with Sampling, or separately.</span></span>

<span data-ttu-id="dc410-120">toofilter télémétrie, vous écrivez un processeur de télémétrie et l’inscrivez auprès de hello Kit de développement logiciel.</span><span class="sxs-lookup"><span data-stu-id="dc410-120">toofilter telemetry, you write a telemetry processor and register it with hello SDK.</span></span> <span data-ttu-id="dc410-121">Toutes les données de télémétrie passe par le processeur, et vous pouvez choisir toodrop à partir de hello diffuser en continu, ou ajouter des propriétés.</span><span class="sxs-lookup"><span data-stu-id="dc410-121">All telemetry goes through your processor, and you can choose toodrop it from hello stream, or add properties.</span></span> <span data-ttu-id="dc410-122">Cela inclut les données de télémétrie à partir des modules standards hello telles que le collecteur de demande HTTP hello et le collecteur de dépendance hello, ainsi que la télémétrie que vous avez écrit vous-même.</span><span class="sxs-lookup"><span data-stu-id="dc410-122">This includes telemetry from hello standard modules such as hello HTTP request collector and hello dependency collector, as well as telemetry you have written yourself.</span></span> <span data-ttu-id="dc410-123">Vous pouvez, par exemple, exclure la télémétrie concernant les demandes émanant de robots ou les appels de dépendance réussis.</span><span class="sxs-lookup"><span data-stu-id="dc410-123">You can, for example, filter out telemetry about requests from robots, or successful dependency calls.</span></span>

> [!WARNING]
> <span data-ttu-id="dc410-124">Le filtrage de télémétrie hello envoyé à partir de hello SDK à l’aide de processeurs peut déformer les statistiques de hello hello portail et de rendre difficile toofollow concernant les éléments.</span><span class="sxs-lookup"><span data-stu-id="dc410-124">Filtering hello telemetry sent from hello SDK using processors can skew hello statistics that you see in hello portal, and make it difficult toofollow related items.</span></span>
>
> <span data-ttu-id="dc410-125">Envisagez plutôt d'utiliser l' [échantillonnage](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="dc410-125">Instead, consider using [sampling](app-insights-sampling.md).</span></span>
>
>

### <a name="create-a-telemetry-processor-c"></a><span data-ttu-id="dc410-126">Créer un processeur de télémétrie (C#)</span><span class="sxs-lookup"><span data-stu-id="dc410-126">Create a telemetry processor (C#)</span></span>
1. <span data-ttu-id="dc410-127">Vérifiez que hello Application Insights SDK dans votre projet est la version 2.0.0 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="dc410-127">Verify that hello Application Insights SDK in your project is  version 2.0.0 or later.</span></span> <span data-ttu-id="dc410-128">Cliquez avec le bouton droit sur votre projet dans l'explorateur de solutions Visual Studio, puis sélectionnez Gérer les packages NuGet.</span><span class="sxs-lookup"><span data-stu-id="dc410-128">Right-click your project in Visual Studio Solution Explorer and choose Manage NuGet Packages.</span></span> <span data-ttu-id="dc410-129">Dans le Gestionnaire de package NuGet, cochez Microsoft.ApplicationInsights.Web.</span><span class="sxs-lookup"><span data-stu-id="dc410-129">In NuGet package manager, check Microsoft.ApplicationInsights.Web.</span></span>
2. <span data-ttu-id="dc410-130">toocreate un filtre, implémenter ITelemetryProcessor.</span><span class="sxs-lookup"><span data-stu-id="dc410-130">toocreate a filter, implement ITelemetryProcessor.</span></span> <span data-ttu-id="dc410-131">Il s’agit d’un autre point d’extensibilité, à l’instar d’un module de télémétrie, d’un initialiseur de télémétrie et d’un canal de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="dc410-131">This is another extensibility point like telemetry module, telemetry initializer, and telemetry channel.</span></span>

    <span data-ttu-id="dc410-132">Notez que les processeurs de télémétrie construisent une chaîne de traitement.</span><span class="sxs-lookup"><span data-stu-id="dc410-132">Notice that Telemetry Processors construct a chain of processing.</span></span> <span data-ttu-id="dc410-133">Lorsque vous instanciez un processeur de télémétrie, vous passez un processeur suivant toohello de lien dans la chaîne de hello.</span><span class="sxs-lookup"><span data-stu-id="dc410-133">When you instantiate a telemetry processor, you pass a link toohello next processor in hello chain.</span></span> <span data-ttu-id="dc410-134">Lorsqu’un point de données de télémétrie est passé procédé toohello, il effectue son travail, et puis appelle hello processeur télémétrie suivant dans la chaîne de hello.</span><span class="sxs-lookup"><span data-stu-id="dc410-134">When a telemetry data point is passed toohello Process method, it does its work and then calls hello next Telemetry Processor in hello chain.</span></span>

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
1. <span data-ttu-id="dc410-135">Insérez-la dans ApplicationInsights.config :</span><span class="sxs-lookup"><span data-stu-id="dc410-135">Insert this in ApplicationInsights.config:</span></span>

```XML

    <TelemetryProcessors>
      <Add Type="WebApplication9.SuccessfulDependencyFilter, WebApplication9">
         <!-- Set public property -->
         <MyParamFromConfigFile>2-beta</MyParamFromConfigFile>
      </Add>
    </TelemetryProcessors>

```

<span data-ttu-id="dc410-136">(Il s’agit de hello section même où vous initialisez un filtre d’échantillonnage.)</span><span class="sxs-lookup"><span data-stu-id="dc410-136">(This is hello same section where you initialize a sampling filter.)</span></span>

<span data-ttu-id="dc410-137">Vous pouvez passer des valeurs de chaîne à partir du fichier .config de hello en fournissant des propriétés nommées publiques dans votre classe.</span><span class="sxs-lookup"><span data-stu-id="dc410-137">You can pass string values from hello .config file by providing public named properties in your class.</span></span>

> [!WARNING]
> <span data-ttu-id="dc410-138">Nom de type hello toomatch et que les noms de propriété dans une classe de toohello du fichier .config hello et des noms de propriété dans le code hello prennent en charge.</span><span class="sxs-lookup"><span data-stu-id="dc410-138">Take care toomatch hello type name and any property names in hello .config file toohello class and property names in hello code.</span></span> <span data-ttu-id="dc410-139">Si le fichier .config de hello fait référence à un type inexistant ou une propriété, hello SDK en mode silencieux ne toosend toutes les données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="dc410-139">If hello .config file references a non-existent type or property, hello SDK may silently fail toosend any telemetry.</span></span>
>
>

<span data-ttu-id="dc410-140">**Vous pouvez également** vous pouvez initialiser filtre hello dans le code.</span><span class="sxs-lookup"><span data-stu-id="dc410-140">**Alternatively,** you can initialize hello filter in code.</span></span> <span data-ttu-id="dc410-141">Dans une classe de l’initialisation approprié - par exemple AppStart dans Global.asax.cs - insérer votre processeur dans la chaîne de hello :</span><span class="sxs-lookup"><span data-stu-id="dc410-141">In a suitable initialization class - for example AppStart in Global.asax.cs - insert your processor into hello chain:</span></span>

```C#

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;
    builder.Use((next) => new SuccessfulDependencyFilter(next));

    // If you have more processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="dc410-142">Les clients de télémétrie créés après ce point utiliseront vos processeurs.</span><span class="sxs-lookup"><span data-stu-id="dc410-142">TelemetryClients created after this point will use your processors.</span></span>

### <a name="example-filters"></a><span data-ttu-id="dc410-143">Exemples de filtres</span><span class="sxs-lookup"><span data-stu-id="dc410-143">Example filters</span></span>
#### <a name="synthetic-requests"></a><span data-ttu-id="dc410-144">Demandes synthétiques</span><span class="sxs-lookup"><span data-stu-id="dc410-144">Synthetic requests</span></span>
<span data-ttu-id="dc410-145">Excluez les robots et les tests web.</span><span class="sxs-lookup"><span data-stu-id="dc410-145">Filter out bots and web tests.</span></span> <span data-ttu-id="dc410-146">Bien que l’offre de Metrics Explorer vous hello toofilter option des sources synthétiques, cette option réduit le trafic en les filtrant à hello Kit de développement logiciel.</span><span class="sxs-lookup"><span data-stu-id="dc410-146">Although Metrics Explorer gives you hello option toofilter out synthetic sources, this option reduces traffic by filtering them at hello SDK.</span></span>

``` C#

    public void Process(ITelemetry item)
    {
      if (!string.IsNullOrEmpty(item.Context.Operation.SyntheticSource)) {return;}

      // Send everything else:
      this.Next.Process(item);
    }

```

#### <a name="failed-authentication"></a><span data-ttu-id="dc410-147">Échec d’authentification</span><span class="sxs-lookup"><span data-stu-id="dc410-147">Failed authentication</span></span>
<span data-ttu-id="dc410-148">Excluez les demandes avec une réponse de type « 401 ».</span><span class="sxs-lookup"><span data-stu-id="dc410-148">Filter out requests with a "401" response.</span></span>

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

#### <a name="filter-out-fast-remote-dependency-calls"></a><span data-ttu-id="dc410-149">Excluez les appels de dépendance à distance rapides.</span><span class="sxs-lookup"><span data-stu-id="dc410-149">Filter out fast remote dependency calls</span></span>
<span data-ttu-id="dc410-150">Si vous ne souhaitez que les appels de toodiagnose qui sont lentes, filtrer ceux d’accélérée hello.</span><span class="sxs-lookup"><span data-stu-id="dc410-150">If you only want toodiagnose calls that are slow, filter out hello fast ones.</span></span>

> [!NOTE]
> <span data-ttu-id="dc410-151">Cela ne fausse pas les statistiques hello que vous voyez sur le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="dc410-151">This will skew hello statistics you see on hello portal.</span></span> <span data-ttu-id="dc410-152">graphique de dépendance Hello aura l’aspect des appels de dépendance hello sont tous les échecs.</span><span class="sxs-lookup"><span data-stu-id="dc410-152">hello dependency chart will look as if hello dependency calls are all failures.</span></span>
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

#### <a name="diagnose-dependency-issues"></a><span data-ttu-id="dc410-153">Diagnostiquer les problèmes de dépendance</span><span class="sxs-lookup"><span data-stu-id="dc410-153">Diagnose dependency issues</span></span>
<span data-ttu-id="dc410-154">[Ce billet de blog](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) décrit un problèmes de dépendance de projet toodiagnose en envoyant des commandes ping régulière toodependencies automatiquement.</span><span class="sxs-lookup"><span data-stu-id="dc410-154">[This blog](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) describes a project toodiagnose dependency issues by automatically sending regular pings toodependencies.</span></span>


<a name="add-properties"></a>

## <a name="add-properties-itelemetryinitializer"></a><span data-ttu-id="dc410-155">Ajouter des propriétés : ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="dc410-155">Add properties: ITelemetryInitializer</span></span>
<span data-ttu-id="dc410-156">Utiliser des données de télémétrie initialiseurs toodefine propriétés globales qui sont envoyées avec toutes les données de télémétrie ; et le comportement de toooverride sélectionné des modules de télémétrie standard hello.</span><span class="sxs-lookup"><span data-stu-id="dc410-156">Use telemetry initializers toodefine global properties that are sent with all telemetry; and toooverride selected behavior of hello standard telemetry modules.</span></span>

<span data-ttu-id="dc410-157">Par exemple, hello Application Insights pour le package Web collecte une télémétrie sur les requêtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="dc410-157">For example, hello Application Insights for Web package collects telemetry about HTTP requests.</span></span> <span data-ttu-id="dc410-158">Il indique par défaut l’échec de toute requête à l’aide d’un code de réponse supérieur ou égal à 400.</span><span class="sxs-lookup"><span data-stu-id="dc410-158">By default, it flags as failed any request with a response code >= 400.</span></span> <span data-ttu-id="dc410-159">Mais si vous souhaitez tootreat 400 comme un succès, vous pouvez fournir un initialiseur de télémétrie qui définit la propriété de réussite hello.</span><span class="sxs-lookup"><span data-stu-id="dc410-159">But if you want tootreat 400 as a success, you can provide a telemetry initializer that sets hello Success property.</span></span>

<span data-ttu-id="dc410-160">Si vous fournissez un initialiseur de télémétrie, elle est appelée chaque fois qu’un des hello Track*() méthodes est appelée.</span><span class="sxs-lookup"><span data-stu-id="dc410-160">If you provide a telemetry initializer, it is called whenever any of hello Track*() methods is called.</span></span> <span data-ttu-id="dc410-161">Cela inclut les méthodes appelées par les modules de télémétrie standard hello.</span><span class="sxs-lookup"><span data-stu-id="dc410-161">This includes methods called by hello standard telemetry modules.</span></span> <span data-ttu-id="dc410-162">Par convention, ces modules ne définissent aucune propriété déjà définie par un initialiseur.</span><span class="sxs-lookup"><span data-stu-id="dc410-162">By convention, these modules do not set any property that has already been set by an initializer.</span></span>

<span data-ttu-id="dc410-163">**Définir votre initialiseur**</span><span class="sxs-lookup"><span data-stu-id="dc410-163">**Define your initializer**</span></span>

<span data-ttu-id="dc410-164">*C#*</span><span class="sxs-lookup"><span data-stu-id="dc410-164">*C#*</span></span>

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

<span data-ttu-id="dc410-165">**Charger votre initialiseur**</span><span class="sxs-lookup"><span data-stu-id="dc410-165">**Load your initializer**</span></span>

<span data-ttu-id="dc410-166">Dans ApplicationInsights.config :</span><span class="sxs-lookup"><span data-stu-id="dc410-166">In ApplicationInsights.config:</span></span>

    <ApplicationInsights>
      <TelemetryInitializers>
        <!-- Fully qualified type name, assembly name: -->
        <Add Type="MvcWebRole.Telemetry.MyTelemetryInitializer, MvcWebRole"/>
        ...
      </TelemetryInitializers>
    </ApplicationInsights>

<span data-ttu-id="dc410-167">*Vous pouvez également* vous pouvez instancier initialiseur hello dans le code, par exemple dans Global.aspx.cs :</span><span class="sxs-lookup"><span data-stu-id="dc410-167">*Alternatively,* you can instantiate hello initializer in code, for example in Global.aspx.cs:</span></span>

```C#
    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```


[<span data-ttu-id="dc410-168">Voir l’intégralité de cet exemple.</span><span class="sxs-lookup"><span data-stu-id="dc410-168">See more of this sample.</span></span>](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/MvcWebRole)

<a name="js-initializer"></a>

### <a name="javascript-telemetry-initializers"></a><span data-ttu-id="dc410-169">Initialiseurs de télémétrie JavaScript</span><span class="sxs-lookup"><span data-stu-id="dc410-169">JavaScript telemetry initializers</span></span>
<span data-ttu-id="dc410-170">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="dc410-170">*JavaScript*</span></span>

<span data-ttu-id="dc410-171">Insérer un initialiseur de télémétrie immédiatement après le code d’initialisation hello que vous avez obtenu à partir du portail de hello :</span><span class="sxs-lookup"><span data-stu-id="dc410-171">Insert a telemetry initializer immediately after hello initialization code that you got from hello portal:</span></span>

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

<span data-ttu-id="dc410-172">Pour obtenir un résumé des propriétés de non-custom hello disponibles sur hello telemetryItem, consultez [modèle exporter des données d’Application Insights](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="dc410-172">For a summary of hello non-custom properties available on hello telemetryItem, see [Application Insights Export Data Model](app-insights-export-data-model.md).</span></span>

<span data-ttu-id="dc410-173">Vous pouvez ajouter autant d'initialiseurs que vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="dc410-173">You can add as many initializers as you like.</span></span>

## <a name="itelemetryprocessor-and-itelemetryinitializer"></a><span data-ttu-id="dc410-174">ITelemetryProcessor et ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="dc410-174">ITelemetryProcessor and ITelemetryInitializer</span></span>
<span data-ttu-id="dc410-175">Qu’est la différence de hello entre les processeurs de télémétrie et les initialiseurs de télémétrie ?</span><span class="sxs-lookup"><span data-stu-id="dc410-175">What's hello difference between telemetry processors and telemetry initializers?</span></span>

* <span data-ttu-id="dc410-176">Il existe des chevauchements dans ce que vous pouvez faire avec eux : les deux peuvent être utilisés tooadd propriétés tootelemetry.</span><span class="sxs-lookup"><span data-stu-id="dc410-176">There are some overlaps in what you can do with them: both can be used tooadd properties tootelemetry.</span></span>
* <span data-ttu-id="dc410-177">Les TelemetryInitializers sont toujours exécutés avant les TelemetryProcessors.</span><span class="sxs-lookup"><span data-stu-id="dc410-177">TelemetryInitializers always run before TelemetryProcessors.</span></span>
* <span data-ttu-id="dc410-178">TelemetryProcessors permettent toocompletely remplacer ou ignorer un élément de données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="dc410-178">TelemetryProcessors allow you toocompletely replace or discard a telemetry item.</span></span>
* <span data-ttu-id="dc410-179">Les TelemetryProcessors ne traitent pas la télémétrie du compteur de performances.</span><span class="sxs-lookup"><span data-stu-id="dc410-179">TelemetryProcessors don't process performance counter telemetry.</span></span>


## <a name="reference-docs"></a><span data-ttu-id="dc410-180">Documents de référence</span><span class="sxs-lookup"><span data-stu-id="dc410-180">Reference docs</span></span>
* [<span data-ttu-id="dc410-181">Présentation de l’API</span><span class="sxs-lookup"><span data-stu-id="dc410-181">API Overview</span></span>](app-insights-api-custom-events-metrics.md)
* [<span data-ttu-id="dc410-182">Référence ASP.NET</span><span class="sxs-lookup"><span data-stu-id="dc410-182">ASP.NET reference</span></span>](https://msdn.microsoft.com/library/dn817570.aspx)

## <a name="sdk-code"></a><span data-ttu-id="dc410-183">Code du Kit de développement logiciel (SDK)</span><span class="sxs-lookup"><span data-stu-id="dc410-183">SDK Code</span></span>
* [<span data-ttu-id="dc410-184">Kit de développement logiciel (SDK) principal ASP.NET</span><span class="sxs-lookup"><span data-stu-id="dc410-184">ASP.NET Core SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [<span data-ttu-id="dc410-185">ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="dc410-185">ASP.NET 5</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [<span data-ttu-id="dc410-186">Kit de développement logiciel (SDK) JavaScript</span><span class="sxs-lookup"><span data-stu-id="dc410-186">JavaScript SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-JS)

## <span data-ttu-id="dc410-187"><a name="next"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dc410-187"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="dc410-188">Recherche d’événements et de journaux</span><span class="sxs-lookup"><span data-stu-id="dc410-188">Search events and logs</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="dc410-189">Échantillonnage</span><span class="sxs-lookup"><span data-stu-id="dc410-189">Sampling</span></span>](app-insights-sampling.md)
* [<span data-ttu-id="dc410-190">Dépannage</span><span class="sxs-lookup"><span data-stu-id="dc410-190">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)
