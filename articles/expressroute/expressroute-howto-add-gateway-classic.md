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
ms.openlocfilehash: 6f37d4d9cba546b5416ab99040f5ef6dae273380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell-classic"></a><span data-ttu-id="1000e-103">Configurer une passerelle de réseau virtuel pour ExpressRoute à l’aide de PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="1000e-103">Configure a virtual network gateway for ExpressRoute using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1000e-104">Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="1000e-104">Resource Manager - PowerShell</span></span>](expressroute-howto-add-gateway-resource-manager.md)
> * [<span data-ttu-id="1000e-105">Classic - PowerShell</span><span class="sxs-lookup"><span data-stu-id="1000e-105">Classic - PowerShell</span></span>](expressroute-howto-add-gateway-classic.md)
> * [<span data-ttu-id="1000e-106">Vidéo - portail Azure</span><span class="sxs-lookup"><span data-stu-id="1000e-106">Video - Azure Portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

<span data-ttu-id="1000e-107">Cet article vous aidera à hello étapes tooadd, redimensionner et supprimer une passerelle de réseau virtuel (VNet) pour un réseau virtuel existant.</span><span class="sxs-lookup"><span data-stu-id="1000e-107">This article will walk you through hello steps tooadd, resize, and remove a virtual network (VNet) gateway for a pre-existing VNet.</span></span> <span data-ttu-id="1000e-108">Hello étapes de cette configuration sont spécifiquement pour les réseaux virtuels qui ont été créés à l’aide de hello **modèle de déploiement classique** qui correspond à être utilisé dans une configuration de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="1000e-108">hello steps for this configuration are specifically for VNets that were created using hello **classic deployment model** and that will be be used in an ExpressRoute configuration.</span></span> 

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="1000e-109">**À propos des modèles de déploiement Azure**</span><span class="sxs-lookup"><span data-stu-id="1000e-109">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-beginning"></a><span data-ttu-id="1000e-110">Avant tout chose</span><span class="sxs-lookup"><span data-stu-id="1000e-110">Before beginning</span></span>
<span data-ttu-id="1000e-111">Vérifiez que vous avez installé les applets de commande PowerShell Azure hello nécessaires pour cette configuration (la version 1.0.2 ou version ultérieure).</span><span class="sxs-lookup"><span data-stu-id="1000e-111">Verify that you have installed hello Azure PowerShell cmdlets needed for this configuration (1.0.2 or later).</span></span> <span data-ttu-id="1000e-112">Si vous n’avez pas installé les applets de commande hello, vous devez toodo par conséquent avant de commencer les étapes de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="1000e-112">If you haven't installed hello cmdlets, you'll need toodo so before beginning hello configuration steps.</span></span> <span data-ttu-id="1000e-113">Pour plus d’informations sur l’installation d’Azure PowerShell, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1000e-113">For more information about installing Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [expressroute-gateway-classic-ps](../../includes/expressroute-gateway-classic-ps-include.md)]

## <a name="next-steps"></a><span data-ttu-id="1000e-114">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1000e-114">Next steps</span></span>
<span data-ttu-id="1000e-115">Une fois que vous avez créé la passerelle de réseau virtuel hello, vous pouvez lier votre réseau virtuel de tooan circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="1000e-115">After you have created hello VNet gateway, you can link your VNet tooan ExpressRoute circuit.</span></span> <span data-ttu-id="1000e-116">Consultez [lier un circuit ExpressRoute de tooan réseau virtuel](expressroute-howto-linkvnet-classic.md).</span><span class="sxs-lookup"><span data-stu-id="1000e-116">See [Link a Virtual Network tooan ExpressRoute circuit](expressroute-howto-linkvnet-classic.md).</span></span>

