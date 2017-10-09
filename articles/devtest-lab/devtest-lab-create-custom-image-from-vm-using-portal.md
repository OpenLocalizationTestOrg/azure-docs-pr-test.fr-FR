---
title: "aaaCreate une image personnalisée de Azure DevTest Labs à partir d’une machine virtuelle | Documents Microsoft"
description: "Découvrez comment une image personnalisée dans Azure DevTest Labs à partir d’une machine virtuelle configurés à l’aide de toocreate hello portail Azure"
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
ms.openlocfilehash: 7dccb79d3db4aae676c7bd2f6b800301210491e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vm"></a><span data-ttu-id="47ac8-103">Créer une image personnalisée à partir d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="47ac8-103">Create a custom image from a VM</span></span>

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="47ac8-104">Instructions pas à pas</span><span class="sxs-lookup"><span data-stu-id="47ac8-104">Step-by-step instructions</span></span>

<span data-ttu-id="47ac8-105">Vous pouvez créer une image personnalisée à partir d’une machine virtuelle configurée et ensuite utiliser cette image personnalisée de toocreate machines virtuelles identiques.</span><span class="sxs-lookup"><span data-stu-id="47ac8-105">You can create a custom image from a provisioned VM, and afterwards use that custom image toocreate identical VMs.</span></span> <span data-ttu-id="47ac8-106">Hello suit illustre comment toocreate personnalisé de l’image à partir d’une machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="47ac8-106">hello following steps illustrate how toocreate a custom image from a VM:</span></span>

1. <span data-ttu-id="47ac8-107">Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="47ac8-107">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="47ac8-108">Sélectionnez **davantage de services**, puis sélectionnez **DevTest Labs** à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="47ac8-108">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="47ac8-109">Dans liste hello labs, sélectionnez lab souhaité de hello.</span><span class="sxs-lookup"><span data-stu-id="47ac8-109">From hello list of labs, select hello desired lab.</span></span>  

1. <span data-ttu-id="47ac8-110">Dans le panneau de hello lab, sélectionnez **mes machines virtuelles**.</span><span class="sxs-lookup"><span data-stu-id="47ac8-110">On hello lab's blade, select **My virtual machines**.</span></span>
 
1. <span data-ttu-id="47ac8-111">Sur hello **mes machines virtuelles** panneau, sélectionnez hello machine virtuelle à partir de laquelle image personnalisée de toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="47ac8-111">On hello **My virtual machines** blade, select hello VM from which you want toocreate hello custom image.</span></span>

1. <span data-ttu-id="47ac8-112">Dans le panneau de la machine virtuelle de hello, sélectionnez **créer une image personnalisée (VHD)**.</span><span class="sxs-lookup"><span data-stu-id="47ac8-112">On hello VM's blade, select **Create custom image (VHD)**.</span></span>

    ![Élément de menu Créer une image personnalisée](./media/devtest-lab-create-template/create-custom-image.png)

1. <span data-ttu-id="47ac8-114">Sur hello **créer une image** panneau, entrez un nom et une description pour votre image personnalisée.</span><span class="sxs-lookup"><span data-stu-id="47ac8-114">On hello **Create image** blade, enter a name and description for your custom image.</span></span> <span data-ttu-id="47ac8-115">Ces informations s’affichent dans la liste hello des bases lorsque vous créez une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="47ac8-115">This information is displayed in hello list of bases when you create a VM.</span></span>

    ![Panneau Créer une image personnalisée](./media/devtest-lab-create-template/create-custom-image-blade.png)

1. <span data-ttu-id="47ac8-117">Déterminez si sysprep a été exécutée sur la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="47ac8-117">Select whether sysprep was run on hello VM.</span></span> <span data-ttu-id="47ac8-118">Si sysprep de hello n’a pas été exécutée sur la machine virtuelle de hello, spécifiez si vous souhaitez que sysprep s’exécuter quand une machine virtuelle est créée à partir de cette image personnalisée.</span><span class="sxs-lookup"><span data-stu-id="47ac8-118">If hello sysprep was not run on hello VM, specify whether you want sysprep run when a VM is created from this custom image.</span></span>

1. <span data-ttu-id="47ac8-119">Sélectionnez **OK** lorsque toocreate terminé hello image personnalisée.</span><span class="sxs-lookup"><span data-stu-id="47ac8-119">Select **OK** when finished toocreate hello custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="47ac8-120">Billets de blog connexes</span><span class="sxs-lookup"><span data-stu-id="47ac8-120">Related blog posts</span></span>

- [<span data-ttu-id="47ac8-121">Custom images or formulas? (Images personnalisées ou formules ?)</span><span class="sxs-lookup"><span data-stu-id="47ac8-121">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="47ac8-122">Copying Custom Images between Azure DevTest Labs (Copie d’images personnalisées entre plusieurs Azure DevTest Labs)</span><span class="sxs-lookup"><span data-stu-id="47ac8-122">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="47ac8-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="47ac8-123">Next steps</span></span>

- [<span data-ttu-id="47ac8-124">Ajouter un laboratoire tooyour de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="47ac8-124">Add a VM tooyour lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
