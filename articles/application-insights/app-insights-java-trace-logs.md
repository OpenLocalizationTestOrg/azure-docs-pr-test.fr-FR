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
# <a name="explore-java-trace-logs-in-application-insights"></a>Exploration du suivi des journaux Java dans Application Insights
Si vous utilisez Logback ou Log4J (version 1.2 ou version 2.0) pour le suivi, vous pouvez avoir vos journaux de trace envoyés automatiquement tooApplication Insights où vous pouvez Explorer et effectuer des recherches.

## <a name="install-hello-java-sdk"></a>Installer hello Kit de développement logiciel Java

Installez le [kit de développement logiciel (SDK) Application Insights pour Java][java], si ce n’est pas déjà fait.

(Si vous ne souhaitez pas les demandes tootrack HTTP, vous pouvez omettre la majeure partie du fichier de configuration .xml hello, mais vous devez inclure au moins hello `InstrumentationKey` élément. Vous devez également appeler `new TelemetryClient()` tooinitialize hello SDK.)


## <a name="add-logging-libraries-tooyour-project"></a>Ajouter un projet de tooyour de bibliothèques de journalisation
*Choisissez hello approprié pour votre projet.*

#### <a name="if-youre-using-maven"></a>Si vous utilisez Maven...
Si votre projet est déjà configuré toouse Maven pour la build, un des hello suivant des extraits de code dans votre fichier pom.xml de fusion.

Puis actualiser les dépendances du projet hello, les binaires de hello tooget téléchargés.

*Logback*

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-logback</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

*Log4J v2.0*

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

*Log4J v1.2*

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j1_2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

#### <a name="if-youre-using-gradle"></a>Si vous utilisez Gradle...
Si votre projet est déjà configuré toouse Gradle pour la build, ajoutez l’un des hello suivant lignes toohello `dependencies` groupe dans votre fichier build.gradle :

Puis actualiser les dépendances du projet hello, les binaires de hello tooget téléchargés.

**Logback**

```

    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-logback', version: '1.0.+'
```

**Log4J v2.0**

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j2', version: '1.0.+'
```

**Log4J v1.2**

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j1_2', version: '1.0.+'
```

#### <a name="otherwise-"></a>Sinon...
Télécharger et extraire appender approprié de hello, puis ajouter un projet de tooyour hello bibliothèque appropriée :

| Enregistreur | Télécharger | Bibliothèque |
| --- | --- | --- |
| Logback |[Kit de développement logiciel (SDK) avec appender Logback](https://aka.ms/xt62a4) |applicationinsights-logging-logback |
| Log4J v2.0 |[Kit de développement logiciel (SDK) avec appender Log4J v2](https://aka.ms/qypznq) |applicationinsights-logging-log4j2 |
| Log4J v1.2 |[Kit de développement logiciel (SDK) avec appender Log4J v1.2](https://aka.ms/ky9cbo) |applicationinsights-logging-log4j1_2 |

## <a name="add-hello-appender-tooyour-logging-framework"></a>Ajouter l’infrastructure de journalisation de tooyour appender hello
toostart mise en route de traces, fusion hello extrait de code toohello Log4J ou Logback les fichier de configuration : 

*Logback*

```XML

    <appender name="aiAppender" 
      class="com.microsoft.applicationinsights.logback.ApplicationInsightsAppender">
    </appender>
    <root level="trace">
      <appender-ref ref="aiAppender" />
    </root>
```

*Log4J v2.0*

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

*Log4J v1.2*

```XML

    <appender name="aiAppender" 
         class="com.microsoft.applicationinsights.log4j.v1_2.ApplicationInsightsAppender">
    </appender>
    <root>
      <priority value ="trace" />
      <appender-ref ref="aiAppender" />
    </root>
```

appenders d’Application Insights Hello peuvent être référencées par n’importe quel journal configuré et pas nécessairement par l’enregistreur d’événements de hello racine (comme indiqué dans les exemples de code hello ci-dessus).

## <a name="explore-your-traces-in-hello-application-insights-portal"></a>Explorer vos traces dans le portail Application Insights de hello
Maintenant que vous avez configuré votre toosend projet effectue le suivi tooApplication Insights, vous pouvez afficher et rechercher ces suivis dans hello du portail Application Insights hello [recherche] [ diagnostic] panneau.

![Dans le portail Application Insights hello, ouvrir la recherche](./media/app-insights-java-trace-logs/10-diagnostics.png)

## <a name="next-steps"></a>Étapes suivantes
[Recherche de diagnostic][diagnostic]

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md


