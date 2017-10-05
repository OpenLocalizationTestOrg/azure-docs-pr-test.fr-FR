---
title: Ouvrir une session sur une machine virtuelle Azure Classic | Microsoft Docs
description: "Utilisez le Portail Azure pour vous connecter à une machine virtuelle Windows créée avec le modèle de déploiement classique."
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
ms.openlocfilehash: 43d54de7e875de9212c23c49ad0539bf2272a312
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="log-on-to-a-windows-virtual-machine-using-the-azure-portal"></a><span data-ttu-id="d6619-103">Ouvrir une session sur une machine virtuelle Windows à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="d6619-103">Log on to a Windows virtual machine using the Azure portal</span></span>
<span data-ttu-id="d6619-104">Sur le portail Azure, vous utilisez le bouton **Connecter** pour démarrer une session Bureau à distance et ouvrir une session sur une machine virtuelle Windows.</span><span class="sxs-lookup"><span data-stu-id="d6619-104">In the Azure portal, you use the **Connect** button to start a Remote Desktop session and log on to a Windows VM.</span></span>

<span data-ttu-id="d6619-105">Vous souhaitez vous connecter à une machine virtuelle Linux ?</span><span class="sxs-lookup"><span data-stu-id="d6619-105">Do you want to connect to a Linux VM?</span></span> <span data-ttu-id="d6619-106">Consultez [Connexion à une machine virtuelle sous Linux](../../linux/mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="d6619-106">See [How to log on to a virtual machine running Linux](../../linux/mac-create-ssh-keys.md).</span></span>

<!--
Deleting, but not 100% sure
Learn how to [perform these steps using new Azure portal](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

> [!IMPORTANT]
> <span data-ttu-id="d6619-107">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d6619-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d6619-108">Cet article traite du modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="d6619-108">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="d6619-109">Pour la plupart des nouveaux déploiements, Microsoft recommande d’utiliser le modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d6619-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="d6619-110">Pour plus d’informations sur la connexion à une machine virtuelle avec le modèle Resource Manager, suivez [ce lien](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d6619-110">For information about how to log on to a VM using the Resource Manager model, see [here](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="connect-to-the-virtual-machine"></a><span data-ttu-id="d6619-111">Connectez-vous à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d6619-111">Connect to the virtual machine</span></span>
1. <span data-ttu-id="d6619-112">Connectez-vous au portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d6619-112">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="d6619-113">Cliquez sur la machine virtuelle à laquelle vous souhaitez accéder.</span><span class="sxs-lookup"><span data-stu-id="d6619-113">Click on the virtual machine that you want to access.</span></span> <span data-ttu-id="d6619-114">Le nom est répertorié dans le volet **Toutes les ressources**.</span><span class="sxs-lookup"><span data-stu-id="d6619-114">The name is listed in the **All resources** pane.</span></span>

    ![Virtual-machine-locations](./media/connect-logon/azureportaldashboard.png)

3. <span data-ttu-id="d6619-116">Cliquez sur **Connexion** dans la barre de commandes en haut du tableau de bord de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d6619-116">Click **Connect** on the command bar atop the virtual machine dashboard.</span></span>

    ![Icône Connexion de la machine virtuelle](./media/connect-logon/virtualmachine_dashboard_connect.png)

<!-- Don't know if this still applies
     I think we can zap this.
> [!TIP]
> If the **Connect** button isn't available, see the troubleshooting tips at the end of this article.
>
>
-->

## <a name="log-on-to-the-virtual-machine"></a><span data-ttu-id="d6619-118">Connexion à la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="d6619-118">Log on to the virtual machine</span></span>
[!INCLUDE [virtual-machines-log-on-win-server](../../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a><span data-ttu-id="d6619-119">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d6619-119">Next steps</span></span>
* <span data-ttu-id="d6619-120">Si le bouton **Connexion** est inactif ou que vous rencontrez d’autres problèmes avec la connexion Bureau à distance, essayez de réinitialiser la configuration.</span><span class="sxs-lookup"><span data-stu-id="d6619-120">If the **Connect** button is inactive or you are having other problems with the Remote Desktop connection, try resetting the configuration.</span></span> <span data-ttu-id="d6619-121">Dans le tableau de bord de la machine virtuelle, cliquez sur **Réinitialiser la configuration à distance**.</span><span class="sxs-lookup"><span data-stu-id="d6619-121">click **Reset remote access** from the virtual machine dashboard.</span></span>

    ![Reset-remote-access](./media/connect-logon/virtualmachine_dashboard_reset_remote_access.png)

* <span data-ttu-id="d6619-123">Si votre mot de passe pose problème, essayez de le réinitialiser.</span><span class="sxs-lookup"><span data-stu-id="d6619-123">For problems with your password, try resetting it.</span></span> <span data-ttu-id="d6619-124">Cliquez sur **Réinitialiser le mot de passe** le long du bord gauche de du tableau de bord de la machine virtuelle, sous **Support + dépannage**.</span><span class="sxs-lookup"><span data-stu-id="d6619-124">Click **Reset password** along the left edge of virtual machine dashboard, under **Support + Troubleshooting**.</span></span>

    ![Reset-password](./media/connect-logon/virtualmachine_dashboard_reset_password.png)

<span data-ttu-id="d6619-126">Si ces conseils ne donnent aucun résultat ou ne vous sont pas utiles, consultez [Résolution des problèmes de connexion du Bureau à distance à une machine virtuelle Azure sous Windows](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d6619-126">If those tips don't work or aren't what you need, see [Troubleshoot Remote Desktop connections to a Windows-based Azure Virtual Machine](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="d6619-127">Cet article vous guide tout au long des opérations de diagnostic et de résolution des problèmes courants.</span><span class="sxs-lookup"><span data-stu-id="d6619-127">This article walks you through diagnosing and resolving common problems.</span></span>
