---
title: "Erreur dans la page d’une application après la connexion | Microsoft Docs"
description: "Comment résoudre les problèmes de connexion à Azure AD quand l’application émet une erreur"
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
ms.openlocfilehash: a8cd93256f79ece268ec3411dfbdf590f4b24447
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="error-on-an-applications-page-after-signing-in"></a><span data-ttu-id="0bbac-103">Erreur dans la page d’une application après la connexion</span><span class="sxs-lookup"><span data-stu-id="0bbac-103">Error on an application's page after signing in</span></span>

<span data-ttu-id="0bbac-104">Dans ce scénario, Azure AD connecte l’utilisateur, mais l’application affiche une erreur qui empêche l’utilisateur de terminer le flux de connexion.</span><span class="sxs-lookup"><span data-stu-id="0bbac-104">In this scenario, Azure AD has signed the user in, but the application is displaying an error not allowing the user to successfully finish the sign in flow.</span></span> <span data-ttu-id="0bbac-105">Dans ce scénario, l’application n’accepte pas la réponse émise par Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0bbac-105">In this scenario, the application is not accepting the response issue by Azure AD.</span></span>

<span data-ttu-id="0bbac-106">Plusieurs raisons peuvent expliquer pourquoi l’application n’a pas accepté la réponse d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0bbac-106">There are some possible reasons why the application didn’t accept the response from Azure AD.</span></span> <span data-ttu-id="0bbac-107">Si l’erreur dans l’application n’est pas suffisamment détaillée pour savoir ce qui manque dans la réponse :</span><span class="sxs-lookup"><span data-stu-id="0bbac-107">If the error in the application is not clear enough to know what is missing in the response, then:</span></span>

-   <span data-ttu-id="0bbac-108">Si l’application est la galerie Azure AD, vérifiez que vous avez suivi toutes les étapes de l’article [Débogage d’une authentification unique basée sur SAML aux applications dans Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).</span><span class="sxs-lookup"><span data-stu-id="0bbac-108">If the application is the Azure AD Gallery, verify you have followed all the steps in the article [How to debug SAML-based single sign-on to applications in Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).</span></span>

-   <span data-ttu-id="0bbac-109">Utilisez un outil tel que [Fiddler](http://www.telerik.com/fiddler) pour capturer la demande, la réponse et le jeton SAML.</span><span class="sxs-lookup"><span data-stu-id="0bbac-109">Use a tool like [Fiddler](http://www.telerik.com/fiddler) to capture SAML request, SAML response and SAML token.</span></span>

-   <span data-ttu-id="0bbac-110">Partagez la réponse SAML avec le fournisseur de l’application pour savoir ce qui manque.</span><span class="sxs-lookup"><span data-stu-id="0bbac-110">Share the SAML response with the application vendor to know what is missing.</span></span>

## <a name="missing-attributes-in-the-saml-response"></a><span data-ttu-id="0bbac-111">Attributs manquants dans la réponse SAML</span><span class="sxs-lookup"><span data-stu-id="0bbac-111">Missing attributes in the SAML response</span></span>

<span data-ttu-id="0bbac-112">Pour ajouter un attribut dans la configuration Azure AD à envoyer dans la réponse Azure AD, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0bbac-112">To add an attribute in the Azure AD configuration to be sent in the Azure AD response, follow the steps below:</span></span>

1.  <span data-ttu-id="0bbac-113">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général** ou **coadministrateur**.</span><span class="sxs-lookup"><span data-stu-id="0bbac-113">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="0bbac-114">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="0bbac-114">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="0bbac-115">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0bbac-115">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="0bbac-116">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0bbac-116">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="0bbac-117">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="0bbac-117">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="0bbac-118">Si l’application que vous recherchez ne figure pas dans la liste, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications.**</span><span class="sxs-lookup"><span data-stu-id="0bbac-118">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="0bbac-119">Sélectionnez l’application pour laquelle vous souhaitez configurer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="0bbac-119">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="0bbac-120">Une fois l’application chargée, cliquez sur **Authentification unique** dans le menu de navigation de gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="0bbac-120">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="0bbac-121">Cliquez sur **Afficher et modifier tous les autres attributs utilisateur** sous **Attributs utilisateur** pour modifier les attributs à envoyer à l’application dans le jeton SAML quand l’utilisateur se connecte.</span><span class="sxs-lookup"><span data-stu-id="0bbac-121">click **View and edit all other user attributes under** the **User Attributes** section to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="0bbac-122">Pour ajouter un attribut :</span><span class="sxs-lookup"><span data-stu-id="0bbac-122">To add an attribute:</span></span>

   * <span data-ttu-id="0bbac-123">Cliquez sur **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="0bbac-123">click **Add attribute**.</span></span> <span data-ttu-id="0bbac-124">Entrez le **Nom**, puis sélectionnez la **Valeur** dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="0bbac-124">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   * <span data-ttu-id="0bbac-125">Cliquez sur **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="0bbac-125">Click **Save.**</span></span> <span data-ttu-id="0bbac-126">Le nouvel attribut s’affiche dans le tableau.</span><span class="sxs-lookup"><span data-stu-id="0bbac-126">You see the new attribute in the table.</span></span>

9.  <span data-ttu-id="0bbac-127">Enregistrez la configuration.</span><span class="sxs-lookup"><span data-stu-id="0bbac-127">Save the configuration.</span></span>

<span data-ttu-id="0bbac-128">La prochaine fois que l’utilisateur se connectera à l’application, Azure AD enverra le nouvel attribut dans la réponse SAML.</span><span class="sxs-lookup"><span data-stu-id="0bbac-128">Next time the user signs in to the application, Azure AD send the new attribute in the SAML response.</span></span>

## <a name="the-application-expects-a-different-user-identifier-value-or-format"></a><span data-ttu-id="0bbac-129">L’application attend une valeur ou un format d’identificateur d’utilisateur différent</span><span class="sxs-lookup"><span data-stu-id="0bbac-129">The application expects a different User Identifier value or format</span></span>

<span data-ttu-id="0bbac-130">La connexion à l’application échoue parce que la réponse SAML ne comprend pas certains attributs tels que des rôles ou parce que l’application attend un format différent pour l’attribut EntityID.</span><span class="sxs-lookup"><span data-stu-id="0bbac-130">The sign-in to the application is failing because the SAML response is missing attributes such as roles or because the application is expecting a different format for the EntityID attribute.</span></span>

## <a name="add-an-attribute-in-the-azure-ad-application-configuration"></a><span data-ttu-id="0bbac-131">Ajoutez un attribut dans la configuration de l’application Azure AD :</span><span class="sxs-lookup"><span data-stu-id="0bbac-131">Add an attribute in the Azure AD application configuration:</span></span>

<span data-ttu-id="0bbac-132">Pour changer la valeur de l’identificateur d’utilisateur, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0bbac-132">To change the User Identifier value, follow the steps below:</span></span>

1.  <span data-ttu-id="0bbac-133">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général** ou **coadministrateur**.</span><span class="sxs-lookup"><span data-stu-id="0bbac-133">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="0bbac-134">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="0bbac-134">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="0bbac-135">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0bbac-135">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="0bbac-136">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0bbac-136">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="0bbac-137">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="0bbac-137">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="0bbac-138">Si l’application que vous recherchez ne figure pas dans la liste, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications.**</span><span class="sxs-lookup"><span data-stu-id="0bbac-138">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="0bbac-139">Sélectionnez l’application pour laquelle vous souhaitez configurer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="0bbac-139">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="0bbac-140">Une fois l’application chargée, cliquez sur **Authentification unique** dans le menu de navigation de gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="0bbac-140">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="0bbac-141">Sous **Attributs d’utilisateur**, sélectionnez l’identificateur unique de vos utilisateurs dans la liste déroulante **Identificateur de l’utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="0bbac-141">Under the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

## <a name="change-entityid-user-identifier-format"></a><span data-ttu-id="0bbac-142">Changer le format d’EntityID (identificateur d’utilisateur)</span><span class="sxs-lookup"><span data-stu-id="0bbac-142">Change EntityID (User Identifier) format</span></span>

<span data-ttu-id="0bbac-143">Si l’application attend un autre format pour l’attribut EntityID,</span><span class="sxs-lookup"><span data-stu-id="0bbac-143">If the application expects another format for the EntityID attribute.</span></span> <span data-ttu-id="0bbac-144">vous ne pouvez pas sélectionner le format d’EntityID (identificateur d’utilisateur) qu’Azure AD envoie à l’application dans la réponse après l’authentification de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0bbac-144">Then, you won’t be able to select the EntityID (User Identifier) format that Azure AD sends to the application in the response after user authentication.</span></span>

<span data-ttu-id="0bbac-145">Azure AD sélectionne le format de l’attribut NameID (identificateur d’utilisateur) en fonction de la valeur sélectionnée ou du format demandé par l’application dans la demande d’authentification SAML.</span><span class="sxs-lookup"><span data-stu-id="0bbac-145">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="0bbac-146">Pour plus d’informations, consultez l’article [Protocole SAML d’authentification unique](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) dans la section NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="0bbac-146">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>

## <a name="the-application-expects-a-different-signature-method-for-the-saml-response"></a><span data-ttu-id="0bbac-147">L’application attend une méthode de signature différente pour la réponse SAML</span><span class="sxs-lookup"><span data-stu-id="0bbac-147">The application expects a different signature method for the SAML response</span></span>

<span data-ttu-id="0bbac-148">Pour modifier les parties du jeton SAML qui sont signées numériquement par Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0bbac-148">To change what parts of the SAML token are digitally signed by Azure Active Directory.</span></span> <span data-ttu-id="0bbac-149">Pour ce faire, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0bbac-149">Follow the steps below:</span></span>

1.  <span data-ttu-id="0bbac-150">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général** ou **coadministrateur**.</span><span class="sxs-lookup"><span data-stu-id="0bbac-150">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="0bbac-151">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="0bbac-151">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="0bbac-152">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0bbac-152">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="0bbac-153">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0bbac-153">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="0bbac-154">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="0bbac-154">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="0bbac-155">Si l’application que vous recherchez ne figure pas dans la liste, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications.**</span><span class="sxs-lookup"><span data-stu-id="0bbac-155">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="0bbac-156">Sélectionnez l’application pour laquelle vous souhaitez configurer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="0bbac-156">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="0bbac-157">Une fois l’application chargée, cliquez sur **Authentification unique** dans le menu de navigation de gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="0bbac-157">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="0bbac-158">Cliquez sur **Afficher les paramètres avancés de signature de certificat** dans la section **Certificat de signature SAML**.</span><span class="sxs-lookup"><span data-stu-id="0bbac-158">click **Show advanced certificate signing settings** under the **SAML Signing Certificate** section.</span></span>

9.  <span data-ttu-id="0bbac-159">Sélectionnez l’**Option de signature** appropriée attendue par l’application :</span><span class="sxs-lookup"><span data-stu-id="0bbac-159">Select the appropriate **Signing Option** expected by the application:</span></span>

  * <span data-ttu-id="0bbac-160">Signer la réponse SAML</span><span class="sxs-lookup"><span data-stu-id="0bbac-160">Sign SAML response</span></span>

  * <span data-ttu-id="0bbac-161">Signer la réponse et l’assertion SAML</span><span class="sxs-lookup"><span data-stu-id="0bbac-161">Sign SAML response and assertion</span></span>

  * <span data-ttu-id="0bbac-162">Signer l’assertion SAML</span><span class="sxs-lookup"><span data-stu-id="0bbac-162">Sign SAML assertion</span></span>

<span data-ttu-id="0bbac-163">La prochaine fois que l’utilisateur se connectera à l’application, Azure AD signera la partie de la réponse SAML sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="0bbac-163">Next time the user signs in to the application, Azure AD sign the part of the SAML response selected.</span></span>

## <a name="the-application-expects-the-signing-algorithm-to-be-sha-1"></a><span data-ttu-id="0bbac-164">L’application attend l’algorithme de signature SHA-1</span><span class="sxs-lookup"><span data-stu-id="0bbac-164">The application expects the signing algorithm to be SHA-1</span></span>

<span data-ttu-id="0bbac-165">Par défaut, Azure AD signe le jeton SAML à l’aide de l’algorithme le plus sécurisé.</span><span class="sxs-lookup"><span data-stu-id="0bbac-165">By default, Azure AD signs the SAML token using the most security algorithm.</span></span> <span data-ttu-id="0bbac-166">Il n’est pas recommandé de remplacer l’algorithme de connexion par SHA-1, sauf si l’application l’exige.</span><span class="sxs-lookup"><span data-stu-id="0bbac-166">Changing the sign algorithm to SHA-1 is not recommended unless required by the application.</span></span>

<span data-ttu-id="0bbac-167">Pour changer l’algorithme de signature, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0bbac-167">To change the signing algorithm, follow the steps below:</span></span>

1.  <span data-ttu-id="0bbac-168">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général** ou **coadministrateur**.</span><span class="sxs-lookup"><span data-stu-id="0bbac-168">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="0bbac-169">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="0bbac-169">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="0bbac-170">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0bbac-170">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="0bbac-171">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0bbac-171">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="0bbac-172">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="0bbac-172">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="0bbac-173">Si l’application que vous recherchez ne figure pas dans la liste, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications.**</span><span class="sxs-lookup"><span data-stu-id="0bbac-173">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="0bbac-174">Sélectionnez l’application pour laquelle vous souhaitez configurer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="0bbac-174">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="0bbac-175">Une fois l’application chargée, cliquez sur **Authentification unique** dans le menu de navigation de gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="0bbac-175">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="0bbac-176">Cliquez sur **Afficher les paramètres avancés de signature de certificat** dans la section **Certificat de signature SAML**.</span><span class="sxs-lookup"><span data-stu-id="0bbac-176">click **Show advanced certificate signing settings** under the **SAML Signing Certificate** section.</span></span>

9.  <span data-ttu-id="0bbac-177">Sélectionnez SHA-1 dans **Algorithme de signature**.</span><span class="sxs-lookup"><span data-stu-id="0bbac-177">Select SHA-1, in the **Signing Algorithm**.</span></span>

<span data-ttu-id="0bbac-178">La prochaine fois que l’utilisateur se connectera à l’application, Azure AD signera le jeton SAML à l’aide de l’algorithme SHA-1.</span><span class="sxs-lookup"><span data-stu-id="0bbac-178">Next time the user signs in to the application, Azure AD sign the SAML token using SHA-1 algorithm.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0bbac-179">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0bbac-179">Next steps</span></span>
[<span data-ttu-id="0bbac-180">Débogage d’une authentification unique basée sur SAML aux applications dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0bbac-180">How to debug SAML-based single sign-on to applications in Azure Active Directory</span></span>](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging)
