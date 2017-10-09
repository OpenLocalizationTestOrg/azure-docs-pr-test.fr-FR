---
title: "aaaHow tooconfigure fédéré l’authentification unique pour une application non-galerie | Documents Microsoft"
description: "Comment tooconfigure fédéré l’authentification unique pour une application non-Galerie personnalisée que vous souhaitez toointegrate avec Azure AD"
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
ms.openlocfilehash: f4a37cb500c075d0ce917ad8f13411f2ce208c56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="57681-103">Comment tooconfigure fédéré l’authentification unique pour une application non-galerie</span><span class="sxs-lookup"><span data-stu-id="57681-103">How tooconfigure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="57681-104">tooconfigure une application non-galerie, vous devez toohave Azure AD premium et l’application hello prend en charge SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="57681-104">tooconfigure a non-gallery application, you need toohave Azure AD premium and hello application supports SAML 2.0.</span></span> <span data-ttu-id="57681-105">Pour plus d’informations sur les versions d’Azure AD, consultez [Tarification d’Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="57681-105">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="57681-106">Vue d’ensemble des étapes requises</span><span class="sxs-lookup"><span data-stu-id="57681-106">Overview of steps required</span></span>
<span data-ttu-id="57681-107">Voici une vue d’ensemble de haut niveau de hello étapes requises tooconfigure fédéré l’authentification unique pour une galerie-non (par exemple, personnalisé) application.</span><span class="sxs-lookup"><span data-stu-id="57681-107">Below is a high level overview of hello steps required tooconfigure federated single sign-on for a non-gallery (e.g., custom) application.</span></span>

-   [<span data-ttu-id="57681-108">Configurer les valeurs de métadonnées de l’application hello dans Azure AD (URL de réponse d’URL, identificateur, authentification)</span><span class="sxs-lookup"><span data-stu-id="57681-108">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#_Configuring_single_sign-on)

-   [<span data-ttu-id="57681-109">Identificateur de l’utilisateur de sélectionner et ajouter l’application utilisateur attributs toobe envoyé toohello</span><span class="sxs-lookup"><span data-stu-id="57681-109">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="57681-110">Récupérer le certificat et les métadonnées Azure AD</span><span class="sxs-lookup"><span data-stu-id="57681-110">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="57681-111">Configurer les valeurs de métadonnées Azure AD dans l’application hello (authentification URL, l’émetteur, URL de déconnexion et un certificat)</span><span class="sxs-lookup"><span data-stu-id="57681-111">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#_Configuring_single_sign-on)

-   [<span data-ttu-id="57681-112">Affecter des utilisateurs toohello application</span><span class="sxs-lookup"><span data-stu-id="57681-112">Assign users toohello application</span></span>](#_Assign_users_to_the_application)

## <a name="configuring-single-sign-on-toonon-gallery-applications"></a><span data-ttu-id="57681-113">Configuration d’applications de l’authentification toonon-la galerie</span><span class="sxs-lookup"><span data-stu-id="57681-113">Configuring single sign-on toonon-gallery applications</span></span>

<span data-ttu-id="57681-114">tooconfigure l’authentification unique pour une application qui n’est pas dans la galerie d’Azure AD hello, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="57681-114">tooconfigure single sign-on for an application that is not in hello Azure AD gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="57681-115">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**</span><span class="sxs-lookup"><span data-stu-id="57681-115">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="57681-116">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="57681-116">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="57681-117">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="57681-117">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="57681-118">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="57681-118">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="57681-119">Cliquez sur hello **ajouter** bouton au coin supérieur droit de hello sur hello **des Applications d’entreprise** panneau.</span><span class="sxs-lookup"><span data-stu-id="57681-119">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="57681-120">Cliquez sur **application Non-gallery** Bonjour **ajouter votre propre application** section</span><span class="sxs-lookup"><span data-stu-id="57681-120">click **Non-gallery application** in hello **Add your own app** section</span></span>

7.  <span data-ttu-id="57681-121">Entrez le nom hello de l’application hello Bonjour **nom** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="57681-121">Enter hello name of hello application in hello **Name** textbox.</span></span>

8.  <span data-ttu-id="57681-122">Cliquez sur **ajouter** bouton, l’application de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="57681-122">Click **Add** button, tooadd hello application.</span></span>

9.  <span data-ttu-id="57681-123">Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="57681-123">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="57681-124">Sélectionnez **SAML-authentification** Bonjour **Mode** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="57681-124">Select **SAML-based Sign-on** in hello **Mode** dropdown.</span></span>

11. <span data-ttu-id="57681-125">Entrez les valeurs hello requis dans **URL et domaine.**</span><span class="sxs-lookup"><span data-stu-id="57681-125">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="57681-126">Vous devez obtenir ces valeurs à partir du fournisseur de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="57681-126">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="57681-127">application de hello tooconfigure en tant que l’authentification unique initiée par les fournisseurs d’identité, entrez hello URL de réponse et hello identificateur.</span><span class="sxs-lookup"><span data-stu-id="57681-127">tooconfigure hello application as IdP-initiated SSO, enter hello Reply URL and hello Identifier.</span></span>

   2. <span data-ttu-id="57681-128">**Facultatif :** application hello tooconfigure authentifications uniques initiées, hello signe sur l’URL, il est obligatoire.</span><span class="sxs-lookup"><span data-stu-id="57681-128">**Optional:** tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="57681-129">Bonjour **attributs utilisateur**, sélectionnez hello un identificateur unique pour vos utilisateurs Bonjour **identificateur de l’utilisateur** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="57681-129">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="57681-130">**Facultatif :** cliquez sur **afficher et modifier tous les autres attributs utilisateur** tooedit hello attributs application de toohello toobe envoyé dans un jeton SAML de hello lorsque l’utilisateur se connecter.</span><span class="sxs-lookup"><span data-stu-id="57681-130">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="57681-131">tooadd un attribut :</span><span class="sxs-lookup"><span data-stu-id="57681-131">tooadd an attribute:</span></span>

   1. <span data-ttu-id="57681-132">Cliquez sur **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="57681-132">click **Add attribute**.</span></span> <span data-ttu-id="57681-133">Entrez hello **nom** et Bonjour sélectionnez Bonjour **valeur** à partir de la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="57681-133">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="57681-134">Cliquez sur **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="57681-134">Click **Save.**</span></span> <span data-ttu-id="57681-135">Vous consultez hello nouvel attribut dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="57681-135">You see hello new attribute in hello table.</span></span>

14. <span data-ttu-id="57681-136">Cliquez sur **configurer &lt;nom de l’application&gt;**  documentation tooaccess sur la tooconfigure l’authentification unique dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="57681-136">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="57681-137">Possède également Azure AD URL et le certificat requis pour l’application hello.</span><span class="sxs-lookup"><span data-stu-id="57681-137">Also, you has Azure AD URLs and certificate required for hello application.</span></span>

15. [<span data-ttu-id="57681-138">Affecter des utilisateurs toohello application.</span><span class="sxs-lookup"><span data-stu-id="57681-138">Assign users toohello application.</span></span>](#assign-users-to-the-application)

## <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="57681-139">Identificateur de l’utilisateur de sélectionner et ajouter l’application utilisateur attributs toobe envoyé toohello</span><span class="sxs-lookup"><span data-stu-id="57681-139">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="57681-140">tooselect hello identificateur d’utilisateur ou ajouter des attributs d’utilisateur, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="57681-140">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="57681-141">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**</span><span class="sxs-lookup"><span data-stu-id="57681-141">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="57681-142">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="57681-142">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="57681-143">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="57681-143">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="57681-144">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="57681-144">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="57681-145">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="57681-145">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="57681-146">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="57681-146">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="57681-147">Sélectionnez l’application hello que vous avez configuré l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="57681-147">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="57681-148">Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="57681-148">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="57681-149">Sous hello **attributs utilisateur** section, sélectionnez hello un identificateur unique pour vos utilisateurs Bonjour **identificateur de l’utilisateur** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="57681-149">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="57681-150">Hello option sélectionnée doit valeur attendue toomatch hello utilisateur hello de tooauthenticate l’application hello.</span><span class="sxs-lookup"><span data-stu-id="57681-150">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

 ><span data-ttu-id="57681-151">[! Remarque} Azure AD, sélectionnez le format hello pour hello NameID identificateur d’attribut (utilisateur) en fonction de la valeur hello sélectionnée ou hello format demandé par l’application hello Bonjour SAML AuthRequest.</span><span class="sxs-lookup"><span data-stu-id="57681-151">[!NOTE} Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="57681-152">Pour plus d’informations, consultez l’article de hello [protocole SAML de l’authentification unique](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) sous hello section NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="57681-152">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
 >
 >

9.  <span data-ttu-id="57681-153">attributs d’utilisateur tooadd, cliquez sur **afficher et modifier tous les autres attributs de l’utilisateur** tooedit hello attributs application de toohello toobe envoyé dans un jeton SAML de hello lorsque l’utilisateur se connecter.</span><span class="sxs-lookup"><span data-stu-id="57681-153">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="57681-154">tooadd un attribut :</span><span class="sxs-lookup"><span data-stu-id="57681-154">tooadd an attribute:</span></span>

   1. <span data-ttu-id="57681-155">Cliquez sur **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="57681-155">click **Add attribute**.</span></span> <span data-ttu-id="57681-156">Entrez hello **nom** et Bonjour sélectionnez Bonjour **valeur** à partir de la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="57681-156">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="57681-157">Cliquez sur **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="57681-157">Click **Save.**</span></span> <span data-ttu-id="57681-158">Vous consultez hello nouvel attribut dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="57681-158">You see hello new attribute in hello table.</span></span>

## <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="57681-159">Télécharger des métadonnées Azure AD hello ou certificat</span><span class="sxs-lookup"><span data-stu-id="57681-159">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="57681-160">métadonnées de l’application hello toodownload ou un certificat d’Azure AD, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="57681-160">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="57681-161">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**</span><span class="sxs-lookup"><span data-stu-id="57681-161">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="57681-162">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="57681-162">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="57681-163">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="57681-163">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="57681-164">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="57681-164">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="57681-165">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="57681-165">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="57681-166">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="57681-166">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="57681-167">Sélectionnez l’application hello que vous avez configuré l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="57681-167">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="57681-168">Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="57681-168">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="57681-169">Accédez trop**le certificat de signature SAML** section, puis cliquez sur **télécharger** valeur de la colonne.</span><span class="sxs-lookup"><span data-stu-id="57681-169">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="57681-170">En fonction de l’application hello nécessite la configuration de l’authentification unique, vous voyez deux toodownload d’option hello hello Metadata XML ou hello du certificat.</span><span class="sxs-lookup"><span data-stu-id="57681-170">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="57681-171">Azure AD ne fournit pas une URL de métadonnées hello tooget.</span><span class="sxs-lookup"><span data-stu-id="57681-171">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="57681-172">Hello métadonnées peuvent uniquement être récupérées dans un fichier XML.</span><span class="sxs-lookup"><span data-stu-id="57681-172">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="assign-users-toohello-application"></a><span data-ttu-id="57681-173">Affecter des utilisateurs toohello application</span><span class="sxs-lookup"><span data-stu-id="57681-173">Assign users toohello application</span></span>

<span data-ttu-id="57681-174">tooassign un ou plusieurs utilisateurs tooan application directement, comme suit hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="57681-174">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="57681-175">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="57681-175">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="57681-176">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="57681-176">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="57681-177">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="57681-177">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="57681-178">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="57681-178">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="57681-179">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="57681-179">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="57681-180">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="57681-180">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="57681-181">Sélectionnez l’application hello tooassign une liste des utilisateurs toofrom hello.</span><span class="sxs-lookup"><span data-stu-id="57681-181">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="57681-182">Une fois le charge de l’application hello, cliquez sur **utilisateurs et groupes** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="57681-182">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="57681-183">Cliquez sur hello **ajouter** bouton par-dessus hello **utilisateurs et groupes** hello tooopen de liste **ajouter l’affectation** panneau.</span><span class="sxs-lookup"><span data-stu-id="57681-183">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="57681-184">Cliquez sur hello **utilisateurs et groupes** sélecteur de hello **ajouter l’affectation** panneau.</span><span class="sxs-lookup"><span data-stu-id="57681-184">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="57681-185">Type Bonjour **nom complet** ou **adresse de messagerie** d’utilisateur hello vous êtes intéressé par attribution dans hello **recherche par nom ou adresse de messagerie** zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="57681-185">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="57681-186">Placez le curseur sur hello **utilisateur** dans hello liste tooreveal un **case à cocher**.</span><span class="sxs-lookup"><span data-stu-id="57681-186">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="57681-187">Cliquez sur tooadd de photo ou le logo de profil hello case à cocher suivante toohello l’utilisateur à votre toohello utilisateur **sélectionnés** liste.</span><span class="sxs-lookup"><span data-stu-id="57681-187">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="57681-188">**Facultatif :** si vous souhaitez que trop**ajouter plusieurs utilisateurs**, type dans un autre **nom complet** ou **adresse de messagerie** dans hello **Rechercher par nom ou l’adresse de messagerie** zone de recherche, cliquez sur tooadd de case à cocher hello cette toohello utilisateur **sélectionnés** liste.</span><span class="sxs-lookup"><span data-stu-id="57681-188">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="57681-189">Lorsque vous avez fini de sélectionner les utilisateurs, cliquez sur hello **sélectionnez** bouton tooadd les toohello la liste des toobe utilisateurs et groupes affectés toohello application.</span><span class="sxs-lookup"><span data-stu-id="57681-189">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="57681-190">**Facultatif :** cliquez sur hello **sélectionner un rôle** sélecteur Bonjour **ajouter l’affectation** panneau tooselect un rôle aux utilisateurs de toohello tooassign que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="57681-190">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="57681-191">Cliquez sur hello **affecter** bouton tooassign hello application toohello les utilisateurs sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="57681-191">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="57681-192">Après une courte période de temps, les utilisateurs de hello que vous avez sélectionné en toolaunch en mesure de ces applications à l’aide de hello des méthodes décrites dans la section de description de solution hello.</span><span class="sxs-lookup"><span data-stu-id="57681-192">After a short period of time, hello users you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span>

## <a name="customizing-hello-saml-claims-sent-tooan-application"></a><span data-ttu-id="57681-193">Personnalisation des revendications SAML hello envoyé tooan application</span><span class="sxs-lookup"><span data-stu-id="57681-193">Customizing hello SAML claims sent tooan application</span></span>

<span data-ttu-id="57681-194">toolearn toocustomize hello SAML attribut revendications envoyées tooyour application, voir [revendications mappage dans Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="57681-194">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57681-195">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="57681-195">Next steps</span></span>
[<span data-ttu-id="57681-196">Fournissent des applications de tooyour de l’authentification unique avec le Proxy d’Application</span><span class="sxs-lookup"><span data-stu-id="57681-196">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
