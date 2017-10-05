---
title: "Guide pratique pour affecter des utilisateurs et des groupes à une application | Microsoft Docs"
description: "Affecter des utilisateurs à l’application pour accorder l’accès"
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
ms.openlocfilehash: 61536612e0dd5102b8f5e911c350826846f5ed77
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-assign-users-and-groups-to-an-application"></a><span data-ttu-id="87737-103">Guide pratique pour affecter des utilisateurs et des groupes à une application</span><span class="sxs-lookup"><span data-stu-id="87737-103">How to assign users and groups to an application</span></span>

<span data-ttu-id="87737-104">Afin de permettre à vos utilisateurs d’effectuer une des opérations ci-dessous pour une application spécifique, vous devez d’abord **les affecter à l’application** pour leur en donner l’accès :</span><span class="sxs-lookup"><span data-stu-id="87737-104">Before your users can do any of the below for a specific application, you need to first **assign them to the application** to grant them access:</span></span>

-   <span data-ttu-id="87737-105">Accéder à une application en **naviguant directement vers l’URL de l’application** (authentification initiée par le fournisseur de services).</span><span class="sxs-lookup"><span data-stu-id="87737-105">Access an application by **navigating to the application’s URL directly** (also known as SP-initiated sign-on).</span></span>

-   <span data-ttu-id="87737-106">Accéder à une application en utilisant l’**URL d’accès utilisateur** sur la page **Propriétés** de l’application (authentification initiée par le fournisseur d’identité).</span><span class="sxs-lookup"><span data-stu-id="87737-106">Access an application by using the **User Access URL** on an application’s **Properties** page (also known as IDP-initiated sign on).</span></span>

-   <span data-ttu-id="87737-107">Afficher une application sur leur [volet d’accès aux applications](https://myapps.microsoft.com/) ou leur application mobile.</span><span class="sxs-lookup"><span data-stu-id="87737-107">See an application appear on their [Application Access Panel](https://myapps.microsoft.com/) or mobile application.</span></span>

-   <span data-ttu-id="87737-108">Afficher une application qui apparaît sur leur [Lanceur d’applications Office 365](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a).</span><span class="sxs-lookup"><span data-stu-id="87737-108">See an application appear on their [Office 365 Application Launcher](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a).</span></span>

## <a name="methods-to-assign-applications-with-azure-active-directory"></a><span data-ttu-id="87737-109">Méthodes d’affectation d’applications avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="87737-109">Methods to assign applications with Azure Active Directory</span></span> 

<span data-ttu-id="87737-110">Il existe 3 méthodes d’affectation d’applications avec Azure Active Directory :</span><span class="sxs-lookup"><span data-stu-id="87737-110">There are 3 ways you can assign applications with Azure Active Directory:</span></span>

-   [<span data-ttu-id="87737-111">Affecter un utilisateur directement à une application en tant qu’administrateur</span><span class="sxs-lookup"><span data-stu-id="87737-111">Assign a user directly to an application as an administrator</span></span>](#assign-a-user-directly-as-an-administrator)

-   [<span data-ttu-id="87737-112">Affecter un groupe directement à une application en tant qu’administrateur</span><span class="sxs-lookup"><span data-stu-id="87737-112">Assign a group directly to an application as an administrator</span></span>](#assign-a-group-directly-to-an-application-as-an-administrator)

-   [<span data-ttu-id="87737-113">Activer l’accès aux applications en libre-service pour permettre aux utilisateurs de rechercher leurs propres applications.</span><span class="sxs-lookup"><span data-stu-id="87737-113">Enable self-service application access to allow users to find their own applications</span></span>](#enable-self-service-application-access-to-allow-users-to-find-their-own-applications)

## <a name="assign-a-user-directly-as-an-administrator"></a><span data-ttu-id="87737-114">Affecter un utilisateur directement en tant qu’administrateur</span><span class="sxs-lookup"><span data-stu-id="87737-114">Assign a user directly as an administrator</span></span>

<span data-ttu-id="87737-115">Pour affecter un ou plusieurs utilisateurs directement à une application, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="87737-115">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="87737-116">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général.**</span><span class="sxs-lookup"><span data-stu-id="87737-116">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="87737-117">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="87737-117">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="87737-118">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="87737-118">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="87737-119">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="87737-119">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="87737-120">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="87737-120">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="87737-121">Si l’application que vous recherchez ne figure pas dans la liste, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications.**</span><span class="sxs-lookup"><span data-stu-id="87737-121">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="87737-122">Dans la liste qui s’affiche, sélectionnez l’application à laquelle vous souhaitez affecter un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="87737-122">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="87737-123">Une fois l’application chargée, cliquez sur **Utilisateurs et groupes** dans le menu de navigation de gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="87737-123">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="87737-124">Cliquez sur le bouton **Ajouter** en haut de la liste **Utilisateurs et groupes** pour ouvrir le panneau **Ajouter une attribution**.</span><span class="sxs-lookup"><span data-stu-id="87737-124">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="87737-125">Cliquez sur le sélecteur **Utilisateurs et groupes** à partir du panneau **Ajouter une attribution**.</span><span class="sxs-lookup"><span data-stu-id="87737-125">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="87737-126">Tapez **le nom complet** ou **l’adresse de messagerie** de l’utilisateur souhaité pour l’attribution dans la zone de recherche **Rechercher par nom ou adresse de messagerie**.</span><span class="sxs-lookup"><span data-stu-id="87737-126">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="87737-127">Pointez sur **l’utilisateur** dans la liste pour afficher une **case à cocher**.</span><span class="sxs-lookup"><span data-stu-id="87737-127">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="87737-128">Cliquez sur la case à cocher en regard de la photo de profil ou du logo de l’utilisateur pour ajouter ce dernier à la liste **Sélectionné**.</span><span class="sxs-lookup"><span data-stu-id="87737-128">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="87737-129">**Facultatif :** si vous souhaitez **ajouter plusieurs utilisateurs**, entrez un autre **nom complet** ou une autre **adresse de messagerie** dans la zone de recherche **Rechercher par nom ou adresse de messagerie**, puis cliquez sur la case à cocher pour ajouter cet utilisateur à la liste **Sélectionné**.</span><span class="sxs-lookup"><span data-stu-id="87737-129">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="87737-130">Après avoir sélectionné les utilisateurs, cliquez sur le bouton **Sélectionner** pour les ajouter à la liste des utilisateurs et des groupes à affecter à l’application.</span><span class="sxs-lookup"><span data-stu-id="87737-130">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="87737-131">**Facultatif :** cliquez sur le sélecteur **Sélectionner un rôle** dans le panneau **Ajouter une attribution** pour sélectionner un rôle à affecter aux utilisateurs que vous avez sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="87737-131">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="87737-132">Cliquez sur le bouton **Attribuer** pour affecter l’application aux utilisateurs sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="87737-132">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="87737-133">Après une courte période, les utilisateurs que vous avez sélectionnés seront en mesure de démarrer ces applications à l’aide des méthodes décrites dans la section de description des solutions.</span><span class="sxs-lookup"><span data-stu-id="87737-133">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span></span>

## <a name="assign-a-group-directly-to-an-application-as-an-administrator"></a><span data-ttu-id="87737-134">Affecter un groupe directement à une application en tant qu’administrateur</span><span class="sxs-lookup"><span data-stu-id="87737-134">Assign a group directly to an application as an administrator</span></span>

<span data-ttu-id="87737-135">Pour affecter un ou plusieurs groupes directement à une application, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="87737-135">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="87737-136">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant **qu’administrateur général**.</span><span class="sxs-lookup"><span data-stu-id="87737-136">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="87737-137">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="87737-137">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="87737-138">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="87737-138">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="87737-139">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="87737-139">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="87737-140">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="87737-140">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="87737-141">Si l’application que vous recherchez ne figure pas dans la liste, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications.**</span><span class="sxs-lookup"><span data-stu-id="87737-141">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="87737-142">Dans la liste qui s’affiche, sélectionnez l’application à laquelle vous souhaitez affecter un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="87737-142">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="87737-143">Une fois l’application chargée, cliquez sur **Utilisateurs et groupes** dans le menu de navigation de gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="87737-143">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="87737-144">Cliquez sur le bouton **Ajouter** en haut de la liste **Utilisateurs et groupes** pour ouvrir le panneau **Ajouter une attribution**.</span><span class="sxs-lookup"><span data-stu-id="87737-144">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="87737-145">Cliquez sur le sélecteur **Utilisateurs et groupes** à partir du panneau **Ajouter une attribution**.</span><span class="sxs-lookup"><span data-stu-id="87737-145">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="87737-146">Tapez le **nom de groupe complet** du groupe souhaité pour l’attribution dans la zone de recherche **Rechercher par nom ou adresse de messagerie**.</span><span class="sxs-lookup"><span data-stu-id="87737-146">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="87737-147">Pointez sur le **groupe** dans la liste pour afficher une **case à cocher**.</span><span class="sxs-lookup"><span data-stu-id="87737-147">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="87737-148">Cliquez sur la case à cocher en regard de la photo de profil ou du logo du groupe pour ajouter ce dernier à la liste **Sélectionné**.</span><span class="sxs-lookup"><span data-stu-id="87737-148">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="87737-149">**Facultatif :** si vous souhaitez **ajouter plusieurs groupes**, entrez un autre **nom de groupe complet** dans la zone de recherche **Rechercher par nom ou adresse de messagerie**, puis cliquez sur la case à cocher pour ajouter ce groupe à la liste **Sélectionné**.</span><span class="sxs-lookup"><span data-stu-id="87737-149">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="87737-150">Lorsque vous avez fini de sélectionner les groupes, cliquez sur le bouton **Sélectionner** pour les ajouter à la liste des utilisateurs et des groupes à affecter à l’application.</span><span class="sxs-lookup"><span data-stu-id="87737-150">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="87737-151">**Facultatif :** cliquez sur le sélecteur **Sélectionner un rôle** dans le panneau **Ajouter une attribution** pour sélectionner un rôle à affecter aux groupes que vous avez sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="87737-151">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="87737-152">Cliquez sur le bouton **Attribuer** pour affecter l’application aux groupes sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="87737-152">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="87737-153">Après une courte période, les utilisateurs des groupes que vous avez sélectionnés seront en mesure de démarrer ces applications à l’aide des méthodes décrites dans la section de description des solutions.</span><span class="sxs-lookup"><span data-stu-id="87737-153">After a short period of time, the users within the groups you have selected be able to launch these applications using the methods described in the solution description section.</span></span> <span data-ttu-id="87737-154">S’il s’agit de groupes dynamiques, un délai de traitement supplémentaire peut survenir avant que les utilisateurs ne voient ces affectations dans ces groupes affectés.</span><span class="sxs-lookup"><span data-stu-id="87737-154">If these are dynamic groups, there may be some additional processing delay in these assignments appearing for users within these assigned groups.</span></span>

## <a name="enable-self-service-application-access-to-allow-users-to-find-their-own-applications"></a><span data-ttu-id="87737-155">Activer l’accès aux applications en libre-service pour permettre aux utilisateurs de rechercher leurs propres applications</span><span class="sxs-lookup"><span data-stu-id="87737-155">Enable self-service application access to allow users to find their own applications</span></span>

<span data-ttu-id="87737-156">L’accès aux applications en libre-service est un excellent moyen pour permettre aux utilisateurs de découvrir eux-mêmes des applications, et éventuellement de permettre au groupe d’entreprise d’approuver l’accès à ces applications.</span><span class="sxs-lookup"><span data-stu-id="87737-156">Self-service application access is a great way to allow users to self-discover applications, optionally allow the business group to approve access to those applications.</span></span> <span data-ttu-id="87737-157">Vous pouvez autoriser le groupe d’entreprise à gérer les informations d’identification affectées à ces utilisateurs dans le cadre d’une authentification unique par mot de passe, directement depuis leurs volets d’accès.</span><span class="sxs-lookup"><span data-stu-id="87737-157">You can allow the business group to manage the credentials assigned to those users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="87737-158">Pour activer l’accès en libre-service à une application, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="87737-158">To enable self-service application access to an application, follow the steps below:</span></span>

1.  <span data-ttu-id="87737-159">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général**.</span><span class="sxs-lookup"><span data-stu-id="87737-159">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="87737-160">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="87737-160">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="87737-161">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="87737-161">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="87737-162">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="87737-162">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="87737-163">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="87737-163">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="87737-164">Si l’application que vous recherchez n’apparaît pas, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="87737-164">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="87737-165">Sélectionnez l’application pour laquelle vous souhaitez activer l’accès en libre-service à partir de la liste.</span><span class="sxs-lookup"><span data-stu-id="87737-165">Select the application you want to enable Self-service access to from the list.</span></span>

7.  <span data-ttu-id="87737-166">Une fois l’application chargée, cliquez sur **Libre-service** dans le menu de navigation gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="87737-166">Once the application loads, click **Self-service** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="87737-167">Pour activer l’accès en libre-service à cette application, définissez l’option **Autoriser les utilisateurs à demander l’accès à cette application ?** sur **Oui.**</span><span class="sxs-lookup"><span data-stu-id="87737-167">To enable Self-service application access for this application, turn the **Allow users to request access to this application?** toggle to **Yes.**</span></span>

9.  <span data-ttu-id="87737-168">Ensuite, pour sélectionner le groupe auquel les utilisateurs qui demandent l’accès à cette application doivent être ajoutés, cliquez sur le sélecteur en regard de l’étiquette **À quel groupe les utilisateurs attribués doivent-ils être ajoutés ?** et sélectionnez un groupe.</span><span class="sxs-lookup"><span data-stu-id="87737-168">Next, to select the group to which users who request access to this application should be added, click the selector next to the label **To which group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="87737-169">**Facultatif :** si vous souhaitez exiger une approbation d’entreprise avant d’accorder l’accès aux utilisateurs, définissez l’option **Demander une approbation avant d’accorder l’accès à cette application ?** sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="87737-169">**Optional:** If you wish to require a business approval before users are allowed access, set the **Require approval before granting access to this application?** toggle to **Yes**.</span></span>

11. <span data-ttu-id="87737-170">**Facultatif : pour les applications qui nécessitent une authentification unique par mot de passe uniquement,** si vous souhaitez autoriser ces approbateurs d’entreprise à spécifier les mots de passe envoyés à cette application pour les utilisateurs approuvés, définissez l’option **Autoriser les approbateurs à définir les mots de passe de l’utilisateur pour cette application ?** sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="87737-170">**Optional: For applications using password single-sign on only,** if you wish to allow those business approvers to specify the passwords that are sent to this application for approved users, set the **Allow approvers to set user’s passwords for this application?** toggle to **Yes**.</span></span>

12. <span data-ttu-id="87737-171">**Facultatif :** pour spécifier les approbateurs d’entreprise autorisés à approuver l’accès à cette application, cliquez sur le sélecteur en regard de l’étiquette **Qui est autorisé à approuver l’accès à cette application ?** pour sélectionner jusqu’à 10 approbateurs d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="87737-171">**Optional:** To specify the business approvers who are allowed to approve access to this application, click the selector next to the label **Who is allowed to approve access to this application?** to select up to 10 individual business approvers.</span></span>

  >[!NOTE]
  ><span data-ttu-id="87737-172">Les groupes ne sont pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="87737-172">Groups are not supported.</span></span>
  >
  >

13. <span data-ttu-id="87737-173">**Facultatif :** **pour les applications qui exposent des rôles**, si vous souhaitez attribuer un rôle à des utilisateurs approuvés en libre-service, cliquez sur le sélecteur en regard de l’option  **À quel rôle attribuer des utilisateurs dans cette application ?** pour sélectionner le rôle à affecter à ces utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="87737-173">**Optional:** **For applications which expose roles**, if you wish to assign self-service approved users to a role, click the selector next to the **To which role should users be assigned in this application?** to select the role to which these users should be assigned.</span></span>

14. <span data-ttu-id="87737-174">Cliquez sur le bouton **Enregistrer** en haut du volet pour terminer.</span><span class="sxs-lookup"><span data-stu-id="87737-174">Click the **Save** button at the top of the blade to finish.</span></span>

<span data-ttu-id="87737-175">Lorsque vous avez terminé la configuration d’applications en libre-service, les utilisateurs peuvent accéder à leur [volet d’accès aux applications](https://myapps.microsoft.com/) et cliquer sur le bouton **+Ajouter** pour choisir les applications pour lesquelles vous avez activé l’accès en libre-service.</span><span class="sxs-lookup"><span data-stu-id="87737-175">Once you complete Self-service application configuration, users can navigate to their [Application Access Panel](https://myapps.microsoft.com/) and click the **+Add** button to find the apps to which you have enabled Self-service access.</span></span> <span data-ttu-id="87737-176">Les approbateurs d’entreprise reçoivent également une notification dans leur [volet d’accès aux applications](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="87737-176">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="87737-177">Vous pouvez leur envoyer une notification par e-mail les avertissant qu’un utilisateur a demandé l’accès à une application nécessitant leur approbation.</span><span class="sxs-lookup"><span data-stu-id="87737-177">You can enable an email notifying them when a user has requested access to an application that requires their approval.</span></span> 

<span data-ttu-id="87737-178">Ces approbations prennent en charge les flux de travail avec approbation unique uniquement, ce qui signifie que si vous spécifiez plusieurs approbateurs, chaque approbateur peut autoriser l’accès à l’application.</span><span class="sxs-lookup"><span data-stu-id="87737-178">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approver access to the application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="87737-179">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="87737-179">Next steps</span></span>
[<span data-ttu-id="87737-180">Fournir une authentification unique à vos applications avec le proxy d’application</span><span class="sxs-lookup"><span data-stu-id="87737-180">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
