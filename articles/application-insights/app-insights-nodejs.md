---
title: aaaMonitor Node.js services avec Azure Application Insights | Documents Microsoft
description: "Analysez les performances et diagnostiquez les problèmes dans les services Node.js avec Application Insights."
services: application-insights
documentationcenter: nodejs
author: joshgav
manager: carmonm
ms.assetid: 2ec7f809-5e1a-41cf-9fcd-d0ed4bebd08c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/01/2017
ms.author: bwren
ms.openlocfilehash: 0a7e66990cd4d3a2fcaf3fa779adb336c861f8ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-nodejs-services-and-apps-with-application-insights"></a><span data-ttu-id="6d0bd-103">Surveiller vos services et applications Node.js avec Application Insights</span><span class="sxs-lookup"><span data-stu-id="6d0bd-103">Monitor your Node.js services and apps with Application Insights</span></span>

<span data-ttu-id="6d0bd-104">[Azure Application Insights](app-insights-overview.md) surveille vos composants et services principaux après avoir déployé les toohelp vous [détecter et diagnostiquer rapidement les problèmes de performances et autres](app-insights-detect-triage-diagnose.md).</span><span class="sxs-lookup"><span data-stu-id="6d0bd-104">[Azure Application Insights](app-insights-overview.md) monitors your backend services and components after you deploy them toohelp you [discover and rapidly diagnose performance and other issues](app-insights-detect-triage-diagnose.md).</span></span> <span data-ttu-id="6d0bd-105">Utilisez ce service pour les services Node.js, où qu’ils soient hébergés : dans votre centre de données, des machines virtuelles Azure et des applications Web, voire d’autres clouds publics.</span><span class="sxs-lookup"><span data-stu-id="6d0bd-105">Use it for Node.js services hosted anywhere: your datacenter, Azure VMs and Web Apps, and even other public clouds.</span></span>

<span data-ttu-id="6d0bd-106">tooreceive, stocker et Explorer vos données d’analyse, suivez hello suivant les instructions tooinclude un agent dans votre code et définir une ressource Application Insights correspondante dans Azure.</span><span class="sxs-lookup"><span data-stu-id="6d0bd-106">tooreceive, store, and explore your monitoring data, follow hello following instructions tooinclude an agent in your code and set up a corresponding Application Insights resource in Azure.</span></span> <span data-ttu-id="6d0bd-107">agent de Hello envoie des ressources toothat de données pour une analyse plus approfondie et l’exploration.</span><span class="sxs-lookup"><span data-stu-id="6d0bd-107">hello agent sends data toothat resource for further analysis and exploration.</span></span>

<span data-ttu-id="6d0bd-108">l’agent de Node.js Hello peut automatiquement détecter entrants et sortants HTTP demandes, plusieurs métriques du système et les exceptions.</span><span class="sxs-lookup"><span data-stu-id="6d0bd-108">hello Node.js agent can automatically monitor incoming and outgoing HTTP requests, several system metrics, and exceptions.</span></span> <span data-ttu-id="6d0bd-109">Depuis la version 0.20, il peut également analyser certains packages tiers courants, tels que `mongodb`, `mysql` et `redis`.</span><span class="sxs-lookup"><span data-stu-id="6d0bd-109">Beginning in v0.20, it can also monitor some common third-party packages such as `mongodb`, `mysql`, and `redis`.</span></span> <span data-ttu-id="6d0bd-110">Tous les événements liés à la demande HTTP entrante tooan sont corrélés de dépannage plus rapide.</span><span class="sxs-lookup"><span data-stu-id="6d0bd-110">All events related tooan incoming HTTP request are correlated for faster troubleshooting.</span></span>

<span data-ttu-id="6d0bd-111">Vous pouvez surveiller plusieurs autres aspects de votre application et système en manuellement en instrumentant les à l’aide des API de l’agent hello décrite plus loin.</span><span class="sxs-lookup"><span data-stu-id="6d0bd-111">You can monitor more aspects of your app and system by manually instrumenting them using hello agent API described later.</span></span>

![Exemples de graphiques d’analyse des performances](./media/app-insights-nodejs/10-perf.png)

## <a name="getting-started"></a><span data-ttu-id="6d0bd-113">Mise en route</span><span class="sxs-lookup"><span data-stu-id="6d0bd-113">Getting Started</span></span>

<span data-ttu-id="6d0bd-114">Voyons comment configurer l’analyse d’une application ou d’un service.</span><span class="sxs-lookup"><span data-stu-id="6d0bd-114">Let's step through setting up monitoring for an app or service.</span></span>

### <span data-ttu-id="6d0bd-115"><a name="resource"></a> Configurer une ressource Application Insights</span><span class="sxs-lookup"><span data-stu-id="6d0bd-115"><a name="resource"></a> Set up an App Insights resource</span></span>

<span data-ttu-id="6d0bd-116">**Avant de commencer**, assurez-vous que vous disposez d’un abonnement Azure ou [obtenez-en un gratuitement][azure-free-offer].</span><span class="sxs-lookup"><span data-stu-id="6d0bd-116">**Before you start**, make sure you have an Azure subscription or [get a new one for free][azure-free-offer].</span></span> <span data-ttu-id="6d0bd-117">Si votre organisation possède déjà un abonnement Azure, un administrateur peut suivre [ces instructions] [ add-aad-user] tooadd tooit vous.</span><span class="sxs-lookup"><span data-stu-id="6d0bd-117">If your organization already has an Azure subscription, an administrator can follow [these instructions][add-aad-user] tooadd you tooit.</span></span>

[azure-free-offer]: https://azure.microsoft.com/en-us/free/
[add-aad-user]: https://docs.microsoft.com/en-us/azure/active-directory/active-directory-users-create-azure-portal

<span data-ttu-id="6d0bd-118">À présent vous connecter toohello [portail Azure] [ portal] et créer une ressource Application Insights, comme illustré dans les éléments suivants de hello - cliquez sur « Nouveau » > « Outils de développement » > « Application Insights ».</span><span class="sxs-lookup"><span data-stu-id="6d0bd-118">Now log in toohello [Azure portal][portal] and create an Application Insights resource as illustrated in hello following - click "New" > "Developer tools" > "Application Insights".</span></span> <span data-ttu-id="6d0bd-119">ressource de Hello inclut un point de terminaison pour recevoir des données de télémétrie, stockage pour ces données, enregistré des rapports et tableaux de bord, règle et configuration d’alerte et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="6d0bd-119">hello resource includes an endpoint for receiving telemetry data, storage for this data, saved reports and dashboards, rule and alert configuration, and more.</span></span>

![Créer une ressource Application Insights](./media/app-insights-nodejs/03-new_appinsights_resource.png)

<span data-ttu-id="6d0bd-121">Sur la page de création d’une ressource de hello, choisissez « Application Node.js » hello application liste déroulante type.</span><span class="sxs-lookup"><span data-stu-id="6d0bd-121">On hello resource creation page, choose "Node.js Application" from hello application type drop-down.</span></span> <span data-ttu-id="6d0bd-122">type d’application Hello détermine l’ensemble de tableaux de bord et rapports créés pour vous par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="6d0bd-122">hello app type determines hello default set of dashboards and reports created for you.</span></span> <span data-ttu-id="6d0bd-123">Ne vous inquiétez pas : toutes les ressources Application Insights peuvent collecter des données à partir de n’importe quel langage et n’importe quelle plateforme.</span><span class="sxs-lookup"><span data-stu-id="6d0bd-123">Don't worry though, any App Insights resource can in fact collect data from any language and platform.</span></span>

![Formulaire de nouvelle ressource Application Insights](./media/app-insights-nodejs/04-create_appinsights_resource.png)

### <span data-ttu-id="6d0bd-125"><a name="agent"></a>Configurer l’agent de hello Node.js</span><span class="sxs-lookup"><span data-stu-id="6d0bd-125"><a name="agent"></a> Set up hello Node.js agent</span></span>

<span data-ttu-id="6d0bd-126">Il est maintenant temps tooinclude hello l’agent dans votre application afin qu’il puisse collecter des données.</span><span class="sxs-lookup"><span data-stu-id="6d0bd-126">Now it's time tooinclude hello agent in your app so it can gather data.</span></span>
<span data-ttu-id="6d0bd-127">Copiez la clé d’Instrumentation de votre ressource (ci-après dénommés tooas votre `ikey`) à partir du portail hello comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="6d0bd-127">Start by copying your resource's Instrumentation Key (hereinafter referred tooas your `ikey`) from hello portal as shown below.</span></span> <span data-ttu-id="6d0bd-128">Hello Insights application système utilise cette tooyour de données de clé toomap ressource Azure, par conséquent, vous devez toospecify dans une variable d’environnement ou hello agent toouse dans votre code.</span><span class="sxs-lookup"><span data-stu-id="6d0bd-128">hello App Insights system uses this key toomap data tooyour Azure resource so you need toospecify it in an environment variable or your code for hello agent toouse.</span></span>  

![Copier la clé d’instrumentation](./media/app-insights-nodejs/05-appinsights_ikey_portal.png)

<span data-ttu-id="6d0bd-130">Ensuite, ajoutez les dépendances hello Node.js agent bibliothèque tooyour l’application via package.json.</span><span class="sxs-lookup"><span data-stu-id="6d0bd-130">Next, add hello Node.js agent library tooyour app's dependencies via package.json.</span></span> <span data-ttu-id="6d0bd-131">À partir du dossier racine de hello de votre application, exécutez :</span><span class="sxs-lookup"><span data-stu-id="6d0bd-131">From hello root folder of your app, run:</span></span>

```bash
npm install applicationinsights --save
```

<span data-ttu-id="6d0bd-132">Vous devez maintenant tooexplicitly chargement de la bibliothèque hello dans votre code.</span><span class="sxs-lookup"><span data-stu-id="6d0bd-132">Now you need tooexplicitly load hello library in your code.</span></span> <span data-ttu-id="6d0bd-133">Étant donné que l’agent de hello injecte instrumentation dans nombreuses autres bibliothèques, vous devez le charger dès que possible, même avant les autres `require` instructions.</span><span class="sxs-lookup"><span data-stu-id="6d0bd-133">Because hello agent injects instrumentation into many other libraries, you should load it as early as possible, even before other `require` statements.</span></span> <span data-ttu-id="6d0bd-134">tooget démarré, en haut de hello de votre premier fichier .js ajouter :</span><span class="sxs-lookup"><span data-stu-id="6d0bd-134">tooget started, at hello top of your first .js file add:</span></span>

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>");
appInsights.start();
```

<span data-ttu-id="6d0bd-135">Hello `setup` méthode configure la clé d’instrumentation hello (et, par conséquent, les ressources Azure) toobe utilisé par défaut pour les éléments de toutes les marques.</span><span class="sxs-lookup"><span data-stu-id="6d0bd-135">hello `setup` method configures hello instrumentation key (and thus Azure resource) toobe used by default for all tracked items.</span></span> <span data-ttu-id="6d0bd-136">Appelez `start` une fois la configuration toobegin terminé collecte et l’envoi des données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="6d0bd-136">Call `start` after configuration is finished toobegin gathering and sending telemetry data.</span></span>

<span data-ttu-id="6d0bd-137">Vous pouvez également fournir un ikey via une variable d’environnement hello APPINSIGHTS\_INSTRUMENTATIONKEY au lieu de passer manuellement trop `setup()` ou `getClient()`.</span><span class="sxs-lookup"><span data-stu-id="6d0bd-137">You can also provide an ikey via hello environment variable APPINSIGHTS\_INSTRUMENTATIONKEY instead of passing it manually too `setup()` or `getClient()`.</span></span> <span data-ttu-id="6d0bd-138">Cette pratique permet de conserver ikeys hors code source validée et toospecify des ikeys différentes pour différents environnements.</span><span class="sxs-lookup"><span data-stu-id="6d0bd-138">This practice lets you keep ikeys out of committed source code and toospecify different ikeys for different environments.</span></span>

<span data-ttu-id="6d0bd-139">Des options de configuration supplémentaires sont présentées ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="6d0bd-139">Additional configuration options are documented below.</span></span>

<span data-ttu-id="6d0bd-140">Vous pouvez essayer de l’agent de hello sans envoyer de télémétrie en définissant la chaîne non vide de hello instrumentation tooany clé.</span><span class="sxs-lookup"><span data-stu-id="6d0bd-140">You can try hello agent without sending telemetry by setting hello instrumentation key tooany non-empty string.</span></span>

### <span data-ttu-id="6d0bd-141"><a name="monitor"></a> Surveiller votre application</span><span class="sxs-lookup"><span data-stu-id="6d0bd-141"><a name="monitor"></a> Monitor your app</span></span>

<span data-ttu-id="6d0bd-142">l’agent de Hello rassemble automatiquement télémétrie à propos du runtime de Node.js hello et certains modules tiers communs.</span><span class="sxs-lookup"><span data-stu-id="6d0bd-142">hello agent automatically gathers telemetry about hello Node.js runtime and some common third-party modules.</span></span> <span data-ttu-id="6d0bd-143">Utilisez votre toogenerate de maintenant application certaines de ces données.</span><span class="sxs-lookup"><span data-stu-id="6d0bd-143">Use your application now toogenerate some of this data.</span></span>

<span data-ttu-id="6d0bd-144">Ensuite, dans hello [portail Azure] [ portal] parcourir les ressources d’Application Insights toohello vous avez créé précédemment et rechercher votre premier quelques points de données dans la chronologie de vue d’ensemble de hello, comme dans hello suivant l’image.</span><span class="sxs-lookup"><span data-stu-id="6d0bd-144">Then, in hello [Azure portal][portal] browse toohello Application Insights resource you created earlier and look for your first few data points in hello Overview timeline, as in hello following image.</span></span> <span data-ttu-id="6d0bd-145">Cliquez sur les graphiques hello pour plus de détails.</span><span class="sxs-lookup"><span data-stu-id="6d0bd-145">Click through hello charts for more details.</span></span>

![Premiers points de données](./media/app-insights-nodejs/12-first-perf.png)

<span data-ttu-id="6d0bd-147">Cliquez sur hello Application carte bouton tooview hello topologie découverte pour votre application, comme dans hello suivant l’image.</span><span class="sxs-lookup"><span data-stu-id="6d0bd-147">Click hello Application map button tooview hello topology discovered for your app, as in hello following image.</span></span> <span data-ttu-id="6d0bd-148">Cliquez sur composants de carte hello pour plus de détails.</span><span class="sxs-lookup"><span data-stu-id="6d0bd-148">Click through components in hello map for more details.</span></span>

![Mise en correspondance d’une application simple](./media/app-insights-nodejs/06-appinsights_appmap.png)

<span data-ttu-id="6d0bd-150">En savoir plus sur votre application et résoudre les problèmes à l’aide de hello autres vues disponibles sous hello « Recherchez » section.</span><span class="sxs-lookup"><span data-stu-id="6d0bd-150">Learn more about your app and troubleshoot problems using hello other views available under hello "Investigate" section.</span></span>

![Section Examiner](./media/app-insights-nodejs/07-appinsights_investigate_blades.png)

#### <a name="no-data"></a><span data-ttu-id="6d0bd-152">Pas de données ?</span><span class="sxs-lookup"><span data-stu-id="6d0bd-152">No data?</span></span>

<span data-ttu-id="6d0bd-153">Étant donné que l’agent de hello des lots de données pour l’envoi d’il peut y avoir un délai avant que les éléments sont affichés dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="6d0bd-153">Because hello agent batches data for submission there may be a delay before items are displayed in hello portal.</span></span> <span data-ttu-id="6d0bd-154">Si vous ne voyez pas les données dans votre ressource essayez certaines des hello suivant les correctifs :</span><span class="sxs-lookup"><span data-stu-id="6d0bd-154">If you don't see data in your resource try some of hello following fixes:</span></span>

* <span data-ttu-id="6d0bd-155">Utilisez application hello plus ; prendre plus d’actions toogenerate plus de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="6d0bd-155">Use hello application some more; take more actions toogenerate more telemetry.</span></span>
* <span data-ttu-id="6d0bd-156">Cliquez sur **Actualiser** dans l’affichage des ressources portail hello.</span><span class="sxs-lookup"><span data-stu-id="6d0bd-156">Click **Refresh** in hello portal resource view.</span></span> <span data-ttu-id="6d0bd-157">Graphiques actualiser automatiquement eux-mêmes régulièrement, mais l’actualisation force ce toohappen immédiatement.</span><span class="sxs-lookup"><span data-stu-id="6d0bd-157">Charts automatically refresh themselves periodically but refreshing forces this toohappen immediately.</span></span>
* <span data-ttu-id="6d0bd-158">Vérifiez que les [ports sortants requis](app-insights-ip-addresses.md) sont ouverts.</span><span class="sxs-lookup"><span data-stu-id="6d0bd-158">Verify that [needed outgoing ports](app-insights-ip-addresses.md) are open.</span></span>
* <span data-ttu-id="6d0bd-159">Ouvrez hello [recherche](app-insights-diagnostic-search.md) vignette et recherchez les événements individuels.</span><span class="sxs-lookup"><span data-stu-id="6d0bd-159">Open hello [Search](app-insights-diagnostic-search.md) tile and look for individual events.</span></span>
* <span data-ttu-id="6d0bd-160">Vérifiez hello [FAQ][].</span><span class="sxs-lookup"><span data-stu-id="6d0bd-160">Check hello [FAQ][].</span></span>


## <a name="agent-configuration"></a><span data-ttu-id="6d0bd-161">Configuration de l’agent</span><span class="sxs-lookup"><span data-stu-id="6d0bd-161">Agent Configuration</span></span>

<span data-ttu-id="6d0bd-162">Voici les méthodes de configuration de l’agent hello et leurs valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="6d0bd-162">Following are hello agent's configuration methods and their default values.</span></span>

<span data-ttu-id="6d0bd-163">événements de mettre en corrélation toofully dans un service, être tooset vraiment `.setAutoDependencyCorrelation(true)`.</span><span class="sxs-lookup"><span data-stu-id="6d0bd-163">toofully correlate events in a service, be sure tooset `.setAutoDependencyCorrelation(true)`.</span></span> <span data-ttu-id="6d0bd-164">Cela permet à l’agent de hello tootrack contexte entre des rappels asynchrones dans Node.js.</span><span class="sxs-lookup"><span data-stu-id="6d0bd-164">This allows hello agent tootrack context across asynchronous callbacks in Node.js.</span></span>

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>")
    .setAutoDependencyCorrelation(false)
    .setAutoCollectRequests(true)
    .setAutoCollectPerformance(true)
    .setAutoCollectExceptions(true)
    .setAutoCollectDependencies(true)
    .start();
```

## <a name="agent-api"></a><span data-ttu-id="6d0bd-165">API de l’agent</span><span class="sxs-lookup"><span data-stu-id="6d0bd-165">Agent API</span></span>

<!-- TODO: Fully document agent API. -->

<span data-ttu-id="6d0bd-166">Hello API de l’agent .NET est décrite en détail [ici](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="6d0bd-166">hello .NET agent API is fully described [here](app-insights-api-custom-events-metrics.md).</span></span>

<span data-ttu-id="6d0bd-167">Vous pouvez suivre n’importe quel demande, un événement, une mesure ou une exception à l’aide du client d’Application Insights Node.js hello.</span><span class="sxs-lookup"><span data-stu-id="6d0bd-167">You can track any request, event, metric, or exception using hello Application Insights Node.js client.</span></span> <span data-ttu-id="6d0bd-168">Hello exemple suivant illustre certains hello API disponibles.</span><span class="sxs-lookup"><span data-stu-id="6d0bd-168">hello following example demonstrates some of hello available APIs.</span></span>

```javascript
let appInsights = require("applicationinsights");
appInsights.setup().start(); // assuming ikey in env var
let client = appInsights.getClient();

client.trackEvent("my custom event", {customProperty: "custom property value"});
client.trackException(new Error("handled exceptions can be logged with this method"));
client.trackMetric("custom metric", 3);
client.trackTrace("trace message");

let http = require("http");
http.createServer( (req, res) => {
  client.trackRequest(req, res); // Place at hello beginning of your request handler
});
```

### <a name="track-your-dependencies"></a><span data-ttu-id="6d0bd-169">Suivre les dépendances</span><span class="sxs-lookup"><span data-stu-id="6d0bd-169">Track your dependencies</span></span>

```javascript
let appInsights = require("applicationinsights");
let client = appInsights.getClient();

var success = false;
let startTime = Date.now();
// execute dependency call here....
let duration = Date.now() - startTime;
success = true;

client.trackDependency("dependency name", "command name", duration, success);
```

### <a name="add-a-custom-property-tooall-events"></a><span data-ttu-id="6d0bd-170">Ajouter une propriété personnalisée des événements tooall</span><span class="sxs-lookup"><span data-stu-id="6d0bd-170">Add a custom property tooall events</span></span>

```javascript
appInsights.client.commonProperties = {
    environment: process.env.SOME_ENV_VARIABLE
};
```

### <a name="track-http-get-requests"></a><span data-ttu-id="6d0bd-171">Suivre les demandes HTTP GET</span><span class="sxs-lookup"><span data-stu-id="6d0bd-171">Track HTTP GET requests</span></span>

```javascript
var server = http.createServer((req, res) => {
    if ( req.method === "GET" ) {
            appInsights.client.trackRequest(req, res);
    }
    // other work here....
    res.end();
});
```

### <a name="track-server-startup-time"></a><span data-ttu-id="6d0bd-172">Suivre le temps de démarrage du serveur</span><span class="sxs-lookup"><span data-stu-id="6d0bd-172">Track server startup time</span></span>

```javascript
let start = Date.now();
server.on("listening", () => {
    let duration = Date.now() - start;
    appInsights.client.trackMetric("server startup time", duration);
});
```

## <a name="more-resources"></a><span data-ttu-id="6d0bd-173">Autres ressources</span><span class="sxs-lookup"><span data-stu-id="6d0bd-173">More resources</span></span>

* [<span data-ttu-id="6d0bd-174">Surveillez la télémétrie dans le portail de hello</span><span class="sxs-lookup"><span data-stu-id="6d0bd-174">Monitor your telemetry in hello portal</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="6d0bd-175">Écrire des requêtes Analytics via vos données de télémétrie</span><span class="sxs-lookup"><span data-stu-id="6d0bd-175">Write Analytics queries over your telemetry</span></span>](app-insights-analytics-tour.md)

<!--references-->

[portal]: https://portal.azure.com/
[FAQ]: app-insights-troubleshoot-faq.md
