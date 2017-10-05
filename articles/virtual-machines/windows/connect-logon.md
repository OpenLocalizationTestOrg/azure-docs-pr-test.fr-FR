---
title: "Connexion à une machine virtuelle Windows Server | Microsoft Docs"
description: "Découvrez comment vous connecter à une machine virtuelle Windows à l’aide du portail Azure et du modèle de déploiement Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ef62b02e-bf35-468d-b4c3-71b63fe7f409
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/01/2017
ms.author: cynthn
ms.openlocfilehash: 88431377a36d5bc36220c630f0c8d4a46ab4a434
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-connect-and-log-on-to-an-azure-virtual-machine-running-windows"></a><span data-ttu-id="656be-103">Connexion à une machine virtuelle Azure exécutant Windows</span><span class="sxs-lookup"><span data-stu-id="656be-103">How to connect and log on to an Azure virtual machine running Windows</span></span>
<span data-ttu-id="656be-104">Vous utilisez le bouton **Connecter** dans le portail Azure pour démarrer une session Bureau à distance (RDP) depuis un bureau Windows.</span><span class="sxs-lookup"><span data-stu-id="656be-104">You'll use the **Connect** button in the Azure portal to start a Remote Desktop (RDP) session from a Windows desktop.</span></span> <span data-ttu-id="656be-105">Tout d’abord, connectez-vous à la machine virtuelle, puis ouvrez une session.</span><span class="sxs-lookup"><span data-stu-id="656be-105">First you connect to the virtual machine, then you log on.</span></span>

<span data-ttu-id="656be-106">Si vous essayez de vous connecter à une machine virtuelle Windows à partir d’un Mac, vous devez installer un client RDP pour Mac du type [Bureau à distance Microsoft](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).</span><span class="sxs-lookup"><span data-stu-id="656be-106">If you are trying to connect to a Windows VM from a Mac, you need to install an RDP client for Mac like [Microsoft Remote Desktop](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).</span></span>

## <a name="connect-to-the-virtual-machine"></a><span data-ttu-id="656be-107">Connectez-vous à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="656be-107">Connect to the virtual machine</span></span>
1. <span data-ttu-id="656be-108">Si ce n’est pas déjà fait, connectez-vous au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="656be-108">If you haven't already done so, sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="656be-109">Dans le menu hub, cliquez sur **Machines virtuelles**.</span><span class="sxs-lookup"><span data-stu-id="656be-109">On the Hub menu, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="656be-110">Sélectionnez la machine virtuelle dans la liste.</span><span class="sxs-lookup"><span data-stu-id="656be-110">Select the virtual machine from the list.</span></span>
4. <span data-ttu-id="656be-111">Dans le panneau de la machine virtuelle, cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="656be-111">On the blade for the virtual machine, click **Connect**.</span></span>
   
    ![Capture d'écran du portail Azure montrant comment se connecter à votre machine virtuelle.](./media/connect-logon/connect.png)
   
   > [!TIP]
   > <span data-ttu-id="656be-113">Si le bouton **Connecter** du portail est grisé et si vous n’êtes pas connecté à Azure avec une connexion [Express Route](../../expressroute/expressroute-introduction.md) ou [réseau privé virtuel de site à site](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md), vous devez créer votre machine virtuelle et lui attribuer une adresse IP publique pour pouvoir utiliser le protocole RDP.</span><span class="sxs-lookup"><span data-stu-id="656be-113">If the **Connect** button in the portal is greyed out and you are not connected to Azure via an [Express Route](../../expressroute/expressroute-introduction.md) or [Site-to-Site VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) connection, you need to create and assign your VM a public IP address before you can use RDP.</span></span> <span data-ttu-id="656be-114">Pour en savoir plus sur les adresses IP publiques dans Azure, consultez [cet article](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span><span class="sxs-lookup"><span data-stu-id="656be-114">You can read more about [public IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span></span>
   > 
   > 

## <a name="log-on-to-the-virtual-machine"></a><span data-ttu-id="656be-115">Connexion à la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="656be-115">Log on to the virtual machine</span></span>
[!INCLUDE [virtual-machines-log-on-win-server](../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a><span data-ttu-id="656be-116">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="656be-116">Next steps</span></span>
<span data-ttu-id="656be-117">En cas de problème de connexion, consultez [Résolution des problèmes de connexion Bureau à distance](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="656be-117">If you run into trouble when you try to connect, see [Troubleshoot Remote Desktop connections](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="656be-118">Cet article vous guide tout au long des opérations de diagnostic et de résolution des problèmes courants.</span><span class="sxs-lookup"><span data-stu-id="656be-118">This article walks you through diagnosing and resolving common problems.</span></span>

