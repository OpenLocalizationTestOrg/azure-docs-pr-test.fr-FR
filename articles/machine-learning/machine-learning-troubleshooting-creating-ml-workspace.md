---
title: "Résoudre les problèmes : Création et la connexion d’espace de travail Machine Learning tooa | Documents Microsoft"
description: "Solutions aux problèmes courants dans la création et l’espace de travail Azure Machine Learning tooan de connexion"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 1a8aec4b-35f9-44e8-9570-2575b8979ab1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 965a0025e85ba4e22c2b037edfa923e7f7599069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-create-and-connect-tooan-machine-learning-workspace"></a><span data-ttu-id="f935c-103">Guide de dépannage : créer et connecter l’espace de travail Machine Learning tooan</span><span class="sxs-lookup"><span data-stu-id="f935c-103">Troubleshooting guide: Create and connect tooan Machine Learning workspace</span></span>
<span data-ttu-id="f935c-104">Ce guide propose des solutions pour quelques-uns des défis qui se posent souvent quand vous configurez des espaces de travail Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f935c-104">This guide provides solutions for some frequently encountered challenges when you are setting up Azure Machine Learning workspaces.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="workspace-owner"></a><span data-ttu-id="f935c-105">Propriétaire de l'espace de travail</span><span class="sxs-lookup"><span data-stu-id="f935c-105">Workspace owner</span></span>
<span data-ttu-id="f935c-106">tooopen un espace de travail dans Machine Learning Studio, vous devez être connecté toohello Account Microsoft, vous avez utilisé l’espace de travail de toocreate hello, ou si vous devez tooreceive une invitation à partir de l’espace de travail hello propriétaire toojoin hello.</span><span class="sxs-lookup"><span data-stu-id="f935c-106">tooopen a workspace in Machine Learning Studio, you must be signed in toohello Microsoft Account you used toocreate hello workspace, or you need tooreceive an invitation from hello owner toojoin hello workspace.</span></span> <span data-ttu-id="f935c-107">À partir de hello portail Azure, vous pouvez gérer hello espace de travail, qui inclut l’accès de tooconfigure possibilité hello.</span><span class="sxs-lookup"><span data-stu-id="f935c-107">From hello Azure portal you can manage hello workspace, which includes hello ability tooconfigure access.</span></span>

<span data-ttu-id="f935c-108">Pour plus d'informations sur la gestion d'un espace de travail, consultez [Gestion d'un espace de travail Azure Machine Learning].</span><span class="sxs-lookup"><span data-stu-id="f935c-108">For more information on managing a workspace, see [Manage an Azure Machine Learning workspace].</span></span>

[Gestion d'un espace de travail Azure Machine Learning]: machine-learning-manage-workspace.md

## <a name="allowed-regions"></a><span data-ttu-id="f935c-110">Régions autorisées</span><span class="sxs-lookup"><span data-stu-id="f935c-110">Allowed regions</span></span>
<span data-ttu-id="f935c-111">Machine Learning est actuellement disponible dans un nombre limité de régions.</span><span class="sxs-lookup"><span data-stu-id="f935c-111">Machine Learning is currently available in a limited number of regions.</span></span> <span data-ttu-id="f935c-112">Si votre abonnement n’inclut pas un de ces régions, vous pouvez voir le message d’erreur hello, « Vous n’avez aucun abonnement Bonjour autorisé régions. »</span><span class="sxs-lookup"><span data-stu-id="f935c-112">If your subscription does not include one of these regions, you may see hello error message, “You have no subscriptions in hello allowed regions.”</span></span>

<span data-ttu-id="f935c-113">toorequest une région être ajouté tooyour abonnement, créer une nouvelle demande de support Microsoft à partir de hello portail Azure, choisissez **facturation** en tant que type de problème hello et suivez hello invite toosubmit votre demande.</span><span class="sxs-lookup"><span data-stu-id="f935c-113">toorequest that a region be added tooyour subscription, create a new Microsoft support request from hello Azure portal, choose **Billing** as hello problem type, and follow hello prompts toosubmit your request.</span></span>

## <a name="storage-account"></a><span data-ttu-id="f935c-114">Compte de stockage</span><span class="sxs-lookup"><span data-stu-id="f935c-114">Storage account</span></span>
<span data-ttu-id="f935c-115">Hello service Machine Learning a besoin de données de toostore d’un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="f935c-115">hello Machine Learning service needs a storage account toostore data.</span></span> <span data-ttu-id="f935c-116">Vous pouvez utiliser un compte de stockage existant, ou vous pouvez créer un compte de stockage lorsque vous créez hello apprentissage espace de travail (si vous avez un compte de stockage à quota toocreate).</span><span class="sxs-lookup"><span data-stu-id="f935c-116">You can use an existing storage account, or you can create a new storage account when you create hello new Machine Learning workspace (if you have quota toocreate a new storage account).</span></span>

<span data-ttu-id="f935c-117">Après la création de l’espace de travail de Machine Learning nouvelle hello, vous pouvez signer dans tooMachine Learning Studio à l’aide du compte Microsoft de hello que vous avez utilisé l’espace de travail toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="f935c-117">After hello new Machine Learning workspace is created, you can sign in tooMachine Learning Studio by using hello Microsoft account you used toocreate hello workspace.</span></span> <span data-ttu-id="f935c-118">Si vous rencontrez le message d’erreur hello, « Espace de travail introuvable » (toohello similaire après la capture d’écran), utilisez hello suivant les étapes toodelete les cookies de votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="f935c-118">If you encounter hello error message, “Workspace Not Found” (similar toohello following screenshot), please use hello following steps toodelete your browser cookies.</span></span>

![Workspace not found][screen3]

<span data-ttu-id="f935c-120">**cookies du navigateur toodelete**</span><span class="sxs-lookup"><span data-stu-id="f935c-120">**toodelete browser cookies**</span></span>

1. <span data-ttu-id="f935c-121">Si vous utilisez Internet Explorer, cliquez sur hello **outils** situé dans le coin supérieur droit de hello et sélectionnez **options Internet**.</span><span class="sxs-lookup"><span data-stu-id="f935c-121">If you use Internet Explorer, click hello **Tools** button in hello upper-right corner and select **Internet options**.</span></span>  

![Options Internet][screen4]

2. <span data-ttu-id="f935c-123">Sous hello **général** , cliquez sur **supprimer...**</span><span class="sxs-lookup"><span data-stu-id="f935c-123">Under hello **General** tab, click **Delete…**</span></span>

![General tab][screen5]

3. <span data-ttu-id="f935c-125">Bonjour **supprimer l’historique de navigation** boîte de dialogue zone, assurez-vous que **les Cookies et les données du site Web** est sélectionné, puis cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="f935c-125">In hello **Delete Browsing History** dialog box, make sure **Cookies and website data** is selected, and click **Delete**.</span></span>

![Delete cookies][screen6]

<span data-ttu-id="f935c-127">Une fois que les cookies de hello sont supprimés, redémarrez le navigateur de hello et passez toohello [Microsoft Azure Machine Learning](https://studio.azureml.net) page.</span><span class="sxs-lookup"><span data-stu-id="f935c-127">After hello cookies are deleted, restart hello browser and then go toohello [Microsoft Azure Machine Learning](https://studio.azureml.net) page.</span></span> <span data-ttu-id="f935c-128">Lorsque vous êtes invité à saisir un nom d’utilisateur et un mot de passe, entrez hello même compte Microsoft que vous avez utilisé l’espace de travail toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="f935c-128">When you are prompted for a user name and password, enter hello same Microsoft account you used toocreate hello workspace.</span></span>

## <a name="comments"></a><span data-ttu-id="f935c-129">Commentaires</span><span class="sxs-lookup"><span data-stu-id="f935c-129">Comments</span></span>

<span data-ttu-id="f935c-130">Notre objectif est toomake hello expérience d’apprentissage plus transparente possible.</span><span class="sxs-lookup"><span data-stu-id="f935c-130">Our goal is toomake hello Machine Learning experience as seamless as possible.</span></span> <span data-ttu-id="f935c-131">Envoyez des commentaires et des problèmes à hello [forum d’Azure Machine Learning](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) toohelp nous mieux vous servir.</span><span class="sxs-lookup"><span data-stu-id="f935c-131">Please post any comments and issues at hello [Azure Machine Learning forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) toohelp us serve you better.</span></span>

[screen1]:media/machine-learning-troubleshooting-creating-ml-workspace/screen1.png
[screen2]:media/machine-learning-troubleshooting-creating-ml-workspace/screen2.png
[screen3]:media/machine-learning-troubleshooting-creating-ml-workspace/screen3.png
[screen4]:media/machine-learning-troubleshooting-creating-ml-workspace/screen4.png
[screen5]:media/machine-learning-troubleshooting-creating-ml-workspace/screen5.png
[screen6]:media/machine-learning-troubleshooting-creating-ml-workspace/screen6.png
