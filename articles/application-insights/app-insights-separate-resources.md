---
title: "Séparation des télémétries de développement, de test et de publication dans Azure Application Insights | Documents Microsoft"
description: "Télémétrie directe de différentes ressources pour les tampons de développement, de test et de production."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 578e30f0-31ed-4f39-baa8-01b4c2f310c9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: f51fa4639aaa60686cc349683713c6e5f9732bb9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="separating-telemetry-from-development-test-and-production"></a><span data-ttu-id="3ce26-103">Séparation des télémétries de développement, de test et de production</span><span class="sxs-lookup"><span data-stu-id="3ce26-103">Separating telemetry from Development, Test, and Production</span></span>

<span data-ttu-id="3ce26-104">Lorsque vous développez la prochaine version d’une application web, vous ne souhaitez pas mélanger les télémétries [Application Insights](app-insights-overview.md) de la nouvelle version et de la version déjà publiée.</span><span class="sxs-lookup"><span data-stu-id="3ce26-104">When you are developing the next version of a web application, you don't want to mix up the [Application Insights](app-insights-overview.md) telemetry from the new version and the already released version.</span></span> <span data-ttu-id="3ce26-105">Pour éviter toute confusion, envoyez la télémétrie des différentes phases de développement à des ressources Application Insights séparées, avec des clés d’instrumentation (ikeys) distinctes.</span><span class="sxs-lookup"><span data-stu-id="3ce26-105">To avoid confusion, send the telemetry from different development stages to separate Application Insights resources, with separate instrumentation keys (ikeys).</span></span> <span data-ttu-id="3ce26-106">Pour faciliter la modification de la clé d’instrumentation à mesure qu’une version passe d’une étape à l’autre, il peut être utile de définir l’ikey dans le code plutôt que dans le fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="3ce26-106">To make it easier to change the instrumentation key as a version moves from one stage to another, it can be useful to set the ikey in code instead of in the configuration file.</span></span> 

<span data-ttu-id="3ce26-107">(Si votre système est un service cloud Azure, il existe [une autre méthode pour configurer des iKeys distinctes](app-insights-cloudservices.md).)</span><span class="sxs-lookup"><span data-stu-id="3ce26-107">(If your system is an Azure Cloud Service, there's [another method of setting separate ikeys](app-insights-cloudservices.md).)</span></span>

## <a name="about-resources-and-instrumentation-keys"></a><span data-ttu-id="3ce26-108">À propos des ressources et des clés d’instrumentation</span><span class="sxs-lookup"><span data-stu-id="3ce26-108">About resources and instrumentation keys</span></span>

<span data-ttu-id="3ce26-109">Lorsque vous définissez un suivi Application Insights pour votre application web, vous créez une *ressource* Application Insights dans Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="3ce26-109">When you set up Application Insights monitoring for your web app, you create an Application Insights *resource* in Microsoft Azure.</span></span> <span data-ttu-id="3ce26-110">Vous ouvrez cette ressource dans le portail Azure pour afficher et analyser la télémétrie recueillie à partir de votre application.</span><span class="sxs-lookup"><span data-stu-id="3ce26-110">You open this resource in the Azure portal in order to see and analyze the telemetry collected from your app.</span></span> <span data-ttu-id="3ce26-111">Chaque ressource est identifiée par une *clé d’instrumentation* (iKey).</span><span class="sxs-lookup"><span data-stu-id="3ce26-111">The resource is identified by an *instrumentation key* (ikey).</span></span> <span data-ttu-id="3ce26-112">Lorsque vous installez le package Application Insights pour surveiller votre application, vous le configurez avec la clé d’instrumentation afin qu’il sache où envoyer la télémétrie.</span><span class="sxs-lookup"><span data-stu-id="3ce26-112">When you install the Application Insights package to monitor your app, you configure it with the instrumentation key, so that it knows where to send the telemetry.</span></span>

<span data-ttu-id="3ce26-113">En général, vous choisissez d’utiliser des ressources séparées ou une ressource partagée unique dans différents scénarios :</span><span class="sxs-lookup"><span data-stu-id="3ce26-113">You typically choose to use separate resources or a single shared resource in different scenarios:</span></span>

* <span data-ttu-id="3ce26-114">Applications différentes, indépendantes : utilisez une ressource et une ikey séparées pour chaque application.</span><span class="sxs-lookup"><span data-stu-id="3ce26-114">Different, independent applications - Use a separate resource and ikey for each app.</span></span>
* <span data-ttu-id="3ce26-115">Plusieurs composants ou rôles d’une application métier : utilisez une [ressource partagée unique](app-insights-monitor-multi-role-apps.md) pour toutes les applications de composant.</span><span class="sxs-lookup"><span data-stu-id="3ce26-115">Multiple components or roles of one business application - Use a [single shared resource](app-insights-monitor-multi-role-apps.md) for all the component apps.</span></span> <span data-ttu-id="3ce26-116">La télémétrie peut être filtrée ou segmentée par la propriété cloud_RoleName.</span><span class="sxs-lookup"><span data-stu-id="3ce26-116">Telemetry can be filtered or segmented by the cloud_RoleName property.</span></span>
* <span data-ttu-id="3ce26-117">Développement, test et publication : utilisez une ressource et une ikey séparées pour les versions du système en « tampon » ou phase de production.</span><span class="sxs-lookup"><span data-stu-id="3ce26-117">Development, Test, and Release - Use a separate resource and ikey for versions of the system in 'stamp' or stage of production.</span></span>
* <span data-ttu-id="3ce26-118">Test A | B : utilisez une seule ressource.</span><span class="sxs-lookup"><span data-stu-id="3ce26-118">A | B testing - Use a single resource.</span></span> <span data-ttu-id="3ce26-119">Créez un TelemetryInitializer pour ajouter une propriété à la télémétrie, qui identifie les variantes.</span><span class="sxs-lookup"><span data-stu-id="3ce26-119">Create a TelemetryInitializer to add a property to the telemetry that identifies the variants.</span></span>


## <span data-ttu-id="3ce26-120"><a name="dynamic-ikey"></a> Clé d'instrumentation dynamique</span><span class="sxs-lookup"><span data-stu-id="3ce26-120"><a name="dynamic-ikey"></a> Dynamic instrumentation key</span></span>

<span data-ttu-id="3ce26-121">Pour faciliter la modification de l’ikey à mesure que le code se déplace entre les phases de production, définissez-la dans le code plutôt que dans le fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="3ce26-121">To make it easier to change the ikey as the code moves between stages of production, set it in code instead of in the configuration file.</span></span>

<span data-ttu-id="3ce26-122">Définissez la clé dans une méthode d'initialisation, par exemple global.aspx.cs dans un service ASP.NET :</span><span class="sxs-lookup"><span data-stu-id="3ce26-122">Set the key in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

<span data-ttu-id="3ce26-123">*C#*</span><span class="sxs-lookup"><span data-stu-id="3ce26-123">*C#*</span></span>

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey = 
          // - for example -
          WebConfigurationManager.AppSettings["ikey"];
      ...

<span data-ttu-id="3ce26-124">Dans cet exemple, les ikeys des différentes ressources sont placées dans différentes versions du fichier de configuration web.</span><span class="sxs-lookup"><span data-stu-id="3ce26-124">In this example, the ikeys for the different resources are placed in different versions of the web configuration file.</span></span> <span data-ttu-id="3ce26-125">Le remplacement du fichier de configuration web, que vous pouvez effectuer dans le cadre du script de lancement, remplacera la ressource cible.</span><span class="sxs-lookup"><span data-stu-id="3ce26-125">Swapping the web configuration file - which you can do as part of the release script - will swap the target resource.</span></span>

### <a name="web-pages"></a><span data-ttu-id="3ce26-126">Pages web</span><span class="sxs-lookup"><span data-stu-id="3ce26-126">Web pages</span></span>
<span data-ttu-id="3ce26-127">L'iKey est également utilisée dans les pages web de votre application, dans le [script que vous avez obtenu à partir du panneau de démarrage rapide](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="3ce26-127">The iKey is also used in your app's web pages, in the [script that you got from the quick start blade](app-insights-javascript.md).</span></span> <span data-ttu-id="3ce26-128">Au lieu de la coder littéralement dans le script, vous devez la générer à partir de l'état du serveur.</span><span class="sxs-lookup"><span data-stu-id="3ce26-128">Instead of coding it literally into the script, generate it from the server state.</span></span> <span data-ttu-id="3ce26-129">Par exemple, dans une application ASP.NET :</span><span class="sxs-lookup"><span data-stu-id="3ce26-129">For example, in an ASP.NET app:</span></span>

<span data-ttu-id="3ce26-130">*JavaScript dans Razor*</span><span class="sxs-lookup"><span data-stu-id="3ce26-130">*JavaScript in Razor*</span></span>

    <script type="text/javascript">
    // Standard Application Insights web page script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      "@Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="create-additional-application-insights-resources"></a><span data-ttu-id="3ce26-131">Créer des ressource Application Insights supplémentaires</span><span class="sxs-lookup"><span data-stu-id="3ce26-131">Create additional Application Insights resources</span></span>
<span data-ttu-id="3ce26-132">Pour séparer la télémétrie de différents composants d’applications ou de différents tampons (développement/test/production) du même composant, vous devez créer une ressource Application Insights.</span><span class="sxs-lookup"><span data-stu-id="3ce26-132">To separate telemetry for different application components, or for different stamps (dev/test/production) of the same component, then you'll have to create a new Application Insights resource.</span></span>

<span data-ttu-id="3ce26-133">Dans le portail [portal.azure.com](https://portal.azure.com), ajoutez une ressource Application Insights :</span><span class="sxs-lookup"><span data-stu-id="3ce26-133">In the [portal.azure.com](https://portal.azure.com), add an Application Insights resource:</span></span>

![Cliquez sur Nouveau > Application Insights](./media/app-insights-separate-resources/01-new.png)

* <span data-ttu-id="3ce26-135">**type d’application** définit le contenu du panneau de présentation et les propriétés disponibles dans [Metrics Explorer](app-insights-metrics-explorer.md)Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="3ce26-135">**Application type** affects what you see on the overview blade and the properties available in [metric explorer](app-insights-metrics-explorer.md).</span></span> <span data-ttu-id="3ce26-136">Si vous ne voyez pas votre type d’application, choisissez un des types web pour les pages web.</span><span class="sxs-lookup"><span data-stu-id="3ce26-136">If you don't see your type of app, choose one of the web types for web pages.</span></span>
* <span data-ttu-id="3ce26-137">**Groupe de ressources** facilite la gestion des propriétés telles que le [contrôle d’accès](app-insights-resources-roles-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="3ce26-137">**Resource group** is a convenience for managing properties like [access control](app-insights-resources-roles-access-control.md).</span></span> <span data-ttu-id="3ce26-138">Vous pouvez utiliser des groupes de ressources distincts pour le développement, le test et la production.</span><span class="sxs-lookup"><span data-stu-id="3ce26-138">You could use separate resource groups for development, test, and production.</span></span>
* <span data-ttu-id="3ce26-139">**Abonnement** est votre compte de paiement dans Azure.</span><span class="sxs-lookup"><span data-stu-id="3ce26-139">**Subscription** is your payment account in Azure.</span></span>
* <span data-ttu-id="3ce26-140">**Emplacement** correspond à l’endroit où nous conservons vos données.</span><span class="sxs-lookup"><span data-stu-id="3ce26-140">**Location** is where we keep your data.</span></span> <span data-ttu-id="3ce26-141">Actuellement, il n’est pas possible de le modifier.</span><span class="sxs-lookup"><span data-stu-id="3ce26-141">Currently it can't be changed.</span></span> 
* <span data-ttu-id="3ce26-142">**Ajouter au tableau de bord** place une vignette d’accès rapide à votre ressource sur votre page d’accueil Azure.</span><span class="sxs-lookup"><span data-stu-id="3ce26-142">**Add to dashboard** puts a quick-access tile for your resource on your Azure Home page.</span></span> 

<span data-ttu-id="3ce26-143">La création de la ressource prend quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="3ce26-143">Creating the resource takes a few seconds.</span></span> <span data-ttu-id="3ce26-144">Une alerte vous prévient lorsque l’opération est terminée.</span><span class="sxs-lookup"><span data-stu-id="3ce26-144">You'll see an alert when it's done.</span></span>

<span data-ttu-id="3ce26-145">(Vous pouvez écrire un [script PowerShell](app-insights-powershell-script-create-resource.md) pour créer automatiquement une ressource.)</span><span class="sxs-lookup"><span data-stu-id="3ce26-145">(You can write a [PowerShell script](app-insights-powershell-script-create-resource.md) to create a resource automatically.)</span></span>

### <a name="getting-the-instrumentation-key"></a><span data-ttu-id="3ce26-146">Récupération de la clé d’instrumentation</span><span class="sxs-lookup"><span data-stu-id="3ce26-146">Getting the instrumentation key</span></span>
<span data-ttu-id="3ce26-147">La clé d'instrumentation identifie la ressource que vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="3ce26-147">The instrumentation key identifies the resource that you created.</span></span> 

![Cliquez sur Essentials, sur la clé d'instrumentation, puis appuyez sur CTRL+C](./media/app-insights-separate-resources/02-props.png)

<span data-ttu-id="3ce26-149">Vous avez besoin des clés d’instrumentation de toutes les ressources auxquelles votre application envoie des données.</span><span class="sxs-lookup"><span data-stu-id="3ce26-149">You need the instrumentation keys of all the resources to which your app will send data.</span></span>

## <a name="filter-on-build-number"></a><span data-ttu-id="3ce26-150">Filtrer sur le numéro de build</span><span class="sxs-lookup"><span data-stu-id="3ce26-150">Filter on build number</span></span>
<span data-ttu-id="3ce26-151">Quand vous publiez une nouvelle version de votre application, vous voulez pouvoir distinguer la télémétrie des différentes builds.</span><span class="sxs-lookup"><span data-stu-id="3ce26-151">When you publish a new version of your app, you'll want to be able to separate the telemetry from different builds.</span></span>

<span data-ttu-id="3ce26-152">Vous pouvez définir la propriété Version de l’application pour filtrer les résultats de [recherche](app-insights-diagnostic-search.md) et de [Metrics Explorer](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="3ce26-152">You can set the Application Version property so that you can filter [search](app-insights-diagnostic-search.md) and [metric explorer](app-insights-metrics-explorer.md) results.</span></span>

![Filtrage sur une propriété](./media/app-insights-separate-resources/050-filter.png)

<span data-ttu-id="3ce26-154">Il existe plusieurs méthodes de définition de la propriété Version de l’application.</span><span class="sxs-lookup"><span data-stu-id="3ce26-154">There are several different methods of setting the Application Version property.</span></span>

* <span data-ttu-id="3ce26-155">Définissez directement :</span><span class="sxs-lookup"><span data-stu-id="3ce26-155">Set directly:</span></span>

    `telemetryClient.Context.Component.Version = typeof(MyProject.MyClass).Assembly.GetName().Version;`
* <span data-ttu-id="3ce26-156">Encapsulez cette ligne dans un [initialiseur de télémétrie](app-insights-api-custom-events-metrics.md#defaults) pour vous assurer que toutes les instances de TelemetryClient sont définies de manière cohérente.</span><span class="sxs-lookup"><span data-stu-id="3ce26-156">Wrap that line in a [telemetry initializer](app-insights-api-custom-events-metrics.md#defaults) to ensure that all TelemetryClient instances are set consistently.</span></span>
* <span data-ttu-id="3ce26-157">[ASP.NET] Définissez la version dans `BuildInfo.config`.</span><span class="sxs-lookup"><span data-stu-id="3ce26-157">[ASP.NET] Set the version in `BuildInfo.config`.</span></span> <span data-ttu-id="3ce26-158">Le module web sélectionnera la version dans le nœud BuildLabel.</span><span class="sxs-lookup"><span data-stu-id="3ce26-158">The web module will pick up the version from the BuildLabel node.</span></span> <span data-ttu-id="3ce26-159">Incluez ce fichier dans votre projet et n’oubliez pas de définir la propriété Toujours copier dans l’Explorateur de solutions.</span><span class="sxs-lookup"><span data-stu-id="3ce26-159">Include this file in your project and remember to set the Copy Always property in Solution Explorer.</span></span>

    ```XML

    <?xml version="1.0" encoding="utf-8"?>
    <DeploymentEvent xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/VisualStudio/DeploymentEvent/2013/06">
      <ProjectName>AppVersionExpt</ProjectName>
      <Build type="MSBuild">
        <MSBuild>
          <BuildLabel kind="label">1.0.0.2</BuildLabel>
        </MSBuild>
      </Build>
    </DeploymentEvent>

    ```
* <span data-ttu-id="3ce26-160">[ASP.NET] Générez automatiquement BuildInfo.config dans MSBuild.</span><span class="sxs-lookup"><span data-stu-id="3ce26-160">[ASP.NET] Generate BuildInfo.config automatically in MSBuild.</span></span> <span data-ttu-id="3ce26-161">Pour ce faire, ajoutez quelques lignes à votre fichier `.csproj` :</span><span class="sxs-lookup"><span data-stu-id="3ce26-161">To do this, add a few lines to your `.csproj` file:</span></span>

    ```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
    ```

    <span data-ttu-id="3ce26-162">Cela génère un fichier appelé *Votre_nom_de_projet*.BuildInfo.config. Le processus de publication le renomme en BuildInfo.config.</span><span class="sxs-lookup"><span data-stu-id="3ce26-162">This generates a file called *yourProjectName*.BuildInfo.config. The Publish process renames it to BuildInfo.config.</span></span>

    <span data-ttu-id="3ce26-163">L’étiquette de build contient un espace réservé (AutoGen_...) quand vous effectuez la génération avec Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3ce26-163">The build label contains a placeholder (AutoGen_...) when you build with Visual Studio.</span></span> <span data-ttu-id="3ce26-164">Mais quand vous utilisez MSBuild, l’espace réservé est remplacé par le numéro de version correct.</span><span class="sxs-lookup"><span data-stu-id="3ce26-164">But when built with MSBuild, it is populated with the correct version number.</span></span>

    <span data-ttu-id="3ce26-165">Pour permettre à MSBuild de générer des numéros de version, définissez la version comme `1.0.*` dans AssemblyReference.cs</span><span class="sxs-lookup"><span data-stu-id="3ce26-165">To allow MSBuild to generate version numbers, set the version like `1.0.*` in AssemblyReference.cs</span></span>

## <a name="version-and-release-tracking"></a><span data-ttu-id="3ce26-166">Suivi de la version</span><span class="sxs-lookup"><span data-stu-id="3ce26-166">Version and release tracking</span></span>
<span data-ttu-id="3ce26-167">Pour vérifier la version de l’application, assurez-vous que `buildinfo.config` est généré par votre processus Microsoft Build Engine.</span><span class="sxs-lookup"><span data-stu-id="3ce26-167">To track the application version, make sure `buildinfo.config` is generated by your Microsoft Build Engine process.</span></span> <span data-ttu-id="3ce26-168">Dans votre fichier .csproj, ajoutez :</span><span class="sxs-lookup"><span data-stu-id="3ce26-168">In your .csproj file, add:</span></span>  

```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
```

<span data-ttu-id="3ce26-169">Quand il détient les informations de version, le module web Application Insights ajoute automatiquement la **version de l’application** en tant que propriété à chaque élément de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="3ce26-169">When it has the build info, the Application Insights web module automatically adds **Application version** as a property to every item of telemetry.</span></span> <span data-ttu-id="3ce26-170">Cela vous permet de filtrer par version lorsque vous effectuez des [recherches de diagnostic](app-insights-diagnostic-search.md) ou que vous [explorez les métriques](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="3ce26-170">That allows you to filter by version when you perform [diagnostic searches](app-insights-diagnostic-search.md), or when you [explore metrics](app-insights-metrics-explorer.md).</span></span>

<span data-ttu-id="3ce26-171">Toutefois, notez que le numéro de version de build est uniquement généré par Microsoft Build Engine, et non par la build de développement dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3ce26-171">However, notice that the build version number is generated only by the Microsoft Build Engine, not by the developer build in Visual Studio.</span></span>

### <a name="release-annotations"></a><span data-ttu-id="3ce26-172">Annotations de version</span><span class="sxs-lookup"><span data-stu-id="3ce26-172">Release annotations</span></span>
<span data-ttu-id="3ce26-173">Si vous utilisez Visual Studio Team Services, vous pouvez [obtenir un marqueur d’annotation](app-insights-annotations.md) ajouté à vos graphiques lorsque vous publiez une nouvelle version.</span><span class="sxs-lookup"><span data-stu-id="3ce26-173">If you use Visual Studio Team Services, you can [get an annotation marker](app-insights-annotations.md) added to your charts whenever you release a new version.</span></span> <span data-ttu-id="3ce26-174">L’illustration suivante montre l’aspect de ce marqueur.</span><span class="sxs-lookup"><span data-stu-id="3ce26-174">The following image shows how this marker appears.</span></span>

![Capture d’écran d’un exemple d’annotation de version sur un graphique](./media/app-insights-asp-net/release-annotation.png)
## <a name="next-steps"></a><span data-ttu-id="3ce26-176">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3ce26-176">Next steps</span></span>

* [<span data-ttu-id="3ce26-177">Ressources partagées pour plusieurs rôles</span><span class="sxs-lookup"><span data-stu-id="3ce26-177">Shared resources for multiple roles</span></span>](app-insights-monitor-multi-role-apps.md)
* [<span data-ttu-id="3ce26-178">Créer un initialiseur de télémétrie pour distinguer des variantes A|B</span><span class="sxs-lookup"><span data-stu-id="3ce26-178">Create a Telemetry Initializer to distinguish A|B variants</span></span>](app-insights-api-filtering-sampling.md#add-properties)
