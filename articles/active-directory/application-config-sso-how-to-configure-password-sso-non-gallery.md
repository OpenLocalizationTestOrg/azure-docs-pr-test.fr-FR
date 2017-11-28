---
title: aaaHow tooconfigure mot de passe de session unique pour un applicationn non-galerie | Documents Microsoft
description: "Comment tooconfigure une application non-Galerie personnalisée pour sécuriser basée sur mot de passe de session unique lorsqu’il n’est pas répertorié dans hello Galerie d’applications Azure AD"
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
ms.openlocfilehash: e3d0e658f792a0a63110a198811edc66acd6ccf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="a931e-103">Comment tooconfigure le mot de passe sur l’authentification unique pour une application non-galerie</span><span class="sxs-lookup"><span data-stu-id="a931e-103">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="a931e-104">En outre toohello choix trouvé dans la galerie d’applications hello Azure AD, vous avez également hello option tooadd un **application non-gallery** lorsque application hello souhaité n’y figure pas.</span><span class="sxs-lookup"><span data-stu-id="a931e-104">In addition toohello choices found within hello Azure AD Application Gallery, you also have hello option tooadd a **non-gallery application** when hello application you want is not listed there.</span></span> <span data-ttu-id="a931e-105">Grâce à cette fonctionnalité, vous pouvez ajouter n’importe quelle application qui existe déjà dans votre organisation, ou n’importe quelle application tiers que vous pouvez utiliser à partir d’un fournisseur qui n’est pas déjà partie de hello [Galerie d’applications Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span><span class="sxs-lookup"><span data-stu-id="a931e-105">Using this capability, you can add any application that already exists in your organization, or any third-party application that you might use from a vendor who is not already part of hello [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span></span>

<span data-ttu-id="a931e-106">Une fois que vous ajoutez une application non-galerie, vous pouvez ensuite configurer hello unique méthode d’authentification utilise de cette application en sélectionnant hello **Single Sign-on** élément de navigation sur une Application d’entreprise Bonjour [portail Azure ](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a931e-106">Once you add a non-gallery application, you can then configure hello Single sign-on method this application uses by selecting hello **Single Sign-on** navigation item on an Enterprise Application in hello [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="a931e-107">Un des hello Single Sign-on méthodes tooyou disponible est hello [mot de passe Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) option.</span><span class="sxs-lookup"><span data-stu-id="a931e-107">One of hello Single Sign-on methods available tooyou is hello [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) option.</span></span> <span data-ttu-id="a931e-108">Avec hello **ajouter une application non-galerie** expérience, vous pouvez intégrer n’importe quelle application qui restitue un nom d’utilisateur basé sur HTML et de mot de passe d’entrée de champ, même si elle n’est pas dans notre ensemble d’applications pré-intégrées.</span><span class="sxs-lookup"><span data-stu-id="a931e-108">With hello **add a non-gallery application** experience, you can integrate any application that renders an HTML-based username and password input field, even if it is not in our set of pre-integrated applications.</span></span>

<span data-ttu-id="a931e-109">Hello cela fonctionne consiste en une page de capture de données technologie faisant partie de hello extension volet d’accès qui permet de tooauto-détecte les champs d’entrée de nom d’utilisateur et mot de passe, de les stocker en toute sécurité de votre instance d’application spécifique.</span><span class="sxs-lookup"><span data-stu-id="a931e-109">hello way this works is by a page scraping technology that is part of hello Access Panel extension that allows us tooauto-detect username and password input fields, store them securely for your specific application instance.</span></span> <span data-ttu-id="a931e-110">Puis relire en toute sécurité les noms d’utilisateur et les champs de toothose les mots de passe lorsqu’un utilisateur navigue application toothat sur le volet d’accès application hello.</span><span class="sxs-lookup"><span data-stu-id="a931e-110">Then securely replay usernames and passwords toothose fields when a user navigates toothat application on hello application access panel.</span></span>

<span data-ttu-id="a931e-111">Il s’agit d’un excellent moyen de tooget démarré l’intégration de tout type d’application dans Azure AD rapidement et vous permet de :</span><span class="sxs-lookup"><span data-stu-id="a931e-111">This is a great way tooget started integrating any kind of application into Azure AD quickly, and allows you to:</span></span>

-   <span data-ttu-id="a931e-112">Intégrer **n’importe quelle application dans Bonjour** avec votre client Azure AD, pour autant qu’il restitue un champ d’entrée HTML nom d’utilisateur et mot de passe</span><span class="sxs-lookup"><span data-stu-id="a931e-112">Integrate **any application in hello world** with your Azure AD tenant, so long as it renders an HTML username and password input field</span></span>

-   <span data-ttu-id="a931e-113">Activer **l’authentification unique pour vos utilisateurs** en stocker en toute sécurité et en relisant les noms d’utilisateur et mots de passe pour l’application hello que vous avez intégré à Azure AD</span><span class="sxs-lookup"><span data-stu-id="a931e-113">Enable **Single Sign-on for your users** by securely storing and replaying usernames and passwords for hello application you’ve integrated with Azure AD</span></span>

-   <span data-ttu-id="a931e-114">**Détection automatique d’entrée** des champs pour n’importe quelle application et vous toomanually détecter ces champs à l’aide de hello Extension volet navigateur d’accès, en cas de détection automatique ne trouve pas les</span><span class="sxs-lookup"><span data-stu-id="a931e-114">**Auto-detect input** fields for any application and allow you toomanually detect those fields using hello Access Panel Browser Extension, in case auto-detection does not find them</span></span>

-   <span data-ttu-id="a931e-115">**Prend en charge les applications qui requièrent plusieurs champs de connexion** pour les applications qui nécessitent toosign champs plus que nom d’utilisateur et mot de passe dans</span><span class="sxs-lookup"><span data-stu-id="a931e-115">**Support applications that require multiple sign-in fields** for applications that require more than just username and password fields toosign in</span></span>

-   <span data-ttu-id="a931e-116">**Personnaliser les étiquettes hello** des champs d’entrée hello nom d’utilisateur et mot de passe, les utilisateurs voient sur hello [volet d’accès Application](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) lorsqu’ils entrent leurs informations d’identification</span><span class="sxs-lookup"><span data-stu-id="a931e-116">**Customize hello labels** of hello username and password input fields your users see on hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) when they enter their credentials</span></span>

-   <span data-ttu-id="a931e-117">Autoriser votre **utilisateurs** tooprovide leurs noms d’utilisateur et les mots de passe pour les comptes d’application existants qu’ils tapent dans manuellement sur hello [Application panneau d’accès](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span><span class="sxs-lookup"><span data-stu-id="a931e-117">Allow your **users** tooprovide their own usernames and passwords for any existing application accounts they are typing in manually on hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span></span>

-   <span data-ttu-id="a931e-118">Autoriser un **membre du groupe d’activités hello** toospecify hello noms et mots de passe assigné tooa utilisateur à l’aide de hello [accès à l’Application libre-service](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) fonctionnalité</span><span class="sxs-lookup"><span data-stu-id="a931e-118">Allow a **member of hello business group** toospecify hello usernames and passwords assigned tooa user by using hello [Self-Service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) feature</span></span>

-   <span data-ttu-id="a931e-119">Autoriser un **administrateur** toospecify hello noms et mots de passe utilisateur de tooa à l’aide des informations d’identification de la mise à jour hello fonction si [affectation d’un utilisateur de l’application tooan](#_How_to_configure_1)</span><span class="sxs-lookup"><span data-stu-id="a931e-119">Allow an **administrator** toospecify hello usernames and passwords assigned tooa user by using hello Update Credentials feature when [assigning a user tooan application](#_How_to_configure_1)</span></span>

-   <span data-ttu-id="a931e-120">Autoriser un **administrateur** toospecify hello partagé utilisateur ou mot de passe utilisé par un groupe de personnes à l’aide des informations d’identification de la mise à jour hello fonction si [attribution d’une application tooan de groupe](#assign-an-application-to-a-group-directly)</span><span class="sxs-lookup"><span data-stu-id="a931e-120">Allow an **administrator** toospecify hello shared username or password used by a group of people by using hello Update Credentials feature when [assigning a group tooan application](#assign-an-application-to-a-group-directly)</span></span>

<span data-ttu-id="a931e-121">Ci-dessous décrit comment vous pouvez activer [mot de passe Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) application tooany que vous ajoutez à l’aide de hello **ajouter une application non-galerie** rencontrer.</span><span class="sxs-lookup"><span data-stu-id="a931e-121">Below describes how you can enable [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) tooany application that you add using hello **add a non-gallery application** experience.</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="a931e-122">Vue d’ensemble des étapes requises</span><span class="sxs-lookup"><span data-stu-id="a931e-122">Overview of steps required</span></span>

<span data-ttu-id="a931e-123">tooconfigure une application à partir de la galerie d’Azure AD hello vous devez :</span><span class="sxs-lookup"><span data-stu-id="a931e-123">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="a931e-124">Ajouter une application ne figurant pas dans la galerie</span><span class="sxs-lookup"><span data-stu-id="a931e-124">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="a931e-125">Configurer une application hello pour mot de passe l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="a931e-125">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="a931e-126">Affecter tooa utilisateur de l’application hello ou un groupe</span><span class="sxs-lookup"><span data-stu-id="a931e-126">Assign hello application tooa user or a group</span></span>](#assign-the-application-to-a-user-or-a-group)

    -   [<span data-ttu-id="a931e-127">Attribuer un utilisateur de l’application tooan directement</span><span class="sxs-lookup"><span data-stu-id="a931e-127">Assign a user tooan application directly</span></span>](#assign-a-user-to-an-application-directly)

    -   [<span data-ttu-id="a931e-128">Affecter un groupe d’applications tooa directement</span><span class="sxs-lookup"><span data-stu-id="a931e-128">Assign an application tooa group directly</span></span>](#assign-an-application-to-a-group-directly)

## <a name="add-a-non-gallery-application"></a><span data-ttu-id="a931e-129">Ajouter une application ne figurant pas dans la galerie</span><span class="sxs-lookup"><span data-stu-id="a931e-129">Add a non-gallery application</span></span>

<span data-ttu-id="a931e-130">tooadd une application à partir de hello Galerie d’Azure AD, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="a931e-130">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="a931e-131">Ouvrez hello [Azure Portal](https://portal.azure.com) et connectez-vous en tant qu’un **administrateur Global** ou **Co-admin**</span><span class="sxs-lookup"><span data-stu-id="a931e-131">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="a931e-132">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="a931e-132">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a931e-133">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="a931e-133">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a931e-134">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a931e-134">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a931e-135">Cliquez sur hello **ajouter** bouton au coin supérieur droit de hello sur hello **des Applications d’entreprise** panneau</span><span class="sxs-lookup"><span data-stu-id="a931e-135">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="a931e-136">Cliquez sur **Application ne figurant pas dans la galerie**.</span><span class="sxs-lookup"><span data-stu-id="a931e-136">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="a931e-137">Entrez le nom hello de votre application Bonjour **nom** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="a931e-137">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="a931e-138">Sélectionnez **Ajouter.**</span><span class="sxs-lookup"><span data-stu-id="a931e-138">Select **Add.**</span></span>

<span data-ttu-id="a931e-139">Après une courte période, vous être Panneau de configuration de l’application en mesure de toosee hello.</span><span class="sxs-lookup"><span data-stu-id="a931e-139">After a short period, you be able toosee hello application’s configuration blade.</span></span>

## <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="a931e-140">Configurer une application hello pour mot de passe l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="a931e-140">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="a931e-141">tooconfigure l’authentification unique pour une application, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="a931e-141">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="a931e-142">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**</span><span class="sxs-lookup"><span data-stu-id="a931e-142">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="a931e-143">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="a931e-143">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a931e-144">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="a931e-144">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a931e-145">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a931e-145">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a931e-146">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="a931e-146">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="a931e-147">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="a931e-147">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="a931e-148">Sélectionnez l’application hello tooconfigure l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="a931e-148">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="a931e-149">Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="a931e-149">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="a931e-150">Mode de sélection hello **mot de passe de session.**</span><span class="sxs-lookup"><span data-stu-id="a931e-150">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="a931e-151">Entrez hello **URL de connexion**.</span><span class="sxs-lookup"><span data-stu-id="a931e-151">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="a931e-152">Il s’agit d’URL de hello où les utilisateurs entrent leur nom d’utilisateur et mot de passe des toosign dans pour.</span><span class="sxs-lookup"><span data-stu-id="a931e-152">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="a931e-153">Vérifiez la connexion hello dans les champs est visibles à l’URL de hello.</span><span class="sxs-lookup"><span data-stu-id="a931e-153">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="a931e-154">Affecter des utilisateurs toohello application.</span><span class="sxs-lookup"><span data-stu-id="a931e-154">Assign users toohello application.</span></span>

11. <span data-ttu-id="a931e-155">En outre, vous pouvez également fournir des informations d’identification pour le compte d’utilisateur de hello en sélectionnant les lignes hello d’utilisateurs de hello en cliquant sur **informations d’identification de la mise à jour** et en entrant hello username et password pour le compte d’utilisateurs de hello.</span><span class="sxs-lookup"><span data-stu-id="a931e-155">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="a931e-156">Dans le cas contraire, les utilisateurs être invité à tooenter hello informations d’identification elles-mêmes lors du lancement.</span><span class="sxs-lookup"><span data-stu-id="a931e-156">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="assign-a-user-tooan-application-directly"></a><span data-ttu-id="a931e-157">Attribuer un utilisateur de l’application tooan directement</span><span class="sxs-lookup"><span data-stu-id="a931e-157">Assign a user tooan application directly</span></span>

<span data-ttu-id="a931e-158">tooassign un ou plusieurs utilisateurs tooan application directement, comme suit hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="a931e-158">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="a931e-159">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="a931e-159">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="a931e-160">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="a931e-160">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a931e-161">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="a931e-161">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a931e-162">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a931e-162">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a931e-163">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="a931e-163">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="a931e-164">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="a931e-164">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="a931e-165">Sélectionnez l’application hello tooassign une liste des utilisateurs toofrom hello.</span><span class="sxs-lookup"><span data-stu-id="a931e-165">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="a931e-166">Une fois le charge de l’application hello, cliquez sur **utilisateurs et groupes** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="a931e-166">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="a931e-167">Cliquez sur hello **ajouter** bouton par-dessus hello **utilisateurs et groupes** hello tooopen de liste **ajouter l’affectation** panneau.</span><span class="sxs-lookup"><span data-stu-id="a931e-167">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="a931e-168">Cliquez sur hello **utilisateurs et groupes** sélecteur de hello **ajouter l’affectation** panneau.</span><span class="sxs-lookup"><span data-stu-id="a931e-168">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="a931e-169">Type Bonjour **nom complet** ou **adresse de messagerie** d’utilisateur hello vous êtes intéressé par attribution dans hello **recherche par nom ou adresse de messagerie** zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="a931e-169">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="a931e-170">Placez le curseur sur hello **utilisateur** dans hello liste tooreveal un **case à cocher**.</span><span class="sxs-lookup"><span data-stu-id="a931e-170">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="a931e-171">Cliquez sur tooadd de photo ou le logo de profil hello case à cocher suivante toohello l’utilisateur à votre toohello utilisateur **sélectionnés** liste.</span><span class="sxs-lookup"><span data-stu-id="a931e-171">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="a931e-172">**Facultatif :** si vous souhaitez que trop**ajouter plusieurs utilisateurs**, type dans un autre **nom complet** ou **adresse de messagerie** dans hello **Rechercher par nom ou l’adresse de messagerie** zone de recherche, cliquez sur tooadd de case à cocher hello cette toohello utilisateur **sélectionnés** liste.</span><span class="sxs-lookup"><span data-stu-id="a931e-172">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="a931e-173">Lorsque vous avez fini de sélectionner les utilisateurs, cliquez sur hello **sélectionnez** bouton tooadd les toohello la liste des toobe utilisateurs et groupes affectés toohello application.</span><span class="sxs-lookup"><span data-stu-id="a931e-173">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="a931e-174">**Facultatif :** cliquez sur hello **sélectionner un rôle** sélecteur Bonjour **ajouter l’affectation** panneau tooselect un rôle aux utilisateurs de toohello tooassign que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="a931e-174">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="a931e-175">Cliquez sur hello **affecter** bouton tooassign hello application toohello les utilisateurs sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="a931e-175">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

## <a name="assign-an-application-tooa-group-directly"></a><span data-ttu-id="a931e-176">Affecter un groupe d’applications tooa directement</span><span class="sxs-lookup"><span data-stu-id="a931e-176">Assign an application tooa group directly</span></span>

<span data-ttu-id="a931e-177">tooassign un ou plusieurs groupes tooan application directement, hello suivez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="a931e-177">tooassign one or more groups tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="a931e-178">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="a931e-178">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="a931e-179">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="a931e-179">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a931e-180">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="a931e-180">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a931e-181">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a931e-181">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a931e-182">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="a931e-182">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="a931e-183">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="a931e-183">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="a931e-184">Sélectionnez l’application hello tooassign une liste des utilisateurs toofrom hello.</span><span class="sxs-lookup"><span data-stu-id="a931e-184">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="a931e-185">Une fois le charge de l’application hello, cliquez sur **utilisateurs et groupes** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="a931e-185">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="a931e-186">Cliquez sur hello **ajouter** bouton par-dessus hello **utilisateurs et groupes** hello tooopen de liste **ajouter l’affectation** panneau.</span><span class="sxs-lookup"><span data-stu-id="a931e-186">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="a931e-187">Cliquez sur hello **utilisateurs et groupes** sélecteur de hello **ajouter l’affectation** panneau.</span><span class="sxs-lookup"><span data-stu-id="a931e-187">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="a931e-188">Type Bonjour **nom de groupe complète** groupe hello vous êtes intéressé par attribution dans hello **recherche par nom ou adresse de messagerie** zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="a931e-188">Type in hello **full group name** of hello group you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="a931e-189">Placez le curseur sur hello **groupe** dans hello liste tooreveal un **case à cocher**.</span><span class="sxs-lookup"><span data-stu-id="a931e-189">Hover over hello **group** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="a931e-190">Cliquez sur tooadd de photo ou le logo de profil de hello case à cocher toohello groupe suivant votre toohello utilisateur **sélectionnés** liste.</span><span class="sxs-lookup"><span data-stu-id="a931e-190">Click hello checkbox next toohello group’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="a931e-191">**Facultatif :** si vous souhaitez que trop**ajouter plusieurs groupes**, type dans un autre **nom de groupe complète** dans hello **recherche par nom ou adresse de messagerie** zone de recherche, Cliquez sur tooadd de case à cocher hello toohello de ce groupe **sélectionnés** liste.</span><span class="sxs-lookup"><span data-stu-id="a931e-191">**Optional:** If you would like too**add more than one group**, type in another **full group name** into hello **Search by name or email address** search box, and click hello checkbox tooadd this group toohello **Selected** list.</span></span>

13. <span data-ttu-id="a931e-192">Lorsque vous avez fini de sélectionner les groupes, cliquez sur hello **sélectionnez** bouton tooadd les toohello la liste des toobe utilisateurs et groupes affectés toohello application.</span><span class="sxs-lookup"><span data-stu-id="a931e-192">When you are finished selecting groups, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="a931e-193">**Facultatif :** cliquez sur hello **sélectionner un rôle** sélecteur Bonjour **ajouter l’affectation** panneau tooselect un toohello de tooassign rôle groupes que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="a931e-193">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello groups you have selected.</span></span>

15. <span data-ttu-id="a931e-194">Cliquez sur hello **affecter** bouton tooassign hello application toohello les groupes sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="a931e-194">Click hello **Assign** button tooassign hello application toohello selected groups.</span></span>

<span data-ttu-id="a931e-195">Après une courte période, les utilisateurs de hello que vous avez sélectionné est en mesure de toolaunch ces applications dans hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="a931e-195">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a931e-196">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a931e-196">Next steps</span></span>
[<span data-ttu-id="a931e-197">Fournissent des applications de tooyour de l’authentification unique avec le Proxy d’Application</span><span class="sxs-lookup"><span data-stu-id="a931e-197">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
