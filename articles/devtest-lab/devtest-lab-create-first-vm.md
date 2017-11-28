---
title: "aaaCreate votre première machine virtuelle dans un laboratoire dans Azure DevTest Labs | Documents Microsoft"
description: "Découvrez comment toocreate votre première machine virtuelle dans un laboratoire dans Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: fbc5a438-6e02-4952-b654-b8fa7322ae5f
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/24/2017
ms.author: tarcher
ms.openlocfilehash: 4c3257efca9be6fdd190eaac1db731464e07fcfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-vm-in-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="a5999-103">Créer votre première machine virtuelle dans un laboratoire dans Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="a5999-103">Create your first VM in a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="a5999-104">Lorsque vous initialement accéder DevTest Labs et toocreate votre première machine virtuelle, vous serez probablement faire à l’aide d’un préchargé [une image marketplace base](devtest-lab-configure-marketplace-images.md).</span><span class="sxs-lookup"><span data-stu-id="a5999-104">When you initially access DevTest Labs and want toocreate your first VM, you will likely do so using a pre-loaded [base marketplace image](devtest-lab-configure-marketplace-images.md).</span></span> <span data-ttu-id="a5999-105">Vous serez également en mesure de toochoose à partir d’un [image personnalisée et une formule](devtest-lab-add-vm.md) lors de la création de plusieurs machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="a5999-105">Later on, you'll also be able toochoose from a [custom image and a formula](devtest-lab-add-vm.md) when creating more VMs.</span></span> 

<span data-ttu-id="a5999-106">Ce didacticiel vous guide à l’aide de hello tooadd portail Azure votre premier atelier tooa de machine virtuelle DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="a5999-106">This tutorial walks you through using hello Azure portal tooadd your first VM tooa lab in DevTest Labs.</span></span>

## <a name="steps-tooadd-your-first-vm-tooa-lab-in-azure-devtest-labs"></a><span data-ttu-id="a5999-107">Les étapes tooadd votre premier atelier tooa de machine virtuelle dans Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="a5999-107">Steps tooadd your first VM tooa lab in Azure DevTest Labs</span></span>
1. <span data-ttu-id="a5999-108">Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="a5999-108">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="a5999-109">Sélectionnez **plus Services**, puis sélectionnez **DevTest Labs** à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="a5999-109">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
1. <span data-ttu-id="a5999-110">Dans liste hello labs, sélectionnez lab hello dans lequel vous souhaitez toocreate hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="a5999-110">From hello list of labs, select hello lab in which you want toocreate hello VM.</span></span>  
1. <span data-ttu-id="a5999-111">Sur du laboratoire hello **vue d’ensemble** panneau, sélectionnez **+ ajouter**.</span><span class="sxs-lookup"><span data-stu-id="a5999-111">On hello lab's **Overview** blade, select **+ Add**.</span></span>  

    ![Ajout du bouton de machine virtuelle](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. <span data-ttu-id="a5999-113">Sur hello **choisir une base** panneau, sélectionnez l’image d’une place de marché pour hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="a5999-113">On hello **Choose a base** blade, select a marketplace image for hello VM.</span></span>
1. <span data-ttu-id="a5999-114">Sur hello **virtuels** panneau, entrez un nom pour la machine virtuelle hello Bonjour **nom de machine virtuelle** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="a5999-114">On hello **Virtual machine** blade, enter a name for hello new virtual machine in hello **Virtual machine name** text box.</span></span>

    ![Panneau Machine virtuelle de laboratoire](./media/devtest-lab-add-vm/devtestlab-lab-add-first-vm.png)

1. <span data-ttu-id="a5999-116">Entrez un **nom d’utilisateur** qui dispose des privilèges d’administrateur sur l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="a5999-116">Enter a **User Name** that is granted administrator privileges on hello virtual machine.</span></span>  
1. <span data-ttu-id="a5999-117">Entrez un mot de passe dans le champ de texte hello étiqueté **une valeur de Type**.</span><span class="sxs-lookup"><span data-stu-id="a5999-117">Enter a password in hello text field labeled **Type a value**.</span></span>
1. <span data-ttu-id="a5999-118">Hello **type de disque de machine virtuelle** détermine le type de disque de stockage est autorisé pour les ordinateurs virtuels de hello dans le laboratoire de hello.</span><span class="sxs-lookup"><span data-stu-id="a5999-118">hello **Virtual machine disk type** determines which storage disk type is allowed for hello virtual machines in hello lab.</span></span>
1. <span data-ttu-id="a5999-119">Sélectionnez **taille de machine virtuelle** et sélectionnez une des hello prédéfinis des éléments qui spécifient les cœurs de processeur hello, la taille de mémoire RAM et taille du disque dur de hello VM toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="a5999-119">Select **Virtual machine size** and select one of hello predefined items that specify hello processor cores, RAM size, and hello hard drive size of hello VM toocreate.</span></span>
1. <span data-ttu-id="a5999-120">Sélectionnez **artefacts** - liste hello d’artefacts - sélectionner et configurer les artefacts hello que vous souhaitez l’image de base tooadd toohello.</span><span class="sxs-lookup"><span data-stu-id="a5999-120">Select **Artifacts** and - from hello list of artifacts - select and configure hello artifacts that you want tooadd toohello base image.</span></span>
    <span data-ttu-id="a5999-121">**Remarque :** si vous nouveaux laboratoires tooDevTest ou configuration des artefacts, consultez toohello [ajouter un tooa d’artefact existant VM](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) section, puis revenez ici une fois.</span><span class="sxs-lookup"><span data-stu-id="a5999-121">**Note:** If you're new tooDevTest Labs or configuring artifacts, refer toohello [Add an existing artifact tooa VM](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span></span>
1. <span data-ttu-id="a5999-122">Sélectionnez **créer** tooadd hello spécifié lab toohello de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="a5999-122">Select **Create** tooadd hello specified VM toohello lab.</span></span>

   <span data-ttu-id="a5999-123">Panneau de laboratoire Hello affiche hello statut de la création de la machine virtuelle hello - tout d’abord **création**, puis en tant que **en cours d’exécution** après hello machine virtuelle a été démarré.</span><span class="sxs-lookup"><span data-stu-id="a5999-123">hello lab blade displays hello status of hello VM's creation - first as **Creating**, then as **Running** after hello VM has been started.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a5999-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a5999-124">Next steps</span></span>
* <span data-ttu-id="a5999-125">Une fois hello machine virtuelle a été créé, vous pouvez vous connecter toohello machine virtuelle en sélectionnant **Connect** sur le panneau de la machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="a5999-125">Once hello VM has been created, you can connect toohello VM by selecting **Connect** on hello VM's blade.</span></span>
* <span data-ttu-id="a5999-126">Extraire [ajouter un laboratoire tooa de machine virtuelle](devtest-lab-add-vm.md) pour des informations plus complètes sur l’ajout de machines virtuelles suivantes dans votre laboratoire.</span><span class="sxs-lookup"><span data-stu-id="a5999-126">Check out [Add a VM tooa lab](devtest-lab-add-vm.md) for more complete info about adding subsequent VMs in your lab.</span></span>
* <span data-ttu-id="a5999-127">Explorer hello [galerie de modèles de DevTest Labs Azure Resource Manager QuickStart](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates).</span><span class="sxs-lookup"><span data-stu-id="a5999-127">Explore hello [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates).</span></span>
