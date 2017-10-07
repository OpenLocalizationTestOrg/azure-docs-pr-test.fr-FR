---
title: "comptes de développeur aaaAuthorize à l’aide d’Azure Active Directory B2C - gestion des API Azure | Documents Microsoft"
description: "Découvrez comment tooauthorize les utilisateurs à l’aide d’Azure Active Directory B2C dans Gestion des API."
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
ms.openlocfilehash: 28f7cae53138938dbbc848b4afcbf08b72690e37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-by-using-azure-active-directory-b2c-in-azure-api-management"></a><span data-ttu-id="5c0b2-103">Le mode tooauthorize développeur de comptes à l’aide d’Azure Active Directory B2C dans Gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="5c0b2-103">How tooauthorize developer accounts by using Azure Active Directory B2C in Azure API Management</span></span>
## <a name="overview"></a><span data-ttu-id="5c0b2-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="5c0b2-104">Overview</span></span>
<span data-ttu-id="5c0b2-105">Azure Active Directory B2C est une solution de gestion des identités de cloud pour applications web et mobiles grand public.</span><span class="sxs-lookup"><span data-stu-id="5c0b2-105">Azure Active Directory B2C is a cloud identity management solution for consumer-facing web and mobile applications.</span></span> <span data-ttu-id="5c0b2-106">Vous pouvez l’utiliser portail des développeurs tooyour toomanage accès.</span><span class="sxs-lookup"><span data-stu-id="5c0b2-106">You can use it toomanage access tooyour developer portal.</span></span> <span data-ttu-id="5c0b2-107">Montre de ce guide vous hello configuration requise dans votre toointegrate du service de gestion des API avec Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="5c0b2-107">This guide shows you hello configuration that's required in your API Management service toointegrate with Azure Active Directory B2C.</span></span> <span data-ttu-id="5c0b2-108">Pour plus d’informations sur l’activation du portail des développeurs toohello accès à l’aide de classique Azure Active Directory, voir [comment tooauthorize développeur comptes à l’aide Azure Active Directory].</span><span class="sxs-lookup"><span data-stu-id="5c0b2-108">For information about enabling access toohello developer portal by using classic Azure Active Directory, see [How tooauthorize developer accounts using Azure Active Directory].</span></span>

> [!NOTE]
> <span data-ttu-id="5c0b2-109">toocomplete hello étapes décrites dans ce guide, vous devez avoir un toocreate de locataire Azure Active Directory B2C une application.</span><span class="sxs-lookup"><span data-stu-id="5c0b2-109">toocomplete hello steps in this guide, you must first have an Azure Active Directory B2C tenant toocreate an application in.</span></span> <span data-ttu-id="5c0b2-110">En outre, vous devez les stratégies d’inscription et connexion toohave prêt.</span><span class="sxs-lookup"><span data-stu-id="5c0b2-110">Also, you need toohave signup and signin policies ready.</span></span> <span data-ttu-id="5c0b2-111">Pour plus d’informations, consultez la [Vue d’ensemble d’Azure Active Directory B2C].</span><span class="sxs-lookup"><span data-stu-id="5c0b2-111">For more information, see [Azure Active Directory B2C overview].</span></span>

## <a name="authorize-developer-accounts-by-using-azure-active-directory-b2c"></a><span data-ttu-id="5c0b2-112">Autoriser des comptes de développeurs avec Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="5c0b2-112">Authorize developer accounts by using Azure Active Directory B2C</span></span>

1. <span data-ttu-id="5c0b2-113">tooget démarré, cliquez sur **portail de publication** Bonjour portail Azure pour votre service de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="5c0b2-113">tooget started, click **Publisher portal** in hello Azure portal for your API Management service.</span></span> <span data-ttu-id="5c0b2-114">Cela vous prend un portail de publication de gestion des API toohello.</span><span class="sxs-lookup"><span data-stu-id="5c0b2-114">This takes you toohello API Management publisher portal.</span></span>

   ![Portail des éditeurs][api-management-management-console]

   > [!NOTE]
   > <span data-ttu-id="5c0b2-116">Si vous n’avez pas encore créé une instance de service de gestion des API, consultez [de créer une instance de service de gestion des API] [ Create an API Management service instance] Bonjour [prise en main le didacticiel de gestion des API Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="5c0b2-116">If you haven't yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management tutorial][Get started with Azure API Management].</span></span>

2. <span data-ttu-id="5c0b2-117">Sur hello **gestion des API** menu, cliquez sur **sécurité**.</span><span class="sxs-lookup"><span data-stu-id="5c0b2-117">On hello **API Management** menu, click **Security**.</span></span> <span data-ttu-id="5c0b2-118">Sur hello **identités** , onglet choisir **Azure Active Directory B2C**.</span><span class="sxs-lookup"><span data-stu-id="5c0b2-118">On hello **Identities** tab, choose **Azure Active Directory B2C**.</span></span>

  ![Identités externes 1][api-management-howto-aad-b2c-security-tab]

3. <span data-ttu-id="5c0b2-120">Prenez note de hello **URL de redirection** et basculer tooAzure Active Directory B2C Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5c0b2-120">Make a note of hello **Redirect URL** and switch over tooAzure Active Directory B2C in hello Azure portal.</span></span>

  ![Identités externes 2][api-management-howto-aad-b2c-security-tab-reply-url]

4. <span data-ttu-id="5c0b2-122">Cliquez sur hello **Applications** bouton.</span><span class="sxs-lookup"><span data-stu-id="5c0b2-122">Click hello **Applications** button.</span></span>

  ![Inscrire une nouvelle application 1][api-management-howto-aad-b2c-portal-menu]

5. <span data-ttu-id="5c0b2-124">Cliquez sur hello **ajouter** bouton toocreate un B2C à Active Directory Azure nouvelle application.</span><span class="sxs-lookup"><span data-stu-id="5c0b2-124">Click hello **Add** button toocreate a new Azure Active Directory B2C application.</span></span>

  ![Inscrire une nouvelle application 2][api-management-howto-aad-b2c-add-button]

6. <span data-ttu-id="5c0b2-126">Bonjour **nouvelle application** panneau, entrez un nom pour l’application hello.</span><span class="sxs-lookup"><span data-stu-id="5c0b2-126">In hello **New application** blade, enter a name for hello application.</span></span> <span data-ttu-id="5c0b2-127">Choisissez **Oui** sous **Application web/API web**, puis choisissez **Oui** sous **Autoriser un flux implicite**.</span><span class="sxs-lookup"><span data-stu-id="5c0b2-127">Choose **Yes** under **Web App/Web API**, and choose **Yes** under **Allow implicit flow**.</span></span> <span data-ttu-id="5c0b2-128">Puis hello de copie **URL de redirection** de hello **Azure Active Directory B2C** section Hello **identités** onglet dans le portail de publication hello et collez-le dans hello **URL de réponse** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="5c0b2-128">Then copy hello **Redirect URL** from hello **Azure Active Directory B2C** section of hello **Identities** tab in hello publisher portal, and paste it into hello **Reply URL** text box.</span></span>

  ![Inscrire une nouvelle application 3][api-management-howto-aad-b2c-app-details]

7. <span data-ttu-id="5c0b2-130">Cliquez sur hello **créer** bouton.</span><span class="sxs-lookup"><span data-stu-id="5c0b2-130">Click hello **Create** button.</span></span> <span data-ttu-id="5c0b2-131">Lorsque l’application hello est créée, elle apparaît dans hello **Applications** panneau.</span><span class="sxs-lookup"><span data-stu-id="5c0b2-131">When hello application is created, it appears in hello **Applications** blade.</span></span> <span data-ttu-id="5c0b2-132">Cliquez sur toosee de nom d’application hello ses détails.</span><span class="sxs-lookup"><span data-stu-id="5c0b2-132">Click hello application name toosee its details.</span></span>

  ![Inscrire une nouvelle application 4][api-management-howto-aad-b2c-app-created]

8. <span data-ttu-id="5c0b2-134">À partir de hello **propriétés** panneau, hello de copie **ID d’Application** toohello Presse-papiers.</span><span class="sxs-lookup"><span data-stu-id="5c0b2-134">From hello **Properties** blade, copy hello **Application ID** toohello clipboard.</span></span>

  ![ID d’application 1][api-management-howto-aad-b2c-app-id]

9. <span data-ttu-id="5c0b2-136">Basculer le portail de publication toohello précédent et collez hello ID hello **Id Client** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="5c0b2-136">Switch back toohello publisher portal and paste hello ID into hello **Client Id** text box.</span></span>

  ![ID d’application 2][api-management-howto-aad-b2c-client-id]

10. <span data-ttu-id="5c0b2-138">Commutateur précédent toohello portail Azure, cliquez sur hello **clés** bouton, puis cliquez sur **générer une clé**.</span><span class="sxs-lookup"><span data-stu-id="5c0b2-138">Switch back toohello Azure portal, click hello **Keys** button, and then click **Generate key**.</span></span> <span data-ttu-id="5c0b2-139">Cliquez sur **enregistrer** hello de configuration et l’affichage de hello toosave **clé application**.</span><span class="sxs-lookup"><span data-stu-id="5c0b2-139">Click **Save** toosave hello configuration and display hello **App key**.</span></span> <span data-ttu-id="5c0b2-140">Copier le Presse-papiers toohello clé hello.</span><span class="sxs-lookup"><span data-stu-id="5c0b2-140">Copy hello key toohello clipboard.</span></span>

  ![Clé d’application 1][api-management-howto-aad-b2c-app-key]

11. <span data-ttu-id="5c0b2-142">Commutateur toohello précédent portal et la coller hello clé publisher dans hello **clé secrète Client** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="5c0b2-142">Switch back toohello publisher portal and paste hello key into hello **Client Secret** text box.</span></span>

  ![Clé d’application 2][api-management-howto-aad-b2c-client-secret]

12. <span data-ttu-id="5c0b2-144">Spécifiez le nom de domaine hello du client hello Azure Active Directory B2C dans **autorisé le client**.</span><span class="sxs-lookup"><span data-stu-id="5c0b2-144">Specify hello domain name of hello Azure Active Directory B2C tenant in **Allowed Tenant**.</span></span>

  ![Client autorisé][api-management-howto-aad-b2c-allowed-tenant]

13. <span data-ttu-id="5c0b2-146">Spécifiez hello **stratégie d’inscription** et **Signin stratégie**.</span><span class="sxs-lookup"><span data-stu-id="5c0b2-146">Specify hello **Signup Policy** and **Signin Policy**.</span></span> <span data-ttu-id="5c0b2-147">Si vous le souhaitez, vous pouvez également fournir hello **stratégie de modification de profil** et **stratégie de réinitialisation du mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="5c0b2-147">Optionally, you can also provide hello **Profile Editing Policy** and **Password Reset Policy**.</span></span>

  ![Stratégies][api-management-howto-aad-b2c-policies]

  > [!NOTE]
  > <span data-ttu-id="5c0b2-149">Pour plus d’informations sur les stratégies, consultez [Azure Active Directory B2C : infrastructure de stratégie extensible].</span><span class="sxs-lookup"><span data-stu-id="5c0b2-149">For more information on policies, see [Azure Active Directory B2C: Extensible policy framework].</span></span>

14. <span data-ttu-id="5c0b2-150">Une fois que vous avez spécifié la configuration souhaitée de hello, cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="5c0b2-150">After you've specified hello desired configuration, click **Save**.</span></span>

  <span data-ttu-id="5c0b2-151">Après avoir enregistrement les modifications de hello, les développeurs seront être toocreate en mesure de nouveaux comptes et se connecter à l’aide d’Azure Active Directory B2C toohello portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="5c0b2-151">After hello changes are saved, developers will be able toocreate new accounts and sign in toohello developer portal by using Azure Active Directory B2C.</span></span>

## <a name="sign-up-for-a-developer-account-by-using-azure-active-directory-b2c"></a><span data-ttu-id="5c0b2-152">Inscrire un compte de développeur avec Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="5c0b2-152">Sign up for a developer account by using Azure Active Directory B2C</span></span>

1. <span data-ttu-id="5c0b2-153">toosign pour un compte de développeur à l’aide de B2C d’Active Directory Azure, ouvrez une nouvelle fenêtre de navigateur et accédez toohello portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="5c0b2-153">toosign up for a developer account by using Azure Active Directory B2C, open a new browser window and go toohello developer portal.</span></span> <span data-ttu-id="5c0b2-154">Cliquez sur hello **inscrire** bouton.</span><span class="sxs-lookup"><span data-stu-id="5c0b2-154">Click hello **Sign up** button.</span></span>

   ![Portail des développeurs 1][api-management-howto-aad-b2c-dev-portal]

2. <span data-ttu-id="5c0b2-156">Cliquez sur toosign avec **Azure Active Directory B2C**.</span><span class="sxs-lookup"><span data-stu-id="5c0b2-156">Choose toosign up with **Azure Active Directory B2C**.</span></span>

   ![Portail des développeurs 2][api-management-howto-aad-b2c-dev-portal-b2c-button]

3. <span data-ttu-id="5c0b2-158">Vous êtes redirigé toohello inscription stratégie que vous avez configuré dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="5c0b2-158">You're redirected toohello signup policy that you configured in hello previous section.</span></span> <span data-ttu-id="5c0b2-159">Choisir toosign à l’aide de votre adresse de messagerie ou l’un de vos comptes sociaux existants.</span><span class="sxs-lookup"><span data-stu-id="5c0b2-159">Choose toosign up by using your email address or one of your existing social accounts.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5c0b2-160">Si Azure Active Directory B2C est hello seule option qui est activée sur hello **identités** onglet dans le portail de publication hello, vous serez redirigé toohello inscription stratégie directement.</span><span class="sxs-lookup"><span data-stu-id="5c0b2-160">If Azure Active Directory B2C is hello only option that's enabled on hello **Identities** tab in hello publisher portal, you'll be redirected toohello signup policy directly.</span></span>

   ![Portail des développeurs][api-management-howto-aad-b2c-dev-portal-b2c-options]

   <span data-ttu-id="5c0b2-162">Lors de l’inscription de hello est terminée, vous êtes redirigé toohello arrière portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="5c0b2-162">When hello signup is complete, you're redirected back toohello developer portal.</span></span> <span data-ttu-id="5c0b2-163">Vous êtes désormais connecté toohello portail des développeurs pour votre instance de service de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="5c0b2-163">You're now signed in toohello developer portal for your API Management service instance.</span></span>

    ![Référencement terminé][api-management-registration-complete]

## <a name="next-steps"></a><span data-ttu-id="5c0b2-165">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5c0b2-165">Next steps</span></span>

*  <span data-ttu-id="5c0b2-166">[Vue d’ensemble d’Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="5c0b2-166">[Azure Active Directory B2C overview]</span></span>
*  <span data-ttu-id="5c0b2-167">[Azure Active Directory B2C : infrastructure de stratégie extensible]</span><span class="sxs-lookup"><span data-stu-id="5c0b2-167">[Azure Active Directory B2C: Extensible policy framework]</span></span>
*  <span data-ttu-id="5c0b2-168">[Utiliser un compte Microsoft comme fournisseur d’identité dans Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="5c0b2-168">[Use a Microsoft account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="5c0b2-169">[Utiliser un compte Google comme fournisseur d’identité dans Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="5c0b2-169">[Use a Google account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="5c0b2-170">[Utiliser un compte LinkedIn comme fournisseur d’identité dans Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="5c0b2-170">[Use a LinkedIn account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="5c0b2-171">[Utiliser un compte Facebook comme fournisseur d’identité dans Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="5c0b2-171">[Use a Facebook account as an identity provider in Azure Active Directory B2C]</span></span>




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

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[Accessing hello Graph API]: http://msdn.microsoft.com/library/azure/dn132599.aspx#BKMK_Graph
[Vue d’ensemble d’Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview
[comment tooauthorize développeur comptes à l’aide Azure Active Directory]: https://docs.microsoft.com/azure/api-management/api-management-howto-aad
[Azure Active Directory B2C : infrastructure de stratégie extensible]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-policies
[Utiliser un compte Microsoft comme fournisseur d’identité dans Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-msa-app
[Utiliser un compte Google comme fournisseur d’identité dans Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-goog-app
[Utiliser un compte Facebook comme fournisseur d’identité dans Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-fb-app
[Utiliser un compte LinkedIn comme fournisseur d’identité dans Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-li-app

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

[Log in toohello Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account
