---
title: "Création d'un espace de travail Machine Learning | Microsoft Docs"
description: "Création d’un espace de travail pour Microsoft Azure Machine Learning Studio."
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
ms.openlocfilehash: 182a34822e71d63f4d7229548ae3f59d9f195337
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-share-an-azure-machine-learning-workspace"></a><span data-ttu-id="d21dd-103">Créer et partager un espace de travail Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d21dd-103">Create and share an Azure Machine Learning workspace</span></span>
<span data-ttu-id="d21dd-104">Ce menu pointe vers des rubriques qui décrivent comment configurer les différents environnements de science de données utilisés par le processus d’analyse Cortana (CAP).</span><span class="sxs-lookup"><span data-stu-id="d21dd-104">This menu links to topics that describe how to set up the various data science environments used by the Cortana Analytics Process (CAPS).</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

<span data-ttu-id="d21dd-105">Pour utiliser Azure Machine Learning Studio, vous devez disposer d’un espace de travail Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="d21dd-105">To use Azure Machine Learning Studio, you need to have a Machine Learning workspace.</span></span> <span data-ttu-id="d21dd-106">Cet espace de travail contient les outils dont vous avez besoin pour créer, gérer et publier des expériences.</span><span class="sxs-lookup"><span data-stu-id="d21dd-106">This workspace contains the tools you need to create, manage, and publish experiments.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="to-create-a-workspace"></a><span data-ttu-id="d21dd-107">Pour créer un espace de travail</span><span class="sxs-lookup"><span data-stu-id="d21dd-107">To create a workspace</span></span>
1. <span data-ttu-id="d21dd-108">Connectez-vous au [portail Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="d21dd-108">Sign in to the [Azure portal](https://portal.azure.com/)</span></span>

    > [!NOTE]
    > <span data-ttu-id="d21dd-109">Pour vous connecter et créer un espace de travail, vous devez être un administrateur d’abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="d21dd-109">To sign in and create a workspace, you need to be an Azure subscription administrator.</span></span> 
    >
    > 

2. <span data-ttu-id="d21dd-110">Cliquez sur **+Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="d21dd-110">Click **+New**</span></span>

3. <span data-ttu-id="d21dd-111">Sélectionnez **Intelligence + analyse**, puis cliquez sur **Espace de travail Machine Learning** et sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="d21dd-111">Select **Intelligence + analytics**, click **Machine Learning Workspace**, then click **Create**</span></span>

4. <span data-ttu-id="d21dd-112">Entrez vos informations d’espace de travail.</span><span class="sxs-lookup"><span data-stu-id="d21dd-112">Enter your workspace information</span></span>

    - <span data-ttu-id="d21dd-113">Le *Nom de l’espace de travail* peut contenir jusqu’à 260 caractères. Il ne doit pas se terminer par un espace.</span><span class="sxs-lookup"><span data-stu-id="d21dd-113">The *workspace name* may be up to 260 characters, not ending in a space.</span></span> <span data-ttu-id="d21dd-114">Le nom ne peut pas contenir ces caractères : `< > * % & : \ ? + /`</span><span class="sxs-lookup"><span data-stu-id="d21dd-114">The name can't include these characters: `< > * % & : \ ? + /`</span></span>
    - <span data-ttu-id="d21dd-115">Le *plan de service web* que vous choisissez (ou créez), ainsi que le *niveau tarifaire* associé que vous sélectionnez, est utilisé si vous déployez des services web à partir de cet espace de travail.</span><span class="sxs-lookup"><span data-stu-id="d21dd-115">The *web service plan* you choose (or create), along with the associated *pricing tier* you select, is used if you deploy web services from this workspace.</span></span>

    ![Créer un espace de travail](media/machine-learning-create-workspace/create-new-workspace.png)

5. <span data-ttu-id="d21dd-117">Cliquez sur **Créer**</span><span class="sxs-lookup"><span data-stu-id="d21dd-117">Click **Create**</span></span>

<span data-ttu-id="d21dd-118">Une fois l’espace de travail déployé, vous pouvez l’ouvrir dans Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="d21dd-118">Once the workspace is deployed, you can open it in Machine Learning Studio.</span></span>

1. <span data-ttu-id="d21dd-119">Accédez à Machine Learning Studio à l’adresse [https://studio.azureml.net](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="d21dd-119">Browse to Machine Learning Studio at [https://studio.azureml.net/](https://studio.azureml.net/).</span></span>

2. <span data-ttu-id="d21dd-120">Sélectionnez votre espace de travail dans le coin supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="d21dd-120">Select your workspace in the upper-right-hand corner.</span></span>

    ![Sélectionner un espace de travail](media/machine-learning-create-workspace/open-workspace.png)

3. <span data-ttu-id="d21dd-122">Cliquez sur **my experiments (mes expérimentations)**.</span><span class="sxs-lookup"><span data-stu-id="d21dd-122">Click **my experiments**.</span></span>

    ![Ouvrir des expérimentations](media/machine-learning-create-workspace/my-experiments.png)

<span data-ttu-id="d21dd-124">Pour plus d’informations sur la gestion de votre espace de travail, consultez [Gestion d’un espace de travail Azure Machine Learning](machine-learning-manage-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="d21dd-124">For information about managing your workspace, see [Manage an Azure Machine Learning workspace](machine-learning-manage-workspace.md).</span></span>
<span data-ttu-id="d21dd-125">En cas de problème lors de la création de votre espace de travail, consultez l’article [Guide de résolution des problèmes : création d’un espace de travail Machine Learning et connexion à celui-ci](machine-learning-troubleshooting-creating-ml-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="d21dd-125">If you encounter a problem creating your workspace, see [Troubleshooting guide: Create and connect to a Machine Learning workspace](machine-learning-troubleshooting-creating-ml-workspace.md).</span></span>


## <a name="sharing-an-azure-machine-learning-workspace"></a><span data-ttu-id="d21dd-126">Partage d’un espace de travail Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d21dd-126">Sharing an Azure Machine Learning workspace</span></span>
<span data-ttu-id="d21dd-127">Une fois l’espace de travail Machine Learning créé, vous pouvez y inviter les utilisateurs pour partager l’accès à votre espace de travail et à l’ensemble de ses expérimentations, jeux de données, bloc-notes, etc. Vous pouvez ajouter des utilisateurs dans l’un des deux rôles :</span><span class="sxs-lookup"><span data-stu-id="d21dd-127">Once a Machine Learning workspace is created, you can invite users to your workspace to share access to your workspace and all its experiments, datasets, notebooks, etc. You can add users in one of two roles:</span></span>

* <span data-ttu-id="d21dd-128">**Utilisateur** : un utilisateur de l’espace de travail peut créer, ouvrir, modifier et supprimer des expérimentations, jeux de données, etc. dans l’espace de travail.</span><span class="sxs-lookup"><span data-stu-id="d21dd-128">**User** - A workspace user can create, open, modify, and delete experiments, datasets, etc. in the workspace.</span></span>
* <span data-ttu-id="d21dd-129">**Propriétaire** : un propriétaire peut inviter et supprimer des utilisateurs dans l’espace de travail, ainsi que les actions qu’ils sont autorisés à effectuer.</span><span class="sxs-lookup"><span data-stu-id="d21dd-129">**Owner** - An owner can invite and remove users in the workspace, in addition to what a user can do.</span></span>

> [!NOTE]
> <span data-ttu-id="d21dd-130">Le compte d’administrateur qui crée l’espace de travail y est automatiquement ajouté en tant que propriétaire de l’espace de travail.</span><span class="sxs-lookup"><span data-stu-id="d21dd-130">The administrator account that creates the workspace is automatically added to the workspace as workspace Owner.</span></span> <span data-ttu-id="d21dd-131">Toutefois, les autres administrateurs ou utilisateurs de cet abonnement ne bénéficient pas automatiquement d’un accès à l’espace de travail : vous devez les inviter explicitement.</span><span class="sxs-lookup"><span data-stu-id="d21dd-131">However, other administrators or users in that subscription are not automatically granted access to the workspace - you need to invite them explicitly.</span></span>
> 
> 

### <a name="to-share-a-workspace"></a><span data-ttu-id="d21dd-132">Pour partager un espace de travail</span><span class="sxs-lookup"><span data-stu-id="d21dd-132">To share a workspace</span></span>

1. <span data-ttu-id="d21dd-133">Connectez-vous à Machine Learning Studio à l’adresse [https://studio.azureml.net/Home](https://studio.azureml.net/Home).</span><span class="sxs-lookup"><span data-stu-id="d21dd-133">Sign in to Machine Learning Studio at [https://studio.azureml.net/Home](https://studio.azureml.net/Home)</span></span>

2. <span data-ttu-id="d21dd-134">Dans le panneau gauche, cliquez sur **SETTINGS (PARAMÈTRES)**.</span><span class="sxs-lookup"><span data-stu-id="d21dd-134">In the left panel, click **SETTINGS**</span></span>

3. <span data-ttu-id="d21dd-135">Cliquez sur l’onglet **USERS (UTILISATEURS)**.</span><span class="sxs-lookup"><span data-stu-id="d21dd-135">Click the **USERS** tab</span></span>

4. <span data-ttu-id="d21dd-136">En bas de la page, cliquez sur **INVITE MORE USERS (INVITER D’AUTRES UTILISATEURS)**.</span><span class="sxs-lookup"><span data-stu-id="d21dd-136">Click **INVITE MORE USERS** at the bottom of the page</span></span>

    ![Paramètres Studio](media/machine-learning-create-workspace/settings.png)

5. <span data-ttu-id="d21dd-138">Entrez une ou plusieurs adresses e-mail.</span><span class="sxs-lookup"><span data-stu-id="d21dd-138">Enter one or more email addresses.</span></span> <span data-ttu-id="d21dd-139">Les utilisateurs ont besoin d’un compte Microsoft valide ou d’un compte d’entreprise (issu d’Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="d21dd-139">The users need a valid Microsoft account or an organizational account (from Azure Active Directory).</span></span>

6. <span data-ttu-id="d21dd-140">Indiquez si vous voulez ajouter des utilisateurs en tant que propriétaire ou utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d21dd-140">Select whether you want to add the users as Owner or User.</span></span>

7. <span data-ttu-id="d21dd-141">Cliquez sur la coche **OK** .</span><span class="sxs-lookup"><span data-stu-id="d21dd-141">Click the **OK** checkmark button.</span></span>

<span data-ttu-id="d21dd-142">Chaque utilisateur ajouté reçoit un e-mail contenant des instructions de connexion à l’espace de travail partagé.</span><span class="sxs-lookup"><span data-stu-id="d21dd-142">Each user you add will receive an email with instructions on how to sign in to the shared workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="d21dd-143">Pour que les utilisateurs puissent déployer ou gérer des services web dans cet espace de travail, ils doivent être collaborateurs ou administrateurs dans l’abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="d21dd-143">For users to be able to deploy or manage web services in this workspace, they must be a contributor or administrator in the Azure subscription.</span></span> 



