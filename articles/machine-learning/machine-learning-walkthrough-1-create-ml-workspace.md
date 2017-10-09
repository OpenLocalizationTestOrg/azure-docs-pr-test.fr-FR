---
title: "Étape 1 : création d’un espace de travail Machine Learning | Microsoft Docs"
description: "Étape 1 de hello développer la procédure pas à pas une solution prédictive : Découvrez comment tooset un nouvel espace de travail Azure Machine Learning Studio."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: b3c97e3d-16ba-4e42-9657-2562854a1e04
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 93d2e240826db9768e85b00cab0eb62510b4efb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-1-create-a-machine-learning-workspace"></a><span data-ttu-id="6d877-103">Étape 1 de la procédure pas à pas : création d’un espace de travail Machine Learning</span><span class="sxs-lookup"><span data-stu-id="6d877-103">Walkthrough Step 1: Create a Machine Learning workspace</span></span>
<span data-ttu-id="6d877-104">Ceci est hello première étape de la procédure pas à pas de hello, [développer une solution prédictive analytique dans Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).</span><span class="sxs-lookup"><span data-stu-id="6d877-104">This is hello first step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).</span></span>

1. <span data-ttu-id="6d877-105">**Créer un espace de travail Machine Learning**</span><span class="sxs-lookup"><span data-stu-id="6d877-105">**Create a Machine Learning workspace**</span></span>
2. [<span data-ttu-id="6d877-106">Télécharger des données existantes</span><span class="sxs-lookup"><span data-stu-id="6d877-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="6d877-107">Créer une expérience</span><span class="sxs-lookup"><span data-stu-id="6d877-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="6d877-108">L’apprentissage et évaluer des modèles de hello</span><span class="sxs-lookup"><span data-stu-id="6d877-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="6d877-109">Déployer le service Web de hello</span><span class="sxs-lookup"><span data-stu-id="6d877-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="6d877-110">Accéder au service Web de hello</span><span class="sxs-lookup"><span data-stu-id="6d877-110">Access hello Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<!-- This needs toobe updated toorefer toohello new way of creating workspaces in hello Ibiza portal -->

<span data-ttu-id="6d877-111">toouse Machine Learning Studio, vous devez toohave un espace de travail Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="6d877-111">toouse Machine Learning Studio, you need toohave a Microsoft Azure Machine Learning workspace.</span></span> <span data-ttu-id="6d877-112">Cet espace de travail contienne des outils de hello vous devez toocreate, gérer et publier des expériences.</span><span class="sxs-lookup"><span data-stu-id="6d877-112">This workspace contains hello tools you need toocreate, manage, and publish experiments.</span></span>  

<!--
## toocreate a workspace
1. Sign in toohello [Azure classic portal](https://manage.windowsazure.com).
2. In hello  Azure services panel, click **MACHINE LEARNING**.  
   ![Create workspace][1]
3. Click **CREATE AN ML WORKSPACE**.
4. On hello **QUICK CREATE** page, enter your workspace information and then click **CREATE AN ML WORKSPACE**.
-->

<span data-ttu-id="6d877-113">administrateur Hello pour votre abonnement Azure a besoin d’espace de travail toocreate hello et puis de vous ajouter en tant que propriétaire ou contributeur.</span><span class="sxs-lookup"><span data-stu-id="6d877-113">hello administrator for your Azure subscription needs toocreate hello workspace and then add you as an owner or contributor.</span></span> <span data-ttu-id="6d877-114">Pour plus d’informations, consultez [Créer et partager un espace de travail Azure Machine Learning](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="6d877-114">For details, see [Create and share an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

<span data-ttu-id="6d877-115">Une fois votre espace de travail créé, ouvrez Machine Learning Studio ([https://studio.azureml.net/Home](https://studio.azureml.net/Home)).</span><span class="sxs-lookup"><span data-stu-id="6d877-115">After your workspace is created, open Machine Learning Studio ([https://studio.azureml.net/Home](https://studio.azureml.net/Home)).</span></span> <span data-ttu-id="6d877-116">Si vous avez plus d’un espace de travail, vous pouvez sélectionner l’espace de travail hello dans la barre d’outils hello hello haut à droite de la fenêtre hello.</span><span class="sxs-lookup"><span data-stu-id="6d877-116">If you have more than one workspace, you can select hello workspace in hello toolbar in hello upper-right corner of hello window.</span></span>

![Sélection de l’espace de travail dans Studio][2]

> [!TIP]
> <span data-ttu-id="6d877-118">Si un propriétaire de l’espace de travail hello ont été apportées, vous pouvez partager des expériences hello sur lequel vous travaillez en invitant à d’autres toohello espace de travail.</span><span class="sxs-lookup"><span data-stu-id="6d877-118">If you were made an owner of hello workspace, you can share hello experiments you're working on by inviting others toohello workspace.</span></span> <span data-ttu-id="6d877-119">Vous pouvez faire cela dans Machine Learning Studio sur hello **paramètres** page.</span><span class="sxs-lookup"><span data-stu-id="6d877-119">You can do this in Machine Learning Studio on hello **SETTINGS** page.</span></span> <span data-ttu-id="6d877-120">Vous devez simplement le compte Microsoft de hello ou compte professionnel pour chaque utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6d877-120">You just need hello Microsoft account or organizational account for each user.</span></span>
> 
> <span data-ttu-id="6d877-121">Sur hello **paramètres** , cliquez sur **utilisateurs**, puis cliquez sur **inviter des utilisateurs plus** bas hello de fenêtre hello.</span><span class="sxs-lookup"><span data-stu-id="6d877-121">On hello **SETTINGS** page, click **USERS**, then click **INVITE MORE USERS** at hello bottom of hello window.</span></span>
> 
> 

- - -
<span data-ttu-id="6d877-122">**Suivant : [Téléchargement de données existantes](machine-learning-walkthrough-2-upload-data.md)**</span><span class="sxs-lookup"><span data-stu-id="6d877-122">**Next: [Upload existing data](machine-learning-walkthrough-2-upload-data.md)**</span></span>

[1]: ./media/machine-learning-walkthrough-1-create-ml-workspace/create1.png
[2]: ./media/machine-learning-walkthrough-1-create-ml-workspace/open-workspace.png
