---
title: "Analyse d’une application web Java avec Azure Application Insights | Microsoft Docs"
description: "Analyse des performances des applications pour les applications web Java à l’aide d’Application Insights. "
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 051d4285-f38a-45d8-ad8a-45c3be828d91
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: a75815885d7ccd7cd56db3da2f3f92cae78fe033
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-application-insights-in-a-java-web-project"></a><span data-ttu-id="93959-103">Prise en main d'Application Insights dans un projet web Java</span><span class="sxs-lookup"><span data-stu-id="93959-103">Get started with Application Insights in a Java web project</span></span>


<span data-ttu-id="93959-104">[Application Insights](https://azure.microsoft.com/services/application-insights/) est un service d’analyse extensible pour développeurs web qui vous permet de comprendre les performances et l’utilisation de votre application en direct.</span><span class="sxs-lookup"><span data-stu-id="93959-104">[Application Insights](https://azure.microsoft.com/services/application-insights/) is an extensible analytics service for web developers that helps you understand the performance and usage of your live application.</span></span> <span data-ttu-id="93959-105">Utilisez-le pour [détecter et diagnostiquer les problèmes de performances et les exceptions](app-insights-detect-triage-diagnose.md), ainsi que pour [écrire du code][api] afin de suivre ce que font les utilisateurs avec votre application.</span><span class="sxs-lookup"><span data-stu-id="93959-105">Use it to [detect and diagnose performance issues and exceptions](app-insights-detect-triage-diagnose.md), and [write code][api] to track what users do with your app.</span></span>

![Exemples de données](./media/app-insights-java-get-started/5-results.png)

<span data-ttu-id="93959-107">Application Insights prend en charge les applications Java exécutées sur Linux, Unix ou Windows.</span><span class="sxs-lookup"><span data-stu-id="93959-107">Application Insights supports Java apps running on Linux, Unix, or Windows.</span></span>

<span data-ttu-id="93959-108">Ce dont vous avez besoin :</span><span class="sxs-lookup"><span data-stu-id="93959-108">You need:</span></span>

* <span data-ttu-id="93959-109">Oracle JRE 1.6 ou version ultérieure ou Zoulou JRE 1.6 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="93959-109">Oracle JRE 1.6 or later, or Zulu JRE 1.6 or later</span></span>
* <span data-ttu-id="93959-110">Un abonnement à [Microsoft Azure](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="93959-110">A subscription to [Microsoft Azure](https://azure.microsoft.com/).</span></span>

<span data-ttu-id="93959-111">*Si vous disposez d’une application web déjà active, vous pouvez suivre la procédure alternative destinée à [ajouter le Kit de développement logiciel (SDK) au moment de l’exécution dans le serveur web](app-insights-java-live.md). Cette alternative évite la régénération du code, mais ne vous permet pas d’écrire du code pour effectuer le suivi de l’activité des utilisateurs.*</span><span class="sxs-lookup"><span data-stu-id="93959-111">*If you have a web app that's already live, you could follow the alternative procedure to [add the SDK at runtime in the web server](app-insights-java-live.md). That alternative avoids rebuilding the code, but you don't get the option to write code to track user activity.*</span></span>

## <a name="1-get-an-application-insights-instrumentation-key"></a><span data-ttu-id="93959-112">1. Obtenir une clé d'instrumentation Application Insights</span><span class="sxs-lookup"><span data-stu-id="93959-112">1. Get an Application Insights instrumentation key</span></span>
1. <span data-ttu-id="93959-113">Connectez-vous au [portail Microsoft Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="93959-113">Sign in to the [Microsoft Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="93959-114">Créez une ressource Application Insights.</span><span class="sxs-lookup"><span data-stu-id="93959-114">Create an Application Insights resource.</span></span> <span data-ttu-id="93959-115">Définissez le type d’application sur Application web Java.</span><span class="sxs-lookup"><span data-stu-id="93959-115">Set the application type to Java web application.</span></span>

    ![Indiquez le nom, choisissez l’application web Java, puis cliquez sur Créer.](./media/app-insights-java-get-started/02-create.png)
3. <span data-ttu-id="93959-117">Obtenez la clé d'instrumentation de la nouvelle ressource.</span><span class="sxs-lookup"><span data-stu-id="93959-117">Find the instrumentation key of the new resource.</span></span> <span data-ttu-id="93959-118">Vous devrez la coller rapidement dans le code de votre projet.</span><span class="sxs-lookup"><span data-stu-id="93959-118">You'll need to paste this key into your code project shortly.</span></span>

    ![Dans la nouvelle vue d'ensemble des ressources, cliquez sur Propriétés et copiez la clé d'instrumentation.](./media/app-insights-java-get-started/03-key.png)

## <a name="2-add-the-application-insights-sdk-for-java-to-your-project"></a><span data-ttu-id="93959-120">2. Ajoutez le Kit de développement logiciel (SDK) Application Insights pour Java à votre projet</span><span class="sxs-lookup"><span data-stu-id="93959-120">2. Add the Application Insights SDK for Java to your project</span></span>
<span data-ttu-id="93959-121">*Choisissez la méthode adaptée à votre projet.*</span><span class="sxs-lookup"><span data-stu-id="93959-121">*Choose the appropriate way for your project.*</span></span>

#### <a name="if-youre-using-eclipse-to-create-a-maven-or-dynamic-web-project-"></a><span data-ttu-id="93959-122">Si vous utilisez Eclipse pour créer un projet Maven ou un projet web dynamique...</span><span class="sxs-lookup"><span data-stu-id="93959-122">If you're using Eclipse to create a Maven or Dynamic Web project ...</span></span>
<span data-ttu-id="93959-123">Utilisez le [Kit de développement logiciel (SDK) Application Insights pour plug-in Java][eclipse].</span><span class="sxs-lookup"><span data-stu-id="93959-123">Use the [Application Insights SDK for Java plug-in][eclipse].</span></span>

#### <a name="if-youre-using-maven"></a><span data-ttu-id="93959-124">Si vous utilisez Maven...</span><span class="sxs-lookup"><span data-stu-id="93959-124">If you're using Maven...</span></span>
<span data-ttu-id="93959-125">Si votre projet est déjà configuré pour être assemblé avec Maven, fusionnez le code suivant dans votre fichier pom.xml.</span><span class="sxs-lookup"><span data-stu-id="93959-125">If your project is already set up to use Maven for build, merge the following code to your pom.xml file.</span></span>

<span data-ttu-id="93959-126">Actualisez ensuite les dépendances du projet pour télécharger les fichiers binaires.</span><span class="sxs-lookup"><span data-stu-id="93959-126">Then, refresh the project dependencies to get the binaries downloaded.</span></span>

```XML

    <repositories>
       <repository>
          <id>central</id>
          <name>Central</name>
          <url>http://repo1.maven.org/maven2</url>
       </repository>
    </repositories>

    <dependencies>
      <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>applicationinsights-web</artifactId>
        <!-- or applicationinsights-core for bare API -->
        <version>[1.0,)</version>
      </dependency>
    </dependencies>
```

* <span data-ttu-id="93959-127">*Des erreurs de validation de build ou de somme de contrôle ?*</span><span class="sxs-lookup"><span data-stu-id="93959-127">*Build or checksum validation errors?*</span></span> <span data-ttu-id="93959-128">Essayez d’utiliser une version spécifique, telle que : `<version>1.0.n</version>`.</span><span class="sxs-lookup"><span data-stu-id="93959-128">Try using a specific version, such as: `<version>1.0.n</version>`.</span></span> <span data-ttu-id="93959-129">Vous trouverez la version la plus récente dans les [notes de publication du Kit de développement logiciel (SDK)](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) ou dans nos [artefacts Maven](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights).</span><span class="sxs-lookup"><span data-stu-id="93959-129">You'll find the latest version in the [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) or in our [Maven artifacts](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights).</span></span>
* <span data-ttu-id="93959-130">*Besoin de mettre à jour vers un nouveau Kit de développement logiciel (SDK) ?*</span><span class="sxs-lookup"><span data-stu-id="93959-130">*Need to update to a new SDK?*</span></span> <span data-ttu-id="93959-131">Actualisez les dépendances de votre projet.</span><span class="sxs-lookup"><span data-stu-id="93959-131">Refresh your project's dependencies.</span></span>

#### <a name="if-youre-using-gradle"></a><span data-ttu-id="93959-132">Si vous utilisez Gradle...</span><span class="sxs-lookup"><span data-stu-id="93959-132">If you're using Gradle...</span></span>
<span data-ttu-id="93959-133">Si votre projet est déjà configuré pour être assemblé avec Gradle, fusionnez le code suivant dans votre fichier build.gradle.xml.</span><span class="sxs-lookup"><span data-stu-id="93959-133">If your project is already set up to use Gradle for build, merge the following code to your build.gradle file.</span></span>

<span data-ttu-id="93959-134">Actualisez ensuite les dépendances du projet pour télécharger les fichiers binaires.</span><span class="sxs-lookup"><span data-stu-id="93959-134">Then refresh the project dependencies to get the binaries downloaded.</span></span>

```JSON

    repositories {
      mavenCentral()
    }

    dependencies {
      compile group: 'com.microsoft.azure', name: 'applicationinsights-web', version: '1.+'
      // or applicationinsights-core for bare API
    }
```

* <span data-ttu-id="93959-135">*Erreurs de validation de build ou de somme de contrôle ? Essayez d’utiliser une version spécifique, telle que :* `version:'1.0.n'`.</span><span class="sxs-lookup"><span data-stu-id="93959-135">*Build or checksum validation errors? Try using a specific version, such as:* `version:'1.0.n'`.</span></span> <span data-ttu-id="93959-136">*Vous trouverez la version la plus récente dans les [notes de publication du kit de développement logiciel (SDK)](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).*</span><span class="sxs-lookup"><span data-stu-id="93959-136">*You'll find the latest version in the [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).*</span></span>
* <span data-ttu-id="93959-137">*Pour effecteur la mise à jour vers un nouveau kit de développement logiciel (SDK)*</span><span class="sxs-lookup"><span data-stu-id="93959-137">*To update to a new SDK*</span></span>
  * <span data-ttu-id="93959-138">Actualisez les dépendances de votre projet.</span><span class="sxs-lookup"><span data-stu-id="93959-138">Refresh your project's dependencies.</span></span>

#### <a name="otherwise-"></a><span data-ttu-id="93959-139">Sinon...</span><span class="sxs-lookup"><span data-stu-id="93959-139">Otherwise ...</span></span>
<span data-ttu-id="93959-140">Ajouter manuellement le Kit de développement logiciel :</span><span class="sxs-lookup"><span data-stu-id="93959-140">Manually add the SDK:</span></span>

1. <span data-ttu-id="93959-141">Téléchargez le [Kit de développement logiciel (SDK) Application Insights pour Java](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="93959-141">Download the [Application Insights SDK for Java](https://aka.ms/aijavasdk).</span></span>
2. <span data-ttu-id="93959-142">Décompressez les fichiers binaires du fichier zip et ajoutez-les à votre projet.</span><span class="sxs-lookup"><span data-stu-id="93959-142">Extract the binaries from the zip file and add them to your project.</span></span>

### <a name="questions"></a><span data-ttu-id="93959-143">Questions...</span><span class="sxs-lookup"><span data-stu-id="93959-143">Questions...</span></span>
* <span data-ttu-id="93959-144">*Quelle est la relation entre les composants `-core` et `-web` du fichier zip ?*</span><span class="sxs-lookup"><span data-stu-id="93959-144">*What's the relationship between the `-core` and `-web` components in the zip?*</span></span>

  * <span data-ttu-id="93959-145">`applicationinsights-core` vous fournit l’API seule.</span><span class="sxs-lookup"><span data-stu-id="93959-145">`applicationinsights-core` gives you the bare API.</span></span> <span data-ttu-id="93959-146">Ce composant est toujours requis.</span><span class="sxs-lookup"><span data-stu-id="93959-146">You always need this component.</span></span>
  * <span data-ttu-id="93959-147">`applicationinsights-web` fournit des mesures qui permettent d’effectuer le suivi du nombre de requêtes HTTP et des temps de réponse.</span><span class="sxs-lookup"><span data-stu-id="93959-147">`applicationinsights-web` gives you metrics that track HTTP request counts and response times.</span></span> <span data-ttu-id="93959-148">Vous pouvez omettre ce composant si vous ne souhaitez pas recueillir automatiquement ces données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="93959-148">You can omit this component if you don't want this telemetry automatically collected.</span></span> <span data-ttu-id="93959-149">Par exemple, si vous préférez écrire vos propres mesures.</span><span class="sxs-lookup"><span data-stu-id="93959-149">For example, if you want to write your own.</span></span>
* <span data-ttu-id="93959-150">*Pour mettre à jour le Kit de développement logiciel lorsque nous publions des modifications*</span><span class="sxs-lookup"><span data-stu-id="93959-150">*To update the SDK when we publish changes*</span></span>

  * <span data-ttu-id="93959-151">Téléchargez le dernier [Kit de développement logiciel Application Insights pour Java](https://aka.ms/qqkaq6) et remplacez les anciens Kits.</span><span class="sxs-lookup"><span data-stu-id="93959-151">Download the latest [Application Insights SDK for Java](https://aka.ms/qqkaq6) and replace the old ones.</span></span>
  * <span data-ttu-id="93959-152">Les modifications sont décrites dans le [notes de publication du kit de développement logiciel (SDK)](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).</span><span class="sxs-lookup"><span data-stu-id="93959-152">Changes are described in the [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).</span></span>

## <a name="3-add-an-application-insights-xml-file"></a><span data-ttu-id="93959-153">3. Ajouter un fichier .xml Application Insights</span><span class="sxs-lookup"><span data-stu-id="93959-153">3. Add an Application Insights .xml file</span></span>
<span data-ttu-id="93959-154">Ajoutez ApplicationInsights.xml dans le dossier de ressources de votre projet, ou vérifiez qu’il est ajouté au chemin de la classe du déploiement de votre projet.</span><span class="sxs-lookup"><span data-stu-id="93959-154">Add ApplicationInsights.xml to the resources folder in your project, or make sure it is added to your project’s deployment class path.</span></span> <span data-ttu-id="93959-155">Copiez-y le code XML suivant.</span><span class="sxs-lookup"><span data-stu-id="93959-155">Copy the following XML into it.</span></span>

<span data-ttu-id="93959-156">Remplacez la clé d'instrumentation que avez obtenue sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="93959-156">Substitute the instrumentation key that you got from the Azure portal.</span></span>

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


* <span data-ttu-id="93959-157">La clé d'instrumentation est envoyée avec chaque élément de télémétrie et indique à Application Insights de l'afficher dans votre ressource.</span><span class="sxs-lookup"><span data-stu-id="93959-157">The instrumentation key is sent along with every item of telemetry and tells Application Insights to display it in your resource.</span></span>
* <span data-ttu-id="93959-158">Le composant de demande HTTP est facultatif.</span><span class="sxs-lookup"><span data-stu-id="93959-158">The HTTP Request component is optional.</span></span> <span data-ttu-id="93959-159">Il envoie automatiquement la télémétrie concernant les demandes et les temps de réponse au portail.</span><span class="sxs-lookup"><span data-stu-id="93959-159">It automatically sends telemetry about requests and response times to the portal.</span></span>
* <span data-ttu-id="93959-160">La corrélation des événements est un complément au composant de demande HTTP.</span><span class="sxs-lookup"><span data-stu-id="93959-160">Events correlation is an addition to the HTTP request component.</span></span> <span data-ttu-id="93959-161">Il assigne un identificateur à chaque demande reçue par le serveur et l'ajoute comme propriété de chaque élément de télémétrie en tant que propriété « Operation.Id ».</span><span class="sxs-lookup"><span data-stu-id="93959-161">It assigns an identifier to each request received by the server, and adds this identifier as a property to every item of telemetry as the property 'Operation.Id'.</span></span> <span data-ttu-id="93959-162">Il vous permet de mettre en corrélation la télémétrie associée à chaque demande en définissant un filtre dans [recherche de diagnostic][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="93959-162">It allows you to correlate the telemetry associated with each request by setting a filter in [diagnostic search][diagnostic].</span></span>
* <span data-ttu-id="93959-163">La clé Application Insights peut être transmise de manière dynamique à partir du Portail Azure sous la forme d’une propriété système (-DAPPLICATION_INSIGHTS_IKEY=votre_iKey).</span><span class="sxs-lookup"><span data-stu-id="93959-163">The Application Insights key can be passed dynamically from the Azure portal as a system property (-DAPPLICATION_INSIGHTS_IKEY=your_ikey).</span></span> <span data-ttu-id="93959-164">Si aucune propriété n’est définie, la variable d’environnement (APPLICATION_INSIGHTS_IKEY) est recherchée dans les paramètres d’application Azure.</span><span class="sxs-lookup"><span data-stu-id="93959-164">If there is no property defined, it checks for environment variable (APPLICATION_INSIGHTS_IKEY) in Azure App Settings.</span></span> <span data-ttu-id="93959-165">Si aucune de ces deux propriétés n’est définie, la clé InstrumentationKey par défaut est utilisée à partir d’ApplicationInsights.xml.</span><span class="sxs-lookup"><span data-stu-id="93959-165">If both the properties are undefined, the default InstrumentationKey is used from ApplicationInsights.xml.</span></span> <span data-ttu-id="93959-166">Cette séquence vous aide à gérer dynamiquement divers éléments InstrumentationKeys pour différents environnements.</span><span class="sxs-lookup"><span data-stu-id="93959-166">This sequence helps you to manage different InstrumentationKeys for different environments dynamically.</span></span>

### <a name="alternative-ways-to-set-the-instrumentation-key"></a><span data-ttu-id="93959-167">Autres méthodes pour définir la clé d’instrumentation</span><span class="sxs-lookup"><span data-stu-id="93959-167">Alternative ways to set the instrumentation key</span></span>
<span data-ttu-id="93959-168">Le kit de développement logiciel (SDK) d’Application Insights recherche la clé dans cet ordre :</span><span class="sxs-lookup"><span data-stu-id="93959-168">Application Insights SDK looks for the key in this order:</span></span>

1. <span data-ttu-id="93959-169">Propriété système : -DAPPLICATION_INSIGHTS_IKEY=votre_ikey</span><span class="sxs-lookup"><span data-stu-id="93959-169">System property: -DAPPLICATION_INSIGHTS_IKEY=your_ikey</span></span>
2. <span data-ttu-id="93959-170">Variable d’environnement : APPLICATION_INSIGHTS_IKEY</span><span class="sxs-lookup"><span data-stu-id="93959-170">Environment variable: APPLICATION_INSIGHTS_IKEY</span></span>
3. <span data-ttu-id="93959-171">Fichier de configuration : ApplicationInsights.xml</span><span class="sxs-lookup"><span data-stu-id="93959-171">Configuration file: ApplicationInsights.xml</span></span>

<span data-ttu-id="93959-172">Vous pouvez également [définir la clé dans le code](app-insights-api-custom-events-metrics.md#ikey):</span><span class="sxs-lookup"><span data-stu-id="93959-172">You can also [set it in code](app-insights-api-custom-events-metrics.md#ikey):</span></span>

```Java

    telemetryClient.InstrumentationKey = "...";
```

## <a name="4-add-an-http-filter"></a><span data-ttu-id="93959-173">4. Ajouter un filtre HTTP</span><span class="sxs-lookup"><span data-stu-id="93959-173">4. Add an HTTP filter</span></span>
<span data-ttu-id="93959-174">La dernière étape de la configuration permet au composant de demande HTTP de consigner toutes les demandes web.</span><span class="sxs-lookup"><span data-stu-id="93959-174">The last configuration step allows the HTTP request component to log each web request.</span></span> <span data-ttu-id="93959-175">(Non requis si vous voulez juste l'API seule.)</span><span class="sxs-lookup"><span data-stu-id="93959-175">(Not required if you just want the bare API.)</span></span>

<span data-ttu-id="93959-176">Recherchez et ouvrez le fichier web.xml dans votre projet et fusionnez le code suivant sous le nœud de l'application web, où vos filtres d'application sont configurés.</span><span class="sxs-lookup"><span data-stu-id="93959-176">Locate and open the web.xml file in your project, and merge the following code under the web-app node, where your application filters are configured.</span></span>

<span data-ttu-id="93959-177">Pour obtenir des résultats plus précis, le filtre doit être mappé avant tous les autres filtres.</span><span class="sxs-lookup"><span data-stu-id="93959-177">To get the most accurate results, the filter should be mapped before all other filters.</span></span>

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

#### <a name="if-youre-using-spring-web-mvc-31-or-later"></a><span data-ttu-id="93959-178">Si vous utilisez Spring Web MVC 3.1 ou une version ultérieure</span><span class="sxs-lookup"><span data-stu-id="93959-178">If you're using Spring Web MVC 3.1 or later</span></span>
<span data-ttu-id="93959-179">Modifiez ces éléments dans *-servlet.xml pour inclure le package Application Insights :</span><span class="sxs-lookup"><span data-stu-id="93959-179">Edit these elements in *-servlet.xml to include the Application Insights package:</span></span>

```XML

    <context:component-scan base-package=" com.springapp.mvc, com.microsoft.applicationinsights.web.spring"/>

    <mvc:interceptors>
        <mvc:interceptor>
            <mvc:mapping path="/**"/>
            <bean class="com.microsoft.applicationinsights.web.spring.RequestNameHandlerInterceptorAdapter" />
        </mvc:interceptor>
    </mvc:interceptors>
```

#### <a name="if-youre-using-struts-2"></a><span data-ttu-id="93959-180">Si vous utilisez Struts 2</span><span class="sxs-lookup"><span data-stu-id="93959-180">If you're using Struts 2</span></span>
<span data-ttu-id="93959-181">Ajoutez cet élément au fichier de configuration Struts (généralement struts.xml ou struts-default.xml) :</span><span class="sxs-lookup"><span data-stu-id="93959-181">Add this item to the Struts configuration file (usually named struts.xml or struts-default.xml):</span></span>

```XML

     <interceptors>
       <interceptor name="ApplicationInsightsRequestNameInterceptor" class="com.microsoft.applicationinsights.web.struts.RequestNameInterceptor" />
     </interceptors>
     <default-interceptor-ref name="ApplicationInsightsRequestNameInterceptor" />
```

<span data-ttu-id="93959-182">(Si vous avez défini des intercepteurs dans une pile par défaut, l'intercepteur peut simplement être ajouté à cette pile).</span><span class="sxs-lookup"><span data-stu-id="93959-182">(If you have interceptors defined in a default stack, the interceptor can simply be added to that stack.)</span></span>

## <a name="5-run-your-application"></a><span data-ttu-id="93959-183">5. Exécuter votre application</span><span class="sxs-lookup"><span data-stu-id="93959-183">5. Run your application</span></span>
<span data-ttu-id="93959-184">Exécutez-le en mode débogage sur votre ordinateur de développement, ou publiez-le sur votre serveur.</span><span class="sxs-lookup"><span data-stu-id="93959-184">Either run it in debug mode on your development machine, or publish to your server.</span></span>

## <a name="6-view-your-telemetry-in-application-insights"></a><span data-ttu-id="93959-185">6. Voir votre télémétrie dans Application Insights</span><span class="sxs-lookup"><span data-stu-id="93959-185">6. View your telemetry in Application Insights</span></span>
<span data-ttu-id="93959-186">Revenez à votre ressource Application Insights sur le [portail Microsoft Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="93959-186">Return to your Application Insights resource in [Microsoft Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="93959-187">Les données des demandes HTTP apparaissent dans le panneau Vue d’ensemble.</span><span class="sxs-lookup"><span data-stu-id="93959-187">HTTP requests data appears on the overview blade.</span></span> <span data-ttu-id="93959-188">(Si elles n’y sont pas, attendez quelques secondes et cliquez sur Actualiser).</span><span class="sxs-lookup"><span data-stu-id="93959-188">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![Exemples de données](./media/app-insights-java-get-started/5-results.png)

<span data-ttu-id="93959-190">[En savoir plus sur les mesures.][metrics]</span><span class="sxs-lookup"><span data-stu-id="93959-190">[Learn more about metrics.][metrics]</span></span>

<span data-ttu-id="93959-191">Cliquez sur un des graphiques pour afficher des métriques agrégées plus détaillées.</span><span class="sxs-lookup"><span data-stu-id="93959-191">Click through any chart to see more detailed aggregated metrics.</span></span>

![](./media/app-insights-java-get-started/6-barchart.png)

> <span data-ttu-id="93959-192">Application Insights repose sur l’hypothèse que le format des requêtes HTTP pour les applications MVC est le suivant : `VERB controller/action`.</span><span class="sxs-lookup"><span data-stu-id="93959-192">Application Insights assumes the format of HTTP requests for MVC applications is: `VERB controller/action`.</span></span> <span data-ttu-id="93959-193">Par exemple, `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` et `GET Home/Product/sdf96vws` sont regroupés dans `GET Home/Product`.</span><span class="sxs-lookup"><span data-stu-id="93959-193">For example, `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` and `GET Home/Product/sdf96vws` are grouped into `GET Home/Product`.</span></span> <span data-ttu-id="93959-194">Ceci permet l’agrégation correcte des demandes, par exemple le nombre de demandes et le temps moyen d’exécution des demandes.</span><span class="sxs-lookup"><span data-stu-id="93959-194">This grouping enables meaningful aggregations of requests, such as number of requests and average execution time for requests.</span></span>
>
>

### <a name="instance-data"></a><span data-ttu-id="93959-195">Données d’instance</span><span class="sxs-lookup"><span data-stu-id="93959-195">Instance data</span></span>
<span data-ttu-id="93959-196">Cliquez sur un type de demande spécifique pour afficher les instances individuelles.</span><span class="sxs-lookup"><span data-stu-id="93959-196">Click through a specific request type to see individual instances.</span></span>

<span data-ttu-id="93959-197">Deux types de données s’affichent dans Application Insights : des données agrégées, stockées et affichées sous forme de moyennes, de nombres et de sommes ; et les données d’instance : des rapports individuels des requêtes HTTP, des exceptions, les vues de page ou des événements personnalisés.</span><span class="sxs-lookup"><span data-stu-id="93959-197">Two kinds of data are displayed in Application Insights: aggregated data, stored and displayed as averages, counts, and sums; and instance data - individual reports of HTTP requests, exceptions, page views, or custom events.</span></span>

<span data-ttu-id="93959-198">Lorsque vous affichez les propriétés d’une demande, vous voyez les événements de télémétrie associés, par exemple les demandes et les exceptions.</span><span class="sxs-lookup"><span data-stu-id="93959-198">When viewing the properties of a request, you can see the telemetry events associated with it such as requests and exceptions.</span></span>

![](./media/app-insights-java-get-started/7-instance.png)

### <a name="analytics-powerful-query-language"></a><span data-ttu-id="93959-199">Analytics : un puissant langage de requête</span><span class="sxs-lookup"><span data-stu-id="93959-199">Analytics: Powerful query language</span></span>
<span data-ttu-id="93959-200">En accumulant toujours plus de données, vous pouvez exécuter des requêtes à la fois pour agréger les données et pour rechercher des instances individuelles.</span><span class="sxs-lookup"><span data-stu-id="93959-200">As you accumulate more data, you can run queries both to aggregate data and to find individual instances.</span></span>  <span data-ttu-id="93959-201">[Analytics](app-insights-analytics.md) est un outil puissant qui permet non seulement de comprendre les performances et l’utilisation, mais également d’effectuer des diagnostics.</span><span class="sxs-lookup"><span data-stu-id="93959-201">[Analytics](app-insights-analytics.md) is a powerful tool for both for understanding performance and usage, and for diagnostic purposes.</span></span>

![Exemple d’Analytics](./media/app-insights-java-get-started/025.png)

## <a name="7-install-your-app-on-the-server"></a><span data-ttu-id="93959-203">7. Installer votre application sur le serveur</span><span class="sxs-lookup"><span data-stu-id="93959-203">7. Install your app on the server</span></span>
<span data-ttu-id="93959-204">Publiez maintenant votre application sur le serveur, laissez le temps aux usagers de l’utiliser, puis observez les données de télémétrie qui s’affichent sur le portail.</span><span class="sxs-lookup"><span data-stu-id="93959-204">Now publish your app to the server, let people use it, and watch the telemetry show up on the portal.</span></span>

* <span data-ttu-id="93959-205">Assurez-vous que votre pare-feu autorise votre application à envoyer les données de télémétrie vers ces ports :</span><span class="sxs-lookup"><span data-stu-id="93959-205">Make sure your firewall allows your application to send telemetry to these ports:</span></span>

  * <span data-ttu-id="93959-206">dc.services.VisualStudio.com:443</span><span class="sxs-lookup"><span data-stu-id="93959-206">dc.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="93959-207">f5.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="93959-207">f5.services.visualstudio.com:443</span></span>

* <span data-ttu-id="93959-208">Si le trafic sortant doit être acheminé via un pare-feu, définissez les propriétés système `http.proxyHost` et `http.proxyPort`.</span><span class="sxs-lookup"><span data-stu-id="93959-208">If outgoing traffic must be routed through a firewall, define system properties `http.proxyHost` and `http.proxyPort`.</span></span>

* <span data-ttu-id="93959-209">Sur les serveurs Windows, installez :</span><span class="sxs-lookup"><span data-stu-id="93959-209">On Windows servers, install:</span></span>

  * [<span data-ttu-id="93959-210">Redistribuable Microsoft Visual C++</span><span class="sxs-lookup"><span data-stu-id="93959-210">Microsoft Visual C++ Redistributable</span></span>](http://www.microsoft.com/download/details.aspx?id=40784)

    <span data-ttu-id="93959-211">(Cette opération active les compteurs de performances.)</span><span class="sxs-lookup"><span data-stu-id="93959-211">(This component enables performance counters.)</span></span>


## <a name="exceptions-and-request-failures"></a><span data-ttu-id="93959-212">Exceptions et échecs de requêtes</span><span class="sxs-lookup"><span data-stu-id="93959-212">Exceptions and request failures</span></span>
<span data-ttu-id="93959-213">Les exceptions non gérées sont collectées automatiquement :</span><span class="sxs-lookup"><span data-stu-id="93959-213">Unhandled exceptions are automatically collected:</span></span>

![Ouvrez Paramètres, Défaillances.](./media/app-insights-java-get-started/21-exceptions.png)

<span data-ttu-id="93959-215">Pour collecter les données concernant d’autres exceptions, vous disposez de deux options :</span><span class="sxs-lookup"><span data-stu-id="93959-215">To collect data on other exceptions, you have two options:</span></span>

* <span data-ttu-id="93959-216">[Insérez des appels à trackException() dans votre code][apiexceptions].</span><span class="sxs-lookup"><span data-stu-id="93959-216">[Insert calls to trackException() in your code][apiexceptions].</span></span>
* <span data-ttu-id="93959-217">[Installez l’agent Java sur votre serveur](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="93959-217">[Install the Java Agent on your server](app-insights-java-agent.md).</span></span> <span data-ttu-id="93959-218">Vous spécifiez les méthodes que vous souhaitez surveiller.</span><span class="sxs-lookup"><span data-stu-id="93959-218">You specify the methods you want to watch.</span></span>

## <a name="monitor-method-calls-and-external-dependencies"></a><span data-ttu-id="93959-219">Surveiller les appels de méthode et les dépendances externes</span><span class="sxs-lookup"><span data-stu-id="93959-219">Monitor method calls and external dependencies</span></span>
<span data-ttu-id="93959-220">[Installez l’agent Java](app-insights-java-agent.md) pour journaliser les méthodes internes spécifiées et les appels effectués via JDBC, avec des données de minutage.</span><span class="sxs-lookup"><span data-stu-id="93959-220">[Install the Java Agent](app-insights-java-agent.md) to log specified internal methods and calls made through JDBC, with timing data.</span></span>

## <a name="performance-counters"></a><span data-ttu-id="93959-221">Compteurs de performances</span><span class="sxs-lookup"><span data-stu-id="93959-221">Performance counters</span></span>
<span data-ttu-id="93959-222">Ouvrez **Paramètres**, **Serveurs** afin d’afficher une gamme de compteurs de performances.</span><span class="sxs-lookup"><span data-stu-id="93959-222">Open **Settings**, **Servers**, to see a range of performance counters.</span></span>

![](./media/app-insights-java-get-started/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a><span data-ttu-id="93959-223">Personnaliser la collecte des compteurs de performances</span><span class="sxs-lookup"><span data-stu-id="93959-223">Customize performance counter collection</span></span>
<span data-ttu-id="93959-224">Pour désactiver la collecte du jeu standard de compteurs de performances, ajoutez le code suivant sous le nœud racine du fichier ApplicationInsights.xml :</span><span class="sxs-lookup"><span data-stu-id="93959-224">To disable collection of the standard set of performance counters, add the following code under the root node of the ApplicationInsights.xml file:</span></span>

```XML
    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a><span data-ttu-id="93959-225">Collecter des compteurs de performances supplémentaires</span><span class="sxs-lookup"><span data-stu-id="93959-225">Collect additional performance counters</span></span>
<span data-ttu-id="93959-226">Vous pouvez spécifier d'autres compteurs de performances à collecter.</span><span class="sxs-lookup"><span data-stu-id="93959-226">You can specify additional performance counters to be collected.</span></span>

#### <a name="jmx-counters-exposed-by-the-java-virtual-machine"></a><span data-ttu-id="93959-227">Compteurs JMX (exposés par la machine virtuelle Java)</span><span class="sxs-lookup"><span data-stu-id="93959-227">JMX counters (exposed by the Java Virtual Machine)</span></span>

```XML
    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* <span data-ttu-id="93959-228">`displayName` : nom affiché sur le portail Application Insights.</span><span class="sxs-lookup"><span data-stu-id="93959-228">`displayName` – The name displayed in the Application Insights portal.</span></span>
* <span data-ttu-id="93959-229">`objectName` : nom de l'objet JMX.</span><span class="sxs-lookup"><span data-stu-id="93959-229">`objectName` – The JMX object name.</span></span>
* <span data-ttu-id="93959-230">`attribute` attribut du nom d'objet JMX à récupérer</span><span class="sxs-lookup"><span data-stu-id="93959-230">`attribute` – The attribute of the JMX object name to fetch</span></span>
* <span data-ttu-id="93959-231">`type` (facultatif) : type d'attribut d'objet JMX :</span><span class="sxs-lookup"><span data-stu-id="93959-231">`type` (optional) - The type of JMX object’s attribute:</span></span>
  * <span data-ttu-id="93959-232">Par défaut : un type simple, comme int ou long.</span><span class="sxs-lookup"><span data-stu-id="93959-232">Default: a simple type such as int or long.</span></span>
  * <span data-ttu-id="93959-233">`composite`: les données du compteur de performances sont au format « Attribute.Data »</span><span class="sxs-lookup"><span data-stu-id="93959-233">`composite`: the perf counter data is in the format of 'Attribute.Data'</span></span>
  * <span data-ttu-id="93959-234">`tabular`: les données du compteur de performances sont au format ligne de tableau</span><span class="sxs-lookup"><span data-stu-id="93959-234">`tabular`: the perf counter data is in the format of a table row</span></span>

#### <a name="windows-performance-counters"></a><span data-ttu-id="93959-235">Compteurs de performances Windows</span><span class="sxs-lookup"><span data-stu-id="93959-235">Windows performance counters</span></span>
<span data-ttu-id="93959-236">Chaque [compteur de performances Windows](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) est un membre d'une catégorie (de la même façon qu'un champ est un membre d'une classe).</span><span class="sxs-lookup"><span data-stu-id="93959-236">Each [Windows performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) is a member of a category (in the same way that a field is a member of a class).</span></span> <span data-ttu-id="93959-237">Les catégories peuvent être globales ou peuvent avoir des instances numérotées ou nommées.</span><span class="sxs-lookup"><span data-stu-id="93959-237">Categories can either be global, or can have numbered or named instances.</span></span>

```XML
    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* <span data-ttu-id="93959-238">displayName : nom affiché sur le portail Application Insights.</span><span class="sxs-lookup"><span data-stu-id="93959-238">displayName – The name displayed in the Application Insights portal.</span></span>
* <span data-ttu-id="93959-239">categoryName : catégorie du compteur de performances (objet de performances) à laquelle ce compteur de performances est associé.</span><span class="sxs-lookup"><span data-stu-id="93959-239">categoryName – The performance counter category (performance object) with which this performance counter is associated.</span></span>
* <span data-ttu-id="93959-240">counterName : nom du compteur de performances.</span><span class="sxs-lookup"><span data-stu-id="93959-240">counterName – The name of the performance counter.</span></span>
* <span data-ttu-id="93959-241">instanceName : nom de l'instance de catégorie de compteur de performances ou une chaîne vide ("") si la catégorie contient une seule instance.</span><span class="sxs-lookup"><span data-stu-id="93959-241">instanceName – The name of the performance counter category instance, or an empty string (""), if the category contains a single instance.</span></span> <span data-ttu-id="93959-242">Si categoryName est Process et que le compteur de performance que vous souhaitez collecter vient du processus en cours de la JVM sur laquelle votre application s'exécute, spécifiez `"__SELF__"`.</span><span class="sxs-lookup"><span data-stu-id="93959-242">If the categoryName is Process, and the performance counter you'd like to collect is from the current JVM process on which your app is running, specify `"__SELF__"`.</span></span>

<span data-ttu-id="93959-243">Les compteurs de performances sont visibles en tant que mesures personnalisées dans [Metrics Explorer][metrics].</span><span class="sxs-lookup"><span data-stu-id="93959-243">Your performance counters are visible as custom metrics in [Metrics Explorer][metrics].</span></span>

![](./media/app-insights-java-get-started/12-custom-perfs.png)

### <a name="unix-performance-counters"></a><span data-ttu-id="93959-244">Compteurs de performances Unix</span><span class="sxs-lookup"><span data-stu-id="93959-244">Unix performance counters</span></span>
* <span data-ttu-id="93959-245">[Installez collectd avec le plug-in Application Insights](app-insights-java-collectd.md) pour obtenir une grande variété de données sur le système et le réseau.</span><span class="sxs-lookup"><span data-stu-id="93959-245">[Install collectd with the Application Insights plugin](app-insights-java-collectd.md) to get a wide variety of system and network data.</span></span>

## <a name="get-user-and-session-data"></a><span data-ttu-id="93959-246">Obtenir des données utilisateur et de session</span><span class="sxs-lookup"><span data-stu-id="93959-246">Get user and session data</span></span>
<span data-ttu-id="93959-247">Vous envoyez des données de télémétrie depuis votre serveur web.</span><span class="sxs-lookup"><span data-stu-id="93959-247">OK, you're sending telemetry from your web server.</span></span> <span data-ttu-id="93959-248">Vous pouvez désormais ajouter plus de surveillance pour obtenir une vue à 360 degrés de votre application :</span><span class="sxs-lookup"><span data-stu-id="93959-248">Now to get the full 360-degree view of your application, you can add more monitoring:</span></span>

* <span data-ttu-id="93959-249">[Ajoutez la télémétrie à vos pages web][usage] pour surveiller les affichages de pages et les mesures relatives à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="93959-249">[Add telemetry to your web pages][usage] to monitor page views and user metrics.</span></span>
* <span data-ttu-id="93959-250">[Configurez les tests web][availability] pour vous assurer que votre application est bien active.</span><span class="sxs-lookup"><span data-stu-id="93959-250">[Set up web tests][availability] to make sure your application stays live and responsive.</span></span>

## <a name="capture-log-traces"></a><span data-ttu-id="93959-251">Capture le suivi des journaux</span><span class="sxs-lookup"><span data-stu-id="93959-251">Capture log traces</span></span>
<span data-ttu-id="93959-252">Vous pouvez utiliser Application Insights pour traiter les journaux Log4J, Logback ou autres frameworks de journalisation.</span><span class="sxs-lookup"><span data-stu-id="93959-252">You can use Application Insights to slice and dice logs from Log4J, Logback, or other logging frameworks.</span></span> <span data-ttu-id="93959-253">Vous pouvez mettre en corrélation les journaux avec les demandes HTTP et autres informations de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="93959-253">You can correlate the logs with HTTP requests and other telemetry.</span></span> <span data-ttu-id="93959-254">[Découvrez comment][javalogs].</span><span class="sxs-lookup"><span data-stu-id="93959-254">[Learn how][javalogs].</span></span>

## <a name="send-your-own-telemetry"></a><span data-ttu-id="93959-255">Envoyer votre propre télémétrie</span><span class="sxs-lookup"><span data-stu-id="93959-255">Send your own telemetry</span></span>
<span data-ttu-id="93959-256">Maintenant que vous avez installé le Kit de développement logiciel (SDK), vous pouvez utiliser l'API pour envoyer votre propre télémétrie.</span><span class="sxs-lookup"><span data-stu-id="93959-256">Now that you've installed the SDK, you can use the API to send your own telemetry.</span></span>

* <span data-ttu-id="93959-257">[Suivez des événements et des mesures personnalisés][api] pour savoir ce que les utilisateurs font avec votre application.</span><span class="sxs-lookup"><span data-stu-id="93959-257">[Track custom events and metrics][api] to learn what users are doing with your application.</span></span>
* <span data-ttu-id="93959-258">[Recherchez les événements et les journaux][diagnostic] pour diagnostiquer les problèmes.</span><span class="sxs-lookup"><span data-stu-id="93959-258">[Search events and logs][diagnostic] to help diagnose problems.</span></span>

## <a name="availability-web-tests"></a><span data-ttu-id="93959-259">Tests web de disponibilité</span><span class="sxs-lookup"><span data-stu-id="93959-259">Availability web tests</span></span>
<span data-ttu-id="93959-260">Application Insights peut tester votre site web à intervalles réguliers pour vérifier qu’il fonctionne et répond correctement.</span><span class="sxs-lookup"><span data-stu-id="93959-260">Application Insights can test your website at regular intervals to check that it's up and responding well.</span></span> <span data-ttu-id="93959-261">[Pour configurer][availability], cliquez sur Tests web.</span><span class="sxs-lookup"><span data-stu-id="93959-261">[To set up][availability], click Web tests.</span></span>

![Cliquez sur Tests web, puis sur Ajouter un test web](./media/app-insights-java-get-started/31-config-web-test.png)

<span data-ttu-id="93959-263">Vous obtenez des graphiques du temps de réponse, ainsi que des notifications par courrier électronique si votre site ne fonctionne plus.</span><span class="sxs-lookup"><span data-stu-id="93959-263">You'll get charts of response times, plus email notifications if your site goes down.</span></span>

![Exemple de test web](./media/app-insights-java-get-started/appinsights-10webtestresult.png)

<span data-ttu-id="93959-265">[En savoir plus sur les tests de disponibilité web.][availability]</span><span class="sxs-lookup"><span data-stu-id="93959-265">[Learn more about availability web tests.][availability]</span></span>

## <a name="questions-problems"></a><span data-ttu-id="93959-266">Des questions ?</span><span class="sxs-lookup"><span data-stu-id="93959-266">Questions?</span></span> <span data-ttu-id="93959-267">Des problèmes ?</span><span class="sxs-lookup"><span data-stu-id="93959-267">Problems?</span></span>
[<span data-ttu-id="93959-268">Résolution des problèmes Java</span><span class="sxs-lookup"><span data-stu-id="93959-268">Troubleshooting Java</span></span>](app-insights-java-troubleshoot.md)

## <a name="video"></a><span data-ttu-id="93959-269">Vidéo</span><span class="sxs-lookup"><span data-stu-id="93959-269">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="93959-270">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="93959-270">Next steps</span></span>
* [<span data-ttu-id="93959-271">Surveillance des appels de dépendance</span><span class="sxs-lookup"><span data-stu-id="93959-271">Monitor dependency calls</span></span>](app-insights-java-agent.md)
* [<span data-ttu-id="93959-272">Surveillance des compteurs de performances Unix</span><span class="sxs-lookup"><span data-stu-id="93959-272">Monitor Unix performance counters</span></span>](app-insights-java-collectd.md)
* <span data-ttu-id="93959-273">Ajoutez [la surveillance à vos pages web](app-insights-javascript.md) pour surveiller le temps de chargement des pages, les appels AJAX et les exceptions du navigateur.</span><span class="sxs-lookup"><span data-stu-id="93959-273">Add [monitoring to your web pages](app-insights-javascript.md) to monitor page load times, AJAX calls, browser exceptions.</span></span>
* <span data-ttu-id="93959-274">Écrivez [télémétrie personnalisée](app-insights-api-custom-events-metrics.md) pour suivre l’utilisation sur le navigateur ou le serveur.</span><span class="sxs-lookup"><span data-stu-id="93959-274">Write [custom telemetry](app-insights-api-custom-events-metrics.md) to track usage in the browser or at the server.</span></span>
* <span data-ttu-id="93959-275">Créez des [tableaux de bord](app-insights-dashboards.md) pour rassembler les graphiques essentiels pour la surveillance de votre système.</span><span class="sxs-lookup"><span data-stu-id="93959-275">Create [dashboards](app-insights-dashboards.md) to bring together the key charts for monitoring your system.</span></span>
* <span data-ttu-id="93959-276">Utilisez [Analytics](app-insights-analytics.md) pour des requêtes puissantes sur les données de télémétrie de votre application</span><span class="sxs-lookup"><span data-stu-id="93959-276">Use  [Analytics](app-insights-analytics.md) for powerful queries over telemetry from your app</span></span>
* <span data-ttu-id="93959-277">Pour plus d’informations, consultez [Azure pour les développeurs Java](/java/azure).</span><span class="sxs-lookup"><span data-stu-id="93959-277">For more information, visit [Azure for Java developers](/java/azure).</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#trackexception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[usage]: app-insights-javascript.md
