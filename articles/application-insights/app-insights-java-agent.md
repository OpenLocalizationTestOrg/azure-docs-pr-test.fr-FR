---
title: "aaaPerformance d’analyse pour les applications web Java dans Azure Application Insights | Documents Microsoft"
description: "Surveillance étendue des performances et de l’utilisation de votre site web Java avec Application Insights."
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 84017a48-1cb3-40c8-aab1-ff68d65e2128
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: bwren
ms.openlocfilehash: bf3983e3b4a16e72bc606b6468a757288d05ebaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-dependencies-exceptions-and-execution-times-in-java-web-apps"></a><span data-ttu-id="7a44b-103">Surveiller les dépendances, les exceptions et les temps d’exécution dans les applications web Java</span><span class="sxs-lookup"><span data-stu-id="7a44b-103">Monitor dependencies, exceptions and execution times in Java web apps</span></span>


<span data-ttu-id="7a44b-104">Si vous avez [instrumenter votre application de web Java avec Application Insights][java], vous pouvez utiliser hello Agent Java tooget des informations plus détaillées, sans aucune modification du code :</span><span class="sxs-lookup"><span data-stu-id="7a44b-104">If you have [instrumented your Java web app with Application Insights][java], you can use hello Java Agent tooget deeper insights, without any code changes:</span></span>

* <span data-ttu-id="7a44b-105">**Dépendances :** données sur les appels que votre application effectue des composants tooother, y compris :</span><span class="sxs-lookup"><span data-stu-id="7a44b-105">**Dependencies:** Data about calls that your application makes tooother components, including:</span></span>
  * <span data-ttu-id="7a44b-106">**Appels REST** passés via HttpClient, OkHttp et RestTemplate (Spring).</span><span class="sxs-lookup"><span data-stu-id="7a44b-106">**REST calls** made via HttpClient, OkHttp, and RestTemplate (Spring).</span></span>
  * <span data-ttu-id="7a44b-107">**Redis** appels effectués via le client Jedis hello.</span><span class="sxs-lookup"><span data-stu-id="7a44b-107">**Redis** calls made via hello Jedis client.</span></span> <span data-ttu-id="7a44b-108">Si l’appel de hello prend plu de 10 s, l’agent de hello extrait également les arguments de l’appel hello.</span><span class="sxs-lookup"><span data-stu-id="7a44b-108">If hello call takes longer than 10s, hello agent also fetches hello call arguments.</span></span>
  * <span data-ttu-id="7a44b-109">**[Appels JDBC](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)** : base de données MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB ou Apache Derby.</span><span class="sxs-lookup"><span data-stu-id="7a44b-109">**[JDBC calls](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)** - MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB or Apache Derby DB.</span></span> <span data-ttu-id="7a44b-110">Les appels de « executeBatch » sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="7a44b-110">"executeBatch" calls are supported.</span></span> <span data-ttu-id="7a44b-111">MySQL et PostgreSQL, si l’appel de hello prend plu de 10 s, l’agent de hello indique plan de requête hello.</span><span class="sxs-lookup"><span data-stu-id="7a44b-111">For MySQL and PostgreSQL, if hello call takes longer than 10s, hello agent reports hello query plan.</span></span>
* <span data-ttu-id="7a44b-112">**Exceptions interceptées** : données concernant les exceptions gérées par votre code.</span><span class="sxs-lookup"><span data-stu-id="7a44b-112">**Caught exceptions:** Data about exceptions that are handled by your code.</span></span>
* <span data-ttu-id="7a44b-113">**Durée d’exécution de méthode :** données sur hello fois qu’il prend tooexecute des méthodes spécifiques.</span><span class="sxs-lookup"><span data-stu-id="7a44b-113">**Method execution time:** Data about hello time it takes tooexecute specific methods.</span></span>

<span data-ttu-id="7a44b-114">l’agent de toouse hello Java, vous installez sur votre serveur.</span><span class="sxs-lookup"><span data-stu-id="7a44b-114">toouse hello Java agent, you install it on your server.</span></span> <span data-ttu-id="7a44b-115">Vos applications web doivent être instrumentées avec hello [Application Insights Java SDK][java].</span><span class="sxs-lookup"><span data-stu-id="7a44b-115">Your web apps must be instrumented with hello [Application Insights Java SDK][java].</span></span> 

## <a name="install-hello-application-insights-agent-for-java"></a><span data-ttu-id="7a44b-116">Installer l’agent d’Application Insights hello pour Java</span><span class="sxs-lookup"><span data-stu-id="7a44b-116">Install hello Application Insights agent for Java</span></span>
1. <span data-ttu-id="7a44b-117">Sur l’ordinateur de hello exécute votre serveur Java, [télécharger l’agent de hello](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="7a44b-117">On hello machine running your Java server, [download hello agent](https://aka.ms/aijavasdk).</span></span>
2. <span data-ttu-id="7a44b-118">Modifier le script de démarrage de server application hello et ajoutez hello suivant JVM :</span><span class="sxs-lookup"><span data-stu-id="7a44b-118">Edit hello application server startup script, and add hello following JVM:</span></span>
   
    <span data-ttu-id="7a44b-119">`javaagent:`*fichier JAR de chemin d’accès complet toohello agent*</span><span class="sxs-lookup"><span data-stu-id="7a44b-119">`javaagent:`*full path toohello agent JAR file*</span></span>
   
    <span data-ttu-id="7a44b-120">Par exemple, dans Tomcat sur une machine Linux :</span><span class="sxs-lookup"><span data-stu-id="7a44b-120">For example, in Tomcat on a Linux machine:</span></span>
   
    `export JAVA_OPTS="$JAVA_OPTS -javaagent:<full path tooagent JAR file>"`
3. <span data-ttu-id="7a44b-121">Redémarrez votre serveur d’applications.</span><span class="sxs-lookup"><span data-stu-id="7a44b-121">Restart your application server.</span></span>

## <a name="configure-hello-agent"></a><span data-ttu-id="7a44b-122">Configurer l’agent de hello</span><span class="sxs-lookup"><span data-stu-id="7a44b-122">Configure hello agent</span></span>
<span data-ttu-id="7a44b-123">Créez un fichier nommé `AI-Agent.xml` et placez-le dans hello même dossier que le fichier JAR de l’agent hello.</span><span class="sxs-lookup"><span data-stu-id="7a44b-123">Create a file named `AI-Agent.xml` and place it in hello same folder as hello agent JAR file.</span></span>

<span data-ttu-id="7a44b-124">Définir le contenu du fichier xml de hello hello.</span><span class="sxs-lookup"><span data-stu-id="7a44b-124">Set hello content of hello xml file.</span></span> <span data-ttu-id="7a44b-125">Modifier hello suivant exemple tooinclude ou omettre des fonctionnalités hello que vous souhaitez.</span><span class="sxs-lookup"><span data-stu-id="7a44b-125">Edit hello following example tooinclude or omit hello features you want.</span></span>

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsightsAgent>
      <Instrumentation>

        <!-- Collect remote dependency data -->
        <BuiltIn enabled="true">
           <!-- Disable Redis or alter threshold call duration above which arguments are sent.
               Defaults: enabled, 10000 ms -->
           <Jedis enabled="true" thresholdInMS="1000"/>

           <!-- Set SQL query duration above which query plan is reported (MySQL, PostgreSQL). Default is 10000 ms. -->
           <MaxStatementQueryLimitInMS>1000</MaxStatementQueryLimitInMS>
        </BuiltIn>

        <!-- Collect data about caught exceptions
             and method execution times -->

        <Class name="com.myCompany.MyClass">
           <Method name="methodOne"
               reportCaughtExceptions="true"
               reportExecutionTime="true"
               />

           <!-- Report on hello particular signature
                void methodTwo(String, int) -->
           <Method name="methodTwo"
              reportExecutionTime="true"
              signature="(Ljava/lang/String;I)V" />
        </Class>

      </Instrumentation>
    </ApplicationInsightsAgent>

```

<span data-ttu-id="7a44b-126">Vous avez tooenable rapports exception et le minutage de méthode pour les méthodes individuelles.</span><span class="sxs-lookup"><span data-stu-id="7a44b-126">You have tooenable reports exception and method timing for individual methods.</span></span>

<span data-ttu-id="7a44b-127">Par défaut, `reportExecutionTime` est défini sur true, et `reportCaughtExceptions` sur false.</span><span class="sxs-lookup"><span data-stu-id="7a44b-127">By default, `reportExecutionTime` is true and `reportCaughtExceptions` is false.</span></span>

## <a name="view-hello-data"></a><span data-ttu-id="7a44b-128">Afficher les données hello</span><span class="sxs-lookup"><span data-stu-id="7a44b-128">View hello data</span></span>
<span data-ttu-id="7a44b-129">Bonjour ressource Application Insights, agrégées temps d’exécution dépendance et la méthode à distance apparaît [sous hello performances vignette][metrics].</span><span class="sxs-lookup"><span data-stu-id="7a44b-129">In hello Application Insights resource, aggregated remote dependency and method execution times appears [under hello Performance tile][metrics].</span></span>

<span data-ttu-id="7a44b-130">toosearch pour des instances de rapports de dépendance, d’exception et de méthode, ouvrez [recherche][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="7a44b-130">toosearch for individual instances of dependency, exception, and method reports, open [Search][diagnostic].</span></span>

<span data-ttu-id="7a44b-131">[En savoir plus sur le diagnostic des problèmes de dépendance](app-insights-asp-net-dependencies.md#diagnosis).</span><span class="sxs-lookup"><span data-stu-id="7a44b-131">[Diagnosing dependency issues - learn more](app-insights-asp-net-dependencies.md#diagnosis).</span></span>

## <a name="questions-problems"></a><span data-ttu-id="7a44b-132">Des questions ?</span><span class="sxs-lookup"><span data-stu-id="7a44b-132">Questions?</span></span> <span data-ttu-id="7a44b-133">Des problèmes ?</span><span class="sxs-lookup"><span data-stu-id="7a44b-133">Problems?</span></span>
* <span data-ttu-id="7a44b-134">Pas de données ?</span><span class="sxs-lookup"><span data-stu-id="7a44b-134">No data?</span></span> [<span data-ttu-id="7a44b-135">Définir les exceptions de pare-feu</span><span class="sxs-lookup"><span data-stu-id="7a44b-135">Set firewall exceptions</span></span>](app-insights-ip-addresses.md)
* [<span data-ttu-id="7a44b-136">Résolution des problèmes Java</span><span class="sxs-lookup"><span data-stu-id="7a44b-136">Troubleshooting Java</span></span>](app-insights-java-troubleshoot.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
