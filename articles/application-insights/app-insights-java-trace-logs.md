---
title: aaaExplore trace de Java consigne dans Azure Application Insights | Documents Microsoft
description: Recherche de suivi Log4J ou Logback dans Application Insights
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: fc0a9e2f-3beb-4f47-a9fe-3f86cd29d97a
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/12/2016
ms.author: bwren
ms.openlocfilehash: e5f8e8c67e57753ba7574b97aa96dbb41db00ce1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="explore-java-trace-logs-in-application-insights"></a><span data-ttu-id="ee0da-103">Exploration du suivi des journaux Java dans Application Insights</span><span class="sxs-lookup"><span data-stu-id="ee0da-103">Explore Java trace logs in Application Insights</span></span>
<span data-ttu-id="ee0da-104">Si vous utilisez Logback ou Log4J (version 1.2 ou version 2.0) pour le suivi, vous pouvez avoir vos journaux de trace envoyés automatiquement tooApplication Insights où vous pouvez Explorer et effectuer des recherches.</span><span class="sxs-lookup"><span data-stu-id="ee0da-104">If you're using Logback or Log4J (v1.2 or v2.0) for tracing, you can have your trace logs sent automatically tooApplication Insights where you can explore and search on them.</span></span>

## <a name="install-hello-java-sdk"></a><span data-ttu-id="ee0da-105">Installer hello Kit de développement logiciel Java</span><span class="sxs-lookup"><span data-stu-id="ee0da-105">Install hello Java SDK</span></span>

<span data-ttu-id="ee0da-106">Installez le [kit de développement logiciel (SDK) Application Insights pour Java][java], si ce n’est pas déjà fait.</span><span class="sxs-lookup"><span data-stu-id="ee0da-106">Install [Application Insights SDK for Java][java], if you haven't already done that.</span></span>

<span data-ttu-id="ee0da-107">(Si vous ne souhaitez pas les demandes tootrack HTTP, vous pouvez omettre la majeure partie du fichier de configuration .xml hello, mais vous devez inclure au moins hello `InstrumentationKey` élément.</span><span class="sxs-lookup"><span data-stu-id="ee0da-107">(If you don't want tootrack HTTP requests, you can omit most of hello .xml configuration file, but you must at least include hello `InstrumentationKey` element.</span></span> <span data-ttu-id="ee0da-108">Vous devez également appeler `new TelemetryClient()` tooinitialize hello SDK.)</span><span class="sxs-lookup"><span data-stu-id="ee0da-108">You should also call `new TelemetryClient()` tooinitialize hello SDK.)</span></span>


## <a name="add-logging-libraries-tooyour-project"></a><span data-ttu-id="ee0da-109">Ajouter un projet de tooyour de bibliothèques de journalisation</span><span class="sxs-lookup"><span data-stu-id="ee0da-109">Add logging libraries tooyour project</span></span>
<span data-ttu-id="ee0da-110">*Choisissez hello approprié pour votre projet.*</span><span class="sxs-lookup"><span data-stu-id="ee0da-110">*Choose hello appropriate way for your project.*</span></span>

#### <a name="if-youre-using-maven"></a><span data-ttu-id="ee0da-111">Si vous utilisez Maven...</span><span class="sxs-lookup"><span data-stu-id="ee0da-111">If you're using Maven...</span></span>
<span data-ttu-id="ee0da-112">Si votre projet est déjà configuré toouse Maven pour la build, un des hello suivant des extraits de code dans votre fichier pom.xml de fusion.</span><span class="sxs-lookup"><span data-stu-id="ee0da-112">If your project is already set up toouse Maven for build, merge one of hello following snippets of code into your pom.xml file.</span></span>

<span data-ttu-id="ee0da-113">Puis actualiser les dépendances du projet hello, les binaires de hello tooget téléchargés.</span><span class="sxs-lookup"><span data-stu-id="ee0da-113">Then refresh hello project dependencies, tooget hello binaries downloaded.</span></span>

<span data-ttu-id="ee0da-114">*Logback*</span><span class="sxs-lookup"><span data-stu-id="ee0da-114">*Logback*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-logback</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

<span data-ttu-id="ee0da-115">*Log4J v2.0*</span><span class="sxs-lookup"><span data-stu-id="ee0da-115">*Log4J v2.0*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

<span data-ttu-id="ee0da-116">*Log4J v1.2*</span><span class="sxs-lookup"><span data-stu-id="ee0da-116">*Log4J v1.2*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j1_2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

#### <a name="if-youre-using-gradle"></a><span data-ttu-id="ee0da-117">Si vous utilisez Gradle...</span><span class="sxs-lookup"><span data-stu-id="ee0da-117">If you're using Gradle...</span></span>
<span data-ttu-id="ee0da-118">Si votre projet est déjà configuré toouse Gradle pour la build, ajoutez l’un des hello suivant lignes toohello `dependencies` groupe dans votre fichier build.gradle :</span><span class="sxs-lookup"><span data-stu-id="ee0da-118">If your project is already set up toouse Gradle for build, add one of hello following lines toohello `dependencies` group in your build.gradle file:</span></span>

<span data-ttu-id="ee0da-119">Puis actualiser les dépendances du projet hello, les binaires de hello tooget téléchargés.</span><span class="sxs-lookup"><span data-stu-id="ee0da-119">Then refresh hello project dependencies, tooget hello binaries downloaded.</span></span>

<span data-ttu-id="ee0da-120">**Logback**</span><span class="sxs-lookup"><span data-stu-id="ee0da-120">**Logback**</span></span>

```

    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-logback', version: '1.0.+'
```

<span data-ttu-id="ee0da-121">**Log4J v2.0**</span><span class="sxs-lookup"><span data-stu-id="ee0da-121">**Log4J v2.0**</span></span>

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j2', version: '1.0.+'
```

<span data-ttu-id="ee0da-122">**Log4J v1.2**</span><span class="sxs-lookup"><span data-stu-id="ee0da-122">**Log4J v1.2**</span></span>

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j1_2', version: '1.0.+'
```

#### <a name="otherwise-"></a><span data-ttu-id="ee0da-123">Sinon...</span><span class="sxs-lookup"><span data-stu-id="ee0da-123">Otherwise ...</span></span>
<span data-ttu-id="ee0da-124">Télécharger et extraire appender approprié de hello, puis ajouter un projet de tooyour hello bibliothèque appropriée :</span><span class="sxs-lookup"><span data-stu-id="ee0da-124">Download and extract hello appropriate appender, then add hello appropriate library tooyour project:</span></span>

| <span data-ttu-id="ee0da-125">Enregistreur</span><span class="sxs-lookup"><span data-stu-id="ee0da-125">Logger</span></span> | <span data-ttu-id="ee0da-126">Télécharger</span><span class="sxs-lookup"><span data-stu-id="ee0da-126">Download</span></span> | <span data-ttu-id="ee0da-127">Bibliothèque</span><span class="sxs-lookup"><span data-stu-id="ee0da-127">Library</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ee0da-128">Logback</span><span class="sxs-lookup"><span data-stu-id="ee0da-128">Logback</span></span> |[<span data-ttu-id="ee0da-129">Kit de développement logiciel (SDK) avec appender Logback</span><span class="sxs-lookup"><span data-stu-id="ee0da-129">SDK with Logback appender</span></span>](https://aka.ms/xt62a4) |<span data-ttu-id="ee0da-130">applicationinsights-logging-logback</span><span class="sxs-lookup"><span data-stu-id="ee0da-130">applicationinsights-logging-logback</span></span> |
| <span data-ttu-id="ee0da-131">Log4J v2.0</span><span class="sxs-lookup"><span data-stu-id="ee0da-131">Log4J v2.0</span></span> |[<span data-ttu-id="ee0da-132">Kit de développement logiciel (SDK) avec appender Log4J v2</span><span class="sxs-lookup"><span data-stu-id="ee0da-132">SDK with Log4J v2 appender</span></span>](https://aka.ms/qypznq) |<span data-ttu-id="ee0da-133">applicationinsights-logging-log4j2</span><span class="sxs-lookup"><span data-stu-id="ee0da-133">applicationinsights-logging-log4j2</span></span> |
| <span data-ttu-id="ee0da-134">Log4J v1.2</span><span class="sxs-lookup"><span data-stu-id="ee0da-134">Log4j v1.2</span></span> |[<span data-ttu-id="ee0da-135">Kit de développement logiciel (SDK) avec appender Log4J v1.2</span><span class="sxs-lookup"><span data-stu-id="ee0da-135">SDK with Log4J v1.2 appender</span></span>](https://aka.ms/ky9cbo) |<span data-ttu-id="ee0da-136">applicationinsights-logging-log4j1_2</span><span class="sxs-lookup"><span data-stu-id="ee0da-136">applicationinsights-logging-log4j1_2</span></span> |

## <a name="add-hello-appender-tooyour-logging-framework"></a><span data-ttu-id="ee0da-137">Ajouter l’infrastructure de journalisation de tooyour appender hello</span><span class="sxs-lookup"><span data-stu-id="ee0da-137">Add hello appender tooyour logging framework</span></span>
<span data-ttu-id="ee0da-138">toostart mise en route de traces, fusion hello extrait de code toohello Log4J ou Logback les fichier de configuration :</span><span class="sxs-lookup"><span data-stu-id="ee0da-138">toostart getting traces, merge hello relevant snippet of code toohello Log4J or Logback configuration file:</span></span> 

<span data-ttu-id="ee0da-139">*Logback*</span><span class="sxs-lookup"><span data-stu-id="ee0da-139">*Logback*</span></span>

```XML

    <appender name="aiAppender" 
      class="com.microsoft.applicationinsights.logback.ApplicationInsightsAppender">
    </appender>
    <root level="trace">
      <appender-ref ref="aiAppender" />
    </root>
```

<span data-ttu-id="ee0da-140">*Log4J v2.0*</span><span class="sxs-lookup"><span data-stu-id="ee0da-140">*Log4J v2.0*</span></span>

```XML

    <Configuration packages="com.microsoft.applicationinsights.Log4j">
      <Appenders>
        <ApplicationInsightsAppender name="aiAppender" />
      </Appenders>
      <Loggers>
        <Root level="trace">
          <AppenderRef ref="aiAppender"/>
        </Root>
      </Loggers>
    </Configuration>
```

<span data-ttu-id="ee0da-141">*Log4J v1.2*</span><span class="sxs-lookup"><span data-stu-id="ee0da-141">*Log4J v1.2*</span></span>

```XML

    <appender name="aiAppender" 
         class="com.microsoft.applicationinsights.log4j.v1_2.ApplicationInsightsAppender">
    </appender>
    <root>
      <priority value ="trace" />
      <appender-ref ref="aiAppender" />
    </root>
```

<span data-ttu-id="ee0da-142">appenders d’Application Insights Hello peuvent être référencées par n’importe quel journal configuré et pas nécessairement par l’enregistreur d’événements de hello racine (comme indiqué dans les exemples de code hello ci-dessus).</span><span class="sxs-lookup"><span data-stu-id="ee0da-142">hello Application Insights appenders can be referenced by any configured logger, and not necessarily by hello root logger (as shown in hello code samples above).</span></span>

## <a name="explore-your-traces-in-hello-application-insights-portal"></a><span data-ttu-id="ee0da-143">Explorer vos traces dans le portail Application Insights de hello</span><span class="sxs-lookup"><span data-stu-id="ee0da-143">Explore your traces in hello Application Insights portal</span></span>
<span data-ttu-id="ee0da-144">Maintenant que vous avez configuré votre toosend projet effectue le suivi tooApplication Insights, vous pouvez afficher et rechercher ces suivis dans hello du portail Application Insights hello [recherche] [ diagnostic] panneau.</span><span class="sxs-lookup"><span data-stu-id="ee0da-144">Now that you've configured your project toosend traces tooApplication Insights, you can view and search these traces in hello Application Insights portal, in hello [Search][diagnostic] blade.</span></span>

![Dans le portail Application Insights hello, ouvrir la recherche](./media/app-insights-java-trace-logs/10-diagnostics.png)

## <a name="next-steps"></a><span data-ttu-id="ee0da-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ee0da-146">Next steps</span></span>
<span data-ttu-id="ee0da-147">[Recherche de diagnostic][diagnostic]</span><span class="sxs-lookup"><span data-stu-id="ee0da-147">[Diagnostic search][diagnostic]</span></span>

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md


