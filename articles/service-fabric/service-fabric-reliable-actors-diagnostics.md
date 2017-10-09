---
title: aaaActors diagnostics et surveillance | Documents Microsoft
description: "Cet article décrit les diagnostics hello et fonctionnalités dans le runtime de Service Fabric Reliable Actors hello, y compris les événements de hello et émis par celui-ci les compteurs de performances d’analyse des performances."
services: service-fabric
documentationcenter: .net
author: abhishekram
manager: timlt
editor: vturecek
ms.assetid: 1c229923-670a-4634-ad59-468ff781ad18
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: abhisram
ms.openlocfilehash: 5b266d67875722feef5c5be8861bda6d8132a7d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-and-performance-monitoring-for-reliable-actors"></a>Diagnostics et surveillance des performances pour Reliable Actors
exécution de Reliable Actors Hello émet [EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) événements et [les compteurs de performance](https://msdn.microsoft.com/library/system.diagnostics.performancecounter.aspx). Ces fournissent des informations sur le fonctionne du runtime de hello et aider à l’analyse des performances et le dépannage.

## <a name="eventsource-events"></a>Événements EventSource
nom du fournisseur EventSource Hello pour hello Reliable Actors runtime est « Microsoft-ServiceFabric-acteurs ». Événements à partir de cette source d’événements s’affichent dans hello [événements de diagnostic](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md#view-service-fabric-system-events-in-visual-studio) fenêtre lors de l’application d’acteur hello [de débogage dans Visual Studio](service-fabric-debugging-your-application.md).

Sont des exemples d’outils et technologies qui permettent de collecter ou afficher des événements EventSource [PerfView](http://www.microsoft.com/download/details.aspx?id=28567), [Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md), [journalisation sémantique](https://msdn.microsoft.com/library/dn774980.aspx)et hello [ La bibliothèque Microsoft TraceEvent](http://www.nuget.org/packages/Microsoft.Diagnostics.Tracing.TraceEvent).

### <a name="keywords"></a>Mots clés
Tous les événements qui appartiennent toohello fiable acteurs EventSource sont associés à un ou plusieurs mots clés. Cela permet de filtrer les événements collectés. Hello suivant les bits du mot clé est définie.

| Bit | Description |
| --- | --- |
| 0x1 |Ensemble d’événements importants qui résument les opération hello du runtime de l’ensemble fibre optique acteurs hello. |
| 0x2 |Jeu d'événements décrivant les appels de méthode d'acteur. Pour plus d’informations, consultez hello [rubrique d’introduction sur les acteurs](service-fabric-reliable-actors-introduction.md). |
| 0x4 |Jeu d’événements connexes tooactor état. Pour plus d’informations, consultez la rubrique de hello sur [gestion d’état acteur](service-fabric-reliable-actors-state-management.md). |
| 0x8 |Jeu d’événements connexes tooturn concurrence d’acteur de hello. Pour plus d’informations, consultez la rubrique de hello sur [concurrence](service-fabric-reliable-actors-introduction.md#concurrency). |

## <a name="performance-counters"></a>Compteurs de performances
Hello Reliable Actors runtime définit hello suivant des catégories de compteurs de performances.

| Catégorie | Description |
| --- | --- |
| Service Fabric Actor |Compteurs spécifiques tooAzure acteurs de l’infrastructure de Service, par exemple, temps toosave un état d’acteur |
| Service Fabric Actor Method |Compteurs spécifiques toomethods implémentée par des acteurs de l’infrastructure de Service, par exemple la fréquence à laquelle une méthode d’acteur est appelée |

Chaque hello au-dessus des catégories a un ou plusieurs compteurs.

Hello [Analyseur de performances Windows](https://technet.microsoft.com/library/cc749249.aspx) application qui est disponible par défaut dans le système d’exploitation de Windows hello peut être utilisé toocollect et affichage de données compteur de performance. [Diagnostics Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) est une autre option pour la collecte de données de compteur de performances et de les télécharger tooAzure tables.

### <a name="performance-counter-instance-names"></a>Noms d'instance de compteur de performances
Un cluster avec un grand nombre de services d'acteur ou de partitions de service d'acteur disposera d'un grand nombre d'instances de compteur de performances d'acteur. Hello noms d’instance de compteur de performances peuvent vous aider à identifier hello spécifiques [partition](service-fabric-reliable-actors-platform.md#service-fabric-partition-concepts-for-actors) et méthode d’acteur (le cas échéant) cette instance de compteur de performances hello est associée.

#### <a name="service-fabric-actor-category"></a>Catégorie Service Fabric Actor
Pour la catégorie de hello `Service Fabric Actor`, noms d’instance de compteur de hello sont Bonjour suivant le format :

`ServiceFabricPartitionID_ActorsRuntimeInternalID`

*ServiceFabricPartitionID* est représentation de chaîne hello Hello ID de partition de Service Fabric qui hello l’instance de compteur de performance est associé. ID de partition Hello est un GUID, et sa représentation sous forme de chaîne est générée via hello [ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx) méthode avec le spécificateur de format « D ».

*ActorRuntimeInternalID* est la représentation sous forme de chaîne hello d’un entier 64 bits qui est généré par le runtime de l’ensemble fibre optique acteurs hello pour son usage interne. Il est inclus dans l’instance de compteur de performance hello nom tooensure son unicité et éviter les conflits avec les autres noms d’instance des compteurs de performance. Les utilisateurs ne doivent pas essayer toointerpret cette partie du nom instance de compteur de performance hello.

Hello Voici un exemple d’un nom d’instance de compteur pour un compteur qui appartient toohello `Service Fabric Actor` catégorie :

`2740af29-78aa-44bc-a20b-7e60fb783264_635650083799324046`

Dans l’exemple hello ci-dessus, `2740af29-78aa-44bc-a20b-7e60fb783264` est la représentation sous forme de chaîne hello d’ID de partition de Service Fabric hello, et `635650083799324046` est hello 64 bits ID généré pour interne du runtime de hello utiliser.

#### <a name="service-fabric-actor-method-category"></a>Catégorie Service Fabric Actor Method
Pour la catégorie de hello `Service Fabric Actor Method`, noms d’instance de compteur de hello sont Bonjour suivant le format :

`MethodName_ActorsRuntimeMethodId_ServiceFabricPartitionID_ActorsRuntimeInternalID`

*MethodName* est le nom hello de méthode intervenant hello hello l’instance de compteur de performance est associé. format Hello hello du nom de méthode est déterminée selon une logique dans hello acteurs de l’ensemble fibre optique runtime qui équilibre la lisibilité hello du nom hello avec des contraintes sur la longueur maximale de hello de noms des instances de compteur performance hello sur Windows.

*ActorsRuntimeMethodId* est la représentation sous forme de chaîne hello d’un entier 32 bits qui est généré par le runtime de l’ensemble fibre optique acteurs hello pour son usage interne. Il est inclus dans l’instance de compteur de performance hello nom tooensure son unicité et éviter les conflits avec les autres noms d’instance des compteurs de performance. Les utilisateurs ne doivent pas essayer toointerpret cette partie du nom instance de compteur de performance hello.

*ServiceFabricPartitionID* est représentation de chaîne hello Hello ID de partition de Service Fabric qui hello l’instance de compteur de performance est associé. ID de partition Hello est un GUID, et sa représentation sous forme de chaîne est générée via hello [ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx) méthode avec le spécificateur de format « D ».

*ActorRuntimeInternalID* est la représentation sous forme de chaîne hello d’un entier 64 bits qui est généré par le runtime de l’ensemble fibre optique acteurs hello pour son usage interne. Il est inclus dans l’instance de compteur de performance hello nom tooensure son unicité et éviter les conflits avec les autres noms d’instance des compteurs de performance. Les utilisateurs ne doivent pas essayer toointerpret cette partie du nom instance de compteur de performance hello.

Hello Voici un exemple d’un nom d’instance de compteur pour un compteur qui appartient toohello `Service Fabric Actor Method` catégorie :

`ivoicemailboxactor.leavemessageasync_2_89383d32-e57e-4a9b-a6ad-57c6792aa521_635650083804480486`

Dans l’exemple hello ci-dessus, `ivoicemailboxactor.leavemessageasync` est le nom de la méthode hello `2` est hello ID 32 bits généré pour interne du runtime de hello utiliser, `89383d32-e57e-4a9b-a6ad-57c6792aa521` est la représentation sous forme de chaîne hello d’ID de partition de Service Fabric hello, et `635650083804480486` hello 64 bits ID généré pour une utilisation interne du runtime hello.

## <a name="list-of-events-and-performance-counters"></a>Liste d'événements et de compteurs de performances
### <a name="actor-method-events-and-performance-counters"></a>Événements et compteurs de performances de la méthode d'acteur
Hello Reliable Actors runtime émet hello suivant des événements liés trop[les méthodes intervenant](service-fabric-reliable-actors-introduction.md).

| Nom de l'événement | ID de l’événement | Level | Mot clé | Description |
| --- | --- | --- | --- | --- |
| ActorMethodStart |7 |Détaillé |0x2 |Acteurs runtime concerne tooinvoke une méthode d’acteur. |
| ActorMethodStop |8 |Détaillé |0x2 |Une méthode d’acteur a fini de s’exécuter. Autrement dit, méthode d’acteur toohello du runtime hello appel asynchrone a retourné et hello la tâche retournée par la méthode d’acteur hello est terminée. |
| ActorMethodThrewException |9 |Avertissement |0x3 |Une exception a été levée pendant l’exécution de hello d’une méthode d’acteur, au cours de la méthode d’acteur toohello du runtime hello appel asynchrone ou lors de l’exécution de hello de tâche hello retourné par la méthode d’acteur hello. Cet événement indique une sorte de défaillance dans le code hello acteur qui nécessite un examen. |

Hello Reliable Actors runtime publie hello suivant des compteurs de performances connexes toohello d’exécution des méthodes d’acteur.

| Nom de la catégorie | Nom du compteur | Description |
| --- | --- | --- |
| Service Fabric Actor Method |Appels/s |Nombre de fois que la méthode de service d’acteur hello est appelé par seconde |
| Service Fabric Actor Method |Moyenne en millisecondes par appel |Méthode de service durée tooexecute hello acteur en millisecondes |
| Service Fabric Actor Method |Exceptions levées/s |Nombre de fois que hello la méthode de service d’acteur a levé une exception par seconde |

### <a name="concurrency-events-and-performance-counters"></a>Événements et compteurs de performances de l'accès concurrentiel
Hello Reliable Actors runtime émet hello suivant des événements liés trop[concurrence](service-fabric-reliable-actors-introduction.md#concurrency).

| Nom de l'événement | ID de l’événement | Level | Mot clé | Description |
| --- | --- | --- | --- | --- |
| ActorMethodCallsWaitingForLock |12 |Détaillé |0x8 |Cet événement est écrit au début de hello de chaque nouvelle tour d’un acteur. Il contient le nombre hello d’appels d’acteur qui attendent un verrou par acteur tooacquire hello qui applique la concurrence activer en attente. |

Hello Reliable Actors runtime publie hello suivant tooconcurrency connexes des compteurs de performances.

| Nom de la catégorie | Nom du compteur | Description |
| --- | --- | --- |
| Service Fabric Actor |Nombre d'appels d'acteur en attente du verrou d'acteur |Nombre d’appels d’acteur en attente d’un verrou par acteur tooacquire hello qui applique la concurrence activer en attente |
| Service Fabric Actor |Moyenne en millisecondes par attente de verrou |Verrou par acteur tooacquire prises (en millisecondes) temps hello qui applique la concurrence activer |
| Service Fabric Actor |Moyenne en millisecondes de maintien du verrou par acteur |Durée (en millisecondes) pour le hello est maintenu un verrou par acteur |

### <a name="actor-state-management-events-and-performance-counters"></a>Événements et compteurs de performances de gestion des états d'acteur
Hello Reliable Actors runtime émet hello suivant des événements liés trop[gestion d’état acteur](service-fabric-reliable-actors-state-management.md).

| Nom de l'événement | ID de l’événement | Level | Mot clé | Description |
| --- | --- | --- | --- | --- |
| ActorSaveStateStart |10 |Détaillé |0x4 |Acteurs runtime est sur un état d’acteur toosave hello. |
| ActorSaveStateStop |11 |Détaillé |0x4 |Acteurs runtime a terminé l’enregistrement de l’état d’acteur hello. |

Hello Reliable Actors runtime publie hello suivant de gestion d’état de performances des compteurs tooactor connexes.

| Nom de la catégorie | Nom du compteur | Description |
| --- | --- | --- |
| Service Fabric Actor |Moyenne en millisecondes par opération d'enregistrement d'état |Durée toosave un état d’acteur en millisecondes |
| Service Fabric Actor |Moyenne en millisecondes par opération de chargement d'état |Durée de l’état d’acteur tooload en millisecondes |

### <a name="events-related-tooactor-replicas"></a>Les événements connexes tooactor réplicas
Hello Reliable Actors runtime émet hello suivant des événements liés trop[réplicas d’acteur](service-fabric-reliable-actors-platform.md#service-fabric-partition-concepts-for-actors).

| Nom de l'événement | ID de l’événement | Level | Mot clé | Description |
| --- | --- | --- | --- | --- |
| ReplicaChangeRoleToPrimary |1 |Informations |0x1 |Réplica d’acteur modifiée tooPrimary de rôle. Cela implique que les acteurs hello pour cette partition seront créées à l’intérieur de ce réplica. |
| ReplicaChangeRoleFromPrimary |2 |Informations |0x1 |Réplica d’acteur modifiée toonon rôle principal. Cela implique que les acteurs hello pour cette partition n’est plus seront créées à l’intérieur de ce réplica. Aucune nouvelle demande ne sera remis tooactors déjà créé au sein de ce réplica. les acteurs Hello seront détruits après avoir effectué toutes les demandes en cours d’exécution. |

### <a name="actor-activation-and-deactivation-events-and-performance-counters"></a>Événements d'activation et de désactivation des acteurs et compteurs de performances
Hello Reliable Actors runtime émet hello suivant des événements liés trop[acteur activation et désactivation](service-fabric-reliable-actors-lifecycle.md).

| Nom de l'événement | ID de l’événement | Level | Mot clé | Description |
| --- | --- | --- | --- | --- |
| ActorActivated |5 |Informations |0x1 |Un acteur a été activé. |
| ActorDeactivated |6 |Informations |0x1 |Un acteur a été désactivé. |

Hello Reliable Actors runtime publie hello suivant des compteurs de performance liés tooactor activation et désactivation.

| Nom de la catégorie | Nom du compteur | Description |
| --- | --- | --- |
| Service Fabric Actor |Moyenne OnActivateAsync en millisecondes |La méthode OnActivateAsync tooexecute de temps en millisecondes |

### <a name="actor-request-processing-performance-counters"></a>Compteurs de performances de traitement de la requête d’acteur
Lorsqu’un client appelle une méthode via un objet de proxy acteur, il renvoie un message de demande qui est envoyé sur le service d’acteur toohello hello réseau. service de Hello traite le message de demande hello et envoie une réponse au client toohello précédent. Hello Reliable Actors runtime publie hello après le traitement de la demande des compteurs connexes tooactor performances.

| Nom de la catégorie | Nom du compteur | Description |
| --- | --- | --- |
| Service Fabric Actor |Nombre de requêtes en attente |Nombre de demandes traitées dans le service hello |
| Service Fabric Actor |Moyenne en millisecondes par requête |Durée (en millisecondes) de hello service tooprocess une demande |
| Service Fabric Actor |Moyenne en millisecondes pour la désérialisation de la requête |Message de demande d’acteur temps toodeserialize prises (en millisecondes) lorsqu’elle est reçue au niveau de service de hello |
| Service Fabric Actor |Moyenne en millisecondes pour la sérialisation de la réponse |Message de réponse temps tooserialize prises (en millisecondes) hello intervenant au niveau de service hello avant hello est envoyée toohello client |

## <a name="next-steps"></a>Étapes suivantes
* [Comment Reliable Actors utiliser hello Service Fabric](service-fabric-reliable-actors-platform.md)
* [Documentation de référence de l’API d’acteur](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [Exemple de code](https://github.com/Azure/servicefabric-samples)
* [Fournisseurs EventSource dans PerfView](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/)
