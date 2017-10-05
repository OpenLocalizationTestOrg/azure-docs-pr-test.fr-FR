---
title: "Autoriser des comptes de développeurs à l’aide d’Azure Active Directory dans Gestion des API Azure | Microsoft Docs"
description: Comment autoriser des utilisateurs avec Azure Active Directory dans Gestion des API.
services: api-management
documentationcenter: API Management
author: steved0x
manager: erikre
editor: 
ms.assetid: 33a69a83-94f2-4e4e-9cef-f2a5af3c9732
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 7637e6419d17a2d75904fbe63df5f27d4be4bbe3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-authorize-developer-accounts-using-azure-active-directory-in-azure-api-management"></a><span data-ttu-id="c39cf-103">Comment autoriser des comptes de développeurs avec Azure Active Directory dans Gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="c39cf-103">How to authorize developer accounts using Azure Active Directory in Azure API Management</span></span>
## <a name="overview"></a><span data-ttu-id="c39cf-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="c39cf-104">Overview</span></span>
<span data-ttu-id="c39cf-105">Ce guide vous explique comment activer l’accès au portail des développeurs pour les utilisateurs d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c39cf-105">This guide shows you how to enable access to the developer portal for users from Azure Active Directory.</span></span> <span data-ttu-id="c39cf-106">Il vous montre également comment gérer des groupes d’utilisateurs Azure Active Directory en ajoutant des groupes externes qui contiennent les utilisateurs d’un annuaire Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c39cf-106">This guide also shows you how to manage groups of Azure Active Directory users by adding external groups that contain the users of an Azure Active Directory.</span></span>

> <span data-ttu-id="c39cf-107">Pour effectuer les étapes de ce guide, vous devez disposer d’un annuaire Azure Active Directory dans lequel vous souhaitez créer une application.</span><span class="sxs-lookup"><span data-stu-id="c39cf-107">To complete the steps in this guide you must first have an Azure Active Directory in which to create an application.</span></span>
> 
> 

## <a name="how-to-authorize-developer-accounts-using-azure-active-directory"></a><span data-ttu-id="c39cf-108">Comment autoriser des comptes de développeurs avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c39cf-108">How to authorize developer accounts using Azure Active Directory</span></span>
<span data-ttu-id="c39cf-109">Pour commencer, cliquez sur **Portail des éditeurs** dans le portail Azure de votre service Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="c39cf-109">To get started, click **Publisher portal** in the Azure portal for your API Management service.</span></span> <span data-ttu-id="c39cf-110">Vous accédez au portail des éditeurs Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="c39cf-110">This takes you to the API Management publisher portal.</span></span>

![Portail des éditeurs][api-management-management-console]

> <span data-ttu-id="c39cf-112">Si vous n’avez pas encore créé une instance de service Gestion des API, consultez la page de [création d’une instance de service Gestion des API][Create an API Management service instance] dans le didacticiel de [prise en main de Gestion des API Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="c39cf-112">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="c39cf-113">Cliquez sur **Sécurité** dans le menu **Gestion des API** à gauche, puis sur **Identités externes**.</span><span class="sxs-lookup"><span data-stu-id="c39cf-113">Click **Security** from the **API Management** menu on the left and click **External Identities**.</span></span>

![Identités externes][api-management-security-external-identities]

<span data-ttu-id="c39cf-115">Cliquez sur **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c39cf-115">Click **Azure Active Directory**.</span></span> <span data-ttu-id="c39cf-116">Notez l’ **URL de redirection** et revenez à votre annuaire Azure Active Directory dans le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="c39cf-116">Make a note of the **Redirect URL** and switch over to your Azure Active Directory in the Azure Classic Portal.</span></span>

![Identités externes][api-management-security-aad-new]

<span data-ttu-id="c39cf-118">Cliquez sur le bouton **Ajouter** pour créer une application Azure Active Directory, puis choisissez **Ajouter une application développée par mon organisation**.</span><span class="sxs-lookup"><span data-stu-id="c39cf-118">Click the **Add** button to create a new Azure Active Directory application, and choose **Add an application my organization is developing**.</span></span>

![Ajouter de nouvelles applications Azure Active Directory][api-management-new-aad-application-menu]

<span data-ttu-id="c39cf-120">Entrez le nom de l’application, sélectionnez **Application web et/ou API web**, puis cliquez sur le bouton Suivant.</span><span class="sxs-lookup"><span data-stu-id="c39cf-120">Enter a name for the application, select **Web application and/or Web API**, and click the next button.</span></span>

![Nouvelle application Azure Active Directory][api-management-new-aad-application-1]

<span data-ttu-id="c39cf-122">Pour **URL de connexion**, entrez l’URL de connexion de votre portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="c39cf-122">For **Sign-on URL**, enter the sign-on URL of your developer portal.</span></span> <span data-ttu-id="c39cf-123">Dans cet exemple, la valeur de **URL de connexion** est `https://aad03.portal.current.int-azure-api.net/signin`.</span><span class="sxs-lookup"><span data-stu-id="c39cf-123">In this example, the **Sign-on URL** is `https://aad03.portal.current.int-azure-api.net/signin`.</span></span> 

<span data-ttu-id="c39cf-124">Dans **URL d’ID de l’application**, entrez le domaine par défaut ou un domaine personnalisé pour Azure Active Directory et ajoutez une chaîne unique.</span><span class="sxs-lookup"><span data-stu-id="c39cf-124">For the **App ID URL**, enter either the default domain or a custom domain for the Azure Active Directory, and append a unique string to it.</span></span> <span data-ttu-id="c39cf-125">Dans cet exemple, le domaine par défaut de **https://contoso5api.onmicrosoft.com** est utilisé avec le suffixe **/api** spécifié.</span><span class="sxs-lookup"><span data-stu-id="c39cf-125">In this example, the default domain of **https://contoso5api.onmicrosoft.com** is used with the suffix of **/api** specified.</span></span>

![Propriétés de la nouvelle application Azure Active Directory][api-management-new-aad-application-2]

<span data-ttu-id="c39cf-127">Cliquez sur la coche pour enregistrer et créer l’application, puis revenez à l’onglet **Configurer** pour configurer la nouvelle application.</span><span class="sxs-lookup"><span data-stu-id="c39cf-127">Click the check button to save and create the application, and switch to the **Configure** tab to configure the new application.</span></span>

![Nouvelle application Azure Active Directory créée][api-management-new-aad-app-created]

<span data-ttu-id="c39cf-129">Si plusieurs annuaires Azure Active Directory vont être utilisés pour cette application, cliquez sur **Oui** pour **Application mutualisée**.</span><span class="sxs-lookup"><span data-stu-id="c39cf-129">If multiple Azure Active Directories are going to be used for this application, click **Yes** for **Application is multi-tenant**.</span></span> <span data-ttu-id="c39cf-130">La valeur par défaut est **Non**.</span><span class="sxs-lookup"><span data-stu-id="c39cf-130">The default is **No**.</span></span>

![Application mutualisée][api-management-aad-app-multi-tenant]

<span data-ttu-id="c39cf-132">Copiez **l’URL de redirection** dans la section **Azure Active Directory** de l’onglet **Identités externes** du portail des éditeurs et collez-la dans la zone de texte **URL de réponse**.</span><span class="sxs-lookup"><span data-stu-id="c39cf-132">Copy the **Redirect URL** from the **Azure Active Directory** section of the **External Identities** tab in the publisher portal and paste it into the **Reply URL** text box.</span></span> 

![URL de réponse][api-management-aad-reply-url]

<span data-ttu-id="c39cf-134">Allez en bas de l’onglet Configurer, sélectionnez la liste déroulante **Autorisations de l’application** et activez l’option **Lire les données de l’annuaire**.</span><span class="sxs-lookup"><span data-stu-id="c39cf-134">Scroll to the bottom of the configure tab, select the **Application Permissions** drop-down, and check **Read directory data**.</span></span>

![Autorisations de l’application][api-management-aad-app-permissions]

<span data-ttu-id="c39cf-136">Sélectionnez la liste déroulante **Déléguer les autorisations** et activez l’option **Activer l’authentification et lire les profils utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="c39cf-136">Select the **Delegate Permissions** drop-down, and check **Enable sign-on and read users' profiles**.</span></span>

![Autorisations déléguées][api-management-aad-delegated-permissions]

> <span data-ttu-id="c39cf-138">Pour plus d’informations sur l’application et les autorisations déléguées, consultez la page [Accès à l’API Graph][Accessing the Graph API].</span><span class="sxs-lookup"><span data-stu-id="c39cf-138">For more information about application and delegated permissions, see [Accessing the Graph API][Accessing the Graph API].</span></span>
> 
> 

<span data-ttu-id="c39cf-139">Copiez l’ **ID de client** dans le Presse-papiers.</span><span class="sxs-lookup"><span data-stu-id="c39cf-139">Copy the **Client Id** to the clipboard.</span></span>

![ID de client][api-management-aad-app-client-id]

<span data-ttu-id="c39cf-141">Revenez au portail des éditeurs et collez l’ **ID de client** copié dans la configuration de l’application Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c39cf-141">Switch back to the publisher portal and paste in the **Client Id** copied from the Azure Active Directory application configuration.</span></span>

![ID de client][api-management-client-id]

<span data-ttu-id="c39cf-143">Revenez à la configuration d’Azure Active Directory, puis cliquez sur la liste déroulante **Sélectionner une durée** dans la section **Clés** et spécifiez un intervalle.</span><span class="sxs-lookup"><span data-stu-id="c39cf-143">Switch back to the Azure Active Directory configuration, and click the **Select duration** drop-down in the **Keys** section and specify an interval.</span></span> <span data-ttu-id="c39cf-144">Dans cet exemple, la valeur **1 an** est utilisée.</span><span class="sxs-lookup"><span data-stu-id="c39cf-144">In this example, **1 year** is used.</span></span>

![Clé][api-management-aad-key-before-save]

<span data-ttu-id="c39cf-146">Cliquez sur **Enregistrer** pour enregistrer la configuration et afficher la clé.</span><span class="sxs-lookup"><span data-stu-id="c39cf-146">Click **Save** to save the configuration and display the key.</span></span> <span data-ttu-id="c39cf-147">Copiez la clé dans le Presse-papiers.</span><span class="sxs-lookup"><span data-stu-id="c39cf-147">Copy the key to the clipboard.</span></span>

> <span data-ttu-id="c39cf-148">Notez sa valeur.</span><span class="sxs-lookup"><span data-stu-id="c39cf-148">Make a note of this key.</span></span> <span data-ttu-id="c39cf-149">Une fois que vous fermez la fenêtre de configuration Azure Active Directory, la clé ne peut plus être affichée.</span><span class="sxs-lookup"><span data-stu-id="c39cf-149">Once you close the Azure Active Directory configuration window, the key cannot be displayed again.</span></span>
> 
> 

![Clé][api-management-aad-key-after-save]

<span data-ttu-id="c39cf-151">Revenez au portail des éditeurs et collez la clé dans la zone de texte **Clé secrète client** .</span><span class="sxs-lookup"><span data-stu-id="c39cf-151">Switch back to the publisher portal and paste the key into the **Client Secret** text box.</span></span>

![Clé secrète client][api-management-client-secret]

<span data-ttu-id="c39cf-153">**Locataires autorisés** spécifie les répertoires qui ont accès aux API de l’instance de service Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="c39cf-153">**Allowed Tenants** specifies which directories have access to the APIs of the API Management service instance.</span></span> <span data-ttu-id="c39cf-154">Spécifiez les domaines des instances Azure Active Directory auxquelles vous souhaitez accorder l’accès.</span><span class="sxs-lookup"><span data-stu-id="c39cf-154">Specify the domains of the Azure Active Directory instances to which you want to grant access.</span></span> <span data-ttu-id="c39cf-155">Vous pouvez séparer plusieurs domaines par des sauts de ligne, des espaces ou des virgules.</span><span class="sxs-lookup"><span data-stu-id="c39cf-155">You can separate multiple domains with newlines, spaces, or commas.</span></span>

![Locataires autorisés][api-management-client-allowed-tenants]


<span data-ttu-id="c39cf-157">Une fois la configuration souhaitée spécifiée, cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="c39cf-157">Once the desired configuration is specified, click **Save**.</span></span>

![Enregistrer][api-management-client-allowed-tenants-save]

<span data-ttu-id="c39cf-159">Après avoir enregistré les modifications, les utilisateurs de l’annuaire Azure Active Directory spécifié peuvent se connecter au portail des développeurs en suivant les étapes de la section [Connexion au portail des développeurs avec un compte Azure Active Directory][Log in to the Developer portal using an Azure Active Directory account].</span><span class="sxs-lookup"><span data-stu-id="c39cf-159">Once the changes are saved, the users in the specified Azure Active Directory can sign in to the Developer portal by following the steps in [Log in to the Developer portal using an Azure Active Directory account][Log in to the Developer portal using an Azure Active Directory account].</span></span>

<span data-ttu-id="c39cf-160">Plusieurs domaines peuvent être spécifiés dans la section **Locataires autorisés** .</span><span class="sxs-lookup"><span data-stu-id="c39cf-160">Multiple domains can be specified in the **Allowed Tenants** section.</span></span> <span data-ttu-id="c39cf-161">Avant qu’un utilisateur puisse se connecter à partir d’un autre domaine que le domaine d’origine dans lequel l’application a été enregistrée, l’administrateur général de l’autre domaine doit accorder à l’application l’autorisation d’accéder aux données de l’annuaire.</span><span class="sxs-lookup"><span data-stu-id="c39cf-161">Before any user can log in from a different domain than the original domain where the application was registered, a global administrator of the different domain must grant permission for the application to access directory data.</span></span> <span data-ttu-id="c39cf-162">Pour accorder l’autorisation, l’administrateur général doit accéder à `https://<URL of your developer portal>/aadadminconsent` (par exemple, https://contoso.portal.azure-api.net/aadadminconsent), entrer le nom de domaine du client Active Directory auquel il souhaite accorder l’accès, puis cliquer sur Envoyer.</span><span class="sxs-lookup"><span data-stu-id="c39cf-162">To grant permission, the global administrator should go to `https://<URL of your developer portal>/aadadminconsent` (for example, https://contoso.portal.azure-api.net/aadadminconsent), type in the domain name of the Active Directory tenant they want to give access to and click Submit.</span></span> <span data-ttu-id="c39cf-163">Dans l’exemple suivant, un administrateur général de `miaoaad.onmicrosoft.com` tente d’accorder l’autorisation à ce portail développeur spécifique.</span><span class="sxs-lookup"><span data-stu-id="c39cf-163">In the following example, a global administrator from `miaoaad.onmicrosoft.com` is trying to give permission to this particular developer portal.</span></span> 

![Autorisations][api-management-aad-consent]

<span data-ttu-id="c39cf-165">Dans l’écran suivant, l’administrateur général sera invité à confirmer l’octroi de l’autorisation.</span><span class="sxs-lookup"><span data-stu-id="c39cf-165">In the next screen, the global administrator will be prompted to confirm giving the permission.</span></span> 

![Autorisations][api-management-permissions-form]

> <span data-ttu-id="c39cf-167">Si un administrateur autre que l’administrateur global tente de se connecter avant que les autorisations ne soient accordées par un administrateur général, la tentative de connexion échoue et un écran d’erreur s’affiche.</span><span class="sxs-lookup"><span data-stu-id="c39cf-167">If a non-global administrator tries to log in before permissions are granted by a global administrator, the login attempt fails and an error screen is displayed.</span></span>
> 
> 

## <a name="how-to-add-an-external-azure-active-directory-group"></a><span data-ttu-id="c39cf-168">Ajout d’un groupe Azure Active Directory externe</span><span class="sxs-lookup"><span data-stu-id="c39cf-168">How to add an external Azure Active Directory Group</span></span>
<span data-ttu-id="c39cf-169">Après avoir activé l’accès pour les utilisateurs dans Azure Active Directory, vous pouvez ajouter des groupes Azure Active Directory à Gestion des API pour gérer plus facilement l’association des développeurs du groupe avec les produits souhaités.</span><span class="sxs-lookup"><span data-stu-id="c39cf-169">After enabling access for users in an Azure Active Directory, you can add Azure Active Directory groups into API Management to more easily manage the association of the developers in the group with the desired products.</span></span>

> <span data-ttu-id="c39cf-170">Pour pouvoir configurer un groupe Azure Active Directory externe, Azure Active Directory doit d’abord être configuré dans l’onglet Identités, selon la procédure décrite dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="c39cf-170">To configure an external Azure Active Directory group, the Azure Active Directory must first be configured in the Identities tab by following the procedure in the previous section.</span></span> 
> 
> 

<span data-ttu-id="c39cf-171">Les groupes Azure Active Directory externes sont ajoutés à partir de l’onglet **Visibilité** du produit auquel vous souhaitez accorder l’accès au groupe.</span><span class="sxs-lookup"><span data-stu-id="c39cf-171">External Azure Active Directory groups are added from the **Visibility** tab of the product for which you wish to grant access to the group.</span></span> <span data-ttu-id="c39cf-172">Cliquez sur **Produits**, puis sur le nom du produit souhaité.</span><span class="sxs-lookup"><span data-stu-id="c39cf-172">Click **Products**, and then click the name of the desired product.</span></span>

![Configure product][api-management-configure-product]

<span data-ttu-id="c39cf-174">Passez à l’onglet **Visibilité**, puis cliquez sur **Ajouter des groupes depuis Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c39cf-174">Switch to the **Visibility** tab, and click **Add Groups from Azure Active Directory**.</span></span>

![Ajouter des groupes][api-management-add-groups]

<span data-ttu-id="c39cf-176">Sélectionnez le **locataire Azure Active Directory** dans la liste déroulante, puis tapez le nom du groupe de votre choix dans la zone de texte des **groupes** à ajouter.</span><span class="sxs-lookup"><span data-stu-id="c39cf-176">Select the **Azure Active Directory Tenant** from the drop-down list, and then type the name of the desired group in the **Groups** to be added text box.</span></span>

![Sélectionner un groupe][api-management-select-group]

<span data-ttu-id="c39cf-178">Ce nom de groupe se trouve dans la liste **Groupes** de votre annuaire Azure Active Directory, comme illustré dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="c39cf-178">This group name can be found in the **Groups** list for your Azure Active Directory, as shown in the following example.</span></span>

![Liste des groupes Azure Active Directory][api-management-aad-groups-list]

<span data-ttu-id="c39cf-180">Cliquez sur **Ajouter** pour valider le nom du groupe et ajouter le groupe.</span><span class="sxs-lookup"><span data-stu-id="c39cf-180">Click **Add** to validate the group name and add the group.</span></span> <span data-ttu-id="c39cf-181">Dans cet exemple, le groupe externe **Contoso 5 Developers** est ajouté.</span><span class="sxs-lookup"><span data-stu-id="c39cf-181">In this example, the **Contoso 5 Developers** external group is added.</span></span> 

![Group added][api-management-aad-group-added]

<span data-ttu-id="c39cf-183">Cliquez sur **Enregistrer** pour enregistrer la nouvelle sélection de groupe.</span><span class="sxs-lookup"><span data-stu-id="c39cf-183">Click **Save** to save the new group selection.</span></span>

<span data-ttu-id="c39cf-184">Une fois le groupe Azure Active Directory configuré à partir d’un produit, il est consultable dans l’onglet **Visibilité** des autres produits dans l’instance de service Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="c39cf-184">Once an Azure Active Directory group has been configured from one product, it is available to be checked on the **Visibility** tab for the other products in the API Management service instance.</span></span>

<span data-ttu-id="c39cf-185">Pour vérifier et configurer les propriétés des groupes externes une fois qu’ils ont été ajoutés, cliquez sur le nom du groupe dans l’onglet **Groupes**.</span><span class="sxs-lookup"><span data-stu-id="c39cf-185">To review and configure the properties for external groups once they have been added, click the name of the group from the **Groups** tab.</span></span>

![Gérer les groupes][api-management-groups]

<span data-ttu-id="c39cf-187">À partir de là, vous pouvez modifier le **nom** et la **description** du groupe.</span><span class="sxs-lookup"><span data-stu-id="c39cf-187">From here you can edit the **Name** and the **Description** of the group.</span></span>

![Modifier un groupe][api-management-edit-group]

<span data-ttu-id="c39cf-189">Les utilisateurs de l’annuaire Azure Active Directory configuré peuvent se connecter au portail des développeurs et consulter des groupes. Ils peuvent s’abonner aux groupes qui leur sont accessibles selon les instructions de la section suivante.</span><span class="sxs-lookup"><span data-stu-id="c39cf-189">Users from the configured Azure Active Directory can sign in to the Developer portal and view and subscribe to any groups for which they have visibility by following the instructions in the following section.</span></span>

## <a name="how-to-log-in-to-the-developer-portal-using-an-azure-active-directory-account"></a><span data-ttu-id="c39cf-190">Connexion au portail des développeurs avec un compte Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c39cf-190">How to log in to the Developer portal using an Azure Active Directory account</span></span>
<span data-ttu-id="c39cf-191">Pour vous connecter au portail des développeurs à l’aide d’un compte Azure Active Directory configuré dans les sections précédentes, ouvrez une nouvelle fenêtre de navigateur avec **l’URL de connexion** dans la configuration de l’application Active Directory, puis cliquez sur **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c39cf-191">To log into the Developer portal using an Azure Active Directory account configured in the previous sections, open a new browser window using the **Sign-on URL** from the Active Directory application configuration, and click **Azure Active Directory**.</span></span>

![Portail des développeurs][api-management-dev-portal-signin]

<span data-ttu-id="c39cf-193">Entrez les informations d’identification d’un des utilisateurs dans votre annuaire Azure Active Directory, puis cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="c39cf-193">Enter the credentials of one of the users in your Azure Active Directory, and click **Sign in**.</span></span>

![Se connecter][api-management-aad-signin]

<span data-ttu-id="c39cf-195">Un formulaire d’inscription peut vous être présenté si certaines informations supplémentaires sont requises.</span><span class="sxs-lookup"><span data-stu-id="c39cf-195">You may be prompted with a registration form if any additional information is required.</span></span> <span data-ttu-id="c39cf-196">Renseignez le formulaire d’inscription, puis cliquez sur **S’inscrire**.</span><span class="sxs-lookup"><span data-stu-id="c39cf-196">Complete the registration form and click **Sign up**.</span></span>

![Inscription][api-management-complete-registration]

<span data-ttu-id="c39cf-198">Votre utilisateur est maintenant connecté au portail des développeurs pour votre instance de service Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="c39cf-198">Your user is now logged into the developer portal for your API Management service instance.</span></span>

![Inscription terminée][api-management-registration-complete]

[api-management-management-console]: ./media/api-management-howto-aad/api-management-management-console.png
[api-management-security-external-identities]: ./media/api-management-howto-aad/api-management-security-external-identities.png
[api-management-security-aad-new]: ./media/api-management-howto-aad/api-management-security-aad-new.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-aad/api-management-new-aad-application-menu.png
[api-management-new-aad-application-1]: ./media/api-management-howto-aad/api-management-new-aad-application-1.png
[api-management-new-aad-application-2]: ./media/api-management-howto-aad/api-management-new-aad-application-2.png
[api-management-new-aad-app-created]: ./media/api-management-howto-aad/api-management-new-aad-app-created.png
[api-management-aad-app-permissions]: ./media/api-management-howto-aad/api-management-aad-app-permissions.png
[api-management-aad-app-client-id]: ./media/api-management-howto-aad/api-management-aad-app-client-id.png
[api-management-client-id]: ./media/api-management-howto-aad/api-management-client-id.png
[api-management-aad-key-before-save]: ./media/api-management-howto-aad/api-management-aad-key-before-save.png
[api-management-aad-key-after-save]: ./media/api-management-howto-aad/api-management-aad-key-after-save.png
[api-management-client-secret]: ./media/api-management-howto-aad/api-management-client-secret.png
[api-management-client-allowed-tenants]: ./media/api-management-howto-aad/api-management-client-allowed-tenants.png
[api-management-client-allowed-tenants-save]: ./media/api-management-howto-aad/api-management-client-allowed-tenants-save.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-aad/api-management-aad-delegated-permissions.png
[api-management-dev-portal-signin]: ./media/api-management-howto-aad/api-management-dev-portal-signin.png
[api-management-aad-signin]: ./media/api-management-howto-aad/api-management-aad-signin.png
[api-management-complete-registration]: ./media/api-management-howto-aad/api-management-complete-registration.png
[api-management-registration-complete]: ./media/api-management-howto-aad/api-management-registration-complete.png
[api-management-aad-app-multi-tenant]: ./media/api-management-howto-aad/api-management-aad-app-multi-tenant.png
[api-management-aad-reply-url]: ./media/api-management-howto-aad/api-management-aad-reply-url.png
[api-management-aad-consent]: ./media/api-management-howto-aad/api-management-aad-consent.png
[api-management-permissions-form]: ./media/api-management-howto-aad/api-management-permissions-form.png
[api-management-configure-product]: ./media/api-management-howto-aad/api-management-configure-product.png
[api-management-add-groups]: ./media/api-management-howto-aad/api-management-add-groups.png
[api-management-select-group]: ./media/api-management-howto-aad/api-management-select-group.png
[api-management-aad-groups-list]: ./media/api-management-howto-aad/api-management-aad-groups-list.png
[api-management-aad-group-added]: ./media/api-management-howto-aad/api-management-aad-group-added.png
[api-management-groups]: ./media/api-management-howto-aad/api-management-groups.png
[api-management-edit-group]: ./media/api-management-howto-aad/api-management-edit-group.png

[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[Accessing the Graph API]: http://msdn.microsoft.com/library/azure/dn132599.aspx#BKMK_Graph

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API to use OAuth 2.0 user authorization]: #step2
[Test the OAuth 2.0 user authorization in the Developer Portal]: #step3
[Next steps]: #next-steps

[Log in to the Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account

