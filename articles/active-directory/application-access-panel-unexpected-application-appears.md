---
title: "applications d’aaaHow apparaissent dans le volet d’accès hello | Documents Microsoft"
description: "Résoudre les problèmes de la raison pour laquelle une application s’affiche dans hello panneau d’accès"
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
ms.openlocfilehash: 14ee732c4ed5260cba878e949cf9d90877aee67e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-applications-appear-on-hello-access-panel"></a><span data-ttu-id="d1d3d-103">L’apparence des applications dans le volet d’accès hello</span><span class="sxs-lookup"><span data-stu-id="d1d3d-103">How applications appear on hello access panel</span></span>

<span data-ttu-id="d1d3d-104">Hello volet d’accès est un portail web qui permet à un utilisateur avec un travail ou compte scolaire dans Azure Active Directory (Azure AD) tooview et démarrer les applications cloud qui hello administrateur Azure AD lui a accordé l’accès à.</span><span class="sxs-lookup"><span data-stu-id="d1d3d-104">hello Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) tooview and start cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="d1d3d-105">Ces applications sont configurées pour le compte d’utilisateur hello dans le portail Azure AD de hello.</span><span class="sxs-lookup"><span data-stu-id="d1d3d-105">These applications are configured on behalf of hello user in hello Azure AD portal.</span></span> <span data-ttu-id="d1d3d-106">Hello admin peut configurer hello toohello utilisateur de l’application directement ou groupe tooa qu'un utilisateur fait partie du résultant dans une application hello figurant sur le panneau d’accès de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="d1d3d-106">hello admin can provision hello application toohello user directly or tooa group a user is part of resulting in hello application appearing on hello user’s Access Panel.</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="d1d3d-107">Général émet toocheck tout d’abord</span><span class="sxs-lookup"><span data-stu-id="d1d3d-107">General issues toocheck first</span></span>

-   <span data-ttu-id="d1d3d-108">Si une application vient d’être supprimée d’un utilisateur ou groupe hello utilisateur est membre de, réessayez toosign et l’extraction dans le volet d’accès de l’utilisateur hello après quelques minutes toosee si l’application hello est supprimée.</span><span class="sxs-lookup"><span data-stu-id="d1d3d-108">If an application was just removed from a user or group hello user is a member of, try toosign in and out again into hello user’s Access Panel after a few minutes toosee if hello application is removed.</span></span>

-   <span data-ttu-id="d1d3d-109">Si une licence vient d’être supprimée d’un utilisateur ou un utilisateur hello le groupe est que membre de ce peut prendre beaucoup de temps, selon la taille de hello et la complexité du groupe hello pour toobe des modifications apportée.</span><span class="sxs-lookup"><span data-stu-id="d1d3d-109">If a license was just removed from a user or group hello user is a member of this may take a long time, depending on hello size and complexity of hello group for changes toobe made.</span></span> <span data-ttu-id="d1d3d-110">Prévoyez du temps supplémentaire avant de vous connecter en hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="d1d3d-110">Allow for extra time before signing into hello Access Panel.</span></span>

## <a name="problems-related-tooassigning-applications-toousers"></a><span data-ttu-id="d1d3d-111">Des problèmes connexes tooassigning applications toousers</span><span class="sxs-lookup"><span data-stu-id="d1d3d-111">Problems related tooassigning applications toousers</span></span>

<span data-ttu-id="d1d3d-112">Un utilisateur peut s’agir d’une application dans leur volet d’accès, car il avaient été précédemment affecté tooit.</span><span class="sxs-lookup"><span data-stu-id="d1d3d-112">A user may be seeing an application on their Access Panel because they had been previously assigned tooit.</span></span> <span data-ttu-id="d1d3d-113">Voici certains toocheck façons :</span><span class="sxs-lookup"><span data-stu-id="d1d3d-113">Below are some ways toocheck:</span></span>

-   [<span data-ttu-id="d1d3d-114">Vérifiez si un utilisateur est affecté toohello application</span><span class="sxs-lookup"><span data-stu-id="d1d3d-114">Check if a user is assigned toohello application</span></span>](#check-if-a-user-is-assigned-to-the-application)

-   [<span data-ttu-id="d1d3d-115">Vérifier si un utilisateur est sous licence toohello application relative</span><span class="sxs-lookup"><span data-stu-id="d1d3d-115">Check if a user is under a license related toohello application</span></span>](#check-if-a-user-is-under-a-license-related-to-the-application)


### <a name="check-if-a-user-is-assigned-toohello-application"></a><span data-ttu-id="d1d3d-116">Vérifiez si un utilisateur est affecté toohello application</span><span class="sxs-lookup"><span data-stu-id="d1d3d-116">Check if a user is assigned toohello application</span></span>

<span data-ttu-id="d1d3d-117">toocheck si un utilisateur est assigné toohello application, procédez comme suit hello :</span><span class="sxs-lookup"><span data-stu-id="d1d3d-117">toocheck if a user is assigned toohello application, follow hello steps below:</span></span>

1.  <span data-ttu-id="d1d3d-118">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="d1d3d-118">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d1d3d-119">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="d1d3d-119">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d1d3d-120">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="d1d3d-120">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d1d3d-121">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d1d3d-121">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d1d3d-122">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="d1d3d-122">click **All Applications** tooview a list of all your applications.</span></span>

6.  <span data-ttu-id="d1d3d-123">**Recherche** pour nom hello de l’application hello en question.</span><span class="sxs-lookup"><span data-stu-id="d1d3d-123">**Search** for hello name of hello application in question.</span></span>

7.  <span data-ttu-id="d1d3d-124">Sélectionnez **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="d1d3d-124">click **Users and groups**.</span></span>

8.  <span data-ttu-id="d1d3d-125">Vérifiez toosee si votre utilisateur est affecté toohello application.</span><span class="sxs-lookup"><span data-stu-id="d1d3d-125">Check toosee if your user is assigned toohello application.</span></span>

  * <span data-ttu-id="d1d3d-126">Si vous souhaitez que les utilisateurs de hello tooremove à partir de l’application hello, **cliquez sur la ligne hello** de l’utilisateur de hello et sélectionnez **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="d1d3d-126">If you want tooremove hello user from hello application, **click hello row** of hello user and select **delete**.</span></span>

### <a name="check-if-a-user-is-under-a-license-related-toohello-application"></a><span data-ttu-id="d1d3d-127">Vérifier si un utilisateur est sous licence toohello application relative</span><span class="sxs-lookup"><span data-stu-id="d1d3d-127">Check if a user is under a license related toohello application</span></span>

<span data-ttu-id="d1d3d-128">toocheck un utilisateur affecté des licences, suivez les étapes hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="d1d3d-128">toocheck a user’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="d1d3d-129">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="d1d3d-129">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d1d3d-130">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="d1d3d-130">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d1d3d-131">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="d1d3d-131">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d1d3d-132">Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.</span><span class="sxs-lookup"><span data-stu-id="d1d3d-132">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="d1d3d-133">Cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="d1d3d-133">click **All users**.</span></span>

6.  <span data-ttu-id="d1d3d-134">**Recherche** pour l’utilisateur hello vous intéressez et **cliquez sur la ligne hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="d1d3d-134">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="d1d3d-135">Cliquez sur **licences** toosee les licences hello d’utilisateur est affectée actuellement.</span><span class="sxs-lookup"><span data-stu-id="d1d3d-135">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

   * <span data-ttu-id="d1d3d-136">Si l’utilisateur de hello est attribué une licence Office tooan Ceci activer premier tiers Office applications tooappear sur hello panneau d’accès de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d1d3d-136">If hello user is assigned tooan Office license this enable First Party Office applications tooappear on hello user’s Access Panel.</span></span>

## <a name="problems-related-tooassigning-applications-toogroups"></a><span data-ttu-id="d1d3d-137">Des problèmes connexes tooassigning applications toogroups</span><span class="sxs-lookup"><span data-stu-id="d1d3d-137">Problems related tooassigning applications toogroups</span></span>

<span data-ttu-id="d1d3d-138">Un utilisateur peut s’agir d’une application dans leur volet d’accès car ils font partie d’un groupe auquel a été attribué application hello.</span><span class="sxs-lookup"><span data-stu-id="d1d3d-138">A user may be seeing an application on their Access Panel because they are part of a group that has been assigned hello application.</span></span> <span data-ttu-id="d1d3d-139">Voici certains toocheck façons :</span><span class="sxs-lookup"><span data-stu-id="d1d3d-139">Below are some ways toocheck:</span></span>

-   [<span data-ttu-id="d1d3d-140">Vérifier les appartenances d’un utilisateur à des groupes</span><span class="sxs-lookup"><span data-stu-id="d1d3d-140">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="d1d3d-141">Vérifiez si un utilisateur est membre d’un groupe tooa licence attribué</span><span class="sxs-lookup"><span data-stu-id="d1d3d-141">Check if a user is a member of a group assigned tooa license</span></span>](#check-if-a-user-is-a-member-of-a-group-assigned-to-a-license)

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="d1d3d-142">Vérifier les appartenances d’un utilisateur à des groupes</span><span class="sxs-lookup"><span data-stu-id="d1d3d-142">Check a user’s group memberships</span></span>

<span data-ttu-id="d1d3d-143">toocheck une appartenance de groupe, suivez les étapes hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="d1d3d-143">toocheck a group’s membership, follow hello steps below:</span></span>

1.  <span data-ttu-id="d1d3d-144">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="d1d3d-144">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d1d3d-145">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="d1d3d-145">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d1d3d-146">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="d1d3d-146">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d1d3d-147">Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.</span><span class="sxs-lookup"><span data-stu-id="d1d3d-147">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="d1d3d-148">Cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="d1d3d-148">click **All users**.</span></span>

6.  <span data-ttu-id="d1d3d-149">**Recherche** pour l’utilisateur hello vous intéressez et **cliquez sur la ligne hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="d1d3d-149">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="d1d3d-150">Cliquez sur **Groupes.**</span><span class="sxs-lookup"><span data-stu-id="d1d3d-150">click **Groups.**</span></span>

8.  <span data-ttu-id="d1d3d-151">Vérifiez toosee si l’utilisateur fait partie d’une application toohello de groupe affecté.</span><span class="sxs-lookup"><span data-stu-id="d1d3d-151">Check toosee if your user is part of a Group assigned toohello application.</span></span>

   * <span data-ttu-id="d1d3d-152">Si vous souhaitez utilisateur de hello tooremove à partir du groupe de hello, **cliquez sur la ligne hello** hello groupe d’et sélectionnez Supprimer.</span><span class="sxs-lookup"><span data-stu-id="d1d3d-152">If you want tooremove hello user from hello group, **click hello row** of hello group and select delete.</span></span>

### <a name="check-if-a-user-is-a-member-of-a-group-assigned-tooa-license"></a><span data-ttu-id="d1d3d-153">Vérifiez si un utilisateur est membre d’un groupe tooa licence attribué</span><span class="sxs-lookup"><span data-stu-id="d1d3d-153">Check if a user is a member of a group assigned tooa license</span></span>

1.  <span data-ttu-id="d1d3d-154">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="d1d3d-154">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d1d3d-155">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="d1d3d-155">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d1d3d-156">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="d1d3d-156">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d1d3d-157">Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.</span><span class="sxs-lookup"><span data-stu-id="d1d3d-157">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="d1d3d-158">Cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="d1d3d-158">click **All users**.</span></span>

6.  <span data-ttu-id="d1d3d-159">**Recherche** pour l’utilisateur hello vous intéressez et **cliquez sur la ligne hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="d1d3d-159">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="d1d3d-160">Cliquez sur **Groupes.**</span><span class="sxs-lookup"><span data-stu-id="d1d3d-160">click **Groups.**</span></span>

8.  <span data-ttu-id="d1d3d-161">Cliquez sur ligne hello d’un groupe spécifique.</span><span class="sxs-lookup"><span data-stu-id="d1d3d-161">click hello row of a specific group.</span></span>

9.  <span data-ttu-id="d1d3d-162">Cliquez sur **licences** toosee quel groupe hello de licences a affecté tooit.</span><span class="sxs-lookup"><span data-stu-id="d1d3d-162">click **Licenses** toosee which licenses hello group has assigned tooit.</span></span>

  * <span data-ttu-id="d1d3d-163">Si le groupe de hello est attribué une licence Office tooan sur que ceci peut activer certaine tooappear d’applications de premier tiers Office hello panneau d’accès de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d1d3d-163">If hello group is assigned tooan Office license this may enable certain First Party Office applications tooappear on hello user’s Access Panel.</span></span>


## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a><span data-ttu-id="d1d3d-164">Si ces étapes de dépannage ne pas hello hello résoudre</span><span class="sxs-lookup"><span data-stu-id="d1d3d-164">If these troubleshooting steps do not hello resolve hello issue</span></span>

<span data-ttu-id="d1d3d-165">Ouvrez un ticket de support avec hello informations suivantes si elle est disponible :</span><span class="sxs-lookup"><span data-stu-id="d1d3d-165">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="d1d3d-166">ID d’erreur de corrélation</span><span class="sxs-lookup"><span data-stu-id="d1d3d-166">Correlation error ID</span></span>

-   <span data-ttu-id="d1d3d-167">Nom d’utilisateur principal (adresse de messagerie de l’utilisateur)</span><span class="sxs-lookup"><span data-stu-id="d1d3d-167">UPN (user email address)</span></span>

-   <span data-ttu-id="d1d3d-168">ID client</span><span class="sxs-lookup"><span data-stu-id="d1d3d-168">Tenant ID</span></span>

-   <span data-ttu-id="d1d3d-169">Type de navigateur</span><span class="sxs-lookup"><span data-stu-id="d1d3d-169">Browser type</span></span>

-   <span data-ttu-id="d1d3d-170">Fuseau horaire et heure/période à laquelle l’erreur se produit</span><span class="sxs-lookup"><span data-stu-id="d1d3d-170">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="d1d3d-171">Traces Fiddler</span><span class="sxs-lookup"><span data-stu-id="d1d3d-171">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1d3d-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d1d3d-172">Next steps</span></span>
[<span data-ttu-id="d1d3d-173">Gestion des applications avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d1d3d-173">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
