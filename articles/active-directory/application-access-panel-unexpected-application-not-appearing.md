---
title: "aaaAn affecté application n’apparaît pas dans le volet d’accès hello | Documents Microsoft"
description: "Résoudre les problèmes de la raison pour laquelle une application n’apparaît pas dans le volet d’accès de hello"
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
ms.reviwer: japere
ms.openlocfilehash: 089883f406267df4552c7fc991883f335ad49fd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="an-assigned-application-is-not-appearing-on-hello-access-panel"></a><span data-ttu-id="c5c55-103">Une application attribuée n’apparaît pas dans le volet d’accès hello</span><span class="sxs-lookup"><span data-stu-id="c5c55-103">An assigned application is not appearing on hello access panel</span></span>

<span data-ttu-id="c5c55-104">Hello volet d’accès est un portail web qui permet à un utilisateur avec un travail ou compte scolaire dans Azure Active Directory (Azure AD) tooview et démarrer les applications cloud qui hello administrateur Azure AD lui a accordé l’accès à.</span><span class="sxs-lookup"><span data-stu-id="c5c55-104">hello Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) tooview and start cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="c5c55-105">Ces applications sont configurées pour le compte d’utilisateur hello dans le portail Azure AD de hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-105">These applications are configured on behalf of hello user in hello Azure AD portal.</span></span> <span data-ttu-id="c5c55-106">application Hello doit être configurée correctement et toohello attribué ou un utilisateur de hello de groupe est un membre de l’application de hello toosee Bonjour panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="c5c55-106">hello application must be configured properly and assigned toohello user or a group hello user is a member of toosee hello application in hello Access Panel.</span></span>

<span data-ttu-id="c5c55-107">type Hello d’applications peut s’agir d’un utilisateur se situent dans hello suivant des catégories :</span><span class="sxs-lookup"><span data-stu-id="c5c55-107">hello type of apps a user may be seeing fall in hello following categories:</span></span>

-   <span data-ttu-id="c5c55-108">Applications Office 365</span><span class="sxs-lookup"><span data-stu-id="c5c55-108">Office 365 Applications</span></span>

-   <span data-ttu-id="c5c55-109">Applications Microsoft et tierces configurées avec l’authentification unique (SSO) basée sur la fédération</span><span class="sxs-lookup"><span data-stu-id="c5c55-109">Microsoft and third-party applications configured with federation-based SSO</span></span>

-   <span data-ttu-id="c5c55-110">Applications à authentification unique (SSO) par mot de passe</span><span class="sxs-lookup"><span data-stu-id="c5c55-110">Password-based SSO applications</span></span>

-   <span data-ttu-id="c5c55-111">Applications avec solutions d’authentification unique (SSO) existantes</span><span class="sxs-lookup"><span data-stu-id="c5c55-111">Applications with existing SSO solutions</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="c5c55-112">Général émet toocheck tout d’abord</span><span class="sxs-lookup"><span data-stu-id="c5c55-112">General issues toocheck first</span></span>

-   <span data-ttu-id="c5c55-113">Si une application vient d’être ajoutée tooa utilisateur, réessayez toosign et l’extraction dans le volet d’accès de l’utilisateur hello après quelques minutes toosee si l’application hello est ajoutée.</span><span class="sxs-lookup"><span data-stu-id="c5c55-113">If an application was just added tooa user, try toosign in and out again into hello user’s Access Panel after a few minutes toosee if hello application is added.</span></span>

-   <span data-ttu-id="c5c55-114">Si une licence vient d’être supprimée d’un utilisateur ou un utilisateur hello le groupe est que membre de ce peut prendre beaucoup de temps, selon la taille de hello et la complexité du groupe hello pour toobe des modifications apportée.</span><span class="sxs-lookup"><span data-stu-id="c5c55-114">If a license was just removed from a user or group hello user is a member of this may take a long time, depending on hello size and complexity of hello group for changes toobe made.</span></span> <span data-ttu-id="c5c55-115">Prévoyez du temps supplémentaire avant de vous connecter en hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="c5c55-115">Allow for extra time before signing into hello Access Panel.</span></span>

## <a name="problems-related-tooapplication-configuration"></a><span data-ttu-id="c5c55-116">Configuration de tooapplication connexes des problèmes</span><span class="sxs-lookup"><span data-stu-id="c5c55-116">Problems related tooapplication configuration</span></span>

<span data-ttu-id="c5c55-117">Une application n’apparaît peut-être pas dans le volet d’accès d’un utilisateur en raison d’une mauvaise configuration.</span><span class="sxs-lookup"><span data-stu-id="c5c55-117">An application may not be appearing in a user’s Access Panel because it is not configured properly.</span></span> <span data-ttu-id="c5c55-118">Voici quelques méthodes que vous pourrez résoudre les problèmes de configuration connexes tooapplication de problèmes :</span><span class="sxs-lookup"><span data-stu-id="c5c55-118">Below are some ways you can troubleshoot issues related tooapplication configuration:</span></span>

-   [<span data-ttu-id="c5c55-119">Comment tooconfigure fédéré l’authentification unique pour une application de la galerie Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5c55-119">How tooconfigure federated single sign-on for an Azure AD gallery application</span></span>](#how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application)

-   [<span data-ttu-id="c5c55-120">Comment tooconfigure fédéré l’authentification unique pour une application non-galerie</span><span class="sxs-lookup"><span data-stu-id="c5c55-120">How tooconfigure federated single sign-on for a non-gallery application</span></span>](#how-to-configure-federated-single-sign-on-for-a-non-gallery-application)

-   [<span data-ttu-id="c5c55-121">Comment tooconfigure un mot de passe une seule application d’authentification pour une application de la galerie Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5c55-121">How tooconfigure a password single sign-on application for an Azure AD gallery application</span></span>](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

-   [<span data-ttu-id="c5c55-122">Comment tooconfigure un mot de passe une seule application d’authentification pour une application non-galerie</span><span class="sxs-lookup"><span data-stu-id="c5c55-122">How tooconfigure a password single sign-on application for a non-gallery application</span></span>](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

### <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="c5c55-123">Comment tooconfigure fédéré l’authentification unique pour une application de la galerie Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5c55-123">How tooconfigure federated single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="c5c55-124">Toutes les applications dans la galerie d’Azure AD hello activé avec la fonctionnalité Enterprise Single Sign-On a un didacticiel pas à pas disponible.</span><span class="sxs-lookup"><span data-stu-id="c5c55-124">All applications in hello Azure AD gallery enabled with Enterprise Single Sign-On capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="c5c55-125">Vous pouvez accéder à hello [liste des didacticiels sur la façon de toointegrate les applications SaaS avec Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) pour obtenir une aide pas à pas détaillé.</span><span class="sxs-lookup"><span data-stu-id="c5c55-125">You can access hello [List of tutorials on how toointegrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

<span data-ttu-id="c5c55-126">tooconfigure une application à partir de la galerie d’Azure AD hello vous devez :</span><span class="sxs-lookup"><span data-stu-id="c5c55-126">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="c5c55-127">Ajouter une application à partir de la galerie d’Azure AD hello</span><span class="sxs-lookup"><span data-stu-id="c5c55-127">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="c5c55-128">Configurer les valeurs de métadonnées de l’application hello dans Azure AD (URL de réponse d’URL, identificateur, authentification)</span><span class="sxs-lookup"><span data-stu-id="c5c55-128">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="c5c55-129">Identificateur de l’utilisateur de sélectionner et ajouter l’application utilisateur attributs toobe envoyé toohello</span><span class="sxs-lookup"><span data-stu-id="c5c55-129">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="c5c55-130">Récupérer le certificat et les métadonnées Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5c55-130">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="c5c55-131">Configurer les valeurs de métadonnées Azure AD dans l’application hello (authentification URL, l’émetteur, URL de déconnexion et un certificat)</span><span class="sxs-lookup"><span data-stu-id="c5c55-131">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

#### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="c5c55-132">Ajouter une application à partir de la galerie d’Azure AD hello</span><span class="sxs-lookup"><span data-stu-id="c5c55-132">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="c5c55-133">tooadd une application à partir de hello Galerie d’Azure AD, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c5c55-133">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="c5c55-134">Ouvrez hello [Azure Portal](https://portal.azure.com) et connectez-vous en tant qu’un **administrateur Global** ou **Co-admin**</span><span class="sxs-lookup"><span data-stu-id="c5c55-134">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="c5c55-135">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-135">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c5c55-136">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="c5c55-136">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c5c55-137">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c5c55-137">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="c5c55-138">Cliquez sur hello **ajouter** bouton au coin supérieur droit de hello sur hello **des Applications d’entreprise** panneau.</span><span class="sxs-lookup"><span data-stu-id="c5c55-138">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="c5c55-139">Bonjour **Entrez un nom** zone de texte à partir de hello **ajouter à partir de la galerie de hello** section, entrez un nom hello de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-139">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="c5c55-140">Sélectionnez hello application tooconfigure pour l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c5c55-140">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="c5c55-141">Avant d’ajouter l’application hello, vous pouvez modifier son nom à partir de hello **nom** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="c5c55-141">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="c5c55-142">Cliquez sur **ajouter** bouton, l’application de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="c5c55-142">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="c5c55-143">Après une courte période, vous être Panneau de configuration de l’application en mesure de toosee hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-143">After a short period, you be able toosee hello application’s configuration blade.</span></span>

#### <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="c5c55-144">Configurer l’authentification unique pour une application à partir de la galerie d’Azure AD hello</span><span class="sxs-lookup"><span data-stu-id="c5c55-144">Configure single sign-on for an application from hello Azure AD gallery</span></span>

<span data-ttu-id="c5c55-145">tooconfigure l’authentification unique pour une application, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c5c55-145">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="c5c55-146">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**</span><span class="sxs-lookup"><span data-stu-id="c5c55-146">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="c5c55-147">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-147">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c5c55-148">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="c5c55-148">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c5c55-149">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c5c55-149">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="c5c55-150">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="c5c55-150">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="c5c55-151">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="c5c55-151">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="c5c55-152">Sélectionnez l’application hello tooconfigure l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c5c55-152">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="c5c55-153">Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-153">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="c5c55-154">Sélectionnez **SAML-authentification** de hello **Mode** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="c5c55-154">Select **SAML-based Sign-on** from hello **Mode** dropdown.</span></span>

9.  <span data-ttu-id="c5c55-155">Entrez les valeurs hello requis dans **URL et domaine.**</span><span class="sxs-lookup"><span data-stu-id="c5c55-155">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="c5c55-156">Vous devez obtenir ces valeurs à partir du fournisseur de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-156">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="c5c55-157">application de hello tooconfigure en tant que l’authentification unique initiée par SP, hello signe sur l’URL, il est obligatoire.</span><span class="sxs-lookup"><span data-stu-id="c5c55-157">tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span> <span data-ttu-id="c5c55-158">Pour certaines applications, hello identificateur est également une valeur requise.</span><span class="sxs-lookup"><span data-stu-id="c5c55-158">For some applications, hello Identifier is also a required value.</span></span>

   2. <span data-ttu-id="c5c55-159">application hello tooconfigure initiées IdP, hello URL de réponse qu’il est obligatoire.</span><span class="sxs-lookup"><span data-stu-id="c5c55-159">tooconfigure hello application as IdP-initiated SSO, hello Reply URL it’s a required value.</span></span> <span data-ttu-id="c5c55-160">Pour certaines applications, hello identificateur est également une valeur requise.</span><span class="sxs-lookup"><span data-stu-id="c5c55-160">For some applications, hello Identifier is also a required value.</span></span>

10. <span data-ttu-id="c5c55-161">**Facultatif :** cliquez sur **afficher les paramètres d’URL avancés** si vous souhaitez que les valeurs toosee hello non requis.</span><span class="sxs-lookup"><span data-stu-id="c5c55-161">**Optional:** click **Show advanced URL settings** if you want toosee hello non-required values.</span></span>

11. <span data-ttu-id="c5c55-162">Bonjour **attributs utilisateur**, sélectionnez hello un identificateur unique pour vos utilisateurs Bonjour **identificateur de l’utilisateur** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="c5c55-162">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="c5c55-163">**Facultatif :** cliquez sur **afficher et modifier tous les autres attributs utilisateur** tooedit hello attributs application de toohello toobe envoyé dans un jeton SAML de hello lorsque l’utilisateur se connecter.</span><span class="sxs-lookup"><span data-stu-id="c5c55-163">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="c5c55-164">tooadd un attribut :</span><span class="sxs-lookup"><span data-stu-id="c5c55-164">tooadd an attribute:</span></span>

   1. <span data-ttu-id="c5c55-165">Cliquez sur **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="c5c55-165">click **Add attribute**.</span></span> <span data-ttu-id="c5c55-166">Entrez hello **nom** et Bonjour sélectionnez Bonjour **valeur** à partir de la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-166">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="c5c55-167">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="c5c55-167">click **Save.**</span></span> <span data-ttu-id="c5c55-168">Vous consultez hello nouvel attribut dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-168">You see hello new attribute in hello table.</span></span>

13. <span data-ttu-id="c5c55-169">Cliquez sur **configurer &lt;nom de l’application&gt;**  documentation tooaccess sur la tooconfigure l’authentification unique dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-169">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="c5c55-170">En outre, vous a hello les URL des métadonnées et le certificat requis toosetup SSO avec l’application hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-170">Also, you has hello metadata URLs and certificate required toosetup SSO with hello application.</span></span>

14. <span data-ttu-id="c5c55-171">Cliquez sur **enregistrer** configuration de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="c5c55-171">click **Save** toosave hello configuration.</span></span>

15. <span data-ttu-id="c5c55-172">Affecter des utilisateurs toohello application.</span><span class="sxs-lookup"><span data-stu-id="c5c55-172">Assign users toohello application.</span></span>

#### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="c5c55-173">Identificateur de l’utilisateur de sélectionner et ajouter l’application utilisateur attributs toobe envoyé toohello</span><span class="sxs-lookup"><span data-stu-id="c5c55-173">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="c5c55-174">tooselect hello identificateur d’utilisateur ou ajouter des attributs d’utilisateur, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c5c55-174">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="c5c55-175">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**</span><span class="sxs-lookup"><span data-stu-id="c5c55-175">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="c5c55-176">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-176">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c5c55-177">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="c5c55-177">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c5c55-178">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c5c55-178">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="c5c55-179">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="c5c55-179">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="c5c55-180">Si vous ne voyez pas l’application hello souhaité tooshow ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="c5c55-180">If you do not see hello application you want tooshow up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="c5c55-181">Sélectionnez l’application hello que vous avez configuré l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c5c55-181">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="c5c55-182">Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-182">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="c5c55-183">Sous hello **attributs utilisateur** section, sélectionnez hello un identificateur unique pour vos utilisateurs Bonjour **identificateur de l’utilisateur** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="c5c55-183">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="c5c55-184">Hello option sélectionnée doit valeur attendue toomatch hello utilisateur hello de tooauthenticate l’application hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-184">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

   >[!NOTE] 
   ><span data-ttu-id="c5c55-185">Format de hello sélectionnez Azure AD pour l’attribut de NameID hello (identifiant d’utilisateur) en fonction de la valeur hello sélectionnée ou hello format demandé par l’application hello Bonjour SAML AuthRequest.</span><span class="sxs-lookup"><span data-stu-id="c5c55-185">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="c5c55-186">Pour plus d’informations, consultez l’article de hello [protocole SAML de l’authentification unique](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) sous hello section NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="c5c55-186">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="c5c55-187">attributs d’utilisateur tooadd, cliquez sur **afficher et modifier tous les autres attributs de l’utilisateur** tooedit hello attributs application de toohello toobe envoyé dans un jeton SAML de hello lorsque l’utilisateur se connecter.</span><span class="sxs-lookup"><span data-stu-id="c5c55-187">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="c5c55-188">tooadd un attribut :</span><span class="sxs-lookup"><span data-stu-id="c5c55-188">tooadd an attribute:</span></span>

   1. <span data-ttu-id="c5c55-189">Cliquez sur **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="c5c55-189">click **Add attribute**.</span></span> <span data-ttu-id="c5c55-190">Entrez hello **nom** et Bonjour sélectionnez Bonjour **valeur** à partir de la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-190">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="c5c55-191">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="c5c55-191">click **Save.**</span></span> <span data-ttu-id="c5c55-192">Vous verrez hello nouvel attribut dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-192">You will see hello new attribute in hello table.</span></span>

#### <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="c5c55-193">Télécharger des métadonnées Azure AD hello ou certificat</span><span class="sxs-lookup"><span data-stu-id="c5c55-193">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="c5c55-194">métadonnées de l’application hello toodownload ou un certificat d’Azure AD, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c5c55-194">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="c5c55-195">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**</span><span class="sxs-lookup"><span data-stu-id="c5c55-195">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="c5c55-196">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-196">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c5c55-197">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="c5c55-197">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c5c55-198">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c5c55-198">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="c5c55-199">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="c5c55-199">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="c5c55-200">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="c5c55-200">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="c5c55-201">Sélectionnez l’application hello que vous avez configuré l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c5c55-201">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="c5c55-202">Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-202">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="c5c55-203">Accédez trop**le certificat de signature SAML** section, puis cliquez sur **télécharger** valeur de la colonne.</span><span class="sxs-lookup"><span data-stu-id="c5c55-203">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="c5c55-204">En fonction de l’application hello nécessite la configuration de l’authentification unique, vous voyez deux toodownload d’option hello hello Metadata XML ou hello du certificat.</span><span class="sxs-lookup"><span data-stu-id="c5c55-204">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

    <span data-ttu-id="c5c55-205">Azure AD ne fournit pas une URL de métadonnées hello tooget.</span><span class="sxs-lookup"><span data-stu-id="c5c55-205">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="c5c55-206">Hello métadonnées peuvent uniquement être récupérées dans un fichier XML.</span><span class="sxs-lookup"><span data-stu-id="c5c55-206">hello metadata can only be retrieved as a XML file.</span></span>

### <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="c5c55-207">Comment tooconfigure fédéré l’authentification unique pour une application non-galerie</span><span class="sxs-lookup"><span data-stu-id="c5c55-207">How tooconfigure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="c5c55-208">tooconfigure une application non-galerie, vous devez toohave Azure AD premium et l’application hello prend en charge SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="c5c55-208">tooconfigure a non-gallery application, you need toohave Azure AD premium and hello application supports SAML 2.0.</span></span> <span data-ttu-id="c5c55-209">Pour plus d’informations sur les versions d’Azure AD, consultez [Tarification d’Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="c5c55-209">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

-   [<span data-ttu-id="c5c55-210">Configurer les valeurs de métadonnées de l’application hello dans Azure AD (URL de réponse d’URL, identificateur, authentification)</span><span class="sxs-lookup"><span data-stu-id="c5c55-210">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configuring-single-sign-on)

-   [<span data-ttu-id="c5c55-211">Identificateur de l’utilisateur de sélectionner et ajouter l’application utilisateur attributs toobe envoyé toohello</span><span class="sxs-lookup"><span data-stu-id="c5c55-211">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="c5c55-212">Récupérer le certificat et les métadonnées Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5c55-212">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="c5c55-213">Configurer les valeurs de métadonnées Azure AD dans l’application hello (authentification URL, l’émetteur, URL de déconnexion et un certificat)</span><span class="sxs-lookup"><span data-stu-id="c5c55-213">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configuring-single-sign-on)

#### <a name="configure-hello-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a><span data-ttu-id="c5c55-214">Configurer les valeurs de métadonnées de l’application hello dans Azure AD (URL de réponse d’URL, identificateur, authentification)</span><span class="sxs-lookup"><span data-stu-id="c5c55-214">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>

<span data-ttu-id="c5c55-215">tooconfigure l’authentification unique pour une application qui n’est pas dans la galerie d’Azure AD hello, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c5c55-215">tooconfigure single sign-on for an application that is not in hello Azure AD gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="c5c55-216">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**</span><span class="sxs-lookup"><span data-stu-id="c5c55-216">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="c5c55-217">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-217">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c5c55-218">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="c5c55-218">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c5c55-219">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c5c55-219">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="c5c55-220">Cliquez sur hello **ajouter** bouton au coin supérieur droit de hello sur hello **des Applications d’entreprise** panneau.</span><span class="sxs-lookup"><span data-stu-id="c5c55-220">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="c5c55-221">Cliquez sur **application Non-gallery** Bonjour **ajouter votre propre application** section.</span><span class="sxs-lookup"><span data-stu-id="c5c55-221">click **Non-gallery application** in hello **Add your own app** section.</span></span>

7.  <span data-ttu-id="c5c55-222">Entrez le nom hello de l’application hello Bonjour **nom** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="c5c55-222">Enter hello name of hello application in hello **Name** textbox.</span></span>

8.  <span data-ttu-id="c5c55-223">Cliquez sur **ajouter** bouton, l’application de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="c5c55-223">Click **Add** button, tooadd hello application.</span></span>

9.  <span data-ttu-id="c5c55-224">Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-224">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="c5c55-225">Sélectionnez **SAML-authentification** Bonjour **Mode** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="c5c55-225">Select **SAML-based Sign-on** in hello **Mode** dropdown.</span></span>

11. <span data-ttu-id="c5c55-226">Entrez les valeurs hello requis dans **URL et domaine.**</span><span class="sxs-lookup"><span data-stu-id="c5c55-226">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="c5c55-227">Vous devez obtenir ces valeurs à partir du fournisseur de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-227">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="c5c55-228">application de hello tooconfigure en tant que l’authentification unique initiée par les fournisseurs d’identité, entrez hello URL de réponse et hello identificateur.</span><span class="sxs-lookup"><span data-stu-id="c5c55-228">tooconfigure hello application as IdP-initiated SSO, enter hello Reply URL and hello Identifier.</span></span>

   2.  <span data-ttu-id="c5c55-229">**Facultatif :** application hello tooconfigure authentifications uniques initiées, hello signe sur l’URL, il est obligatoire.</span><span class="sxs-lookup"><span data-stu-id="c5c55-229">**Optional:** tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="c5c55-230">Bonjour **attributs utilisateur**, sélectionnez hello un identificateur unique pour vos utilisateurs Bonjour **identificateur de l’utilisateur** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="c5c55-230">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="c5c55-231">**Facultatif :** cliquez sur **afficher et modifier tous les autres attributs utilisateur** tooedit hello attributs application de toohello toobe envoyé dans un jeton SAML de hello lorsque l’utilisateur se connecter.</span><span class="sxs-lookup"><span data-stu-id="c5c55-231">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="c5c55-232">tooadd un attribut :</span><span class="sxs-lookup"><span data-stu-id="c5c55-232">tooadd an attribute:</span></span>

   1. <span data-ttu-id="c5c55-233">Cliquez sur **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="c5c55-233">click **Add attribute**.</span></span> <span data-ttu-id="c5c55-234">Entrez hello **nom** et Bonjour sélectionnez Bonjour **valeur** à partir de la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-234">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="c5c55-235">Cliquez sur **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="c5c55-235">Click **Save.**</span></span> <span data-ttu-id="c5c55-236">Vous consultez hello nouvel attribut dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-236">You see hello new attribute in hello table.</span></span>

14. <span data-ttu-id="c5c55-237">Cliquez sur **configurer &lt;nom de l’application&gt;**  documentation tooaccess sur la tooconfigure l’authentification unique dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-237">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="c5c55-238">Possède également Azure AD URL et le certificat requis pour l’application hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-238">Also, you has Azure AD URLs and certificate required for hello application.</span></span>

#### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="c5c55-239">Identificateur de l’utilisateur de sélectionner et ajouter l’application utilisateur attributs toobe envoyé toohello</span><span class="sxs-lookup"><span data-stu-id="c5c55-239">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="c5c55-240">tooselect hello identificateur d’utilisateur ou ajouter des attributs d’utilisateur, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c5c55-240">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="c5c55-241">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**</span><span class="sxs-lookup"><span data-stu-id="c5c55-241">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="c5c55-242">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-242">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c5c55-243">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="c5c55-243">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c5c55-244">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c5c55-244">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="c5c55-245">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="c5c55-245">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="c5c55-246">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="c5c55-246">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="c5c55-247">Sélectionnez l’application hello que vous avez configuré l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c5c55-247">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="c5c55-248">Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-248">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="c5c55-249">Sous hello **attributs utilisateur** section, sélectionnez hello un identificateur unique pour vos utilisateurs Bonjour **identificateur de l’utilisateur** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="c5c55-249">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="c5c55-250">Hello option sélectionnée doit valeur attendue toomatch hello utilisateur hello de tooauthenticate l’application hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-250">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

   >[!NOTE] 
   ><span data-ttu-id="c5c55-251">Format de hello sélectionnez Azure AD pour l’attribut de NameID hello (identifiant d’utilisateur) en fonction de la valeur hello sélectionnée ou hello format demandé par l’application hello Bonjour SAML AuthRequest.</span><span class="sxs-lookup"><span data-stu-id="c5c55-251">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="c5c55-252">Pour plus d’informations, consultez l’article de hello [protocole SAML de l’authentification unique](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) sous hello section NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="c5c55-252">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="c5c55-253">attributs d’utilisateur tooadd, cliquez sur **afficher et modifier tous les autres attributs de l’utilisateur** tooedit hello attributs application de toohello toobe envoyé dans un jeton SAML de hello lorsque l’utilisateur se connecter.</span><span class="sxs-lookup"><span data-stu-id="c5c55-253">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="c5c55-254">tooadd un attribut :</span><span class="sxs-lookup"><span data-stu-id="c5c55-254">tooadd an attribute:</span></span>

   1. <span data-ttu-id="c5c55-255">Cliquez sur **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="c5c55-255">click **Add attribute**.</span></span> <span data-ttu-id="c5c55-256">Entrez hello **nom** et Bonjour sélectionnez Bonjour **valeur** à partir de la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-256">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="c5c55-257">Cliquez sur **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="c5c55-257">Click **Save.**</span></span> <span data-ttu-id="c5c55-258">Vous consultez hello nouvel attribut dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-258">You see hello new attribute in hello table.</span></span>

#### <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="c5c55-259">Télécharger des métadonnées Azure AD hello ou certificat</span><span class="sxs-lookup"><span data-stu-id="c5c55-259">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="c5c55-260">métadonnées de l’application hello toodownload ou un certificat d’Azure AD, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c5c55-260">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="c5c55-261">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**</span><span class="sxs-lookup"><span data-stu-id="c5c55-261">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="c5c55-262">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-262">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c5c55-263">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="c5c55-263">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c5c55-264">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c5c55-264">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="c5c55-265">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="c5c55-265">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="c5c55-266">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="c5c55-266">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="c5c55-267">Sélectionnez l’application hello que vous avez configuré l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c5c55-267">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="c5c55-268">Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-268">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="c5c55-269">Accédez trop**le certificat de signature SAML** section, puis cliquez sur **télécharger** valeur de la colonne.</span><span class="sxs-lookup"><span data-stu-id="c5c55-269">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="c5c55-270">En fonction de l’application hello nécessite la configuration de l’authentification unique, vous voyez deux toodownload d’option hello hello Metadata XML ou hello du certificat.</span><span class="sxs-lookup"><span data-stu-id="c5c55-270">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="c5c55-271">Azure AD ne fournit pas une URL de métadonnées hello tooget.</span><span class="sxs-lookup"><span data-stu-id="c5c55-271">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="c5c55-272">Hello métadonnées peuvent uniquement être récupérées dans un fichier XML.</span><span class="sxs-lookup"><span data-stu-id="c5c55-272">hello metadata can only be retrieved as a XML file.</span></span>

### <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="c5c55-273">Comment tooconfigure le mot de passe sur l’authentification unique pour une application de la galerie Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5c55-273">How tooconfigure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="c5c55-274">tooconfigure une application à partir de la galerie d’Azure AD hello vous devez :</span><span class="sxs-lookup"><span data-stu-id="c5c55-274">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="c5c55-275">Ajouter une application à partir de la galerie d’Azure AD hello</span><span class="sxs-lookup"><span data-stu-id="c5c55-275">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="c5c55-276">Configurer une application hello pour mot de passe l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="c5c55-276">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

#### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="c5c55-277">Ajouter une application à partir de la galerie d’Azure AD hello</span><span class="sxs-lookup"><span data-stu-id="c5c55-277">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="c5c55-278">tooadd une application à partir de hello Galerie d’Azure AD, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c5c55-278">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="c5c55-279">Ouvrez hello [Azure Portal](https://portal.azure.com) et connectez-vous en tant qu’un **administrateur Global** ou **Co-admin**</span><span class="sxs-lookup"><span data-stu-id="c5c55-279">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="c5c55-280">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-280">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c5c55-281">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="c5c55-281">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c5c55-282">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c5c55-282">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="c5c55-283">Cliquez sur hello **ajouter** bouton au coin supérieur droit de hello sur hello **des Applications d’entreprise** panneau.</span><span class="sxs-lookup"><span data-stu-id="c5c55-283">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="c5c55-284">Bonjour **Entrez un nom** zone de texte à partir de hello **ajouter à partir de la galerie de hello** section, entrez un nom hello de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-284">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="c5c55-285">Sélectionnez hello application tooconfigure pour l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c5c55-285">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="c5c55-286">Avant d’ajouter l’application hello, vous pouvez modifier son nom à partir de hello **nom** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="c5c55-286">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="c5c55-287">Cliquez sur **ajouter** bouton, l’application de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="c5c55-287">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="c5c55-288">Après une courte période, vous être Panneau de configuration de l’application en mesure de toosee hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-288">After a short period, you be able toosee hello application’s configuration blade.</span></span>

#### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="c5c55-289">Configurer une application hello pour mot de passe l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="c5c55-289">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="c5c55-290">tooconfigure l’authentification unique pour une application, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c5c55-290">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="c5c55-291">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**</span><span class="sxs-lookup"><span data-stu-id="c5c55-291">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="c5c55-292">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-292">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c5c55-293">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="c5c55-293">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c5c55-294">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c5c55-294">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="c5c55-295">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="c5c55-295">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="c5c55-296">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="c5c55-296">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="c5c55-297">Sélectionnez l’application hello tooconfigure l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c5c55-297">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="c5c55-298">Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-298">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="c5c55-299">Mode de sélection hello **mot de passe de session.**</span><span class="sxs-lookup"><span data-stu-id="c5c55-299">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="c5c55-300">[Affecter des utilisateurs toohello application](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="c5c55-300">[Assign users toohello application](#how-to-assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="c5c55-301">En outre, vous pouvez également fournir des informations d’identification pour le compte d’utilisateur de hello en sélectionnant les lignes hello d’utilisateurs de hello en cliquant sur **informations d’identification de la mise à jour** et en entrant hello username et password pour le compte d’utilisateurs de hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-301">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="c5c55-302">Dans le cas contraire, les utilisateurs être invité à tooenter hello informations d’identification elles-mêmes lors du lancement.</span><span class="sxs-lookup"><span data-stu-id="c5c55-302">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

### <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="c5c55-303">Comment tooconfigure le mot de passe sur l’authentification unique pour une application non-galerie</span><span class="sxs-lookup"><span data-stu-id="c5c55-303">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="c5c55-304">tooconfigure une application à partir de la galerie d’Azure AD hello vous devez :</span><span class="sxs-lookup"><span data-stu-id="c5c55-304">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="c5c55-305">Ajouter une application ne figurant pas dans la galerie</span><span class="sxs-lookup"><span data-stu-id="c5c55-305">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="c5c55-306">Configurer une application hello pour mot de passe l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="c5c55-306">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

#### <a name="add-a-non-gallery-application"></a><span data-ttu-id="c5c55-307">Ajouter une application ne figurant pas dans la galerie</span><span class="sxs-lookup"><span data-stu-id="c5c55-307">Add a non-gallery application</span></span>

<span data-ttu-id="c5c55-308">tooadd une application à partir de hello Galerie d’Azure AD, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c5c55-308">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="c5c55-309">Ouvrez hello [Azure Portal](https://portal.azure.com) et connectez-vous en tant qu’un **administrateur Global** ou **Co-admin**.</span><span class="sxs-lookup"><span data-stu-id="c5c55-309">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="c5c55-310">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-310">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c5c55-311">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="c5c55-311">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c5c55-312">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c5c55-312">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="c5c55-313">Cliquez sur hello **ajouter** bouton au coin supérieur droit de hello sur hello **des Applications d’entreprise** panneau.</span><span class="sxs-lookup"><span data-stu-id="c5c55-313">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="c5c55-314">Cliquez sur **Application ne figurant pas dans la galerie**.</span><span class="sxs-lookup"><span data-stu-id="c5c55-314">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="c5c55-315">Entrez le nom hello de votre application Bonjour **nom** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="c5c55-315">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="c5c55-316">Sélectionnez **Ajouter.**</span><span class="sxs-lookup"><span data-stu-id="c5c55-316">Select **Add.**</span></span>

<span data-ttu-id="c5c55-317">Après une courte période, vous être Panneau de configuration de l’application en mesure de toosee hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-317">After a short period, you be able toosee hello application’s configuration blade.</span></span>

#### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="c5c55-318">Configurer une application hello pour mot de passe l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="c5c55-318">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="c5c55-319">tooconfigure l’authentification unique pour une application, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c5c55-319">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="c5c55-320">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**</span><span class="sxs-lookup"><span data-stu-id="c5c55-320">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="c5c55-321">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-321">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c5c55-322">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="c5c55-322">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c5c55-323">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c5c55-323">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="c5c55-324">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="c5c55-324">click **All Applications** tooview a list of all your applications.</span></span>

    1.  <span data-ttu-id="c5c55-325">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="c5c55-325">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="c5c55-326">Sélectionnez l’application hello tooconfigure l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c5c55-326">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="c5c55-327">Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-327">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="c5c55-328">Mode de sélection hello **mot de passe de session.**</span><span class="sxs-lookup"><span data-stu-id="c5c55-328">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="c5c55-329">Entrez hello **URL de connexion**.</span><span class="sxs-lookup"><span data-stu-id="c5c55-329">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="c5c55-330">Il s’agit d’URL de hello où les utilisateurs entrent leur nom d’utilisateur et mot de passe des toosign dans pour.</span><span class="sxs-lookup"><span data-stu-id="c5c55-330">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="c5c55-331">Vérifiez la connexion hello dans les champs est visibles à l’URL de hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-331">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="c5c55-332">[Affecter des utilisateurs toohello application](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="c5c55-332">[Assign users toohello application](#how-to-assign-a-user-to-an-application-directly).</span></span>

11. <span data-ttu-id="c5c55-333">En outre, vous pouvez également fournir des informations d’identification pour le compte d’utilisateur de hello en sélectionnant les lignes hello d’utilisateurs de hello en cliquant sur **informations d’identification de la mise à jour** et en entrant hello username et password pour le compte d’utilisateurs de hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-333">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="c5c55-334">Dans le cas contraire, les utilisateurs être invité à tooenter hello informations d’identification elles-mêmes lors du lancement.</span><span class="sxs-lookup"><span data-stu-id="c5c55-334">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="problems-related-tooassigning-applications-toousers"></a><span data-ttu-id="c5c55-335">Des problèmes connexes tooassigning applications toousers</span><span class="sxs-lookup"><span data-stu-id="c5c55-335">Problems related tooassigning applications toousers</span></span>

<span data-ttu-id="c5c55-336">Un utilisateur ne peut pas s’agir d’une application dans leur volet d’accès, car ils ne sont pas affectés toohello application.</span><span class="sxs-lookup"><span data-stu-id="c5c55-336">A user may not be seeing an application on their Access Panel because they are not assigned toohello application.</span></span> <span data-ttu-id="c5c55-337">Voici certains toocheck façons :</span><span class="sxs-lookup"><span data-stu-id="c5c55-337">Below are some ways toocheck:</span></span>

-   [<span data-ttu-id="c5c55-338">Vérifiez si un utilisateur est affecté toohello application</span><span class="sxs-lookup"><span data-stu-id="c5c55-338">Check if a user is assigned toohello application</span></span>](#check-if-a-user-is-assigned-to-the-application)

-   [<span data-ttu-id="c5c55-339">Comment tooassign directement une application de tooan utilisateur</span><span class="sxs-lookup"><span data-stu-id="c5c55-339">How tooassign a user tooan application directly</span></span>](#how-to-assign-a-user-to-an-application-directly)

-   [<span data-ttu-id="c5c55-340">Vérifiez si un utilisateur est assigné tooa licence liées toohello application</span><span class="sxs-lookup"><span data-stu-id="c5c55-340">Check if a user is assigned tooa license related toohello application</span></span>](#check-if-a-user-is-under-a-license-related-to-the-application)

-   [<span data-ttu-id="c5c55-341">Comment tooassign un utilisateur tooa de licence</span><span class="sxs-lookup"><span data-stu-id="c5c55-341">How tooassign a license tooa user</span></span>](#how-to-assign-a-user-a-license)

### <a name="check-if-a-user-is-assigned-toohello-application"></a><span data-ttu-id="c5c55-342">Vérifiez si un utilisateur est affecté toohello application</span><span class="sxs-lookup"><span data-stu-id="c5c55-342">Check if a user is assigned toohello application</span></span>

<span data-ttu-id="c5c55-343">toocheck si un utilisateur est assigné toohello application, procédez comme suit hello :</span><span class="sxs-lookup"><span data-stu-id="c5c55-343">toocheck if a user is assigned toohello application, follow hello steps below:</span></span>

1.  <span data-ttu-id="c5c55-344">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="c5c55-344">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="c5c55-345">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-345">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c5c55-346">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="c5c55-346">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c5c55-347">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c5c55-347">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="c5c55-348">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="c5c55-348">click **All Applications** tooview a list of all your applications.</span></span>

6.  <span data-ttu-id="c5c55-349">**Recherche** pour nom hello de l’application hello en question.</span><span class="sxs-lookup"><span data-stu-id="c5c55-349">**Search** for hello name of hello application in question.</span></span>

7.  <span data-ttu-id="c5c55-350">Sélectionnez **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c5c55-350">click **Users and groups**.</span></span>

8.  <span data-ttu-id="c5c55-351">Vérifiez toosee si votre utilisateur est affecté toohello application.</span><span class="sxs-lookup"><span data-stu-id="c5c55-351">Check toosee if your user is assigned toohello application.</span></span>

   * <span data-ttu-id="c5c55-352">Si ce n’est pas hello comme suit dans « comment tooassign directement une application de tooan utilisateur » toodo donc.</span><span class="sxs-lookup"><span data-stu-id="c5c55-352">If not follow hello steps in “How tooassign a user tooan application directly” toodo so.</span></span>

### <a name="how-tooassign-a-user-tooan-application-directly"></a><span data-ttu-id="c5c55-353">Comment tooassign directement une application de tooan utilisateur</span><span class="sxs-lookup"><span data-stu-id="c5c55-353">How tooassign a user tooan application directly</span></span>

<span data-ttu-id="c5c55-354">tooassign un ou plusieurs utilisateurs tooan application directement, comme suit hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c5c55-354">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="c5c55-355">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global**.</span><span class="sxs-lookup"><span data-stu-id="c5c55-355">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator**.</span></span>

2.  <span data-ttu-id="c5c55-356">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-356">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c5c55-357">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="c5c55-357">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c5c55-358">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c5c55-358">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="c5c55-359">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="c5c55-359">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="c5c55-360">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="c5c55-360">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="c5c55-361">Sélectionnez l’application hello tooassign une liste des utilisateurs toofrom hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-361">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="c5c55-362">Une fois le charge de l’application hello, cliquez sur **utilisateurs et groupes** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-362">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="c5c55-363">Cliquez sur hello **ajouter** bouton par-dessus hello **utilisateurs et groupes** hello tooopen de liste **ajouter l’affectation** panneau.</span><span class="sxs-lookup"><span data-stu-id="c5c55-363">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="c5c55-364">Cliquez sur hello **utilisateurs et groupes** sélecteur de hello **ajouter l’affectation** panneau.</span><span class="sxs-lookup"><span data-stu-id="c5c55-364">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="c5c55-365">Type Bonjour **nom complet** ou **adresse de messagerie** d’utilisateur hello vous êtes intéressé par attribution dans hello **recherche par nom ou adresse de messagerie** zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="c5c55-365">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="c5c55-366">Placez le curseur sur hello **utilisateur** dans hello liste tooreveal un **case à cocher**.</span><span class="sxs-lookup"><span data-stu-id="c5c55-366">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="c5c55-367">Cliquez sur tooadd de photo ou le logo de profil hello case à cocher suivante toohello l’utilisateur à votre toohello utilisateur **sélectionnés** liste.</span><span class="sxs-lookup"><span data-stu-id="c5c55-367">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="c5c55-368">**Facultatif :** si vous souhaitez que trop**ajouter plusieurs utilisateurs**, type dans un autre **nom complet** ou **adresse de messagerie** dans hello **Rechercher par nom ou l’adresse de messagerie** zone de recherche, cliquez sur tooadd de case à cocher hello cette toohello utilisateur **sélectionnés** liste.</span><span class="sxs-lookup"><span data-stu-id="c5c55-368">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="c5c55-369">Lorsque vous avez fini de sélectionner les utilisateurs, cliquez sur hello **sélectionnez** bouton tooadd les toohello la liste des toobe utilisateurs et groupes affectés toohello application.</span><span class="sxs-lookup"><span data-stu-id="c5c55-369">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="c5c55-370">**Facultatif :** cliquez sur hello **sélectionner un rôle** sélecteur Bonjour **ajouter l’affectation** panneau tooselect un rôle aux utilisateurs de toohello tooassign que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="c5c55-370">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="c5c55-371">Cliquez sur hello **affecter** bouton tooassign hello application toohello les utilisateurs sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="c5c55-371">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="c5c55-372">Après une courte période, les utilisateurs de hello que vous avez sélectionné est en mesure de toolaunch ces applications dans hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="c5c55-372">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

### <a name="check-if-a-user-is-under-a-license-related-toohello-application"></a><span data-ttu-id="c5c55-373">Vérifier si un utilisateur est sous licence toohello application relative</span><span class="sxs-lookup"><span data-stu-id="c5c55-373">Check if a user is under a license related toohello application</span></span>

<span data-ttu-id="c5c55-374">toocheck un utilisateur affecté des licences, suivez les étapes hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c5c55-374">toocheck a user’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="c5c55-375">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="c5c55-375">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="c5c55-376">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-376">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c5c55-377">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="c5c55-377">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c5c55-378">Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-378">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="c5c55-379">Cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="c5c55-379">click **All users**.</span></span>

6.  <span data-ttu-id="c5c55-380">**Recherche** pour l’utilisateur hello vous intéressez et **cliquez sur la ligne hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="c5c55-380">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="c5c55-381">Cliquez sur **licences** toosee les licences hello d’utilisateur est affectée actuellement.</span><span class="sxs-lookup"><span data-stu-id="c5c55-381">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

  * <span data-ttu-id="c5c55-382">Si l’utilisateur de hello est attribué une licence Office tooan Ceci activer premier tiers Office applications tooappear sur hello panneau d’accès de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c5c55-382">If hello user is assigned tooan Office license this enable First Party Office applications tooappear on hello user’s Access Panel.</span></span>

### <a name="how-tooassign-a-user-a-license"></a><span data-ttu-id="c5c55-383">Comment tooassign un utilisateur une licence</span><span class="sxs-lookup"><span data-stu-id="c5c55-383">How tooassign a user a license</span></span> 

<span data-ttu-id="c5c55-384">tooassign un utilisateur tooa de licences, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c5c55-384">tooassign a license tooa user, follow hello steps below:</span></span>

1.  <span data-ttu-id="c5c55-385">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="c5c55-385">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="c5c55-386">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-386">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c5c55-387">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="c5c55-387">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c5c55-388">Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-388">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="c5c55-389">Cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="c5c55-389">click **All users**.</span></span>

6.  <span data-ttu-id="c5c55-390">**Recherche** pour l’utilisateur hello vous intéressez et **cliquez sur la ligne hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="c5c55-390">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="c5c55-391">Cliquez sur **licences** toosee les licences hello d’utilisateur est affectée actuellement.</span><span class="sxs-lookup"><span data-stu-id="c5c55-391">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

8.  <span data-ttu-id="c5c55-392">Cliquez sur hello **affecter** bouton.</span><span class="sxs-lookup"><span data-stu-id="c5c55-392">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="c5c55-393">Sélectionnez **un ou plusieurs produits** à partir de la liste de hello des produits disponibles.</span><span class="sxs-lookup"><span data-stu-id="c5c55-393">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="c5c55-394">**Facultatif** cliquez sur hello **options d’attribution** élément toogranularly affecter des produits.</span><span class="sxs-lookup"><span data-stu-id="c5c55-394">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="c5c55-395">Cliquez sur **OK** lorsque l’opération est terminée.</span><span class="sxs-lookup"><span data-stu-id="c5c55-395">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="c5c55-396">Cliquez sur hello **affecter** bouton tooassign ces utilisateur toothis de licences.</span><span class="sxs-lookup"><span data-stu-id="c5c55-396">Click hello **Assign** button tooassign these licenses toothis user.</span></span>

## <a name="problems-related-tooassigning-applications-toogroups"></a><span data-ttu-id="c5c55-397">Des problèmes connexes tooassigning applications toogroups</span><span class="sxs-lookup"><span data-stu-id="c5c55-397">Problems related tooassigning applications toogroups</span></span>

<span data-ttu-id="c5c55-398">Un utilisateur peut s’agir d’une application dans leur volet d’accès car ils font partie d’un groupe auquel a été attribué application hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-398">A user may be seeing an application on their Access Panel because they are part of a group that has been assigned hello application.</span></span> <span data-ttu-id="c5c55-399">Voici certains toocheck façons :</span><span class="sxs-lookup"><span data-stu-id="c5c55-399">Below are some ways toocheck:</span></span>

-   [<span data-ttu-id="c5c55-400">Vérifier les appartenances d’un utilisateur à des groupes</span><span class="sxs-lookup"><span data-stu-id="c5c55-400">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="c5c55-401">Comment tooassign un tooa application groupe directement</span><span class="sxs-lookup"><span data-stu-id="c5c55-401">How tooassign an application tooa group directly</span></span>](#how-to-assign-an-application-to-a-group-directly)

-   [<span data-ttu-id="c5c55-402">Vérifiez si un utilisateur fait partie du groupe tooa licence attribuée</span><span class="sxs-lookup"><span data-stu-id="c5c55-402">Check if a user is part of group assigned tooa license</span></span>](#check-if-a-user-is-part-of-group-assigned-to-a-license)

-   [<span data-ttu-id="c5c55-403">Comment tooassign un tooa un groupe de licences</span><span class="sxs-lookup"><span data-stu-id="c5c55-403">How tooassign a license tooa group</span></span>](#how-to-assign-a-license-to-a-group)

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="c5c55-404">Vérifier les appartenances d’un utilisateur à des groupes</span><span class="sxs-lookup"><span data-stu-id="c5c55-404">Check a user’s group memberships</span></span>

<span data-ttu-id="c5c55-405">toocheck une appartenance de groupe, suivez les étapes hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c5c55-405">toocheck a group’s membership, follow hello steps below:</span></span>

1.  <span data-ttu-id="c5c55-406">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="c5c55-406">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="c5c55-407">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-407">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c5c55-408">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="c5c55-408">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c5c55-409">Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-409">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="c5c55-410">Cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="c5c55-410">click **All users**.</span></span>

6.  <span data-ttu-id="c5c55-411">**Recherche** pour l’utilisateur hello vous intéressez et **cliquez sur la ligne hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="c5c55-411">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="c5c55-412">Cliquez sur **Groupes**.</span><span class="sxs-lookup"><span data-stu-id="c5c55-412">click **Groups**.</span></span>

8.  <span data-ttu-id="c5c55-413">Vérifiez toosee si l’utilisateur fait partie d’une application toohello de groupe affecté.</span><span class="sxs-lookup"><span data-stu-id="c5c55-413">Check toosee if your user is part of a Group assigned toohello application.</span></span>

  * <span data-ttu-id="c5c55-414">Si vous souhaitez utilisateur de hello tooremove à partir du groupe de hello, **cliquez sur la ligne hello** hello groupe d’et sélectionnez Supprimer.</span><span class="sxs-lookup"><span data-stu-id="c5c55-414">If you want tooremove hello user from hello group, **click hello row** of hello group and select delete.</span></span>

### <a name="how-tooassign-an-application-tooa-group-directly"></a><span data-ttu-id="c5c55-415">Comment tooassign un tooa application groupe directement</span><span class="sxs-lookup"><span data-stu-id="c5c55-415">How tooassign an application tooa group directly</span></span>

<span data-ttu-id="c5c55-416">tooassign un ou plusieurs groupes tooan application directement, hello suivez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c5c55-416">tooassign one or more groups tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="c5c55-417">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global**.</span><span class="sxs-lookup"><span data-stu-id="c5c55-417">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator**.</span></span>

2.  <span data-ttu-id="c5c55-418">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-418">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c5c55-419">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="c5c55-419">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c5c55-420">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c5c55-420">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="c5c55-421">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="c5c55-421">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="c5c55-422">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="c5c55-422">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="c5c55-423">Sélectionnez l’application hello tooassign une liste des utilisateurs toofrom hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-423">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="c5c55-424">Une fois le charge de l’application hello, cliquez sur **utilisateurs et groupes** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-424">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="c5c55-425">Cliquez sur hello **ajouter** bouton par-dessus hello **utilisateurs et groupes** hello tooopen de liste **ajouter l’affectation** panneau.</span><span class="sxs-lookup"><span data-stu-id="c5c55-425">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="c5c55-426">Cliquez sur hello **utilisateurs et groupes** sélecteur de hello **ajouter l’affectation** panneau.</span><span class="sxs-lookup"><span data-stu-id="c5c55-426">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="c5c55-427">Type Bonjour **nom de groupe complète** groupe hello vous êtes intéressé par attribution dans hello **recherche par nom ou adresse de messagerie** zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="c5c55-427">Type in hello **full group name** of hello group you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="c5c55-428">Placez le curseur sur hello **groupe** dans hello liste tooreveal un **case à cocher**.</span><span class="sxs-lookup"><span data-stu-id="c5c55-428">Hover over hello **group** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="c5c55-429">Cliquez sur tooadd de photo ou le logo de profil de hello case à cocher toohello groupe suivant votre toohello utilisateur **sélectionnés** liste.</span><span class="sxs-lookup"><span data-stu-id="c5c55-429">Click hello checkbox next toohello group’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="c5c55-430">**Facultatif :** si vous souhaitez que trop**ajouter plusieurs groupes**, type dans un autre **nom de groupe complète** dans hello **recherche par nom ou adresse de messagerie** zone de recherche, Cliquez sur tooadd de case à cocher hello toohello de ce groupe **sélectionnés** liste.</span><span class="sxs-lookup"><span data-stu-id="c5c55-430">**Optional:** If you would like too**add more than one group**, type in another **full group name** into hello **Search by name or email address** search box, and click hello checkbox tooadd this group toohello **Selected** list.</span></span>

13. <span data-ttu-id="c5c55-431">Lorsque vous avez fini de sélectionner les groupes, cliquez sur hello **sélectionnez** bouton tooadd les toohello la liste des toobe utilisateurs et groupes affectés toohello application.</span><span class="sxs-lookup"><span data-stu-id="c5c55-431">When you are finished selecting groups, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="c5c55-432">**Facultatif :** cliquez sur hello **sélectionner un rôle** sélecteur Bonjour **ajouter l’affectation** panneau tooselect un toohello de tooassign rôle groupes que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="c5c55-432">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello groups you have selected.</span></span>

15. <span data-ttu-id="c5c55-433">Cliquez sur hello **affecter** bouton tooassign hello application toohello les groupes sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="c5c55-433">Click hello **Assign** button tooassign hello application toohello selected groups.</span></span>

<span data-ttu-id="c5c55-434">Après une courte période, les utilisateurs de hello que vous avez sélectionné est en mesure de toolaunch ces applications dans hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="c5c55-434">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

### <a name="check-if-a-user-is-part-of-group-assigned-tooa-license"></a><span data-ttu-id="c5c55-435">Vérifiez si un utilisateur fait partie du groupe tooa licence attribuée</span><span class="sxs-lookup"><span data-stu-id="c5c55-435">Check if a user is part of group assigned tooa license</span></span>

1.  <span data-ttu-id="c5c55-436">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="c5c55-436">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="c5c55-437">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-437">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c5c55-438">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="c5c55-438">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c5c55-439">Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-439">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="c5c55-440">Cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="c5c55-440">click **All users**.</span></span>

6.  <span data-ttu-id="c5c55-441">**Recherche** pour l’utilisateur hello vous intéressez et **cliquez sur la ligne hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="c5c55-441">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="c5c55-442">Cliquez sur **Groupes**.</span><span class="sxs-lookup"><span data-stu-id="c5c55-442">click **Groups**.</span></span>

8.  <span data-ttu-id="c5c55-443">Cliquez sur ligne hello d’un groupe spécifique.</span><span class="sxs-lookup"><span data-stu-id="c5c55-443">click hello row of a specific group.</span></span>

9.  <span data-ttu-id="c5c55-444">Cliquez sur **licences** toosee quel groupe hello de licences a affecté tooit.</span><span class="sxs-lookup"><span data-stu-id="c5c55-444">click **Licenses** toosee which licenses hello group has assigned tooit.</span></span>

   * <span data-ttu-id="c5c55-445">Si le groupe de hello est attribué une licence Office tooan sur que ceci peut activer certaine tooappear d’applications de premier tiers Office hello panneau d’accès de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c5c55-445">If hello group is assigned tooan Office license this may enable certain First Party Office applications tooappear on hello user’s Access Panel.</span></span>

### <a name="how-tooassign-a-license-tooa-group"></a><span data-ttu-id="c5c55-446">Comment tooassign un tooa un groupe de licences</span><span class="sxs-lookup"><span data-stu-id="c5c55-446">How tooassign a license tooa group</span></span>

<span data-ttu-id="c5c55-447">tooassign un groupe tooa de licences, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c5c55-447">tooassign a license tooa group, follow hello steps below:</span></span>

1.  <span data-ttu-id="c5c55-448">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="c5c55-448">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="c5c55-449">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-449">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c5c55-450">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="c5c55-450">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c5c55-451">Cliquez sur **utilisateurs et groupes** dans le menu de navigation hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-451">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="c5c55-452">Cliquez sur **Tous les groupes**.</span><span class="sxs-lookup"><span data-stu-id="c5c55-452">click **All groups**.</span></span>

6.  <span data-ttu-id="c5c55-453">**Recherche** pour groupe hello vous intéressez et **cliquez sur la ligne hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="c5c55-453">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="c5c55-454">Cliquez sur **licences** toosee quel groupe hello de licences est affectée actuellement.</span><span class="sxs-lookup"><span data-stu-id="c5c55-454">click **Licenses** toosee which licenses hello group currently has assigned.</span></span>

8.  <span data-ttu-id="c5c55-455">Cliquez sur hello **affecter** bouton.</span><span class="sxs-lookup"><span data-stu-id="c5c55-455">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="c5c55-456">Sélectionnez **un ou plusieurs produits** à partir de la liste de hello des produits disponibles.</span><span class="sxs-lookup"><span data-stu-id="c5c55-456">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="c5c55-457">**Facultatif** cliquez sur hello **options d’attribution** élément toogranularly affecter des produits.</span><span class="sxs-lookup"><span data-stu-id="c5c55-457">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="c5c55-458">Cliquez sur **OK** lorsque l’opération est terminée.</span><span class="sxs-lookup"><span data-stu-id="c5c55-458">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="c5c55-459">Cliquez sur hello **affecter** bouton tooassign ces toothis de groupe de licences.</span><span class="sxs-lookup"><span data-stu-id="c5c55-459">Click hello **Assign** button tooassign these licenses toothis group.</span></span> <span data-ttu-id="c5c55-460">Cette opération peut prendre beaucoup de temps, selon la taille de hello et la complexité du groupe de hello.</span><span class="sxs-lookup"><span data-stu-id="c5c55-460">This may take a long time, depending on hello size and complexity of hello group.</span></span>

>[!NOTE]
><span data-ttu-id="c5c55-461">toodo cela plus rapide, envisagez temporairement attribution directement à un utilisateur de toohello de licence.</span><span class="sxs-lookup"><span data-stu-id="c5c55-461">toodo this faster, consider temporarily assigning a license toohello user directly.</span></span> 
>
>

## <a name="next-steps"></a><span data-ttu-id="c5c55-462">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c5c55-462">Next steps</span></span>
[<span data-ttu-id="c5c55-463">Ajouter de nouveaux utilisateurs tooAzure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c5c55-463">Add new users tooAzure Active Directory</span></span>](active-directory-users-create-azure-portal.md)

