---
title: "entités aaaHow tooview Azure Service Fabric agrégé d’intégrité | Documents Microsoft"
description: "Décrit comment tooquery, lecture et l’évaluation d’intégrité agrégé des entités Azure Service Fabric, par le biais de requêtes d’intégrité et des requêtes générales."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: fa34c52d-3a74-4b90-b045-ad67afa43fe5
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: oanapl
ms.openlocfilehash: add810551cac26d2b4ff81b57d94ddd780c2cc2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="view-service-fabric-health-reports"></a>Affichage rapports d’intégrité de Service Fabric
Azure Service Fabric propose un [modèle d’intégrité](service-fabric-health-introduction.md) avec des entités d’intégrité sur lesquelles les composants système et les agents de surveillance peuvent signaler les conditions locales qu’ils surveillent. Hello [magasin de contrôle d’intégrité](service-fabric-health-introduction.md#health-store) regroupe tous les toodetermine de données de contrôle d’intégrité si les entités sont intègres.

cluster de Hello est automatiquement remplie avec les rapports d’intégrité envoyés par les composants du système hello. En savoir plus sur [tootroubleshoot des rapports d’intégrité du système utilisez](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).

Service Fabric fournit plusieurs façons tooget hello agrégé d’intégrité des entités de hello :

* [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) ou d’autres outils de visualisation
* Requêtes d’intégrité (via PowerShell, API ou REST)
* Général requêtes qui retournent une liste des entités qui ont le contrôle d’intégrité en tant qu’une des propriétés hello (via PowerShell, API ou REST)

toodemonstrate ces options, nous allons utiliser un cluster local avec cinq nœuds et hello [fabric : / WordCount application](http://aka.ms/servicefabric-wordcountapp). Hello **fabric : / WordCount** application contient deux services par défaut, un service avec état de type `WordCountServiceType`et un service sans état du type `WordCountWebServiceType`. J’ai modifié hello `ApplicationManifest.xml` toorequire sept des réplicas de cibles pour un service avec état hello et une partition. Étant donné que cinq nœuds de cluster de hello, composants du système hello signalent un avertissement sur la partition de service hello, car il est sous le nombre de cibles hello.

```xml
<Service Name="WordCountService">
<<<<<<< HEAD
    <StatefulService ServiceTypeName="WordCountServiceType" TargetReplicaSetSize="7" MinReplicaSetSize="3">
      <UniformInt64Partition PartitionCount="1" LowKey="1" HighKey="26" />
    </StatefulService>
=======
  <StatefulService ServiceTypeName="WordCountServiceType" TargetReplicaSetSize="7" MinReplicaSetSize="2">
    <UniformInt64Partition PartitionCount="[WordCountService_PartitionCount]" LowKey="1" HighKey="26" />
  </StatefulService>
>>>>>>> 5e84dbdd8e45a5d6b36f435a550b7433b873bf11
</Service>
```

## <a name="health-in-service-fabric-explorer"></a>Intégrité dans Service Fabric Explorer
Service Fabric Explorer fournit un affichage visuel du cluster de hello. Dans l’image hello ci-dessous, vous pouvez voir que :

* Hello application **fabric : / WordCount** est rouge (erreur), car il possède un événement d’erreur signalé par **MyWatchdog** pour la propriété de hello **disponibilité**.
* L’un de ses services, **fabric:/WordCount/WordCountService** apparaît en jaune (avertissement). service de Hello est configuré avec des sept réplicas et cluster de hello a cinq nœuds, deux repicas ne peut pas être placés. Bien que cela n’est pas indiqué ici, partition de service hello est jaune en raison d’un rapport du système à partir de `System.FM` indiquant que `Partition is below target replica or instance count`. déclencheurs de partition jaune Hello hello service jaune.
* cluster de Hello est rouge en raison de l’application hello rouge.

évaluation de Hello utilise des stratégies par défaut de manifeste du cluster hello et manifeste d’application. Il s’agit de stratégies strictes qui ne tolèrent aucun échec.

Affichage du cluster Service Fabric Explorer hello :

![Affichage du cluster Service Fabric Explorer hello.][1]

[1]: ./media/service-fabric-view-entities-aggregated-health/servicefabric-explorer-cluster-health.png


> [!NOTE]
> En savoir plus sur [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).
>
>

## <a name="health-queries"></a>Requêtes d'intégrité
L’infrastructure de service expose les requêtes d’intégrité pour chacun des hello pris en charge [types d’entités](service-fabric-health-introduction.md#health-entities-and-hierarchy). Ils sont accessibles via hello API, à l’aide des méthodes sur [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), applets de commande PowerShell et REST. Ces requêtes retournent entièrement l’intégrité des informations sur l’entité de hello : hello agrégé de l’état d’intégrité, événements de contrôle d’intégrité d’entité, les États d’intégrité enfant (le cas échéant), évaluations non intègres (lorsque l’entité de hello n’est pas intègre) et les statistiques d’intégrité enfants (lorsque applicable).

> [!NOTE]
> Une entité de contrôle d’intégrité est retournée s’il est entièrement rempli dans le magasin de contrôle d’intégrité hello. entité de Hello doit être active (ne pas supprimé) et disposez d’un rapport du système. Ses entités parent sur la chaîne de hiérarchie hello doivent également avoir des rapports sur le système. Si une de ces conditions ne sont pas satisfaite, le contrôle d’intégrité hello requêtes retournent un [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) avec [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` qui montre pourquoi les entités hello ne sont pas renvoyée.
>
>

requêtes d’intégrité de Hello doivent passer dans un identificateur d’entité hello, qui varie selon le type d’entité hello. les requêtes Hello acceptent des paramètres de stratégie d’intégrité facultatifs. Si aucune stratégie de contrôle d’intégrité n’est spécifiés, hello [stratégies d’intégrité](service-fabric-health-introduction.md#health-policies) à partir du manifeste de cluster ou une application hello sont utilisées pour l’évaluation. Si les manifestes hello ne contiennent pas de définition pour les stratégies d’intégrité, les stratégies de contrôle d’intégrité par défaut hello sont utilisées pour l’évaluation. stratégies de contrôle d’intégrité par défaut Hello ne tolèrent pas les échecs. les requêtes de Hello acceptent également des filtres pour retourner uniquement les enfants partielles ou événements--hello ceux qui respectent hello filtres spécifiés. Un autre filtre permet à l’exclusion des statistiques de hello enfants.

> [!NOTE]
> filtres de sortie Hello sont appliquées côté serveur de hello, taille de la réponse message hello est réduit. Il est recommandé d’utiliser des filtres de sortie hello toolimit hello données retournent, plutôt qu’appliquent des filtres côté client de hello.
>
>

Les données d’intégrité d’une entité incluent les éléments suivants :

* Bonjour état d’intégrité agrégé de l’entité de hello. Calculée par le magasin de contrôle d’intégrité hello basé sur les rapports d’intégrité d’entité, telles que les États d’intégrité enfant (le cas échéant) et stratégies d’intégrité. En savoir plus sur l’ [évaluation de l’intégrité de l’entité](service-fabric-health-introduction.md#health-evaluation).  
* événements de contrôle d’intégrité Hello sur l’entité de hello.
* collection de Hello des États d’intégrité de tous les enfants pour les entités hello qui peuvent avoir des enfants. les États d’intégrité Hello contiennent les identificateurs d’entité et hello état d’intégrité agrégé. tooget entièrement l’intégrité pour un enfant, appeler un contrôle d’intégrité de la requête hello pour le type d’entité enfant hello et transmettez identificateur enfant de hello.
* les évaluations non intègres Hello toohello de ce point de rapport qui a déclenché état hello d’entité de hello, si l’entité de hello n’est pas intègre. les évaluations de Hello sont récursifs, contenant les évaluations d’intégrité hello enfants qui a déclenché l’état d’intégrité actuel. Par exemple, un agent de surveillance a signalé une erreur sur un réplica. intégrité des applications Hello montre une évaluation défectueuse en raison de service non intègre de tooan ; service de Hello est défectueux en raison de la partition tooa erreur ; partition de Hello est défectueux en raison de réplica tooa erreur ; réplica de Hello est défectueux en raison de l’état d’intégrité toohello surveillance erreur.
* statistiques de contrôle d’intégrité Hello pour tous les types enfants d’entités hello qui ont des enfants. Par exemple, l’intégrité du cluster affiche hello le nombre total d’applications, services, partitions, les réplicas et déployé des entités dans un cluster de hello. L’intégrité du service indique le nombre total de hello de partitions et réplicas sous hello de service spécifié.

## <a name="get-cluster-health"></a>Obtenir les données d’intégrité du cluster
Retourne hello d’intégrité de l’entité de cluster hello et contient les États d’intégrité hello d’applications et les nœuds (enfants de cluster de hello). Entrée :

* Stratégie de contrôle d’intégrité du cluster hello [facultatif] utilisé des nœuds de hello tooevaluate et les événements de cluster hello.
* Mappage de stratégie d’intégrité [facultatif] hello application, avec des stratégies de contrôle d’intégrité hello utilisé stratégies manifeste d’application hello toooverride.
* [Facultatif] Les filtres des événements, les nœuds et les applications qui spécifient les entrées sont dignes d’intérêt et doivent être retournés dans le résultat de hello (par exemple, uniquement, les erreurs ou avertissements et erreurs). Tous les événements, les nœuds et les applications sont utilisées tooevaluate hello entité agrégée contrôle d’intégrité, quel que soit le filtre de hello.
* [Facultatif] Filtrer les statistiques d’intégrité tooexclude.
* [Facultatif] Filtrer l’ensemble fibre optique tooinclude : / statistiques d’intégrité système dans hello statistiques d’intégrité. Applicable uniquement lorsque les statistiques d’intégrité hello ne sont pas exclus. Par défaut, les statistiques d’intégrité hello incluent uniquement les statistiques pour les applications utilisateur et application du système de hello pas.

### <a name="api"></a>API
tooget d’intégrité de cluster, créez un `FabricClient` et appel hello [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) méthode sur son **HealthManager**.

Hello appel suivant reçoit l’intégrité du cluster hello :

```csharp
ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync();
```

Bonjour de code suivant obtient l’intégrité du cluster hello en utilisant une stratégie de contrôle d’intégrité de cluster personnalisé et les filtres pour les nœuds et les applications. Il spécifie que les statistiques d’intégrité hello incluent l’ensemble fibre optique hello : / statistiques du système. Il crée [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), qui contient des informations d’entrée de hello.

```csharp
var policy = new ClusterHealthPolicy()
{
    MaxPercentUnhealthyNodes = 20
};
var nodesFilter = new NodeHealthStatesFilter()
{
    HealthStateFilterValue = HealthStateFilter.Error | HealthStateFilter.Warning
};
var applicationsFilter = new ApplicationHealthStatesFilter()
{
    HealthStateFilterValue = HealthStateFilter.Error
};
var healthStatisticsFilter = new ClusterHealthStatisticsFilter()
{
    ExcludeHealthStatistics = false,
    IncludeSystemApplicationHealthStatistics = true
};
var queryDescription = new ClusterHealthQueryDescription()
{
    HealthPolicy = policy,
    ApplicationsFilter = applicationsFilter,
    NodesFilter = nodesFilter,
    HealthStatisticsFilter = healthStatisticsFilter
};

ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
intégrité de cluster hello Hello applet de commande tooget [Get-ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth). Tout d’abord, connectez toohello cluster à l’aide de hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) applet de commande.

Hello état du cluster de hello est cinq nœuds, l’application système hello et fabric : / WordCount configurée comme décrit.

Hello suivant l’applet de commande Obtient l’intégrité du cluster à l’aide de stratégies de contrôle d’intégrité par défaut. Hello état d’intégrité agrégé est un avertissement, car l’ensemble fibre optique de hello : WordCount application est avertissement. Notez comment les évaluations non intègres hello fournissent des détails sur les conditions de hello qui a déclenché la santé hello agrégée.

```xml
PS D:\ServiceFabric> Get-ServiceFabricClusterHealth


AggregatedHealthState   : Warning
UnhealthyEvaluations    : 
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.
                          
                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Warning'.
                          
                            Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                          
                            Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.
                          
                                Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                          
                                Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                          
                                    Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                          
                          
NodeHealthStates        : 
                          NodeName              : _Node_4
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_3
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_2
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_1
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_0
                          AggregatedHealthState : Ok
                          
ApplicationHealthStates : 
                          ApplicationName       : fabric:/System
                          AggregatedHealthState : Ok
                          
                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Warning
                          
HealthEvents            : None
HealthStatistics        : 
                          Node                  : 5 Ok, 0 Warning, 0 Error
                          Replica               : 6 Ok, 0 Warning, 0 Error
                          Partition             : 1 Ok, 1 Warning, 0 Error
                          Service               : 1 Ok, 1 Warning, 0 Error
                          DeployedServicePackage : 6 Ok, 0 Warning, 0 Error
                          DeployedApplication   : 5 Ok, 0 Warning, 0 Error
                          Application           : 0 Ok, 1 Warning, 0 Error
```

Hello applet de commande PowerShell suivante obtient hello état d’intégrité du cluster de hello en utilisant une stratégie d’application personnalisée. Il filtre les résultats tooget seules les applications et les nœuds d’erreur ou un avertissement. En conséquence, aucun nœud n’est renvoyé puisqu’ils sont tous sains. Uniquement hello fabric : / WordCount application respecte le filtre d’applications hello. Étant donné que la stratégie personnalisée de hello spécifie tooconsider avertissements comme des erreurs pour l’ensemble fibre optique hello : / application WordCount, application hello est évaluée comme erronée, et est donc de cluster de hello.

```powershell
PS D:\ServiceFabric> $appHealthPolicy = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicy
$appHealthPolicy.ConsiderWarningAsError = $true
$appHealthPolicyMap = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicyMap
$appUri1 = New-Object -TypeName System.Uri -ArgumentList "fabric:/WordCount"
$appHealthPolicyMap.Add($appUri1, $appHealthPolicy)
Get-ServiceFabricClusterHealth -ApplicationHealthPolicyMap $appHealthPolicyMap -ApplicationsFilter "Warning,Error" -NodesFilter "Warning,Error" -ExcludeHealthStatistics


AggregatedHealthState   : Error
UnhealthyEvaluations    : 
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.
                          
                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Error'.
                          
                            Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                          
                            Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                          
                                Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                          
                                Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                          
                                    Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=true.
                          
                          
NodeHealthStates        : None
ApplicationHealthStates : 
                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Error
                          
HealthEvents            : None
```

### <a name="rest"></a>REST
Vous pouvez obtenir l’intégrité du cluster avec un [demande GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) ou un [demande POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) qui inclut les stratégies de contrôle d’intégrité décrits dans le corps de hello.

## <a name="get-node-health"></a>Obtenir les données d’intégrité du nœud
Retourne hello d’intégrité d’une entité de nœud et contient des événements de contrôle d’intégrité hello signalés sur le nœud de hello. Entrée :

* Nom du nœud hello [obligatoire] qui identifie le nœud de hello.
* Paramètres de stratégie de contrôle d’intégrité de cluster [facultatif] hello utilisé tooevaluate intégrité.
* [Facultatif] Filtres pour les événements qui indiquent les entrées sont dignes d’intérêt et doivent être retournés dans le résultat de hello (par exemple, uniquement, les erreurs ou avertissements et erreurs). Tous les événements sont utilisés tooevaluate hello entité agrégée contrôle d’intégrité, quel que soit le filtre de hello.

### <a name="api"></a>API
contrôle d’intégrité de nœud tooget via hello API, créez un `FabricClient` et appel hello [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) méthode sur son HealthManager.

Hello de code suivant obtient d’intégrité de nœud hello pour le nom du nœud spécifié hello :

```csharp
NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(nodeName);
```

Hello de code suivant obtient le contrôle d’intégrité de nœud hello pour hello spécifié de nom de nœud et passe dans le filtre d’événements et de stratégie personnalisée à l’aide [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):

```csharp
var queryDescription = new NodeHealthQueryDescription(nodeName)
{
    HealthPolicy = new ClusterHealthPolicy() {  ConsiderWarningAsError = true },
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.Warning },
};

NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
intégrité de nœud hello Hello applet de commande tooget [Get-ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth). Tout d’abord, connectez toohello cluster à l’aide de hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) applet de commande.
Hello suivant l’applet de commande Obtient le contrôle d’intégrité de nœud hello à l’aide de stratégies de contrôle d’intégrité par défaut :

```powershell
PS D:\ServiceFabric> Get-ServiceFabricNodeHealth _Node_1


NodeName              : _Node_1
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 3
                        SentAt                : 7/13/2017 4:39:23 PM
                        ReceivedAt            : 7/13/2017 4:40:47 PM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 4:40:47 PM, LastWarning = 1/1/0001 12:00:00 AM
```

Hello applet de commande suivante obtient hello état d’intégrité de tous les nœuds de cluster de hello :

```powershell
PS D:\ServiceFabric> Get-ServiceFabricNode | Get-ServiceFabricNodeHealth | select NodeName, AggregatedHealthState | ft -AutoSize

NodeName AggregatedHealthState
-------- ---------------------
_Node_4                     Ok
_Node_3                     Ok
_Node_2                     Ok
_Node_1                     Ok
_Node_0                     Ok
```

### <a name="rest"></a>REST
Vous pouvez obtenir l’intégrité du nœud avec un [demande GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) ou un [demande POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) qui inclut les stratégies de contrôle d’intégrité décrits dans le corps de hello.

## <a name="get-application-health"></a>Obtenir les données d’intégrité des applications
Hello retourne l’intégrité d’une entité de l’application. Il contient les États d’intégrité de hello de l’application hello déployé et les enfants de service. Entrée :

* Hello [obligatoire] nom de l’application (URI) qui identifie l’application hello.
* Stratégie de contrôle d’intégrité d’application hello [facultatif] utilisé des stratégies de manifeste d’application toooverride hello.
* [Facultatif] Les filtres des événements, les services et les applications déployées, spécifient les entrées sont dignes d’intérêt et doivent être retournés dans le résultat de hello (par exemple, uniquement, les erreurs ou avertissements et erreurs). Tous les événements, les services et les applications déployées sont l’intégrité de l’entité agrégée d’hello tooevaluate utilisé, quel que soit le filtre de hello.
* [Facultatif] Filtrer les statistiques d’intégrité tooexclude hello. Si non spécifié, les statistiques d’intégrité hello incluent OK de hello, d’avertissement et nombre d’erreurs pour tous les enfants de l’application : services, partitions, les réplicas, des applications déployées et déployé des packages de service.

### <a name="api"></a>API
intégrité d’application tooget, créer un `FabricClient` et appel hello [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) méthode sur son HealthManager.

Hello de code suivant obtient l’intégrité d’applications hello pour le nom d’application spécifié hello (URI) :

```csharp
ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(applicationName);
```

Hello de code suivant obtient l’intégrité d’applications hello pour le nom d’application spécifié hello (URI), avec des filtres et des stratégies personnalisées spécifié via [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).

```csharp
HealthStateFilter warningAndErrors = HealthStateFilter.Error | HealthStateFilter.Warning;
var serviceTypePolicy = new ServiceTypeHealthPolicy()
{
    MaxPercentUnhealthyPartitionsPerService = 0,
    MaxPercentUnhealthyReplicasPerPartition = 5,
    MaxPercentUnhealthyServices = 0,
};
var policy = new ApplicationHealthPolicy()
{
    ConsiderWarningAsError = false,
    DefaultServiceTypeHealthPolicy = serviceTypePolicy,
    MaxPercentUnhealthyDeployedApplications = 0,
};

var queryDescription = new ApplicationHealthQueryDescription(applicationName)
{
    HealthPolicy = policy,
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = warningAndErrors },
    ServicesFilter = new ServiceHealthStatesFilter() { HealthStateFilterValue = warningAndErrors },
    DeployedApplicationsFilter = new DeployedApplicationHealthStatesFilter() { HealthStateFilterValue = warningAndErrors },
};

ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
intégrité des applications Hello applet de commande tooget hello est [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps). Tout d’abord, connectez toohello cluster à l’aide de hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) applet de commande.

applet de commande suivante Hello retourne intégrité hello hello **fabric : / WordCount** application :

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth fabric:/WordCount


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Warning
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                                  
                                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                                  
ServiceHealthStates             : 
                                  ServiceName           : fabric:/WordCount/WordCountWebService
                                  AggregatedHealthState : Ok
                                  
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Warning
                                  
DeployedApplicationHealthStates : 
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_4
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_3
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_0
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_2
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_1
                                  AggregatedHealthState : Ok
                                  
HealthEvents                    : 
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 282
                                  SentAt                : 7/13/2017 5:57:05 PM
                                  ReceivedAt            : 7/13/2017 5:57:05 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 7/13/2017 5:57:05 PM, LastWarning = 1/1/0001 12:00:00 AM
                                  
HealthStatistics                : 
                                  Replica               : 6 Ok, 0 Warning, 0 Error
                                  Partition             : 1 Ok, 1 Warning, 0 Error
                                  Service               : 1 Ok, 1 Warning, 0 Error
                                  DeployedServicePackage : 6 Ok, 0 Warning, 0 Error
                                  DeployedApplication   : 5 Ok, 0 Warning, 0 Error
```

Hello suivant passe d’applet de commande PowerShell dans les stratégies personnalisées. filtre les enfants et les événements.

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth -ApplicationName fabric:/WordCount -ConsiderWarningAsError $true -ServicesFilter Error -EventsFilter Error -DeployedApplicationsFilter Error -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                                  
                                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=true.
                                  
ServiceHealthStates             : 
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Error
                                  
DeployedApplicationHealthStates : None
HealthEvents                    : None
```

### <a name="rest"></a>REST
Vous pouvez obtenir le contrôle d’intégrité de l’application avec un [demande GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) ou un [demande POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) qui inclut les stratégies de contrôle d’intégrité décrits dans le corps de hello.

## <a name="get-service-health"></a>Obtenir l’état d’intégrité du service
Hello retourne l’intégrité d’une entité de service. Il contient les États d’intégrité de partition hello. Entrée :

* Hello [obligatoire] nom de service (URI) qui identifie le service de hello.
* Stratégie de contrôle d’intégrité d’application hello [facultatif] utilisé stratégie manifeste d’application hello toooverride.
* [Facultatif] Filtres pour les événements et les partitions qui spécifient les entrées sont dignes d’intérêt et doivent être retournés dans le résultat de hello (par exemple, uniquement, les erreurs ou avertissements et erreurs). Tous les événements et les partitions sont utilisées tooevaluate hello entité agrégée contrôle d’intégrité, quel que soit le filtre de hello.
* [Facultatif] Filtrer les statistiques d’intégrité tooexclude. Si non spécifié, hello hello d’afficher l’intégrité des statistiques OK, avertissement et erreur compter pour toutes les partitions et réplicas du service de hello.

### <a name="api"></a>API
l’intégrité du service tooget via hello API, créez un `FabricClient` et appel hello [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) méthode sur son HealthManager.

Hello exemple suivant obtient le contrôle d’intégrité hello d’un service avec le nom de service spécifié (URI) :

```charp
ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(serviceName);
```

Hello de code suivant obtient hello l’intégrité du service pour le nom de service spécifié hello (URI), en spécifiant des filtres et stratégie personnalisée via [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):

```csharp
var queryDescription = new ServiceHealthQueryDescription(serviceName)
{
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.All },
    PartitionsFilter = new PartitionHealthStatesFilter() { HealthStateFilterValue = HealthStateFilter.Error },
};

ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
contrôle d’intégrité du service de hello tooget Hello applet de commande est [Get-ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth). Tout d’abord, connectez toohello cluster à l’aide de hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) applet de commande.

Hello suivant l’applet de commande Obtient l’intégrité du service hello à l’aide de stratégies de contrôle d’intégrité par défaut :

```powershell
PS D:\ServiceFabric> Get-ServiceFabricServiceHealth -ServiceName fabric:/WordCount/WordCountService


ServiceName           : fabric:/WordCount/WordCountService
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                        
                        Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                        
                            Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
PartitionHealthStates : 
                        PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
                        AggregatedHealthState : Warning
                        
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 15
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Service has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                        
HealthStatistics      : 
                        Replica               : 5 Ok, 0 Warning, 0 Error
                        Partition             : 0 Ok, 1 Warning, 0 Error
```

### <a name="rest"></a>REST
Vous pouvez obtenir l’intégrité du service avec un [demande GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) ou un [demande POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) qui inclut les stratégies de contrôle d’intégrité décrits dans le corps de hello.

## <a name="get-partition-health"></a>Obtenir l'intégrité de la partition
Hello retourne l’intégrité d’une entité de la partition. Il contient les États d’intégrité de réplica hello. Entrée :

* Partition hello [obligatoire] ID (GUID) qui identifie la partition de hello.
* Stratégie de contrôle d’intégrité d’application hello [facultatif] utilisé stratégie manifeste d’application hello toooverride.
* [Facultatif] Filtres des réplicas qui spécifient les entrées et les événements sont dignes d’intérêt et doivent être retournés dans le résultat de hello (par exemple, uniquement, les erreurs ou avertissements et erreurs). Tous les événements et les réplicas sont utilisés tooevaluate hello entité agrégée contrôle d’intégrité, quel que soit le filtre de hello.
* [Facultatif] Filtrer les statistiques d’intégrité tooexclude. Si non spécifié, les statistiques d’intégrité hello indiquent le nombre de réplicas dans OK, avertissement et erreur États.

### <a name="api"></a>API
contrôle d’intégrité de la partition tooget via hello API, créez un `FabricClient` et appel hello [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) méthode sur son HealthManager. créer des paramètres facultatifs de toospecify, [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).

```csharp
PartitionHealth partitionHealth = await fabricClient.HealthManager.GetPartitionHealthAsync(partitionId);
```

### <a name="powershell"></a>PowerShell
intégrité de partition hello Hello applet de commande tooget [Get-ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth). Tout d’abord, connectez toohello cluster à l’aide de hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) applet de commande.

Hello applet de commande suivante obtient hello pour toutes les partitions de hello **fabric : / WordCount/WordCountService** service et exclut les États d’intégrité de réplica :

```powershell
PS D:\ServiceFabric> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricPartitionHealth -ReplicasFilter None

PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Warning
                        SequenceNumber        : 72
                        SentAt                : 7/13/2017 5:57:29 PM
                        ReceivedAt            : 7/13/2017 5:57:48 PM
                        TTL                   : Infinite
                        Description           : Partition is below target replica or instance count.
                        fabric:/WordCount/WordCountService 7 2 af2e3e44-a8f8-45ac-9f31-4093eb897600
                          N/P RD _Node_2 Up 131444422260002646
                          N/S RD _Node_4 Up 131444422293113678
                          N/S RD _Node_3 Up 131444422293113679
                          N/S RD _Node_1 Up 131444422293118720
                          N/S RD _Node_0 Up 131444422293118721
                          (Showing 5 out of 5 replicas. Total available replicas: 5.)
                        
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Ok->Warning = 7/13/2017 5:57:48 PM, LastError = 1/1/0001 12:00:00 AM
                        
                        SourceId              : System.PLB
                        Property              : ServiceReplicaUnplacedHealth_Secondary_af2e3e44-a8f8-45ac-9f31-4093eb897600
                        HealthState           : Warning
                        SequenceNumber        : 131444445174851664
                        SentAt                : 7/13/2017 6:35:17 PM
                        ReceivedAt            : 7/13/2017 6:35:18 PM
                        TTL                   : 00:01:05
                        Description           : hello Load Balancer was unable toofind a placement for one or more of hello Service's Replicas:
                        Secondary replica could not be placed due toohello following constraints and properties:  
                        TargetReplicaSetSize: 7
                        Placement Constraint: N/A
                        Parent Service: N/A
                        
                        Constraint Elimination Sequence:
                        Existing Secondary Replicas eliminated 4 possible node(s) for placement -- 1/5 node(s) remain.
                        Existing Primary Replica eliminated 1 possible node(s) for placement -- 0/5 node(s) remain.
                        
                        Nodes Eliminated By Constraints:
                        
                        Existing Secondary Replicas -- Nodes with Partition's Existing Secondary Replicas/Instances:
                        --
                        FaultDomain:fd:/4 NodeName:_Node_4 NodeType:NodeType4 UpgradeDomain:4 UpgradeDomain: ud:/4 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/3 NodeName:_Node_3 NodeType:NodeType3 UpgradeDomain:3 UpgradeDomain: ud:/3 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/1 NodeName:_Node_1 NodeType:NodeType1 UpgradeDomain:1 UpgradeDomain: ud:/1 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/0 NodeName:_Node_0 NodeType:NodeType0 UpgradeDomain:0 UpgradeDomain: ud:/0 Deactivation Intent/Status: None/None
                        
                        Existing Primary Replica -- Nodes with Partition's Existing Primary Replica or Secondary Replicas:
                        --
                        FaultDomain:fd:/2 NodeName:_Node_2 NodeType:NodeType2 UpgradeDomain:2 UpgradeDomain: ud:/2 Deactivation Intent/Status: None/None
                        
                        
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/13/2017 5:57:48 PM, LastOk = 1/1/0001 12:00:00 AM
                        
HealthStatistics      : 
                        Replica               : 5 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a>REST
Vous pouvez obtenir le contrôle d’intégrité de la partition avec un [demande GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) ou un [demande POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) qui inclut les stratégies de contrôle d’intégrité décrits dans le corps de hello.

## <a name="get-replica-health"></a>Obtenir les données d’intégrité des réplicas
Retourne le contrôle d’intégrité hello d’un réplica de service avec état ou d’une instance de service sans état. Entrée :

* Hello [obligatoire] ID (GUID) et le réplica ID de partition qui identifie le réplica de hello.
* Les paramètres de stratégie de contrôle d’intégrité application hello [facultatif] utilisé des stratégies de manifeste d’application toooverride hello.
* [Facultatif] Filtres pour les événements qui indiquent les entrées sont dignes d’intérêt et doivent être retournés dans le résultat de hello (par exemple, uniquement, les erreurs ou avertissements et erreurs). Tous les événements sont utilisés tooevaluate hello entité agrégée contrôle d’intégrité, quel que soit le filtre de hello.

### <a name="api"></a>API
contrôle d’intégrité du réplica tooget hello via hello API, créez un `FabricClient` et appel hello [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) méthode sur son HealthManager. toospecify avancée des paramètres, utilisez [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).

```csharp
ReplicaHealth replicaHealth = await fabricClient.HealthManager.GetReplicaHealthAsync(partitionId, replicaId);
```

### <a name="powershell"></a>PowerShell
intégrité de réplica hello Hello applet de commande tooget [Get-ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth). Tout d’abord, connectez toohello cluster à l’aide de hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) applet de commande.

Hello applet de commande suivante obtient hello du réplica principal de hello pour toutes les partitions du service de hello :

```powershell
PS D:\ServiceFabric> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricReplica | where {$_.ReplicaRole -eq "Primary"} | Get-ServiceFabricReplicaHealth


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422260002646
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131444422263668344
                        SentAt                : 7/13/2017 5:57:06 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_2
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a>REST
Vous pouvez obtenir l’intégrité du réplica avec une [demande GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) ou un [demande POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) qui inclut les stratégies de contrôle d’intégrité décrits dans le corps de hello.

## <a name="get-deployed-application-health"></a>Obtenir les données d’intégrité des applications déployées
Hello retourne l’intégrité d’une application déployée sur une entité de nœud. Il contient les États de fonctionnement de package de service hello déployé. Entrée :

* Nom de l’application hello [obligatoire] (URI) et le nom de nœud (chaîne) qui identifient hello déploiement l’application.
* Stratégie de contrôle d’intégrité d’application hello [facultatif] utilisé des stratégies de manifeste d’application toooverride hello.
* [Facultatif] Filtres pour les événements et les packages de service déployé qui spécifient les entrées sont dignes d’intérêt et doivent être retournés dans le résultat de hello (par exemple, uniquement, les erreurs ou avertissements et erreurs). Tous les événements et les packages de service déployé sont l’intégrité de l’entité agrégée d’hello tooevaluate utilisé, quel que soit le filtre de hello.
* [Facultatif] Filtrer les statistiques d’intégrité tooexclude. Si non spécifié, les statistiques d’intégrité hello affichent nombre hello des packages de service déployé dans les États d’intégrité OK, avertissement et erreur.

### <a name="api"></a>API
contrôle d’intégrité de hello tooget d’une application déployée sur un nœud via hello API, créez un `FabricClient` et appel hello [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) méthode sur son HealthManager. utiliser des paramètres facultatifs de toospecify, [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).

```csharp
DeployedApplicationHealth health = await fabricClient.HealthManager.GetDeployedApplicationHealthAsync(
    new DeployedApplicationHealthQueryDescription(applicationName, nodeName));
```

### <a name="powershell"></a>PowerShell
Bonjour applet de commande tooget hello déployé l’intégrité d’applications est [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps). Tout d’abord, connectez toohello cluster à l’aide de hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) applet de commande. toofind out où une application est déployée, exécutez [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) et examinez hello déployé des enfants de l’application.

Hello applet de commande suivante obtient intégrité hello hello **fabric : / WordCount** application déployée sur **_Node_2**.

```powershell
PS D:\ServiceFabric> Get-ServiceFabricDeployedApplicationHealth -ApplicationName fabric:/WordCount -NodeName _Node_0


ApplicationName                    : fabric:/WordCount
NodeName                           : _Node_0
AggregatedHealthState              : Ok
DeployedServicePackageHealthStates : 
                                     ServiceManifestName   : WordCountServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_0
                                     AggregatedHealthState : Ok
                                     
                                     ServiceManifestName   : WordCountWebServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_0
                                     AggregatedHealthState : Ok
                                     
HealthEvents                       : 
                                     SourceId              : System.Hosting
                                     Property              : Activation
                                     HealthState           : Ok
                                     SequenceNumber        : 131444422261848308
                                     SentAt                : 7/13/2017 5:57:06 PM
                                     ReceivedAt            : 7/13/2017 5:57:17 PM
                                     TTL                   : Infinite
                                     Description           : hello application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/13/2017 5:57:17 PM, LastWarning = 1/1/0001 12:00:00 AM
                                     
HealthStatistics                   : 
                                     DeployedServicePackage : 2 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a>REST
Vous pouvez obtenir le contrôle d’intégrité de l’application déployée avec une [demande GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) ou un [demande POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) qui inclut les stratégies de contrôle d’intégrité décrits dans le corps de hello.

## <a name="get-deployed-service-package-health"></a>Obtenir les données d’intégrité d’un package de services déployé
Retourne hello d’intégrité d’une entité de package de service déployé. Entrée :

* Nom de l’application hello [obligatoire] (URI), le nom de nœud (chaîne) et nom de manifeste de service (chaîne) qui identifient hello déploiement le package de service.
* Stratégie de contrôle d’intégrité d’application hello [facultatif] utilisé stratégie manifeste d’application hello toooverride.
* [Facultatif] Filtres pour les événements qui indiquent les entrées sont dignes d’intérêt et doivent être retournés dans le résultat de hello (par exemple, uniquement, les erreurs ou avertissements et erreurs). Tous les événements sont utilisés tooevaluate hello entité agrégée contrôle d’intégrité, quel que soit le filtre de hello.

### <a name="api"></a>API
contrôle d’intégrité de hello tooget d’un package de service déployé via hello API, créez un `FabricClient` et appel hello [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) méthode sur son HealthManager. utiliser des paramètres facultatifs de toospecify, [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).

```csharp
DeployedServicePackageHealth health = await fabricClient.HealthManager.GetDeployedServicePackageHealthAsync(
    new DeployedServicePackageHealthQueryDescription(applicationName, nodeName, serviceManifestName));
```

### <a name="powershell"></a>PowerShell
Bonjour applet de commande tooget hello déployé package l’intégrité du service est [Get-ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth). Tout d’abord, connectez toohello cluster à l’aide de hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) applet de commande. toosee où une application est déployée, exécutez [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) et examinez les applications hello déployé. toosee qui packages de service figurent dans une application, recherchez à hello déployé enfants de package de service Bonjour [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) sortie.

Hello applet de commande suivante obtient intégrité hello hello **WordCountServicePkg** package de service de hello **fabric : / WordCount** application déployée sur **_Node_2**. entité de Hello a **System.Hosting** des rapports d’activation d’un package de service et de point d’entrée et une inscription réussie de type de service.

```powershell
PS D:\ServiceFabric> Get-ServiceFabricDeployedApplication -ApplicationName fabric:/WordCount -NodeName _Node_2 | Get-ServiceFabricDeployedServicePackageHealth -ServiceManifestName WordCountServicePkg


ApplicationName            : fabric:/WordCount
ServiceManifestName        : WordCountServicePkg
ServicePackageActivationId : 
NodeName                   : _Node_2
AggregatedHealthState      : Ok
HealthEvents               : 
                             SourceId              : System.Hosting
                             Property              : Activation
                             HealthState           : Ok
                             SequenceNumber        : 131444422267693359
                             SentAt                : 7/13/2017 5:57:06 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : hello ServicePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : CodePackageActivation:Code:EntryPoint
                             HealthState           : Ok
                             SequenceNumber        : 131444422267903345
                             SentAt                : 7/13/2017 5:57:06 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : hello CodePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : ServiceTypeRegistration:WordCountServiceType
                             HealthState           : Ok
                             SequenceNumber        : 131444422272458374
                             SentAt                : 7/13/2017 5:57:07 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : hello ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a>REST
Vous pouvez obtenir l’intégrité de package de service déployé avec un [demande GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) ou un [demande POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) qui inclut les stratégies de contrôle d’intégrité décrits dans le corps de hello.

## <a name="health-chunk-queries"></a>Requêtes par segment d’intégrité
les requêtes de bloc de contrôle d’intégrité Hello peuvent retourner des enfants de cluster à plusieurs niveaux (de manière récursive), par les filtres d’entrée. Il prend en charge les filtres avancés qui permettent une grande souplesse dans le choix des enfants de hello toobe retourné. les filtres de Hello peuvent spécifier des enfants en identificateur hello ou par d’autres identificateurs de groupe et/ou les États d’intégrité. Par défaut, aucun enfant n’est inclus, que les commandes toohealth opposés qui incluent toujours les enfants de premier niveau.

Hello [requêtes d’intégrité](service-fabric-view-entities-aggregated-health.md#health-queries) retournés enfants de premier niveau uniquement de hello spécifié entité par les filtres requis. tooget hello les enfants des enfants de hello, vous devez appeler d’intégrité supplémentaires API pour chaque entité d’intérêt. De même, la santé hello tooget des entités spécifiques, vous devez appeler d’intégrité une d’API pour chaque entité de votre choix. Hello segment requête filtrage avancé vous permet de toorequest plusieurs éléments d’intérêt dans une requête, en réduisant la taille des messages hello et nombre hello de messages.

valeur de Hello de requête de segment hello est que vous pouvez obtenir l’état d’intégrité pour plusieurs entités de cluster (potentiellement toutes les entités de cluster en commençant à la racine requis) dans un seul appel. Vous pouvez transmettre des requêtes d’intégrité complexes, comme :

* Retourner uniquement les applications ayant des erreurs, et pour ces applications inclure l’ensemble des services affichant un état d’avertissement ou d’erreur. Pour les services renvoyés, inclure l’ensemble des partitions.
* Retourner uniquement hello contrôle d’intégrité de quatre applications, spécifiée par leurs noms.
* Retourner uniquement hello contrôle d’intégrité des applications d’un type de l’application souhaitée.
* Renvoyer l’ensemble des entités déployées sur un nœud. Retourne toutes les applications, toutes les applications déployées sur le nœud spécifié de hello et tous les packages de service hello déployé sur ce nœud.
* Retourner l’ensemble des réplicas présentant l’état d’erreur. L’ensemble des applications, des services, des partitions et uniquement les réplicas présentant un état d’erreur sont retournés.
* Renvoyer l’ensemble des applications. Pour un service spécifié, inclure l’ensemble des partitions.

Actuellement, requête de bloc de contrôle d’intégrité hello est exposé uniquement pour les entités de cluster hello. Elle renvoie un segment d’intégrité de cluster, qui comprend :

* état d’intégrité de cluster agrégée Hello.
* liste de segment état Hello d’intégrité des nœuds qui respectent les filtres d’entrée.
* liste de segment état Hello d’intégrité des applications qui respectent les filtres d’entrée. Chaque segment d’état de santé application contient une liste de blocs avec tous les services qui respectent les filtres d’entrée et une liste de blocs avec toutes les applications déployées qui respectent les filtres hello. Même pour les enfants hello des services et des applications déployées. De cette manière, toutes les entités dans un cluster de hello peuvent être potentiellement retournées si nécessaire, de manière hiérarchique.

### <a name="cluster-health-chunk-query"></a>Requête par segment d’intégrité de cluster
Retourne hello d’intégrité de l’entité de cluster hello et contient des segments d’état d’intégrité hiérarchique hello des enfants obligatoires. Entrée :

* Stratégie de contrôle d’intégrité du cluster hello [facultatif] utilisé des nœuds de hello tooevaluate et les événements de cluster hello.
* Mappage de stratégie d’intégrité [facultatif] hello application, avec des stratégies de contrôle d’intégrité hello utilisé stratégies manifeste d’application hello toooverride.
* [Facultatif] Filtres pour les nœuds et les applications qui spécifient les entrées sont dignes d’intérêt et doivent être retournés dans le résultat de hello. filtres de Hello sont spécifiques tooan entité/groupe d’entités ou entités tooall applicable à ce niveau. liste de Hello de filtres peut contenir un seul filtre général et/ou des filtres pour les entités de granularité toofine identificateurs spécifique retournées par la requête de hello. Si elle est vide, les enfants de hello ne sont pas retournés par défaut.
  En savoir plus sur les filtres de hello au [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) et [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter). récursive de Hello application des filtres peuvent spécifier des filtres avancés pour les enfants.

résultat de segment Hello inclut enfants hello qui respectent les filtres hello.

Actuellement, requête de segment hello ne retourne pas les événements de l’entité ou les évaluations non intègres. Ces informations supplémentaires peuvent être obtenues à l’aide de la requête de contrôle d’intégrité de cluster existante hello.

### <a name="api"></a>API
l’intégrité du cluster tooget segment, créez un `FabricClient` et appel hello [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) méthode sur son **HealthManager**. Vous pouvez passer dans [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) toodescribe des stratégies d’intégrité et les filtres avancés.

Hello de code suivant obtient blocs de contrôle d’intégrité de cluster avec des filtres avancés.

```csharp
var queryDescription = new ClusterHealthChunkQueryDescription();
queryDescription.ApplicationFilters.Add(new ApplicationHealthStateFilter()
    {
        // Return applications only if they are in error
        HealthStateFilter = HealthStateFilter.Error
    });

// Return all replicas
var wordCountServiceReplicaFilter = new ReplicaHealthStateFilter()
    {
        HealthStateFilter = HealthStateFilter.All
    };

// Return all replicas and all partitions
var wordCountServicePartitionFilter = new PartitionHealthStateFilter()
    {
        HealthStateFilter = HealthStateFilter.All
    };
wordCountServicePartitionFilter.ReplicaFilters.Add(wordCountServiceReplicaFilter);

// For specific service, return all partitions and all replicas
var wordCountServiceFilter = new ServiceHealthStateFilter()
{
    ServiceNameFilter = new Uri("fabric:/WordCount/WordCountService"),
};
wordCountServiceFilter.PartitionFilters.Add(wordCountServicePartitionFilter);

// Application filter: for specific application, return no services except hello ones of interest
var wordCountApplicationFilter = new ApplicationHealthStateFilter()
    {
        // Always return fabric:/WordCount application
        ApplicationNameFilter = new Uri("fabric:/WordCount"),
    };
wordCountApplicationFilter.ServiceFilters.Add(wordCountServiceFilter);

queryDescription.ApplicationFilters.Add(wordCountApplicationFilter);

var result = await fabricClient.HealthManager.GetClusterHealthChunkAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
intégrité de cluster hello Hello applet de commande tooget [Get-ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk). Tout d’abord, connectez toohello cluster à l’aide de hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) applet de commande.

Hello de code suivant obtient nœuds uniquement si elles sont dans l’erreur à l’exception d’un nœud spécifique, qui doit-elle être renvoyé.

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$nodeFilter1 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{HealthStateFilter=$errorFilter}
$nodeFilter2 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{NodeNameFilter="_Node_1";HealthStateFilter=$allFilter}
# Create node filter list that will be passed in hello cmdlet
$nodeFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.NodeHealthStateFilter]
$nodeFilters.Add($nodeFilter1)
$nodeFilters.Add($nodeFilter2)

Get-ServiceFabricClusterHealthChunk -NodeFilters $nodeFilters


HealthState                  : Warning
NodeHealthStateChunks        : 
                               TotalCount            : 1
                               
                               NodeName              : _Node_1
                               HealthState           : Ok
                               
ApplicationHealthStateChunks : None
```

Hello suivant l’applet de commande Obtient le segment du cluster avec les filtres d’application.

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

# All replicas
$replicaFilter = New-Object System.Fabric.Health.ReplicaHealthStateFilter -Property @{HealthStateFilter=$allFilter}

# All partitions
$partitionFilter = New-Object System.Fabric.Health.PartitionHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$partitionFilter.ReplicaFilters.Add($replicaFilter)

# For WordCountService, return all partitions and all replicas
$svcFilter1 = New-Object System.Fabric.Health.ServiceHealthStateFilter -Property @{ServiceNameFilter="fabric:/WordCount/WordCountService"}
$svcFilter1.PartitionFilters.Add($partitionFilter)

$svcFilter2 = New-Object System.Fabric.Health.ServiceHealthStateFilter -Property @{HealthStateFilter=$errorFilter}

$appFilter = New-Object System.Fabric.Health.ApplicationHealthStateFilter -Property @{ApplicationNameFilter="fabric:/WordCount"}
$appFilter.ServiceFilters.Add($svcFilter1)
$appFilter.ServiceFilters.Add($svcFilter2)

$appFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.ApplicationHealthStateFilter]
$appFilters.Add($appFilter)

Get-ServiceFabricClusterHealthChunk -ApplicationFilters $appFilters


HealthState                  : Error
NodeHealthStateChunks        : None
ApplicationHealthStateChunks : 
                               TotalCount            : 1
                               
                               ApplicationName       : fabric:/WordCount
                               ApplicationTypeName   : WordCount
                               HealthState           : Error
                               ServiceHealthStateChunks : 
                                TotalCount            : 1
                               
                                ServiceName           : fabric:/WordCount/WordCountService
                                HealthState           : Error
                                PartitionHealthStateChunks : 
                                    TotalCount            : 1
                               
                                    PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
                                    HealthState           : Error
                                    ReplicaHealthStateChunks : 
                                        TotalCount            : 5
                               
                                        ReplicaOrInstanceId   : 131444422293118720
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293118721
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293113678
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293113679
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422260002646
                                        HealthState           : Error
```

Hello applet de commande suivante retourne déployées toutes les entités sur un nœud.

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$dspFilter = New-Object System.Fabric.Health.DeployedServicePackageHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$daFilter =  New-Object System.Fabric.Health.DeployedApplicationHealthStateFilter -Property @{HealthStateFilter=$allFilter;NodeNameFilter="_Node_2"}
$daFilter.DeployedServicePackageFilters.Add($dspFilter)

$appFilter = New-Object System.Fabric.Health.ApplicationHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$appFilter.DeployedApplicationFilters.Add($daFilter)

$appFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.ApplicationHealthStateFilter]
$appFilters.Add($appFilter)
Get-ServiceFabricClusterHealthChunk -ApplicationFilters $appFilters


HealthState                  : Error
NodeHealthStateChunks        : None
ApplicationHealthStateChunks : 
                               TotalCount            : 2
                               
                               ApplicationName       : fabric:/System
                               HealthState           : Ok
                               DeployedApplicationHealthStateChunks : 
                                TotalCount            : 1
                               
                                NodeName              : _Node_2
                                HealthState           : Ok
                                DeployedServicePackageHealthStateChunks :
                                    TotalCount            : 1
                               
                                    ServiceManifestName   : FAS
                                    ServicePackageActivationId : 
                                    HealthState           : Ok
                               
                               
                               
                               ApplicationName       : fabric:/WordCount
                               ApplicationTypeName   : WordCount
                               HealthState           : Error
                               DeployedApplicationHealthStateChunks : 
                                TotalCount            : 1
                               
                                NodeName              : _Node_2
                                HealthState           : Ok
                                DeployedServicePackageHealthStateChunks :
                                    TotalCount            : 1
                               
                                    ServiceManifestName   : WordCountServicePkg
                                    ServicePackageActivationId : 
                                    HealthState           : Ok
```

### <a name="rest"></a>REST
Vous pouvez obtenir le segment de contrôle d’intégrité de cluster avec un [demande GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) ou un [demande POST](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) qui inclut les stratégies d’intégrité et les filtres avancés, décrits dans le corps de hello.

## <a name="general-queries"></a>Requêtes générales
Les requêtes générales renvoient la liste des entités Service Fabric d’un type spécifié. Elles sont exposées via hello API (via des méthodes hello sur **FabricClient.QueryManager**), applets de commande PowerShell et REST. Ces requêtes agrègent les sous-requêtes de plusieurs composants. Un d’eux est hello [magasin de contrôle d’intégrité](service-fabric-health-introduction.md#health-store), qui remplit hello agrégées l’état d’intégrité de chaque résultat de la requête.  

> [!NOTE]
> Requêtes générales retournent hello agrégée état d’intégrité de l’entité de hello et ne contiennent pas de données d’intégrité riche. Si une entité n’est pas intègre, vous pouvez suivre avec tooget de requêtes d’intégrité toutes ses informations de contrôle d’intégrité, y compris les événements, les États d’intégrité enfant et évaluations non intègres.
>
>

Si des requêtes générales retournent un état d’intégrité inconnu pour une entité, il est possible de que ce magasin de contrôle d’intégrité hello n’a pas les données complètes sur l’entité de hello. Il est également possible qu’un magasin de contrôle d’intégrité de sous-requête toohello a échoué (par exemple, une erreur de communication s’est produite ou magasin de contrôle d’intégrité hello a été limitée). Effectuez le suivi avec une requête de contrôle d’intégrité d’entité de hello. Si la sous-requête de hello a rencontré des erreurs temporaires, tels que des problèmes de réseau, cette requête de suivi peut réussir. Il peut également vous fournit plus de détails à partir du magasin de contrôle d’intégrité hello sur la raison pour laquelle les entités hello ne sont pas exposée.

Hello des requêtes qui contiennent des **HealthState** pour les entités sont :

* Liste de nœuds : retourne les nœuds de liste hello cluster hello (paginée).
  * API : [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)
  * Powershell : Get-ServiceFabricNode
* Liste des applications : renvoie la liste des applications en cluster hello (paginée) hello.
  * API : [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)
  * Powershell : Get-ServiceFabricApplication
* Liste de services : renvoie la liste des services dans une application (paginée) hello.
  * API : [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)
  * Powershell : Get-ServiceFabricService
* Liste de partitions : renvoie la liste de partitions dans un service (paginée) hello.
  * API : [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)
  * PowerShell : Get-ServiceFabricPartition
* Liste des réplicas : renvoie la liste de réplicas dans une partition (paginée) hello.
  * API : [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)
  * PowerShell : Get-ServiceFabricReplica
* Déployé la liste des applications : renvoie la liste des applications déployées sur un nœud hello.
  * API : [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)
  * PowerShell : Get-ServiceFabricDeployedApplication
* Déployé la liste des packages de service : renvoie la liste des packages de service dans une application déployée hello.
  * API : [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)
  * PowerShell : Get-ServiceFabricDeployedApplication

> [!NOTE]
> Certaines requêtes de hello retourner des résultats paginés. retour de ces requêtes Hello est une liste dérivée [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1). Si les résultats hello ne tiennent pas un message, une page est retournée et un ContinuationToken qui assure le suivi où l’énumération s’est arrêté. Continuer toocall hello même requête et que vous passez dans un jeton de continuation hello hello précédente résultats de requête tooget suivants.
>
>

### <a name="examples"></a>Exemples
Hello de code suivant obtient les applications non intègres hello dans un cluster de hello :

```csharp
var applications = fabricClient.QueryManager.GetApplicationListAsync().Result.Where(
  app => app.HealthState == HealthState.Error);
```

Détails de l’application hello pour l’ensemble fibre optique hello obtient Hello applet de commande suivante : / WordCount application. Notez l’état d’intégrité d’avertissement.

```powershell
PS C:\> Get-ServiceFabricApplication -ApplicationName fabric:/WordCount

ApplicationName        : fabric:/WordCount
ApplicationTypeName    : WordCount
ApplicationTypeVersion : 1.0.0
ApplicationStatus      : Ready
HealthState            : Warning
ApplicationParameters  : { "WordCountWebService_InstanceCount" = "1";
                         "_WFDebugParams_" = "[{"ServiceManifestName":"WordCountWebServicePkg","CodePackageName":"Code","EntryPointType":"Main","Debug
                         ExePath":"C:\\Program Files (x86)\\Microsoft Visual Studio
                         14.0\\Common7\\Packages\\Debugger\\VsDebugLaunchNotify.exe","DebugArguments":" {74f7e5d5-71a9-47e2-a8cd-1878ec4734f1} -p
                         [ProcessId] -tid [ThreadId]","EnvironmentBlock":"_NO_DEBUG_HEAP=1\u0000"},{"ServiceManifestName":"WordCountServicePkg","CodeP
                         ackageName":"Code","EntryPointType":"Main","DebugExePath":"C:\\Program Files (x86)\\Microsoft Visual Studio
                         14.0\\Common7\\Packages\\Debugger\\VsDebugLaunchNotify.exe","DebugArguments":" {2ab462e6-e0d1-4fda-a844-972f561fe751} -p
                         [ProcessId] -tid [ThreadId]","EnvironmentBlock":"_NO_DEBUG_HEAP=1\u0000"}]" }
```

Hello applet de commande suivante obtient les services hello dont l’état d’intégrité de l’erreur :

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplication | Get-ServiceFabricService | where {$_.HealthState -eq "Error"}


ServiceName            : fabric:/WordCount/WordCountService
ServiceKind            : Stateful
ServiceTypeName        : WordCountServiceType
IsServiceGroup         : False
ServiceManifestVersion : 1.0.0
HasPersistedState      : True
ServiceStatus          : Active
HealthState            : Error
```

## <a name="cluster-and-application-upgrades"></a>Mises à niveau d’applications et de clusters
Pendant une mise à niveau analysé du cluster de hello et application, Service Fabric vérifie tooensure de contrôle d’intégrité que tout est bonne. Si une entité n’est pas sain telle qu’évaluée à l’aide de stratégies d’intégrité configurée, mise à niveau hello applique prochaine action des stratégies spécifiques à la mise à niveau toodetermine hello. mise à niveau Hello peut être mis en pause tooallow intervention de l’utilisateur (par exemple, la fixation des conditions d’erreur ou la modification des stratégies), ou il peut automatiquement restaurer version correcte de toohello précédente.

Pendant un *cluster* mise à niveau, vous pouvez obtenir l’état de mise à niveau de cluster hello. état de mise à niveau Hello inclut des évaluations non intègres, quels toowhat point est défectueux dans un cluster de hello. Si la mise à niveau hello est restaurée en raison de problèmes de toohealth, état de mise à niveau hello souvient de raisons de fonctionnement anormal dernière hello. Cette information peut aider les administrateurs à examiner la cause du problème après que la mise à niveau hello restaurée ou arrêté.

De même, pendant une *application* mise à niveau, les évaluations défectueuses sont contenues dans l’état de mise à niveau l’application hello.

Hello Voici état de mise à niveau l’application hello pour une infrastructure modifiée : / WordCount application. Un agent de surveillance a signalé une erreur sur l’un de ses réplicas. mise à niveau Hello est propagée, car les vérifications de contrôle d’intégrité hello ne sont pas respectées.

```powershell
PS C:\> Get-ServiceFabricApplicationUpgrade fabric:/WordCount

ApplicationName               : fabric:/WordCount
ApplicationTypeName           : WordCount
TargetApplicationTypeVersion  : 1.0.0.0
ApplicationParameters         : {}
StartTimestampUtc             : 4/21/2017 5:23:26 PM
FailureTimestampUtc           : 4/21/2017 5:23:37 PM
FailureReason                 : HealthCheck
UpgradeState                  : RollingBackInProgress
UpgradeDuration               : 00:00:23
CurrentUpgradeDomainDuration  : 00:00:00
CurrentUpgradeDomainProgress  : UD1

                                NodeName            : _Node_1
                                UpgradePhase        : Upgrading

                                NodeName            : _Node_2
                                UpgradePhase        : Upgrading

                                NodeName            : _Node_3
                                UpgradePhase        : PreUpgradeSafetyCheck
                                PendingSafetyChecks :
                                EnsurePartitionQuorum - PartitionId: 30db5be6-4e20-4698-8185-4bd7ca744020
NextUpgradeDomain             : UD2
UpgradeDomainsStatus          : { "UD1" = "Completed";
                                "UD2" = "Pending";
                                "UD3" = "Pending";
                                "UD4" = "Pending" }
UnhealthyEvaluations          :
                                Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.

                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.

                                      Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                      Unhealthy partition: PartitionId='a1f83a35-d6bf-4d39-b90d-28d15f39599b', AggregatedHealthState='Error'.

                                          Unhealthy replicas: 20% (1/5), MaxPercentUnhealthyReplicasPerPartition=0%.

                                          Unhealthy replica: PartitionId='a1f83a35-d6bf-4d39-b90d-28d15f39599b',
                                  ReplicaOrInstanceId='131031502346844058', AggregatedHealthState='Error'.

                                              Error event: SourceId='DiskWatcher', Property='Disk'.

UpgradeKind                   : Rolling
RollingUpgradeMode            : UnmonitoredAuto
ForceRestart                  : False
UpgradeReplicaSetCheckTimeout : 00:15:00
```

En savoir plus sur hello [mise à niveau de Service Fabric application](service-fabric-application-upgrade.md).

## <a name="use-health-evaluations-tootroubleshoot"></a>Utilisez tootroubleshoot d’évaluations d’intégrité
Chaque fois qu’il existe un problème avec le cluster de hello ou d’une application, recherchez toopinpoint de contrôle d’intégrité de cluster ou une application hello quel est le problème. les évaluations non intègres Hello fournissent des détails sur l’état non intègre hello déclenchées en cours. Si vous le souhaitez, vous pouvez descendre dans la cause première enfants non intègres entités tooidentify hello.

Par exemple, considérez une application comme non intègre du fait de l’existence d’un rapport d’erreurs sur l’un de ses réplicas. Hello applet de commande Powershell suivante montre les évaluations non intègres hello :

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth fabric:/WordCount -EventsFilter None -ServicesFilter None -DeployedApplicationsFilter None -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                                  
                                        Unhealthy replicas: 20% (1/5), MaxPercentUnhealthyReplicasPerPartition=0%.
                                  
                                        Unhealthy replica: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', ReplicaOrInstanceId='131444422260002646', AggregatedHealthState='Error'.
                                  
                                            Error event: SourceId='MyWatchdog', Property='Memory'.
                                  
ServiceHealthStates             : None
DeployedApplicationHealthStates : None
HealthEvents                    : None
```

Vous pouvez examiner hello réplica tooget plus d’informations :

```powershell
PS D:\ServiceFabric> Get-ServiceFabricReplicaHealth -ReplicaOrInstanceId 131444422260002646 -PartitionId af2e3e44-a8f8-45ac-9f31-4093eb897600


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422260002646
AggregatedHealthState : Error
UnhealthyEvaluations  : 
                        Error event: SourceId='MyWatchdog', Property='Memory'.
                        
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131444422263668344
                        SentAt                : 7/13/2017 5:57:06 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_2
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                        
                        SourceId              : MyWatchdog
                        Property              : Memory
                        HealthState           : Error
                        SequenceNumber        : 131444451657749403
                        SentAt                : 7/13/2017 6:46:05 PM
                        ReceivedAt            : 7/13/2017 6:46:05 PM
                        TTL                   : Infinite
                        Description           : 
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Warning->Error = 7/13/2017 6:46:05 PM, LastOk = 1/1/0001 12:00:00 AM
```

> [!NOTE]
> Hello première raison évaluations non intègres afficher hello hello entité est évaluée toocurrent l’état d’intégrité. Il peut y avoir plusieurs autres événements qui déclenchent cet état, mais ils ne sont pas reflétées dans les évaluations hello. tooget plus d’informations, développez hello intégrité entités toofigure tous les rapports défectueux hello dans un cluster de hello.
>
>

## <a name="next-steps"></a>Étapes suivantes
[Utilisez tootroubleshoot de rapports d’intégrité système](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[Ajout de rapports d’intégrité Service Fabric personnalisés](service-fabric-report-health.md)

[Comment tooreport et vérification du service d’intégrité](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[Surveiller et diagnostiquer les services localement](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Mise à niveau des applications Service Fabric](service-fabric-application-upgrade.md)
