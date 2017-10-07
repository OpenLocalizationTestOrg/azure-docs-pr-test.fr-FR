---
title: "aaaCreate une image personnalisée de Azure DevTest Labs à partir d’un fichier de disque dur virtuel | Documents Microsoft"
description: "Découvrez comment une image personnalisée dans Azure DevTest Labs à partir d’un fichier de disque dur virtuel à l’aide de toocreate hello portail Azure"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: b795bc61-7c28-40e6-82fc-96d629ee0568
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 80af8ea1cb72380f868df0a76c4a0dcd92e63cf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vhd-file"></a><span data-ttu-id="4e2d3-103">Créer une image personnalisée à partir d’un fichier de disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="4e2d3-103">Create a custom image from a VHD file</span></span>

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="4e2d3-104">Instructions pas à pas</span><span class="sxs-lookup"><span data-stu-id="4e2d3-104">Step-by-step instructions</span></span>

<span data-ttu-id="4e2d3-105">Hello étapes suivantes vous aider à créer une image personnalisée à partir d’un fichier de disque dur virtuel à l’aide de hello portail Azure :</span><span class="sxs-lookup"><span data-stu-id="4e2d3-105">hello following steps walk you through creating a custom image from a VHD file using hello Azure portal:</span></span>

1. <span data-ttu-id="4e2d3-106">Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="4e2d3-106">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="4e2d3-107">Sélectionnez **davantage de services**, puis sélectionnez **DevTest Labs** à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="4e2d3-107">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="4e2d3-108">Dans liste hello labs, sélectionnez lab souhaité de hello.</span><span class="sxs-lookup"><span data-stu-id="4e2d3-108">From hello list of labs, select hello desired lab.</span></span>  

1. <span data-ttu-id="4e2d3-109">Dans le panneau de hello lab, sélectionnez **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="4e2d3-109">On hello lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="4e2d3-110">Atelier de hello **Configuration** panneau, sélectionnez **les images personnalisées (VHD)**.</span><span class="sxs-lookup"><span data-stu-id="4e2d3-110">On hello lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="4e2d3-111">Sur hello **les images personnalisées** panneau, sélectionnez **+ ajouter**.</span><span class="sxs-lookup"><span data-stu-id="4e2d3-111">On hello **Custom images** blade, select **+Add**.</span></span>

    ![Ajouter une image personnalisée](./media/devtest-lab-create-template/add-custom-image.png)

1. <span data-ttu-id="4e2d3-113">Entrez le nom hello d’image personnalisée de hello.</span><span class="sxs-lookup"><span data-stu-id="4e2d3-113">Enter hello name of hello custom image.</span></span> <span data-ttu-id="4e2d3-114">Ce nom s’affiche dans la liste hello des images de base lors de la création d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="4e2d3-114">This name is displayed in hello list of base images when creating a VM.</span></span>

1. <span data-ttu-id="4e2d3-115">Entrez la description hello d’image personnalisée de hello.</span><span class="sxs-lookup"><span data-stu-id="4e2d3-115">Enter hello description of hello custom image.</span></span> <span data-ttu-id="4e2d3-116">Cette description s’affiche dans la liste hello des images de base lors de la création d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="4e2d3-116">This description is displayed in hello list of base images when creating a VM.</span></span>

1. <span data-ttu-id="4e2d3-117">Sélectionnez **VHD**.</span><span class="sxs-lookup"><span data-stu-id="4e2d3-117">Select **VHD**.</span></span>

1. <span data-ttu-id="4e2d3-118">À partir de hello **VHD** panneau, un fichier de disque dur virtuel sélectionnez hello souhaité.</span><span class="sxs-lookup"><span data-stu-id="4e2d3-118">From hello **VHD** blade, select hello desired VHD file.</span></span>

1. <span data-ttu-id="4e2d3-119">Sélectionnez **OK** tooclose hello **VHD** panneau.</span><span class="sxs-lookup"><span data-stu-id="4e2d3-119">Select **OK** tooclose hello **VHD** blade.</span></span>

1. <span data-ttu-id="4e2d3-120">Sélectionnez **Configuration du système d’exploitation**.</span><span class="sxs-lookup"><span data-stu-id="4e2d3-120">Select **OS configuration**.</span></span>

1. <span data-ttu-id="4e2d3-121">Sur hello **configuration du système d’exploitation** , sélectionnez soit **Windows** ou **Linux**.</span><span class="sxs-lookup"><span data-stu-id="4e2d3-121">On hello **OS configuration** tab, select either **Windows** or **Linux**.</span></span>

1. <span data-ttu-id="4e2d3-122">Si **Windows** est sélectionnée, spécifiez via la case à cocher hello si *Sysprep* a été exécuté sur l’ordinateur de hello.</span><span class="sxs-lookup"><span data-stu-id="4e2d3-122">If **Windows** is selected, specify via hello checkbox whether *Sysprep* has been run on hello machine.</span></span> 

1. <span data-ttu-id="4e2d3-123">Sélectionnez **OK** tooclose hello **configuration du système d’exploitation** panneau.</span><span class="sxs-lookup"><span data-stu-id="4e2d3-123">Select **OK** tooclose hello **OS configuration** blade.</span></span>

1. <span data-ttu-id="4e2d3-124">Sélectionnez **OK** image personnalisée de toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="4e2d3-124">Select **OK** toocreate hello custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="4e2d3-125">Billets de blog connexes</span><span class="sxs-lookup"><span data-stu-id="4e2d3-125">Related blog posts</span></span>

- [<span data-ttu-id="4e2d3-126">Custom images or formulas? (Images personnalisées ou formules ?)</span><span class="sxs-lookup"><span data-stu-id="4e2d3-126">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="4e2d3-127">Copying Custom Images between Azure DevTest Labs (Copie d’images personnalisées entre plusieurs Azure DevTest Labs)</span><span class="sxs-lookup"><span data-stu-id="4e2d3-127">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="4e2d3-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4e2d3-128">Next steps</span></span>

- [<span data-ttu-id="4e2d3-129">Ajouter un laboratoire tooyour de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="4e2d3-129">Add a VM tooyour lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
