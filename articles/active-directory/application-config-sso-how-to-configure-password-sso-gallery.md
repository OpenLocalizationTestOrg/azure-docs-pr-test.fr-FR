---
title: "aaaHow tooconfigure mot de passe l’authentification unique pour une application Azure AD galerie | Documents Microsoft"
description: "Comment tooconfigure une application pour sécuriser basée sur mot de passe de session unique lorsqu’il est déjà répertorié dans hello Galerie d’applications Azure AD"
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
ms.openlocfilehash: 7a93bff119b477d946368686fc2d9006ca2722a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="0b4bf-103">Comment tooconfigure le mot de passe sur l’authentification unique pour une application de la galerie d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b4bf-103">How tooconfigure password single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="0b4bf-104">Lorsque vous ajoutez une application à partir de hello [Galerie d’applications Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery), vous pouvez hello comment vous souhaitez que votre toosign d’utilisateurs dans l’application de toothat.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-104">When you add an application from hello [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery), you have hello choice of how you want your users toosign in toothat application.</span></span> <span data-ttu-id="0b4bf-105">Vous pouvez configurer ce choix à tout moment en sélectionnant hello **Single Sign-on** élément de navigation sur une Application d’entreprise Bonjour [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0b4bf-105">You can configure this choice at any time by selecting hello **Single Sign-on** navigation item on an Enterprise Application in hello [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="0b4bf-106">Un des tooyou disponibles des méthodes d’authentification unique de hello est hello [mot de passe Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) option.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-106">One of hello single sign-on methods available tooyou is hello [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) option.</span></span> <span data-ttu-id="0b4bf-107">Il s’agit d’un excellent moyen de tooget démarré l’intégration d’applications dans Azure AD rapidement et vous permet de :</span><span class="sxs-lookup"><span data-stu-id="0b4bf-107">This is a great way tooget started integrating applications into Azure AD quickly, and allows you to:</span></span>

-   <span data-ttu-id="0b4bf-108">Activer **l’authentification unique pour vos utilisateurs** en stocker en toute sécurité et en relisant les noms d’utilisateur et mots de passe pour l’application hello que vous avez intégré à Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b4bf-108">Enable **Single Sign-on for your users** by securely storing and replaying usernames and passwords for hello application you’ve integrated with Azure AD</span></span>

-   <span data-ttu-id="0b4bf-109">**Prend en charge les applications qui requièrent plusieurs champs de connexion** pour les applications qui nécessitent toosign champs plus que nom d’utilisateur et mot de passe dans</span><span class="sxs-lookup"><span data-stu-id="0b4bf-109">**Support applications that require multiple sign-in fields** for applications that require more than just username and password fields toosign in</span></span>

-   <span data-ttu-id="0b4bf-110">**Personnaliser les étiquettes hello** des champs d’entrée hello nom d’utilisateur et mot de passe, les utilisateurs voient sur hello [volet d’accès Application](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) lorsqu’ils entrent leurs informations d’identification</span><span class="sxs-lookup"><span data-stu-id="0b4bf-110">**Customize hello labels** of hello username and password input fields your users see on hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) when they enter their credentials</span></span>

-   <span data-ttu-id="0b4bf-111">Autoriser votre **utilisateurs** tooprovide leurs noms d’utilisateur et les mots de passe pour les comptes d’application existants qu’ils tapent dans manuellement sur hello [Application panneau d’accès](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span><span class="sxs-lookup"><span data-stu-id="0b4bf-111">Allow your **users** tooprovide their own usernames and passwords for any existing application accounts they are typing in manually on hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span></span>

-   <span data-ttu-id="0b4bf-112">Autoriser un **membre du groupe d’activités hello** toospecify hello noms et mots de passe assigné tooa utilisateur à l’aide de hello [accès à l’Application libre-service](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) fonctionnalité</span><span class="sxs-lookup"><span data-stu-id="0b4bf-112">Allow a **member of hello business group** toospecify hello usernames and passwords assigned tooa user by using hello [Self-Service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) feature</span></span>

-   <span data-ttu-id="0b4bf-113">Autoriser un **administrateur** toospecify hello noms et mots de passe utilisateur de tooa à l’aide des informations d’identification de la mise à jour hello fonction si [affectation d’un utilisateur de l’application tooan](#assign-a-user-to-an-application-directly)</span><span class="sxs-lookup"><span data-stu-id="0b4bf-113">Allow an **administrator** toospecify hello usernames and passwords assigned tooa user by using hello Update Credentials feature when [assigning a user tooan application](#assign-a-user-to-an-application-directly)</span></span>

-   <span data-ttu-id="0b4bf-114">Autoriser un **administrateur** toospecify hello partagé utilisateur ou mot de passe utilisé par un groupe de personnes à l’aide des informations d’identification de la mise à jour hello fonction si [attribution d’une application tooan de groupe](#assign-an-application-to-a-group-directly)</span><span class="sxs-lookup"><span data-stu-id="0b4bf-114">Allow an **administrator** toospecify hello shared username or password used by a group of people by using hello Update Credentials feature when [assigning a group tooan application](#assign-an-application-to-a-group-directly)</span></span>

<span data-ttu-id="0b4bf-115">Ci-dessous décrit comment vous pouvez activer [mot de passe Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) tooan application qui est déjà hello [Galerie d’applications Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span><span class="sxs-lookup"><span data-stu-id="0b4bf-115">Below describes how you can enable [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) tooan application that is already in hello [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="0b4bf-116">Vue d’ensemble des étapes requises</span><span class="sxs-lookup"><span data-stu-id="0b4bf-116">Overview of steps required</span></span>
<span data-ttu-id="0b4bf-117">tooconfigure une application à partir de la galerie d’Azure AD hello vous devez :</span><span class="sxs-lookup"><span data-stu-id="0b4bf-117">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="0b4bf-118">Ajouter une application à partir de la galerie d’Azure AD hello</span><span class="sxs-lookup"><span data-stu-id="0b4bf-118">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="0b4bf-119">Configurer une application hello pour mot de passe l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="0b4bf-119">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="0b4bf-120">Affecter tooa utilisateur de l’application hello ou un groupe</span><span class="sxs-lookup"><span data-stu-id="0b4bf-120">Assign hello application tooa user or a group</span></span>](#assign-the-application-to-a-user-or-a-group)

    -   [<span data-ttu-id="0b4bf-121">Attribuer un utilisateur de l’application tooan directement</span><span class="sxs-lookup"><span data-stu-id="0b4bf-121">Assign a user tooan application directly</span></span>](#assign-a-user-to-an-application-directly)

    -   [<span data-ttu-id="0b4bf-122">Affecter un groupe d’applications tooa directement</span><span class="sxs-lookup"><span data-stu-id="0b4bf-122">Assign an application tooa group directly</span></span>](#assign-an-application-to-a-group-directly)

## <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="0b4bf-123">Ajouter une application à partir de la galerie d’Azure AD hello</span><span class="sxs-lookup"><span data-stu-id="0b4bf-123">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="0b4bf-124">tooadd une application à partir de hello Galerie d’Azure AD, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="0b4bf-124">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="0b4bf-125">Ouvrez hello [Azure Portal](https://portal.azure.com) et connectez-vous en tant qu’un **administrateur Global** ou **Co-admin**</span><span class="sxs-lookup"><span data-stu-id="0b4bf-125">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="0b4bf-126">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-126">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="0b4bf-127">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-127">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="0b4bf-128">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-128">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="0b4bf-129">Cliquez sur hello **ajouter** bouton au coin supérieur droit de hello sur hello **des Applications d’entreprise** panneau</span><span class="sxs-lookup"><span data-stu-id="0b4bf-129">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="0b4bf-130">Bonjour **Entrez un nom** zone de texte à partir de hello **ajouter à partir de la galerie de hello** section, entrez un nom hello de l’application hello</span><span class="sxs-lookup"><span data-stu-id="0b4bf-130">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application</span></span>

7.  <span data-ttu-id="0b4bf-131">Sélectionnez hello application tooconfigure pour l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="0b4bf-131">Select hello application you want tooconfigure for single sign-on</span></span>

8.  <span data-ttu-id="0b4bf-132">Avant d’ajouter l’application hello, vous pouvez modifier son nom à partir de hello **nom** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-132">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="0b4bf-133">Cliquez sur **ajouter** bouton, l’application de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-133">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="0b4bf-134">Après une courte période, vous être Panneau de configuration de l’application en mesure de toosee hello.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-134">After a short period, you be able toosee hello application’s configuration blade.</span></span>

## <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="0b4bf-135">Configurer une application hello pour mot de passe l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="0b4bf-135">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="0b4bf-136">tooconfigure l’authentification unique pour une application, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="0b4bf-136">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="0b4bf-137">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**</span><span class="sxs-lookup"><span data-stu-id="0b4bf-137">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="0b4bf-138">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-138">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="0b4bf-139">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-139">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="0b4bf-140">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-140">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="0b4bf-141">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-141">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="0b4bf-142">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="0b4bf-142">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="0b4bf-143">Sélectionnez application hello tooconfigure l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="0b4bf-143">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="0b4bf-144">Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-144">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="0b4bf-145">Mode de sélection hello **mot de passe de session.**</span><span class="sxs-lookup"><span data-stu-id="0b4bf-145">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="0b4bf-146">[Affecter des utilisateurs toohello application](#assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="0b4bf-146">[Assign users toohello application](#assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="0b4bf-147">En outre, vous pouvez également fournir des informations d’identification pour le compte d’utilisateur de hello en sélectionnant les lignes hello d’utilisateurs de hello en cliquant sur **informations d’identification de la mise à jour** et en entrant hello username et password pour le compte d’utilisateurs de hello.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-147">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="0b4bf-148">Dans le cas contraire, les utilisateurs être invité à tooenter hello informations d’identification elles-mêmes lors du lancement.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-148">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="assign-a-user-tooan-application-directly"></a><span data-ttu-id="0b4bf-149">Attribuer un utilisateur de l’application tooan directement</span><span class="sxs-lookup"><span data-stu-id="0b4bf-149">Assign a user tooan application directly</span></span>

<span data-ttu-id="0b4bf-150">tooassign un ou plusieurs utilisateurs tooan application directement, comme suit hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="0b4bf-150">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="0b4bf-151">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="0b4bf-151">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="0b4bf-152">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-152">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="0b4bf-153">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-153">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="0b4bf-154">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-154">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="0b4bf-155">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-155">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="0b4bf-156">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="0b4bf-156">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="0b4bf-157">Sélectionnez l’application hello tooassign une liste des utilisateurs toofrom hello.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-157">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="0b4bf-158">Une fois le charge de l’application hello, cliquez sur **utilisateurs et groupes** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-158">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="0b4bf-159">Cliquez sur hello **ajouter** bouton par-dessus hello **utilisateurs et groupes** hello tooopen de liste **ajouter l’affectation** panneau.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-159">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="0b4bf-160">Cliquez sur hello **utilisateurs et groupes** sélecteur de hello **ajouter l’affectation** panneau.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-160">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="0b4bf-161">Type Bonjour **nom complet** ou **adresse de messagerie** d’utilisateur hello vous êtes intéressé par attribution dans hello **recherche par nom ou adresse de messagerie** zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-161">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="0b4bf-162">Placez le curseur sur hello **utilisateur** dans hello liste tooreveal un **case à cocher**.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-162">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="0b4bf-163">Cliquez sur tooadd de photo ou le logo de profil hello case à cocher suivante toohello l’utilisateur à votre toohello utilisateur **sélectionnés** liste.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-163">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="0b4bf-164">**Facultatif :** si vous souhaitez que trop**ajouter plusieurs utilisateurs**, type dans un autre **nom complet** ou **adresse de messagerie** dans hello **Rechercher par nom ou l’adresse de messagerie** zone de recherche, cliquez sur tooadd de case à cocher hello cette toohello utilisateur **sélectionnés** liste.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-164">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="0b4bf-165">Lorsque vous avez fini de sélectionner les utilisateurs, cliquez sur hello **sélectionnez** bouton tooadd les toohello la liste des toobe utilisateurs et groupes affectés toohello application.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-165">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="0b4bf-166">**Facultatif :** cliquez sur hello **sélectionner un rôle** sélecteur Bonjour **ajouter l’affectation** panneau tooselect un rôle aux utilisateurs de toohello tooassign que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-166">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="0b4bf-167">Cliquez sur hello **affecter** bouton tooassign hello application toohello les utilisateurs sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-167">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

## <a name="assign-an-application-tooa-group-directly"></a><span data-ttu-id="0b4bf-168">Affecter un groupe d’applications tooa directement</span><span class="sxs-lookup"><span data-stu-id="0b4bf-168">Assign an application tooa group directly</span></span>

<span data-ttu-id="0b4bf-169">tooassign un ou plusieurs groupes tooan application directement, hello suivez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="0b4bf-169">tooassign one or more groups tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="0b4bf-170">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="0b4bf-170">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="0b4bf-171">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-171">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="0b4bf-172">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-172">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="0b4bf-173">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-173">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="0b4bf-174">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-174">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="0b4bf-175">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="0b4bf-175">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="0b4bf-176">Sélectionnez l’application hello tooassign une liste des utilisateurs toofrom hello.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-176">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="0b4bf-177">Une fois le charge de l’application hello, cliquez sur **utilisateurs et groupes** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-177">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="0b4bf-178">Cliquez sur hello **ajouter** bouton par-dessus hello **utilisateurs et groupes** hello tooopen de liste **ajouter l’affectation** panneau.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-178">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="0b4bf-179">Cliquez sur hello **utilisateurs et groupes** sélecteur de hello **ajouter l’affectation** panneau.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-179">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="0b4bf-180">Type Bonjour **nom de groupe complète** groupe hello vous êtes intéressé par attribution dans hello **recherche par nom ou adresse de messagerie** zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-180">Type in hello **full group name** of hello group you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="0b4bf-181">Placez le curseur sur hello **groupe** dans hello liste tooreveal un **case à cocher**.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-181">Hover over hello **group** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="0b4bf-182">Cliquez sur tooadd de photo ou le logo de profil de hello case à cocher toohello groupe suivant votre toohello utilisateur **sélectionnés** liste.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-182">Click hello checkbox next toohello group’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="0b4bf-183">**Facultatif :** si vous souhaitez que trop**ajouter plusieurs groupes**, type dans un autre **nom de groupe complète** dans hello **recherche par nom ou adresse de messagerie** zone de recherche, Cliquez sur tooadd de case à cocher hello toohello de ce groupe **sélectionnés** liste.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-183">**Optional:** If you would like too**add more than one group**, type in another **full group name** into hello **Search by name or email address** search box, and click hello checkbox tooadd this group toohello **Selected** list.</span></span>

13. <span data-ttu-id="0b4bf-184">Lorsque vous avez fini de sélectionner les groupes, cliquez sur hello **sélectionnez** bouton tooadd les toohello la liste des toobe utilisateurs et groupes affectés toohello application.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-184">When you are finished selecting groups, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="0b4bf-185">**Facultatif :** cliquez sur hello **sélectionner un rôle** sélecteur Bonjour **ajouter l’affectation** panneau tooselect un toohello de tooassign rôle groupes que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-185">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello groups you have selected.</span></span>

15. <span data-ttu-id="0b4bf-186">Cliquez sur hello **affecter** bouton tooassign hello application toohello les groupes sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-186">Click hello **Assign** button tooassign hello application toohello selected groups.</span></span>

<span data-ttu-id="0b4bf-187">Après une courte période, les utilisateurs de hello que vous avez sélectionné est en mesure de toolaunch ces applications dans hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="0b4bf-187">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0b4bf-188">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0b4bf-188">Next steps</span></span>
[<span data-ttu-id="0b4bf-189">Fournissent des applications de tooyour de l’authentification unique avec le Proxy d’Application</span><span class="sxs-lookup"><span data-stu-id="0b4bf-189">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
