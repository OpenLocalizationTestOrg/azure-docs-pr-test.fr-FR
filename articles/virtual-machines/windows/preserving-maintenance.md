---
title: maintenance de conservation de machine virtuelle AAA pour les machines virtuelles Windows dans Azure | Documents Microsoft
description: "Migration sur place de machines virtuelles pour la préservation des mises à jour en mémoire."
services: virtual-machines-windows
documentationcenter: 
author: zivr
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: zivr
ms.openlocfilehash: b798f0afd9d8dc60ca8a78f7cc77435a0ddc76fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="vm-preserving-maintenance-with-in-place-vm-migration"></a><span data-ttu-id="ffa62-103">Maintenance de préservation pour les machines virtuelles Windows dans Azure</span><span class="sxs-lookup"><span data-stu-id="ffa62-103">VM preserving maintenance with In-place VM migration</span></span>

<span data-ttu-id="ffa62-104">Majorité hello des mises à jour ont aucun toohosted impact sur les machines virtuelles, il existe lorsque toocomponents de mises à jour ou de services conduisent interférence minimale toorunning machines virtuelles (sans redémarrage complet de l’ordinateur virtuel de hello).</span><span class="sxs-lookup"><span data-stu-id="ffa62-104">While hello majority of updates have no impact toohosted VMs, there are cases where updates toocomponents or services result in minimal interference toorunning VMs (without a full reboot of hello virtual machine).</span></span>

<span data-ttu-id="ffa62-105">Ces mises à jour sont réalisées avec une technologie qui permet la migration dynamique sur place, également appelée « mise à jour avec préservation de la mémoire ».</span><span class="sxs-lookup"><span data-stu-id="ffa62-105">These updates are accomplished with technology that enables in-place live migration, also called "memory-preserving update".</span></span> <span data-ttu-id="ffa62-106">Lors de la mise à jour d’hôte de hello, ordinateur virtuel de hello est placé dans un état « suspendu », en conservant mémoire hello dans la mémoire RAM, tandis que hello hébergeant l’environnement (par exemple, le système d’exploitation sous-jacent) applique les correctifs et mises à jour nécessaires de hello.</span><span class="sxs-lookup"><span data-stu-id="ffa62-106">When updating hello host, hello virtual machine is placed into a “paused” state, preserving hello memory in RAM, while hello hosting environment (e.g. the underlying operating system) applies hello necessary updates and patches.</span></span>
<span data-ttu-id="ffa62-107">Hello ordinateur virtuel est ensuite redémarré dans les 30 secondes en pause.</span><span class="sxs-lookup"><span data-stu-id="ffa62-107">hello virtual machine is then resumed within 30 seconds of being paused.</span></span>
<span data-ttu-id="ffa62-108">Après la reprise, l’horloge de l’ordinateur virtuel de hello hello est automatiquement synchronisé.</span><span class="sxs-lookup"><span data-stu-id="ffa62-108">After resuming, hello clock of hello virtual machine is automatically synchronized.</span></span>

<span data-ttu-id="ffa62-109">Pas toutes les mises à jour peuvent être déployés à l’aide de ce mécanisme, mais le délai court instant, déploiement des mises à jour de cette façon considérablement réduit les ordinateurs toovirtual impact.</span><span class="sxs-lookup"><span data-stu-id="ffa62-109">Not all updates can be deployed by using this mechanism, but given the short pause period, deploying updates in this way greatly reduces impact toovirtual machines.</span></span>

<span data-ttu-id="ffa62-110">Les mises à jour multi-instances (machines virtuelles d’un groupe à haute disponibilité) se voient appliquer un seul domaine de mise à jour à la fois.</span><span class="sxs-lookup"><span data-stu-id="ffa62-110">Multi-instance updates (VMs in an availability set) are applied one update domain at a time.</span></span>

<span data-ttu-id="ffa62-111">Certaines applications peuvent être affectées plus que d’autres par ces mises à jour.</span><span class="sxs-lookup"><span data-stu-id="ffa62-111">Some applications may be impacted by these updates more than others.</span></span> <span data-ttu-id="ffa62-112">Les applications qui effectuent le traitement des événements en temps réel, diffusion multimédia en continu ou le transcodage ou un débit élevé, les scénarios de mise en réseau, par exemple, peut-être pas tootolerate conçu une pause deuxième 30.</span><span class="sxs-lookup"><span data-stu-id="ffa62-112">Applications that perform real-time event processing, media streaming or transcoding, or high throughput networking scenarios, for example, may not be designed tootolerate a 30 second pause.</span></span> <span data-ttu-id="ffa62-113">Applications qui s’exécutent sur une machine virtuelle peuvent en savoir plus sur les mises à jour à venir en appelant hello [événements planifiés](../virtual-machines-scheduled-events.md) API Hello [Service de métadonnées Azure](../virtual-machines-instancemetadataservice-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ffa62-113">Applications running in a virtual machine can learn about upcoming updates by calling hello [Scheduled Events](../virtual-machines-scheduled-events.md) API of hello [Azure Metadata Service](../virtual-machines-instancemetadataservice-overview.md).</span></span>
