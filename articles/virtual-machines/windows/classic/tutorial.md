---
title: aaaCreate une machine virtuelle dans hello portail Azure | Documents Microsoft
description: "Créer une machine virtuelle Windows dans hello portail Azure."
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
ms.openlocfilehash: 3848a3d06a7ce377633db78ea385826ed40f94fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-running-windows-in-hello-azure-portal"></a><span data-ttu-id="8a86e-103">Créer une machine virtuelle exécutant Windows Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="8a86e-103">Create a virtual machine running Windows in hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8a86e-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="8a86e-104">Azure portal</span></span>](tutorial.md)
> * [<span data-ttu-id="8a86e-105">PowerShell : Déploiement classique</span><span class="sxs-lookup"><span data-stu-id="8a86e-105">PowerShell: Classic deployment</span></span>](create-powershell.md)
>
>

<br>

> [!IMPORTANT]
> <span data-ttu-id="8a86e-106">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="8a86e-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="8a86e-107">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="8a86e-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="8a86e-108">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="8a86e-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="8a86e-109">Découvrez comment trop[effectuer ces étapes à l’aide du modèle de déploiement du Gestionnaire de ressources hello](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) à l’aide de hello **portail Azure**.</span><span class="sxs-lookup"><span data-stu-id="8a86e-109">Learn how too[perform these steps using hello Resource Manager deployment model](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) using hello **Azure portal**.</span></span>

<span data-ttu-id="8a86e-110">Ce didacticiel vous montre comment toocreate Azure exécutant Windows Bonjour Azure portal de la machine virtuelle (VM).</span><span class="sxs-lookup"><span data-stu-id="8a86e-110">This tutorial shows you how toocreate an Azure virtual machine (VM) running Windows in hello Azure portal.</span></span> <span data-ttu-id="8a86e-111">Nous allons utiliser une image Windows Server par exemple, mais qui est simplement l’une de hello plusieurs images offres Azure.</span><span class="sxs-lookup"><span data-stu-id="8a86e-111">We'll use a Windows Server image as an example, but that's just one of hello many images Azure offers.</span></span> <span data-ttu-id="8a86e-112">Notez que votre choix en matière d’images dépend de votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="8a86e-112">Note that your image choices depend on your subscription.</span></span> <span data-ttu-id="8a86e-113">Par exemple, les images de bureau Windows peuvent être disponible tooMSDN abonnés.</span><span class="sxs-lookup"><span data-stu-id="8a86e-113">For example, Windows desktop images may be available tooMSDN subscribers.</span></span>

<span data-ttu-id="8a86e-114">Cette section vous montre comment toouse hello **tableau de bord** hello tooselect portail Azure et puis créer la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="8a86e-114">This section shows you how toouse hello **Dashboard** in hello Azure portal tooselect and then create hello virtual machine.</span></span>

<span data-ttu-id="8a86e-115">Vous pouvez également créer des machines virtuelles en utilisant [vos propres images](createupload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="8a86e-115">You can also create VMs using [your own images](createupload-vhd.md).</span></span> <span data-ttu-id="8a86e-116">toolearn à ce sujet et d’autres méthodes, consultez [toocreate de différentes manières une machine virtuelle Windows](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8a86e-116">toolearn about this and other methods, see [Different ways toocreate a Windows virtual machine](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<!-- 02/27/2017 Video removed as it was based on hello classic portal. -->

## <span data-ttu-id="8a86e-117"><a id="createvirtualmachine"></a>Créer la machine virtuelle de hello</span><span class="sxs-lookup"><span data-stu-id="8a86e-117"><a id="createvirtualmachine"> </a>Create hello virtual machine</span></span>
[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

## <a name="next-steps"></a><span data-ttu-id="8a86e-118">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8a86e-118">Next steps</span></span>
* <span data-ttu-id="8a86e-119">Découvrez comment trop[créer une machine virtuelle à l’aide du modèle de déploiement du Gestionnaire de ressources hello](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8a86e-119">Learn how too[create a VM using hello Resource Manager deployment model](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in hello Azure portal.</span></span>
* <span data-ttu-id="8a86e-120">Ouvrez une session sur l’ordinateur virtuel de toohello.</span><span class="sxs-lookup"><span data-stu-id="8a86e-120">Log on toohello virtual machine.</span></span> <span data-ttu-id="8a86e-121">Pour obtenir des instructions, consultez [ouvrir une session sur l’ordinateur virtuel de tooa exécutant Windows Server](connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="8a86e-121">For instructions, see [Log on tooa virtual machine running Windows Server](connect-logon.md).</span></span>
* <span data-ttu-id="8a86e-122">Attacher un toostore de données de disque.</span><span class="sxs-lookup"><span data-stu-id="8a86e-122">Attach a disk toostore data.</span></span> <span data-ttu-id="8a86e-123">Vous pouvez attacher des disques, qu'ils soient vides ou non.</span><span class="sxs-lookup"><span data-stu-id="8a86e-123">You can attach both empty disks and disks that contain data.</span></span> <span data-ttu-id="8a86e-124">Pour obtenir des instructions, consultez hello [attacher une machine virtuelle données disque tooa Windows créée avec le modèle de déploiement classique hello](attach-disk.md).</span><span class="sxs-lookup"><span data-stu-id="8a86e-124">For instructions, see hello [Attach a data disk tooa Windows virtual machine created with hello classic deployment model](attach-disk.md).</span></span>
