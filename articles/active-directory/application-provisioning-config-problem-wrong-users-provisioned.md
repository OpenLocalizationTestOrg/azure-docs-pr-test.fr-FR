---
title: "ensemble aaaWrong d’utilisateurs sont en cours d’application de la galerie tooan mis en service Azure AD | Documents Microsoft"
description: "Découvrez comment toofind les pourquoi un ensemble différent d’utilisateurs sont mis en service application tooan que ceux attendus"
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
ms.openlocfilehash: adb90b12a53fb3160ce2b73b2559df92b283438e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="wrong-set-of-users-are-being-provisioned-tooan-azure-ad-gallery-application"></a><span data-ttu-id="80201-103">Mauvais groupe d’utilisateurs sont en cours d’application de la galerie tooan mis en service Azure AD</span><span class="sxs-lookup"><span data-stu-id="80201-103">Wrong set of users are being provisioned tooan Azure AD Gallery application</span></span>

<span data-ttu-id="80201-104">Les utilisateurs qui sont approvisionnés toohello application est basée sur les utilisateurs et les groupes auxquels ont été **affecté** toohello application.</span><span class="sxs-lookup"><span data-stu-id="80201-104">Which users are provisioned toohello app is primarily driven by which users and groups have been **assigned** toohello application.</span></span>

<span data-ttu-id="80201-105">Utilisez les ressources hello ci-dessous toolearn comment toocheck les utilisateurs et les groupes auxquels ont été attribué des application tooan dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="80201-105">Use hello resources below toolearn how toocheck which users and groups have been assigned tooan application within Azure Active Directory.</span></span>

## <a name="assign-a-user-directly-as-an-administrator"></a><span data-ttu-id="80201-106">Affecter un utilisateur directement en tant qu’administrateur</span><span class="sxs-lookup"><span data-stu-id="80201-106">Assign a user directly as an administrator</span></span>

<span data-ttu-id="80201-107">tooassign un ou plusieurs utilisateurs tooan application directement, comme suit hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="80201-107">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="80201-108">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="80201-108">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="80201-109">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="80201-109">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="80201-110">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="80201-110">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="80201-111">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="80201-111">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="80201-112">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="80201-112">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="80201-113">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="80201-113">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="80201-114">Sélectionnez l’application hello tooassign une liste des utilisateurs toofrom hello.</span><span class="sxs-lookup"><span data-stu-id="80201-114">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="80201-115">Une fois le charge de l’application hello, cliquez sur **utilisateurs et groupes** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="80201-115">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="80201-116">Cliquez sur hello **ajouter** bouton par-dessus hello **utilisateurs et groupes** hello tooopen de liste **ajouter l’affectation** panneau.</span><span class="sxs-lookup"><span data-stu-id="80201-116">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="80201-117">Cliquez sur hello **utilisateurs et groupes** sélecteur de hello **ajouter l’affectation** panneau.</span><span class="sxs-lookup"><span data-stu-id="80201-117">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="80201-118">Type Bonjour **nom complet** ou **adresse de messagerie** d’utilisateur hello vous êtes intéressé par attribution dans hello **recherche par nom ou adresse de messagerie** zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="80201-118">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="80201-119">Placez le curseur sur hello **utilisateur** dans hello liste tooreveal un **case à cocher**.</span><span class="sxs-lookup"><span data-stu-id="80201-119">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="80201-120">Cliquez sur tooadd de photo ou le logo de profil hello case à cocher suivante toohello l’utilisateur à votre toohello utilisateur **sélectionnés** liste.</span><span class="sxs-lookup"><span data-stu-id="80201-120">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="80201-121">**Facultatif :** si vous souhaitez que trop**ajouter plusieurs utilisateurs**, type dans un autre **nom complet** ou **adresse de messagerie** dans hello **Rechercher par nom ou l’adresse de messagerie** zone de recherche, cliquez sur tooadd de case à cocher hello cette toohello utilisateur **sélectionnés** liste.</span><span class="sxs-lookup"><span data-stu-id="80201-121">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="80201-122">Lorsque vous avez fini de sélectionner les utilisateurs, cliquez sur hello **sélectionnez** bouton tooadd les toohello la liste des toobe utilisateurs et groupes affectés toohello application.</span><span class="sxs-lookup"><span data-stu-id="80201-122">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="80201-123">**Facultatif :** cliquez sur hello **sélectionner un rôle** sélecteur Bonjour **ajouter l’affectation** panneau tooselect un rôle aux utilisateurs de toohello tooassign que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="80201-123">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="80201-124">Cliquez sur hello **affecter** bouton tooassign hello application toohello les utilisateurs sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="80201-124">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="80201-125">Si cette configuration est configuré et en cours d’exécution pour une application, les nouveaux utilisateurs doivent être application tooan approvisionnés dans 10 minutes environ.</span><span class="sxs-lookup"><span data-stu-id="80201-125">If provisioning is configured and already running for an app, new users should be provisioned tooan application in approximately 10 minutes.</span></span> <span data-ttu-id="80201-126">Vérifiez hello **les journaux d’Audit** pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="80201-126">Check hello **Audit Logs** for details.</span></span>

## <a name="assign-a-group-directly-tooan-application-as-an-administrator"></a><span data-ttu-id="80201-127">Assigner un groupe directement tooan application en tant qu’administrateur</span><span class="sxs-lookup"><span data-stu-id="80201-127">Assign a group directly tooan application as an administrator</span></span>

<span data-ttu-id="80201-128">tooassign un ou plusieurs groupes tooan application directement, hello suivez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="80201-128">tooassign one or more groups tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="80201-129">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="80201-129">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="80201-130">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="80201-130">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="80201-131">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="80201-131">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="80201-132">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="80201-132">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="80201-133">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="80201-133">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="80201-134">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="80201-134">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="80201-135">Sélectionnez l’application hello tooassign une liste des utilisateurs toofrom hello.</span><span class="sxs-lookup"><span data-stu-id="80201-135">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="80201-136">Une fois le charge de l’application hello, cliquez sur **utilisateurs et groupes** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="80201-136">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="80201-137">Cliquez sur hello **ajouter** bouton par-dessus hello **utilisateurs et groupes** hello tooopen de liste **ajouter l’affectation** panneau.</span><span class="sxs-lookup"><span data-stu-id="80201-137">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="80201-138">Cliquez sur hello **utilisateurs et groupes** sélecteur de hello **ajouter l’affectation** panneau.</span><span class="sxs-lookup"><span data-stu-id="80201-138">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="80201-139">Type Bonjour **nom de groupe complète** groupe hello vous êtes intéressé par attribution dans hello **recherche par nom ou adresse de messagerie** zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="80201-139">Type in hello **full group name** of hello group you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="80201-140">Placez le curseur sur hello **groupe** dans hello liste tooreveal un **case à cocher**.</span><span class="sxs-lookup"><span data-stu-id="80201-140">Hover over hello **group** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="80201-141">Cliquez sur tooadd de photo ou le logo de profil de hello case à cocher toohello groupe suivant votre toohello utilisateur **sélectionnés** liste.</span><span class="sxs-lookup"><span data-stu-id="80201-141">Click hello checkbox next toohello group’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="80201-142">**Facultatif :** si vous souhaitez que trop**ajouter plusieurs groupes**, type dans un autre **nom de groupe complète** dans hello **recherche par nom ou adresse de messagerie** zone de recherche, Cliquez sur tooadd de case à cocher hello toohello de ce groupe **sélectionnés** liste.</span><span class="sxs-lookup"><span data-stu-id="80201-142">**Optional:** If you would like too**add more than one group**, type in another **full group name** into hello **Search by name or email address** search box, and click hello checkbox tooadd this group toohello **Selected** list.</span></span>

13. <span data-ttu-id="80201-143">Lorsque vous avez fini de sélectionner les groupes, cliquez sur hello **sélectionnez** bouton tooadd les toohello la liste des toobe utilisateurs et groupes affectés toohello application.</span><span class="sxs-lookup"><span data-stu-id="80201-143">When you are finished selecting groups, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="80201-144">**Facultatif :** cliquez sur hello **sélectionner un rôle** sélecteur Bonjour **ajouter l’affectation** panneau tooselect un toohello de tooassign rôle groupes que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="80201-144">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello groups you have selected.</span></span>

15. <span data-ttu-id="80201-145">Cliquez sur hello **affecter** bouton tooassign hello application toohello les groupes sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="80201-145">Click hello **Assign** button tooassign hello application toohello selected groups.</span></span>

<span data-ttu-id="80201-146">Si cette configuration est configuré et en cours d’exécution pour une application, les nouveaux utilisateurs contenus dans le groupe de hello doivent être application tooan approvisionnés dans 10 minutes environ.</span><span class="sxs-lookup"><span data-stu-id="80201-146">If provisioning is configured and already running for an app, new users contained within hello group should be provisioned tooan application in approximately 10 minutes.</span></span> <span data-ttu-id="80201-147">Vérifiez hello **les journaux d’Audit** pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="80201-147">Check hello **Audit Logs** for details.</span></span>

>[!IMPORTANT]
><span data-ttu-id="80201-148">Hello nom du groupe de configuration d’et de groupe plus d’informations, dans les membres de toohello de plus, si la prise en charge pour certaines applications.</span><span class="sxs-lookup"><span data-stu-id="80201-148">Provisioning of hello group name and group details, in addition toohello members, if supported for some applications.</span></span> <span data-ttu-id="80201-149">Vous pouvez activer ou désactiver cette fonctionnalité en activant ou désactivant hello **mappage** pour les objets de groupe affichés dans hello **Provisioning** onglet.</span><span class="sxs-lookup"><span data-stu-id="80201-149">You can enable or disable this functionality by enabling or disabling hello **Mapping** for group objects shown in hello **Provisioning** tab.</span></span> 
>
>

<span data-ttu-id="80201-150">Si la configuration des groupes est activée, veillez à tooreview hello attribut mappages tooensure un champ approprié est utilisé pour hello « correspondant ID ».</span><span class="sxs-lookup"><span data-stu-id="80201-150">If provisioning groups is enabled, be sure tooreview hello attribute mappings tooensure an appropriate field is being used for hello “matching ID”.</span></span> <span data-ttu-id="80201-151">Cela peut être le nom d’affichage hello ou par courrier électronique à l’alias, que hello groupe et ses membres ne pas être configurés si hello correspondant est vide ou non remplie pour un groupe dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="80201-151">This can be hello display name or email alias, as hello group and its members not be provisioned if hello matching property is empty or not populated for a group in Azure AD.</span></span>

## <a name="next-steps"></a><span data-ttu-id="80201-152">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="80201-152">Next steps</span></span>
[<span data-ttu-id="80201-153">Automatiser la configuration de l’utilisateur et Deprovisioning tooSaaS Applications avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="80201-153">Automate User Provisioning and Deprovisioning tooSaaS Applications with Azure Active Directory</span></span>](active-directory-saas-app-provisioning.md)
