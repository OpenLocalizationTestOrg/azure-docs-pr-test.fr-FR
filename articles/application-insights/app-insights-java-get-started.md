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
# <a name="get-started-with-application-insights-in-a-java-web-project"></a>Prise en main d'Application Insights dans un projet web Java


[Application Insights](https://azure.microsoft.com/services/application-insights/) est un service analytique extensible pour les développeurs web qui vous permet de comprennent l’utilisation de votre application en temps réel et les performances de hello. Utilisez-le trop[détecter et diagnostiquer les problèmes de performances et exceptions](app-insights-detect-triage-diagnose.md), et [écrire du code] [ api] tootrack faire de ce que les utilisateurs avec votre application.

![Exemples de données](./media/app-insights-java-get-started/5-results.png)

Application Insights prend en charge les applications Java exécutées sur Linux, Unix ou Windows.

Ce dont vous avez besoin :

* Oracle JRE 1.6 ou version ultérieure ou Zoulou JRE 1.6 ou version ultérieure
* Un abonnement trop[Microsoft Azure](https://azure.microsoft.com/).

*Si vous avez une application web qui est déjà en ligne, pourrait procédure hello autre trop[ajouter hello SDK lors de l’exécution dans le serveur web de hello](app-insights-java-live.md). Cette solution permet d’éviter la reconstruction du code de hello, mais ne pas obtenir d’activités des utilisateurs tootrack hello option toowrite code.*

## <a name="1-get-an-application-insights-instrumentation-key"></a>1. Obtenir une clé d'instrumentation Application Insights
1. Connectez-vous à toohello [portail Microsoft Azure](https://portal.azure.com).
2. Créez une ressource Application Insights. Définissez des applications web tooJava hello application type.

    ![Indiquez le nom, choisissez l’application web Java, puis cliquez sur Créer.](./media/app-insights-java-get-started/02-create.png)
3. Trouver la clé d’instrumentation hello de ressource hello. Vous devez toopaste cette clé dans votre projet de code dans quelques instants.

    ![Dans hello nouvelle ressource vue d’ensemble, cliquez sur Propriétés et copiez hello clé d’Instrumentation](./media/app-insights-java-get-started/03-key.png)

## <a name="2-add-hello-application-insights-sdk-for-java-tooyour-project"></a>2. Ajouter hello Application Insights SDK pour le projet de tooyour Java
*Choisissez hello approprié pour votre projet.*

#### <a name="if-youre-using-eclipse-toocreate-a-maven-or-dynamic-web-project-"></a>Si vous utilisez Eclipse toocreate un projet Maven ou Web dynamique...
Hello d’utilisation [Application Insights SDK pour Java plug-in][eclipse].

#### <a name="if-youre-using-maven"></a>Si vous utilisez Maven...
Si votre projet est déjà configuré toouse Maven pour la build, fusion hello code tooyour pom.xml fichier suivant.

Ensuite, les fichiers binaires actualisation hello projet dépendances tooget hello téléchargé.

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

* *Des erreurs de validation de build ou de somme de contrôle ?* Essayez d’utiliser une version spécifique, telle que : `<version>1.0.n</version>`. Vous trouverez la version la plus récente hello Bonjour [notes de publication du Kit de développement logiciel](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) ou dans notre [les artefacts Maven](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights).
* *Devez tooupdate tooa nouveau SDK ?* Actualisez les dépendances de votre projet.

#### <a name="if-youre-using-gradle"></a>Si vous utilisez Gradle...
Si votre projet est déjà configuré toouse Gradle pour la build, du fichier build.gradle tooyour code fusion hello suivant.

Actualisation hello projet dépendances tooget hello binaires téléchargés.

```JSON

    repositories {
      mavenCentral()
    }

    dependencies {
      compile group: 'com.microsoft.azure', name: 'applicationinsights-web', version: '1.+'
      // or applicationinsights-core for bare API
    }
```

* *Erreurs de validation de build ou de somme de contrôle ? Essayez d’utiliser une version spécifique, telle que :* `version:'1.0.n'`. *Vous trouverez la version la plus récente hello Bonjour [notes de publication du Kit de développement logiciel](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).*
* *tooupdate tooa nouveau SDK*
  * Actualisez les dépendances de votre projet.

#### <a name="otherwise-"></a>Sinon...
Ajoutez manuellement hello SDK :

1. Télécharger hello [Application Insights SDK pour Java](https://aka.ms/aijavasdk).
2. Extraire les fichiers binaires de hello à partir du fichier zip de hello et ajoutez-les tooyour projet.

### <a name="questions"></a>Questions...
* *Quelle est la relation hello entre hello `-core` et `-web` composants dans le zip de hello ?*

  * `applicationinsights-core`permet de vous hello API système. Ce composant est toujours requis.
  * `applicationinsights-web` fournit des mesures qui permettent d’effectuer le suivi du nombre de requêtes HTTP et des temps de réponse. Vous pouvez omettre ce composant si vous ne souhaitez pas recueillir automatiquement ces données de télémétrie. Par exemple, si vous souhaitez toowrite votre propre.
* *tooupdate hello SDK lorsque nous publions des modifications*

  * Télécharger le dernier hello [Application Insights SDK pour Java](https://aka.ms/qqkaq6) et remplacer hello anciens.
  * Modifications sont décrites dans hello [notes de publication du Kit de développement logiciel](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).

## <a name="3-add-an-application-insights-xml-file"></a>3. Ajouter un fichier .xml Application Insights
Ajouter un dossier de ressources ApplicationInsights.xml toohello dans votre projet, ou assurez-vous que le chemin d’accès de classe de déploiement du projet tooyour est ajouté. Copiez hello XML suivant dans celui-ci.

Remplacer la clé d’instrumentation hello que vous avez obtenu hello portail Azure.

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


* clé d’instrumentation Hello est envoyé avec chaque élément de données de télémétrie et indique à Application Insights toodisplay dans votre ressource.
* Hello composant de requête HTTP est facultative. Il envoie automatiquement télémétrie concernant les requêtes et le portail de toohello de temps de réponse.
* Corrélation des événements est un composant de requête Ajout toohello HTTP. Il attribue à une demande de tooeach identificateur reçue par le serveur de hello et ajoute cet identificateur en tant qu’un élément tooevery de propriété de télémétrie en tant que propriété de hello 'Operation.Id'. Il vous permet de télémétrie de hello toocorrelate associé à chaque requête en définissant un filtre dans [recherche diagnostic][diagnostic].
* clé d’Application Insights Hello peut être passée dynamiquement hello portail Azure en tant que propriété par le système (-DAPPLICATION_INSIGHTS_IKEY = your_ikey). Si aucune propriété n’est définie, la variable d’environnement (APPLICATION_INSIGHTS_IKEY) est recherchée dans les paramètres d’application Azure. Si les deux propriétés hello ne sont pas définies, la valeur par défaut de hello InstrumentationKey est utilisée à partir de ApplicationInsights.xml. Cette séquence vous aide à toomanage InstrumentationKeys différents pour différents environnements dynamiquement.

### <a name="alternative-ways-tooset-hello-instrumentation-key"></a>Clé d’instrumentation d’autres méthodes tooset hello
Application Insights SDK recherche clé hello dans cet ordre :

1. Propriété système : -DAPPLICATION_INSIGHTS_IKEY=votre_ikey
2. Variable d’environnement : APPLICATION_INSIGHTS_IKEY
3. Fichier de configuration : ApplicationInsights.xml

Vous pouvez également [définir la clé dans le code](app-insights-api-custom-events-metrics.md#ikey):

```Java

    telemetryClient.InstrumentationKey = "...";
```

## <a name="4-add-an-http-filter"></a>4. Ajouter un filtre HTTP
dernière étape de configuration Hello permet hello HTTP demande composant toolog chaque demande web. (Non requis si vous voulez simplement les API système hello.)

Recherchez et ouvrez le fichier de web.xml hello dans votre projet, puis hello fusion suivant code sous le nœud de l’application web hello, dans lequel les filtres d’application sont configurés.

tooget hello les résultats plus précis, filtre de hello doivent être mappés avant tous les autres filtres.

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

#### <a name="if-youre-using-spring-web-mvc-31-or-later"></a>Si vous utilisez Spring Web MVC 3.1 ou une version ultérieure
Modifier ces éléments en *-package d’Application Insights servlet.xml tooinclude hello :

```XML

    <context:component-scan base-package=" com.springapp.mvc, com.microsoft.applicationinsights.web.spring"/>

    <mvc:interceptors>
        <mvc:interceptor>
            <mvc:mapping path="/**"/>
            <bean class="com.microsoft.applicationinsights.web.spring.RequestNameHandlerInterceptorAdapter" />
        </mvc:interceptor>
    </mvc:interceptors>
```

#### <a name="if-youre-using-struts-2"></a>Si vous utilisez Struts 2
Ajoutez ce fichier de configuration élément toohello Connections (généralement nommé struts.xml ou default.xml de Connections) :

```XML

     <interceptors>
       <interceptor name="ApplicationInsightsRequestNameInterceptor" class="com.microsoft.applicationinsights.web.struts.RequestNameInterceptor" />
     </interceptors>
     <default-interceptor-ref name="ApplicationInsightsRequestNameInterceptor" />
```

(Si vous avez des intercepteurs définis dans une pile par défaut, l’intercepteur de hello peut simplement être ajouté toothat pile.)

## <a name="5-run-your-application"></a>5. Exécuter votre application
Exécuter en mode débogage sur votre ordinateur de développement, ou tooyour serveur de publication.

## <a name="6-view-your-telemetry-in-application-insights"></a>6. Voir votre télémétrie dans Application Insights
Retourner la ressource Application Insights tooyour [portail Microsoft Azure](https://portal.azure.com).

Les données de demandes HTTP s’affiche sur le panneau de vue d’ensemble de hello. (Si elles n’y sont pas, attendez quelques secondes et cliquez sur Actualiser).

![Exemples de données](./media/app-insights-java-get-started/5-results.png)

[En savoir plus sur les mesures.][metrics]

Cliquez sur n’importe quel toosee graphique plu agrégées des métriques.

![](./media/app-insights-java-get-started/6-barchart.png)

> Application Insights suppose que le format de requêtes HTTP pour les applications MVC hello est : `VERB controller/action`. Par exemple, `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` et `GET Home/Product/sdf96vws` sont regroupés dans `GET Home/Product`. Ceci permet l’agrégation correcte des demandes, par exemple le nombre de demandes et le temps moyen d’exécution des demandes.
>
>

### <a name="instance-data"></a>Données d’instance
Cliquez sur une demande spécifique au type toosee des instances individuelles.

Deux types de données s’affichent dans Application Insights : des données agrégées, stockées et affichées sous forme de moyennes, de nombres et de sommes ; et les données d’instance : des rapports individuels des requêtes HTTP, des exceptions, les vues de page ou des événements personnalisés.

Lorsque vous affichez les propriétés hello d’une demande, vous pouvez voir les événements de télémétrie hello associés tels que les demandes et les exceptions.

![](./media/app-insights-java-get-started/7-instance.png)

### <a name="analytics-powerful-query-language"></a>Analytics : un puissant langage de requête
Comme vous accumulent des données, vous pouvez exécuter des requêtes instances tooaggregate toofind et de données individuelles.  [Analytics](app-insights-analytics.md) est un outil puissant qui permet non seulement de comprendre les performances et l’utilisation, mais également d’effectuer des diagnostics.

![Exemple d’Analytics](./media/app-insights-java-get-started/025.png)

## <a name="7-install-your-app-on-hello-server"></a>7. Installer votre application sur le serveur de hello
Maintenant publier le serveur de votre application toohello, permettent aux utilisateurs de l’utiliser et observer les données de télémétrie hello apparaissent dans le portail de hello.

* Assurez-vous que votre pare-feu autorise votre toosend application ports toothese de télémétrie :

  * dc.services.VisualStudio.com:443
  * f5.services.visualstudio.com:443

* Si le trafic sortant doit être acheminé via un pare-feu, définissez les propriétés système `http.proxyHost` et `http.proxyPort`.

* Sur les serveurs Windows, installez :

  * [Redistribuable Microsoft Visual C++](http://www.microsoft.com/download/details.aspx?id=40784)

    (Cette opération active les compteurs de performances.)


## <a name="exceptions-and-request-failures"></a>Exceptions et échecs de requêtes
Les exceptions non gérées sont collectées automatiquement :

![Ouvrez Paramètres, Défaillances.](./media/app-insights-java-get-started/21-exceptions.png)

toocollect des données sur les autres exceptions, vous avez deux options :

* [Insérer des appels dans votre code tootrackException()][apiexceptions].
* [Installez hello Agent Java sur votre serveur](app-insights-java-agent.md). Vous spécifiez des méthodes hello toowatch.

## <a name="monitor-method-calls-and-external-dependencies"></a>Surveiller les appels de méthode et les dépendances externes
[Installer hello Agent Java](app-insights-java-agent.md) toolog spécifié méthodes internes et les appels effectués via JDBC, avec des données de temporisation.

## <a name="performance-counters"></a>Compteurs de performances
Ouvrez **paramètres**, **serveurs**, toosee une plage de compteurs de performance.

![](./media/app-insights-java-get-started/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a>Personnaliser la collecte des compteurs de performances
collection de toodisable ensemble standard de hello des compteurs de performances, ajouter hello suivant code sous le nœud racine de hello du fichier de ApplicationInsights.xml hello :

```XML
    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a>Collecter des compteurs de performances supplémentaires
Vous pouvez spécifier toobe de compteurs de performances supplémentaires collectées.

#### <a name="jmx-counters-exposed-by-hello-java-virtual-machine"></a>Compteurs JMX (exposées par la Machine virtuelle Java de hello)

```XML
    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* `displayName`– nom hello affiché dans le portail d’Application Insights hello.
* `objectName`– nom de l’objet JMX hello.
* `attribute`: attribut hello de hello JMX objet nom toofetch
* `type`(facultatif) : hello du type d’attribut de l’objet JMX :
  * Par défaut : un type simple, comme int ou long.
  * `composite`: des données de compteur de performances hello sont au format hello de 'Attribute.Data'
  * `tabular`: des données de compteur de performances hello sont au format hello d’une ligne de table

#### <a name="windows-performance-counters"></a>Compteurs de performances Windows
Chaque [compteur de performances Windows](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) est un membre d’une catégorie (Bonjour même manière qu’un champ est un membre d’une classe). Les catégories peuvent être globales ou peuvent avoir des instances numérotées ou nommées.

```XML
    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* displayName : nom hello affiché dans le portail d’Application Insights hello.
* nom de la catégorie : catégorie de compteur de performances hello (objet de performance) à laquelle ce compteur de performance est associé.
* counterName – nom hello hello du compteur de performance.
* instanceName – nom hello de l’instance de catégorie de compteur de performance hello ou une chaîne vide (" »), si la catégorie de hello contient une seule instance. Si hello categoryName est le processus et compteur de performances hello vous aimeriez toocollect est à partir de processus de machine virtuelle Java hello actuel sur lequel votre application est en cours d’exécution, spécifiez `"__SELF__"`.

Les compteurs de performances sont visibles en tant que mesures personnalisées dans [Metrics Explorer][metrics].

![](./media/app-insights-java-get-started/12-custom-perfs.png)

### <a name="unix-performance-counters"></a>Compteurs de performances Unix
* [Installer collectd avec le plug-in de hello Application Insights](app-insights-java-collectd.md) tooget une grande variété de données système et réseau.

## <a name="get-user-and-session-data"></a>Obtenir des données utilisateur et de session
Vous envoyez des données de télémétrie depuis votre serveur web. Maintenant tooget hello vue 360 degrés de votre application, vous pouvez ajouter plus de surveillance :

* [Ajouter des pages web télémétrie tooyour] [ usage] toomonitor page des vues et des mesures de l’utilisateur.
* [Configurer des tests web] [ availability] toomake que votre application reste en direct et réactives.

## <a name="capture-log-traces"></a>Capture le suivi des journaux
Vous pouvez utiliser Application Insights tooslice et manipulent des journaux à partir d’autres infrastructures de journalisation Log4J ou Logback. Vous pouvez corréler les journaux hello avec les requêtes HTTP et d’autres données de télémétrie. [Découvrez comment][javalogs].

## <a name="send-your-own-telemetry"></a>Envoyer votre propre télémétrie
Maintenant que vous avez installé le Kit de développement logiciel de hello, vous pouvez utiliser vos propres données de télémétrie hello API toosend.

* [Effectuer le suivi des événements et métriques personnalisés] [ api] toolearn ce que les utilisateurs font avec votre application.
* [Rechercher des événements et journaux] [ diagnostic] toohelp diagnostiquer les problèmes.

## <a name="availability-web-tests"></a>Tests web de disponibilité
Application Insights peuvent tester votre site Web à intervalles réguliers toocheck que c’est et répond bien. [tooset des][availability], cliquez sur les tests Web.

![Cliquez sur Tests web, puis sur Ajouter un test web](./media/app-insights-java-get-started/31-config-web-test.png)

Vous obtenez des graphiques du temps de réponse, ainsi que des notifications par courrier électronique si votre site ne fonctionne plus.

![Exemple de test web](./media/app-insights-java-get-started/appinsights-10webtestresult.png)

[En savoir plus sur les tests de disponibilité web.][availability]

## <a name="questions-problems"></a>Des questions ? Des problèmes ?
[Résolution des problèmes Java](app-insights-java-troubleshoot.md)

## <a name="video"></a>Vidéo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Étapes suivantes
* [Surveillance des appels de dépendance](app-insights-java-agent.md)
* [Surveillance des compteurs de performances Unix](app-insights-java-collectd.md)
* Ajouter [analyse les pages web tooyour](app-insights-javascript.md) chargement de la page toomonitor délai d’attente, les appels AJAX, les exceptions de navigateur.
* Écrire [une télémétrie personnalisée](app-insights-api-custom-events-metrics.md) tootrack utilisation dans le navigateur de hello ou sur le serveur de hello.
* Créer [tableaux de bord](app-insights-dashboards.md) graphiques des clés toobring hello ensemble pour l’analyse de votre système.
* Utilisez [Analytics](app-insights-analytics.md) pour des requêtes puissantes sur les données de télémétrie de votre application
* Pour plus d’informations, consultez [Azure pour les développeurs Java](/java/azure).

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#trackexception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[usage]: app-insights-javascript.md
