---
title: "Apparence des applications dans le volet d’accès | Microsoft Docs"
description: "Identifier pourquoi une application apparaît dans le volet d’accès"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.reviewr: japere
ms.openlocfilehash: f8ccf2cf66b49940bc7f2b9f4764020efc04838e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="how-applications-appear-on-the-access-panel"></a><span data-ttu-id="08695-103">Apparence des applications dans le volet d’accès</span><span class="sxs-lookup"><span data-stu-id="08695-103">How applications appear on the access panel</span></span>

<span data-ttu-id="08695-104">Le volet d’accès est un portail Web qui permet à un utilisateur disposant d’un compte professionnel ou scolaire dans Azure Active Directory (Azure AD) d’afficher et de démarrer des applications basées sur le cloud auxquelles l’administrateur Azure AD lui a accordé un accès.</span><span class="sxs-lookup"><span data-stu-id="08695-104">The Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="08695-105">Ces applications sont configurées pour le compte de l’utilisateur dans le portail Azure AD.</span><span class="sxs-lookup"><span data-stu-id="08695-105">These applications are configured on behalf of the user in the Azure AD portal.</span></span> <span data-ttu-id="08695-106">L’administrateur peut fournir directement l’application à l’utilisateur ou à un groupe dont l’utilisateur fait partie, l’application apparaissant alors dans le volet d’accès de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="08695-106">The admin can provision the application to the user directly or to a group a user is part of resulting in the application appearing on the user’s Access Panel.</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="08695-107">Problèmes d’ordre général à vérifier en premier</span><span class="sxs-lookup"><span data-stu-id="08695-107">General issues to check first</span></span>

-   <span data-ttu-id="08695-108">Si une application vient d’être supprimée d’un utilisateur ou d’un groupe dont fait partie l’utilisateur, essayez de vous connecter / déconnecter de nouveau sur le volet d’accès de l’utilisateur après quelques minutes pour voir si l’application a été supprimée.</span><span class="sxs-lookup"><span data-stu-id="08695-108">If an application was just removed from a user or group the user is a member of, try to sign in and out again into the user’s Access Panel after a few minutes to see if the application is removed.</span></span>

-   <span data-ttu-id="08695-109">Si une licence vient d’être supprimée pour un utilisateur ou un groupe dont l’utilisateur est membre, la prise en compte des modifications peut prendre du temps, en fonction de la taille et de la complexité du groupe.</span><span class="sxs-lookup"><span data-stu-id="08695-109">If a license was just removed from a user or group the user is a member of this may take a long time, depending on the size and complexity of the group for changes to be made.</span></span> <span data-ttu-id="08695-110">Prévoyez du temps supplémentaire avant de vous connecter au volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="08695-110">Allow for extra time before signing into the Access Panel.</span></span>

## <a name="problems-related-to-assigning-applications-to-users"></a><span data-ttu-id="08695-111">Problèmes liés à l’affectation des applications aux utilisateurs</span><span class="sxs-lookup"><span data-stu-id="08695-111">Problems related to assigning applications to users</span></span>

<span data-ttu-id="08695-112">Un utilisateur peut voir une application sur son volet d’accès car il y a été affecté auparavant.</span><span class="sxs-lookup"><span data-stu-id="08695-112">A user may be seeing an application on their Access Panel because they had been previously assigned to it.</span></span> <span data-ttu-id="08695-113">Voici plusieurs méthodes pour vérifier :</span><span class="sxs-lookup"><span data-stu-id="08695-113">Below are some ways to check:</span></span>

-   [<span data-ttu-id="08695-114">Vérifier si un utilisateur est affecté à l’application</span><span class="sxs-lookup"><span data-stu-id="08695-114">Check if a user is assigned to the application</span></span>](#check-if-a-user-is-assigned-to-the-application)

-   [<span data-ttu-id="08695-115">Vérifier si un utilisateur est affecté à une licence liée à l’application</span><span class="sxs-lookup"><span data-stu-id="08695-115">Check if a user is under a license related to the application</span></span>](#check-if-a-user-is-under-a-license-related-to-the-application)


### <a name="check-if-a-user-is-assigned-to-the-application"></a><span data-ttu-id="08695-116">Vérifier si un utilisateur est affecté à l’application</span><span class="sxs-lookup"><span data-stu-id="08695-116">Check if a user is assigned to the application</span></span>

<span data-ttu-id="08695-117">Pour vérifier si un utilisateur est affecté à l’application, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="08695-117">To check if a user is assigned to the application, follow the steps below:</span></span>

1.  <span data-ttu-id="08695-118">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général.**</span><span class="sxs-lookup"><span data-stu-id="08695-118">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="08695-119">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="08695-119">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="08695-120">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="08695-120">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="08695-121">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="08695-121">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="08695-122">Cliquez sur **Toutes les applications** pour afficher la liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="08695-122">click **All Applications** to view a list of all your applications.</span></span>

6.  <span data-ttu-id="08695-123">**Recherchez** le nom de l’application en question.</span><span class="sxs-lookup"><span data-stu-id="08695-123">**Search** for the name of the application in question.</span></span>

7.  <span data-ttu-id="08695-124">Sélectionnez **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="08695-124">click **Users and groups**.</span></span>

8.  <span data-ttu-id="08695-125">Vérifiez si votre utilisateur est affecté à l’application.</span><span class="sxs-lookup"><span data-stu-id="08695-125">Check to see if your user is assigned to the application.</span></span>

  * <span data-ttu-id="08695-126">Si vous souhaitez supprimer l’utilisateur de l’application, **cliquez sur la ligne** de l’utilisateur et sélectionnez **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="08695-126">If you want to remove the user from the application, **click the row** of the user and select **delete**.</span></span>

### <a name="check-if-a-user-is-under-a-license-related-to-the-application"></a><span data-ttu-id="08695-127">Vérifier si un utilisateur est affecté à une licence liée à l’application</span><span class="sxs-lookup"><span data-stu-id="08695-127">Check if a user is under a license related to the application</span></span>

<span data-ttu-id="08695-128">Pour vérifier les licences affectées à un utilisateur, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="08695-128">To check a user’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="08695-129">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général.**</span><span class="sxs-lookup"><span data-stu-id="08695-129">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="08695-130">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="08695-130">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="08695-131">Tapez « **Azure Active Directory** » dans la zone de recherche du filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="08695-131">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="08695-132">Cliquez sur **Utilisateurs et groupes** dans le menu de navigation.</span><span class="sxs-lookup"><span data-stu-id="08695-132">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="08695-133">Cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="08695-133">click **All users**.</span></span>

6.  <span data-ttu-id="08695-134">**Recherchez** l’utilisateur qui vous intéresse et **cliquez sur la ligne** pour le sélectionner.</span><span class="sxs-lookup"><span data-stu-id="08695-134">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="08695-135">Cliquez sur **Licences** pour voir quelles licences sont actuellement affectées à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="08695-135">click **Licenses** to see which licenses the user currently has assigned.</span></span>

   * <span data-ttu-id="08695-136">Si l’utilisateur est affecté à une licence Office, les applications Office internes apparaîtront dans le volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="08695-136">If the user is assigned to an Office license this enable First Party Office applications to appear on the user’s Access Panel.</span></span>

## <a name="problems-related-to-assigning-applications-to-groups"></a><span data-ttu-id="08695-137">Problèmes liés à l’affectation des applications aux groupes</span><span class="sxs-lookup"><span data-stu-id="08695-137">Problems related to assigning applications to groups</span></span>

<span data-ttu-id="08695-138">Un utilisateur peut ne pas voir une application sur son volet d’accès, car il ne fait pas partie d’un groupe affecté à l’application.</span><span class="sxs-lookup"><span data-stu-id="08695-138">A user may be seeing an application on their Access Panel because they are part of a group that has been assigned the application.</span></span> <span data-ttu-id="08695-139">Voici plusieurs méthodes pour vérifier :</span><span class="sxs-lookup"><span data-stu-id="08695-139">Below are some ways to check:</span></span>

-   [<span data-ttu-id="08695-140">Vérifier les appartenances d’un utilisateur à des groupes</span><span class="sxs-lookup"><span data-stu-id="08695-140">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="08695-141">Vérifier si un utilisateur fait partie d’un groupe affecté à une licence</span><span class="sxs-lookup"><span data-stu-id="08695-141">Check if a user is a member of a group assigned to a license</span></span>](#check-if-a-user-is-a-member-of-a-group-assigned-to-a-license)

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="08695-142">Vérifier les appartenances d’un utilisateur à des groupes</span><span class="sxs-lookup"><span data-stu-id="08695-142">Check a user’s group memberships</span></span>

<span data-ttu-id="08695-143">Pour vérifier l’appartenance d’un utilisateur à un groupe, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="08695-143">To check a group’s membership, follow the steps below:</span></span>

1.  <span data-ttu-id="08695-144">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général.**</span><span class="sxs-lookup"><span data-stu-id="08695-144">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="08695-145">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="08695-145">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="08695-146">Tapez « **Azure Active Directory** » dans la zone de recherche du filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="08695-146">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="08695-147">Cliquez sur **Utilisateurs et groupes** dans le menu de navigation.</span><span class="sxs-lookup"><span data-stu-id="08695-147">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="08695-148">Cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="08695-148">click **All users**.</span></span>

6.  <span data-ttu-id="08695-149">**Recherchez** l’utilisateur qui vous intéresse et **cliquez sur la ligne** pour le sélectionner.</span><span class="sxs-lookup"><span data-stu-id="08695-149">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="08695-150">Cliquez sur **Groupes.**</span><span class="sxs-lookup"><span data-stu-id="08695-150">click **Groups.**</span></span>

8.  <span data-ttu-id="08695-151">Vérifiez si votre utilisateur fait partie d’un groupe affecté à l’application.</span><span class="sxs-lookup"><span data-stu-id="08695-151">Check to see if your user is part of a Group assigned to the application.</span></span>

   * <span data-ttu-id="08695-152">Si vous souhaitez supprimer l’utilisateur du groupe, **cliquez sur la ligne** du groupe et sélectionnez Supprimer.</span><span class="sxs-lookup"><span data-stu-id="08695-152">If you want to remove the user from the group, **click the row** of the group and select delete.</span></span>

### <a name="check-if-a-user-is-a-member-of-a-group-assigned-to-a-license"></a><span data-ttu-id="08695-153">Vérifier si un utilisateur fait partie d’un groupe affecté à une licence</span><span class="sxs-lookup"><span data-stu-id="08695-153">Check if a user is a member of a group assigned to a license</span></span>

1.  <span data-ttu-id="08695-154">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général.**</span><span class="sxs-lookup"><span data-stu-id="08695-154">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="08695-155">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="08695-155">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="08695-156">Tapez « **Azure Active Directory** » dans la zone de recherche du filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="08695-156">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="08695-157">Cliquez sur **Utilisateurs et groupes** dans le menu de navigation.</span><span class="sxs-lookup"><span data-stu-id="08695-157">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="08695-158">Cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="08695-158">click **All users**.</span></span>

6.  <span data-ttu-id="08695-159">**Recherchez** l’utilisateur qui vous intéresse et **cliquez sur la ligne** pour le sélectionner.</span><span class="sxs-lookup"><span data-stu-id="08695-159">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="08695-160">Cliquez sur **Groupes.**</span><span class="sxs-lookup"><span data-stu-id="08695-160">click **Groups.**</span></span>

8.  <span data-ttu-id="08695-161">Cliquez sur la ligne d’un groupe spécifique.</span><span class="sxs-lookup"><span data-stu-id="08695-161">click the row of a specific group.</span></span>

9.  <span data-ttu-id="08695-162">Cliquez sur **Licences** pour voir quelles licences sont affectées au groupe.</span><span class="sxs-lookup"><span data-stu-id="08695-162">click **Licenses** to see which licenses the group has assigned to it.</span></span>

  * <span data-ttu-id="08695-163">Si le groupe est affecté à une licence Office, certaines applications Office internes pourront apparaître dans le volet d’accès de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="08695-163">If the group is assigned to an Office license this may enable certain First Party Office applications to appear on the user’s Access Panel.</span></span>


## <a name="if-these-troubleshooting-steps-do-not-the-resolve-the-issue"></a><span data-ttu-id="08695-164">Si ces étapes de dépannage ne résolvent pas le problème</span><span class="sxs-lookup"><span data-stu-id="08695-164">If these troubleshooting steps do not the resolve the issue</span></span>

<span data-ttu-id="08695-165">Créez un ticket de support en fournissant les informations suivantes, si disponibles :</span><span class="sxs-lookup"><span data-stu-id="08695-165">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="08695-166">ID d’erreur de corrélation</span><span class="sxs-lookup"><span data-stu-id="08695-166">Correlation error ID</span></span>

-   <span data-ttu-id="08695-167">Nom d’utilisateur principal (adresse de messagerie de l’utilisateur)</span><span class="sxs-lookup"><span data-stu-id="08695-167">UPN (user email address)</span></span>

-   <span data-ttu-id="08695-168">ID client</span><span class="sxs-lookup"><span data-stu-id="08695-168">Tenant ID</span></span>

-   <span data-ttu-id="08695-169">Type de navigateur</span><span class="sxs-lookup"><span data-stu-id="08695-169">Browser type</span></span>

-   <span data-ttu-id="08695-170">Fuseau horaire et heure/période à laquelle l’erreur se produit</span><span class="sxs-lookup"><span data-stu-id="08695-170">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="08695-171">Traces Fiddler</span><span class="sxs-lookup"><span data-stu-id="08695-171">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="08695-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="08695-172">Next steps</span></span>
[<span data-ttu-id="08695-173">Gestion des applications avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="08695-173">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
