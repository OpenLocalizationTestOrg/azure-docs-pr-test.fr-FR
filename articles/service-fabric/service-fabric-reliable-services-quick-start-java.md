---
title: aaaCreate votre premier microservice de Azure fiable dans Java | Documents Microsoft
description: "Introduction toocreating une application Microsoft Azure Service Fabric avec et sans état des services."
services: service-fabric
documentationcenter: java
author: vturecek
manager: timlt
editor: 
ms.assetid: 7831886f-7ec4-4aef-95c5-b2469a5b7b5d
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 577d96591797bbfe6be5c1094426b5f1435cca0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-reliable-services"></a><span data-ttu-id="6d8a6-103">Prise en main de Reliable Services</span><span class="sxs-lookup"><span data-stu-id="6d8a6-103">Get started with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6d8a6-104">C# sur Windows</span><span class="sxs-lookup"><span data-stu-id="6d8a6-104">C# on Windows</span></span>](service-fabric-reliable-services-quick-start.md)
> * [<span data-ttu-id="6d8a6-105">Java sur Linux</span><span class="sxs-lookup"><span data-stu-id="6d8a6-105">Java on Linux</span></span>](service-fabric-reliable-services-quick-start-java.md)
>
>

<span data-ttu-id="6d8a6-106">Cet article explique les principes fondamentaux de hello de Azure Service Fabric des Services fiables et vous guide dans la création et déploiement d’une simple application de Service fiable écrite en Java.</span><span class="sxs-lookup"><span data-stu-id="6d8a6-106">This article explains hello basics of Azure Service Fabric Reliable Services and walks you through creating and deploying a simple Reliable Service application written in Java.</span></span> <span data-ttu-id="6d8a6-107">Cette vidéo Microsoft Virtual Academy montre également comment toocreate un service fiable sans état :<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965"></span><span class="sxs-lookup"><span data-stu-id="6d8a6-107">This Microsoft Virtual Academy video also shows you how toocreate a stateless Reliable service: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965"></span></span>  
<img src="./media/service-fabric-reliable-services-quick-start-java/ReliableServicesJavaVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="installation-and-setup"></a><span data-ttu-id="6d8a6-108">Installation et configuration</span><span class="sxs-lookup"><span data-stu-id="6d8a6-108">Installation and setup</span></span>
<span data-ttu-id="6d8a6-109">Avant de commencer, assurez-vous que vous disposez d’environnement de développement de Service Fabric hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="6d8a6-109">Before you start, make sure you have hello Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="6d8a6-110">Si vous avez besoin de tooset, ça trop[mise en route sur Mac](service-fabric-get-started-mac.md) ou [mise en route sur Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="6d8a6-110">If you need tooset it up, go too[getting started on Mac](service-fabric-get-started-mac.md) or [getting started on Linux](service-fabric-get-started-linux.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="6d8a6-111">Concepts de base</span><span class="sxs-lookup"><span data-stu-id="6d8a6-111">Basic concepts</span></span>
<span data-ttu-id="6d8a6-112">tooget en main des Services fiables, vous seulement devez toounderstand quelques concepts de base :</span><span class="sxs-lookup"><span data-stu-id="6d8a6-112">tooget started with Reliable Services, you only need toounderstand a few basic concepts:</span></span>

* <span data-ttu-id="6d8a6-113">**Type de service** : il s’agit de l’implémentation de votre service.</span><span class="sxs-lookup"><span data-stu-id="6d8a6-113">**Service type**: This is your service implementation.</span></span> <span data-ttu-id="6d8a6-114">Il est défini par la classe hello vous écrivez qui étend `StatelessService` et tout autre code ou les dépendances utilisés ici, avec un nom et un numéro de version.</span><span class="sxs-lookup"><span data-stu-id="6d8a6-114">It is defined by hello class you write that extends `StatelessService` and any other code or dependencies used therein, along with a name and a version number.</span></span>
* <span data-ttu-id="6d8a6-115">**Instance de service nommée**: toorun votre service, vous créez des instances nommées de votre type de service, beaucoup comme vous créez des instances d’objet d’un type de classe.</span><span class="sxs-lookup"><span data-stu-id="6d8a6-115">**Named service instance**: toorun your service, you create named instances of your service type, much like you create object instances of a class type.</span></span> <span data-ttu-id="6d8a6-116">Les instances de service sont en fait des instanciations d’objet de votre classe de service que vous écrivez.</span><span class="sxs-lookup"><span data-stu-id="6d8a6-116">Service instances are in fact object instantiations of your service class that you write.</span></span>
* <span data-ttu-id="6d8a6-117">**Hôte de service**: hello nommé des instances de service que vous créez toorun nécessaire à l’intérieur d’un ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="6d8a6-117">**Service host**: hello named service instances you create need toorun inside a host.</span></span> <span data-ttu-id="6d8a6-118">hôte de service Hello est simplement un processus dans lequel les instances de votre service peuvent exécuter.</span><span class="sxs-lookup"><span data-stu-id="6d8a6-118">hello service host is just a process where instances of your service can run.</span></span>
* <span data-ttu-id="6d8a6-119">**Inscription du service** : l’inscription rassemble tous les éléments.</span><span class="sxs-lookup"><span data-stu-id="6d8a6-119">**Service registration**: Registration brings everything together.</span></span> <span data-ttu-id="6d8a6-120">Hello service type doit être inscrit avec hello Service Fabric runtime dans un service hôte tooallow Service Fabric toocreate ses instances toorun.</span><span class="sxs-lookup"><span data-stu-id="6d8a6-120">hello service type must be registered with hello Service Fabric runtime in a service host tooallow Service Fabric toocreate instances of it toorun.</span></span>  

## <a name="create-a-stateless-service"></a><span data-ttu-id="6d8a6-121">Création d'un service sans état</span><span class="sxs-lookup"><span data-stu-id="6d8a6-121">Create a stateless service</span></span>
<span data-ttu-id="6d8a6-122">Commencez par créer une application Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6d8a6-122">Start by creating a Service Fabric application.</span></span> <span data-ttu-id="6d8a6-123">Hello SDK de l’infrastructure de Service pour Linux comprend un Yeoman générateur tooprovide hello génération de modèles automatique pour une application de Service Fabric avec un service sans état.</span><span class="sxs-lookup"><span data-stu-id="6d8a6-123">hello Service Fabric SDK for Linux includes a Yeoman generator tooprovide hello scaffolding for a Service Fabric application with a stateless service.</span></span> <span data-ttu-id="6d8a6-124">Commencez par exécuter hello suivant Yeoman commande :</span><span class="sxs-lookup"><span data-stu-id="6d8a6-124">Start by running hello following Yeoman command:</span></span>

```bash
$ yo azuresfjava
```

<span data-ttu-id="6d8a6-125">Suivez hello instructions toocreate un **un Service fiable sans état**.</span><span class="sxs-lookup"><span data-stu-id="6d8a6-125">Follow hello instructions toocreate a **Reliable Stateless Service**.</span></span> <span data-ttu-id="6d8a6-126">Pour ce didacticiel, l’application hello de nom « HelloWorldApplication » et hello service « HelloWorld ».</span><span class="sxs-lookup"><span data-stu-id="6d8a6-126">For this tutorial, name hello application "HelloWorldApplication" and hello service "HelloWorld".</span></span> <span data-ttu-id="6d8a6-127">résultat de Hello contient des répertoires pour hello `HelloWorldApplication` et `HelloWorld`.</span><span class="sxs-lookup"><span data-stu-id="6d8a6-127">hello result includes directories for hello `HelloWorldApplication` and `HelloWorld`.</span></span>

```bash
HelloWorldApplication/
├── build.gradle
├── HelloWorld
│   ├── build.gradle
│   └── src
│       └── statelessservice
│           ├── HelloWorldServiceHost.java
│           └── HelloWorldService.java
├── HelloWorldApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   └── _readme.txt
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── install.sh
├── settings.gradle
└── uninstall.sh
```

## <a name="implement-hello-service"></a><span data-ttu-id="6d8a6-128">Implémenter le service de hello</span><span class="sxs-lookup"><span data-stu-id="6d8a6-128">Implement hello service</span></span>
<span data-ttu-id="6d8a6-129">Ouvrez **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**.</span><span class="sxs-lookup"><span data-stu-id="6d8a6-129">Open **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**.</span></span> <span data-ttu-id="6d8a6-130">Cette classe définit le type de service hello et peut exécuter n’importe quel code.</span><span class="sxs-lookup"><span data-stu-id="6d8a6-130">This class defines hello service type, and can run any code.</span></span> <span data-ttu-id="6d8a6-131">API de service Hello fournit deux points d’entrée pour votre code :</span><span class="sxs-lookup"><span data-stu-id="6d8a6-131">hello service API provides two entry points for your code:</span></span>

* <span data-ttu-id="6d8a6-132">Une méthode de point d’entrée de durée indéterminée, appelée `runAsync()`, avec laquelle vous pouvez commencer l’exécution de toute charge de travail, y compris les charges de travail de calcul de longue durée.</span><span class="sxs-lookup"><span data-stu-id="6d8a6-132">An open-ended entry point method, called `runAsync()`, where you can begin executing any workloads, including long-running compute workloads.</span></span>

```java
@Override
protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {
    ...
}
```

* <span data-ttu-id="6d8a6-133">Un point d’entrée de communication où vous pouvez connecter la pile de communication de votre choix.</span><span class="sxs-lookup"><span data-stu-id="6d8a6-133">A communication entry point where you can plug in your communication stack of choice.</span></span> <span data-ttu-id="6d8a6-134">C’est là que vous pouvez commencer à recevoir des demandes des utilisateurs et des autres services.</span><span class="sxs-lookup"><span data-stu-id="6d8a6-134">This is where you can start receiving requests from users and other services.</span></span>

```java
@Override
protected List<ServiceInstanceListener> createServiceInstanceListeners() {
    ...
}
```

<span data-ttu-id="6d8a6-135">Dans ce didacticiel, nous nous concentrer sur hello `runAsync()` méthode point d’entrée.</span><span class="sxs-lookup"><span data-stu-id="6d8a6-135">In this tutorial, we focus on hello `runAsync()` entry point method.</span></span> <span data-ttu-id="6d8a6-136">C’est là que vous pouvez commencer immédiatement à exécuter votre code.</span><span class="sxs-lookup"><span data-stu-id="6d8a6-136">This is where you can immediately start running your code.</span></span>

### <a name="runasync"></a><span data-ttu-id="6d8a6-137">RunAsync</span><span class="sxs-lookup"><span data-stu-id="6d8a6-137">RunAsync</span></span>
<span data-ttu-id="6d8a6-138">plateforme de Hello appelle cette méthode lorsqu’une instance d’un service est tooexecute endroit et est prêt.</span><span class="sxs-lookup"><span data-stu-id="6d8a6-138">hello platform calls this method when an instance of a service is placed and ready tooexecute.</span></span> <span data-ttu-id="6d8a6-139">Pour un service sans état, cela signifie simplement lors de l’instance de service hello est ouverte.</span><span class="sxs-lookup"><span data-stu-id="6d8a6-139">For a stateless service, that simply means when hello service instance is opened.</span></span> <span data-ttu-id="6d8a6-140">Un jeton d’annulation est fourni toocoordinate lorsque votre instance de service doit toobe fermé.</span><span class="sxs-lookup"><span data-stu-id="6d8a6-140">A cancellation token is provided toocoordinate when your service instance needs toobe closed.</span></span> <span data-ttu-id="6d8a6-141">Dans l’infrastructure de Service, ce cycle d’ouverture/fermeture d’une instance de service peut se produire plusieurs fois sur la durée de vie hello du service de hello dans sa globalité.</span><span class="sxs-lookup"><span data-stu-id="6d8a6-141">In Service Fabric, this open/close cycle of a service instance can occur many times over hello lifetime of hello service as a whole.</span></span> <span data-ttu-id="6d8a6-142">Il existe diverses raisons à cela, notamment :</span><span class="sxs-lookup"><span data-stu-id="6d8a6-142">This can happen for various reasons, including:</span></span>

* <span data-ttu-id="6d8a6-143">système de Hello déplace vos instances de service pour l’équilibrage des ressources.</span><span class="sxs-lookup"><span data-stu-id="6d8a6-143">hello system moves your service instances for resource balancing.</span></span>
* <span data-ttu-id="6d8a6-144">Des erreurs surviennent dans votre code.</span><span class="sxs-lookup"><span data-stu-id="6d8a6-144">Faults occur in your code.</span></span>
* <span data-ttu-id="6d8a6-145">application Hello ou système est mis à niveau.</span><span class="sxs-lookup"><span data-stu-id="6d8a6-145">hello application or system is upgraded.</span></span>
* <span data-ttu-id="6d8a6-146">matériel sous-jacent de Hello connaît une panne.</span><span class="sxs-lookup"><span data-stu-id="6d8a6-146">hello underlying hardware experiences an outage.</span></span>

<span data-ttu-id="6d8a6-147">Cette orchestration est gérée par le Service Fabric tookeep votre service hautement disponible et correctement à charge équilibrée.</span><span class="sxs-lookup"><span data-stu-id="6d8a6-147">This orchestration is managed by Service Fabric tookeep your service highly available and properly balanced.</span></span>

<span data-ttu-id="6d8a6-148">`runAsync()` ne doit pas se bloquer de façon synchrone.</span><span class="sxs-lookup"><span data-stu-id="6d8a6-148">`runAsync()` should not block synchronously.</span></span> <span data-ttu-id="6d8a6-149">Votre implémentation de runAsync doit retourner un toocontinue de runtime CompletableFuture tooallow hello.</span><span class="sxs-lookup"><span data-stu-id="6d8a6-149">Your implementation of runAsync should return a CompletableFuture tooallow hello runtime toocontinue.</span></span> <span data-ttu-id="6d8a6-150">Si votre charge de travail a besoin d’une tâche de longue durée qui doit être effectuée à l’intérieur de tooimplement hello CompletableFuture.</span><span class="sxs-lookup"><span data-stu-id="6d8a6-150">If your workload needs tooimplement a long running task that should be done inside hello CompletableFuture.</span></span>

#### <a name="cancellation"></a><span data-ttu-id="6d8a6-151">Annulation</span><span class="sxs-lookup"><span data-stu-id="6d8a6-151">Cancellation</span></span>
<span data-ttu-id="6d8a6-152">L’annulation de votre charge de travail est un effort conjoint orchestré par hello fourni le jeton d’annulation.</span><span class="sxs-lookup"><span data-stu-id="6d8a6-152">Cancellation of your workload is a cooperative effort orchestrated by hello provided cancellation token.</span></span> <span data-ttu-id="6d8a6-153">Hello le système attend votre tooend tâche (par la réussite, l’annulation ou erreur) avant de poursuivre.</span><span class="sxs-lookup"><span data-stu-id="6d8a6-153">hello system waits for your task tooend (by successful completion, cancellation, or fault) before it moves on.</span></span> <span data-ttu-id="6d8a6-154">Il est important toohonor hello annulation jeton, terminer un travail et quitter `runAsync()` aussi rapidement que possible lorsque le système de hello demande l’annulation.</span><span class="sxs-lookup"><span data-stu-id="6d8a6-154">It is important toohonor hello cancellation token, finish any work, and exit `runAsync()` as quickly as possible when hello system requests cancellation.</span></span> <span data-ttu-id="6d8a6-155">Hello exemple suivant montre comment un événement d’annulation de toohandle :</span><span class="sxs-lookup"><span data-stu-id="6d8a6-155">hello following example demonstrates how toohandle a cancellation event:</span></span>

```java
    @Override
    protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {

        // TODO: Replace hello following sample code with your own logic
        // or remove this runAsync override if it's not needed in your service.

        CompletableFuture.runAsync(() -> {
          long iterations = 0;
          while(true)
          {
            cancellationToken.throwIfCancellationRequested();
            logger.log(Level.INFO, "Working-{0}", ++iterations);

            try
            {
              Thread.sleep(1000);
            }
            catch (IOException ex) {}
          }
        });
    }
```

### <a name="service-registration"></a><span data-ttu-id="6d8a6-156">Inscription du service</span><span class="sxs-lookup"><span data-stu-id="6d8a6-156">Service registration</span></span>
<span data-ttu-id="6d8a6-157">Types de service doivent être inscrit avec le runtime du Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="6d8a6-157">Service types must be registered with hello Service Fabric runtime.</span></span> <span data-ttu-id="6d8a6-158">type de service Hello est défini dans hello `ServiceManifest.xml` et votre classe de service qui implémente `StatelessService`.</span><span class="sxs-lookup"><span data-stu-id="6d8a6-158">hello service type is defined in hello `ServiceManifest.xml` and your service class that implements `StatelessService`.</span></span> <span data-ttu-id="6d8a6-159">L’enregistrement du service est effectué dans le point d’entrée principal processus hello.</span><span class="sxs-lookup"><span data-stu-id="6d8a6-159">Service registration is performed in hello process main entry point.</span></span> <span data-ttu-id="6d8a6-160">Dans cet exemple, hello le processus de point d’entrée principal est `HelloWorldServiceHost.java`:</span><span class="sxs-lookup"><span data-stu-id="6d8a6-160">In this example, hello process main entry point is `HelloWorldServiceHost.java`:</span></span>

```java
public static void main(String[] args) throws Exception {
    try {
        ServiceRuntime.registerStatelessServiceAsync("HelloWorldType", (context) -> new HelloWorldService(), Duration.ofSeconds(10));
        logger.log(Level.INFO, "Registered stateless service type HelloWorldType.");
        Thread.sleep(Long.MAX_VALUE);
    }
    catch (Exception ex) {
        logger.log(Level.SEVERE, "Exception in registration:", ex);
        throw ex;
    }
}
```

## <a name="run-hello-application"></a><span data-ttu-id="6d8a6-161">Exécutez l’application hello</span><span class="sxs-lookup"><span data-stu-id="6d8a6-161">Run hello application</span></span>

<span data-ttu-id="6d8a6-162">Hello Yeoman la structure inclut un gradle script toobuild hello d’application et un interpréteur de commandes de scripts toodeploy et supprimer l’application.</span><span class="sxs-lookup"><span data-stu-id="6d8a6-162">hello Yeoman scaffolding includes a gradle script toobuild hello application and bash scripts toodeploy and remove the application.</span></span> <span data-ttu-id="6d8a6-163">application de hello toorun, première application hello de build avec gradle :</span><span class="sxs-lookup"><span data-stu-id="6d8a6-163">toorun hello application, first build hello application with gradle:</span></span>

```bash
$ gradle
```

<span data-ttu-id="6d8a6-164">Cela génère un package d’application Service Fabric qui peut être déployé à l’aide de l’interface CLI Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6d8a6-164">This produces a Service Fabric application package that can be deployed using Service Fabric CLI.</span></span>

### <a name="deploy-with-service-fabric-cli"></a><span data-ttu-id="6d8a6-165">Effectuer un déploiement à l’aide de l’interface CLI Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6d8a6-165">Deploy with Service Fabric CLI</span></span>

<span data-ttu-id="6d8a6-166">script de install.sh Hello contient hello nécessaire Service Fabric CLI commandes toodeploy hello package d’application.</span><span class="sxs-lookup"><span data-stu-id="6d8a6-166">hello install.sh script contains hello necessary Service Fabric CLI commands toodeploy hello application package.</span></span> <span data-ttu-id="6d8a6-167">Exécutez l’application de hello install.sh script toodeploy.</span><span class="sxs-lookup"><span data-stu-id="6d8a6-167">Run the install.sh script toodeploy hello application.</span></span>

```bash
$ ./install.sh
```

## <a name="next-steps"></a><span data-ttu-id="6d8a6-168">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6d8a6-168">Next steps</span></span>

* [<span data-ttu-id="6d8a6-169">Prise en main de l’interface de ligne de commande Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6d8a6-169">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
