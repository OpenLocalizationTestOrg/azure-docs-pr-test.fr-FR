---
title: "Déployer un groupe de machines virtuelles identiques à l’aide de Visual Studio | Microsoft Docs"
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
ms.openlocfilehash: 78a4b0c8d305f57f495402cecb92d18425ff6bff
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-create-a-virtual-machine-scale-set-with-visual-studio"></a><span data-ttu-id="7be31-103">Création d’un jeu de mise à l’échelle de machines virtuelles avec Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7be31-103">How to create a Virtual Machine Scale Set with Visual Studio</span></span>
<span data-ttu-id="7be31-104">Cet article vous indique comment déployer un jeu de mise à l’échelle de machines virtuelles Azure à l'aide d'un déploiement de groupe de ressources Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7be31-104">This article shows you how to deploy an Azure Virtual Machine Scale Set using a Visual Studio Resource Group Deployment.</span></span>

<span data-ttu-id="7be31-105">Les [groupes de machines virtuelles identiques Azure](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) représentent une ressource de calcul Azure qui permet de déployer et de gérer une collection de machines virtuelles similaires via des options de mise à l'échelle automatique et d'équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="7be31-105">[Azure Virtual Machine Scale Sets](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) is an Azure Compute resource to deploy and manage a collection of similar virtual machines with auto-scale and load balancing.</span></span> <span data-ttu-id="7be31-106">Vous pouvez configurer et déployer des groupes de machines virtuelles identiques à l’aide de [modèles Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="7be31-106">You can provision and deploy Virtual Machine Scale Sets using [Azure Resource Manager Templates](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="7be31-107">Les modèles Azure Resource Manager peuvent être déployés à l’aide de l’interface de ligne de commande (CLI) Azure, de PowerShell, de REST et directement à partir de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7be31-107">Azure Resource Manager Templates can be deployed using Azure CLI, PowerShell, REST and also directly from Visual Studio.</span></span> <span data-ttu-id="7be31-108">Visual Studio fournit des exemples de modèles qui peuvent être déployés dans le cadre d’un projet de déploiement de groupe de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="7be31-108">Visual Studio provides a set of example templates, which can be deployed as part of an Azure Resource Group Deployment project.</span></span>

<span data-ttu-id="7be31-109">Les déploiements de groupe de ressources Azure vous permettent de regrouper et de publier un ensemble de ressources Azure connexes dans une même opération de déploiement.</span><span class="sxs-lookup"><span data-stu-id="7be31-109">Azure Resource Group deployments are a way to group and publish a set of related Azure resources in a single deployment operation.</span></span> <span data-ttu-id="7be31-110">Pour en savoir plus, consultez la rubrique [Création et déploiement de groupes de ressources Azure à l’aide de Visual Studio](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="7be31-110">You can learn more about them here: [Creating and deploying Azure resource groups through Visual Studio](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="7be31-111">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="7be31-111">Pre-requisites</span></span>
<span data-ttu-id="7be31-112">Pour commencer le déploiement de groupes de machines virtuelles identiques dans Visual Studio, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="7be31-112">To get started deploying Virtual Machine Scale Sets in Visual Studio, you need the following:</span></span>

* <span data-ttu-id="7be31-113">Visual Studio 2013 ou une version ultérieure</span><span class="sxs-lookup"><span data-stu-id="7be31-113">Visual Studio 2013 or later</span></span>
* <span data-ttu-id="7be31-114">Kit de développement logiciel (SDK) Azure 2.7, 2.8 ou 2.9</span><span class="sxs-lookup"><span data-stu-id="7be31-114">Azure SDK 2.7, 2.8 or 2.9</span></span>

>[!NOTE]
><span data-ttu-id="7be31-115">Ces instructions partent du principe que vous utilisez Visual Studio avec le [Kit de développement logiciel (SDK) Azure 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).</span><span class="sxs-lookup"><span data-stu-id="7be31-115">These instructions assume you are using Visual Studio with [Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).</span></span>

## <a name="creating-a-project"></a><span data-ttu-id="7be31-116">Création d’un projet</span><span class="sxs-lookup"><span data-stu-id="7be31-116">Creating a Project</span></span>
1. <span data-ttu-id="7be31-117">Créez un projet dans Visual Studio en sélectionnant **Fichier | Nouveau | Projet**.</span><span class="sxs-lookup"><span data-stu-id="7be31-117">Create a new project in Visual Studio by choosing **File | New | Project**.</span></span>
   
    ![Fichier Nouveau][file_new]

2. <span data-ttu-id="7be31-119">Sous **Visual C# | Cloud**, sélectionnez **Azure Resource Manager** pour créer un projet de déploiement d’un modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7be31-119">Under **Visual C# | Cloud**, choose **Azure Resource Manager** to create a project for deploying an Azure Resource Manager Template.</span></span>
   
    ![Créer un projet][create_project]

3. <span data-ttu-id="7be31-121">Depuis la liste des modèles, sélectionnez le modèle de jeux de mise à l'échelle de machines virtuelles Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="7be31-121">From the list of Templates, select either the Linux or Windows Virtual Machine Scale Set Template.</span></span>
   
   ![Sélectionner un modèle][select_Template]

4. <span data-ttu-id="7be31-123">Une fois votre projet créé, des scripts de déploiement PowerShell, un modèle Azure Resource Manager et un fichier de paramètres pour le groupe de machines virtuelles identiques s’affichent.</span><span class="sxs-lookup"><span data-stu-id="7be31-123">Once your project is created you see PowerShell deployment scripts, an Azure Resource Manager Template, and a parameter file for the Virtual Machine Scale Set.</span></span>
   
    ![Explorateur de solutions][solution_explorer]

## <a name="customize-your-project"></a><span data-ttu-id="7be31-125">Personnalisation de votre projet</span><span class="sxs-lookup"><span data-stu-id="7be31-125">Customize your project</span></span>
<span data-ttu-id="7be31-126">Vous pouvez modifier dès à présent le modèle pour le personnaliser en fonction des besoins de votre application, en ajoutant par exemple des propriétés d'extension de machines virtuelles ou en modifiant les règles d'équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="7be31-126">Now you can edit the Template to customize it for your application's needs, such as adding VM extension properties or editing load balancing rules.</span></span> <span data-ttu-id="7be31-127">Par défaut, les modèles de groupe de machines virtuelles identiques sont configurés pour déployer l’extension AzureDiagnostics qui permet d’ajouter très facilement des règles de mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="7be31-127">By default the Virtual Machine Scale Set Templates are configured to deploy the AzureDiagnostics extension, which makes it easy to add autoscale rules.</span></span> <span data-ttu-id="7be31-128">Il déploie également un équilibreur de charge avec une adresse IP publique, configuré avec les règles NAT entrantes.</span><span class="sxs-lookup"><span data-stu-id="7be31-128">It also deploys a load balancer with a public IP address, configured with inbound NAT rules.</span></span> 

<span data-ttu-id="7be31-129">L’équilibrage de charge vous permet de vous connecter aux instances de machine virtuelle avec SSH (Linux) ou RDP (Windows).</span><span class="sxs-lookup"><span data-stu-id="7be31-129">The load balancer lets you connect to the VM instances with SSH (Linux) or RDP (Windows).</span></span> <span data-ttu-id="7be31-130">La plage de ports frontaux commence à 50000.</span><span class="sxs-lookup"><span data-stu-id="7be31-130">The front-end port range starts at 50000.</span></span> <span data-ttu-id="7be31-131">Pour Linux, cela signifie que si vous utilisez SSH pour le port 50000, vous êtes redirigé vers le port 22 de la première machine virtuelle dans le groupe identique.</span><span class="sxs-lookup"><span data-stu-id="7be31-131">For linux this means that if you SSH to port 50000, you are routed to port 22 of the first VM in the Scale Set.</span></span> <span data-ttu-id="7be31-132">La connexion au port 50001 est acheminée vers le port 22 de la deuxième machine virtuelle et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="7be31-132">Connecting to port 50001 is routed to port 22 of the second VM and so on.</span></span>

 <span data-ttu-id="7be31-133">Un bon moyen de modifier vos modèles avec Visual Studio consiste à utiliser le plan JSON pour organiser des paramètres, des variables et des ressources.</span><span class="sxs-lookup"><span data-stu-id="7be31-133">A good way to edit your Templates with Visual Studio is to use the JSON Outline to organize the parameters, variables, and resources.</span></span> <span data-ttu-id="7be31-134">En comprenant le schéma, Visual Studio peut signaler les erreurs figurant dans votre modèle avant de le déployer.</span><span class="sxs-lookup"><span data-stu-id="7be31-134">With an understanding of the schema Visual Studio can point out errors in your Template before you deploy it.</span></span>

![JSON Explorer][json_explorer]

## <a name="deploy-the-project"></a><span data-ttu-id="7be31-136">Déployer le projet</span><span class="sxs-lookup"><span data-stu-id="7be31-136">Deploy the project</span></span>
1. <span data-ttu-id="7be31-137">Déployez le modèle Azure Resource Manager pour créer la ressource du groupe de machines virtuelles identiques.</span><span class="sxs-lookup"><span data-stu-id="7be31-137">Deploy the Azure Resource Manager Template to create the Virtual Machine Scale Set resource.</span></span> <span data-ttu-id="7be31-138">Cliquez avec le bouton droit de la souris sur le nœud du projet et sélectionnez **Déployer | Nouveau déploiement**.</span><span class="sxs-lookup"><span data-stu-id="7be31-138">Right-click on the project node and choose **Deploy | New Deployment**.</span></span>
   
    ![Déployer un modèle][5deploy_Template]
    
2. <span data-ttu-id="7be31-140">Sélectionnez votre abonnement dans la boîte de dialogue « Déploiement vers un groupe de ressources ».</span><span class="sxs-lookup"><span data-stu-id="7be31-140">Select your subscription in the “Deploy to Resource Group” dialog.</span></span>
   
    ![Déployer un modèle][6deploy_Template]

3. <span data-ttu-id="7be31-142">À ce stade, vous pouvez créer un groupe de ressources Azure sur lequel déployer votre modèle.</span><span class="sxs-lookup"><span data-stu-id="7be31-142">From here, you can create an Azure Resource Group to deploy your Template to.</span></span>
   
    ![Nouveau groupe de ressources][new_resource]

4. <span data-ttu-id="7be31-144">Ensuite, cliquez sur **Modifier les paramètres** pour entrer des paramètres qui sont transmis à votre modèle.</span><span class="sxs-lookup"><span data-stu-id="7be31-144">Next, click **Edit Parameters** to enter parameters that are passed to your Template.</span></span> <span data-ttu-id="7be31-145">Entrez le nom d’utilisateur et le mot de passe pour le système d’exploitation, requis pour créer le déploiement.</span><span class="sxs-lookup"><span data-stu-id="7be31-145">Provide the username and password for the OS, which is required to create the deployment.</span></span> <span data-ttu-id="7be31-146">Si les outils PowerShell pour Visual Studio ne sont pas installés, il est recommandé d’activer l’option **Enregistrer les mots de passe** afin d’éviter une invite de ligne de commande PowerShell masquée, ou utilisez le [support KeyVault](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/).</span><span class="sxs-lookup"><span data-stu-id="7be31-146">If you don't have PowerShell Tools for Visual Studio installed, it is recommended to check **Save passwords** to avoid a hidden PowerShell command-line prompt, or use [keyvault support](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/).</span></span>
   
    ![Modifier les paramètres][edit_parameters]

5. <span data-ttu-id="7be31-148">Cliquez maintenant sur **Déployer**.</span><span class="sxs-lookup"><span data-stu-id="7be31-148">Now click **Deploy**.</span></span> <span data-ttu-id="7be31-149">La fenêtre **Sortie** affiche la progression du déploiement.</span><span class="sxs-lookup"><span data-stu-id="7be31-149">The **Output** window shows the deployment progress.</span></span> <span data-ttu-id="7be31-150">Notez que l’action exécute le script **Deploy-AzureResourceGroup.ps1**.</span><span class="sxs-lookup"><span data-stu-id="7be31-150">Note that the action is executing the **Deploy-AzureResourceGroup.ps1** script.</span></span>
   
   ![Fenêtre Sortie][output_window]

## <a name="exploring-your-virtual-machine-scale-set"></a><span data-ttu-id="7be31-152">Exploration de votre groupe de machines virtuelles identiques</span><span class="sxs-lookup"><span data-stu-id="7be31-152">Exploring your Virtual Machine Scale Set</span></span>
<span data-ttu-id="7be31-153">Une fois le déploiement terminé, vous pouvez afficher le nouveau groupe de machines virtuelles identiques dans le **Cloud Explorer** de Visual Studio (actualisez la liste).</span><span class="sxs-lookup"><span data-stu-id="7be31-153">Once the deployment completes, you can view the new Virtual Machine Scale Set in the Visual Studio **Cloud Explorer** (refresh the list).</span></span> <span data-ttu-id="7be31-154">Cloud Explorer vous permet de gérer des ressources Azure dans Visual Studio lors du développement d'applications.</span><span class="sxs-lookup"><span data-stu-id="7be31-154">Cloud Explorer lets you manage Azure resources in Visual Studio while developing applications.</span></span> <span data-ttu-id="7be31-155">Vous pouvez également afficher votre groupe identique de machines virtuelles dans le [portail Azure](https://portal.azure.com) et [l’Explorateur de ressources Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="7be31-155">You can also view your Virtual Machine Scale Set in the [Azure portal](https://portal.azure.com) and [Azure Resource Explorer](https://resources.azure.com/).</span></span>

![Cloud Explorer][cloud_explorer]

 <span data-ttu-id="7be31-157">Le portail vous explique comment gérer visuellement votre infrastructure Azure par le biais d’un navigateur web, tandis qu’Azure Resource Explorer vous permet d’explorer et de déboguer très facilement des ressources Azure, en vous donnant un aperçu de la « vue d’instance » et en vous indiquant également les commandes PowerShell pour les ressources que vous recherchez.</span><span class="sxs-lookup"><span data-stu-id="7be31-157">The portal provides the best way to visually manage your Azure infrastructure with a web browser, while Azure Resource Explorer provides an easy way to explore and debug Azure resources, giving a window into the "instance view" and also showing PowerShell commands for the resources you are looking at.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7be31-158">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7be31-158">Next steps</span></span>
<span data-ttu-id="7be31-159">Une fois les groupes de machines virtuelles identiques déployés avec succès via Visual Studio, vous pouvez personnaliser davantage votre projet en fonction des besoins de votre application.</span><span class="sxs-lookup"><span data-stu-id="7be31-159">Once you’ve successfully deployed Virtual Machine Scale Sets through Visual Studio, you can further customize your project to suit your application requirements.</span></span> <span data-ttu-id="7be31-160">Vous pouvez, par exemple, configurer la mise à l’échelle automatique via l’ajout d’une ressource **Insights**, l’ajout d’une infrastructure à votre modèle (comme des machines virtuelles autonomes) ou le déploiement d’applications à l’aide de l’extension de script personnalisé.</span><span class="sxs-lookup"><span data-stu-id="7be31-160">For example, configure auto-scale by adding an **Insights** resource, adding infrastructure to your Template (like standalone VMs), or deploying applications using the custom script extension.</span></span> <span data-ttu-id="7be31-161">Vous trouverez de bons exemples de modèles dans le référentiel GitHub [Modèles de démarrage rapide Azure](https://github.com/Azure/azure-quickstart-templates) (recherchez le terme « vmss »).</span><span class="sxs-lookup"><span data-stu-id="7be31-161">Good example templates can be found in the [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates) GitHub repository (search for "vmss").</span></span>

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
