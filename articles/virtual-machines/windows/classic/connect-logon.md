---
title: aaaLog sur tooa classique Azure VM | Documents Microsoft
description: "Sur l’ordinateur virtuel de tooa Windows créé avec le modèle de déploiement classique de hello, utilisez hello toolog portail Azure."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 3c1239ed-07dc-48b8-8b3d-dc8c5f0ab20e
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 2e32b7036c2538e73b46580e0f5f8f4979e8a685
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="log-on-tooa-windows-virtual-machine-using-hello-azure-portal"></a>Ouvrez une session sur tooa machine virtuelle de Windows à l’aide de hello portail Azure
Bonjour portail Azure, vous utilisez hello **Connect** bouton toostart une session de bureau à distance et les journaux sur tooa machine virtuelle Windows.

Voulez-vous tooconnect tooa Linux VM ? Consultez [comment toolog sur l’ordinateur virtuel de tooa exécutant Linux](../../linux/mac-create-ssh-keys.md).

<!--
Deleting, but not 100% sure
Learn how too[perform these steps using new Azure portal](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

> [!IMPORTANT]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello. Pour plus d’informations sur la façon dont toolog sur l’utilisation de machines virtuelles tooa hello Gestionnaire de ressources du modèle, consultez [ici](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="connect-toohello-virtual-machine"></a>Connecter l’ordinateur virtuel de toohello
1. Se connecter toohello portail Azure.
2. Cliquez sur l’ordinateur virtuel de hello que tooaccess. nom de Hello est répertorié dans hello **toutes les ressources** volet.

    ![Virtual-machine-locations](./media/connect-logon/azureportaldashboard.png)

3. Cliquez sur **Connect** sur la barre de commandes hello au-dessus du tableau de bord hello machine virtuelle.

    ![Icône pour l’ordinateur virtuel de hello de connexion](./media/connect-logon/virtualmachine_dashboard_connect.png)

<!-- Don't know if this still applies
     I think we can zap this.
> [!TIP]
> If hello **Connect** button isn't available, see hello troubleshooting tips at hello end of this article.
>
>
-->

## <a name="log-on-toohello-virtual-machine"></a>Ouvrez une session sur l’ordinateur virtuel de toohello
[!INCLUDE [virtual-machines-log-on-win-server](../../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a>Étapes suivantes
* Si hello **Connect** bouton est inactif ou que vous rencontrez d’autres problèmes de connexion Bureau à distance de hello, essayez de réinitialiser la configuration de hello. Cliquez sur **réinitialisez l’accès à distance** à partir du tableau de bord de machine virtuelle hello.

    ![Reset-remote-access](./media/connect-logon/virtualmachine_dashboard_reset_remote_access.png)

* Si votre mot de passe pose problème, essayez de le réinitialiser. Cliquez sur **réinitialisation de mot de passe** le long de hello bord gauche du tableau de bord de l’ordinateur virtuel, sous **prise en charge + dépannage**.

    ![Reset-password](./media/connect-logon/virtualmachine_dashboard_reset_password.png)

Si ces conseils ne fonctionnent pas ou ne sont pas de ce que vous avez besoin, consultez [tooa de connexions de résoudre les problèmes de bureau à distance basé sur Windows Azure Virtual Machine](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Cet article vous guide tout au long des opérations de diagnostic et de résolution des problèmes courants.
