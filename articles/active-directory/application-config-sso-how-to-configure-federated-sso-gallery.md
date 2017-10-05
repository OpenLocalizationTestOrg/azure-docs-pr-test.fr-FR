---
title: "Comment configurer l’authentification unique fédérée pour une application de la galerie Azure AD | Microsoft Docs"
description: "Comment configurer l’authentification unique fédérée pour une application de la galerie Azure AD existante et utiliser les didacticiels pour se lancer rapidement"
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
ms.openlocfilehash: 1b1d00718981b2c7d11f5b88428d02e16dd0b34d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="adf8d-103">Comment configurer l’authentification unique fédérée pour une application de la galerie Azure AD</span><span class="sxs-lookup"><span data-stu-id="adf8d-103">How to configure federated single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="adf8d-104">Un didacticiel pas à pas est disponible pour toutes les applications de la galerie Azure AD dans lesquelles est activée la fonctionnalité Enterprise Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="adf8d-104">All applications in the Azure AD gallery enabled with Enterprise single sign-on capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="adf8d-105">Pour une aide pas à pas détaillée, vous pouvez accéder à la [Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/).</span><span class="sxs-lookup"><span data-stu-id="adf8d-105">You can access the [List of tutorials on how to integrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for detailed step-by-step guidance.</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="adf8d-106">Vue d’ensemble des étapes requises</span><span class="sxs-lookup"><span data-stu-id="adf8d-106">Overview of steps required</span></span>
<span data-ttu-id="adf8d-107">Pour configurer une application à partir de la galerie Azure AD, vous devez effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="adf8d-107">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="adf8d-108">Ajouter une application à partir de la galerie Azure AD</span><span class="sxs-lookup"><span data-stu-id="adf8d-108">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="adf8d-109">Configurer les valeurs de métadonnées de l’application dans Azure AD (URL de connexion, identificateur, URL de réponse)</span><span class="sxs-lookup"><span data-stu-id="adf8d-109">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="adf8d-110">Sélectionner l’identificateur de l’utilisateur et ajouter les attributs d’utilisateur à envoyer à l’application</span><span class="sxs-lookup"><span data-stu-id="adf8d-110">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="adf8d-111">Récupérer le certificat et les métadonnées Azure AD</span><span class="sxs-lookup"><span data-stu-id="adf8d-111">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="adf8d-112">Configurer les valeurs de métadonnées Azure AD dans l’application (URL de connexion, émetteur, URL de déconnexion et certificat)</span><span class="sxs-lookup"><span data-stu-id="adf8d-112">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="adf8d-113">Affecter des utilisateurs à l’application</span><span class="sxs-lookup"><span data-stu-id="adf8d-113">Assign users to the application</span></span>](#assign-users-to-the-application)

## <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="adf8d-114">Ajouter une application à partir de la galerie Azure AD</span><span class="sxs-lookup"><span data-stu-id="adf8d-114">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="adf8d-115">Pour ajouter une application à partir de la galerie Azure AD, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="adf8d-115">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="adf8d-116">Ouvrez le [portail Azure](https://portal.azure.com) et connectez-vous en tant qu’**administrateur général** ou **coadministrateur**</span><span class="sxs-lookup"><span data-stu-id="adf8d-116">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="adf8d-117">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="adf8d-117">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="adf8d-118">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="adf8d-118">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="adf8d-119">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="adf8d-119">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="adf8d-120">Cliquez sur le bouton **Ajouter** dans le coin supérieur droit du panneau **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="adf8d-120">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="adf8d-121">Dans la zone de texte **Entrer un nom** de la section **Ajouter à partir de la galerie**, tapez le nom de l’application.</span><span class="sxs-lookup"><span data-stu-id="adf8d-121">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="adf8d-122">Sélectionnez l’application pour laquelle vous souhaitez configurer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="adf8d-122">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="adf8d-123">Avant d’ajouter l’application, vous pouvez la renommer dans la zone de texte **Nom**.</span><span class="sxs-lookup"><span data-stu-id="adf8d-123">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="adf8d-124">Pour ajouter l’application, cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="adf8d-124">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="adf8d-125">Après une courte période, vous pourrez voir le panneau de configuration de l’application.</span><span class="sxs-lookup"><span data-stu-id="adf8d-125">After a short period of time, you be able to see the application’s configuration blade.</span></span>

## <a name="configure-single-sign-on-for-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="adf8d-126">Configurer l’authentification unique pour une application à partir de la galerie Azure AD</span><span class="sxs-lookup"><span data-stu-id="adf8d-126">Configure single sign-on for an application from the Azure AD gallery</span></span>

<span data-ttu-id="adf8d-127">Pour configurer l’authentification unique pour une application, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="adf8d-127">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="adf8d-128">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général** ou **coadministrateur**.</span><span class="sxs-lookup"><span data-stu-id="adf8d-128">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="adf8d-129">Ouvrez l’**extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="adf8d-129">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="adf8d-130">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="adf8d-130">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="adf8d-131">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="adf8d-131">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="adf8d-132">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="adf8d-132">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="adf8d-133">Si l’application que vous recherchez ne figure pas dans la liste, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications.**</span><span class="sxs-lookup"><span data-stu-id="adf8d-133">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="adf8d-134">Sélectionnez l’application pour laquelle vous souhaitez configurer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="adf8d-134">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="adf8d-135">Une fois l’application chargée, cliquez sur **Authentification unique** dans le menu de navigation de gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="adf8d-135">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="adf8d-136">Sélectionnez **Authentification basée sur SAML** dans la liste déroulante **Mode**.</span><span class="sxs-lookup"><span data-stu-id="adf8d-136">Select **SAML-based Sign-on** from the **Mode** dropdown.</span></span>

9.  <span data-ttu-id="adf8d-137">Entrez les valeurs obligatoires dans **Domaine et URL.**</span><span class="sxs-lookup"><span data-stu-id="adf8d-137">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="adf8d-138">Ces valeurs doivent vous être communiquées par le fournisseur de l’application.</span><span class="sxs-lookup"><span data-stu-id="adf8d-138">You should get these values from the application vendor.</span></span>

   1. <span data-ttu-id="adf8d-139">Pour configurer l’application en tant qu’application à authentification unique lancée par le fournisseur de services, une URL de connexion est obligatoire.</span><span class="sxs-lookup"><span data-stu-id="adf8d-139">To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span> <span data-ttu-id="adf8d-140">Pour certaines applications, l’identificateur est également une valeur obligatoire.</span><span class="sxs-lookup"><span data-stu-id="adf8d-140">For some applications, the Identifier is also a required value.</span></span>

   2. <span data-ttu-id="adf8d-141">Pour configurer l’application en tant qu’application à authentification unique lancée par le fournisseur d’identité, une URL de réponse est obligatoire.</span><span class="sxs-lookup"><span data-stu-id="adf8d-141">To configure the application as IdP-initiated SSO, the Reply URL it’s a required value.</span></span> <span data-ttu-id="adf8d-142">Pour certaines applications, l’identificateur est également une valeur obligatoire.</span><span class="sxs-lookup"><span data-stu-id="adf8d-142">For some applications, the Identifier is also a required value.</span></span>

10. <span data-ttu-id="adf8d-143">**Facultatif** : pour afficher les valeurs non obligatoires, cliquez sur **Afficher les paramètres d’URL avancés**.</span><span class="sxs-lookup"><span data-stu-id="adf8d-143">**Optional:** click **Show advanced URL settings** if you want to see the non-required values.</span></span>

11. <span data-ttu-id="adf8d-144">Dans **Attributs d’utilisateur**, sélectionnez l’identificateur unique de vos utilisateurs dans la liste déroulante **Identificateur de l’utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="adf8d-144">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="adf8d-145">**Facultatif** : pour modifier les attributs à envoyer à l’application dans le jeton SAML lorsque l’utilisateur se connecte, cliquez sur **Afficher et modifier tous les autres attributs utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="adf8d-145">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

  <span data-ttu-id="adf8d-146">Pour ajouter un attribut :</span><span class="sxs-lookup"><span data-stu-id="adf8d-146">To add an attribute:</span></span>
   
   1. <span data-ttu-id="adf8d-147">Cliquez sur **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="adf8d-147">click **Add attribute**.</span></span> <span data-ttu-id="adf8d-148">Entrez le **Nom**, puis sélectionnez la **Valeur** dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="adf8d-148">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   1. <span data-ttu-id="adf8d-149">Cliquez sur **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="adf8d-149">Click **Save.**</span></span> <span data-ttu-id="adf8d-150">Le nouvel attribut s’affiche dans le tableau.</span><span class="sxs-lookup"><span data-stu-id="adf8d-150">You see the new attribute in the table.</span></span>

13. <span data-ttu-id="adf8d-151">Cliquez sur **Configurer &lt;nom de l’application&gt;** pour accéder à la documentation sur la façon de configurer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="adf8d-151">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="adf8d-152">En outre, vous disposez des URL de métadonnées et du certificat nécessaires à la configuration de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="adf8d-152">Also, you has the metadata URLs and certificate required to setup SSO with the application.</span></span>

14. <span data-ttu-id="adf8d-153">Pour enregistrer la configuration, cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="adf8d-153">Click **Save** to save the configuration.</span></span>

15. <span data-ttu-id="adf8d-154">Affectez des utilisateurs à l’application.</span><span class="sxs-lookup"><span data-stu-id="adf8d-154">Assign users to the application.</span></span>

## <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="adf8d-155">Sélectionner l’identificateur de l’utilisateur et ajouter les attributs d’utilisateur à envoyer à l’application</span><span class="sxs-lookup"><span data-stu-id="adf8d-155">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="adf8d-156">Pour sélectionner l’identificateur de l’utilisateur ou ajouter des attributs d’utilisateur, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="adf8d-156">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="adf8d-157">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général** ou **coadministrateur**</span><span class="sxs-lookup"><span data-stu-id="adf8d-157">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="adf8d-158">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="adf8d-158">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="adf8d-159">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="adf8d-159">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="adf8d-160">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="adf8d-160">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="adf8d-161">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="adf8d-161">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="adf8d-162">Si l’application que vous recherchez ne figure pas dans la liste, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications.**</span><span class="sxs-lookup"><span data-stu-id="adf8d-162">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="adf8d-163">Sélectionnez l’application pour laquelle vous avez configuré l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="adf8d-163">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="adf8d-164">Une fois l’application chargée, cliquez sur **Authentification unique** dans le menu de navigation de gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="adf8d-164">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="adf8d-165">Dans la section **Attributs d’utilisateur**, sélectionnez l’identificateur unique de vos utilisateurs dans la liste déroulante **Identificateur de l’utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="adf8d-165">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="adf8d-166">L’option sélectionnée doit correspondre à la valeur attendue dans l’application pour authentifier l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="adf8d-166">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

  >[!NOTE] 
  ><span data-ttu-id="adf8d-167">Azure AD sélectionne le format de l’attribut NameID (Identificateur d’utilisateur) en fonction de la valeur sélectionnée ou du format demandé par l’application dans la demande d’authentification SAML.</span><span class="sxs-lookup"><span data-stu-id="adf8d-167">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="adf8d-168">Pour plus d’informations, consultez l’article [Protocole SAML d’authentification unique](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) dans la section NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="adf8d-168">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
  >
  >

9.  <span data-ttu-id="adf8d-169">Pour ajouter des attributs d’utilisateur, cliquez sur **Afficher et modifier tous les autres attributs utilisateur** afin de modifier les attributs à envoyer à l’application dans le jeton SAML lorsque l’utilisateur se connecte.</span><span class="sxs-lookup"><span data-stu-id="adf8d-169">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="adf8d-170">Pour ajouter un attribut :</span><span class="sxs-lookup"><span data-stu-id="adf8d-170">To add an attribute:</span></span>
  
   1. <span data-ttu-id="adf8d-171">Cliquez sur **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="adf8d-171">click **Add attribute**.</span></span> <span data-ttu-id="adf8d-172">Entrez le **Nom**, puis sélectionnez la **Valeur** dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="adf8d-172">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="adf8d-173">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="adf8d-173">Click **Save**.</span></span> <span data-ttu-id="adf8d-174">Le nouvel attribut s’affiche dans le tableau.</span><span class="sxs-lookup"><span data-stu-id="adf8d-174">You see the new attribute in the table.</span></span>

## <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="adf8d-175">Télécharger les métadonnées ou le certificat Azure AD</span><span class="sxs-lookup"><span data-stu-id="adf8d-175">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="adf8d-176">Pour télécharger les métadonnées ou le certificat de l’application à partir d’Azure AD, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="adf8d-176">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="adf8d-177">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général** ou **coadministrateur**</span><span class="sxs-lookup"><span data-stu-id="adf8d-177">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="adf8d-178">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="adf8d-178">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="adf8d-179">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="adf8d-179">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="adf8d-180">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="adf8d-180">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="adf8d-181">Cliquez sur **Toutes les applications** pour afficher la liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="adf8d-181">click **All Applications** to view a list of all your applications.</span></span>

  *  <span data-ttu-id="adf8d-182">Si l’application que vous recherchez ne figure pas dans la liste, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="adf8d-182">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications**.</span></span>

6.  <span data-ttu-id="adf8d-183">Sélectionnez l’application pour laquelle vous avez configuré l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="adf8d-183">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="adf8d-184">Une fois l’application chargée, cliquez sur **Authentification unique** dans le menu de navigation de gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="adf8d-184">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="adf8d-185">Accédez à la section **Certificat de signature SAML**, puis cliquez sur la valeur de colonne **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="adf8d-185">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="adf8d-186">En fonction de ce que l’application nécessite pour configurer l’authentification unique, vous voyez soit l’option de téléchargement des métadonnées XML, soit le certificat.</span><span class="sxs-lookup"><span data-stu-id="adf8d-186">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="adf8d-187">Azure AD ne fournit pas d’URL permettant d’obtenir les métadonnées.</span><span class="sxs-lookup"><span data-stu-id="adf8d-187">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="adf8d-188">Les métadonnées peuvent uniquement être récupérées sous forme de fichier XML.</span><span class="sxs-lookup"><span data-stu-id="adf8d-188">The metadata can only be retrieved as a XML file.</span></span>

## <a name="assign-users-to-the-application"></a><span data-ttu-id="adf8d-189">Affecter des utilisateurs à l’application</span><span class="sxs-lookup"><span data-stu-id="adf8d-189">Assign users to the application</span></span>

<span data-ttu-id="adf8d-190">Pour affecter un ou plusieurs utilisateurs directement à une application, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="adf8d-190">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="adf8d-191">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général.**</span><span class="sxs-lookup"><span data-stu-id="adf8d-191">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="adf8d-192">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="adf8d-192">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="adf8d-193">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="adf8d-193">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="adf8d-194">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="adf8d-194">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="adf8d-195">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="adf8d-195">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="adf8d-196">Si l’application que vous recherchez ne figure pas dans la liste, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications.**</span><span class="sxs-lookup"><span data-stu-id="adf8d-196">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="adf8d-197">Dans la liste qui s’affiche, sélectionnez l’application à laquelle vous souhaitez affecter un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="adf8d-197">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="adf8d-198">Une fois l’application chargée, cliquez sur **Utilisateurs et groupes** dans le menu de navigation de gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="adf8d-198">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="adf8d-199">Cliquez sur le bouton **Ajouter** en haut de la liste **Utilisateurs et groupes** pour ouvrir le panneau **Ajouter une attribution**.</span><span class="sxs-lookup"><span data-stu-id="adf8d-199">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="adf8d-200">Cliquez sur le sélecteur **Utilisateurs et groupes** à partir du panneau **Ajouter une attribution**.</span><span class="sxs-lookup"><span data-stu-id="adf8d-200">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="adf8d-201">Tapez **le nom complet** ou **l’adresse de messagerie** de l’utilisateur souhaité pour l’attribution dans la zone de recherche **Rechercher par nom ou adresse de messagerie**.</span><span class="sxs-lookup"><span data-stu-id="adf8d-201">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="adf8d-202">Pointez sur **l’utilisateur** dans la liste pour afficher une **case à cocher**.</span><span class="sxs-lookup"><span data-stu-id="adf8d-202">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="adf8d-203">Cliquez sur la case à cocher en regard de la photo de profil ou du logo de l’utilisateur pour ajouter ce dernier à la liste **Sélectionné**.</span><span class="sxs-lookup"><span data-stu-id="adf8d-203">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="adf8d-204">**Facultatif :** si vous souhaitez **ajouter plusieurs utilisateurs**, entrez un autre **nom complet** ou une autre **adresse de messagerie** dans la zone de recherche **Rechercher par nom ou adresse de messagerie**, puis cliquez sur la case à cocher pour ajouter cet utilisateur à la liste **Sélectionné**.</span><span class="sxs-lookup"><span data-stu-id="adf8d-204">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="adf8d-205">Après avoir sélectionné les utilisateurs, cliquez sur le bouton **Sélectionner** pour les ajouter à la liste des utilisateurs et des groupes à affecter à l’application.</span><span class="sxs-lookup"><span data-stu-id="adf8d-205">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="adf8d-206">**Facultatif :** cliquez sur le sélecteur **Sélectionner un rôle** dans le panneau **Ajouter une attribution** pour sélectionner un rôle à affecter aux utilisateurs que vous avez sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="adf8d-206">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="adf8d-207">Cliquez sur le bouton **Attribuer** pour affecter l’application aux utilisateurs sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="adf8d-207">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="adf8d-208">Après quelques instants, les utilisateurs que vous avez sélectionnés seront en mesure de démarrer ces applications à l’aide des méthodes décrites dans la section de description des solutions.</span><span class="sxs-lookup"><span data-stu-id="adf8d-208">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span></span>

## <a name="customizing-the-saml-claims-sent-to-an-application"></a><span data-ttu-id="adf8d-209">Personnaliser des revendications SAML envoyées à une application</span><span class="sxs-lookup"><span data-stu-id="adf8d-209">Customizing the SAML claims sent to an application</span></span>

<span data-ttu-id="adf8d-210">Pour savoir comment personnaliser les revendications d’attribut SAML envoyées à votre application, consultez l’article [Mappage des revendications dans Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="adf8d-210">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="adf8d-211">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="adf8d-211">Next steps</span></span>
[<span data-ttu-id="adf8d-212">Fournir une authentification unique à vos applications avec le proxy d’application</span><span class="sxs-lookup"><span data-stu-id="adf8d-212">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)



