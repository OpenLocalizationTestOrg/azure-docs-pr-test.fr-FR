---
title: "Gestion des états de Reliable Actors | Microsoft Docs"
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
ms.openlocfilehash: aca8cf2b94e8b746a5cac6af021c7221a29b7345
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="reliable-actors-state-management"></a><span data-ttu-id="8744e-103">Gestion des états de Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="8744e-103">Reliable Actors state management</span></span>
<span data-ttu-id="8744e-104">Reliable Actors désignent des objets monothread capables d’encapsuler la logique et l’état.</span><span class="sxs-lookup"><span data-stu-id="8744e-104">Reliable Actors are single-threaded objects that can encapsulate both logic and state.</span></span> <span data-ttu-id="8744e-105">Étant donné que les acteurs s’exécutent sur Reliable Services, ils peuvent conserver leur état de façon fiable à l’aide des mêmes mécanismes de persistance et de réplication que ceux utilisés par Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="8744e-105">Because actors run on Reliable Services, they can maintain state reliably by using the same persistence and replication mechanisms that Reliable Services uses.</span></span> <span data-ttu-id="8744e-106">De cette façon, les acteurs ne perdent pas leur état après des incidents, après une réactivation consécutive à un nettoyage de la mémoire, ou encore après leur déplacement entre des nœuds d’un cluster dans le cadre d’un équilibrage des ressources ou de mises à niveau.</span><span class="sxs-lookup"><span data-stu-id="8744e-106">This way, actors don't lose their state after failures, upon reactivation after garbage collection, or when they are moved around between nodes in a cluster due to resource balancing or upgrades.</span></span>

## <a name="state-persistence-and-replication"></a><span data-ttu-id="8744e-107">Persistance et réplication de l’état</span><span class="sxs-lookup"><span data-stu-id="8744e-107">State persistence and replication</span></span>
<span data-ttu-id="8744e-108">Toutes les instances Reliable Actors sont considérées comme des instances *avec état* étant donné que chaque instance d’acteur est mappée à un identifiant unique.</span><span class="sxs-lookup"><span data-stu-id="8744e-108">All Reliable Actors are considered *stateful* because each actor instance maps to a unique ID.</span></span> <span data-ttu-id="8744e-109">Autrement dit, les appels répétés au même ID d’acteur sont acheminés vers la même instance d’acteur.</span><span class="sxs-lookup"><span data-stu-id="8744e-109">This means that repeated calls to the same actor ID are routed to the same actor instance.</span></span> <span data-ttu-id="8744e-110">En revanche, dans un système sans état, rien ne peut garantir que les appels client sont acheminés vers le même serveur à chaque fois.</span><span class="sxs-lookup"><span data-stu-id="8744e-110">In a stateless system, by contrast, client calls are not guaranteed to be routed to the same server every time.</span></span> <span data-ttu-id="8744e-111">Pour cette raison, les services d’acteur sont toujours des services avec état.</span><span class="sxs-lookup"><span data-stu-id="8744e-111">For this reason, actor services are always stateful services.</span></span>

<span data-ttu-id="8744e-112">Même si les acteurs sont considérés comme des services avec état, cela ne signifie pas qu’ils doivent stocker l’état de manière fiable.</span><span class="sxs-lookup"><span data-stu-id="8744e-112">Even though actors are considered stateful, that does not mean they must store state reliably.</span></span> <span data-ttu-id="8744e-113">Les acteurs peuvent choisir le niveau de persistance et de réplication de l’état en fonction de leurs exigences en matière de stockage de données :</span><span class="sxs-lookup"><span data-stu-id="8744e-113">Actors can choose the level of state persistence and replication based on their data storage requirements:</span></span>

* <span data-ttu-id="8744e-114">**État persistant** : l’état est conservé sur le disque et est répliqué sur au moins 3 réplicas.</span><span class="sxs-lookup"><span data-stu-id="8744e-114">**Persisted state**: State is persisted to disk and is replicated to 3 or more replicas.</span></span> <span data-ttu-id="8744e-115">Il s’agit de l’option de stockage d’état la plus fiable, où l’état peut persister après une panne complète du cluster.</span><span class="sxs-lookup"><span data-stu-id="8744e-115">This is the most durable state storage option, where state can persist through complete cluster outage.</span></span>
* <span data-ttu-id="8744e-116">**État volatil** : l’état est répliqué sur au moins 3 réplicas et est conservé uniquement en mémoire.</span><span class="sxs-lookup"><span data-stu-id="8744e-116">**Volatile state**: State is replicated to 3 or more replicas and only kept in memory.</span></span> <span data-ttu-id="8744e-117">Cette option garantit une résilience contre les défaillances de nœud et d’acteur, ainsi que pendant les mises à niveau et l’équilibrage des ressources.</span><span class="sxs-lookup"><span data-stu-id="8744e-117">This provides resilience against node failure and actor failure, and during upgrades and resource balancing.</span></span> <span data-ttu-id="8744e-118">Toutefois, l’état n’est pas conservé sur le disque.</span><span class="sxs-lookup"><span data-stu-id="8744e-118">However, state is not persisted to disk.</span></span> <span data-ttu-id="8744e-119">Si tous les réplicas sont perdus en même temps, l’état est également perdu.</span><span class="sxs-lookup"><span data-stu-id="8744e-119">So if all replicas are lost at once, the state is lost as well.</span></span>
* <span data-ttu-id="8744e-120">**État non persistant** : l’état n’est ni répliqué ni écrit sur le disque.</span><span class="sxs-lookup"><span data-stu-id="8744e-120">**No persisted state**: State is not replicated or written to disk.</span></span> <span data-ttu-id="8744e-121">Ce niveau est destiné aux acteurs qui n’ont simplement pas besoin de maintenir leur état de manière fiable.</span><span class="sxs-lookup"><span data-stu-id="8744e-121">This level is for actors that simply don't need to maintain state reliably.</span></span>

<span data-ttu-id="8744e-122">Chaque niveau de persistance représente simplement une autre configuration du *fournisseur d’état* et de la *réplication* de votre service.</span><span class="sxs-lookup"><span data-stu-id="8744e-122">Each level of persistence is simply a different *state provider* and *replication* configuration of your service.</span></span> <span data-ttu-id="8744e-123">Le fournisseur d’état (le composant Reliable Service conçu pour stocker l’état) détermine si l’état sera ou non écrit sur le disque.</span><span class="sxs-lookup"><span data-stu-id="8744e-123">Whether or not state is written to disk depends on the state provider--the component in a reliable service that stores state.</span></span> <span data-ttu-id="8744e-124">La réplication varie selon le nombre de réplicas avec lesquels est déployé un service.</span><span class="sxs-lookup"><span data-stu-id="8744e-124">Replication depends on how many replicas a service is deployed with.</span></span> <span data-ttu-id="8744e-125">De la même manière que Reliable Services, le fournisseur d’état et le nombre de réplicas peuvent facilement être définis manuellement.</span><span class="sxs-lookup"><span data-stu-id="8744e-125">As with Reliable Services, both the state provider and replica count can easily be set manually.</span></span> <span data-ttu-id="8744e-126">L’infrastructure d’acteurs fournit un attribut, qui, lorsqu’il est utilisé sur un acteur, sélectionne automatiquement un fournisseur d’état par défaut et génère automatiquement des paramètres pour le nombre de réplicas afin d’obtenir un de ces trois paramètres de persistance.</span><span class="sxs-lookup"><span data-stu-id="8744e-126">The actor framework provides an attribute that, when used on an actor, automatically selects a default state provider and automatically generates settings for replica count to achieve one of these three persistence settings.</span></span> <span data-ttu-id="8744e-127">L’attribut StatePersistence n’est pas hérité par la classe dérivée, chaque type d’acteur doit fournir son niveau de StatePersistence.</span><span class="sxs-lookup"><span data-stu-id="8744e-127">The StatePersistence attribute is not inherited by derived class, each Actor type must provide its StatePersistence level.</span></span>

### <a name="persisted-state"></a><span data-ttu-id="8744e-128">État persistant</span><span class="sxs-lookup"><span data-stu-id="8744e-128">Persisted state</span></span>
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
<span data-ttu-id="8744e-129">Ce paramètre utilise un fournisseur d’état qui stocke les données sur disque et définit automatiquement le nombre de réplicas de service à 3.</span><span class="sxs-lookup"><span data-stu-id="8744e-129">This setting uses a state provider that stores data on disk and automatically sets the service replica count to 3.</span></span>

### <a name="volatile-state"></a><span data-ttu-id="8744e-130">État volatil</span><span class="sxs-lookup"><span data-stu-id="8744e-130">Volatile state</span></span>
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
<span data-ttu-id="8744e-131">Ce paramètre utilise un fournisseur d’état uniquement en mémoire et définit le nombre de réplicas à 3.</span><span class="sxs-lookup"><span data-stu-id="8744e-131">This setting uses an in-memory-only state provider and sets the replica count to 3.</span></span>

### <a name="no-persisted-state"></a><span data-ttu-id="8744e-132">État non persistant</span><span class="sxs-lookup"><span data-stu-id="8744e-132">No persisted state</span></span>
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
<span data-ttu-id="8744e-133">Ce paramètre utilise un fournisseur d’état uniquement en mémoire et définit le nombre de réplicas à 1.</span><span class="sxs-lookup"><span data-stu-id="8744e-133">This setting uses an in-memory-only state provider and sets the replica count to 1.</span></span>

### <a name="defaults-and-generated-settings"></a><span data-ttu-id="8744e-134">Valeurs par défaut et paramètres générés</span><span class="sxs-lookup"><span data-stu-id="8744e-134">Defaults and generated settings</span></span>
<span data-ttu-id="8744e-135">Lorsque vous utilisez l’attribut `StatePersistence`, un fournisseur d’état est automatiquement sélectionné pour vous lors de l’exécution au démarrage du service d’acteur.</span><span class="sxs-lookup"><span data-stu-id="8744e-135">When you're using the `StatePersistence` attribute, a state provider is automatically selected for you at runtime when the actor service starts.</span></span> <span data-ttu-id="8744e-136">Toutefois, le nombre de réplicas est défini au moment de la compilation par les outils de génération d’acteurs Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8744e-136">The replica count, however, is set at compile time by the Visual Studio actor build tools.</span></span> <span data-ttu-id="8744e-137">Ces outils génèrent automatiquement un *service par défaut* pour le service d’acteur dans ApplicationManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="8744e-137">The build tools automatically generate a *default service* for the actor service in ApplicationManifest.xml.</span></span> <span data-ttu-id="8744e-138">Les paramètres sont créés pour la **taille minimale du jeu de réplicas** et la **taille cible du jeu de réplicas**.</span><span class="sxs-lookup"><span data-stu-id="8744e-138">Parameters are created for **min replica set size** and **target replica set size**.</span></span>

<span data-ttu-id="8744e-139">Vous pouvez modifier ces paramètres manuellement.</span><span class="sxs-lookup"><span data-stu-id="8744e-139">You can change these parameters manually.</span></span> <span data-ttu-id="8744e-140">Cependant, chaque fois que l’attribut `StatePersistence` est modifié, les paramètres sont rétablis aux valeurs par défaut de taille de jeu de réplicas pour l’attribut `StatePersistence` sélectionné, ce qui remplace toutes les valeurs précédentes.</span><span class="sxs-lookup"><span data-stu-id="8744e-140">But each time the `StatePersistence` attribute is changed, the parameters are set to the default replica set size values for the selected `StatePersistence` attribute, overriding any previous values.</span></span> <span data-ttu-id="8744e-141">En d’autres termes, les valeurs que vous définissez dans le fichier ServiceManifest.xml sont remplacées au moment de la génération *uniquement* quand vous modifiez la valeur d’attribut `StatePersistence`.</span><span class="sxs-lookup"><span data-stu-id="8744e-141">In other words, the values that you set in ServiceManifest.xml are *only* overridden at build time when you change the `StatePersistence` attribute value.</span></span>

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

## <a name="state-manager"></a><span data-ttu-id="8744e-142">Gestionnaire d’état</span><span class="sxs-lookup"><span data-stu-id="8744e-142">State manager</span></span>
<span data-ttu-id="8744e-143">Chaque instance d’acteur possède son propre gestionnaire d’état, c’est-à-dire une structure de données de type dictionnaire qui stocke les paires clé/valeur de manière fiable.</span><span class="sxs-lookup"><span data-stu-id="8744e-143">Every actor instance has its own state manager: a dictionary-like data structure that reliably stores key/value pairs.</span></span> <span data-ttu-id="8744e-144">Le gestionnaire d’état est un wrapper autour d’un fournisseur d’état.</span><span class="sxs-lookup"><span data-stu-id="8744e-144">The state manager is a wrapper around a state provider.</span></span> <span data-ttu-id="8744e-145">Vous pouvez l’utiliser pour stocker des données, quel que soit le réglage de persistance utilisé.</span><span class="sxs-lookup"><span data-stu-id="8744e-145">You can use it to store data regardless of which persistence setting is used.</span></span> <span data-ttu-id="8744e-146">Il ne garantit pas qu’un service d’acteur en cours d’exécution puisse être modifié pour passer d’un paramètre d’état volatil (en mémoire uniquement) à un paramètre d’état persistant via une mise à niveau propagée, tout en conservant les données.</span><span class="sxs-lookup"><span data-stu-id="8744e-146">It does not provide any guarantees that a running actor service can be changed from a volatile (in-memory-only) state setting to a persisted state setting through a rolling upgrade while preserving data.</span></span> <span data-ttu-id="8744e-147">Toutefois, il est possible de modifier le nombre de réplicas d’un service en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="8744e-147">However, it is possible to change replica count for a running service.</span></span>

<span data-ttu-id="8744e-148">Les clés de gestionnaire d’état doivent être des chaînes.</span><span class="sxs-lookup"><span data-stu-id="8744e-148">State manager keys must be strings.</span></span> <span data-ttu-id="8744e-149">Les valeurs sont génériques et peuvent être de n’importe quel type, y compris de types personnalisés.</span><span class="sxs-lookup"><span data-stu-id="8744e-149">Values are generic and can be any type, including custom types.</span></span> <span data-ttu-id="8744e-150">Les valeurs stockées dans le gestionnaire d’état doivent être sérialisables en contrat de données, car elles peuvent être transmises sur le réseau vers d’autres nœuds pendant la réplication et peuvent être écrites sur le disque, en fonction du paramètre de persistance d’état d’un acteur.</span><span class="sxs-lookup"><span data-stu-id="8744e-150">Values stored in the state manager must be data contract serializable because they might be transmitted over the network to other nodes during replication and might be written to disk, depending on an actor's state persistence setting.</span></span>

<span data-ttu-id="8744e-151">Pour la gestion des états, le gestionnaire d’état expose des méthodes de dictionnaire courantes similaires à celles disponibles dans Reliable Dictionary.</span><span class="sxs-lookup"><span data-stu-id="8744e-151">The state manager exposes common dictionary methods for managing state, similar to those found in Reliable Dictionary.</span></span>

### <a name="accessing-state"></a><span data-ttu-id="8744e-152">Accès à l’état</span><span class="sxs-lookup"><span data-stu-id="8744e-152">Accessing state</span></span>
<span data-ttu-id="8744e-153">L’état est accessible via le gestionnaire d’état par l’intermédiaire d’une clé.</span><span class="sxs-lookup"><span data-stu-id="8744e-153">State can be accessed through the state manager by key.</span></span> <span data-ttu-id="8744e-154">Les méthodes du gestionnaire d’état sont toutes asynchrones, car elles peuvent nécessiter des E/S disque lorsque les acteurs sont à l’état persistant.</span><span class="sxs-lookup"><span data-stu-id="8744e-154">State manager methods are all asynchronous because they might require disk I/O when actors have persisted state.</span></span> <span data-ttu-id="8744e-155">Lors du premier accès, les objets d’état sont mis en mémoire cache.</span><span class="sxs-lookup"><span data-stu-id="8744e-155">Upon first access, state objects are cached in memory.</span></span> <span data-ttu-id="8744e-156">Les opérations d’accès répétées permettent d’accéder aux objets directement à partir de la mémoire et sont retournées de façon synchrone sans entraîner d’E/S disque ou de surcharge asynchrone en cas de changement de contexte.</span><span class="sxs-lookup"><span data-stu-id="8744e-156">Repeat access operations access objects directly from memory and return synchronously without incurring disk I/O or asynchronous context-switching overhead.</span></span> <span data-ttu-id="8744e-157">Un objet d’état est supprimé du cache dans les cas suivants :</span><span class="sxs-lookup"><span data-stu-id="8744e-157">A state object is removed from the cache in the following cases:</span></span>

* <span data-ttu-id="8744e-158">Une méthode d’acteur lève une exception non gérée après avoir récupéré un objet à partir du gestionnaire d’état.</span><span class="sxs-lookup"><span data-stu-id="8744e-158">An actor method throws an unhandled exception after it retrieves an object from the state manager.</span></span>
* <span data-ttu-id="8744e-159">Un acteur est réactivé soit après avoir été désactivé, soit en raison d’un échec.</span><span class="sxs-lookup"><span data-stu-id="8744e-159">An actor is reactivated, either after being deactivated or after failure.</span></span>
* <span data-ttu-id="8744e-160">Si le fournisseur d’état écrit l’état sur le disque.</span><span class="sxs-lookup"><span data-stu-id="8744e-160">The state provider pages state to disk.</span></span> <span data-ttu-id="8744e-161">Ce comportement dépend de l’implémentation du fournisseur d’état.</span><span class="sxs-lookup"><span data-stu-id="8744e-161">This behavior depends on the state provider implementation.</span></span> <span data-ttu-id="8744e-162">Le fournisseur d’état par défaut pour le paramètre `Persisted` présente ce comportement.</span><span class="sxs-lookup"><span data-stu-id="8744e-162">The default state provider for the `Persisted` setting has this behavior.</span></span>

<span data-ttu-id="8744e-163">Vous pouvez récupérer l’état à l’aide d’une opération *Get* standard qui lève l’exception `KeyNotFoundException`(C#) ou `NoSuchElementException`(Java) s’il n’existe aucune entrée pour la clé :</span><span class="sxs-lookup"><span data-stu-id="8744e-163">You can retrieve state by using a standard *Get* operation that throws `KeyNotFoundException`(C#) or `NoSuchElementException`(Java) if an entry does not exist for the key:</span></span>

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

<span data-ttu-id="8744e-164">Vous pouvez également récupérer l’état à l’aide d’une opération *TryGet* qui ne lève pas d’exception s’il n’existe aucune entrée pour la clé :</span><span class="sxs-lookup"><span data-stu-id="8744e-164">You can also retrieve state by using a *TryGet* method that does not throw if an entry does not exist for a key:</span></span>

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

### <a name="saving-state"></a><span data-ttu-id="8744e-165">Enregistrement de l’état</span><span class="sxs-lookup"><span data-stu-id="8744e-165">Saving state</span></span>
<span data-ttu-id="8744e-166">Les méthodes de récupération du gestionnaire d’état renvoient une référence à un objet dans la mémoire locale.</span><span class="sxs-lookup"><span data-stu-id="8744e-166">The state manager retrieval methods return a reference to an object in local memory.</span></span> <span data-ttu-id="8744e-167">La modification de cet objet dans la mémoire locale uniquement ne permet pas de l’enregistrer durablement.</span><span class="sxs-lookup"><span data-stu-id="8744e-167">Modifying this object in local memory alone does not cause it to be saved durably.</span></span> <span data-ttu-id="8744e-168">Lorsqu’un objet est récupéré à partir du gestionnaire d’état puis modifié, il doit être réinséré dans le gestionnaire d’état afin d’être enregistré de façon durable.</span><span class="sxs-lookup"><span data-stu-id="8744e-168">When an object is retrieved from the state manager and modified, it must be reinserted into the state manager to be saved durably.</span></span>

<span data-ttu-id="8744e-169">Vous pouvez insérer l’état en utilisant une méthode *Set* inconditionnelle, ce qui équivaut à la syntaxe `dictionary["key"] = value` :</span><span class="sxs-lookup"><span data-stu-id="8744e-169">You can insert state by using an unconditional *Set*, which is the equivalent of the `dictionary["key"] = value` syntax:</span></span>

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

<span data-ttu-id="8744e-170">Vous pouvez ajouter l’état en utilisant une méthode *Add*.</span><span class="sxs-lookup"><span data-stu-id="8744e-170">You can add state by using an *Add* method.</span></span> <span data-ttu-id="8744e-171">Cette méthode lève une exception `InvalidOperationException`(C#) ou `IllegalStateException`(Java) lorsqu’elle tente d’ajouter une clé qui existe.</span><span class="sxs-lookup"><span data-stu-id="8744e-171">This method throws `InvalidOperationException`(C#) or `IllegalStateException`(Java) when it tries to add a key that already exists.</span></span>

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

<span data-ttu-id="8744e-172">Vous pouvez également ajouter l’état en utilisant une méthode *TryAdd*.</span><span class="sxs-lookup"><span data-stu-id="8744e-172">You can also add state by using a *TryAdd* method.</span></span> <span data-ttu-id="8744e-173">Cette méthode ne lève pas d’exception lorsqu’elle tente d’ajouter une clé qui existe déjà.</span><span class="sxs-lookup"><span data-stu-id="8744e-173">This method does not throw when it tries to add a key that already exists.</span></span>

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

<span data-ttu-id="8744e-174">À la fin d’une méthode d’acteur, le gestionnaire d’état enregistre automatiquement toutes les valeurs qui ont été ajoutées ou modifiées par une opération insert ou update.</span><span class="sxs-lookup"><span data-stu-id="8744e-174">At the end of an actor method, the state manager automatically saves any values that have been added or modified by an insert or update operation.</span></span> <span data-ttu-id="8744e-175">Une opération « save » peut inclure la conservation sur disque et la réplication, selon les paramètres utilisés.</span><span class="sxs-lookup"><span data-stu-id="8744e-175">A "save" can include persisting to disk and replication, depending on the settings used.</span></span> <span data-ttu-id="8744e-176">Les valeurs qui n’ont pas été modifiées ne sont pas conservées ou répliquées.</span><span class="sxs-lookup"><span data-stu-id="8744e-176">Values that have not been modified are not persisted or replicated.</span></span> <span data-ttu-id="8744e-177">Si aucune valeur n’a été modifiée, l’opération n’aura aucun effet.</span><span class="sxs-lookup"><span data-stu-id="8744e-177">If no values have been modified, the save operation does nothing.</span></span> <span data-ttu-id="8744e-178">En cas d’échec de l’enregistrement, l’état modifié est ignoré et l’état d’origine est rechargé.</span><span class="sxs-lookup"><span data-stu-id="8744e-178">If saving fails, the modified state is discarded and the original state is reloaded.</span></span>

<span data-ttu-id="8744e-179">Vous pouvez également enregistrer l’état manuellement en appelant la méthode `SaveStateAsync` sur la base d’acteur :</span><span class="sxs-lookup"><span data-stu-id="8744e-179">You can also save state manually by calling the `SaveStateAsync` method on the actor base:</span></span>

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

### <a name="removing-state"></a><span data-ttu-id="8744e-180">Suppression de l’état</span><span class="sxs-lookup"><span data-stu-id="8744e-180">Removing state</span></span>
<span data-ttu-id="8744e-181">Vous pouvez supprimer définitivement l’état du gestionnaire d’état d’un acteur en appelant la méthode *Remove*.</span><span class="sxs-lookup"><span data-stu-id="8744e-181">You can remove state permanently from an actor's state manager by calling the *Remove* method.</span></span> <span data-ttu-id="8744e-182">Cette méthode lève une exception `KeyNotFoundException`(C#) ou `NoSuchElementException`(Java) lorsqu’elle tente de supprimer une clé qui n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="8744e-182">This method throws `KeyNotFoundException`(C#) or `NoSuchElementException`(Java) when it tries to remove a key that doesn't exist.</span></span>

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

<span data-ttu-id="8744e-183">Vous pouvez également supprimer définitivement l’état en utilisant la méthode *TryRemove*.</span><span class="sxs-lookup"><span data-stu-id="8744e-183">You can also remove state permanently by using the *TryRemove* method.</span></span> <span data-ttu-id="8744e-184">Cette méthode ne lève pas d’exception lorsqu’elle tente de supprimer une clé qui n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="8744e-184">This method does not throw when it tries to remove a key that does not exist.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="8744e-185">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8744e-185">Next steps</span></span>

<span data-ttu-id="8744e-186">L’état stocké dans Reliable Actors doit être sérialisé avant d’être écrit sur le disque et répliqué pour une haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="8744e-186">State that's stored in Reliable Actors must be serialized before its written to disk and replicated for high availability.</span></span> <span data-ttu-id="8744e-187">En savoir plus sur [Sérialisation du type d’acteur](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="8744e-187">Learn more about [Actor type serialization](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span></span>

<span data-ttu-id="8744e-188">Ensuite, en savoir plus sur l’[analyse des performances et des diagnostics des acteurs](service-fabric-reliable-actors-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="8744e-188">Next, learn more about [Actor diagnostics and performance monitoring](service-fabric-reliable-actors-diagnostics.md).</span></span>
