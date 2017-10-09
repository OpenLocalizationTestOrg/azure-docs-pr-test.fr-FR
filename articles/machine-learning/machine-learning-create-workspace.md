---
title: aaaCreate un espace de travail Machine Learning | Documents Microsoft
description: Comment toocreate un espace de travail pour Azure Machine Learning Studio
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: aa96b784-ac6c-44bc-a28a-85d49fbe90a2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: garye;bradsev;ahgyger
ms.openlocfilehash: 178293af222365993fade666124f34269d892325
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-share-an-azure-machine-learning-workspace"></a><span data-ttu-id="efac2-103">Créer et partager un espace de travail Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="efac2-103">Create and share an Azure Machine Learning workspace</span></span>
<span data-ttu-id="efac2-104">Ce menu lie tootopics qui décrivent comment tooset des hello différents environnements de science des données utilisé par hello Cortana Analytique processus (CAP).</span><span class="sxs-lookup"><span data-stu-id="efac2-104">This menu links tootopics that describe how tooset up hello various data science environments used by hello Cortana Analytics Process (CAPS).</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

<span data-ttu-id="efac2-105">toouse Azure Machine Learning Studio, vous devez toohave un espace de travail Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="efac2-105">toouse Azure Machine Learning Studio, you need toohave a Machine Learning workspace.</span></span> <span data-ttu-id="efac2-106">Cet espace de travail contienne des outils de hello vous devez toocreate, gérer et publier des expériences.</span><span class="sxs-lookup"><span data-stu-id="efac2-106">This workspace contains hello tools you need toocreate, manage, and publish experiments.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="toocreate-a-workspace"></a><span data-ttu-id="efac2-107">toocreate un espace de travail</span><span class="sxs-lookup"><span data-stu-id="efac2-107">toocreate a workspace</span></span>
1. <span data-ttu-id="efac2-108">Connectez-vous à toohello [portail Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="efac2-108">Sign in toohello [Azure portal](https://portal.azure.com/)</span></span>

    > [!NOTE]
    > <span data-ttu-id="efac2-109">toosign dans et créer un espace de travail, vous devez toobe administrateur d’abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="efac2-109">toosign in and create a workspace, you need toobe an Azure subscription administrator.</span></span> 
    >
    > 

2. <span data-ttu-id="efac2-110">Cliquez sur **+Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="efac2-110">Click **+New**</span></span>

3. <span data-ttu-id="efac2-111">Sélectionnez **Intelligence + analyse**, puis cliquez sur **Espace de travail Machine Learning** et sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="efac2-111">Select **Intelligence + analytics**, click **Machine Learning Workspace**, then click **Create**</span></span>

4. <span data-ttu-id="efac2-112">Entrez vos informations d’espace de travail.</span><span class="sxs-lookup"><span data-stu-id="efac2-112">Enter your workspace information</span></span>

    - <span data-ttu-id="efac2-113">Hello *nom de l’espace de travail* peuvent être des caractères too260, se termine ne pas par un espace.</span><span class="sxs-lookup"><span data-stu-id="efac2-113">hello *workspace name* may be up too260 characters, not ending in a space.</span></span> <span data-ttu-id="efac2-114">nom de Hello ne peut pas contenir ces caractères :`< > * % & : \ ? + /`</span><span class="sxs-lookup"><span data-stu-id="efac2-114">hello name can't include these characters: `< > * % & : \ ? + /`</span></span>
    - <span data-ttu-id="efac2-115">Hello *plan de service web* vous choisissez (ou créer), ainsi que de hello associé *tarification* vous sélectionnez, est utilisé si vous déployez des services web à partir de cet espace de travail.</span><span class="sxs-lookup"><span data-stu-id="efac2-115">hello *web service plan* you choose (or create), along with hello associated *pricing tier* you select, is used if you deploy web services from this workspace.</span></span>

    ![Créer un espace de travail](media/machine-learning-create-workspace/create-new-workspace.png)

5. <span data-ttu-id="efac2-117">Cliquez sur **Créer**</span><span class="sxs-lookup"><span data-stu-id="efac2-117">Click **Create**</span></span>

<span data-ttu-id="efac2-118">Une fois que l’espace de travail hello est déployé, vous pouvez l’ouvrir dans Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="efac2-118">Once hello workspace is deployed, you can open it in Machine Learning Studio.</span></span>

1. <span data-ttu-id="efac2-119">Parcourir tooMachine Learning Studio à [https://studio.azureml.net/](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="efac2-119">Browse tooMachine Learning Studio at [https://studio.azureml.net/](https://studio.azureml.net/).</span></span>

2. <span data-ttu-id="efac2-120">Sélectionnez votre espace de travail dans l’angle supérieure droite de hello.</span><span class="sxs-lookup"><span data-stu-id="efac2-120">Select your workspace in hello upper-right-hand corner.</span></span>

    ![Sélectionner un espace de travail](media/machine-learning-create-workspace/open-workspace.png)

3. <span data-ttu-id="efac2-122">Cliquez sur **my experiments (mes expérimentations)**.</span><span class="sxs-lookup"><span data-stu-id="efac2-122">Click **my experiments**.</span></span>

    ![Ouvrir des expérimentations](media/machine-learning-create-workspace/my-experiments.png)

<span data-ttu-id="efac2-124">Pour plus d’informations sur la gestion de votre espace de travail, consultez [Gestion d’un espace de travail Azure Machine Learning](machine-learning-manage-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="efac2-124">For information about managing your workspace, see [Manage an Azure Machine Learning workspace](machine-learning-manage-workspace.md).</span></span>
<span data-ttu-id="efac2-125">Si vous rencontrez un problème de création de votre espace de travail, consultez [guide de dépannage : créer et connecter l’espace de travail Machine Learning tooa](machine-learning-troubleshooting-creating-ml-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="efac2-125">If you encounter a problem creating your workspace, see [Troubleshooting guide: Create and connect tooa Machine Learning workspace](machine-learning-troubleshooting-creating-ml-workspace.md).</span></span>


## <a name="sharing-an-azure-machine-learning-workspace"></a><span data-ttu-id="efac2-126">Partage d’un espace de travail Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="efac2-126">Sharing an Azure Machine Learning workspace</span></span>
<span data-ttu-id="efac2-127">Une fois qu’un espace de travail Machine Learning est créé, vous pouvez inviter les utilisateurs tooyour espace de travail tooshare accès tooyour espace de travail et tous les ses expériences, jeux de données, ordinateurs portables, etc.. Vous pouvez ajouter des utilisateurs dans l’un des deux rôles :</span><span class="sxs-lookup"><span data-stu-id="efac2-127">Once a Machine Learning workspace is created, you can invite users tooyour workspace tooshare access tooyour workspace and all its experiments, datasets, notebooks, etc. You can add users in one of two roles:</span></span>

* <span data-ttu-id="efac2-128">**Utilisateur** -un utilisateur de l’espace de travail peut créer, ouvrir, modifier et supprimer des expériences, jeux de données, etc. dans l’espace de travail hello.</span><span class="sxs-lookup"><span data-stu-id="efac2-128">**User** - A workspace user can create, open, modify, and delete experiments, datasets, etc. in hello workspace.</span></span>
* <span data-ttu-id="efac2-129">**Propriétaire** - invite un propriétaire et supprimer des utilisateurs dans hello espace de travail, ajout toowhat un utilisateur peuvent faire.</span><span class="sxs-lookup"><span data-stu-id="efac2-129">**Owner** - An owner can invite and remove users in hello workspace, in addition toowhat a user can do.</span></span>

> [!NOTE]
> <span data-ttu-id="efac2-130">compte d’administrateur Hello qui crée l’espace de travail hello est automatiquement ajouté toohello espace de travail en tant que propriétaire de l’espace de travail.</span><span class="sxs-lookup"><span data-stu-id="efac2-130">hello administrator account that creates hello workspace is automatically added toohello workspace as workspace Owner.</span></span> <span data-ttu-id="efac2-131">Toutefois, autres administrateurs ou des utilisateurs dans la mesure où abonnement ne sont pas automatiquement accordé l’accès toohello espace de travail : vous devez tooinvite les explicitement.</span><span class="sxs-lookup"><span data-stu-id="efac2-131">However, other administrators or users in that subscription are not automatically granted access toohello workspace - you need tooinvite them explicitly.</span></span>
> 
> 

### <a name="tooshare-a-workspace"></a><span data-ttu-id="efac2-132">tooshare un espace de travail</span><span class="sxs-lookup"><span data-stu-id="efac2-132">tooshare a workspace</span></span>

1. <span data-ttu-id="efac2-133">Se connecter tooMachine Learning Studio à [https://studio.azureml.net/Home](https://studio.azureml.net/Home)</span><span class="sxs-lookup"><span data-stu-id="efac2-133">Sign in tooMachine Learning Studio at [https://studio.azureml.net/Home](https://studio.azureml.net/Home)</span></span>

2. <span data-ttu-id="efac2-134">Dans le volet gauche de hello, cliquez sur **paramètres**</span><span class="sxs-lookup"><span data-stu-id="efac2-134">In hello left panel, click **SETTINGS**</span></span>

3. <span data-ttu-id="efac2-135">Cliquez sur hello **utilisateurs** onglet</span><span class="sxs-lookup"><span data-stu-id="efac2-135">Click hello **USERS** tab</span></span>

4. <span data-ttu-id="efac2-136">Cliquez sur **inviter des utilisateurs plus** bas hello de page de hello</span><span class="sxs-lookup"><span data-stu-id="efac2-136">Click **INVITE MORE USERS** at hello bottom of hello page</span></span>

    ![Paramètres Studio](media/machine-learning-create-workspace/settings.png)

5. <span data-ttu-id="efac2-138">Entrez une ou plusieurs adresses e-mail.</span><span class="sxs-lookup"><span data-stu-id="efac2-138">Enter one or more email addresses.</span></span> <span data-ttu-id="efac2-139">les utilisateurs de Hello besoin d’un compte Microsoft valide ou un compte professionnel (à partir d’Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="efac2-139">hello users need a valid Microsoft account or an organizational account (from Azure Active Directory).</span></span>

6. <span data-ttu-id="efac2-140">Sélectionnez si vous souhaitez que les utilisateurs de hello tooadd en tant que propriétaire ou utilisateur.</span><span class="sxs-lookup"><span data-stu-id="efac2-140">Select whether you want tooadd hello users as Owner or User.</span></span>

7. <span data-ttu-id="efac2-141">Cliquez sur hello **OK** coche.</span><span class="sxs-lookup"><span data-stu-id="efac2-141">Click hello **OK** checkmark button.</span></span>

<span data-ttu-id="efac2-142">Chaque utilisateur que vous ajoutez recevra un e-mail contenant des instructions sur le mode de partage de l’espace de travail de toosign dans toohello.</span><span class="sxs-lookup"><span data-stu-id="efac2-142">Each user you add will receive an email with instructions on how toosign in toohello shared workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="efac2-143">Pour toodeploy en mesure de toobe les utilisateurs ou gérer des services web dans cet espace de travail, ils doivent être un contributeur ou un administrateur Bonjour abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="efac2-143">For users toobe able toodeploy or manage web services in this workspace, they must be a contributor or administrator in hello Azure subscription.</span></span> 



