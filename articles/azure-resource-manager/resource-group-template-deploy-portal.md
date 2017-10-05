---
title: "Utiliser le Portail Azure pour déployer des ressources Azure | Microsoft Docs"
description: "Utilisez le Portail Azure et Azure Resource Manager pour déployer vos ressources."
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 2c98a4aa-8d9f-4a0a-b764-214dbe8ed009
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: a4cac5834c667976b0a2d1f2748e4309a166d16a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-portal"></a><span data-ttu-id="363b8-103">Déployer des ressources à l’aide de modèles Resource Manager et du Portail Azure</span><span class="sxs-lookup"><span data-stu-id="363b8-103">Deploy resources with Resource Manager templates and Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="363b8-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="363b8-104">PowerShell</span></span>](resource-group-template-deploy.md)
> * [<span data-ttu-id="363b8-105">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="363b8-105">Azure CLI</span></span>](resource-group-template-deploy-cli.md)
> * [<span data-ttu-id="363b8-106">Portail</span><span class="sxs-lookup"><span data-stu-id="363b8-106">Portal</span></span>](resource-group-template-deploy-portal.md)
> * [<span data-ttu-id="363b8-107">API REST</span><span class="sxs-lookup"><span data-stu-id="363b8-107">REST API</span></span>](resource-group-template-deploy-rest.md)
> 
> 

<span data-ttu-id="363b8-108">Cette rubrique montre comment utiliser le [portail Azure](https://portal.azure.com) avec [Azure Resource Manager](resource-group-overview.md) pour déployer vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="363b8-108">This topic shows how to use the [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) to deploy your Azure resources.</span></span> <span data-ttu-id="363b8-109">Pour en savoir plus sur la gestion de vos ressources, consultez [Gérer des ressources Azure avec le portail](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="363b8-109">To learn about managing your resources, see [Manage Azure resources through portal](resource-group-portal.md).</span></span>

<span data-ttu-id="363b8-110">Actuellement, certains services ne prennent pas en charge le portail ou Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="363b8-110">Currently, not every service supports the portal or Resource Manager.</span></span> <span data-ttu-id="363b8-111">Pour ces services, vous devez utiliser le [Portail Azure Classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="363b8-111">For those services, you need to use the [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="363b8-112">Pour connaître l’état de chaque service, voir [Graphique de la disponibilité du portail Azure](https://azure.microsoft.com/features/azure-portal/availability/).</span><span class="sxs-lookup"><span data-stu-id="363b8-112">For the status of each service, see [Azure portal availability chart](https://azure.microsoft.com/features/azure-portal/availability/).</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="363b8-113">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="363b8-113">Create resource group</span></span>
1. <span data-ttu-id="363b8-114">Pour créer un groupe de ressources vide, sélectionnez **Nouveau** > **Gestion** > **Groupe de ressources**.</span><span class="sxs-lookup"><span data-stu-id="363b8-114">To create an empty resource group, select **New** > **Management** > **Resource Group**.</span></span>
   
    ![créer un groupe de ressources vide](./media/resource-group-template-deploy-portal/create-empty-group.png)
2. <span data-ttu-id="363b8-116">Spécifiez un nom et un emplacement, puis, si nécessaire, sélectionnez un abonnement.</span><span class="sxs-lookup"><span data-stu-id="363b8-116">Give it a name and location, and, if necessary, select a subscription.</span></span> <span data-ttu-id="363b8-117">Vous devez fournir un emplacement pour le groupe de ressources, car celui-ci stocke des métadonnées sur les ressources.</span><span class="sxs-lookup"><span data-stu-id="363b8-117">You need to provide a location for the resource group because the resource group stores metadata about the resources.</span></span> <span data-ttu-id="363b8-118">Pour des raisons de conformité, vous souhaiterez peut-être indiquer où sont stockées métadonnées.</span><span class="sxs-lookup"><span data-stu-id="363b8-118">For compliance reasons, you may want to specify where that metadata is stored.</span></span> <span data-ttu-id="363b8-119">En règle générale, nous vous recommandons de spécifier l’emplacement où réside la plupart de vos ressources.</span><span class="sxs-lookup"><span data-stu-id="363b8-119">In general, we recommend that you specify a location where most of your resources will reside.</span></span> <span data-ttu-id="363b8-120">L’utilisation du même emplacement permet de simplifier votre modèle.</span><span class="sxs-lookup"><span data-stu-id="363b8-120">Using the same location can simplify your template.</span></span>
   
    ![définir les valeurs d’un groupe](./media/resource-group-template-deploy-portal/set-group-properties.png)

## <a name="deploy-resources-from-marketplace"></a><span data-ttu-id="363b8-122">Déployer des ressources à partir de Marketplace</span><span class="sxs-lookup"><span data-stu-id="363b8-122">Deploy resources from Marketplace</span></span>
<span data-ttu-id="363b8-123">Une fois votre groupe de ressources créé, vous pouvez y déployer des ressources à partir de Marketplace.</span><span class="sxs-lookup"><span data-stu-id="363b8-123">After you create a resource group, you can deploy resources to it from the Marketplace.</span></span> <span data-ttu-id="363b8-124">Marketplace fournit des solutions prédéfinies pour les scénarios courants.</span><span class="sxs-lookup"><span data-stu-id="363b8-124">The Marketplace provides pre-defined solutions for common scenarios.</span></span>

1. <span data-ttu-id="363b8-125">Pour commencer un déploiement, sélectionnez **Nouveau** et choisissez le type de ressource que vous souhaitez déployer.</span><span class="sxs-lookup"><span data-stu-id="363b8-125">To start a deployment, select **New** and the type of resource you would like to deploy.</span></span> <span data-ttu-id="363b8-126">Ensuite, recherchez la version de la ressource que vous souhaitez déployer.</span><span class="sxs-lookup"><span data-stu-id="363b8-126">Then, look for the particular version of the resource you would like to deploy.</span></span>
   
    ![déployer des ressources](./media/resource-group-template-deploy-portal/deploy-resource.png)
2. <span data-ttu-id="363b8-128">Si vous ne voyez pas la solution que vous souhaitez déployer, vous pouvez lancer une recherche sur le Marketplace.</span><span class="sxs-lookup"><span data-stu-id="363b8-128">If you do not see the particular solution you would like to deploy, you can search the Marketplace for it.</span></span>
   
    ![effectuer une recherche sur le marketplace](./media/resource-group-template-deploy-portal/search-resource.png)
3. <span data-ttu-id="363b8-130">Selon le type de ressource que vous avez sélectionné, vous devrez définir une collection de propriétés pertinentes avant le déploiement.</span><span class="sxs-lookup"><span data-stu-id="363b8-130">Depending on the type of selected resource, you have a collection of relevant properties to set before deployment.</span></span> <span data-ttu-id="363b8-131">Ces options ne sont pas présentées ici, car elles varient selon le type de ressource.</span><span class="sxs-lookup"><span data-stu-id="363b8-131">Those options are not shown here, as they vary based on resource type.</span></span> <span data-ttu-id="363b8-132">Pour tous les types, vous devez sélectionner un groupe de ressources de destination.</span><span class="sxs-lookup"><span data-stu-id="363b8-132">For all types, you must select a destination resource group.</span></span> <span data-ttu-id="363b8-133">L’illustration suivante montre comment créer une application web et la déployer dans le groupe de ressources que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="363b8-133">The following image shows how to create a web app and deploy it to the resource group you created.</span></span>
   
    ![Créer un groupe de ressources](./media/resource-group-template-deploy-portal/select-existing-group.png)
   
    <span data-ttu-id="363b8-135">Vous pouvez également décider de créer un groupe de ressources lors du déploiement de vos ressources.</span><span class="sxs-lookup"><span data-stu-id="363b8-135">Alternatively, you can decide to create a resource group when deploying your resources.</span></span> <span data-ttu-id="363b8-136">Sélectionnez **Créer** et donnez un nom au groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="363b8-136">Select **Create new** and give the resource group a name.</span></span>
   
    ![créer un groupe de ressources](./media/resource-group-template-deploy-portal/select-new-group.png)
4. <span data-ttu-id="363b8-138">Votre déploiement se met en route.</span><span class="sxs-lookup"><span data-stu-id="363b8-138">Your deployment begins.</span></span> <span data-ttu-id="363b8-139">Ce déploiement peut prendre quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="363b8-139">The deployment could take a few minutes.</span></span> <span data-ttu-id="363b8-140">Vous recevez une notification une fois le déploiement terminé.</span><span class="sxs-lookup"><span data-stu-id="363b8-140">When the deployment has finished, you see a notification.</span></span>
   
    ![afficher une notification](./media/resource-group-template-deploy-portal/view-notification.png)
5. <span data-ttu-id="363b8-142">Après avoir déployé vos ressources, vous pouvez ajouter d’autres ressources au groupe de ressources au moyen de la commande **Ajouter** sur le panneau du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="363b8-142">After deploying your resources, you can add more resources to the resource group by using the **Add** command on the resource group blade.</span></span>
   
    ![ajouter une ressource](./media/resource-group-template-deploy-portal/add-resource.png)

## <a name="deploy-resources-from-custom-template"></a><span data-ttu-id="363b8-144">Déployer des ressources à partir d’un modèle personnalisé</span><span class="sxs-lookup"><span data-stu-id="363b8-144">Deploy resources from custom template</span></span>
<span data-ttu-id="363b8-145">Si vous souhaitez effectuer un déploiement sans utiliser l’un des modèles de Marketplace, vous pouvez créer un modèle personnalisé qui définit l’infrastructure de votre solution.</span><span class="sxs-lookup"><span data-stu-id="363b8-145">If you want to execute a deployment but not use any of the templates in the Marketplace, you can create a customized template that defines the infrastructure for your solution.</span></span> <span data-ttu-id="363b8-146">Pour en savoir plus sur la création de modèles, consultez [Création de modèles Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="363b8-146">To learn about creating templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

1. <span data-ttu-id="363b8-147">Pour déployer un modèle personnalisé à travers le portail, sélectionnez **Nouveau**, puis recherchez le **Déploiement de modèle** jusqu’à ce que vous puissiez le sélectionner dans les options.</span><span class="sxs-lookup"><span data-stu-id="363b8-147">To deploy a customized template through the portal, select **New**, and start searching for **Template Deployment** until you can select it from the options.</span></span>
   
    ![rechercher un déploiement de modèle](./media/resource-group-template-deploy-portal/search-template.png)
2. <span data-ttu-id="363b8-149">Sélectionnez **Déploiement de modèle** dans les ressources disponibles.</span><span class="sxs-lookup"><span data-stu-id="363b8-149">Select **Template Deployment** from the available resources.</span></span>
   
    ![sélectionner un déploiement de modèle](./media/resource-group-template-deploy-portal/select-template.png)
3. <span data-ttu-id="363b8-151">Après avoir lancé le déploiement du modèle, ouvrez le modèle vide qui peut être personnalisé.</span><span class="sxs-lookup"><span data-stu-id="363b8-151">After launching the template deployment, open the blank template that is available for customizing.</span></span>
   
    ![créer un modèle](./media/resource-group-template-deploy-portal/show-custom-template.png)
   
    <span data-ttu-id="363b8-153">Dans l’éditeur, ajoutez la syntaxe JSON qui définit les ressources que vous souhaitez déployer.</span><span class="sxs-lookup"><span data-stu-id="363b8-153">In the editor, add the JSON syntax that defines the resources you want to deploy.</span></span> <span data-ttu-id="363b8-154">Sélectionnez **Enregistrer** lorsque vous avez terminé.</span><span class="sxs-lookup"><span data-stu-id="363b8-154">Select **Save** when done.</span></span> <span data-ttu-id="363b8-155">Pour obtenir des conseils sur l’écriture de la syntaxe JSON, consultez [Guide de création d’un modèle Resource Manager](resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="363b8-155">For guidance on writing the JSON syntax, see [Resource Manager template walkthrough](resource-manager-template-walkthrough.md).</span></span>
   
    ![modifier un modèle](./media/resource-group-template-deploy-portal/edit-template.png)
4. <span data-ttu-id="363b8-157">Vous pouvez également sélectionner un modèle existant à partir des [modèles de démarrage rapide Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="363b8-157">Or, you can select a pre-existing template from the [Azure quickstart templates](https://azure.microsoft.com/documentation/templates/).</span></span> <span data-ttu-id="363b8-158">Ces modèles sont fournis par la communauté.</span><span class="sxs-lookup"><span data-stu-id="363b8-158">These templates are contributed by the community.</span></span> <span data-ttu-id="363b8-159">Ils couvrent de nombreux scénarios courants, et il est donc possible que quelqu’un ait ajouté un modèle semblable à celui que vous tentez de déployer.</span><span class="sxs-lookup"><span data-stu-id="363b8-159">They cover many common scenarios, and someone may have added a template that is similar to what you are trying to deploy.</span></span> <span data-ttu-id="363b8-160">Vous pouvez rechercher parmi les modèles pour trouver un élément qui correspond à votre scénario.</span><span class="sxs-lookup"><span data-stu-id="363b8-160">You can search the templates to find something that matches your scenario.</span></span>
   
    ![sélectionner un modèle de démarrage rapide](./media/resource-group-template-deploy-portal/select-quickstart-template.png)
   
    <span data-ttu-id="363b8-162">Vous pouvez afficher le modèle sélectionné dans l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="363b8-162">You can view the selected template in the editor.</span></span>
5. <span data-ttu-id="363b8-163">Après avoir entré toutes les autres valeurs, sélectionnez **Créer** pour déployer le modèle.</span><span class="sxs-lookup"><span data-stu-id="363b8-163">After providing all the other values, select **Create** to deploy the template.</span></span> 
   
    ![déployer un modèle](./media/resource-group-template-deploy-portal/create-custom-deploy.png)

## <a name="deploy-resources-from-a-template-saved-to-your-account"></a><span data-ttu-id="363b8-165">Déployer des ressources à partir d’un modèle enregistré dans votre compte</span><span class="sxs-lookup"><span data-stu-id="363b8-165">Deploy resources from a template saved to your account</span></span>
<span data-ttu-id="363b8-166">Le portail vous permet d’enregistrer un modèle dans votre compte Azure et de le redéployer ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="363b8-166">The portal enables you to save a template to your Azure account, and redeploy it later.</span></span> <span data-ttu-id="363b8-167">Pour plus d’informations sur l’utilisation de ces modèles enregistrés, accédez à [Prise en main des modèles privés sur le Portail Azure](../marketplace-consumer/mytemplates-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="363b8-167">For more information about working with these saved templates, [Get started with private templates on the Azure portal](../marketplace-consumer/mytemplates-getstarted.md).</span></span>

1. <span data-ttu-id="363b8-168">Pour rechercher vos modèles enregistrés, sélectionnez **Parcourir** > **Modèles**.</span><span class="sxs-lookup"><span data-stu-id="363b8-168">To find your saved templates, select **Browse** > **Templates**.</span></span>
   
    ![parcourir les modèles](./media/resource-group-template-deploy-portal/browse-templates.png)
2. <span data-ttu-id="363b8-170">Dans la liste des modèles enregistrés dans votre compte, sélectionnez celui sur lequel vous souhaitez travailler.</span><span class="sxs-lookup"><span data-stu-id="363b8-170">From the list of templates saved to your account, select the one you wish to work on.</span></span>
   
    ![modèles enregistrés](./media/resource-group-template-deploy-portal/saved-templates.png)
3. <span data-ttu-id="363b8-172">Sélectionnez **Déployer** pour redéployer ce modèle enregistré.</span><span class="sxs-lookup"><span data-stu-id="363b8-172">Select **Deploy** to redeploy this saved template.</span></span>
   
    ![déployer un modèle enregistré](./media/resource-group-template-deploy-portal/deploy-saved-template.png)

## <a name="next-steps"></a><span data-ttu-id="363b8-174">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="363b8-174">Next steps</span></span>
* <span data-ttu-id="363b8-175">Pour visualiser les journaux d’audit, voir [Opérations d’audit avec Resource Manager](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="363b8-175">To view audit logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="363b8-176">Pour résoudre les erreurs de déploiement, consultez [Voir les opérations de déploiement](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="363b8-176">To troubleshoot deployment errors, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="363b8-177">Pour récupérer un modèle à partir d’un déploiement ou d’un groupe de ressources, consultez [Exporter un modèle Azure Resource Manager à partir de ressources existantes](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="363b8-177">To retrieve a template from a deployment or resource group, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="363b8-178">Pour obtenir des conseils sur l’utilisation de Resource Manager par les entreprises pour gérer efficacement les abonnements, voir [Structure d’Azure Enterprise - Gouvernance normative de l’abonnement](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="363b8-178">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

