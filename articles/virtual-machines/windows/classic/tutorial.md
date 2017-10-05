---
title: "Créer une machine virtuelle sur le Portail Azure | Microsoft Docs"
description: "Création d'une machine virtuelle Windows dans le portail Azure."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1871f823-ebd7-4eff-9a22-8e2411555595
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 0981872ff819fdf49a9cc97afce3c212013ce76b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-machine-running-windows-in-the-azure-portal"></a><span data-ttu-id="fe7ab-103">Créer une machine virtuelle exécutant Windows dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="fe7ab-103">Create a virtual machine running Windows in the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fe7ab-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="fe7ab-104">Azure portal</span></span>](tutorial.md)
> * [<span data-ttu-id="fe7ab-105">PowerShell : Déploiement classique</span><span class="sxs-lookup"><span data-stu-id="fe7ab-105">PowerShell: Classic deployment</span></span>](create-powershell.md)
>
>

<br>

> [!IMPORTANT]
> <span data-ttu-id="fe7ab-106">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="fe7ab-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="fe7ab-107">Cet article traite du modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="fe7ab-107">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="fe7ab-108">Pour la plupart des nouveaux déploiements, Microsoft recommande d’utiliser le modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fe7ab-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="fe7ab-109">Découvrez comment [suivre ces étapes à l’aide du modèle de déploiement Resource Manager](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) à l’aide du **Portail Azure**.</span><span class="sxs-lookup"><span data-stu-id="fe7ab-109">Learn how to [perform these steps using the Resource Manager deployment model](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) using the **Azure portal**.</span></span>

<span data-ttu-id="fe7ab-110">Ce didacticiel vous montre comment créer une machine virtuelle Azure exécutant Windows sur le Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fe7ab-110">This tutorial shows you how to create an Azure virtual machine (VM) running Windows in the Azure portal.</span></span> <span data-ttu-id="fe7ab-111">Nous allons utiliser une image Windows Server comme exemple, mais il s’agit simplement d’un des nombreux types d’images proposés par Azure.</span><span class="sxs-lookup"><span data-stu-id="fe7ab-111">We'll use a Windows Server image as an example, but that's just one of the many images Azure offers.</span></span> <span data-ttu-id="fe7ab-112">Notez que votre choix en matière d’images dépend de votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="fe7ab-112">Note that your image choices depend on your subscription.</span></span> <span data-ttu-id="fe7ab-113">Par exemple, les images de bureau Windows peuvent être accessibles aux abonnés MSDN.</span><span class="sxs-lookup"><span data-stu-id="fe7ab-113">For example, Windows desktop images may be available to MSDN subscribers.</span></span>

<span data-ttu-id="fe7ab-114">Cette section vous montre comment utiliser le **Tableau de bord** sur le Portail Azure pour sélectionner, puis créer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="fe7ab-114">This section shows you how to use the **Dashboard** in the Azure portal to select and then create the virtual machine.</span></span>

<span data-ttu-id="fe7ab-115">Vous pouvez également créer des machines virtuelles en utilisant [vos propres images](createupload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="fe7ab-115">You can also create VMs using [your own images](createupload-vhd.md).</span></span> <span data-ttu-id="fe7ab-116">Pour en savoir plus à ce sujet et connaître d’autres méthodes, consultez [les différentes façons de créer une machine virtuelle Windows](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fe7ab-116">To learn about this and other methods, see [Different ways to create a Windows virtual machine](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<!-- 02/27/2017 Video removed as it was based on the classic portal. -->

## <span data-ttu-id="fe7ab-117"><a id="createvirtualmachine"> </a>Créer la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="fe7ab-117"><a id="createvirtualmachine"> </a>Create the virtual machine</span></span>
[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

## <a name="next-steps"></a><span data-ttu-id="fe7ab-118">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fe7ab-118">Next steps</span></span>
* <span data-ttu-id="fe7ab-119">Découvrez comment [créer une machine virtuelle à l’aide du modèle de déploiement Resource Manager](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) sur le Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fe7ab-119">Learn how to [create a VM using the Resource Manager deployment model](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in the Azure portal.</span></span>
* <span data-ttu-id="fe7ab-120">Connectez-vous à votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="fe7ab-120">Log on to the virtual machine.</span></span> <span data-ttu-id="fe7ab-121">Pour obtenir des instructions, consultez [Connexion à une machine virtuelle exécutant Windows Server](connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="fe7ab-121">For instructions, see [Log on to a virtual machine running Windows Server](connect-logon.md).</span></span>
* <span data-ttu-id="fe7ab-122">Attacher un disque pour stocker des données.</span><span class="sxs-lookup"><span data-stu-id="fe7ab-122">Attach a disk to store data.</span></span> <span data-ttu-id="fe7ab-123">Vous pouvez attacher des disques, qu'ils soient vides ou non.</span><span class="sxs-lookup"><span data-stu-id="fe7ab-123">You can attach both empty disks and disks that contain data.</span></span> <span data-ttu-id="fe7ab-124">Pour obtenir des instructions, consultez la page [Attacher un disque de données à une machine virtuelle Windows créée avec le modèle de déploiement Classic](attach-disk.md).</span><span class="sxs-lookup"><span data-stu-id="fe7ab-124">For instructions, see the [Attach a data disk to a Windows virtual machine created with the classic deployment model](attach-disk.md).</span></span>
