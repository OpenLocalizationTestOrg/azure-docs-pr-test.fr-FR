---
title: "aaaCreate votre premier microservice Azure basé sur acteur en C# | Documents Microsoft"
description: "Ce didacticiel vous guide tout au long des étapes hello de création, de débogage et de déploiement d’un service basé sur acteur simple à l’aide de l’infrastructure de Service Reliable Actors."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d4aebe72-1551-4062-b1eb-54d83297f139
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: ab4f75bef0adb6e70f0ead587475b3fb51e6e6a5
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

Cet article explique les principes fondamentaux de hello de Azure Service Fabric Reliable Actors et vous présente la création, de débogage et de déploiement d’une application fiable acteur simple dans Visual Studio.

## <a name="installation-and-setup"></a>Installation et configuration
Avant de commencer, assurez-vous d’avoir l’environnement de développement de Service Fabric hello sur votre ordinateur.
Si vous avez besoin de tooset, configurez-le, consultez les instructions détaillées sur [comment tooset d’environnement de développement hello](service-fabric-get-started.md).

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

## <a name="create-a-new-project-in-visual-studio"></a>Création d'un projet dans Visual Studio
Lancez Visual Studio 2015 ou Visual Studio 2017 en tant qu’administrateur et créez un projet d’application Service Fabric :

![Outils Service Fabric pour Visual Studio - nouveau projet][1]

Dans la boîte de dialogue hello suivante, vous pouvez choisir de type hello de projet que vous souhaitez toocreate.

![Modèles de projets Service Fabric][5]

Pour le projet HelloWorld de hello, nous allons utiliser le service de l’infrastructure de Service Reliable Actors hello.

Une fois que vous avez créé des solutions de hello, vous devez voir hello suivant structure :

![Structure d’un projet Service Fabric][2]

## <a name="reliable-actors-basic-building-blocks"></a>Blocs de construction de base des acteurs fiables
Une solution Reliable Actors standard est composée de trois projets :

* **projet d’application Hello (MyActorApplication)**. Il s’agit de projet hello que tous les services hello ensemble pour le déploiement de packages. Il contient hello *ApplicationManifest.xml* et les scripts PowerShell pour gérer l’application hello.
* **projet d’interface Hello (MyActor.Interfaces)**. Il s’agit de projet hello qui contient la définition d’interface hello pour l’acteur de hello. Dans le projet de MyActor.Interfaces hello, vous pouvez définir les interfaces hello qui seront utilisés par les acteurs hello dans les solutions hello. Vos interfaces acteur peuvent être définies dans n’importe quel projet avec n’importe quel nom, mais l’interface de hello définit contrat acteur hello qui est partagé par implémentation d’acteur hello et clients hello appelant acteur de hello, il est donc généralement toodefine de sens dans un assembly séparer de hello acteur implémentation et peut être partagé par plusieurs autres projets.

```csharp
public interface IMyActor : IActor
{
    Task<string> HelloWorld();
}
```

* **projet de service d’acteur Hello (MyActor)**. Il s’agit de hello projet utilisé toodefine hello Service Fabric service est continu toohost hello acteur. Il contient la mise en œuvre hello d’acteur de hello. Une implémentation d’un acteur est une classe qui dérive du type de base hello `Actor` et implémente hello des interfaces qui sont définis dans le projet de MyActor.Interfaces hello. Une classe d’acteur doit également implémenter un constructeur qui accepte un `ActorService` instance et un `ActorId` et les transmet toohello base `Actor` classe. Cela permet l’injection d’une dépendance de constructeur pour des dépendances de plateforme.

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<string> HelloWorld()
    {
        return Task.FromResult("Hello world!");
    }
}
```

service d’acteur Hello doit être enregistré avec un type de service dans le runtime du Service Fabric hello. Dans commande pour hello acteur Service toorun vos instances de l’acteur, votre type d’acteur doit également être enregistré avec hello Service d’acteur. Hello `ActorRuntime` méthode d’inscription exécute cette tâche pour acteurs.

```csharp
internal static class Program
{
    private static void Main()
    {
        try
        {
            ActorRuntime.RegisterActorAsync<MyActor>(
                (context, actorType) => new ActorService(context, actorType, () => new MyActor())).GetAwaiter().GetResult();

            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ActorEventSource.Current.ActorHostInitializationFailed(e.ToString());
            throw;
        }
    }
}

```

Si vous démarrez un nouveau projet dans Visual Studio et vous n'avez qu’une seule définition d’acteur, l’inscription de hello est incluse par défaut dans le code hello généré par Visual Studio. Si vous définissez les autres intervenants dans le service hello, vous devez l’inscription de tooadd hello intervenant à l’aide de :

```csharp
 ActorRuntime.RegisterActorAsync<MyOtherActor>();

```

> [!TIP]
> Hello acteurs de l’infrastructure de Service runtime émet certaines [événements et compteurs de performance liés tooactor méthodes](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters). Ces événements sont utiles dans les diagnostics et la surveillance des performances.
> 
> 

## <a name="debugging"></a>Débogage
outils de Service Fabric Hello pour Visual Studio prend en charge le débogage sur votre ordinateur local. Vous pouvez démarrer une session de débogage en hello atteinte touche F5. Visual Studio génère (si nécessaire) des packages. Il déploie l’application hello Cluster Service Fabric local de hello et attache le débogueur de hello.

Au cours du processus de déploiement hello, vous pouvez voir la progression hello Bonjour **sortie** fenêtre.

![Fenêtre de sortie de débogage Service Fabric][3]

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur [comment Reliable Actors utiliser hello Service Fabric](service-fabric-reliable-actors-platform.md).

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject.PNG
[2]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-projectstructure.PNG
[3]: ./media/service-fabric-reliable-actors-get-started/debugging-output.PNG
[4]: ./media/service-fabric-reliable-actors-get-started/vs-context-menu.png
[5]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject1.PNG
