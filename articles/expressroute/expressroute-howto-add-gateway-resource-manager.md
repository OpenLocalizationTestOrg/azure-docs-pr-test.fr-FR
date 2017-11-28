---
title: "Ajouter une passerelle de réseau virtuel à un réseau virtuel pour ExpressRoute avec PowerShell et Azure | Microsoft Docs"
description: "Cet article vous explique comment ajouter une passerelle de réseau virtuel à un réseau virtuel Resource Manager déjà créé pour ExpressRoute."
documentationcenter: na
services: expressroute
author: charwen
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 63e0bd60-abad-4963-8e27-3aa973e0d968
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/17/2017
ms.author: charwen
ms.openlocfilehash: 3aeddd03e0be548933775164ae790ba208fc13ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell"></a><span data-ttu-id="ea80a-103">Configurer une passerelle de réseau virtuel pour ExpressRoute à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="ea80a-103">Configure a virtual network gateway for ExpressRoute using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ea80a-104">Resource Manager - Portail Azure</span><span class="sxs-lookup"><span data-stu-id="ea80a-104">Resource Manager - Azure portal</span></span>](expressroute-howto-add-gateway-portal-resource-manager.md)
> * [<span data-ttu-id="ea80a-105">Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="ea80a-105">Resource Manager - PowerShell</span></span>](expressroute-howto-add-gateway-resource-manager.md)
> * [<span data-ttu-id="ea80a-106">Classic - PowerShell</span><span class="sxs-lookup"><span data-stu-id="ea80a-106">Classic - PowerShell</span></span>](expressroute-howto-add-gateway-classic.md)
> * [<span data-ttu-id="ea80a-107">Vidéo - portail Azure</span><span class="sxs-lookup"><span data-stu-id="ea80a-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

<span data-ttu-id="ea80a-108">Cet article vous montre les étapes nécessaires pour ajouter, redimensionner et supprimer une passerelle de réseau virtuel pour un réseau virtuel existant.</span><span class="sxs-lookup"><span data-stu-id="ea80a-108">This article walks you through the steps to add, resize, and remove a virtual network (VNet) gateway for a pre-existing VNet.</span></span> <span data-ttu-id="ea80a-109">Les étapes de cette configuration sont spécifiquement adaptées aux réseaux virtuels qui ont été créés à l’aide du modèle de déploiement Resource Manager qui sera utilisé dans une configuration ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ea80a-109">The steps for this configuration are specifically for VNets that were created using the Resource Manager deployment model that will be used in an ExpressRoute configuration.</span></span> <span data-ttu-id="ea80a-110">Pour plus d’informations sur les passerelles de réseau virtuel et les paramètres de configuration de passerelle pour ExpressRoute, consultez [À propos des passerelles de réseau virtuel pour ExpressRoute](expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="ea80a-110">For more information about virtual network gateways and gateway configuration settings for ExpressRoute, see [About virtual network gateways for ExpressRoute](expressroute-about-virtual-network-gateways.md).</span></span> 


## <a name="before-beginning"></a><span data-ttu-id="ea80a-111">Avant tout chose</span><span class="sxs-lookup"><span data-stu-id="ea80a-111">Before beginning</span></span>
<span data-ttu-id="ea80a-112">Assurez-vous que vous avez installé les dernières applets de commande Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ea80a-112">Verify that you have installed the latest Azure PowerShell cmdlets.</span></span> <span data-ttu-id="ea80a-113">Si vous n’avez pas installé les dernières applets de commande, vous devez le faire avant de commencer les étapes de configuration.</span><span class="sxs-lookup"><span data-stu-id="ea80a-113">If you haven't installed the latest cmdlets, you need to do so before beginning the configuration steps.</span></span> <span data-ttu-id="ea80a-114">Pour plus d’informations, consultez [Installer et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ea80a-114">For more information, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [expressroute-gateway-rm-ps](../../includes/expressroute-gateway-rm-ps-include.md)]

## <a name="next-steps"></a><span data-ttu-id="ea80a-115">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ea80a-115">Next steps</span></span>
<span data-ttu-id="ea80a-116">Une fois que vous avez créé la passerelle de réseau virtuel, vous pouvez lier votre réseau virtuel à un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ea80a-116">After you have created the VNet gateway, you can link your VNet to an ExpressRoute circuit.</span></span> <span data-ttu-id="ea80a-117">Consultez [Liaison d’un réseau virtuel à un circuit ExpressRoute](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="ea80a-117">See [Link a Virtual Network to an ExpressRoute circuit](expressroute-howto-linkvnet-arm.md).</span></span>

