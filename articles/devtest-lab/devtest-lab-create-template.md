---
title: "Créer une image personnalisée Azure DevTest Labs à partir d’un fichier de disque dur virtuel | Microsoft Docs"
description: "Apprenez à créer une image personnalisée dans Azure DevTest Labs à partir d’un fichier de disque dur virtuel à l’aide du portail Azure"
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
ms.openlocfilehash: 9983ea9b847f44ed18a6169a4bdb224b63626a64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-image-from-a-vhd-file"></a><span data-ttu-id="f46fb-103">Créer une image personnalisée à partir d’un fichier de disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="f46fb-103">Create a custom image from a VHD file</span></span>

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="f46fb-104">Instructions pas à pas</span><span class="sxs-lookup"><span data-stu-id="f46fb-104">Step-by-step instructions</span></span>

<span data-ttu-id="f46fb-105">La procédure suivante décrit comment créer une image personnalisée à partir d’un fichier de disque dur virtuel avec le portail Azure :</span><span class="sxs-lookup"><span data-stu-id="f46fb-105">The following steps walk you through creating a custom image from a VHD file using the Azure portal:</span></span>

1. <span data-ttu-id="f46fb-106">Connectez-vous au [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="f46fb-106">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="f46fb-107">Sélectionnez **Plus de services**, puis **DevTest Labs** dans la liste.</span><span class="sxs-lookup"><span data-stu-id="f46fb-107">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="f46fb-108">Sélectionnez le laboratoire souhaité dans la liste des laboratoires.</span><span class="sxs-lookup"><span data-stu-id="f46fb-108">From the list of labs, select the desired lab.</span></span>  

1. <span data-ttu-id="f46fb-109">Dans le panneau du laboratoire, sélectionnez **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="f46fb-109">On the lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="f46fb-110">Dans le panneau **Configuration** du laboratoire, sélectionnez **Custom images (VHDs)** (Images personnalisées (disques durs virtuels)).</span><span class="sxs-lookup"><span data-stu-id="f46fb-110">On the lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="f46fb-111">Dans le panneau **Images personnalisées**, sélectionnez **+Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f46fb-111">On the **Custom images** blade, select **+Add**.</span></span>

    ![Ajouter une image personnalisée](./media/devtest-lab-create-template/add-custom-image.png)

1. <span data-ttu-id="f46fb-113">Entrez le nom de l’image personnalisée.</span><span class="sxs-lookup"><span data-stu-id="f46fb-113">Enter the name of the custom image.</span></span> <span data-ttu-id="f46fb-114">Ce nom s’affiche dans la liste des images de base quand vous créez une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f46fb-114">This name is displayed in the list of base images when creating a VM.</span></span>

1. <span data-ttu-id="f46fb-115">Entrez la description de l’image personnalisée.</span><span class="sxs-lookup"><span data-stu-id="f46fb-115">Enter the description of the custom image.</span></span> <span data-ttu-id="f46fb-116">Cette description s’affiche dans la liste des images de base quand vous créez une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f46fb-116">This description is displayed in the list of base images when creating a VM.</span></span>

1. <span data-ttu-id="f46fb-117">Sélectionnez **VHD**.</span><span class="sxs-lookup"><span data-stu-id="f46fb-117">Select **VHD**.</span></span>

1. <span data-ttu-id="f46fb-118">Dans le panneau **VHD**, sélectionnez le fichier de disque dur virtuel souhaité.</span><span class="sxs-lookup"><span data-stu-id="f46fb-118">From the **VHD** blade, select the desired VHD file.</span></span>

1. <span data-ttu-id="f46fb-119">Cliquez sur **OK** pour fermer le panneau **VHD**.</span><span class="sxs-lookup"><span data-stu-id="f46fb-119">Select **OK** to close the **VHD** blade.</span></span>

1. <span data-ttu-id="f46fb-120">Sélectionnez **Configuration du système d’exploitation**.</span><span class="sxs-lookup"><span data-stu-id="f46fb-120">Select **OS configuration**.</span></span>

1. <span data-ttu-id="f46fb-121">Sous l’onglet **Configuration du système d’exploitation**, sélectionnez **Windows** ou **Linux**.</span><span class="sxs-lookup"><span data-stu-id="f46fb-121">On the **OS configuration** tab, select either **Windows** or **Linux**.</span></span>

1. <span data-ttu-id="f46fb-122">Si vous sélectionnez **Windows** , cochez la case pour indiquer si *Sysprep* a été exécuté sur la machine.</span><span class="sxs-lookup"><span data-stu-id="f46fb-122">If **Windows** is selected, specify via the checkbox whether *Sysprep* has been run on the machine.</span></span> 

1. <span data-ttu-id="f46fb-123">Cliquez sur **OK** pour fermer le panneau **Configuration du système d’exploitation**.</span><span class="sxs-lookup"><span data-stu-id="f46fb-123">Select **OK** to close the **OS configuration** blade.</span></span>

1. <span data-ttu-id="f46fb-124">Cliquez sur **OK** pour créer l’image personnalisée.</span><span class="sxs-lookup"><span data-stu-id="f46fb-124">Select **OK** to create the custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="f46fb-125">Billets de blog connexes</span><span class="sxs-lookup"><span data-stu-id="f46fb-125">Related blog posts</span></span>

- [<span data-ttu-id="f46fb-126">Custom images or formulas? (Images personnalisées ou formules ?)</span><span class="sxs-lookup"><span data-stu-id="f46fb-126">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="f46fb-127">Copying Custom Images between Azure DevTest Labs (Copie d’images personnalisées entre plusieurs Azure DevTest Labs)</span><span class="sxs-lookup"><span data-stu-id="f46fb-127">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="f46fb-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f46fb-128">Next steps</span></span>

- [<span data-ttu-id="f46fb-129">Ajout d’une machine virtuelle à votre laboratoire</span><span class="sxs-lookup"><span data-stu-id="f46fb-129">Add a VM to your lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
