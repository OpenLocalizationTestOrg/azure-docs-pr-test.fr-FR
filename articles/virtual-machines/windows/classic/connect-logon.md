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
# <a name="log-on-tooa-windows-virtual-machine-using-hello-azure-portal"></a><span data-ttu-id="0c225-103">Ouvrez une session sur tooa machine virtuelle de Windows à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="0c225-103">Log on tooa Windows virtual machine using hello Azure portal</span></span>
<span data-ttu-id="0c225-104">Bonjour portail Azure, vous utilisez hello **Connect** bouton toostart une session de bureau à distance et les journaux sur tooa machine virtuelle Windows.</span><span class="sxs-lookup"><span data-stu-id="0c225-104">In hello Azure portal, you use hello **Connect** button toostart a Remote Desktop session and log on tooa Windows VM.</span></span>

<span data-ttu-id="0c225-105">Voulez-vous tooconnect tooa Linux VM ?</span><span class="sxs-lookup"><span data-stu-id="0c225-105">Do you want tooconnect tooa Linux VM?</span></span> <span data-ttu-id="0c225-106">Consultez [comment toolog sur l’ordinateur virtuel de tooa exécutant Linux](../../linux/mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="0c225-106">See [How toolog on tooa virtual machine running Linux](../../linux/mac-create-ssh-keys.md).</span></span>

<!--
Deleting, but not 100% sure
Learn how too[perform these steps using new Azure portal](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

> [!IMPORTANT]
> <span data-ttu-id="0c225-107">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="0c225-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="0c225-108">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="0c225-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="0c225-109">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="0c225-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="0c225-110">Pour plus d’informations sur la façon dont toolog sur l’utilisation de machines virtuelles tooa hello Gestionnaire de ressources du modèle, consultez [ici](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0c225-110">For information about how toolog on tooa VM using hello Resource Manager model, see [here](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="0c225-111">Connecter l’ordinateur virtuel de toohello</span><span class="sxs-lookup"><span data-stu-id="0c225-111">Connect toohello virtual machine</span></span>
1. <span data-ttu-id="0c225-112">Se connecter toohello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0c225-112">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="0c225-113">Cliquez sur l’ordinateur virtuel de hello que tooaccess.</span><span class="sxs-lookup"><span data-stu-id="0c225-113">Click on hello virtual machine that you want tooaccess.</span></span> <span data-ttu-id="0c225-114">nom de Hello est répertorié dans hello **toutes les ressources** volet.</span><span class="sxs-lookup"><span data-stu-id="0c225-114">hello name is listed in hello **All resources** pane.</span></span>

    ![Virtual-machine-locations](./media/connect-logon/azureportaldashboard.png)

3. <span data-ttu-id="0c225-116">Cliquez sur **Connect** sur la barre de commandes hello au-dessus du tableau de bord hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="0c225-116">Click **Connect** on hello command bar atop hello virtual machine dashboard.</span></span>

    ![Icône pour l’ordinateur virtuel de hello de connexion](./media/connect-logon/virtualmachine_dashboard_connect.png)

<!-- Don't know if this still applies
     I think we can zap this.
> [!TIP]
> If hello **Connect** button isn't available, see hello troubleshooting tips at hello end of this article.
>
>
-->

## <a name="log-on-toohello-virtual-machine"></a><span data-ttu-id="0c225-118">Ouvrez une session sur l’ordinateur virtuel de toohello</span><span class="sxs-lookup"><span data-stu-id="0c225-118">Log on toohello virtual machine</span></span>
[!INCLUDE [virtual-machines-log-on-win-server](../../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a><span data-ttu-id="0c225-119">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0c225-119">Next steps</span></span>
* <span data-ttu-id="0c225-120">Si hello **Connect** bouton est inactif ou que vous rencontrez d’autres problèmes de connexion Bureau à distance de hello, essayez de réinitialiser la configuration de hello.</span><span class="sxs-lookup"><span data-stu-id="0c225-120">If hello **Connect** button is inactive or you are having other problems with hello Remote Desktop connection, try resetting hello configuration.</span></span> <span data-ttu-id="0c225-121">Cliquez sur **réinitialisez l’accès à distance** à partir du tableau de bord de machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="0c225-121">click **Reset remote access** from hello virtual machine dashboard.</span></span>

    ![Reset-remote-access](./media/connect-logon/virtualmachine_dashboard_reset_remote_access.png)

* <span data-ttu-id="0c225-123">Si votre mot de passe pose problème, essayez de le réinitialiser.</span><span class="sxs-lookup"><span data-stu-id="0c225-123">For problems with your password, try resetting it.</span></span> <span data-ttu-id="0c225-124">Cliquez sur **réinitialisation de mot de passe** le long de hello bord gauche du tableau de bord de l’ordinateur virtuel, sous **prise en charge + dépannage**.</span><span class="sxs-lookup"><span data-stu-id="0c225-124">Click **Reset password** along hello left edge of virtual machine dashboard, under **Support + Troubleshooting**.</span></span>

    ![Reset-password](./media/connect-logon/virtualmachine_dashboard_reset_password.png)

<span data-ttu-id="0c225-126">Si ces conseils ne fonctionnent pas ou ne sont pas de ce que vous avez besoin, consultez [tooa de connexions de résoudre les problèmes de bureau à distance basé sur Windows Azure Virtual Machine](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0c225-126">If those tips don't work or aren't what you need, see [Troubleshoot Remote Desktop connections tooa Windows-based Azure Virtual Machine](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="0c225-127">Cet article vous guide tout au long des opérations de diagnostic et de résolution des problèmes courants.</span><span class="sxs-lookup"><span data-stu-id="0c225-127">This article walks you through diagnosing and resolving common problems.</span></span>
