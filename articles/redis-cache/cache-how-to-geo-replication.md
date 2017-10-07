---
title: "aaaHow tooconfigure géo-réplication Azure Redis cache | Documents Microsoft"
description: "Découvrez comment tooreplicate votre le Cache Redis Azure instances différentes régions géographiques."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 375643dc-dbac-4bab-8004-d9ae9570440d
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: sdanie
ms.openlocfilehash: edcd6f202b51055d1a4e47ecaf11f9977d50aa81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-geo-replication-for-azure-redis-cache"></a>Comment tooconfigure géo-réplication Azure Redis cache

La géoréplication fournit un mécanisme permettant de lier deux instances Cache Redis Azure de niveau Premium. Un cache est désigné comme le cache de lié principal hello et hello autre en tant que cache de lié secondaire hello. cache lié de Hello secondaire devient en lecture seule, et les données toohello écrit le cache principal est répliquée toohello cache lié secondaire. Cette fonctionnalité peut être utilisé tooreplicate un cache entre les régions Azure. Cet article fournit un guide de tooconfiguring géo-réplication pour vos instances de Cache Redis Azure de niveau Premium.

## <a name="geo-replication-prerequisites"></a>Conditions préalables à la géoréplication

tooconfigure géo-réplication entre deux caches, hello suivant les conditions préalables doit être remplie :

- Les deux caches doivent être de [niveau Premium](cache-premium-tier-intro.md).
- Les deux caches doivent être Bonjour même abonnement Azure.
- cache lié de Hello secondaire doit être soit hello même tarification couche ou un niveau tarifaire supérieur hello principal lié de cache.
- Si le cache lié principaux de hello a activé le clustering, hello secondaire lié doit être cache clustering activé avec hello même nombre de partitions que le cache de lié principal hello.
- Les deux caches doivent être créés et en cours d’exécution.
- La persistance ne doit être activée sur aucun des caches.
- Géo-réplication entre des caches Bonjour que même réseau virtuel est prise en charge. Géo-réplication entre des caches dans des réseaux virtuels différents est également prise en charge, tant que hello deux des réseaux virtuels sont configurés de telle sorte que les ressources dans des réseaux virtuels hello sont en mesure de tooreach eux via des connexions TCP.

Après avoir configuré la géo-réplication, hello restrictions suivantes s’appliquent paire de cache lié tooyour :

- cache de lié secondaire Hello est en lecture seule ; Vous pouvez lire à partir de celui-ci, mais vous ne peut pas écrire n’importe quel tooit de données. 
- Toutes les données qui était en cache lié de hello secondaire avant l’ajout de lien de hello sont supprimées. Si hello géo-réplication est ensuite supprimée toutefois hello répliquées données demeurent dans le cache lié secondaire hello.
- Vous ne pouvez pas lancer un [opération de mise à l’échelle](cache-how-to-scale.md) sur un cache ou [modifier le nombre de hello de partitions](cache-how-to-premium-clustering.md) si le cache de hello a activé le clustering.
- Vous ne pouvez activer la persistance sur aucun des caches.
- Vous pouvez utiliser [exporter](cache-how-to-import-export-data.md#export) avec un cache, mais vous ne pouvez [importation](cache-how-to-import-export-data.md#import) dans hello principal lié du cache.
- Impossible de supprimer du cache lié, ou groupe de ressources hello qui les contient, jusqu'à la suppression de liens de géo-réplication hello. Pour plus d’informations, consultez [pourquoi hello opération échouer lorsque j’ai essayé toodelete mon cache lié ?](#why-did-the-operation-fail-when-i-tried-to-delete-my-linked-cache)
- Si deux caches de hello sont dans des régions différentes, les frais de sortie réseau appliquera toohello les données répliquées sur cache lié de régions toohello secondaire. Pour plus d’informations, consultez [combien coûte tooreplicate mes données entre les régions Azure ?](#how-much-does-it-cost-to-replicate-my-data-across-azure-regions)
- Aucun basculement automatique toohello secondaire lié cache ne s’arrêtent cache principal de hello (et son réplica). Dans les applications clientes ordre toofailover, vous devez toomanually supprimer le lien géo-réplication hello et point hello client applications toohello de cache qui était auparavant cache lié secondaire de hello. Pour plus d’informations, consultez [comment fonctionne basculement toohello de cache lié secondaire ?](#how-does-failing-over-to-the-secondary-linked-cache-work)

## <a name="add-a-geo-replication-link"></a>Ajouter un lien de géoréplication

1. toolink premium deux caches ensemble pour la géo-réplication, cliquez sur **géoréplication** à partir du menu de ressource hello du cache hello conçu comme hello principal lié mettre en cache, puis cliquez sur **ajouter le lien de réplication du cache**de hello **géo-réplication** panneau.

    ![Ajouter un lien](./media/cache-how-to-geo-replication/cache-geo-location-menu.png)

2. Cliquez sur nom hello de cache secondaire de hello souhaité à partir de hello **caches Compatible** liste. Si votre cache souhaité n’est pas affiché dans la liste de hello, vérifiez que hello [conditions préalables de géo-réplication](#geo-replication-prerequisites) pour hello souhaité de cache secondaire sont remplies. les caches de hello toofilter par région, cliquez sur la région souhaités hello dans toodisplay de carte hello uniquement les caches de hello **caches Compatible** liste.

    ![Caches compatibles avec la géoréplication](./media/cache-how-to-geo-replication/cache-geo-location-select-link.png)
    
    Vous pouvez également initier hello liaison processus ou la vue Détails sur le cache de hello secondaire à l’aide du menu contextuel de hello.

    ![Menu contextuel de la géoréplication](./media/cache-how-to-geo-replication/cache-geo-location-select-link-context-menu.png)

3. Cliquez sur **lien** toolink hello deux caches ensemble et commencer le processus de réplication hello.

    ![Lier des caches](./media/cache-how-to-geo-replication/cache-geo-location-confirm-link.png)

4. Vous pouvez afficher la progression de hello du processus de réplication hello sur hello **géo-réplication** panneau.

    ![État du lien](./media/cache-how-to-geo-replication/cache-geo-location-linking.png)

    Vous pouvez également afficher hello cet état sur hello **vue d’ensemble** panneau pour les deux caches de hello principaux et secondaires.

    ![État du cache](./media/cache-how-to-geo-replication/cache-geo-location-link-status.png)

    Une fois le processus de réplication hello est terminé, hello **lien état** change également**Succeeded**.

    ![État du cache](./media/cache-how-to-geo-replication/cache-geo-location-link-successful.png)

    Pendant le processus de liaison de hello, cache lié de hello principal reste disponible pour une utilisation mais cache lié secondaire de hello n’est pas disponible tant que se termine le processus de liaison de hello.

## <a name="remove-a-geo-replication-link"></a>Supprimer un lien de géoréplication

1. Cliquez sur le lien de hello tooremove entre deux caches et d’arrêter la géo-réplication, **dissocier les caches** de hello **géo-réplication** panneau.
    
    ![Dissocier les caches](./media/cache-how-to-geo-replication/cache-geo-location-unlink.png)

    Lors de la fin du processus de suppression de la liaison de hello, hello secondaire cache disponible pour les opérations de lecture et écrit.

>[!NOTE]
>Lorsque le lien de hello géo-réplication est supprimée, hello des données répliquées à partir du reste du cache lié principaux hello dans le cache secondaire hello.
>
>

## <a name="geo-replication-faq"></a>FAQ concernant la géoréplication

- [Puis-je utiliser la géoréplication avec un cache de niveau Standard ou De base ?](#can-i-use-geo-replication-with-a-standard-or-basic-tier-cache)
- [Mon cache n’est disponible pour utilisation pendant hello liaison ou le processus de suppression de la liaison ?](#is-my-cache-available-for-use-during-the-linking-or-unlinking-process)
- [Puis-je lier plus de deux caches ?](#can-i-link-more-than-two-caches-together)
- [Puis-je lier deux caches d’abonnements Azure différents ?](#can-i-link-two-caches-from-different-azure-subscriptions)
- [Puis-je lier deux caches de tailles différentes ?](#can-i-link-two-caches-with-different-sizes)
- [Puis-je utiliser la géoréplication quand le clustering est activé ?](#can-i-use-geo-replication-with-clustering-enabled)
- [Puis-je utiliser la géoréplication avec mes caches dans un réseau virtuel ?](#can-i-use-geo-replication-with-my-caches-in-a-vnet)
- [Puis-je utiliser PowerShell ou CLI d’Azure toomanage géo-réplication ?](#can-i-use-powershell-or-azure-cli-to-manage-geo-replication)
- [Combien coûte tooreplicate mes données entre les régions Azure ?](#how-much-does-it-cost-to-replicate-my-data-across-azure-regions)
- [Pourquoi les opération hello échouent lorsque je toodelete mon cache lié ?](#why-did-the-operation-fail-when-i-tried-to-delete-my-linked-cache)
- [Quelle région dois-je utiliser pour mon cache lié secondaire ?](#what-region-should-i-use-for-my-secondary-linked-cache)
- [Comment fonctionne le basculement toohello de cache lié secondaire ?](#how-does-failing-over-to-the-secondary-linked-cache-work)

### <a name="can-i-use-geo-replication-with-a-standard-or-basic-tier-cache"></a>Puis-je utiliser la géoréplication avec un cache de niveau Standard ou De base ?

Non, la géoréplication est disponible uniquement pour des caches de niveau Premium.

### <a name="is-my-cache-available-for-use-during-hello-linking-or-unlinking-process"></a>Mon cache n’est disponible pour utilisation pendant hello liaison ou le processus de suppression de la liaison ?

- Lorsque vous liez deux caches ensemble pour la géo-réplication, cache lié de hello principal reste disponible pour une utilisation mais cache lié secondaire de hello n’est pas disponible tant que se termine le processus de liaison de hello.
- Lors de la suppression de lien de hello géo-réplication entre deux caches, les deux caches restent disponibles.

### <a name="can-i-link-more-than-two-caches-together"></a>Puis-je lier plus de deux caches ?

Non, lors de l’utilisation de la géoréplication, vous ne pouvez pas lier plus de deux caches.

### <a name="can-i-link-two-caches-from-different-azure-subscriptions"></a>Puis-je lier deux caches d’abonnements Azure différents ?

Non, les deux caches doivent être Bonjour même abonnement Azure.

### <a name="can-i-link-two-caches-with-different-sizes"></a>Puis-je lier deux caches de tailles différentes ?

Oui, tant que cache de lié secondaire hello est plus grande que hello cache lié principal.

### <a name="can-i-use-geo-replication-with-clustering-enabled"></a>Puis-je utiliser la géoréplication quand le clustering est activé ?

Oui, tant que les deux caches ont hello même nombre de partitions.

### <a name="can-i-use-geo-replication-with-my-caches-in-a-vnet"></a>Puis-je utiliser la géoréplication avec mes caches dans un réseau virtuel ?

Oui, la géoréplication de caches dans des réseaux virtuels est prise en charge. 

- Géo-réplication entre des caches Bonjour que même réseau virtuel est prise en charge.
- Géo-réplication entre des caches dans des réseaux virtuels différents est également prise en charge, tant que hello deux des réseaux virtuels sont configurés de telle sorte que les ressources dans des réseaux virtuels hello sont en mesure de tooreach eux via des connexions TCP.

### <a name="can-i-use-powershell-or-azure-cli-toomanage-geo-replication"></a>Puis-je utiliser PowerShell ou CLI d’Azure toomanage géo-réplication ?

À ce stade, vous ne pouvez gérer à l’aide de géo-réplication hello portail Azure.

### <a name="how-much-does-it-cost-tooreplicate-my-data-across-azure-regions"></a>Combien coûte tooreplicate mes données entre les régions Azure ?

Lorsque vous utilisez la géo-réplication, données du cache de lié principal hello sont répliquée toohello secondaire lié cache. Si hello deux lié les caches sont Bonjour même région Azure, il n’existe aucun frais pour le transfert de données hello. Si hello deux lié sont des caches dans différentes régions Azure, les coûts de bande passante hello de réplication des autres région Azure qui toohello de données sont hello frais de transfert de données de géo-réplication. Pour plus d'informations, consultez [Détails de la tarification de la bande passante](https://azure.microsoft.com/pricing/details/bandwidth/).

### <a name="why-did-hello-operation-fail-when-i-tried-toodelete-my-linked-cache"></a>Pourquoi les opération hello échouent lorsque je toodelete mon cache lié ?

Lorsque deux caches sont liées entre elles, vous ne pouvez supprimer du cache ou hello groupe de ressources qui les contient jusqu'à la suppression de liens de géo-réplication hello. Si vous essayez de groupe de ressources hello toodelete contenant un ou deux hello lié caches, hello autres ressources dans le groupe de ressources hello sont supprimés, mais reste par groupe de ressources hello Bonjour `deleting` état et toute lié caches dans le groupe de ressources hello restent Bonjour `running` état. suppression de hello toocomplete de groupe de ressources hello et hello lié caches qu’il contient, rompre la liaison hello géo-réplication comme décrit dans [supprimer un lien de géo-réplication](#remove-a-geo-replication-link).

### <a name="what-region-should-i-use-for-my-secondary-linked-cache"></a>Quelle région dois-je utiliser pour mon cache lié secondaire ?

En règle générale, il est recommandé pour votre tooexist cache Bonjour même région Azure en tant qu’application hello qui y accède. Si votre application dispose d’une région primaire et d’une région de secours, vos caches principal et secondaire doivent exister dans ces mêmes régions. Pour plus d’informations sur les régions liées, consultez [Meilleures pratiques : régions Azure liées](../best-practices-availability-paired-regions.md).

### <a name="how-does-failing-over-toohello-secondary-linked-cache-work"></a>Comment fonctionne le basculement toohello de cache lié secondaire ?

Dans la version initiale de hello de géo-réplication, le Cache Redis Azure ne prend pas en charge le basculement automatique entre les régions Azure. La géoréplication est utilisée principalement dans un scénario de récupération d’urgence. Dans un scénario de récupération distater, clients doivent afficher pile d’ensemble de l’application hello dans une région de sauvegarde de manière coordonnée plutôt que de laisser les composants d’application individuels à décider quand tooswitch tootheir les sauvegardes sur leurs propres. Cela est particulièrement pertinente tooRedis. Un des avantages clés de hello de Redis est qu’il s’agit d’un magasin de très faible latence. Si Redis est utilisé par une application échoue sur une région Azure différente tooa mais n’est pas le cas de couche de calcul hello, hello ajouté round durée aurait un impact perceptible sur les performances. Pour cette raison, nous aimerions tooavoid Redis défectueuse sur automatiquement en raison de problèmes de disponibilité tootransient.

Actuellement, tooinitiate hello basculement, vous devez tooremove hello géo-réplication lier Bonjour portail Azure, puis modifiez le point de terminaison hello connexion dans le client de Redis hello de base de données secondaire hello cache lié principaux toohello (anciennement lié) cache. Lorsque hello deux caches sont dissociées, réplica de hello devient une expression régulière est en lecture-écriture à nouveau cache et accepte les requêtes directement à partir de clients Redis.


## <a name="next-steps"></a>Étapes suivantes

En savoir plus sur hello [niveau Azure Redis Cache Premium](cache-premium-tier-intro.md).

