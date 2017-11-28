---
title: "Créer une image personnalisée Azure DevTest Labs à partir d’une machine virtuelle | Microsoft Docs"
description: "Découvrez comment créer une image personnalisée dans Azure DevTest Labs à partir d’une machine virtuelle approvisionnée à l’aide du portail Azure"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 9d2dcf7164985508d691e8a0c123efaf3b8aa19a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-image-from-a-vm"></a><span data-ttu-id="7ca10-103">Créer une image personnalisée à partir d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="7ca10-103">Create a custom image from a VM</span></span>

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="7ca10-104">Instructions pas à pas</span><span class="sxs-lookup"><span data-stu-id="7ca10-104">Step-by-step instructions</span></span>

<span data-ttu-id="7ca10-105">Vous pouvez créer une image personnalisée à partir d’une machine virtuelle approvisionnée et ensuite utiliser cette image personnalisée pour créer d’autres machines virtuelles identiques.</span><span class="sxs-lookup"><span data-stu-id="7ca10-105">You can create a custom image from a provisioned VM, and afterwards use that custom image to create identical VMs.</span></span> <span data-ttu-id="7ca10-106">Les étapes suivantes expliquent comment créer une image personnalisée à partir d’une machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="7ca10-106">The following steps illustrate how to create a custom image from a VM:</span></span>

1. <span data-ttu-id="7ca10-107">Connectez-vous au [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="7ca10-107">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="7ca10-108">Sélectionnez **Plus de services**, puis **DevTest Labs** dans la liste.</span><span class="sxs-lookup"><span data-stu-id="7ca10-108">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="7ca10-109">Sélectionnez le laboratoire souhaité dans la liste des laboratoires.</span><span class="sxs-lookup"><span data-stu-id="7ca10-109">From the list of labs, select the desired lab.</span></span>  

1. <span data-ttu-id="7ca10-110">Sur le panneau du laboratoire, sélectionnez **Mes machines virtuelles**.</span><span class="sxs-lookup"><span data-stu-id="7ca10-110">On the lab's blade, select **My virtual machines**.</span></span>
 
1. <span data-ttu-id="7ca10-111">Dans le panneau **Mes machines virtuelles** du laboratoire, sélectionnez la machine virtuelle à partir de laquelle vous souhaitez créer l’image personnalisée.</span><span class="sxs-lookup"><span data-stu-id="7ca10-111">On the **My virtual machines** blade, select the VM from which you want to create the custom image.</span></span>

1. <span data-ttu-id="7ca10-112">Sur le panneau de la machine virtuelle, sélectionnez **Créer une image personnalisée (VHD)**.</span><span class="sxs-lookup"><span data-stu-id="7ca10-112">On the VM's blade, select **Create custom image (VHD)**.</span></span>

    ![Élément de menu Créer une image personnalisée](./media/devtest-lab-create-template/create-custom-image.png)

1. <span data-ttu-id="7ca10-114">Dans le panneau **Créer une image** , entrez un nom et une description pour votre image personnalisée.</span><span class="sxs-lookup"><span data-stu-id="7ca10-114">On the **Create image** blade, enter a name and description for your custom image.</span></span> <span data-ttu-id="7ca10-115">Ces informations s’affichent dans la liste de bases lorsque vous créez une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7ca10-115">This information is displayed in the list of bases when you create a VM.</span></span>

    ![Panneau Créer une image personnalisée](./media/devtest-lab-create-template/create-custom-image-blade.png)

1. <span data-ttu-id="7ca10-117">Choisissez si sysprep a été exécuté sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7ca10-117">Select whether sysprep was run on the VM.</span></span> <span data-ttu-id="7ca10-118">Si sysprep n’a pas été exécuté sur la machine virtuelle, sélectionnez si vous souhaitez exécuter sysprep lorsqu’une machine virtuelle est créée à partir de cette image personnalisée.</span><span class="sxs-lookup"><span data-stu-id="7ca10-118">If the sysprep was not run on the VM, specify whether you want sysprep run when a VM is created from this custom image.</span></span>

1. <span data-ttu-id="7ca10-119">Cliquez sur **OK** lorsque vous avez terminé de créer l’image personnalisée.</span><span class="sxs-lookup"><span data-stu-id="7ca10-119">Select **OK** when finished to create the custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="7ca10-120">Billets de blog connexes</span><span class="sxs-lookup"><span data-stu-id="7ca10-120">Related blog posts</span></span>

- [<span data-ttu-id="7ca10-121">Custom images or formulas? (Images personnalisées ou formules ?)</span><span class="sxs-lookup"><span data-stu-id="7ca10-121">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="7ca10-122">Copying Custom Images between Azure DevTest Labs (Copie d’images personnalisées entre plusieurs Azure DevTest Labs)</span><span class="sxs-lookup"><span data-stu-id="7ca10-122">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="7ca10-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7ca10-123">Next steps</span></span>

- [<span data-ttu-id="7ca10-124">Ajout d’une machine virtuelle à votre laboratoire</span><span class="sxs-lookup"><span data-stu-id="7ca10-124">Add a VM to your lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
