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
# <a name="monitor-dependencies-exceptions-and-execution-times-in-java-web-apps"></a>Surveiller les dépendances, les exceptions et les temps d’exécution dans les applications web Java


Si vous avez [instrumenté votre application web Java avec Application Insights][java], vous pouvez utiliser l’agent Java pour obtenir des informations plus détaillées, sans pour autant modifier le code :

* **Dépendances :** données sur les appels passés par votre application à destination d’autres composants, dont :
  * **Appels REST** passés via HttpClient, OkHttp et RestTemplate (Spring).
  * **Redis** passés via le client Jedis. Si l’appel prend plus de 10 s, l’agent récupère également les arguments d’appel.
  * **[Appels JDBC](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)** : base de données MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB ou Apache Derby. Les appels de « executeBatch » sont pris en charge. Pour MySQL et PostgreSQL, si l’appel prend plus de 10 s, l’agent signale le plan de requête.
* **Exceptions interceptées** : données concernant les exceptions gérées par votre code.
* **Temps d’exécution de la méthode** : données concernant le temps nécessaire pour exécuter des méthodes spécifiques.

Pour utiliser l’agent Java, installez-le sur votre serveur. Vos applications web doivent être instrumentées à l’aide du [Kit de développement logiciel (SDK) Java Application Insights][java]. 

## <a name="install-the-application-insights-agent-for-java"></a>Installer l’agent Application Insights pour Java
1. [Téléchargez l'agent](https://aka.ms/aijavasdk) sur la machine exécutant votre serveur Java.
2. Modifiez le script de démarrage du serveur d’applications et ajoutez la Machine virtuelle Java (JVM) suivante :
   
    `javaagent:`*chemin d’accès complet au fichier JAR de l’agent*
   
    Par exemple, dans Tomcat sur une machine Linux :
   
    `export JAVA_OPTS="$JAVA_OPTS -javaagent:<full path to agent JAR file>"`
3. Redémarrez votre serveur d’applications.

## <a name="configure-the-agent"></a>Configurer l’agent
Créez un fichier nommé `AI-Agent.xml` et placez-le dans le même dossier que le fichier JAR de l’agent.

Définissez le contenu du fichier xml. Modifiez l’exemple suivant pour inclure ou omettre les fonctionnalités souhaitées.

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

Vous devez activer l’exception de rapports et le minutage pour les méthodes individuelles.

Par défaut, `reportExecutionTime` est défini sur true, et `reportCaughtExceptions` sur false.

## <a name="view-the-data"></a>Visualiser les données
Dans la ressource Application Insights, les temps d’exécution cumulés de la méthode et de la dépendance distante apparaissent [dans la vignette Performances][metrics].

Pour rechercher des instances de dépendance et d’exception ainsi que des rapports de méthode, ouvrez [Rechercher][diagnostic].

[En savoir plus sur le diagnostic des problèmes de dépendance](app-insights-asp-net-dependencies.md#diagnosis).

## <a name="questions-problems"></a>Des questions ? Des problèmes ?
* Pas de données ? [Définir les exceptions de pare-feu](app-insights-ip-addresses.md)
* [Résolution des problèmes Java](app-insights-java-troubleshoot.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
