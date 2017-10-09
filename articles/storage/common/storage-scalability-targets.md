---
title: "aaaAzure stockage objectifs d’évolutivité et performances | Documents Microsoft"
description: "En savoir plus sur les cibles de performances et évolutivité hello pour le stockage Azure, y compris la capacité, la fréquence de demande et la bande passante entrante et sortante pour les deux comptes de stockage standard et premium. Comprendre les objectifs de performances pour les partitions dans chacun des services de stockage Azure hello."
services: storage
documentationcenter: na
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: be721bd3-159f-40a1-88c1-96418537fe75
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 07/12/2017
ms.author: robinsh
ms.openlocfilehash: 7afe4366a02887b4e3d9781c26c8adda81adce95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-scalability-and-performance-targets"></a>Objectifs de performance et évolutivité d'Azure Storage
## <a name="overview"></a>Vue d'ensemble
Cette rubrique décrit les rubriques d’évolutivité et de performances hello pour le stockage Microsoft Azure. Pour prendre connaissance des autres informations relatives aux limites Azure, consultez [Limites, quotas et contraintes applicables aux services et abonnements Azure](../../azure-subscription-service-limits.md).

> [!NOTE]
> Tous les comptes de stockage s’exécutent sur une nouvelle topologie de réseau plat hello et prend en charge hello évolutivité et performances expliqués ci-après, quel que soit le moment de leur création. Pour plus d’informations sur l’architecture de réseau plat Azure Storage hello et son évolutivité, consultez [Microsoft Azure Storage : A hautement disponible Service de stockage Cloud à forte cohérence](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx).
> 
> [!IMPORTANT]
> cibles d’évolutivité et de performances Hello répertoriés ici sont des objectifs haut de gamme, mais sont réalisables. Dans tous les cas, demande hello vitesse et la bande passante atteints par votre compte de stockage dépend de la taille de hello des objets stockés, les modèles d’accès hello utilisées et hello des charges de travail de que votre application effectue. Être tootest que votre service toodetermine si ses performances répondent à vos besoins. Si possible, éviter des pics soudains dans taux hello de trafic et assurez-vous que le trafic est bien réparti sur plusieurs partitions.
> 
> Lorsque votre application atteint la limite de hello de ce que peut gérer une partition pour votre charge de travail, le stockage Azure commencera tooreturn code d’erreur 503 (serveur occupé) ou le code d’erreur 500 réponses (délai d’expiration de l’opération). Lorsque cela se produit, application hello doit utiliser une stratégie d’interruption exponentielle des nouvelles tentatives. exponentiel Hello permet charge hello sur hello partition toodecrease et tooease les pics de partition toothat de trafic.
> 
> 

Si hello a besoin de votre application dépassent les objectifs d’évolutivité hello d’un seul compte de stockage, vous pouvez générer votre application toouse plusieurs comptes de stockage et vos objets de données de partition sur les comptes de stockage. Pour plus d’informations sur la tarification des licences en volume, consultez la page [Prix appliqués à Azure Storage](https://azure.microsoft.com/pricing/details/storage/) .

## <a name="scalability-targets-for-blobs-queues-tables-and-files"></a>Objectifs d'évolutivité pour les objets Blob, les files d'attente, les tables et les fichiers
[!INCLUDE [azure-storage-limits](../../../includes/azure-storage-limits.md)]

<!-- conceptual info about disk limits -- applies toounmanaged and managed -->
## <a name="scalability-targets-for-virtual-machine-disks"></a>Objectifs d'évolutivité pour les disques de machines virtuelles
[!INCLUDE [azure-storage-limits-vm-disks](../../../includes/azure-storage-limits-vm-disks.md)]

Pour plus d’informations, consultez la page [Tailles des machine virtuelles dans Azure (Windows)](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ou [Tailles des machines virtuelles dans Azure (Linux)](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="managed-virtual-machine-disks"></a>Disques de machines virtuelles gérées

[!INCLUDE [azure-storage-limits-vm-disks-managed](../../../includes/azure-storage-limits-vm-disks-managed.md)]

## <a name="unmanaged-virtual-machine-disks"></a>Disques de machines virtuelles non gérées
[!INCLUDE [azure-storage-limits-vm-disks-standard](../../../includes/azure-storage-limits-vm-disks-standard.md)]

[!INCLUDE [azure-storage-limits-vm-disks-premium](../../../includes/azure-storage-limits-vm-disks-premium.md)]

## <a name="scalability-targets-for-azure-resource-manager"></a>Objectifs d'évolutivité pour Azure Resource Manager
[!INCLUDE [azure-storage-limits-azure-resource-manager](../../../includes/azure-storage-limits-azure-resource-manager.md)]

## <a name="partitions-in-azure-storage"></a>Partitions dans Azure Storage
Chaque objet qui conserve les données qui sont stockées dans le stockage Azure (objets BLOB, les messages, entités et fichiers) appartient tooa partition et est identifiée par une clé de partition. partition de Hello détermine comment le stockage Azure équilibre la charge de fichiers, les messages, les entités et les objets BLOB entre les besoins de trafic serveurs toomeet hello de ces objets. clé de partition Hello est unique et est utilisé toolocate un objet blob, un message ou une entité.

tableau Hello dans [objectifs d’évolutivité pour les comptes de stockage Standard](#standard-storage-accounts) listes hello objectifs de performances d’une seule partition pour chaque service.

Partitions affectent l’évolutivité et l’équilibrage de charge pour chacun des services de stockage hello Bonjour suivant façons :

* **Objets BLOB**: clé de partition hello pour un objet blob est le nom du compte, nom de conteneur + nom d’objet blob. Cela signifie que chaque objet blob peut avoir sa propre partition si elle demande une charge sur l’objet blob de hello. Objets BLOB permettre être répartis sur plusieurs serveurs dans tooscale de commande out toothem d’accès, mais un seul objet blob ne peut être servi que par un seul serveur. Si les blobs peuvent être regroupés de manière logique dans des conteneurs, ce regroupement n’a aucune incidence sur le partitionnement.
* **Fichiers**: clé de partition hello pour un fichier est le nom + fichier partage le nom de compte. Cela signifie que tous les fichiers dans un partage de fichiers sont également dans une seule partition.
* **Messages**: clé de partition hello d’un message étant nom de compte hello + nom de la file d’attente, tous les messages dans une file d’attente sont regroupées en une seule partition et servis par un seul serveur. Différentes files d’attente peuvent être traités par les différents serveurs toobalance hello charger pour mais peut-être de files d’attente un compte de stockage.
* **Entités**: clé de partition hello pour une entité est le nom du compte + nom de la table + clé de partition, où la clé de partition hello est valeur hello hello requis-défini par l’utilisateur **PartitionKey** propriété d’entité de hello. Serveur de partition de toutes les entités avec la même valeur de clé de partition sont regroupées en hello de partition et servis par hello même de hello. Il s’agit d’un toounderstand point important dans la conception de votre application. Votre application doit équilibrer les avantages de l’évolutivité hello de propagation des entités sur plusieurs partitions avec hello données accès aux avantages du regroupement des entités dans une seule partition.  

Des avantages clés toogrouping qu'un jeu d’entités dans une table en une seule partition est qu’il s’agit des opérations par lots atomiques de tooperform possible entre les entités Bonjour même partition, car une partition existe sur un serveur unique. Par conséquent, si vous le souhaitez tooperform opérations par lots sur un groupe d’entités, envisagez de les regrouper par hello même clé de partition. 

Sur hello autre part, les entités qui se trouvent dans la même table mais que vous avez différentes clés de partition de hello peuvent être équilibrée entre différents serveurs, rendant possible toohave une plus grande évolutivité.

Des recommandations détaillées pour la conception d’une stratégie de partitionnement pour des tables sont disponibles [ici](https://msdn.microsoft.com/library/azure/hh508997.aspx).

## <a name="see-also"></a>Voir aussi
* [Tarification Azure Storage](https://azure.microsoft.com/pricing/details/storage/)
* [Abonnement Azure et limites, quotas et contraintes du service](../../azure-subscription-service-limits.md)
* [Stockage Premium : stockage hautes performances pour les charges de travail des machines virtuelles Azure.](../storage-premium-storage.md)
* [Réplication Azure Storage](../storage-redundancy.md)
* [Liste de contrôle des performances et de l’évolutivité de Microsoft Azure Storage](../storage-performance-checklist.md)
* [Microsoft Azure Storage : service de stockage sur le cloud à haute disponibilité et à cohérence forte](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)

