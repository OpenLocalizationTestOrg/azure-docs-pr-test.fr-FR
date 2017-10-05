---
title: Surveillance des performances des applications web Java dans Azure Application Insights | Microsoft Docs
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
ms.openlocfilehash: 4e56998382610ad3d7224e6a8de5aee5419ebe43
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-dependencies-exceptions-and-execution-times-in-java-web-apps"></a><span data-ttu-id="d3a49-103">Surveiller les dépendances, les exceptions et les temps d’exécution dans les applications web Java</span><span class="sxs-lookup"><span data-stu-id="d3a49-103">Monitor dependencies, exceptions and execution times in Java web apps</span></span>


<span data-ttu-id="d3a49-104">Si vous avez [instrumenté votre application web Java avec Application Insights][java], vous pouvez utiliser l’agent Java pour obtenir des informations plus détaillées, sans pour autant modifier le code :</span><span class="sxs-lookup"><span data-stu-id="d3a49-104">If you have [instrumented your Java web app with Application Insights][java], you can use the Java Agent to get deeper insights, without any code changes:</span></span>

* <span data-ttu-id="d3a49-105">**Dépendances :** données sur les appels passés par votre application à destination d’autres composants, dont :</span><span class="sxs-lookup"><span data-stu-id="d3a49-105">**Dependencies:** Data about calls that your application makes to other components, including:</span></span>
  * <span data-ttu-id="d3a49-106">**Appels REST** passés via HttpClient, OkHttp et RestTemplate (Spring).</span><span class="sxs-lookup"><span data-stu-id="d3a49-106">**REST calls** made via HttpClient, OkHttp, and RestTemplate (Spring).</span></span>
  * <span data-ttu-id="d3a49-107">**Redis** passés via le client Jedis.</span><span class="sxs-lookup"><span data-stu-id="d3a49-107">**Redis** calls made via the Jedis client.</span></span> <span data-ttu-id="d3a49-108">Si l’appel prend plus de 10 s, l’agent récupère également les arguments d’appel.</span><span class="sxs-lookup"><span data-stu-id="d3a49-108">If the call takes longer than 10s, the agent also fetches the call arguments.</span></span>
  * <span data-ttu-id="d3a49-109">**[Appels JDBC](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)** : base de données MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB ou Apache Derby.</span><span class="sxs-lookup"><span data-stu-id="d3a49-109">**[JDBC calls](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)** - MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB or Apache Derby DB.</span></span> <span data-ttu-id="d3a49-110">Les appels de « executeBatch » sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="d3a49-110">"executeBatch" calls are supported.</span></span> <span data-ttu-id="d3a49-111">Pour MySQL et PostgreSQL, si l’appel prend plus de 10 s, l’agent signale le plan de requête.</span><span class="sxs-lookup"><span data-stu-id="d3a49-111">For MySQL and PostgreSQL, if the call takes longer than 10s, the agent reports the query plan.</span></span>
* <span data-ttu-id="d3a49-112">**Exceptions interceptées** : données concernant les exceptions gérées par votre code.</span><span class="sxs-lookup"><span data-stu-id="d3a49-112">**Caught exceptions:** Data about exceptions that are handled by your code.</span></span>
* <span data-ttu-id="d3a49-113">**Temps d’exécution de la méthode** : données concernant le temps nécessaire pour exécuter des méthodes spécifiques.</span><span class="sxs-lookup"><span data-stu-id="d3a49-113">**Method execution time:** Data about the time it takes to execute specific methods.</span></span>

<span data-ttu-id="d3a49-114">Pour utiliser l’agent Java, installez-le sur votre serveur.</span><span class="sxs-lookup"><span data-stu-id="d3a49-114">To use the Java agent, you install it on your server.</span></span> <span data-ttu-id="d3a49-115">Vos applications web doivent être instrumentées à l’aide du [Kit de développement logiciel (SDK) Java Application Insights][java].</span><span class="sxs-lookup"><span data-stu-id="d3a49-115">Your web apps must be instrumented with the [Application Insights Java SDK][java].</span></span> 

## <a name="install-the-application-insights-agent-for-java"></a><span data-ttu-id="d3a49-116">Installer l’agent Application Insights pour Java</span><span class="sxs-lookup"><span data-stu-id="d3a49-116">Install the Application Insights agent for Java</span></span>
1. <span data-ttu-id="d3a49-117">[Téléchargez l'agent](https://aka.ms/aijavasdk) sur la machine exécutant votre serveur Java.</span><span class="sxs-lookup"><span data-stu-id="d3a49-117">On the machine running your Java server, [download the agent](https://aka.ms/aijavasdk).</span></span>
2. <span data-ttu-id="d3a49-118">Modifiez le script de démarrage du serveur d’applications et ajoutez la Machine virtuelle Java (JVM) suivante :</span><span class="sxs-lookup"><span data-stu-id="d3a49-118">Edit the application server startup script, and add the following JVM:</span></span>
   
    <span data-ttu-id="d3a49-119">`javaagent:`*chemin d’accès complet au fichier JAR de l’agent*</span><span class="sxs-lookup"><span data-stu-id="d3a49-119">`javaagent:`*full path to the agent JAR file*</span></span>
   
    <span data-ttu-id="d3a49-120">Par exemple, dans Tomcat sur une machine Linux :</span><span class="sxs-lookup"><span data-stu-id="d3a49-120">For example, in Tomcat on a Linux machine:</span></span>
   
    `export JAVA_OPTS="$JAVA_OPTS -javaagent:<full path to agent JAR file>"`
3. <span data-ttu-id="d3a49-121">Redémarrez votre serveur d’applications.</span><span class="sxs-lookup"><span data-stu-id="d3a49-121">Restart your application server.</span></span>

## <a name="configure-the-agent"></a><span data-ttu-id="d3a49-122">Configurer l’agent</span><span class="sxs-lookup"><span data-stu-id="d3a49-122">Configure the agent</span></span>
<span data-ttu-id="d3a49-123">Créez un fichier nommé `AI-Agent.xml` et placez-le dans le même dossier que le fichier JAR de l’agent.</span><span class="sxs-lookup"><span data-stu-id="d3a49-123">Create a file named `AI-Agent.xml` and place it in the same folder as the agent JAR file.</span></span>

<span data-ttu-id="d3a49-124">Définissez le contenu du fichier xml.</span><span class="sxs-lookup"><span data-stu-id="d3a49-124">Set the content of the xml file.</span></span> <span data-ttu-id="d3a49-125">Modifiez l’exemple suivant pour inclure ou omettre les fonctionnalités souhaitées.</span><span class="sxs-lookup"><span data-stu-id="d3a49-125">Edit the following example to include or omit the features you want.</span></span>

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

           <!-- Report on the particular signature
                void methodTwo(String, int) -->
           <Method name="methodTwo"
              reportExecutionTime="true"
              signature="(Ljava/lang/String;I)V" />
        </Class>

      </Instrumentation>
    </ApplicationInsightsAgent>

```

<span data-ttu-id="d3a49-126">Vous devez activer l’exception de rapports et le minutage pour les méthodes individuelles.</span><span class="sxs-lookup"><span data-stu-id="d3a49-126">You have to enable reports exception and method timing for individual methods.</span></span>

<span data-ttu-id="d3a49-127">Par défaut, `reportExecutionTime` est défini sur true, et `reportCaughtExceptions` sur false.</span><span class="sxs-lookup"><span data-stu-id="d3a49-127">By default, `reportExecutionTime` is true and `reportCaughtExceptions` is false.</span></span>

## <a name="view-the-data"></a><span data-ttu-id="d3a49-128">Visualiser les données</span><span class="sxs-lookup"><span data-stu-id="d3a49-128">View the data</span></span>
<span data-ttu-id="d3a49-129">Dans la ressource Application Insights, les temps d’exécution cumulés de la méthode et de la dépendance distante apparaissent [dans la vignette Performances][metrics].</span><span class="sxs-lookup"><span data-stu-id="d3a49-129">In the Application Insights resource, aggregated remote dependency and method execution times appears [under the Performance tile][metrics].</span></span>

<span data-ttu-id="d3a49-130">Pour rechercher des instances de dépendance et d’exception ainsi que des rapports de méthode, ouvrez [Rechercher][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="d3a49-130">To search for individual instances of dependency, exception, and method reports, open [Search][diagnostic].</span></span>

<span data-ttu-id="d3a49-131">[En savoir plus sur le diagnostic des problèmes de dépendance](app-insights-asp-net-dependencies.md#diagnosis).</span><span class="sxs-lookup"><span data-stu-id="d3a49-131">[Diagnosing dependency issues - learn more](app-insights-asp-net-dependencies.md#diagnosis).</span></span>

## <a name="questions-problems"></a><span data-ttu-id="d3a49-132">Des questions ?</span><span class="sxs-lookup"><span data-stu-id="d3a49-132">Questions?</span></span> <span data-ttu-id="d3a49-133">Des problèmes ?</span><span class="sxs-lookup"><span data-stu-id="d3a49-133">Problems?</span></span>
* <span data-ttu-id="d3a49-134">Pas de données ?</span><span class="sxs-lookup"><span data-stu-id="d3a49-134">No data?</span></span> [<span data-ttu-id="d3a49-135">Définir les exceptions de pare-feu</span><span class="sxs-lookup"><span data-stu-id="d3a49-135">Set firewall exceptions</span></span>](app-insights-ip-addresses.md)
* [<span data-ttu-id="d3a49-136">Résolution des problèmes Java</span><span class="sxs-lookup"><span data-stu-id="d3a49-136">Troubleshooting Java</span></span>](app-insights-java-troubleshoot.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
