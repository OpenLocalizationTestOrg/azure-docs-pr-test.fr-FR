---
title: "aaaCreate votre premier microservice Azure basé sur acteur dans Java | Documents Microsoft"
description: "Ce didacticiel vous guide tout au long des étapes hello de création, de débogage et de déploiement d’un service basé sur acteur simple à l’aide de l’infrastructure de Service Reliable Actors."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d31dc8ab-9760-4619-a641-facb8324c759
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/04/2017
ms.author: vturecek
ms.openlocfilehash: 24718a8d7034360c53597f139169580f1a6ce732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-reliable-actors"></a><span data-ttu-id="ba599-103">Prise en main de Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="ba599-103">Getting started with Reliable Actors</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ba599-104">C# sur Windows</span><span class="sxs-lookup"><span data-stu-id="ba599-104">C# on Windows</span></span>](service-fabric-reliable-actors-get-started.md)
> * [<span data-ttu-id="ba599-105">Java sur Linux</span><span class="sxs-lookup"><span data-stu-id="ba599-105">Java on Linux</span></span>](service-fabric-reliable-actors-get-started-java.md)
> 
> 

<span data-ttu-id="ba599-106">Cet article explique les principes fondamentaux de hello de Azure Service Fabric Reliable Actors et vous guide dans la création et déploiement d’une application fiable acteur simple en Java.</span><span class="sxs-lookup"><span data-stu-id="ba599-106">This article explains hello basics of Azure Service Fabric Reliable Actors and walks you through creating and deploying a simple Reliable Actor application in Java.</span></span>

## <a name="installation-and-setup"></a><span data-ttu-id="ba599-107">Installation et configuration</span><span class="sxs-lookup"><span data-stu-id="ba599-107">Installation and setup</span></span>
<span data-ttu-id="ba599-108">Avant de commencer, assurez-vous que vous disposez d’environnement de développement de Service Fabric hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="ba599-108">Before you start, make sure you have hello Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="ba599-109">Si vous avez besoin de tooset, ça trop[mise en route sur Mac](service-fabric-get-started-mac.md) ou [mise en route sur Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="ba599-109">If you need tooset it up, go too[getting started on Mac](service-fabric-get-started-mac.md) or [getting started on Linux](service-fabric-get-started-linux.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="ba599-110">Concepts de base</span><span class="sxs-lookup"><span data-stu-id="ba599-110">Basic concepts</span></span>
<span data-ttu-id="ba599-111">tooget main Reliable Actors, vous seulement devez toounderstand quelques concepts de base :</span><span class="sxs-lookup"><span data-stu-id="ba599-111">tooget started with Reliable Actors, you only need toounderstand a few basic concepts:</span></span>

* <span data-ttu-id="ba599-112">**Service d’acteur**.</span><span class="sxs-lookup"><span data-stu-id="ba599-112">**Actor service**.</span></span> <span data-ttu-id="ba599-113">Reliable Actors sont empaquetées dans des Services fiables qui peut être déployé dans une infrastructure de Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="ba599-113">Reliable Actors are packaged in Reliable Services that can be deployed in hello Service Fabric infrastructure.</span></span> <span data-ttu-id="ba599-114">Les instances d’acteur sont activées dans une instance de service nommée.</span><span class="sxs-lookup"><span data-stu-id="ba599-114">Actor instances are activated in a named service instance.</span></span>
* <span data-ttu-id="ba599-115">**Enregistrement d’acteur**.</span><span class="sxs-lookup"><span data-stu-id="ba599-115">**Actor registration**.</span></span> <span data-ttu-id="ba599-116">Comme avec les Services fiables, un service Reliable Actor doit toobe inscrit avec le runtime du Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="ba599-116">As with Reliable Services, a Reliable Actor service needs toobe registered with hello Service Fabric runtime.</span></span> <span data-ttu-id="ba599-117">En outre, le type d’acteur hello doit toobe inscrit avec le runtime d’acteur hello.</span><span class="sxs-lookup"><span data-stu-id="ba599-117">In addition, hello actor type needs toobe registered with hello Actor runtime.</span></span>
* <span data-ttu-id="ba599-118">**Interface d’acteur**.</span><span class="sxs-lookup"><span data-stu-id="ba599-118">**Actor interface**.</span></span> <span data-ttu-id="ba599-119">interface d’acteur Hello est toodefine utilisé une interface publique fortement typée d’un acteur.</span><span class="sxs-lookup"><span data-stu-id="ba599-119">hello actor interface is used toodefine a strongly typed public interface of an actor.</span></span> <span data-ttu-id="ba599-120">Bonjour terminologie relative aux modèles de Reliable Actor, interface d’acteur hello définit hello types de messages hello acteur peuvent comprendre et traiter.</span><span class="sxs-lookup"><span data-stu-id="ba599-120">In hello Reliable Actor model terminology, hello actor interface defines hello types of messages that hello actor can understand and process.</span></span> <span data-ttu-id="ba599-121">interface d’acteur Hello est utilisé par d’autres acteurs et les applications clientes trop « envoient » (de façon asynchrone) acteur toohello de messages.</span><span class="sxs-lookup"><span data-stu-id="ba599-121">hello actor interface is used by other actors and client applications too"send" (asynchronously) messages toohello actor.</span></span> <span data-ttu-id="ba599-122">Reliable Actors peut implémenter plusieurs interfaces.</span><span class="sxs-lookup"><span data-stu-id="ba599-122">Reliable Actors can implement multiple interfaces.</span></span>
* <span data-ttu-id="ba599-123">**Classe ActorProxy**.</span><span class="sxs-lookup"><span data-stu-id="ba599-123">**ActorProxy class**.</span></span> <span data-ttu-id="ba599-124">Hello ActorProxy classe est utilisée par le client applications tooinvoke hello méthodes exposées via l’interface d’acteur hello.</span><span class="sxs-lookup"><span data-stu-id="ba599-124">hello ActorProxy class is used by client applications tooinvoke hello methods exposed through hello actor interface.</span></span> <span data-ttu-id="ba599-125">Hello ActorProxy classe fournit deux fonctionnalités importantes :</span><span class="sxs-lookup"><span data-stu-id="ba599-125">hello ActorProxy class provides two important functionalities:</span></span>
  
  * <span data-ttu-id="ba599-126">La résolution de noms : il s’agit d’acteur de hello toolocate en mesure de cluster de hello (rechercher le nœud hello du cluster hello où il est hébergé).</span><span class="sxs-lookup"><span data-stu-id="ba599-126">Name resolution: It is able toolocate hello actor in hello cluster (find hello node of hello cluster where it is hosted).</span></span>
  * <span data-ttu-id="ba599-127">Gestion de défaillance : il peut réessayer d’appels de méthode et de résoudre cet emplacement hello intervenant après avoir, par exemple, un échec qui nécessite hello acteur toobe déplacé tooanother nœud de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="ba599-127">Failure handling: It can retry method invocations and re-resolve hello actor location after, for example, a failure that requires hello actor toobe relocated tooanother node in hello cluster.</span></span>

<span data-ttu-id="ba599-128">Hello, suivant les règles qui se rapportent les interfaces tooactor est intéressant de mentionner :</span><span class="sxs-lookup"><span data-stu-id="ba599-128">hello following rules that pertain tooactor interfaces are worth mentioning:</span></span>

* <span data-ttu-id="ba599-129">Les méthodes d'interface d'acteur ne peuvent pas être surchargées.</span><span class="sxs-lookup"><span data-stu-id="ba599-129">Actor interface methods cannot be overloaded.</span></span>
* <span data-ttu-id="ba599-130">Les méthodes d’interface d'acteur ne doivent pas avoir de paramètres de sortie, de paramètres de référence ou de paramètres facultatifs.</span><span class="sxs-lookup"><span data-stu-id="ba599-130">Actor interface methods must not have out, ref, or optional parameters.</span></span>
* <span data-ttu-id="ba599-131">Les interfaces génériques ne sont pas prises en charge.</span><span class="sxs-lookup"><span data-stu-id="ba599-131">Generic interfaces are not supported.</span></span>

## <a name="create-an-actor-service"></a><span data-ttu-id="ba599-132">Création d’un service d’acteur</span><span class="sxs-lookup"><span data-stu-id="ba599-132">Create an actor service</span></span>
<span data-ttu-id="ba599-133">Commencez par créer une application Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ba599-133">Start by creating a new Service Fabric application.</span></span> <span data-ttu-id="ba599-134">Hello SDK de l’infrastructure de Service pour Linux comprend un Yeoman générateur tooprovide hello génération de modèles automatique pour une application de Service Fabric avec un service sans état.</span><span class="sxs-lookup"><span data-stu-id="ba599-134">hello Service Fabric SDK for Linux includes a Yeoman generator tooprovide hello scaffolding for a Service Fabric application with a stateless service.</span></span> <span data-ttu-id="ba599-135">Commencez par exécuter hello suivant Yeoman commande :</span><span class="sxs-lookup"><span data-stu-id="ba599-135">Start by running hello following Yeoman command:</span></span>

```bash
$ yo azuresfjava
```

<span data-ttu-id="ba599-136">Suivez hello instructions toocreate un **fiable acteur Service**.</span><span class="sxs-lookup"><span data-stu-id="ba599-136">Follow hello instructions toocreate a **Reliable Actor Service**.</span></span> <span data-ttu-id="ba599-137">Pour ce didacticiel, nommez hello application « HelloWorldActorApplication » et hello acteur « HelloWorldActor ».</span><span class="sxs-lookup"><span data-stu-id="ba599-137">For this tutorial, name hello application "HelloWorldActorApplication" and hello actor "HelloWorldActor."</span></span> <span data-ttu-id="ba599-138">Hello suivant la génération de modèles automatique sera créé :</span><span class="sxs-lookup"><span data-stu-id="ba599-138">hello following scaffolding will be created:</span></span>

```bash
HelloWorldActorApplication/
├── build.gradle
├── HelloWorldActor
│   ├── build.gradle
│   ├── settings.gradle
│   └── src
│       └── reliableactor
│           ├── HelloWorldActorHost.java
│           └── HelloWorldActorImpl.java
├── HelloWorldActorApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldActorPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   ├── _readme.txt
│       │   └── Settings.xml
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── HelloWorldActorInterface
│   ├── build.gradle
│   └── src
│       └── reliableactor
│           └── HelloWorldActor.java
├── HelloWorldActorTestClient
│   ├── build.gradle
│   ├── settings.gradle
│   ├── src
│   │   └── reliableactor
│   │       └── test
│   │           └── HelloWorldActorTestClient.java
│   └── testclient.sh
├── install.sh
├── settings.gradle
└── uninstall.sh
```

## <a name="reliable-actors-basic-building-blocks"></a><span data-ttu-id="ba599-139">Blocs de construction de base des acteurs fiables</span><span class="sxs-lookup"><span data-stu-id="ba599-139">Reliable Actors basic building blocks</span></span>
<span data-ttu-id="ba599-140">concepts de base Hello décrits précédemment se traduisent par hello blocs de construction d’un service Reliable Actor.</span><span class="sxs-lookup"><span data-stu-id="ba599-140">hello basic concepts described earlier translate into hello basic building blocks of a Reliable Actor service.</span></span>

### <a name="actor-interface"></a><span data-ttu-id="ba599-141">Interface d’acteur</span><span class="sxs-lookup"><span data-stu-id="ba599-141">Actor interface</span></span>
<span data-ttu-id="ba599-142">Il contient la définition d’interface hello pour l’acteur de hello.</span><span class="sxs-lookup"><span data-stu-id="ba599-142">This contains hello interface definition for hello actor.</span></span> <span data-ttu-id="ba599-143">Cette interface définit le contrat d’acteur hello qui est partagé par implémentation d’acteur hello et clients hello appelant acteur de hello, il est donc généralement toodefine de sens dans un emplacement séparer d’implémentation d’acteur hello et peut être partagé par plusieurs autres les services ou les applications clientes.</span><span class="sxs-lookup"><span data-stu-id="ba599-143">This interface defines hello actor contract that is shared by hello actor implementation and hello clients calling hello actor, so it typically makes sense toodefine it in a place that is separate from hello actor implementation and can be shared by multiple other services or client applications.</span></span>

<span data-ttu-id="ba599-144">`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:</span><span class="sxs-lookup"><span data-stu-id="ba599-144">`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:</span></span>

```java
public interface HelloWorldActor extends Actor {
    @Readonly   
    CompletableFuture<Integer> getCountAsync();

    CompletableFuture<?> setCountAsync(int count);
}
```

### <a name="actor-service"></a><span data-ttu-id="ba599-145">Service d’acteur</span><span class="sxs-lookup"><span data-stu-id="ba599-145">Actor service</span></span>
<span data-ttu-id="ba599-146">Il contient votre implémentation d’acteur et le code d’inscription de l’acteur.</span><span class="sxs-lookup"><span data-stu-id="ba599-146">This contains your actor implementation and actor registration code.</span></span> <span data-ttu-id="ba599-147">classe d’acteur Hello implémente l’interface d’acteur hello.</span><span class="sxs-lookup"><span data-stu-id="ba599-147">hello actor class implements hello actor interface.</span></span> <span data-ttu-id="ba599-148">Il s’agit de l’endroit dans quelquel votre acteur effectue son travail.</span><span class="sxs-lookup"><span data-stu-id="ba599-148">This is where your actor does its work.</span></span>

<span data-ttu-id="ba599-149">`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:</span><span class="sxs-lookup"><span data-stu-id="ba599-149">`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:</span></span>

```java
@ActorServiceAttribute(name = "HelloWorldActor.HelloWorldActorService")
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class HelloWorldActorImpl extends ReliableActor implements HelloWorldActor {
    Logger logger = Logger.getLogger(this.getClass().getName());

    protected CompletableFuture<?> onActivateAsync() {
        logger.log(Level.INFO, "onActivateAsync");

        return this.stateManager().tryAddStateAsync("count", 0);
    }

    @Override
    public CompletableFuture<Integer> getCountAsync() {
        logger.log(Level.INFO, "Getting current count value");
        return this.stateManager().getStateAsync("count");
    }

    @Override
    public CompletableFuture<?> setCountAsync(int count) {
        logger.log(Level.INFO, "Setting current count value {0}", count);
        return this.stateManager().addOrUpdateStateAsync("count", count, (key, value) -> count > value ? count : value);
    }
}
```

### <a name="actor-registration"></a><span data-ttu-id="ba599-150">Enregistrement d’acteur</span><span class="sxs-lookup"><span data-stu-id="ba599-150">Actor registration</span></span>
<span data-ttu-id="ba599-151">service d’acteur Hello doit être enregistré avec un type de service dans le runtime du Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="ba599-151">hello actor service must be registered with a service type in hello Service Fabric runtime.</span></span> <span data-ttu-id="ba599-152">Dans commande pour hello acteur Service toorun vos instances de l’acteur, votre type d’acteur doit également être enregistré avec hello Service d’acteur.</span><span class="sxs-lookup"><span data-stu-id="ba599-152">In order for hello Actor Service toorun your actor instances, your actor type must also be registered with hello Actor Service.</span></span> <span data-ttu-id="ba599-153">Hello `ActorRuntime` méthode d’inscription exécute cette tâche pour acteurs.</span><span class="sxs-lookup"><span data-stu-id="ba599-153">hello `ActorRuntime` registration method performs this work for actors.</span></span>

<span data-ttu-id="ba599-154">`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:</span><span class="sxs-lookup"><span data-stu-id="ba599-154">`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:</span></span>

```java
public class HelloWorldActorHost {

    public static void main(String[] args) throws Exception {

        try {
            ActorRuntime.registerActorAsync(HelloWorldActorImpl.class, (context, actorType) -> new ActorServiceImpl(context, actorType, ()-> new HelloWorldActorImpl()), Duration.ofSeconds(10));

            Thread.sleep(Long.MAX_VALUE);

        } catch (Exception e) {
            e.printStackTrace();
            throw e;
        }
    }
}
```

### <a name="test-client"></a><span data-ttu-id="ba599-155">Test client</span><span class="sxs-lookup"><span data-stu-id="ba599-155">Test client</span></span>
<span data-ttu-id="ba599-156">Il s’agit d’une application cliente de test simple vous pouvez exécuter séparément hello Service Fabric application tootest votre service d’acteur.</span><span class="sxs-lookup"><span data-stu-id="ba599-156">This is a simple test client application you can run separately from hello Service Fabric application tootest your actor service.</span></span> <span data-ttu-id="ba599-157">Il s’agit d’un exemple d’où hello ActorProxy peut être utilisé tooactivate et communiquer avec les instances de l’acteur.</span><span class="sxs-lookup"><span data-stu-id="ba599-157">This is an example of where hello ActorProxy can be used tooactivate and communicate with actor instances.</span></span> <span data-ttu-id="ba599-158">Il n’est pas déployé avec votre service.</span><span class="sxs-lookup"><span data-stu-id="ba599-158">It does not get deployed with your service.</span></span>

### <a name="hello-application"></a><span data-ttu-id="ba599-159">application Hello</span><span class="sxs-lookup"><span data-stu-id="ba599-159">hello application</span></span>
<span data-ttu-id="ba599-160">Enfin, les packages d’application hello hello service d’acteur et d’autres services, que vous pouvez ajouter dans hello future ensemble pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="ba599-160">Finally, hello application packages hello actor service and any other services you might add in hello future together for deployment.</span></span> <span data-ttu-id="ba599-161">Il contient hello *ApplicationManifest.xml* et espaces réservés pour le package de service d’acteur hello.</span><span class="sxs-lookup"><span data-stu-id="ba599-161">It contains hello *ApplicationManifest.xml* and place holders for hello actor service package.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="ba599-162">Exécutez l’application hello</span><span class="sxs-lookup"><span data-stu-id="ba599-162">Run hello application</span></span>

<span data-ttu-id="ba599-163">Hello Yeoman la structure inclut un gradle script toobuild hello d’application et un interpréteur de commandes de scripts toodeploy et supprimer l’application.</span><span class="sxs-lookup"><span data-stu-id="ba599-163">hello Yeoman scaffolding includes a gradle script toobuild hello application and bash scripts toodeploy and remove the application.</span></span> <span data-ttu-id="ba599-164">application de hello toodeploy, première application hello de build avec gradle :</span><span class="sxs-lookup"><span data-stu-id="ba599-164">toodeploy hello application, first build hello application with gradle:</span></span>

```bash
$ gradle
```

<span data-ttu-id="ba599-165">Cela génère un package d’application Service Fabric qui peut être déployé à l’aide des outils de l’interface de ligne de commande (CLI) Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ba599-165">This will produce a Service Fabric application package that can be deployed using Service Fabric CLI tools.</span></span>

### <a name="deploy-service-fabric-cli"></a><span data-ttu-id="ba599-166">Déployer l’interface CLI Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ba599-166">Deploy Service Fabric CLI</span></span>

<span data-ttu-id="ba599-167">script de install.sh Hello contient hello nécessaire Service Fabric CLI (sfctl) commandes toodeploy hello package d’application.</span><span class="sxs-lookup"><span data-stu-id="ba599-167">hello install.sh script contains hello necessary Service Fabric CLI (sfctl) commands toodeploy hello application package.</span></span>
<span data-ttu-id="ba599-168">Exécutez hello install.sh script toodeploy hello application.</span><span class="sxs-lookup"><span data-stu-id="ba599-168">Run hello install.sh script toodeploy hello application.</span></span>

```bash
$ ./install.sh
```

## <a name="next-steps"></a><span data-ttu-id="ba599-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ba599-169">Next steps</span></span>

* [<span data-ttu-id="ba599-170">Prise en main de l’interface de ligne de commande Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ba599-170">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
