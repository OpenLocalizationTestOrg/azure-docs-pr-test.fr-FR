---
title: "aaaAvailability définit pour les machines virtuelles Windows classiques | Documents Microsoft"
description: "Configurer un groupe à haute disponibilité pour un ordinateur virtuel Windows existant ou nouveau modèle de déploiement classique de hello à l’aide de hello portail Azure et Azure PowerShell."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: c3b7fdec-fb59-4412-a4f4-f3a0b9c62e93
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: cynthn
ms.openlocfilehash: bd652a0401a34b57447551204b8f50d106715e1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-an-availability-set-for-windows-virtual-machines-in-hello-classic-deployment-model"></a><span data-ttu-id="f7c0a-103">Comment tooconfigure un ensemble de disponibilité pour les machines virtuelles Windows dans le modèle de déploiement classique de hello</span><span class="sxs-lookup"><span data-stu-id="f7c0a-103">How tooconfigure an availability set for Windows virtual machines in hello classic deployment model</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="f7c0a-104">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f7c0a-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f7c0a-105">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="f7c0a-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="f7c0a-106">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="f7c0a-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="f7c0a-107">Vous pouvez également [configurer des groupes à haute disponibilité](../tutorial-availability-sets.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) dans des déploiements Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f7c0a-107">You can also [configure availability sets](../tutorial-availability-sets.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in Resource Manager deployments.</span></span>

[!INCLUDE [virtual-machines-common-classic-configure-availability](../../../../includes/virtual-machines-common-classic-configure-availability.md)]

