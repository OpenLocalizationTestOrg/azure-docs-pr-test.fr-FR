---
title: aaaAzure Application Insights prennent en charge de plusieurs composants, microservices et conteneurs | Documents Microsoft
description: "Surveillance des performances et de l’utilisation des applications constituées de plusieurs composants ou de plusieurs rôles."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/17/2017
ms.author: bwren
ms.openlocfilehash: 6185eedf32ec450d7541603b94de6c3dcdf64a85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-multi-component-applications-with-application-insights-preview"></a>Surveiller des applications multicomposants avec Application Insights (préversion)

Vous pouvez surveiller des applications constituées de plusieurs composants serveurs, rôles ou services avec [Azure Application Insights](app-insights-overview.md). contrôle d’intégrité Hello des composants de hello et des relations hello entre eux sont affichés sur un seul mappage d’Application. Vous pouvez suivre des opérations individuelles à travers plusieurs composants avec une corrélation HTTP automatique. Vous pouvez intégrer et corréler les diagnostics des conteneurs à la télémétrie de l’application. Utiliser une seule ressource Application Insights pour tous les composants hello de votre application. 

![Plan d’application multicomposant](./media/app-insights-monitor-multi-role-apps/app-map.png)

Nous utilisons 'composant' toomean ici une partie de fonctionnement d’une application volumineuse. Par exemple, une application métier classique peut se composer de code client en cours d’exécution dans les navigateurs web, ils s’adressent tooone ou services de fin de plusieurs services d’application web, qui à leur tour utilisent précédent. Les composants de serveur peuvent être hébergé localement sur dans le cloud de hello, ou des rôles web et de travail Azure peuvent être ou peuvent s’exécuter dans des conteneurs tels que Docker ou Service Fabric. 

### <a name="sharing-a-single-application-insights-resource"></a>Partage d’une seule ressource Application Insights 

Hello technique clé ici est télémétrie toosend à partir de tous les composants de toohello de votre application même ressource Application Insights, mais utilisez hello `cloud_RoleName` composants de toodistinguish propriété lorsque cela est nécessaire. Hello Application Insights SDK ajoute hello `cloud_RoleName` émettre des composants de télémétrie toohello de propriété. Par exemple, hello Kit de développement logiciel ajoute un nom de site web, ou toohello de nom de rôle service `cloud_RoleName` propriété. Vous pouvez remplacer cette valeur par un telemetryinitializer. Hello mappage d’Application utilise hello `cloud_RoleName` composants de hello tooidentify de propriété sur la carte de hello.

Pour plus d’informations sur la façon de remplacer hello `cloud_RoleName` propriété Voir [ajouter des propriétés : ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).  

Dans certains cas, cela n’est peut-être pas approprié, et vous pouvez toouse des ressources distinctes pour différents groupes de composants. Par exemple, vous devrez peut-être toouse différentes ressources de la gestion ou à des fins de facturation. À l’aide des ressources distinctes signifie que vous ne voyez pas tous les composants hello affichées sur un seul mappage de l’Application ; et que vous ne peut pas interroger les composants dans [Analytique](app-insights-analytics.md). Vous avez également tooset des ressources distinctes de hello.

Avec cet inconvénient, nous supposons que dans le reste de hello de ce document que vous souhaitez toosend les données à partir de plusieurs composants tooone ressource Application Insights.

## <a name="configure-multi-component-applications"></a>Configurer des applications multicomposants

mappage d’une application à plusieurs composant tooget, vous devez tooachieve ces objectifs :

* **Installez la version préliminaire hello** package d’Application Insights dans chaque composant d’application hello. 
* **Partager une seule ressource Application Insights** pour tous les hello des composants de votre application.
* **Activer le mappage d’Application de plusieurs rôles** dans le panneau des aperçus hello.

Configurez chaque composant de votre application à l’aide de la méthode appropriée de hello pour son type. ([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md).)

### <a name="1-install-hello-latest-pre-release-package"></a>1. Installer le dernier package de version préliminaire hello

Mettre à jour ou installer des packages d’application Insights hello dans projet hello pour chaque composant de serveur. Si vous utilisez Visual Studio :

1. Cliquez avec le bouton droit sur un projet et sélectionnez **Gérer les packages NuGet**. 
2. Sélectionnez **Inclure la préversion**.
3. Si des packages Application Insights apparaissent dans les mises à jour, sélectionnez-les. 

    Sinon, recherchez et installez hello approprié :
    
    * Microsoft.ApplicationInsights.WindowsServer
    * Microsoft.ApplicationInsights.ServiceFabric : pour les composants s’exécutant en tant qu’exécutables invités et les conteneurs Docker s’exécutant dans une application Service Fabric
    * Microsoft.ApplicationInsights.ServiceFabric.Native : pour des services fiables dans les applications Service Fabric
    * Microsoft.ApplicationInsights.Kubernetes : pour les composants s’exécutant dans Docker sur Kubernetes

### <a name="2-share-a-single-application-insights-resource"></a>2. Partager une même ressource Application Insights

* Dans Visual Studio, cliquez avec le bouton droit sur un projet et sélectionnez **Configurer Application Insights** ou **Application Insights > Configurer**. Pour le premier projet de hello, utilisez hello Assistant toocreate une ressource Application Insights. Pour les projets suivants, sélectionnez hello même ressource.
* S’il n’existe aucun menu Application Insights, configurez-le manuellement :

   1. Dans [portail Azure](https://portal,azure.com), ouvrez la ressource d’Application Insights hello vous avez déjà créé pour un autre composant.
   2. Dans Panneau de vue d’ensemble de hello, onglet de hello ouvrir déroulante Essentials et hello de copie **clé d’Instrumentation.**
   3. Dans votre projet, ouvrez ApplicationInsights.config et insérez : `<InstrumentationKey>your copied key</InstrumentationKey>`

![Copier le fichier .config de hello instrumentation toohello clé](./media/app-insights-monitor-multi-role-apps/copy-instrumentation-key.png)


### <a name="3-enable-multi-role-application-map"></a>3. Activer Plan d’une application multirôle

Bonjour portail Azure, ouvrez la ressource hello pour votre application. Dans le panneau de versions préliminaires de hello, activez *mappage plusieurs rôles d’Application*.

### <a name="4-enable-docker-metrics-optional"></a>4. Activer les métriques Docker (facultatif) 

Si un composant s’exécute dans une Docker hébergée sur un ordinateur virtuel de Windows Azure, vous pouvez collecter des mesures supplémentaires à partir du conteneur de hello. Dans votre fichier de configuration [Azure Diagnostics](../monitoring-and-diagnostics/azure-diagnostics.md), insérez ceci :

```
"DiagnosticMonitorConfiguration": {
        ...
        "sinks": "applicationInsights",
        "DockerSources": {
                "Stats": {
                    "enabled": true,
                    "sampleRate": "PT1M"
                }
            },
        ...
    }
    ...   
    "SinksConfig": {
        "Sink": [{
            "name": "applicationInsights",
            "ApplicationInsights": "<your instrumentation key here>"
        }]
    }
    ...
}

```

## <a name="use-cloudrolename-tooseparate-components"></a>Utiliser des composants de tooseparate cloud_RoleName

Hello `cloud_RoleName` propriété est jointe tooall télémétrie. Il identifie le composant hello - rôle de hello ou un service - provenant des données de télémétrie hello. (Il est même ne Hello pas en tant que cloud_RoleInstance, qui sépare les rôles identiques qui sont exécutent en parallèle sur plusieurs ordinateurs ou les processus serveur).

Dans le portail hello, vous pouvez filtrer ou segment de votre télémétrie à l’aide de cette propriété. Dans cet exemple, le panneau de défaillances de hello est tooshow filtré simplement des informations du service web frontal de hello, filtrant des échecs de hello API CRM principal :

![Graphique des métriques segmentées par nom de rôle cloud](./media/app-insights-monitor-multi-role-apps/cloud-role-name.png)

## <a name="trace-operations-between-components"></a>Suivre les opérations entre les composants

Vous pouvez tracer à partir d’un composant tooanother, appels hello lors du traitement d’une opération individuelle.


![Afficher la télémétrie pour une opération](./media/app-insights-monitor-multi-role-apps/show-telemetry-for-operation.png)

Parcourez la liste corrélés de tooa de télémétrie pour cette opération sur le serveur web frontal de hello et API de serveur principal hello :

![Rechercher dans l’ensemble des composants](./media/app-insights-monitor-multi-role-apps/search-across-components.png)


## <a name="next-steps"></a>Étapes suivantes

* [Télémétrie distincte entre le développement, les tests et la production](app-insights-separate-resources.md)
