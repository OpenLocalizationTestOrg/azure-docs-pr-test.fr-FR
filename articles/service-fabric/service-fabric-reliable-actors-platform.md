---
title: aaaReliable acteurs sur Service Fabric | Documents Microsoft
description: "Décrit comment Reliable Actors sont posés en couches sur des Services fiables et utiliser les fonctionnalités de hello de plateforme de Service Fabric hello."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: amanbha
ms.assetid: 45839a7f-0536-46f1-ae2b-8ba3556407fb
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: vturecek
ms.openlocfilehash: ecffb54139f1171c7839b77fed0be60950881198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-reliable-actors-use-hello-service-fabric-platform"></a>Comment Reliable Actors utiliser hello Service Fabric
Cet article explique le fonctionnement des acteurs fiable sur la plateforme Azure Service Fabric de hello. Reliable Actors s’exécutent dans une infrastructure qui est hébergée dans une implémentation d’un service fiable avec état appelée hello *service d’acteur*. service d’acteur Hello contient tous les cycle de vie hello composants nécessaires toomanage hello et un message destiné à votre acteurs :

* Hello acteur Runtime gère le cycle de vie, le garbage collection et applique l’accès de thread unique.
* Un écouteur de la communication à distance d’acteur service accepte tooactors des appels de l’accès à distance et les envoie instance de tooa répartiteur tooroute toohello acteur approprié.
* Hello fournisseur d’état acteur encapsule les fournisseurs d’état (par exemple, le fournisseur d’état de Collections fiable hello) et fournit un adaptateur pour la gestion d’état acteur.

Ces framework Reliable Actor de composants forment hello.

## <a name="service-layering"></a>Couches de service
Étant donné que le service d’acteur hello lui-même est un service fiable, tous les hello [modèle d’application](service-fabric-application-model.md), cycle de vie, [empaquetage](service-fabric-package-apps.md), [déploiement](service-fabric-deploy-remove-applications.md), mettre à niveau et mise à l’échelle des concepts de Services fiables appliquent hello même tooactor façon dont les services. 

![Superposition de service d’acteur][1]

Hello diagramme précédent montre relation hello entre les infrastructures d’application Service Fabric hello et code utilisateur. Éléments bleus représentent l’infrastructure d’application des Services fiables hello, orange représente le framework d’acteur fiable hello et verte représente le code utilisateur.

Dans les Services fiables, votre service hérite hello `StatefulService` classe. Cette classe est dérivée de `StatefulServiceBase` (ou `StatelessService` pour les services sans état). Dans Reliable Actors, vous utilisez service d’acteur hello. service d’acteur Hello est une implémentation différente de hello `StatefulServiceBase` classe ce modèle d’acteur hello implémente où votre acteurs exécutent. Étant donné que le service d’acteur hello lui-même est simplement une implémentation de `StatefulServiceBase`, vous pouvez écrire votre propre service qui dérive de `ActorService` et fonctionnalités de niveau de service implémentent hello même façon que lors de l’héritage `StatefulService`, telles que :

* Sauvegarde et restauration du service.
* Fonctionnalité partagée par tous les acteurs. Par exemple, un disjoncteur.
* Appels de procédure distante sur le service d’acteur hello proprement dit et sur chaque acteur individuel.

> [!NOTE]
> Actuellement, les services avec état ne sont pas pris en charge par Java / Linux.

### <a name="using-hello-actor-service"></a>À l’aide du service d’acteur hello
Les instances d’acteur ont service d’acteur toohello accès dans lequel ils sont en cours d’exécution. Via le service d’acteur hello, instances de l’acteur peuvent obtenir par programmation le contexte de service hello. contexte de service Hello a l’ID de partition hello, nom du service, nom de l’application et autres informations spécifiques à la plateforme de l’infrastructure de Service :

```csharp
Task MyActorMethod()
{
    Guid partitionId = this.ActorService.Context.PartitionId;
    string serviceTypeName = this.ActorService.Context.ServiceTypeName;
    Uri serviceInstanceName = this.ActorService.Context.ServiceName;
    string applicationInstanceName = this.ActorService.Context.CodePackageActivationContext.ApplicationName;
}
```
```Java
CompletableFuture<?> MyActorMethod()
{
    UUID partitionId = this.getActorService().getServiceContext().getPartitionId();
    String serviceTypeName = this.getActorService().getServiceContext().getServiceTypeName();
    URI serviceInstanceName = this.getActorService().getServiceContext().getServiceName();
    String applicationInstanceName = this.getActorService().getServiceContext().getCodePackageActivationContext().getApplicationName();
}
```


Comme tous les Services fiables, le service d’acteur hello doit être inscrite avec un type de service dans le runtime du Service Fabric hello. Pour du service d’acteur de hello toorun vos instances de l’acteur, votre type d’acteur doit également être inscrit dans hello acteur service. Hello `ActorRuntime` méthode d’inscription exécute cette tâche pour acteurs. Dans le cas le plus simple hello, vous pouvez inscrire simplement votre type d’acteur et service d’acteur hello avec les paramètres par défaut sera utilisé implicitement :

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>().GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
    }
}
```

Vous pouvez également utiliser une expression lambda fournie par service d’acteur hello inscription méthode tooconstruct hello, vous-même. Vous pouvez ensuite configurer le service d’acteur hello et construire explicitement vos instances de l’acteur, où vous pouvez injecter un acteur tooyour de dépendances via son constructeur :

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>(
            (context, actorType) => new ActorService(context, actorType, () => new MyActor()))
            .GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
    }
}
```
```Java
static class Program
{
    private static void Main()
    {
      ActorRuntime.registerActorAsync(
              MyActor.class,
              (context, actorTypeInfo) -> new FabricActorService(context, actorTypeInfo),
              timeout);

        Thread.sleep(Long.MAX_VALUE);
    }
}
```

### <a name="actor-service-methods"></a>Méthodes du service d’acteur
Hello implémente de service d’acteur `IActorService` (c#) ou `ActorService` (Java), qui à son tour implémente `IService` (c#) ou `Service` (Java). Il s’agit d’interface hello utilisé par la communication à distance des Services fiables, ce qui autorise les appels de procédure distante sur les méthodes de service. Elle contient des méthodes de niveau de service qui peuvent être appelées à distance via la communication à distance des services.

#### <a name="enumerating-actors"></a>Énumération des acteurs
service d’acteur Hello permet à un client tooenumerate des métadonnées sur des intervenants hello qui héberge le service de hello. Étant donné que le service d’acteur hello est un service avec état partitionné, l’énumération est effectuée par partition. Étant donné que chaque partition peut contenir de nombreux acteurs, énumération de hello est retournée en tant qu’ensemble de résultats paginés. pages de Hello sont boucle jusqu'à ce que toutes les pages sont lues. Hello suivant montre l’exemple de comment toocreate une liste de tous les intervenants actives dans une partition d’un service d’acteur :

```csharp
IActorService actorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), partitionKey);

ContinuationToken continuationToken = null;
List<ActorInformation> activeActors = new List<ActorInformation>();

do
{
    PagedResult<ActorInformation> page = await actorServiceProxy.GetActorsAsync(continuationToken, cancellationToken);

    activeActors.AddRange(page.Items.Where(x => x.IsActive));

    continuationToken = page.ContinuationToken;
}
while (continuationToken != null);
```

```Java
ActorService actorServiceProxy = ActorServiceProxy.create(
    new URI("fabric:/MyApp/MyService"), partitionKey);

ContinuationToken continuationToken = null;
List<ActorInformation> activeActors = new ArrayList<ActorInformation>();

do
{
    PagedResult<ActorInformation> page = actorServiceProxy.getActorsAsync(continuationToken);

    while(ActorInformation x: page.getItems())
    {
         if(x.isActive()){
              activeActors.add(x);
         }
    }

    continuationToken = page.getContinuationToken();
}
while (continuationToken != null);
```

#### <a name="deleting-actors"></a>Suppression d’acteurs
service d’acteur Hello fournit également une fonction de suppression des acteurs :

```csharp
ActorId actorToDelete = new ActorId(id);

IActorService myActorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

await myActorServiceProxy.DeleteActorAsync(actorToDelete, cancellationToken)
```
```Java
ActorId actorToDelete = new ActorId(id);

ActorService myActorServiceProxy = ActorServiceProxy.create(
    new URI("fabric:/MyApp/MyService"), actorToDelete);

myActorServiceProxy.deleteActorAsync(actorToDelete);
```

Pour plus d’informations sur la suppression des acteurs et leur état, consultez hello [documentation du cycle de vie acteur](service-fabric-reliable-actors-lifecycle.md).

### <a name="custom-actor-service"></a>Service d’acteur personnalisé
À l’aide de lambda de hello acteur d’inscription, vous pouvez inscrire votre propre service d’acteur personnalisée qui dérive de `ActorService` (c#) et `FabricActorService` (Java). Dans ce service d’acteur personnalisé, vous pouvez implémenter vos propres fonctionnalités de niveau de service en écrivant une classe de service qui hérite de `ActorService` (c#) ou `FabricActorService` (Java). Un service d’acteur personnalisée hérite de toutes les fonctionnalités de runtime acteur hello de `ActorService` (c#) ou `FabricActorService` (Java) et peut être utilisé tooimplement vos propres méthodes de service.

```csharp
class MyActorService : ActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<ActorBase> newActor)
        : base(context, typeInfo, newActor)
    { }
}
```
```Java
class MyActorService extends FabricActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, BiFunction<FabricActorService, ActorId, ActorBase> newActor)
    {
         super(context, typeInfo, newActor);
    }
}
```

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>(
            (context, actorType) => new MyActorService(context, actorType, () => new MyActor()))
            .GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
    }
}
```
```Java
public class Program
{
    public static void main(String[] args)
    {
        ActorRuntime.registerActorAsync(
                MyActor.class,
                (context, actorTypeInfo) -> new FabricActorService(context, actorTypeInfo),
                timeout);
        Thread.sleep(Long.MAX_VALUE);
    }
}
```

#### <a name="implementing-actor-backup-and-restore"></a>Implémentation d’une sauvegarde et restauration d’acteur
 Dans l’exemple suivant de hello, service d’acteur personnalisée hello expose un tooback (méthode), les données d’acteur en tirant parti de l’écouteur de la communication à distance hello déjà présente dans `ActorService`:

```csharp
public interface IMyActorService : IService
{
    Task BackupActorsAsync();
}

class MyActorService : ActorService, IMyActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<ActorBase> newActor)
        : base(context, typeInfo, newActor)
    { }

    public Task BackupActorsAsync()
    {
        return this.BackupAsync(new BackupDescription(PerformBackupAsync));
    }

    private async Task<bool> PerformBackupAsync(BackupInfo backupInfo, CancellationToken cancellationToken)
    {
        try
        {
           // store hello contents of backupInfo.Directory
           return true;
        }
        finally
        {
           Directory.Delete(backupInfo.Directory, recursive: true);
        }
    }
}
```
```Java
public interface MyActorService extends Service
{
    CompletableFuture<?> backupActorsAsync();
}

class MyActorServiceImpl extends ActorService implements MyActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<FabricActorService, ActorId, ActorBase> newActor)
    {
       super(context, typeInfo, newActor);
    }

    public CompletableFuture backupActorsAsync()
    {
        return this.backupAsync(new BackupDescription((backupInfo, cancellationToken) -> performBackupAsync(backupInfo, cancellationToken)));
    }

    private CompletableFuture<Boolean> performBackupAsync(BackupInfo backupInfo, CancellationToken cancellationToken)
    {
        try
        {
           // store hello contents of backupInfo.Directory
           return true;
        }
        finally
        {
           deleteDirectory(backupInfo.Directory)
        }
    }

    void deleteDirectory(File file) {
        File[] contents = file.listFiles();
        if (contents != null) {
            for (File f : contents) {
               deleteDirectory(f);
             }
        }
        file.delete();
    }
}
```


Dans cet exemple, `IMyActorService` est un contrat de communication à distance qui implémente `IService` (C#) et `Service` (Java) et est ensuite implémenté par `MyActorService`. En ajoutant ce contrat la communication à distance, les méthodes sur `IMyActorService` sont désormais également disponibles tooa client en créant un proxy de communication à distance via `ActorServiceProxy`:

```csharp
IMyActorService myActorServiceProxy = ActorServiceProxy.Create<IMyActorService>(
    new Uri("fabric:/MyApp/MyService"), ActorId.CreateRandom());

await myActorServiceProxy.BackupActorsAsync();
```
```Java
MyActorService myActorServiceProxy = ActorServiceProxy.create(MyActorService.class,
    new URI("fabric:/MyApp/MyService"), actorId);

myActorServiceProxy.backupActorsAsync();
```

## <a name="application-model"></a>Modèle d'application
Services d’acteur étant des Services fiables, modèle d’application hello est hello identiques. Toutefois, des outils de génération hello acteur framework génèrent des fichiers de modèle d’application hello pour vous.

### <a name="service-manifest"></a>Manifeste de service
outils de génération de framework Hello acteur génèrent automatiquement le contenu hello du fichier de ServiceManifest.xml de votre service d’acteur. Ce fichier inclut :

* Le type de service d’acteur. nom de type Hello est généré en fonction du nom du projet de votre acteur. En fonction de l’attribut de persistance hello sur votre acteur, hello HasPersistedState indicateur est également définie en conséquence.
* le package de code ;
* le package de configuration ;
* les ressources et points de terminaison.

### <a name="application-manifest"></a>Manifeste d’application
outils de génération de framework Hello acteur créent automatiquement une définition de service par défaut pour votre service d’acteur. outils de génération Hello remplissent les propriétés de service par défaut hello :

* Nombre de jeu de réplica est déterminé par l’attribut persistance hello sur votre acteur. Chaque attribut de persistance hello heure sur votre acteur est modifié, nombre de jeu de réplica hello dans la définition de service par défaut hello est réinitialisé en conséquence.
* Plage et le schéma de partition sont définies tooUniform Int64 avec complète plage de clés Int64 hello.

## <a name="service-fabric-partition-concepts-for-actors"></a>Concepts de partition Service Fabric pour les acteurs
Les services d’acteur sont des services partitionnés avec état. Chaque partition d’un service d’acteur contient un ensemble d’acteurs. Les partitions de service sont automatiquement distribuées sur plusieurs nœuds dans Service Fabric. Par conséquent, les instances d’acteur sont distribuées.

![Partitionnement et distribution d’acteur][5]

Vous pouvez créer des Reliable Services avec différents schémas de partition et plages de clés de partition. service d’acteur Hello utilise schéma de partitionnement hello Int64 avec toomap acteurs toopartitions hello complètes Int64 plage de clés.

### <a name="actor-id"></a>ID d’acteur
Chaque acteur qui est créé dans le service hello a un ID unique associé, représenté par hello `ActorId` classe. `ActorId`est une valeur d’ID opaque pouvant servir pour une distribution uniforme des acteurs sur plusieurs partitions de service hello en générant des identifiants aléatoires :

```csharp
ActorProxy.Create<IMyActor>(ActorId.CreateRandom());
```
```Java
ActorProxyBase.create<MyActor>(MyActor.class, ActorId.newId());
```


Chaque `ActorId` est haché tooan Int64. C’est pourquoi le service d’acteur hello doit utiliser un schéma de partitionnement de Int64 avec complète plage de clés Int64 hello. Toutefois, vous pouvez utiliser des valeurs d’ID personnalisées pour un `ActorID`, dont des GUID / UUID, des chaînes et des valeurs Int64s.

```csharp
ActorProxy.Create<IMyActor>(new ActorId(Guid.NewGuid()));
ActorProxy.Create<IMyActor>(new ActorId("myActorId"));
ActorProxy.Create<IMyActor>(new ActorId(1234));
```
```Java
ActorProxyBase.create(MyActor.class, new ActorId(UUID.randomUUID()));
ActorProxyBase.create(MyActor.class, new ActorId("myActorId"));
ActorProxyBase.create(MyActor.class, new ActorId(1234));
```

Lorsque vous utilisez des chaînes et des GUID/UUID, les valeurs hello sont haché tooan Int64. Toutefois, lorsque vous êtes en fournissant explicitement un tooan Int64 `ActorId`, hello Int64 mappera directement tooa partition sans davantage de hachage. Vous pouvez utiliser cette toocontrol technique qui acteurs hello de partition sont placés dans.

## <a name="next-steps"></a>Étapes suivantes
* [Gestion des états d’acteur](service-fabric-reliable-actors-state-management.md)
* [Cycle de vie des acteurs et Garbage Collection](service-fabric-reliable-actors-lifecycle.md)
* [Documentation de référence de l’API Actors](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [Exemple de code .NET](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [Exemple de code Java](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-platform/actor-service.png
[2]: ./media/service-fabric-reliable-actors-platform/app-deployment-scripts.png
[3]: ./media/service-fabric-reliable-actors-platform/actor-partition-info.png
[4]: ./media/service-fabric-reliable-actors-platform/actor-replica-role.png
[5]: ./media/service-fabric-reliable-actors-introduction/distribution.png
