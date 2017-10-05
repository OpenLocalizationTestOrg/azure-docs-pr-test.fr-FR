---
title: "Étude technique approfondie de la migration prise en charge par la plateforme de ressources Classic vers Azure Resource Manager | Microsoft Docs"
description: "Cet article présente une étude technique approfondie de la migration de ressources prise en charge par la plateforme de l’environnement Classic vers Azure Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 1ee40d32-a5e8-42a2-97d0-3232fd3cbb98
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: 4898998fe27c48bab4dee3dbaed5a174e23dc83a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="technical-deep-dive-on-platform-supported-migration-from-classic-to-azure-resource-manager"></a><span data-ttu-id="61028-103">Étude technique approfondie de la migration prise en charge par la plateforme de ressources Classic vers Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="61028-103">Technical deep dive on platform-supported migration from classic to Azure Resource Manager</span></span>
<span data-ttu-id="61028-104">Examinons en détail la migration à partir du modèle de déploiement Azure classique vers le modèle de déploiement Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="61028-104">Let's take a deep-dive on migrating from the Azure classic deployment model to the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="61028-105">Nous examinons les ressources au niveau des fonctionnalités et des ressources pour vous aider à comprendre comment la plateforme Azure migre les ressources entre les deux modèles de déploiement.</span><span class="sxs-lookup"><span data-stu-id="61028-105">We look at resources at a resource and feature level to help you understand how the Azure platform migrates resources between the two deployment models.</span></span> <span data-ttu-id="61028-106">Pour en savoir plus, consultez l’article d’annonce de service [Migration prise en charge par la plateforme de ressources IaaS Classic vers Azure Resource Manager](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="61028-106">For more information, please read the service announcement article: [Platform-supported migration of IaaS resources from classic to Azure Resource Manager](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-migration-deep-dive](../../../includes/virtual-machines-common-classic-resource-manager-migration-deep-dive.md)]

## <a name="next-steps"></a><span data-ttu-id="61028-107">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="61028-107">Next steps</span></span>

* [<span data-ttu-id="61028-108">Vue d’ensemble de la migration prise en charge par la plateforme de ressources IaaS Classic vers Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="61028-108">Overview of platform-supported migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="61028-109">Planification de la migration des ressources IaaS d’Azure Classic vers Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="61028-109">Planning for migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="61028-110">Faire migrer des ressources IaaS Classic vers Azure Resource Manager à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="61028-110">Use PowerShell to migrate IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="61028-111">Faire migrer des ressources IaaS Classic vers Azure Resource Manager à l’aide de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="61028-111">Use CLI to migrate IaaS resources from classic to Azure Resource Manager</span></span>](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="61028-112">Outils de la communauté pour aider à la migration de ressources IaaS de Classic vers Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="61028-112">Community tools for assisting with migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="61028-113">Passer en revue les erreurs courantes de migration</span><span class="sxs-lookup"><span data-stu-id="61028-113">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="61028-114">Passez en revue les questions fréquemment posées sur la migration des ressources IaaS de Classic vers Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="61028-114">Review the most frequently asked questions about migrating IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
