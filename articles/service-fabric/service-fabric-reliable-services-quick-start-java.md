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
# <a name="get-started-with-reliable-services"></a>Prise en main de Reliable Services
> [!div class="op_single_selector"]
> * [C# sur Windows](service-fabric-reliable-services-quick-start.md)
> * [Java sur Linux](service-fabric-reliable-services-quick-start-java.md)
>
>

Cet article explique les principes fondamentaux de hello de Azure Service Fabric des Services fiables et vous guide dans la création et déploiement d’une simple application de Service fiable écrite en Java. Cette vidéo Microsoft Virtual Academy montre également comment toocreate un service fiable sans état :<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965">  
<img src="./media/service-fabric-reliable-services-quick-start-java/ReliableServicesJavaVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="installation-and-setup"></a>Installation et configuration
Avant de commencer, assurez-vous que vous disposez d’environnement de développement de Service Fabric hello sur votre ordinateur.
Si vous avez besoin de tooset, ça trop[mise en route sur Mac](service-fabric-get-started-mac.md) ou [mise en route sur Linux](service-fabric-get-started-linux.md).

## <a name="basic-concepts"></a>Concepts de base
tooget en main des Services fiables, vous seulement devez toounderstand quelques concepts de base :

* **Type de service** : il s’agit de l’implémentation de votre service. Il est défini par la classe hello vous écrivez qui étend `StatelessService` et tout autre code ou les dépendances utilisés ici, avec un nom et un numéro de version.
* **Instance de service nommée**: toorun votre service, vous créez des instances nommées de votre type de service, beaucoup comme vous créez des instances d’objet d’un type de classe. Les instances de service sont en fait des instanciations d’objet de votre classe de service que vous écrivez.
* **Hôte de service**: hello nommé des instances de service que vous créez toorun nécessaire à l’intérieur d’un ordinateur hôte. hôte de service Hello est simplement un processus dans lequel les instances de votre service peuvent exécuter.
* **Inscription du service** : l’inscription rassemble tous les éléments. Hello service type doit être inscrit avec hello Service Fabric runtime dans un service hôte tooallow Service Fabric toocreate ses instances toorun.  

## <a name="create-a-stateless-service"></a>Création d'un service sans état
Commencez par créer une application Service Fabric. Hello SDK de l’infrastructure de Service pour Linux comprend un Yeoman générateur tooprovide hello génération de modèles automatique pour une application de Service Fabric avec un service sans état. Commencez par exécuter hello suivant Yeoman commande :

```bash
$ yo azuresfjava
```

Suivez hello instructions toocreate un **un Service fiable sans état**. Pour ce didacticiel, l’application hello de nom « HelloWorldApplication » et hello service « HelloWorld ». résultat de Hello contient des répertoires pour hello `HelloWorldApplication` et `HelloWorld`.

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

## <a name="implement-hello-service"></a>Implémenter le service de hello
Ouvrez **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**. Cette classe définit le type de service hello et peut exécuter n’importe quel code. API de service Hello fournit deux points d’entrée pour votre code :

* Une méthode de point d’entrée de durée indéterminée, appelée `runAsync()`, avec laquelle vous pouvez commencer l’exécution de toute charge de travail, y compris les charges de travail de calcul de longue durée.

```java
@Override
protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {
    ...
}
```

* Un point d’entrée de communication où vous pouvez connecter la pile de communication de votre choix. C’est là que vous pouvez commencer à recevoir des demandes des utilisateurs et des autres services.

```java
@Override
protected List<ServiceInstanceListener> createServiceInstanceListeners() {
    ...
}
```

Dans ce didacticiel, nous nous concentrer sur hello `runAsync()` méthode point d’entrée. C’est là que vous pouvez commencer immédiatement à exécuter votre code.

### <a name="runasync"></a>RunAsync
plateforme de Hello appelle cette méthode lorsqu’une instance d’un service est tooexecute endroit et est prêt. Pour un service sans état, cela signifie simplement lors de l’instance de service hello est ouverte. Un jeton d’annulation est fourni toocoordinate lorsque votre instance de service doit toobe fermé. Dans l’infrastructure de Service, ce cycle d’ouverture/fermeture d’une instance de service peut se produire plusieurs fois sur la durée de vie hello du service de hello dans sa globalité. Il existe diverses raisons à cela, notamment :

* système de Hello déplace vos instances de service pour l’équilibrage des ressources.
* Des erreurs surviennent dans votre code.
* application Hello ou système est mis à niveau.
* matériel sous-jacent de Hello connaît une panne.

Cette orchestration est gérée par le Service Fabric tookeep votre service hautement disponible et correctement à charge équilibrée.

`runAsync()` ne doit pas se bloquer de façon synchrone. Votre implémentation de runAsync doit retourner un toocontinue de runtime CompletableFuture tooallow hello. Si votre charge de travail a besoin d’une tâche de longue durée qui doit être effectuée à l’intérieur de tooimplement hello CompletableFuture.

#### <a name="cancellation"></a>Annulation
L’annulation de votre charge de travail est un effort conjoint orchestré par hello fourni le jeton d’annulation. Hello le système attend votre tooend tâche (par la réussite, l’annulation ou erreur) avant de poursuivre. Il est important toohonor hello annulation jeton, terminer un travail et quitter `runAsync()` aussi rapidement que possible lorsque le système de hello demande l’annulation. Hello exemple suivant montre comment un événement d’annulation de toohandle :

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

### <a name="service-registration"></a>Inscription du service
Types de service doivent être inscrit avec le runtime du Service Fabric hello. type de service Hello est défini dans hello `ServiceManifest.xml` et votre classe de service qui implémente `StatelessService`. L’enregistrement du service est effectué dans le point d’entrée principal processus hello. Dans cet exemple, hello le processus de point d’entrée principal est `HelloWorldServiceHost.java`:

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

## <a name="run-hello-application"></a>Exécutez l’application hello

Hello Yeoman la structure inclut un gradle script toobuild hello d’application et un interpréteur de commandes de scripts toodeploy et supprimer l’application. application de hello toorun, première application hello de build avec gradle :

```bash
$ gradle
```

Cela génère un package d’application Service Fabric qui peut être déployé à l’aide de l’interface CLI Azure Service Fabric.

### <a name="deploy-with-service-fabric-cli"></a>Effectuer un déploiement à l’aide de l’interface CLI Service Fabric

script de install.sh Hello contient hello nécessaire Service Fabric CLI commandes toodeploy hello package d’application. Exécutez l’application de hello install.sh script toodeploy.

```bash
$ ./install.sh
```

## <a name="next-steps"></a>Étapes suivantes

* [Prise en main de l’interface de ligne de commande Service Fabric](service-fabric-cli.md)
