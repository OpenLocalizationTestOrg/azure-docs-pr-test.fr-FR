---
title: "Étape 1 : création d’un espace de travail Machine Learning | Microsoft Docs"
description: "Étape 1 de la procédure pas à pas de développement d’une solution prédictive : apprenez à configurer un nouvel espace de travail Azure Machine Learning Studio."
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
ms.openlocfilehash: 8ca42ef8f5314866301f5c9e93caa90dc837a66e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-1-create-a-machine-learning-workspace"></a><span data-ttu-id="fb2c5-103">Étape 1 de la procédure pas à pas : création d’un espace de travail Machine Learning</span><span class="sxs-lookup"><span data-stu-id="fb2c5-103">Walkthrough Step 1: Create a Machine Learning workspace</span></span>
<span data-ttu-id="fb2c5-104">Voici la première étape de la procédure pas à pas [Développement d'une solution d'analyse prédictive dans Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).</span><span class="sxs-lookup"><span data-stu-id="fb2c5-104">This is the first step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).</span></span>

1. <span data-ttu-id="fb2c5-105">**Créer un espace de travail Machine Learning**</span><span class="sxs-lookup"><span data-stu-id="fb2c5-105">**Create a Machine Learning workspace**</span></span>
2. [<span data-ttu-id="fb2c5-106">Télécharger des données existantes</span><span class="sxs-lookup"><span data-stu-id="fb2c5-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="fb2c5-107">Créer une expérience</span><span class="sxs-lookup"><span data-stu-id="fb2c5-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="fb2c5-108">Former et évaluer les modèles</span><span class="sxs-lookup"><span data-stu-id="fb2c5-108">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="fb2c5-109">Déployer le service web</span><span class="sxs-lookup"><span data-stu-id="fb2c5-109">Deploy the Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="fb2c5-110">Accéder au service web</span><span class="sxs-lookup"><span data-stu-id="fb2c5-110">Access the Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<!-- This needs to be updated to refer to the new way of creating workspaces in the Ibiza portal -->

<span data-ttu-id="fb2c5-111">Pour utiliser Machine Learning Studio, vous devez disposer d’un espace de travail Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="fb2c5-111">To use Machine Learning Studio, you need to have a Microsoft Azure Machine Learning workspace.</span></span> <span data-ttu-id="fb2c5-112">Cet espace de travail contient les outils dont vous avez besoin pour créer, gérer et publier des expériences.</span><span class="sxs-lookup"><span data-stu-id="fb2c5-112">This workspace contains the tools you need to create, manage, and publish experiments.</span></span>  

<!--
## To create a workspace
1. Sign in to the [Azure classic portal](https://manage.windowsazure.com).
2. In the  Azure services panel, click **MACHINE LEARNING**.  
   ![Create workspace][1]
3. Click **CREATE AN ML WORKSPACE**.
4. On the **QUICK CREATE** page, enter your workspace information and then click **CREATE AN ML WORKSPACE**.
-->

<span data-ttu-id="fb2c5-113">L’administrateur de votre abonnement Azure doit créer l’espace de travail, puis vous ajouter en tant que propriétaire ou collaborateur.</span><span class="sxs-lookup"><span data-stu-id="fb2c5-113">The administrator for your Azure subscription needs to create the workspace and then add you as an owner or contributor.</span></span> <span data-ttu-id="fb2c5-114">Pour plus d’informations, consultez [Créer et partager un espace de travail Azure Machine Learning](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="fb2c5-114">For details, see [Create and share an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

<span data-ttu-id="fb2c5-115">Une fois votre espace de travail créé, ouvrez Machine Learning Studio ([https://studio.azureml.net/Home](https://studio.azureml.net/Home)).</span><span class="sxs-lookup"><span data-stu-id="fb2c5-115">After your workspace is created, open Machine Learning Studio ([https://studio.azureml.net/Home](https://studio.azureml.net/Home)).</span></span> <span data-ttu-id="fb2c5-116">Si vous disposez de plusieurs espaces de travail, vous pouvez sélectionner l’espace de travail dans la barre d’outils dans le coin supérieur droit de la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="fb2c5-116">If you have more than one workspace, you can select the workspace in the toolbar in the upper-right corner of the window.</span></span>

![Sélection de l’espace de travail dans Studio][2]

> [!TIP]
> <span data-ttu-id="fb2c5-118">Si vous avez été désigné comme propriétaire de l’espace de travail, vous pouvez partager les expériences sur lesquelles vous travaillez en invitant d’autres personnes dans l’espace de travail.</span><span class="sxs-lookup"><span data-stu-id="fb2c5-118">If you were made an owner of the workspace, you can share the experiments you're working on by inviting others to the workspace.</span></span> <span data-ttu-id="fb2c5-119">Pour cela, dans Machine Learning Studio, ouvrez la page **PARAMÈTRES** .</span><span class="sxs-lookup"><span data-stu-id="fb2c5-119">You can do this in Machine Learning Studio on the **SETTINGS** page.</span></span> <span data-ttu-id="fb2c5-120">Vous avez simplement besoin du compte Microsoft ou du compte professionnel de chaque utilisateur.</span><span class="sxs-lookup"><span data-stu-id="fb2c5-120">You just need the Microsoft account or organizational account for each user.</span></span>
> 
> <span data-ttu-id="fb2c5-121">Dans la page **PARAMÈTRES**, cliquez sur **UTILISATEURS**, puis cliquez sur **INVITER PLUS D’UTILISATEURS** en bas de la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="fb2c5-121">On the **SETTINGS** page, click **USERS**, then click **INVITE MORE USERS** at the bottom of the window.</span></span>
> 
> 

- - -
<span data-ttu-id="fb2c5-122">**Suivant : [Téléchargement de données existantes](machine-learning-walkthrough-2-upload-data.md)**</span><span class="sxs-lookup"><span data-stu-id="fb2c5-122">**Next: [Upload existing data](machine-learning-walkthrough-2-upload-data.md)**</span></span>

[1]: ./media/machine-learning-walkthrough-1-create-ml-workspace/create1.png
[2]: ./media/machine-learning-walkthrough-1-create-ml-workspace/open-workspace.png
