---
title: aaaCreate un laboratoire dans Azure DevTest Labs | Documents Microsoft
description: "Créer un laboratoire dans Azure DevTest Labs pour les machines virtuelles"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 8b6d3e70-6528-42a4-a2ef-449575d0f928
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/30/2017
ms.author: tarcher
ms.openlocfilehash: 2ec5498f10e0cc06a196a71e319e340937abb1a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="63103-103">Créer un laboratoire dans Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="63103-103">Create a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="63103-104">Un laboratoire dans Azure DevTest Labs est infrastructure hello englobe un groupe de ressources, telles que les Machines virtuelles (VM), qui vous permet de mieux gérer ces ressources en spécifiant des limites et quotas.</span><span class="sxs-lookup"><span data-stu-id="63103-104">A lab in Azure DevTest Labs is hello infrastructure that encompasses a group of resources, such as Virtual Machines (VMs), that lets you better manage those resources by specifying limits and quotas.</span></span> <span data-ttu-id="63103-105">Cet article vous guide tout au long des processus de hello de création d’un laboratoire à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="63103-105">This article walks you through hello process of creating a lab using hello Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="63103-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="63103-106">Prerequisites</span></span>
<span data-ttu-id="63103-107">toocreate un laboratoire, vous devez :</span><span class="sxs-lookup"><span data-stu-id="63103-107">toocreate a lab, you need:</span></span>

* <span data-ttu-id="63103-108">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="63103-108">An Azure subscription.</span></span> <span data-ttu-id="63103-109">toolearn sur les options d’achat d’Azure, consultez [comment toobuy Azure](https://azure.microsoft.com/pricing/purchase-options/) ou [version d’évaluation d’un mois gratuite](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="63103-109">toolearn about Azure purchase options, see [How toobuy Azure](https://azure.microsoft.com/pricing/purchase-options/) or [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="63103-110">Vous devez être propriétaire de hello du laboratoire de hello abonnement toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="63103-110">You must be hello owner of hello subscription toocreate hello lab.</span></span>

## <a name="steps-toocreate-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="63103-111">Étapes toocreate un laboratoire dans Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="63103-111">Steps toocreate a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="63103-112">Hello suit illustre comment toouse hello toocreate portail Azure, un laboratoire dans Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="63103-112">hello following steps illustrate how toouse hello Azure portal toocreate a lab in Azure DevTest Labs.</span></span> 

1. <span data-ttu-id="63103-113">Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="63103-113">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="63103-114">À partir du menu principal de hello sur le côté gauche de hello, sélectionnez **plus Services** (bas hello de hello liste).</span><span class="sxs-lookup"><span data-stu-id="63103-114">From hello main menu on hello left side, select **More Services** (at hello bottom of hello list).</span></span>

    ![Option de menu Plus de services](./media/devtest-lab-create-lab/more-services-menu-option.png)

1. <span data-ttu-id="63103-116">À partir de la liste de hello des services disponibles, **DevTest Labs**.</span><span class="sxs-lookup"><span data-stu-id="63103-116">From hello list of available services, **DevTest Labs**.</span></span>
1. <span data-ttu-id="63103-117">Sur hello **DevTest Labs** panneau, sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="63103-117">On hello **DevTest Labs** blade, select **Add**.</span></span>
   
    ![Ajouter un laboratoire](./media/devtest-lab-create-lab/add-lab-button.png)

1. <span data-ttu-id="63103-119">Sur hello **créer un laboratoire DevTest** panneau :</span><span class="sxs-lookup"><span data-stu-id="63103-119">On hello **Create a DevTest Lab** blade:</span></span>
   
    1. <span data-ttu-id="63103-120">Entrez un **nom Lab** atelier de nouveau hello.</span><span class="sxs-lookup"><span data-stu-id="63103-120">Enter a **Lab Name** for hello new lab.</span></span>
    2. <span data-ttu-id="63103-121">Sélectionnez hello **abonnement** tooassociate Lab, hello.</span><span class="sxs-lookup"><span data-stu-id="63103-121">Select hello **Subscription** tooassociate with hello lab.</span></span>
    3. <span data-ttu-id="63103-122">Sélectionnez un **emplacement** dans le laboratoire de hello toostore.</span><span class="sxs-lookup"><span data-stu-id="63103-122">Select a **Location** in which toostore hello lab.</span></span>
    4. <span data-ttu-id="63103-123">Sélectionnez **arrêt automatique** toospecify si vous souhaitez tooenable - et paramètres hello - hello automatique d’arrêt des machines virtuelles de tous les hello lab.</span><span class="sxs-lookup"><span data-stu-id="63103-123">Select **Auto-shutdown** toospecify if you want tooenable - and define hello parameters for - hello automatic shutting down of all hello lab's VMs.</span></span> <span data-ttu-id="63103-124">fonction d’arrêt automatique Hello est principalement une fonctionnalité de l’enregistrement du coût par laquelle vous pouvez spécifier lorsque vous souhaitez que la machine virtuelle de hello tooautomatically être arrêté.</span><span class="sxs-lookup"><span data-stu-id="63103-124">hello auto-shutdown feature is mainly a cost-saving feature whereby you can specify when you want hello VM tooautomatically be shut down.</span></span> <span data-ttu-id="63103-125">Vous pouvez modifier les paramètres de l’arrêt automatique après avoir créé le laboratoire de hello en suivant les étapes de hello décrites dans l’article hello, [gérer toutes les stratégies pour un atelier de Azure DevTest Labs](./devtest-lab-set-lab-policy.md#set-auto-shutdown).</span><span class="sxs-lookup"><span data-stu-id="63103-125">You can change auto-shutdown settings after creating hello lab by following hello steps outlined in hello article, [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md#set-auto-shutdown).</span></span>
    5. <span data-ttu-id="63103-126">Sélectionnez **tooDashboard du code confidentiel** si vous souhaitez un raccourci de tooappear de laboratoire hello sur le tableau de bord de portail hello.</span><span class="sxs-lookup"><span data-stu-id="63103-126">Select **Pin tooDashboard** if you want a shortcut of hello lab tooappear on hello portal dashboard.</span></span>
    6. <span data-ttu-id="63103-127">Sélectionnez **options d’automatisation** tooget les modèles Azure Resource Manager pour l’automatisation de la configuration.</span><span class="sxs-lookup"><span data-stu-id="63103-127">Select **Automation options** tooget Azure Resource Manager templates for configuration automation.</span></span> 
    7. <span data-ttu-id="63103-128">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="63103-128">Select **Create**.</span></span> <span data-ttu-id="63103-129">Après avoir sélectionné **créer**, hello **DevTest Labs** panneau affiche.</span><span class="sxs-lookup"><span data-stu-id="63103-129">After selecting **Create**, hello **DevTest Labs** blade displays.</span></span> <span data-ttu-id="63103-130">Vous pouvez surveiller l’état hello du processus de création de laboratoire hello en regardant hello **Notifications** zone.</span><span class="sxs-lookup"><span data-stu-id="63103-130">You can monitor hello status of hello lab creation process by watching hello **Notifications** area.</span></span> <span data-ttu-id="63103-131">Une fois terminé, actualisez le laboratoire de hello page toosee hello nouvellement créé dans la liste hello des laboratoires.</span><span class="sxs-lookup"><span data-stu-id="63103-131">Once completed, refresh hello page toosee hello newly created lab in hello list of labs.</span></span>  
    
    ![Créer un panneau de laboratoire](./media/devtest-lab-create-lab/create-devtestlab-blade.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="63103-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="63103-133">Next steps</span></span>
<span data-ttu-id="63103-134">Une fois que vous avez créé votre laboratoire, voici quelques tooconsider étapes suivant :</span><span class="sxs-lookup"><span data-stu-id="63103-134">Once you've created your lab, here are some next steps tooconsider:</span></span>

* <span data-ttu-id="63103-135">[Laboratoire tooa de sécuriser l’accès](devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="63103-135">[Secure access tooa lab](devtest-lab-add-devtest-user.md).</span></span>
* <span data-ttu-id="63103-136">[Définir des stratégies de laboratoire](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="63103-136">[Set lab policies](devtest-lab-set-lab-policy.md).</span></span>
* <span data-ttu-id="63103-137">[Créer un modèle de laboratoire](devtest-lab-create-template.md).</span><span class="sxs-lookup"><span data-stu-id="63103-137">[Create a lab template](devtest-lab-create-template.md).</span></span>
* <span data-ttu-id="63103-138">[Créer des artefacts personnalisés pour vos machines virtuelles](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="63103-138">[Create custom artifacts for your VMs](devtest-lab-artifact-author.md).</span></span>
* <span data-ttu-id="63103-139">[Ajouter une machine virtuelle avec lab de tooa artefacts](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/).</span><span class="sxs-lookup"><span data-stu-id="63103-139">[Add a VM with artifacts tooa lab](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/).</span></span>

