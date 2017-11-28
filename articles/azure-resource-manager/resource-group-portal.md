---
title: aaaUse toomanage portail Azure ressources Azure | Documents Microsoft
description: "Utiliser le portail Azure et gérer les ressources Azure de toomanage vos ressources. Montre comment toowork avec des ressources toomonitor de tableaux de bord."
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
ms.openlocfilehash: 0c89a197a31c5b6dd03ba457cb4d1fdf9f6d00f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-resources-through-portal"></a><span data-ttu-id="99869-104">Gérer les ressources Azure sur le portail</span><span class="sxs-lookup"><span data-stu-id="99869-104">Manage Azure resources through portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="99869-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="99869-105">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="99869-106">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="99869-106">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="99869-107">Portail</span><span class="sxs-lookup"><span data-stu-id="99869-107">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="99869-108">API REST</span><span class="sxs-lookup"><span data-stu-id="99869-108">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="99869-109">Cette rubrique montre comment toouse hello [portail Azure](https://portal.azure.com) avec [Azure Resource Manager](resource-group-overview.md) toomanage vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="99869-109">This topic shows how toouse hello [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) toomanage your Azure resources.</span></span> <span data-ttu-id="99869-110">toolearn sur le déploiement de ressources via le portail de hello, consultez [déployer des ressources avec des modèles de gestionnaire de ressources et le portail Azure](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="99869-110">toolearn about deploying resources through hello portal, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>

<span data-ttu-id="99869-111">Actuellement, pas tous les services prend en charge le portail de hello ou Gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="99869-111">Currently, not every service supports hello portal or Resource Manager.</span></span> <span data-ttu-id="99869-112">Pour ces services, vous devez toouse hello [portail classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="99869-112">For those services, you need toouse hello [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="99869-113">Statut de hello de chaque service, consultez [graphique de la disponibilité de portail Azure](https://azure.microsoft.com/features/azure-portal/availability/).</span><span class="sxs-lookup"><span data-stu-id="99869-113">For hello status of each service, see [Azure portal availability chart](https://azure.microsoft.com/features/azure-portal/availability/).</span></span>

## <a name="manage-resource-groups"></a><span data-ttu-id="99869-114">Gérer des groupes de ressources</span><span class="sxs-lookup"><span data-stu-id="99869-114">Manage resource groups</span></span>

<span data-ttu-id="99869-115">Un groupe de ressources est un conteneur réunissant les ressources associées d’une solution Azure.</span><span class="sxs-lookup"><span data-stu-id="99869-115">A resource group is a container that holds related resources for an Azure solution.</span></span> <span data-ttu-id="99869-116">groupe de ressources Hello peut inclure toutes les ressources de hello pour les solutions hello, ou uniquement les ressources que vous souhaitez toomanage en tant que groupe.</span><span class="sxs-lookup"><span data-stu-id="99869-116">hello resource group can include all hello resources for hello solution, or only those resources that you want toomanage as a group.</span></span> <span data-ttu-id="99869-117">Vous décidez comment vous souhaitez que les ressources de tooallocate tooresource groupes en fonction de ce que hello plus logique pour votre organisation.</span><span class="sxs-lookup"><span data-stu-id="99869-117">You decide how you want tooallocate resources tooresource groups based on what makes hello most sense for your organization.</span></span> <span data-ttu-id="99869-118">En règle générale, ajouter des ressources qui partagent hello même cycle de vie toohello même ressource de groupe afin de pouvoir facilement déployer, mettre à jour et les supprimer en tant que groupe.</span><span class="sxs-lookup"><span data-stu-id="99869-118">Generally, add resources that share hello same lifecycle toohello same resource group so you can easily deploy, update, and delete them as a group.</span></span> 

<span data-ttu-id="99869-119">groupe de ressources Hello stocke les métadonnées sur les ressources de hello.</span><span class="sxs-lookup"><span data-stu-id="99869-119">hello resource group stores metadata about hello resources.</span></span> <span data-ttu-id="99869-120">Par conséquent, lorsque vous spécifiez un emplacement pour le groupe de ressources hello, vous spécifiez que les métadonnées de stockage.</span><span class="sxs-lookup"><span data-stu-id="99869-120">Therefore, when you specify a location for hello resource group, you are specifying where that metadata is stored.</span></span> <span data-ttu-id="99869-121">Pour des raisons de compatibilité, vous devrez peut-être tooensure que vos données sont stockées dans une région particulière.</span><span class="sxs-lookup"><span data-stu-id="99869-121">For compliance reasons, you may need tooensure that your data is stored in a particular region.</span></span>

1. <span data-ttu-id="99869-122">toosee tous les groupes de ressources de hello dans votre abonnement, sélectionnez **groupes de ressources**.</span><span class="sxs-lookup"><span data-stu-id="99869-122">toosee all hello resource groups in your subscription, select **Resource groups**.</span></span>
   
    ![parcourir les groupes de ressources](./media/resource-group-portal/browse-groups.png)
2. <span data-ttu-id="99869-124">toocreate un groupe de ressources vide, sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="99869-124">toocreate an empty resource group, select **Add**.</span></span>
   
    ![ajouter un groupe de ressources](./media/resource-group-portal/add-resource-group.png)
3. <span data-ttu-id="99869-126">Fournissez un nom et un emplacement pour le nouveau groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="99869-126">Provide a name and location for hello new resource group.</span></span> <span data-ttu-id="99869-127">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="99869-127">Select **Create**.</span></span>
   
    ![Créer un groupe de ressources](./media/resource-group-portal/create-empty-group.png)
4. <span data-ttu-id="99869-129">Vous devrez peut-être tooselect **Actualiser** groupe de ressources toosee hello récemment créé.</span><span class="sxs-lookup"><span data-stu-id="99869-129">You may need tooselect **Refresh** toosee hello recently created resource group.</span></span>
   
    ![actualiser un groupe de ressources](./media/resource-group-portal/refresh-resource-groups.png)
5. <span data-ttu-id="99869-131">toocustomize hello afficher les informations sur vos groupes de ressources, sélectionnez **colonnes**.</span><span class="sxs-lookup"><span data-stu-id="99869-131">toocustomize hello information displayed for your resource groups, select **Columns**.</span></span>
   
    ![personnaliser des colonnes](./media/resource-group-portal/select-columns.png)
6. <span data-ttu-id="99869-133">Sélectionnez hello colonnes tooadd, puis **mise à jour**.</span><span class="sxs-lookup"><span data-stu-id="99869-133">Select hello columns tooadd, and then select **Update**.</span></span>
   
    ![ajouter des colonnes](./media/resource-group-portal/add-columns.png)
7. <span data-ttu-id="99869-135">toolearn sur le déploiement de ressources tooyour nouveau groupe de ressources, consultez [déployer des ressources avec des modèles de gestionnaire de ressources et le portail Azure](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="99869-135">toolearn about deploying resources tooyour new resource group, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>
8. <span data-ttu-id="99869-136">Accès rapide tooa groupe de ressources, vous pouvez épingler tooyour du tableau de bord panneau hello.</span><span class="sxs-lookup"><span data-stu-id="99869-136">For quick access tooa resource group, you can pin hello blade tooyour dashboard.</span></span>
   
    ![épingler un groupe de ressources](./media/resource-group-portal/pin-group.png)
9. <span data-ttu-id="99869-138">tableau de bord Hello affiche le groupe de ressources hello et ses ressources.</span><span class="sxs-lookup"><span data-stu-id="99869-138">hello dashboard displays hello resource group and its resources.</span></span> <span data-ttu-id="99869-139">Vous pouvez sélectionner des groupes de ressources hello ou un de ses éléments de toohello toonavigate ressources.</span><span class="sxs-lookup"><span data-stu-id="99869-139">You can select either hello resource groups or any of its resources toonavigate toohello item.</span></span>
   
    ![épingler un groupe de ressources](./media/resource-group-portal/show-resource-group-dashboard.png)

## <a name="tag-resources"></a><span data-ttu-id="99869-141">Baliser des ressources</span><span class="sxs-lookup"><span data-stu-id="99869-141">Tag resources</span></span>
<span data-ttu-id="99869-142">Vous pouvez appliquer des balises tooresource groupes et ressources toologically organiser vos éléments multimédias.</span><span class="sxs-lookup"><span data-stu-id="99869-142">You can apply tags tooresource groups and resources toologically organize your assets.</span></span> <span data-ttu-id="99869-143">Pour plus d’informations sur l’utilisation des balises, consultez [à l’aide des balises tooorganize vos ressources Azure](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="99869-143">For information about working with tags, see [Using tags tooorganize your Azure resources](resource-group-using-tags.md).</span></span>

[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]

## <a name="monitor-resources"></a><span data-ttu-id="99869-144">Surveiller les ressources</span><span class="sxs-lookup"><span data-stu-id="99869-144">Monitor resources</span></span>
<span data-ttu-id="99869-145">Lorsque vous sélectionnez une ressource, le panneau des ressources hello présente graphiques par défaut et les tables pour l’analyse de ce type de ressource.</span><span class="sxs-lookup"><span data-stu-id="99869-145">When you select a resource, hello resource blade presents default graphs and tables for monitoring that resource type.</span></span>

1. <span data-ttu-id="99869-146">Sélectionnez un Bonjour ressource et notez **analyse** section.</span><span class="sxs-lookup"><span data-stu-id="99869-146">Select a resource and notice hello **Monitoring** section.</span></span> <span data-ttu-id="99869-147">Elle inclut des graphiques qui sont de type de ressource toohello pertinentes.</span><span class="sxs-lookup"><span data-stu-id="99869-147">It includes graphs that are relevant toohello resource type.</span></span> <span data-ttu-id="99869-148">Hello image suivante montre les données pour un compte de stockage de surveillance de la valeur par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="99869-148">hello following image shows hello default monitoring data for a storage account.</span></span>
   
    ![afficher la surveillance](./media/resource-group-portal/show-monitoring.png)
2. <span data-ttu-id="99869-150">Vous pouvez épingler une section du tableau de bord hello panneau tooyour en sélectionnant les points de suspension hello (...) au-dessus de la section de hello.</span><span class="sxs-lookup"><span data-stu-id="99869-150">You can pin a section of hello blade tooyour dashboard by selecting hello ellipsis (...) above hello section.</span></span> <span data-ttu-id="99869-151">Vous pouvez également personnaliser hello taille hello section dans le panneau de hello ou supprimez-le complètement.</span><span class="sxs-lookup"><span data-stu-id="99869-151">You can also customize hello size hello section in hello blade or remove it completely.</span></span> <span data-ttu-id="99869-152">Hello image suivante montre comment toopin, personnaliser ou supprimer hello du processeur et la section de mémoire.</span><span class="sxs-lookup"><span data-stu-id="99869-152">hello following image shows how toopin, customize, or remove hello CPU and Memory section.</span></span>
   
    ![épingler une section](./media/resource-group-portal/pin-cpu-section.png)
3. <span data-ttu-id="99869-154">Après épinglage de tableau de bord toohello hello section, vous verrez hello résumé sur le tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="99869-154">After pinning hello section toohello dashboard, you will see hello summary on hello dashboard.</span></span> <span data-ttu-id="99869-155">Et, sélectionnez-le immédiatement toomore des détails concernant hello.</span><span class="sxs-lookup"><span data-stu-id="99869-155">And, selecting it immediately takes you toomore details about hello data.</span></span>
   
    ![afficher le tableau de bord](./media/resource-group-portal/view-startboard.png)
4. <span data-ttu-id="99869-157">toocompletely personnaliser les surveiller via le portail de hello, accédez tooyour du tableau de bord par défaut, puis sélectionnez les données de salutation **nouveau tableau de bord**.</span><span class="sxs-lookup"><span data-stu-id="99869-157">toocompletely customize hello data you monitor through hello portal, navigate tooyour default dashboard, and select **New dashboard**.</span></span>
   
    ![dashboard](./media/resource-group-portal/dashboard.png)
5. <span data-ttu-id="99869-159">Donnez un nom à votre nouveau tableau de bord et faites glisser les mosaïques sur le tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="99869-159">Give your new dashboard a name and drag tiles onto hello dashboard.</span></span> <span data-ttu-id="99869-160">les vignettes de Hello sont filtrés par les différentes options.</span><span class="sxs-lookup"><span data-stu-id="99869-160">hello tiles are filtered by different options.</span></span>
   
    ![dashboard](./media/resource-group-portal/create-dashboard.png)
   
     <span data-ttu-id="99869-162">toolearn sur l’utilisation des tableaux de bord, consultez [de création et de partage de tableaux de bord Bonjour Azure portal](../azure-portal/azure-portal-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="99869-162">toolearn about working with dashboards, see [Creating and sharing dashboards in hello Azure portal](../azure-portal/azure-portal-dashboards.md).</span></span>

## <a name="manage-resources"></a><span data-ttu-id="99869-163">Gestion des ressources</span><span class="sxs-lookup"><span data-stu-id="99869-163">Manage resources</span></span>
<span data-ttu-id="99869-164">Dans le panneau hello pour une ressource, vous voyez les options hello pour la gestion des ressources de hello.</span><span class="sxs-lookup"><span data-stu-id="99869-164">In hello blade for a resource, you see hello options for managing hello resource.</span></span> <span data-ttu-id="99869-165">portail de Hello présente les options de gestion pour ce type de ressource spécifique.</span><span class="sxs-lookup"><span data-stu-id="99869-165">hello portal presents management options for that particular resource type.</span></span> <span data-ttu-id="99869-166">Vous consultez les commandes de gestion hello haut hello du panneau des ressources hello et sur le côté gauche de hello.</span><span class="sxs-lookup"><span data-stu-id="99869-166">You see hello management commands across hello top of hello resource blade and on hello left side.</span></span>

![Gestion des ressources](./media/resource-group-portal/manage-resources.png)

<span data-ttu-id="99869-168">À partir de ces options, vous pouvez effectuer des opérations telles que le démarrage et l’arrêt d’un ordinateur virtuel ou le reconfigurer les propriétés de hello de machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="99869-168">From these options, you can perform operations such as starting and stopping a virtual machine, or reconfiguring hello properties of hello virtual machine.</span></span>

## <a name="move-resources"></a><span data-ttu-id="99869-169">Déplacer des ressources</span><span class="sxs-lookup"><span data-stu-id="99869-169">Move resources</span></span>
<span data-ttu-id="99869-170">Si vous avez besoin de groupe de ressources toomove ressources tooanother ou un autre abonnement, consultez [déplacer le groupe de ressources toonew ressources ou d’un abonnement](resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="99869-170">If you need toomove resources tooanother resource group or another subscription, see [Move resources toonew resource group or subscription](resource-group-move-resources.md).</span></span>

## <a name="lock-resources"></a><span data-ttu-id="99869-171">Verrouiller des ressources</span><span class="sxs-lookup"><span data-stu-id="99869-171">Lock resources</span></span>
<span data-ttu-id="99869-172">Vous pouvez verrouiller un abonnement, le groupe de ressources ou la ressource tooprevent autres utilisateurs de votre organisation d’accidentellement supprimer ou modifier des ressources critiques.</span><span class="sxs-lookup"><span data-stu-id="99869-172">You can lock a subscription, resource group, or resource tooprevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="99869-173">Pour plus d’informations, consultez [Verrouiller des ressources avec Azure Resource Manager](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="99869-173">For more information, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="view-your-subscription-and-costs"></a><span data-ttu-id="99869-174">Afficher votre abonnement et vos coûts</span><span class="sxs-lookup"><span data-stu-id="99869-174">View your subscription and costs</span></span>
<span data-ttu-id="99869-175">Vous pouvez afficher plus d’informations sur votre abonnement et les coûts de multi-niveaux hello pour toutes vos ressources.</span><span class="sxs-lookup"><span data-stu-id="99869-175">You can view information about your subscription and hello rolled-up costs for all your resources.</span></span> <span data-ttu-id="99869-176">Sélectionnez **abonnements** et abonnement hello toosee.</span><span class="sxs-lookup"><span data-stu-id="99869-176">Select **Subscriptions** and hello subscription you want toosee.</span></span> <span data-ttu-id="99869-177">Vous pouvez uniquement avoir un abonnement tooselect.</span><span class="sxs-lookup"><span data-stu-id="99869-177">You might only have one subscription tooselect.</span></span>

![abonnement](./media/resource-group-portal/select-subscription.png)

<span data-ttu-id="99869-179">Dans le panneau d’abonnement hello, vous voyez un taux d’avancement.</span><span class="sxs-lookup"><span data-stu-id="99869-179">Within hello subscription blade, you see a burn rate.</span></span>

![taux d’avancement](./media/resource-group-portal/burn-rate.png)

<span data-ttu-id="99869-181">Ainsi qu’une répartition des coûts par type de ressource.</span><span class="sxs-lookup"><span data-stu-id="99869-181">And, a breakdown of costs by resource type.</span></span>

![coût des ressources](./media/resource-group-portal/cost-by-resource.png)

## <a name="export-template"></a><span data-ttu-id="99869-183">Exportation du modèle</span><span class="sxs-lookup"><span data-stu-id="99869-183">Export template</span></span>
<span data-ttu-id="99869-184">Après avoir configuré votre groupe de ressources, vous pouvez choisir modèle de gestionnaire de ressources tooview hello pour le groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="99869-184">After setting up your resource group, you may want tooview hello Resource Manager template for hello resource group.</span></span> <span data-ttu-id="99869-185">Exportation de modèle de hello offre deux avantages :</span><span class="sxs-lookup"><span data-stu-id="99869-185">Exporting hello template offers two benefits:</span></span>

1. <span data-ttu-id="99869-186">Vous pouvez automatiser facilement les futurs déploiements de solution de hello, car le modèle de hello contient une infrastructure complète hello tous les.</span><span class="sxs-lookup"><span data-stu-id="99869-186">You can easily automate future deployments of hello solution because hello template contains all hello complete infrastructure.</span></span>
2. <span data-ttu-id="99869-187">Vous pouvez vous familiariser avec la syntaxe de modèle en examinant hello Notation JSON (JavaScript Object) qui représente votre solution.</span><span class="sxs-lookup"><span data-stu-id="99869-187">You can become familiar with template syntax by looking at hello JavaScript Object Notation (JSON) that represents your solution.</span></span>

<span data-ttu-id="99869-188">Pour obtenir des instructions détaillées, voir [Exporter un modèle Azure Resource Manager à partir de ressources existantes](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="99869-188">For step-by-step guidance, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>

## <a name="delete-resource-group-or-resources"></a><span data-ttu-id="99869-189">Supprimer des ressources ou un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="99869-189">Delete resource group or resources</span></span>
<span data-ttu-id="99869-190">Suppression d’un groupe de ressources supprime toutes les ressources hello qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="99869-190">Deleting a resource group deletes all hello resources contained within it.</span></span> <span data-ttu-id="99869-191">Vous pouvez également supprimer des ressources individuelles d'un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="99869-191">You can also delete individual resources within a resource group.</span></span> <span data-ttu-id="99869-192">Vous souhaitez tooexercise attention lorsque vous supprimez un groupe de ressources, car il peut y avoir des ressources dans d’autres groupes de ressources sont tooit lié.</span><span class="sxs-lookup"><span data-stu-id="99869-192">You want tooexercise caution when you delete a resource group because there might be resources in other resource groups that are linked tooit.</span></span> <span data-ttu-id="99869-193">Le Gestionnaire de ressources ne supprime pas les ressources liées, mais ils ne peuvent pas fonctionner correctement sans les ressources hello attendu.</span><span class="sxs-lookup"><span data-stu-id="99869-193">Resource Manager does not delete linked resources, but they may not operate correctly without hello expected resources.</span></span>

![supprimer un groupe](./media/resource-group-portal/delete-group.png)

## <a name="next-steps"></a><span data-ttu-id="99869-195">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="99869-195">Next steps</span></span>
* <span data-ttu-id="99869-196">journaux d’activité tooview, consultez [auditer les opérations effectuées avec le Gestionnaire de ressources](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="99869-196">tooview activity logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="99869-197">tooview plus d’informations sur le déploiement, consultez [afficher les opérations de déploiement](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="99869-197">tooview details about a deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="99869-198">ressources toodeploy via le portail de hello, consultez [déployer des ressources avec des modèles de gestionnaire de ressources et le portail Azure](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="99869-198">toodeploy resources through hello portal, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>
* <span data-ttu-id="99869-199">toomanage accès tooresources, consultez [utiliser les ressources de rôle affectations toomanage accès tooyour abonnement Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="99869-199">toomanage access tooresources, see [Use role assignments toomanage access tooyour Azure subscription resources](../active-directory/role-based-access-control-configure.md).</span></span>
* <span data-ttu-id="99869-200">Pour obtenir des conseils comment les entreprises peuvent utiliser le Gestionnaire de ressources tooeffectively gérer les abonnements, consultez [une vue de structure Azure enterprise - gouvernance de l’abonnement normative](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="99869-200">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

