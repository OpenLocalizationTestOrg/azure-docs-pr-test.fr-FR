---
title: "une connexion de passerelle VPN d’aaaVerify | Documents Microsoft"
description: "Cet article vous montre comment la connexion de la passerelle VPN de réseau tooverify a virtual."
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
ms.openlocfilehash: 0d3da94a76b36251d629f82b1575328c7ac10b26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="verify-a-vpn-gateway-connection"></a><span data-ttu-id="3b29d-103">Vérifier une connexion de passerelle VPN</span><span class="sxs-lookup"><span data-stu-id="3b29d-103">Verify a VPN Gateway connection</span></span>

<span data-ttu-id="3b29d-104">Cet article vous montre comment tooverify une connexion de passerelle VPN pour hello classique et les modèles de déploiement de gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="3b29d-104">This article shows you how tooverify a VPN gateway connection for both hello classic and Resource Manager deployment models.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="3b29d-105">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="3b29d-105">Azure portal</span></span>

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="powershell"></a><span data-ttu-id="3b29d-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3b29d-106">PowerShell</span></span>

<span data-ttu-id="3b29d-107">tooverify une connexion de passerelle VPN pour hello déploiement du Gestionnaire de ressources de modèle à l’aide de PowerShell, installer la version la plus récente de hello hello [applets de commande PowerShell de gestionnaire de ressources Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3b29d-107">tooverify a VPN gateway connection for hello Resource Manager deployment model using PowerShell, install hello latest version of hello [Azure Resource Manager PowerShell cmdlets](/powershell/azure/overview).</span></span>

[!INCLUDE [PowerShell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="azure-cli"></a><span data-ttu-id="3b29d-108">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="3b29d-108">Azure CLI</span></span>

<span data-ttu-id="3b29d-109">tooverify une connexion de passerelle VPN pour hello déploiement du Gestionnaire de ressources de modèle à l’aide d’Azure CLI, installer la version la plus récente de hello hello [commandes CLI](https://docs.microsoft.com/cli/azure/install-azure-cli) (version 2.0 ou version ultérieure).</span><span class="sxs-lookup"><span data-stu-id="3b29d-109">tooverify a VPN gateway connection for hello Resource Manager deployment model using Azure CLI, install hello latest version of hello [CLI commands](https://docs.microsoft.com/cli/azure/install-azure-cli) (2.0 or later).</span></span>

[!INCLUDE [CLI](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]


## <a name="azure-portal-classic"></a><span data-ttu-id="3b29d-110">Portail Azure (Classic)</span><span class="sxs-lookup"><span data-stu-id="3b29d-110">Azure portal (classic)</span></span>

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

## <a name="powershell-classic"></a><span data-ttu-id="3b29d-111">PowerShell (Classic)</span><span class="sxs-lookup"><span data-stu-id="3b29d-111">PowerShell (classic)</span></span>

<span data-ttu-id="3b29d-112">tooverify votre connexion de passerelle VPN pour le déploiement classique de hello de modèle à l’aide de PowerShell, installer hello dernières versions de hello applets de commande PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="3b29d-112">tooverify your VPN gateway connection for hello classic deployment model using PowerShell, install hello latest versions of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="3b29d-113">Être vraiment hello de toodownload et installer [de gestion des services](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0) module.</span><span class="sxs-lookup"><span data-stu-id="3b29d-113">Be sure toodownload and install hello [Service Management](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0) module.</span></span> <span data-ttu-id="3b29d-114">Utilisez 'Add-AzureAccount' toolog dans le modèle de déploiement classique toohello.</span><span class="sxs-lookup"><span data-stu-id="3b29d-114">Use 'Add-AzureAccount' toolog in toohello classic deployment model.</span></span>

[!INCLUDE [Classic PowerShell](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

## <a name="next-steps"></a><span data-ttu-id="3b29d-115">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3b29d-115">Next steps</span></span>

* <span data-ttu-id="3b29d-116">Vous pouvez ajouter des machines virtuelles tooyour des réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="3b29d-116">You can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="3b29d-117">Consultez [Création d’une machine virtuelle](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) pour connaître les différentes étapes.</span><span class="sxs-lookup"><span data-stu-id="3b29d-117">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>
