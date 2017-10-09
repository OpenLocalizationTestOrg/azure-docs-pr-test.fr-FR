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
# <a name="getting-started-with-reliable-actors"></a>Prise en main de Reliable Actors
> [!div class="op_single_selector"]
> * [C# sur Windows](service-fabric-reliable-actors-get-started.md)
> * [Java sur Linux](service-fabric-reliable-actors-get-started-java.md)
> 
> 

Cet article explique les principes fondamentaux de hello de Azure Service Fabric Reliable Actors et vous guide dans la création et déploiement d’une application fiable acteur simple en Java.

## <a name="installation-and-setup"></a>Installation et configuration
Avant de commencer, assurez-vous que vous disposez d’environnement de développement de Service Fabric hello sur votre ordinateur.
Si vous avez besoin de tooset, ça trop[mise en route sur Mac](service-fabric-get-started-mac.md) ou [mise en route sur Linux](service-fabric-get-started-linux.md).

## <a name="basic-concepts"></a>Concepts de base
tooget main Reliable Actors, vous seulement devez toounderstand quelques concepts de base :

* **Service d’acteur**. Reliable Actors sont empaquetées dans des Services fiables qui peut être déployé dans une infrastructure de Service Fabric hello. Les instances d’acteur sont activées dans une instance de service nommée.
* **Enregistrement d’acteur**. Comme avec les Services fiables, un service Reliable Actor doit toobe inscrit avec le runtime du Service Fabric hello. En outre, le type d’acteur hello doit toobe inscrit avec le runtime d’acteur hello.
* **Interface d’acteur**. interface d’acteur Hello est toodefine utilisé une interface publique fortement typée d’un acteur. Bonjour terminologie relative aux modèles de Reliable Actor, interface d’acteur hello définit hello types de messages hello acteur peuvent comprendre et traiter. interface d’acteur Hello est utilisé par d’autres acteurs et les applications clientes trop « envoient » (de façon asynchrone) acteur toohello de messages. Reliable Actors peut implémenter plusieurs interfaces.
* **Classe ActorProxy**. Hello ActorProxy classe est utilisée par le client applications tooinvoke hello méthodes exposées via l’interface d’acteur hello. Hello ActorProxy classe fournit deux fonctionnalités importantes :
  
  * La résolution de noms : il s’agit d’acteur de hello toolocate en mesure de cluster de hello (rechercher le nœud hello du cluster hello où il est hébergé).
  * Gestion de défaillance : il peut réessayer d’appels de méthode et de résoudre cet emplacement hello intervenant après avoir, par exemple, un échec qui nécessite hello acteur toobe déplacé tooanother nœud de cluster de hello.

Hello, suivant les règles qui se rapportent les interfaces tooactor est intéressant de mentionner :

* Les méthodes d'interface d'acteur ne peuvent pas être surchargées.
* Les méthodes d’interface d'acteur ne doivent pas avoir de paramètres de sortie, de paramètres de référence ou de paramètres facultatifs.
* Les interfaces génériques ne sont pas prises en charge.

## <a name="create-an-actor-service"></a>Création d’un service d’acteur
Commencez par créer une application Service Fabric. Hello SDK de l’infrastructure de Service pour Linux comprend un Yeoman générateur tooprovide hello génération de modèles automatique pour une application de Service Fabric avec un service sans état. Commencez par exécuter hello suivant Yeoman commande :

```bash
$ yo azuresfjava
```

Suivez hello instructions toocreate un **fiable acteur Service**. Pour ce didacticiel, nommez hello application « HelloWorldActorApplication » et hello acteur « HelloWorldActor ». Hello suivant la génération de modèles automatique sera créé :

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

## <a name="reliable-actors-basic-building-blocks"></a>Blocs de construction de base des acteurs fiables
concepts de base Hello décrits précédemment se traduisent par hello blocs de construction d’un service Reliable Actor.

### <a name="actor-interface"></a>Interface d’acteur
Il contient la définition d’interface hello pour l’acteur de hello. Cette interface définit le contrat d’acteur hello qui est partagé par implémentation d’acteur hello et clients hello appelant acteur de hello, il est donc généralement toodefine de sens dans un emplacement séparer d’implémentation d’acteur hello et peut être partagé par plusieurs autres les services ou les applications clientes.

`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:

```java
public interface HelloWorldActor extends Actor {
    @Readonly   
    CompletableFuture<Integer> getCountAsync();

    CompletableFuture<?> setCountAsync(int count);
}
```

### <a name="actor-service"></a>Service d’acteur
Il contient votre implémentation d’acteur et le code d’inscription de l’acteur. classe d’acteur Hello implémente l’interface d’acteur hello. Il s’agit de l’endroit dans quelquel votre acteur effectue son travail.

`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:

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

### <a name="actor-registration"></a>Enregistrement d’acteur
service d’acteur Hello doit être enregistré avec un type de service dans le runtime du Service Fabric hello. Dans commande pour hello acteur Service toorun vos instances de l’acteur, votre type d’acteur doit également être enregistré avec hello Service d’acteur. Hello `ActorRuntime` méthode d’inscription exécute cette tâche pour acteurs.

`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:

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

### <a name="test-client"></a>Test client
Il s’agit d’une application cliente de test simple vous pouvez exécuter séparément hello Service Fabric application tootest votre service d’acteur. Il s’agit d’un exemple d’où hello ActorProxy peut être utilisé tooactivate et communiquer avec les instances de l’acteur. Il n’est pas déployé avec votre service.

### <a name="hello-application"></a>application Hello
Enfin, les packages d’application hello hello service d’acteur et d’autres services, que vous pouvez ajouter dans hello future ensemble pour le déploiement. Il contient hello *ApplicationManifest.xml* et espaces réservés pour le package de service d’acteur hello.

## <a name="run-hello-application"></a>Exécutez l’application hello

Hello Yeoman la structure inclut un gradle script toobuild hello d’application et un interpréteur de commandes de scripts toodeploy et supprimer l’application. application de hello toodeploy, première application hello de build avec gradle :

```bash
$ gradle
```

Cela génère un package d’application Service Fabric qui peut être déployé à l’aide des outils de l’interface de ligne de commande (CLI) Service Fabric.

### <a name="deploy-service-fabric-cli"></a>Déployer l’interface CLI Service Fabric

script de install.sh Hello contient hello nécessaire Service Fabric CLI (sfctl) commandes toodeploy hello package d’application.
Exécutez hello install.sh script toodeploy hello application.

```bash
$ ./install.sh
```

## <a name="next-steps"></a>Étapes suivantes

* [Prise en main de l’interface de ligne de commande Service Fabric](service-fabric-cli.md)
