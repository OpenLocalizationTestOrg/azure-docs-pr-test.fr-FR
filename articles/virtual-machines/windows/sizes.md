---
title: "tailles d’aaaWindows machine virtuelle dans Azure | Documents Microsoft"
description: "Répertorie les tailles disponibles pour les machines virtuelles Windows Azure hello différentes."
services: virtual-machines-windows
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: aabf0d30-04eb-4d34-b44a-69f8bfb84f22
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 80bd8241b134031c41b56224e841c7557c4845cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sizes-for-windows-virtual-machines-in-azure"></a>Tailles des machines virtuelles Windows dans Azure

Cet article décrit les tailles disponibles hello et des options pour hello des machines virtuelles Azure, vous pouvez utiliser toorun vos applications Windows et les charges de travail. Il fournit également des toobe de considérations de déploiement prenant en charge de lorsque vous planifiez toouse ces ressources.  Cet article est également disponible pour les [machines virtuelles Linux](../linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


| Type                     | Tailles           |    Description       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [Usage général](sizes-general.md)          | Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7 | Ratio processeur/mémoire équilibré. Idéal pour le test et développement toomedium petites bases de données et des serveurs web toomedium faible trafic. |
| [Optimisé pour le calcul](sizes-compute.md)        | Fs, F             | Ratio processeur/mémoire élevé. Convient pour les serveurs web au trafic moyen, les appareils réseau, les processus de traitement par lots et les serveurs d’application.        |
| [Mémoire optimisée](../virtual-machines-windows-sizes-memory.md)         | Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D   | Ratio mémoire/processeur élevé. Idéal pour les serveurs de base de données relationnelle, toolarge moyennes caches et en mémoire analytique.                 |
| [Optimisé pour le stockage](../virtual-machines-windows-sizes-storage.md)        | Ls                | Débit de disque et E/S élevés. Idéale pour les bases de données NoSQL, SQL et Big Data.                                                         |
| [GPU](sizes-gpu.md)            | NV, NC            | Machines virtuelles spécialisées conçues pour les opérations graphiques lourdes et la retouche vidéo. Disponible avec un ou plusieurs GPU.       |
| [Calcul haute performance](sizes-hpc.md) | H, A8-11          | Nos machines virtuelles les plus rapides et dotées des processeurs les plus puissants avec interfaces réseau haut débit en option (RDMA). 

<br> 

- Pour plus d’informations sur la tarification de hello de différentes tailles, consultez [tarification des Machines virtuelles](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows). 
- limites de toosee général sur des machines virtuelles Azure, consultez [abonnement Azure et limites de service, quotas et contraintes](../../azure-subscription-service-limits.md).
- Les coûts de stockage sont calculés séparément en fonction des pages utilisées dans le compte de stockage hello. Pour plus d’informations, consultez [Prix appliqués à Azure Storage](https://azure.microsoft.com/pricing/details/storage/).
- Lisez-en davantage sur les [Unités de calcul Azure (ACU)](acu.md) pour découvrir comment comparer les performances de calcul entre les références Azure.



## <a name="rest-api"></a>API REST

Pour des informations sur l’utilisation de tooquery d’API REST hello pour les tailles de machine virtuelle, voir hello :

- [Répertorier les tailles disponibles des machines virtuelles pour le redimensionnement](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing)
- [Répertorier les tailles disponibles des machines virtuelles pour un abonnement](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region)
- [Répertorier les tailles de machine virtuelle disponibles dans un groupe à haute disponibilité](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set)

## <a name="acu"></a>ACU

Lisez-en davantage sur les [Unités de calcul Azure (ACU)](acu.md) pour découvrir comment comparer les performances de calcul entre les références Azure.

## <a name="next-steps"></a>Étapes suivantes

En savoir plus sur hello différentes tailles de machine virtuelle qui sont disponibles :
- [Usage général](sizes-general.md)
- [Optimisé pour le calcul](sizes-compute.md)
- [Mémoire optimisée](../virtual-machines-windows-sizes-memory.md)
- [Optimisé pour le stockage](../virtual-machines-windows-sizes-storage.md)
- [Optimisé pour le GPU](sizes-gpu.md)
- [Calcul haute performance](sizes-hpc.md)



