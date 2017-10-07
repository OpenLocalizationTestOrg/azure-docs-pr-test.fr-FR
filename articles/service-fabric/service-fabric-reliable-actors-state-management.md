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
# <a name="reliable-actors-state-management"></a><span data-ttu-id="63303-103">Gestion des états de Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="63303-103">Reliable Actors state management</span></span>
<span data-ttu-id="63303-104">Reliable Actors désignent des objets monothread capables d’encapsuler la logique et l’état.</span><span class="sxs-lookup"><span data-stu-id="63303-104">Reliable Actors are single-threaded objects that can encapsulate both logic and state.</span></span> <span data-ttu-id="63303-105">Acteurs exécutés sur des Services fiables, ils peuvent conserver leur état fiable à l’aide de hello les mêmes mécanismes de réplication et de persistance qui utilise des Services fiables.</span><span class="sxs-lookup"><span data-stu-id="63303-105">Because actors run on Reliable Services, they can maintain state reliably by using hello same persistence and replication mechanisms that Reliable Services uses.</span></span> <span data-ttu-id="63303-106">De cette manière, les acteurs ne perdent pas leur état après des incidents, à la réactivation après le garbage collection ou qu’ils sont déplacés entre les nœuds dans un cluster en raison de l’équilibrage de la tooresource ou mises à niveau.</span><span class="sxs-lookup"><span data-stu-id="63303-106">This way, actors don't lose their state after failures, upon reactivation after garbage collection, or when they are moved around between nodes in a cluster due tooresource balancing or upgrades.</span></span>

## <a name="state-persistence-and-replication"></a><span data-ttu-id="63303-107">Persistance et réplication de l’état</span><span class="sxs-lookup"><span data-stu-id="63303-107">State persistence and replication</span></span>
<span data-ttu-id="63303-108">Tous les intervenants fiable sont considérés comme *avec état* , car chaque instance de l’acteur mappe les ID tooa unique.</span><span class="sxs-lookup"><span data-stu-id="63303-108">All Reliable Actors are considered *stateful* because each actor instance maps tooa unique ID.</span></span> <span data-ttu-id="63303-109">Cela signifie que toohello des appels répétés même acteur ID sont acheminés toohello même instance d’acteur.</span><span class="sxs-lookup"><span data-stu-id="63303-109">This means that repeated calls toohello same actor ID are routed toohello same actor instance.</span></span> <span data-ttu-id="63303-110">Dans un système sans état, en revanche, les appels de client ne sont pas garantis toobe routé toohello même serveur chaque fois.</span><span class="sxs-lookup"><span data-stu-id="63303-110">In a stateless system, by contrast, client calls are not guaranteed toobe routed toohello same server every time.</span></span> <span data-ttu-id="63303-111">Pour cette raison, les services d’acteur sont toujours des services avec état.</span><span class="sxs-lookup"><span data-stu-id="63303-111">For this reason, actor services are always stateful services.</span></span>

<span data-ttu-id="63303-112">Même si les acteurs sont considérés comme des services avec état, cela ne signifie pas qu’ils doivent stocker l’état de manière fiable.</span><span class="sxs-lookup"><span data-stu-id="63303-112">Even though actors are considered stateful, that does not mean they must store state reliably.</span></span> <span data-ttu-id="63303-113">Acteurs peuvent choisir le niveau hello de persistance de l’état et la réplication basée sur leurs données, les exigences de stockage :</span><span class="sxs-lookup"><span data-stu-id="63303-113">Actors can choose hello level of state persistence and replication based on their data storage requirements:</span></span>

* <span data-ttu-id="63303-114">**État persistant**: état est persistante toodisk et est répliqué too3 ou plusieurs réplicas.</span><span class="sxs-lookup"><span data-stu-id="63303-114">**Persisted state**: State is persisted toodisk and is replicated too3 or more replicas.</span></span> <span data-ttu-id="63303-115">Il s’agit d’une option de stockage pour état durable plus de hello, où l’état peut être rendue persistante via l’arrêt de la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="63303-115">This is hello most durable state storage option, where state can persist through complete cluster outage.</span></span>
* <span data-ttu-id="63303-116">**Un état volatile**: état est répliquée too3 ou plusieurs réplicas et conservée uniquement en mémoire.</span><span class="sxs-lookup"><span data-stu-id="63303-116">**Volatile state**: State is replicated too3 or more replicas and only kept in memory.</span></span> <span data-ttu-id="63303-117">Cette option garantit une résilience contre les défaillances de nœud et d’acteur, ainsi que pendant les mises à niveau et l’équilibrage des ressources.</span><span class="sxs-lookup"><span data-stu-id="63303-117">This provides resilience against node failure and actor failure, and during upgrades and resource balancing.</span></span> <span data-ttu-id="63303-118">Toutefois, l’état n’est pas persistante toodisk.</span><span class="sxs-lookup"><span data-stu-id="63303-118">However, state is not persisted toodisk.</span></span> <span data-ttu-id="63303-119">Si tous les réplicas sont perdus à la fois, état de hello sont également perdue.</span><span class="sxs-lookup"><span data-stu-id="63303-119">So if all replicas are lost at once, hello state is lost as well.</span></span>
* <span data-ttu-id="63303-120">**Aucun état persistant**: état n’est pas répliqué ou écrit toodisk.</span><span class="sxs-lookup"><span data-stu-id="63303-120">**No persisted state**: State is not replicated or written toodisk.</span></span> <span data-ttu-id="63303-121">Ce niveau est pour les acteurs qui ne suffit toomaintain état fiable.</span><span class="sxs-lookup"><span data-stu-id="63303-121">This level is for actors that simply don't need toomaintain state reliably.</span></span>

<span data-ttu-id="63303-122">Chaque niveau de persistance représente simplement une autre configuration du *fournisseur d’état* et de la *réplication* de votre service.</span><span class="sxs-lookup"><span data-stu-id="63303-122">Each level of persistence is simply a different *state provider* and *replication* configuration of your service.</span></span> <span data-ttu-id="63303-123">État est écrit ou non toodisk dépend de fournisseur d’état hello--composant hello dans un service fiable qui stocke l’état.</span><span class="sxs-lookup"><span data-stu-id="63303-123">Whether or not state is written toodisk depends on hello state provider--hello component in a reliable service that stores state.</span></span> <span data-ttu-id="63303-124">La réplication varie selon le nombre de réplicas avec lesquels est déployé un service.</span><span class="sxs-lookup"><span data-stu-id="63303-124">Replication depends on how many replicas a service is deployed with.</span></span> <span data-ttu-id="63303-125">Comme avec les Services fiables, les deux hello fournisseur d’état et nombre de réplicas peut aisément être défini manuellement.</span><span class="sxs-lookup"><span data-stu-id="63303-125">As with Reliable Services, both hello state provider and replica count can easily be set manually.</span></span> <span data-ttu-id="63303-126">infrastructure d’acteur Hello fournit un attribut, lorsqu’il est utilisé sur un acteur, sélectionne automatiquement un fournisseur d’état par défaut et génère automatiquement les paramètres de réplica nombre tooachieve, un de ces trois paramètres de persistance.</span><span class="sxs-lookup"><span data-stu-id="63303-126">hello actor framework provides an attribute that, when used on an actor, automatically selects a default state provider and automatically generates settings for replica count tooachieve one of these three persistence settings.</span></span> <span data-ttu-id="63303-127">attribut StatePersistence de Hello n’est pas hérité par la classe dérivée, chaque type d’acteur doit fournir son niveau de StatePersistence.</span><span class="sxs-lookup"><span data-stu-id="63303-127">hello StatePersistence attribute is not inherited by derived class, each Actor type must provide its StatePersistence level.</span></span>

### <a name="persisted-state"></a><span data-ttu-id="63303-128">État persistant</span><span class="sxs-lookup"><span data-stu-id="63303-128">Persisted state</span></span>
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
<span data-ttu-id="63303-129">Ce paramètre utilise un fournisseur d’état qui stocke les données sur disque et définit automatiquement too3 de nombre de réplicas de service hello.</span><span class="sxs-lookup"><span data-stu-id="63303-129">This setting uses a state provider that stores data on disk and automatically sets hello service replica count too3.</span></span>

### <a name="volatile-state"></a><span data-ttu-id="63303-130">État volatil</span><span class="sxs-lookup"><span data-stu-id="63303-130">Volatile state</span></span>
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
<span data-ttu-id="63303-131">Ce paramètre utilise un fournisseur d’état dans-uniquement en mémoire et jeux hello too3 nombre de réplicas.</span><span class="sxs-lookup"><span data-stu-id="63303-131">This setting uses an in-memory-only state provider and sets hello replica count too3.</span></span>

### <a name="no-persisted-state"></a><span data-ttu-id="63303-132">État non persistant</span><span class="sxs-lookup"><span data-stu-id="63303-132">No persisted state</span></span>
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
<span data-ttu-id="63303-133">Ce paramètre utilise un fournisseur d’état dans-uniquement en mémoire et jeux hello too1 nombre de réplicas.</span><span class="sxs-lookup"><span data-stu-id="63303-133">This setting uses an in-memory-only state provider and sets hello replica count too1.</span></span>

### <a name="defaults-and-generated-settings"></a><span data-ttu-id="63303-134">Valeurs par défaut et paramètres générés</span><span class="sxs-lookup"><span data-stu-id="63303-134">Defaults and generated settings</span></span>
<span data-ttu-id="63303-135">Lorsque vous utilisez hello `StatePersistence` attribut, un fournisseur d’état est sélectionné automatiquement lors de l’exécution au démarrage du service d’acteur hello.</span><span class="sxs-lookup"><span data-stu-id="63303-135">When you're using hello `StatePersistence` attribute, a state provider is automatically selected for you at runtime when hello actor service starts.</span></span> <span data-ttu-id="63303-136">nombre de réplicas Hello, toutefois, est défini au moment de la compilation par hello acteur de Visual Studio des outils de génération.</span><span class="sxs-lookup"><span data-stu-id="63303-136">hello replica count, however, is set at compile time by hello Visual Studio actor build tools.</span></span> <span data-ttu-id="63303-137">Hello outils de génération de génèrent automatiquement un *service par défaut* pour le service d’acteur hello dans ApplicationManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="63303-137">hello build tools automatically generate a *default service* for hello actor service in ApplicationManifest.xml.</span></span> <span data-ttu-id="63303-138">Les paramètres sont créés pour la **taille minimale du jeu de réplicas** et la **taille cible du jeu de réplicas**.</span><span class="sxs-lookup"><span data-stu-id="63303-138">Parameters are created for **min replica set size** and **target replica set size**.</span></span>

<span data-ttu-id="63303-139">Vous pouvez modifier ces paramètres manuellement.</span><span class="sxs-lookup"><span data-stu-id="63303-139">You can change these parameters manually.</span></span> <span data-ttu-id="63303-140">Mais chaque hello temps `StatePersistence` attribut est modifié, les paramètres de hello sont définis toohello réplica ensemble taille par défaut pour hello sélectionné `StatePersistence` attribut, en remplaçant toutes les valeurs précédentes.</span><span class="sxs-lookup"><span data-stu-id="63303-140">But each time hello `StatePersistence` attribute is changed, hello parameters are set toohello default replica set size values for hello selected `StatePersistence` attribute, overriding any previous values.</span></span> <span data-ttu-id="63303-141">En d’autres termes, les valeurs hello que vous définissez dans ServiceManifest.xml sont *uniquement* remplacée au moment de la génération lorsque vous modifiez hello `StatePersistence` valeur d’attribut.</span><span class="sxs-lookup"><span data-stu-id="63303-141">In other words, hello values that you set in ServiceManifest.xml are *only* overridden at build time when you change hello `StatePersistence` attribute value.</span></span>

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

## <a name="state-manager"></a><span data-ttu-id="63303-142">Gestionnaire d’état</span><span class="sxs-lookup"><span data-stu-id="63303-142">State manager</span></span>
<span data-ttu-id="63303-143">Chaque instance d’acteur possède son propre gestionnaire d’état, c’est-à-dire une structure de données de type dictionnaire qui stocke les paires clé/valeur de manière fiable.</span><span class="sxs-lookup"><span data-stu-id="63303-143">Every actor instance has its own state manager: a dictionary-like data structure that reliably stores key/value pairs.</span></span> <span data-ttu-id="63303-144">Gestionnaire d’état Hello est un wrapper autour d’un fournisseur d’état.</span><span class="sxs-lookup"><span data-stu-id="63303-144">hello state manager is a wrapper around a state provider.</span></span> <span data-ttu-id="63303-145">Vous pouvez l’utiliser toostore données quel que soit le paramètre de persistance est utilisé.</span><span class="sxs-lookup"><span data-stu-id="63303-145">You can use it toostore data regardless of which persistence setting is used.</span></span> <span data-ttu-id="63303-146">Il ne fournit pas toutes les garanties qu’un service d’acteur en cours d’exécution peut être modifié à partir d’un tooa de paramètre rémanente (en mémoire-uniquement) persistant paramètre via une mise à niveau propagée, tout en conservant les données d’état.</span><span class="sxs-lookup"><span data-stu-id="63303-146">It does not provide any guarantees that a running actor service can be changed from a volatile (in-memory-only) state setting tooa persisted state setting through a rolling upgrade while preserving data.</span></span> <span data-ttu-id="63303-147">Toutefois, il est possible toochange nombre de réplica pour un service en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="63303-147">However, it is possible toochange replica count for a running service.</span></span>

<span data-ttu-id="63303-148">Les clés de gestionnaire d’état doivent être des chaînes.</span><span class="sxs-lookup"><span data-stu-id="63303-148">State manager keys must be strings.</span></span> <span data-ttu-id="63303-149">Les valeurs sont génériques et peuvent être de n’importe quel type, y compris de types personnalisés.</span><span class="sxs-lookup"><span data-stu-id="63303-149">Values are generic and can be any type, including custom types.</span></span> <span data-ttu-id="63303-150">Valeurs stockées dans le Gestionnaire d’état hello doivent être de contrat de données sérialisable, car elles peuvent être transmises sur des nœuds de tooother hello réseau pendant la réplication et peuvent être écrits toodisk, selon le paramètre de persistance d’état d’un acteur.</span><span class="sxs-lookup"><span data-stu-id="63303-150">Values stored in hello state manager must be data contract serializable because they might be transmitted over hello network tooother nodes during replication and might be written toodisk, depending on an actor's state persistence setting.</span></span>

<span data-ttu-id="63303-151">Gestionnaire d’état Hello expose les méthodes courantes de dictionnaire pour la gestion d’état, semblable toothose trouvé dans le dictionnaire fiable.</span><span class="sxs-lookup"><span data-stu-id="63303-151">hello state manager exposes common dictionary methods for managing state, similar toothose found in Reliable Dictionary.</span></span>

### <a name="accessing-state"></a><span data-ttu-id="63303-152">Accès à l’état</span><span class="sxs-lookup"><span data-stu-id="63303-152">Accessing state</span></span>
<span data-ttu-id="63303-153">État est accessible via le Gestionnaire d’état hello par clé.</span><span class="sxs-lookup"><span data-stu-id="63303-153">State can be accessed through hello state manager by key.</span></span> <span data-ttu-id="63303-154">Les méthodes du gestionnaire d’état sont toutes asynchrones, car elles peuvent nécessiter des E/S disque lorsque les acteurs sont à l’état persistant.</span><span class="sxs-lookup"><span data-stu-id="63303-154">State manager methods are all asynchronous because they might require disk I/O when actors have persisted state.</span></span> <span data-ttu-id="63303-155">Lors du premier accès, les objets d’état sont mis en mémoire cache.</span><span class="sxs-lookup"><span data-stu-id="63303-155">Upon first access, state objects are cached in memory.</span></span> <span data-ttu-id="63303-156">Les opérations d’accès répétées permettent d’accéder aux objets directement à partir de la mémoire et sont retournées de façon synchrone sans entraîner d’E/S disque ou de surcharge asynchrone en cas de changement de contexte.</span><span class="sxs-lookup"><span data-stu-id="63303-156">Repeat access operations access objects directly from memory and return synchronously without incurring disk I/O or asynchronous context-switching overhead.</span></span> <span data-ttu-id="63303-157">Un objet d’état est supprimé à partir du cache hello hello suivant cas :</span><span class="sxs-lookup"><span data-stu-id="63303-157">A state object is removed from hello cache in hello following cases:</span></span>

* <span data-ttu-id="63303-158">Une méthode d’acteur lève une exception non gérée une fois qu’il extrait un objet de gestionnaire d’état hello.</span><span class="sxs-lookup"><span data-stu-id="63303-158">An actor method throws an unhandled exception after it retrieves an object from hello state manager.</span></span>
* <span data-ttu-id="63303-159">Un acteur est réactivé soit après avoir été désactivé, soit en raison d’un échec.</span><span class="sxs-lookup"><span data-stu-id="63303-159">An actor is reactivated, either after being deactivated or after failure.</span></span>
* <span data-ttu-id="63303-160">pages de fournisseurs d’état Hello toodisk d’état.</span><span class="sxs-lookup"><span data-stu-id="63303-160">hello state provider pages state toodisk.</span></span> <span data-ttu-id="63303-161">Ce comportement dépend de l’implémentation de fournisseur d’état hello.</span><span class="sxs-lookup"><span data-stu-id="63303-161">This behavior depends on hello state provider implementation.</span></span> <span data-ttu-id="63303-162">fournisseur d’état par défaut Hello hello `Persisted` paramètre a ce comportement.</span><span class="sxs-lookup"><span data-stu-id="63303-162">hello default state provider for hello `Persisted` setting has this behavior.</span></span>

<span data-ttu-id="63303-163">Vous pouvez récupérer l’état à l’aide d’une norme *obtenir* opération lève `KeyNotFoundException`(c#) ou `NoSuchElementException`(Java) si une entrée n’existe pas de clé de hello :</span><span class="sxs-lookup"><span data-stu-id="63303-163">You can retrieve state by using a standard *Get* operation that throws `KeyNotFoundException`(C#) or `NoSuchElementException`(Java) if an entry does not exist for hello key:</span></span>

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

<span data-ttu-id="63303-164">Vous pouvez également récupérer l’état à l’aide d’une opération *TryGet* qui ne lève pas d’exception s’il n’existe aucune entrée pour la clé :</span><span class="sxs-lookup"><span data-stu-id="63303-164">You can also retrieve state by using a *TryGet* method that does not throw if an entry does not exist for a key:</span></span>

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

### <a name="saving-state"></a><span data-ttu-id="63303-165">Enregistrement de l’état</span><span class="sxs-lookup"><span data-stu-id="63303-165">Saving state</span></span>
<span data-ttu-id="63303-166">méthodes de récupération du gestionnaire Hello état retournent un objet de tooan de référence dans la mémoire locale.</span><span class="sxs-lookup"><span data-stu-id="63303-166">hello state manager retrieval methods return a reference tooan object in local memory.</span></span> <span data-ttu-id="63303-167">Modification de cet objet dans la mémoire locale uniquement ne provoque pas il toobe enregistré de façon durable.</span><span class="sxs-lookup"><span data-stu-id="63303-167">Modifying this object in local memory alone does not cause it toobe saved durably.</span></span> <span data-ttu-id="63303-168">Lorsqu’un objet est récupéré à partir du Gestionnaire d’état hello et modifié, il doit être réinséré hello état manager toobe enregistré de façon durable.</span><span class="sxs-lookup"><span data-stu-id="63303-168">When an object is retrieved from hello state manager and modified, it must be reinserted into hello state manager toobe saved durably.</span></span>

<span data-ttu-id="63303-169">Vous pouvez insérer l’état à l’aide un inconditionnel *définir*, qui est hello équivalent de hello `dictionary["key"] = value` syntaxe :</span><span class="sxs-lookup"><span data-stu-id="63303-169">You can insert state by using an unconditional *Set*, which is hello equivalent of hello `dictionary["key"] = value` syntax:</span></span>

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

<span data-ttu-id="63303-170">Vous pouvez ajouter l’état en utilisant une méthode *Add*.</span><span class="sxs-lookup"><span data-stu-id="63303-170">You can add state by using an *Add* method.</span></span> <span data-ttu-id="63303-171">Cette méthode lève `InvalidOperationException`(c#) ou `IllegalStateException`(Java) quand il tente de tooadd une clé qui existe déjà.</span><span class="sxs-lookup"><span data-stu-id="63303-171">This method throws `InvalidOperationException`(C#) or `IllegalStateException`(Java) when it tries tooadd a key that already exists.</span></span>

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

<span data-ttu-id="63303-172">Vous pouvez également ajouter l’état en utilisant une méthode *TryAdd*.</span><span class="sxs-lookup"><span data-stu-id="63303-172">You can also add state by using a *TryAdd* method.</span></span> <span data-ttu-id="63303-173">Cette méthode ne lève pas quand il tente de tooadd une clé qui existe déjà.</span><span class="sxs-lookup"><span data-stu-id="63303-173">This method does not throw when it tries tooadd a key that already exists.</span></span>

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

<span data-ttu-id="63303-174">Extrémité hello d’une méthode d’acteur, gestionnaire d’état hello enregistre automatiquement toutes les valeurs qui ont été ajoutées ou modifiées par une opération insert ou update.</span><span class="sxs-lookup"><span data-stu-id="63303-174">At hello end of an actor method, hello state manager automatically saves any values that have been added or modified by an insert or update operation.</span></span> <span data-ttu-id="63303-175">Un « Enregistrer » peut inclure toodisk persistante et la réplication, en fonction des paramètres hello utilisé.</span><span class="sxs-lookup"><span data-stu-id="63303-175">A "save" can include persisting toodisk and replication, depending on hello settings used.</span></span> <span data-ttu-id="63303-176">Les valeurs qui n’ont pas été modifiées ne sont pas conservées ou répliquées.</span><span class="sxs-lookup"><span data-stu-id="63303-176">Values that have not been modified are not persisted or replicated.</span></span> <span data-ttu-id="63303-177">Si aucune valeur n’ont été modifiés, hello opération d’enregistrement ne fait rien.</span><span class="sxs-lookup"><span data-stu-id="63303-177">If no values have been modified, hello save operation does nothing.</span></span> <span data-ttu-id="63303-178">Si l’enregistrement échoue, hello état modifié est ignoré et état d’origine de hello est rechargé.</span><span class="sxs-lookup"><span data-stu-id="63303-178">If saving fails, hello modified state is discarded and hello original state is reloaded.</span></span>

<span data-ttu-id="63303-179">Vous pouvez également enregistrer état manuellement en appelant hello `SaveStateAsync` méthode sur acteur hello base :</span><span class="sxs-lookup"><span data-stu-id="63303-179">You can also save state manually by calling hello `SaveStateAsync` method on hello actor base:</span></span>

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

### <a name="removing-state"></a><span data-ttu-id="63303-180">Suppression de l’état</span><span class="sxs-lookup"><span data-stu-id="63303-180">Removing state</span></span>
<span data-ttu-id="63303-181">Vous pouvez supprimer état définitivement à partir du Gestionnaire d’état d’un acteur en appelant hello *supprimer* (méthode).</span><span class="sxs-lookup"><span data-stu-id="63303-181">You can remove state permanently from an actor's state manager by calling hello *Remove* method.</span></span> <span data-ttu-id="63303-182">Cette méthode lève `KeyNotFoundException`(c#) ou `NoSuchElementException`(Java) quand il tente de tooremove une clé qui n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="63303-182">This method throws `KeyNotFoundException`(C#) or `NoSuchElementException`(Java) when it tries tooremove a key that doesn't exist.</span></span>

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

<span data-ttu-id="63303-183">Vous pouvez également supprimer définitivement état à l’aide de hello *TryRemove* (méthode).</span><span class="sxs-lookup"><span data-stu-id="63303-183">You can also remove state permanently by using hello *TryRemove* method.</span></span> <span data-ttu-id="63303-184">Cette méthode ne lève pas quand il tente de tooremove une clé qui n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="63303-184">This method does not throw when it tries tooremove a key that does not exist.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="63303-185">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="63303-185">Next steps</span></span>

<span data-ttu-id="63303-186">État qui est stocké dans Reliable Actors doit être sérialisé avant son toodisk écrite et répliquée pour la haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="63303-186">State that's stored in Reliable Actors must be serialized before its written toodisk and replicated for high availability.</span></span> <span data-ttu-id="63303-187">En savoir plus sur [Sérialisation du type d’acteur](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="63303-187">Learn more about [Actor type serialization](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span></span>

<span data-ttu-id="63303-188">Ensuite, en savoir plus sur l’[analyse des performances et des diagnostics des acteurs](service-fabric-reliable-actors-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="63303-188">Next, learn more about [Actor diagnostics and performance monitoring](service-fabric-reliable-actors-diagnostics.md).</span></span>
