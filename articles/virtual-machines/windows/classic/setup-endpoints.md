---
title: aaaSet des points de terminaison sur une machine virtuelle Windows classique | Documents Microsoft
description: En savoir plus tooset des points de terminaison pour une machine virtuelle Windows dans hello tooallow de portail classique Azure communication avec un ordinateur virtuel de Windows dans Azure.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 8afc21c2-d3fb-43a3-acce-aa06be448bb6
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: e817076f16d3a245a8d19add7b2f2cf5e3baa17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-endpoints-on-a-classic-windows-virtual-machine-in-azure"></a><span data-ttu-id="db08c-103">Comment tooset des points de terminaison sur un ordinateur de virtuel Windows classique dans Azure</span><span class="sxs-lookup"><span data-stu-id="db08c-103">How tooset up endpoints on a classic Windows virtual machine in Azure</span></span>
<span data-ttu-id="db08c-104">Toutes les fenêtres de machines virtuelles que vous créez dans Azure à l’aide du modèle de déploiement classique hello peuvent communiquer automatiquement via un canal réseau privé avec d’autres ordinateurs virtuels de hello même service cloud ou réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="db08c-104">All Windows virtual machines that you create in Azure using hello classic deployment model can automatically communicate over a private network channel with other virtual machines in hello same cloud service or virtual network.</span></span> <span data-ttu-id="db08c-105">Toutefois, les ordinateurs sur hello Internet ou d’autres réseaux virtuels nécessitent des points de terminaison toodirect hello réseau entrant trafic tooa machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="db08c-105">However, computers on hello Internet or other virtual networks require endpoints toodirect hello inbound network traffic tooa virtual machine.</span></span> <span data-ttu-id="db08c-106">Cet article est également disponible pour les [machines virtuelles Linux](../../linux/classic/setup-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="db08c-106">This article is also available for [Linux virtual machines](../../linux/classic/setup-endpoints.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="db08c-107">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="db08c-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="db08c-108">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="db08c-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="db08c-109">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="db08c-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="db08c-110">Bonjour **le Gestionnaire de ressources** modèle de déploiement, points de terminaison sont configurés à l’aide de **groupes de sécurité réseau (NSG)**.</span><span class="sxs-lookup"><span data-stu-id="db08c-110">In hello **Resource Manager** deployment model, endpoints are configured using **Network Security Groups (NSGs)**.</span></span> <span data-ttu-id="db08c-111">Pour plus d’informations, consultez [autoriser un accès externe tooyour machine virtuelle en utilisant hello Azure portal](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="db08c-111">For more information, see [Allow external access tooyour VM using hello Azure portal](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="db08c-112">Lorsque vous créez une machine virtuelle Windows dans hello portail Azure, des points de terminaison courantes telles que celles pour le Bureau à distance et accès distant Windows PowerShell sont généralement créées pour vous automatiquement.</span><span class="sxs-lookup"><span data-stu-id="db08c-112">When you create a Windows virtual machine in hello Azure portal, common endpoints like those for Remote Desktop and Windows PowerShell Remoting are typically created for you automatically.</span></span> <span data-ttu-id="db08c-113">Vous pouvez configurer des points de terminaison supplémentaires lors de la création d’ordinateur virtuel de hello ou par la suite si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="db08c-113">You can configure additional endpoints while creating hello virtual machine or afterwards as needed.</span></span>

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a><span data-ttu-id="db08c-114">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="db08c-114">Next steps</span></span>
* <span data-ttu-id="db08c-115">toouse un tooset d’applet de commande Azure PowerShell du point de terminaison de la machine virtuelle, consultez [Add-AzureEndpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx).</span><span class="sxs-lookup"><span data-stu-id="db08c-115">toouse an Azure PowerShell cmdlet tooset up a VM endpoint, see [Add-AzureEndpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx).</span></span>
* <span data-ttu-id="db08c-116">toouse un toomanage d’applet de commande Azure PowerShell une ACL sur un point de terminaison, consultez [contrôle d’accès de gestion des listes (ACL) pour les points de terminaison à l’aide de PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="db08c-116">toouse an Azure PowerShell cmdlet toomanage an ACL on an endpoint, see [Managing access control lists (ACLs) for endpoints by using PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md).</span></span>
* <span data-ttu-id="db08c-117">Si vous avez créé une machine virtuelle dans le modèle de déploiement du Gestionnaire de ressources hello, vous pouvez utiliser Azure PowerShell trop[créer des groupes de sécurité réseau](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) toocontrol trafic toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="db08c-117">If you created a virtual machine in hello Resource Manager deployment model, you can use Azure PowerShell too[create network security groups](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) toocontrol traffic toohello VM.</span></span>
