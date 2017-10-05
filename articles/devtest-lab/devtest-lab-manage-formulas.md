---
title: "Gérer les formules dans Azure DevTest Labs pour créer des machines virtuelles | Microsoft Docs"
description: "Découvrez comment mettre à jour et supprimer des formules Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 841dd95a-657f-4d80-ba26-59a9b5104fe4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: tarcher
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bfdab5def50158f9b764bbb1e50c2624cc6d5fb3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-devtest-labs-formulas"></a><span data-ttu-id="3d6d8-103">Gérer les formules Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="3d6d8-103">Manage Azure DevTest Labs formulas</span></span>

[!INCLUDE [devtest-lab-formula-definition](../../includes/devtest-lab-formula-definition.md)]

<span data-ttu-id="3d6d8-104">Cet article explique comment créer une formule à partir d’une base (une image personnalisée, une image Place de marché ou une autre formule) ou d’une machine virtuelle existante.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-104">This article illustrates how to create a formula from either a base (custom image, Marketplace image, or another formula) or an existing VM.</span></span> <span data-ttu-id="3d6d8-105">Cet article vous guide aussi dans la gestion des formules existantes.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-105">This article also guides you through managing existing formulas.</span></span>

## <a name="create-a-formula"></a><span data-ttu-id="3d6d8-106">Créer une formule</span><span class="sxs-lookup"><span data-stu-id="3d6d8-106">Create a formula</span></span>
<span data-ttu-id="3d6d8-107">Toute personne disposant des autorisations *Utilisateurs* de DevTest Labs est en mesure de créer des machines virtuelles en utilisant une formule comme base.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-107">Anyone with DevTest Labs *Users* permissions is able to create VMs using a formula as a base.</span></span> <span data-ttu-id="3d6d8-108">Il existe deux façons de créer des formules :</span><span class="sxs-lookup"><span data-stu-id="3d6d8-108">There are two ways to create formulas:</span></span> 

* <span data-ttu-id="3d6d8-109">À partir d’une base : quand vous voulez définir toutes les caractéristiques de la formule.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-109">From a base - Use when you want to define all the characteristics of the formula.</span></span>
* <span data-ttu-id="3d6d8-110">À partir d’une machine virtuelle de laboratoire existante : quand vous voulez créer une formule à partir des paramètres d’une machine virtuelle existante.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-110">From an existing lab VM - Use when you want to create a formula based on the settings of an existing VM.</span></span>

<span data-ttu-id="3d6d8-111">Pour plus d’informations sur l’ajout des utilisateurs et des autorisations, consultez [Ajouter des propriétaires et des utilisateurs dans Azure DevTest Labs](./devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="3d6d8-111">For more information about adding users and permissions, see [Add owners and users in Azure DevTest Labs](./devtest-lab-add-devtest-user.md).</span></span>

### <a name="create-a-formula-from-a-base"></a><span data-ttu-id="3d6d8-112">Créer une formule à partir d’une base</span><span class="sxs-lookup"><span data-stu-id="3d6d8-112">Create a formula from a base</span></span>
<span data-ttu-id="3d6d8-113">Les étapes suivantes vous guideront tout au long du processus de création d’une formule à partir d’une image personnalisée, image Marketplace ou autre formule.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-113">The following steps guide you through the process of creating a formula from a custom image, Marketplace image, or another formula.</span></span>

1. <span data-ttu-id="3d6d8-114">Connectez-vous au [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="3d6d8-114">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

2. <span data-ttu-id="3d6d8-115">Sélectionnez **Autres services**, puis **DevTest Labs** dans la liste.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-115">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>

3. <span data-ttu-id="3d6d8-116">Sélectionnez le laboratoire souhaité dans la liste des laboratoires.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-116">From the list of labs, select the desired lab.</span></span>  

4. <span data-ttu-id="3d6d8-117">Dans le panneau du laboratoire, sélectionnez **Formules (bases réutilisables)**.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-117">On the lab's blade, select **Formulas (reusable bases)**.</span></span>
   
    ![Menu de formule](./media/devtest-lab-create-formulas/lab-settings-formulas.png)

5. <span data-ttu-id="3d6d8-119">Dans le panneau **Formules**, sélectionnez **+ Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-119">On the **Formulas** blade, select **+ Add**.</span></span>
   
    ![Ajouter une formule](./media/devtest-lab-create-formulas/add-formula.png)

6. <span data-ttu-id="3d6d8-121">Dans le panneau **Choisir une base** , sélectionnez la base (l’image personnalisée, l’image Marketplace ou la formule) à partir de laquelle vous voulez créer la formule.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-121">On the **Choose a base** blade, select the base (custom image, Marketplace image, or formula) from which you want to create the formula.</span></span>
   
    ![Liste de base](./media/devtest-lab-create-formulas/base-list.png)

7. <span data-ttu-id="3d6d8-123">Sur le panneau **Créer une formule** , spécifiez les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="3d6d8-123">On the **Create formula** blade, specify the following values:</span></span>
   
    * <span data-ttu-id="3d6d8-124">**Nom de la formule** : entrez un nom pour votre formule.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-124">**Formula name** - Enter a name for your formula.</span></span> <span data-ttu-id="3d6d8-125">Cette valeur s’affiche dans la liste des images de base lorsque vous créez une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-125">This value is displayed in the list of base images when you create a VM.</span></span> <span data-ttu-id="3d6d8-126">Le nom est validé au fur et à mesure que vous le tapez. S’il n’est pas valide, un message indique les exigences d’un nom valide.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-126">The name is validated as you type it, and if not valid, a message indicates the requirements for a valid name.</span></span>
    * <span data-ttu-id="3d6d8-127">**Description** : entrez une description significative pour votre formule.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-127">**Description** - Enter a meaningful description for your formula.</span></span> <span data-ttu-id="3d6d8-128">Cette valeur est disponible dans le menu contextuel de la formule quand vous créez une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-128">This value is available from the formula's context menu when you create a VM.</span></span>
    * <span data-ttu-id="3d6d8-129">**Nom d’utilisateur** - Entrez un nom d’utilisateur qui obtient les privilèges d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-129">**User name** - Enter a user name that is granted administrator privileges.</span></span>
    * <span data-ttu-id="3d6d8-130">**Mot de passe** - Entrez, ou sélectionnez dans la liste déroulante, une valeur qui est associée au secret (mot de passe) que vous souhaitez utiliser pour l’utilisateur spécifié.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-130">**Password** - Enter - or select from the dropdown - a value that is associated with the secret (password) that you want to use for the specified user.</span></span> <span data-ttu-id="3d6d8-131">Pour plus d’informations sur les secrets, consultez [Azure DevTest Labs: Personal secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/) (Azure DevTest Labs : magasin des secrets personnel).</span><span class="sxs-lookup"><span data-stu-id="3d6d8-131">For more information about the secrets, see [Azure DevTest Labs: Personal secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/).</span></span>
    * <span data-ttu-id="3d6d8-132">**Type de disque de machine virtuelle** : sélectionnez HDD (disque dur) ou SSD (disque SSD) pour indiquer le type de disque de stockage autorisé pour les machines virtuelles approvisionnées à l’aide de cette image de base.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-132">**Virtual machine disk type** - Specify either HDD (hard-disk drive) or SSD (solid-state drive) to indicate which storage disk type is allowed for the virtual machines provisioned using this base image.</span></span>
    * <span data-ttu-id="3d6d8-133">**Taille de la machine virtuelle** - Sélectionnez l’un des éléments prédéfinis qui spécifient les cœurs du processeur, la taille de la RAM et la taille du disque dur de la machine virtuelle à créer.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-133">** Virtual machine size** - Select one of the predefined items that specify the processor cores, RAM size, and the hard drive size of the VM to create.</span></span> 
    * <span data-ttu-id="3d6d8-134">**Artefacts** - Sélectionnez cette option pour ouvrir le panneau **Ajouter des artefacts**, dans lequel vous pouvez sélectionner et configurer les artefacts que vous souhaitez ajouter à l’image de base.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-134">**Artifacts** - Select to open the **Add artifacts** blade, in which you select and configure the artifacts that you want to add to the base image.</span></span> <span data-ttu-id="3d6d8-135">Pour plus d’informations sur les artefacts, consultez [Gérer les artefacts de machine virtuelle dans Azure DevTest Labs](./devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="3d6d8-135">For more information about artifacts, see [Manage VM artifacts in Azure DevTest Labs](./devtest-lab-add-vm-with-artifacts.md).</span></span>
    * <span data-ttu-id="3d6d8-136">**Paramètres avancés** - Sélectionnez cette option pour ouvrir le panneau **Avancé** dans lequel vous configurez les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="3d6d8-136">**Advanced settings** - Select to open the **Advanced** blade where you configure the following settings:</span></span>
        * <span data-ttu-id="3d6d8-137">**Réseau virtuel** - Spécifiez le réseau virtuel souhaité.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-137">**Virtual network** - Specify the desired virtual network.</span></span>
        * <span data-ttu-id="3d6d8-138">**Sous-réseau** - Spécifiez le sous-réseau souhaité.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-138">**Subnet** - Specify the desired subnet.</span></span>    
        * <span data-ttu-id="3d6d8-139">**Configuration de l’adresse IP** - Spécifiez si vous souhaitez que les adresses IP soient partagées, privées ou publiques.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-139">**IP address configuration** - Specify if you want the Public, Private, or Shared IP addresses.</span></span> <span data-ttu-id="3d6d8-140">Pour plus d’informations sur les adresses IP partagées, consultez [Comprendre les adresses IP partagées dans Azure DevTest Labs](./devtest-lab-shared-ip.md).</span><span class="sxs-lookup"><span data-stu-id="3d6d8-140">For more information about shared IP addresses, see [Understand shared IP addresses in Azure DevTest Labs](./devtest-lab-shared-ip.md).</span></span>
        * <span data-ttu-id="3d6d8-141">**Make this machine claimable** (Rendre cette machine exigible) - Lorsqu’une machine est « exigible », cela signifie qu’aucune propriété ne lui sera affectée au moment de la création.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-141">**Make this machine claimable** - Making a machine "claimable" means that it will not be assigned ownership at the time of creation.</span></span> <span data-ttu-id="3d6d8-142">En revanche, les utilisateurs du laboratoire seront en mesure de prendre possession de la machine (de la « revendiquer ») dans le panneau du laboratoire.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-142">Instead lab users will be able to take ownership ("claim") the machine in the lab's blade.</span></span>     
    * <span data-ttu-id="3d6d8-143">**Image** : ce champ affiche le nom de l'image de base que vous avez sélectionnée dans le panneau précédent.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-143">**Image** - This field displays name of the base image you selected on the previous blade.</span></span> 
     
       ![Créer une formule](./media/devtest-lab-create-formulas/create-formula.png)

8. <span data-ttu-id="3d6d8-145">sélectionnez **Créer** pour créer la formule.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-145">Select **Create** to create the formula.</span></span>

9. <span data-ttu-id="3d6d8-146">Une fois la formule créée, elle s’affiche dans la liste sur le panneau **Formules**.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-146">When the formula has been created, it displays in the list on the **Formulas** blade.</span></span>

### <a name="create-a-formula-from-a-vm"></a><span data-ttu-id="3d6d8-147">Créer une formule depuis une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="3d6d8-147">Create a formula from a VM</span></span>
<span data-ttu-id="3d6d8-148">Les étapes suivantes vous guident dans le processus de création d’une formule à partir d’une machine virtuelle existante.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-148">The following steps guide you through the process of creating a formula based on an existing VM.</span></span> 

> [!NOTE]
> <span data-ttu-id="3d6d8-149">Pour créer une formule à partir d’une machine virtuelle, la machine virtuelle doit avoir été créée après le 30 mars 2016.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-149">To create a formula from a VM, the VM must have been created after March 30, 2016.</span></span> 
> 
> 

1. <span data-ttu-id="3d6d8-150">Connectez-vous au [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="3d6d8-150">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="3d6d8-151">Sélectionnez **Autres services**, puis **DevTest Labs** dans la liste.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-151">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="3d6d8-152">Sélectionnez le laboratoire souhaité dans la liste des laboratoires.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-152">From the list of labs, select the desired lab.</span></span>  
4. <span data-ttu-id="3d6d8-153">Dans le panneau **Présentation** du laboratoire, sélectionnez la machine virtuelle à partir de laquelle vous souhaitez créer la formule.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-153">On the lab's **Overview** blade, select the VM from which you wish to create the formula.</span></span>
   
    ![Machines virtuelles de labo](./media/devtest-lab-create-formulas/my-vms.png)
5. <span data-ttu-id="3d6d8-155">Dans le panneau de la machine virtuelle, cliquez sur **Créer une formule (base réutilisable)**.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-155">On the VM's blade, select **Create formula (reusable base)**.</span></span>
   
    ![Créer une formule](./media/devtest-lab-create-formulas/create-formula-menu.png)
6. <span data-ttu-id="3d6d8-157">Dans le panneau **Créer une formule**, entrez un **Nom** et une **Description** pour votre nouvelle formule.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-157">On the **Create formula** blade, enter a **Name** and **Description** for your new formula.</span></span>
   
    ![Panneau Créer une formule](./media/devtest-lab-create-formulas/create-formula-blade.png)
7. <span data-ttu-id="3d6d8-159">Sélectionnez **OK** pour créer la formule.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-159">Select **OK** to create the formula.</span></span>

## <a name="modify-a-formula"></a><span data-ttu-id="3d6d8-160">Modifier une formule</span><span class="sxs-lookup"><span data-stu-id="3d6d8-160">Modify a formula</span></span>
<span data-ttu-id="3d6d8-161">Pour modifier une formule, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="3d6d8-161">To modify a formula, follow these steps:</span></span>

1. <span data-ttu-id="3d6d8-162">Connectez-vous au [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="3d6d8-162">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="3d6d8-163">Sélectionnez **Autres services**, puis **DevTest Labs** dans la liste.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-163">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="3d6d8-164">Sélectionnez le laboratoire souhaité dans la liste des laboratoires.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-164">From the list of labs, select the desired lab.</span></span>  
4. <span data-ttu-id="3d6d8-165">Dans le panneau du laboratoire, sélectionnez **Formules (bases réutilisables)**.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-165">On the lab's blade, select **Formulas (reusable bases)**.</span></span>
   
    ![Menu de formule](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. <span data-ttu-id="3d6d8-167">Dans le panneau des **formules de laboratoire** , sélectionnez la formule à modifier.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-167">On the **Lab formulas** blade, select the formula you wish to modify.</span></span>
6. <span data-ttu-id="3d6d8-168">Dans le panneau **Mettre à jour la formule**, effectuez les modifications souhaitées, puis sélectionnez **Mettre à jour**.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-168">On the **Update formula** blade, make the desired edits, and select **Update**.</span></span>

## <a name="delete-a-formula"></a><span data-ttu-id="3d6d8-169">Supprimer une formule</span><span class="sxs-lookup"><span data-stu-id="3d6d8-169">Delete a formula</span></span>
<span data-ttu-id="3d6d8-170">Pour supprimer une formule, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="3d6d8-170">To delete a formula, follow these steps:</span></span>

1. <span data-ttu-id="3d6d8-171">Connectez-vous au [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="3d6d8-171">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="3d6d8-172">Sélectionnez **Autres services**, puis **DevTest Labs** dans la liste.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-172">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="3d6d8-173">Sélectionnez le laboratoire souhaité dans la liste des laboratoires.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-173">From the list of labs, select the desired lab.</span></span>  
4. <span data-ttu-id="3d6d8-174">Dans le panneau **Paramètres** du laboratoire, sélectionnez **Formules**.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-174">On the lab **Settings** blade, select **Formulas**.</span></span>
   
    ![Menu de formule](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. <span data-ttu-id="3d6d8-176">Dans le panneau des **formules de laboratoire** , sélectionnez les points de suspension à droite de la formule à supprimer.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-176">On the **Lab formulas** blade, select the ellipsis to the right of the formula you wish to delete.</span></span>
   
    ![Menu de formule](./media/devtest-lab-manage-formulas/lab-formulas-blade.png)
6. <span data-ttu-id="3d6d8-178">Dans le menu contextuel de la formule, sélectionnez **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-178">On the formula's context menu, select **Delete**.</span></span>
   
    ![Menu contextuel de la formule](./media/devtest-lab-manage-formulas/formula-delete-context-menu.png)
7. <span data-ttu-id="3d6d8-180">sélectionnez **Oui** dans la boîte de dialogue de confirmation de la suppression.</span><span class="sxs-lookup"><span data-stu-id="3d6d8-180">Select **Yes** to the deletion confirmation dialog.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="3d6d8-181">Billets de blog connexes</span><span class="sxs-lookup"><span data-stu-id="3d6d8-181">Related blog posts</span></span>
* [<span data-ttu-id="3d6d8-182">Images personnalisées ou formules ?</span><span class="sxs-lookup"><span data-stu-id="3d6d8-182">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a><span data-ttu-id="3d6d8-183">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3d6d8-183">Next steps</span></span>
<span data-ttu-id="3d6d8-184">Quand vous avez créé une formule à utiliser lors de la création d’une machine virtuelle, l’étape suivante consiste à [ajouter une machine virtuelle à votre laboratoire](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="3d6d8-184">Once you have created a formula for use when creating a VM, the next step is to [add a VM to your lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

