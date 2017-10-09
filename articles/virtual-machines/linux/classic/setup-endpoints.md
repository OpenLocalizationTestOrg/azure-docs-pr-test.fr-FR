---
title: aaaSet des points de terminaison sur un VM Linux classique | Documents Microsoft
description: En savoir plus tooset des points de terminaison pour un VM Linux Bonjour tooallow de portail classique Azure communication avec un ordinateur virtuel de Linux dans Azure
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: f3749738-1109-4a1d-8635-40e4bd220e91
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: 1c959d10dd1e20228fa4a20e1cc0205c1d12f185
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-endpoints-on-a-linux-classic-virtual-machine-in-azure"></a><span data-ttu-id="67e71-103">Comment tooset des points de terminaison sur une machine virtuelle Linux la classique dans Azure</span><span class="sxs-lookup"><span data-stu-id="67e71-103">How tooset up endpoints on a Linux classic virtual machine in Azure</span></span>
<span data-ttu-id="67e71-104">Tous les ordinateurs virtuels Linux que vous créez dans Azure à l’aide du modèle de déploiement classique hello peuvent communiquer automatiquement via un canal réseau privé avec d’autres ordinateurs virtuels de hello que même service ou de réseau virtuel de cloud.</span><span class="sxs-lookup"><span data-stu-id="67e71-104">All Linux virtual machines that you create in Azure using hello classic deployment model can automatically communicate over a private network channel with other virtual machines in hello same cloud service or virtual network.</span></span> <span data-ttu-id="67e71-105">Toutefois, les ordinateurs sur hello Internet ou d’autres réseaux virtuels nécessitent des points de terminaison toodirect hello réseau entrant trafic tooa machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="67e71-105">However, computers on hello Internet or other virtual networks require endpoints toodirect hello inbound network traffic tooa virtual machine.</span></span> <span data-ttu-id="67e71-106">Cet article est également disponible pour les [machines virtuelles Windows](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="67e71-106">This article is also available for [Windows virtual machines](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="67e71-107">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="67e71-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="67e71-108">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="67e71-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="67e71-109">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="67e71-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="67e71-110">Bonjour **le Gestionnaire de ressources** modèle de déploiement, points de terminaison sont configurés à l’aide de **groupes de sécurité réseau (NSG)**.</span><span class="sxs-lookup"><span data-stu-id="67e71-110">In hello **Resource Manager** deployment model, endpoints are configured using **Network Security Groups (NSGs)**.</span></span> <span data-ttu-id="67e71-111">Pour plus d’informations, consultez la page [Ouverture des ports et des points de terminaison](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="67e71-111">For more information, see [Opening ports and endpoints](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="67e71-112">Lorsque vous créez une machine virtuelle Linux Bonjour portail Azure, un point de terminaison pour SSH (Secure Shell) est généralement créé pour vous automatiquement.</span><span class="sxs-lookup"><span data-stu-id="67e71-112">When you create a Linux virtual machine in hello Azure portal, an endpoint for Secure Shell (SSH) is typically created for you automatically.</span></span> <span data-ttu-id="67e71-113">Vous pouvez configurer des points de terminaison supplémentaires lors de la création d’ordinateur virtuel de hello ou par la suite si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="67e71-113">You can configure additional endpoints while creating hello virtual machine or afterwards as needed.</span></span>

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a><span data-ttu-id="67e71-114">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="67e71-114">Next steps</span></span>
* <span data-ttu-id="67e71-115">Vous pouvez également créer un point de terminaison de machine virtuelle à l’aide de hello [Interface de ligne de commande Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="67e71-115">You can also create a VM endpoint by using hello [Azure Command-Line Interface](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span> <span data-ttu-id="67e71-116">Exécutez hello **créer de point de terminaison de machine virtuelle azure** commande.</span><span class="sxs-lookup"><span data-stu-id="67e71-116">Run hello **azure vm endpoint create** command.</span></span>
* <span data-ttu-id="67e71-117">Si vous avez créé une machine virtuelle dans le modèle de déploiement du Gestionnaire de ressources hello, vous pouvez utiliser hello CLI d’Azure en mode de gestionnaire de ressources trop[créer des groupes de sécurité réseau](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) toocontrol trafic toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="67e71-117">If you created a virtual machine in hello Resource Manager deployment model, you can use hello Azure CLI in Resource Manager mode too[create network security groups](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) toocontrol traffic toohello VM.</span></span>
