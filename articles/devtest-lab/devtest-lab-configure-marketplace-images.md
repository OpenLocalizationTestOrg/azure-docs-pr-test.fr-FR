---
title: "paramètres d’image aaaConfigure Azure Marketplace dans Azure DevTest Labs | Documents Microsoft"
description: "Configurer quelles images Azure Marketplace peuvent être utilisées lors de la création d’une machine virtuelle dans Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 804c6af2-17e9-4320-af3a-f454bd398379
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: bb4b7f1c0cbe967bee724f7ee20f64f8c4ea58ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-marketplace-image-settings-in-azure-devtest-labs"></a><span data-ttu-id="e26be-103">Configuration des paramètres d’image Azure Marketplace dans Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="e26be-103">Configure Azure Marketplace image settings in Azure DevTest Labs</span></span>
<span data-ttu-id="e26be-104">DevTest Labs prend en charge la création de machines virtuelles basées sur des images Azure Marketplace en fonction de la façon dont vous avez configuré toobe d’images Azure Marketplace utilisé dans votre laboratoire.</span><span class="sxs-lookup"><span data-stu-id="e26be-104">DevTest Labs supports creating VMs based on Azure Marketplace images depending on how you have configured Azure Marketplace images toobe used in your lab.</span></span> <span data-ttu-id="e26be-105">Cet article vous montre comment toospecify qui, le cas échéant, les images Azure Marketplace peuvent être utilisés lors de la création de machines virtuelles dans un laboratoire.</span><span class="sxs-lookup"><span data-stu-id="e26be-105">This article shows you how toospecify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span> <span data-ttu-id="e26be-106">Cela garantit que votre équipe dispose uniquement des images de Marketplace toohello accès que dont ils ont besoin.</span><span class="sxs-lookup"><span data-stu-id="e26be-106">This ensures that your team only has access toohello Marketplace images they need.</span></span> 

## <a name="select-which-azure-marketplace-images-are-allowed-when-creating-a-vm"></a><span data-ttu-id="e26be-107">Sélection des images Azure Marketplace autorisées lors de la création d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e26be-107">Select which Azure Marketplace images are allowed when creating a VM</span></span>
1. <span data-ttu-id="e26be-108">Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="e26be-108">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="e26be-109">Sélectionnez **plus Services**, puis sélectionnez **DevTest Labs** à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="e26be-109">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="e26be-110">Dans liste hello labs, sélectionnez lab souhaité de hello.</span><span class="sxs-lookup"><span data-stu-id="e26be-110">From hello list of labs, select hello desired lab.</span></span> 
4. <span data-ttu-id="e26be-111">Dans le panneau de hello lab, sélectionnez **stratégies de Configuration et**.</span><span class="sxs-lookup"><span data-stu-id="e26be-111">On hello lab's blade, select **Configuration and policies**.</span></span>
5. <span data-ttu-id="e26be-112">Dans le panneau **Configuration et stratégies** du laboratoire, sous **Bases de machine virtuelle**, sélectionnez **Images de la Place de marché**.</span><span class="sxs-lookup"><span data-stu-id="e26be-112">On lab's **Configuration and policies** blade under **Virtual Machine Bases**, select **Marketplace images**.</span></span>
6. <span data-ttu-id="e26be-113">Spécifiez si vous souhaitez que tous les hello qualifié toobe images Azure Marketplace disponible pour une utilisation comme base d’une nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e26be-113">Specify whether you want all hello qualified Azure Marketplace images toobe available for use as a base of a new VM.</span></span> <span data-ttu-id="e26be-114">Si vous sélectionnez **Oui**, puis toutes les images d’Azure Marketplace hello qui remplissent toutes hello après les critères sont autorisés dans le laboratoire de hello :</span><span class="sxs-lookup"><span data-stu-id="e26be-114">If you select **Yes**, then all hello Azure Marketplace images that meet all hello following criteria are allowed in hello lab:</span></span>
   
   * <span data-ttu-id="e26be-115">image de Hello crée une seule machine virtuelle, **et**</span><span class="sxs-lookup"><span data-stu-id="e26be-115">hello image creates a single VM, **and**</span></span>
   * <span data-ttu-id="e26be-116">image de Hello utilise les machines virtuelles Azure Resource Manager tooprovision, **et**</span><span class="sxs-lookup"><span data-stu-id="e26be-116">hello image uses Azure Resource Manager tooprovision VMs, **and**</span></span>
   * <span data-ttu-id="e26be-117">image de Hello ne nécessite pas d’achat d’un régime de licences supplémentaires</span><span class="sxs-lookup"><span data-stu-id="e26be-117">hello image doesn't require purchasing an extra licensing plan</span></span>
     
    <span data-ttu-id="e26be-118">Si vous ne souhaitez aucun toobe images autorisé, ou vous souhaitez toospecify images qui peuvent être utilisées, sélectionnez **non**.</span><span class="sxs-lookup"><span data-stu-id="e26be-118">If you want no images toobe allowed, or you want toospecify which images can be used, select **No**.</span></span>
     
     ![Option tooallow toobe d’images Marketplace tous les utilisé en tant qu’images de base pour les machines virtuelles](./media/devtest-lab-configure-marketplace-images/allow-all-marketplace-images.png)
7. <span data-ttu-id="e26be-120">Si vous sélectionnez **non** toohello précédente étape, hello **autorisées images/sélectionner tous les** case à cocher est activée.</span><span class="sxs-lookup"><span data-stu-id="e26be-120">If you select **No** toohello previous step, hello **Allowed images/Select all** checkbox is enabled.</span></span> 
   <span data-ttu-id="e26be-121">Vous pouvez utiliser cette option avec recherche hello tooquickly Sélectionnez ou désélectionnez tous les éléments de hello affichés dans la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="e26be-121">You can use this option together with hello search box tooquickly select or deselect all hello items displayed in hello list.</span></span>
   * <span data-ttu-id="e26be-122">Sélectionnez hello Azure Marketplace images tooallow pour la création de la machine virtuelle individuellement en activant les cases à cocher correspondantes de chaque image.</span><span class="sxs-lookup"><span data-stu-id="e26be-122">Select hello Azure Marketplace images you want tooallow for VM creation individually by checking each image's corresponding checkbox.</span></span>
   * <span data-ttu-id="e26be-123">N’effectuez aucune sélection à partir de la liste de hello si vous ne souhaitez pas tooallow tout toobe d’images Azure Marketplace utilisé dans le laboratoire de hello.</span><span class="sxs-lookup"><span data-stu-id="e26be-123">Select nothing from hello list if you don't want tooallow any Azure Marketplace images toobe used in hello lab.</span></span>
   
    ![Vous pouvez spécifier les images Azure Marketplace pouvant être utilisées en tant qu’images de base pour des machines virtuelles](./media/devtest-lab-configure-marketplace-images/select-marketplace-images.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="e26be-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e26be-125">Next steps</span></span>
<span data-ttu-id="e26be-126">Une fois que vous avez configuré la façon dont les images Azure Marketplace sont autorisés lors de la création d’une machine virtuelle, étape suivante de hello est trop[ajouter un laboratoire tooyour de machine virtuelle](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="e26be-126">Once you have configured how Azure Marketplace images are allowed when creating a VM, hello next step is too[add a VM tooyour lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

