---
title: "Utiliser le portail Azure pour gérer des ressources Azure | Microsoft Docs"
description: "Utilisez le Portail Azure et Azure Resource Manager pour gérer vos ressources. Montre comment utiliser des tableaux de bord pour surveiller les ressources."
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 0725bbf2-5913-4c07-af6e-24e11d957fbc
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: 7a94fd5065de93384460e851627a9813d439956b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="manage-azure-resources-through-portal"></a><span data-ttu-id="5c48c-104">Gérer les ressources Azure sur le portail</span><span class="sxs-lookup"><span data-stu-id="5c48c-104">Manage Azure resources through portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5c48c-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5c48c-105">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="5c48c-106">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="5c48c-106">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="5c48c-107">Portail</span><span class="sxs-lookup"><span data-stu-id="5c48c-107">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="5c48c-108">API REST</span><span class="sxs-lookup"><span data-stu-id="5c48c-108">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="5c48c-109">Cette rubrique montre comment utiliser le [Portail Azure](https://portal.azure.com) avec [Azure Resource Manager](resource-group-overview.md) pour gérer vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="5c48c-109">This topic shows how to use the [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) to manage your Azure resources.</span></span> <span data-ttu-id="5c48c-110">Pour en savoir plus sur le déploiement des ressources avec le portail, voir [Déployer des ressources avec des modèles Resource Manager et le portail Azure](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5c48c-110">To learn about deploying resources through the portal, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>

<span data-ttu-id="5c48c-111">Actuellement, certains services ne prennent pas en charge le portail ou Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5c48c-111">Currently, not every service supports the portal or Resource Manager.</span></span> <span data-ttu-id="5c48c-112">Pour ces services, vous devez utiliser le [Portail Azure Classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="5c48c-112">For those services, you need to use the [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="5c48c-113">Pour connaître l’état de chaque service, voir [Graphique de la disponibilité du portail Azure](https://azure.microsoft.com/features/azure-portal/availability/).</span><span class="sxs-lookup"><span data-stu-id="5c48c-113">For the status of each service, see [Azure portal availability chart](https://azure.microsoft.com/features/azure-portal/availability/).</span></span>

## <a name="manage-resource-groups"></a><span data-ttu-id="5c48c-114">Gérer des groupes de ressources</span><span class="sxs-lookup"><span data-stu-id="5c48c-114">Manage resource groups</span></span>

<span data-ttu-id="5c48c-115">Un groupe de ressources est un conteneur réunissant les ressources associées d’une solution Azure.</span><span class="sxs-lookup"><span data-stu-id="5c48c-115">A resource group is a container that holds related resources for an Azure solution.</span></span> <span data-ttu-id="5c48c-116">Le groupe de ressources peut inclure toutes les ressources de la solution, ou uniquement celles que vous souhaitez gérer en tant que groupe.</span><span class="sxs-lookup"><span data-stu-id="5c48c-116">The resource group can include all the resources for the solution, or only those resources that you want to manage as a group.</span></span> <span data-ttu-id="5c48c-117">Pour déterminer comment allouer des ressources aux groupes de ressources, choisissez l’approche la plus pertinente pour votre organisation.</span><span class="sxs-lookup"><span data-stu-id="5c48c-117">You decide how you want to allocate resources to resource groups based on what makes the most sense for your organization.</span></span> <span data-ttu-id="5c48c-118">En règle générale, il convient d’ajouter des ressources qui partagent le même cycle de vie dans un même groupe de ressources afin de pouvoir facilement les déployer, les mettre à jour et les supprimer en tant que groupe.</span><span class="sxs-lookup"><span data-stu-id="5c48c-118">Generally, add resources that share the same lifecycle to the same resource group so you can easily deploy, update, and delete them as a group.</span></span> 

<span data-ttu-id="5c48c-119">Le groupe de ressources stocke des métadonnées sur les ressources.</span><span class="sxs-lookup"><span data-stu-id="5c48c-119">The resource group stores metadata about the resources.</span></span> <span data-ttu-id="5c48c-120">Par conséquent, lorsque vous spécifiez un emplacement pour le groupe de ressources, vous indiquez où stocker ces métadonnées.</span><span class="sxs-lookup"><span data-stu-id="5c48c-120">Therefore, when you specify a location for the resource group, you are specifying where that metadata is stored.</span></span> <span data-ttu-id="5c48c-121">Pour des raisons de conformité, vous devrez peut-être vous assurer que vos données sont stockées dans une région particulière.</span><span class="sxs-lookup"><span data-stu-id="5c48c-121">For compliance reasons, you may need to ensure that your data is stored in a particular region.</span></span>

1. <span data-ttu-id="5c48c-122">Pour afficher tous les groupes de ressources de votre abonnement, sélectionnez **Groupes de ressources**.</span><span class="sxs-lookup"><span data-stu-id="5c48c-122">To see all the resource groups in your subscription, select **Resource groups**.</span></span>
   
    ![parcourir les groupes de ressources](./media/resource-group-portal/browse-groups.png)
2. <span data-ttu-id="5c48c-124">Pour créer un groupe de ressources vide, sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="5c48c-124">To create an empty resource group, select **Add**.</span></span>
   
    ![ajouter un groupe de ressources](./media/resource-group-portal/add-resource-group.png)
3. <span data-ttu-id="5c48c-126">Fournissez un nom et un emplacement pour le nouveau groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="5c48c-126">Provide a name and location for the new resource group.</span></span> <span data-ttu-id="5c48c-127">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="5c48c-127">Select **Create**.</span></span>
   
    ![Créer un groupe de ressources](./media/resource-group-portal/create-empty-group.png)
4. <span data-ttu-id="5c48c-129">Vous pourrez avoir besoin de sélectionner **Actualiser** pour afficher le groupe de ressources que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="5c48c-129">You may need to select **Refresh** to see the recently created resource group.</span></span>
   
    ![actualiser un groupe de ressources](./media/resource-group-portal/refresh-resource-groups.png)
5. <span data-ttu-id="5c48c-131">Pour personnaliser les informations affichées pour vos groupes de ressources, sélectionnez **Colonnes**.</span><span class="sxs-lookup"><span data-stu-id="5c48c-131">To customize the information displayed for your resource groups, select **Columns**.</span></span>
   
    ![personnaliser des colonnes](./media/resource-group-portal/select-columns.png)
6. <span data-ttu-id="5c48c-133">Sélectionnez les colonnes à ajouter, puis sélectionnez **Mettre à jour**.</span><span class="sxs-lookup"><span data-stu-id="5c48c-133">Select the columns to add, and then select **Update**.</span></span>
   
    ![ajouter des colonnes](./media/resource-group-portal/add-columns.png)
7. <span data-ttu-id="5c48c-135">Pour plus d’informations sur le déploiement de ressources dans votre nouveau groupe de ressources, voir [Déployer des ressources à l’aide de modèles Resource Manager et du Portail Azure](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5c48c-135">To learn about deploying resources to your new resource group, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>
8. <span data-ttu-id="5c48c-136">Pour accéder rapidement à un groupe de ressources, vous pouvez épingler le panneau à votre tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="5c48c-136">For quick access to a resource group, you can pin the blade to your dashboard.</span></span>
   
    ![épingler un groupe de ressources](./media/resource-group-portal/pin-group.png)
9. <span data-ttu-id="5c48c-138">Le tableau de bord affiche le groupe de ressources et ses ressources.</span><span class="sxs-lookup"><span data-stu-id="5c48c-138">The dashboard displays the resource group and its resources.</span></span> <span data-ttu-id="5c48c-139">Vous pouvez sélectionner les groupes de ressources ou l’une de leurs ressources pour accéder à l’élément correspondant.</span><span class="sxs-lookup"><span data-stu-id="5c48c-139">You can select either the resource groups or any of its resources to navigate to the item.</span></span>
   
    ![épingler un groupe de ressources](./media/resource-group-portal/show-resource-group-dashboard.png)

## <a name="tag-resources"></a><span data-ttu-id="5c48c-141">Baliser des ressources</span><span class="sxs-lookup"><span data-stu-id="5c48c-141">Tag resources</span></span>
<span data-ttu-id="5c48c-142">Vous pouvez appliquer des balises à des groupes de ressources pour organiser logiquement vos ressources.</span><span class="sxs-lookup"><span data-stu-id="5c48c-142">You can apply tags to resource groups and resources to logically organize your assets.</span></span> <span data-ttu-id="5c48c-143">Pour plus d’informations sur l’utilisation des balises, voir [Organisation des ressources Azure à l’aide de balises](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="5c48c-143">For information about working with tags, see [Using tags to organize your Azure resources](resource-group-using-tags.md).</span></span>

[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]

## <a name="monitor-resources"></a><span data-ttu-id="5c48c-144">Surveiller les ressources</span><span class="sxs-lookup"><span data-stu-id="5c48c-144">Monitor resources</span></span>
<span data-ttu-id="5c48c-145">Lorsque vous sélectionnez une ressource, le panneau de ressources présente les graphiques et tables par défaut pour la surveillance de ce type de ressource.</span><span class="sxs-lookup"><span data-stu-id="5c48c-145">When you select a resource, the resource blade presents default graphs and tables for monitoring that resource type.</span></span>

1. <span data-ttu-id="5c48c-146">Sélectionnez une ressource, puis observez la section **Surveillance** .</span><span class="sxs-lookup"><span data-stu-id="5c48c-146">Select a resource and notice the **Monitoring** section.</span></span> <span data-ttu-id="5c48c-147">Elle contient des graphiques pertinents pour le type de ressource.</span><span class="sxs-lookup"><span data-stu-id="5c48c-147">It includes graphs that are relevant to the resource type.</span></span> <span data-ttu-id="5c48c-148">L’illustration suivante montre les données de surveillance par défaut pour un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="5c48c-148">The following image shows the default monitoring data for a storage account.</span></span>
   
    ![afficher la surveillance](./media/resource-group-portal/show-monitoring.png)
2. <span data-ttu-id="5c48c-150">Vous pouvez épingler une section du panneau à votre tableau de bord en sélectionnant les points de suspension (...) situés au-dessus de la section.</span><span class="sxs-lookup"><span data-stu-id="5c48c-150">You can pin a section of the blade to your dashboard by selecting the ellipsis (...) above the section.</span></span> <span data-ttu-id="5c48c-151">Vous pouvez aussi personnaliser la taille de la section dans le panneau ou supprimer complètement cette section.</span><span class="sxs-lookup"><span data-stu-id="5c48c-151">You can also customize the size the section in the blade or remove it completely.</span></span> <span data-ttu-id="5c48c-152">L’illustration suivante montre comment épingler, personnaliser ou supprimer la section Processeur et mémoire.</span><span class="sxs-lookup"><span data-stu-id="5c48c-152">The following image shows how to pin, customize, or remove the CPU and Memory section.</span></span>
   
    ![épingler une section](./media/resource-group-portal/pin-cpu-section.png)
3. <span data-ttu-id="5c48c-154">Après avoir épinglé la section au tableau de bord, vous obtenez le résumé sur le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="5c48c-154">After pinning the section to the dashboard, you will see the summary on the dashboard.</span></span> <span data-ttu-id="5c48c-155">Vous pouvez le sélectionner immédiatement pour obtenir plus de détails sur les données.</span><span class="sxs-lookup"><span data-stu-id="5c48c-155">And, selecting it immediately takes you to more details about the data.</span></span>
   
    ![afficher le tableau de bord](./media/resource-group-portal/view-startboard.png)
4. <span data-ttu-id="5c48c-157">Pour personnaliser entièrement les données que vous surveillez via le portail, accédez à votre tableau de bord par défaut, puis sélectionnez **Nouveau tableau de bord**.</span><span class="sxs-lookup"><span data-stu-id="5c48c-157">To completely customize the data you monitor through the portal, navigate to your default dashboard, and select **New dashboard**.</span></span>
   
    ![dashboard](./media/resource-group-portal/dashboard.png)
5. <span data-ttu-id="5c48c-159">Donnez un nom à votre tableau de bord et faites glisser les mosaïques dessus.</span><span class="sxs-lookup"><span data-stu-id="5c48c-159">Give your new dashboard a name and drag tiles onto the dashboard.</span></span> <span data-ttu-id="5c48c-160">Les mosaïques sont filtrées par différentes options.</span><span class="sxs-lookup"><span data-stu-id="5c48c-160">The tiles are filtered by different options.</span></span>
   
    ![dashboard](./media/resource-group-portal/create-dashboard.png)
   
     <span data-ttu-id="5c48c-162">Pour plus d’informations sur l’utilisation des tableaux de bord, consultez [Création et partage de tableaux de bord sur le Portail Azure](../azure-portal/azure-portal-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="5c48c-162">To learn about working with dashboards, see [Creating and sharing dashboards in the Azure portal](../azure-portal/azure-portal-dashboards.md).</span></span>

## <a name="manage-resources"></a><span data-ttu-id="5c48c-163">Gestion des ressources</span><span class="sxs-lookup"><span data-stu-id="5c48c-163">Manage resources</span></span>
<span data-ttu-id="5c48c-164">Le panneau d’une ressource montre les options de gestion de cette ressource.</span><span class="sxs-lookup"><span data-stu-id="5c48c-164">In the blade for a resource, you see the options for managing the resource.</span></span> <span data-ttu-id="5c48c-165">Le portail présente les options de gestion pour ce type de ressource particulier.</span><span class="sxs-lookup"><span data-stu-id="5c48c-165">The portal presents management options for that particular resource type.</span></span> <span data-ttu-id="5c48c-166">Les commandes de gestion se trouvent dans la partie supérieure et sur le côté gauche du panneau de la ressource.</span><span class="sxs-lookup"><span data-stu-id="5c48c-166">You see the management commands across the top of the resource blade and on the left side.</span></span>

![Gestion des ressources](./media/resource-group-portal/manage-resources.png)

<span data-ttu-id="5c48c-168">À partir de ces options, vous pouvez effectuer des opérations telles que le démarrage et l’arrêt d’une machine virtuelle, ou la reconfiguration des propriétés de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5c48c-168">From these options, you can perform operations such as starting and stopping a virtual machine, or reconfiguring the properties of the virtual machine.</span></span>

## <a name="move-resources"></a><span data-ttu-id="5c48c-169">Déplacer des ressources</span><span class="sxs-lookup"><span data-stu-id="5c48c-169">Move resources</span></span>
<span data-ttu-id="5c48c-170">Si vous souhaitez déplacer des ressources vers un autre groupe de ressources ou un autre abonnement, voir [Déplacer des ressources vers un nouveau groupe de ressources ou un nouvel abonnement](resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="5c48c-170">If you need to move resources to another resource group or another subscription, see [Move resources to new resource group or subscription](resource-group-move-resources.md).</span></span>

## <a name="lock-resources"></a><span data-ttu-id="5c48c-171">Verrouiller des ressources</span><span class="sxs-lookup"><span data-stu-id="5c48c-171">Lock resources</span></span>
<span data-ttu-id="5c48c-172">Vous pouvez verrouiller un abonnement, un groupe de ressources ou une ressource afin d’empêcher d’autres utilisateurs de votre organisation de supprimer ou modifier accidentellement des ressources cruciales.</span><span class="sxs-lookup"><span data-stu-id="5c48c-172">You can lock a subscription, resource group, or resource to prevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="5c48c-173">Pour plus d’informations, consultez [Verrouiller des ressources avec Azure Resource Manager](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="5c48c-173">For more information, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="view-your-subscription-and-costs"></a><span data-ttu-id="5c48c-174">Afficher votre abonnement et vos coûts</span><span class="sxs-lookup"><span data-stu-id="5c48c-174">View your subscription and costs</span></span>
<span data-ttu-id="5c48c-175">Vous pouvez afficher des informations sur votre abonnement et les coûts cumulés de toutes vos ressources.</span><span class="sxs-lookup"><span data-stu-id="5c48c-175">You can view information about your subscription and the rolled-up costs for all your resources.</span></span> <span data-ttu-id="5c48c-176">Sélectionnez **Abonnements** , puis l’abonnement de votre choix.</span><span class="sxs-lookup"><span data-stu-id="5c48c-176">Select **Subscriptions** and the subscription you want to see.</span></span> <span data-ttu-id="5c48c-177">Il se peut que vous n’ayez qu’un seul abonnement à sélectionner.</span><span class="sxs-lookup"><span data-stu-id="5c48c-177">You might only have one subscription to select.</span></span>

![abonnement](./media/resource-group-portal/select-subscription.png)

<span data-ttu-id="5c48c-179">Le panneau de l’abonnement vous présente un taux d’avancement.</span><span class="sxs-lookup"><span data-stu-id="5c48c-179">Within the subscription blade, you see a burn rate.</span></span>

![taux d’avancement](./media/resource-group-portal/burn-rate.png)

<span data-ttu-id="5c48c-181">Ainsi qu’une répartition des coûts par type de ressource.</span><span class="sxs-lookup"><span data-stu-id="5c48c-181">And, a breakdown of costs by resource type.</span></span>

![coût des ressources](./media/resource-group-portal/cost-by-resource.png)

## <a name="export-template"></a><span data-ttu-id="5c48c-183">Exportation du modèle</span><span class="sxs-lookup"><span data-stu-id="5c48c-183">Export template</span></span>
<span data-ttu-id="5c48c-184">Après avoir configuré votre groupe de ressources, vous pouvez éventuellement afficher le modèle Resource Manager pour le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="5c48c-184">After setting up your resource group, you may want to view the Resource Manager template for the resource group.</span></span> <span data-ttu-id="5c48c-185">L’exportation du modèle offre deux avantages :</span><span class="sxs-lookup"><span data-stu-id="5c48c-185">Exporting the template offers two benefits:</span></span>

1. <span data-ttu-id="5c48c-186">Vous pouvez facilement automatiser les futurs déploiements de la solution, car le modèle contient la totalité de l’infrastructure.</span><span class="sxs-lookup"><span data-stu-id="5c48c-186">You can easily automate future deployments of the solution because the template contains all the complete infrastructure.</span></span>
2. <span data-ttu-id="5c48c-187">Vous pouvez vous familiariser avec la syntaxe de modèle en regardant dans la JSON (JavaScript Object Notation) qui représente votre solution.</span><span class="sxs-lookup"><span data-stu-id="5c48c-187">You can become familiar with template syntax by looking at the JavaScript Object Notation (JSON) that represents your solution.</span></span>

<span data-ttu-id="5c48c-188">Pour obtenir des instructions détaillées, voir [Exporter un modèle Azure Resource Manager à partir de ressources existantes](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="5c48c-188">For step-by-step guidance, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>

## <a name="delete-resource-group-or-resources"></a><span data-ttu-id="5c48c-189">Supprimer des ressources ou un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="5c48c-189">Delete resource group or resources</span></span>
<span data-ttu-id="5c48c-190">La suppression d’un groupe de ressources supprime toutes les ressources qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="5c48c-190">Deleting a resource group deletes all the resources contained within it.</span></span> <span data-ttu-id="5c48c-191">Vous pouvez également supprimer des ressources individuelles d'un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="5c48c-191">You can also delete individual resources within a resource group.</span></span> <span data-ttu-id="5c48c-192">Faites preuve de prudence lorsque vous supprimez un groupe de ressources, car des ressources d’autres groupes de ressources peuvent y être liées.</span><span class="sxs-lookup"><span data-stu-id="5c48c-192">You want to exercise caution when you delete a resource group because there might be resources in other resource groups that are linked to it.</span></span> <span data-ttu-id="5c48c-193">Resource Manager ne supprime pas les ressources liées, mais ces dernières risquent de ne pas fonctionner correctement sans les ressources attendues.</span><span class="sxs-lookup"><span data-stu-id="5c48c-193">Resource Manager does not delete linked resources, but they may not operate correctly without the expected resources.</span></span>

![supprimer un groupe](./media/resource-group-portal/delete-group.png)

## <a name="next-steps"></a><span data-ttu-id="5c48c-195">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5c48c-195">Next steps</span></span>
* <span data-ttu-id="5c48c-196">Pour visualiser les journaux d’activité, consultez la rubrique [Opérations d’audit avec Resource Manager](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="5c48c-196">To view activity logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="5c48c-197">Pour plus d’informations sur le déploiement, consultez la page [Voir les opérations de déploiement](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="5c48c-197">To view details about a deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="5c48c-198">Pour déployer des ressources via le portail, voir [Déployer des ressources à l’aide de modèles Resource Manager et du Portail Azure](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5c48c-198">To deploy resources through the portal, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>
* <span data-ttu-id="5c48c-199">Pour gérer l’accès aux ressources, voir [Utiliser les attributions de rôle pour gérer l’accès à vos ressources d’abonnement Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="5c48c-199">To manage access to resources, see [Use role assignments to manage access to your Azure subscription resources](../active-directory/role-based-access-control-configure.md).</span></span>
* <span data-ttu-id="5c48c-200">Pour obtenir des conseils sur l’utilisation de Resource Manager par les entreprises pour gérer efficacement les abonnements, voir [Structure d’Azure Enterprise - Gouvernance normative de l’abonnement](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="5c48c-200">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

