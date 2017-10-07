---
title: "aaaAvailability définit pour les machines virtuelles Linux dans Azure | Documents Microsoft"
description: "Découvrez hello clé conception et implémentation des recommandations pour le déploiement de haute disponibilité dans les services d’infrastructure Azure."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 24f1d91c-8cc0-4251-bb67-ac4c4c37e8cd
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 78e4da5c8fd9eb186cafacb46454444b73a9439c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-availability-sets-guidelines-for-linux-vms"></a>Instructions pour les groupes à haute disponibilité Azure pour les machines virtuelles Linux

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

Cet article se concentre sur hello compréhension requis étapes de planification pour la haute disponibilité tooensure vos applications reste accessible pendant les événements planifiés ou non.

## <a name="implementation-guidelines-for-availability-sets"></a>Instructions d’implémentation pour groupes à haute disponibilité
Décisions :

* Groupes à haute disponibilité Combien avez-vous besoin pour hello différents niveaux et les rôles dans votre infrastructure d’application ?

Tâches :

* Définir le nombre hello d’ordinateurs virtuels dans chaque couche d’application que vous avez besoin.
* Déterminez si vous devez tooadjust hello de panne ou mise à jour toobe domaines utilisé pour votre application.
* Définir hello requis à haute disponibilité à l’aide de votre convention d’affectation de noms et les machines virtuelles se trouvent dans les. Une machine virtuelle ne peut résider que dans un seul groupe à haute disponibilité. 

## <a name="availability-sets"></a>Groupes à haute disponibilité
Dans Azure, les machines virtuelles (VM) peut être placées dans un regroupement logique de tooa appelé un ensemble de disponibilité. Lorsque vous créez des machines virtuelles au sein d’un ensemble de disponibilité, hello plateforme Azure répartit la sélection élective hello de ces ordinateurs virtuels sur hello sous-jacent d’infrastructure. Il convient un toohello d’événement de maintenance planifiée plateforme Azure ou d’un matériel sous-jacent / erreur d’infrastructure, utilisez hello de haute disponibilité garantit qu’au moins une machine virtuelle reste en cours d’exécution.

En tant que meilleure pratique, les applications ne doivent pas résider sur une seule machine virtuelle. Un ensemble de disponibilité qui contient une seule machine virtuelle ne prendre aucune protection contre les événements planifiés ou au sein de hello plateforme Azure. Hello [contrat SLA Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines) requiert deux ou plusieurs des ordinateurs virtuels au sein d’une disponibilité ensemble tooallow hello distribution des machines virtuelles entre hello sous-jacent d’infrastructure. Si vous utilisez [stockage Azure Premium](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), hello contrat SLA Azure s’applique tooa unique machine virtuelle.

infrastructure sous-jacente de Hello dans Azure est divisé en clusters matériels de toomultiple. Chaque cluster de matériel peut prendre en charge une plage de tailles de machine virtuelle. Un groupe à haute disponibilité ne peut être hébergé que sur un seul cluster de matériel à la fois. Par conséquent, hello plage de tailles de machine virtuelle qui peuvent exister dans un ensemble de disponibilité unique est limité toohello plage de tailles de machine virtuelle pris en charge par cluster de matériel hello. cluster de matériel Hello pour hello à haute disponibilité est sélectionné lorsque hello première machine virtuelle dans le groupe à haute disponibilité hello est déployé ou lorsque le démarrage hello première machine virtuelle dans un ensemble de disponibilité où tous les ordinateurs virtuels sont actuellement en état arrêté désalloué de hello. Hello CLI commande suivante peut être utilisé toodetermine hello plage de machine virtuelle tailles disponibles pour un ensemble de disponibilité : « az liste-tailles de machine virtuelle--emplacement \<chaîne\>»

Chaque cluster matériel est divisée dans les domaines de mise à jour toomultiple et les domaines d’erreur. Ces domaines sont définis par les hôtes qui partagent un cycle de mise à jour commun, ou une infrastructure physique similaire, comme l’alimentation ou la mise en réseau. Azure distribue automatiquement vos machines virtuelles au sein d’un groupe à haute disponibilité sur la disponibilité de toomaintain de domaines et la tolérance de panne. Selon la taille de hello de votre application et le nombre de hello d’ordinateurs virtuels au sein d’un ensemble de disponibilité, vous pouvez ajuster le nombre de hello des domaines, vous souhaitez toouse. Vous pouvez en savoir plus sur [la gestion de la disponibilité et l’utilisation des domaines d’erreur et de mise à jour](manage-availability.md).

Lorsque vous concevez votre infrastructure d’application, planifiez toouse de niveaux d’application hello. Machines virtuelles de groupe qui font Office de hello même objectif dans les jeux de tooavailability, par exemple un groupe à haute disponibilité pour les machines virtuelles votre frontales en cours d’exécution nginx ou Apache. Créez un groupe à haute disponibilité distinct pour les machines virtuelles principales tournant sous MongoDB ou MySQL. Hello vise tooensure que chaque composant de votre application est protégé par un ensemble de disponibilité et au moins une fois instance reste toujours en cours d’exécution.

Équilibreurs de charge peuvent être utilisés devant chaque toowork de la couche application en même temps que la haute disponibilité et assurez-vous que le trafic peut toujours être routé tooa instance en cours d’exécution. Sans un équilibreur de charge, vos machines virtuelles peuvent continuer à s’exécuter dans l’ensemble des événements de maintenance planifiées et non planifiées, mais l’utilisateur final n’est peut-être pas en mesure de tooresolve les si hello d’ordinateurs virtuels principal n’est pas disponible.

Concevez votre application à des fins de haute disponibilité au niveau de la couche de stockage. Il est recommandé de Hello est trop[utiliser des disques gérés pour les machines virtuelles dans un ensemble de disponibilité](manage-availability.md#use-managed-disks-for-vms-in-an-availability-set). Si vous utilisez actuellement des disques non managées, nous recommandons vivement que vous trop[convertir des machines virtuelles dans le groupe à haute disponibilité des disques gérés toouse](convert-unmanaged-to-managed-disks.md#convert-vms-in-an-availability-set).

## <a name="next-steps"></a>Étapes suivantes
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

