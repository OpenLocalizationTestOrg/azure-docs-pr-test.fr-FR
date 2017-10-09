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
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell-classic"></a>Configurer une passerelle de réseau virtuel pour ExpressRoute à l’aide de PowerShell (classique)
> [!div class="op_single_selector"]
> * [Resource Manager - PowerShell](expressroute-howto-add-gateway-resource-manager.md)
> * [Classic - PowerShell](expressroute-howto-add-gateway-classic.md)
> * [Vidéo - portail Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

Cet article vous aidera à hello étapes tooadd, redimensionner et supprimer une passerelle de réseau virtuel (VNet) pour un réseau virtuel existant. Hello étapes de cette configuration sont spécifiquement pour les réseaux virtuels qui ont été créés à l’aide de hello **modèle de déploiement classique** qui correspond à être utilisé dans une configuration de ExpressRoute. 

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**À propos des modèles de déploiement Azure**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-beginning"></a>Avant tout chose
Vérifiez que vous avez installé les applets de commande PowerShell Azure hello nécessaires pour cette configuration (la version 1.0.2 ou version ultérieure). Si vous n’avez pas installé les applets de commande hello, vous devez toodo par conséquent avant de commencer les étapes de configuration hello. Pour plus d’informations sur l’installation d’Azure PowerShell, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).

[!INCLUDE [expressroute-gateway-classic-ps](../../includes/expressroute-gateway-classic-ps-include.md)]

## <a name="next-steps"></a>Étapes suivantes
Une fois que vous avez créé la passerelle de réseau virtuel hello, vous pouvez lier votre réseau virtuel de tooan circuit ExpressRoute. Consultez [lier un circuit ExpressRoute de tooan réseau virtuel](expressroute-howto-linkvnet-classic.md).

