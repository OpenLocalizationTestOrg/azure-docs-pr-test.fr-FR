---
title: "aaaOverview du modèle de programmation de Service fiable de l’infrastructure de Service hello | Documents Microsoft"
description: "Apprenez-en plus sur le modèle de programmation Service fiable de Service Fabric et commencez à écrire vos propres services."
services: Service-Fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: vturecek; mani-ramaswamy
ms.assetid: 0c88a533-73f8-4ae1-a939-67d17456ac06
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: masnider;
ms.openlocfilehash: 41d1826df902b1f1845c4702bf2567e6b9ca1f1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-services-overview"></a>Présentation de Reliable Services
Azure Service Fabric simplifie l’écriture et la gestion de Reliable Services avec et sans état. Cette rubrique couvre :

* modèle de programmation des Services fiables Hello pour les services et sans état.
* choix de Hello, vous avez toomake lors de l’écriture d’un Service fiable.
* Des scénarios et des exemples de situations dans lesquelles toouse des Services fiables et la manière dont elles sont écrites.

Services fiables est un des hello disponibles sur le Service Fabric des modèles de programmation. Hello autres est hello Reliable Actor modèle de programmation, qui fournit un modèle de programmation intervenant virtuel sur le modèle de Services fiables hello. Pour plus d’informations sur le modèle de programmation Reliable Actors hello, consultez [Introduction tooService infrastructure Reliable Actors](service-fabric-reliable-actors-introduction.md).

L’infrastructure de service gère la durée de vie de hello de services, à partir de la configuration et de déploiement via la mise à niveau et de suppression, via [gestion des applications de Service Fabric](service-fabric-deploy-remove-applications.md).

## <a name="what-are-reliable-services"></a>Définition de Reliable Services
Services fiables vous donne un simple, puissant, de niveau supérieur de programmation toohelp modèle express à ce qui est important tooyour application. Avec les Services fiables de hello modèle de programmation, vous obtenez :

* Autres toohello accès hello Service Fabric API de programmation. Contrairement aux Services de Fabric Service modélisée en tant que [invité exécutables](service-fabric-deploy-existing-app.md), des Services fiables obtenir directement les autres hello toouse hello API de l’infrastructure de Service. Les services peuvent ainsi :
  * Interrogation du système hello
  * signalement d’intégrité sur les entités dans un cluster de hello
  * recevoir des notifications sur les modifications de la configuration et du code
  * rechercher et communiquer avec d’autres services
  * (facultatif) utilisez hello [Collections fiable](service-fabric-reliable-services-reliable-collections.md)
  * ... et en leur donnant accès réduire autres fonctionnalités, à partir d’un modèle de programmation de première classe dans plusieurs langages de programmation.
* Un modèle simple pour exécuter votre propre code qui ressemble aux modèles de programmation auxquels vous êtes habitué. Votre code comporte un point d’entrée bien défini, et son cycle de vie est facile à gérer.
* Un modèle de communication enfichable. Utiliser le transport de votre choix, par exemple HTTP avec hello [API Web](service-fabric-reliable-services-communication-webapi.md), WebSockets, les protocoles TCP personnalisés ou tout autre élément. Le modèle Reliable Services fournit de remarquables options prêtes à l’emploi que vous pouvez utiliser. Vous pouvez également définir les vôtres.
* Pour les services avec état, modèle de programmation des Services fiables hello vous permet de tooconsistently et stocker en toute fiabilité votre état directement dans votre service à l’aide de [fiable Collections](service-fabric-reliable-services-reliable-collections.md). Collections fiables sont un ensemble de classes de collection hautement fiable et disponible qui sera familier tooanyone qui a utilisé des collections c# simple. Traditionnellement, les services nécessitaient des systèmes externes pour la gestion d’état fiable. Grâce aux Collections fiable, vous pouvez stocker votre calcul tooyour suivant d’état avec hello même haute disponibilité et la fiabilité que vous avez arrivé tooexpect à partir de magasins externes hautement disponibles. Ce modèle améliore également la latence, car vous sont la colocalisation de calcul de hello et état, il doit toofunction.

Regardez cette vidéo Microsoft Virtual Academy pour une vue d’ensemble de Reliable Services : <center>
<a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=HhD9566yC_4106218965">
<img src="./media/service-fabric-reliable-services-introduction/ReliableServicesVid.png" WIDTH="360" HEIGHT="244" />
</a>
</center>

## <a name="what-makes-reliable-services-different"></a>En quoi le modèle Reliable Services est-il différent ?
Les Services fiables dans Service Fabric sont différents des services que vous avez peut-être écrits auparavant. Service Fabric fournit la fiabilité, la disponibilité, la cohérence et l'évolutivité.

* **Fiabilité** : votre service reste les même dans des environnements non fiables dans lequel vos ordinateurs échoueront ou atteint des problèmes de réseau, ou dans les cas où hello services eux-mêmes rencontrer des erreurs et les pannes ou faire échouer. Pour les services avec état, l’état est conservée même en présence de hello de réseau ou d’autres échecs.
* **Disponibilité** : votre service est accessible et réactif. Service Fabric gère le nombre souhaité de copies en cours d’exécution.
* **Évolutivité** - Services sont dissociés de matériel spécifique, et ils peuvent augmenter ou réduire selon les besoins via l’ajout de hello ou la suppression de matériel ou d’autres ressources. Les services sont tooensure facilement partitionnée (en particulier dans les cas avec état hello) service de hello capable d’évoluer et gérer les défaillances partielles. Les services peuvent être créés et supprimés dynamiquement par le biais de code, l’activation de plusieurs instances toobe lancé selon les besoins, par exemple dans les demandes de toocustomer de réponse. Enfin, le Service Fabric encourage lightweight toobe de services. L’infrastructure de service permet à des milliers de services toobe configurés dans un seul processus plutôt que nécessitant ou consacrer des instances du système d’exploitation complètes ou processus tooa seule instance d’un service.
* **Cohérence** -toutes les informations stockées dans ce service peuvent être garanties toobe cohérent. Cela s’applique également à plusieurs collections fiables au sein d’un service. Les modifications dans des collections au sein d’un service peuvent être effectuées de manière atomique au niveau transactionnel.

## <a name="service-lifecycle"></a>Cycle de vie du service
Que votre service soit avec état ou sans état, Reliable Services fournit un cycle de vie simple qui vous permet de rattacher rapidement votre code et de vous lancer.  Il existe une ou deux méthodes que vous devez tooimplement tooget votre service opérationnel et en cours d’exécution.

* **CreateServiceReplicaListeners/CreateServiceInstanceListeners** -cette méthode est où le service de hello définit les piles de communication hello qu’elles souhaitent toouse. Hello pile de communication, tel que [API Web](service-fabric-reliable-services-communication-webapi.md), est ce que définit hello de point de terminaison écoute ou de points de terminaison de Bienvenue (comment les clients atteindre le service de hello) de service. Il définit également la façon dont les messages hello qui s’affichent interagissent avec rest hello hello du code de service.
* **RunAsync** -cette méthode est où votre service s’exécute sa logique d’entreprise, et où elle serait déclencher les tâches en arrière-plan qui doivent s’exécuter pour la durée de vie hello du service de hello. jeton d’annulation Hello fourni est un signal pour lorsque ce travail doit s’arrêter. Par exemple, si le service de hello doit toopull des messages en dehors d’une file d’attente fiable et les traiter, voici où ce travail se produit.

Si vous êtes apprendre à utiliser des services fiables pour hello première fois, lisez la suite ! Si vous avez besoin d’une description détaillée de hello du cycle de vie des services fiables, vous pouvez head sur trop[cet article](service-fabric-reliable-services-lifecycle.md).

## <a name="example-services"></a>Exemples de service
En sachant ce modèle de programmation, jetons un œil rapide à deux services différents toosee comment ces éléments s’imbriquent.

### <a name="stateless-reliable-services"></a>Services fiables sans état
Un service sans état est celui dans lequel aucun état conservées dans le service de hello d’appels. Tout état présent est entièrement jetable et ne nécessite aucune synchronisation, réplication, persistance ou haute disponibilité.

Par exemple, considérez une calculatrice qui n’a aucune mémoire et reçoit tous les tooperform de termes et les opérations en une seule fois.

Dans ce cas, hello `RunAsync()` (c#) ou `runAsync()` (Java) de hello service peut être vide, car il n’existe aucun arrière-plan-traitement de la tâche que le service hello doit toodo. Lorsque le service de calculatrice hello est créée, elle retourne un `ICommunicationListener` (c#) ou `CommunicationListener` (Java) (par exemple [API Web](service-fabric-reliable-services-communication-webapi.md)) qui ouvre un point de terminaison écoute sur certains ports. Ce point de terminaison écoute raccorde toohello différentes méthodes de calcul (exemple : « Add (n1, n2) ») qui définissent l’API publique de la calculatrice hello.

Lorsqu’un appel est effectué à partir d’un client, méthode appropriée de hello est appelé, et service de calculatrice hello effectue des opérations de hello sur hello données fournie et retourne le résultat de hello. Il ne stocke aucun état.

Le fait de ne pas stocker d’état interne rend cet exemple de calculatrice simple, mais la plupart des services ne sont pas réellement sans état. Au lieu de cela, ils externaliser leur toosome état autre magasin. (Par exemple, toute application web qui s’appuie sur la conservation de l’état de session dans un magasin de stockage ou un cache n’est pas sans état.)

Un exemple courant de services comment sans état sont utilisés dans le Service Fabric est un serveur frontal qu’expose hello API publique pour une application web. le service frontal Hello traite puis toostateful services toocomplete une demande de l’utilisateur. Dans ce cas, les appels à partir de clients sont dirigée tooa connu de port, par exemple, 80, où un service sans état hello est à l’écoute. Ce service sans état reçoit l’appel de hello et détermine si les appels de hello est d’un tiers de confiance et dont le service est destiné.  Ensuite, un service sans état hello transfère la partition correcte du toohello hello appel d’un service avec état hello et attend une réponse. Lorsqu’un service sans état hello reçoit une réponse, il répond toohello initiale du client. Vous trouverez un exemple de ce type de service dans nos exemples [C#](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started) / [Java](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Actors/VisualObjectActor/VisualObjectWebService). Cela n'est qu’un exemple de ce modèle dans les exemples de hello, d’autres sont également d’autres exemples.

### <a name="stateful-reliable-services"></a>Services fiables avec état
Un service avec état est celle qui doit avoir une partie de l’état restent cohérentes et présent dans l’ordre pour hello service toofunction. Prenons pour exemple un service qui calcule constamment une moyenne mobile d’une valeur en fonction des mises à jour qu’il reçoit. toodo, il doit avoir hello le jeu actuel de demandes entrantes, il doit tooprocess et hello moyenne actuelle. Tout service qui récupère, traite et stocke des informations dans un magasin externe (comme un magasin de tables ou d’objets blob Azure) est un service avec état. Simplement, il conserve son état dans le magasin d’état externe hello.

La plupart des services stocker aujourd'hui leur état en externe, car le magasin externe hello est ce que fournit la fiabilité, disponibilité, évolutivité et la cohérence pour cet état. Dans l’infrastructure de Service, les services ne sont pas requis toostore leur état en externe. L’infrastructure de service prend en charge des conditions requises pour le code de service hello et état du service hello.

> [!NOTE]
> La prise en charge de Reliable Services avec état n’est pas encore disponible sur Linux (pour C# ou Java).
>

Supposons que nous voulons toowrite un service qui traite des images. toodo cela, prend de service hello dans une série d’image et hello de tooperform conversions sur cette image. Ce service renvoie un écouteur de communication (par exemple, une API Web) qui expose une API telle que `ConvertImage(Image i, IList<Conversion> conversions)`. Lorsqu’il reçoit une demande, le service de hello stocke dans un `IReliableQueue`et retourne un client de toohello id afin qu’il peut suivre la demande de hello.

Dans ce service, `RunAsync()` pourrait être plus complexe. service de Hello comporte une boucle à l’intérieur de son `RunAsync()` qui extrait des demandes de `IReliableQueue` et effectue des conversions hello demandées. les résultats de Hello obtient stockés dans un `IReliableDictionary` afin que lorsque le client de hello est restauré, ils peuvent récupérer leurs images converties. tooensure que même en cas de problème image de hello n’est perdue, ce Service fiable serait extrait file d’attente hello, effectuer des conversions de hello et stocker les résultats de hello dans une transaction unique. Dans ce cas, message de type hello est supprimé de la file d’attente hello et résultats de hello sont stockés dans le dictionnaire de résultat hello uniquement lorsque les conversions hello sont terminées. Vous pouvez également hello service pourrait extraire l’image hello en dehors de la file d’attente hello ; immédiatement stockez-le dans un magasin distant Cela réduit hello quantité du service d’état hello a toomanage, mais augmente la complexité, car le service de hello a tookeep hello nécessaires toomanage hello distant magasin de métadonnées de. Deux approches, si quelque chose a échoué dans demande de milieu hello hello reste dans toobe d’attente de file d’attente hello traité.

Une chose toonote, à propos de ce service est qu’il peut sembler un service .NET normal ! Bonjour seule différence est que les structures de données de salutation utilisé (`IReliableQueue` et `IReliableDictionary`) sont fournies par l’infrastructure de Service et sont hautement fiable, disponible et cohérente.

## <a name="when-toouse-reliable-services-apis"></a>Lorsque toouse API des Services fiables
Si hello suivantes caractérisent les besoins de votre service d’application, vous devez envisager les API des Services fiables :

* Vous souhaitez que le code de votre service (et éventuellement d’état) toobe hautement fiable et disponible
* Vous avez besoin de garanties transactionnelles entre plusieurs unités d’état (par exemple, commandes et éléments de ligne de commande).
* L’état de votre application peut être naturellement modélisé sous forme de Files d’attente et de Dictionnaires fiables
* Votre code d’application ou l’état doit toobe hautement disponible avec une latence faible lectures et écritures.
* Votre application a besoin d’accès concurrentiel de hello de toocontrol ou de la granularité d’opérations traitées sur un ou plusieurs regroupements fiable.
* Vous souhaitez les communications hello toomanage ou hello contrôle le schéma de votre service de partitionnement.
* Votre code a besoin d’un environnement d’exécution libre de threads.
* Votre application doit toodynamically créer ou de détruire des dictionnaires fiable ou les files d’attente ou les Services ensemble lors de l’exécution.
* Vous devez tooprogrammatically fournie par l’infrastructure de Service de sauvegarde et restauration fonctionnalités de contrôle pour l’état de votre service.
* Votre application a besoin de l’historique des modifications toomaintain ses unités de l’état.
* Vous souhaitez toodevelop ou consommer des fournisseurs d’état personnalisé, développé tiers.

## <a name="next-steps"></a>Étapes suivantes
* [Démarrage rapide de Reliable Services](service-fabric-reliable-services-quick-start.md)
* [Utilisation avancée de Reliable Services](service-fabric-reliable-services-advanced-usage.md)
* [modèle de programmation Hello Reliable Actors](service-fabric-reliable-actors-introduction.md)
