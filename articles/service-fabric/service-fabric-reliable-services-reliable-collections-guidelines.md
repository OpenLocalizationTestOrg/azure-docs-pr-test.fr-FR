---
title: aaaGuidelines & recommandations pour les Collections fiable dans Azure Service Fabric | Documents Microsoft
description: "Instructions et recommandations relatives à l’utilisation de collections fiables Fabric Service"
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
ms.date: 5/3/2017
ms.author: mcoskun
ms.openlocfilehash: bcdbc9d013bc044e06c43761e7f515c7e4bf340c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="guidelines-and-recommendations-for-reliable-collections-in-azure-service-fabric"></a>Instructions et recommandations pour les collections fiables dans Azure Service Fabric
Cette section fournit des instructions pour l’utilisation du gestionnaire d’état fiable et des collections fiables. Hello vise toohelp utilisateurs évitent les pièges courants.

les instructions Hello sont organisées comme des recommandations simples ci-après préfixés avec les termes du contrat de hello *faire*, *envisagez*, *Évitez* et *pas*.

* Ne modifiez pas un objet de type personnalisé renvoyé par les opérations de lecture (par exemple, `TryPeekAsync` ou `TryGetValueAsync`). Collections fiables, tout comme les Collections simultanées, retournent un toohello des objets de référence et non une copie.
* Faire hello en copie complète a retourné d’objet d’un type personnalisé avant de le modifier. Étant donné que les structures et les types intégrés sont passés par valeur, vous n’avez pas besoin de toodo une copie complète sur les.
* N’utilisez pas `TimeSpan.MaxValue` pour les délais d’attente. Délais d’expiration doivent être utilisé toodetect blocages.
* N’utilisez pas une transaction une fois qu’elle a été validée, abandonnée ou supprimée.
* N’utilisez pas une énumération en dehors de l’étendue de transaction hello qu'il a été créé.
* Ne créez pas une transaction au sein de l’instruction `using` d’une autre transaction, car cela peut provoquer des blocages.
* Assurez-vous que votre implémentation de `IComparable<TKey>` est correcte. système de Hello prend la dépendance `IComparable<TKey>` pour fusionner des points de contrôle et des lignes.
* Utilisez le verrou de mise à jour lors de la lecture d’un élément avec un tooupdate intention il tooprevent une certaine classe de blocages.
* Envisagez de vos éléments (par exemple, TKey + TValue dictionnaire fiable) ci-dessous 80 kilo-octets : hello plus petit mieux. Cela réduit hello des spécifications d’e/s de tas des objets volumineux d’utilisation, ainsi que de disque et réseau. Souvent, il réduit la réplication des données en double lorsque qu’une petite partie de la valeur de hello est en cours de mise à jour. Tooachieve de manière commune dans le dictionnaire fiable, est toobreak les lignes dans les lignes de toomultiple.
* Envisagez d’utiliser la sauvegarde et de restauration de la récupération d’urgence toohave fonctionnalité.
* Évitez de combiner des opérations d’entité unique et les opérations de plusieurs entités (par exemple `GetCountAsync`, `CreateEnumerableAsync`) Bonjour même échéance toohello différents niveaux d’isolation de la transaction.
* Gérez l’exception InvalidOperationException. Les transactions utilisateur peuvent être annulées par le système hello pour diverses raisons. Par exemple, lorsque hello fiable Gestionnaire d’état change son rôle de principal ou lorsqu’une transaction à long terme bloque la troncation du journal des transactions hello. Dans ce cas, l’utilisateur peut recevoir l’exception InvalidOperationException, indiquant que sa transaction a déjà été terminée. En supposant que, arrêt hello de transaction de hello n’a pas été demandé par l’utilisateur de hello, meilleure manière toohandle cette exception est la transaction de hello toodispose, vérifiez si le jeton d’annulation hello a été signalé (ou rôle hello du réplica de hello a été modifié) et dans le cas contraire créer une nouvelle transaction et une nouvelle tentative.  

Voici certains tookeep choses à l’esprit :

* le délai d’attente de Hello par défaut est quatre secondes pour hello toutes les API de Collection fiable. La plupart des utilisateurs doivent utiliser le délai d’attente de hello par défaut.
* Bonjour jeton d’annulation par défaut est `CancellationToken.None` dans toutes les API de Collections fiable.
* Hello du paramètre de type de clé (*TKey*) pour un dictionnaire fiable doit implémenter correctement `GetHashCode()` et `Equals()`. Les clés doivent être immuables.
* tooachieve haute disponibilité pour hello Collections fiable, chaque service doit avoir au moins une cible et un réplica minimum définir la taille de 3.
* Les opérations de lecture sur hello secondaire peuvent lire les versions qui ne sont pas validée de quorum.
  Cela signifie qu’une version des données lue à partir d’un seul secondaire peut présenter une progression erronée.
  Les lectures à partir du principal sont toujours stables : la progression n’est jamais erronée.

### <a name="next-steps"></a>Étapes suivantes
* [Utilisation des collections fiables](service-fabric-work-with-reliable-collections.md)
* [Transactions et verrous](service-fabric-reliable-services-reliable-collections-transactions-locks.md)
* [Gestionnaire d’état fiable et éléments internes de collections](service-fabric-reliable-services-reliable-collections-internals.md)
* Gestion des données
  * [Sauvegarde et restauration](service-fabric-reliable-services-backup-restore.md)
  * [Notifications](service-fabric-reliable-services-notifications.md)
  * [Sérialisation et mise à niveau](service-fabric-application-upgrade-data-serialization.md)
  * [Configuration du Gestionnaire d’état fiable](service-fabric-reliable-services-configuration.md)
* Autres
  * [Démarrage rapide de Reliable Services](service-fabric-reliable-services-quick-start.md)
  * [Référence du développeur pour les Collections fiables](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
