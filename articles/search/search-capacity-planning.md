---
title: "planification pour Azure Search d’aaaCapacity | Documents Microsoft"
description: "Ajustez les ressources informatiques des partitions et des réplicas dans Recherche Azure, où chaque ressource est facturée en unités de recherche facturables."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 1dc16afe-56f9-439d-8874-1733ae1a2b74
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 02/08/2017
ms.author: heidist
ms.openlocfilehash: 4bbbb929a36b932ea7af12e494ca095d98b9005e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-resource-levels-for-query-and-indexing-workloads-in-azure-search"></a>Mettre à l’échelle les niveaux de ressources pour interroger et indexer les charges de travail dans Azure Search
Après avoir [choisir un niveau de tarification](search-sku-tier.md) et [configurer un service de recherche](search-create-service-portal.md), hello prochaine étape consiste toooptionally augmentation hello différents réplicas ou les partitions utilisées par votre service. Chaque niveau propose un nombre fixe d’unités de facturation. Cet article explique comment tooallocate ces tooachieve unités une configuration optimale qui équilibre vos besoins pour l’exécution des requêtes, l’indexation et de stockage.

Configuration de la ressource est disponible lorsque vous configurez un service à hello [le niveau de base](http://aka.ms/azuresearchbasic) ou l’un des hello [niveaux Standard](search-limits-quotas-capacity.md). Pour les services facturables à ces niveaux, la capacité est achetée par incréments *d’unités de recherche* (SU) où chaque partition et chaque réplica est considéré comme une SU. 

La facture est proportionnelle au nombre de SU : moins elles sont nombreuses, plus la facture diminue. La facturation est appliquée pour tant que service de hello est défini. Si vous utilisez temporairement pas un service, hello seule façon tooavoid facturation est par la suppression du service de hello et puis de les recréer lorsque vous avez besoin.

> [!Note]
> La suppression d’un service a pour effet de supprimer toutes les données qui s’y trouvent. Il n’existe aucune fonctionnalité dans Azure Search permettant de sauvegarder et restaurer les données de recherche persistantes. tooredeploy un index existant sur un nouveau service, vous devez exécuter hello programme utilisé toocreate et à l’origine de la charge. 

## <a name="terminology-partitions-and-replicas"></a>Terminologie : partitions et réplicas
Partitions et réplicas sont des ressources principales hello qui assurent un service de recherche.

| Ressource | Définition |
|----------|------------|
|*Partitions* | Fournissent un stockage des index et des E/S pour les opérations de lecture-écriture (par exemple, lors de la reconstruction ou de l’actualisation d’un index).|
|*Réplicas* | Les instances du service de recherche de hello, utilisées principalement les opérations de requête de solde tooload. Chaque réplica héberge toujours une seule copie d’un index. Si vous avez des 12 réplicas, vous aurez 12 copies de chaque index chargées sur le service de hello.|

> [!NOTE]
> Il n’existe aucun moyen toodirectly manipuler ou gérer les index qui s’exécutent sur un réplica. Une seule copie de chaque index de chaque réplica fait partie de l’architecture de service hello.
>

## <a name="how-tooallocate-partitions-and-replicas"></a>Comment tooallocate les partitions et réplicas
Dans Azure Search, un service se voit initialement allouer un niveau minimal de ressources consistant en une partition et un réplica. Pour les niveaux qui le prennent en charge, vous pouvez ajuster progressivement les ressources de calcul en augmentant les partitions si vous avez besoin de plus de stockage et d’E/S ou de réplicas pour des volumes de requêtes plus importants ou des performances améliorées. Un seul service doit avoir suffisamment toohandle de ressources de toutes les charges de travail (index et des requêtes). Vous ne pouvez pas subdiviser les charges de travail entre plusieurs services.

allocation hello tooincrease ou modifier des réplicas et des partitions, nous vous recommandons d’utiliser hello portail Azure. portail de Hello impose des limites sur les combinaisons autorisées dépasser les limites maximales :

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/) et sélectionnez le service de recherche hello.
2. Dans **paramètres**, ouvrez hello **échelle** lame et utilisez hello curseurs tooincrease ou diminuer le nombre hello de partitions et réplicas.

Si vous avez besoin d’une approche d’approvisionnement basée sur le code ou script, hello [API REST de gestion](https://msdn.microsoft.com/library/azure/dn832687.aspx) est un portail toohello autre.

En règle générale, les applications de recherche nécessitent plus de réplicas que les partitions, en particulier lorsque les opérations de service hello sont en faveur de charges de travail de requête. Hello section sur [haute disponibilité](#HA) explique pourquoi.

> [!NOTE]
> Une fois un service est configuré, il ne peut pas être mis à niveau tooa SKU supérieure. Vous devez toocreate un service de recherche au niveau de nouveau hello et recharger votre index. Consultez [créer un service Azure Search dans le portail de hello](search-create-service-portal.md) pour vous aider à la mise en service.
>
>

<a id="HA"></a>

## <a name="high-availability"></a>Haute disponibilité
Car il est facile et relativement rapide tooscale haut, nous déconseillons généralement que vous démarrez avec une partition et un ou deux réplicas, puis montée en puissance en tant que volumes de requêtes de build. Pour de nombreux services à des niveaux de base ou S1 hello, une partition fournit suffisamment d’e/s et de stockage (à 15 millions de documents par partition).

Les charges de travail de requêtes s’exécutent principalement sur des réplicas. Si vous nécessitez une haute disponibilité ou un débit plus important, vous aurez probablement besoin de réplicas supplémentaires.

Recommandations générales pour la haute disponibilité :

* Deux réplicas pour la haute disponibilité des charges de travail en lecture seule (requêtes)
* Trois réplicas minimum pour la haute disponibilité des charges de travail en lecture/écriture (les requêtes et l’indexation en tant que documents individuels sont ajoutées, mises à jour ou supprimées)

Les contrats de niveau de service (SLA) pour la Recherche Azure sont ciblés au moment des opérations de requête et des mises à jour d’index qui se composent d’ajout, de mise à jour ou de suppression de documents.

### <a name="index-availability-during-a-rebuild"></a>Disponibilité des index lors d’une reconstruction

Haute disponibilité pour Azure Search concernant les mises à jour tooqueries et les index qui n’incluent pas de reconstruction d’un index. Si vous supprimez un champ, modifiez un type de données ou renommez un champ, vous devez les index de hello toorebuild. index de hello toorebuild, vous devez supprimer hello indexer, recréer les index hello et recharger les données hello.

> [!NOTE]
> Vous pouvez ajouter des index Azure Search de nouveaux champs tooan sans reconstruire les index hello. valeur de Hello du nouveau champ de hello sera null pour tous les documents déjà présents dans les index de hello.

disponibilité d’index toomaintain lors d’une reconstruction, doit avoir une copie d’index hello avec un nom différent sur hello même service, ou une copie de hello d’index par hello même nom sur un autre service, puis fournir une logique de redirection ou de basculement dans votre code.

## <a name="disaster-recovery"></a>Récupération d'urgence
Il n'existe actuellement aucun mécanisme intégré de récupération d'urgence. Ajout de partitions ou de réplicas serait stratégie incorrect de hello pour les objectifs de récupération d’urgence. approche la plus courante Hello est tooadd la redondance au niveau de service hello en configurant un deuxième service de recherche dans une autre région. Comme avec la disponibilité pendant une reconstruction d’index, la redirection de hello ou logique de basculement doit provenir de votre code.

## <a name="increase-query-performance-with-replicas"></a>Augmenter les performances des requêtes avec des réplicas
La latence des requêtes vous permet de découvrir si des réplicas supplémentaires doivent être ajoutés. En règle générale, la première étape vers l’amélioration des performances de requête est tooadd plus de cette ressource. Lorsque vous ajoutez des réplicas, des copies supplémentaires de l’index de hello sont mis en ligne toosupport plus grandes requête les charges de travail et hello de solde tooload demande sur hello plusieurs réplicas.

Nous ne pouvons pas fournir des estimations de disque durs sur des requêtes par seconde (QPS) : requête performances dépendent de la complexité de hello de hello de requêtes et de charges de travail concurrents. En moyenne, un réplica au niveau de référence (SKU) De base ou S1 peut traiter environ 15 requêtes par seconde, mais le débit sera supérieur ou inférieur en fonction de la complexité de la requête (les requêtes à facettes sont plus complexes) et de la latence du réseau. En outre, il est important de toorecognize que bien que l’ajout de réplicas augmente indiscutablement l’échelle et performances, hello résultat n’est pas strictement linéaire : ajout de trois réplicas ne garantit pas le triplement du débit.

toolearn sur les requêtes par seconde, y compris les approches d’estimation de requêtes par seconde pour vos charges de travail, consultez [gérer votre service de recherche](search-manage.md).

## <a name="increase-indexing-performance-with-partitions"></a>Améliorer les performances d’indexation avec des partitions
Les applications de recherche nécessitant une actualisation des données en temps réel ou presque ont proportionnellement besoin de plus de partitions que de réplicas. L’ajout de partitions répartit les opérations de lecture/écriture sur un plus grand nombre de ressources de calcul. Il vous offre également davantage d’espace disque pour stocker des documents et des index supplémentaires.

Plus grands index prennent plus de temps tooquery. Par conséquent, peut-être constaterez-vous que chaque augmentation incrémentielle des partitions nécessite une augmentation plus faible mais proportionnelle des réplicas. complexité Hello de vos requêtes et le volume de la requête sera contribuer à la vitesse à laquelle l’exécution des requêtes est activée.

## <a name="basic-tier-partition-and-replica-combinations"></a>Niveau de base : combinaisons de partitions et de réplicas
Un service de base peut avoir une seule partition et de réplicas toothree, pour un maximum de trois SUs. la ressource uniquement réglable Hello est réplicas. Vous devez disposer d’au moins 2 réplicas pour la haute disponibilité sur des requêtes.

<a id="chart"></a>

## <a name="standard-tiers-partition-and-replica-combinations"></a>Niveaux Standard : combinaisons de partitions et de réplicas
Ce tableau montre les combinaisons de toosupport requis hello SUs des réplicas et des partitions, limite de 36-SU toohello sujet, pour tous les niveaux Standard.

|   | **1 partition** | **2 partitions** | **3 partitions** | **4 partitions** | **6 partitions** | **12 partitions** |
| --- | --- | --- | --- | --- | --- | --- |
| **1 réplica** |1 unité de recherche |2 unités de recherche |3 unités de recherche |4 unités de recherche |6 unités de recherche |12 unités de recherche |
| **2 réplicas** |2 unités de recherche |4 unités de recherche |6 unités de recherche |8 unités de recherche |12 unités de recherche |24 unités de recherche |
| **3 réplicas** |3 unités de recherche |6 unités de recherche |9 unités de recherche |12 unités de recherche |18 unités de recherche |36 unités de recherche |
| **4 réplicas** |4 unités de recherche |8 unités de recherche |12 unités de recherche |16 unités de recherche |24 unités de recherche |N/A |
| **5 réplicas** |5 unités de recherche |10 unités de recherche |15 unités de recherche |20 unités de recherche |30 unités de recherche |N/A |
| **6 réplicas** |6 unités de recherche |12 unités de recherche |18 unités de recherche |24 unités de recherche |36 unités de recherche |N/A |
| **12 réplicas** |12 unités de recherche |24 unités de recherche |36 unités de recherche |N/A |N/A |N/A |

SUs, la tarification et la capacité sont expliquées en détail sur hello site Web Azure. Pour plus d'informations, consultez la rubrique [Tarification](https://azure.microsoft.com/pricing/details/search/).

> [!NOTE]
> nombre de Hello des réplicas et des partitions divise uniformément en 12 (plus précisément, 1, 2, 3, 4, 6, 12). Azure Search divise au préalable chaque index en 12 partitions pour que celles-ci puissent être réparties équitablement sur plusieurs partitions. Par exemple, si votre service comporte trois partitions et que vous créez un index, chaque partition contiendra quatre partitions d’index de hello. Comment Azure Search fragmente un index est un détail d’implémentation, objet toochange dans les futures versions. Bien qu’il soit hello 12 aujourd'hui, vous ne doit pas s’attendre que nombre tooalways être 12 Bonjour futures.
>
>

## <a name="billing-formula-for-replica-and-partition-resources"></a>Formule de facturation des ressources de type réplica et partition
formule Hello pour le calcul de SUs combien sont utilisés pour des combinaisons spécifiques est produit hello des réplicas et des partitions, ou (R X P = SU). Par exemple, le produit de trois réplicas par trois partitions est facturé comme neuf SU.

Coût par SU est déterminée par la couche hello, avec un taux de facturation inférieur par unité de base que pour Standard. Consultez la [Tarification](https://azure.microsoft.com/pricing/details/search/)pour connaître les coûts pour chaque niveau.
