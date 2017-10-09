---
title: "aaaApplication Insights pour Java web des applications qui sont déjà actives"
description: "Commencez à surveiller une application web qui est déjà en cours d’exécution sur votre serveur."
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 12f3dbb9-915f-4087-87c9-807286030b0b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/10/2016
ms.author: bwren
ms.openlocfilehash: 2b01cd61657522ccf1d2d97b2a29cdeb08ec9a18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-java-web-apps-that-are-already-live"></a><span data-ttu-id="4e19b-103">Application Insights pour les applications web qui sont déjà actives</span><span class="sxs-lookup"><span data-stu-id="4e19b-103">Application Insights for Java web apps that are already live</span></span>


<span data-ttu-id="4e19b-104">Si vous avez une application web qui est déjà en cours d’exécution sur votre serveur J2EE, vous pouvez démarrer l’analyse avec [Application Insights](app-insights-overview.md) sans hello devez toomake aux modifications de code ou à recompiler votre projet.</span><span class="sxs-lookup"><span data-stu-id="4e19b-104">If you have a web application that is already running on your J2EE server, you can start monitoring it with [Application Insights](app-insights-overview.md) without hello need toomake code changes or recompile your project.</span></span> <span data-ttu-id="4e19b-105">Avec cette option, vous obtenez des informations sur les requêtes HTTP envoyées tooyour serveur, les exceptions non gérées et les compteurs de performance.</span><span class="sxs-lookup"><span data-stu-id="4e19b-105">With this option, you get information about HTTP requests sent tooyour server, unhandled exceptions, and performance counters.</span></span>

<span data-ttu-id="4e19b-106">Vous aurez besoin d’un abonnement trop[Microsoft Azure](https://azure.com).</span><span class="sxs-lookup"><span data-stu-id="4e19b-106">You'll need a subscription too[Microsoft Azure](https://azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="4e19b-107">procédure de Hello sur cette page ajoute hello SDK tooyour web application lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="4e19b-107">hello procedure on this page adds hello SDK tooyour web app at runtime.</span></span> <span data-ttu-id="4e19b-108">Cette instrumentation du runtime est utile si vous ne souhaitez tooupdate ou régénérez votre code source.</span><span class="sxs-lookup"><span data-stu-id="4e19b-108">This runtime instrumentation is useful if you don't want tooupdate or rebuild your source code.</span></span> <span data-ttu-id="4e19b-109">Mais si vous le pouvez, nous vous recommandons de vous [ajouter le code source de hello SDK toohello](app-insights-java-get-started.md) à la place.</span><span class="sxs-lookup"><span data-stu-id="4e19b-109">But if you can, we recommend you [add hello SDK toohello source code](app-insights-java-get-started.md) instead.</span></span> <span data-ttu-id="4e19b-110">Qui vous donne davantage d’options telles que l’écriture d’activité de code tootrack utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4e19b-110">That gives you more options such as writing code tootrack user activity.</span></span>
> 
> 

## <a name="1-get-an-application-insights-instrumentation-key"></a><span data-ttu-id="4e19b-111">1. Obtenir une clé d'instrumentation Application Insights</span><span class="sxs-lookup"><span data-stu-id="4e19b-111">1. Get an Application Insights instrumentation key</span></span>
1. <span data-ttu-id="4e19b-112">Connectez-vous à toohello [portail Microsoft Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="4e19b-112">Sign in toohello [Microsoft Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="4e19b-113">Créer une ressource Application Insights et définir l’application web de hello application type tooJava.</span><span class="sxs-lookup"><span data-stu-id="4e19b-113">Create a new Application Insights resource and set hello application type tooJava web application.</span></span>
   
    ![Indiquez le nom, choisissez l’application web Java, puis cliquez sur Créer.](./media/app-insights-java-live/02-create.png)

    <span data-ttu-id="4e19b-115">ressource de Hello est créée en quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="4e19b-115">hello resource is created in a few seconds.</span></span>

4. <span data-ttu-id="4e19b-116">Ouvrir la ressource hello et sa clé d’instrumentation.</span><span class="sxs-lookup"><span data-stu-id="4e19b-116">Open hello new resource and get its instrumentation key.</span></span> <span data-ttu-id="4e19b-117">Vous devez toopaste cette clé dans votre projet de code dans quelques instants.</span><span class="sxs-lookup"><span data-stu-id="4e19b-117">You'll need toopaste this key into your code project shortly.</span></span>
   
    ![Dans hello nouvelle ressource vue d’ensemble, cliquez sur Propriétés et copiez hello clé d’Instrumentation](./media/app-insights-java-live/03-key.png)

## <a name="2-download-hello-sdk"></a><span data-ttu-id="4e19b-119">2. Télécharger hello SDK</span><span class="sxs-lookup"><span data-stu-id="4e19b-119">2. Download hello SDK</span></span>
1. <span data-ttu-id="4e19b-120">Télécharger hello [Application Insights SDK pour Java](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="4e19b-120">Download hello [Application Insights SDK for Java](https://aka.ms/aijavasdk).</span></span> 
2. <span data-ttu-id="4e19b-121">Sur votre serveur, extraire le répertoire de toohello hello du SDK du contenu à partir de laquelle les fichiers binaires du projet sont chargés.</span><span class="sxs-lookup"><span data-stu-id="4e19b-121">On your server, extract hello SDK contents toohello directory from which your project binaries are loaded.</span></span> <span data-ttu-id="4e19b-122">Si vous utilisez Tomcat, ce répertoire se trouve généralement sous `webapps/<your_app_name>/WEB-INF/lib`</span><span class="sxs-lookup"><span data-stu-id="4e19b-122">If you’re using Tomcat, this directory would typically be under `webapps/<your_app_name>/WEB-INF/lib`</span></span>

<span data-ttu-id="4e19b-123">Notez que vous devez toorepeat cela sur chaque instance de serveur et pour chaque application.</span><span class="sxs-lookup"><span data-stu-id="4e19b-123">Note that you need toorepeat this on each server instance, and for each app.</span></span>

## <a name="3-add-an-application-insights-xml-file"></a><span data-ttu-id="4e19b-124">3. Ajouter un fichier xml Application Insights</span><span class="sxs-lookup"><span data-stu-id="4e19b-124">3. Add an Application Insights xml file</span></span>
<span data-ttu-id="4e19b-125">Créer ApplicationInsights.xml dans le dossier hello dans lequel vous avez ajouté hello SDK.</span><span class="sxs-lookup"><span data-stu-id="4e19b-125">Create ApplicationInsights.xml in hello folder in which you added hello SDK.</span></span> <span data-ttu-id="4e19b-126">Y hello suivants XML.</span><span class="sxs-lookup"><span data-stu-id="4e19b-126">Put into it hello following XML.</span></span>

<span data-ttu-id="4e19b-127">Remplacer la clé d’instrumentation hello que vous avez obtenu hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="4e19b-127">Substitute hello instrumentation key that you got from hello Azure portal.</span></span>

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsights xmlns="http://schemas.microsoft.com/ApplicationInsights/2013/Settings" schemaVersion="2014-05-30">


      <!-- hello key from hello portal: -->

      <InstrumentationKey>** Your instrumentation key **</InstrumentationKey>


      <!-- HTTP request component (not required for bare API) -->

      <TelemetryModules>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebRequestTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebSessionTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebUserTrackingTelemetryModule"/>
      </TelemetryModules>

      <!-- Events correlation (not required for bare API) -->
      <!-- These initializers add context data tooeach event -->

      <TelemetryInitializers>
        <Add   type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationIdTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationNameTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebSessionTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserAgentTelemetryInitializer"/>

      </TelemetryInitializers>
    </ApplicationInsights>
```

* <span data-ttu-id="4e19b-128">clé d’instrumentation Hello est envoyé avec chaque élément de données de télémétrie et indique à Application Insights toodisplay dans votre ressource.</span><span class="sxs-lookup"><span data-stu-id="4e19b-128">hello instrumentation key is sent along with every item of telemetry and tells Application Insights toodisplay it in your resource.</span></span>
* <span data-ttu-id="4e19b-129">Hello composant de requête HTTP est facultative.</span><span class="sxs-lookup"><span data-stu-id="4e19b-129">hello HTTP Request component is optional.</span></span> <span data-ttu-id="4e19b-130">Il envoie automatiquement télémétrie concernant les requêtes et le portail de toohello de temps de réponse.</span><span class="sxs-lookup"><span data-stu-id="4e19b-130">It automatically sends telemetry about requests and response times toohello portal.</span></span>
* <span data-ttu-id="4e19b-131">Corrélation des événements est un composant de requête Ajout toohello HTTP.</span><span class="sxs-lookup"><span data-stu-id="4e19b-131">Events correlation is an addition toohello HTTP request component.</span></span> <span data-ttu-id="4e19b-132">Il attribue à une demande de tooeach identificateur reçue par le serveur de hello et ajoute cet identificateur en tant qu’un élément tooevery de propriété de télémétrie en tant que propriété de hello 'Operation.Id'.</span><span class="sxs-lookup"><span data-stu-id="4e19b-132">It assigns an identifier tooeach request received by hello server, and adds this identifier as a property tooevery item of telemetry as hello property 'Operation.Id'.</span></span> <span data-ttu-id="4e19b-133">Il vous permet de télémétrie de hello toocorrelate associé à chaque requête en définissant un filtre dans [recherche diagnostic](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="4e19b-133">It allows you toocorrelate hello telemetry associated with each request by setting a filter in [diagnostic search](app-insights-diagnostic-search.md).</span></span>

## <a name="4-add-an-http-filter"></a><span data-ttu-id="4e19b-134">4. Ajouter un filtre HTTP</span><span class="sxs-lookup"><span data-stu-id="4e19b-134">4. Add an HTTP filter</span></span>
<span data-ttu-id="4e19b-135">Recherchez et ouvrez le fichier de web.xml hello dans votre projet, puis hello fusion suivante extrait de code sous le nœud de l’application web hello, dans lequel les filtres d’application sont configurés.</span><span class="sxs-lookup"><span data-stu-id="4e19b-135">Locate and open hello web.xml file in your project, and merge hello following snippet of code under hello web-app node, where your application filters are configured.</span></span>

<span data-ttu-id="4e19b-136">tooget hello les résultats plus précis, filtre de hello doivent être mappés avant tous les autres filtres.</span><span class="sxs-lookup"><span data-stu-id="4e19b-136">tooget hello most accurate results, hello filter should be mapped before all other filters.</span></span>

```XML

    <filter>
      <filter-name>ApplicationInsightsWebFilter</filter-name>
      <filter-class>
        com.microsoft.applicationinsights.web.internal.WebRequestTrackingFilter
      </filter-class>
    </filter>
    <filter-mapping>
       <filter-name>ApplicationInsightsWebFilter</filter-name>
       <url-pattern>/*</url-pattern>
    </filter-mapping>
```

## <a name="5-check-firewall-exceptions"></a><span data-ttu-id="4e19b-137">5. Vérifier les exceptions de pare-feu</span><span class="sxs-lookup"><span data-stu-id="4e19b-137">5. Check firewall exceptions</span></span>
<span data-ttu-id="4e19b-138">Vous devrez peut-être trop[toosend les données sortantes de définir des exceptions](app-insights-ip-addresses.md).</span><span class="sxs-lookup"><span data-stu-id="4e19b-138">You might need too[set exceptions toosend outgoing data](app-insights-ip-addresses.md).</span></span>

## <a name="6-restart-your-web-app"></a><span data-ttu-id="4e19b-139">6. Redémarrer votre application web</span><span class="sxs-lookup"><span data-stu-id="4e19b-139">6. Restart your web app</span></span>
## <a name="7-view-your-telemetry-in-application-insights"></a><span data-ttu-id="4e19b-140">7. Voir votre télémétrie dans Application Insights</span><span class="sxs-lookup"><span data-stu-id="4e19b-140">7. View your telemetry in Application Insights</span></span>
<span data-ttu-id="4e19b-141">Retourner la ressource Application Insights tooyour [portail Microsoft Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4e19b-141">Return tooyour Application Insights resource in [Microsoft Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="4e19b-142">Télémétrie sur les requêtes HTTP s’affiche sur le panneau de vue d’ensemble de hello.</span><span class="sxs-lookup"><span data-stu-id="4e19b-142">Telemetry about HTTP requests appears on hello overview blade.</span></span> <span data-ttu-id="4e19b-143">(Si elles n’y sont pas, attendez quelques secondes et cliquez sur Actualiser).</span><span class="sxs-lookup"><span data-stu-id="4e19b-143">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![Exemples de données](./media/app-insights-java-live/5-results.png)

<span data-ttu-id="4e19b-145">Cliquez sur via n’importe quel toosee graphique plus des métriques.</span><span class="sxs-lookup"><span data-stu-id="4e19b-145">Click through any chart toosee more detailed metrics.</span></span> 

![](./media/app-insights-java-live/6-barchart.png)

<span data-ttu-id="4e19b-146">Et lorsque vous affichez les propriétés hello d’une demande, vous pouvez voir les événements de télémétrie hello associés tels que les demandes et les exceptions.</span><span class="sxs-lookup"><span data-stu-id="4e19b-146">And when viewing hello properties of a request, you can see hello telemetry events associated with it such as requests and exceptions.</span></span>

![](./media/app-insights-java-live/7-instance.png)

[<span data-ttu-id="4e19b-147">En savoir plus sur les mesures.</span><span class="sxs-lookup"><span data-stu-id="4e19b-147">Learn more about metrics.</span></span>](app-insights-metrics-explorer.md)

## <a name="next-steps"></a><span data-ttu-id="4e19b-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4e19b-148">Next steps</span></span>
* <span data-ttu-id="4e19b-149">[Ajouter des pages web télémétrie tooyour](app-insights-javascript.md) toomonitor page des vues et des mesures de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4e19b-149">[Add telemetry tooyour web pages](app-insights-javascript.md) toomonitor page views and user metrics.</span></span>
* <span data-ttu-id="4e19b-150">[Configurer des tests web](app-insights-monitor-web-app-availability.md) toomake que votre application reste en direct et réactives.</span><span class="sxs-lookup"><span data-stu-id="4e19b-150">[Set up web tests](app-insights-monitor-web-app-availability.md) toomake sure your application stays live and responsive.</span></span>
* [<span data-ttu-id="4e19b-151">Capture le suivi des journaux</span><span class="sxs-lookup"><span data-stu-id="4e19b-151">Capture log traces</span></span>](app-insights-java-trace-logs.md)
* <span data-ttu-id="4e19b-152">[Rechercher des événements et journaux](app-insights-diagnostic-search.md) toohelp diagnostiquer les problèmes.</span><span class="sxs-lookup"><span data-stu-id="4e19b-152">[Search events and logs](app-insights-diagnostic-search.md) toohelp diagnose problems.</span></span>

