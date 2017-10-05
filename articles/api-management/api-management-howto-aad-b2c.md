---
title: "Autoriser des comptes de développeurs avec Azure Active Directory B2C dans Gestion des API Azure | Microsoft Docs"
description: "Découvrez comment autoriser des utilisateurs avec Azure Active Directory B2C dans Gestion des API."
services: api-management
documentationcenter: API Management
author: miaojiang
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
ms.openlocfilehash: eb7deb1a79d9db9ac5cfbea69b8d3c564eb55577
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-authorize-developer-accounts-by-using-azure-active-directory-b2c-in-azure-api-management"></a><span data-ttu-id="d5c67-103">Comment autoriser des comptes de développeurs avec Azure Active Directory B2C dans Gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="d5c67-103">How to authorize developer accounts by using Azure Active Directory B2C in Azure API Management</span></span>
## <a name="overview"></a><span data-ttu-id="d5c67-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="d5c67-104">Overview</span></span>
<span data-ttu-id="d5c67-105">Azure Active Directory B2C est une solution de gestion des identités de cloud pour applications web et mobiles grand public.</span><span class="sxs-lookup"><span data-stu-id="d5c67-105">Azure Active Directory B2C is a cloud identity management solution for consumer-facing web and mobile applications.</span></span> <span data-ttu-id="d5c67-106">Vous pouvez l’utiliser pour gérer l’accès au portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="d5c67-106">You can use it to manage access to your developer portal.</span></span> <span data-ttu-id="d5c67-107">Ce guide explique comment configurer votre service Gestion des API requis pour l’intégration avec Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="d5c67-107">This guide shows you the configuration that's required in your API Management service to integrate with Azure Active Directory B2C.</span></span> <span data-ttu-id="d5c67-108">Pour plus d’informations sur l’activation de l’accès au portail des développeurs à l’aide d’Active Directory Azure classique, consultez [Comment autoriser des comptes de développeurs avec Azure Active Directory].</span><span class="sxs-lookup"><span data-stu-id="d5c67-108">For information about enabling access to the developer portal by using classic Azure Active Directory, see [How to authorize developer accounts using Azure Active Directory].</span></span>

> [!NOTE]
> <span data-ttu-id="d5c67-109">Pour effectuer les étapes de ce guide, vous devez disposer d’un client Azure Active Directory B2C dans lequel vous souhaitez créer une application.</span><span class="sxs-lookup"><span data-stu-id="d5c67-109">To complete the steps in this guide, you must first have an Azure Active Directory B2C tenant to create an application in.</span></span> <span data-ttu-id="d5c67-110">Vous devez également disposer de stratégies d’inscription et de connexion.</span><span class="sxs-lookup"><span data-stu-id="d5c67-110">Also, you need to have signup and signin policies ready.</span></span> <span data-ttu-id="d5c67-111">Pour plus d’informations, consultez la [Vue d’ensemble d’Azure Active Directory B2C].</span><span class="sxs-lookup"><span data-stu-id="d5c67-111">For more information, see [Azure Active Directory B2C overview].</span></span>

## <a name="authorize-developer-accounts-by-using-azure-active-directory-b2c"></a><span data-ttu-id="d5c67-112">Autoriser des comptes de développeurs avec Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="d5c67-112">Authorize developer accounts by using Azure Active Directory B2C</span></span>

1. <span data-ttu-id="d5c67-113">Pour commencer, cliquez sur **Portail des éditeurs** dans le portail Azure de votre service Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="d5c67-113">To get started, click **Publisher portal** in the Azure portal for your API Management service.</span></span> <span data-ttu-id="d5c67-114">Vous accédez au portail des éditeurs Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="d5c67-114">This takes you to the API Management publisher portal.</span></span>

   ![Portail des éditeurs][api-management-management-console]

   > [!NOTE]
   > <span data-ttu-id="d5c67-116">Si vous n’avez pas encore créé d’instance de service Gestion des API, consultez la page [Création d’une instance de service Gestion des API][Create an API Management service instance] dans le didacticiel [Prise en main de Gestion des API Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="d5c67-116">If you haven't yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management tutorial][Get started with Azure API Management].</span></span>

2. <span data-ttu-id="d5c67-117">Dans le menu **Gestion des API**, cliquez sur **Sécurité**.</span><span class="sxs-lookup"><span data-stu-id="d5c67-117">On the **API Management** menu, click **Security**.</span></span> <span data-ttu-id="d5c67-118">Dans l’onglet **Identités**, choisissez **Azure Active Directory B2C**.</span><span class="sxs-lookup"><span data-stu-id="d5c67-118">On the **Identities** tab, choose **Azure Active Directory B2C**.</span></span>

  ![Identités externes 1][api-management-howto-aad-b2c-security-tab]

3. <span data-ttu-id="d5c67-120">Notez **l’URL de redirection** et revenez dans Azure Active Directory B2C sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d5c67-120">Make a note of the **Redirect URL** and switch over to Azure Active Directory B2C in the Azure portal.</span></span>

  ![Identités externes 2][api-management-howto-aad-b2c-security-tab-reply-url]

4. <span data-ttu-id="d5c67-122">Cliquez sur le bouton **Applications**.</span><span class="sxs-lookup"><span data-stu-id="d5c67-122">Click the **Applications** button.</span></span>

  ![Inscrire une nouvelle application 1][api-management-howto-aad-b2c-portal-menu]

5. <span data-ttu-id="d5c67-124">Cliquez sur le bouton **Ajouter** pour créer une nouvelle application Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="d5c67-124">Click the **Add** button to create a new Azure Active Directory B2C application.</span></span>

  ![Inscrire une nouvelle application 2][api-management-howto-aad-b2c-add-button]

6. <span data-ttu-id="d5c67-126">Dans le panneau **Nouvelle application**, entrez un nom pour l’application.</span><span class="sxs-lookup"><span data-stu-id="d5c67-126">In the **New application** blade, enter a name for the application.</span></span> <span data-ttu-id="d5c67-127">Choisissez **Oui** sous **Application web/API web**, puis choisissez **Oui** sous **Autoriser un flux implicite**.</span><span class="sxs-lookup"><span data-stu-id="d5c67-127">Choose **Yes** under **Web App/Web API**, and choose **Yes** under **Allow implicit flow**.</span></span> <span data-ttu-id="d5c67-128">Copiez ensuite **l’URL de redirection** dans la section **Azure Active Directory B2C** de l’onglet **Identités** du portail des éditeurs et collez-la dans la zone de texte **URL de réponse**.</span><span class="sxs-lookup"><span data-stu-id="d5c67-128">Then copy the **Redirect URL** from the **Azure Active Directory B2C** section of the **Identities** tab in the publisher portal, and paste it into the **Reply URL** text box.</span></span>

  ![Inscrire une nouvelle application 3][api-management-howto-aad-b2c-app-details]

7. <span data-ttu-id="d5c67-130">Cliquez sur le bouton **Créer** .</span><span class="sxs-lookup"><span data-stu-id="d5c67-130">Click the **Create** button.</span></span> <span data-ttu-id="d5c67-131">Lorsque l’application est créée, elle apparaît dans le panneau **Applications**.</span><span class="sxs-lookup"><span data-stu-id="d5c67-131">When the application is created, it appears in the **Applications** blade.</span></span> <span data-ttu-id="d5c67-132">Cliquez sur le nom de l’application pour afficher les informations la concernant.</span><span class="sxs-lookup"><span data-stu-id="d5c67-132">Click the application name to see its details.</span></span>

  ![Inscrire une nouvelle application 4][api-management-howto-aad-b2c-app-created]

8. <span data-ttu-id="d5c67-134">À partir du panneau **Propriétés**, copiez **l’ID de l’application** dans le Presse-papiers.</span><span class="sxs-lookup"><span data-stu-id="d5c67-134">From the **Properties** blade, copy the **Application ID** to the clipboard.</span></span>

  ![ID d’application 1][api-management-howto-aad-b2c-app-id]

9. <span data-ttu-id="d5c67-136">Revenez au portail des éditeurs et collez l’ID dans la zone de texte **ID client** .</span><span class="sxs-lookup"><span data-stu-id="d5c67-136">Switch back to the publisher portal and paste the ID into the **Client Id** text box.</span></span>

  ![ID d’application 2][api-management-howto-aad-b2c-client-id]

10. <span data-ttu-id="d5c67-138">Revenez au portail Azure, cliquez sur le bouton **Clés**, puis sur **Générer une clé**.</span><span class="sxs-lookup"><span data-stu-id="d5c67-138">Switch back to the Azure portal, click the **Keys** button, and then click **Generate key**.</span></span> <span data-ttu-id="d5c67-139">Cliquez sur **Enregistrer** pour enregistrer la configuration et afficher la **clé d’application**.</span><span class="sxs-lookup"><span data-stu-id="d5c67-139">Click **Save** to save the configuration and display the **App key**.</span></span> <span data-ttu-id="d5c67-140">Copiez la clé dans le Presse-papiers.</span><span class="sxs-lookup"><span data-stu-id="d5c67-140">Copy the key to the clipboard.</span></span>

  ![Clé d’application 1][api-management-howto-aad-b2c-app-key]

11. <span data-ttu-id="d5c67-142">Revenez au portail des éditeurs et collez la clé dans la zone de texte **Clé secrète client** .</span><span class="sxs-lookup"><span data-stu-id="d5c67-142">Switch back to the publisher portal and paste the key into the **Client Secret** text box.</span></span>

  ![Clé d’application 2][api-management-howto-aad-b2c-client-secret]

12. <span data-ttu-id="d5c67-144">Spécifiez le nom de domaine du client Azure Active Directory B2C dans **Client autorisé**.</span><span class="sxs-lookup"><span data-stu-id="d5c67-144">Specify the domain name of the Azure Active Directory B2C tenant in **Allowed Tenant**.</span></span>

  ![Client autorisé][api-management-howto-aad-b2c-allowed-tenant]

13. <span data-ttu-id="d5c67-146">Spécifiez la **Stratégie d’inscription** et la **Stratégie de connexion**.</span><span class="sxs-lookup"><span data-stu-id="d5c67-146">Specify the **Signup Policy** and **Signin Policy**.</span></span> <span data-ttu-id="d5c67-147">Si vous le souhaitez, vous pouvez également fournir la **Stratégie de modification du profil** et la **Stratégie de réinitialisation du mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="d5c67-147">Optionally, you can also provide the **Profile Editing Policy** and **Password Reset Policy**.</span></span>

  ![Stratégies][api-management-howto-aad-b2c-policies]

  > [!NOTE]
  > <span data-ttu-id="d5c67-149">Pour plus d’informations sur les stratégies, consultez [Azure Active Directory B2C : infrastructure de stratégie extensible].</span><span class="sxs-lookup"><span data-stu-id="d5c67-149">For more information on policies, see [Azure Active Directory B2C: Extensible policy framework].</span></span>

14. <span data-ttu-id="d5c67-150">Après avoir spécifié la configuration souhaitée, cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="d5c67-150">After you've specified the desired configuration, click **Save**.</span></span>

  <span data-ttu-id="d5c67-151">Après avoir enregistré les modifications, les développeurs pourront créer de nouveaux comptes et se connecter au portail des développeurs à l’aide d’Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="d5c67-151">After the changes are saved, developers will be able to create new accounts and sign in to the developer portal by using Azure Active Directory B2C.</span></span>

## <a name="sign-up-for-a-developer-account-by-using-azure-active-directory-b2c"></a><span data-ttu-id="d5c67-152">Inscrire un compte de développeur avec Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="d5c67-152">Sign up for a developer account by using Azure Active Directory B2C</span></span>

1. <span data-ttu-id="d5c67-153">Pour inscrire un compte de développeur avec Azure Active Directory B2C, ouvrez une nouvelle fenêtre de navigateur et accédez au portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="d5c67-153">To sign up for a developer account by using Azure Active Directory B2C, open a new browser window and go to the developer portal.</span></span> <span data-ttu-id="d5c67-154">Cliquez sur le bouton **S’inscrire**.</span><span class="sxs-lookup"><span data-stu-id="d5c67-154">Click the **Sign up** button.</span></span>

   ![Portail des développeurs 1][api-management-howto-aad-b2c-dev-portal]

2. <span data-ttu-id="d5c67-156">Choisissez de vous inscrire avec **Azure Active Directory B2C**.</span><span class="sxs-lookup"><span data-stu-id="d5c67-156">Choose to sign up with **Azure Active Directory B2C**.</span></span>

   ![Portail des développeurs 2][api-management-howto-aad-b2c-dev-portal-b2c-button]

3. <span data-ttu-id="d5c67-158">Vous êtes redirigé vers la stratégie d’inscription que vous avez configurée dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="d5c67-158">You're redirected to the signup policy that you configured in the previous section.</span></span> <span data-ttu-id="d5c67-159">Choisissez de vous inscrire avec votre adresse de messagerie ou l’un de vos comptes sociaux existants.</span><span class="sxs-lookup"><span data-stu-id="d5c67-159">Choose to sign up by using your email address or one of your existing social accounts.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d5c67-160">Si Azure Active Directory B2C est la seule option activée dans l’onglet **Identités** sur le portail des éditeurs, vous êtes redirigé directement vers la stratégie d’inscription.</span><span class="sxs-lookup"><span data-stu-id="d5c67-160">If Azure Active Directory B2C is the only option that's enabled on the **Identities** tab in the publisher portal, you'll be redirected to the signup policy directly.</span></span>

   ![Portail des développeurs][api-management-howto-aad-b2c-dev-portal-b2c-options]

   <span data-ttu-id="d5c67-162">Une fois l’inscription terminée, vous êtes redirigé vers le portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="d5c67-162">When the signup is complete, you're redirected back to the developer portal.</span></span> <span data-ttu-id="d5c67-163">Vous êtes maintenant inscrit sur le portail des développeurs pour votre instance de service Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="d5c67-163">You're now signed in to the developer portal for your API Management service instance.</span></span>

    ![Référencement terminé][api-management-registration-complete]

## <a name="next-steps"></a><span data-ttu-id="d5c67-165">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d5c67-165">Next steps</span></span>

*  <span data-ttu-id="d5c67-166">[Vue d’ensemble d’Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="d5c67-166">[Azure Active Directory B2C overview]</span></span>
*  <span data-ttu-id="d5c67-167">[Azure Active Directory B2C : infrastructure de stratégie extensible]</span><span class="sxs-lookup"><span data-stu-id="d5c67-167">[Azure Active Directory B2C: Extensible policy framework]</span></span>
*  <span data-ttu-id="d5c67-168">[Utiliser un compte Microsoft comme fournisseur d’identité dans Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="d5c67-168">[Use a Microsoft account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="d5c67-169">[Utiliser un compte Google comme fournisseur d’identité dans Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="d5c67-169">[Use a Google account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="d5c67-170">[Utiliser un compte LinkedIn comme fournisseur d’identité dans Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="d5c67-170">[Use a LinkedIn account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="d5c67-171">[Utiliser un compte Facebook comme fournisseur d’identité dans Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="d5c67-171">[Use a Facebook account as an identity provider in Azure Active Directory B2C]</span></span>




[api-management-howto-aad-b2c-security-tab]: ./media/api-management-howto-aad-b2c/api-management-b2c-security-tab.PNG
[api-management-howto-aad-b2c-security-tab-reply-url]: ./media/api-management-howto-aad-b2c/api-management-b2c-security-tab-reply-url.PNG
[api-management-howto-aad-b2c-portal-menu]: ./media/api-management-howto-aad-b2c/api-management-b2c-portal-menu.PNG
[api-management-howto-aad-b2c-add-button]: ./media/api-management-howto-aad-b2c/api-management-b2c-add-button.PNG
[api-management-howto-aad-b2c-app-details]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-details.PNG
[api-management-howto-aad-b2c-app-created]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-created.PNG
[api-management-howto-aad-b2c-app-id]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-id.PNG
[api-management-howto-aad-b2c-client-id]: ./media/api-management-howto-aad-b2c/api-management-b2c-client-id.PNG
[api-management-howto-aad-b2c-app-key]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-key.PNG
[api-management-howto-aad-b2c-app-key-saved]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-key-saved.PNG
[api-management-howto-aad-b2c-client-secret]: ./media/api-management-howto-aad-b2c/api-management-b2c-client-secret.PNG
[api-management-howto-aad-b2c-allowed-tenant]: ./media/api-management-howto-aad-b2c/api-management-b2c-allowed-tenant.PNG
[api-management-howto-aad-b2c-policies]: ./media/api-management-howto-aad-b2c/api-management-b2c-policies.PNG
[api-management-howto-aad-b2c-dev-portal]: ./media/api-management-howto-aad-b2c/api-management-b2c-dev-portal.PNG
[api-management-howto-aad-b2c-dev-portal-b2c-button]: ./media/api-management-howto-aad-b2c/api-management-b2c-dev-portal-b2c-button.PNG
[api-management-howto-aad-b2c-dev-portal-b2c-options]: ./media/api-management-howto-aad-b2c/api-management-b2c-dev-portal-b2c-options.PNG
[api-management-complete-registration]: ./media/api-management-howto-aad/api-management-complete-registration.PNG
[api-management-registration-complete]: ./media/api-management-howto-aad/api-management-registration-complete.png

[api-management-management-console]: ./media/api-management-howto-aad/api-management-management-console.png
[api-management-security-external-identities]: ./media/api-management-howto-aad/api-management-b2c-security-tab.png
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
[api-management-aad-app-multi-tenant]: ./media/api-management-howto-aad/api-management-aad-app-multi-tenant.png
[api-management-aad-reply-url]: ./media/api-management-howto-aad/api-management-aad-reply-url.png
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
<span data-ttu-id="d5c67-172">[Vue d’ensemble d’Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview</span><span class="sxs-lookup"><span data-stu-id="d5c67-172">[Azure Active Directory B2C overview]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview</span></span>
<span data-ttu-id="d5c67-173">[Comment autoriser des comptes de développeurs avec Azure Active Directory]: https://docs.microsoft.com/azure/api-management/api-management-howto-aad</span><span class="sxs-lookup"><span data-stu-id="d5c67-173">[How to authorize developer accounts using Azure Active Directory]: https://docs.microsoft.com/azure/api-management/api-management-howto-aad</span></span>
<span data-ttu-id="d5c67-174">[Azure Active Directory B2C : infrastructure de stratégie extensible]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-policies</span><span class="sxs-lookup"><span data-stu-id="d5c67-174">[Azure Active Directory B2C: Extensible policy framework]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-policies</span></span>
<span data-ttu-id="d5c67-175">[Utiliser un compte Microsoft comme fournisseur d’identité dans Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-msa-app</span><span class="sxs-lookup"><span data-stu-id="d5c67-175">[Use a Microsoft account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-msa-app</span></span>
<span data-ttu-id="d5c67-176">[Utiliser un compte Google comme fournisseur d’identité dans Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-goog-app</span><span class="sxs-lookup"><span data-stu-id="d5c67-176">[Use a Google account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-goog-app</span></span>
<span data-ttu-id="d5c67-177">[Utiliser un compte Facebook comme fournisseur d’identité dans Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-fb-app</span><span class="sxs-lookup"><span data-stu-id="d5c67-177">[Use a Facebook account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-fb-app</span></span>
<span data-ttu-id="d5c67-178">[Utiliser un compte LinkedIn comme fournisseur d’identité dans Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-li-app</span><span class="sxs-lookup"><span data-stu-id="d5c67-178">[Use a LinkedIn account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-li-app</span></span>

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API to use OAuth 2.0 user authorization]: #step2
[Test the OAuth 2.0 user authorization in the Developer Portal]: #step3
[Next steps]: #next-steps

[Log in to the Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account
