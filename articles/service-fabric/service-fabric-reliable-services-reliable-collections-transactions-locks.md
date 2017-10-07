---
title: aaaTransactions et Modes de verrouillage dans Azure Service Fabric fiable Collections | Documents Microsoft
description: "Verrouillage et transactions des collections fiables et gestionnaire d’état fiable Azure Service Fabric."
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
ms.openlocfilehash: 340e029aa98f43ad6e46b48f687dad01f9d96f69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="transactions-and-lock-modes-in-azure-service-fabric-reliable-collections"></a>Modes Transactions et Verrouillage dans les Collections fiables Azure Service Fabric

## <a name="transaction"></a>Transaction
Une transaction est une séquence d’opérations effectuées en tant qu’unité logique de travail unique.
Une transaction doit présenter hello propriétés ACID suivantes. (voir : https://technet.microsoft.com/en-us/library/ms190612)
* **Atomicité** : une transaction doit correspondre à une unité de travail atomique. En d’autres termes, soit toutes les modifications de données sont effectuées, soit aucune n’est effectuée.
* **Cohérence** : une fois terminée, une transaction doit laisser toutes les données dans un état cohérent. Toutes les structures de données internes doivent être corrects à fin hello de transaction de hello.
* **Isolation**: les Modifications apportées par les transactions simultanées doivent être isolées des modifications de hello effectuées par d’autres transactions simultanées. niveau d’isolation de Hello utilisé pour une opération dans une ITransaction est déterminé par hello IReliableState une opération de hello.
* **Durabilité**: une fois une transaction terminée, ses effets sont définitivement en place dans le système de hello. modifications de Hello sont conservées même en cas de hello une défaillance du système.

### <a name="isolation-levels"></a>Niveaux d'isolement
Niveau d’isolement définit le degré de hello transaction de hello toowhich doit être isolée des modifications apportées par d’autres transactions.
Il existe deux niveaux d'isolement pris en charge dans les Collections fiables :

* **Lecture renouvelable**: Spécifie que les instructions ne peuvent pas lire les données qui a été modifiées mais pas encore validées par d’autres transactions et qu’aucune autre transaction ne peut modifier les données qui a été lu par la transaction en cours hello jusqu'à hello en cours fin de la transaction. Pour plus d’informations, consultez la page [https://msdn.microsoft.com/library/ms173763.aspx](https://msdn.microsoft.com/library/ms173763.aspx).
* **Instantané**: Spécifie que les données lues par n’importe quelle instruction dans une transaction sont la version cohérente de hello de données hello qui existaient au début de hello de transaction de hello.
  transaction de Hello peut reconnaître seulement les modifications de données qui ont été validées avant le début de hello de transaction de hello.
  Modifications de données effectuées par d’autres transactions après hello de début de la transaction en cours hello ne sont pas visibles toostatements l’exécution de la transaction en cours hello.
  Hello se comme si les instructions de hello dans une transaction obtenaient un instantané des données de hello validée telles qu’elles existaient au début de hello de transaction de hello.
  Les instantanés sont cohérents sur les Collections fiables.
  Pour plus d’informations, consultez la page [https://msdn.microsoft.com/library/ms173763.aspx](https://msdn.microsoft.com/library/ms173763.aspx).

Collections fiables choisissent automatiquement hello toouse de niveau d’isolation pour une opération de lecture donnée selon l’opération de hello et rôle hello du réplica de hello lors de la création de la transaction hello.
Voici la table hello qui décrit les valeurs par défaut au niveau d’isolation pour les opérations de dictionnaire fiable et de file d’attente.

| Fonctionnement \ Rôle | Primaire | Secondaire |
| --- |:--- |:--- |
| Lecture d'une seule entité |Lecture renouvelée |Instantané |
| Énumération, décompte |Instantané |Instantané |

> [!NOTE]
> `IReliableDictionary.TryGetValueAsync` et `IReliableQueue.TryPeekAsync` sont des exemples typiques d’opérations à une seule entité.
> 

Hello dictionnaire fiable et hello file d’attente fiable prend en charge l’écrit votre lecture.
En d’autres termes, toute écriture dans une transaction ne sera visible tooa suivant lue qui appartient toohello la même transaction.

## <a name="locks"></a>Verrous
Dans les Collections fiable, implémentez de toutes les transactions rigoureux à deux phases de verrouillage : une transaction ne libère pas les verrous hello elle a acquis jusqu'à ce que la transaction de hello se termine avec un abandon ou une validation.

Dictionnaire fiable utilise le verrou au niveau des lignes pour toutes les opérations à une seule entité.
File d’attente fiable compense la concurrence par une propriété FIFO transactionnelle stricte.
File d’attente fiable utilise des verrous au niveau des opérations permettant une transaction avec `TryPeekAsync` et/ou `TryDequeueAsync`, et une transaction avec `EnqueueAsync` à la fois.
Notez que toopreserve FIFO, si un `TryPeekAsync` ou `TryDequeueAsync` jamais observe que hello fiable de file d’attente est vide, ils seront également verrouiller `EnqueueAsync`.

Les opérations d’écriture prennent toujours des verrous exclusifs.
Pour les opérations de lecture, hello verrouillage dépend de plusieurs facteurs.
Les opérations de lecture effectuées à l’aide de l’isolement d’instantané ne sont pas verrouillées.
Les opérations de lecture renouvelée utilisent par défaut des verrous partagés.
Toutefois, pour toute opération de lecture qui prend en charge la lecture renouvelable, utilisateur de hello peut demander un verrou de mise à jour au lieu de hello verrou partagé.
Un verrou de mise à jour est qu'un verrou asymétrique utilisé tooprevent une forme courante d’interblocage se produit lorsque plusieurs transactions verrouillent les ressources pour les mises à jour potentielles à une date ultérieure.

Vous trouverez la matrice de compatibilité de verrouillage Hello Bonjour tableau suivant :

| Requête \ Accordé | Aucun | Partagé | Mettre à jour | Exclusif |
| --- |:--- |:--- |:--- |:--- |
| Partagé |Aucun conflit |Aucun conflit |Conflit |Conflit |
| Mettre à jour |Aucun conflit |Aucun conflit |Conflit |Conflit |
| Exclusif |Aucun conflit |Conflit |Conflit |Conflit |

Argument de délai d’attente Bonjour fiable API de Collections est utilisé pour la détection de blocage.
Par exemple, deux transactions (T1 et T2) essaient tooread et mettre à jour K1.
Il est possible de leur toodeadlock, car ils sont tous deux avoir hello des verrou partagé.
Dans ce cas, une ou les deux opérations de hello expire.

Ce scénario de blocage est un exemple illustrant parfaitement en quoi le verrou de mise à jour peut empêcher les blocages.

## <a name="next-steps"></a>Étapes suivantes
* [Utilisation des collections fiables](service-fabric-work-with-reliable-collections.md)
* [Notifications Reliable Services](service-fabric-reliable-services-notifications.md)
* [Sauvegarde et restauration de Reliable Services (récupération d’urgence)](service-fabric-reliable-services-backup-restore.md)
* [Configuration du Gestionnaire d’état fiable](service-fabric-reliable-services-configuration.md)
* [Référence du développeur pour les Collections fiables](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

