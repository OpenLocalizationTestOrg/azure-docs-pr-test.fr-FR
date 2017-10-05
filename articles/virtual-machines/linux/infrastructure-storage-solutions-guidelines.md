---
title: Solutions de stockage pour les machines virtuelles Linux dans Azure | Microsoft Docs
description: "Découvrez-en plus sur les principales instructions de conception et d’implémentation pour le déploiement de solutions de stockage dans des services d’infrastructure Azure."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3c368f07-189b-4520-bbe2-f4080253bbf2
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7c5089b9db945b0e0f4523e53bb44c178ffd0781
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-storage-infrastructure-guidelines-for-linux-vms"></a>Instructions pour les infrastructures Stockage Azure pour machines virtuelles Linux

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

Cet article se concentre sur la compréhension des besoins de stockage et les considérations de conception pour obtenir des performances de machines virtuelles optimales.

## <a name="implementation-guidelines-for-storage"></a>Instructions d’implémentation pour le stockage
Décisions :

* Allez-vous utiliser des disques managés Azure ou des disques non managés ?
* Devez-vous utiliser le stockage Standard ou Premium pour votre charge de travail ?
* Avez-vous besoin d’un entrelacement de disques pour créer des disques d’une taille supérieure à 4 To ?
* Avez-vous besoin d’un entrelacement pour optimiser les performances d’E/S de votre charge de travail ?
* Quel est l’ensemble de comptes de stockage dont vous avez besoin pour héberger votre charge de travail ou votre infrastructure informatique ?

Tâches :

* Passez en revue les demandes d’E/S des applications que vous déployez et planifiez le numéro et le type de compte de stockage.
* Créer l’ensemble de comptes de stockage à l’aide de votre convention d’affectation de noms. Vous pouvez utiliser le portail ou l’interface de ligne de commande Azure.

## <a name="storage"></a>Storage
Azure Storage est un élément essentiel du déploiement et de la gestion des applications et des machines virtuelles. Azure Storage fournit des services pour le stockage des données de fichiers, les données non structurées et les messages. Il fait également partie de l’infrastructure de prise en charge des machines virtuelles.

[Les disques managés Azure](../../storage/storage-managed-disks-overview.md) gèrent le stockage pour vous en arrière-plan. Avec les disques non managés, vous créez des comptes de stockage dédiés à la prise en charge des disques (fichiers de disques durs virtuels) de vos machines virtuelles Azure. Dans le cadre d’une scalabilité verticale, vous devez créer la quantité suffisante de comptes de stockage supplémentaires. Ceci vous évite de dépasser la limite d’E/S associée au stockage de vos disques. Maintenant que votre stockage est géré par Managed Disks, vous n’êtes plus restreint par les limites des comptes de stockage (comme 20 000 E/S par seconde et par compte). Vous n’avez plus à copier vos images personnalisées (fichiers de disques durs virtuels) sur plusieurs comptes de stockage. Vous pouvez les gérer à partir d’un emplacement centralisé (un compte de stockage par région Azure) et les utiliser pour créer des centaines de machines virtuelles dans un abonnement. Nous vous recommandons d’utiliser des disques managés pour les nouveaux déploiements.

Il existe deux types de comptes de stockage disponibles dans pour prendre en charge les machines virtuelles :

* Les comptes de stockage standard vous donnent accès au Stockage Blob (utilisé pour le stockage de disques de machines virtuelles Azure), au Stockage Table, au Stockage File d’attente et au Stockage Fichier.
* [Stockage Premium](../../storage/storage-premium-storage.md) offrent une prise en charge des disques hautes performances à faible latence pour les charges de travail gourmandes en E/S, telles que le cluster partitionné MongoDB. Actuellement, le Stockage Premium prend uniquement en charge les disques de machines virtuelles Azure.

Azure crée des machines virtuelles avec un disque de système d’exploitation, et éventuellement plusieurs disques de données facultatifs. Le disque de système d’exploitation et les disques de données sont des objets blob de pages Azure, tandis que le disque temporaire est stocké localement sur le nœud comprenant l’emplacement de la machine. Lors de la conception d’applications, veillez à utiliser uniquement ce disque temporaire pour des données non persistantes, car la machine virtuelle peut être migrée entre ordinateurs hôtes pendant un événement de maintenance. Toutes les données stockées sur le disque temporaire seraient alors perdues.

La durabilité et la haute disponibilité sont fournies par l’environnement de Stockage Azure sous-jacent afin de garantir que vos données restent protégées contre les défaillances matérielles et les maintenances non planifiées. Lorsque vous concevez votre environnement de stockage Azure, vous pouvez choisir de répliquer le stockage de machines virtuelles :

* en local dans un centre de données Azure donné
* entre centres de données Azure dans une région donnée
* entre centres de données Azure dans des régions différentes.

Vous pouvez lire [plus d’informations sur les options de réplication pour la haute disponibilité](../../storage/storage-introduction.md#replication-for-durability-and-high-availability).

Les disques de système d’exploitation et disques de données ont une taille maximale de 4 To. Vous pouvez utiliser le Gestionnaire de volumes logiques (LVM) pour dépasser cette limite en regroupant des disques de données pour présenter des volumes logiques plus de 1 023 Go à votre machine virtuelle.

Il existe certaines limites d’évolutivité lors de la conception de vos déploiements de Stockage Azure. Consultez [Abonnement Microsoft Azure et limites, quotas et contraintes du service](../../azure-subscription-service-limits.md#storage-limits) pour plus de détails. Voir également [Objectifs de performance et d’extensibilité de Stockage Azure](../../storage/storage-scalability-targets.md).

En ce qui concerne le stockage d’applications, vous pouvez stocker des données d’objets non structurées, comme des documents, des images, des sauvegardes, des données de configuration, des journaux, etc. à l’aide de Stockage Blob. Plutôt que d’écrire sur un disque virtuel connecté à la machine virtuelle, l’application peut écrire directement sur le stockage d’objets blob. Stockage Blob offre également la possibilité de choisir entre [des niveaux de stockage chaud et froid](../../storage/storage-blob-storage-tiers.md) selon vos besoins de disponibilité et vos contraintes de coût.

## <a name="striped-disks"></a>Disques agrégés par bandes
En plus de vous permettre de créer des disques d’une taille supérieure à 1 023 Go dans plusieurs instances, l’entrelacement de disques améliore les performances en permettant à plusieurs objets blob de sauvegarder le stockage d’un seul volume. Avec l’agrégation par bandes, l’E/S requise pour écrire et lire des données à partir d’un seul disque logique est exécutée en parallèle.

Azure impose des limites quant au nombre de disques de données et à la quantité de bande passante disponible, selon la taille de la machine virtuelle. Pour en savoir plus, consultez [Tailles de machines virtuelles](sizes.md).

Si vous utilisez l’entrelacement pour les disques de données Azure, respectez les consignes suivantes :

* Attachez le nombre maximum autorisé de disques de données pour la taille de machine virtuelle.
* Utilisez LVM.
* Évitez d’utiliser des options de mise en cache des disques de données Azure (Stratégie de mise en cache = Aucune).

Pour en savoir plus, consultez la rubrique [Configurer LVM sur une machine virtuelle Linux](configure-lvm.md).

## <a name="multiple-storage-accounts"></a>Comptes de stockage multiples
Cette section ne s’applique pas aux [disques managés Azure](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), étant donné que vous ne créez pas de comptes de stockage distincts. 

Lorsque vous concevez votre environnement Stockage Azure pour les disques non managés, vous pouvez utiliser plusieurs comptes de stockage quand le nombre de machines virtuelles que vous déployez augmente. Cette approche permet de répartir les E/S sur l’infrastructure de Stockage Azure sous-jacente afin de maintenir des performances optimales pour vos machines virtuelles et vos applications. Lorsque vous concevez des applications que vous déployez, prenez en compte les exigences d’E/S de chaque machine virtuelle et équilibrez ces machines virtuelles à travers les comptes de Stockage Azure. Essayez d’éviter de grouper toutes les machines virtuelles gourmandes en E/S sur un ou deux comptes de stockage seulement.

Pour plus d’informations sur les fonctionnalités d’E/S des différentes options de Stockage Azure et des valeurs maximales recommandées, consultez [Objectifs de performance et d’évolutivité du Stockage Azure](../../storage/storage-scalability-targets.md).

## <a name="next-steps"></a>Étapes suivantes
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

