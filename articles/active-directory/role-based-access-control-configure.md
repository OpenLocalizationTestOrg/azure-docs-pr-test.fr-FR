---
title: "Contrôle d’accès basé sur les aaaRole Bonjour portail Azure | Documents Microsoft"
description: "Prise en main de la gestion de l’accès en fonction du rôle hello Azure Portal de contrôle d’accès. Utiliser les ressources de rôle affectations tooassign autorisations tooyour."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 8078f366-a2c4-4fbb-a44b-fc39fd89df81
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/17/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: b87e00089b0fc93fb212b318330a6f22bfbf59e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-role-based-access-control-toomanage-access-tooyour-azure-subscription-resources"></a><span data-ttu-id="4e51d-104">Utiliser les ressources de contrôle d’accès en fonction du rôle toomanage accès tooyour abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="4e51d-104">Use Role-Based Access Control toomanage access tooyour Azure subscription resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4e51d-105">Gérer l’accès par utilisateur ou par groupe</span><span class="sxs-lookup"><span data-stu-id="4e51d-105">Manage access by user or group</span></span>](role-based-access-control-manage-assignments.md)
> * [<span data-ttu-id="4e51d-106">Gérer l’accès par ressource</span><span class="sxs-lookup"><span data-stu-id="4e51d-106">Manage access by resource</span></span>](role-based-access-control-configure.md)

<span data-ttu-id="4e51d-107">Le contrôle d’accès en fonction du rôle (RBAC) Azure permet une gestion précise de l’accès pour Azure.</span><span class="sxs-lookup"><span data-stu-id="4e51d-107">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure.</span></span> <span data-ttu-id="4e51d-108">À l’aide de RBAC, vous pouvez accorder uniquement les quantité hello d’accès que les utilisateurs doivent tooperform leur travail.</span><span class="sxs-lookup"><span data-stu-id="4e51d-108">Using RBAC, you can grant only hello amount of access that users need tooperform their jobs.</span></span> <span data-ttu-id="4e51d-109">Cet article vous aidera à obtenir en cours d’exécution avec RBAC Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="4e51d-109">This article helps you get up and running with RBAC in hello Azure portal.</span></span> <span data-ttu-id="4e51d-110">Si vous souhaitez plus d’informations sur la gestion des droits d’accès avec RBAC, consultez [Prise en main de la gestion des accès dans le portail Azure](role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="4e51d-110">If you want more details about how RBAC helps you manage access, see [What is Role-Based Access Control](role-based-access-control-what-is.md).</span></span>

<span data-ttu-id="4e51d-111">Dans chaque abonnement, vous pouvez accorder des attributions de rôles too2000.</span><span class="sxs-lookup"><span data-stu-id="4e51d-111">Within each subscription, you can grant up too2000 role assignments.</span></span> 

## <a name="view-access"></a><span data-ttu-id="4e51d-112">Voir l’accès</span><span class="sxs-lookup"><span data-stu-id="4e51d-112">View access</span></span>
<span data-ttu-id="4e51d-113">Vous pouvez voir qui a accès tooa ressource, un groupe de ressources ou abonnement depuis son panneau principal Bonjour [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4e51d-113">You can see who has access tooa resource, resource group, or subscription from its main blade in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4e51d-114">Par exemple, nous souhaitons toosee ayant tooone accès notre des groupes de ressources :</span><span class="sxs-lookup"><span data-stu-id="4e51d-114">For example, we want toosee who has access tooone of our resource groups:</span></span>

1. <span data-ttu-id="4e51d-115">Sélectionnez **groupes de ressources** dans la barre de navigation hello sur hello gauche.</span><span class="sxs-lookup"><span data-stu-id="4e51d-115">Select **Resource groups** in hello navigation bar on hello left.</span></span>  
    <span data-ttu-id="4e51d-116">![Groupes de ressources - icône](./media/role-based-access-control-configure/resourcegroups_icon.png)</span><span class="sxs-lookup"><span data-stu-id="4e51d-116">![Resource groups - icon](./media/role-based-access-control-configure/resourcegroups_icon.png)</span></span>
2. <span data-ttu-id="4e51d-117">Nom hello sélectionnez hello du groupe de ressources à partir de hello **groupes de ressources** panneau.</span><span class="sxs-lookup"><span data-stu-id="4e51d-117">Select hello name of hello resource group from hello **Resource groups** blade.</span></span>
3. <span data-ttu-id="4e51d-118">Sélectionnez **(IAM) de contrôle d’accès** à partir du menu de gauche hello.</span><span class="sxs-lookup"><span data-stu-id="4e51d-118">Select **Access control (IAM)** from hello left menu.</span></span>  
4. <span data-ttu-id="4e51d-119">Panneau de contrôle d’accès Hello répertorie tous les utilisateurs, les groupes et les applications qui ont été accordées à groupe de ressources toohello accès.</span><span class="sxs-lookup"><span data-stu-id="4e51d-119">hello Access control blade lists all users, groups, and applications that have been granted access toohello resource group.</span></span>  
   
    ![Panneau Utilisateurs - comparaison Accès hérité et accès affecté (capture d’écran)](./media/role-based-access-control-configure/view-access.png)

<span data-ttu-id="4e51d-121">Notez que certains rôles sont trop limitées**cette ressource** tandis que d’autres sont **Inherited** à partir d’une autre étendue.</span><span class="sxs-lookup"><span data-stu-id="4e51d-121">Notice that some roles are scoped too**This resource** while others are **Inherited** it from another scope.</span></span> <span data-ttu-id="4e51d-122">L’accès est attribué spécifiquement le groupe de ressources toohello ou hérité d’un abonnement de parent toohello affectation.</span><span class="sxs-lookup"><span data-stu-id="4e51d-122">Access is either assigned specifically toohello resource group or inherited from an assignment toohello parent subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="4e51d-123">Les administrateurs d’abonnements classique et coadministrateurs sont considérés comme des propriétaires d’abonnement de hello dans le nouveau modèle RBAC hello.</span><span class="sxs-lookup"><span data-stu-id="4e51d-123">Classic subscription admins and co-admins are considered owners of hello subscription in hello new RBAC model.</span></span>

## <a name="add-access"></a><span data-ttu-id="4e51d-124">Ajout d’un accès</span><span class="sxs-lookup"><span data-stu-id="4e51d-124">Add Access</span></span>
<span data-ttu-id="4e51d-125">Vous accordez l’accès à partir de hello ressource, un groupe de ressources ou abonnement est étendue hello d’attribution de rôle hello.</span><span class="sxs-lookup"><span data-stu-id="4e51d-125">You grant access from within hello resource, resource group, or subscription that is hello scope of hello role assignment.</span></span>

1. <span data-ttu-id="4e51d-126">Sélectionnez **ajouter** sur le panneau de contrôle d’accès hello.</span><span class="sxs-lookup"><span data-stu-id="4e51d-126">Select **Add** on hello Access control blade.</span></span>  
2. <span data-ttu-id="4e51d-127">Rôle hello SELECT que vous souhaitez tooassign de hello **sélectionner un rôle** panneau.</span><span class="sxs-lookup"><span data-stu-id="4e51d-127">Select hello role that you wish tooassign from hello **Select a role** blade.</span></span>
3. <span data-ttu-id="4e51d-128">Sélectionnez hello utilisateur, groupe ou application dans le répertoire que vous souhaitez accéder toogrant à.</span><span class="sxs-lookup"><span data-stu-id="4e51d-128">Select hello user, group, or application in your directory that you wish toogrant access to.</span></span> <span data-ttu-id="4e51d-129">Vous pouvez rechercher le répertoire hello avec des noms complets, les adresses de messagerie et les identificateurs d’objet.</span><span class="sxs-lookup"><span data-stu-id="4e51d-129">You can search hello directory with display names, email addresses, and object identifiers.</span></span>  
   
    ![Panneau Ajouter des utilisateurs - rechercher (capture d’écran)](./media/role-based-access-control-configure/grant-access2.png)
4. <span data-ttu-id="4e51d-131">Sélectionnez **OK** toocreate l’attribution hello.</span><span class="sxs-lookup"><span data-stu-id="4e51d-131">Select **OK** toocreate hello assignment.</span></span> <span data-ttu-id="4e51d-132">Hello **Ajout utilisateur** popup hello de progression.</span><span class="sxs-lookup"><span data-stu-id="4e51d-132">hello **Adding user** popup tracks hello progress.</span></span>  
    <span data-ttu-id="4e51d-133">![Barre de progression Ajout d’utilisateur - capture d’écran](./media/role-based-access-control-configure/addinguser_popup.png)</span><span class="sxs-lookup"><span data-stu-id="4e51d-133">![Adding user progress bar - screenshot](./media/role-based-access-control-configure/addinguser_popup.png)</span></span>

<span data-ttu-id="4e51d-134">Après avoir ajouté avec succès une attribution de rôle, il apparaîtra sur hello **utilisateurs** panneau.</span><span class="sxs-lookup"><span data-stu-id="4e51d-134">After successfully adding a role assignment, it will appear on hello **Users** blade.</span></span>

## <a name="remove-access"></a><span data-ttu-id="4e51d-135">Supprimer un accès</span><span class="sxs-lookup"><span data-stu-id="4e51d-135">Remove Access</span></span>
1. <span data-ttu-id="4e51d-136">Pointez votre curseur sur nom hello d’assignation hello que vous souhaitez tooremove.</span><span class="sxs-lookup"><span data-stu-id="4e51d-136">Hover your cursor over hello name of hello assignment that you want tooremove.</span></span> <span data-ttu-id="4e51d-137">Une case à cocher s’affiche le nom de toohello suivant.</span><span class="sxs-lookup"><span data-stu-id="4e51d-137">A check box appears next toohello name.</span></span>
2. <span data-ttu-id="4e51d-138">Utilisez tooselect de cases à cocher hello une ou plusieurs attributions de rôle.</span><span class="sxs-lookup"><span data-stu-id="4e51d-138">Use hello check boxes tooselect one or more role assignments.</span></span>
2. <span data-ttu-id="4e51d-139">Sélectionnez **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="4e51d-139">Select **Remove**.</span></span>  
3. <span data-ttu-id="4e51d-140">Sélectionnez **Oui** la suppression de tooconfirm hello.</span><span class="sxs-lookup"><span data-stu-id="4e51d-140">Select **Yes** tooconfirm hello removal.</span></span>

<span data-ttu-id="4e51d-141">Les attributions héritées ne peuvent pas être supprimées.</span><span class="sxs-lookup"><span data-stu-id="4e51d-141">Inherited assignments cannot be removed.</span></span> <span data-ttu-id="4e51d-142">Si vous devez tooremove une affectation héritée, vous devez toodo à hello étendue où l’attribution de rôle hello a été créée.</span><span class="sxs-lookup"><span data-stu-id="4e51d-142">If you need tooremove an inherited assignment, you need toodo it at hello scope where hello role assignment was created.</span></span> <span data-ttu-id="4e51d-143">Bonjour **étendue** colonne, en regard trop**Inherited** il existe un lien qui vous toohello ressources où ce rôle a été attribué.</span><span class="sxs-lookup"><span data-stu-id="4e51d-143">In hello **Scope** column, next too**Inherited** there is a link that takes you toohello resources where this role was assigned.</span></span> <span data-ttu-id="4e51d-144">Accédez ressource toohello figure attribution de rôle tooremove hello.</span><span class="sxs-lookup"><span data-stu-id="4e51d-144">Go toohello resource listed there tooremove hello role assignment.</span></span>

![Panneau Utilisateurs - l’accès hérité désactive le bouton (capture d’écran)](./media/role-based-access-control-configure/remove-access2.png)

## <a name="other-tools-toomanage-access"></a><span data-ttu-id="4e51d-146">Accès toomanage des autres outils</span><span class="sxs-lookup"><span data-stu-id="4e51d-146">Other tools toomanage access</span></span>
<span data-ttu-id="4e51d-147">Vous pouvez attribuer des rôles et gérer l’accès avec les commandes Azure RBAC dans outils autres que hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="4e51d-147">You can assign roles and manage access with Azure RBAC commands in tools other than hello Azure portal.</span></span>  <span data-ttu-id="4e51d-148">Suivez les toolearn de liens hello plus d’informations sur les conditions préalables de hello et prise en main avec les commandes de Azure RBAC hello.</span><span class="sxs-lookup"><span data-stu-id="4e51d-148">Follow hello links toolearn more about hello prerequisites and get started with hello Azure RBAC commands.</span></span>

* [<span data-ttu-id="4e51d-149">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4e51d-149">Azure PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
* [<span data-ttu-id="4e51d-150">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="4e51d-150">Azure Command-Line Interface</span></span>](role-based-access-control-manage-access-azure-cli.md)
* [<span data-ttu-id="4e51d-151">API REST</span><span class="sxs-lookup"><span data-stu-id="4e51d-151">REST API</span></span>](role-based-access-control-manage-access-rest.md)

## <a name="next-steps"></a><span data-ttu-id="4e51d-152">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4e51d-152">Next Steps</span></span>
* [<span data-ttu-id="4e51d-153">Créer un rapport d’historique des modifications d’accès</span><span class="sxs-lookup"><span data-stu-id="4e51d-153">Create an access change history report</span></span>](role-based-access-control-access-change-history-report.md)
* <span data-ttu-id="4e51d-154">Consultez hello [rôles intégrés RBAC](role-based-access-built-in-roles.md)</span><span class="sxs-lookup"><span data-stu-id="4e51d-154">See hello [RBAC built-in roles](role-based-access-built-in-roles.md)</span></span>
* <span data-ttu-id="4e51d-155">Définissez vos propres [rôles personnalisés dans Azure RBAC](role-based-access-control-custom-roles.md)</span><span class="sxs-lookup"><span data-stu-id="4e51d-155">Define your own [Custom roles in Azure RBAC](role-based-access-control-custom-roles.md)</span></span>

