---
title: "Une application affectée n’apparaît pas sur le volet d’accès | Microsoft Docs"
description: "Identifier pourquoi une application n’apparaît pas sur le volet d’accès"
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
ms.openlocfilehash: 9ea5744d77b90929598ea5feb80c7bbdff3772fc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="an-assigned-application-is-not-appearing-on-the-access-panel"></a><span data-ttu-id="172db-103">Une application affectée n’apparaît pas sur le volet d’accès</span><span class="sxs-lookup"><span data-stu-id="172db-103">An assigned application is not appearing on the access panel</span></span>

<span data-ttu-id="172db-104">Le volet d’accès est un portail Web qui permet à un utilisateur disposant d’un compte professionnel ou scolaire dans Azure Active Directory (Azure AD) d’afficher et de démarrer des applications basées sur le cloud auxquelles l’administrateur Azure AD lui a accordé un accès.</span><span class="sxs-lookup"><span data-stu-id="172db-104">The Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="172db-105">Ces applications sont configurées pour le compte de l’utilisateur dans le portail Azure AD.</span><span class="sxs-lookup"><span data-stu-id="172db-105">These applications are configured on behalf of the user in the Azure AD portal.</span></span> <span data-ttu-id="172db-106">Pour que l’application soit visible dans le volet d’accès, elle doit être correctement configurée et affectée à l’utilisateur ou à un groupe dont est membre l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="172db-106">The application must be configured properly and assigned to the user or a group the user is a member of to see the application in the Access Panel.</span></span>

<span data-ttu-id="172db-107">Les types d’applications que peut voir l’utilisateur tombent dans les catégories suivantes :</span><span class="sxs-lookup"><span data-stu-id="172db-107">The type of apps a user may be seeing fall in the following categories:</span></span>

-   <span data-ttu-id="172db-108">Applications Office 365</span><span class="sxs-lookup"><span data-stu-id="172db-108">Office 365 Applications</span></span>

-   <span data-ttu-id="172db-109">Applications Microsoft et tierces configurées avec l’authentification unique (SSO) basée sur la fédération</span><span class="sxs-lookup"><span data-stu-id="172db-109">Microsoft and third-party applications configured with federation-based SSO</span></span>

-   <span data-ttu-id="172db-110">Applications à authentification unique (SSO) par mot de passe</span><span class="sxs-lookup"><span data-stu-id="172db-110">Password-based SSO applications</span></span>

-   <span data-ttu-id="172db-111">Applications avec solutions d’authentification unique (SSO) existantes</span><span class="sxs-lookup"><span data-stu-id="172db-111">Applications with existing SSO solutions</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="172db-112">Problèmes d’ordre général à vérifier en premier</span><span class="sxs-lookup"><span data-stu-id="172db-112">General issues to check first</span></span>

-   <span data-ttu-id="172db-113">Si une application vient d’être ajoutée pour un utilisateur, essayez de vous connecter / déconnecter de nouveau sur le volet d’accès de l’utilisateur après quelques minutes pour voir si l’application a été ajoutée.</span><span class="sxs-lookup"><span data-stu-id="172db-113">If an application was just added to a user, try to sign in and out again into the user’s Access Panel after a few minutes to see if the application is added.</span></span>

-   <span data-ttu-id="172db-114">Si une licence vient d’être supprimée pour un utilisateur ou un groupe dont l’utilisateur est membre, la prise en compte des modifications peut prendre du temps, en fonction de la taille et de la complexité du groupe.</span><span class="sxs-lookup"><span data-stu-id="172db-114">If a license was just removed from a user or group the user is a member of this may take a long time, depending on the size and complexity of the group for changes to be made.</span></span> <span data-ttu-id="172db-115">Prévoyez du temps supplémentaire avant de vous connecter au volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="172db-115">Allow for extra time before signing into the Access Panel.</span></span>

## <a name="problems-related-to-application-configuration"></a><span data-ttu-id="172db-116">Problèmes liés à la configuration d’applications</span><span class="sxs-lookup"><span data-stu-id="172db-116">Problems related to application configuration</span></span>

<span data-ttu-id="172db-117">Une application n’apparaît peut-être pas dans le volet d’accès d’un utilisateur en raison d’une mauvaise configuration.</span><span class="sxs-lookup"><span data-stu-id="172db-117">An application may not be appearing in a user’s Access Panel because it is not configured properly.</span></span> <span data-ttu-id="172db-118">Voici quelques méthodes pour résoudre les problèmes liés à la configuration d’applications :</span><span class="sxs-lookup"><span data-stu-id="172db-118">Below are some ways you can troubleshoot issues related to application configuration:</span></span>

-   [<span data-ttu-id="172db-119">Comment configurer l’authentification unique fédérée pour une application de la galerie Azure AD</span><span class="sxs-lookup"><span data-stu-id="172db-119">How to configure federated single sign-on for an Azure AD gallery application</span></span>](#how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application)

-   [<span data-ttu-id="172db-120">Comment configurer l’authentification unique fédérée pour une application non issue de la galerie</span><span class="sxs-lookup"><span data-stu-id="172db-120">How to configure federated single sign-on for a non-gallery application</span></span>](#how-to-configure-federated-single-sign-on-for-a-non-gallery-application)

-   [<span data-ttu-id="172db-121">Comment configurer l’authentification unique avec mot de passe pour une application de la galerie Azure AD</span><span class="sxs-lookup"><span data-stu-id="172db-121">How to configure a password single sign-on application for an Azure AD gallery application</span></span>](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

-   [<span data-ttu-id="172db-122">Comment configurer l’authentification unique avec mot de passe pour une application non issue de la galerie Azure AD</span><span class="sxs-lookup"><span data-stu-id="172db-122">How to configure a password single sign-on application for a non-gallery application</span></span>](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

### <a name="how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="172db-123">Comment configurer l’authentification unique fédérée pour une application de la galerie Azure AD</span><span class="sxs-lookup"><span data-stu-id="172db-123">How to configure federated single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="172db-124">Un didacticiel pas à pas est disponible pour toutes les applications de la galerie Azure AD dans lesquelles est activée la fonctionnalité Enterprise Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="172db-124">All applications in the Azure AD gallery enabled with Enterprise Single Sign-On capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="172db-125">Pour une aide pas à pas détaillée, vous pouvez accéder à la [Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/).</span><span class="sxs-lookup"><span data-stu-id="172db-125">You can access the [List of tutorials on how to integrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

<span data-ttu-id="172db-126">Pour configurer une application à partir de la galerie Azure AD, vous devez effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="172db-126">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="172db-127">Ajouter une application à partir de la galerie Azure AD</span><span class="sxs-lookup"><span data-stu-id="172db-127">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="172db-128">Configurer les valeurs de métadonnées de l’application dans Azure AD (URL de connexion, identificateur, URL de réponse)</span><span class="sxs-lookup"><span data-stu-id="172db-128">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="172db-129">Sélectionner l’identificateur de l’utilisateur et ajouter les attributs d’utilisateur à envoyer à l’application</span><span class="sxs-lookup"><span data-stu-id="172db-129">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="172db-130">Récupérer le certificat et les métadonnées Azure AD</span><span class="sxs-lookup"><span data-stu-id="172db-130">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="172db-131">Configurer les valeurs de métadonnées Azure AD dans l’application (URL de connexion, émetteur, URL de déconnexion et certificat)</span><span class="sxs-lookup"><span data-stu-id="172db-131">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

#### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="172db-132">Ajouter une application à partir de la galerie Azure AD</span><span class="sxs-lookup"><span data-stu-id="172db-132">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="172db-133">Pour ajouter une application à partir de la galerie Azure AD, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="172db-133">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="172db-134">Ouvrez le [portail Azure](https://portal.azure.com) et connectez-vous en tant qu’**administrateur général** ou **coadministrateur**</span><span class="sxs-lookup"><span data-stu-id="172db-134">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="172db-135">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="172db-135">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="172db-136">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="172db-136">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="172db-137">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="172db-137">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="172db-138">Cliquez sur le bouton **Ajouter** dans le coin supérieur droit du panneau **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="172db-138">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="172db-139">Dans la zone de texte **Entrer un nom** de la section **Ajouter à partir de la galerie**, tapez le nom de l’application.</span><span class="sxs-lookup"><span data-stu-id="172db-139">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="172db-140">Sélectionnez l’application pour laquelle vous souhaitez configurer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="172db-140">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="172db-141">Avant d’ajouter l’application, vous pouvez la renommer dans la zone de texte **Nom**.</span><span class="sxs-lookup"><span data-stu-id="172db-141">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="172db-142">Pour ajouter l’application, cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="172db-142">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="172db-143">Après une courte période, vous pourrez voir le panneau de configuration de l’application.</span><span class="sxs-lookup"><span data-stu-id="172db-143">After a short period, you be able to see the application’s configuration blade.</span></span>

#### <a name="configure-single-sign-on-for-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="172db-144">Configurer l’authentification unique pour une application à partir de la galerie Azure AD</span><span class="sxs-lookup"><span data-stu-id="172db-144">Configure single sign-on for an application from the Azure AD gallery</span></span>

<span data-ttu-id="172db-145">Pour configurer l’authentification unique pour une application, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="172db-145">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="172db-146">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général** ou **coadministrateur**</span><span class="sxs-lookup"><span data-stu-id="172db-146">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="172db-147">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="172db-147">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="172db-148">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="172db-148">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="172db-149">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="172db-149">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="172db-150">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="172db-150">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="172db-151">Si l’application que vous recherchez ne figure pas dans la liste, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications.**</span><span class="sxs-lookup"><span data-stu-id="172db-151">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="172db-152">Sélectionnez l’application pour laquelle vous souhaitez configurer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="172db-152">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="172db-153">Une fois l’application chargée, cliquez sur **Authentification unique** dans le menu de navigation de gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="172db-153">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="172db-154">Sélectionnez **Authentification basée sur SAML** dans la liste déroulante **Mode**.</span><span class="sxs-lookup"><span data-stu-id="172db-154">Select **SAML-based Sign-on** from the **Mode** dropdown.</span></span>

9.  <span data-ttu-id="172db-155">Entrez les valeurs obligatoires dans **Domaine et URL.**</span><span class="sxs-lookup"><span data-stu-id="172db-155">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="172db-156">Ces valeurs doivent vous être communiquées par le fournisseur de l’application.</span><span class="sxs-lookup"><span data-stu-id="172db-156">You should get these values from the application vendor.</span></span>

   1. <span data-ttu-id="172db-157">Pour configurer l’application en tant qu’application à authentification unique lancée par le fournisseur de services, une URL de connexion est obligatoire.</span><span class="sxs-lookup"><span data-stu-id="172db-157">To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span> <span data-ttu-id="172db-158">Pour certaines applications, l’identificateur est également une valeur obligatoire.</span><span class="sxs-lookup"><span data-stu-id="172db-158">For some applications, the Identifier is also a required value.</span></span>

   2. <span data-ttu-id="172db-159">Pour configurer l’application en tant qu’application à authentification unique lancée par le fournisseur d’identité, une URL de réponse est obligatoire.</span><span class="sxs-lookup"><span data-stu-id="172db-159">To configure the application as IdP-initiated SSO, the Reply URL it’s a required value.</span></span> <span data-ttu-id="172db-160">Pour certaines applications, l’identificateur est également une valeur obligatoire.</span><span class="sxs-lookup"><span data-stu-id="172db-160">For some applications, the Identifier is also a required value.</span></span>

10. <span data-ttu-id="172db-161">**Facultatif** : pour afficher les valeurs non obligatoires, cliquez sur **Afficher les paramètres d’URL avancés**.</span><span class="sxs-lookup"><span data-stu-id="172db-161">**Optional:** click **Show advanced URL settings** if you want to see the non-required values.</span></span>

11. <span data-ttu-id="172db-162">Dans **Attributs d’utilisateur**, sélectionnez l’identificateur unique de vos utilisateurs dans la liste déroulante **Identificateur de l’utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="172db-162">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="172db-163">**Facultatif** : pour modifier les attributs à envoyer à l’application dans le jeton SAML lorsque l’utilisateur se connecte, cliquez sur **Afficher et modifier tous les autres attributs utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="172db-163">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="172db-164">Pour ajouter un attribut :</span><span class="sxs-lookup"><span data-stu-id="172db-164">To add an attribute:</span></span>

   1. <span data-ttu-id="172db-165">Cliquez sur **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="172db-165">click **Add attribute**.</span></span> <span data-ttu-id="172db-166">Entrez le **Nom**, puis sélectionnez la **Valeur** dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="172db-166">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="172db-167">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="172db-167">click **Save.**</span></span> <span data-ttu-id="172db-168">Le nouvel attribut s’affiche dans le tableau.</span><span class="sxs-lookup"><span data-stu-id="172db-168">You see the new attribute in the table.</span></span>

13. <span data-ttu-id="172db-169">Cliquez sur **Configurer &lt;nom de l’application&gt;** pour accéder à la documentation sur la façon de configurer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="172db-169">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="172db-170">En outre, vous disposez des URL de métadonnées et du certificat nécessaires à la configuration de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="172db-170">Also, you has the metadata URLs and certificate required to setup SSO with the application.</span></span>

14. <span data-ttu-id="172db-171">Cliquez sur **Enregistrer** pour enregistrer la configuration.</span><span class="sxs-lookup"><span data-stu-id="172db-171">click **Save** to save the configuration.</span></span>

15. <span data-ttu-id="172db-172">Affectez des utilisateurs à l’application.</span><span class="sxs-lookup"><span data-stu-id="172db-172">Assign users to the application.</span></span>

#### <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="172db-173">Sélectionner l’identificateur de l’utilisateur et ajouter les attributs d’utilisateur à envoyer à l’application</span><span class="sxs-lookup"><span data-stu-id="172db-173">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="172db-174">Pour sélectionner l’identificateur de l’utilisateur ou ajouter des attributs d’utilisateur, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="172db-174">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="172db-175">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général** ou **coadministrateur**</span><span class="sxs-lookup"><span data-stu-id="172db-175">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="172db-176">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="172db-176">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="172db-177">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="172db-177">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="172db-178">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="172db-178">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="172db-179">Cliquez sur **Toutes les applications** pour afficher la liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="172db-179">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="172db-180">Si l’application que vous recherchez ne figure pas dans la liste, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications.**</span><span class="sxs-lookup"><span data-stu-id="172db-180">If you do not see the application you want to show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="172db-181">Sélectionnez l’application pour laquelle vous avez configuré l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="172db-181">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="172db-182">Une fois l’application chargée, cliquez sur **Authentification unique** dans le menu de navigation de gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="172db-182">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="172db-183">Dans la section **Attributs d’utilisateur**, sélectionnez l’identificateur unique de vos utilisateurs dans la liste déroulante **Identificateur de l’utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="172db-183">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="172db-184">L’option sélectionnée doit correspondre à la valeur attendue dans l’application pour authentifier l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="172db-184">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

   >[!NOTE] 
   ><span data-ttu-id="172db-185">Azure AD sélectionne le format de l’attribut NameID (Identificateur d’utilisateur) en fonction de la valeur sélectionnée ou du format demandé par l’application dans la demande d’authentification SAML.</span><span class="sxs-lookup"><span data-stu-id="172db-185">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="172db-186">Pour plus d’informations, consultez l’article [Protocole SAML d’authentification unique](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) dans la section NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="172db-186">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="172db-187">Pour ajouter des attributs d’utilisateur, cliquez sur **Afficher et modifier tous les autres attributs utilisateur** afin de modifier les attributs à envoyer à l’application dans le jeton SAML lorsque l’utilisateur se connecte.</span><span class="sxs-lookup"><span data-stu-id="172db-187">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="172db-188">Pour ajouter un attribut :</span><span class="sxs-lookup"><span data-stu-id="172db-188">To add an attribute:</span></span>

   1. <span data-ttu-id="172db-189">Cliquez sur **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="172db-189">click **Add attribute**.</span></span> <span data-ttu-id="172db-190">Entrez le **Nom**, puis sélectionnez la **Valeur** dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="172db-190">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="172db-191">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="172db-191">click **Save.**</span></span> <span data-ttu-id="172db-192">Le nouvel attribut s’affiche dans le tableau.</span><span class="sxs-lookup"><span data-stu-id="172db-192">You will see the new attribute in the table.</span></span>

#### <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="172db-193">Télécharger les métadonnées ou le certificat Azure AD</span><span class="sxs-lookup"><span data-stu-id="172db-193">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="172db-194">Pour télécharger les métadonnées ou le certificat de l’application à partir d’Azure AD, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="172db-194">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="172db-195">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général** ou **coadministrateur**</span><span class="sxs-lookup"><span data-stu-id="172db-195">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="172db-196">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="172db-196">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="172db-197">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="172db-197">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="172db-198">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="172db-198">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="172db-199">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="172db-199">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="172db-200">Si l’application que vous recherchez ne figure pas dans la liste, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications.**</span><span class="sxs-lookup"><span data-stu-id="172db-200">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="172db-201">Sélectionnez l’application pour laquelle vous avez configuré l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="172db-201">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="172db-202">Une fois l’application chargée, cliquez sur **Authentification unique** dans le menu de navigation de gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="172db-202">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="172db-203">Accédez à la section **Certificat de signature SAML**, puis cliquez sur la valeur de colonne **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="172db-203">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="172db-204">En fonction de ce que l’application nécessite pour configurer l’authentification unique, vous voyez soit l’option de téléchargement des métadonnées XML, soit le certificat.</span><span class="sxs-lookup"><span data-stu-id="172db-204">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

    <span data-ttu-id="172db-205">Azure AD ne fournit pas d’URL permettant d’obtenir les métadonnées.</span><span class="sxs-lookup"><span data-stu-id="172db-205">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="172db-206">Les métadonnées peuvent uniquement être récupérées sous forme de fichier XML.</span><span class="sxs-lookup"><span data-stu-id="172db-206">The metadata can only be retrieved as a XML file.</span></span>

### <a name="how-to-configure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="172db-207">Comment configurer l’authentification unique fédérée pour une application non issue de la galerie</span><span class="sxs-lookup"><span data-stu-id="172db-207">How to configure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="172db-208">Pour configurer une application non issue de la galerie, vous devez disposer d’Azure AD Premium, et l’application doit prendre en charge SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="172db-208">To configure a non-gallery application, you need to have Azure AD premium and the application supports SAML 2.0.</span></span> <span data-ttu-id="172db-209">Pour plus d’informations sur les versions d’Azure AD, consultez [Tarification d’Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="172db-209">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

-   [<span data-ttu-id="172db-210">Configurer les valeurs de métadonnées de l’application dans Azure AD (URL de connexion, identificateur, URL de réponse)</span><span class="sxs-lookup"><span data-stu-id="172db-210">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configuring-single-sign-on)

-   [<span data-ttu-id="172db-211">Sélectionner l’identificateur de l’utilisateur et ajouter les attributs d’utilisateur à envoyer à l’application</span><span class="sxs-lookup"><span data-stu-id="172db-211">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="172db-212">Récupérer le certificat et les métadonnées Azure AD</span><span class="sxs-lookup"><span data-stu-id="172db-212">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="172db-213">Configurer les valeurs de métadonnées Azure AD dans l’application (URL de connexion, émetteur, URL de déconnexion et certificat)</span><span class="sxs-lookup"><span data-stu-id="172db-213">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configuring-single-sign-on)

#### <a name="configure-the-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a><span data-ttu-id="172db-214">Configurer les valeurs de métadonnées de l’application dans Azure AD (URL de connexion, identificateur, URL de réponse)</span><span class="sxs-lookup"><span data-stu-id="172db-214">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>

<span data-ttu-id="172db-215">Pour configurer l’authentification unique pour une application qui n’est pas issue de la galerie Azure AD, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="172db-215">To configure single sign-on for an application that is not in the Azure AD gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="172db-216">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général** ou **coadministrateur**</span><span class="sxs-lookup"><span data-stu-id="172db-216">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="172db-217">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="172db-217">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="172db-218">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="172db-218">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="172db-219">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="172db-219">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="172db-220">Cliquez sur le bouton **Ajouter** dans le coin supérieur droit du panneau **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="172db-220">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="172db-221">Cliquez sur **Application ne figurant pas dans la galerie** dans la section **Ajouter votre propre application**.</span><span class="sxs-lookup"><span data-stu-id="172db-221">click **Non-gallery application** in the **Add your own app** section.</span></span>

7.  <span data-ttu-id="172db-222">Entrez le nom de votre application dans la zone de texte **Nom**.</span><span class="sxs-lookup"><span data-stu-id="172db-222">Enter the name of the application in the **Name** textbox.</span></span>

8.  <span data-ttu-id="172db-223">Pour ajouter l’application, cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="172db-223">Click **Add** button, to add the application.</span></span>

9.  <span data-ttu-id="172db-224">Une fois l’application chargée, cliquez sur **Authentification unique** dans le menu de navigation de gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="172db-224">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="172db-225">Sélectionnez **Authentification basée sur SAML** dans la liste déroulante **Mode**.</span><span class="sxs-lookup"><span data-stu-id="172db-225">Select **SAML-based Sign-on** in the **Mode** dropdown.</span></span>

11. <span data-ttu-id="172db-226">Entrez les valeurs obligatoires dans **Domaine et URL.**</span><span class="sxs-lookup"><span data-stu-id="172db-226">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="172db-227">Ces valeurs doivent vous être communiquées par le fournisseur de l’application.</span><span class="sxs-lookup"><span data-stu-id="172db-227">You should get these values from the application vendor.</span></span>

   1. <span data-ttu-id="172db-228">Pour configurer l’application en tant qu’application à authentification unique lancée par le fournisseur d’identité, entrez l’URL de réponse et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="172db-228">To configure the application as IdP-initiated SSO, enter the Reply URL and the Identifier.</span></span>

   2.  <span data-ttu-id="172db-229">**Facultatif** : pour configurer l’application comme une application à authentification unique initiée par le fournisseur de services, une URL de connexion est obligatoire.</span><span class="sxs-lookup"><span data-stu-id="172db-229">**Optional:** To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="172db-230">Dans **Attributs d’utilisateur**, sélectionnez l’identificateur unique de vos utilisateurs dans la liste déroulante **Identificateur de l’utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="172db-230">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="172db-231">**Facultatif** : pour modifier les attributs à envoyer à l’application dans le jeton SAML lorsque l’utilisateur se connecte, cliquez sur **Afficher et modifier tous les autres attributs utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="172db-231">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="172db-232">Pour ajouter un attribut :</span><span class="sxs-lookup"><span data-stu-id="172db-232">To add an attribute:</span></span>

   1. <span data-ttu-id="172db-233">Cliquez sur **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="172db-233">click **Add attribute**.</span></span> <span data-ttu-id="172db-234">Entrez le **Nom**, puis sélectionnez la **Valeur** dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="172db-234">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="172db-235">Cliquez sur **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="172db-235">Click **Save.**</span></span> <span data-ttu-id="172db-236">Le nouvel attribut s’affiche dans le tableau.</span><span class="sxs-lookup"><span data-stu-id="172db-236">You see the new attribute in the table.</span></span>

14. <span data-ttu-id="172db-237">Cliquez sur **Configurer &lt;nom de l’application&gt;** pour accéder à la documentation expliquant comment configurer l’authentification unique pour l’application.</span><span class="sxs-lookup"><span data-stu-id="172db-237">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="172db-238">En outre, vous disposez des URL et du certificat Azure AD nécessaires pour l’application.</span><span class="sxs-lookup"><span data-stu-id="172db-238">Also, you has Azure AD URLs and certificate required for the application.</span></span>

#### <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="172db-239">Sélectionner l’identificateur de l’utilisateur et ajouter les attributs d’utilisateur à envoyer à l’application</span><span class="sxs-lookup"><span data-stu-id="172db-239">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="172db-240">Pour sélectionner l’identificateur de l’utilisateur ou ajouter des attributs d’utilisateur, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="172db-240">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="172db-241">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général** ou **coadministrateur**</span><span class="sxs-lookup"><span data-stu-id="172db-241">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="172db-242">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="172db-242">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="172db-243">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="172db-243">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="172db-244">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="172db-244">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="172db-245">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="172db-245">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="172db-246">Si l’application que vous recherchez ne figure pas dans la liste, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications.**</span><span class="sxs-lookup"><span data-stu-id="172db-246">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="172db-247">Sélectionnez l’application pour laquelle vous avez configuré l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="172db-247">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="172db-248">Une fois l’application chargée, cliquez sur **Authentification unique** dans le menu de navigation de gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="172db-248">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="172db-249">Dans la section **Attributs d’utilisateur**, sélectionnez l’identificateur unique de vos utilisateurs dans la liste déroulante **Identificateur de l’utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="172db-249">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="172db-250">L’option sélectionnée doit correspondre à la valeur attendue dans l’application pour authentifier l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="172db-250">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

   >[!NOTE] 
   ><span data-ttu-id="172db-251">Azure AD sélectionne le format de l’attribut NameID (Identificateur d’utilisateur) en fonction de la valeur sélectionnée ou du format demandé par l’application dans la demande d’authentification SAML.</span><span class="sxs-lookup"><span data-stu-id="172db-251">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="172db-252">Pour plus d’informations, consultez l’article [Protocole SAML d’authentification unique](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) dans la section NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="172db-252">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="172db-253">Pour ajouter des attributs d’utilisateur, cliquez sur **Afficher et modifier tous les autres attributs utilisateur** afin de modifier les attributs à envoyer à l’application dans le jeton SAML lorsque l’utilisateur se connecte.</span><span class="sxs-lookup"><span data-stu-id="172db-253">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="172db-254">Pour ajouter un attribut :</span><span class="sxs-lookup"><span data-stu-id="172db-254">To add an attribute:</span></span>

   1. <span data-ttu-id="172db-255">Cliquez sur **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="172db-255">click **Add attribute**.</span></span> <span data-ttu-id="172db-256">Entrez le **Nom**, puis sélectionnez la **Valeur** dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="172db-256">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="172db-257">Cliquez sur **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="172db-257">Click **Save.**</span></span> <span data-ttu-id="172db-258">Le nouvel attribut s’affiche dans le tableau.</span><span class="sxs-lookup"><span data-stu-id="172db-258">You see the new attribute in the table.</span></span>

#### <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="172db-259">Télécharger les métadonnées ou le certificat Azure AD</span><span class="sxs-lookup"><span data-stu-id="172db-259">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="172db-260">Pour télécharger les métadonnées ou le certificat de l’application à partir d’Azure AD, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="172db-260">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="172db-261">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général** ou **coadministrateur**</span><span class="sxs-lookup"><span data-stu-id="172db-261">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="172db-262">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="172db-262">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="172db-263">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="172db-263">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="172db-264">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="172db-264">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="172db-265">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="172db-265">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="172db-266">Si l’application que vous recherchez ne figure pas dans la liste, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications.**</span><span class="sxs-lookup"><span data-stu-id="172db-266">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="172db-267">Sélectionnez l’application pour laquelle vous avez configuré l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="172db-267">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="172db-268">Une fois l’application chargée, cliquez sur **Authentification unique** dans le menu de navigation de gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="172db-268">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="172db-269">Accédez à la section **Certificat de signature SAML**, puis cliquez sur la valeur de colonne **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="172db-269">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="172db-270">En fonction de ce que l’application nécessite pour configurer l’authentification unique, vous voyez soit l’option de téléchargement des métadonnées XML, soit le certificat.</span><span class="sxs-lookup"><span data-stu-id="172db-270">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="172db-271">Azure AD ne fournit pas d’URL permettant d’obtenir les métadonnées.</span><span class="sxs-lookup"><span data-stu-id="172db-271">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="172db-272">Les métadonnées peuvent uniquement être récupérées sous forme de fichier XML.</span><span class="sxs-lookup"><span data-stu-id="172db-272">The metadata can only be retrieved as a XML file.</span></span>

### <a name="how-to-configure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="172db-273">Comment configurer l’authentification unique par mot de passe pour une application de la galerie Azure AD</span><span class="sxs-lookup"><span data-stu-id="172db-273">How to configure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="172db-274">Pour configurer une application à partir de la galerie Azure AD, vous devez effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="172db-274">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="172db-275">Ajouter une application à partir de la galerie Azure AD</span><span class="sxs-lookup"><span data-stu-id="172db-275">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="172db-276">Configurer l’application pour l’authentification unique par mot de passe</span><span class="sxs-lookup"><span data-stu-id="172db-276">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

#### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="172db-277">Ajouter une application à partir de la galerie Azure AD</span><span class="sxs-lookup"><span data-stu-id="172db-277">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="172db-278">Pour ajouter une application à partir de la galerie Azure AD, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="172db-278">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="172db-279">Ouvrez le [portail Azure](https://portal.azure.com) et connectez-vous en tant qu’**administrateur général** ou **coadministrateur**</span><span class="sxs-lookup"><span data-stu-id="172db-279">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="172db-280">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="172db-280">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="172db-281">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="172db-281">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="172db-282">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="172db-282">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="172db-283">Cliquez sur le bouton **Ajouter** dans le coin supérieur droit du panneau **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="172db-283">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="172db-284">Dans la zone de texte **Entrer un nom** de la section **Ajouter à partir de la galerie**, tapez le nom de l’application.</span><span class="sxs-lookup"><span data-stu-id="172db-284">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="172db-285">Sélectionnez l’application pour laquelle vous souhaitez configurer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="172db-285">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="172db-286">Avant d’ajouter l’application, vous pouvez la renommer dans la zone de texte **Nom**.</span><span class="sxs-lookup"><span data-stu-id="172db-286">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="172db-287">Pour ajouter l’application, cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="172db-287">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="172db-288">Après une courte période, vous pouvez voir le panneau de configuration de l’application.</span><span class="sxs-lookup"><span data-stu-id="172db-288">After a short period, you be able to see the application’s configuration blade.</span></span>

#### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="172db-289">Configurer l’application pour l’authentification unique par mot de passe</span><span class="sxs-lookup"><span data-stu-id="172db-289">Configure the application for password single sign-on</span></span>

<span data-ttu-id="172db-290">Pour configurer l’authentification unique pour une application, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="172db-290">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="172db-291">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général** ou **coadministrateur**</span><span class="sxs-lookup"><span data-stu-id="172db-291">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="172db-292">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="172db-292">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="172db-293">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="172db-293">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="172db-294">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="172db-294">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="172db-295">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="172db-295">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="172db-296">Si l’application que vous recherchez ne figure pas dans la liste, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications.**</span><span class="sxs-lookup"><span data-stu-id="172db-296">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="172db-297">Sélectionnez l’application pour laquelle vous souhaitez configurer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="172db-297">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="172db-298">Une fois l’application chargée, cliquez sur **Authentification unique** dans le menu de navigation de gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="172db-298">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="172db-299">Sélectionnez le mode **Authentification par mot de passe.**</span><span class="sxs-lookup"><span data-stu-id="172db-299">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="172db-300">[Affectez des utilisateurs à l’application](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="172db-300">[Assign users to the application](#how-to-assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="172db-301">En outre, vous pouvez également fournir des informations d’identification pour le compte de l’utilisateur en sélectionnant les lignes des utilisateurs, en cliquant sur **Mettre à jour les informations d’identification** et en entrant le nom d’utilisateur et le mot de passe à la place des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="172db-301">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="172db-302">Autrement, les utilisateurs devront entrer les informations d’identification eux-mêmes lors du lancement.</span><span class="sxs-lookup"><span data-stu-id="172db-302">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

### <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="172db-303">Comment configurer l’authentification unique par mot de passe pour une application ne figurant pas dans la galerie</span><span class="sxs-lookup"><span data-stu-id="172db-303">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="172db-304">Pour configurer une application à partir de la galerie Azure AD, vous devez effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="172db-304">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="172db-305">Ajouter une application ne figurant pas dans la galerie</span><span class="sxs-lookup"><span data-stu-id="172db-305">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="172db-306">Configurer l’application pour l’authentification unique par mot de passe</span><span class="sxs-lookup"><span data-stu-id="172db-306">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

#### <a name="add-a-non-gallery-application"></a><span data-ttu-id="172db-307">Ajouter une application ne figurant pas dans la galerie</span><span class="sxs-lookup"><span data-stu-id="172db-307">Add a non-gallery application</span></span>

<span data-ttu-id="172db-308">Pour ajouter une application à partir de la galerie Azure AD, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="172db-308">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="172db-309">Ouvrez le [portail Azure](https://portal.azure.com) et connectez-vous en tant qu’**administrateur général** ou **coadministrateur**.</span><span class="sxs-lookup"><span data-stu-id="172db-309">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="172db-310">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="172db-310">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="172db-311">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="172db-311">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="172db-312">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="172db-312">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="172db-313">Cliquez sur le bouton **Ajouter** dans le coin supérieur droit du panneau **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="172db-313">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="172db-314">Cliquez sur **Application ne figurant pas dans la galerie.**</span><span class="sxs-lookup"><span data-stu-id="172db-314">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="172db-315">Entrez le nom de votre application dans la zone de texte **Nom**.</span><span class="sxs-lookup"><span data-stu-id="172db-315">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="172db-316">Sélectionnez **Ajouter.**</span><span class="sxs-lookup"><span data-stu-id="172db-316">Select **Add.**</span></span>

<span data-ttu-id="172db-317">Après une courte période, vous pourrez voir le panneau de configuration de l’application.</span><span class="sxs-lookup"><span data-stu-id="172db-317">After a short period, you be able to see the application’s configuration blade.</span></span>

#### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="172db-318">Configurer l’application pour l’authentification unique par mot de passe</span><span class="sxs-lookup"><span data-stu-id="172db-318">Configure the application for password single sign-on</span></span>

<span data-ttu-id="172db-319">Pour configurer l’authentification unique pour une application, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="172db-319">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="172db-320">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général** ou **coadministrateur**</span><span class="sxs-lookup"><span data-stu-id="172db-320">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="172db-321">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="172db-321">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="172db-322">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="172db-322">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="172db-323">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="172db-323">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="172db-324">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="172db-324">click **All Applications** to view a list of all your applications.</span></span>

    1.  <span data-ttu-id="172db-325">Si l’application que vous recherchez ne figure pas dans la liste, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications.**</span><span class="sxs-lookup"><span data-stu-id="172db-325">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="172db-326">Sélectionnez l’application pour laquelle vous souhaitez configurer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="172db-326">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="172db-327">Une fois l’application chargée, cliquez sur **Authentification unique** dans le menu de navigation de gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="172db-327">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="172db-328">Sélectionnez le mode **Authentification par mot de passe.**</span><span class="sxs-lookup"><span data-stu-id="172db-328">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="172db-329">Entrez **l’URL de connexion**.</span><span class="sxs-lookup"><span data-stu-id="172db-329">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="172db-330">Il s’agit de l’URL où les utilisateurs entrent leurs nom d’utilisateur et mot de passe pour se connecter.</span><span class="sxs-lookup"><span data-stu-id="172db-330">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="172db-331">Vérifiez que les champs de connexion sont visibles dans l’URL.</span><span class="sxs-lookup"><span data-stu-id="172db-331">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="172db-332">[Affectez des utilisateurs à l’application](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="172db-332">[Assign users to the application](#how-to-assign-a-user-to-an-application-directly).</span></span>

11. <span data-ttu-id="172db-333">En outre, vous pouvez également fournir des informations d’identification pour le compte de l’utilisateur en sélectionnant les lignes des utilisateurs, en cliquant sur **Mettre à jour les informations d’identification** et en entrant le nom d’utilisateur et le mot de passe à la place des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="172db-333">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="172db-334">Autrement, les utilisateurs devront entrer les informations d’identification eux-mêmes lors du lancement.</span><span class="sxs-lookup"><span data-stu-id="172db-334">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="problems-related-to-assigning-applications-to-users"></a><span data-ttu-id="172db-335">Problèmes liés à l’affectation des applications aux utilisateurs</span><span class="sxs-lookup"><span data-stu-id="172db-335">Problems related to assigning applications to users</span></span>

<span data-ttu-id="172db-336">Un utilisateur peut ne pas voir une application sur son volet d’accès, car il n’y est pas affecté.</span><span class="sxs-lookup"><span data-stu-id="172db-336">A user may not be seeing an application on their Access Panel because they are not assigned to the application.</span></span> <span data-ttu-id="172db-337">Voici plusieurs méthodes pour vérifier :</span><span class="sxs-lookup"><span data-stu-id="172db-337">Below are some ways to check:</span></span>

-   [<span data-ttu-id="172db-338">Vérifier si un utilisateur est affecté à l’application</span><span class="sxs-lookup"><span data-stu-id="172db-338">Check if a user is assigned to the application</span></span>](#check-if-a-user-is-assigned-to-the-application)

-   [<span data-ttu-id="172db-339">Comment affecter un utilisateur directement à une application</span><span class="sxs-lookup"><span data-stu-id="172db-339">How to assign a user to an application directly</span></span>](#how-to-assign-a-user-to-an-application-directly)

-   [<span data-ttu-id="172db-340">Vérifier si un utilisateur est affecté à une licence liée à l’application</span><span class="sxs-lookup"><span data-stu-id="172db-340">Check if a user is assigned to a license related to the application</span></span>](#check-if-a-user-is-under-a-license-related-to-the-application)

-   [<span data-ttu-id="172db-341">Comment attribuer une licence à un utilisateur</span><span class="sxs-lookup"><span data-stu-id="172db-341">How to assign a license to a user</span></span>](#how-to-assign-a-user-a-license)

### <a name="check-if-a-user-is-assigned-to-the-application"></a><span data-ttu-id="172db-342">Vérifier si un utilisateur est affecté à l’application</span><span class="sxs-lookup"><span data-stu-id="172db-342">Check if a user is assigned to the application</span></span>

<span data-ttu-id="172db-343">Pour vérifier si un utilisateur est affecté à l’application, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="172db-343">To check if a user is assigned to the application, follow the steps below:</span></span>

1.  <span data-ttu-id="172db-344">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général.**</span><span class="sxs-lookup"><span data-stu-id="172db-344">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="172db-345">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="172db-345">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="172db-346">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="172db-346">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="172db-347">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="172db-347">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="172db-348">Cliquez sur **Toutes les applications** pour afficher la liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="172db-348">click **All Applications** to view a list of all your applications.</span></span>

6.  <span data-ttu-id="172db-349">**Recherchez** le nom de l’application en question.</span><span class="sxs-lookup"><span data-stu-id="172db-349">**Search** for the name of the application in question.</span></span>

7.  <span data-ttu-id="172db-350">Sélectionnez **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="172db-350">click **Users and groups**.</span></span>

8.  <span data-ttu-id="172db-351">Vérifiez si votre utilisateur est affecté à l’application.</span><span class="sxs-lookup"><span data-stu-id="172db-351">Check to see if your user is assigned to the application.</span></span>

   * <span data-ttu-id="172db-352">Si ce n’est pas le cas, suivez les étapes décrites dans « Comment affecter un utilisateur directement à une application ».</span><span class="sxs-lookup"><span data-stu-id="172db-352">If not follow the steps in “How to assign a user to an application directly” to do so.</span></span>

### <a name="how-to-assign-a-user-to-an-application-directly"></a><span data-ttu-id="172db-353">Comment affecter un utilisateur directement à une application</span><span class="sxs-lookup"><span data-stu-id="172db-353">How to assign a user to an application directly</span></span>

<span data-ttu-id="172db-354">Pour affecter un ou plusieurs utilisateurs directement à une application, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="172db-354">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="172db-355">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général**.</span><span class="sxs-lookup"><span data-stu-id="172db-355">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator**.</span></span>

2.  <span data-ttu-id="172db-356">Ouvrez l’**extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="172db-356">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="172db-357">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="172db-357">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="172db-358">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="172db-358">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="172db-359">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="172db-359">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="172db-360">Si l’application que vous recherchez ne figure pas dans la liste, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications.**</span><span class="sxs-lookup"><span data-stu-id="172db-360">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="172db-361">Dans la liste qui s’affiche, sélectionnez l’application à laquelle vous souhaitez affecter un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="172db-361">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="172db-362">Une fois l’application chargée, cliquez sur **Utilisateurs et groupes** dans le menu de navigation de gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="172db-362">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="172db-363">Cliquez sur le bouton **Ajouter** en haut de la liste **Utilisateurs et groupes** pour ouvrir le panneau **Ajouter une attribution**.</span><span class="sxs-lookup"><span data-stu-id="172db-363">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="172db-364">Cliquez sur le sélecteur **Utilisateurs et groupes** à partir du panneau **Ajouter une attribution**.</span><span class="sxs-lookup"><span data-stu-id="172db-364">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="172db-365">Tapez **le nom complet** ou **l’adresse de messagerie** de l’utilisateur souhaité pour l’attribution dans la zone de recherche **Rechercher par nom ou adresse de messagerie**.</span><span class="sxs-lookup"><span data-stu-id="172db-365">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="172db-366">Pointez sur **l’utilisateur** dans la liste pour afficher une **case à cocher**.</span><span class="sxs-lookup"><span data-stu-id="172db-366">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="172db-367">Cliquez sur la case à cocher en regard de la photo de profil ou du logo de l’utilisateur pour ajouter ce dernier à la liste **Sélectionné**.</span><span class="sxs-lookup"><span data-stu-id="172db-367">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="172db-368">**Facultatif :** si vous souhaitez **ajouter plusieurs utilisateurs**, entrez un autre **nom complet** ou une autre **adresse de messagerie** dans la zone de recherche **Rechercher par nom ou adresse de messagerie**, puis cliquez sur la case à cocher pour ajouter cet utilisateur à la liste **Sélectionné**.</span><span class="sxs-lookup"><span data-stu-id="172db-368">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="172db-369">Après avoir sélectionné les utilisateurs, cliquez sur le bouton **Sélectionner** pour les ajouter à la liste des utilisateurs et des groupes à affecter à l’application.</span><span class="sxs-lookup"><span data-stu-id="172db-369">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="172db-370">**Facultatif :** cliquez sur le sélecteur **Sélectionner un rôle** dans le panneau **Ajouter une attribution** pour sélectionner un rôle à affecter aux utilisateurs que vous avez sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="172db-370">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="172db-371">Cliquez sur le bouton **Attribuer** pour affecter l’application aux utilisateurs sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="172db-371">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="172db-372">Après une courte période, les utilisateurs que vous avez sélectionnés seront en mesure de lancer ces applications dans le volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="172db-372">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

### <a name="check-if-a-user-is-under-a-license-related-to-the-application"></a><span data-ttu-id="172db-373">Vérifier si un utilisateur est affecté à une licence liée à l’application</span><span class="sxs-lookup"><span data-stu-id="172db-373">Check if a user is under a license related to the application</span></span>

<span data-ttu-id="172db-374">Pour vérifier les licences affectées à un utilisateur, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="172db-374">To check a user’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="172db-375">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général.**</span><span class="sxs-lookup"><span data-stu-id="172db-375">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="172db-376">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="172db-376">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="172db-377">Tapez « **Azure Active Directory** » dans la zone de recherche du filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="172db-377">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="172db-378">Cliquez sur **Utilisateurs et groupes** dans le menu de navigation.</span><span class="sxs-lookup"><span data-stu-id="172db-378">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="172db-379">Cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="172db-379">click **All users**.</span></span>

6.  <span data-ttu-id="172db-380">**Recherchez** l’utilisateur qui vous intéresse et **cliquez sur la ligne** pour le sélectionner.</span><span class="sxs-lookup"><span data-stu-id="172db-380">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="172db-381">Cliquez sur **Licences** pour voir quelles licences sont actuellement affectées à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="172db-381">click **Licenses** to see which licenses the user currently has assigned.</span></span>

  * <span data-ttu-id="172db-382">Si l’utilisateur est affecté à une licence Office, les applications Office internes apparaîtront dans le volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="172db-382">If the user is assigned to an Office license this enable First Party Office applications to appear on the user’s Access Panel.</span></span>

### <a name="how-to-assign-a-user-a-license"></a><span data-ttu-id="172db-383">Comment affecter une licence à un utilisateur</span><span class="sxs-lookup"><span data-stu-id="172db-383">How to assign a user a license</span></span> 

<span data-ttu-id="172db-384">Pour affecter une licence à un utilisateur, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="172db-384">To assign a license to a user, follow the steps below:</span></span>

1.  <span data-ttu-id="172db-385">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général.**</span><span class="sxs-lookup"><span data-stu-id="172db-385">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="172db-386">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="172db-386">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="172db-387">Tapez « **Azure Active Directory** » dans la zone de recherche du filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="172db-387">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="172db-388">Cliquez sur **Utilisateurs et groupes** dans le menu de navigation.</span><span class="sxs-lookup"><span data-stu-id="172db-388">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="172db-389">Cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="172db-389">click **All users**.</span></span>

6.  <span data-ttu-id="172db-390">**Recherchez** l’utilisateur qui vous intéresse et **cliquez sur la ligne** pour le sélectionner.</span><span class="sxs-lookup"><span data-stu-id="172db-390">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="172db-391">Cliquez sur **Licences** pour voir quelles licences sont actuellement affectées à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="172db-391">click **Licenses** to see which licenses the user currently has assigned.</span></span>

8.  <span data-ttu-id="172db-392">Cliquez sur le bouton **Attribuer**.</span><span class="sxs-lookup"><span data-stu-id="172db-392">click the **Assign** button.</span></span>

9.  <span data-ttu-id="172db-393">Sélectionnez **un ou plusieurs produits** dans la liste des produits disponibles.</span><span class="sxs-lookup"><span data-stu-id="172db-393">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="172db-394">**Facultatif** Cliquez sur l’élément **Options d’affectation** pour affecter les produits de façon granulaire.</span><span class="sxs-lookup"><span data-stu-id="172db-394">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="172db-395">Cliquez sur **OK** lorsque l’opération est terminée.</span><span class="sxs-lookup"><span data-stu-id="172db-395">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="172db-396">Cliquez sur le bouton **Attribuer** pour affecter ces licences à cet utilisateur.</span><span class="sxs-lookup"><span data-stu-id="172db-396">Click the **Assign** button to assign these licenses to this user.</span></span>

## <a name="problems-related-to-assigning-applications-to-groups"></a><span data-ttu-id="172db-397">Problèmes liés à l’affectation des applications aux groupes</span><span class="sxs-lookup"><span data-stu-id="172db-397">Problems related to assigning applications to groups</span></span>

<span data-ttu-id="172db-398">Un utilisateur peut ne pas voir une application sur son volet d’accès, car il ne fait pas partie d’un groupe affecté à l’application.</span><span class="sxs-lookup"><span data-stu-id="172db-398">A user may be seeing an application on their Access Panel because they are part of a group that has been assigned the application.</span></span> <span data-ttu-id="172db-399">Voici plusieurs méthodes pour vérifier :</span><span class="sxs-lookup"><span data-stu-id="172db-399">Below are some ways to check:</span></span>

-   [<span data-ttu-id="172db-400">Vérifier les appartenances d’un utilisateur à des groupes</span><span class="sxs-lookup"><span data-stu-id="172db-400">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="172db-401">Comment affecter une application directement à un groupe</span><span class="sxs-lookup"><span data-stu-id="172db-401">How to assign an application to a group directly</span></span>](#how-to-assign-an-application-to-a-group-directly)

-   [<span data-ttu-id="172db-402">Vérifier si un utilisateur fait partie d’un groupe affecté à une licence</span><span class="sxs-lookup"><span data-stu-id="172db-402">Check if a user is part of group assigned to a license</span></span>](#check-if-a-user-is-part-of-group-assigned-to-a-license)

-   [<span data-ttu-id="172db-403">Comment attribuer une licence à un groupe</span><span class="sxs-lookup"><span data-stu-id="172db-403">How to assign a license to a group</span></span>](#how-to-assign-a-license-to-a-group)

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="172db-404">Vérifier les appartenances d’un utilisateur à des groupes</span><span class="sxs-lookup"><span data-stu-id="172db-404">Check a user’s group memberships</span></span>

<span data-ttu-id="172db-405">Pour vérifier l’appartenance d’un utilisateur à un groupe, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="172db-405">To check a group’s membership, follow the steps below:</span></span>

1.  <span data-ttu-id="172db-406">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général.**</span><span class="sxs-lookup"><span data-stu-id="172db-406">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="172db-407">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="172db-407">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="172db-408">Tapez « **Azure Active Directory** » dans la zone de recherche du filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="172db-408">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="172db-409">Cliquez sur **Utilisateurs et groupes** dans le menu de navigation.</span><span class="sxs-lookup"><span data-stu-id="172db-409">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="172db-410">Cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="172db-410">click **All users**.</span></span>

6.  <span data-ttu-id="172db-411">**Recherchez** l’utilisateur qui vous intéresse et **cliquez sur la ligne** pour le sélectionner.</span><span class="sxs-lookup"><span data-stu-id="172db-411">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="172db-412">Cliquez sur **Groupes**.</span><span class="sxs-lookup"><span data-stu-id="172db-412">click **Groups**.</span></span>

8.  <span data-ttu-id="172db-413">Vérifiez si votre utilisateur fait partie d’un groupe affecté à l’application.</span><span class="sxs-lookup"><span data-stu-id="172db-413">Check to see if your user is part of a Group assigned to the application.</span></span>

  * <span data-ttu-id="172db-414">Si vous souhaitez supprimer l’utilisateur du groupe, **cliquez sur la ligne** du groupe et sélectionnez Supprimer.</span><span class="sxs-lookup"><span data-stu-id="172db-414">If you want to remove the user from the group, **click the row** of the group and select delete.</span></span>

### <a name="how-to-assign-an-application-to-a-group-directly"></a><span data-ttu-id="172db-415">Comment affecter une application directement à un groupe</span><span class="sxs-lookup"><span data-stu-id="172db-415">How to assign an application to a group directly</span></span>

<span data-ttu-id="172db-416">Pour affecter un ou plusieurs groupes directement à une application, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="172db-416">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="172db-417">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général**.</span><span class="sxs-lookup"><span data-stu-id="172db-417">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator**.</span></span>

2.  <span data-ttu-id="172db-418">Ouvrez l’**extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="172db-418">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="172db-419">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="172db-419">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="172db-420">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="172db-420">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="172db-421">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="172db-421">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="172db-422">Si l’application que vous recherchez ne figure pas dans la liste, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications.**</span><span class="sxs-lookup"><span data-stu-id="172db-422">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="172db-423">Dans la liste qui s’affiche, sélectionnez l’application à laquelle vous souhaitez affecter un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="172db-423">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="172db-424">Une fois l’application chargée, cliquez sur **Utilisateurs et groupes** dans le menu de navigation de gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="172db-424">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="172db-425">Cliquez sur le bouton **Ajouter** en haut de la liste **Utilisateurs et groupes** pour ouvrir le panneau **Ajouter une attribution**.</span><span class="sxs-lookup"><span data-stu-id="172db-425">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="172db-426">Cliquez sur le sélecteur **Utilisateurs et groupes** à partir du panneau **Ajouter une attribution**.</span><span class="sxs-lookup"><span data-stu-id="172db-426">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="172db-427">Tapez le **nom de groupe complet** du groupe souhaité pour l’attribution dans la zone de recherche **Rechercher par nom ou adresse de messagerie**.</span><span class="sxs-lookup"><span data-stu-id="172db-427">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="172db-428">Pointez sur le **groupe** dans la liste pour afficher une **case à cocher**.</span><span class="sxs-lookup"><span data-stu-id="172db-428">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="172db-429">Cliquez sur la case à cocher en regard de la photo de profil ou du logo du groupe pour ajouter ce dernier à la liste **Sélectionné**.</span><span class="sxs-lookup"><span data-stu-id="172db-429">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="172db-430">**Facultatif :** si vous souhaitez **ajouter plusieurs groupes**, entrez un autre **nom de groupe complet** dans la zone de recherche **Rechercher par nom ou adresse de messagerie**, puis cliquez sur la case à cocher pour ajouter ce groupe à la liste **Sélectionné**.</span><span class="sxs-lookup"><span data-stu-id="172db-430">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="172db-431">Lorsque vous avez fini de sélectionner les groupes, cliquez sur le bouton **Sélectionner** pour les ajouter à la liste des utilisateurs et des groupes à affecter à l’application.</span><span class="sxs-lookup"><span data-stu-id="172db-431">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="172db-432">**Facultatif :** cliquez sur le sélecteur **Sélectionner un rôle** dans le panneau **Ajouter une attribution** pour sélectionner un rôle à affecter aux groupes que vous avez sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="172db-432">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="172db-433">Cliquez sur le bouton **Attribuer** pour affecter l’application aux groupes sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="172db-433">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="172db-434">Après une courte période, les utilisateurs que vous avez sélectionnés seront en mesure de lancer ces applications dans le volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="172db-434">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

### <a name="check-if-a-user-is-part-of-group-assigned-to-a-license"></a><span data-ttu-id="172db-435">Vérifier si un utilisateur fait partie d’un groupe affecté à une licence</span><span class="sxs-lookup"><span data-stu-id="172db-435">Check if a user is part of group assigned to a license</span></span>

1.  <span data-ttu-id="172db-436">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général.**</span><span class="sxs-lookup"><span data-stu-id="172db-436">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="172db-437">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="172db-437">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="172db-438">Tapez « **Azure Active Directory** » dans la zone de recherche du filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="172db-438">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="172db-439">Cliquez sur **Utilisateurs et groupes** dans le menu de navigation.</span><span class="sxs-lookup"><span data-stu-id="172db-439">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="172db-440">Cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="172db-440">click **All users**.</span></span>

6.  <span data-ttu-id="172db-441">**Recherchez** l’utilisateur qui vous intéresse et **cliquez sur la ligne** pour le sélectionner.</span><span class="sxs-lookup"><span data-stu-id="172db-441">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="172db-442">Cliquez sur **Groupes**.</span><span class="sxs-lookup"><span data-stu-id="172db-442">click **Groups**.</span></span>

8.  <span data-ttu-id="172db-443">Cliquez sur la ligne d’un groupe spécifique.</span><span class="sxs-lookup"><span data-stu-id="172db-443">click the row of a specific group.</span></span>

9.  <span data-ttu-id="172db-444">Cliquez sur **Licences** pour voir quelles licences sont affectées au groupe.</span><span class="sxs-lookup"><span data-stu-id="172db-444">click **Licenses** to see which licenses the group has assigned to it.</span></span>

   * <span data-ttu-id="172db-445">Si le groupe est affecté à une licence Office, certaines applications Office internes pourront apparaître dans le volet d’accès de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="172db-445">If the group is assigned to an Office license this may enable certain First Party Office applications to appear on the user’s Access Panel.</span></span>

### <a name="how-to-assign-a-license-to-a-group"></a><span data-ttu-id="172db-446">Comment attribuer une licence à un groupe</span><span class="sxs-lookup"><span data-stu-id="172db-446">How to assign a license to a group</span></span>

<span data-ttu-id="172db-447">Pour affecter une licence à un groupe, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="172db-447">To assign a license to a group, follow the steps below:</span></span>

1.  <span data-ttu-id="172db-448">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général.**</span><span class="sxs-lookup"><span data-stu-id="172db-448">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="172db-449">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="172db-449">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="172db-450">Tapez « **Azure Active Directory** » dans la zone de recherche du filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="172db-450">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="172db-451">Cliquez sur **Utilisateurs et groupes** dans le menu de navigation.</span><span class="sxs-lookup"><span data-stu-id="172db-451">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="172db-452">Cliquez sur **Tous les groupes**.</span><span class="sxs-lookup"><span data-stu-id="172db-452">click **All groups**.</span></span>

6.  <span data-ttu-id="172db-453">**Recherchez** le groupe qui vous intéresse et **cliquez sur la ligne** pour le sélectionner.</span><span class="sxs-lookup"><span data-stu-id="172db-453">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="172db-454">Cliquez sur **Licences** pour voir quelles licences sont actuellement affectées au groupe.</span><span class="sxs-lookup"><span data-stu-id="172db-454">click **Licenses** to see which licenses the group currently has assigned.</span></span>

8.  <span data-ttu-id="172db-455">Cliquez sur le bouton **Attribuer**.</span><span class="sxs-lookup"><span data-stu-id="172db-455">click the **Assign** button.</span></span>

9.  <span data-ttu-id="172db-456">Sélectionnez **un ou plusieurs produits** dans la liste des produits disponibles.</span><span class="sxs-lookup"><span data-stu-id="172db-456">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="172db-457">**Facultatif** Cliquez sur l’élément **Options d’affectation** pour affecter les produits de façon granulaire.</span><span class="sxs-lookup"><span data-stu-id="172db-457">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="172db-458">Cliquez sur **OK** lorsque l’opération est terminée.</span><span class="sxs-lookup"><span data-stu-id="172db-458">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="172db-459">Cliquez sur le bouton **Attribuer** pour affecter ces licences à ce groupe.</span><span class="sxs-lookup"><span data-stu-id="172db-459">Click the **Assign** button to assign these licenses to this group.</span></span> <span data-ttu-id="172db-460">Cette opération peut être très longue, selon la taille et la complexité du groupe.</span><span class="sxs-lookup"><span data-stu-id="172db-460">This may take a long time, depending on the size and complexity of the group.</span></span>

>[!NOTE]
><span data-ttu-id="172db-461">Pour accélérer ce processus, vous pouvez affecter temporairement une licence directement à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="172db-461">To do this faster, consider temporarily assigning a license to the user directly.</span></span> 
>
>

## <a name="next-steps"></a><span data-ttu-id="172db-462">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="172db-462">Next steps</span></span>
[<span data-ttu-id="172db-463">Ajout de nouveaux utilisateurs à Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="172db-463">Add new users to Azure Active Directory</span></span>](active-directory-users-create-azure-portal.md)

