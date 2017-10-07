---
title: formules aaaManage dans Azure DevTest Labs toocreate machines virtuelles | Documents Microsoft
description: "Découvrez comment tooupdate et supprimez les formules Azure DevTest Labs"
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
ms.openlocfilehash: 855debe46f3b70cc45ea5d55869663b64e225124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-devtest-labs-formulas"></a><span data-ttu-id="f5747-103">Gérer les formules Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="f5747-103">Manage Azure DevTest Labs formulas</span></span>

[!INCLUDE [devtest-lab-formula-definition](../../includes/devtest-lab-formula-definition.md)]

<span data-ttu-id="f5747-104">Cet article explique comment toocreate une formule à partir d’une base (image personnalisée, une image Marketplace ou un autre formule) ou sur une machine virtuelle existante.</span><span class="sxs-lookup"><span data-stu-id="f5747-104">This article illustrates how toocreate a formula from either a base (custom image, Marketplace image, or another formula) or an existing VM.</span></span> <span data-ttu-id="f5747-105">Cet article vous guide aussi dans la gestion des formules existantes.</span><span class="sxs-lookup"><span data-stu-id="f5747-105">This article also guides you through managing existing formulas.</span></span>

## <a name="create-a-formula"></a><span data-ttu-id="f5747-106">Créer une formule</span><span class="sxs-lookup"><span data-stu-id="f5747-106">Create a formula</span></span>
<span data-ttu-id="f5747-107">Toute personne ayant DevTest Labs *utilisateurs* autorisations est VMs toocreate en mesure d’à l’aide d’une formule comme base.</span><span class="sxs-lookup"><span data-stu-id="f5747-107">Anyone with DevTest Labs *Users* permissions is able toocreate VMs using a formula as a base.</span></span> <span data-ttu-id="f5747-108">Il existe deux façons de toocreate formules :</span><span class="sxs-lookup"><span data-stu-id="f5747-108">There are two ways toocreate formulas:</span></span> 

* <span data-ttu-id="f5747-109">À partir d’une base - Utilisez toodefine toutes les caractéristiques de hello de formule de hello.</span><span class="sxs-lookup"><span data-stu-id="f5747-109">From a base - Use when you want toodefine all hello characteristics of hello formula.</span></span>
* <span data-ttu-id="f5747-110">À partir d’un laboratoire existant VM - à utiliser toocreate une formule en fonction des paramètres de hello d’une machine virtuelle existante.</span><span class="sxs-lookup"><span data-stu-id="f5747-110">From an existing lab VM - Use when you want toocreate a formula based on hello settings of an existing VM.</span></span>

<span data-ttu-id="f5747-111">Pour plus d’informations sur l’ajout des utilisateurs et des autorisations, consultez [Ajouter des propriétaires et des utilisateurs dans Azure DevTest Labs](./devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="f5747-111">For more information about adding users and permissions, see [Add owners and users in Azure DevTest Labs](./devtest-lab-add-devtest-user.md).</span></span>

### <a name="create-a-formula-from-a-base"></a><span data-ttu-id="f5747-112">Créer une formule à partir d’une base</span><span class="sxs-lookup"><span data-stu-id="f5747-112">Create a formula from a base</span></span>
<span data-ttu-id="f5747-113">Hello comme suit vous guide tout au long des processus hello de création d’une formule à partir d’une image personnalisée, une image Marketplace ou une autre formule.</span><span class="sxs-lookup"><span data-stu-id="f5747-113">hello following steps guide you through hello process of creating a formula from a custom image, Marketplace image, or another formula.</span></span>

1. <span data-ttu-id="f5747-114">Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="f5747-114">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

2. <span data-ttu-id="f5747-115">Sélectionnez **plus Services**, puis sélectionnez **DevTest Labs** à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="f5747-115">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>

3. <span data-ttu-id="f5747-116">Dans liste hello labs, sélectionnez lab souhaité de hello.</span><span class="sxs-lookup"><span data-stu-id="f5747-116">From hello list of labs, select hello desired lab.</span></span>  

4. <span data-ttu-id="f5747-117">Dans le panneau de hello lab, sélectionnez **formules (réutilisables bases)**.</span><span class="sxs-lookup"><span data-stu-id="f5747-117">On hello lab's blade, select **Formulas (reusable bases)**.</span></span>
   
    ![Menu de formule](./media/devtest-lab-create-formulas/lab-settings-formulas.png)

5. <span data-ttu-id="f5747-119">Sur hello **formules** panneau, sélectionnez **+ ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f5747-119">On hello **Formulas** blade, select **+ Add**.</span></span>
   
    ![Ajouter une formule](./media/devtest-lab-create-formulas/add-formula.png)

6. <span data-ttu-id="f5747-121">Sur hello **choisir une base** panneau, base hello select (image personnalisée, une image Marketplace ou formule) à partir de laquelle vous souhaitez que la formule de hello de toocreate.</span><span class="sxs-lookup"><span data-stu-id="f5747-121">On hello **Choose a base** blade, select hello base (custom image, Marketplace image, or formula) from which you want toocreate hello formula.</span></span>
   
    ![Liste de base](./media/devtest-lab-create-formulas/base-list.png)

7. <span data-ttu-id="f5747-123">Sur hello **créer formule** panneau, spécifiez hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="f5747-123">On hello **Create formula** blade, specify hello following values:</span></span>
   
    * <span data-ttu-id="f5747-124">**Nom de la formule** : entrez un nom pour votre formule.</span><span class="sxs-lookup"><span data-stu-id="f5747-124">**Formula name** - Enter a name for your formula.</span></span> <span data-ttu-id="f5747-125">Cette valeur est affichée dans la liste hello des images de base lorsque vous créez une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f5747-125">This value is displayed in hello list of base images when you create a VM.</span></span> <span data-ttu-id="f5747-126">nom de Hello est validé comme vous le tapez, et si elle est non valide, un message indique exigences hello d’un nom valide.</span><span class="sxs-lookup"><span data-stu-id="f5747-126">hello name is validated as you type it, and if not valid, a message indicates hello requirements for a valid name.</span></span>
    * <span data-ttu-id="f5747-127">**Description** : entrez une description significative pour votre formule.</span><span class="sxs-lookup"><span data-stu-id="f5747-127">**Description** - Enter a meaningful description for your formula.</span></span> <span data-ttu-id="f5747-128">Cette valeur est disponible à partir du menu contextuel de la formule hello lorsque vous créez une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f5747-128">This value is available from hello formula's context menu when you create a VM.</span></span>
    * <span data-ttu-id="f5747-129">**Nom d’utilisateur** - Entrez un nom d’utilisateur qui obtient les privilèges d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="f5747-129">**User name** - Enter a user name that is granted administrator privileges.</span></span>
    * <span data-ttu-id="f5747-130">**Mot de passe** - Entrez - ou sélectionnez dans la liste déroulante de hello - une valeur qui est associée à hello mot de passe que vous souhaitez toouse pour l’utilisateur spécifié de hello.</span><span class="sxs-lookup"><span data-stu-id="f5747-130">**Password** - Enter - or select from hello dropdown - a value that is associated with hello secret (password) that you want toouse for hello specified user.</span></span> <span data-ttu-id="f5747-131">Pour plus d’informations sur les secrets hello, consultez [Azure DevTest Labs : magasin des secrets personnel](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/).</span><span class="sxs-lookup"><span data-stu-id="f5747-131">For more information about hello secrets, see [Azure DevTest Labs: Personal secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/).</span></span>
    * <span data-ttu-id="f5747-132">**Type de disque de machine virtuelle** - spécifier un disque dur (lecteur de disque dur) ou tooindicate SSD (disque SSD) type de disque de stockage est autorisée pour les ordinateurs virtuels de hello configurés à l’aide de cette image de base.</span><span class="sxs-lookup"><span data-stu-id="f5747-132">**Virtual machine disk type** - Specify either HDD (hard-disk drive) or SSD (solid-state drive) tooindicate which storage disk type is allowed for hello virtual machines provisioned using this base image.</span></span>
    * <span data-ttu-id="f5747-133">** De machine virtuelle taille ** : sélectionnez un des éléments de hello prédéfini qui spécifient les hello cœurs de processeur, mémoire RAM et taille du disque dur de hello VM toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="f5747-133">** Virtual machine size** - Select one of hello predefined items that specify hello processor cores, RAM size, and hello hard drive size of hello VM toocreate.</span></span> 
    * <span data-ttu-id="f5747-134">**Artefacts** -tooopen sélectionnez hello **ajouter des artefacts** panneau, dans lequel vous sélectionnez et configurez les artefacts hello que vous souhaitez l’image de base tooadd toohello.</span><span class="sxs-lookup"><span data-stu-id="f5747-134">**Artifacts** - Select tooopen hello **Add artifacts** blade, in which you select and configure hello artifacts that you want tooadd toohello base image.</span></span> <span data-ttu-id="f5747-135">Pour plus d’informations sur les artefacts, consultez [Gérer les artefacts de machine virtuelle dans Azure DevTest Labs](./devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="f5747-135">For more information about artifacts, see [Manage VM artifacts in Azure DevTest Labs](./devtest-lab-add-vm-with-artifacts.md).</span></span>
    * <span data-ttu-id="f5747-136">**Paramètres avancés** -tooopen sélectionnez hello **avancé** panneau où vous configurez hello suivant les paramètres :</span><span class="sxs-lookup"><span data-stu-id="f5747-136">**Advanced settings** - Select tooopen hello **Advanced** blade where you configure hello following settings:</span></span>
        * <span data-ttu-id="f5747-137">**Réseau virtuel** -spécifiez hello souhaité de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f5747-137">**Virtual network** - Specify hello desired virtual network.</span></span>
        * <span data-ttu-id="f5747-138">**Sous-réseau** -spécifiez le sous-réseau de hello souhaité.</span><span class="sxs-lookup"><span data-stu-id="f5747-138">**Subnet** - Specify hello desired subnet.</span></span>    
        * <span data-ttu-id="f5747-139">**Configuration d’adresse IP** -Spécifie que les adresses publiques, privées ou IP partagé hello.</span><span class="sxs-lookup"><span data-stu-id="f5747-139">**IP address configuration** - Specify if you want hello Public, Private, or Shared IP addresses.</span></span> <span data-ttu-id="f5747-140">Pour plus d’informations sur les adresses IP partagées, consultez [Comprendre les adresses IP partagées dans Azure DevTest Labs](./devtest-lab-shared-ip.md).</span><span class="sxs-lookup"><span data-stu-id="f5747-140">For more information about shared IP addresses, see [Understand shared IP addresses in Azure DevTest Labs](./devtest-lab-shared-ip.md).</span></span>
        * <span data-ttu-id="f5747-141">**Rendre cet ordinateur qui peuvent être réclamés** -effectue une machine « qui peuvent être réclamés » signifie qu’il ne sera pas attribué la propriété au moment de la création de hello.</span><span class="sxs-lookup"><span data-stu-id="f5747-141">**Make this machine claimable** - Making a machine "claimable" means that it will not be assigned ownership at hello time of creation.</span></span> <span data-ttu-id="f5747-142">Au lieu de cela, les utilisateurs du laboratoire sera machine de hello tootake en mesure de la propriété (« revendications ») dans le panneau de laboratoire hello.</span><span class="sxs-lookup"><span data-stu-id="f5747-142">Instead lab users will be able tootake ownership ("claim") hello machine in hello lab's blade.</span></span>     
    * <span data-ttu-id="f5747-143">**Image** -ce champ affiche le nom de l’image de base hello sélectionnée sur le panneau précédent de hello.</span><span class="sxs-lookup"><span data-stu-id="f5747-143">**Image** - This field displays name of hello base image you selected on hello previous blade.</span></span> 
     
       ![Créer une formule](./media/devtest-lab-create-formulas/create-formula.png)

8. <span data-ttu-id="f5747-145">Sélectionnez **créer** formule de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="f5747-145">Select **Create** toocreate hello formula.</span></span>

9. <span data-ttu-id="f5747-146">Lors de la formule de hello a été créé, il s’affiche dans la liste hello sur hello **formules** panneau.</span><span class="sxs-lookup"><span data-stu-id="f5747-146">When hello formula has been created, it displays in hello list on hello **Formulas** blade.</span></span>

### <a name="create-a-formula-from-a-vm"></a><span data-ttu-id="f5747-147">Créer une formule depuis une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="f5747-147">Create a formula from a VM</span></span>
<span data-ttu-id="f5747-148">Hello étapes suivantes vous guident hello de création d’une formule basée sur une machine virtuelle existante.</span><span class="sxs-lookup"><span data-stu-id="f5747-148">hello following steps guide you through hello process of creating a formula based on an existing VM.</span></span> 

> [!NOTE]
> <span data-ttu-id="f5747-149">toocreate une formule d’une machine virtuelle, hello machine virtuelle doit avoir été créé après le 30 mars 2016.</span><span class="sxs-lookup"><span data-stu-id="f5747-149">toocreate a formula from a VM, hello VM must have been created after March 30, 2016.</span></span> 
> 
> 

1. <span data-ttu-id="f5747-150">Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="f5747-150">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="f5747-151">Sélectionnez **plus Services**, puis sélectionnez **DevTest Labs** à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="f5747-151">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="f5747-152">Dans liste hello labs, sélectionnez lab souhaité de hello.</span><span class="sxs-lookup"><span data-stu-id="f5747-152">From hello list of labs, select hello desired lab.</span></span>  
4. <span data-ttu-id="f5747-153">Sur du laboratoire hello **vue d’ensemble** panneau, VM hello select à partir de laquelle vous souhaitez formule de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="f5747-153">On hello lab's **Overview** blade, select hello VM from which you wish toocreate hello formula.</span></span>
   
    ![Machines virtuelles de labo](./media/devtest-lab-create-formulas/my-vms.png)
5. <span data-ttu-id="f5747-155">Dans le panneau de la machine virtuelle de hello, sélectionnez **créer la formule (base réutilisable)**.</span><span class="sxs-lookup"><span data-stu-id="f5747-155">On hello VM's blade, select **Create formula (reusable base)**.</span></span>
   
    ![Créer une formule](./media/devtest-lab-create-formulas/create-formula-menu.png)
6. <span data-ttu-id="f5747-157">Sur hello **créer formule** panneau, entrez un **nom** et **Description** pour votre nouvelle formule.</span><span class="sxs-lookup"><span data-stu-id="f5747-157">On hello **Create formula** blade, enter a **Name** and **Description** for your new formula.</span></span>
   
    ![Panneau Créer une formule](./media/devtest-lab-create-formulas/create-formula-blade.png)
7. <span data-ttu-id="f5747-159">Sélectionnez **OK** formule de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="f5747-159">Select **OK** toocreate hello formula.</span></span>

## <a name="modify-a-formula"></a><span data-ttu-id="f5747-160">Modifier une formule</span><span class="sxs-lookup"><span data-stu-id="f5747-160">Modify a formula</span></span>
<span data-ttu-id="f5747-161">toomodify une formule, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f5747-161">toomodify a formula, follow these steps:</span></span>

1. <span data-ttu-id="f5747-162">Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="f5747-162">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="f5747-163">Sélectionnez **plus Services**, puis sélectionnez **DevTest Labs** à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="f5747-163">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="f5747-164">Dans liste hello labs, sélectionnez lab souhaité de hello.</span><span class="sxs-lookup"><span data-stu-id="f5747-164">From hello list of labs, select hello desired lab.</span></span>  
4. <span data-ttu-id="f5747-165">Dans le panneau de hello lab, sélectionnez **formules (réutilisables bases)**.</span><span class="sxs-lookup"><span data-stu-id="f5747-165">On hello lab's blade, select **Formulas (reusable bases)**.</span></span>
   
    ![Menu de formule](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. <span data-ttu-id="f5747-167">Sur hello **les formules Lab** panneau, formule Sélectionnez hello toomodify vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="f5747-167">On hello **Lab formulas** blade, select hello formula you wish toomodify.</span></span>
6. <span data-ttu-id="f5747-168">Sur hello **mise à jour de la formule** panneau, apporter des modifications de hello souhaité, puis sélectionnez **mise à jour**.</span><span class="sxs-lookup"><span data-stu-id="f5747-168">On hello **Update formula** blade, make hello desired edits, and select **Update**.</span></span>

## <a name="delete-a-formula"></a><span data-ttu-id="f5747-169">Supprimer une formule</span><span class="sxs-lookup"><span data-stu-id="f5747-169">Delete a formula</span></span>
<span data-ttu-id="f5747-170">toodelete une formule, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f5747-170">toodelete a formula, follow these steps:</span></span>

1. <span data-ttu-id="f5747-171">Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="f5747-171">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="f5747-172">Sélectionnez **plus Services**, puis sélectionnez **DevTest Labs** à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="f5747-172">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="f5747-173">Dans liste hello labs, sélectionnez lab souhaité de hello.</span><span class="sxs-lookup"><span data-stu-id="f5747-173">From hello list of labs, select hello desired lab.</span></span>  
4. <span data-ttu-id="f5747-174">Atelier de hello **paramètres** panneau, sélectionnez **formules**.</span><span class="sxs-lookup"><span data-stu-id="f5747-174">On hello lab **Settings** blade, select **Formulas**.</span></span>
   
    ![Menu de formule](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. <span data-ttu-id="f5747-176">Sur hello **les formules Lab** panneau, sélectionnez hello des toohello de points de suspension à droite de la formule de hello vous souhaitez toodelete.</span><span class="sxs-lookup"><span data-stu-id="f5747-176">On hello **Lab formulas** blade, select hello ellipsis toohello right of hello formula you wish toodelete.</span></span>
   
    ![Menu de formule](./media/devtest-lab-manage-formulas/lab-formulas-blade.png)
6. <span data-ttu-id="f5747-178">Dans le menu contextuel de la formule hello, sélectionnez **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="f5747-178">On hello formula's context menu, select **Delete**.</span></span>
   
    ![Menu contextuel de la formule](./media/devtest-lab-manage-formulas/formula-delete-context-menu.png)
7. <span data-ttu-id="f5747-180">Sélectionnez **Oui** toohello la boîte de dialogue de la confirmation de suppression.</span><span class="sxs-lookup"><span data-stu-id="f5747-180">Select **Yes** toohello deletion confirmation dialog.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="f5747-181">Billets de blog connexes</span><span class="sxs-lookup"><span data-stu-id="f5747-181">Related blog posts</span></span>
* [<span data-ttu-id="f5747-182">Images personnalisées ou formules ?</span><span class="sxs-lookup"><span data-stu-id="f5747-182">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a><span data-ttu-id="f5747-183">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f5747-183">Next steps</span></span>
<span data-ttu-id="f5747-184">Une fois que vous avez créé une formule à utiliser lors de la création d’une machine virtuelle, étape suivante de hello est trop[ajouter un laboratoire tooyour de machine virtuelle](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="f5747-184">Once you have created a formula for use when creating a VM, hello next step is too[add a VM tooyour lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

