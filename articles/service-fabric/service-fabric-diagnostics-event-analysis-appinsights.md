---
title: "aaaAzure analyse des événements Service Fabric avec Application Insights | Documents Microsoft"
description: "Découvrez l’analyse et la visualisation d’événements à l’aide d’Application Insights pour la surveillance et le diagnostic de clusters Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/26/2017
ms.author: dekapur
ms.openlocfilehash: 59bb5a409f2951e5b2034049e782dd0da67f933c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="event-analysis-and-visualization-with-application-insights"></a>Analyse et visualisation d’événements avec Application Insights

Azure Application Insights est une plateforme extensible pour la surveillance et le diagnostic d’application. Elle inclut un puissant outil d’analyse et de requête, un tableau de bord et des visualisations personnalisables, ainsi que d’autres options incluant l’alerte automatisée. Il est hello recommandé de plateforme pour l’analyse et diagnostics pour les services et applications de Service Fabric.

## <a name="setting-up-application-insights"></a>Configuration d'Application Insights

### <a name="creating-an-ai-resource"></a>Création d’une ressource AI (Application Insights)

ressources de toocreate une AI principal sur toohello Azure Marketplace et recherchez « Application Insights ». Il doit s’afficher en tant que solution de première hello (il se trouve sous la catégorie « Mobile de + Web »). Cliquez sur **créer** lorsque vous examinez les ressources droite hello (Vérifiez que votre chemin d’accès correspond à l’image hello ci-dessous).

![Nouvelle ressource Application Insights](media/service-fabric-diagnostics-event-analysis-appinsights/create-new-ai-resource.png)

Vous devez toofill à certaines ressources de hello tooprovision informations correctement. Bonjour *Type d’Application* champ, utilisez « Application de web ASP.NET » si vous utilisez un de l’infrastructure de Service de modèles de programmation ou publication d’un cluster de toohello d’application .NET. Utilisez « Général » si vous souhaitez déployer des conteneurs et ses exécutables invités. En règle générale, par défaut toousing « Application de web ASP.NET » tookeep vos options ouvrent Bonjour futures. nom de Hello est en tooyour préférence, et groupe de ressources hello et abonnement sont modifiable après le déploiement de ressource de hello. Il est recommandé que votre ressource AI Bonjour même groupe de ressources que votre cluster. Si vous voulez obtenir des informations supplémentaires, consultez [Création d’une ressource Application Insights dans Azure](../application-insights/app-insights-create-new-resource.md).

Vous devez tooconfigure de clé d’Instrumentation AI hello AI avec votre outil d’agrégation d’événement. Une fois que votre ressource AI est défini (prend quelques minutes après le déploiement de hello est validé), accédez tooit et recherche hello **propriétés** section sur la barre de navigation gauche hello. Un nouveau panneau s’ouvre, affichant une *CLÉ D’INSTRUMENTATION*. Si vous avez besoin d’abonnement de hello toochange ou groupe de ressources de la ressource de hello, il est possible ici également.

### <a name="configuring-ai-with-wad"></a>Configuration de AI avec WAD

Il existe deux façons principales de données toosend de WAD tooAzure AI, qui sont obtenues en ajoutant une configuration de Diagnostics Windows AZURE AI récepteur toohello, comme détaillé dans [cet article](../monitoring-and-diagnostics/azure-diagnostics-configure-application-insights.md).

#### <a name="add-an-ai-instrumentation-key-when-creating-a-cluster-in-azure-portal"></a>Ajouter une clé d’instrumentation AI lors de la création d’un cluster dans le portail Azure

![Ajout d’une clé AIKey](media/service-fabric-diagnostics-event-analysis-appinsights/azure-enable-diagnostics.png)

Lorsque vous créez un cluster, si les Diagnostics est activée « On », un champ facultatif de tooenter une clé d’Instrumentation d’Application Insights affichera. Si vous collez votre IKey AI ici, récepteur de hello AI sera automatiquement configuré pour vous dans le modèle de gestionnaire de ressources hello toodeploy utilisé votre cluster.

#### <a name="add-hello-ai-sink-toohello-resource-manager-template"></a>Ajouter hello AI récepteur toohello Gestionnaire de ressources du modèle

Bonjour « WadCfg » du modèle de gestionnaire de ressources hello, ajoutez un « récepteur » en incluant hello deux modifications suivantes :

1. Ajouter la configuration du récepteur hello :

    ```json
    "SinksConfig": {
        "Sink": [
            {
                "name": "applicationInsights",
                "ApplicationInsights": "***ADD INSTRUMENTATION KEY HERE***"
            }
        ]
    }

    ```

2. Inclure hello récepteur Bonjour DiagnosticMonitorConfiguration en ajoutant des hello ligne dans « DiagnosticMonitorConfiguration » de hello « WadCfg » :

    ```json
    "sinks": "applicationInsights"
    ```

Dans les deux extraits de code hello ci-dessus, hello nom « applicationInsights » était récepteur de hello toodescribe utilisé. Cela n’est pas obligatoire, et tant que nom de hello du récepteur de hello est inclus dans les « récepteurs », vous pouvez définir la chaîne de nom de tooany hello.

Actuellement, les journaux de cluster de hello apparaît comme suivis dans la visionneuse du journal de AI. Étant donné que la plupart des traces hello en provenance de plateforme de hello est de niveau « Informations », vous pouvez également envisager la modification hello récepteur configuration tooonly envoi des journaux de type « Critique » ou « Erreur ». Cela est possible en ajoutant le récepteur de tooyour « Canaux », comme illustré dans [cet article](../monitoring-and-diagnostics/azure-diagnostics-configure-application-insights.md).

>[!NOTE]
>Si vous utilisez un IKey AI incorrect dans le portail ou dans votre modèle de gestionnaire de ressources, vous devez toomanually modifier la clé de hello / redéployer et mettre à jour hello cluster. 

### <a name="configuring-ai-with-eventflow"></a>Configuration de AI avec EventFlow

Si vous utilisez des événements de tooaggregate EventFlow, assurez-vous que tooimport hello `Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights`package NuGet. Hello suivant a toobe inclus dans hello *génère* section Hello *eventFlowConfig.json*:

```json
"outputs": [
    {
        "type": "ApplicationInsights",
        // (replace hello following value with your AI resource's instrumentation key)
        "instrumentationKey": "00000000-0000-0000-0000-000000000000"
    }
]
```

Apporter des modifications de hello requis toomake que dans vos filtres, ainsi qu’inclure d’autres entrées (ainsi que leurs packages NuGet respectifs).

## <a name="aisdk"></a>SDK AI (Application Insights)

Il est généralement recommandé toouse EventFlow et diagnostics Windows AZURE en tant que solutions d’agrégation, car elles permettent une toodiagnostics approche modulaire plus et d’analyse, par exemple, si vous souhaitez toochange votre sorties à partir de EventFlow, nécessite aucune modification de tooyour réel instrumentation, juste un fichier de configuration tooyour modification simple. Si, toutefois, vous décidez tooinvest à l’aide d’Application Insights ne sont pas susceptibles de toochange tooa autre plateforme, vous devez rechercher dans à l’aide nouveau SDK de AI pour agréger des événements et en les envoyant tooAI. Cela signifie que vous n’aurez plus tooconfigure EventFlow toosend tooAI de vos données, mais au lieu de cela installera le package de NuGet de l’infrastructure de Service de ApplicationInsight hello. Plus de détails sur le package de hello [ici](https://github.com/Microsoft/ApplicationInsights-ServiceFabric).

[Application Insights prennent en charge pour les conteneurs et Microservices](https://azure.microsoft.com/app-insights-microservices/) vous montre quelques hello nouvelles fonctionnalités qui sont en cours de traitement (toujours actuellement en version bêta), qui vous permettent toohave options de surveillance plus riches out of box avec AI. Celles-ci incluent le suivi des dépendances (utilisé dans la création d’un AppMap de tous vos services et applications dans un cluster et hello de communication entre eux) et une meilleure corrélation des suivis en provenance de vos services (permet de mieux localiser un problème dans hello flux de travail d’une application ou un service).

Si vous développez dans .NET et probablement à l’aide des modèles de programmation de Service Fabric et sont prêt toouse AI comme plate-forme pour visualiser et analyser les données de journaux et d’événements, il est recommandé que vous accédez via hello itinéraire AI SDK comme votre analyse et flux de travail de Diagnostics. Lecture [cela](../application-insights/app-insights-asp-net-more.md) et [cela](../application-insights/app-insights-asp-net-trace-logs.md) tooget main à l’aide de AI toocollect et afficher vos journaux.

## <a name="navigating-hello-ai-resource-in-azure-portal"></a>Navigation dans les ressources de AI hello dans le portail Azure

Une fois que vous avez configuré les AI comme sortie pour les événements et les journaux, informations devraient démarrer tooshow dans votre ressource AI dans quelques minutes. Accédez à la ressource AI toohello, qui prendra vous toohello AI ressources du tableau de bord. Cliquez sur **recherche** dans hello AI barre des tâches toosee hello dernières traces qu’il a reçus et toofilter en mesure de toobe via les.

*Metrics Explorer* est un outil utile pour la création de tableaux de bord personnalisés basés sur les indicateurs de performance que vos applications, vos services et votre cluster peuvent signaler. Consultez [exploration des mesures d’Application Insights](../application-insights/app-insights-metrics-explorer.md) tooset des graphiques quelques pour vous-même en fonction des données de hello vous collectez.

En cliquant sur **Analytique** vous conduira portail Application Insights Analytique de toohello, où vous pouvez rechercher des événements et des traces avec une plus grande portée et caractère facultatif. Vous pouvez en apprendre plus à ce sujet dans [Analytics dans Application Insights](../application-insights/app-insights-analytics.md).

## <a name="next-steps"></a>Étapes suivantes

* [Configurer des alertes dans AI](../application-insights/app-insights-alerts.md) toobe informé des changements apportés dans les performances ou d’utilisation
* [Active la détection dans Application Insights](../application-insights/app-insights-proactive-diagnostics.md) effectue une analyse proactive de télémétrie hello envoyé tooAI toowarn d’éventuels problèmes de performances
