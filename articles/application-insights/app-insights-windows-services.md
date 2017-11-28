---
title: "rôles serveur et de travail d’Application Insights pour Windows aaaAzure | Documents Microsoft"
description: "Ajouter manuellement des performances, la disponibilité et l’utilisation des hello Application Insights SDK tooyour ASP.NET applications tooanalyze."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 106ba99b-b57a-43b8-8866-e02f626c8190
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: 64643ef637195d10f87fc6020a77169bca66c1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manually-configure-application-insights-for-net-applications"></a><span data-ttu-id="e5be0-103">Configurer manuellement Application Insights pour des applications .NET</span><span class="sxs-lookup"><span data-stu-id="e5be0-103">Manually configure Application Insights for .NET applications</span></span>

<span data-ttu-id="e5be0-104">Vous pouvez configurer [Application Insights](app-insights-overview.md) toomonitor une grande variété d’applications ou les rôles d’application, les composants ou microservices.</span><span class="sxs-lookup"><span data-stu-id="e5be0-104">You can configure [Application Insights](app-insights-overview.md) toomonitor a wide variety of applications or application roles, components, or microservices.</span></span> <span data-ttu-id="e5be0-105">Pour les services et applications web, Visual Studio permet un [configuration en une seule étape](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="e5be0-105">For web apps and services, Visual Studio offers [one-step configuration](app-insights-asp-net.md).</span></span> <span data-ttu-id="e5be0-106">Pour les autres types d’application .NET, telles que les rôles de serveur principal ou les applications de bureau, vous pouvez configurer Application Insights manuellement.</span><span class="sxs-lookup"><span data-stu-id="e5be0-106">For other types of .NET application, such as backend server roles or desktop applications, you can configure Application Insights manually.</span></span>

![Exemples de graphiques d’analyse des performances](./media/app-insights-windows-services/10-perf.png)

#### <a name="before-you-start"></a><span data-ttu-id="e5be0-108">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="e5be0-108">Before you start</span></span>

<span data-ttu-id="e5be0-109">Ce dont vous avez besoin :</span><span class="sxs-lookup"><span data-stu-id="e5be0-109">You need:</span></span>

* <span data-ttu-id="e5be0-110">Un abonnement trop[Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="e5be0-110">A subscription too[Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="e5be0-111">Si votre équipe ou organisation dispose d’un abonnement Azure, propriétaire de hello vous pouvez ajouter des tooit, à l’aide de votre [compte Microsoft](http://live.com).</span><span class="sxs-lookup"><span data-stu-id="e5be0-111">If your team or organization has an Azure subscription, hello owner can add you tooit, using your [Microsoft account](http://live.com).</span></span>
* <span data-ttu-id="e5be0-112">Visual Studio 2013 ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="e5be0-112">Visual Studio 2013 or later.</span></span>

## <span data-ttu-id="e5be0-113"><a name="add"></a>1. Choix d’une ressource Application Insights</span><span class="sxs-lookup"><span data-stu-id="e5be0-113"><a name="add"></a>1. Choose an Application Insights resource</span></span>

<span data-ttu-id="e5be0-114">Hello « ressource » est où vos données sont collectées et affichées dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e5be0-114">hello 'resource' is where your data is collected and displayed in hello Azure portal.</span></span> <span data-ttu-id="e5be0-115">Vous devez toodecide si toocreate un, ou partager un existant.</span><span class="sxs-lookup"><span data-stu-id="e5be0-115">You need toodecide whether toocreate a new one, or share an existing one.</span></span>

### <a name="part-of-a-larger-app-use-existing-resource"></a><span data-ttu-id="e5be0-116">Partie d’une application plus volumineuse : utiliser des ressources existantes</span><span class="sxs-lookup"><span data-stu-id="e5be0-116">Part of a larger app: Use existing resource</span></span>

<span data-ttu-id="e5be0-117">Si votre application web comporte plusieurs composants - par exemple, une application web frontal et un ou plusieurs services back-end - puis doit envoyer la télémétrie toohello de composants hello tous les mêmes ressources.</span><span class="sxs-lookup"><span data-stu-id="e5be0-117">If your web application has several components - for example, a front-end web app and one or more back-end services - then you should send telemetry from all hello components toohello same resource.</span></span> <span data-ttu-id="e5be0-118">Cela active les toobe affichée sur un seul mappage d’Application et rendre possible tootrace une demande à partir d’un composant tooanother.</span><span class="sxs-lookup"><span data-stu-id="e5be0-118">This will enable them toobe displayed on a single Application Map, and make it possible tootrace a request from one component tooanother.</span></span>

<span data-ttu-id="e5be0-119">Par conséquent, si vous êtes déjà analyse des autres composants de cette application, puis utilisez simplement hello même ressource.</span><span class="sxs-lookup"><span data-stu-id="e5be0-119">So, if you're already monitoring other components of this app, then just use hello same resource.</span></span>

<span data-ttu-id="e5be0-120">Ouvrir la ressource de hello Bonjour [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e5be0-120">Open hello resource in hello [Azure portal](https://portal.azure.com/).</span></span> 

### <a name="self-contained-app-create-a-new-resource"></a><span data-ttu-id="e5be0-121">Application autonome : créer une nouvelle ressource</span><span class="sxs-lookup"><span data-stu-id="e5be0-121">Self-contained app: Create a new resource</span></span>

<span data-ttu-id="e5be0-122">Si les applications non liées tooother n’est hello nouvelle application, il doit avoir sa propre ressource.</span><span class="sxs-lookup"><span data-stu-id="e5be0-122">If hello new app is unrelated tooother applications, then it should have its own resource.</span></span>

<span data-ttu-id="e5be0-123">Connectez-vous à toohello [portail Azure](https://portal.azure.com/)et créer une nouvelle ressource Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e5be0-123">Sign in toohello [Azure portal](https://portal.azure.com/), and create a new Application Insights resource.</span></span> <span data-ttu-id="e5be0-124">Choisissez ASP.NET en tant que type de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="e5be0-124">Choose ASP.NET as hello application type.</span></span>

![Cliquez sur Nouveau > Application Insights](./media/app-insights-windows-services/01-new-asp.png)

<span data-ttu-id="e5be0-126">choix de Hello du type d’application définit le contenu par défaut hello de panneaux de ressource hello.</span><span class="sxs-lookup"><span data-stu-id="e5be0-126">hello choice of application type sets hello default content of hello resource blades.</span></span>

## <a name="2-copy-hello-instrumentation-key"></a><span data-ttu-id="e5be0-127">2. Copiez la clé d’Instrumentation de hello</span><span class="sxs-lookup"><span data-stu-id="e5be0-127">2. Copy hello Instrumentation Key</span></span>
<span data-ttu-id="e5be0-128">clé de Hello identifie les ressources hello.</span><span class="sxs-lookup"><span data-stu-id="e5be0-128">hello key identifies hello resource.</span></span> <span data-ttu-id="e5be0-129">Vous allez l’installer dès Bonjour SDK, dans la ressource de toohello commande toodirect données.</span><span class="sxs-lookup"><span data-stu-id="e5be0-129">You'll install it soon in hello SDK, in order toodirect data toohello resource.</span></span>

![Cliquez sur Propriétés, sélectionnez la clé de hello et appuyez sur ctrl + C](./media/app-insights-windows-services/02-props-asp.png)

## <span data-ttu-id="e5be0-131"><a name="sdk"></a>3. Installer le package d’Application Insights hello dans votre application</span><span class="sxs-lookup"><span data-stu-id="e5be0-131"><a name="sdk"></a>3. Install hello Application Insights package in your application</span></span>
<span data-ttu-id="e5be0-132">Installation et configuration hello Application Insights package varie selon la plateforme hello sur lequel vous travaillez.</span><span class="sxs-lookup"><span data-stu-id="e5be0-132">Installing and configuring hello Application Insights package varies depending on hello platform you're working on.</span></span> 

1. <span data-ttu-id="e5be0-133">Dans Visual Studio, cliquez avec le bouton droit sur votre projet et choisissez **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="e5be0-133">In Visual Studio, right-click your project and choose **Manage Nuget Packages**.</span></span>
   
    ![Droit hello projet, puis sélectionnez Gérer les Packages Nuget](./media/app-insights-windows-services/03-nuget.png)
2. <span data-ttu-id="e5be0-135">Installer le package d’Application Insights hello pour les applications Windows server, « Microsoft.ApplicationInsights.WindowsServer. »</span><span class="sxs-lookup"><span data-stu-id="e5be0-135">Install hello Application Insights package for Windows server apps, "Microsoft.ApplicationInsights.WindowsServer."</span></span>
   
    ![Recherchez « Application Insights »](./media/app-insights-windows-services/04-ai-nuget.png)
   
    <span data-ttu-id="e5be0-137">*Quelle version ?*</span><span class="sxs-lookup"><span data-stu-id="e5be0-137">*Which version?*</span></span>

    <span data-ttu-id="e5be0-138">Vérifiez **inclure la version préliminaire** si vous souhaitez tootry nos dernières fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="e5be0-138">Check **Include prerelease** if you want tootry our latest features.</span></span> <span data-ttu-id="e5be0-139">les documents correspondants Hello ou blogs Notez si vous avez besoin d’une version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="e5be0-139">hello relevant documents or blogs note whether you need a prerelease version.</span></span>
    
    <span data-ttu-id="e5be0-140">*Puis-je utiliser d’autres packages ?*</span><span class="sxs-lookup"><span data-stu-id="e5be0-140">*Can I use other packages?*</span></span>
   
    <span data-ttu-id="e5be0-141">Oui.</span><span class="sxs-lookup"><span data-stu-id="e5be0-141">Yes.</span></span> <span data-ttu-id="e5be0-142">Choisissez « Microsoft.ApplicationInsights » si vous souhaitez uniquement toouse hello API toosend vos propres données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="e5be0-142">Choose "Microsoft.ApplicationInsights" if you only want toouse hello API toosend your own telemetry.</span></span> <span data-ttu-id="e5be0-143">Hello Windows Server inclut hello API et plusieurs autres packages tels que la collecte des compteurs de performances et l’analyse de dépendance.</span><span class="sxs-lookup"><span data-stu-id="e5be0-143">hello Windows Server package includes hello API plus a number of other packages such as performance counter collection and dependency monitoring.</span></span> 

### <a name="tooupgrade-toofuture-package-versions"></a><span data-ttu-id="e5be0-144">versions de package tooupgrade toofuture</span><span class="sxs-lookup"><span data-stu-id="e5be0-144">tooupgrade toofuture package versions</span></span>
<span data-ttu-id="e5be0-145">Nous libérer une nouvelle version de hello SDK à partir de tootime de temps.</span><span class="sxs-lookup"><span data-stu-id="e5be0-145">We release a new version of hello SDK from time tootime.</span></span>

<span data-ttu-id="e5be0-146">tooupgrade tooa [nouvelle version de package de hello](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/), ouvrez le Gestionnaire de package NuGet à nouveau et filtrer sur les packages installés.</span><span class="sxs-lookup"><span data-stu-id="e5be0-146">tooupgrade tooa [new release of hello package](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/), open NuGet package manager again and filter on installed packages.</span></span> <span data-ttu-id="e5be0-147">Sélectionnez **Microsoft.ApplicationInsights.WindowsServer** et choisissez **Mettre à niveau**.</span><span class="sxs-lookup"><span data-stu-id="e5be0-147">Select **Microsoft.ApplicationInsights.WindowsServer** and choose **Upgrade**.</span></span>

<span data-ttu-id="e5be0-148">Si vous avez apporté des personnalisations tooApplicationInsights.config, enregistrer une copie de celui-ci avant de mettre à niveau et par la suite de fusionner vos modifications dans la nouvelle version de hello.</span><span class="sxs-lookup"><span data-stu-id="e5be0-148">If you made any customizations tooApplicationInsights.config, save a copy of it before you upgrade, and afterwards merge your changes into hello new version.</span></span>

## <a name="4-send-telemetry"></a><span data-ttu-id="e5be0-149">4. Envoyer des données de télémétrie</span><span class="sxs-lookup"><span data-stu-id="e5be0-149">4. Send telemetry</span></span>
<span data-ttu-id="e5be0-150">**Si vous avez installé le package de hello API uniquement :**</span><span class="sxs-lookup"><span data-stu-id="e5be0-150">**If you installed only hello API package:**</span></span>

* <span data-ttu-id="e5be0-151">Valeur de clé d’instrumentation hello dans le code, par exemple `main()`:</span><span class="sxs-lookup"><span data-stu-id="e5be0-151">Set hello instrumentation key in code, for example in `main()`:</span></span> 
  
    <span data-ttu-id="e5be0-152">`TelemetryConfiguration.Active.InstrumentationKey = "`*votre clé*`";`</span><span class="sxs-lookup"><span data-stu-id="e5be0-152">`TelemetryConfiguration.Active.InstrumentationKey = "` *your key* `";`</span></span> 
* <span data-ttu-id="e5be0-153">[Écrire vos propres données de télémétrie à l’aide des API de hello](app-insights-api-custom-events-metrics.md#ikey).</span><span class="sxs-lookup"><span data-stu-id="e5be0-153">[Write your own telemetry using hello API](app-insights-api-custom-events-metrics.md#ikey).</span></span>

<span data-ttu-id="e5be0-154">**Si vous avez installé d’autres packages d’Application Insights,** vous pouvez, si vous préférez, utiliser clé d’instrumentation hello hello .config fichier tooset :</span><span class="sxs-lookup"><span data-stu-id="e5be0-154">**If you installed other Application Insights packages,** you can, if you prefer, use hello .config file tooset hello instrumentation key:</span></span>

* <span data-ttu-id="e5be0-155">Modifier ApplicationInsights.config (qui a été ajouté par hello NuGet installer).</span><span class="sxs-lookup"><span data-stu-id="e5be0-155">Edit ApplicationInsights.config (which was added by hello NuGet install).</span></span> <span data-ttu-id="e5be0-156">Insérez ce juste avant la balise de fermeture de hello :</span><span class="sxs-lookup"><span data-stu-id="e5be0-156">Insert this just before hello closing tag:</span></span>
  
    <span data-ttu-id="e5be0-157">`<InstrumentationKey>`*clé d’instrumentation hello vous avez copié*`</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="e5be0-157">`<InstrumentationKey>` *hello instrumentation key you copied* `</InstrumentationKey>`</span></span>
* <span data-ttu-id="e5be0-158">Assurez-vous que les propriétés de hello de ApplicationInsights.config dans l’Explorateur de solutions sont définies trop**Build Action = le contenu, copie tooOutput Directory = copie**.</span><span class="sxs-lookup"><span data-stu-id="e5be0-158">Make sure that hello properties of ApplicationInsights.config in Solution Explorer are set too**Build Action = Content, Copy tooOutput Directory = Copy**.</span></span>

<span data-ttu-id="e5be0-159">Il est la clé d’instrumentation hello tooset utiles dans le code si vous souhaitez trop[clé hello de commutateur pour différentes configurations de build](app-insights-separate-resources.md).</span><span class="sxs-lookup"><span data-stu-id="e5be0-159">It's useful tooset hello instrumentation key in code if you want too[switch hello key for different build configurations](app-insights-separate-resources.md).</span></span> <span data-ttu-id="e5be0-160">Si vous définissez la clé de hello dans le code, vous n’avez pas tooset dans hello `.config` fichier.</span><span class="sxs-lookup"><span data-stu-id="e5be0-160">If you set hello key in code, you don't have tooset it in hello `.config` file.</span></span>

## <span data-ttu-id="e5be0-161"><a name="run"></a> Exécution de votre projet</span><span class="sxs-lookup"><span data-stu-id="e5be0-161"><a name="run"></a> Run your project</span></span>
<span data-ttu-id="e5be0-162">Hello d’utilisation **F5** toorun votre application et essayez-la : ouvrir différentes pages toogenerate certaines données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="e5be0-162">Use hello **F5** toorun your application and try it out: open different pages toogenerate some telemetry.</span></span>

<span data-ttu-id="e5be0-163">Dans Visual Studio, vous verrez un nombre d’événements de hello qui ont été envoyés.</span><span class="sxs-lookup"><span data-stu-id="e5be0-163">In Visual Studio, you'll see a count of hello events that have been sent.</span></span>

![Nombre d’événements dans Visual Studio](./media/app-insights-windows-services/appinsights-09eventcount.png)

## <span data-ttu-id="e5be0-165"><a name="monitor"></a> Affichage de vos données de télémétrie</span><span class="sxs-lookup"><span data-stu-id="e5be0-165"><a name="monitor"></a> View your telemetry</span></span>
<span data-ttu-id="e5be0-166">Retourner toohello [portail Azure](https://portal.azure.com/) et parcourir les ressources d’Application Insights tooyour.</span><span class="sxs-lookup"><span data-stu-id="e5be0-166">Return toohello [Azure portal](https://portal.azure.com/) and browse tooyour Application Insights resource.</span></span>

<span data-ttu-id="e5be0-167">Rechercher des données dans les graphiques en vue d’ensemble de hello.</span><span class="sxs-lookup"><span data-stu-id="e5be0-167">Look for data in hello Overview charts.</span></span> <span data-ttu-id="e5be0-168">Au début, seuls un ou deux points s'affichent.</span><span class="sxs-lookup"><span data-stu-id="e5be0-168">At first, you'll just see one or two points.</span></span> <span data-ttu-id="e5be0-169">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="e5be0-169">For example:</span></span>

![Parcourez les données toomore](./media/app-insights-windows-services/12-first-perf.png)

<span data-ttu-id="e5be0-171">Cliquez sur via n’importe quel toosee graphique plus des métriques.</span><span class="sxs-lookup"><span data-stu-id="e5be0-171">Click through any chart toosee more detailed metrics.</span></span> [<span data-ttu-id="e5be0-172">En savoir plus sur les mesures.</span><span class="sxs-lookup"><span data-stu-id="e5be0-172">Learn more about metrics.</span></span>](app-insights-web-monitor-performance.md)

### <a name="no-data"></a><span data-ttu-id="e5be0-173">Pas de données ?</span><span class="sxs-lookup"><span data-stu-id="e5be0-173">No data?</span></span>
* <span data-ttu-id="e5be0-174">Utilisez l’application hello, ouvrir des pages différentes, afin qu’il génère des données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="e5be0-174">Use hello application, opening different pages so that it generates some telemetry.</span></span>
* <span data-ttu-id="e5be0-175">Ouvrez hello [recherche](app-insights-diagnostic-search.md) vignette, toosee des événements individuels.</span><span class="sxs-lookup"><span data-stu-id="e5be0-175">Open hello [Search](app-insights-diagnostic-search.md) tile, toosee individual events.</span></span> <span data-ttu-id="e5be0-176">Il prend événements parfois un peu longtemps tooget via le pipeline de métriques hello.</span><span class="sxs-lookup"><span data-stu-id="e5be0-176">Sometimes it takes events a little while longer tooget through hello metrics pipeline.</span></span>
* <span data-ttu-id="e5be0-177">Attendez quelques secondes, puis cliquez sur **Actualiser**.</span><span class="sxs-lookup"><span data-stu-id="e5be0-177">Wait a few seconds and click **Refresh**.</span></span> <span data-ttu-id="e5be0-178">Graphiques eux-mêmes actualiser régulièrement, mais vous pouvez actualiser manuellement si vous vous attendez tooshow de certaines données.</span><span class="sxs-lookup"><span data-stu-id="e5be0-178">Charts refresh themselves periodically, but you can refresh manually if you're waiting for some data tooshow up.</span></span>
* <span data-ttu-id="e5be0-179">Consultez la rubrique [Résolution des problèmes](app-insights-troubleshoot-faq.md).</span><span class="sxs-lookup"><span data-stu-id="e5be0-179">See [Troubleshooting](app-insights-troubleshoot-faq.md).</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="e5be0-180">Publier votre application</span><span class="sxs-lookup"><span data-stu-id="e5be0-180">Publish your app</span></span>
<span data-ttu-id="e5be0-181">Déployer maintenant votre serveur d’applications tooyour ou tooAzure et Espion hello s’accumulent des données.</span><span class="sxs-lookup"><span data-stu-id="e5be0-181">Now deploy your application tooyour server or tooAzure and watch hello data accumulate.</span></span>

![Utiliser Visual Studio toopublish votre application](./media/app-insights-windows-services/15-publish.png)

<span data-ttu-id="e5be0-183">Lorsque vous exécutez en mode débogage, la télémétrie s’effectue via le pipeline de hello, afin que vous devez voir les données figurant dans les secondes.</span><span class="sxs-lookup"><span data-stu-id="e5be0-183">When you run in debug mode, telemetry is expedited through hello pipeline, so that you should see data appearing within seconds.</span></span> <span data-ttu-id="e5be0-184">Quand vous déployez votre application dans la configuration Release, les données s’accumulent plus lentement.</span><span class="sxs-lookup"><span data-stu-id="e5be0-184">When you deploy your app in Release configuration, data accumulates more slowly.</span></span>

### <a name="no-data-after-you-publish-tooyour-server"></a><span data-ttu-id="e5be0-185">Aucune donnée après la publication tooyour serveur ?</span><span class="sxs-lookup"><span data-stu-id="e5be0-185">No data after you publish tooyour server?</span></span>
<span data-ttu-id="e5be0-186">Ouvrez les ports pour le trafic sortant dans le pare-feu de votre serveur.</span><span class="sxs-lookup"><span data-stu-id="e5be0-186">Open ports for outgoing traffic in your server's firewall.</span></span> <span data-ttu-id="e5be0-187">Consultez [cette page](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses) pour la liste d’adresses requises hello</span><span class="sxs-lookup"><span data-stu-id="e5be0-187">See [this page](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses) for hello list of required addresses</span></span> 

### <a name="trouble-on-your-build-server"></a><span data-ttu-id="e5be0-188">Vous rencontrez des problèmes sur votre serveur de builds ?</span><span class="sxs-lookup"><span data-stu-id="e5be0-188">Trouble on your build server?</span></span>
<span data-ttu-id="e5be0-189">Consultez cet article de [résolution des problèmes](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild).</span><span class="sxs-lookup"><span data-stu-id="e5be0-189">Please see [this Troubleshooting item](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild).</span></span>

> [!NOTE]
> <span data-ttu-id="e5be0-190">Si votre application génère un grand nombre de télémétrie, module d’échantillonnage adaptive hello réduira automatiquement volume hello envoyé toohello portail en envoyant qu’une fraction représentative d’événements.</span><span class="sxs-lookup"><span data-stu-id="e5be0-190">If your app generates a lot of telemetry, hello adaptive sampling module will automatically reduce hello volume that is sent toohello portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="e5be0-191">Toutefois, les événements qui sont associée toohello même demande sera sélectionné ou désélectionné en tant que groupe, afin que vous pouvez naviguer entre les événements connexes.</span><span class="sxs-lookup"><span data-stu-id="e5be0-191">However, events that are related toohello same request will be selected or deselected as a group, so that you can navigate between related events.</span></span> 
> <span data-ttu-id="e5be0-192">[En savoir plus sur l'échantillonnage](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="e5be0-192">[Learn about sampling](app-insights-sampling.md).</span></span>
> 
> 

## <a name="video"></a><span data-ttu-id="e5be0-193">Vidéo</span><span class="sxs-lookup"><span data-stu-id="e5be0-193">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="e5be0-194">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e5be0-194">Next steps</span></span>
* <span data-ttu-id="e5be0-195">[Ajouter des données de télémétrie plus](app-insights-asp-net-more.md) tooget hello vue 360 degrés de votre application.</span><span class="sxs-lookup"><span data-stu-id="e5be0-195">[Add more telemetry](app-insights-asp-net-more.md) tooget hello full 360-degree view of your application.</span></span>

