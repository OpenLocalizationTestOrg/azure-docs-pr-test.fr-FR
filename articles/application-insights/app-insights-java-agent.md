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
# <a name="monitor-dependencies-exceptions-and-execution-times-in-java-web-apps"></a>Surveiller les dépendances, les exceptions et les temps d’exécution dans les applications web Java


Si vous avez [instrumenter votre application de web Java avec Application Insights][java], vous pouvez utiliser hello Agent Java tooget des informations plus détaillées, sans aucune modification du code :

* **Dépendances :** données sur les appels que votre application effectue des composants tooother, y compris :
  * **Appels REST** passés via HttpClient, OkHttp et RestTemplate (Spring).
  * **Redis** appels effectués via le client Jedis hello. Si l’appel de hello prend plu de 10 s, l’agent de hello extrait également les arguments de l’appel hello.
  * **[Appels JDBC](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)** : base de données MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB ou Apache Derby. Les appels de « executeBatch » sont pris en charge. MySQL et PostgreSQL, si l’appel de hello prend plu de 10 s, l’agent de hello indique plan de requête hello.
* **Exceptions interceptées** : données concernant les exceptions gérées par votre code.
* **Durée d’exécution de méthode :** données sur hello fois qu’il prend tooexecute des méthodes spécifiques.

l’agent de toouse hello Java, vous installez sur votre serveur. Vos applications web doivent être instrumentées avec hello [Application Insights Java SDK][java]. 

## <a name="install-hello-application-insights-agent-for-java"></a>Installer l’agent d’Application Insights hello pour Java
1. Sur l’ordinateur de hello exécute votre serveur Java, [télécharger l’agent de hello](https://aka.ms/aijavasdk).
2. Modifier le script de démarrage de server application hello et ajoutez hello suivant JVM :
   
    `javaagent:`*fichier JAR de chemin d’accès complet toohello agent*
   
    Par exemple, dans Tomcat sur une machine Linux :
   
    `export JAVA_OPTS="$JAVA_OPTS -javaagent:<full path tooagent JAR file>"`
3. Redémarrez votre serveur d’applications.

## <a name="configure-hello-agent"></a>Configurer l’agent de hello
Créez un fichier nommé `AI-Agent.xml` et placez-le dans hello même dossier que le fichier JAR de l’agent hello.

Définir le contenu du fichier xml de hello hello. Modifier hello suivant exemple tooinclude ou omettre des fonctionnalités hello que vous souhaitez.

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

Vous avez tooenable rapports exception et le minutage de méthode pour les méthodes individuelles.

Par défaut, `reportExecutionTime` est défini sur true, et `reportCaughtExceptions` sur false.

## <a name="view-hello-data"></a>Afficher les données hello
Bonjour ressource Application Insights, agrégées temps d’exécution dépendance et la méthode à distance apparaît [sous hello performances vignette][metrics].

toosearch pour des instances de rapports de dépendance, d’exception et de méthode, ouvrez [recherche][diagnostic].

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
