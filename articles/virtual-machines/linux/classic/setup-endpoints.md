---
title: Configurer des points de terminaison sur une machine virtuelle Linux classique | Microsoft Docs
description: "Apprenez à configurer des points de terminaison pour une machine virtuelle Linux dans le portail Azure Classic pour permettre la communication avec une machine virtuelle Linux dans Azure"
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
ms.openlocfilehash: 4fd8b847b0f60648d1661ce5a8667c641e616ed4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-set-up-endpoints-on-a-linux-classic-virtual-machine-in-azure"></a><span data-ttu-id="529be-103">Comment configurer des points de terminaison sur une machine virtuelle Linux classique dans Azure</span><span class="sxs-lookup"><span data-stu-id="529be-103">How to set up endpoints on a Linux classic virtual machine in Azure</span></span>
<span data-ttu-id="529be-104">Toutes les machines virtuelles Linux créées dans Azure à l’aide du modèle de déploiement classique peuvent automatiquement communiquer sur un canal réseau privé avec d’autres machines virtuelles dans le même service cloud ou réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="529be-104">All Linux virtual machines that you create in Azure using the classic deployment model can automatically communicate over a private network channel with other virtual machines in the same cloud service or virtual network.</span></span> <span data-ttu-id="529be-105">Toutefois, les ordinateurs sur Internet ou d'autres réseaux virtuels requièrent des points de terminaison pour diriger le trafic réseau entrant vers une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="529be-105">However, computers on the Internet or other virtual networks require endpoints to direct the inbound network traffic to a virtual machine.</span></span> <span data-ttu-id="529be-106">Cet article est également disponible pour les [machines virtuelles Windows](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="529be-106">This article is also available for [Windows virtual machines](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="529be-107">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="529be-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="529be-108">Cet article traite du modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="529be-108">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="529be-109">Pour la plupart des nouveaux déploiements, Microsoft recommande d’utiliser le modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="529be-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="529be-110">Dans le modèle de déploiement **Resource Manager**, les points de terminaison sont configurés à l’aide de **groupes de sécurité réseau (NSG)**.</span><span class="sxs-lookup"><span data-stu-id="529be-110">In the **Resource Manager** deployment model, endpoints are configured using **Network Security Groups (NSGs)**.</span></span> <span data-ttu-id="529be-111">Pour plus d’informations, consultez la page [Ouverture des ports et des points de terminaison](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="529be-111">For more information, see [Opening ports and endpoints](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="529be-112">Lorsque vous créez une machine virtuelle Linux sur le portail Azure, un point de terminaison pour Secure Shell (SSH) est en général créé automatiquement pour vous.</span><span class="sxs-lookup"><span data-stu-id="529be-112">When you create a Linux virtual machine in the Azure portal, an endpoint for Secure Shell (SSH) is typically created for you automatically.</span></span> <span data-ttu-id="529be-113">Vous pouvez configurer des points de terminaison supplémentaires lors de la création de la machine virtuelle, ou ultérieurement si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="529be-113">You can configure additional endpoints while creating the virtual machine or afterwards as needed.</span></span>

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a><span data-ttu-id="529be-114">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="529be-114">Next steps</span></span>
* <span data-ttu-id="529be-115">Vous pouvez également créer un point de terminaison de machine virtuelle à l’aide de l’ [interface de ligne de commande Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="529be-115">You can also create a VM endpoint by using the [Azure Command-Line Interface](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span> <span data-ttu-id="529be-116">Exécutez la commande **azure vm endpoint create** .</span><span class="sxs-lookup"><span data-stu-id="529be-116">Run the **azure vm endpoint create** command.</span></span>
* <span data-ttu-id="529be-117">Si vous avez créé une machine virtuelle dans le modèle de déploiement Resource Manager, vous pouvez utiliser l’interface CLI Azure en mode Resource Manager pour [créer des groupes de sécurité réseau](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) afin de contrôler le trafic vers la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="529be-117">If you created a virtual machine in the Resource Manager deployment model, you can use the Azure CLI in Resource Manager mode to [create network security groups](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) to control traffic to the VM.</span></span>
