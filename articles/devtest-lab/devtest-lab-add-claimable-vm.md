---
title: "aaaAdd un laboratoire de tooa de machine virtuelle qui peuvent être réclamé dans Azure DevTest Labs | Documents Microsoft"
description: "Découvrez comment tooadd un laboratoire de tooa qui peuvent être réclamés machine virtuelle dans Azure DevTest Labs"
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
ms.openlocfilehash: fe6385ae2e59b9636b82aec250dc3a1f8a40ba5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-claimable-vm-tooa-lab-in-azure-devtest-labs"></a><span data-ttu-id="13cf3-103">Ajouter un laboratoire tooa de machine virtuelle qui peuvent être réclamé dans Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="13cf3-103">Add a claimable VM tooa lab in Azure DevTest Labs</span></span>
<span data-ttu-id="13cf3-104">Vous ajoutez un laboratoire tooa de machine virtuelle qui peuvent être réclamé dans un toohow de manière similaire vous [ajouter une machine virtuelle standard](devtest-lab-add-vm.md) – dans un *base* qui est soit un [image personnalisée](devtest-lab-create-template.md), [formule](devtest-lab-manage-formulas.md), ou [une image Marketplace](devtest-lab-configure-marketplace-images.md).</span><span class="sxs-lookup"><span data-stu-id="13cf3-104">You add a claimable VM tooa lab in a similar manner toohow you [add a standard VM](devtest-lab-add-vm.md) – from a *base* that is either a [custom image](devtest-lab-create-template.md), [formula](devtest-lab-manage-formulas.md), or [Marketplace image](devtest-lab-configure-marketplace-images.md).</span></span> <span data-ttu-id="13cf3-105">Ce didacticiel vous guide à l’aide de hello tooadd portail Azure un laboratoire de tooa de machine virtuelle qui peuvent être réclamé dans DevTest Labs et présente le processus de hello qu'un utilisateur suit tooclaim hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="13cf3-105">This tutorial walks you through using hello Azure portal tooadd a claimable VM tooa lab in DevTest Labs, and shows hello process a user follows tooclaim hello VM.</span></span>

> [!NOTE]
> <span data-ttu-id="13cf3-106">Si vous déployez des ordinateurs virtuels de lab via [modèles Azure Resource Manager](devtest-lab-create-environment-from-arm.md), vous pouvez créer des machines virtuelles qui peuvent être réclamés en définissant un hello **allowClaim** tootrue de propriété dans la section des propriétés hello.</span><span class="sxs-lookup"><span data-stu-id="13cf3-106">If you deploy lab VMs through [Azure Resource Manager templates](devtest-lab-create-environment-from-arm.md), you can create claimable VMs by setting hello **allowClaim** property tootrue in hello properties section.</span></span>
>
>

## <a name="steps-tooadd-a-claimable-vm-tooa-lab-in-azure-devtest-labs"></a><span data-ttu-id="13cf3-107">Étapes tooadd un laboratoire de tooa de machine virtuelle qui peuvent être réclamé dans Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="13cf3-107">Steps tooadd a claimable VM tooa lab in Azure DevTest Labs</span></span>
1. <span data-ttu-id="13cf3-108">Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="13cf3-108">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="13cf3-109">Sélectionnez **plus Services**, puis sélectionnez **DevTest Labs** à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="13cf3-109">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
1. <span data-ttu-id="13cf3-110">À partir de la liste hello de labs, sélectionnez le laboratoire de hello dans lequel vous voulez toocreate hello qui peuvent être réclamé machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="13cf3-110">From hello list of labs, select hello lab in which you want toocreate hello claimable VM.</span></span>  
1. <span data-ttu-id="13cf3-111">Sur du laboratoire hello **vue d’ensemble** panneau, sélectionnez **+ ajouter**.</span><span class="sxs-lookup"><span data-stu-id="13cf3-111">On hello lab's **Overview** blade, select **+ Add**.</span></span>  

    ![Ajout du bouton de machine virtuelle](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. <span data-ttu-id="13cf3-113">Sur hello **choisir une base** panneau, sélectionnez une base de hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="13cf3-113">On hello **Choose a base** blade, select a base for hello VM.</span></span>
1. <span data-ttu-id="13cf3-114">Sur hello **virtuels** panneau, entrez un nom pour la machine virtuelle hello Bonjour **nom de machine virtuelle** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="13cf3-114">On hello **Virtual machine** blade, enter a name for hello new virtual machine in hello **Virtual machine name** text box.</span></span>

    ![Panneau Machine virtuelle de laboratoire](./media/devtest-lab-add-vm/devtestlab-lab-vm-blade.png)

1. <span data-ttu-id="13cf3-116">Entrez un **nom d’utilisateur** qui dispose des privilèges d’administrateur sur l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="13cf3-116">Enter a **User Name** that is granted administrator privileges on hello virtual machine.</span></span>  
1. <span data-ttu-id="13cf3-117">Si vous voulez toouse un mot de passe stockés dans votre [magasin des secrets](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), sélectionnez **utiliser une clé secrète enregistrée**et spécifiez une valeur clée correspondant tooyour secret (mot de passe).</span><span class="sxs-lookup"><span data-stu-id="13cf3-117">If you want toouse a password stored in your [secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), select **Use a saved secret**, and specify a key value that corresponds tooyour secret (password).</span></span> <span data-ttu-id="13cf3-118">Dans le cas contraire, entrez un mot de passe dans le champ de texte hello étiqueté **une valeur de Type**.</span><span class="sxs-lookup"><span data-stu-id="13cf3-118">Otherwise, enter a password in hello text field labeled **Type a value**.</span></span>
1. <span data-ttu-id="13cf3-119">Hello **type de disque de machine virtuelle** détermine le type de disque de stockage est autorisé pour les ordinateurs virtuels de hello dans le laboratoire de hello.</span><span class="sxs-lookup"><span data-stu-id="13cf3-119">hello **Virtual machine disk type** determines which storage disk type is allowed for hello virtual machines in hello lab.</span></span>
1. <span data-ttu-id="13cf3-120">Sélectionnez **taille de machine virtuelle** et sélectionnez une des hello prédéfinis des éléments qui spécifient les cœurs de processeur hello, la taille de mémoire RAM et taille du disque dur de hello VM toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="13cf3-120">Select **Virtual machine size** and select one of hello predefined items that specify hello processor cores, RAM size, and hello hard drive size of hello VM toocreate.</span></span>
1. <span data-ttu-id="13cf3-121">Sélectionnez **artefacts** liste hello des artefacts, sélectionner et configurer les artefacts hello que vous souhaitez l’image de base tooadd toohello.</span><span class="sxs-lookup"><span data-stu-id="13cf3-121">Select **Artifacts** and from hello list of artifacts, select and configure hello artifacts that you want tooadd toohello base image.</span></span> <span data-ttu-id="13cf3-122">Si vous les nouveaux laboratoires tooDevTest ou configuration des artefacts, consultez toohello [ajouter un tooa d’artefact existant VM](devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) section, puis revenez ici une fois.</span><span class="sxs-lookup"><span data-stu-id="13cf3-122">If you're new tooDevTest Labs or configuring artifacts, refer toohello [Add an existing artifact tooa VM](devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span></span>
1. <span data-ttu-id="13cf3-123">Sélectionnez **paramètres avancés** options d’expiration et les options de réseau de tooconfigure hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="13cf3-123">Select **Advanced settings** tooconfigure hello VM's network options and expiration options.</span></span> <span data-ttu-id="13cf3-124">Sous **revendication options**, choisissez **Oui** machine de hello toomake qui peuvent être réclamé.</span><span class="sxs-lookup"><span data-stu-id="13cf3-124">Under **Claim options**, choose **Yes** toomake hello machine claimable.</span></span>

  ![Choisissez toomake hello qui peuvent être réclamé machine virtuelle.](./media/devtest-lab-add-vm/devtestlab-claim-VM-option.png)

1. <span data-ttu-id="13cf3-126">Si vous souhaitez tooview ou copiez le modèle de hello Azure Resource Manager, consultez toohello [modèle Enregistrer Azure Resource Manager](devtest-lab-add-vm.md#save-azure-resource-manager-template) section et revenez ici une fois.</span><span class="sxs-lookup"><span data-stu-id="13cf3-126">If you want tooview or copy hello Azure Resource Manager template, refer toohello [Save Azure Resource Manager template](devtest-lab-add-vm.md#save-azure-resource-manager-template) section, and return here when finished.</span></span>
1. <span data-ttu-id="13cf3-127">Sélectionnez **créer** tooadd hello spécifié lab toohello de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="13cf3-127">Select **Create** tooadd hello specified VM toohello lab.</span></span>
1. <span data-ttu-id="13cf3-128">Panneau de laboratoire Hello affiche hello statut de la création de la machine virtuelle hello - tout d’abord **création**, puis en tant que **en cours d’exécution** après hello machine virtuelle a été démarré.</span><span class="sxs-lookup"><span data-stu-id="13cf3-128">hello lab blade displays hello status of hello VM's creation - first as **Creating**, then as **Running** after hello VM has been started.</span></span>


## <a name="using-a-claimable-vm"></a><span data-ttu-id="13cf3-129">Utilisation d’une machine virtuelle exigible</span><span class="sxs-lookup"><span data-stu-id="13cf3-129">Using a claimable VM</span></span>

<span data-ttu-id="13cf3-130">Un utilisateur peut demander toutes les machines virtuelles à partir de la liste hello de « Ordinateurs virtuels qui peuvent être réclamés » en effectuant l’une de ces étapes :</span><span class="sxs-lookup"><span data-stu-id="13cf3-130">A user can claim any VM from hello list of "Claimable virtual machines" by doing one of these steps:</span></span>

* <span data-ttu-id="13cf3-131">À partir de la liste de hello des « Ordinateurs virtuels qui peuvent être réclamés » en bas de hello du Panneau de vue d’ensemble du laboratoire hello, avec le bouton droit sur l’un des hello machines virtuelles dans la liste de hello et choisissez **machine de revendication**.</span><span class="sxs-lookup"><span data-stu-id="13cf3-131">From hello list of "Claimable virtual machines" at hello bottom of hello lab's Overview blade, right-click on one of hello VMs in hello list and choose **Claim machine**.</span></span>

 ![Demandez une machine virtuelle exigible spécifique.](./media/devtest-lab-add-vm/devtestlab-claim-VM.png)


* <span data-ttu-id="13cf3-133">En haut de hello Hello **vue d’ensemble** panneau, choisissez **demander une**.</span><span class="sxs-lookup"><span data-stu-id="13cf3-133">At hello top of hello **Overview** blade, choose **Claim any**.</span></span> <span data-ttu-id="13cf3-134">Un ordinateur virtuel aléatoire est attribué à partir de la liste de hello de machines virtuelles qui peuvent être réclamés.</span><span class="sxs-lookup"><span data-stu-id="13cf3-134">A random virtual machine is assigned from hello list of claimable VMs.</span></span>

 ![Demandez n’importe quelle machine virtuelle exigible.](./media/devtest-lab-add-vm/devtestlab-claim-any.png)


<span data-ttu-id="13cf3-136">Une fois que l’utilisateur revendique une machine virtuelle, cette dernière est placée dans la liste « Mes machines virtuelles » et n’est plus exigible par un autre utilisateur.</span><span class="sxs-lookup"><span data-stu-id="13cf3-136">After a user claims a VM, it is moved up into their list of "My virtual machines" and is no longer claimable by any other user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="13cf3-137">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="13cf3-137">Next steps</span></span>
* <span data-ttu-id="13cf3-138">Une fois hello machine virtuelle a été créé, vous pouvez vous connecter toohello machine virtuelle en sélectionnant **Connect** sur le panneau de la machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="13cf3-138">Once hello VM has been created, you can connect toohello VM by selecting **Connect** on hello VM's blade.</span></span>
* <span data-ttu-id="13cf3-139">Explorer hello [galerie de modèles de DevTest Labs Azure Resource Manager QuickStart](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)</span><span class="sxs-lookup"><span data-stu-id="13cf3-139">Explore hello [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)</span></span>
