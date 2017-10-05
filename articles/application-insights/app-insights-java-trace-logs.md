---
title: "Exploration des journaux de traçage Java dans Application Insights | Documents Microsoft"
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
ms.openlocfilehash: 5baba3deaf58a1a24995c60381592a9c2ffefd81
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="explore-java-trace-logs-in-application-insights"></a><span data-ttu-id="3ba3a-103">Exploration du suivi des journaux Java dans Application Insights</span><span class="sxs-lookup"><span data-stu-id="3ba3a-103">Explore Java trace logs in Application Insights</span></span>
<span data-ttu-id="3ba3a-104">Si vous utilisez Logback ou Log4J (v1.2 ou v2.0) pour le suivi, vous pouvez faire en sorte que vos journaux de suivi soient envoyés automatiquement à Application Insights, où vous pouvez les explorer et effectuer des recherches.</span><span class="sxs-lookup"><span data-stu-id="3ba3a-104">If you're using Logback or Log4J (v1.2 or v2.0) for tracing, you can have your trace logs sent automatically to Application Insights where you can explore and search on them.</span></span>

## <a name="install-the-java-sdk"></a><span data-ttu-id="3ba3a-105">Installer le Kit de développement logiciel (SDK) Java</span><span class="sxs-lookup"><span data-stu-id="3ba3a-105">Install the Java SDK</span></span>

<span data-ttu-id="3ba3a-106">Installez le [kit de développement logiciel (SDK) Application Insights pour Java][java], si ce n’est pas déjà fait.</span><span class="sxs-lookup"><span data-stu-id="3ba3a-106">Install [Application Insights SDK for Java][java], if you haven't already done that.</span></span>

<span data-ttu-id="3ba3a-107">(Si vous ne voulez pas suivre les demandes HTTP, vous pouvez omettre la majeure partie du fichier de configuration .xml, mais vous devez inclure au moins l’élément `InstrumentationKey`.</span><span class="sxs-lookup"><span data-stu-id="3ba3a-107">(If you don't want to track HTTP requests, you can omit most of the .xml configuration file, but you must at least include the `InstrumentationKey` element.</span></span> <span data-ttu-id="3ba3a-108">Vous devez également appeler `new TelemetryClient()` pour initialiser le Kit de développement logiciel [SDK].)</span><span class="sxs-lookup"><span data-stu-id="3ba3a-108">You should also call `new TelemetryClient()` to initialize the SDK.)</span></span>


## <a name="add-logging-libraries-to-your-project"></a><span data-ttu-id="3ba3a-109">Ajouter des bibliothèques de journalisation à votre projet</span><span class="sxs-lookup"><span data-stu-id="3ba3a-109">Add logging libraries to your project</span></span>
<span data-ttu-id="3ba3a-110">*Choisissez la méthode adaptée à votre projet.*</span><span class="sxs-lookup"><span data-stu-id="3ba3a-110">*Choose the appropriate way for your project.*</span></span>

#### <a name="if-youre-using-maven"></a><span data-ttu-id="3ba3a-111">Si vous utilisez Maven...</span><span class="sxs-lookup"><span data-stu-id="3ba3a-111">If you're using Maven...</span></span>
<span data-ttu-id="3ba3a-112">Si votre projet est déjà configuré pour être assemblé avec Maven, fusionnez les extraits de code suivants dans votre fichier pom.xml.</span><span class="sxs-lookup"><span data-stu-id="3ba3a-112">If your project is already set up to use Maven for build, merge one of the following snippets of code into your pom.xml file.</span></span>

<span data-ttu-id="3ba3a-113">Actualisez ensuite les dépendances du projet pour télécharger les fichiers binaires.</span><span class="sxs-lookup"><span data-stu-id="3ba3a-113">Then refresh the project dependencies, to get the binaries downloaded.</span></span>

<span data-ttu-id="3ba3a-114">*Logback*</span><span class="sxs-lookup"><span data-stu-id="3ba3a-114">*Logback*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-logback</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

<span data-ttu-id="3ba3a-115">*Log4J v2.0*</span><span class="sxs-lookup"><span data-stu-id="3ba3a-115">*Log4J v2.0*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

<span data-ttu-id="3ba3a-116">*Log4J v1.2*</span><span class="sxs-lookup"><span data-stu-id="3ba3a-116">*Log4J v1.2*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j1_2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

#### <a name="if-youre-using-gradle"></a><span data-ttu-id="3ba3a-117">Si vous utilisez Gradle...</span><span class="sxs-lookup"><span data-stu-id="3ba3a-117">If you're using Gradle...</span></span>
<span data-ttu-id="3ba3a-118">Si votre projet est déjà configuré pour utiliser Gradle, ajoutez une des lignes suivantes au groupe `dependencies` dans votre fichier build.gradle :</span><span class="sxs-lookup"><span data-stu-id="3ba3a-118">If your project is already set up to use Gradle for build, add one of the following lines to the `dependencies` group in your build.gradle file:</span></span>

<span data-ttu-id="3ba3a-119">Actualisez ensuite les dépendances du projet pour télécharger les fichiers binaires.</span><span class="sxs-lookup"><span data-stu-id="3ba3a-119">Then refresh the project dependencies, to get the binaries downloaded.</span></span>

<span data-ttu-id="3ba3a-120">**Logback**</span><span class="sxs-lookup"><span data-stu-id="3ba3a-120">**Logback**</span></span>

```

    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-logback', version: '1.0.+'
```

<span data-ttu-id="3ba3a-121">**Log4J v2.0**</span><span class="sxs-lookup"><span data-stu-id="3ba3a-121">**Log4J v2.0**</span></span>

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j2', version: '1.0.+'
```

<span data-ttu-id="3ba3a-122">**Log4J v1.2**</span><span class="sxs-lookup"><span data-stu-id="3ba3a-122">**Log4J v1.2**</span></span>

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j1_2', version: '1.0.+'
```

#### <a name="otherwise-"></a><span data-ttu-id="3ba3a-123">Sinon...</span><span class="sxs-lookup"><span data-stu-id="3ba3a-123">Otherwise ...</span></span>
<span data-ttu-id="3ba3a-124">Téléchargez et décompressez l’appender approprié, puis ajoutez la bibliothèque qui convient à votre projet :</span><span class="sxs-lookup"><span data-stu-id="3ba3a-124">Download and extract the appropriate appender, then add the appropriate library to your project:</span></span>

| <span data-ttu-id="3ba3a-125">Enregistreur</span><span class="sxs-lookup"><span data-stu-id="3ba3a-125">Logger</span></span> | <span data-ttu-id="3ba3a-126">Télécharger</span><span class="sxs-lookup"><span data-stu-id="3ba3a-126">Download</span></span> | <span data-ttu-id="3ba3a-127">Bibliothèque</span><span class="sxs-lookup"><span data-stu-id="3ba3a-127">Library</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3ba3a-128">Logback</span><span class="sxs-lookup"><span data-stu-id="3ba3a-128">Logback</span></span> |[<span data-ttu-id="3ba3a-129">Kit de développement logiciel (SDK) avec appender Logback</span><span class="sxs-lookup"><span data-stu-id="3ba3a-129">SDK with Logback appender</span></span>](https://aka.ms/xt62a4) |<span data-ttu-id="3ba3a-130">applicationinsights-logging-logback</span><span class="sxs-lookup"><span data-stu-id="3ba3a-130">applicationinsights-logging-logback</span></span> |
| <span data-ttu-id="3ba3a-131">Log4J v2.0</span><span class="sxs-lookup"><span data-stu-id="3ba3a-131">Log4J v2.0</span></span> |[<span data-ttu-id="3ba3a-132">Kit de développement logiciel (SDK) avec appender Log4J v2</span><span class="sxs-lookup"><span data-stu-id="3ba3a-132">SDK with Log4J v2 appender</span></span>](https://aka.ms/qypznq) |<span data-ttu-id="3ba3a-133">applicationinsights-logging-log4j2</span><span class="sxs-lookup"><span data-stu-id="3ba3a-133">applicationinsights-logging-log4j2</span></span> |
| <span data-ttu-id="3ba3a-134">Log4J v1.2</span><span class="sxs-lookup"><span data-stu-id="3ba3a-134">Log4j v1.2</span></span> |[<span data-ttu-id="3ba3a-135">Kit de développement logiciel (SDK) avec appender Log4J v1.2</span><span class="sxs-lookup"><span data-stu-id="3ba3a-135">SDK with Log4J v1.2 appender</span></span>](https://aka.ms/ky9cbo) |<span data-ttu-id="3ba3a-136">applicationinsights-logging-log4j1_2</span><span class="sxs-lookup"><span data-stu-id="3ba3a-136">applicationinsights-logging-log4j1_2</span></span> |

## <a name="add-the-appender-to-your-logging-framework"></a><span data-ttu-id="3ba3a-137">Ajouter l’appender à votre infrastructure de journalisation</span><span class="sxs-lookup"><span data-stu-id="3ba3a-137">Add the appender to your logging framework</span></span>
<span data-ttu-id="3ba3a-138">Pour recevoir le suivi, fusionnez l’extrait de code approprié dans le fichier de configuration Log4J ou Logback :</span><span class="sxs-lookup"><span data-stu-id="3ba3a-138">To start getting traces, merge the relevant snippet of code to the Log4J or Logback configuration file:</span></span> 

<span data-ttu-id="3ba3a-139">*Logback*</span><span class="sxs-lookup"><span data-stu-id="3ba3a-139">*Logback*</span></span>

```XML

    <appender name="aiAppender" 
      class="com.microsoft.applicationinsights.logback.ApplicationInsightsAppender">
    </appender>
    <root level="trace">
      <appender-ref ref="aiAppender" />
    </root>
```

<span data-ttu-id="3ba3a-140">*Log4J v2.0*</span><span class="sxs-lookup"><span data-stu-id="3ba3a-140">*Log4J v2.0*</span></span>

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

<span data-ttu-id="3ba3a-141">*Log4J v1.2*</span><span class="sxs-lookup"><span data-stu-id="3ba3a-141">*Log4J v1.2*</span></span>

```XML

    <appender name="aiAppender" 
         class="com.microsoft.applicationinsights.log4j.v1_2.ApplicationInsightsAppender">
    </appender>
    <root>
      <priority value ="trace" />
      <appender-ref ref="aiAppender" />
    </root>
```

<span data-ttu-id="3ba3a-142">Les appenders Application Insights peuvent être référencés par n’importe quel enregistreur configuré et pas nécessairement par l’enregistreur racine (comme indiqué dans les exemples de code ci-dessus).</span><span class="sxs-lookup"><span data-stu-id="3ba3a-142">The Application Insights appenders can be referenced by any configured logger, and not necessarily by the root logger (as shown in the code samples above).</span></span>

## <a name="explore-your-traces-in-the-application-insights-portal"></a><span data-ttu-id="3ba3a-143">Explorer le suivi dans le portail Application Insights</span><span class="sxs-lookup"><span data-stu-id="3ba3a-143">Explore your traces in the Application Insights portal</span></span>
<span data-ttu-id="3ba3a-144">Maintenant que vous avez configuré votre projet pour qu’il envoie le suivi à Application Insights, vous pouvez rechercher et consulter ce suivi dans le portail Application Insights, dans le panneau [Recherche][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="3ba3a-144">Now that you've configured your project to send traces to Application Insights, you can view and search these traces in the Application Insights portal, in the [Search][diagnostic] blade.</span></span>

![Dans Application Insights, ouvrez Recherche](./media/app-insights-java-trace-logs/10-diagnostics.png)

## <a name="next-steps"></a><span data-ttu-id="3ba3a-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3ba3a-146">Next steps</span></span>
<span data-ttu-id="3ba3a-147">[Recherche de diagnostic][diagnostic]</span><span class="sxs-lookup"><span data-stu-id="3ba3a-147">[Diagnostic search][diagnostic]</span></span>

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md


