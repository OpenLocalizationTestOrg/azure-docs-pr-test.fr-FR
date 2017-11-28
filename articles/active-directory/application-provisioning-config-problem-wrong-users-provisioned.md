---
title: "Un mauvais ensemble d’utilisateurs est affecté à une application de la galerie Azure AD | Microsoft Docs"
description: "Découvrez pourquoi un autre ensemble d’utilisateurs que celui que vous attendiez est affecté à une application"
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
ms.openlocfilehash: 85b533584c8ec15a23be32e20db7de583fced6a0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="wrong-set-of-users-are-being-provisioned-to-an-azure-ad-gallery-application"></a><span data-ttu-id="dfe86-103">Un mauvais ensemble d’utilisateurs est affecté à une application de la galerie Azure AD</span><span class="sxs-lookup"><span data-stu-id="dfe86-103">Wrong set of users are being provisioned to an Azure AD Gallery application</span></span>

<span data-ttu-id="dfe86-104">Le choix des utilisateurs affectés à l’application dépend principalement des utilisateurs et groupes qui ont été **affectés** à l’application.</span><span class="sxs-lookup"><span data-stu-id="dfe86-104">Which users are provisioned to the app is primarily driven by which users and groups have been **assigned** to the application.</span></span>

<span data-ttu-id="dfe86-105">Utilisez les ressources ci-dessous pour déterminer quels utilisateurs et groupes ont été affectés à une application dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="dfe86-105">Use the resources below to learn how to check which users and groups have been assigned to an application within Azure Active Directory.</span></span>

## <a name="assign-a-user-directly-as-an-administrator"></a><span data-ttu-id="dfe86-106">Affecter un utilisateur directement en tant qu’administrateur</span><span class="sxs-lookup"><span data-stu-id="dfe86-106">Assign a user directly as an administrator</span></span>

<span data-ttu-id="dfe86-107">Pour affecter un ou plusieurs utilisateurs directement à une application, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="dfe86-107">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="dfe86-108">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général.**</span><span class="sxs-lookup"><span data-stu-id="dfe86-108">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="dfe86-109">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="dfe86-109">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="dfe86-110">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dfe86-110">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="dfe86-111">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="dfe86-111">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="dfe86-112">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="dfe86-112">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="dfe86-113">Si l’application que vous recherchez ne figure pas dans la liste, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications.**</span><span class="sxs-lookup"><span data-stu-id="dfe86-113">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="dfe86-114">Dans la liste qui s’affiche, sélectionnez l’application à laquelle vous souhaitez affecter un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="dfe86-114">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="dfe86-115">Une fois l’application chargée, cliquez sur **Utilisateurs et groupes** dans le menu de navigation de gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="dfe86-115">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="dfe86-116">Cliquez sur le bouton **Ajouter** en haut de la liste **Utilisateurs et groupes** pour ouvrir le panneau **Ajouter une attribution**.</span><span class="sxs-lookup"><span data-stu-id="dfe86-116">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="dfe86-117">Cliquez sur le sélecteur **Utilisateurs et groupes** à partir du panneau **Ajouter une attribution**.</span><span class="sxs-lookup"><span data-stu-id="dfe86-117">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="dfe86-118">Tapez **le nom complet** ou **l’adresse de messagerie** de l’utilisateur souhaité pour l’attribution dans la zone de recherche **Rechercher par nom ou adresse de messagerie**.</span><span class="sxs-lookup"><span data-stu-id="dfe86-118">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="dfe86-119">Pointez sur **l’utilisateur** dans la liste pour afficher une **case à cocher**.</span><span class="sxs-lookup"><span data-stu-id="dfe86-119">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="dfe86-120">Cliquez sur la case à cocher en regard de la photo de profil ou du logo de l’utilisateur pour ajouter ce dernier à la liste **Sélectionné**.</span><span class="sxs-lookup"><span data-stu-id="dfe86-120">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="dfe86-121">**Facultatif :** si vous souhaitez **ajouter plusieurs utilisateurs**, entrez un autre **nom complet** ou une autre **adresse de messagerie** dans la zone de recherche **Rechercher par nom ou adresse de messagerie**, puis cliquez sur la case à cocher pour ajouter cet utilisateur à la liste **Sélectionné**.</span><span class="sxs-lookup"><span data-stu-id="dfe86-121">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="dfe86-122">Après avoir sélectionné les utilisateurs, cliquez sur le bouton **Sélectionner** pour les ajouter à la liste des utilisateurs et des groupes à affecter à l’application.</span><span class="sxs-lookup"><span data-stu-id="dfe86-122">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="dfe86-123">**Facultatif :** cliquez sur le sélecteur **Sélectionner un rôle** dans le panneau **Ajouter une attribution** pour sélectionner un rôle à affecter aux utilisateurs que vous avez sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="dfe86-123">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="dfe86-124">Cliquez sur le bouton **Attribuer** pour affecter l’application aux utilisateurs sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="dfe86-124">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="dfe86-125">Si l’approvisionnement est configuré et déjà en cours d’exécution pour une application, les nouveaux utilisateurs doivent être affectés à une application en 10 minutes environ.</span><span class="sxs-lookup"><span data-stu-id="dfe86-125">If provisioning is configured and already running for an app, new users should be provisioned to an application in approximately 10 minutes.</span></span> <span data-ttu-id="dfe86-126">Consultez **les journaux d’audit** pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="dfe86-126">Check the **Audit Logs** for details.</span></span>

## <a name="assign-a-group-directly-to-an-application-as-an-administrator"></a><span data-ttu-id="dfe86-127">Affecter un groupe directement à une application en tant qu’administrateur</span><span class="sxs-lookup"><span data-stu-id="dfe86-127">Assign a group directly to an application as an administrator</span></span>

<span data-ttu-id="dfe86-128">Pour affecter un ou plusieurs groupes directement à une application, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="dfe86-128">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="dfe86-129">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant **qu’administrateur général**.</span><span class="sxs-lookup"><span data-stu-id="dfe86-129">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="dfe86-130">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="dfe86-130">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="dfe86-131">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dfe86-131">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="dfe86-132">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="dfe86-132">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="dfe86-133">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="dfe86-133">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="dfe86-134">Si l’application que vous recherchez ne figure pas dans la liste, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications.**</span><span class="sxs-lookup"><span data-stu-id="dfe86-134">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="dfe86-135">Dans la liste qui s’affiche, sélectionnez l’application à laquelle vous souhaitez affecter un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="dfe86-135">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="dfe86-136">Une fois l’application chargée, cliquez sur **Utilisateurs et groupes** dans le menu de navigation de gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="dfe86-136">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="dfe86-137">Cliquez sur le bouton **Ajouter** en haut de la liste **Utilisateurs et groupes** pour ouvrir le panneau **Ajouter une attribution**.</span><span class="sxs-lookup"><span data-stu-id="dfe86-137">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="dfe86-138">Cliquez sur le sélecteur **Utilisateurs et groupes** à partir du panneau **Ajouter une attribution**.</span><span class="sxs-lookup"><span data-stu-id="dfe86-138">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="dfe86-139">Tapez le **nom de groupe complet** du groupe souhaité pour l’attribution dans la zone de recherche **Rechercher par nom ou adresse de messagerie**.</span><span class="sxs-lookup"><span data-stu-id="dfe86-139">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="dfe86-140">Pointez sur le **groupe** dans la liste pour afficher une **case à cocher**.</span><span class="sxs-lookup"><span data-stu-id="dfe86-140">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="dfe86-141">Cliquez sur la case à cocher en regard de la photo de profil ou du logo du groupe pour ajouter ce dernier à la liste **Sélectionné**.</span><span class="sxs-lookup"><span data-stu-id="dfe86-141">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="dfe86-142">**Facultatif :** si vous souhaitez **ajouter plusieurs groupes**, entrez un autre **nom de groupe complet** dans la zone de recherche **Rechercher par nom ou adresse de messagerie**, puis cliquez sur la case à cocher pour ajouter ce groupe à la liste **Sélectionné**.</span><span class="sxs-lookup"><span data-stu-id="dfe86-142">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="dfe86-143">Lorsque vous avez fini de sélectionner les groupes, cliquez sur le bouton **Sélectionner** pour les ajouter à la liste des utilisateurs et des groupes à affecter à l’application.</span><span class="sxs-lookup"><span data-stu-id="dfe86-143">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="dfe86-144">**Facultatif :** cliquez sur le sélecteur **Sélectionner un rôle** dans le panneau **Ajouter une attribution** pour sélectionner un rôle à affecter aux groupes que vous avez sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="dfe86-144">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="dfe86-145">Cliquez sur le bouton **Attribuer** pour affecter l’application aux groupes sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="dfe86-145">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="dfe86-146">Si l’approvisionnement est configuré et déjà en cours d’exécution pour une application, les nouveaux utilisateurs de ce groupe doivent être affectés à une application en 10 minutes environ.</span><span class="sxs-lookup"><span data-stu-id="dfe86-146">If provisioning is configured and already running for an app, new users contained within the group should be provisioned to an application in approximately 10 minutes.</span></span> <span data-ttu-id="dfe86-147">Consultez **les journaux d’audit** pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="dfe86-147">Check the **Audit Logs** for details.</span></span>

>[!IMPORTANT]
><span data-ttu-id="dfe86-148">Approvisionnement du nom du groupe et des détails du groupe, en plus des membres, si la prise en charge est effective pour certaines applications.</span><span class="sxs-lookup"><span data-stu-id="dfe86-148">Provisioning of the group name and group details, in addition to the members, if supported for some applications.</span></span> <span data-ttu-id="dfe86-149">Vous pouvez activer ou désactiver cette fonctionnalité en activant ou désactivant la **mappage** pour les objets de groupe affichés dans l’onglet **Approvisionnement**.</span><span class="sxs-lookup"><span data-stu-id="dfe86-149">You can enable or disable this functionality by enabling or disabling the **Mapping** for group objects shown in the **Provisioning** tab.</span></span> 
>
>

<span data-ttu-id="dfe86-150">Si les groupes de configuration sont activés, veillez à passer en revue les mappages d’attributs afin de vous assurer qu'un champ approprié est utilisé pour l’« ID correspondant ».</span><span class="sxs-lookup"><span data-stu-id="dfe86-150">If provisioning groups is enabled, be sure to review the attribute mappings to ensure an appropriate field is being used for the “matching ID”.</span></span> <span data-ttu-id="dfe86-151">Il peut s’agir du nom d’affichage ou de l’alias de courrier électronique, comme le groupe et ses membres qui ne sont pas approvisionnés si la propriété correspondante est vide ou n’est pas remplie pour un groupe dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dfe86-151">This can be the display name or email alias, as the group and its members not be provisioned if the matching property is empty or not populated for a group in Azure AD.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dfe86-152">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dfe86-152">Next steps</span></span>
[<span data-ttu-id="dfe86-153">Automatisation de l’approvisionnement et de la l’annulation de l’approvisionnement des utilisateurs pour les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dfe86-153">Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory</span></span>](active-directory-saas-app-provisioning.md)
