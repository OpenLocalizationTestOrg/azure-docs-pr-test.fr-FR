---
title: "aaaJava analytique d’application web avec Azure Application Insights | Documents Microsoft"
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
ms.openlocfilehash: 6555ee53a44f937350e4fa296080f7dce4f45226
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-insights-in-a-java-web-project"></a><span data-ttu-id="7bb17-103">Prise en main d'Application Insights dans un projet web Java</span><span class="sxs-lookup"><span data-stu-id="7bb17-103">Get started with Application Insights in a Java web project</span></span>


<span data-ttu-id="7bb17-104">[Application Insights](https://azure.microsoft.com/services/application-insights/) est un service analytique extensible pour les développeurs web qui vous permet de comprennent l’utilisation de votre application en temps réel et les performances de hello.</span><span class="sxs-lookup"><span data-stu-id="7bb17-104">[Application Insights](https://azure.microsoft.com/services/application-insights/) is an extensible analytics service for web developers that helps you understand hello performance and usage of your live application.</span></span> <span data-ttu-id="7bb17-105">Utilisez-le trop[détecter et diagnostiquer les problèmes de performances et exceptions](app-insights-detect-triage-diagnose.md), et [écrire du code] [ api] tootrack faire de ce que les utilisateurs avec votre application.</span><span class="sxs-lookup"><span data-stu-id="7bb17-105">Use it too[detect and diagnose performance issues and exceptions](app-insights-detect-triage-diagnose.md), and [write code][api] tootrack what users do with your app.</span></span>

![Exemples de données](./media/app-insights-java-get-started/5-results.png)

<span data-ttu-id="7bb17-107">Application Insights prend en charge les applications Java exécutées sur Linux, Unix ou Windows.</span><span class="sxs-lookup"><span data-stu-id="7bb17-107">Application Insights supports Java apps running on Linux, Unix, or Windows.</span></span>

<span data-ttu-id="7bb17-108">Ce dont vous avez besoin :</span><span class="sxs-lookup"><span data-stu-id="7bb17-108">You need:</span></span>

* <span data-ttu-id="7bb17-109">Oracle JRE 1.6 ou version ultérieure ou Zoulou JRE 1.6 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="7bb17-109">Oracle JRE 1.6 or later, or Zulu JRE 1.6 or later</span></span>
* <span data-ttu-id="7bb17-110">Un abonnement trop[Microsoft Azure](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="7bb17-110">A subscription too[Microsoft Azure](https://azure.microsoft.com/).</span></span>

<span data-ttu-id="7bb17-111">*Si vous avez une application web qui est déjà en ligne, pourrait procédure hello autre trop[ajouter hello SDK lors de l’exécution dans le serveur web de hello](app-insights-java-live.md). Cette solution permet d’éviter la reconstruction du code de hello, mais ne pas obtenir d’activités des utilisateurs tootrack hello option toowrite code.*</span><span class="sxs-lookup"><span data-stu-id="7bb17-111">*If you have a web app that's already live, you could follow hello alternative procedure too[add hello SDK at runtime in hello web server](app-insights-java-live.md). That alternative avoids rebuilding hello code, but you don't get hello option toowrite code tootrack user activity.*</span></span>

## <a name="1-get-an-application-insights-instrumentation-key"></a><span data-ttu-id="7bb17-112">1. Obtenir une clé d'instrumentation Application Insights</span><span class="sxs-lookup"><span data-stu-id="7bb17-112">1. Get an Application Insights instrumentation key</span></span>
1. <span data-ttu-id="7bb17-113">Connectez-vous à toohello [portail Microsoft Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7bb17-113">Sign in toohello [Microsoft Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7bb17-114">Créez une ressource Application Insights.</span><span class="sxs-lookup"><span data-stu-id="7bb17-114">Create an Application Insights resource.</span></span> <span data-ttu-id="7bb17-115">Définissez des applications web tooJava hello application type.</span><span class="sxs-lookup"><span data-stu-id="7bb17-115">Set hello application type tooJava web application.</span></span>

    ![Indiquez le nom, choisissez l’application web Java, puis cliquez sur Créer.](./media/app-insights-java-get-started/02-create.png)
3. <span data-ttu-id="7bb17-117">Trouver la clé d’instrumentation hello de ressource hello.</span><span class="sxs-lookup"><span data-stu-id="7bb17-117">Find hello instrumentation key of hello new resource.</span></span> <span data-ttu-id="7bb17-118">Vous devez toopaste cette clé dans votre projet de code dans quelques instants.</span><span class="sxs-lookup"><span data-stu-id="7bb17-118">You'll need toopaste this key into your code project shortly.</span></span>

    ![Dans hello nouvelle ressource vue d’ensemble, cliquez sur Propriétés et copiez hello clé d’Instrumentation](./media/app-insights-java-get-started/03-key.png)

## <a name="2-add-hello-application-insights-sdk-for-java-tooyour-project"></a><span data-ttu-id="7bb17-120">2. Ajouter hello Application Insights SDK pour le projet de tooyour Java</span><span class="sxs-lookup"><span data-stu-id="7bb17-120">2. Add hello Application Insights SDK for Java tooyour project</span></span>
<span data-ttu-id="7bb17-121">*Choisissez hello approprié pour votre projet.*</span><span class="sxs-lookup"><span data-stu-id="7bb17-121">*Choose hello appropriate way for your project.*</span></span>

#### <a name="if-youre-using-eclipse-toocreate-a-maven-or-dynamic-web-project-"></a><span data-ttu-id="7bb17-122">Si vous utilisez Eclipse toocreate un projet Maven ou Web dynamique...</span><span class="sxs-lookup"><span data-stu-id="7bb17-122">If you're using Eclipse toocreate a Maven or Dynamic Web project ...</span></span>
<span data-ttu-id="7bb17-123">Hello d’utilisation [Application Insights SDK pour Java plug-in][eclipse].</span><span class="sxs-lookup"><span data-stu-id="7bb17-123">Use hello [Application Insights SDK for Java plug-in][eclipse].</span></span>

#### <a name="if-youre-using-maven"></a><span data-ttu-id="7bb17-124">Si vous utilisez Maven...</span><span class="sxs-lookup"><span data-stu-id="7bb17-124">If you're using Maven...</span></span>
<span data-ttu-id="7bb17-125">Si votre projet est déjà configuré toouse Maven pour la build, fusion hello code tooyour pom.xml fichier suivant.</span><span class="sxs-lookup"><span data-stu-id="7bb17-125">If your project is already set up toouse Maven for build, merge hello following code tooyour pom.xml file.</span></span>

<span data-ttu-id="7bb17-126">Ensuite, les fichiers binaires actualisation hello projet dépendances tooget hello téléchargé.</span><span class="sxs-lookup"><span data-stu-id="7bb17-126">Then, refresh hello project dependencies tooget hello binaries downloaded.</span></span>

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

* <span data-ttu-id="7bb17-127">*Des erreurs de validation de build ou de somme de contrôle ?*</span><span class="sxs-lookup"><span data-stu-id="7bb17-127">*Build or checksum validation errors?*</span></span> <span data-ttu-id="7bb17-128">Essayez d’utiliser une version spécifique, telle que : `<version>1.0.n</version>`.</span><span class="sxs-lookup"><span data-stu-id="7bb17-128">Try using a specific version, such as: `<version>1.0.n</version>`.</span></span> <span data-ttu-id="7bb17-129">Vous trouverez la version la plus récente hello Bonjour [notes de publication du Kit de développement logiciel](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) ou dans notre [les artefacts Maven](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights).</span><span class="sxs-lookup"><span data-stu-id="7bb17-129">You'll find hello latest version in hello [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) or in our [Maven artifacts](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights).</span></span>
* <span data-ttu-id="7bb17-130">*Devez tooupdate tooa nouveau SDK ?*</span><span class="sxs-lookup"><span data-stu-id="7bb17-130">*Need tooupdate tooa new SDK?*</span></span> <span data-ttu-id="7bb17-131">Actualisez les dépendances de votre projet.</span><span class="sxs-lookup"><span data-stu-id="7bb17-131">Refresh your project's dependencies.</span></span>

#### <a name="if-youre-using-gradle"></a><span data-ttu-id="7bb17-132">Si vous utilisez Gradle...</span><span class="sxs-lookup"><span data-stu-id="7bb17-132">If you're using Gradle...</span></span>
<span data-ttu-id="7bb17-133">Si votre projet est déjà configuré toouse Gradle pour la build, du fichier build.gradle tooyour code fusion hello suivant.</span><span class="sxs-lookup"><span data-stu-id="7bb17-133">If your project is already set up toouse Gradle for build, merge hello following code tooyour build.gradle file.</span></span>

<span data-ttu-id="7bb17-134">Actualisation hello projet dépendances tooget hello binaires téléchargés.</span><span class="sxs-lookup"><span data-stu-id="7bb17-134">Then refresh hello project dependencies tooget hello binaries downloaded.</span></span>

```JSON

    repositories {
      mavenCentral()
    }

    dependencies {
      compile group: 'com.microsoft.azure', name: 'applicationinsights-web', version: '1.+'
      // or applicationinsights-core for bare API
    }
```

* <span data-ttu-id="7bb17-135">*Erreurs de validation de build ou de somme de contrôle ? Essayez d’utiliser une version spécifique, telle que :* `version:'1.0.n'`.</span><span class="sxs-lookup"><span data-stu-id="7bb17-135">*Build or checksum validation errors? Try using a specific version, such as:* `version:'1.0.n'`.</span></span> <span data-ttu-id="7bb17-136">*Vous trouverez la version la plus récente hello Bonjour [notes de publication du Kit de développement logiciel](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).*</span><span class="sxs-lookup"><span data-stu-id="7bb17-136">*You'll find hello latest version in hello [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).*</span></span>
* <span data-ttu-id="7bb17-137">*tooupdate tooa nouveau SDK*</span><span class="sxs-lookup"><span data-stu-id="7bb17-137">*tooupdate tooa new SDK*</span></span>
  * <span data-ttu-id="7bb17-138">Actualisez les dépendances de votre projet.</span><span class="sxs-lookup"><span data-stu-id="7bb17-138">Refresh your project's dependencies.</span></span>

#### <a name="otherwise-"></a><span data-ttu-id="7bb17-139">Sinon...</span><span class="sxs-lookup"><span data-stu-id="7bb17-139">Otherwise ...</span></span>
<span data-ttu-id="7bb17-140">Ajoutez manuellement hello SDK :</span><span class="sxs-lookup"><span data-stu-id="7bb17-140">Manually add hello SDK:</span></span>

1. <span data-ttu-id="7bb17-141">Télécharger hello [Application Insights SDK pour Java](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="7bb17-141">Download hello [Application Insights SDK for Java](https://aka.ms/aijavasdk).</span></span>
2. <span data-ttu-id="7bb17-142">Extraire les fichiers binaires de hello à partir du fichier zip de hello et ajoutez-les tooyour projet.</span><span class="sxs-lookup"><span data-stu-id="7bb17-142">Extract hello binaries from hello zip file and add them tooyour project.</span></span>

### <a name="questions"></a><span data-ttu-id="7bb17-143">Questions...</span><span class="sxs-lookup"><span data-stu-id="7bb17-143">Questions...</span></span>
* <span data-ttu-id="7bb17-144">*Quelle est la relation hello entre hello `-core` et `-web` composants dans le zip de hello ?*</span><span class="sxs-lookup"><span data-stu-id="7bb17-144">*What's hello relationship between hello `-core` and `-web` components in hello zip?*</span></span>

  * <span data-ttu-id="7bb17-145">`applicationinsights-core`permet de vous hello API système.</span><span class="sxs-lookup"><span data-stu-id="7bb17-145">`applicationinsights-core` gives you hello bare API.</span></span> <span data-ttu-id="7bb17-146">Ce composant est toujours requis.</span><span class="sxs-lookup"><span data-stu-id="7bb17-146">You always need this component.</span></span>
  * <span data-ttu-id="7bb17-147">`applicationinsights-web` fournit des mesures qui permettent d’effectuer le suivi du nombre de requêtes HTTP et des temps de réponse.</span><span class="sxs-lookup"><span data-stu-id="7bb17-147">`applicationinsights-web` gives you metrics that track HTTP request counts and response times.</span></span> <span data-ttu-id="7bb17-148">Vous pouvez omettre ce composant si vous ne souhaitez pas recueillir automatiquement ces données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="7bb17-148">You can omit this component if you don't want this telemetry automatically collected.</span></span> <span data-ttu-id="7bb17-149">Par exemple, si vous souhaitez toowrite votre propre.</span><span class="sxs-lookup"><span data-stu-id="7bb17-149">For example, if you want toowrite your own.</span></span>
* <span data-ttu-id="7bb17-150">*tooupdate hello SDK lorsque nous publions des modifications*</span><span class="sxs-lookup"><span data-stu-id="7bb17-150">*tooupdate hello SDK when we publish changes*</span></span>

  * <span data-ttu-id="7bb17-151">Télécharger le dernier hello [Application Insights SDK pour Java](https://aka.ms/qqkaq6) et remplacer hello anciens.</span><span class="sxs-lookup"><span data-stu-id="7bb17-151">Download hello latest [Application Insights SDK for Java](https://aka.ms/qqkaq6) and replace hello old ones.</span></span>
  * <span data-ttu-id="7bb17-152">Modifications sont décrites dans hello [notes de publication du Kit de développement logiciel](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).</span><span class="sxs-lookup"><span data-stu-id="7bb17-152">Changes are described in hello [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).</span></span>

## <a name="3-add-an-application-insights-xml-file"></a><span data-ttu-id="7bb17-153">3. Ajouter un fichier .xml Application Insights</span><span class="sxs-lookup"><span data-stu-id="7bb17-153">3. Add an Application Insights .xml file</span></span>
<span data-ttu-id="7bb17-154">Ajouter un dossier de ressources ApplicationInsights.xml toohello dans votre projet, ou assurez-vous que le chemin d’accès de classe de déploiement du projet tooyour est ajouté.</span><span class="sxs-lookup"><span data-stu-id="7bb17-154">Add ApplicationInsights.xml toohello resources folder in your project, or make sure it is added tooyour project’s deployment class path.</span></span> <span data-ttu-id="7bb17-155">Copiez hello XML suivant dans celui-ci.</span><span class="sxs-lookup"><span data-stu-id="7bb17-155">Copy hello following XML into it.</span></span>

<span data-ttu-id="7bb17-156">Remplacer la clé d’instrumentation hello que vous avez obtenu hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7bb17-156">Substitute hello instrumentation key that you got from hello Azure portal.</span></span>

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


* <span data-ttu-id="7bb17-157">clé d’instrumentation Hello est envoyé avec chaque élément de données de télémétrie et indique à Application Insights toodisplay dans votre ressource.</span><span class="sxs-lookup"><span data-stu-id="7bb17-157">hello instrumentation key is sent along with every item of telemetry and tells Application Insights toodisplay it in your resource.</span></span>
* <span data-ttu-id="7bb17-158">Hello composant de requête HTTP est facultative.</span><span class="sxs-lookup"><span data-stu-id="7bb17-158">hello HTTP Request component is optional.</span></span> <span data-ttu-id="7bb17-159">Il envoie automatiquement télémétrie concernant les requêtes et le portail de toohello de temps de réponse.</span><span class="sxs-lookup"><span data-stu-id="7bb17-159">It automatically sends telemetry about requests and response times toohello portal.</span></span>
* <span data-ttu-id="7bb17-160">Corrélation des événements est un composant de requête Ajout toohello HTTP.</span><span class="sxs-lookup"><span data-stu-id="7bb17-160">Events correlation is an addition toohello HTTP request component.</span></span> <span data-ttu-id="7bb17-161">Il attribue à une demande de tooeach identificateur reçue par le serveur de hello et ajoute cet identificateur en tant qu’un élément tooevery de propriété de télémétrie en tant que propriété de hello 'Operation.Id'.</span><span class="sxs-lookup"><span data-stu-id="7bb17-161">It assigns an identifier tooeach request received by hello server, and adds this identifier as a property tooevery item of telemetry as hello property 'Operation.Id'.</span></span> <span data-ttu-id="7bb17-162">Il vous permet de télémétrie de hello toocorrelate associé à chaque requête en définissant un filtre dans [recherche diagnostic][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="7bb17-162">It allows you toocorrelate hello telemetry associated with each request by setting a filter in [diagnostic search][diagnostic].</span></span>
* <span data-ttu-id="7bb17-163">clé d’Application Insights Hello peut être passée dynamiquement hello portail Azure en tant que propriété par le système (-DAPPLICATION_INSIGHTS_IKEY = your_ikey).</span><span class="sxs-lookup"><span data-stu-id="7bb17-163">hello Application Insights key can be passed dynamically from hello Azure portal as a system property (-DAPPLICATION_INSIGHTS_IKEY=your_ikey).</span></span> <span data-ttu-id="7bb17-164">Si aucune propriété n’est définie, la variable d’environnement (APPLICATION_INSIGHTS_IKEY) est recherchée dans les paramètres d’application Azure.</span><span class="sxs-lookup"><span data-stu-id="7bb17-164">If there is no property defined, it checks for environment variable (APPLICATION_INSIGHTS_IKEY) in Azure App Settings.</span></span> <span data-ttu-id="7bb17-165">Si les deux propriétés hello ne sont pas définies, la valeur par défaut de hello InstrumentationKey est utilisée à partir de ApplicationInsights.xml.</span><span class="sxs-lookup"><span data-stu-id="7bb17-165">If both hello properties are undefined, hello default InstrumentationKey is used from ApplicationInsights.xml.</span></span> <span data-ttu-id="7bb17-166">Cette séquence vous aide à toomanage InstrumentationKeys différents pour différents environnements dynamiquement.</span><span class="sxs-lookup"><span data-stu-id="7bb17-166">This sequence helps you toomanage different InstrumentationKeys for different environments dynamically.</span></span>

### <a name="alternative-ways-tooset-hello-instrumentation-key"></a><span data-ttu-id="7bb17-167">Clé d’instrumentation d’autres méthodes tooset hello</span><span class="sxs-lookup"><span data-stu-id="7bb17-167">Alternative ways tooset hello instrumentation key</span></span>
<span data-ttu-id="7bb17-168">Application Insights SDK recherche clé hello dans cet ordre :</span><span class="sxs-lookup"><span data-stu-id="7bb17-168">Application Insights SDK looks for hello key in this order:</span></span>

1. <span data-ttu-id="7bb17-169">Propriété système : -DAPPLICATION_INSIGHTS_IKEY=votre_ikey</span><span class="sxs-lookup"><span data-stu-id="7bb17-169">System property: -DAPPLICATION_INSIGHTS_IKEY=your_ikey</span></span>
2. <span data-ttu-id="7bb17-170">Variable d’environnement : APPLICATION_INSIGHTS_IKEY</span><span class="sxs-lookup"><span data-stu-id="7bb17-170">Environment variable: APPLICATION_INSIGHTS_IKEY</span></span>
3. <span data-ttu-id="7bb17-171">Fichier de configuration : ApplicationInsights.xml</span><span class="sxs-lookup"><span data-stu-id="7bb17-171">Configuration file: ApplicationInsights.xml</span></span>

<span data-ttu-id="7bb17-172">Vous pouvez également [définir la clé dans le code](app-insights-api-custom-events-metrics.md#ikey):</span><span class="sxs-lookup"><span data-stu-id="7bb17-172">You can also [set it in code](app-insights-api-custom-events-metrics.md#ikey):</span></span>

```Java

    telemetryClient.InstrumentationKey = "...";
```

## <a name="4-add-an-http-filter"></a><span data-ttu-id="7bb17-173">4. Ajouter un filtre HTTP</span><span class="sxs-lookup"><span data-stu-id="7bb17-173">4. Add an HTTP filter</span></span>
<span data-ttu-id="7bb17-174">dernière étape de configuration Hello permet hello HTTP demande composant toolog chaque demande web.</span><span class="sxs-lookup"><span data-stu-id="7bb17-174">hello last configuration step allows hello HTTP request component toolog each web request.</span></span> <span data-ttu-id="7bb17-175">(Non requis si vous voulez simplement les API système hello.)</span><span class="sxs-lookup"><span data-stu-id="7bb17-175">(Not required if you just want hello bare API.)</span></span>

<span data-ttu-id="7bb17-176">Recherchez et ouvrez le fichier de web.xml hello dans votre projet, puis hello fusion suivant code sous le nœud de l’application web hello, dans lequel les filtres d’application sont configurés.</span><span class="sxs-lookup"><span data-stu-id="7bb17-176">Locate and open hello web.xml file in your project, and merge hello following code under hello web-app node, where your application filters are configured.</span></span>

<span data-ttu-id="7bb17-177">tooget hello les résultats plus précis, filtre de hello doivent être mappés avant tous les autres filtres.</span><span class="sxs-lookup"><span data-stu-id="7bb17-177">tooget hello most accurate results, hello filter should be mapped before all other filters.</span></span>

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

#### <a name="if-youre-using-spring-web-mvc-31-or-later"></a><span data-ttu-id="7bb17-178">Si vous utilisez Spring Web MVC 3.1 ou une version ultérieure</span><span class="sxs-lookup"><span data-stu-id="7bb17-178">If you're using Spring Web MVC 3.1 or later</span></span>
<span data-ttu-id="7bb17-179">Modifier ces éléments en *-package d’Application Insights servlet.xml tooinclude hello :</span><span class="sxs-lookup"><span data-stu-id="7bb17-179">Edit these elements in *-servlet.xml tooinclude hello Application Insights package:</span></span>

```XML

    <context:component-scan base-package=" com.springapp.mvc, com.microsoft.applicationinsights.web.spring"/>

    <mvc:interceptors>
        <mvc:interceptor>
            <mvc:mapping path="/**"/>
            <bean class="com.microsoft.applicationinsights.web.spring.RequestNameHandlerInterceptorAdapter" />
        </mvc:interceptor>
    </mvc:interceptors>
```

#### <a name="if-youre-using-struts-2"></a><span data-ttu-id="7bb17-180">Si vous utilisez Struts 2</span><span class="sxs-lookup"><span data-stu-id="7bb17-180">If you're using Struts 2</span></span>
<span data-ttu-id="7bb17-181">Ajoutez ce fichier de configuration élément toohello Connections (généralement nommé struts.xml ou default.xml de Connections) :</span><span class="sxs-lookup"><span data-stu-id="7bb17-181">Add this item toohello Struts configuration file (usually named struts.xml or struts-default.xml):</span></span>

```XML

     <interceptors>
       <interceptor name="ApplicationInsightsRequestNameInterceptor" class="com.microsoft.applicationinsights.web.struts.RequestNameInterceptor" />
     </interceptors>
     <default-interceptor-ref name="ApplicationInsightsRequestNameInterceptor" />
```

<span data-ttu-id="7bb17-182">(Si vous avez des intercepteurs définis dans une pile par défaut, l’intercepteur de hello peut simplement être ajouté toothat pile.)</span><span class="sxs-lookup"><span data-stu-id="7bb17-182">(If you have interceptors defined in a default stack, hello interceptor can simply be added toothat stack.)</span></span>

## <a name="5-run-your-application"></a><span data-ttu-id="7bb17-183">5. Exécuter votre application</span><span class="sxs-lookup"><span data-stu-id="7bb17-183">5. Run your application</span></span>
<span data-ttu-id="7bb17-184">Exécuter en mode débogage sur votre ordinateur de développement, ou tooyour serveur de publication.</span><span class="sxs-lookup"><span data-stu-id="7bb17-184">Either run it in debug mode on your development machine, or publish tooyour server.</span></span>

## <a name="6-view-your-telemetry-in-application-insights"></a><span data-ttu-id="7bb17-185">6. Voir votre télémétrie dans Application Insights</span><span class="sxs-lookup"><span data-stu-id="7bb17-185">6. View your telemetry in Application Insights</span></span>
<span data-ttu-id="7bb17-186">Retourner la ressource Application Insights tooyour [portail Microsoft Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7bb17-186">Return tooyour Application Insights resource in [Microsoft Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="7bb17-187">Les données de demandes HTTP s’affiche sur le panneau de vue d’ensemble de hello.</span><span class="sxs-lookup"><span data-stu-id="7bb17-187">HTTP requests data appears on hello overview blade.</span></span> <span data-ttu-id="7bb17-188">(Si elles n’y sont pas, attendez quelques secondes et cliquez sur Actualiser).</span><span class="sxs-lookup"><span data-stu-id="7bb17-188">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![Exemples de données](./media/app-insights-java-get-started/5-results.png)

<span data-ttu-id="7bb17-190">[En savoir plus sur les mesures.][metrics]</span><span class="sxs-lookup"><span data-stu-id="7bb17-190">[Learn more about metrics.][metrics]</span></span>

<span data-ttu-id="7bb17-191">Cliquez sur n’importe quel toosee graphique plu agrégées des métriques.</span><span class="sxs-lookup"><span data-stu-id="7bb17-191">Click through any chart toosee more detailed aggregated metrics.</span></span>

![](./media/app-insights-java-get-started/6-barchart.png)

> <span data-ttu-id="7bb17-192">Application Insights suppose que le format de requêtes HTTP pour les applications MVC hello est : `VERB controller/action`.</span><span class="sxs-lookup"><span data-stu-id="7bb17-192">Application Insights assumes hello format of HTTP requests for MVC applications is: `VERB controller/action`.</span></span> <span data-ttu-id="7bb17-193">Par exemple, `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` et `GET Home/Product/sdf96vws` sont regroupés dans `GET Home/Product`.</span><span class="sxs-lookup"><span data-stu-id="7bb17-193">For example, `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` and `GET Home/Product/sdf96vws` are grouped into `GET Home/Product`.</span></span> <span data-ttu-id="7bb17-194">Ceci permet l’agrégation correcte des demandes, par exemple le nombre de demandes et le temps moyen d’exécution des demandes.</span><span class="sxs-lookup"><span data-stu-id="7bb17-194">This grouping enables meaningful aggregations of requests, such as number of requests and average execution time for requests.</span></span>
>
>

### <a name="instance-data"></a><span data-ttu-id="7bb17-195">Données d’instance</span><span class="sxs-lookup"><span data-stu-id="7bb17-195">Instance data</span></span>
<span data-ttu-id="7bb17-196">Cliquez sur une demande spécifique au type toosee des instances individuelles.</span><span class="sxs-lookup"><span data-stu-id="7bb17-196">Click through a specific request type toosee individual instances.</span></span>

<span data-ttu-id="7bb17-197">Deux types de données s’affichent dans Application Insights : des données agrégées, stockées et affichées sous forme de moyennes, de nombres et de sommes ; et les données d’instance : des rapports individuels des requêtes HTTP, des exceptions, les vues de page ou des événements personnalisés.</span><span class="sxs-lookup"><span data-stu-id="7bb17-197">Two kinds of data are displayed in Application Insights: aggregated data, stored and displayed as averages, counts, and sums; and instance data - individual reports of HTTP requests, exceptions, page views, or custom events.</span></span>

<span data-ttu-id="7bb17-198">Lorsque vous affichez les propriétés hello d’une demande, vous pouvez voir les événements de télémétrie hello associés tels que les demandes et les exceptions.</span><span class="sxs-lookup"><span data-stu-id="7bb17-198">When viewing hello properties of a request, you can see hello telemetry events associated with it such as requests and exceptions.</span></span>

![](./media/app-insights-java-get-started/7-instance.png)

### <a name="analytics-powerful-query-language"></a><span data-ttu-id="7bb17-199">Analytics : un puissant langage de requête</span><span class="sxs-lookup"><span data-stu-id="7bb17-199">Analytics: Powerful query language</span></span>
<span data-ttu-id="7bb17-200">Comme vous accumulent des données, vous pouvez exécuter des requêtes instances tooaggregate toofind et de données individuelles.</span><span class="sxs-lookup"><span data-stu-id="7bb17-200">As you accumulate more data, you can run queries both tooaggregate data and toofind individual instances.</span></span>  <span data-ttu-id="7bb17-201">[Analytics](app-insights-analytics.md) est un outil puissant qui permet non seulement de comprendre les performances et l’utilisation, mais également d’effectuer des diagnostics.</span><span class="sxs-lookup"><span data-stu-id="7bb17-201">[Analytics](app-insights-analytics.md) is a powerful tool for both for understanding performance and usage, and for diagnostic purposes.</span></span>

![Exemple d’Analytics](./media/app-insights-java-get-started/025.png)

## <a name="7-install-your-app-on-hello-server"></a><span data-ttu-id="7bb17-203">7. Installer votre application sur le serveur de hello</span><span class="sxs-lookup"><span data-stu-id="7bb17-203">7. Install your app on hello server</span></span>
<span data-ttu-id="7bb17-204">Maintenant publier le serveur de votre application toohello, permettent aux utilisateurs de l’utiliser et observer les données de télémétrie hello apparaissent dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="7bb17-204">Now publish your app toohello server, let people use it, and watch hello telemetry show up on hello portal.</span></span>

* <span data-ttu-id="7bb17-205">Assurez-vous que votre pare-feu autorise votre toosend application ports toothese de télémétrie :</span><span class="sxs-lookup"><span data-stu-id="7bb17-205">Make sure your firewall allows your application toosend telemetry toothese ports:</span></span>

  * <span data-ttu-id="7bb17-206">dc.services.VisualStudio.com:443</span><span class="sxs-lookup"><span data-stu-id="7bb17-206">dc.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="7bb17-207">f5.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="7bb17-207">f5.services.visualstudio.com:443</span></span>

* <span data-ttu-id="7bb17-208">Si le trafic sortant doit être acheminé via un pare-feu, définissez les propriétés système `http.proxyHost` et `http.proxyPort`.</span><span class="sxs-lookup"><span data-stu-id="7bb17-208">If outgoing traffic must be routed through a firewall, define system properties `http.proxyHost` and `http.proxyPort`.</span></span>

* <span data-ttu-id="7bb17-209">Sur les serveurs Windows, installez :</span><span class="sxs-lookup"><span data-stu-id="7bb17-209">On Windows servers, install:</span></span>

  * [<span data-ttu-id="7bb17-210">Redistribuable Microsoft Visual C++</span><span class="sxs-lookup"><span data-stu-id="7bb17-210">Microsoft Visual C++ Redistributable</span></span>](http://www.microsoft.com/download/details.aspx?id=40784)

    <span data-ttu-id="7bb17-211">(Cette opération active les compteurs de performances.)</span><span class="sxs-lookup"><span data-stu-id="7bb17-211">(This component enables performance counters.)</span></span>


## <a name="exceptions-and-request-failures"></a><span data-ttu-id="7bb17-212">Exceptions et échecs de requêtes</span><span class="sxs-lookup"><span data-stu-id="7bb17-212">Exceptions and request failures</span></span>
<span data-ttu-id="7bb17-213">Les exceptions non gérées sont collectées automatiquement :</span><span class="sxs-lookup"><span data-stu-id="7bb17-213">Unhandled exceptions are automatically collected:</span></span>

![Ouvrez Paramètres, Défaillances.](./media/app-insights-java-get-started/21-exceptions.png)

<span data-ttu-id="7bb17-215">toocollect des données sur les autres exceptions, vous avez deux options :</span><span class="sxs-lookup"><span data-stu-id="7bb17-215">toocollect data on other exceptions, you have two options:</span></span>

* <span data-ttu-id="7bb17-216">[Insérer des appels dans votre code tootrackException()][apiexceptions].</span><span class="sxs-lookup"><span data-stu-id="7bb17-216">[Insert calls tootrackException() in your code][apiexceptions].</span></span>
* <span data-ttu-id="7bb17-217">[Installez hello Agent Java sur votre serveur](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="7bb17-217">[Install hello Java Agent on your server](app-insights-java-agent.md).</span></span> <span data-ttu-id="7bb17-218">Vous spécifiez des méthodes hello toowatch.</span><span class="sxs-lookup"><span data-stu-id="7bb17-218">You specify hello methods you want toowatch.</span></span>

## <a name="monitor-method-calls-and-external-dependencies"></a><span data-ttu-id="7bb17-219">Surveiller les appels de méthode et les dépendances externes</span><span class="sxs-lookup"><span data-stu-id="7bb17-219">Monitor method calls and external dependencies</span></span>
<span data-ttu-id="7bb17-220">[Installer hello Agent Java](app-insights-java-agent.md) toolog spécifié méthodes internes et les appels effectués via JDBC, avec des données de temporisation.</span><span class="sxs-lookup"><span data-stu-id="7bb17-220">[Install hello Java Agent](app-insights-java-agent.md) toolog specified internal methods and calls made through JDBC, with timing data.</span></span>

## <a name="performance-counters"></a><span data-ttu-id="7bb17-221">Compteurs de performances</span><span class="sxs-lookup"><span data-stu-id="7bb17-221">Performance counters</span></span>
<span data-ttu-id="7bb17-222">Ouvrez **paramètres**, **serveurs**, toosee une plage de compteurs de performance.</span><span class="sxs-lookup"><span data-stu-id="7bb17-222">Open **Settings**, **Servers**, toosee a range of performance counters.</span></span>

![](./media/app-insights-java-get-started/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a><span data-ttu-id="7bb17-223">Personnaliser la collecte des compteurs de performances</span><span class="sxs-lookup"><span data-stu-id="7bb17-223">Customize performance counter collection</span></span>
<span data-ttu-id="7bb17-224">collection de toodisable ensemble standard de hello des compteurs de performances, ajouter hello suivant code sous le nœud racine de hello du fichier de ApplicationInsights.xml hello :</span><span class="sxs-lookup"><span data-stu-id="7bb17-224">toodisable collection of hello standard set of performance counters, add hello following code under hello root node of hello ApplicationInsights.xml file:</span></span>

```XML
    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a><span data-ttu-id="7bb17-225">Collecter des compteurs de performances supplémentaires</span><span class="sxs-lookup"><span data-stu-id="7bb17-225">Collect additional performance counters</span></span>
<span data-ttu-id="7bb17-226">Vous pouvez spécifier toobe de compteurs de performances supplémentaires collectées.</span><span class="sxs-lookup"><span data-stu-id="7bb17-226">You can specify additional performance counters toobe collected.</span></span>

#### <a name="jmx-counters-exposed-by-hello-java-virtual-machine"></a><span data-ttu-id="7bb17-227">Compteurs JMX (exposées par la Machine virtuelle Java de hello)</span><span class="sxs-lookup"><span data-stu-id="7bb17-227">JMX counters (exposed by hello Java Virtual Machine)</span></span>

```XML
    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* <span data-ttu-id="7bb17-228">`displayName`– nom hello affiché dans le portail d’Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="7bb17-228">`displayName` – hello name displayed in hello Application Insights portal.</span></span>
* <span data-ttu-id="7bb17-229">`objectName`– nom de l’objet JMX hello.</span><span class="sxs-lookup"><span data-stu-id="7bb17-229">`objectName` – hello JMX object name.</span></span>
* <span data-ttu-id="7bb17-230">`attribute`: attribut hello de hello JMX objet nom toofetch</span><span class="sxs-lookup"><span data-stu-id="7bb17-230">`attribute` – hello attribute of hello JMX object name toofetch</span></span>
* <span data-ttu-id="7bb17-231">`type`(facultatif) : hello du type d’attribut de l’objet JMX :</span><span class="sxs-lookup"><span data-stu-id="7bb17-231">`type` (optional) - hello type of JMX object’s attribute:</span></span>
  * <span data-ttu-id="7bb17-232">Par défaut : un type simple, comme int ou long.</span><span class="sxs-lookup"><span data-stu-id="7bb17-232">Default: a simple type such as int or long.</span></span>
  * <span data-ttu-id="7bb17-233">`composite`: des données de compteur de performances hello sont au format hello de 'Attribute.Data'</span><span class="sxs-lookup"><span data-stu-id="7bb17-233">`composite`: hello perf counter data is in hello format of 'Attribute.Data'</span></span>
  * <span data-ttu-id="7bb17-234">`tabular`: des données de compteur de performances hello sont au format hello d’une ligne de table</span><span class="sxs-lookup"><span data-stu-id="7bb17-234">`tabular`: hello perf counter data is in hello format of a table row</span></span>

#### <a name="windows-performance-counters"></a><span data-ttu-id="7bb17-235">Compteurs de performances Windows</span><span class="sxs-lookup"><span data-stu-id="7bb17-235">Windows performance counters</span></span>
<span data-ttu-id="7bb17-236">Chaque [compteur de performances Windows](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) est un membre d’une catégorie (Bonjour même manière qu’un champ est un membre d’une classe).</span><span class="sxs-lookup"><span data-stu-id="7bb17-236">Each [Windows performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) is a member of a category (in hello same way that a field is a member of a class).</span></span> <span data-ttu-id="7bb17-237">Les catégories peuvent être globales ou peuvent avoir des instances numérotées ou nommées.</span><span class="sxs-lookup"><span data-stu-id="7bb17-237">Categories can either be global, or can have numbered or named instances.</span></span>

```XML
    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* <span data-ttu-id="7bb17-238">displayName : nom hello affiché dans le portail d’Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="7bb17-238">displayName – hello name displayed in hello Application Insights portal.</span></span>
* <span data-ttu-id="7bb17-239">nom de la catégorie : catégorie de compteur de performances hello (objet de performance) à laquelle ce compteur de performance est associé.</span><span class="sxs-lookup"><span data-stu-id="7bb17-239">categoryName – hello performance counter category (performance object) with which this performance counter is associated.</span></span>
* <span data-ttu-id="7bb17-240">counterName – nom hello hello du compteur de performance.</span><span class="sxs-lookup"><span data-stu-id="7bb17-240">counterName – hello name of hello performance counter.</span></span>
* <span data-ttu-id="7bb17-241">instanceName – nom hello de l’instance de catégorie de compteur de performance hello ou une chaîne vide (" »), si la catégorie de hello contient une seule instance.</span><span class="sxs-lookup"><span data-stu-id="7bb17-241">instanceName – hello name of hello performance counter category instance, or an empty string (""), if hello category contains a single instance.</span></span> <span data-ttu-id="7bb17-242">Si hello categoryName est le processus et compteur de performances hello vous aimeriez toocollect est à partir de processus de machine virtuelle Java hello actuel sur lequel votre application est en cours d’exécution, spécifiez `"__SELF__"`.</span><span class="sxs-lookup"><span data-stu-id="7bb17-242">If hello categoryName is Process, and hello performance counter you'd like toocollect is from hello current JVM process on which your app is running, specify `"__SELF__"`.</span></span>

<span data-ttu-id="7bb17-243">Les compteurs de performances sont visibles en tant que mesures personnalisées dans [Metrics Explorer][metrics].</span><span class="sxs-lookup"><span data-stu-id="7bb17-243">Your performance counters are visible as custom metrics in [Metrics Explorer][metrics].</span></span>

![](./media/app-insights-java-get-started/12-custom-perfs.png)

### <a name="unix-performance-counters"></a><span data-ttu-id="7bb17-244">Compteurs de performances Unix</span><span class="sxs-lookup"><span data-stu-id="7bb17-244">Unix performance counters</span></span>
* <span data-ttu-id="7bb17-245">[Installer collectd avec le plug-in de hello Application Insights](app-insights-java-collectd.md) tooget une grande variété de données système et réseau.</span><span class="sxs-lookup"><span data-stu-id="7bb17-245">[Install collectd with hello Application Insights plugin](app-insights-java-collectd.md) tooget a wide variety of system and network data.</span></span>

## <a name="get-user-and-session-data"></a><span data-ttu-id="7bb17-246">Obtenir des données utilisateur et de session</span><span class="sxs-lookup"><span data-stu-id="7bb17-246">Get user and session data</span></span>
<span data-ttu-id="7bb17-247">Vous envoyez des données de télémétrie depuis votre serveur web.</span><span class="sxs-lookup"><span data-stu-id="7bb17-247">OK, you're sending telemetry from your web server.</span></span> <span data-ttu-id="7bb17-248">Maintenant tooget hello vue 360 degrés de votre application, vous pouvez ajouter plus de surveillance :</span><span class="sxs-lookup"><span data-stu-id="7bb17-248">Now tooget hello full 360-degree view of your application, you can add more monitoring:</span></span>

* <span data-ttu-id="7bb17-249">[Ajouter des pages web télémétrie tooyour] [ usage] toomonitor page des vues et des mesures de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7bb17-249">[Add telemetry tooyour web pages][usage] toomonitor page views and user metrics.</span></span>
* <span data-ttu-id="7bb17-250">[Configurer des tests web] [ availability] toomake que votre application reste en direct et réactives.</span><span class="sxs-lookup"><span data-stu-id="7bb17-250">[Set up web tests][availability] toomake sure your application stays live and responsive.</span></span>

## <a name="capture-log-traces"></a><span data-ttu-id="7bb17-251">Capture le suivi des journaux</span><span class="sxs-lookup"><span data-stu-id="7bb17-251">Capture log traces</span></span>
<span data-ttu-id="7bb17-252">Vous pouvez utiliser Application Insights tooslice et manipulent des journaux à partir d’autres infrastructures de journalisation Log4J ou Logback.</span><span class="sxs-lookup"><span data-stu-id="7bb17-252">You can use Application Insights tooslice and dice logs from Log4J, Logback, or other logging frameworks.</span></span> <span data-ttu-id="7bb17-253">Vous pouvez corréler les journaux hello avec les requêtes HTTP et d’autres données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="7bb17-253">You can correlate hello logs with HTTP requests and other telemetry.</span></span> <span data-ttu-id="7bb17-254">[Découvrez comment][javalogs].</span><span class="sxs-lookup"><span data-stu-id="7bb17-254">[Learn how][javalogs].</span></span>

## <a name="send-your-own-telemetry"></a><span data-ttu-id="7bb17-255">Envoyer votre propre télémétrie</span><span class="sxs-lookup"><span data-stu-id="7bb17-255">Send your own telemetry</span></span>
<span data-ttu-id="7bb17-256">Maintenant que vous avez installé le Kit de développement logiciel de hello, vous pouvez utiliser vos propres données de télémétrie hello API toosend.</span><span class="sxs-lookup"><span data-stu-id="7bb17-256">Now that you've installed hello SDK, you can use hello API toosend your own telemetry.</span></span>

* <span data-ttu-id="7bb17-257">[Effectuer le suivi des événements et métriques personnalisés] [ api] toolearn ce que les utilisateurs font avec votre application.</span><span class="sxs-lookup"><span data-stu-id="7bb17-257">[Track custom events and metrics][api] toolearn what users are doing with your application.</span></span>
* <span data-ttu-id="7bb17-258">[Rechercher des événements et journaux] [ diagnostic] toohelp diagnostiquer les problèmes.</span><span class="sxs-lookup"><span data-stu-id="7bb17-258">[Search events and logs][diagnostic] toohelp diagnose problems.</span></span>

## <a name="availability-web-tests"></a><span data-ttu-id="7bb17-259">Tests web de disponibilité</span><span class="sxs-lookup"><span data-stu-id="7bb17-259">Availability web tests</span></span>
<span data-ttu-id="7bb17-260">Application Insights peuvent tester votre site Web à intervalles réguliers toocheck que c’est et répond bien.</span><span class="sxs-lookup"><span data-stu-id="7bb17-260">Application Insights can test your website at regular intervals toocheck that it's up and responding well.</span></span> <span data-ttu-id="7bb17-261">[tooset des][availability], cliquez sur les tests Web.</span><span class="sxs-lookup"><span data-stu-id="7bb17-261">[tooset up][availability], click Web tests.</span></span>

![Cliquez sur Tests web, puis sur Ajouter un test web](./media/app-insights-java-get-started/31-config-web-test.png)

<span data-ttu-id="7bb17-263">Vous obtenez des graphiques du temps de réponse, ainsi que des notifications par courrier électronique si votre site ne fonctionne plus.</span><span class="sxs-lookup"><span data-stu-id="7bb17-263">You'll get charts of response times, plus email notifications if your site goes down.</span></span>

![Exemple de test web](./media/app-insights-java-get-started/appinsights-10webtestresult.png)

<span data-ttu-id="7bb17-265">[En savoir plus sur les tests de disponibilité web.][availability]</span><span class="sxs-lookup"><span data-stu-id="7bb17-265">[Learn more about availability web tests.][availability]</span></span>

## <a name="questions-problems"></a><span data-ttu-id="7bb17-266">Des questions ?</span><span class="sxs-lookup"><span data-stu-id="7bb17-266">Questions?</span></span> <span data-ttu-id="7bb17-267">Des problèmes ?</span><span class="sxs-lookup"><span data-stu-id="7bb17-267">Problems?</span></span>
[<span data-ttu-id="7bb17-268">Résolution des problèmes Java</span><span class="sxs-lookup"><span data-stu-id="7bb17-268">Troubleshooting Java</span></span>](app-insights-java-troubleshoot.md)

## <a name="video"></a><span data-ttu-id="7bb17-269">Vidéo</span><span class="sxs-lookup"><span data-stu-id="7bb17-269">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="7bb17-270">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7bb17-270">Next steps</span></span>
* [<span data-ttu-id="7bb17-271">Surveillance des appels de dépendance</span><span class="sxs-lookup"><span data-stu-id="7bb17-271">Monitor dependency calls</span></span>](app-insights-java-agent.md)
* [<span data-ttu-id="7bb17-272">Surveillance des compteurs de performances Unix</span><span class="sxs-lookup"><span data-stu-id="7bb17-272">Monitor Unix performance counters</span></span>](app-insights-java-collectd.md)
* <span data-ttu-id="7bb17-273">Ajouter [analyse les pages web tooyour](app-insights-javascript.md) chargement de la page toomonitor délai d’attente, les appels AJAX, les exceptions de navigateur.</span><span class="sxs-lookup"><span data-stu-id="7bb17-273">Add [monitoring tooyour web pages](app-insights-javascript.md) toomonitor page load times, AJAX calls, browser exceptions.</span></span>
* <span data-ttu-id="7bb17-274">Écrire [une télémétrie personnalisée](app-insights-api-custom-events-metrics.md) tootrack utilisation dans le navigateur de hello ou sur le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="7bb17-274">Write [custom telemetry](app-insights-api-custom-events-metrics.md) tootrack usage in hello browser or at hello server.</span></span>
* <span data-ttu-id="7bb17-275">Créer [tableaux de bord](app-insights-dashboards.md) graphiques des clés toobring hello ensemble pour l’analyse de votre système.</span><span class="sxs-lookup"><span data-stu-id="7bb17-275">Create [dashboards](app-insights-dashboards.md) toobring together hello key charts for monitoring your system.</span></span>
* <span data-ttu-id="7bb17-276">Utilisez [Analytics](app-insights-analytics.md) pour des requêtes puissantes sur les données de télémétrie de votre application</span><span class="sxs-lookup"><span data-stu-id="7bb17-276">Use  [Analytics](app-insights-analytics.md) for powerful queries over telemetry from your app</span></span>
* <span data-ttu-id="7bb17-277">Pour plus d’informations, consultez [Azure pour les développeurs Java](/java/azure).</span><span class="sxs-lookup"><span data-stu-id="7bb17-277">For more information, visit [Azure for Java developers](/java/azure).</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#trackexception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[usage]: app-insights-javascript.md
