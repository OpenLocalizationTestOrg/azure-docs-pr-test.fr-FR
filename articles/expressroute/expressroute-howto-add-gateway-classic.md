---
title: "Configurer une passerelle de réseau virtuel pour ExpressRoute à l’aide de PowerShell et Azure Classic | Microsoft Docs"
description: "Configurez une passerelle de réseau virtuel pour un réseau virtuel suivant le modèle de déploiement classique avec PowerShell pour une configuration ExpressRoute."
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: 85ee0bc1-55be-4760-bfb4-34d9f2c96f30
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: charwen
ms.openlocfilehash: 195a38fa45f1c514a93980e777fb0d8238aa3f3f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell-classic"></a><span data-ttu-id="01031-103">Configurer une passerelle de réseau virtuel pour ExpressRoute à l’aide de PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="01031-103">Configure a virtual network gateway for ExpressRoute using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="01031-104">Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="01031-104">Resource Manager - PowerShell</span></span>](expressroute-howto-add-gateway-resource-manager.md)
> * [<span data-ttu-id="01031-105">Classic - PowerShell</span><span class="sxs-lookup"><span data-stu-id="01031-105">Classic - PowerShell</span></span>](expressroute-howto-add-gateway-classic.md)
> * [<span data-ttu-id="01031-106">Vidéo - portail Azure</span><span class="sxs-lookup"><span data-stu-id="01031-106">Video - Azure Portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

<span data-ttu-id="01031-107">Cet article vous montrera les étapes nécessaires pour ajouter, redimensionner et supprimer une passerelle de réseau virtuel pour un réseau virtuel existant.</span><span class="sxs-lookup"><span data-stu-id="01031-107">This article will walk you through the steps to add, resize, and remove a virtual network (VNet) gateway for a pre-existing VNet.</span></span> <span data-ttu-id="01031-108">Les étapes de cette configuration sont spécifiquement adaptées aux réseaux virtuels qui ont été créés à l’aide du **modèle de déploiement classique** et qui seront utilisés dans une configuration ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="01031-108">The steps for this configuration are specifically for VNets that were created using the **classic deployment model** and that will be be used in an ExpressRoute configuration.</span></span> 

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="01031-109">**À propos des modèles de déploiement Azure**</span><span class="sxs-lookup"><span data-stu-id="01031-109">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-beginning"></a><span data-ttu-id="01031-110">Avant tout chose</span><span class="sxs-lookup"><span data-stu-id="01031-110">Before beginning</span></span>
<span data-ttu-id="01031-111">Vérifiez que vous avez installé les applets de commande Azure PowerShell nécessaires pour cette configuration (1.0.2 ou ultérieure).</span><span class="sxs-lookup"><span data-stu-id="01031-111">Verify that you have installed the Azure PowerShell cmdlets needed for this configuration (1.0.2 or later).</span></span> <span data-ttu-id="01031-112">Si vous n’avez pas installé les applets de commande, vous devez le faire avant de commencer les étapes de configuration.</span><span class="sxs-lookup"><span data-stu-id="01031-112">If you haven't installed the cmdlets, you'll need to do so before beginning the configuration steps.</span></span> <span data-ttu-id="01031-113">Pour plus d’informations sur l’installation d’Azure PowerShell, consultez la page [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="01031-113">For more information about installing Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [expressroute-gateway-classic-ps](../../includes/expressroute-gateway-classic-ps-include.md)]

## <a name="next-steps"></a><span data-ttu-id="01031-114">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="01031-114">Next steps</span></span>
<span data-ttu-id="01031-115">Une fois que vous avez créé la passerelle de réseau virtuel, vous pouvez lier votre réseau virtuel à un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="01031-115">After you have created the VNet gateway, you can link your VNet to an ExpressRoute circuit.</span></span> <span data-ttu-id="01031-116">Consultez [Liaison d’un réseau virtuel à un circuit ExpressRoute](expressroute-howto-linkvnet-classic.md).</span><span class="sxs-lookup"><span data-stu-id="01031-116">See [Link a Virtual Network to an ExpressRoute circuit](expressroute-howto-linkvnet-classic.md).</span></span>

