---
title: "aaaApplication Insights pour Java web des applications qui sont déjà actives"
description: "Commencez à surveiller une application web qui est déjà en cours d’exécution sur votre serveur."
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 12f3dbb9-915f-4087-87c9-807286030b0b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/10/2016
ms.author: bwren
ms.openlocfilehash: 2b01cd61657522ccf1d2d97b2a29cdeb08ec9a18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-java-web-apps-that-are-already-live"></a>Application Insights pour les applications web qui sont déjà actives


Si vous avez une application web qui est déjà en cours d’exécution sur votre serveur J2EE, vous pouvez démarrer l’analyse avec [Application Insights](app-insights-overview.md) sans hello devez toomake aux modifications de code ou à recompiler votre projet. Avec cette option, vous obtenez des informations sur les requêtes HTTP envoyées tooyour serveur, les exceptions non gérées et les compteurs de performance.

Vous aurez besoin d’un abonnement trop[Microsoft Azure](https://azure.com).

> [!NOTE]
> procédure de Hello sur cette page ajoute hello SDK tooyour web application lors de l’exécution. Cette instrumentation du runtime est utile si vous ne souhaitez tooupdate ou régénérez votre code source. Mais si vous le pouvez, nous vous recommandons de vous [ajouter le code source de hello SDK toohello](app-insights-java-get-started.md) à la place. Qui vous donne davantage d’options telles que l’écriture d’activité de code tootrack utilisateur.
> 
> 

## <a name="1-get-an-application-insights-instrumentation-key"></a>1. Obtenir une clé d'instrumentation Application Insights
1. Connectez-vous à toohello [portail Microsoft Azure](https://portal.azure.com)
2. Créer une ressource Application Insights et définir l’application web de hello application type tooJava.
   
    ![Indiquez le nom, choisissez l’application web Java, puis cliquez sur Créer.](./media/app-insights-java-live/02-create.png)

    ressource de Hello est créée en quelques secondes.

4. Ouvrir la ressource hello et sa clé d’instrumentation. Vous devez toopaste cette clé dans votre projet de code dans quelques instants.
   
    ![Dans hello nouvelle ressource vue d’ensemble, cliquez sur Propriétés et copiez hello clé d’Instrumentation](./media/app-insights-java-live/03-key.png)

## <a name="2-download-hello-sdk"></a>2. Télécharger hello SDK
1. Télécharger hello [Application Insights SDK pour Java](https://aka.ms/aijavasdk). 
2. Sur votre serveur, extraire le répertoire de toohello hello du SDK du contenu à partir de laquelle les fichiers binaires du projet sont chargés. Si vous utilisez Tomcat, ce répertoire se trouve généralement sous `webapps/<your_app_name>/WEB-INF/lib`

Notez que vous devez toorepeat cela sur chaque instance de serveur et pour chaque application.

## <a name="3-add-an-application-insights-xml-file"></a>3. Ajouter un fichier xml Application Insights
Créer ApplicationInsights.xml dans le dossier hello dans lequel vous avez ajouté hello SDK. Y hello suivants XML.

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
* Corrélation des événements est un composant de requête Ajout toohello HTTP. Il attribue à une demande de tooeach identificateur reçue par le serveur de hello et ajoute cet identificateur en tant qu’un élément tooevery de propriété de télémétrie en tant que propriété de hello 'Operation.Id'. Il vous permet de télémétrie de hello toocorrelate associé à chaque requête en définissant un filtre dans [recherche diagnostic](app-insights-diagnostic-search.md).

## <a name="4-add-an-http-filter"></a>4. Ajouter un filtre HTTP
Recherchez et ouvrez le fichier de web.xml hello dans votre projet, puis hello fusion suivante extrait de code sous le nœud de l’application web hello, dans lequel les filtres d’application sont configurés.

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

## <a name="5-check-firewall-exceptions"></a>5. Vérifier les exceptions de pare-feu
Vous devrez peut-être trop[toosend les données sortantes de définir des exceptions](app-insights-ip-addresses.md).

## <a name="6-restart-your-web-app"></a>6. Redémarrer votre application web
## <a name="7-view-your-telemetry-in-application-insights"></a>7. Voir votre télémétrie dans Application Insights
Retourner la ressource Application Insights tooyour [portail Microsoft Azure](https://portal.azure.com).

Télémétrie sur les requêtes HTTP s’affiche sur le panneau de vue d’ensemble de hello. (Si elles n’y sont pas, attendez quelques secondes et cliquez sur Actualiser).

![Exemples de données](./media/app-insights-java-live/5-results.png)

Cliquez sur via n’importe quel toosee graphique plus des métriques. 

![](./media/app-insights-java-live/6-barchart.png)

Et lorsque vous affichez les propriétés hello d’une demande, vous pouvez voir les événements de télémétrie hello associés tels que les demandes et les exceptions.

![](./media/app-insights-java-live/7-instance.png)

[En savoir plus sur les mesures.](app-insights-metrics-explorer.md)

## <a name="next-steps"></a>Étapes suivantes
* [Ajouter des pages web télémétrie tooyour](app-insights-javascript.md) toomonitor page des vues et des mesures de l’utilisateur.
* [Configurer des tests web](app-insights-monitor-web-app-availability.md) toomake que votre application reste en direct et réactives.
* [Capture le suivi des journaux](app-insights-java-trace-logs.md)
* [Rechercher des événements et journaux](app-insights-diagnostic-search.md) toohelp diagnostiquer les problèmes.

