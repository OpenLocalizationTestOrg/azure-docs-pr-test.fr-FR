---
title: "aaaTroubleshoot avec les rapports d’intégrité système | Documents Microsoft"
description: "Décrit les rapports de contrôle d’intégrité hello envoyés par les composants d’infrastructure de Service Azure et leur utilisation pour la résolution des problèmes de cluster ou de problèmes liés aux applications."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: 52574ea7-eb37-47e0-a20a-101539177625
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: oanapl
ms.openlocfilehash: c77a6cdd0440ce5d354cd8760f40151f674a3529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-system-health-reports-tootroubleshoot"></a>Utilisez tootroubleshoot de rapports d’intégrité système
Azure Service Fabric composants rapport prédéfinies hello sur toutes les entités dans un cluster de hello. Hello [magasin de contrôle d’intégrité](service-fabric-health-introduction.md#health-store) crée et supprime les entités en fonction des rapports sur le système hello. Il les organise au sein d’une hiérarchie qui tient compte des interactions entre les entités.

> [!NOTE]
> concepts relatifs à l’état de toounderstand, en savoir plus sur [modèle de contrôle d’intégrité de l’infrastructure de Service](service-fabric-health-introduction.md).
> 
> 

Les rapports d’intégrité du système procurent une visibilité sur les fonctionnalités du cluster et des applications, et signalent les problèmes d’intégrité. Pour les applications et services, rapports d’intégrité système Vérifiez que les entités sont implémentées et sont comportent correctement à partir de hello perspective de l’infrastructure de Service. rapports de Hello ne fournissent pas de n’importe quel contrôle d’intégrité de la logique métier de hello du service de hello ou détection de processus bloqués. Services de l’utilisateur peuvent enrichir les données de contrôle d’intégrité de hello avec une logique spécifique tootheir plus d’informations.

> [!NOTE]
> Agents de surveillance des rapports d’intégrité sont visibles uniquement *après* composants du système hello créent une entité. Lorsqu’une entité est supprimée, magasin de contrôle d’intégrité hello supprime automatiquement tous les rapports d’intégrité associées. Hello même a la valeur true lors de la création d’une nouvelle instance de l’entité de hello (par exemple, une nouvelle instance de réplica de service rendues persistantes avec état est créée). Tous les rapports associés avec l’ancienne instance de hello sont supprimés et supprimés du magasin de hello.
> 
> 

rapports sur les composants système Hello sont identifiés par source de hello, qui commence par hello »**système.**» . Agents de surveillance ne peut pas utiliser hello même préfixe de leurs sources, comme des rapports avec des paramètres non valides sont rejetées.
Nous allons examiner certains rapports toounderstand ce qui déclenche les et comment toocorrect hello éventuels problèmes qu’ils représentent.

> [!NOTE]
> Service Fabric continue tooadd des rapports sur les conditions d’intérêt qui améliorent la visibilité de ce qui se passe dans l’application et du cluster de hello. Les rapports existants peuvent également être améliorées avec plus de détails toohelp dépannage hello plus rapidement.
> 
> 

## <a name="cluster-system-health-reports"></a>Rapports d’intégrité du système sur le cluster
entité de contrôle d’intégrité de cluster Hello est créée automatiquement dans le magasin de contrôle d’intégrité hello. Si tout fonctionne correctement, elle ne présente pas de rapport système.

### <a name="neighborhood-loss"></a>Perte de voisinage
**System.Federation** indique une erreur s’il détecte une perte de voisinage. rapport de Hello est à partir des nœuds individuels, et ID de nœud hello est inclus dans le nom de la propriété hello. Si un cercle est perdue au cours de l’anneau de Service Fabric entière hello, vous verrez généralement deux événements (les deux côtés du rapport d’écart hello). Si plusieurs voisinages sont perdus, d’autres d’événements ont lieu.

rapport de Hello Spécifie le délai d’attente de hello bail global comme heure hello toolive. rapport de Hello est renvoyée à chaque semestre de durée de vie hello pour tant que condition de hello demeure active. événement de Hello est automatiquement supprimé lorsqu’il arrive à expiration. Supprimer lorsque le comportement expirée permet de s’assurer que les rapports de hello sont nettoyées à partir du magasin de contrôle d’intégrité hello correctement, même si le nœud de création de rapports hello est arrêté.

* **SourceId**: System.Federation.
* **Property** : commence par **Neighborhood** et inclut des informations sur le nœud.
* **Étapes suivantes**: recherchez pourquoi le voisinage de hello est perdue (par exemple, la communication de hello cocher entre les nœuds de cluster).

## <a name="node-system-health-reports"></a>Rapports d’intégrité du système sur les nœuds
**System.FM**, qui représente le service de gestionnaire de basculement hello, est l’autorité hello qui gère des informations sur les nœuds de cluster. Un rapport System.FM indiquant son état doit être alloué à chaque nœud. entités de nœud de Hello sont supprimées lors de l’état du nœud hello est supprimé (consultez [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).

### <a name="node-updown"></a>Nœud activé/désactivé
System.FM signale comme OK lorsque le nœud de hello joint anneau hello (il est en cours d’exécution). Il signale une erreur lors de l’anneau de hello de départ du nœud de hello (elle est activée, la mise à niveau ou simplement, car il a échoué). hiérarchie de contrôle d’intégrité Hello généré par le magasin de contrôle d’intégrité hello entreprend des actions sur les entités déployées en corrélation avec les rapports de nœuds System.FM. Il considère que le nœud de hello virtuel parent de toutes les entités déployés. entités Hello déployé sur ce nœud sont exposées via des requêtes si le nœud de hello est signalée comme par System.FM, avec hello même l’instance comme instance hello associée aux entités de hello. Lorsque System.FM signale ce nœud hello est arrêté ou redémarré (une nouvelle instance), magasin de contrôle d’intégrité hello nettoie automatiquement les entités hello déployé qui peuvent exister uniquement sur hello nœud vers le bas ou sur l’instance précédente de hello du nœud de hello.

* **SourceId**: System.FM
* **Property**: State
* **Étapes suivantes**: si le nœud de hello est arrêté pour une mise à niveau, il doit s’afficher dans une fois qu’il a été mis à niveau. Dans ce cas, l’état d’intégrité hello doit basculer tooOK précédent. Si le nœud de hello ne revenez ou il échoue, problème de hello doit investigations plus poussées.

Hello exemple suivant montre hello System.FM événement avec un état d’intégrité de OK pour le nœud :

```powershell
PS C:\> Get-ServiceFabricNodeHealth  _Node_0

NodeName              : _Node_0
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 8
                        SentAt                : 7/14/2017 4:54:51 PM
                        ReceivedAt            : 7/14/2017 4:55:14 PM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```


### <a name="certificate-expiration"></a>Expiration du certificat
**System.FabricNode** émet un avertissement quand les certificats utilisés par le nœud de hello sont arrivant à expiration. Chaque nœud comporte trois certificats associés : **Certificate_cluster**, **Certificate_server** et **Certificate_default_client**. Lorsque le délai d’expiration de la hello est au moins deux semaines, état d’intégrité de rapport hello est OK. Lorsque le délai d’expiration de hello est dans les deux semaines, le type de rapport hello est un avertissement. Durée de vie de ces événements est infinie, et ils sont supprimés quand un nœud quitte hello cluster.

* **SourceId**: System.FabricNode
* **Propriété**: commence par **certificat** et contient plus d’informations sur le type de certificat hello
* **Étapes suivantes**: mettre à jour les certificats hello s’ils sont arrivant à expiration.

### <a name="load-capacity-violation"></a>Violation de capacité de charge
Hello équilibrage de charge de l’infrastructure de Service émet un avertissement lorsqu’il détecte une violation de capacité de nœud.

* **SourceId**: System.PLB
* **Property** : commence par **Capacity**
* **Étapes suivantes**: vérification fournies capacité actuelle de métriques et vue hello sur le nœud de hello.

## <a name="application-system-health-reports"></a>Rapports d’intégrité du système sur les applications
**System.CM**, qui représente le service de gestionnaire du Cluster de hello, est l’autorité hello qui gère les informations relatives à une application.

### <a name="state"></a>State
System.CM signale comme OK lorsque l’application hello a été créée ou mis à jour. Il informe magasin de contrôle d’intégrité hello lors de l’application hello a été supprimée, afin qu’il peut être supprimé de la banque.

* **SourceId**: System.CM
* **Property**: State
* **Étapes suivantes**: si l’application hello a été créée ou mis à jour, elle doit inclure un rapport de contrôle d’intégrité hello Gestionnaire du Cluster. Vous pouvez aussi consulter état hello de l’application hello en émettant une requête (par exemple, hello applet de commande PowerShell **ServiceFabricApplication de Get - ApplicationName *applicationName***).

Hello suivant montre l’événement d’état hello sur hello **fabric : / WordCount** application :

```powershell
PS C:\> Get-ServiceFabricApplicationHealth fabric:/WordCount -ServicesFilter None -DeployedApplicationsFilter None -ExcludeHealthStatistics

ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Ok
ServiceHealthStates             : None
DeployedApplicationHealthStates : None
HealthEvents                    : 
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 282
                                  SentAt                : 7/13/2017 5:57:05 PM
                                  ReceivedAt            : 7/14/2017 4:55:10 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 7/13/2017 5:57:05 PM, LastWarning = 1/1/0001 12:00:00 AM
```

## <a name="service-system-health-reports"></a>Rapports d’intégrité du système sur les services
**System.FM**, qui représente le service de gestionnaire de basculement hello, est l’autorité hello qui gère les informations sur les services.

### <a name="state"></a>State
System.FM signale comme OK lorsque hello service a été créé. Supprime les entités hello à partir du magasin de contrôle d’intégrité hello lorsque hello service a été supprimé.

* **SourceId**: System.FM
* **Property**: State

Hello suivant montre l’événement d’état hello sur le service de hello **fabric : / WordCount/WordCountWebService**:

```powershell
PS C:\> Get-ServiceFabricServiceHealth fabric:/WordCount/WordCountWebService -ExcludeHealthStatistics


ServiceName           : fabric:/WordCount/WordCountWebService
AggregatedHealthState : Ok
PartitionHealthStates : 
                        PartitionId           : 8bbcd03a-3a53-47ec-a5f1-9b77f73c53b2
                        AggregatedHealthState : Ok
                        
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 14
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/14/2017 4:55:10 PM
                        TTL                   : Infinite
                        Description           : Service has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="service-correlation-error"></a>Erreur de corrélation de services
**System.PLB** signale une erreur lorsqu’il détecte que la mise à jour d’un toobe de service mis en corrélation avec un autre service crée une chaîne d’affinité. rapport de Hello est désactivée lors de la mise à jour réussie se produit.

* **SourceId**: System.PLB
* **Property** : ServiceDescription
* **Étapes suivantes**: hello de vérification mis en corrélation les descriptions de service.

## <a name="partition-system-health-reports"></a>Rapports d’intégrité du système sur les partitions
**System.FM**, qui représente le service de gestionnaire de basculement hello, est l’autorité hello qui gère les informations sur les partitions de service.

### <a name="state"></a>State
System.FM signale comme OK lors de la partition de hello a été créée et est intègre. Supprime les entités hello à partir du magasin de contrôle d’intégrité hello lorsque hello partition est supprimée.

Si la partition de hello est inférieur à nombre de réplicas minimale hello, il signale une erreur. Si la partition de hello n’est pas sous le nombre de réplicas minimale hello, mais il est sous le nombre de réplicas cible hello, il émet un avertissement. Si la partition de hello est une perte de quorum, System.FM signale une erreur.

Autres événements importants incluent un avertissement lors de la reconfiguration de hello prend plus de temps que prévu, et lors de la génération de hello prend plus longtemps que prévu. fois Hello attendu pour la génération de hello et la reconfiguration sont configurables selon les scénarios de service. Par exemple, si un service dispose d’un téraoctet d’état, telles que de la base de données SQL, génération de hello prend plue d’un service avec une petite quantité d’état.

* **SourceId**: System.FM
* **Property**: State
* **Étapes suivantes**: si l’état d’intégrité hello n’est pas OK, il est possible que certains réplicas n’ont pas été promue, créé ou ouvert tooprimary ou base de données secondaire correctement. Dans de nombreux cas, la cause première hello est un bogue de service dans hello ouverte ou l’implémentation de la modification du rôle.

Bonjour à l’exemple suivant montre une partition intègre :

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountWebService | Get-ServiceFabricPartitionHealth -ExcludeHealthStatistics -ReplicasFilter None

PartitionId           : 8bbcd03a-3a53-47ec-a5f1-9b77f73c53b2
AggregatedHealthState : Ok
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 70
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/14/2017 4:55:10 PM
                        TTL                   : Infinite
                        Description           : Partition is healthy.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

Hello suivant montre la santé d’une partition qui est sous le nombre de réplicas cible hello. étape suivante de Hello est tooget hello description de la partition, ce qui indique la façon dont il est configuré : **MinReplicaSetSize** est trois et **TargetReplicaSetSize** est sept. Puis obtenir nombre hello de nœuds de cluster de hello : cinq. Par conséquent, dans ce cas, deux réplicas ne peut pas être placés, car le nombre de cibles hello de réplicas est supérieur au numéro de hello de nœuds disponibles.

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricPartitionHealth -ReplicasFilter None -ExcludeHealthStatistics


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Warning
                        SequenceNumber        : 123
                        SentAt                : 7/14/2017 4:55:39 PM
                        ReceivedAt            : 7/14/2017 4:55:44 PM
                        TTL                   : Infinite
                        Description           : Partition is below target replica or instance count.
                        fabric:/WordCount/WordCountService 7 2 af2e3e44-a8f8-45ac-9f31-4093eb897600
                          N/S RD _Node_2 Up 131444422260002646
                          N/S RD _Node_4 Up 131444422293113678
                          N/S RD _Node_3 Up 131444422293113679
                          N/S RD _Node_1 Up 131444422293118720
                          N/P RD _Node_0 Up 131444422293118721
                          (Showing 5 out of 5 replicas. Total available replicas: 5.)
                        
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/14/2017 4:55:44 PM, LastOk = 1/1/0001 12:00:00 AM
                        
                        SourceId              : System.PLB
                        Property              : ServiceReplicaUnplacedHealth_Secondary_af2e3e44-a8f8-45ac-9f31-4093eb897600
                        HealthState           : Warning
                        SequenceNumber        : 131445250939703027
                        SentAt                : 7/14/2017 4:58:13 PM
                        ReceivedAt            : 7/14/2017 4:58:14 PM
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
                        FaultDomain:fd:/2 NodeName:_Node_2 NodeType:NodeType2 UpgradeDomain:2 UpgradeDomain: ud:/2 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/1 NodeName:_Node_1 NodeType:NodeType1 UpgradeDomain:1 UpgradeDomain: ud:/1 Deactivation Intent/Status: None/None
                        
                        Existing Primary Replica -- Nodes with Partition's Existing Primary Replica or Secondary Replicas:
                        --
                        FaultDomain:fd:/0 NodeName:_Node_0 NodeType:NodeType0 UpgradeDomain:0 UpgradeDomain: ud:/0 Deactivation Intent/Status: None/None
                        
                        
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/14/2017 4:56:14 PM, LastOk = 1/1/0001 12:00:00 AM

PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | select MinReplicaSetSize,TargetReplicaSetSize

MinReplicaSetSize TargetReplicaSetSize
----------------- --------------------
                2                    7                        

PS C:\> @(Get-ServiceFabricNode).Count
5
```

### <a name="replica-constraint-violation"></a>Violation des contraintes de réplicas
**System.PLB** indique un avertissement s’il détecte une violation des contraintes de réplicas et qu’il ne peut pas placer tous les réplicas de la partition. affichent les détails du rapport Hello les contraintes et les propriétés empêchent le positionnement de réplica hello.

* **SourceId**: System.PLB
* **Property** : commence par **ReplicaConstraintViolation**

## <a name="replica-system-health-reports"></a>Rapports d’intégrité du système sur les réplicas
**System.RA**, qui représente le composant de l’agent de reconfiguration hello, est l’autorité hello pour l’état du réplica hello.

### <a name="state"></a>State
**System.RA** indique OK lorsque hello réplica a été créé.

* **SourceId**: System.RA
* **Property**: State

Bonjour à l’exemple suivant montre un réplica intègre :

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricReplica | where {$_.ReplicaRole -eq "Primary"} | Get-ServiceFabricReplicaHealth

PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422293118721
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131445248920273536
                        SentAt                : 7/14/2017 4:54:52 PM
                        ReceivedAt            : 7/14/2017 4:55:13 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_0
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/14/2017 4:55:13 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="replica-open-status"></a>État d’ouverture du réplica
description de Hello de ce rapport d’intégrité contient l’heure de début de hello (temps universel) lors de l’appel de hello API a été appelé.

**System.RA** émet un avertissement si le réplica hello ouvrir dure plus longtemps que la période de hello configuré (par défaut : 30 minutes). Si hello API a un impact sur la disponibilité du service, les rapports hello sont émise beaucoup plus rapidement (un intervalle peut être configuré avec une valeur par défaut de 30 secondes). Durée Hello mesuré inclut temps hello réplicateur hello ouvert et service hello ouvert. tooOK de modifications de propriété Hello si hello ouvrez se termine.

* **SourceId**: System.RA
* **Property**: **ReplicaOpenStatus**
* **Étapes suivantes**: si l’état d’intégrité hello n’est pas OK, recherchez pourquoi le réplica hello ouvrir prend plus longtemps que prévu.

### <a name="slow-service-api-call"></a>Appel lent d’API de service
**System.RAP** et **System.Replicator** signaler un avertissement si un code de service appel toohello utilisateur prend plu de temps de hello configuré. Avertissement de Hello est désactivée lors de la fin de l’appel hello.

* **SourceId**: System.RAP ou System.Replicator
* **Propriété**: nom hello de l’API de lentes hello. description de Hello fournit plus de détails sur hello de temps hello API a été en attente.
* **Étapes suivantes**: recherchez pourquoi l’appel de hello prend plus de temps que prévu.

Hello, l’exemple suivant montre une partition de perte de quorum et hello enquête étapes faits toofigure pourquoi. Un des réplicas de hello a un état d’avertissement, vous obtenir son intégrité. Il indique qu’opération de service hello l'prend plus longtemps que prévu, un événement signalé par System.RAP. Une fois ces informations sont reçues, étape suivante de hello est toolook au code de service hello et examinez il. Dans ce cas, hello **RunAsync** implémentation d’un service avec état hello lève une exception non gérée. les réplicas Hello sont recyclage, donc vous ne pouvez pas voir tous les réplicas dans un état d’avertissement hello. Vous pouvez réessayer de l’état d’intégrité hello lors de l’obtention et voir les différences dans l’ID de réplica hello. Dans certains cas, les tentatives de hello peuvent vous donner des indices.

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/HelloWorldStatefulApplication/HelloWorldStateful | Get-ServiceFabricPartitionHealth -ExcludeHealthStatistics

PartitionId           : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
AggregatedHealthState : Error
UnhealthyEvaluations  :
                        Error event: SourceId='System.FM', Property='State'.

ReplicaHealthStates   :
                        ReplicaId             : 130743748372546446
                        AggregatedHealthState : Ok

                        ReplicaId             : 130743746168084332
                        AggregatedHealthState : Ok

                        ReplicaId             : 130743746195428808
                        AggregatedHealthState : Warning

                        ReplicaId             : 130743746195428807
                        AggregatedHealthState : Ok

HealthEvents          :
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Error
                        SequenceNumber        : 182
                        SentAt                : 4/24/2015 7:00:17 PM
                        ReceivedAt            : 4/24/2015 7:00:31 PM
                        TTL                   : Infinite
                        Description           : Partition is in quorum loss.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Warning->Error = 4/24/2015 6:51:31 PM

PS C:\> Get-ServiceFabricPartition fabric:/HelloWorldStatefulApplication/HelloWorldStateful

PartitionId            : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
PartitionKind          : Int64Range
PartitionLowKey        : -9223372036854775808
PartitionHighKey       : 9223372036854775807
PartitionStatus        : InQuorumLoss
LastQuorumLossDuration : 00:00:13
MinReplicaSetSize      : 3
TargetReplicaSetSize   : 3
HealthState            : Error
DataLossNumber         : 130743746152927699
ConfigurationNumber    : 227633266688

PS C:\> Get-ServiceFabricReplica 72a0fb3e-53ec-44f2-9983-2f272aca3e38 130743746195428808

ReplicaId           : 130743746195428808
ReplicaAddress      : PartitionId: 72a0fb3e-53ec-44f2-9983-2f272aca3e38, ReplicaId: 130743746195428808
ReplicaRole         : Primary
NodeName            : Node.3
ReplicaStatus       : Ready
LastInBuildDuration : 00:00:01
HealthState         : Warning

PS C:\> Get-ServiceFabricReplicaHealth 72a0fb3e-53ec-44f2-9983-2f272aca3e38 130743746195428808

PartitionId           : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
ReplicaId             : 130743746195428808
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.RAP', Property='ServiceOpenOperationDuration', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 130743756170185892
                        SentAt                : 4/24/2015 7:00:17 PM
                        ReceivedAt            : 4/24/2015 7:00:33 PM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/24/2015 7:00:33 PM

                        SourceId              : System.RAP
                        Property              : ServiceOpenOperationDuration
                        HealthState           : Warning
                        SequenceNumber        : 130743756399407044
                        SentAt                : 4/24/2015 7:00:39 PM
                        ReceivedAt            : 4/24/2015 7:00:59 PM
                        TTL                   : Infinite
                        Description           : Start Time (UTC): 2015-04-24 19:00:17.019
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Warning = 4/24/2015 7:00:59 PM
```

Lorsque vous démarrez application défectueux hello sous le débogueur de hello, windows des événements de diagnostic hello affichent hello une exception à partir de RunAsync :

![Événements de diagnostic Visual Studio 2015 : Échec de RunAsync dans la structure : /HelloWorldStatefulApplication.][1]

Événements de diagnostic Visual Studio 2015 : Échec de RunAsync dans la **structure : /HelloWorldStatefulApplication**.

[1]: ./media/service-fabric-understand-and-troubleshoot-with-system-health-reports/servicefabric-health-vs-runasync-exception.png


### <a name="replication-queue-full"></a>File d’attente de réplication complète
**System.Replicator** émet un avertissement lors de la file d’attente de réplication hello est plein. Sur hello principal, file d’attente de réplication généralement est saturé, car un ou plusieurs réplicas secondaires sont des opérations de tooacknowledge lente. Sur hello secondaire, cela se produit généralement lorsque les service hello est tooapply lentes hello operations. Avertissement de Hello est désactivée lors de la file d’attente hello n’est plus complète.

* **SourceId**: System.Replicator
* **Propriété**: **PrimaryReplicationQueueStatus** ou **SecondaryReplicationQueueStatus**, en fonction du rôle de réplica hello

### <a name="slow-naming-operations"></a>Opérations de nommage lentes
**System.NamingService** signale l’intégrité sur son réplica principal quand une opération de nommage prend trop de temps. [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) et [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) sont des exemples d’opérations de nommage. D’autres méthodes se trouvent sous FabricClient, par exemple dans les [méthodes de gestion de service](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) ou les [méthodes de gestion de propriété](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).

> [!NOTE]
> Hello Naming service résout l’emplacement de tooa de noms de service dans un cluster de hello et permet les propriétés et les noms de service toomanage les utilisateurs. Il s’agit d’un service persistant partitionné Service Fabric. Une des partitions de hello représente hello Authority Owner, qui contient des métadonnées sur tous les services et les noms de Service Fabric. noms de Service Fabric Hello sont des partitions de toodifferent mappé, appelées partitions du nom du propriétaire, le service hello est extensible. En savoir plus sur le [service de nommage](service-fabric-architecture.md).
> 
> 

Quand une opération d’affectation de noms prend plus longtemps que prévu, l’opération de hello est marquée avec un état d’avertissement sur hello *réplica principal de hello d’affectation de noms partition de service qui sert d’opération de hello*. Si l’opération de hello est correctement exécutée, hello avertissement est désactivé. Si l’opération de hello est terminée avec une erreur hello d’intégrité inclut des détails sur les erreurs hello.

* **SourceId**: System.NamingService
* **Propriété**: commence par le préfixe **Duration_** et identifie les opération lente hello et nom de Service Fabric hello sur quel hello opération est appliquée. Par exemple, si créer un service à l’ensemble fibre optique de nom : / MyApp/MyService prend trop de temps, la propriété de hello est Duration_AOCreateService.fabric:/MyApp/MyService. Rôle de toohello AO points Hello partition d’affectation de noms pour ce nom et l’opération.
* **Étapes suivantes**: vérification pourquoi hello d’affectation de noms opération échoue. Chaque opération peut avoir différentes causes principales. Par exemple, supprimez service peut se bloquer sur un nœud, car l’hôte d’application hello conserve en panne sur un nœud en raison du bogue d’utilisateur tooa dans le code de service hello.

Bonjour à l’exemple suivant montre une opération de service de création. opération de Hello a duré plus longtemps que durée de hello configuré. AO nouvelle tentative et envoie le travail tooNO. AUCUNE opération dernière hello terminé avec délai d’attente. Dans ce cas, hello même réplica est principal pour hello AO et aucun rôle.

```powershell
PartitionId           : 00000000-0000-0000-0000-000000001000
ReplicaId             : 131064359253133577
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.NamingService', Property='Duration_AOCreateService.fabric:/MyApp/MyService', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131064359308715535
                        SentAt                : 4/29/2016 8:38:50 PM
                        ReceivedAt            : 4/29/2016 8:39:08 PM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 4/29/2016 8:39:08 PM, LastWarning = 1/1/0001 12:00:00 AM

                        SourceId              : System.NamingService
                        Property              : Duration_AOCreateService.fabric:/MyApp/MyService
                        HealthState           : Warning
                        SequenceNumber        : 131064359526778775
                        SentAt                : 4/29/2016 8:39:12 PM
                        ReceivedAt            : 4/29/2016 8:39:38 PM
                        TTL                   : 00:05:00
                        Description           : hello AOCreateService started at 2016-04-29 20:39:08.677 is taking longer than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM

                        SourceId              : System.NamingService
                        Property              : Duration_NOCreateService.fabric:/MyApp/MyService
                        HealthState           : Warning
                        SequenceNumber        : 131064360657607311
                        SentAt                : 4/29/2016 8:41:05 PM
                        ReceivedAt            : 4/29/2016 8:41:08 PM
                        TTL                   : 00:00:15
                        Description           : hello NOCreateService started at 2016-04-29 20:39:08.689 completed with FABRIC_E_TIMEOUT in more than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM
```

## <a name="deployedapplication-system-health-reports"></a>Rapports d’intégrité du système sur les applications déployées
**System.Hosting** est autorité hello sur les entités déployées.

### <a name="activation"></a>Activation
System.Hosting signale comme OK quand une application a été activée avec succès sur le nœud de hello. Dans le cas contraire, il indique une erreur.

* **SourceId**: System.Hosting
* **Propriété**: l’Activation, y compris la version de déploiement hello
* **Étapes suivantes**: si l’application hello est défectueux, recherchez pourquoi l’activation hello a échoué.

Hello exemple suivant illustre l’activation réussie :

```powershell
PS C:\> Get-ServiceFabricDeployedApplicationHealth -NodeName _Node_1 -ApplicationName fabric:/WordCount -ExcludeHealthStatistics

ApplicationName                    : fabric:/WordCount
NodeName                           : _Node_1
AggregatedHealthState              : Ok
DeployedServicePackageHealthStates : 
                                     ServiceManifestName   : WordCountServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_1
                                     AggregatedHealthState : Ok
                                     
HealthEvents                       : 
                                     SourceId              : System.Hosting
                                     Property              : Activation
                                     HealthState           : Ok
                                     SequenceNumber        : 131445249083836329
                                     SentAt                : 7/14/2017 4:55:08 PM
                                     ReceivedAt            : 7/14/2017 4:55:14 PM
                                     TTL                   : Infinite
                                     Description           : hello application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a>Télécharger
**System.Hosting** signale une erreur si le téléchargement de package d’application hello échoue.

* **SourceId**: System.Hosting
* **Property** : **Download:*RolloutVersion***
* **Étapes suivantes**: recherchez pourquoi le téléchargement de hello a échoué sur le nœud de hello.

## <a name="deployedservicepackage-system-health-reports"></a>Rapports d’intégrité du système sur le package de service déployé
**System.Hosting** est autorité hello sur les entités déployées.

### <a name="service-package-activation"></a>Activation du package de service
System.Hosting signale comme OK si l’activation du package service hello sur le nœud de hello a réussi. Dans le cas contraire, il indique une erreur.

* **SourceId**: System.Hosting
* **Property**: Activation
* **Étapes suivantes**: recherchez pourquoi l’activation hello a échoué.

### <a name="code-package-activation"></a>Activation du package de code
**System.Hosting** signale comme OK pour chaque package de code si hello activation a réussi. Si l’activation de hello échoue, il émet un avertissement, tel que configuré. Si **CodePackage** tooactivate d’échoue ou se termine avec une erreur supérieure hello configuré **CodePackageHealthErrorThreshold**, hébergement signale une erreur. Si un package de service contient plusieurs packages de code, un rapport d’activation est généré pour chacun d’entre eux.

* **SourceId**: System.Hosting
* **Propriété**: préfixe de hello utilise **CodePackageActivation** et contient le nom hello de package de code hello et le point d’entrée hello en tant que  **CodePackageActivation :* CodePackageName*:*SetupEntryPoint/EntryPoint*** (par exemple, **CodePackageActivation:Code:SetupEntryPoint**)

### <a name="service-type-registration"></a>Inscription du type de service
**System.Hosting** signale comme OK si le type de service hello a été correctement enregistré. Il signale une erreur si l’inscription de hello n’était pas terminée dans le temps (tel que configuré à l’aide de **ServiceTypeRegistrationTimeout**). Si l’exécution de hello est fermée, le type de service hello est plus inscrit dans le nœud de hello et hébergement émet un avertissement.

* **SourceId**: System.Hosting
* **Propriété**: préfixe de hello utilise **ServiceTypeRegistration** et contient le nom de type hello service (par exemple, **ServiceTypeRegistration:FileStoreServiceType**)

Bonjour à l’exemple suivant montre un package de service déployé intègre :

```powershell
PS C:\> Get-ServiceFabricDeployedServicePackageHealth -NodeName _Node_1 -ApplicationName fabric:/WordCount -ServiceManifestName WordCountServicePkg


ApplicationName            : fabric:/WordCount
ServiceManifestName        : WordCountServicePkg
ServicePackageActivationId : 
NodeName                   : _Node_1
AggregatedHealthState      : Ok
HealthEvents               : 
                             SourceId              : System.Hosting
                             Property              : Activation
                             HealthState           : Ok
                             SequenceNumber        : 131445249084026346
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : hello ServicePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : CodePackageActivation:Code:EntryPoint
                             HealthState           : Ok
                             SequenceNumber        : 131445249084306362
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : hello CodePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : ServiceTypeRegistration:WordCountServiceType
                             HealthState           : Ok
                             SequenceNumber        : 131445249088096842
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : hello ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a>Télécharger
**System.Hosting** signale une erreur si le téléchargement du package hello service échoue.

* **SourceId**: System.Hosting
* **Property** : **Download:*RolloutVersion***
* **Étapes suivantes**: recherchez pourquoi le téléchargement de hello a échoué sur le nœud de hello.

### <a name="upgrade-validation"></a>Validation de mise à niveau
**System.Hosting** signale une erreur si la validation pendant la mise à niveau hello échoue ou si hello mise à niveau échoue sur le nœud de hello.

* **SourceId**: System.Hosting
* **Propriété**: préfixe de hello utilise **FabricUpgradeValidation** et contient la version de mise à niveau hello
* **Description**: erreur toohello de pointe

## <a name="next-steps"></a>Étapes suivantes
[Affichage rapports d’intégrité de Service Fabric](service-fabric-view-entities-aggregated-health.md)

[Comment tooreport et vérification du service d’intégrité](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[Surveiller et diagnostiquer les services localement](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Mise à niveau des applications Service Fabric](service-fabric-application-upgrade.md)

