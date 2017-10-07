---
title: "aaaService Gestionnaire de ressources de Cluster de l’ensemble fibre optique - groupes d’applications | Documents Microsoft"
description: "Vue d’ensemble de fonctionnalités de groupe d’applications dans le Gestionnaire de ressources du Cluster Service Fabric de hello de hello"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 4cae2370-77b3-49ce-bf40-030400c4260d
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: b4f068862d962b53a0b3ea813b89bb13ee395681
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooapplication-groups"></a>Introduction tooApplication groupes
Gestionnaire de ressources de Cluster du service Fabric gère en général des ressources de cluster en répartissant la charge de hello (représenté par [métriques](service-fabric-cluster-resource-manager-metrics.md)) uniformément dans l’ensemble de cluster de hello. L’infrastructure de service gère la capacité hello des nœuds hello hello et hello clusters dans sa globalité via [capacité](service-fabric-cluster-resource-manager-cluster-description.md). Les mesures et la capacité sont idéales pour divers types de charges de travail, mais les modèles qui utilisent beaucoup d’instances d’application Service Fabric différentes imposent parfois des conditions supplémentaires. Par exemple, vous pouvez :

- Réservation de capacité sur les nœuds hello dans un cluster de hello pour les services de hello dans certaines instances de l’application nommée
- Limiter le nombre total de hello de nœuds services hello dans une instance de l’application nommée exécutent (au lieu de les répartir les sur l’intégralité du cluster hello)
- Définir des capacités sur l’instance d’application nommée hello lui-même nombre de hello de toolimit services ou le nombre total de consommation des ressources des services hello qu’il contient

toomeet ces exigences, hello Gestionnaire de ressources du Cluster Service Fabric prend en charge une fonctionnalité appelée groupes d’applications.

## <a name="limiting-hello-maximum-number-of-nodes"></a>Hello le nombre maximal de nœuds
cas d’utilisation la plus simple Hello pour la capacité de l’Application est lorsqu’une instance d’application doit toobe limitée tooa certain nombre maximal de nœuds. Cela consolide tous les services au sein de cette instance d’application sur un nombre défini d’ordinateurs. Consolidation est utile lorsque vous essayez de toopredict ou imposer l’utilisation des ressources physiques par les services au sein de cette instance de l’application nommée hello. 

Hello image suivante montre une instance d’application avec et sans un nombre maximal de nœuds définis :

<center>
![Instance d’application définissant le nombre maximal de nœuds][Image1]
</center>

Dans l’exemple de gauche hello, application hello n’a pas un nombre maximal de nœuds définis, et il a trois services. Hello, Gestionnaire de ressources du Cluster a distribuées tous les réplicas sur six nœuds disponibles tooachieve hello meilleur équilibre dans le cluster hello (comportement par défaut de hello). Dans l’exemple de droite hello, nous constatons hello même application limitée toothree nœuds.

paramètre Hello qui contrôle ce comportement est appelé MaximumNodes. Ce paramètre peut être défini lors de la création de l’application, ou mis à jour pour une instance d’application qui était déjà en cours d’exécution.

PowerShell

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MaximumNodes 3
Update-ServiceFabricApplication –Name fabric:/AppName –MaximumNodes 5
```

C#

``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";
ad.MaximumNodes = 3;
await fc.ApplicationManager.CreateApplicationAsync(ad);

ApplicationUpdateDescription adUpdate = new ApplicationUpdateDescription(new Uri("fabric:/AppName"));
adUpdate.MaximumNodes = 5;
await fc.ApplicationManager.UpdateApplicationAsync(adUpdate);

```

Dans le jeu de nœuds de hello, hello Gestionnaire de ressources de Cluster ne garantit pas placés ensemble les objets de service ou les nœuds obtient utilisés.

## <a name="application-metrics-load-and-capacity"></a>Mesures, charge et capacité d’application
Groupes d’applications vous permettent également les métriques de toodefine associées à une instance d’application nommé donné et la capacité de cette instance de l’application de ces mesures. Mesures de l’application vous permettent de tootrack, réserver et limite la consommation des ressources hello de services hello à l’intérieur de cette instance d’application.

Pour chaque mesure d’application, il existe deux valeurs qui peuvent être définies :

- **Nombre total de capacité de l’Application** : ce paramètre représente la capacité totale de hello d’application hello pour une mesure particulière. Hello, Gestionnaire de ressources de Cluster n’autorise pas la création de hello de nouveaux services au sein de cette instance d’application qui provoquerait tooexceed de la charge totale de cette valeur. Par exemple, supposons qu’instance de l’application hello avait une capacité de 10 et bénéficie déjà d’un chargement de cinq. Création de Hello d’un service avec une charge de total par défaut de 10 est pas autorisée.
- **Capacité maximale de nœud** – ce paramètre spécifie la charge totale maximale de hello pour une application hello sur un nœud unique. Si la charge dépasse cette capacité, hello Gestionnaire de ressources de Cluster déplace les nœuds tooother de réplicas afin que hello charge diminue.


PowerShell :

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -Metrics @("MetricName:Metric1,MaximumNodeCapacity:100,MaximumApplicationCapacity:1000")
```

C# :

``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";

var appMetric = new ApplicationMetricDescription();
appMetric.Name = "Metric1";
appMetric.TotalApplicationCapacity = 1000;
appMetric.MaximumNodeCapacity = 100;
ad.Metrics.Add(appMetric);
await fc.ApplicationManager.CreateApplicationAsync(ad);
```

## <a name="reserving-capacity"></a>Capacité réservée
Une autre utilisation courante pour les groupes d’applications est tooensure que les ressources au sein de hello cluster sont réservés pour une instance d’une application donnée. Hello espace est toujours réservé lors de la création d’instance de l’application hello.

Réservation d’espace dans le cluster de hello pour application hello se produit immédiatement, même lorsque :
- instance de l’application Hello est créée mais n’avez pas encore tous les services qu’il contient
- nombre de Hello de services au sein de l’instance de l’application hello change chaque fois 
- services de Hello existent mais ne sont pas consomment des ressources de hello 

La réservation de ressources pour une instance d’application implique de spécifier deux paramètres supplémentaires : *MinimumNodes* et *NodeReservationCapacity*

- **MinimumNodes** -définit le nombre minimal de hello de nœuds hello application instance doit être exécutée.  
- **NodeReservationCapacity** -ce paramètre est défini par la mesure de l’application hello. valeur de Hello est hello cette métrique réservée à l’application hello sur n’importe quel nœud où hello services dans cette application à exécuter.

Combinaison de **MinimumNodes** et **NodeReservationCapacity** garantit une réservation d’une charge minimale pour une application hello au sein du cluster de hello. S’il existe moins restant capacité Bonjour de cluster que réservation total de hello requis, la création d’une application hello échoue. 

Voyons un exemple de réservation de capacité :

<center>
![Instances d’application définissant la capacité de réserve][Image2]
</center>

Dans l’exemple de gauche hello, les applications n’ont pas de toute capacité de l’Application définie. tous les éléments selon les règles toonormal équilibre la Hello Gestionnaire de ressources du Cluster.

Dans l’exemple hello sur hello droite, disons que Application1 a été créé avec hello suivant les paramètres :

- MinimumNodes ensemble tootwo
- Une mesure d’application définie avec
  - NodeReservationCapacity sur 20

PowerShell

 ``` posh
 New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MinimumNodes 2 -Metrics @("MetricName:Metric1,NodeReservationCapacity:20")
 ```

C#

 ``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";
ad.MinimumNodes = 2;

var appMetric = new ApplicationMetricDescription();
appMetric.Name = "Metric1";
appMetric.NodeReservationCapacity = 20;

ad.Metrics.Add(appMetric);

await fc.ApplicationManager.CreateApplicationAsync(ad);
```

Service Fabric réserves de ressources de capacité sur les deux nœuds pour Application1 et n’autorise pas les services à partir de l’Application2 tooconsume cette capacité même si il n’y a qu'aucun charge n’est consommée par les services hello Application1 au moment de hello. Cette capacité réservée d’application est considérée comme consommé et déduit du nombre de hello capacité sur ce nœud et dans le cluster de hello restante.  réservation de Hello est déduite hello restant immédiatement de la capacité de cluster, mais hello réservé consommation est déduite de capacité hello d’un nœud spécifique uniquement lorsque l’objet d’au moins un service est placé sur celui-ci. Cette dernière réservation permet plus de flexibilité et une meilleure utilisation des ressources dans la mesure où les ressources sont réservées uniquement sur des nœuds lorsque cela est nécessaire.

## <a name="obtaining-hello-application-load-information"></a>Obtention des informations de charge de l’application hello
Pour chaque application qui a une capacité de l’Application définie pour une ou plusieurs mesures, vous pouvez obtenir des informations de hello sur la charge globale de hello signalé par les réplicas de ses services.

PowerShell :

``` posh
Get-ServiceFabricApplicationLoad –ApplicationName fabric:/MyApplication1
```

C#

``` csharp
var v = await fc.QueryManager.GetApplicationLoadInformationAsync("fabric:/MyApplication1");
var metrics = v.ApplicationLoadMetricInformation;
foreach (ApplicationLoadMetricInformation metric in metrics)
{
    Console.WriteLine(metric.ApplicationCapacity);  //total capacity for this metric in this application instance
    Console.WriteLine(metric.ReservationCapacity);  //reserved capacity for this metric in this application instance
    Console.WriteLine(metric.ApplicationLoad);  //current load for this metric in this application instance
}
```

requête de ApplicationLoad Hello retourne des informations de base de hello sur la capacité d’Application qui a été spécifié pour l’application hello. Ces informations comprennent des informations sur les nœuds de valeur minimale et maximale hello et le numéro de hello application hello est actuellement occupée par. Elles comprennent également des informations sur chaque mesure de charge d’application, notamment :

* : Métrique nom de métrique de hello.
* Capacité de réservation : La capacité de Cluster qui est réservée dans le cluster de hello pour cette Application.
* Charge de l’application : la charge totale des réplicas enfants de cette application.
* Capacité d’application : la valeur maximale autorisée pour la charge de l’application.

## <a name="removing-application-capacity"></a>Suppression de la capacité d’application
Une fois les paramètres de capacité de l’Application hello définies pour une application, ils peuvent être supprimés à l’aide des API d’Application de mise à jour ou des cmdlets PowerShell. Par exemple :

``` posh
Update-ServiceFabricApplication –Name fabric:/MyApplication1 –RemoveApplicationCapacity

```

Cette commande supprime tous les paramètres de gestion de capacité Application à partir de l’instance de l’application hello. Cela inclut MinimumNodes, MaximumNodes et les mesures de l’Application hello, le cas échéant. effet Hello de commande hello est immédiate. Une fois cette commande terminée, hello Gestionnaire de ressources de Cluster utilise le comportement de par défaut hello pour la gestion des applications. Les paramètres de capacité d’application peuvent être spécifiés à nouveau via `Update-ServiceFabricApplication`/`System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()`.

### <a name="restrictions-on-application-capacity"></a>Restrictions sur la capacité d’application
Il existe plusieurs restrictions à respecter concernant les paramètres de capacité d’application. En cas d’erreurs de validation, aucune modification n’est appliquée.

- Tous les paramètres entiers doivent être des nombres positifs.
- La valeur du paramètre MinimumNodes ne doit jamais être supérieure à celle du paramètre MaximumNodes.
- Si les capacités d’une mesure de charge sont définies, elles doivent respecter les règles suivantes :
  - La capacité de réservation de nœud ne doit pas être supérieure à la capacité maximale de nœud. Par exemple, vous ne peut pas limiter la capacité de hello pour métrique hello « UC » sur des unités de tootwo nœud hello et essayez tooreserve trois unités sur chaque nœud.
  - Si MaximumNodes est spécifié, produit hello de MaximumNodes et la capacité maximale de nœud ne doit pas être supérieure à la capacité de l’Application. Par exemple, supposons hello capacité maximale de nœud pour la métrique de charge « UC » a la valeur tooeight. Supposons également que vous définissez hello too10 de nœuds au Maximum. Dans ce cas, la capacité totale de l’application doit être supérieure à 80 pour cette mesure de charge.

restrictions de Hello sont appliquées à la fois au cours des mises à jour et la création d’application.

## <a name="how-not-toouse-application-capacity"></a>Comment pas toouse capacité de l’Application
- N’essayez pas de toouse hello groupe d’applications fonctionnalités tooconstrain hello application tooa _spécifique_ sous-ensemble de nœuds. En d’autres termes, vous pouvez spécifier que l’application hello s’exécute au maximum cinq nœuds, mais pas les cinq nœuds spécifiques dans un cluster de hello. Contraint un toospecific application nœuds peuvent être obtenus à l’aide des contraintes de placement des services.
- N’essayez pas de tooensure de capacité de l’Application hello toouse que deux services de hello même application sont placés sur hello mêmes nœuds. Utilisez plutôt l’[affinité](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md) ou les [contraintes de placement](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints).

## <a name="next-steps"></a>Étapes suivantes
- Pour plus d’informations sur la configuration des services, consultez la rubrique [En savoir plus sur la configuration des services](service-fabric-cluster-resource-manager-configure-services.md)
- toofind out sur comment hello Gestionnaire de ressources de Cluster gère et équilibre la charge du cluster de hello, consultez l’article de hello sur [équilibrage de charge](service-fabric-cluster-resource-manager-balancing.md)
- Démarrer à partir du début de hello et [obtenir une présentation de toohello Gestionnaire de ressources du Cluster Service Fabric](service-fabric-cluster-resource-manager-introduction.md)
- Pour plus d’informations sur le fonctionnement des mesures en général, consultez les informations sur les [mesures de charge Service Fabric](service-fabric-cluster-resource-manager-metrics.md)
- Hello, Gestionnaire de ressources du Cluster possède de nombreuses options permettant de décrire le cluster de hello. toofind plus d’informations à leur sujet, consultez cet article sur [décrivant un cluster Service Fabric](service-fabric-cluster-resource-manager-cluster-description.md)

[Image1]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-max-nodes.png
[Image2]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-reserved-capacity.png
