---
title: aaaUse toodeploy portail Azure ressources Azure | Documents Microsoft
description: "Utiliser le portail Azure et gérer les ressources Azure de toodeploy vos ressources."
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
ms.openlocfilehash: 5a5217f94c8dfc0c1ebd613903ea3dcbe1197bfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-portal"></a><span data-ttu-id="f7600-103">Déployer des ressources à l’aide de modèles Resource Manager et du Portail Azure</span><span class="sxs-lookup"><span data-stu-id="f7600-103">Deploy resources with Resource Manager templates and Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f7600-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f7600-104">PowerShell</span></span>](resource-group-template-deploy.md)
> * [<span data-ttu-id="f7600-105">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="f7600-105">Azure CLI</span></span>](resource-group-template-deploy-cli.md)
> * [<span data-ttu-id="f7600-106">Portail</span><span class="sxs-lookup"><span data-stu-id="f7600-106">Portal</span></span>](resource-group-template-deploy-portal.md)
> * [<span data-ttu-id="f7600-107">API REST</span><span class="sxs-lookup"><span data-stu-id="f7600-107">REST API</span></span>](resource-group-template-deploy-rest.md)
> 
> 

<span data-ttu-id="f7600-108">Cette rubrique montre comment toouse hello [portail Azure](https://portal.azure.com) avec [Azure Resource Manager](resource-group-overview.md) toodeploy vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="f7600-108">This topic shows how toouse hello [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) toodeploy your Azure resources.</span></span> <span data-ttu-id="f7600-109">toolearn sur la gestion de vos ressources, consultez [des ressources de gestion de Azure via le portail](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f7600-109">toolearn about managing your resources, see [Manage Azure resources through portal](resource-group-portal.md).</span></span>

<span data-ttu-id="f7600-110">Actuellement, pas tous les services prend en charge le portail de hello ou Gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="f7600-110">Currently, not every service supports hello portal or Resource Manager.</span></span> <span data-ttu-id="f7600-111">Pour ces services, vous devez toouse hello [portail classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="f7600-111">For those services, you need toouse hello [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="f7600-112">Statut de hello de chaque service, consultez [graphique de la disponibilité de portail Azure](https://azure.microsoft.com/features/azure-portal/availability/).</span><span class="sxs-lookup"><span data-stu-id="f7600-112">For hello status of each service, see [Azure portal availability chart](https://azure.microsoft.com/features/azure-portal/availability/).</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="f7600-113">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="f7600-113">Create resource group</span></span>
1. <span data-ttu-id="f7600-114">toocreate un groupe de ressources vide, sélectionnez **nouveau** > **gestion** > **groupe de ressources**.</span><span class="sxs-lookup"><span data-stu-id="f7600-114">toocreate an empty resource group, select **New** > **Management** > **Resource Group**.</span></span>
   
    ![créer un groupe de ressources vide](./media/resource-group-template-deploy-portal/create-empty-group.png)
2. <span data-ttu-id="f7600-116">Spécifiez un nom et un emplacement, puis, si nécessaire, sélectionnez un abonnement.</span><span class="sxs-lookup"><span data-stu-id="f7600-116">Give it a name and location, and, if necessary, select a subscription.</span></span> <span data-ttu-id="f7600-117">Vous devez tooprovide un emplacement pour le groupe de ressources hello, car le groupe de ressources hello stocke les métadonnées sur les ressources de hello.</span><span class="sxs-lookup"><span data-stu-id="f7600-117">You need tooprovide a location for hello resource group because hello resource group stores metadata about hello resources.</span></span> <span data-ttu-id="f7600-118">Pour des raisons de compatibilité, vous souhaiterez toospecify où que les métadonnées sont stockées.</span><span class="sxs-lookup"><span data-stu-id="f7600-118">For compliance reasons, you may want toospecify where that metadata is stored.</span></span> <span data-ttu-id="f7600-119">En règle générale, nous vous recommandons de spécifier l’emplacement où réside la plupart de vos ressources.</span><span class="sxs-lookup"><span data-stu-id="f7600-119">In general, we recommend that you specify a location where most of your resources will reside.</span></span> <span data-ttu-id="f7600-120">À l’aide de hello même emplacement peut simplifier votre modèle.</span><span class="sxs-lookup"><span data-stu-id="f7600-120">Using hello same location can simplify your template.</span></span>
   
    ![définir les valeurs d’un groupe](./media/resource-group-template-deploy-portal/set-group-properties.png)

## <a name="deploy-resources-from-marketplace"></a><span data-ttu-id="f7600-122">Déployer des ressources à partir de Marketplace</span><span class="sxs-lookup"><span data-stu-id="f7600-122">Deploy resources from Marketplace</span></span>
<span data-ttu-id="f7600-123">Après avoir créé un groupe de ressources, vous pouvez déployer tooit de ressources à partir de hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f7600-123">After you create a resource group, you can deploy resources tooit from hello Marketplace.</span></span> <span data-ttu-id="f7600-124">Hello Marketplace fournit des solutions prédéfinies pour les scénarios courants.</span><span class="sxs-lookup"><span data-stu-id="f7600-124">hello Marketplace provides pre-defined solutions for common scenarios.</span></span>

1. <span data-ttu-id="f7600-125">toostart un déploiement, sélectionnez **nouveau** et hello type de ressource, vous aimeriez toodeploy.</span><span class="sxs-lookup"><span data-stu-id="f7600-125">toostart a deployment, select **New** and hello type of resource you would like toodeploy.</span></span> <span data-ttu-id="f7600-126">Ensuite, recherchez version particulière de hello de ressource de hello vous aimeriez toodeploy.</span><span class="sxs-lookup"><span data-stu-id="f7600-126">Then, look for hello particular version of hello resource you would like toodeploy.</span></span>
   
    ![déployer des ressources](./media/resource-group-template-deploy-portal/deploy-resource.png)
2. <span data-ttu-id="f7600-128">Si vous ne voyez pas de solution spécifique de hello toodeploy voulue, vous pouvez rechercher hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f7600-128">If you do not see hello particular solution you would like toodeploy, you can search hello Marketplace for it.</span></span>
   
    ![effectuer une recherche sur le marketplace](./media/resource-group-template-deploy-portal/search-resource.png)
3. <span data-ttu-id="f7600-130">En fonction de type hello de ressource sélectionnée, vous avez une collection de propriétés pertinentes des tooset avant le déploiement.</span><span class="sxs-lookup"><span data-stu-id="f7600-130">Depending on hello type of selected resource, you have a collection of relevant properties tooset before deployment.</span></span> <span data-ttu-id="f7600-131">Ces options ne sont pas présentées ici, car elles varient selon le type de ressource.</span><span class="sxs-lookup"><span data-stu-id="f7600-131">Those options are not shown here, as they vary based on resource type.</span></span> <span data-ttu-id="f7600-132">Pour tous les types, vous devez sélectionner un groupe de ressources de destination.</span><span class="sxs-lookup"><span data-stu-id="f7600-132">For all types, you must select a destination resource group.</span></span> <span data-ttu-id="f7600-133">image de suivante de Hello montre comment toocreate une application web et le déployer le groupe de ressources toohello vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="f7600-133">hello following image shows how toocreate a web app and deploy it toohello resource group you created.</span></span>
   
    ![Créer un groupe de ressources](./media/resource-group-template-deploy-portal/select-existing-group.png)
   
    <span data-ttu-id="f7600-135">Ou bien, vous pouvez décider toocreate un groupe de ressources lors du déploiement de vos ressources.</span><span class="sxs-lookup"><span data-stu-id="f7600-135">Alternatively, you can decide toocreate a resource group when deploying your resources.</span></span> <span data-ttu-id="f7600-136">Sélectionnez **nouvel** et donnez un nom à groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="f7600-136">Select **Create new** and give hello resource group a name.</span></span>
   
    ![créer un groupe de ressources](./media/resource-group-template-deploy-portal/select-new-group.png)
4. <span data-ttu-id="f7600-138">Votre déploiement se met en route.</span><span class="sxs-lookup"><span data-stu-id="f7600-138">Your deployment begins.</span></span> <span data-ttu-id="f7600-139">déploiement de Hello peut prendre quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="f7600-139">hello deployment could take a few minutes.</span></span> <span data-ttu-id="f7600-140">Déploiement de hello terminée, vous voyez une notification.</span><span class="sxs-lookup"><span data-stu-id="f7600-140">When hello deployment has finished, you see a notification.</span></span>
   
    ![afficher une notification](./media/resource-group-template-deploy-portal/view-notification.png)
5. <span data-ttu-id="f7600-142">Après avoir déployé vos ressources, vous pouvez ajouter le groupe de ressources de plusieurs ressources toohello à l’aide de hello **ajouter** commande sur le panneau des ressources de groupe hello.</span><span class="sxs-lookup"><span data-stu-id="f7600-142">After deploying your resources, you can add more resources toohello resource group by using hello **Add** command on hello resource group blade.</span></span>
   
    ![ajouter une ressource](./media/resource-group-template-deploy-portal/add-resource.png)

## <a name="deploy-resources-from-custom-template"></a><span data-ttu-id="f7600-144">Déployer des ressources à partir d’un modèle personnalisé</span><span class="sxs-lookup"><span data-stu-id="f7600-144">Deploy resources from custom template</span></span>
<span data-ttu-id="f7600-145">Si vous voulez tooexecute un déploiement mais pas un des modèles de hello Bonjour Marketplace, vous pouvez créer un modèle personnalisé qui définit l’infrastructure hello pour votre solution.</span><span class="sxs-lookup"><span data-stu-id="f7600-145">If you want tooexecute a deployment but not use any of hello templates in hello Marketplace, you can create a customized template that defines hello infrastructure for your solution.</span></span> <span data-ttu-id="f7600-146">toolearn sur la création de modèles, consultez [les modèles de programmation Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f7600-146">toolearn about creating templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

1. <span data-ttu-id="f7600-147">toodeploy un modèle personnalisé via le portail de hello, sélectionnez **nouveau**et commencer à rechercher **déploiement d’un modèle** jusqu'à ce que vous pouvez le sélectionner à partir des options de hello.</span><span class="sxs-lookup"><span data-stu-id="f7600-147">toodeploy a customized template through hello portal, select **New**, and start searching for **Template Deployment** until you can select it from hello options.</span></span>
   
    ![rechercher un déploiement de modèle](./media/resource-group-template-deploy-portal/search-template.png)
2. <span data-ttu-id="f7600-149">Sélectionnez **déploiement d’un modèle** à partir des ressources disponibles de hello.</span><span class="sxs-lookup"><span data-stu-id="f7600-149">Select **Template Deployment** from hello available resources.</span></span>
   
    ![sélectionner un déploiement de modèle](./media/resource-group-template-deploy-portal/select-template.png)
3. <span data-ttu-id="f7600-151">Après le lancement du déploiement d’un modèle hello, ouvrez le modèle vide hello n’est disponible pour la personnalisation.</span><span class="sxs-lookup"><span data-stu-id="f7600-151">After launching hello template deployment, open hello blank template that is available for customizing.</span></span>
   
    ![créer un modèle](./media/resource-group-template-deploy-portal/show-custom-template.png)
   
    <span data-ttu-id="f7600-153">Dans l’éditeur de hello, ajoutez la syntaxe hello JSON qui définit les ressources hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="f7600-153">In hello editor, add hello JSON syntax that defines hello resources you want toodeploy.</span></span> <span data-ttu-id="f7600-154">Sélectionnez **Enregistrer** lorsque vous avez terminé.</span><span class="sxs-lookup"><span data-stu-id="f7600-154">Select **Save** when done.</span></span> <span data-ttu-id="f7600-155">Pour obtenir des conseils sur l’écriture de syntaxe de hello JSON, consultez [procédure pas à pas de gestionnaire de ressources du modèle](resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="f7600-155">For guidance on writing hello JSON syntax, see [Resource Manager template walkthrough](resource-manager-template-walkthrough.md).</span></span>
   
    ![modifier un modèle](./media/resource-group-template-deploy-portal/edit-template.png)
4. <span data-ttu-id="f7600-157">Ou bien, vous pouvez sélectionner un modèle existant à partir de hello [modèles de démarrage rapide Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="f7600-157">Or, you can select a pre-existing template from hello [Azure quickstart templates](https://azure.microsoft.com/documentation/templates/).</span></span> <span data-ttu-id="f7600-158">Ces modèles sont fournis par la Communauté de hello.</span><span class="sxs-lookup"><span data-stu-id="f7600-158">These templates are contributed by hello community.</span></span> <span data-ttu-id="f7600-159">Qu’ils couvrent de nombreux scénarios courants, et une personne a peut-être ajouté un modèle similaire toowhat vous essayez de toodeploy.</span><span class="sxs-lookup"><span data-stu-id="f7600-159">They cover many common scenarios, and someone may have added a template that is similar toowhat you are trying toodeploy.</span></span> <span data-ttu-id="f7600-160">Vous pouvez rechercher un élément qui correspond à votre scénario hello modèles toofind.</span><span class="sxs-lookup"><span data-stu-id="f7600-160">You can search hello templates toofind something that matches your scenario.</span></span>
   
    ![sélectionner un modèle de démarrage rapide](./media/resource-group-template-deploy-portal/select-quickstart-template.png)
   
    <span data-ttu-id="f7600-162">Vous pouvez afficher le modèle sélectionné de hello dans l’éditeur de hello.</span><span class="sxs-lookup"><span data-stu-id="f7600-162">You can view hello selected template in hello editor.</span></span>
5. <span data-ttu-id="f7600-163">Après avoir entré hello toutes les autres valeurs, sélectionnez **créer** modèle de hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="f7600-163">After providing all hello other values, select **Create** toodeploy hello template.</span></span> 
   
    ![déployer un modèle](./media/resource-group-template-deploy-portal/create-custom-deploy.png)

## <a name="deploy-resources-from-a-template-saved-tooyour-account"></a><span data-ttu-id="f7600-165">Déployer des ressources à partir d’un modèle enregistré tooyour compte</span><span class="sxs-lookup"><span data-stu-id="f7600-165">Deploy resources from a template saved tooyour account</span></span>
<span data-ttu-id="f7600-166">Hello portail permet de toosave un tooyour modèle compte Azure et recommencer ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="f7600-166">hello portal enables you toosave a template tooyour Azure account, and redeploy it later.</span></span> <span data-ttu-id="f7600-167">Pour plus d’informations sur l’utilisation de ces enregistré des modèles, [prise en main des modèles privés sur hello portail Azure](../marketplace-consumer/mytemplates-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="f7600-167">For more information about working with these saved templates, [Get started with private templates on hello Azure portal](../marketplace-consumer/mytemplates-getstarted.md).</span></span>

1. <span data-ttu-id="f7600-168">sélectionner de vos modèles enregistrés, toofind **Parcourir** > **modèles**.</span><span class="sxs-lookup"><span data-stu-id="f7600-168">toofind your saved templates, select **Browse** > **Templates**.</span></span>
   
    ![parcourir les modèles](./media/resource-group-template-deploy-portal/browse-templates.png)
2. <span data-ttu-id="f7600-170">Dans liste de hello des modèles enregistrés tooyour compte, sélectionnez hello celui que vous souhaitez toowork sur.</span><span class="sxs-lookup"><span data-stu-id="f7600-170">From hello list of templates saved tooyour account, select hello one you wish toowork on.</span></span>
   
    ![modèles enregistrés](./media/resource-group-template-deploy-portal/saved-templates.png)
3. <span data-ttu-id="f7600-172">Sélectionnez **déployer** tooredeploy que cela enregistré le modèle.</span><span class="sxs-lookup"><span data-stu-id="f7600-172">Select **Deploy** tooredeploy this saved template.</span></span>
   
    ![déployer un modèle enregistré](./media/resource-group-template-deploy-portal/deploy-saved-template.png)

## <a name="next-steps"></a><span data-ttu-id="f7600-174">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f7600-174">Next steps</span></span>
* <span data-ttu-id="f7600-175">les journaux d’audit de tooview, consultez [auditer les opérations effectuées avec le Gestionnaire de ressources](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="f7600-175">tooview audit logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="f7600-176">tootroubleshoot des erreurs de déploiement, consultez [afficher les opérations de déploiement](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="f7600-176">tootroubleshoot deployment errors, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="f7600-177">tooretrieve un modèle à partir d’un déploiement ou d’un groupe de ressources, consultez [modèle exporter Azure Resource Manager à partir de ressources existants](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="f7600-177">tooretrieve a template from a deployment or resource group, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="f7600-178">Pour obtenir des conseils comment les entreprises peuvent utiliser le Gestionnaire de ressources tooeffectively gérer les abonnements, consultez [une vue de structure Azure enterprise - gouvernance de l’abonnement normative](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="f7600-178">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

