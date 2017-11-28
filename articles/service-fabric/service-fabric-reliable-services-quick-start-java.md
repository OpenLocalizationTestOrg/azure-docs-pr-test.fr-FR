---
title: "Créer votre premier microservice Azure fiable en Java | Microsoft Docs"
description: "Introduction à la création d'une application Microsoft Azure Service Fabric avec des services avec et sans état."
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
ms.openlocfilehash: 1ebabe4844732412e04bab8c277f7ebbc4a5737c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-reliable-services"></a><span data-ttu-id="2401f-103">Prise en main de Reliable Services</span><span class="sxs-lookup"><span data-stu-id="2401f-103">Get started with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2401f-104">C# sur Windows</span><span class="sxs-lookup"><span data-stu-id="2401f-104">C# on Windows</span></span>](service-fabric-reliable-services-quick-start.md)
> * [<span data-ttu-id="2401f-105">Java sur Linux</span><span class="sxs-lookup"><span data-stu-id="2401f-105">Java on Linux</span></span>](service-fabric-reliable-services-quick-start-java.md)
>
>

<span data-ttu-id="2401f-106">Cet article explique les notions de base d’Azure Service Fabric Reliable Services et vous guide pas à pas dans la création et le déploiement d’une application Reliable Service simple écrite en Java.</span><span class="sxs-lookup"><span data-stu-id="2401f-106">This article explains the basics of Azure Service Fabric Reliable Services and walks you through creating and deploying a simple Reliable Service application written in Java.</span></span> <span data-ttu-id="2401f-107">Cette vidéo Microsoft Virtual Academy vous montre également comment créer un service Reliable sans état :<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965"></span><span class="sxs-lookup"><span data-stu-id="2401f-107">This Microsoft Virtual Academy video also shows you how to create a stateless Reliable service: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965"></span></span>  
<img src="./media/service-fabric-reliable-services-quick-start-java/ReliableServicesJavaVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="installation-and-setup"></a><span data-ttu-id="2401f-108">Installation et configuration</span><span class="sxs-lookup"><span data-stu-id="2401f-108">Installation and setup</span></span>
<span data-ttu-id="2401f-109">Avant de commencer, assurez-vous que l’environnement de développement Service Fabric est configuré sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="2401f-109">Before you start, make sure you have the Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="2401f-110">Si vous devez le configurer, référez-vous à l’article sur la [prise en main sur Mac](service-fabric-get-started-mac.md) ou sur la [prise en main sur Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="2401f-110">If you need to set it up, go to [getting started on Mac](service-fabric-get-started-mac.md) or [getting started on Linux](service-fabric-get-started-linux.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="2401f-111">Concepts de base</span><span class="sxs-lookup"><span data-stu-id="2401f-111">Basic concepts</span></span>
<span data-ttu-id="2401f-112">Pour prendre en main Reliable Services, il vous suffit de comprendre quelques concepts de base :</span><span class="sxs-lookup"><span data-stu-id="2401f-112">To get started with Reliable Services, you only need to understand a few basic concepts:</span></span>

* <span data-ttu-id="2401f-113">**Type de service** : il s’agit de l’implémentation de votre service.</span><span class="sxs-lookup"><span data-stu-id="2401f-113">**Service type**: This is your service implementation.</span></span> <span data-ttu-id="2401f-114">Elle est définie par la classe que vous écrivez qui étend `StatelessService` et tout autre code ou dépendances utilisés ici, ainsi qu’un nom et un numéro de version.</span><span class="sxs-lookup"><span data-stu-id="2401f-114">It is defined by the class you write that extends `StatelessService` and any other code or dependencies used therein, along with a name and a version number.</span></span>
* <span data-ttu-id="2401f-115">**Instance de service nommée** : pour exécuter votre service, vous créez des instances nommées de votre type de service, de la même manière que vous créez des instances d’objet d’un type de classe.</span><span class="sxs-lookup"><span data-stu-id="2401f-115">**Named service instance**: To run your service, you create named instances of your service type, much like you create object instances of a class type.</span></span> <span data-ttu-id="2401f-116">Les instances de service sont en fait des instanciations d’objet de votre classe de service que vous écrivez.</span><span class="sxs-lookup"><span data-stu-id="2401f-116">Service instances are in fact object instantiations of your service class that you write.</span></span>
* <span data-ttu-id="2401f-117">**Hôte de service** : les instances de service nommées que vous créez doivent s’exécuter au sein d’un ordinateur hôte.</span><span class="sxs-lookup"><span data-stu-id="2401f-117">**Service host**: The named service instances you create need to run inside a host.</span></span> <span data-ttu-id="2401f-118">L’hôte de service est simplement un processus dans lequel les instances de votre service peuvent s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="2401f-118">The service host is just a process where instances of your service can run.</span></span>
* <span data-ttu-id="2401f-119">**Inscription du service** : l’inscription rassemble tous les éléments.</span><span class="sxs-lookup"><span data-stu-id="2401f-119">**Service registration**: Registration brings everything together.</span></span> <span data-ttu-id="2401f-120">Le type de service doit être inscrit auprès du runtime Service Fabric dans un hôte de service pour autoriser Service Fabric à créer des instances de ce type à exécuter.</span><span class="sxs-lookup"><span data-stu-id="2401f-120">The service type must be registered with the Service Fabric runtime in a service host to allow Service Fabric to create instances of it to run.</span></span>  

## <a name="create-a-stateless-service"></a><span data-ttu-id="2401f-121">Création d'un service sans état</span><span class="sxs-lookup"><span data-stu-id="2401f-121">Create a stateless service</span></span>
<span data-ttu-id="2401f-122">Commencez par créer une application Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2401f-122">Start by creating a Service Fabric application.</span></span> <span data-ttu-id="2401f-123">Le Kit de développement logiciel (SDK) Service Fabric pour Linux comprend un générateur Yeoman qui assure la génération de modèles automatique pour une application Service Fabric avec un service sans état.</span><span class="sxs-lookup"><span data-stu-id="2401f-123">The Service Fabric SDK for Linux includes a Yeoman generator to provide the scaffolding for a Service Fabric application with a stateless service.</span></span> <span data-ttu-id="2401f-124">Commencez par exécuter la commande Yeoman suivante :</span><span class="sxs-lookup"><span data-stu-id="2401f-124">Start by running the following Yeoman command:</span></span>

```bash
$ yo azuresfjava
```

<span data-ttu-id="2401f-125">Suivez les instructions pour créer un **service sans état fiable**.</span><span class="sxs-lookup"><span data-stu-id="2401f-125">Follow the instructions to create a **Reliable Stateless Service**.</span></span> <span data-ttu-id="2401f-126">Pour ce didacticiel, nommez l’application « HelloWorldApplication » et le service « HelloWorld ».</span><span class="sxs-lookup"><span data-stu-id="2401f-126">For this tutorial, name the application "HelloWorldApplication" and the service "HelloWorld".</span></span> <span data-ttu-id="2401f-127">Le résultat comprend des répertoires pour `HelloWorldApplication` et `HelloWorld`.</span><span class="sxs-lookup"><span data-stu-id="2401f-127">The result includes directories for the `HelloWorldApplication` and `HelloWorld`.</span></span>

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

## <a name="implement-the-service"></a><span data-ttu-id="2401f-128">Mettre en œuvre le service</span><span class="sxs-lookup"><span data-stu-id="2401f-128">Implement the service</span></span>
<span data-ttu-id="2401f-129">Ouvrez **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**.</span><span class="sxs-lookup"><span data-stu-id="2401f-129">Open **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**.</span></span> <span data-ttu-id="2401f-130">Cette classe définit le type de service et peut exécuter n’importe quel code.</span><span class="sxs-lookup"><span data-stu-id="2401f-130">This class defines the service type, and can run any code.</span></span> <span data-ttu-id="2401f-131">L'API de service fournit deux points d'entrée pour votre code :</span><span class="sxs-lookup"><span data-stu-id="2401f-131">The service API provides two entry points for your code:</span></span>

* <span data-ttu-id="2401f-132">Une méthode de point d’entrée de durée indéterminée, appelée `runAsync()`, avec laquelle vous pouvez commencer l’exécution de toute charge de travail, y compris les charges de travail de calcul de longue durée.</span><span class="sxs-lookup"><span data-stu-id="2401f-132">An open-ended entry point method, called `runAsync()`, where you can begin executing any workloads, including long-running compute workloads.</span></span>

```java
@Override
protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {
    ...
}
```

* <span data-ttu-id="2401f-133">Un point d’entrée de communication où vous pouvez connecter la pile de communication de votre choix.</span><span class="sxs-lookup"><span data-stu-id="2401f-133">A communication entry point where you can plug in your communication stack of choice.</span></span> <span data-ttu-id="2401f-134">C’est là que vous pouvez commencer à recevoir des demandes des utilisateurs et des autres services.</span><span class="sxs-lookup"><span data-stu-id="2401f-134">This is where you can start receiving requests from users and other services.</span></span>

```java
@Override
protected List<ServiceInstanceListener> createServiceInstanceListeners() {
    ...
}
```

<span data-ttu-id="2401f-135">Dans ce didacticiel, nous nous concentrons sur la méthode de point d’entrée `runAsync()`.</span><span class="sxs-lookup"><span data-stu-id="2401f-135">In this tutorial, we focus on the `runAsync()` entry point method.</span></span> <span data-ttu-id="2401f-136">C’est là que vous pouvez commencer immédiatement à exécuter votre code.</span><span class="sxs-lookup"><span data-stu-id="2401f-136">This is where you can immediately start running your code.</span></span>

### <a name="runasync"></a><span data-ttu-id="2401f-137">RunAsync</span><span class="sxs-lookup"><span data-stu-id="2401f-137">RunAsync</span></span>
<span data-ttu-id="2401f-138">La plateforme appelle cette méthode quand une instance d’un service est placée et prête à être exécutée.</span><span class="sxs-lookup"><span data-stu-id="2401f-138">The platform calls this method when an instance of a service is placed and ready to execute.</span></span> <span data-ttu-id="2401f-139">Pour un service sans état, cela signifie simplement le moment où l’instance de service est ouverte.</span><span class="sxs-lookup"><span data-stu-id="2401f-139">For a stateless service, that simply means when the service instance is opened.</span></span> <span data-ttu-id="2401f-140">Un jeton d'annulation est fourni pour coordonner lorsque l'instance de service doit être fermée.</span><span class="sxs-lookup"><span data-stu-id="2401f-140">A cancellation token is provided to coordinate when your service instance needs to be closed.</span></span> <span data-ttu-id="2401f-141">Dans Service Fabric, ce cycle d’ouverture/fermeture d’une instance de service peut se produire plusieurs fois au cours de la durée de vie de votre service dans son ensemble.</span><span class="sxs-lookup"><span data-stu-id="2401f-141">In Service Fabric, this open/close cycle of a service instance can occur many times over the lifetime of the service as a whole.</span></span> <span data-ttu-id="2401f-142">Il existe diverses raisons à cela, notamment :</span><span class="sxs-lookup"><span data-stu-id="2401f-142">This can happen for various reasons, including:</span></span>

* <span data-ttu-id="2401f-143">Le système déplace vos instances de service à des fins d’équilibrage des ressources.</span><span class="sxs-lookup"><span data-stu-id="2401f-143">The system moves your service instances for resource balancing.</span></span>
* <span data-ttu-id="2401f-144">Des erreurs surviennent dans votre code.</span><span class="sxs-lookup"><span data-stu-id="2401f-144">Faults occur in your code.</span></span>
* <span data-ttu-id="2401f-145">L’application ou le système sont mis à niveau.</span><span class="sxs-lookup"><span data-stu-id="2401f-145">The application or system is upgraded.</span></span>
* <span data-ttu-id="2401f-146">Le matériel sous-jacent tombe en panne.</span><span class="sxs-lookup"><span data-stu-id="2401f-146">The underlying hardware experiences an outage.</span></span>

<span data-ttu-id="2401f-147">Cette orchestration est gérée par Service Fabric afin de maintenir une haute disponibilité et un équilibrage correct pour votre service.</span><span class="sxs-lookup"><span data-stu-id="2401f-147">This orchestration is managed by Service Fabric to keep your service highly available and properly balanced.</span></span>

<span data-ttu-id="2401f-148">`runAsync()` ne doit pas se bloquer de façon synchrone.</span><span class="sxs-lookup"><span data-stu-id="2401f-148">`runAsync()` should not block synchronously.</span></span> <span data-ttu-id="2401f-149">Votre implémentation de runAsync doit renvoyer un objet CompletableFuture pour permettre au runtime de continuer</span><span class="sxs-lookup"><span data-stu-id="2401f-149">Your implementation of runAsync should return a CompletableFuture to allow the runtime to continue.</span></span> <span data-ttu-id="2401f-150">si votre charge de travail a besoin d’implémenter une tâche longue qui doit être effectuée à l’intérieur de l’objet CompletableFuture.</span><span class="sxs-lookup"><span data-stu-id="2401f-150">If your workload needs to implement a long running task that should be done inside the CompletableFuture.</span></span>

#### <a name="cancellation"></a><span data-ttu-id="2401f-151">Annulation</span><span class="sxs-lookup"><span data-stu-id="2401f-151">Cancellation</span></span>
<span data-ttu-id="2401f-152">L'annulation de votre charge de travail est un effort conjoint orchestré par le jeton d'annulation fourni.</span><span class="sxs-lookup"><span data-stu-id="2401f-152">Cancellation of your workload is a cooperative effort orchestrated by the provided cancellation token.</span></span> <span data-ttu-id="2401f-153">Le système attend la fin de la tâche (suite à sa réussite, à son annulation ou à une défaillance) avant de poursuivre.</span><span class="sxs-lookup"><span data-stu-id="2401f-153">The system waits for your task to end (by successful completion, cancellation, or fault) before it moves on.</span></span> <span data-ttu-id="2401f-154">Il est important de respecter le jeton d’annulation, de terminer le travail et de quitter `runAsync()` aussi rapidement que possible quand le système demande une annulation.</span><span class="sxs-lookup"><span data-stu-id="2401f-154">It is important to honor the cancellation token, finish any work, and exit `runAsync()` as quickly as possible when the system requests cancellation.</span></span> <span data-ttu-id="2401f-155">L’exemple suivant montre comment gérer un événement d’annulation :</span><span class="sxs-lookup"><span data-stu-id="2401f-155">The following example demonstrates how to handle a cancellation event:</span></span>

```java
    @Override
    protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {

        // TODO: Replace the following sample code with your own logic
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

### <a name="service-registration"></a><span data-ttu-id="2401f-156">Inscription du service</span><span class="sxs-lookup"><span data-stu-id="2401f-156">Service registration</span></span>
<span data-ttu-id="2401f-157">Les types de service doivent être inscrits auprès du runtime Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2401f-157">Service types must be registered with the Service Fabric runtime.</span></span> <span data-ttu-id="2401f-158">Le type de service est défini dans le fichier `ServiceManifest.xml` et votre classe de service qui implémente `StatelessService`.</span><span class="sxs-lookup"><span data-stu-id="2401f-158">The service type is defined in the `ServiceManifest.xml` and your service class that implements `StatelessService`.</span></span> <span data-ttu-id="2401f-159">L’inscription du service est réalisée dans le point d’entrée principal du processus.</span><span class="sxs-lookup"><span data-stu-id="2401f-159">Service registration is performed in the process main entry point.</span></span> <span data-ttu-id="2401f-160">Dans cet exemple, le point d’entrée principal du processus est `HelloWorldServiceHost.java` :</span><span class="sxs-lookup"><span data-stu-id="2401f-160">In this example, the process main entry point is `HelloWorldServiceHost.java`:</span></span>

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

## <a name="run-the-application"></a><span data-ttu-id="2401f-161">Exécution de l'application</span><span class="sxs-lookup"><span data-stu-id="2401f-161">Run the application</span></span>

<span data-ttu-id="2401f-162">La génération de modèles automatique Yeoman inclut un script Gradle permettant de créer l’application et des scripts bash permettant le déploiement et la suppression de l’application.</span><span class="sxs-lookup"><span data-stu-id="2401f-162">The Yeoman scaffolding includes a gradle script to build the application and bash scripts to deploy and remove the application.</span></span> <span data-ttu-id="2401f-163">Pour exécuter l’application, commencez par créer l’application avec Gradle :</span><span class="sxs-lookup"><span data-stu-id="2401f-163">To run the application, first build the application with gradle:</span></span>

```bash
$ gradle
```

<span data-ttu-id="2401f-164">Cela génère un package d’application Service Fabric qui peut être déployé à l’aide de l’interface CLI Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2401f-164">This produces a Service Fabric application package that can be deployed using Service Fabric CLI.</span></span>

### <a name="deploy-with-service-fabric-cli"></a><span data-ttu-id="2401f-165">Effectuer un déploiement à l’aide de l’interface CLI Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2401f-165">Deploy with Service Fabric CLI</span></span>

<span data-ttu-id="2401f-166">Le script install.sh contient les commandes de l’interface CLI Service Fabric nécessaires pour déployer le package d’application.</span><span class="sxs-lookup"><span data-stu-id="2401f-166">The install.sh script contains the necessary Service Fabric CLI commands to deploy the application package.</span></span> <span data-ttu-id="2401f-167">Exécutez le script install.sh pour déployer l’application.</span><span class="sxs-lookup"><span data-stu-id="2401f-167">Run the install.sh script to deploy the application.</span></span>

```bash
$ ./install.sh
```

## <a name="next-steps"></a><span data-ttu-id="2401f-168">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2401f-168">Next steps</span></span>

* [<span data-ttu-id="2401f-169">Bien démarrer avec l’interface de ligne de commande Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2401f-169">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
