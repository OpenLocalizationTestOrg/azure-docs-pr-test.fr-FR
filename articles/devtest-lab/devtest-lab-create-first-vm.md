---
title: "Créer votre première machine virtuelle dans un laboratoire dans Azure DevTest Labs | Microsoft Docs"
description: "Découvrez comment créer votre première machine virtuelle dans un laboratoire dans Azure DevTest Labs"
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
ms.openlocfilehash: aa6b60b799e1e98815cf288d5612f98cd77cc00e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-first-vm-in-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="688ca-103">Créer votre première machine virtuelle dans un laboratoire dans Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="688ca-103">Create your first VM in a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="688ca-104">Lorsque vous accédez initialement à DevTest Labs et que vous voulez créer votre première machine virtuelle, téléchargez une [image préchargée de base de la Place de marché](devtest-lab-configure-marketplace-images.md).</span><span class="sxs-lookup"><span data-stu-id="688ca-104">When you initially access DevTest Labs and want to create your first VM, you will likely do so using a pre-loaded [base marketplace image](devtest-lab-configure-marketplace-images.md).</span></span> <span data-ttu-id="688ca-105">Vous pourrez également choisir une [image personnalisée et une formule](devtest-lab-add-vm.md) lorsque vous allez créer d’autres machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="688ca-105">Later on, you'll also be able to choose from a [custom image and a formula](devtest-lab-add-vm.md) when creating more VMs.</span></span> 

<span data-ttu-id="688ca-106">Ce tutoriel vous guide tout au long de l’utilisation du Portail Azure pour ajouter votre première machine virtuelle à un laboratoire dans DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="688ca-106">This tutorial walks you through using the Azure portal to add your first VM to a lab in DevTest Labs.</span></span>

## <a name="steps-to-add-your-first-vm-to-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="688ca-107">Procédure d’ajout de votre première machine virtuelle à un laboratoire dans Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="688ca-107">Steps to add your first VM to a lab in Azure DevTest Labs</span></span>
1. <span data-ttu-id="688ca-108">Connectez-vous au [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="688ca-108">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="688ca-109">Sélectionnez **Autres services**, puis **DevTest Labs** dans la liste.</span><span class="sxs-lookup"><span data-stu-id="688ca-109">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
1. <span data-ttu-id="688ca-110">Dans la liste des laboratoires, sélectionnez le laboratoire dans lequel vous souhaitez créer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="688ca-110">From the list of labs, select the lab in which you want to create the VM.</span></span>  
1. <span data-ttu-id="688ca-111">Dans le panneau **Vue d’ensemble** du laboratoire, sélectionnez **+ Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="688ca-111">On the lab's **Overview** blade, select **+ Add**.</span></span>  

    ![Ajout du bouton de machine virtuelle](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. <span data-ttu-id="688ca-113">Dans le panneau **Choisir une base**, sélectionnez une image de la Place de marché pour la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="688ca-113">On the **Choose a base** blade, select a marketplace image for the VM.</span></span>
1. <span data-ttu-id="688ca-114">Dans le panneau **Machine virtuelle**, entrez un nom pour la nouvelle machine virtuelle dans la zone de texte **Nom de la machine virtuelle**.</span><span class="sxs-lookup"><span data-stu-id="688ca-114">On the **Virtual machine** blade, enter a name for the new virtual machine in the **Virtual machine name** text box.</span></span>

    ![Panneau Machine virtuelle de laboratoire](./media/devtest-lab-add-vm/devtestlab-lab-add-first-vm.png)

1. <span data-ttu-id="688ca-116">Entrez un **nom d’utilisateur** qui obtient les privilèges d’administrateur sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="688ca-116">Enter a **User Name** that is granted administrator privileges on the virtual machine.</span></span>  
1. <span data-ttu-id="688ca-117">Entrez un mot de passe dans le champ de texte intitulé **Tapez une valeur**.</span><span class="sxs-lookup"><span data-stu-id="688ca-117">Enter a password in the text field labeled **Type a value**.</span></span>
1. <span data-ttu-id="688ca-118">Le **type de disque de machine virtuelle** détermine le type de disque de stockage autorisé pour les machines virtuelles dans le laboratoire.</span><span class="sxs-lookup"><span data-stu-id="688ca-118">The **Virtual machine disk type** determines which storage disk type is allowed for the virtual machines in the lab.</span></span>
1. <span data-ttu-id="688ca-119">Sélectionnez **Taille de machine virtuelle** , puis l’un des éléments prédéfinis qui spécifient les cœurs du processeur, la taille de la RAM et la taille du disque dur de la machine virtuelle à créer.</span><span class="sxs-lookup"><span data-stu-id="688ca-119">Select **Virtual machine size** and select one of the predefined items that specify the processor cores, RAM size, and the hard drive size of the VM to create.</span></span>
1. <span data-ttu-id="688ca-120">Sélectionnez **Artefacts** et, dans la liste des artefacts, sélectionnez et configurez les artefacts que vous souhaitez ajouter à l’image de base.</span><span class="sxs-lookup"><span data-stu-id="688ca-120">Select **Artifacts** and - from the list of artifacts - select and configure the artifacts that you want to add to the base image.</span></span>
    <span data-ttu-id="688ca-121">**Remarque :** si vous n’êtes pas familier avec DevTest Labs ou avec la configuration d’artefacts, reportez-vous à la section [Ajout d’un artefact existant à une machine virtuelle](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm), puis reprenez la procédure à ce stade.</span><span class="sxs-lookup"><span data-stu-id="688ca-121">**Note:** If you're new to DevTest Labs or configuring artifacts, refer to the [Add an existing artifact to a VM](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span></span>
1. <span data-ttu-id="688ca-122">Sélectionnez **Créer** pour ajouter la machine virtuelle spécifiée au laboratoire.</span><span class="sxs-lookup"><span data-stu-id="688ca-122">Select **Create** to add the specified VM to the lab.</span></span>

   <span data-ttu-id="688ca-123">Le panneau du laboratoire affiche l’état de la création de la machine virtuelle, tout d’abord sous la forme **Création en cours**, puis sous la forme **En cours d’exécution** après le démarrage de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="688ca-123">The lab blade displays the status of the VM's creation - first as **Creating**, then as **Running** after the VM has been started.</span></span>

## <a name="next-steps"></a><span data-ttu-id="688ca-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="688ca-124">Next steps</span></span>
* <span data-ttu-id="688ca-125">Une fois la machine virtuelle créée, vous pouvez vous y connecter en sélectionnant **Connexion** dans le panneau de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="688ca-125">Once the VM has been created, you can connect to the VM by selecting **Connect** on the VM's blade.</span></span>
* <span data-ttu-id="688ca-126">Pour plus d’informations sur l’ajout des machines virtuelles suivantes à votre laboratoire, consultez [Ajouter une machine virtuelle à un laboratoire](devtest-lab-add-vm.md).</span><span class="sxs-lookup"><span data-stu-id="688ca-126">Check out [Add a VM to a lab](devtest-lab-add-vm.md) for more complete info about adding subsequent VMs in your lab.</span></span>
* <span data-ttu-id="688ca-127">Explorez la [Galerie de modèles de démarrage rapide d’Azure Resource Manager DevTest Labs](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates).</span><span class="sxs-lookup"><span data-stu-id="688ca-127">Explore the [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates).</span></span>
