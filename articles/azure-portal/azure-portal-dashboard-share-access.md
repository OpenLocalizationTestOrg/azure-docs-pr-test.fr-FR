---
title: "aaaShare Azure portail tableaux de bord à l’aide de RBAC | Documents Microsoft"
description: "Cet article explique comment tooshare un tableau de bord dans hello portail Azure à l’aide du contrôle d’accès en fonction du rôle."
services: azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 8908a6ce-ae0c-4f60-a0c9-b3acfe823365
ms.service: multiple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2016
ms.author: tomfitz
ms.openlocfilehash: b12f9f8582596ee14aa8bfdfb4772cc139e3bf45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="share-azure-dashboards-by-using-role-based-access-control"></a><span data-ttu-id="06142-103">Partager des tableaux de bord Azure à l’aide du contrôle d’accès en fonction du rôle</span><span class="sxs-lookup"><span data-stu-id="06142-103">Share Azure dashboards by using Role-Based Access Control</span></span>
<span data-ttu-id="06142-104">Après avoir configuré un tableau de bord, vous pouvez le publier et le partager avec d’autres utilisateurs de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="06142-104">After configuring a dashboard, you can publish it and share it with other users in your organization.</span></span> <span data-ttu-id="06142-105">Vous permettre d’autres tooview votre tableau de bord à l’aide d’Azure [Role-Based Access Control](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="06142-105">You allow others tooview your dashboard by using Azure [Role-Based Access Control](../active-directory/role-based-access-control-configure.md).</span></span> <span data-ttu-id="06142-106">Vous affectez un utilisateur ou un groupe de rôle tooa d’utilisateurs, et ce rôle définit si les utilisateurs peuvent afficher ou modifier le tableau de bord publié hello.</span><span class="sxs-lookup"><span data-stu-id="06142-106">You assign a user or group of users tooa role, and that role defines whether those users can view or modify hello published dashboard.</span></span> 

<span data-ttu-id="06142-107">Tous les tableaux de bord publiés sont implémentés en tant que ressources Azure, ce qui signifie qu’ils constituent des éléments gérables dans votre abonnement et qu’ils sont contenus dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="06142-107">All published dashboards are implemented as Azure resources, which means they exist as manageable items within your subscription and are contained in a resource group.</span></span>  <span data-ttu-id="06142-108">En termes de contrôle d’accès, les tableaux de bord sont traités de la même manière que les autres ressources, telles qu’une machine virtuelle ou un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="06142-108">From an access control perspective, dashboards are no different than other resources, such as a virtual machine or a storage account.</span></span>

> [!TIP]
> <span data-ttu-id="06142-109">Mosaïque individuelle sur le tableau de bord hello applique ses propres exigences de contrôle d’accès en fonction des ressources hello qu'elles s’affichent.</span><span class="sxs-lookup"><span data-stu-id="06142-109">Individual tiles on hello dashboard enforce their own access control requirements based on hello resources they display.</span></span>  <span data-ttu-id="06142-110">Par conséquent, vous pouvez concevoir un tableau de bord est partagé largement tout en protégeant les données hello sur les vignettes individuels.</span><span class="sxs-lookup"><span data-stu-id="06142-110">Therefore, you can design a dashboard that is shared broadly while still protecting hello data on individual tiles.</span></span>
> 
> 

## <a name="understanding-access-control-for-dashboards"></a><span data-ttu-id="06142-111">Présentation du contrôle d’accès relatif aux tableaux de bord</span><span class="sxs-lookup"><span data-stu-id="06142-111">Understanding access control for dashboards</span></span>
<span data-ttu-id="06142-112">Avec les contrôle de l’accès en fonction du rôle (RBAC), vous pouvez attribuer tooroles les utilisateurs à trois différents niveaux de portée :</span><span class="sxs-lookup"><span data-stu-id="06142-112">With Role-Based Access Control (RBAC), you can assign users tooroles at three different levels of scope:</span></span>

* <span data-ttu-id="06142-113">abonnement</span><span class="sxs-lookup"><span data-stu-id="06142-113">subscription</span></span>
* <span data-ttu-id="06142-114">resource group</span><span class="sxs-lookup"><span data-stu-id="06142-114">resource group</span></span>
* <span data-ttu-id="06142-115">resource</span><span class="sxs-lookup"><span data-stu-id="06142-115">resource</span></span>

<span data-ttu-id="06142-116">vous attribuez des autorisations Hello sont héritées d’abonnement vers le bas toohello ressource.</span><span class="sxs-lookup"><span data-stu-id="06142-116">hello permissions you assign are inherited from subscription down toohello resource.</span></span> <span data-ttu-id="06142-117">tableau de bord publié Hello est une ressource.</span><span class="sxs-lookup"><span data-stu-id="06142-117">hello published dashboard is a resource.</span></span> <span data-ttu-id="06142-118">Par conséquent, vous avez peut-être déjà tooroles utilisateurs affectés pour l’abonnement de hello qui fonctionnent également pour un tableau de bord publié hello.</span><span class="sxs-lookup"><span data-stu-id="06142-118">Therefore, you may already have users assigned tooroles for hello subscription which also work for hello published dashboard.</span></span> 

<span data-ttu-id="06142-119">Voici un exemple.</span><span class="sxs-lookup"><span data-stu-id="06142-119">Here is an example.</span></span>  <span data-ttu-id="06142-120">Supposons que vous avez un abonnement Azure et de différents membres de votre équipe ont été affectés des rôles de hello de **propriétaire**, **collaborateur**, ou **lecteur** pour l’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="06142-120">Let's say you have an Azure subscription and various members of your team have been assigned hello roles of **owner**, **contributor**, or **reader** for hello subscription.</span></span> <span data-ttu-id="06142-121">Les utilisateurs qui sont propriétaires ou collaborateurs sont en mesure de toolist, afficher, créer, modifier ou supprimer des tableaux de bord dans l’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="06142-121">Users who are owners or contributors are able toolist, view, create, modify, or delete dashboards within hello subscription.</span></span>  <span data-ttu-id="06142-122">Les utilisateurs qui sont des lecteurs sont en mesure de toolist et afficher des tableaux de bord, mais ne peut pas modifier ou les supprimer.</span><span class="sxs-lookup"><span data-stu-id="06142-122">Users who are readers are able toolist and view dashboards, but cannot modify or delete them.</span></span>  <span data-ttu-id="06142-123">Les utilisateurs avec accès en lecture sont en mesure de toomake modifications locales tooa tableau de bord publié (telles que, lors du dépannage d’un problème), mais est toopublish n’a pas pu ces server toohello arrière de modifications.</span><span class="sxs-lookup"><span data-stu-id="06142-123">Users with reader access are able toomake local edits tooa published dashboard (such as, when troubleshooting an issue), but are not able toopublish those changes back toohello server.</span></span>  <span data-ttu-id="06142-124">Ils auront hello option toomake une copie privée d’un tableau de bord hello pour eux-mêmes</span><span class="sxs-lookup"><span data-stu-id="06142-124">They will have hello option toomake a private copy of hello dashboard for themselves</span></span>

<span data-ttu-id="06142-125">Toutefois, vous pouvez également affecter autorisations toohello ressource groupe qui contient plusieurs tableaux de bord ou tableau de bord tooan individuels.</span><span class="sxs-lookup"><span data-stu-id="06142-125">However, you could also assign permissions toohello resource group that contains several dashboards or tooan individual dashboard.</span></span> <span data-ttu-id="06142-126">Par exemple, vous pouvez décider qu’un groupe d’utilisateurs doit-elle disposer d’autorisations limitées sur l’abonnement de hello mais supérieur accès tooa particulier du tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="06142-126">For example, you may decide that a group of users should have limited permissions across hello subscription but greater access tooa particular dashboard.</span></span> <span data-ttu-id="06142-127">Vous affectez ces rôle tooa d’utilisateurs pour ce tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="06142-127">You assign those users tooa role for that dashboard.</span></span> 

## <a name="publish-dashboard"></a><span data-ttu-id="06142-128">Publier un tableau de bord</span><span class="sxs-lookup"><span data-stu-id="06142-128">Publish dashboard</span></span>
<span data-ttu-id="06142-129">Supposons que vous avez terminé de configurer un tableau de bord que vous souhaitez tooshare avec un groupe d’utilisateurs dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="06142-129">Let's suppose you have finished configuring a dashboard that you want tooshare with a group of users in your subscription.</span></span> <span data-ttu-id="06142-130">étapes Hello ci-dessous représentent un groupe personnalisé appelé responsables du stockage, mais vous pouvez nommer votre groupe de ce que vous voulez.</span><span class="sxs-lookup"><span data-stu-id="06142-130">hello steps below depict a customized group called Storage Managers, but you can name your group whatever you would like.</span></span> <span data-ttu-id="06142-131">Pour plus d’informations sur la création d’un groupe Active Directory et l’ajout de groupe d’utilisateurs toothat, consultez [la gestion des groupes dans Azure Active Directory](../active-directory/active-directory-accessmanagement-manage-groups.md).</span><span class="sxs-lookup"><span data-stu-id="06142-131">For information about creating an Active Directory group and adding users toothat group, see [Managing groups in Azure Active Directory](../active-directory/active-directory-accessmanagement-manage-groups.md).</span></span>

1. <span data-ttu-id="06142-132">Dans le tableau de bord hello, sélectionnez **partage**.</span><span class="sxs-lookup"><span data-stu-id="06142-132">In hello dashboard, select **Share**.</span></span>
   
     ![sélectionner Partager](./media/azure-portal-dashboard-share-access/select-share.png)
2. <span data-ttu-id="06142-134">Avant d’attribuer l’accès, vous devez publier le tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="06142-134">Before assigning access, you must publish hello dashboard.</span></span> <span data-ttu-id="06142-135">Par défaut, tableau de bord hello sera publiée tooa groupe de ressources nommé **tableaux de bord**.</span><span class="sxs-lookup"><span data-stu-id="06142-135">By default, hello dashboard will be published tooa resource group named **dashboards**.</span></span> <span data-ttu-id="06142-136">Sélectionnez **Publier**.</span><span class="sxs-lookup"><span data-stu-id="06142-136">Select **Publish**.</span></span>
   
     ![Publier](./media/azure-portal-dashboard-share-access/publish.png)

<span data-ttu-id="06142-138">Votre tableau de bord est à présent publié.</span><span class="sxs-lookup"><span data-stu-id="06142-138">Your dashboard is now published.</span></span> <span data-ttu-id="06142-139">Si les autorisations de hello héritées de l’abonnement de hello sont appropriées, il est inutile toodo rien de plus.</span><span class="sxs-lookup"><span data-stu-id="06142-139">If hello permissions inherited from hello subscription are suitable, you do not need toodo anything more.</span></span> <span data-ttu-id="06142-140">Autres utilisateurs de votre organisation seront être en mesure de tooaccess et modifier le tableau de bord hello en fonction de leur rôle au niveau d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="06142-140">Other users in your organization will be able tooaccess and modify hello dashboard based on their subscription level role.</span></span> <span data-ttu-id="06142-141">Toutefois, pour ce didacticiel, nous allons assigner un groupe de rôle tooa d’utilisateurs pour ce tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="06142-141">However, for this tutorial, let's assign a group of users tooa role for that dashboard.</span></span>

## <a name="assign-access-tooa-dashboard"></a><span data-ttu-id="06142-142">Attribuer l’accès tooa tableau de bord</span><span class="sxs-lookup"><span data-stu-id="06142-142">Assign access tooa dashboard</span></span>
1. <span data-ttu-id="06142-143">Après la publication de tableau de bord hello, sélectionnez **gérer les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="06142-143">After publishing hello dashboard, select **Manage users**.</span></span>
   
     ![gérer des utilisateurs](./media/azure-portal-dashboard-share-access/manage-users.png)
2. <span data-ttu-id="06142-145">Vous obtenez une liste d’utilisateurs existants déjà dotés d’un rôle pour ce tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="06142-145">You will see a list of existing users that are already assigned a role for this dashboard.</span></span> <span data-ttu-id="06142-146">Votre liste d’utilisateurs existants sera différente de celle image hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="06142-146">Your list of existing users will be different than hello image below.</span></span> <span data-ttu-id="06142-147">Très probablement, les attributions de hello sont héritées d’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="06142-147">Most likely, hello assignments are inherited from hello subscription.</span></span> <span data-ttu-id="06142-148">tooadd un nouvel utilisateur ou groupe, sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="06142-148">tooadd a new user or group, select **Add**.</span></span>
   
     ![ajouter un utilisateur](./media/azure-portal-dashboard-share-access/existing-users.png)
3. <span data-ttu-id="06142-150">Sélectionnez rôle hello qui représente les autorisations hello toogrant voulue.</span><span class="sxs-lookup"><span data-stu-id="06142-150">Select hello role that represents hello permissions you would like toogrant.</span></span> <span data-ttu-id="06142-151">Dans cet exemple, sélectionnez **Contributeur**.</span><span class="sxs-lookup"><span data-stu-id="06142-151">For this example, select **Contributor**.</span></span>
   
     ![sélectionner un rôle](./media/azure-portal-dashboard-share-access/select-role.png)
4. <span data-ttu-id="06142-153">Sélectionnez l’utilisateur de hello ou un groupe que vous souhaitez tooassign toohello rôle.</span><span class="sxs-lookup"><span data-stu-id="06142-153">Select hello user or group that you wish tooassign toohello role.</span></span> <span data-ttu-id="06142-154">Si vous ne voyez pas l’utilisateur de hello ou un groupe que vous recherchez dans la liste de hello, utilisez la zone de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="06142-154">If you do not see hello user or group you are looking for in hello list, use hello search box.</span></span> <span data-ttu-id="06142-155">La liste des groupes disponibles dépendent des groupes hello que vous avez créé dans Active Directory.</span><span class="sxs-lookup"><span data-stu-id="06142-155">Your list of available groups will depend on hello groups you have created in your Active Directory.</span></span>
   
     ![sélectionner un utilisateur](./media/azure-portal-dashboard-share-access/select-user.png) 
5. <span data-ttu-id="06142-157">Lorsque vous avez terminé d’ajouter des utilisateurs ou des groupes, sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="06142-157">When you have finished adding users or groups, select **OK**.</span></span> 
6. <span data-ttu-id="06142-158">nouvelle attribution de Hello est ajoutée toohello la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="06142-158">hello new assignment is added toohello list of users.</span></span> <span data-ttu-id="06142-159">Notez que son **Accès** présente la valeur **Affecté** plutôt que la valeur **Hérité**.</span><span class="sxs-lookup"><span data-stu-id="06142-159">Notice that its **Access** is listed as **Assigned** rather than **Inherited**.</span></span>
   
     ![rôles affectés](./media/azure-portal-dashboard-share-access/assigned-roles.png)

## <a name="next-steps"></a><span data-ttu-id="06142-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="06142-161">Next steps</span></span>
* <span data-ttu-id="06142-162">Pour obtenir la liste des rôles, voir [RBAC : rôles intégrés](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="06142-162">For a list of roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="06142-163">toolearn sur la gestion des ressources, consultez [des ressources de gestion de Azure via le portail](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="06142-163">toolearn about managing resources, see [Manage Azure resources through portal](resource-group-portal.md).</span></span>
