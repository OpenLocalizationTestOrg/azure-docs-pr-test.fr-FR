---
title: "échecs d’aaaSimulate dans Azure microservices | Documents Microsoft"
description: "Cet article traite sur les actions de testabilité hello trouvées dans Microsoft Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: motanv
manager: timlt
editor: toddabel
ms.assetid: ed53ca5c-4d5e-4b48-93c9-e386f32d8b7a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: motanv;heeldin
ms.openlocfilehash: 5bdda1c0c5a40b243ab956c4791afd52e11c4089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="testability-actions"></a>Actions de testabilité
Dans l’ordre toosimulate une infrastructure fiable, Azure Service Fabric fournit, hello pour le développeur toosimulate de façons différentes défaillances réelles et les transitions d’état. Elles sont exposées en tant qu’actions de testabilité. actions de Hello sont hello API de bas niveau qui provoquent une injection d’erreurs spécifiques, la transition d’état ou la validation. En combinant ces actions, vous êtes en mesure d’écrire des scénarios de test complets pour vos services.

Service Fabric fournit en standard des scénarios courants de test, constitués de ces actions. Nous recommandons vivement que vous utilisez ces scénarios intégrés, qui sont choisies avec soin les transitions d’état commun tootest et cas d’échec. Toutefois, les actions peuvent être des scénarios de test personnalisée toocreate utilisé lorsque vous souhaitez que la couverture du tooadd pour les scénarios qui ne relèvent pas des scénarios intégrés hello encore ou qui sont personnalisés adaptés à votre application.

Les implémentations c# des actions de hello sont trouvent dans hello System.Fabric.dll assembly. module PowerShell de l’infrastructure de système de Hello se trouve dans hello Microsoft.ServiceFabric.Powershell.dll assembly. Dans le cadre de l’installation du runtime, hello module ServiceFabric PowerShell est installé tooallow de facilité d’utilisation.

## <a name="graceful-vs-ungraceful-fault-actions"></a>Actions d’erreurs avec et sans perte de données
Les actions de testabilité sont répertoriées en deux groupes principaux :

* Erreurs avec perte de données : ces erreurs simulent des défaillances comme les redémarrages de machines ou les incidents de processus. Dans ce cas d’échecs, contexte d’exécution hello du processus s’arrête brusquement. Cela signifie qu'aucun nettoyage de l’état de hello ne peut s’exécuter avant l’application hello redémarre.
* Erreurs sans perte de données : ces erreurs simulent des actions comme des déplacements ou des abandons de réplicas provoqués par l’équilibrage de la charge. Dans ce cas, service de hello Obtient une notification de hello fermer et pouvez nettoyer l’état de hello avant de quitter.

Pour la validation de meilleure qualité, exécuter le service de hello et charge de travail entreprise tout en INDUISANT différents normale et anormal des erreurs. Erreurs anormal couvrir des scénarios où hello service processus s’arrête brusquement au milieu de hello de certains flux de travail. Ce test chemin de récupération hello une fois que le réplica de service hello est restaurée par l’infrastructure de Service. Cela permet de tester la cohérence des données et si l’état du service hello est maintenue correctement après des incidents. Hello autre ensemble d’échecs (hello normale) tester que le service de hello réagit correctement tooreplicas déplacés ce par l’infrastructure de Service. Cette commande teste la gestion de l’annulation dans la méthode de RunAsync hello. service de Hello doit toocheck pour hello annulation jeton qui est défini correctement enregistrer son état et quitte la méthode de RunAsync hello.

## <a name="testability-actions-list"></a>Liste des actions de testabilité
| Action | Description | API gérée | Applet de commande PowerShell | Erreurs sans/avec perte de données |
| --- | --- | --- | --- | --- |
| CleanTestState |Supprime tous les États de test hello cluster hello en cas d’un arrêt incorrect du pilote de test hello. |CleanTestStateAsync |Remove-ServiceFabricTestState |Non applicable |
| InvokeDataLoss |Provoque une perte de données dans une partition de service. |InvokeDataLossAsync |Invoke-ServiceFabricPartitionDataLoss |Sans perte de données |
| InvokeQuorumLoss |Entraîne une perte de quorum dans une partition considérée de service avec état. |InvokeQuorumLossAsync |Invoke-ServiceFabricQuorumLoss |Sans perte de données |
| MovePrimary |Déplace hello spécifié le réplica principal d’un nœud de cluster spécifié toohello service avec état. |MovePrimaryAsync |Move-ServiceFabricPrimaryReplica |Sans perte de données |
| MoveSecondary |Déplace le réplica secondaire de hello actuel d’un nœud de cluster différent tooa service avec état. |MoveSecondaryAsync |Move-ServiceFabricSecondaryReplica |Sans perte de données |
| RemoveReplica |Simule une défaillance de réplica en supprimant un réplica d’un cluster. Cela ferme le réplica de hello et il passera toorole 'None', supprimant tous de l’état du cluster de hello. |RemoveReplicaAsync |Remove-ServiceFabricReplica |Sans perte de données |
| RestartDeployedCodePackage |Simule une défaillance de processus de package de code en redémarrant un package de code déployé sur un nœud de cluster. Cela annule les processus du package de code hello, qui va redémarrer tous les réplicas de service d’utilisateur hello hébergés dans ce processus. |RestartDeployedCodePackageAsync |Restart-ServiceFabricDeployedCodePackage |Avec perte de données |
| RestartNode |Simule la défaillance d’un nœud de cluster Service Fabric en redémarrant un nœud. |RestartNodeAsync |Restart-ServiceFabricNode |Avec perte de données |
| RestartPartition |Simule un scénario d’indisponibilité de centre de données ou de cluster en redémarrant certains des réplicas d’une partition, ou tous ces réplicas. |RestartPartitionAsync |Restart-ServiceFabricPartition |Sans perte de données |
| RestartReplica |Simule un échec de réplication par le redémarrage d’un réplica persistant dans un cluster, fermeture de réplica de hello et puis de le rouvrir. |RestartReplicaAsync |Restart-ServiceFabricReplica |Sans perte de données |
| StartNode |Démarre un nœud dans un cluster déjà arrêté. |StartNodeAsync |Start-ServiceFabricNode |Non applicable |
| StopNode |Simule une défaillance de nœud en arrêtant un nœud dans un cluster. nœud de Hello restera vers le bas jusqu'à ce que StartNode est appelée. |StopNodeAsync |Stop-ServiceFabricNode |Avec perte de données |
| ValidateApplication |Valide l’intégrité de tous les services de l’infrastructure de Service dans une application, généralement après induire des erreurs dans le système de hello et la disponibilité de hello. |ValidateApplicationAsync |Test-ServiceFabricApplication |Non applicable |
| ValidateService |Valide la disponibilité de hello et l’intégrité d’un service Service Fabric, généralement après induire des erreurs dans le système de hello. |ValidateServiceAsync |Test-ServiceFabricService |Non applicable |

## <a name="running-a-testability-action-using-powershell"></a>Exécution d’une action de testabilité à l’aide de PowerShell
Ce didacticiel vous montre comment toorun une action de test à l’aide de PowerShell. Vous allez apprendre comment toorun une action de test par rapport à un cluster (une case) local ou un cluster Azure. Microsoft.Fabric.Powershell.dll--hello Service Fabric module PowerShell--est installé automatiquement lorsque vous installez hello MSI de l’infrastructure de Service de Microsoft. module de Hello est chargé automatiquement lorsque vous ouvrez une invite de commandes PowerShell.

Sections du didacticiel :

* [Exécuter une action dans un cluster à boîtier unique](#run-an-action-against-a-one-box-cluster)
* [Exécuter une action dans un cluster Microsoft Azure](#run-an-action-against-an-azure-cluster)

### <a name="run-an-action-against-a-one-box-cluster"></a>Exécuter une action dans un cluster à boîtier unique
toorun une action de test par rapport à un cluster local, connectez-vous d’abord toohello cluster et l’invite de commandes PowerShell hello ouvert en mode administrateur. Examinons hello **ServiceFabricNode de redémarrage** action.

```powershell
Restart-ServiceFabricNode -NodeName Node1 -CompletionMode DoNotVerify
```

Ici hello action **ServiceFabricNode de redémarrage** est en cours d’exécution sur un nœud nommé « Node1 ». mode de saisie semi-automatique Hello Spécifie qu’il ne doit pas vérifier si action de redémarrage-nœud hello a réussi. Mode de saisie semi-automatique hello en spécifiant en tant que « Vérifier » entraînera tooverify si l’action de redémarrage hello a réussi. Au lieu de spécifier directement le nœud de hello par son nom, vous pouvez spécifier via un type de clé et hello partition du réplica, comme suit :

```powershell
Restart-ServiceFabricNode -ReplicaKindPrimary  -PartitionKindNamed -PartitionKey Partition3 -CompletionMode Verify
```


```powershell
$connection = "localhost:19000"
$nodeName = "Node1"

Connect-ServiceFabricCluster $connection
Restart-ServiceFabricNode -NodeName $nodeName -CompletionMode DoNotVerify
```

**Redémarrage-ServiceFabricNode** doit être toorestart utilisé un nœud de l’infrastructure de Service dans un cluster. Cette commande arrête le processus de Fabric.exe hello, qui va redémarrer tous hello système utilisateur et service service réplicas hébergés sur ce nœud. Votre service à l’aide de cette tootest API permet de découvrir des bogues sur les chemins de récupération de basculement hello. Il permet de simuler des défaillances de nœud de cluster de hello.

Hello capture d’écran suivante montre hello **ServiceFabricNode de redémarrage** commande testabilité en action.

![](media/service-fabric-testability-actions/Restart-ServiceFabricNode.png)

Hello de sortie de hello tout d’abord **Get-ServiceFabricNode** (une applet de commande du module PowerShell de l’infrastructure de Service de hello) indique que le cluster local hello comporte cinq nœuds : Node.1 tooNode.5. Après l’action de testabilité hello (applet de commande) **ServiceFabricNode de redémarrage** est exécutée sur le nœud de hello, nommé Node.4, nous voyons les temps de fonctionnement de ce nœud hello a été réinitialisé.

### <a name="run-an-action-against-an-azure-cluster"></a>Exécuter une action dans un cluster Microsoft Azure
Exécute une action de testabilité (à l’aide de PowerShell) par rapport à un cluster Azure est la même action de hello toorunning par rapport à un cluster local. Hello seule différence est que, avant de pouvoir exécuter action hello, au lieu de la connexion cluster local toohello, vous devez tooconnect toohello Azure tout d’abord de cluster.

## <a name="running-a-testability-action-using-c35"></a>Exécution d’une action de testabilité à l’aide de C&#35;
toorun une action de test à l’aide de c#, vous devez tooconnect toohello cluster à l’aide de fabricclient ne. Puis obtenir hello paramètres nécessaires toorun hello action. Différents paramètres peuvent être utilisés toorun hello même action.
Consulte hello action RestartServiceFabricNode, toorun monodirectionnelle, il est à l’aide des informations sur les nœuds hello (nom de nœud et ID d’instance de nœud) dans le cluster de hello.

```csharp
RestartNodeAsync(nodeName, nodeInstanceId, completeMode, operationTimeout, CancellationToken.None)
```

Explications de paramètres :

* **CompleteMode** Spécifie que le mode hello ne doit pas vérifier si action de redémarrage hello a réussi. Mode de saisie semi-automatique hello en spécifiant en tant que « Vérifier » entraînera tooverify si l’action de redémarrage hello a réussi.  
* **OperationTimeout** jeux hello laps de temps hello opération toofinish avant qu’une exception TimeoutException est levée.
* **CancellationToken** permet un toobe en attente d’appel annulé.

Au lieu de spécifier directement le nœud de hello par son nom, vous pouvez spécifier via un type de clé et hello de partition de réplica.

Pour plus d’informations, consultez la section [Sélecteur de partitions et sélecteur de réplicas](#partition_replica_selector).

```csharp
// Add a reference tooSystem.Fabric.Testability.dll and System.Fabric.dll
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Fabric.Testability;
using System.Fabric;
using System.Threading;
using System.Numerics;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";
        Uri serviceName = new Uri("fabric:/samples/PersistentToDoListApp/PersistentToDoListService");
        string nodeName = "N0040";
        BigInteger nodeInstanceId = 130743013389060139;

        Console.WriteLine("Starting RestartNode test");
        try
        {
            //Restart hello node by using ReplicaSelector
            RestartNodeAsync(clusterConnection, serviceName).Wait();

            //Another way toorestart node is by using nodeName and nodeInstanceId
            RestartNodeAsync(clusterConnection, nodeName, nodeInstanceId).Wait();
        }
        catch (AggregateException exAgg)
        {
            Console.WriteLine("RestartNode did not complete: ");
            foreach (Exception ex in exAgg.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("RestartNode completed.");
        return 0;
    }

    static async Task RestartNodeAsync(string clusterConnection, Uri serviceName)
    {
        PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);
        ReplicaSelector primaryofReplicaSelector = ReplicaSelector.PrimaryOf(randomPartitionSelector);

        // Create FabricClient with connection and security information here
        FabricClient fabricclient = new FabricClient(clusterConnection);
        await fabricclient.FaultManager.RestartNodeAsync(primaryofReplicaSelector, CompletionMode.Verify);
    }

    static async Task RestartNodeAsync(string clusterConnection, string nodeName, BigInteger nodeInstanceId)
    {
        // Create FabricClient with connection and security information here
        FabricClient fabricclient = new FabricClient(clusterConnection);
        await fabricclient.FaultManager.RestartNodeAsync(nodeName, nodeInstanceId, CompletionMode.Verify);
    }
}
```

## <a name="partitionselector-and-replicaselector"></a>Sélecteur de partitions et sélecteur de réplicas
### <a name="partitionselector"></a>PartitionSelector
PartitionSelector est une application d’assistance exposée dans la testabilité et est utilisé tooselect spécifique de partition sur le tooperform une des actions de testabilité hello. Il peut être utilisé tooselect une partition spécifique si les ID de partition hello est connu au préalable. Ou, vous pouvez fournir la clé de partition hello et opération de hello peut résoudre les ID de partition hello en interne. Vous avez également option hello de sélection d’une partition aléatoire.

toouse ce programme d’assistance, créer l’objet de PartitionSelector hello et sélectionnez hello partition en utilisant l’une des méthodes de hello Select *. Passez dans hello PartitionSelector objet toohello API qui le requiert. Si aucune option n’est sélectionnée, la valeur par défaut partition aléatoire de tooa.

```csharp
Uri serviceName = new Uri("fabric:/samples/InMemoryToDoListApp/InMemoryToDoListService");
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
string partitionName = "Partition1";
Int64 partitionKeyUniformInt64 = 1;

// Select a random partition
PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);

// Select a partition based on ID
PartitionSelector partitionSelectorById = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);

// Select a partition based on name
PartitionSelector namedPartitionSelector = PartitionSelector.PartitionKeyOf(serviceName, partitionName);

// Select a partition based on partition key
PartitionSelector uniformIntPartitionSelector = PartitionSelector.PartitionKeyOf(serviceName, partitionKeyUniformInt64);
```

### <a name="replicaselector"></a>ReplicaSelector
ReplicaSelector est une application d’assistance exposée dans la testabilité et est utilisé toohelp sélectionnez un réplica sur le tooperform une des actions de testabilité hello. Il peut être utilisé tooselect un réplica spécifique si les ID de réplica hello est connu au préalable. En outre, vous pouvez hello en sélectionnant un réplica principal ou secondaire aléatoire. ReplicaSelector dérive PartitionSelector, donc vous devez tooselect deux hello hello et réplica de partition sur laquelle vous souhaitez l’opération de testabilité tooperform hello.

toouse ce programme d’assistance, créez un objet de ReplicaSelector et définissez hello librement tooselect hello réplica et hello partition. Vous pouvez puis passez-la dans hello API qui le requiert. Si aucune option n’est sélectionnée, la valeur par défaut réplica aléatoire de tooa et partition aléatoire.

```csharp
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);
long replicaId = 130559876481875498;

// Select a random replica
ReplicaSelector randomReplicaSelector = ReplicaSelector.RandomOf(partitionSelector);

// Select hello primary replica
ReplicaSelector primaryReplicaSelector = ReplicaSelector.PrimaryOf(partitionSelector);

// Select hello replica by ID
ReplicaSelector replicaByIdSelector = ReplicaSelector.ReplicaIdOf(partitionSelector, replicaId);

// Select a random secondary replica
ReplicaSelector secondaryReplicaSelector = ReplicaSelector.RandomSecondaryOf(partitionSelector);
```

## <a name="next-steps"></a>Étapes suivantes
* [Scénarios de testabilité](service-fabric-testability-scenarios.md)
* Comment tootest votre service
  * [Simuler des défaillances au cours des charges de travail de services](service-fabric-testability-workload-tests.md)
  * [Échecs de communication de service à service](service-fabric-testability-scenarios-service-communication.md)

