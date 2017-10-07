---
title: "aaaService vue d’ensemble des acteurs fiable Fabric | Documents Microsoft"
description: "Modèle de la programmation de l’infrastructure de Service Reliable Actors toohello de présentation."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 7fdad07f-f2d6-4c74-804d-e0d56131f060
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: ab010cbf936c6cf723b3d453ef95a9bf51f76c95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooservice-fabric-reliable-actors"></a>Introduction tooService infrastructure Reliable Actors
Reliable Actors est une infrastructure d’application de Service Fabric selon hello [Virtual Actor](http://research.microsoft.com/en-us/projects/orleans/) modèle. Hello fiable acteurs API fournit un modèle de programmation monothread reposant sur hello l’évolutivité et la fiabilité les garanties fournies par l’infrastructure de Service.

## <a name="what-are-actors"></a>Qu’est-ce qu’un « acteur » ?
Un acteur est une unité de calcul et d’état indépendante et isolée, associée à une exécution monothread. Hello [modèle d’acteur](https://en.wikipedia.org/wiki/Actor_model) est un modèle de calcul pour les systèmes simultanés ou distribuées dans laquelle un grand nombre de ces acteurs peut exécuter simultanément et indépendamment les uns des autres. Les acteurs peuvent communiquer entre eux et créer d’autres acteurs.

### <a name="when-toouse-reliable-actors"></a>Lorsque toouse Reliable Actors
Service Fabric Reliable Actors est une implémentation du modèle de conception d’acteur hello. Comme avec n’importe quel modèle de conception de logiciels, décision hello se toouse un modèle spécifique est effectué en se basant sur ou non un logiciel de conception problème adapté à un modèle de hello.

Bien que le modèle de conception hello acteur peut être un bon tooa adapté de problèmes de systèmes distribués et scénarios, tenez compte des contraintes de hello de modèle de hello et d’implémentation de framework hello que doivent figurer. En règle générale, envisagez hello acteur modèle toomodel votre scénario ou un problème si :

* Votre espace de problème implique un nombre élevé (plusieurs milliers) de petites unités d’état et de logique indépendantes et isolées.
* Vous souhaitez toowork avec des objets à thread unique qui ne nécessitent pas d’interaction significative à partir des composants externes, y compris l’interrogation d’état sur un ensemble d’intervenants.
* Vos instances d’acteurs ne bloquent pas les appelants avec des retards inattendus en exécutant des opérations d’E/S.

## <a name="actors-in-service-fabric"></a>Le rôle des acteurs dans Service Fabric
Dans l’infrastructure de Service, les acteurs sont implémentées dans le framework Reliable Actors de hello : une infrastructure d’application de modèle-basé sur acteur construite sur [Service des Services de Fabric fiables](service-fabric-reliable-services-introduction.md). Chaque service Reliable Actor que vous écrivez correspond en fait à une instance Reliable Service partitionnée avec état.

Chaque acteur est définie comme une instance d’un type d’acteur, toohello identiques façon un objet .NET est une instance d’un type .NET. Par exemple, il peut y avoir un type d’acteur qui implémente les fonctionnalités de hello d’une calculatrice, et il peut y avoir de nombreux acteurs de ce type qui sont réparties sur différents nœuds sur un cluster. Chaque acteur de ce type est identifié de façon unique par un ID d'acteur.

### <a name="actor-lifetime"></a>Durée de vie de l’acteur
Les acteurs de l’infrastructure de service sont virtuelles, ce qui signifie que leur durée de vie est pas de représentation en mémoire de tootheir liée. Par conséquent, ils n’avez pas besoin de toobe explicitement créé ou détruit. Hello Reliable Actors runtime active automatiquement une hello acteur première fois qu’il reçoit une demande pour cet ID d’acteur. Si un intervenant n’est pas utilisé pour une période donnée, hello Reliable Actors runtime garbage-collecte les objets de hello en mémoire. Il gère également les connaissances d’existence de hello acteur devez toobe réactivé ultérieurement. Pour plus de détails, consultez la page [Cycle de vie des acteurs et Garbage Collection](service-fabric-reliable-actors-lifecycle.md).

Cette abstraction de la durée de vie acteur virtuel exécute certaines restrictions à la suite de modèle d’acteur virtuel hello et en fait hello mise en œuvre Reliable Actors dévie parfois à partir de ce modèle.

* Un acteur est activé automatiquement (ce qui provoque un acteur toobe objet construit) hello la première fois, un message est envoyé à tooits acteur ID. Après un certain temps, hello acteur l’objet est le garbage collecté. Bonjour futur, à l’aide de l’ID d’acteur hello, entraîne un acteur nouvelle toobe objet construit. État d’un acteur est supérieure à celle durée de vie de l’objet hello lorsque stockées dans le Gestionnaire d’état hello.
* Le déclenchement d’une méthode d’acteur pour un ID d’acteur donné aura pour effet d’activer cet acteur. Pour cette raison, les types d’acteur ont leur constructeur appelé implicitement par le runtime de hello. Par conséquent, le code client ne peut pas passer au constructeur du type de paramètres toohello acteur, bien que les paramètres peuvent être passés constructeur de toohello acteur par service hello lui-même. résultat de Hello est que les acteurs peuvent être construites dans un état partiellement initialisée par heure hello, d’autres méthodes sont appelées si acteur de hello requiert des paramètres de l’initialisation à partir du client de hello. Il n’existe aucun point d’entrée unique pour l’activation d’un acteur à partir du client de hello hello.
* Bien que Reliable Actors créent implicitement des objets de l’acteur. vous n’avez pas hello capacité tooexplicitly supprimer un acteur et son état.

### <a name="distribution-and-failover"></a>Distribution et basculement
tooprovide évolutivité et la fiabilité, Service Fabric distribue les acteurs dans l’ensemble de cluster de hello et automatiquement les transfère à partir des nœuds ayant échoué toohealthy celles en fonction des besoins. Il s’agit ici d’une abstraction sur une instance [Reliable Service partitionnée avec état](service-fabric-concepts-partitioning.md). Distribution, d’évolutivité, de fiabilité et de basculement automatique sont toutes fournies fait hello acteurs sont en cours d’exécution à l’intérieur d’un Service fiable sans état appelée hello *acteur Service*.

Acteurs sont répartis entre des partitions hello Hello acteur Service, et ces partitions sont réparties entre les nœuds de hello dans un cluster Service Fabric. Chaque partition de service contient un ensemble d’acteurs. L’infrastructure de service gère la distribution et le basculement de partitions de service hello.

Par exemple, un service d’acteur avec neuf partitions déployée toothree nœuds à l’aide de placement de partition acteur hello par défaut est distribuées doit être remplacé :

![Distribution Reliable Actors][2]

Hello acteur Framework gère les paramètres de plage des schéma et clé de partition pour vous. Bien que cela simplifie certains choix, certains aspects méritent d’être pris en compte :

* Services fiables vous permet de toochoose un schéma de partitionnement, plage de clés (lorsque vous utilisez une plage de schéma de partitionnement), et le nombre de partition. Reliable Actors est le schéma de partitionnement de plage toohello restreint (schéma de Int64 uniforme hello) et vous demande d’utiliser complète plage de clés Int64 hello.
* Par défaut, les acteurs sont placés aléatoirement dans les partitions, ce qui entraîne une distribution uniforme.
* Du fait de ce placement aléatoire, il faudra vraisemblablement s’attendre à ce que les opérations d’acteur requièrent systématiquement une communication réseau, y compris la sérialisation et la désérialisation des données d’appel de méthode, ce qui implique un effet de latence et une surcharge.
* Dans les scénarios avancés, il est placement de partition d’acteur toocontrol possible à l’aide de l’acteur Int64 ID mapper les partitions toospecific. Toutefois, cette opération peut entraîner une répartition déséquilibrée des acteurs sur les différentes partitions.

Pour plus d’informations sur la façon dont les services d’acteur sont partitionnées, consultez trop[concepts de partitionnement pour les acteurs](service-fabric-reliable-actors-platform.md#service-fabric-partition-concepts-for-actors).

### <a name="actor-communication"></a>Communication d’acteur
Interactions d’acteur sont définies dans une interface qui est partagée par acteur hello qui implémente l’interface de hello et client hello qui obtient un proxy acteur tooan via hello même interface. Étant donné que cette interface est utilisée tooinvoke acteur méthodes en mode asynchrone, toutes les méthodes sur l’interface de hello doivent être retournant des tâches.

Appels de méthode et leurs réponses ultime demandes réseau entre le cluster de hello, c’est le cas hello arguments hello résultat et des tâches hello qu’elles renvoient doivent être sérialisables par la plateforme de hello. En particulier, ils doivent être [sérialisables en contrat de données](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).

#### <a name="hello-actor-proxy"></a>proxy d’acteur Hello
API du client Reliable Actors Hello assure la communication entre une instance de l’acteur et un client de l’acteur. toocommunicate avec un acteur, un client crée un objet proxy acteur qui implémente l’interface d’acteur hello. client de Hello interagit avec l’acteur de hello en appelant les méthodes sur l’objet de proxy hello. proxy d’acteur de Hello peut être utilisé pour la communication client à acteur et acteur à acteur.

```csharp
// Create a randomly distributed actor ID
ActorId actorId = ActorId.CreateRandom();

// This only creates a proxy object, it does not activate an actor or invoke any methods yet.
IMyActor myActor = ActorProxy.Create<IMyActor>(actorId, new Uri("fabric:/MyApp/MyActorService"));

// This will invoke a method on hello actor. If an actor with hello given ID does not exist, it will be activated by this method call.
await myActor.DoWorkAsync();
```

```java
// Create actor ID with some name
ActorId actorId = new ActorId("Actor1");

// This only creates a proxy object, it does not activate an actor or invoke any methods yet.
MyActor myActor = ActorProxyBase.create(actorId, new URI("fabric:/MyApp/MyActorService"), MyActor.class);

// This will invoke a method on hello actor. If an actor with hello given ID does not exist, it will be activated by this method call.
myActor.DoWorkAsync().get();
```


Notez que deux hello deux informations utilisées objet de proxy toocreate hello acteur sont l’ID d’acteur hello et le nom de l’application hello. ID d’acteur Hello identifie acteur de hello, tandis que le nom de l’application hello identifie hello [application Service Fabric](service-fabric-reliable-actors-platform.md#application-model) où l’acteur de hello est déployé.

Hello `ActorProxy`(c#) / `ActorProxyBase`classe (Java) côté client de hello effectue l’acteur de hello toolocate hello résolution nécessaire par ID et ouvrir un canal de communication avec lui. Il réessaie également acteur de hello toolocate dans le cas de hello des échecs de communication et les basculements. Par conséquent, remise de messages a hello suivant caractéristiques :

* La remise de messages est conseillée.
* Acteurs peuvent recevoir des messages en double de hello même client.

### <a name="concurrency"></a>Accès concurrentiel
Hello Reliable Actors runtime fournit un modèle simple accès de tour pour accéder aux méthodes d’acteur. Cela signifie qu’un seul thread peut être actif à tout moment à l’intérieur du code d’un objet d’acteur. L’accès en alternance simplifie considérablement l’exécution de systèmes simultanés dans la mesure où aucun mécanisme de synchronisation n’est nécessaire pour accéder aux données. Cela signifie également systèmes doivent être conçues avec des remarques particulières sur la nature de l’accès monothread hello de chaque instance de l’acteur.

* Une instance unique d’acteur ne peut pas traiter plusieurs demandes à la fois. Une instance de l’acteur peut provoquer un goulot d’étranglement de débit s’il s’agit de requêtes simultanées toohandle attendu.
* Acteurs se bloquer mutuellement s’il existe une demande circulaire entre les deux intervenants pendant une demande externe est tooone des acteurs de hello simultanément. Hello acteur runtime sera automatiquement une fois sur acteur appelle et lever une toointerrupt d’appelant exception toohello une situation de blocage possible.

![Communication Reliable Actors][3]

#### <a name="turn-based-access"></a>Accès en alternance
Tour de rôle se compose de terminer l’exécution de hello d’une méthode d’acteur dans tooa demande à partir d’autres acteurs ou les clients, ou l’exécution complète de hello d’un [du minuteur/rappel](service-fabric-reliable-actors-timers-reminders.md) rappel. Bien que ces méthodes et les rappels sont asynchrones, hello acteurs runtime ne pas entrelacer les. Un tour doit être totalement terminé avant qu’un nouveau tour soit autorisé. En d’autres termes, un rappel de méthode ou un minuteur/rappel d’acteur en cours d’exécution doit être entièrement terminé avant une nouvelle méthode de tooa d’appel ou de rappel est autorisé. Une méthode ou un rappel est considéré comme toohave terminé si l’exécution de hello a retourné à partir de la méthode hello ou la fin de la tâche de rappel et hello retourné par la méthode hello ou un rappel. Il est important de souligner que cet accès concurrentiel en alternance est respecté même dans les différents rappels, minuteries et méthodes.

Hello acteurs runtime applique à concurrence de tour en obtenant un verrou par acteur au début de hello de tour de rôle et activer la libération de verrou hello à fin hello Hello. Par conséquent, l'accès concurrentiel en alternance est appliqué sur une base par acteur et non entre acteurs. Les méthodes d'acteur et les rappels de minuterie/rappel peuvent s'exécuter simultanément pour le compte de différents acteurs.

Hello l’exemple suivant illustre hello au-dessus de concepts. Prenons l’exemple d’un type d’acteur qui implémente deux méthodes asynchrones (par exemple, *Method1* et *Method2*), une minuterie et un rappel. diagramme Hello ci-dessous montre un exemple d’une chronologie pour l’exécution de hello de ces méthodes et les rappels pour le compte de deux acteurs (*ActorId1* et *ActorId2*) qui appartiennent à toothis le type d’acteur.

![Accès et accès concurrentiel en alternance avec le runtime Reliable Actors][1]

Ce diagramme suit les conventions suivantes :

* Chaque ligne verticale indique flux logique de hello de l’exécution d’une méthode ou d’un rappel pour le compte d’un acteur particulier.
* Hello marqué sur chaque ligne verticale se produisent dans l’ordre chronologique, avec les événements plus récents qui se produisent sous les plus anciens.
* Différentes couleurs sont utilisées pour les chronologies correspondante toodifferent acteurs.
* Mise en surbrillance est la durée de hello tooindicate utilisés pour le hello un verrou par acteur est maintenu pour le compte d’une méthode ou un rappel.

Tooconsider de certains points importants suivants :

* Alors que *Method1* est l’exécution de la part de *ActorId2* dans la demande de réponse tooclient *xyz789*, une autre demande de client (*abc123*) arrive et qu’il requiert également *Method1* toobe exécutée par *ActorId2*. Toutefois, hello deuxième exécution de *Method1* ne commence pas jusqu'à la fin de l’exécution préalable de hello. De même, un rappel inscrit par *ActorId2* se déclenche lors de la *Method1* est en cours d’exécution dans la demande de réponse tooclient *xyz789*. rappel de rappel Hello est exécuté uniquement après les deux exécutions de *Method1* sont terminées. Tout ceci est dû concurrence tooturn appliquée pour *ActorId2*.
* De même, concurrence activer est également appliquée pour *ActorId1*, comme illustré par l’exécution de hello de *Method1*, *méthode2*, et hello du rappel timer de la part de *ActorId1* passe en série.
* L'exécution de *Method1* pour le compte *d'ActorId1* se chevauche avec son exécution pour le compte *d'ActorId2*. En effet, l’accès concurrentiel en alternance est appliqué uniquement au sein d’un acteur et non entre les acteurs.
* Dans certains des exécutions de méthode/rappel hello, hello `Task`(c#) / `CompletableFuture`(Java) retourné par hello méthode/rappel termine après le retour de la méthode hello. Dans d’autres, opération asynchrone de hello terminée en heure hello hello méthode/rappel retourne. Dans les deux cas, un verrou par acteur hello est publié uniquement après les deux produits rappel de la méthode hello retourne et la fin de l’opération asynchrone hello.

#### <a name="reentrancy"></a>Réentrance
Hello acteurs runtime permet de réentrance par défaut. Cela signifie que si une méthode d’acteur de *acteur A* appelle une méthode sur *acteur B*, qui appelle à son tour une autre méthode sur *acteur A*, que méthode est autorisée à toorun. Il s’agit, car il fait partie de hello même contexte de la chaîne d’appel logique. Tous les appels du minuteur et rappel démarrer avec le contexte d’appel logique nouvelle hello. Consultez hello [réentrance de Reliable Actors](service-fabric-reliable-actors-reentrancy.md) pour plus d’informations.

#### <a name="scope-of-concurrency-guarantees"></a>Étendue des garanties d'accès concurrentiel
Hello acteurs runtime fournit ces garanties d’accès concurrentiel dans les situations où il contrôle appel hello de ces méthodes. Par exemple, il fournit ces garanties pour les appels de méthode hello qui sont effectuées dans la demande du client tooa réponse, ainsi que pour les rappels timer et de rappel. Toutefois, si le code d’acteur hello appelle directement ces méthodes en dehors des mécanismes hello fournies par le runtime d’acteurs hello, hello runtime ne peut pas fournir aucune garantie d’accès concurrentiel. Par exemple, si la méthode hello est appelé dans le contexte de hello d’une tâche qui n’est pas associée avec la tâche hello retourné par les méthodes d’acteur hello, hello runtime ne peut pas fournir d’accès concurrentiel garanties. Si la méthode hello est appelé à partir d’un thread acteur hello crée sur son propre, puis hello runtime ne peut pas fournir d’accès concurrentiel garanties. Par conséquent, les opérations d’arrière-plan tooperform, acteurs doivent utiliser [minuteries d’acteur et les rappels d’acteur](service-fabric-reliable-actors-timers-reminders.md) qui respectent la concurrence basée sur Activer.

## <a name="next-steps"></a>Étapes suivantes
* Commencez par créer votre premier service Reliable Actors :
   * [Prise en main de Reliable Actors sur .NET](service-fabric-reliable-actors-get-started.md)
   * [Prise en main de Reliable Actors sur Java](service-fabric-reliable-actors-get-started-java.md)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-introduction/concurrency.png
[2]: ./media/service-fabric-reliable-actors-introduction/distribution.png
[3]: ./media/service-fabric-reliable-actors-introduction/actor-communication.png
