---
title: "Ajouter une machine virtuelle exigible à un laboratoire dans Azure DevTest Labs | Microsoft Docs"
description: "Découvrez comment ajouter une machine virtuelle exigible à un laboratoire dans Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: f671e66e-9630-4e30-a131-a6bad9ed9c11
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: tarcher
ms.openlocfilehash: 98950d72e90b0e178bae2fffa7644fd824a25eea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-claimable-vm-to-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="8d041-103">Ajout d’une machine virtuelle à un laboratoire dans Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="8d041-103">Add a claimable VM to a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="8d041-104">Vous ajoutez une machine virtuelle exigible à un laboratoire comme vous [ajouteriez une machine virtuelle standard](devtest-lab-add-vm.md), à partir d’une *base* qui est une [image personnalisée](devtest-lab-create-template.md), une [formule](devtest-lab-manage-formulas.md) ou une [image de la plateforme Place de marché](devtest-lab-configure-marketplace-images.md).</span><span class="sxs-lookup"><span data-stu-id="8d041-104">You add a claimable VM to a lab in a similar manner to how you [add a standard VM](devtest-lab-add-vm.md) – from a *base* that is either a [custom image](devtest-lab-create-template.md), [formula](devtest-lab-manage-formulas.md), or [Marketplace image](devtest-lab-configure-marketplace-images.md).</span></span> <span data-ttu-id="8d041-105">Ce didacticiel vous guide tout au long de l’utilisation du Portail Azure pour ajouter une machine virtuelle exigible à un laboratoire dans DevTest Labs, et vous présente la procédure qu’un utilisateur suit pour revendiquer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="8d041-105">This tutorial walks you through using the Azure portal to add a claimable VM to a lab in DevTest Labs, and shows the process a user follows to claim the VM.</span></span>

> [!NOTE]
> <span data-ttu-id="8d041-106">Si vous déployez des machines virtuelles via des [Modèles Azure Resource Manager](devtest-lab-create-environment-from-arm.md), vous pouvez créer des machines virtuelles exigibles qui peuvent être revendiquées en définissant la propriété **allowClaim** sur true dans la section Propriétés.</span><span class="sxs-lookup"><span data-stu-id="8d041-106">If you deploy lab VMs through [Azure Resource Manager templates](devtest-lab-create-environment-from-arm.md), you can create claimable VMs by setting the **allowClaim** property to true in the properties section.</span></span>
>
>

## <a name="steps-to-add-a-claimable-vm-to-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="8d041-107">Procédure d’ajout d’une machine virtuelle exigible à un laboratoire dans Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="8d041-107">Steps to add a claimable VM to a lab in Azure DevTest Labs</span></span>
1. <span data-ttu-id="8d041-108">Connectez-vous au [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="8d041-108">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="8d041-109">Sélectionnez **Autres services**, puis **DevTest Labs** dans la liste.</span><span class="sxs-lookup"><span data-stu-id="8d041-109">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
1. <span data-ttu-id="8d041-110">Dans la liste des laboratoires, sélectionnez le laboratoire dans lequel vous souhaitez créer la machine virtuelle revendicable.</span><span class="sxs-lookup"><span data-stu-id="8d041-110">From the list of labs, select the lab in which you want to create the claimable VM.</span></span>  
1. <span data-ttu-id="8d041-111">Dans le panneau **Vue d’ensemble** du laboratoire, sélectionnez **+ Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="8d041-111">On the lab's **Overview** blade, select **+ Add**.</span></span>  

    ![Ajout du bouton de machine virtuelle](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. <span data-ttu-id="8d041-113">Dans le panneau **Choisir une base** , sélectionnez une base pour la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="8d041-113">On the **Choose a base** blade, select a base for the VM.</span></span>
1. <span data-ttu-id="8d041-114">Dans le panneau **Machine virtuelle**, entrez un nom pour la nouvelle machine virtuelle dans la zone de texte **Nom de la machine virtuelle**.</span><span class="sxs-lookup"><span data-stu-id="8d041-114">On the **Virtual machine** blade, enter a name for the new virtual machine in the **Virtual machine name** text box.</span></span>

    ![Panneau Machine virtuelle de laboratoire](./media/devtest-lab-add-vm/devtestlab-lab-vm-blade.png)

1. <span data-ttu-id="8d041-116">Entrez un **nom d’utilisateur** qui obtient les privilèges d’administrateur sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="8d041-116">Enter a **User Name** that is granted administrator privileges on the virtual machine.</span></span>  
1. <span data-ttu-id="8d041-117">Si vous souhaitez utiliser un mot de passe stocké dans votre [magasin des secrets](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), sélectionnez **Use a saved secret** (Utiliser un secret enregistré), et spécifiez une valeur de clé correspondant à votre secret (mot de passe).</span><span class="sxs-lookup"><span data-stu-id="8d041-117">If you want to use a password stored in your [secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), select **Use a saved secret**, and specify a key value that corresponds to your secret (password).</span></span> <span data-ttu-id="8d041-118">Dans le cas contraire, entrez un mot de passe dans le champ de texte intitulé **Tapez une valeur**.</span><span class="sxs-lookup"><span data-stu-id="8d041-118">Otherwise, enter a password in the text field labeled **Type a value**.</span></span>
1. <span data-ttu-id="8d041-119">Le **type de disque de machine virtuelle** détermine le type de disque de stockage autorisé pour les machines virtuelles dans le laboratoire.</span><span class="sxs-lookup"><span data-stu-id="8d041-119">The **Virtual machine disk type** determines which storage disk type is allowed for the virtual machines in the lab.</span></span>
1. <span data-ttu-id="8d041-120">Sélectionnez **Taille de machine virtuelle** , puis l’un des éléments prédéfinis qui spécifient les cœurs du processeur, la taille de la RAM et la taille du disque dur de la machine virtuelle à créer.</span><span class="sxs-lookup"><span data-stu-id="8d041-120">Select **Virtual machine size** and select one of the predefined items that specify the processor cores, RAM size, and the hard drive size of the VM to create.</span></span>
1. <span data-ttu-id="8d041-121">Sélectionnez **Artefacts** et, dans la liste des artefacts, sélectionnez et configurez les artefacts que vous souhaitez ajouter à l’image de base.</span><span class="sxs-lookup"><span data-stu-id="8d041-121">Select **Artifacts** and from the list of artifacts, select and configure the artifacts that you want to add to the base image.</span></span> <span data-ttu-id="8d041-122">Si vous n’êtes pas familier avec DevTest Labs ou avec la configuration d’artefacts, reportez-vous à la section [Ajout d’un artefact existant à une machine virtuelle](devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm), puis reprenez la procédure à ce stade.</span><span class="sxs-lookup"><span data-stu-id="8d041-122">If you're new to DevTest Labs or configuring artifacts, refer to the [Add an existing artifact to a VM](devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span></span>
1. <span data-ttu-id="8d041-123">Sélectionnez **Paramètres avancés** pour configurer les options réseau et les options d’expiration de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="8d041-123">Select **Advanced settings** to configure the VM's network options and expiration options.</span></span> <span data-ttu-id="8d041-124">Sous **Options de revendication**, choisissez **Oui** pour rendre la machine exigible.</span><span class="sxs-lookup"><span data-stu-id="8d041-124">Under **Claim options**, choose **Yes** to make the machine claimable.</span></span>

  ![Choisissez de rendre la machine virtuelle exigible.](./media/devtest-lab-add-vm/devtestlab-claim-VM-option.png)

1. <span data-ttu-id="8d041-126">Si vous voulez visualiser ou copier le modèle Azure Resource Manager, reportez-vous à la section [Enregistrer un modèle Azure Resource Manager](devtest-lab-add-vm.md#save-azure-resource-manager-template), puis reprenez la procédure à ce stade.</span><span class="sxs-lookup"><span data-stu-id="8d041-126">If you want to view or copy the Azure Resource Manager template, refer to the [Save Azure Resource Manager template](devtest-lab-add-vm.md#save-azure-resource-manager-template) section, and return here when finished.</span></span>
1. <span data-ttu-id="8d041-127">Sélectionnez **Créer** pour ajouter la machine virtuelle spécifiée au laboratoire.</span><span class="sxs-lookup"><span data-stu-id="8d041-127">Select **Create** to add the specified VM to the lab.</span></span>
1. <span data-ttu-id="8d041-128">Le panneau du laboratoire affiche l’état de la création de la machine virtuelle, tout d’abord sous la forme **Création en cours**, puis sous la forme **En cours d’exécution** après le démarrage de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="8d041-128">The lab blade displays the status of the VM's creation - first as **Creating**, then as **Running** after the VM has been started.</span></span>


## <a name="using-a-claimable-vm"></a><span data-ttu-id="8d041-129">Utilisation d’une machine virtuelle exigible</span><span class="sxs-lookup"><span data-stu-id="8d041-129">Using a claimable VM</span></span>

<span data-ttu-id="8d041-130">Un utilisateur peut revendiquer toute machine virtuelle dans la liste des « Machines virtuelles exigibles » en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="8d041-130">A user can claim any VM from the list of "Claimable virtual machines" by doing one of these steps:</span></span>

* <span data-ttu-id="8d041-131">Dans la liste des « Machines virtuelles exigibles » en bas du panneau Vue d’ensemble du laboratoire, cliquez avec le bouton droit sur une des machines virtuelles dans la liste et choisissez **Revendiquer la machine**.</span><span class="sxs-lookup"><span data-stu-id="8d041-131">From the list of "Claimable virtual machines" at the bottom of the lab's Overview blade, right-click on one of the VMs in the list and choose **Claim machine**.</span></span>

 ![Demandez une machine virtuelle exigible spécifique.](./media/devtest-lab-add-vm/devtestlab-claim-VM.png)


* <span data-ttu-id="8d041-133">En haut du panneau **Vue d’ensemble**, choisissez **N’importe laquelle**.</span><span class="sxs-lookup"><span data-stu-id="8d041-133">At the top of the **Overview** blade, choose **Claim any**.</span></span> <span data-ttu-id="8d041-134">Une machine virtuelle aléatoire est attribuée dans la liste des machines virtuelles qui peuvent être revendiquées.</span><span class="sxs-lookup"><span data-stu-id="8d041-134">A random virtual machine is assigned from the list of claimable VMs.</span></span>

 ![Demandez n’importe quelle machine virtuelle exigible.](./media/devtest-lab-add-vm/devtestlab-claim-any.png)


<span data-ttu-id="8d041-136">Une fois que l’utilisateur revendique une machine virtuelle, cette dernière est placée dans la liste « Mes machines virtuelles » et n’est plus exigible par un autre utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8d041-136">After a user claims a VM, it is moved up into their list of "My virtual machines" and is no longer claimable by any other user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8d041-137">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8d041-137">Next steps</span></span>
* <span data-ttu-id="8d041-138">Une fois la machine virtuelle créée, vous pouvez vous y connecter en sélectionnant **Connexion** dans le panneau de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="8d041-138">Once the VM has been created, you can connect to the VM by selecting **Connect** on the VM's blade.</span></span>
* <span data-ttu-id="8d041-139">Explorez la [Galerie de modèles de démarrage rapide d’Azure Resource Manager DevTest Labs](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates).</span><span class="sxs-lookup"><span data-stu-id="8d041-139">Explore the [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)</span></span>
