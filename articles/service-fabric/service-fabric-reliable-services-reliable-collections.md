---
title: "aaaIntroduction tooReliable Collections dans les services avec état Azure Service Fabric | Documents Microsoft"
description: "Services avec état service Fabric fournissent des collections fiables qui vous toowrite les applications de cloud hautement disponibles, évolutives et à faible latence."
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: masnider,rajak
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: mcoskun
ms.openlocfilehash: 9f67c48f13e8b91b84977e127e2545cbb9d9a158
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooreliable-collections-in-azure-service-fabric-stateful-services"></a>Introduction tooReliable Collections dans les services avec état Azure Service Fabric
Fiables Collections vous permettent aux applications de cloud hautement disponibles, évolutives et à faible latence toowrite comme si vous écrivez des applications d’ordinateur unique. Hello classes Bonjour **Microsoft.ServiceFabric.Data.Collections** espace de noms fournissent un jeu de collections qui automatiquement votre état hautement disponible. Les développeurs doivent tooprogram, toohello uniquement les API de Collection fiable et permettent à des Collections fiable de gérer hello répliquées et état local.

Hello principale différence entre les Collections fiable et d’autres technologies de haute disponibilité (par exemple, Redis, service de Table Azure et le service de file d’attente Azure) est que l’état de hello est conservé localement dans l’instance de service hello lors également rendue hautement disponible. Cela signifie que :

* Toutes les lectures sont locales, ce qui entraîne des lectures à faible latence et à débit élevé.
* Toutes les écritures entraînent hello minimum d’e/s du réseau, ce qui entraîne une latence faible et haut débit est écrit.

![Image de l'évolution des collections.](media/service-fabric-reliable-services-reliable-collections/ReliableCollectionsEvolution.png)

Collections fiables peuvent être considérées comme évolution naturelle de hello Hello **System.Collections** classes : un nouveau jeu de collections qui sont conçues pour les applications cloud et sur plusieurs ordinateurs hello sans augmenter la complexité de la développeur de Hello. En tant que telles, les Collections fiables sont :

* Répliquées : les modifications d'état sont répliquées pour une haute disponibilité.
* Persistantes : Les données sont persistante toodisk pour une durabilité contre les pannes à grande échelle (par exemple, une panne de courant de centre de données).
* Asynchrone : Les API sont tooensure asynchrone que les threads ne sont pas bloqués lors de subir des e/s.
* Transactionnelle : API utilise abstraction hello de transactions vous pouvez de gérer facilement plusieurs Collections fiable au sein d’un service.

Collections fiables fournissent des garanties de cohérence forte hors toomake de zone hello raisonnement concernant l’état de l’application plus facile.
Cohérence forte est obtenue en s’assurant que la transaction est validée terminer uniquement après que l’intégralité de la transaction hello a été enregistré sur un quorum majoritaire de réplicas, y compris hello principal.
tooachieve de cohérence plus faible, applications peuvent accuser réception différé toohello client/demandeur avant le retour de validation asynchrone de hello.

API de Collections fiable Hello sont une évolution de collections simultanées API (trouvé dans hello **System.Collections.Concurrent** espace de noms) :

* Asynchrone : Retourne une tâche puisque, contrairement aux regroupements simultanées, les opérations de hello sont répliquées et persistante.
* Paramètres de sortie ne : utilise `ConditionalValue<T>` tooreturn un bool et une valeur à la place de paramètres de sortie. `ConditionalValue<T>`est semblable à `Nullable<T>` mais ne nécessite ne pas de T toobe un struct.
* Transactions : Utilise un transaction objet tooenable hello utilisateur toogroup d’actions sur plusieurs Collections fiable dans une transaction.

Actuellement, **Microsoft.ServiceFabric.Data.Collections** contient trois collections :

* [Dictionnaire fiable](https://msdn.microsoft.com/library/azure/dn971511.aspx): représente une collection répliquée, transactionnelle et asynchrone de paires clé/valeur. Similaire trop**ConcurrentDictionary**, les deux hello clé et valeur de hello peut être de n’importe quel type.
* [File d’attente fiable](https://msdn.microsoft.com/library/azure/dn971527.aspx): représente une file d’attente FIFO stricte, répliquée, transactionnelle et asynchrone. Similaire trop**ConcurrentQueue**, valeur de hello peut être de n’importe quel type.
* [File d’attente simultanée fiable](service-fabric-reliable-services-reliable-concurrent-queue.md) : représente une file d’attente de classement de meilleur effort répliquée, transactionnelle et asynchrone, pour un débit élevé. Similaire toohello **ConcurrentQueue**, valeur de hello peut être de n’importe quel type.

## <a name="next-steps"></a>Étapes suivantes
* [Instructions et recommandations relatives aux collections fiables](service-fabric-reliable-services-reliable-collections-guidelines.md)
* [Utilisation des collections fiables](service-fabric-work-with-reliable-collections.md)
* [Transactions et verrous](service-fabric-reliable-services-reliable-collections-transactions-locks.md)
* [Gestionnaire d’état fiable et éléments internes de collections](service-fabric-reliable-services-reliable-collections-internals.md)
* Gestion des données
  * [Sauvegarde et restauration](service-fabric-reliable-services-backup-restore.md)
  * [Notifications](service-fabric-reliable-services-notifications.md)
  * [Sérialisation de Collection fiable](service-fabric-reliable-services-reliable-collections-serialization.md)
  * [Sérialisation et mise à niveau](service-fabric-application-upgrade-data-serialization.md)
  * [Configuration du Gestionnaire d’état fiable](service-fabric-reliable-services-configuration.md)
* Autres
  * [Démarrage rapide de Reliable Services](service-fabric-reliable-services-quick-start.md)
  * [Référence du développeur pour les Collections fiables](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
