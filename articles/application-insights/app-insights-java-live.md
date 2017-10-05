---
title: "Application Insights pour les applications web qui sont déjà actives"
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
ms.openlocfilehash: a2731e3e44f8f3d104d8abc7dbe71fe3a4c3a690
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="application-insights-for-java-web-apps-that-are-already-live"></a><span data-ttu-id="26848-103">Application Insights pour les applications web qui sont déjà actives</span><span class="sxs-lookup"><span data-stu-id="26848-103">Application Insights for Java web apps that are already live</span></span>


<span data-ttu-id="26848-104">Si vous disposez d’une application web qui est déjà en cours d’exécution sur votre serveur J2EE, vous pouvez commencer à la surveiller avec [Application Insights](app-insights-overview.md) sans avoir à modifier le code ni à recompiler votre projet.</span><span class="sxs-lookup"><span data-stu-id="26848-104">If you have a web application that is already running on your J2EE server, you can start monitoring it with [Application Insights](app-insights-overview.md) without the need to make code changes or recompile your project.</span></span> <span data-ttu-id="26848-105">Grâce à cette option, vous obtenez des informations sur les requêtes HTTP envoyées à votre serveur, les exceptions non gérées et les compteurs de performances.</span><span class="sxs-lookup"><span data-stu-id="26848-105">With this option, you get information about HTTP requests sent to your server, unhandled exceptions, and performance counters.</span></span>

<span data-ttu-id="26848-106">Vous devrez vous abonner à [Microsoft Azure](https://azure.com).</span><span class="sxs-lookup"><span data-stu-id="26848-106">You'll need a subscription to [Microsoft Azure](https://azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="26848-107">La procédure décrite ici ajoute le Kit de développement logiciel (SDK) à votre application web au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="26848-107">The procedure on this page adds the SDK to your web app at runtime.</span></span> <span data-ttu-id="26848-108">Cette instrumentation du runtime est utile si vous ne souhaitez pas mettre à jour ni régénérer votre code source.</span><span class="sxs-lookup"><span data-stu-id="26848-108">This runtime instrumentation is useful if you don't want to update or rebuild your source code.</span></span> <span data-ttu-id="26848-109">Mais si vous le pouvez, nous vous recommandons plutôt d’ [ajouter le Kit de développement logiciel au code source](app-insights-java-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="26848-109">But if you can, we recommend you [add the SDK to the source code](app-insights-java-get-started.md) instead.</span></span> <span data-ttu-id="26848-110">Cette approche vous offre davantage d’options, telles que l’écriture de code pour effectuer le suivi de l’activité des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="26848-110">That gives you more options such as writing code to track user activity.</span></span>
> 
> 

## <a name="1-get-an-application-insights-instrumentation-key"></a><span data-ttu-id="26848-111">1. Obtenir une clé d'instrumentation Application Insights</span><span class="sxs-lookup"><span data-stu-id="26848-111">1. Get an Application Insights instrumentation key</span></span>
1. <span data-ttu-id="26848-112">Se connecter au [portail Microsoft Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="26848-112">Sign in to the [Microsoft Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="26848-113">Créez une ressource Application Insights et paramétrez le type d’application sur application web Java.</span><span class="sxs-lookup"><span data-stu-id="26848-113">Create a new Application Insights resource and set the application type to Java web application.</span></span>
   
    ![Indiquez le nom, choisissez l’application web Java, puis cliquez sur Créer.](./media/app-insights-java-live/02-create.png)

    <span data-ttu-id="26848-115">La ressource est créée en quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="26848-115">The resource is created in a few seconds.</span></span>

4. <span data-ttu-id="26848-116">Ouvrez la nouvelle ressource et obtenez sa clé d’instrumentation.</span><span class="sxs-lookup"><span data-stu-id="26848-116">Open the new resource and get its instrumentation key.</span></span> <span data-ttu-id="26848-117">Vous devrez la coller rapidement dans le code de votre projet.</span><span class="sxs-lookup"><span data-stu-id="26848-117">You'll need to paste this key into your code project shortly.</span></span>
   
    ![Dans la nouvelle vue d'ensemble des ressources, cliquez sur Propriétés et copiez la clé d'instrumentation.](./media/app-insights-java-live/03-key.png)

## <a name="2-download-the-sdk"></a><span data-ttu-id="26848-119">2. Télécharger le Kit de développement logiciel (SDK)</span><span class="sxs-lookup"><span data-stu-id="26848-119">2. Download the SDK</span></span>
1. <span data-ttu-id="26848-120">Téléchargez le [Kit de développement logiciel (SDK) Application Insights pour Java](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="26848-120">Download the [Application Insights SDK for Java](https://aka.ms/aijavasdk).</span></span> 
2. <span data-ttu-id="26848-121">Sur votre serveur, extrayez le contenu du Kit de développement logiciel dans le répertoire à partir duquel les fichiers binaires de votre projet sont chargés.</span><span class="sxs-lookup"><span data-stu-id="26848-121">On your server, extract the SDK contents to the directory from which your project binaries are loaded.</span></span> <span data-ttu-id="26848-122">Si vous utilisez Tomcat, ce répertoire se trouve généralement sous `webapps/<your_app_name>/WEB-INF/lib`</span><span class="sxs-lookup"><span data-stu-id="26848-122">If you’re using Tomcat, this directory would typically be under `webapps/<your_app_name>/WEB-INF/lib`</span></span>

<span data-ttu-id="26848-123">Notez que vous devez répéter cette opération pour chaque application sur chaque instance de serveur.</span><span class="sxs-lookup"><span data-stu-id="26848-123">Note that you need to repeat this on each server instance, and for each app.</span></span>

## <a name="3-add-an-application-insights-xml-file"></a><span data-ttu-id="26848-124">3. Ajouter un fichier xml Application Insights</span><span class="sxs-lookup"><span data-stu-id="26848-124">3. Add an Application Insights xml file</span></span>
<span data-ttu-id="26848-125">Créez le fichier ApplicationInsights.xml dans le dossier auquel vous avez ajouté le Kit de développement logiciel.</span><span class="sxs-lookup"><span data-stu-id="26848-125">Create ApplicationInsights.xml in the folder in which you added the SDK.</span></span> <span data-ttu-id="26848-126">Placez-y le code XML suivant.</span><span class="sxs-lookup"><span data-stu-id="26848-126">Put into it the following XML.</span></span>

<span data-ttu-id="26848-127">Remplacez la clé d'instrumentation que avez obtenue sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="26848-127">Substitute the instrumentation key that you got from the Azure portal.</span></span>

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsights xmlns="http://schemas.microsoft.com/ApplicationInsights/2013/Settings" schemaVersion="2014-05-30">


      <!-- The key from the portal: -->

      <InstrumentationKey>** Your instrumentation key **</InstrumentationKey>


      <!-- HTTP request component (not required for bare API) -->

      <TelemetryModules>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebRequestTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebSessionTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebUserTrackingTelemetryModule"/>
      </TelemetryModules>

      <!-- Events correlation (not required for bare API) -->
      <!-- These initializers add context data to each event -->

      <TelemetryInitializers>
        <Add   type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationIdTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationNameTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebSessionTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserAgentTelemetryInitializer"/>

      </TelemetryInitializers>
    </ApplicationInsights>
```

* <span data-ttu-id="26848-128">La clé d'instrumentation est envoyée avec chaque élément de télémétrie et indique à Application Insights de l'afficher dans votre ressource.</span><span class="sxs-lookup"><span data-stu-id="26848-128">The instrumentation key is sent along with every item of telemetry and tells Application Insights to display it in your resource.</span></span>
* <span data-ttu-id="26848-129">Le composant de demande HTTP est facultatif.</span><span class="sxs-lookup"><span data-stu-id="26848-129">The HTTP Request component is optional.</span></span> <span data-ttu-id="26848-130">Il envoie automatiquement la télémétrie concernant les demandes et les temps de réponse au portail.</span><span class="sxs-lookup"><span data-stu-id="26848-130">It automatically sends telemetry about requests and response times to the portal.</span></span>
* <span data-ttu-id="26848-131">La corrélation des événements est un complément au composant de demande HTTP.</span><span class="sxs-lookup"><span data-stu-id="26848-131">Events correlation is an addition to the HTTP request component.</span></span> <span data-ttu-id="26848-132">Il assigne un identificateur à chaque demande reçue par le serveur et l'ajoute comme propriété de chaque élément de télémétrie en tant que propriété « Operation.Id ».</span><span class="sxs-lookup"><span data-stu-id="26848-132">It assigns an identifier to each request received by the server, and adds this identifier as a property to every item of telemetry as the property 'Operation.Id'.</span></span> <span data-ttu-id="26848-133">Il vous permet de mettre en corrélation la télémétrie associée à chaque demande en définissant un filtre dans [recherche de diagnostic](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="26848-133">It allows you to correlate the telemetry associated with each request by setting a filter in [diagnostic search](app-insights-diagnostic-search.md).</span></span>

## <a name="4-add-an-http-filter"></a><span data-ttu-id="26848-134">4. Ajouter un filtre HTTP</span><span class="sxs-lookup"><span data-stu-id="26848-134">4. Add an HTTP filter</span></span>
<span data-ttu-id="26848-135">Recherchez et ouvrez le fichier web.xml dans votre projet et fusionnez l'extrait de code suivant sous le nœud de l'application web, où vos filtres d'application sont configurés.</span><span class="sxs-lookup"><span data-stu-id="26848-135">Locate and open the web.xml file in your project, and merge the following snippet of code under the web-app node, where your application filters are configured.</span></span>

<span data-ttu-id="26848-136">Pour obtenir des résultats plus précis, le filtre doit être mappé avant tous les autres filtres.</span><span class="sxs-lookup"><span data-stu-id="26848-136">To get the most accurate results, the filter should be mapped before all other filters.</span></span>

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

## <a name="5-check-firewall-exceptions"></a><span data-ttu-id="26848-137">5. Vérifier les exceptions de pare-feu</span><span class="sxs-lookup"><span data-stu-id="26848-137">5. Check firewall exceptions</span></span>
<span data-ttu-id="26848-138">Vous devrez peut-être [définir des exceptions pour envoyer les données sortantes](app-insights-ip-addresses.md).</span><span class="sxs-lookup"><span data-stu-id="26848-138">You might need to [set exceptions to send outgoing data](app-insights-ip-addresses.md).</span></span>

## <a name="6-restart-your-web-app"></a><span data-ttu-id="26848-139">6. Redémarrer votre application web</span><span class="sxs-lookup"><span data-stu-id="26848-139">6. Restart your web app</span></span>
## <a name="7-view-your-telemetry-in-application-insights"></a><span data-ttu-id="26848-140">7. Voir votre télémétrie dans Application Insights</span><span class="sxs-lookup"><span data-stu-id="26848-140">7. View your telemetry in Application Insights</span></span>
<span data-ttu-id="26848-141">Revenez à votre ressource Application Insights sur le [portail Microsoft Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="26848-141">Return to your Application Insights resource in [Microsoft Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="26848-142">La télémétrie des demandes HTTP apparaît dans le panneau Vue d’ensemble.</span><span class="sxs-lookup"><span data-stu-id="26848-142">Telemetry about HTTP requests appears on the overview blade.</span></span> <span data-ttu-id="26848-143">(Si elles n’y sont pas, attendez quelques secondes et cliquez sur Actualiser).</span><span class="sxs-lookup"><span data-stu-id="26848-143">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![Exemples de données](./media/app-insights-java-live/5-results.png)

<span data-ttu-id="26848-145">Cliquez sur un des graphiques pour afficher des mesures plus détaillées.</span><span class="sxs-lookup"><span data-stu-id="26848-145">Click through any chart to see more detailed metrics.</span></span> 

![](./media/app-insights-java-live/6-barchart.png)

<span data-ttu-id="26848-146">Et lorsque vous affichez les propriétés d'une demande, vous voyez les événements de télémétrie associés, par exemple les demandes et les exceptions.</span><span class="sxs-lookup"><span data-stu-id="26848-146">And when viewing the properties of a request, you can see the telemetry events associated with it such as requests and exceptions.</span></span>

![](./media/app-insights-java-live/7-instance.png)

[<span data-ttu-id="26848-147">En savoir plus sur les mesures.</span><span class="sxs-lookup"><span data-stu-id="26848-147">Learn more about metrics.</span></span>](app-insights-metrics-explorer.md)

## <a name="next-steps"></a><span data-ttu-id="26848-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="26848-148">Next steps</span></span>
* <span data-ttu-id="26848-149">[Ajoutez la télémétrie à vos pages web](app-insights-javascript.md) pour surveiller les affichages de pages et les mesures relatives à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="26848-149">[Add telemetry to your web pages](app-insights-javascript.md) to monitor page views and user metrics.</span></span>
* <span data-ttu-id="26848-150">[Configurez les tests web](app-insights-monitor-web-app-availability.md) pour vous assurer que votre application est bien active.</span><span class="sxs-lookup"><span data-stu-id="26848-150">[Set up web tests](app-insights-monitor-web-app-availability.md) to make sure your application stays live and responsive.</span></span>
* [<span data-ttu-id="26848-151">Capture le suivi des journaux</span><span class="sxs-lookup"><span data-stu-id="26848-151">Capture log traces</span></span>](app-insights-java-trace-logs.md)
* <span data-ttu-id="26848-152">[Recherchez les événements et les journaux](app-insights-diagnostic-search.md) pour diagnostiquer les problèmes.</span><span class="sxs-lookup"><span data-stu-id="26848-152">[Search events and logs](app-insights-diagnostic-search.md) to help diagnose problems.</span></span>

