---
title: Configurer des points de terminaison sur une machine virtuelle Windows classique | Microsoft Docs
description: "Apprenez à configurer des points de terminaison pour une machine virtuelle Windows dans le portail Azure Classic pour permettre la communication avec une machine virtuelle Windows dans Azure."
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
ms.openlocfilehash: 60861819a7e437bb715b14c0e8eaf74f13b33ebf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-set-up-endpoints-on-a-classic-windows-virtual-machine-in-azure"></a><span data-ttu-id="6ec95-103">Comment configurer des points de terminaison sur une machine virtuelle Windows classique dans Azure</span><span class="sxs-lookup"><span data-stu-id="6ec95-103">How to set up endpoints on a classic Windows virtual machine in Azure</span></span>
<span data-ttu-id="6ec95-104">Toutes les machines virtuelles Windows créées dans Azure à l’aide du modèle de déploiement classique peuvent automatiquement communiquer à travers un canal réseau privé avec d’autres machines virtuelles dans le même service cloud ou réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="6ec95-104">All Windows virtual machines that you create in Azure using the classic deployment model can automatically communicate over a private network channel with other virtual machines in the same cloud service or virtual network.</span></span> <span data-ttu-id="6ec95-105">Toutefois, les ordinateurs sur Internet ou d'autres réseaux virtuels requièrent des points de terminaison pour diriger le trafic réseau entrant vers une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6ec95-105">However, computers on the Internet or other virtual networks require endpoints to direct the inbound network traffic to a virtual machine.</span></span> <span data-ttu-id="6ec95-106">Cet article est également disponible pour les [machines virtuelles Linux](../../linux/classic/setup-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="6ec95-106">This article is also available for [Linux virtual machines](../../linux/classic/setup-endpoints.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6ec95-107">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="6ec95-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="6ec95-108">Cet article traite du modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="6ec95-108">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="6ec95-109">Pour la plupart des nouveaux déploiements, Microsoft recommande d’utiliser le modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6ec95-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="6ec95-110">Dans le modèle de déploiement **Resource Manager**, les points de terminaison sont configurés à l’aide de **groupes de sécurité réseau (NSG)**.</span><span class="sxs-lookup"><span data-stu-id="6ec95-110">In the **Resource Manager** deployment model, endpoints are configured using **Network Security Groups (NSGs)**.</span></span> <span data-ttu-id="6ec95-111">Pour plus d’informations, voir [Autoriser l’accès externe à votre machine virtuelle à l’aide du portail Azure](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6ec95-111">For more information, see [Allow external access to your VM using the Azure portal](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="6ec95-112">Quand vous créez une machine virtuelle Windows dans le portail Azure, les points de terminaison courants, notamment ceux du Bureau à distance et de l’Accès distant Windows PowerShell, sont généralement créés pour vous automatiquement.</span><span class="sxs-lookup"><span data-stu-id="6ec95-112">When you create a Windows virtual machine in the Azure portal, common endpoints like those for Remote Desktop and Windows PowerShell Remoting are typically created for you automatically.</span></span> <span data-ttu-id="6ec95-113">Vous pouvez configurer des points de terminaison supplémentaires lors de la création de la machine virtuelle, ou ultérieurement si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="6ec95-113">You can configure additional endpoints while creating the virtual machine or afterwards as needed.</span></span>

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a><span data-ttu-id="6ec95-114">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6ec95-114">Next steps</span></span>
* <span data-ttu-id="6ec95-115">Pour configurer un point de terminaison de machine virtuelle à l’aide d’une applet de commande Azure PowerShell, consultez [Add-AzureEndpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx).</span><span class="sxs-lookup"><span data-stu-id="6ec95-115">To use an Azure PowerShell cmdlet to set up a VM endpoint, see [Add-AzureEndpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx).</span></span>
* <span data-ttu-id="6ec95-116">Pour gérer une liste de contrôle d’accès sur un point de terminaison à l’aide d’une applet de commande Azure PowerShell, consultez [Gestion des listes de contrôle d’accès (ACL) pour les points de terminaison à l’aide de PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="6ec95-116">To use an Azure PowerShell cmdlet to manage an ACL on an endpoint, see [Managing access control lists (ACLs) for endpoints by using PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md).</span></span>
* <span data-ttu-id="6ec95-117">Si vous avez créé une machine virtuelle dans le modèle de déploiement Resource Manager, vous pouvez utiliser Azure PowerShell pour [créer des groupes de sécurité réseau](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) afin de contrôler le trafic vers la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6ec95-117">If you created a virtual machine in the Resource Manager deployment model, you can use Azure PowerShell to [create network security groups](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) to control traffic to the VM.</span></span>
