---
title: "Créer un laboratoire dans Azure DevTest Labs | Microsoft Docs"
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
ms.openlocfilehash: 265a968f902f53c7561c8c7e937f8eacfdb37167
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="0b876-103">Créer un laboratoire dans Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="0b876-103">Create a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="0b876-104">Un laboratoire dans Azure DevTest Labs est l’infrastructure qui comprend un groupe de ressources, telles que des machines virtuelles, qui vous permet de mieux gérer ces ressources en spécifiant des limites et des quotas.</span><span class="sxs-lookup"><span data-stu-id="0b876-104">A lab in Azure DevTest Labs is the infrastructure that encompasses a group of resources, such as Virtual Machines (VMs), that lets you better manage those resources by specifying limits and quotas.</span></span> <span data-ttu-id="0b876-105">Cet article vous guide dans le processus de création d’un laboratoire à l’aide du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0b876-105">This article walks you through the process of creating a lab using the Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0b876-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="0b876-106">Prerequisites</span></span>
<span data-ttu-id="0b876-107">Pour créer un laboratoire, vous devez avoir :</span><span class="sxs-lookup"><span data-stu-id="0b876-107">To create a lab, you need:</span></span>

* <span data-ttu-id="0b876-108">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="0b876-108">An Azure subscription.</span></span> <span data-ttu-id="0b876-109">Pour en savoir plus sur les options d’achat d’Azure, consultez [Comment acheter Azure](https://azure.microsoft.com/pricing/purchase-options/) ou [Évaluation d’un mois gratuite](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0b876-109">To learn about Azure purchase options, see [How to buy Azure](https://azure.microsoft.com/pricing/purchase-options/) or [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="0b876-110">Pour créer le laboratoire, vous devez être le propriétaire de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="0b876-110">You must be the owner of the subscription to create the lab.</span></span>

## <a name="steps-to-create-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="0b876-111">Étapes de création d’un laboratoire dans Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="0b876-111">Steps to create a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="0b876-112">Les étapes suivantes montrent comment utiliser le portail Azure pour créer un laboratoire dans Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="0b876-112">The following steps illustrate how to use the Azure portal to create a lab in Azure DevTest Labs.</span></span> 

1. <span data-ttu-id="0b876-113">Connectez-vous au [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="0b876-113">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="0b876-114">Dans le menu principal sur le côté gauche, sélectionnez **Plus de services** (en bas de la liste).</span><span class="sxs-lookup"><span data-stu-id="0b876-114">From the main menu on the left side, select **More Services** (at the bottom of the list).</span></span>

    ![Option de menu Plus de services](./media/devtest-lab-create-lab/more-services-menu-option.png)

1. <span data-ttu-id="0b876-116">Dans la liste des services disponibles, cliquez sur **DevTest Labs**.</span><span class="sxs-lookup"><span data-stu-id="0b876-116">From the list of available services, **DevTest Labs**.</span></span>
1. <span data-ttu-id="0b876-117">Dans le panneau **DevTest Labs**, sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="0b876-117">On the **DevTest Labs** blade, select **Add**.</span></span>
   
    ![Ajouter un laboratoire](./media/devtest-lab-create-lab/add-lab-button.png)

1. <span data-ttu-id="0b876-119">Dans le panneau **Créer un laboratoire de test et développement** :</span><span class="sxs-lookup"><span data-stu-id="0b876-119">On the **Create a DevTest Lab** blade:</span></span>
   
    1. <span data-ttu-id="0b876-120">Entrez un **Nom de laboratoire** pour le nouveau laboratoire.</span><span class="sxs-lookup"><span data-stu-id="0b876-120">Enter a **Lab Name** for the new lab.</span></span>
    2. <span data-ttu-id="0b876-121">Sélectionnez **l’abonnement** à associer au laboratoire.</span><span class="sxs-lookup"><span data-stu-id="0b876-121">Select the **Subscription** to associate with the lab.</span></span>
    3. <span data-ttu-id="0b876-122">Sélectionnez un **Emplacement** dans lequel stocker le laboratoire.</span><span class="sxs-lookup"><span data-stu-id="0b876-122">Select a **Location** in which to store the lab.</span></span>
    4. <span data-ttu-id="0b876-123">Sélectionnez **Arrêt automatique** pour spécifier si vous souhaitez activer l’arrêt automatique de toutes les machines virtuelles du laboratoire et en définir les paramètres.</span><span class="sxs-lookup"><span data-stu-id="0b876-123">Select **Auto-shutdown** to specify if you want to enable - and define the parameters for - the automatic shutting down of all the lab's VMs.</span></span> <span data-ttu-id="0b876-124">La fonction d’arrêt automatique est essentiellement une fonctionnalité économique dans laquelle vous pouvez spécifier les moments auxquels arrêter automatiquement la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="0b876-124">The auto-shutdown feature is mainly a cost-saving feature whereby you can specify when you want the VM to automatically be shut down.</span></span> <span data-ttu-id="0b876-125">Vous pouvez modifier les paramètres d’arrêt automatique après avoir créé le laboratoire en suivant les étapes décrites dans l’article [Gérer toutes les stratégies d’un laboratoire dans Azure DevTest Labs](./devtest-lab-set-lab-policy.md#set-auto-shutdown).</span><span class="sxs-lookup"><span data-stu-id="0b876-125">You can change auto-shutdown settings after creating the lab by following the steps outlined in the article, [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md#set-auto-shutdown).</span></span>
    5. <span data-ttu-id="0b876-126">Sélectionnez **Épingler au tableau de bord** si vous souhaitez faire apparaître un raccourci vers le laboratoire sur le tableau de bord du portail.</span><span class="sxs-lookup"><span data-stu-id="0b876-126">Select **Pin to Dashboard** if you want a shortcut of the lab to appear on the portal dashboard.</span></span>
    6. <span data-ttu-id="0b876-127">Sélectionnez **Options d’automatisation** pour obtenir des modèles Azure Resource Manager pour l’automatisation de la configuration.</span><span class="sxs-lookup"><span data-stu-id="0b876-127">Select **Automation options** to get Azure Resource Manager templates for configuration automation.</span></span> 
    7. <span data-ttu-id="0b876-128">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="0b876-128">Select **Create**.</span></span> <span data-ttu-id="0b876-129">Après avoir sélectionné **Créer**, le panneau **DevTest Labs** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="0b876-129">After selecting **Create**, the **DevTest Labs** blade displays.</span></span> <span data-ttu-id="0b876-130">Vous pouvez surveiller l’état du processus de création de laboratoire en regardant la zone **Notifications**.</span><span class="sxs-lookup"><span data-stu-id="0b876-130">You can monitor the status of the lab creation process by watching the **Notifications** area.</span></span> <span data-ttu-id="0b876-131">Une fois terminé, actualisez la page pour afficher le laboratoire nouvellement créé dans la liste des laboratoires.</span><span class="sxs-lookup"><span data-stu-id="0b876-131">Once completed, refresh the page to see the newly created lab in the list of labs.</span></span>  
    
    ![Créer un panneau de laboratoire](./media/devtest-lab-create-lab/create-devtestlab-blade.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="0b876-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0b876-133">Next steps</span></span>
<span data-ttu-id="0b876-134">Une fois que vous avez créé votre laboratoire, voici quelques étapes à prendre en compte :</span><span class="sxs-lookup"><span data-stu-id="0b876-134">Once you've created your lab, here are some next steps to consider:</span></span>

* <span data-ttu-id="0b876-135">[Sécuriser l’accès à un laboratoire](devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="0b876-135">[Secure access to a lab](devtest-lab-add-devtest-user.md).</span></span>
* <span data-ttu-id="0b876-136">[Définir des stratégies de laboratoire](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="0b876-136">[Set lab policies](devtest-lab-set-lab-policy.md).</span></span>
* <span data-ttu-id="0b876-137">[Créer un modèle de laboratoire](devtest-lab-create-template.md).</span><span class="sxs-lookup"><span data-stu-id="0b876-137">[Create a lab template](devtest-lab-create-template.md).</span></span>
* <span data-ttu-id="0b876-138">[Créer des artefacts personnalisés pour vos machines virtuelles](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="0b876-138">[Create custom artifacts for your VMs](devtest-lab-artifact-author.md).</span></span>
* <span data-ttu-id="0b876-139">[Ajouter une machine virtuelle avec des artefacts à un laboratoire](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/).</span><span class="sxs-lookup"><span data-stu-id="0b876-139">[Add a VM with artifacts to a lab](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/).</span></span>

