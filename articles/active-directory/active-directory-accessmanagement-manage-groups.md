---
title: Gestion de groupes dans Azure Active Directory | Microsoft Docs
description: "Découvrez comment créer et gérer des groupes pour gérer les utilisateurs d’Azure à l’aide d’Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d1f5451c-3807-423c-8bac-2822d27b893f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/24/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 2cc2b63312b331a19c61cd7b59a4cac78edf32e6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="managing-groups-in-azure-active-directory"></a><span data-ttu-id="50ee9-103">Gestion des groupes dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="50ee9-103">Managing groups in Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="50ee9-104">portail Azure</span><span class="sxs-lookup"><span data-stu-id="50ee9-104">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="50ee9-105">Portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="50ee9-105">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="50ee9-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="50ee9-106">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="50ee9-107">L’une des principales fonctionnalités de la gestion des utilisateurs Azure Active Directory (Azure AD) est la possibilité de créer des groupes d’utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="50ee9-107">One of the features of Azure Active Directory (Azure AD) user management is the ability to create groups of users.</span></span> <span data-ttu-id="50ee9-108">Un groupe vous permet d’effectuer différentes tâches de gestion, par exemple l’attribution de licences ou autorisations à plusieurs utilisateurs simultanément.</span><span class="sxs-lookup"><span data-stu-id="50ee9-108">You use a group to perform management tasks such as assigning licenses or permissions to a number of users at once.</span></span> <span data-ttu-id="50ee9-109">Vous pouvez également utiliser des groupes pour affecter des autorisations d’accès à</span><span class="sxs-lookup"><span data-stu-id="50ee9-109">You can also use groups to assign access permission to</span></span>

* <span data-ttu-id="50ee9-110">Ressources telles que des objets de l’annuaire</span><span class="sxs-lookup"><span data-stu-id="50ee9-110">Resources such as objects in the directory</span></span>
* <span data-ttu-id="50ee9-111">Il peut s’agir de ressources externes à l’annuaire, comme des applications SaaS, des services Azure, des sites SharePoint ou des ressources locales.</span><span class="sxs-lookup"><span data-stu-id="50ee9-111">Resources external to the directory such as SaaS applications, Azure services, SharePoint sites, or on-premises resources</span></span>

<span data-ttu-id="50ee9-112">En outre, le propriétaire d’une ressource peut également attribuer l’accès à une ressource à un groupe Azure AD appartenant à quelqu’un d’autre.</span><span class="sxs-lookup"><span data-stu-id="50ee9-112">In addition, a resource owner can also assign access to a resource to an Azure AD group owned by someone else.</span></span> <span data-ttu-id="50ee9-113">Cette attribution autorise les membres de ce groupe à accéder à la ressource.</span><span class="sxs-lookup"><span data-stu-id="50ee9-113">This assignment grants the members of that group access to the resource.</span></span> <span data-ttu-id="50ee9-114">De son côté, le propriétaire du groupe gère l’appartenance au groupe.</span><span class="sxs-lookup"><span data-stu-id="50ee9-114">Then, the owner of the group manages membership in the group.</span></span> <span data-ttu-id="50ee9-115">Le propriétaire de la ressource délègue au propriétaire du groupe l’autorisation d’affecter des utilisateurs à ses ressources.</span><span class="sxs-lookup"><span data-stu-id="50ee9-115">Effectively, the resource owner delegates to the owner of the group the permission to assign users to their resource.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="50ee9-116">Microsoft recommande de gérer Azure AD à l’aide du [Centre d’administration Azure AD](https://aad.portal.azure.com) dans le portail Azure au lieu d’utiliser le portail Azure classique référencé dans cet article.</span><span class="sxs-lookup"><span data-stu-id="50ee9-116">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> <span data-ttu-id="50ee9-117">Pour savoir comment gérer des groupes dans le centre d’administration Azure AD, consultez [Créer un groupe et ajouter des membres dans Azure Active Directory](active-directory-groups-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="50ee9-117">For how to manage groups in the Azure AD admin center, see [Create a group and add members in Azure Active Directory](active-directory-groups-create-azure-portal.md).</span></span>

## <a name="how-do-i-create-a-group"></a><span data-ttu-id="50ee9-118">Comment créer un groupe ?</span><span class="sxs-lookup"><span data-stu-id="50ee9-118">How do I create a group?</span></span>
<span data-ttu-id="50ee9-119">Selon les services auxquels votre organisation s’est abonnée, vous pouvez créer un groupe à l’aide de l’un des portails suivants :</span><span class="sxs-lookup"><span data-stu-id="50ee9-119">Depending on the services to which your organization has subscribed, you can create a group using one of the following:</span></span>

* <span data-ttu-id="50ee9-120">le Portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="50ee9-120">the Azure classic portal</span></span>
* <span data-ttu-id="50ee9-121">le portail des comptes Office 365</span><span class="sxs-lookup"><span data-stu-id="50ee9-121">the Office 365 account portal</span></span>
* <span data-ttu-id="50ee9-122">le portail des comptes Windows Intune</span><span class="sxs-lookup"><span data-stu-id="50ee9-122">the Windows Intune account portal</span></span>

<span data-ttu-id="50ee9-123">Nous décrivons ici les tâches effectuées dans le Portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="50ee9-123">We'll describe tasks as performed in the Azure classic portal.</span></span> <span data-ttu-id="50ee9-124">Pour plus d’informations sur l’utilisation des portails non Azure pour gérer Azure Active Directory, consultez [Administration de votre annuaire Azure AD](active-directory-administer.md).</span><span class="sxs-lookup"><span data-stu-id="50ee9-124">For more information about using non-Azure portals to manage your Azure AD directory, see [Administering your Azure AD directory](active-directory-administer.md).</span></span>

1. <span data-ttu-id="50ee9-125">Dans le [Portail Azure Classic](https://manage.windowsazure.com), sélectionnez **Active Directory**, puis le nom de l’annuaire de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="50ee9-125">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select the name of the directory for your organization.</span></span>
2. <span data-ttu-id="50ee9-126">Sélectionnez l’onglet **Groupes** .</span><span class="sxs-lookup"><span data-stu-id="50ee9-126">Select the **Groups** tab.</span></span>
3. <span data-ttu-id="50ee9-127">Sélectionnez **Ajouter un groupe**.</span><span class="sxs-lookup"><span data-stu-id="50ee9-127">Select **Add Group**.</span></span>
4. <span data-ttu-id="50ee9-128">Dans la fenêtre **Ajouter un groupe** , spécifiez le nom et la description d’un groupe.</span><span class="sxs-lookup"><span data-stu-id="50ee9-128">In the **Add Group** window, specify the name and the description of a group.</span></span>

## <a name="how-do-i-add-or-remove-individual-users-in-a-security-group"></a><span data-ttu-id="50ee9-129">Comment ajouter ou supprimer des utilisateurs individuels dans un groupe de sécurité ?</span><span class="sxs-lookup"><span data-stu-id="50ee9-129">How do I add or remove individual users in a security group?</span></span>
<span data-ttu-id="50ee9-130">**Pour ajouter un utilisateur individuel à un groupe**</span><span class="sxs-lookup"><span data-stu-id="50ee9-130">**To add an individual user to a group**</span></span>

1. <span data-ttu-id="50ee9-131">Dans le [Portail Azure Classic](https://manage.windowsazure.com), sélectionnez **Active Directory**, puis le nom de l’annuaire de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="50ee9-131">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select the name of the directory for your organization.</span></span>
2. <span data-ttu-id="50ee9-132">Sélectionnez l’onglet **Groupes** .</span><span class="sxs-lookup"><span data-stu-id="50ee9-132">Select the **Groups** tab.</span></span>
3. <span data-ttu-id="50ee9-133">Ouvrez le groupe auquel vous souhaitez ajouter des membres.</span><span class="sxs-lookup"><span data-stu-id="50ee9-133">Open the group to which you want to add members.</span></span> <span data-ttu-id="50ee9-134">Ouvrez l’onglet **Membres** du groupe sélectionné s’il n’est pas déjà affiché.</span><span class="sxs-lookup"><span data-stu-id="50ee9-134">Open the **Members** tab of the selected group if it not already displaying.</span></span>
4. <span data-ttu-id="50ee9-135">Sélectionnez **Ajouter des membres**.</span><span class="sxs-lookup"><span data-stu-id="50ee9-135">Select **Add Members**.</span></span>
5. <span data-ttu-id="50ee9-136">Dans la page **Ajouter des membres** , sélectionnez le nom de l’utilisateur ou du groupe à ajouter en tant que membre de ce groupe.</span><span class="sxs-lookup"><span data-stu-id="50ee9-136">On the **Add Members** page, select the name of the user or a group that you want to add as a member of this group.</span></span> <span data-ttu-id="50ee9-137">Vérifiez qu’il a été ajouté au volet **Sélectionné** .</span><span class="sxs-lookup"><span data-stu-id="50ee9-137">Make sure that this name is added to the **Selected** pane.</span></span>

<span data-ttu-id="50ee9-138">**Pour supprimer un utilisateur individuel d’un groupe**</span><span class="sxs-lookup"><span data-stu-id="50ee9-138">**To remove an individual user from a group**</span></span>

1. <span data-ttu-id="50ee9-139">Dans le [Portail Azure Classic](https://manage.windowsazure.com), sélectionnez **Active Directory**, puis le nom de l’annuaire de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="50ee9-139">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select the name of the directory for your organization.</span></span>
2. <span data-ttu-id="50ee9-140">Sélectionnez l’onglet **Groupes** .</span><span class="sxs-lookup"><span data-stu-id="50ee9-140">Select the **Groups** tab.</span></span>
3. <span data-ttu-id="50ee9-141">Ouvrez le groupe duquel vous souhaitez supprimer des membres.</span><span class="sxs-lookup"><span data-stu-id="50ee9-141">Open the group from which you want to remove members.</span></span>
4. <span data-ttu-id="50ee9-142">Sélectionnez l’onglet **Membres**, puis le nom du membre à supprimer de ce groupe, et enfin **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="50ee9-142">Select the **Members** tab, select the name of the member that you want to remove from this group, and then click **Remove**.</span></span>
5. <span data-ttu-id="50ee9-143">À l’invite, confirmez que vous souhaitez supprimer ce membre du groupe.</span><span class="sxs-lookup"><span data-stu-id="50ee9-143">Confirm at the prompt that you want to remove this member from the group.</span></span>

## <a name="how-can-i-manage-the-membership-of-a-group-dynamically"></a><span data-ttu-id="50ee9-144">Comment puis-je gérer dynamiquement l’appartenance à un groupe ?</span><span class="sxs-lookup"><span data-stu-id="50ee9-144">How can I manage the membership of a group dynamically?</span></span>
<span data-ttu-id="50ee9-145">Dans Azure AD, vous pouvez très facilement définir une règle simple pour déterminer les utilisateurs qui sont membres du groupe.</span><span class="sxs-lookup"><span data-stu-id="50ee9-145">In Azure AD, you can very easily set up a simple rule to determine which users are to be members of the group.</span></span> <span data-ttu-id="50ee9-146">Une règle simple est une règle qui ne fait qu’une seule comparaison.</span><span class="sxs-lookup"><span data-stu-id="50ee9-146">A simple rule is one that makes only a single comparison.</span></span> <span data-ttu-id="50ee9-147">Par exemple, si un groupe est affecté à une application SaaS, vous pouvez définir une règle pour ajouter des utilisateurs ayant la fonction « Représentant ».</span><span class="sxs-lookup"><span data-stu-id="50ee9-147">For example, if a group is assigned to a SaaS application, you can set up a rule to add users who have a job title of "Sales Rep."</span></span> <span data-ttu-id="50ee9-148">Cette règle accorde ensuite l’accès à cette application SaaS à tous les utilisateurs ayant ce poste dans votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="50ee9-148">This rule then grants access to this SaaS application to all users with that job title in your directory.</span></span>

<span data-ttu-id="50ee9-149">Lorsqu’un attribut d’un utilisateur change, le système évalue toutes les règles de groupe dynamique d’un annuaire pour voir si la modification de l’attribut de l’utilisateur déclenche des ajouts ou suppressions de groupe.</span><span class="sxs-lookup"><span data-stu-id="50ee9-149">When any attributes of a user change, the system evaluates all dynamic group rules in a directory to see if the attribute change of the user would trigger any group adds or removes.</span></span> <span data-ttu-id="50ee9-150">Si un utilisateur respecte une règle d’un groupe, il est ajouté en tant que membre de ce groupe.</span><span class="sxs-lookup"><span data-stu-id="50ee9-150">If a user satisfies a rule on a group, they are added as a member to that group.</span></span> <span data-ttu-id="50ee9-151">S’il ne respecte plus la règle d’un groupe dont il est membre, il est supprimé de ce groupe.</span><span class="sxs-lookup"><span data-stu-id="50ee9-151">If they no longer satisfy the rule of a group they are a member of, they are removed as a members from that group.</span></span>

> [!NOTE]
> <span data-ttu-id="50ee9-152">Vous pouvez définir une règle d’appartenance dynamique sur les groupes de sécurité ou Office 365.</span><span class="sxs-lookup"><span data-stu-id="50ee9-152">You can set up a rule for dynamic membership on security groups or Office 365 groups.</span></span> <span data-ttu-id="50ee9-153">Les appartenances à des groupes imbriquées ne sont pas prises en charge pour l’affectation basée sur le groupe à des applications.</span><span class="sxs-lookup"><span data-stu-id="50ee9-153">Nested group memberships aren't currently supported for group-based assignment to applications.</span></span>
>
> <span data-ttu-id="50ee9-154">L’appartenance dynamique à des groupes nécessite qu’une licence Azure AD Premium soit affectée à</span><span class="sxs-lookup"><span data-stu-id="50ee9-154">Dynamic memberships for groups require an Azure AD Premium license to be assigned to</span></span>
>
> * <span data-ttu-id="50ee9-155">L’administrateur qui gère la règle sur un groupe</span><span class="sxs-lookup"><span data-stu-id="50ee9-155">The administrator who manages the rule on a group</span></span>
> * <span data-ttu-id="50ee9-156">Tous les membres du groupe</span><span class="sxs-lookup"><span data-stu-id="50ee9-156">All members of the group</span></span>
>
>

<span data-ttu-id="50ee9-157">**Pour activer l’appartenance dynamique pour un groupe**</span><span class="sxs-lookup"><span data-stu-id="50ee9-157">**To enable dynamic membership for a group**</span></span>

1. <span data-ttu-id="50ee9-158">Dans le [Portail Azure Classic](https://manage.windowsazure.com), sélectionnez **Active Directory**, puis le nom de l’annuaire de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="50ee9-158">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select the name of the directory for your organization.</span></span>
2. <span data-ttu-id="50ee9-159">Sélectionnez l’onglet **Groupes** , puis ouvrez le groupe que vous souhaitez modifier.</span><span class="sxs-lookup"><span data-stu-id="50ee9-159">Select the **Groups** tab, and open the group you want to edit.</span></span>
3. <span data-ttu-id="50ee9-160">Sélectionnez l’onglet **Configurer**, puis définissez **Activer les appartenances dynamiques** sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="50ee9-160">Select the **Configure** tab, and then set **Enable Dynamic Memberships** to **Yes**.</span></span>
4. <span data-ttu-id="50ee9-161">Définissez une seule règle simple pour le groupe, qui contrôle la manière dont l’appartenance dynamique fonctionne pour ce groupe.</span><span class="sxs-lookup"><span data-stu-id="50ee9-161">Set up a simple single rule for the group to control how dynamic membership for this group functions.</span></span> <span data-ttu-id="50ee9-162">Assurez-vous que l’option **Ajouter des utilisateurs où** est cochée, puis sélectionnez une propriété d’utilisateur dans la liste (par exemple, department, jobTitle, etc.).</span><span class="sxs-lookup"><span data-stu-id="50ee9-162">Make sure the **Add users where** option is selected, and then select a user property from the list (for example, department, jobTitle, etc.),</span></span>
5. <span data-ttu-id="50ee9-163">Ensuite, sélectionnez une condition (Non égal à, Égal à, Ne commence pas par, Commence par, Ne contient pas, Contient, Ne correspond pas, Correspond).</span><span class="sxs-lookup"><span data-stu-id="50ee9-163">Next, select a condition (Not Equals, Equals, Not Starts With, Starts With, Not Contains, Contains, Not Match, Match).</span></span>
6. <span data-ttu-id="50ee9-164">Spécifiez une valeur de comparaison pour la propriété d’utilisateur sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="50ee9-164">Specify a comparison value for the selected user property.</span></span>

<span data-ttu-id="50ee9-165">Pour en savoir plus sur la création de règles *avancées* (règles pouvant contenir plusieurs comparaisons) pour l’appartenance dynamique à un groupe, consultez la page [Utilisation d’attributs pour créer des règles avancées](active-directory-accessmanagement-groups-with-advanced-rules.md).</span><span class="sxs-lookup"><span data-stu-id="50ee9-165">To learn about how to create *advanced* rules (rules that can contain multiple comparisons) for dynamic group membership, see [Using attributes to create advanced rules](active-directory-accessmanagement-groups-with-advanced-rules.md).</span></span>

## <a name="additional-information"></a><span data-ttu-id="50ee9-166">Informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="50ee9-166">Additional information</span></span>
<span data-ttu-id="50ee9-167">Ces articles fournissent des informations supplémentaires sur Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="50ee9-167">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="50ee9-168">Gestion de l’accès aux ressources avec les groupes Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="50ee9-168">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="50ee9-169">Configuration des paramètres de groupe avec les applets de commande Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="50ee9-169">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="50ee9-170">Index d’articles pour la gestion des applications dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="50ee9-170">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="50ee9-171">Qu’est-ce qu’Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="50ee9-171">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="50ee9-172">Intégration des identités locales dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="50ee9-172">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
