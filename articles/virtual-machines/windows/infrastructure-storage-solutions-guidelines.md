---
title: solutions aaaStorage pour les machines virtuelles Windows dans Azure | Documents Microsoft
description: "Découvrez hello clé conception et implémentation des recommandations pour déployer des solutions de stockage dans les services d’infrastructure Azure."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ceb7d32-7a0d-4004-b701-c2bbcaff6b0b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 57c27a7305964a56e6b2d1e73dee8e7da19fa8f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-infrastructure-guidelines-for-windows-vms"></a>Instructions pour les infrastructures Stockage Azure pour machines virtuelles Windows

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

Cet article se concentre sur la compréhension des besoins de stockage et les considérations de conception pour obtenir des performances de machines virtuelles optimales.

## <a name="implementation-guidelines-for-storage"></a>Instructions d’implémentation pour le stockage
Décisions :

* Vous allez toouse disques gérés d’Azure ou des disques non managés ?
* Avez-vous besoin d’un stockage Standard ou Premium de toouse pour votre charge de travail ?
* Avez-vous besoin de disques de toocreate d’agrégation par bandes supérieure à 4 To ?
* Avez-vous besoin des performances optimales d’e/s disque répartition tooachieve pour votre charge de travail ?
* Le jeu de comptes de stockage devez-vous toohost votre charge de travail informatique ou d’infrastructure ?

Tâches :

* Passez en revue les exigences d’e/s des applications hello vous déployez et planifiez le nombre approprié de hello et le type de compte de stockage.
* Créer un jeu hello de comptes de stockage à l’aide de votre convention d’affectation de noms. Vous pouvez utiliser Azure PowerShell ou le portail de hello.

## <a name="storage"></a>Storage
Azure Storage est un élément essentiel du déploiement et de la gestion des applications et des machines virtuelles. Le stockage Azure fournit des services pour le stockage des données de fichier, les données non structurées et les messages, et il fait également partie de l’infrastructure hello prenant en charge des machines virtuelles.

[Les disques Azure géré](../../storage/storage-managed-disks-overview.md) gère le stockage pour vous coulisses hello. Avec des disques non managés, vous créez des comptes de stockage toohold des disques hello (fichiers VHD) pour vos machines virtuelles Azure. Lors de la montée en puissance, il se peut que vous devez vous assurer que vous avez créé des comptes de stockage supplémentaires afin de ne pas dépasser limite d’IOPS hello pour le stockage avec un de vos disques. Avec la gestion du stockage des disques gérés, vous n’êtes n’est plus limité par les limites de compte de stockage hello (tels que 20 000 IOPS / compte). Vous avez également n’est plus toocopy vos comptes de stockage toomultiple des images personnalisées (fichiers VHD). Vous pouvez les gérer dans un emplacement central, un compte de stockage par région Azure et les utiliser toocreate des centaines d’ordinateurs virtuels dans un abonnement. Nous vous recommandons d’utiliser des disques managés pour les nouveaux déploiements.

Il existe deux types de comptes de stockage disponibles dans pour prendre en charge les machines virtuelles :

* Stockage standard comptes vous donnent accès stockage tooblob (utilisé pour le stockage des disques de machine virtuelle Azure), stockage, stockage de file d’attente, de table et un stockage de fichiers.
* [Stockage Premium](../../storage/storage-premium-storage.md) offrent une prise en charge des disques hautes performances à faible latence pour les charges de travail gourmandes en E/S, telles que des serveurs SQL dans un cluster AlwaysOn. Actuellement, le Stockage Premium prend uniquement en charge les disques de machines virtuelles Azure.

Azure crée des machines virtuelles avec un disque de système d’exploitation, et éventuellement plusieurs disques de données facultatifs. disque de système d’exploitation Hello et des disques de données sont des objets BLOB de pages Azure tandis que le disque temporaire de hello est stockée localement sur le nœud hello où se trouve la machine de hello. Prenez soin lors de la conception d’applications tooonly utilisent ce disque temporaire pour les données non persistantes en tant que machine virtuelle peut être migrée entre des ordinateurs hôtes pendant un événement de maintenance de hello. Toutes les données stockées sur le disque temporaire de hello seraient perdues.

La durabilité et la haute disponibilité est fournie par hello sous-jacent Azure Storage environnement tooensure que vos données restent protégées contre les défaillances non planifiées de maintenance ou de matériel. Lorsque vous concevez votre environnement de stockage Azure, vous pouvez choisir le stockage de machine virtuelle tooreplicate :

* en local dans un centre de données Azure donné
* entre centres de données Azure dans une région donnée
* entre centres de données Azure dans des régions différentes

Vous pouvez lire [plus d’informations sur les options de réplication hello pour la haute disponibilité](../../storage/storage-introduction.md#replication-for-durability-and-high-availability).

Les disques de système d’exploitation et disques de données ont une taille maximale de 4 To. Vous pouvez utiliser des espaces de stockage dans Windows Server 2012 ou version ultérieure toosurpass cette limite en regroupant les disques toopresent logique des volumes de données supérieure à 4 To tooyour machine virtuelle.

Il existe certaines limites d’évolutivité lors de la conception de vos déploiements de Stockage Azure. Consultez [Abonnement Microsoft Azure et limites, quotas et contraintes du service](../../azure-subscription-service-limits.md#storage-limits) pour plus de détails. Voir également [Objectifs de performance et d’extensibilité de Stockage Azure](../../storage/storage-scalability-targets.md).

En ce qui concerne le stockage d’applications, vous pouvez stocker des données d’objets non structurées, comme des documents, des images, des sauvegardes, des données de configuration, des journaux, etc. à l’aide de Stockage Blob. Au lieu de votre application, l’écriture tooa disque virtuel attaché toohello VM, application hello permettre écrire directement tooAzure stockage d’objets blob. Stockage d’objets BLOB fournit également l’option hello de [à chaud et refroidir des niveaux de stockage](../../storage/storage-blob-storage-tiers.md) selon vos besoins de disponibilité et les contraintes liées au coût.

## <a name="striped-disks"></a>Disques agrégés par bandes
En plus de vous toocreate disques supérieure à 4 To, dans de nombreux cas, à l’aide de la répartition des disques de données améliore les performances en permettant à plusieurs objets BLOB de stockage de hello tooback pour un volume unique. L’agrégation par bandes, hello d’e/s requis toowrite et les données lues à partir d’un seul disque logique se déroule en parallèle.

Azure impose des limites de nombre de hello de disques de données et de la quantité de bande passante disponible, en fonction de la taille de machine virtuelle hello. Pour en savoir plus, voir la rubrique [Tailles de machines virtuelles](sizes.md).

Si vous utilisez l’entrelacement de disques de données Azure, tenez compte des hello instructions :

* Attachez les disques de données maximale hello autorisés pour hello taille de machine virtuelle.
* Utilisez les espaces de stockage.
* Évitez d’utiliser des options de mise en cache des disques de données Azure (Stratégie de mise en cache = Aucune).

Pour plus d’informations, voir la page [Espaces de stockage : une conception pour la performance](http://social.technet.microsoft.com/wiki/contents/articles/15200.storage-spaces-designing-for-performance.aspx).

## <a name="multiple-storage-accounts"></a>Comptes de stockage multiples
Cette section ne s’applique pas trop[disques gérés d’Azure](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), comme vous ne créez pas de comptes de stockage distinct. 

Lorsque vous concevez votre environnement de stockage Azure pour les disques non managés, vous pouvez utiliser plusieurs comptes de stockage en tant que nombre hello d’ordinateurs virtuels, vous déployez augmente. Cette approche permet de distribuer des hello d’e/s entre hello sous-jacent Azure Storage infrastructure toomaintain des performances optimales pour vos machines virtuelles et les applications. Conception hello les applications que vous déployez, tenez compte des exigences d’e/s de hello que chaque machine virtuelle a et équilibrer les machines virtuelles sur les comptes de stockage Azure. Essayez tooavoid regroupant tous les hello élevé d’e/s en exigeant des machines virtuelles dans des comptes de stockage toojust un ou deux.

Pour plus d’informations sur les fonctions hello d’e/s de différentes options de stockage Azure hello et certains recommandent des valeurs maximales, consultez [cibles de l’évolutivité et les performances de stockage Azure](../../storage/storage-scalability-targets.md).

## <a name="next-steps"></a>Étapes suivantes
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

