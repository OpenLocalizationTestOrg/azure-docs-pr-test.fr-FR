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
# <a name="how-tooconnect-and-log-on-tooan-azure-virtual-machine-running-windows"></a>Comment tooconnect et ouverture de session tooan Azure virtual machine exécutant Windows
Vous allez utiliser hello **Connect** bouton Bonjour Azure toostart portail une session Bureau à distance (RDP) à partir d’un ordinateur de bureau Windows. Tout d’abord vous connectez toohello virtual machine, puis vous connectez.

Si vous essayez de tooconnect tooa virtuelle Windows à partir d’un Mac, vous devez tooinstall un client RDP pour Mac comme [Bureau à distance Microsoft](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).

## <a name="connect-toohello-virtual-machine"></a>Connecter l’ordinateur virtuel de toohello
1. Si vous n’avez pas déjà fait, connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2. Dans le menu du Hub hello, cliquez sur **virtuels**.
3. Sélectionnez hello virtuels à partir de la liste de hello.
4. Dans le panneau hello pour la machine virtuelle de hello, cliquez sur **connexion**.
   
    ![Capture d’écran de hello montrant portail Azure comment tooconnect tooyour machine virtuelle.](./media/connect-logon/connect.png)
   
   > [!TIP]
   > Si hello **Connect** bouton dans le portail de hello est grisé et vous n’êtes pas connecté tooAzure via un [Express Route](../../expressroute/expressroute-introduction.md) ou [VPN de Site à Site](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) connexion, vous devez toocreate et avant de pouvoir utiliser RDP, affecter votre machine virtuelle une adresse IP publique. Pour en savoir plus sur les adresses IP publiques dans Azure, consultez [cet article](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).
   > 
   > 

## <a name="log-on-toohello-virtual-machine"></a>Ouvrez une session sur l’ordinateur virtuel de toohello
[!INCLUDE [virtual-machines-log-on-win-server](../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a>Étapes suivantes
Si vous rencontrez des problèmes lorsque vous essayez de tooconnect, consultez [connexions résoudre les problèmes de bureau à distance](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Cet article vous guide tout au long des opérations de diagnostic et de résolution des problèmes courants.

