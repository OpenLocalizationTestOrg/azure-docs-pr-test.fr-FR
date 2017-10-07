---
title: "gestion d’état aaaReliable acteurs | Documents Microsoft"
description: "Décrit la manière dont l’état de Reliable Actors est géré, conservé et répliqué pour garantir une haute disponibilité."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 37cf466a-5293-44c0-a4e0-037e5d292214
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 346d92426b1890617d108a9504afb179e463bded
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-actors-state-management"></a>Gestion des états de Reliable Actors
Reliable Actors désignent des objets monothread capables d’encapsuler la logique et l’état. Acteurs exécutés sur des Services fiables, ils peuvent conserver leur état fiable à l’aide de hello les mêmes mécanismes de réplication et de persistance qui utilise des Services fiables. De cette manière, les acteurs ne perdent pas leur état après des incidents, à la réactivation après le garbage collection ou qu’ils sont déplacés entre les nœuds dans un cluster en raison de l’équilibrage de la tooresource ou mises à niveau.

## <a name="state-persistence-and-replication"></a>Persistance et réplication de l’état
Tous les intervenants fiable sont considérés comme *avec état* , car chaque instance de l’acteur mappe les ID tooa unique. Cela signifie que toohello des appels répétés même acteur ID sont acheminés toohello même instance d’acteur. Dans un système sans état, en revanche, les appels de client ne sont pas garantis toobe routé toohello même serveur chaque fois. Pour cette raison, les services d’acteur sont toujours des services avec état.

Même si les acteurs sont considérés comme des services avec état, cela ne signifie pas qu’ils doivent stocker l’état de manière fiable. Acteurs peuvent choisir le niveau hello de persistance de l’état et la réplication basée sur leurs données, les exigences de stockage :

* **État persistant**: état est persistante toodisk et est répliqué too3 ou plusieurs réplicas. Il s’agit d’une option de stockage pour état durable plus de hello, où l’état peut être rendue persistante via l’arrêt de la création du cluster.
* **Un état volatile**: état est répliquée too3 ou plusieurs réplicas et conservée uniquement en mémoire. Cette option garantit une résilience contre les défaillances de nœud et d’acteur, ainsi que pendant les mises à niveau et l’équilibrage des ressources. Toutefois, l’état n’est pas persistante toodisk. Si tous les réplicas sont perdus à la fois, état de hello sont également perdue.
* **Aucun état persistant**: état n’est pas répliqué ou écrit toodisk. Ce niveau est pour les acteurs qui ne suffit toomaintain état fiable.

Chaque niveau de persistance représente simplement une autre configuration du *fournisseur d’état* et de la *réplication* de votre service. État est écrit ou non toodisk dépend de fournisseur d’état hello--composant hello dans un service fiable qui stocke l’état. La réplication varie selon le nombre de réplicas avec lesquels est déployé un service. Comme avec les Services fiables, les deux hello fournisseur d’état et nombre de réplicas peut aisément être défini manuellement. infrastructure d’acteur Hello fournit un attribut, lorsqu’il est utilisé sur un acteur, sélectionne automatiquement un fournisseur d’état par défaut et génère automatiquement les paramètres de réplica nombre tooachieve, un de ces trois paramètres de persistance. attribut StatePersistence de Hello n’est pas hérité par la classe dérivée, chaque type d’acteur doit fournir son niveau de StatePersistence.

### <a name="persisted-state"></a>État persistant
```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl  extends FabricActor implements MyActor
{
}
```  
Ce paramètre utilise un fournisseur d’état qui stocke les données sur disque et définit automatiquement too3 de nombre de réplicas de service hello.

### <a name="volatile-state"></a>État volatil
```csharp
[StatePersistence(StatePersistence.Volatile)]
class MyActor : Actor, IMyActor
{
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Volatile)
class MyActorImpl extends FabricActor implements MyActor
{
}
```
Ce paramètre utilise un fournisseur d’état dans-uniquement en mémoire et jeux hello too3 nombre de réplicas.

### <a name="no-persisted-state"></a>État non persistant
```csharp
[StatePersistence(StatePersistence.None)]
class MyActor : Actor, IMyActor
{
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.None)
class MyActorImpl extends FabricActor implements MyActor
{
}
```
Ce paramètre utilise un fournisseur d’état dans-uniquement en mémoire et jeux hello too1 nombre de réplicas.

### <a name="defaults-and-generated-settings"></a>Valeurs par défaut et paramètres générés
Lorsque vous utilisez hello `StatePersistence` attribut, un fournisseur d’état est sélectionné automatiquement lors de l’exécution au démarrage du service d’acteur hello. nombre de réplicas Hello, toutefois, est défini au moment de la compilation par hello acteur de Visual Studio des outils de génération. Hello outils de génération de génèrent automatiquement un *service par défaut* pour le service d’acteur hello dans ApplicationManifest.xml. Les paramètres sont créés pour la **taille minimale du jeu de réplicas** et la **taille cible du jeu de réplicas**.

Vous pouvez modifier ces paramètres manuellement. Mais chaque hello temps `StatePersistence` attribut est modifié, les paramètres de hello sont définis toohello réplica ensemble taille par défaut pour hello sélectionné `StatePersistence` attribut, en remplaçant toutes les valeurs précédentes. En d’autres termes, les valeurs hello que vous définissez dans ServiceManifest.xml sont *uniquement* remplacée au moment de la génération lorsque vous modifiez hello `StatePersistence` valeur d’attribut.

```xml
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="Application12Type" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Parameters>
      <Parameter Name="MyActorService_PartitionCount" DefaultValue="10" />
      <Parameter Name="MyActorService_MinReplicaSetSize" DefaultValue="3" />
      <Parameter Name="MyActorService_TargetReplicaSetSize" DefaultValue="3" />
   </Parameters>
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyActorPkg" ServiceManifestVersion="1.0.0" />
   </ServiceManifestImport>
   <DefaultServices>
      <Service Name="MyActorService" GeneratedIdRef="77d965dc-85fb-488c-bd06-c6c1fe29d593|Persisted">
         <StatefulService ServiceTypeName="MyActorServiceType" TargetReplicaSetSize="[MyActorService_TargetReplicaSetSize]" MinReplicaSetSize="[MyActorService_MinReplicaSetSize]">
            <UniformInt64Partition PartitionCount="[MyActorService_PartitionCount]" LowKey="-9223372036854775808" HighKey="9223372036854775807" />
         </StatefulService>
      </Service>
   </DefaultServices>
</ApplicationManifest>
```

## <a name="state-manager"></a>Gestionnaire d’état
Chaque instance d’acteur possède son propre gestionnaire d’état, c’est-à-dire une structure de données de type dictionnaire qui stocke les paires clé/valeur de manière fiable. Gestionnaire d’état Hello est un wrapper autour d’un fournisseur d’état. Vous pouvez l’utiliser toostore données quel que soit le paramètre de persistance est utilisé. Il ne fournit pas toutes les garanties qu’un service d’acteur en cours d’exécution peut être modifié à partir d’un tooa de paramètre rémanente (en mémoire-uniquement) persistant paramètre via une mise à niveau propagée, tout en conservant les données d’état. Toutefois, il est possible toochange nombre de réplica pour un service en cours d’exécution.

Les clés de gestionnaire d’état doivent être des chaînes. Les valeurs sont génériques et peuvent être de n’importe quel type, y compris de types personnalisés. Valeurs stockées dans le Gestionnaire d’état hello doivent être de contrat de données sérialisable, car elles peuvent être transmises sur des nœuds de tooother hello réseau pendant la réplication et peuvent être écrits toodisk, selon le paramètre de persistance d’état d’un acteur.

Gestionnaire d’état Hello expose les méthodes courantes de dictionnaire pour la gestion d’état, semblable toothose trouvé dans le dictionnaire fiable.

### <a name="accessing-state"></a>Accès à l’état
État est accessible via le Gestionnaire d’état hello par clé. Les méthodes du gestionnaire d’état sont toutes asynchrones, car elles peuvent nécessiter des E/S disque lorsque les acteurs sont à l’état persistant. Lors du premier accès, les objets d’état sont mis en mémoire cache. Les opérations d’accès répétées permettent d’accéder aux objets directement à partir de la mémoire et sont retournées de façon synchrone sans entraîner d’E/S disque ou de surcharge asynchrone en cas de changement de contexte. Un objet d’état est supprimé à partir du cache hello hello suivant cas :

* Une méthode d’acteur lève une exception non gérée une fois qu’il extrait un objet de gestionnaire d’état hello.
* Un acteur est réactivé soit après avoir été désactivé, soit en raison d’un échec.
* pages de fournisseurs d’état Hello toodisk d’état. Ce comportement dépend de l’implémentation de fournisseur d’état hello. fournisseur d’état par défaut Hello hello `Persisted` paramètre a ce comportement.

Vous pouvez récupérer l’état à l’aide d’une norme *obtenir* opération lève `KeyNotFoundException`(c#) ou `NoSuchElementException`(Java) si une entrée n’existe pas de clé de hello :

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<int> GetCountAsync()
    {
        return this.StateManager.GetStateAsync<int>("MyState");
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture<Integer> getCountAsync()
    {
        return this.stateManager().getStateAsync("MyState");
    }
}
```

Vous pouvez également récupérer l’état à l’aide d’une opération *TryGet* qui ne lève pas d’exception s’il n’existe aucune entrée pour la clé :

```csharp
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public async Task<int> GetCountAsync()
    {
        ConditionalValue<int> result = await this.StateManager.TryGetStateAsync<int>("MyState");
        if (result.HasValue)
        {
            return result.Value;
        }

        return 0;
    }
}
```
```Java
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture<Integer> getCountAsync()
    {
        return this.stateManager().<Integer>tryGetStateAsync("MyState").thenApply(result -> {
            if (result.hasValue()) {
                return result.getValue();
            } else {
                return 0;
            });
    }
}
```

### <a name="saving-state"></a>Enregistrement de l’état
méthodes de récupération du gestionnaire Hello état retournent un objet de tooan de référence dans la mémoire locale. Modification de cet objet dans la mémoire locale uniquement ne provoque pas il toobe enregistré de façon durable. Lorsqu’un objet est récupéré à partir du Gestionnaire d’état hello et modifié, il doit être réinséré hello état manager toobe enregistré de façon durable.

Vous pouvez insérer l’état à l’aide un inconditionnel *définir*, qui est hello équivalent de hello `dictionary["key"] = value` syntaxe :

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task SetCountAsync(int value)
    {
        return this.StateManager.SetStateAsync<int>("MyState", value);
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture setCountAsync(int value)
    {
        return this.stateManager().setStateAsync("MyState", value);
    }
}
```

Vous pouvez ajouter l’état en utilisant une méthode *Add*. Cette méthode lève `InvalidOperationException`(c#) ou `IllegalStateException`(Java) quand il tente de tooadd une clé qui existe déjà.

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task AddCountAsync(int value)
    {
        return this.StateManager.AddStateAsync<int>("MyState", value);
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture addCountAsync(int value)
    {
        return this.stateManager().addOrUpdateStateAsync("MyState", value, (key, old_value) -> old_value + value);
    }
}
```

Vous pouvez également ajouter l’état en utilisant une méthode *TryAdd*. Cette méthode ne lève pas quand il tente de tooadd une clé qui existe déjà.

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public async Task AddCountAsync(int value)
    {
        bool result = await this.StateManager.TryAddStateAsync<int>("MyState", value);

        if (result)
        {
            // Added successfully!
        }
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture addCountAsync(int value)
    {
        return this.stateManager().tryAddStateAsync("MyState", value).thenApply((result)->{
            if(result)
            {
                // Added successfully!
            }
        });
    }
}
```

Extrémité hello d’une méthode d’acteur, gestionnaire d’état hello enregistre automatiquement toutes les valeurs qui ont été ajoutées ou modifiées par une opération insert ou update. Un « Enregistrer » peut inclure toodisk persistante et la réplication, en fonction des paramètres hello utilisé. Les valeurs qui n’ont pas été modifiées ne sont pas conservées ou répliquées. Si aucune valeur n’ont été modifiés, hello opération d’enregistrement ne fait rien. Si l’enregistrement échoue, hello état modifié est ignoré et état d’origine de hello est rechargé.

Vous pouvez également enregistrer état manuellement en appelant hello `SaveStateAsync` méthode sur acteur hello base :

```csharp
async Task IMyActor.SetCountAsync(int count)
{
    await this.StateManager.AddOrUpdateStateAsync("count", count, (key, value) => count > value ? count : value);

    await this.SaveStateAsync();
}
```
```Java
interface MyActor {
    CompletableFuture setCountAsync(int count)
    {
        this.stateManager().addOrUpdateStateAsync("count", count, (key, value) -> count > value ? count : value).thenApply();

        this.stateManager().saveStateAsync().thenApply();
    }
}
```

### <a name="removing-state"></a>Suppression de l’état
Vous pouvez supprimer état définitivement à partir du Gestionnaire d’état d’un acteur en appelant hello *supprimer* (méthode). Cette méthode lève `KeyNotFoundException`(c#) ou `NoSuchElementException`(Java) quand il tente de tooremove une clé qui n’existe pas.

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task RemoveCountAsync()
    {
        return this.StateManager.RemoveStateAsync("MyState");
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture removeCountAsync()
    {
        return this.stateManager().removeStateAsync("MyState");
    }
}
```

Vous pouvez également supprimer définitivement état à l’aide de hello *TryRemove* (méthode). Cette méthode ne lève pas quand il tente de tooremove une clé qui n’existe pas.

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public async Task RemoveCountAsync()
    {
        bool result = await this.StateManager.TryRemoveStateAsync("MyState");

        if (result)
        {
            // State removed!
        }
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture removeCountAsync()
    {
        return this.stateManager().tryRemoveStateAsync("MyState").thenApply((result)->{
            if(result)
            {
                // State removed!
            }
        });
    }
}
```

## <a name="next-steps"></a>Étapes suivantes

État qui est stocké dans Reliable Actors doit être sérialisé avant son toodisk écrite et répliquée pour la haute disponibilité. En savoir plus sur [Sérialisation du type d’acteur](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).

Ensuite, en savoir plus sur l’[analyse des performances et des diagnostics des acteurs](service-fabric-reliable-actors-diagnostics.md).
