---
title: aaaGet en main Azure Application Insights avec Java dans Eclipse | Documents Microsoft
description: "Utilisez hello performances de tooadd plug-in Eclipse et l’utilisation de la surveillance tooyour Java avec Application Insights"
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: e88c9f53-cd90-4abc-b097-1f170937908e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/12/2016
ms.author: bwren
ms.openlocfilehash: 3142a26a9e2d14c2c433882e3d337f2a8c8f2247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-insights-with-java-in-eclipse"></a>Prise en main d’Application Insights avec Java dans Eclipse
Hello Application Insights SDK envoie les données de télémétrie à partir de votre application web Java afin que vous pouvez analyser les performances et l’utilisation. Hello Eclipse plug-in pour Application Insights installe automatiquement hello SDK dans votre projet afin que vous obtenez la télémétrie de zone hello, ainsi qu’une API que vous pouvez utiliser les données de télémétrie personnalisées toowrite.   

## <a name="prerequisites"></a>Composants requis
Plug-in de hello travaille actuellement pour les projets Maven et des projets Web dynamique dans Eclipse.
([Types de tooother ajouter Application Insights de projet Java][java].)

Vous devez disposer des éléments suivants :

* Oracle JRE 1.6 ou version ultérieure
* Un abonnement trop[Microsoft Azure](https://azure.microsoft.com/).
* [IDE Eclipse pour développeurs Java EE](http://www.eclipse.org/downloads/), Indigo ou version ultérieure.
* Windows 7 ou version ultérieure ou Windows Server 2008 ou version ultérieure

## <a name="install-hello-sdk-on-eclipse-one-time"></a>Installer hello SDK sur Eclipse (une fois)
Vous ne devez toodo une seule fois par ordinateur. Cette étape installe un kit de ressources qui peut ajouter puis hello SDK tooeach projet Web dynamique.

1. Dans Eclipse, cliquez sur Aide, Installer un nouveau logiciel.

    ![Aide, installation de nouveaux logiciels](./media/app-insights-java-eclipse/0-plugin.png)
2. Hello SDK est http://dl.microsoft.com/eclipse, dans la boîte à outils Azure.
3. Désactivez l’option **Contacter tous les sites de mise à jour...**

    ![Pour le Kit de développement logiciel (SDK) Application Insights, désactivez Contacter tous les sites de mise à jour.](./media/app-insights-java-eclipse/1-plugin.png)

Suivez hello restant comme suit pour chaque projet Java.

## <a name="create-an-application-insights-resource-in-azure"></a>Créer une ressource Application Insights dans Azure
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Créez une ressource Application Insights. Définissez des applications web tooJava hello application type.  

    ![Cliquez sur + et choisissez Ajouter Application Insights.](./media/app-insights-java-eclipse/01-create.png)  

4. Trouver la clé d’instrumentation hello de ressource hello. Vous en aurez besoin toopaste dans votre projet de code dans quelques instants.  

    ![Dans hello nouvelle ressource vue d’ensemble, cliquez sur Propriétés et copiez hello clé d’Instrumentation](./media/app-insights-java-eclipse/03-key.png)  

## <a name="add-application-insights-tooyour-project"></a>Ajouter Application Insights tooyour projet
1. Ajouter Application Insights à partir du menu contextuel de hello du projet web Java.

    ![Dans hello nouvelle ressource vue d’ensemble, cliquez sur Propriétés et copiez hello clé d’Instrumentation](./media/app-insights-java-eclipse/02-context-menu.png)
2. Collez la clé d’instrumentation hello que vous avez obtenu hello portail Azure.

    ![Dans hello nouvelle ressource vue d’ensemble, cliquez sur Propriétés et copiez hello clé d’Instrumentation](./media/app-insights-java-eclipse/03-ikey.png)

clé de Hello est envoyé avec chaque élément de données de télémétrie et indique à Application Insights toodisplay dans votre ressource.

## <a name="run-hello-application-and-see-metrics"></a>Exécutez l’application hello et voir les métriques
Exécutez votre application.

Retourner la ressource d’Application Insights tooyour dans Microsoft Azure.

Les données de demandes HTTP seront affiche sur le panneau de vue d’ensemble de hello. (Si elles n’y sont pas, attendez quelques secondes et cliquez sur Actualiser).

![Réponse du serveur, nombre de demandes et échecs ](./media/app-insights-java-eclipse/5-results.png)

Cliquez sur via n’importe quel toosee graphique plus des métriques.

![Nombres de demandes par nom](./media/app-insights-java-eclipse/6-barchart.png)

[En savoir plus sur les mesures.][metrics]

Et lorsque vous affichez les propriétés hello d’une demande, vous pouvez voir les événements de télémétrie hello associés tels que les demandes et les exceptions.

![Tous le suivi pour cette demande](./media/app-insights-java-eclipse/7-instance.png)

## <a name="client-side-telemetry"></a>Télémétrie côté client
À partir du Panneau de démarrage rapide de hello, cliquez sur Get code toomonitor Mes pages web :

![Sur votre Panneau de vue d’ensemble des applications, sélectionnez Démarrage rapide, obtenir code toomonitor Mes pages web. Copiez le script de hello.](./media/app-insights-java-eclipse/02-monitor-web-page.png)

Insérer l’extrait de code hello dans head hello de vos fichiers HTML.

#### <a name="view-client-side-data"></a>Affichage des données côté client
Ouvrez et utilisez vos pages web mises à jour. Attendez une ou deux minutes, puis retourner tooApplication Insights et panneau de l’utilisation de hello ouvert. (À partir du Panneau de vue d’ensemble de hello, faites défiler la liste et cliquez sur l’utilisation).

Mesures de session, utilisateur et afficher la page seront affiche sur le panneau de l’utilisation de hello :

![Sessions, utilisateurs et affichages de pages](./media/app-insights-java-eclipse/appinsights-47usage-2.png)

[En savoir plus sur la configuration de la télémétrie côté client.][usage]

## <a name="publish-your-application"></a>Publication de votre application
Maintenant publier le serveur de votre application toohello, permettent aux utilisateurs de l’utiliser et observer les données de télémétrie hello apparaissent dans le portail de hello.

* Assurez-vous que votre pare-feu autorise votre toosend application ports toothese de télémétrie :

  * dc.services.VisualStudio.com:443
  * dc.services.visualstudio.com:80
  * f5.services.visualstudio.com:443
  * f5.services.visualstudio.com:80
* Sur les serveurs Windows, installez :

  * [Redistribuable Microsoft Visual C++](http://www.microsoft.com/download/details.aspx?id=40784)

    (Cette opération active les compteurs de performances.)

## <a name="exceptions-and-request-failures"></a>Exceptions et échecs de requêtes
Les exceptions non gérées sont collectées automatiquement :

![](./media/app-insights-java-eclipse/21-exceptions.png)

toocollect des données sur les autres exceptions, vous avez deux options :

* [Insérer des appels tooTrackException dans votre code](app-insights-api-custom-events-metrics.md#trackexception).
* [Installez hello Agent Java sur votre serveur](app-insights-java-agent.md). Vous spécifiez des méthodes hello toowatch.

## <a name="monitor-method-calls-and-external-dependencies"></a>Surveiller les appels de méthode et les dépendances externes
[Installer hello Agent Java](app-insights-java-agent.md) toolog spécifié méthodes internes et les appels effectués via JDBC, avec des données de temporisation.

## <a name="performance-counters"></a>Compteurs de performances
Dans votre Panneau de vue d’ensemble, défiler et cliquez sur hello **serveurs** vignette. Vous verrez un ensemble de compteurs de performances.

![Faites défiler la liste en mosaïque de serveurs tooclick hello](./media/app-insights-java-eclipse/11-perf-counters.png)

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

![](./media/app-insights-java-eclipse/12-custom-perfs.png)

### <a name="unix-performance-counters"></a>Compteurs de performances Unix
* [Installer collectd avec le plug-in de hello Application Insights](app-insights-java-collectd.md) tooget une grande variété de données système et réseau.

## <a name="availability-web-tests"></a>Tests web de disponibilité
Application Insights peuvent tester votre site Web à intervalles réguliers toocheck que c’est et répond bien. [tooset des][availability], faites défiler vers le bas tooclick disponibilité.

![Faites défiler vers le bas, cliquez sur Disponibilité, puis sur Ajouter un test web](./media/app-insights-java-eclipse/31-config-web-test.png)

Vous obtenez des graphiques du temps de réponse, ainsi que des notifications par courrier électronique si votre site ne fonctionne plus.

![Exemple de test web](./media/app-insights-java-eclipse/appinsights-10webtestresult.png)

[En savoir plus sur les tests de disponibilité web.][availability]

## <a name="diagnostic-logs"></a>Journaux de diagnostic
Si vous utilisez Logback ou Log4J (version 1.2 ou version 2.0) pour le suivi, vous pouvez avoir vos journaux de trace envoyés automatiquement tooApplication Insights où vous pouvez Explorer et effectuer des recherches.

[En savoir plus sur les journaux de diagnostic][javalogs]

## <a name="custom-telemetry"></a>Télémétrie personnalisée
Insérer quelques lignes de code dans votre toofind d’application web Java à ce que les utilisateurs sont en servent ou toohelp diagnostiquer des problèmes.

Vous pouvez insérer le code JavaScript des pages web et hello côté serveur Java.

[En savoir plus sur la télémétrie personnalisée][track]

## <a name="next-steps"></a>Étapes suivantes
#### <a name="detect-and-diagnose-issues"></a>Détecter et diagnostiquer les problèmes
* [Ajouter des données de télémétrie de client web] [ usage] tooget télémétrie des performances à partir du client web de hello.
* [Configurer des tests web] [ availability] toomake que votre application reste en direct et réactives.
* [Rechercher des événements et journaux] [ diagnostic] toohelp diagnostiquer les problèmes.
* [Capturez le suivi Log4J ou Logback][javalogs]

#### <a name="track-usage"></a>Suivi de l'utilisation
* [Ajouter des données de télémétrie de client web] [ usage] toomonitor page des vues et des mesures de l’utilisateur de base.
* [Effectuer le suivi des événements et métriques personnalisés](app-insights-web-track-usage.md) toolearn sur la façon dont votre application est utilisée, à la fois au client de hello et le serveur de hello.

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md
