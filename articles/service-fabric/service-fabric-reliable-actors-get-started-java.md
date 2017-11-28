---
title: "Créer votre premier microservice Azure basé sur acteur en Java | Microsoft Docs"
description: "Ce didacticiel vous guide dans les étapes de création, de débogage et de déploiement d’un service simple basé sur acteur à l’aide de Service Fabric Reliable Actors."
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
ms.openlocfilehash: 288f1ed1016f50031065e66444d2562427194dc7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="getting-started-with-reliable-actors"></a><span data-ttu-id="eb27b-103">Prise en main de Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="eb27b-103">Getting started with Reliable Actors</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="eb27b-104">C# sur Windows</span><span class="sxs-lookup"><span data-stu-id="eb27b-104">C# on Windows</span></span>](service-fabric-reliable-actors-get-started.md)
> * [<span data-ttu-id="eb27b-105">Java sur Linux</span><span class="sxs-lookup"><span data-stu-id="eb27b-105">Java on Linux</span></span>](service-fabric-reliable-actors-get-started-java.md)
> 
> 

<span data-ttu-id="eb27b-106">Cet article explique les notions de base d’Azure Service Fabric Reliable Actors et vous présente la création et le déploiement d’une application Reliable Actor simple dans Java.</span><span class="sxs-lookup"><span data-stu-id="eb27b-106">This article explains the basics of Azure Service Fabric Reliable Actors and walks you through creating and deploying a simple Reliable Actor application in Java.</span></span>

## <a name="installation-and-setup"></a><span data-ttu-id="eb27b-107">Installation et configuration</span><span class="sxs-lookup"><span data-stu-id="eb27b-107">Installation and setup</span></span>
<span data-ttu-id="eb27b-108">Avant de commencer, assurez-vous que l’environnement de développement Service Fabric est configuré sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="eb27b-108">Before you start, make sure you have the Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="eb27b-109">Si vous devez le configurer, référez-vous à l’article sur la [prise en main sur Mac](service-fabric-get-started-mac.md) ou sur la [prise en main sur Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="eb27b-109">If you need to set it up, go to [getting started on Mac](service-fabric-get-started-mac.md) or [getting started on Linux](service-fabric-get-started-linux.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="eb27b-110">Concepts de base</span><span class="sxs-lookup"><span data-stu-id="eb27b-110">Basic concepts</span></span>
<span data-ttu-id="eb27b-111">Pour prendre en main Reliable Actors, il vous suffit de comprendre quelques concepts de base :</span><span class="sxs-lookup"><span data-stu-id="eb27b-111">To get started with Reliable Actors, you only need to understand a few basic concepts:</span></span>

* <span data-ttu-id="eb27b-112">**Service d’acteur**.</span><span class="sxs-lookup"><span data-stu-id="eb27b-112">**Actor service**.</span></span> <span data-ttu-id="eb27b-113">Les entités Reliable Actors sont empaquetées dans des Reliable Services qui peuvent être déployés dans l’infrastructure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="eb27b-113">Reliable Actors are packaged in Reliable Services that can be deployed in the Service Fabric infrastructure.</span></span> <span data-ttu-id="eb27b-114">Les instances d’acteur sont activées dans une instance de service nommée.</span><span class="sxs-lookup"><span data-stu-id="eb27b-114">Actor instances are activated in a named service instance.</span></span>
* <span data-ttu-id="eb27b-115">**Enregistrement d’acteur**.</span><span class="sxs-lookup"><span data-stu-id="eb27b-115">**Actor registration**.</span></span> <span data-ttu-id="eb27b-116">Comme avec les Reliable Services, un service Reliable Actor doit être enregistré avec le runtime Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="eb27b-116">As with Reliable Services, a Reliable Actor service needs to be registered with the Service Fabric runtime.</span></span> <span data-ttu-id="eb27b-117">En outre, le type d’acteur doit être enregistré auprès du runtime de l’acteur.</span><span class="sxs-lookup"><span data-stu-id="eb27b-117">In addition, the actor type needs to be registered with the Actor runtime.</span></span>
* <span data-ttu-id="eb27b-118">**Interface d’acteur**.</span><span class="sxs-lookup"><span data-stu-id="eb27b-118">**Actor interface**.</span></span> <span data-ttu-id="eb27b-119">L’interface d’acteur est utilisée pour définir une interface publique fortement typée d’un acteur.</span><span class="sxs-lookup"><span data-stu-id="eb27b-119">The actor interface is used to define a strongly typed public interface of an actor.</span></span> <span data-ttu-id="eb27b-120">Dans la terminologie du modèle Reliable Actor, l’interface d’acteur définit les types de messages que l’acteur peut comprendre et traiter.</span><span class="sxs-lookup"><span data-stu-id="eb27b-120">In the Reliable Actor model terminology, the actor interface defines the types of messages that the actor can understand and process.</span></span> <span data-ttu-id="eb27b-121">L’interface d’acteur est utilisée par d’autres acteurs et applications clientes pour « envoyer » (de façon asynchrone) des messages à l’acteur.</span><span class="sxs-lookup"><span data-stu-id="eb27b-121">The actor interface is used by other actors and client applications to "send" (asynchronously) messages to the actor.</span></span> <span data-ttu-id="eb27b-122">Reliable Actors peut implémenter plusieurs interfaces.</span><span class="sxs-lookup"><span data-stu-id="eb27b-122">Reliable Actors can implement multiple interfaces.</span></span>
* <span data-ttu-id="eb27b-123">**Classe ActorProxy**.</span><span class="sxs-lookup"><span data-stu-id="eb27b-123">**ActorProxy class**.</span></span> <span data-ttu-id="eb27b-124">La classe ActorProxy est utilisée par des applications clientes pour appeler les méthodes exposées par le biais de l’interface d’acteur.</span><span class="sxs-lookup"><span data-stu-id="eb27b-124">The ActorProxy class is used by client applications to invoke the methods exposed through the actor interface.</span></span> <span data-ttu-id="eb27b-125">La classe ActorProxy fournit deux fonctionnalités importantes :</span><span class="sxs-lookup"><span data-stu-id="eb27b-125">The ActorProxy class provides two important functionalities:</span></span>
  
  * <span data-ttu-id="eb27b-126">Résolution de noms : elle est en mesure de localiser l’acteur dans le cluster (en recherchant le nœud du cluster dans lequel il est hébergé).</span><span class="sxs-lookup"><span data-stu-id="eb27b-126">Name resolution: It is able to locate the actor in the cluster (find the node of the cluster where it is hosted).</span></span>
  * <span data-ttu-id="eb27b-127">Gestion des défaillances : elle peut retenter les appels de méthode et déterminer de nouveau l’emplacement de l’acteur après une défaillance qui, par exemple, nécessite le déplacement de l’acteur vers un autre nœud du cluster.</span><span class="sxs-lookup"><span data-stu-id="eb27b-127">Failure handling: It can retry method invocations and re-resolve the actor location after, for example, a failure that requires the actor to be relocated to another node in the cluster.</span></span>

<span data-ttu-id="eb27b-128">Les règles suivantes, qui se rapportent aux interfaces d’acteur, sont importantes :</span><span class="sxs-lookup"><span data-stu-id="eb27b-128">The following rules that pertain to actor interfaces are worth mentioning:</span></span>

* <span data-ttu-id="eb27b-129">Les méthodes d'interface d'acteur ne peuvent pas être surchargées.</span><span class="sxs-lookup"><span data-stu-id="eb27b-129">Actor interface methods cannot be overloaded.</span></span>
* <span data-ttu-id="eb27b-130">Les méthodes d’interface d'acteur ne doivent pas avoir de paramètres de sortie, de paramètres de référence ou de paramètres facultatifs.</span><span class="sxs-lookup"><span data-stu-id="eb27b-130">Actor interface methods must not have out, ref, or optional parameters.</span></span>
* <span data-ttu-id="eb27b-131">Les interfaces génériques ne sont pas prises en charge.</span><span class="sxs-lookup"><span data-stu-id="eb27b-131">Generic interfaces are not supported.</span></span>

## <a name="create-an-actor-service"></a><span data-ttu-id="eb27b-132">Création d’un service d’acteur</span><span class="sxs-lookup"><span data-stu-id="eb27b-132">Create an actor service</span></span>
<span data-ttu-id="eb27b-133">Commencez par créer une application Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="eb27b-133">Start by creating a new Service Fabric application.</span></span> <span data-ttu-id="eb27b-134">Le Kit de développement logiciel (SDK) Service Fabric pour Linux comprend un générateur Yeoman qui assure la génération de modèles automatique pour une application Service Fabric avec un service sans état.</span><span class="sxs-lookup"><span data-stu-id="eb27b-134">The Service Fabric SDK for Linux includes a Yeoman generator to provide the scaffolding for a Service Fabric application with a stateless service.</span></span> <span data-ttu-id="eb27b-135">Commencez par exécuter la commande Yeoman suivante :</span><span class="sxs-lookup"><span data-stu-id="eb27b-135">Start by running the following Yeoman command:</span></span>

```bash
$ yo azuresfjava
```

<span data-ttu-id="eb27b-136">Suivez les instructions pour créer un **service Reliable Actor**.</span><span class="sxs-lookup"><span data-stu-id="eb27b-136">Follow the instructions to create a **Reliable Actor Service**.</span></span> <span data-ttu-id="eb27b-137">Pour ce didacticiel, nommez l’application « HelloWorldActorApplication » et l’acteur « HelloWorldActor ».</span><span class="sxs-lookup"><span data-stu-id="eb27b-137">For this tutorial, name the application "HelloWorldActorApplication" and the actor "HelloWorldActor."</span></span> <span data-ttu-id="eb27b-138">La structure suivante sera créée :</span><span class="sxs-lookup"><span data-stu-id="eb27b-138">The following scaffolding will be created:</span></span>

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

## <a name="reliable-actors-basic-building-blocks"></a><span data-ttu-id="eb27b-139">Blocs de construction de base des acteurs fiables</span><span class="sxs-lookup"><span data-stu-id="eb27b-139">Reliable Actors basic building blocks</span></span>
<span data-ttu-id="eb27b-140">Les concepts de base décrits précédemment se traduisent par les blocs de construction de base d’un service Reliable Actor.</span><span class="sxs-lookup"><span data-stu-id="eb27b-140">The basic concepts described earlier translate into the basic building blocks of a Reliable Actor service.</span></span>

### <a name="actor-interface"></a><span data-ttu-id="eb27b-141">Interface d’acteur</span><span class="sxs-lookup"><span data-stu-id="eb27b-141">Actor interface</span></span>
<span data-ttu-id="eb27b-142">Elle contient la définition d'interface de l'acteur.</span><span class="sxs-lookup"><span data-stu-id="eb27b-142">This contains the interface definition for the actor.</span></span> <span data-ttu-id="eb27b-143">Cette interface définit le contrat de l’acteur qui est partagé par l’implémentation de l’acteur et les clients appelant l’acteur, donc il est généralement justifié de le définir dans un endroit distinct de l’implémentation de l’acteur et qui peut être partagé par plusieurs autres services ou application clientes.</span><span class="sxs-lookup"><span data-stu-id="eb27b-143">This interface defines the actor contract that is shared by the actor implementation and the clients calling the actor, so it typically makes sense to define it in a place that is separate from the actor implementation and can be shared by multiple other services or client applications.</span></span>

<span data-ttu-id="eb27b-144">`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:</span><span class="sxs-lookup"><span data-stu-id="eb27b-144">`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:</span></span>

```java
public interface HelloWorldActor extends Actor {
    @Readonly   
    CompletableFuture<Integer> getCountAsync();

    CompletableFuture<?> setCountAsync(int count);
}
```

### <a name="actor-service"></a><span data-ttu-id="eb27b-145">Service d’acteur</span><span class="sxs-lookup"><span data-stu-id="eb27b-145">Actor service</span></span>
<span data-ttu-id="eb27b-146">Il contient votre implémentation d’acteur et le code d’inscription de l’acteur.</span><span class="sxs-lookup"><span data-stu-id="eb27b-146">This contains your actor implementation and actor registration code.</span></span> <span data-ttu-id="eb27b-147">La classe d’acteur implémente l’interface d’acteur.</span><span class="sxs-lookup"><span data-stu-id="eb27b-147">The actor class implements the actor interface.</span></span> <span data-ttu-id="eb27b-148">Il s’agit de l’endroit dans quelquel votre acteur effectue son travail.</span><span class="sxs-lookup"><span data-stu-id="eb27b-148">This is where your actor does its work.</span></span>

<span data-ttu-id="eb27b-149">`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:</span><span class="sxs-lookup"><span data-stu-id="eb27b-149">`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:</span></span>

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

### <a name="actor-registration"></a><span data-ttu-id="eb27b-150">Enregistrement d’acteur</span><span class="sxs-lookup"><span data-stu-id="eb27b-150">Actor registration</span></span>
<span data-ttu-id="eb27b-151">Le service de l’acteur doit être enregistré avec un type de service dans le runtime Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="eb27b-151">The actor service must be registered with a service type in the Service Fabric runtime.</span></span> <span data-ttu-id="eb27b-152">Afin que le service de l’acteur exécute vos instances d’acteur, le type d’acteur doit également être enregistré auprès du Service de l’acteur.</span><span class="sxs-lookup"><span data-stu-id="eb27b-152">In order for the Actor Service to run your actor instances, your actor type must also be registered with the Actor Service.</span></span> <span data-ttu-id="eb27b-153">La méthode d’inscription `ActorRuntime` effectue ce travail pour les acteurs.</span><span class="sxs-lookup"><span data-stu-id="eb27b-153">The `ActorRuntime` registration method performs this work for actors.</span></span>

<span data-ttu-id="eb27b-154">`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:</span><span class="sxs-lookup"><span data-stu-id="eb27b-154">`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:</span></span>

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

### <a name="test-client"></a><span data-ttu-id="eb27b-155">Test client</span><span class="sxs-lookup"><span data-stu-id="eb27b-155">Test client</span></span>
<span data-ttu-id="eb27b-156">Il s’agit d’une application cliente de test simple que vous pouvez exécuter séparément à partir de l’application Service Fabric pour tester votre service d’acteur.</span><span class="sxs-lookup"><span data-stu-id="eb27b-156">This is a simple test client application you can run separately from the Service Fabric application to test your actor service.</span></span> <span data-ttu-id="eb27b-157">Voici un exemple d’endroit où l’ActorProxy peut être utilisé pour activer et communiquer avec des instances d’acteur.</span><span class="sxs-lookup"><span data-stu-id="eb27b-157">This is an example of where the ActorProxy can be used to activate and communicate with actor instances.</span></span> <span data-ttu-id="eb27b-158">Il n’est pas déployé avec votre service.</span><span class="sxs-lookup"><span data-stu-id="eb27b-158">It does not get deployed with your service.</span></span>

### <a name="the-application"></a><span data-ttu-id="eb27b-159">L'application</span><span class="sxs-lookup"><span data-stu-id="eb27b-159">The application</span></span>
<span data-ttu-id="eb27b-160">Enfin, les packages d’applications, le service d’acteur et tout autre service, que vous pouvez ajouter ensemble à l’avenir pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="eb27b-160">Finally, the application packages the actor service and any other services you might add in the future together for deployment.</span></span> <span data-ttu-id="eb27b-161">Elle contient le fichier *ApplicationManifest.xml* et des espaces réservés pour le package de service d’acteur.</span><span class="sxs-lookup"><span data-stu-id="eb27b-161">It contains the *ApplicationManifest.xml* and place holders for the actor service package.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="eb27b-162">Exécution de l'application</span><span class="sxs-lookup"><span data-stu-id="eb27b-162">Run the application</span></span>

<span data-ttu-id="eb27b-163">La génération de modèles automatique Yeoman inclut un script Gradle permettant de créer l’application et des scripts bash permettant le déploiement et la suppression de l’application.</span><span class="sxs-lookup"><span data-stu-id="eb27b-163">The Yeoman scaffolding includes a gradle script to build the application and bash scripts to deploy and remove the application.</span></span> <span data-ttu-id="eb27b-164">Pour déployer l’application, commencez par créer l’application avec Gradle :</span><span class="sxs-lookup"><span data-stu-id="eb27b-164">To deploy the application, first build the application with gradle:</span></span>

```bash
$ gradle
```

<span data-ttu-id="eb27b-165">Cela génère un package d’application Service Fabric qui peut être déployé à l’aide des outils de l’interface de ligne de commande (CLI) Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="eb27b-165">This will produce a Service Fabric application package that can be deployed using Service Fabric CLI tools.</span></span>

### <a name="deploy-service-fabric-cli"></a><span data-ttu-id="eb27b-166">Déployer l’interface CLI Service Fabric</span><span class="sxs-lookup"><span data-stu-id="eb27b-166">Deploy Service Fabric CLI</span></span>

<span data-ttu-id="eb27b-167">Le script install.sh contient les commandes de l’interface CLI Service Fabric (sfctl) nécessaires pour déployer le package d’application.</span><span class="sxs-lookup"><span data-stu-id="eb27b-167">The install.sh script contains the necessary Service Fabric CLI (sfctl) commands to deploy the application package.</span></span>
<span data-ttu-id="eb27b-168">Exécutez le script install.sh pour déployer l’application.</span><span class="sxs-lookup"><span data-stu-id="eb27b-168">Run the install.sh script to deploy the application.</span></span>

```bash
$ ./install.sh
```

## <a name="next-steps"></a><span data-ttu-id="eb27b-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="eb27b-169">Next steps</span></span>

* [<span data-ttu-id="eb27b-170">Bien démarrer avec l’interface de ligne de commande Service Fabric</span><span class="sxs-lookup"><span data-stu-id="eb27b-170">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
