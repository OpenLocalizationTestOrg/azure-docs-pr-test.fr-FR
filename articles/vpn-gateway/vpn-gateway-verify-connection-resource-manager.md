---
title: "Vérifier la connexion d’une passerelle VPN | Microsoft Docs"
description: "Cet article vous montre comment vérifier une connexion de passerelle VPN de réseau virtuel."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 7e3d1043-caa9-4472-96d3-832f4e2c91ee
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/16/2017
ms.author: cherylmc
ms.openlocfilehash: b2d702ecdd5e1fca342e7c84c6e75339097f0bcd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="verify-a-vpn-gateway-connection"></a><span data-ttu-id="dbec8-103">Vérifier une connexion de passerelle VPN</span><span class="sxs-lookup"><span data-stu-id="dbec8-103">Verify a VPN Gateway connection</span></span>

<span data-ttu-id="dbec8-104">Cet article vous montre comment vérifier une connexion à une passerelle VPN à la fois pour le modèle de déploiement Classic et pour le modèle de déploiement Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="dbec8-104">This article shows you how to verify a VPN gateway connection for both the classic and Resource Manager deployment models.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="dbec8-105">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="dbec8-105">Azure portal</span></span>

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="powershell"></a><span data-ttu-id="dbec8-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dbec8-106">PowerShell</span></span>

<span data-ttu-id="dbec8-107">Pour vérifier une connexion de passerelle VPN pour le modèle de déploiement Resource Manager à l’aide de PowerShell, installez la dernière version des [cmdlets PowerShell Azure Resource Manager](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dbec8-107">To verify a VPN gateway connection for the Resource Manager deployment model using PowerShell, install the latest version of the [Azure Resource Manager PowerShell cmdlets](/powershell/azure/overview).</span></span>

[!INCLUDE [PowerShell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="azure-cli"></a><span data-ttu-id="dbec8-108">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="dbec8-108">Azure CLI</span></span>

<span data-ttu-id="dbec8-109">Pour vérifier une connexion de passerelle VPN pour le modèle de déploiement Resource Manager à l’aide d’Azure CLI, installez la dernière version des [commandes CLI](https://docs.microsoft.com/cli/azure/install-azure-cli) (2.0 ou version ultérieure).</span><span class="sxs-lookup"><span data-stu-id="dbec8-109">To verify a VPN gateway connection for the Resource Manager deployment model using Azure CLI, install the latest version of the [CLI commands](https://docs.microsoft.com/cli/azure/install-azure-cli) (2.0 or later).</span></span>

[!INCLUDE [CLI](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]


## <a name="azure-portal-classic"></a><span data-ttu-id="dbec8-110">Portail Azure (Classic)</span><span class="sxs-lookup"><span data-stu-id="dbec8-110">Azure portal (classic)</span></span>

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

## <a name="powershell-classic"></a><span data-ttu-id="dbec8-111">PowerShell (Classic)</span><span class="sxs-lookup"><span data-stu-id="dbec8-111">PowerShell (classic)</span></span>

<span data-ttu-id="dbec8-112">Pour vérifier votre connexion de passerelle VPN pour le modèle de déploiement classique à l’aide de PowerShell, installez les dernières versions des cmdlets Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dbec8-112">To verify your VPN gateway connection for the classic deployment model using PowerShell, install the latest versions of the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="dbec8-113">Veillez à télécharger et à installer le module [Gestion des services](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="dbec8-113">Be sure to download and install the [Service Management](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0) module.</span></span> <span data-ttu-id="dbec8-114">Utilisez « Add-AzureAccount » pour vous connecter au modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="dbec8-114">Use 'Add-AzureAccount' to log in to the classic deployment model.</span></span>

[!INCLUDE [Classic PowerShell](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

## <a name="next-steps"></a><span data-ttu-id="dbec8-115">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dbec8-115">Next steps</span></span>

* <span data-ttu-id="dbec8-116">Vous pouvez ajouter des machines virtuelles à vos réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="dbec8-116">You can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="dbec8-117">Consultez [Création d’une machine virtuelle](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) pour connaître les différentes étapes.</span><span class="sxs-lookup"><span data-stu-id="dbec8-117">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>