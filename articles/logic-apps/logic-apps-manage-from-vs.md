---
title: aaaManage logic apps dans Visual Studio - Azure Logic Apps | Documents Microsoft
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
ms.openlocfilehash: 419f83eb062b56e4ac2642dea4de1a025f747521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-logic-apps-with-visual-studio-cloud-explorer"></a><span data-ttu-id="0e444-103">Gestion de vos applications logiques à l’aide de Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="0e444-103">Manage your logic apps with Visual Studio Cloud Explorer</span></span>

<span data-ttu-id="0e444-104">Bien que hello [portail Azure](https://portal.azure.com/) offre un excellent moyen de vous toodesign et gérer Azure Logic Apps, vous pouvez utiliser Visual Studio Cloud Explorer pour la gestion de nombreuses ressources Azure, y compris les applications de la logique.</span><span class="sxs-lookup"><span data-stu-id="0e444-104">Although hello [Azure portal](https://portal.azure.com/) offers a great way for you toodesign and manage Azure Logic Apps, you can use Visual Studio Cloud Explorer for managing many Azure assets, including logic apps.</span></span> <span data-ttu-id="0e444-105">Visual Studio Cloud Explorer vous permet de parcourir, de gérer, de modifier et de télécharger des applications logiques publiées.</span><span class="sxs-lookup"><span data-stu-id="0e444-105">Visual Studio Cloud Explorer lets you browse, manage, edit, and download published logic apps.</span></span> <span data-ttu-id="0e444-106">Les tâches de gestion incluent notamment l’activation, la désactivation et l’affichage de l’historique des exécutions.</span><span class="sxs-lookup"><span data-stu-id="0e444-106">Management tasks include enable, disable, and view run history.</span></span> 

<span data-ttu-id="0e444-107">Avant de pouvoir accéder à vos applications logiques et les gérer dans Visual Studio, installez et configurez ces outils Visual Studio pour Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="0e444-107">Before you can access and manage your logic apps in Visual Studio, install and configure these Visual Studio tools for Azure Logic Apps.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0e444-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="0e444-108">Prerequisites</span></span>

* [<span data-ttu-id="0e444-109">Visual Studio 2015 ou Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="0e444-109">Visual Studio 2015 or Visual Studio 2017</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* <span data-ttu-id="0e444-110">[Dernier kit de développement logiciel (SDK) Azure](https://azure.microsoft.com/downloads/) (2.9.1 ou supérieur)</span><span class="sxs-lookup"><span data-stu-id="0e444-110">[Latest Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or greater)</span></span>
* [<span data-ttu-id="0e444-111">Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="0e444-111">Visual Studio Cloud Explorer</span></span>](https://marketplace.visualstudio.com/items?itemName=MicrosoftCloudExplorer.CloudExplorerforVisualStudio2015)
* <span data-ttu-id="0e444-112">Web toohello d’accès lorsque vous utilisez le concepteur incorporé hello</span><span class="sxs-lookup"><span data-stu-id="0e444-112">Access toohello web when using hello embedded designer</span></span>

## <a name="install-visual-studio-tools-for-logic-apps"></a><span data-ttu-id="0e444-113">Installer les outils Visual Studio pour Logic Apps</span><span class="sxs-lookup"><span data-stu-id="0e444-113">Install Visual Studio tools for Logic Apps</span></span>

<span data-ttu-id="0e444-114">Après avoir installé les composants requis de hello, téléchargez et installez les outils d’applications logique hello Azure pour Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0e444-114">After you install hello prerequisites, download and install hello Azure Logic Apps Tools for Visual Studio.</span></span>

1. <span data-ttu-id="0e444-115">Ouvrez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0e444-115">Open Visual Studio.</span></span> <span data-ttu-id="0e444-116">Sur hello **outils** menu, sélectionnez **Extensions et mises à jour**.</span><span class="sxs-lookup"><span data-stu-id="0e444-116">On hello **Tools** menu, select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="0e444-117">Développez hello **Online** catégorie, vous pouvez rechercher en ligne Bonjour galerie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0e444-117">Expand hello **Online** category so you can search online in hello Visual Studio Gallery.</span></span>
3. <span data-ttu-id="0e444-118">Parcourez les résultats ou recherchez **Logic Apps** jusqu’à ce que vous trouviez **Outils Azure Logic Apps pour Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="0e444-118">Browse or search for **Logic Apps** until you find **Azure Logic Apps Tools for Visual Studio**.</span></span>
4. <span data-ttu-id="0e444-119">toodownload et installer une extension hello, cliquez sur **télécharger**.</span><span class="sxs-lookup"><span data-stu-id="0e444-119">toodownload and install hello extension, click **Download**.</span></span>
5. <span data-ttu-id="0e444-120">Redémarrez Visual Studio après l’installation.</span><span class="sxs-lookup"><span data-stu-id="0e444-120">Restart Visual Studio after installation.</span></span>

> [!NOTE]
> <span data-ttu-id="0e444-121">hello de toodownload Azure logique applications Tools pour Visual Studio accéder directement, toohello [Visual Studio Marketplace](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9).</span><span class="sxs-lookup"><span data-stu-id="0e444-121">toodownload hello Azure Logic Apps Tools for Visual Studio directly, go toohello [Visual Studio Marketplace](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9).</span></span>

## <a name="browse-for-logic-apps-in-cloud-explorer"></a><span data-ttu-id="0e444-122">Recherche d’applications logiques dans Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="0e444-122">Browse for logic apps in Cloud Explorer</span></span>

1.  <span data-ttu-id="0e444-123">tooopen Cloud Explorer, sur hello **vue** menu, choisissez **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="0e444-123">tooopen Cloud Explorer, on hello **View** menu, choose **Cloud Explorer**.</span></span>
2.  <span data-ttu-id="0e444-124">Recherchez votre application logique, par groupe de ressources ou par type de ressource.</span><span class="sxs-lookup"><span data-stu-id="0e444-124">Browse for your logic app, either by resource group or by resource type.</span></span> 

    * <span data-ttu-id="0e444-125">Si vous y accédez par type de ressource, sélectionnez votre abonnement Azure, développez hello **Logic Apps** section et sélectionnez votre application logique.</span><span class="sxs-lookup"><span data-stu-id="0e444-125">If you browse by resource type, select your Azure subscription, expand hello **Logic Apps** section, and select your logic app.</span></span> 
    * <span data-ttu-id="0e444-126">Si vous y accédez par groupe de ressources, développez le groupe de ressources hello où votre application logique et sélectionnez votre application logique.</span><span class="sxs-lookup"><span data-stu-id="0e444-126">If you browse by resource group, expand hello resource group that has your logic app, and select your logic app.</span></span>

    <span data-ttu-id="0e444-127">les commandes tooview pour votre application logique, avec le bouton droit de votre application logique, ou bas hello du Cloud Explorer, choisissez hello **Actions** menu.</span><span class="sxs-lookup"><span data-stu-id="0e444-127">tooview commands for your logic app, either right-click your logic app, or at hello bottom of Cloud Explorer, choose from hello **Actions** menu.</span></span>

    ![Accès à votre application logique](./media/logic-apps-manage-from-vs/browse.png)

## <a name="edit-your-logic-app-with-logic-apps-designer"></a><span data-ttu-id="0e444-129">Modifier votre application logique avec le Concepteur d’applications logiques</span><span class="sxs-lookup"><span data-stu-id="0e444-129">Edit your logic app with Logic Apps Designer</span></span>

<span data-ttu-id="0e444-130">À partir du Cloud Explorer, vous pouvez ouvrir une application actuellement déployé logique Bonjour même concepteur que vous utilisez dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0e444-130">From Cloud Explorer, you can open a currently deployed logic app in hello same designer that you use in hello Azure portal.</span></span> 

* <span data-ttu-id="0e444-131">tooedit votre application logique, dans l’Explorateur de Cloud, avec le bouton droit de votre application logique, puis sélectionnez **ouvert avec l’éditeur d’application logique**.</span><span class="sxs-lookup"><span data-stu-id="0e444-131">tooedit your logic app, in Cloud Explorer, right-click your logic app, and select **Open with Logic App Editor**.</span></span> 

* <span data-ttu-id="0e444-132">toopublish votre toohello mises à jour le cloud, choisissez **publier**.</span><span class="sxs-lookup"><span data-stu-id="0e444-132">toopublish your updates toohello cloud, choose **Publish**.</span></span> 

* <span data-ttu-id="0e444-133">toostart une nouvelle exécution, choisissez **exécuter un déclencheur**.</span><span class="sxs-lookup"><span data-stu-id="0e444-133">toostart a new run, choose **Run Trigger**.</span></span>

![Concepteur Logic Apps](./media/logic-apps-manage-from-vs/designer.png)

<span data-ttu-id="0e444-135">À partir du concepteur hello, vous pouvez également **télécharger** une application logique.</span><span class="sxs-lookup"><span data-stu-id="0e444-135">From hello designer, you can also **Download** a logic app.</span></span> <span data-ttu-id="0e444-136">Cette action est la définition de la logique d’application hello automatiquement et enregistre la définition de hello sous la forme d’un modèle de déploiement Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0e444-136">This action automatically parameterizes hello logic app definition, and saves hello definition as an Azure Resource Manager deployment template.</span></span> <span data-ttu-id="0e444-137">Vous pouvez ajouter ce projet de déploiement modèle tooyour groupe de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="0e444-137">You can add this deployment template tooyour Azure Resource Group project.</span></span>

## <a name="browse-your-logic-app-run-history"></a><span data-ttu-id="0e444-138">Parcourir votre historique des exécutions d’une application logique</span><span class="sxs-lookup"><span data-stu-id="0e444-138">Browse your logic app run history</span></span>

<span data-ttu-id="0e444-139">hello tooview l’historique de votre application logique, d’exécution avec le bouton droit de votre application logique, puis sélectionnez **ouvrir l’historique d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="0e444-139">tooview hello run history for your logic app, right-click your logic app, and select **Open run history**.</span></span> <span data-ttu-id="0e444-140">tooreorder votre historique d’exécution basée sur n’importe quel en-tête de colonne de hello indiqué, sélectionnez Propriétés hello.</span><span class="sxs-lookup"><span data-stu-id="0e444-140">tooreorder your run history based on any of hello properties shown, select hello column header.</span></span>

![Historique d’exécution](media/logic-apps-manage-from-vs/runs.png)

<span data-ttu-id="0e444-142">hello tooshow l’historique d’une instance d’exécution pour pouvoir consulter hello exécuter des résultats, y compris les entrées de hello et des sorties à partir de chaque étape, double-cliquez sur un des hello exécuter des instances.</span><span class="sxs-lookup"><span data-stu-id="0e444-142">tooshow hello run history for an instance so you can review hello run results, including hello inputs and outputs from each step, double-click one of hello run instances.</span></span>

![Exécution des résultats de l’historique, des entrées et des sorties](./media/logic-apps-manage-from-vs/history.png)

## <a name="next-steps"></a><span data-ttu-id="0e444-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0e444-144">Next steps</span></span>

* [<span data-ttu-id="0e444-145">Créez votre première application logique</span><span class="sxs-lookup"><span data-stu-id="0e444-145">Create your first logic app</span></span>](logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="0e444-146">Concevoir, créer et déployer des applications logiques dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0e444-146">Design, build, and deploy logic apps in Visual Studio</span></span>](logic-apps-deploy-from-vs.md)
* [<span data-ttu-id="0e444-147">Afficher des exemples et des scénarios courants</span><span class="sxs-lookup"><span data-stu-id="0e444-147">View common examples and scenarios</span></span>](logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="0e444-148">Vidéo : Automatisez vos processus métiers avec Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="0e444-148">Video: Automate business processes with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/T694)
* [<span data-ttu-id="0e444-149">Vidéo : Intégrez vos systèmes à Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="0e444-149">Video: Integrate your systems with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/P462)
