---
title: "Maintenance de préservation pour les machines virtuelles Windows dans Azure | Microsoft Docs"
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
ms.openlocfilehash: 8888bafbc3aba24168312b611a9b4fbde25f376d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="vm-preserving-maintenance-with-in-place-vm-migration"></a><span data-ttu-id="51433-103">Maintenance de préservation pour les machines virtuelles Windows dans Azure</span><span class="sxs-lookup"><span data-stu-id="51433-103">VM preserving maintenance with In-place VM migration</span></span>

<span data-ttu-id="51433-104">Bien que la majorité des mises à jour n’aient aucun impact sur les machines virtuelles hébergées, il existe néanmoins des cas où les mises à jour de composants ou de services ont une interférence minimale sur les machines virtuelles en cours d’exécution (sans un redémarrage complet de la machine virtuelle).</span><span class="sxs-lookup"><span data-stu-id="51433-104">While the majority of updates have no impact to hosted VMs, there are cases where updates to components or services result in minimal interference to running VMs (without a full reboot of the virtual machine).</span></span>

<span data-ttu-id="51433-105">Ces mises à jour sont réalisées avec une technologie qui permet la migration dynamique sur place, également appelée « mise à jour avec préservation de la mémoire ».</span><span class="sxs-lookup"><span data-stu-id="51433-105">These updates are accomplished with technology that enables in-place live migration, also called "memory-preserving update".</span></span> <span data-ttu-id="51433-106">Lors de la mise à jour de l’hôte, la machine virtuelle est mise en pause, ce qui préserve la mémoire dans la RAM, pendant que l’environnement d’hébergement (le système d’exploitation hôte sous-jacent) applique les correctifs et les mises à jour nécessaires.</span><span class="sxs-lookup"><span data-stu-id="51433-106">When updating the host, the virtual machine is placed into a “paused” state, preserving the memory in RAM, while the hosting environment (e.g. the underlying operating system) applies the necessary updates and patches.</span></span>
<span data-ttu-id="51433-107">La machine virtuelle reprend alors 30 secondes après avoir été mise en pause.</span><span class="sxs-lookup"><span data-stu-id="51433-107">The virtual machine is then resumed within 30 seconds of being paused.</span></span>
<span data-ttu-id="51433-108">Une fois redémarrée, l’horloge de la machine virtuelle est automatiquement synchronisée.</span><span class="sxs-lookup"><span data-stu-id="51433-108">After resuming, the clock of the virtual machine is automatically synchronized.</span></span>

<span data-ttu-id="51433-109">Les mises à jour ne peuvent pas toutes êtes déployées à l’aide de ce mécanisme, mais étant donné la courte interruption, ce type de déploiement des mises à jour réduit considérablement l’impact sur les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="51433-109">Not all updates can be deployed by using this mechanism, but given the short pause period, deploying updates in this way greatly reduces impact to virtual machines.</span></span>

<span data-ttu-id="51433-110">Les mises à jour multi-instances (machines virtuelles d’un groupe à haute disponibilité) se voient appliquer un seul domaine de mise à jour à la fois.</span><span class="sxs-lookup"><span data-stu-id="51433-110">Multi-instance updates (VMs in an availability set) are applied one update domain at a time.</span></span>

<span data-ttu-id="51433-111">Certaines applications peuvent être affectées plus que d’autres par ces mises à jour.</span><span class="sxs-lookup"><span data-stu-id="51433-111">Some applications may be impacted by these updates more than others.</span></span> <span data-ttu-id="51433-112">Par exemple, les applications qui effectuent des scénarios de traitement d’événements en temps réel, de streaming multimédia, de transcodage multimédia ou de mise en réseau à débit élevé ne peuvent pas être conçues pour tolérer une pause de 30 secondes.</span><span class="sxs-lookup"><span data-stu-id="51433-112">Applications that perform real-time event processing, media streaming or transcoding, or high throughput networking scenarios, for example, may not be designed to tolerate a 30 second pause.</span></span> <span data-ttu-id="51433-113">Les applications qui s’exécutent sur une machine virtuelle peuvent obtenir des informations sur les mises à jour à venir en appelant l’API des [événements planifiés](../virtual-machines-scheduled-events.md) [d’Azure Metadata Service](../virtual-machines-instancemetadataservice-overview.md).</span><span class="sxs-lookup"><span data-stu-id="51433-113">Applications running in a virtual machine can learn about upcoming updates by calling the [Scheduled Events](../virtual-machines-scheduled-events.md) API of the [Azure Metadata Service](../virtual-machines-instancemetadataservice-overview.md).</span></span>
