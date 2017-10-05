---
title: "Gestion d’applications logiques dans Visual Studio - Azure Logic Apps | Microsoft Docs"
description: "Gestion d’applications logiques et d’autres ressources à l’aide de Visual Studio Cloud Explorer"
author: klam
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 12/19/2016
ms.author: LADocs; klam
ms.openlocfilehash: a5bf24de1a7a2b6d4c1ae6416c95d83ef7506da3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="manage-your-logic-apps-with-visual-studio-cloud-explorer"></a><span data-ttu-id="9e841-103">Gestion de vos applications logiques à l’aide de Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="9e841-103">Manage your logic apps with Visual Studio Cloud Explorer</span></span>

<span data-ttu-id="9e841-104">Bien que le [Portail Azure](https://portal.azure.com/) vous offre un excellent moyen de concevoir et de gérer des applications logiques Azure, vous pouvez utiliser Visual Studio Cloud Explorer pour gérer un grand nombre de vos ressources Azure, y compris les applications logiques.</span><span class="sxs-lookup"><span data-stu-id="9e841-104">Although the [Azure portal](https://portal.azure.com/) offers a great way for you to design and manage Azure Logic Apps, you can use Visual Studio Cloud Explorer for managing many Azure assets, including logic apps.</span></span> <span data-ttu-id="9e841-105">Visual Studio Cloud Explorer vous permet de parcourir, de gérer, de modifier et de télécharger des applications logiques publiées.</span><span class="sxs-lookup"><span data-stu-id="9e841-105">Visual Studio Cloud Explorer lets you browse, manage, edit, and download published logic apps.</span></span> <span data-ttu-id="9e841-106">Les tâches de gestion incluent notamment l’activation, la désactivation et l’affichage de l’historique des exécutions.</span><span class="sxs-lookup"><span data-stu-id="9e841-106">Management tasks include enable, disable, and view run history.</span></span> 

<span data-ttu-id="9e841-107">Avant de pouvoir accéder à vos applications logiques et les gérer dans Visual Studio, installez et configurez ces outils Visual Studio pour Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="9e841-107">Before you can access and manage your logic apps in Visual Studio, install and configure these Visual Studio tools for Azure Logic Apps.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="9e841-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9e841-108">Prerequisites</span></span>

* [<span data-ttu-id="9e841-109">Visual Studio 2015 ou Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="9e841-109">Visual Studio 2015 or Visual Studio 2017</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* <span data-ttu-id="9e841-110">[Dernier kit de développement logiciel (SDK) Azure](https://azure.microsoft.com/downloads/) (2.9.1 ou supérieur)</span><span class="sxs-lookup"><span data-stu-id="9e841-110">[Latest Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or greater)</span></span>
* [<span data-ttu-id="9e841-111">Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="9e841-111">Visual Studio Cloud Explorer</span></span>](https://marketplace.visualstudio.com/items?itemName=MicrosoftCloudExplorer.CloudExplorerforVisualStudio2015)
* <span data-ttu-id="9e841-112">Accès au web lors de l’utilisation du concepteur intégré</span><span class="sxs-lookup"><span data-stu-id="9e841-112">Access to the web when using the embedded designer</span></span>

## <a name="install-visual-studio-tools-for-logic-apps"></a><span data-ttu-id="9e841-113">Installer les outils Visual Studio pour Logic Apps</span><span class="sxs-lookup"><span data-stu-id="9e841-113">Install Visual Studio tools for Logic Apps</span></span>

<span data-ttu-id="9e841-114">Après avoir installé les prérequis, téléchargez et installez les outils Azure Logic Apps pour Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9e841-114">After you install the prerequisites, download and install the Azure Logic Apps Tools for Visual Studio.</span></span>

1. <span data-ttu-id="9e841-115">Ouvrez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9e841-115">Open Visual Studio.</span></span> <span data-ttu-id="9e841-116">Dans le menu **Outils**, sélectionnez **Extensions et mises à jour**.</span><span class="sxs-lookup"><span data-stu-id="9e841-116">On the **Tools** menu, select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="9e841-117">Développez la catégorie **En ligne** pour effectuer une recherche en ligne dans la galerie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9e841-117">Expand the **Online** category so you can search online in the Visual Studio Gallery.</span></span>
3. <span data-ttu-id="9e841-118">Parcourez les résultats ou recherchez **Logic Apps** jusqu’à ce que vous trouviez **Outils Azure Logic Apps pour Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="9e841-118">Browse or search for **Logic Apps** until you find **Azure Logic Apps Tools for Visual Studio**.</span></span>
4. <span data-ttu-id="9e841-119">Pour télécharger et installer l’extension, cliquez sur **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="9e841-119">To download and install the extension, click **Download**.</span></span>
5. <span data-ttu-id="9e841-120">Redémarrez Visual Studio après l’installation.</span><span class="sxs-lookup"><span data-stu-id="9e841-120">Restart Visual Studio after installation.</span></span>

> [!NOTE]
> <span data-ttu-id="9e841-121">Pour télécharger directement les outils Azure Logic Apps pour Visual Studio, accédez à [Visual Studio Marketplace](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9).</span><span class="sxs-lookup"><span data-stu-id="9e841-121">To download the Azure Logic Apps Tools for Visual Studio directly, go to the [Visual Studio Marketplace](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9).</span></span>

## <a name="browse-for-logic-apps-in-cloud-explorer"></a><span data-ttu-id="9e841-122">Recherche d’applications logiques dans Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="9e841-122">Browse for logic apps in Cloud Explorer</span></span>

1.  <span data-ttu-id="9e841-123">Pour ouvrir Cloud Explorer, sur le menu **Affichage**, choisissez **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="9e841-123">To open Cloud Explorer, on the **View** menu, choose **Cloud Explorer**.</span></span>
2.  <span data-ttu-id="9e841-124">Recherchez votre application logique, par groupe de ressources ou par type de ressource.</span><span class="sxs-lookup"><span data-stu-id="9e841-124">Browse for your logic app, either by resource group or by resource type.</span></span> 

    * <span data-ttu-id="9e841-125">Si vous les parcourez par type de ressource, sélectionnez un abonnement Azure, développez la section **Logic Apps**, puis sélectionnez une application logique.</span><span class="sxs-lookup"><span data-stu-id="9e841-125">If you browse by resource type, select your Azure subscription, expand the **Logic Apps** section, and select your logic app.</span></span> 
    * <span data-ttu-id="9e841-126">Si vous y accédez par groupe de ressources, développez le groupe de ressources qui contient votre application logique, puis sélectionnez votre application logique.</span><span class="sxs-lookup"><span data-stu-id="9e841-126">If you browse by resource group, expand the resource group that has your logic app, and select your logic app.</span></span>

    <span data-ttu-id="9e841-127">Pour afficher les commandes de votre application logique, cliquez avec le bouton droit sur votre application logique, ou en bas de Cloud Explorer, choisissez le menu **Actions**.</span><span class="sxs-lookup"><span data-stu-id="9e841-127">To view commands for your logic app, either right-click your logic app, or at the bottom of Cloud Explorer, choose from the **Actions** menu.</span></span>

    ![Accès à votre application logique](./media/logic-apps-manage-from-vs/browse.png)

## <a name="edit-your-logic-app-with-logic-apps-designer"></a><span data-ttu-id="9e841-129">Modifier votre application logique avec le Concepteur d’applications logiques</span><span class="sxs-lookup"><span data-stu-id="9e841-129">Edit your logic app with Logic Apps Designer</span></span>

<span data-ttu-id="9e841-130">Dans Cloud Explorer, vous pouvez ouvrir une application logique actuellement déployée dans le même concepteur que celui que vous utilisez dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="9e841-130">From Cloud Explorer, you can open a currently deployed logic app in the same designer that you use in the Azure portal.</span></span> 

* <span data-ttu-id="9e841-131">Pour modifier votre application logique, dans Cloud Explorer, cliquez avec le bouton droit sur votre application logique, puis sélectionnez **Ouvrir avec l'éditeur d'application logique**.</span><span class="sxs-lookup"><span data-stu-id="9e841-131">To edit your logic app, in Cloud Explorer, right-click your logic app, and select **Open with Logic App Editor**.</span></span> 

* <span data-ttu-id="9e841-132">Pour publier vos mises à jour dans le cloud, choisissez **Publier**.</span><span class="sxs-lookup"><span data-stu-id="9e841-132">To publish your updates to the cloud, choose **Publish**.</span></span> 

* <span data-ttu-id="9e841-133">Pour démarrer une nouvelle exécution, choisissez **Déclencheur d'exécution**.</span><span class="sxs-lookup"><span data-stu-id="9e841-133">To start a new run, choose **Run Trigger**.</span></span>

![Concepteur Logic Apps](./media/logic-apps-manage-from-vs/designer.png)

<span data-ttu-id="9e841-135">Dans le concepteur, vous pouvez également **Télécharger** une application logique.</span><span class="sxs-lookup"><span data-stu-id="9e841-135">From the designer, you can also **Download** a logic app.</span></span> <span data-ttu-id="9e841-136">Cette action paramètre automatiquement la définition de l’application logique et l’enregistre sous la forme d’un modèle de déploiement Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9e841-136">This action automatically parameterizes the logic app definition, and saves the definition as an Azure Resource Manager deployment template.</span></span> <span data-ttu-id="9e841-137">Vous pouvez ajouter ce modèle de déploiement à votre projet de groupe de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="9e841-137">You can add this deployment template to your Azure Resource Group project.</span></span>

## <a name="browse-your-logic-app-run-history"></a><span data-ttu-id="9e841-138">Parcourir votre historique des exécutions d’une application logique</span><span class="sxs-lookup"><span data-stu-id="9e841-138">Browse your logic app run history</span></span>

<span data-ttu-id="9e841-139">Pour afficher l’historique des exécutions de votre application logique, cliquez avec le bouton droit sur votre application logique et sélectionnez **Ouvrir l’historique des exécutions**.</span><span class="sxs-lookup"><span data-stu-id="9e841-139">To view the run history for your logic app, right-click your logic app, and select **Open run history**.</span></span> <span data-ttu-id="9e841-140">Pour réorganiser votre historique des exécutions en fonction de l’une des propriétés affichées, sélectionnez l’en-tête de colonne.</span><span class="sxs-lookup"><span data-stu-id="9e841-140">To reorder your run history based on any of the properties shown, select the column header.</span></span>

![Historique d’exécution](media/logic-apps-manage-from-vs/runs.png)

<span data-ttu-id="9e841-142">Pour afficher l’historique des exécutions d’une instance et voir les résultats de l’exécution, notamment les entrées et sorties de chaque étape, double-cliquez sur l’une des instances d’exécution.</span><span class="sxs-lookup"><span data-stu-id="9e841-142">To show the run history for an instance so you can review the run results, including the inputs and outputs from each step, double-click one of the run instances.</span></span>

![Exécution des résultats de l’historique, des entrées et des sorties](./media/logic-apps-manage-from-vs/history.png)

## <a name="next-steps"></a><span data-ttu-id="9e841-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9e841-144">Next steps</span></span>

* [<span data-ttu-id="9e841-145">Créez votre première application logique</span><span class="sxs-lookup"><span data-stu-id="9e841-145">Create your first logic app</span></span>](logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="9e841-146">Concevoir, créer et déployer des applications logiques dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9e841-146">Design, build, and deploy logic apps in Visual Studio</span></span>](logic-apps-deploy-from-vs.md)
* [<span data-ttu-id="9e841-147">Afficher des exemples et des scénarios courants</span><span class="sxs-lookup"><span data-stu-id="9e841-147">View common examples and scenarios</span></span>](logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="9e841-148">Vidéo : Automatisez vos processus métiers avec Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="9e841-148">Video: Automate business processes with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/T694)
* [<span data-ttu-id="9e841-149">Vidéo : Intégrez vos systèmes à Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="9e841-149">Video: Integrate your systems with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/P462)
