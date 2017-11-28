---
title: aaaConnect tooa machine virtuelle Windows Server | Documents Microsoft
description: "Découvrez comment tooconnect et connectez-vous à l’aide de machine virtuelle Windows tooa hello Azure portal et hello Gestionnaire de ressources du modèle de déploiement."
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
ms.openlocfilehash: dc397f435ef165ae5af09f1d037ad3d520bb7ac3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconnect-and-log-on-tooan-azure-virtual-machine-running-windows"></a><span data-ttu-id="e3f72-103">Comment tooconnect et ouverture de session tooan Azure virtual machine exécutant Windows</span><span class="sxs-lookup"><span data-stu-id="e3f72-103">How tooconnect and log on tooan Azure virtual machine running Windows</span></span>
<span data-ttu-id="e3f72-104">Vous allez utiliser hello **Connect** bouton Bonjour Azure toostart portail une session Bureau à distance (RDP) à partir d’un ordinateur de bureau Windows.</span><span class="sxs-lookup"><span data-stu-id="e3f72-104">You'll use hello **Connect** button in hello Azure portal toostart a Remote Desktop (RDP) session from a Windows desktop.</span></span> <span data-ttu-id="e3f72-105">Tout d’abord vous connectez toohello virtual machine, puis vous connectez.</span><span class="sxs-lookup"><span data-stu-id="e3f72-105">First you connect toohello virtual machine, then you log on.</span></span>

<span data-ttu-id="e3f72-106">Si vous essayez de tooconnect tooa virtuelle Windows à partir d’un Mac, vous devez tooinstall un client RDP pour Mac comme [Bureau à distance Microsoft](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).</span><span class="sxs-lookup"><span data-stu-id="e3f72-106">If you are trying tooconnect tooa Windows VM from a Mac, you need tooinstall an RDP client for Mac like [Microsoft Remote Desktop](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).</span></span>

## <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="e3f72-107">Connecter l’ordinateur virtuel de toohello</span><span class="sxs-lookup"><span data-stu-id="e3f72-107">Connect toohello virtual machine</span></span>
1. <span data-ttu-id="e3f72-108">Si vous n’avez pas déjà fait, connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e3f72-108">If you haven't already done so, sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="e3f72-109">Dans le menu du Hub hello, cliquez sur **virtuels**.</span><span class="sxs-lookup"><span data-stu-id="e3f72-109">On hello Hub menu, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="e3f72-110">Sélectionnez hello virtuels à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="e3f72-110">Select hello virtual machine from hello list.</span></span>
4. <span data-ttu-id="e3f72-111">Dans le panneau hello pour la machine virtuelle de hello, cliquez sur **connexion**.</span><span class="sxs-lookup"><span data-stu-id="e3f72-111">On hello blade for hello virtual machine, click **Connect**.</span></span>
   
    ![Capture d’écran de hello montrant portail Azure comment tooconnect tooyour machine virtuelle.](./media/connect-logon/connect.png)
   
   > [!TIP]
   > <span data-ttu-id="e3f72-113">Si hello **Connect** bouton dans le portail de hello est grisé et vous n’êtes pas connecté tooAzure via un [Express Route](../../expressroute/expressroute-introduction.md) ou [VPN de Site à Site](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) connexion, vous devez toocreate et avant de pouvoir utiliser RDP, affecter votre machine virtuelle une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="e3f72-113">If hello **Connect** button in hello portal is greyed out and you are not connected tooAzure via an [Express Route](../../expressroute/expressroute-introduction.md) or [Site-to-Site VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) connection, you need toocreate and assign your VM a public IP address before you can use RDP.</span></span> <span data-ttu-id="e3f72-114">Pour en savoir plus sur les adresses IP publiques dans Azure, consultez [cet article](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span><span class="sxs-lookup"><span data-stu-id="e3f72-114">You can read more about [public IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span></span>
   > 
   > 

## <a name="log-on-toohello-virtual-machine"></a><span data-ttu-id="e3f72-115">Ouvrez une session sur l’ordinateur virtuel de toohello</span><span class="sxs-lookup"><span data-stu-id="e3f72-115">Log on toohello virtual machine</span></span>
[!INCLUDE [virtual-machines-log-on-win-server](../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a><span data-ttu-id="e3f72-116">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e3f72-116">Next steps</span></span>
<span data-ttu-id="e3f72-117">Si vous rencontrez des problèmes lorsque vous essayez de tooconnect, consultez [connexions résoudre les problèmes de bureau à distance](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e3f72-117">If you run into trouble when you try tooconnect, see [Troubleshoot Remote Desktop connections](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="e3f72-118">Cet article vous guide tout au long des opérations de diagnostic et de résolution des problèmes courants.</span><span class="sxs-lookup"><span data-stu-id="e3f72-118">This article walks you through diagnosing and resolving common problems.</span></span>

