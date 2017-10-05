---
title: "Résolution de problèmes : création d'un espace de travail Machine Learning et connexion à celui-ci | Microsoft Docs"
description: "Solutions aux problèmes courants liés à la création d'un espace de travail Azure Machine Learning et à la connexion à un tel espace"
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
ms.openlocfilehash: 398ac3d9c9d32a1ab10413ce0d7ce8d448890409
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-guide-create-and-connect-to-an-machine-learning-workspace"></a><span data-ttu-id="0cb1d-103">Guide de résolution des problèmes : création d'un espace de travail Machine Learning et connexion à celui-ci</span><span class="sxs-lookup"><span data-stu-id="0cb1d-103">Troubleshooting guide: Create and connect to an Machine Learning workspace</span></span>
<span data-ttu-id="0cb1d-104">Ce guide propose des solutions pour quelques-uns des défis qui se posent souvent quand vous configurez des espaces de travail Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="0cb1d-104">This guide provides solutions for some frequently encountered challenges when you are setting up Azure Machine Learning workspaces.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="workspace-owner"></a><span data-ttu-id="0cb1d-105">Propriétaire de l'espace de travail</span><span class="sxs-lookup"><span data-stu-id="0cb1d-105">Workspace owner</span></span>
<span data-ttu-id="0cb1d-106">Pour ouvrir un espace de travail de Machine Learning Studio, vous devez être connecté au compte Microsoft utilisé pour créer l’espace de travail ou recevoir une invitation du propriétaire à rejoindre l’espace de travail.</span><span class="sxs-lookup"><span data-stu-id="0cb1d-106">To open a workspace in Machine Learning Studio, you must be signed in to the Microsoft Account you used to create the workspace, or you need to receive an invitation from the owner to join the workspace.</span></span> <span data-ttu-id="0cb1d-107">À partir du portail Azure, vous pouvez gérer l’espace de travail, notamment configurer l’accès.</span><span class="sxs-lookup"><span data-stu-id="0cb1d-107">From the Azure portal you can manage the workspace, which includes the ability to configure access.</span></span>

<span data-ttu-id="0cb1d-108">Pour plus d'informations sur la gestion d'un espace de travail, consultez [Gestion d'un espace de travail Azure Machine Learning].</span><span class="sxs-lookup"><span data-stu-id="0cb1d-108">For more information on managing a workspace, see [Manage an Azure Machine Learning workspace].</span></span>

<span data-ttu-id="0cb1d-109">[Gestion d'un espace de travail Azure Machine Learning]: machine-learning-manage-workspace.md</span><span class="sxs-lookup"><span data-stu-id="0cb1d-109">[Manage an Azure Machine Learning workspace]: machine-learning-manage-workspace.md</span></span>

## <a name="allowed-regions"></a><span data-ttu-id="0cb1d-110">Régions autorisées</span><span class="sxs-lookup"><span data-stu-id="0cb1d-110">Allowed regions</span></span>
<span data-ttu-id="0cb1d-111">Machine Learning est actuellement disponible dans un nombre limité de régions.</span><span class="sxs-lookup"><span data-stu-id="0cb1d-111">Machine Learning is currently available in a limited number of regions.</span></span> <span data-ttu-id="0cb1d-112">Si votre abonnement n’inclut une de ces régions, le message d’erreur suivant risque de s’afficher : « Vous ne disposez d’aucun abonnement dans les régions autorisées ».</span><span class="sxs-lookup"><span data-stu-id="0cb1d-112">If your subscription does not include one of these regions, you may see the error message, “You have no subscriptions in the allowed regions.”</span></span>

<span data-ttu-id="0cb1d-113">Pour demander qu’une région soit ajoutée à votre abonnement, créez une nouvelle demande d’assistance depuis le portail Azure, choisissez **Facturation** comme type de problème, puis suivez les invites pour envoyer votre demande.</span><span class="sxs-lookup"><span data-stu-id="0cb1d-113">To request that a region be added to your subscription, create a new Microsoft support request from the Azure portal, choose **Billing** as the problem type, and follow the prompts to submit your request.</span></span>

## <a name="storage-account"></a><span data-ttu-id="0cb1d-114">Compte de stockage</span><span class="sxs-lookup"><span data-stu-id="0cb1d-114">Storage account</span></span>
<span data-ttu-id="0cb1d-115">Le service Machine Learning a besoin d'un compte de stockage pour stocker les données.</span><span class="sxs-lookup"><span data-stu-id="0cb1d-115">The Machine Learning service needs a storage account to store data.</span></span> <span data-ttu-id="0cb1d-116">Vous pouvez utiliser un compte de stockage existant ou vous pouvez en créer un quand vous créez l’espace de travail Machine Learning (si vous disposez d’un quota pour la création d’un compte de stockage).</span><span class="sxs-lookup"><span data-stu-id="0cb1d-116">You can use an existing storage account, or you can create a new storage account when you create the new Machine Learning workspace (if you have quota to create a new storage account).</span></span>

<span data-ttu-id="0cb1d-117">Une fois l’espace de travail Machine Learning créé, vous pouvez vous connecter à Machine Learning Studio au moyen du compte Microsoft utilisé pour créer l’espace de travail.</span><span class="sxs-lookup"><span data-stu-id="0cb1d-117">After the new Machine Learning workspace is created, you can sign in to Machine Learning Studio by using the Microsoft account you used to create the workspace.</span></span> <span data-ttu-id="0cb1d-118">Si vous rencontrez le message d'erreur « Espace de travail introuvable » (comme dans la capture d'écran suivante), effectuez les étapes suivantes pour supprimer les cookies de votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="0cb1d-118">If you encounter the error message, “Workspace Not Found” (similar to the following screenshot), please use the following steps to delete your browser cookies.</span></span>

![Workspace not found][screen3]

<span data-ttu-id="0cb1d-120">**Pour supprimer les cookies du navigateur**</span><span class="sxs-lookup"><span data-stu-id="0cb1d-120">**To delete browser cookies**</span></span>

1. <span data-ttu-id="0cb1d-121">Si vous utilisez Internet Explorer, cliquez sur le bouton **Outils** dans le coin supérieur droit et sélectionnez **Options Internet**.</span><span class="sxs-lookup"><span data-stu-id="0cb1d-121">If you use Internet Explorer, click the **Tools** button in the upper-right corner and select **Internet options**.</span></span>  

![Options Internet][screen4]

2. <span data-ttu-id="0cb1d-123">Sous l'onglet **Général**, cliquez sur **Supprimer…**</span><span class="sxs-lookup"><span data-stu-id="0cb1d-123">Under the **General** tab, click **Delete…**</span></span>

![General tab][screen5]

3. <span data-ttu-id="0cb1d-125">Dans la boîte de dialogue **Supprimer l’historique de navigation**, vérifiez que **Cookies et données de sites web** est sélectionné, puis cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="0cb1d-125">In the **Delete Browsing History** dialog box, make sure **Cookies and website data** is selected, and click **Delete**.</span></span>

![Delete cookies][screen6]

<span data-ttu-id="0cb1d-127">Une fois les cookies supprimés, redémarrez le navigateur, puis accédez à la page [Microsoft Azure Machine Learning](https://studio.azureml.net) .</span><span class="sxs-lookup"><span data-stu-id="0cb1d-127">After the cookies are deleted, restart the browser and then go to the [Microsoft Azure Machine Learning](https://studio.azureml.net) page.</span></span> <span data-ttu-id="0cb1d-128">Lorsque vous êtes invité à fournir un nom d’utilisateur et un mot de passe, entrez le même compte Microsoft que celui utilisé pour créer l’espace de travail.</span><span class="sxs-lookup"><span data-stu-id="0cb1d-128">When you are prompted for a user name and password, enter the same Microsoft account you used to create the workspace.</span></span>

## <a name="comments"></a><span data-ttu-id="0cb1d-129">Commentaires</span><span class="sxs-lookup"><span data-stu-id="0cb1d-129">Comments</span></span>

<span data-ttu-id="0cb1d-130">Notre objectif est de vous offrir une expérience de Machine Learning qui soit aussi transparente que possible.</span><span class="sxs-lookup"><span data-stu-id="0cb1d-130">Our goal is to make the Machine Learning experience as seamless as possible.</span></span> <span data-ttu-id="0cb1d-131">Publiez tous vos commentaires et problèmes sur le [forum Azure Machine Learning](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) pour nous permettre de vous aider au mieux.</span><span class="sxs-lookup"><span data-stu-id="0cb1d-131">Please post any comments and issues at the [Azure Machine Learning forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) to help us serve you better.</span></span>

[screen1]:media/machine-learning-troubleshooting-creating-ml-workspace/screen1.png
[screen2]:media/machine-learning-troubleshooting-creating-ml-workspace/screen2.png
[screen3]:media/machine-learning-troubleshooting-creating-ml-workspace/screen3.png
[screen4]:media/machine-learning-troubleshooting-creating-ml-workspace/screen4.png
[screen5]:media/machine-learning-troubleshooting-creating-ml-workspace/screen5.png
[screen6]:media/machine-learning-troubleshooting-creating-ml-workspace/screen6.png
