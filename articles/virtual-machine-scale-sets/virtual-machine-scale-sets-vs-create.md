---
title: "aaaDeploy ensemble d’échelle de Machine virtuelle à l’aide de Visual Studio | Documents Microsoft"
description: "Déployer des jeux de mise à l'échelle de machines virtuelles à l'aide de Visual Studio et d’un modèle Resource Manager"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ed0786b8-34b2-49a8-85b5-2a628128ead6
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: guybo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c89a9f2478ccc3d22989aea604a4273bcc46df82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-virtual-machine-scale-set-with-visual-studio"></a><span data-ttu-id="90f4e-103">Comment toocreate une échelle de l’ordinateur virtuel défini avec Visual Studio</span><span class="sxs-lookup"><span data-stu-id="90f4e-103">How toocreate a Virtual Machine Scale Set with Visual Studio</span></span>
<span data-ttu-id="90f4e-104">Cet article vous explique comment toodeploy une échelle de machines virtuelles Azure définie à l’aide d’un déploiement de groupe de ressources Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="90f4e-104">This article shows you how toodeploy an Azure Virtual Machine Scale Set using a Visual Studio Resource Group Deployment.</span></span>

<span data-ttu-id="90f4e-105">[Machines virtuelles Azure identiques](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) est une toodeploy de ressources de calcul Azure et de gérer une collection de machines virtuelles similaires à l’échelle automatique et de l’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="90f4e-105">[Azure Virtual Machine Scale Sets](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) is an Azure Compute resource toodeploy and manage a collection of similar virtual machines with auto-scale and load balancing.</span></span> <span data-ttu-id="90f4e-106">Vous pouvez configurer et déployer des groupes de machines virtuelles identiques à l’aide de [modèles Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="90f4e-106">You can provision and deploy Virtual Machine Scale Sets using [Azure Resource Manager Templates](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="90f4e-107">Les modèles Azure Resource Manager peuvent être déployés à l’aide de l’interface de ligne de commande (CLI) Azure, de PowerShell, de REST et directement à partir de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="90f4e-107">Azure Resource Manager Templates can be deployed using Azure CLI, PowerShell, REST and also directly from Visual Studio.</span></span> <span data-ttu-id="90f4e-108">Visual Studio fournit des exemples de modèles qui peuvent être déployés dans le cadre d’un projet de déploiement de groupe de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="90f4e-108">Visual Studio provides a set of example templates, which can be deployed as part of an Azure Resource Group Deployment project.</span></span>

<span data-ttu-id="90f4e-109">Déploiements de groupe de ressources Azure sont un moyen toogroup et publient un ensemble de ressources Azure connexes dans une même opération de déploiement.</span><span class="sxs-lookup"><span data-stu-id="90f4e-109">Azure Resource Group deployments are a way toogroup and publish a set of related Azure resources in a single deployment operation.</span></span> <span data-ttu-id="90f4e-110">Pour en savoir plus, consultez la rubrique [Création et déploiement de groupes de ressources Azure à l’aide de Visual Studio](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="90f4e-110">You can learn more about them here: [Creating and deploying Azure resource groups through Visual Studio](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="90f4e-111">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="90f4e-111">Pre-requisites</span></span>
<span data-ttu-id="90f4e-112">tooget de déployer des machines virtuelles identiques dans Visual Studio, hello éléments suivants sont nécessaires :</span><span class="sxs-lookup"><span data-stu-id="90f4e-112">tooget started deploying Virtual Machine Scale Sets in Visual Studio, you need hello following:</span></span>

* <span data-ttu-id="90f4e-113">Visual Studio 2013 ou une version ultérieure</span><span class="sxs-lookup"><span data-stu-id="90f4e-113">Visual Studio 2013 or later</span></span>
* <span data-ttu-id="90f4e-114">Kit de développement logiciel (SDK) Azure 2.7, 2.8 ou 2.9</span><span class="sxs-lookup"><span data-stu-id="90f4e-114">Azure SDK 2.7, 2.8 or 2.9</span></span>

>[!NOTE]
><span data-ttu-id="90f4e-115">Ces instructions partent du principe que vous utilisez Visual Studio avec le [Kit de développement logiciel (SDK) Azure 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).</span><span class="sxs-lookup"><span data-stu-id="90f4e-115">These instructions assume you are using Visual Studio with [Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).</span></span>

## <a name="creating-a-project"></a><span data-ttu-id="90f4e-116">Création d’un projet</span><span class="sxs-lookup"><span data-stu-id="90f4e-116">Creating a Project</span></span>
1. <span data-ttu-id="90f4e-117">Créez un projet dans Visual Studio en sélectionnant **Fichier | Nouveau | Projet**.</span><span class="sxs-lookup"><span data-stu-id="90f4e-117">Create a new project in Visual Studio by choosing **File | New | Project**.</span></span>
   
    ![Fichier Nouveau][file_new]

2. <span data-ttu-id="90f4e-119">Sous **Visual C# | Cloud**, choisissez **Azure Resource Manager** toocreate un projet pour le déploiement d’un modèle de gestionnaire de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="90f4e-119">Under **Visual C# | Cloud**, choose **Azure Resource Manager** toocreate a project for deploying an Azure Resource Manager Template.</span></span>
   
    ![Créer un projet][create_project]

3. <span data-ttu-id="90f4e-121">À partir de la liste de hello des modèles, sélectionnez hello Linux ou modèle de définir de mise à l’échelle d’ordinateur virtuel Windows.</span><span class="sxs-lookup"><span data-stu-id="90f4e-121">From hello list of Templates, select either hello Linux or Windows Virtual Machine Scale Set Template.</span></span>
   
   ![Sélectionner un modèle][select_Template]

4. <span data-ttu-id="90f4e-123">Une fois votre projet créé, vous voyez les scripts de déploiement PowerShell, un modèle de gestionnaire de ressources Azure et un fichier de paramètres pour hello ensemble d’échelle de Machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="90f4e-123">Once your project is created you see PowerShell deployment scripts, an Azure Resource Manager Template, and a parameter file for hello Virtual Machine Scale Set.</span></span>
   
    ![Explorateur de solutions][solution_explorer]

## <a name="customize-your-project"></a><span data-ttu-id="90f4e-125">Personnalisation de votre projet</span><span class="sxs-lookup"><span data-stu-id="90f4e-125">Customize your project</span></span>
<span data-ttu-id="90f4e-126">Maintenant vous pouvez modifier toocustomize du modèle hello pour les besoins de votre application, telles que l’ajout de propriétés d’extension de machine virtuelle ou la modification de charger les règles d’équilibrage.</span><span class="sxs-lookup"><span data-stu-id="90f4e-126">Now you can edit hello Template toocustomize it for your application's needs, such as adding VM extension properties or editing load balancing rules.</span></span> <span data-ttu-id="90f4e-127">Par défaut les modèles d’ensembles hello Machine virtuelle mise à l’échelle sont extension toodeploy configuré hello AzureDiagnostics, ce qui rend les règles de mise à l’échelle tooadd facile.</span><span class="sxs-lookup"><span data-stu-id="90f4e-127">By default hello Virtual Machine Scale Set Templates are configured toodeploy hello AzureDiagnostics extension, which makes it easy tooadd autoscale rules.</span></span> <span data-ttu-id="90f4e-128">Il déploie également un équilibreur de charge avec une adresse IP publique, configuré avec les règles NAT entrantes.</span><span class="sxs-lookup"><span data-stu-id="90f4e-128">It also deploys a load balancer with a public IP address, configured with inbound NAT rules.</span></span> 

<span data-ttu-id="90f4e-129">équilibrage de charge Hello vous permet de connecter des instances de machine virtuelle toohello avec SSH (Linux) ou RDP (Windows).</span><span class="sxs-lookup"><span data-stu-id="90f4e-129">hello load balancer lets you connect toohello VM instances with SSH (Linux) or RDP (Windows).</span></span> <span data-ttu-id="90f4e-130">plage de ports frontaux de Hello commence à 50000.</span><span class="sxs-lookup"><span data-stu-id="90f4e-130">hello front-end port range starts at 50000.</span></span> <span data-ttu-id="90f4e-131">Pour linux, cela signifie que si vous SSH tooport 50000, vous êtes routé tooport 22 de hello première machine virtuelle Bonjour ensemble d’échelle.</span><span class="sxs-lookup"><span data-stu-id="90f4e-131">For linux this means that if you SSH tooport 50000, you are routed tooport 22 of hello first VM in hello Scale Set.</span></span> <span data-ttu-id="90f4e-132">Connexion tooport 50001 est routé tooport 22 Hello deuxième machine virtuelle et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="90f4e-132">Connecting tooport 50001 is routed tooport 22 of hello second VM and so on.</span></span>

 <span data-ttu-id="90f4e-133">Un bon moyen tooedit vos modèles avec Visual Studio est le paramètres hello tooorganize toouse hello structure JSON, des variables et des ressources.</span><span class="sxs-lookup"><span data-stu-id="90f4e-133">A good way tooedit your Templates with Visual Studio is toouse hello JSON Outline tooorganize hello parameters, variables, and resources.</span></span> <span data-ttu-id="90f4e-134">Le fonctionnement de hello schéma Visual Studio peut souligner les erreurs dans votre modèle avant de le déployer.</span><span class="sxs-lookup"><span data-stu-id="90f4e-134">With an understanding of hello schema Visual Studio can point out errors in your Template before you deploy it.</span></span>

![JSON Explorer][json_explorer]

## <a name="deploy-hello-project"></a><span data-ttu-id="90f4e-136">Déployer le projet de hello</span><span class="sxs-lookup"><span data-stu-id="90f4e-136">Deploy hello project</span></span>
1. <span data-ttu-id="90f4e-137">Déployer hello Azure Resource Manager ressource modèle de toocreate hello ensemble d’échelle de Machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="90f4e-137">Deploy hello Azure Resource Manager Template toocreate hello Virtual Machine Scale Set resource.</span></span> <span data-ttu-id="90f4e-138">Avec le bouton droit sur le nœud de projet hello et choisissez **déployer | Nouveau déploiement**.</span><span class="sxs-lookup"><span data-stu-id="90f4e-138">Right-click on hello project node and choose **Deploy | New Deployment**.</span></span>
   
    ![Déployer un modèle][5deploy_Template]
    
2. <span data-ttu-id="90f4e-140">Dans la boîte de dialogue « Déployer tooResource groupe » hello, sélectionnez votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="90f4e-140">Select your subscription in hello “Deploy tooResource Group” dialog.</span></span>
   
    ![Déployer un modèle][6deploy_Template]

3. <span data-ttu-id="90f4e-142">À ce stade, vous pouvez créer un groupe de ressources Azure de toodeploy votre modèle de.</span><span class="sxs-lookup"><span data-stu-id="90f4e-142">From here, you can create an Azure Resource Group toodeploy your Template to.</span></span>
   
    ![Nouveau groupe de ressources][new_resource]

4. <span data-ttu-id="90f4e-144">Ensuite, cliquez sur **modifier les paramètres** tooenter les paramètres qui sont passés tooyour modèle.</span><span class="sxs-lookup"><span data-stu-id="90f4e-144">Next, click **Edit Parameters** tooenter parameters that are passed tooyour Template.</span></span> <span data-ttu-id="90f4e-145">Fournissez hello username et password pour hello du système d’exploitation, qui est le déploiement de hello toocreate requis.</span><span class="sxs-lookup"><span data-stu-id="90f4e-145">Provide hello username and password for hello OS, which is required toocreate hello deployment.</span></span> <span data-ttu-id="90f4e-146">Si vous n’avez outils PowerShell pour Visual Studio est installé, il est recommandé de toocheck **enregistrer les mots de passe** tooavoid une ligne de commande PowerShell masqué invite, ou utilisez [prise en charge keyvault](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/).</span><span class="sxs-lookup"><span data-stu-id="90f4e-146">If you don't have PowerShell Tools for Visual Studio installed, it is recommended toocheck **Save passwords** tooavoid a hidden PowerShell command-line prompt, or use [keyvault support](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/).</span></span>
   
    ![Modifier les paramètres][edit_parameters]

5. <span data-ttu-id="90f4e-148">Cliquez maintenant sur **Déployer**.</span><span class="sxs-lookup"><span data-stu-id="90f4e-148">Now click **Deploy**.</span></span> <span data-ttu-id="90f4e-149">Hello **sortie** fenêtre affiche la progression du déploiement hello.</span><span class="sxs-lookup"><span data-stu-id="90f4e-149">hello **Output** window shows hello deployment progress.</span></span> <span data-ttu-id="90f4e-150">Notez que les actions hello exécute hello **Deploy-azureresourcegroup.ps1** script.</span><span class="sxs-lookup"><span data-stu-id="90f4e-150">Note that hello action is executing hello **Deploy-AzureResourceGroup.ps1** script.</span></span>
   
   ![Fenêtre Sortie][output_window]

## <a name="exploring-your-virtual-machine-scale-set"></a><span data-ttu-id="90f4e-152">Exploration de votre groupe de machines virtuelles identiques</span><span class="sxs-lookup"><span data-stu-id="90f4e-152">Exploring your Virtual Machine Scale Set</span></span>
<span data-ttu-id="90f4e-153">Hello déploiement terminé, vous pouvez afficher hello nouvelle Machine virtuelle ensemble d’échelle Bonjour Visual Studio **Cloud Explorer** (liste d’actualisation hello).</span><span class="sxs-lookup"><span data-stu-id="90f4e-153">Once hello deployment completes, you can view hello new Virtual Machine Scale Set in hello Visual Studio **Cloud Explorer** (refresh hello list).</span></span> <span data-ttu-id="90f4e-154">Cloud Explorer vous permet de gérer des ressources Azure dans Visual Studio lors du développement d'applications.</span><span class="sxs-lookup"><span data-stu-id="90f4e-154">Cloud Explorer lets you manage Azure resources in Visual Studio while developing applications.</span></span> <span data-ttu-id="90f4e-155">Vous pouvez également afficher votre ensemble d’échelle de Machine virtuelle dans hello [portail Azure](https://portal.azure.com) et [Explorateur de ressources Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="90f4e-155">You can also view your Virtual Machine Scale Set in hello [Azure portal](https://portal.azure.com) and [Azure Resource Explorer](https://resources.azure.com/).</span></span>

![Cloud Explorer][cloud_explorer]

 <span data-ttu-id="90f4e-157">portail de Hello fournit la meilleure hello toovisually gérer votre infrastructure d’Azure avec un navigateur web, alors que l’Explorateur de ressources Azure fournit un moyen simple de tooexplore et débogage des ressources Azure, ce qui dans une fenêtre de hello « afficher les instance » et en montrant également PowerShell commandes pour les ressources hello que vous examinez.</span><span class="sxs-lookup"><span data-stu-id="90f4e-157">hello portal provides hello best way toovisually manage your Azure infrastructure with a web browser, while Azure Resource Explorer provides an easy way tooexplore and debug Azure resources, giving a window into hello "instance view" and also showing PowerShell commands for hello resources you are looking at.</span></span>

## <a name="next-steps"></a><span data-ttu-id="90f4e-158">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="90f4e-158">Next steps</span></span>
<span data-ttu-id="90f4e-159">Une fois que vous avez correctement déployé des machines virtuelles identiques via Visual Studio, vous pouvez personnaliser davantage votre toosuit projet spécifications de votre application.</span><span class="sxs-lookup"><span data-stu-id="90f4e-159">Once you’ve successfully deployed Virtual Machine Scale Sets through Visual Studio, you can further customize your project toosuit your application requirements.</span></span> <span data-ttu-id="90f4e-160">Par exemple, configurer à l’échelle automatique en ajoutant un **Insights** ressource, ajout d’infrastructure tooyour modèle (comme les ordinateurs virtuels autonomes), ou du déploiement des applications à l’aide d’extension de script personnalisé hello.</span><span class="sxs-lookup"><span data-stu-id="90f4e-160">For example, configure auto-scale by adding an **Insights** resource, adding infrastructure tooyour Template (like standalone VMs), or deploying applications using hello custom script extension.</span></span> <span data-ttu-id="90f4e-161">Bon exemple modèles se trouvent dans hello [modèles de démarrage rapide Azure](https://github.com/Azure/azure-quickstart-templates) le référentiel GitHub (recherche de « mise »).</span><span class="sxs-lookup"><span data-stu-id="90f4e-161">Good example templates can be found in hello [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates) GitHub repository (search for "vmss").</span></span>

[file_new]: ./media/virtual-machine-scale-sets-vs-create/1-FileNew.png
[create_project]: ./media/virtual-machine-scale-sets-vs-create/2-CreateProject.png
[select_Template]: ./media/virtual-machine-scale-sets-vs-create/3b-SelectTemplateLin.png
[solution_explorer]: ./media/virtual-machine-scale-sets-vs-create/4-SolutionExplorer.png
[json_explorer]: ./media/virtual-machine-scale-sets-vs-create/10-JsonExplorer.png
[5deploy_Template]: ./media/virtual-machine-scale-sets-vs-create/5-DeployTemplate.png
[6deploy_Template]: ./media/virtual-machine-scale-sets-vs-create/6-DeployTemplate.png
[new_resource]: ./media/virtual-machine-scale-sets-vs-create/7-NewResourceGroup.png
[edit_parameters]: ./media/virtual-machine-scale-sets-vs-create/8-EditParameter.png
[output_window]: ./media/virtual-machine-scale-sets-vs-create/9-Output.png
[cloud_explorer]: ./media/virtual-machine-scale-sets-vs-create/12-CloudExplorer.png
