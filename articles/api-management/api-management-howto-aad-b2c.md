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
# <a name="how-tooauthorize-developer-accounts-by-using-azure-active-directory-b2c-in-azure-api-management"></a>Le mode tooauthorize développeur de comptes à l’aide d’Azure Active Directory B2C dans Gestion des API Azure
## <a name="overview"></a>Vue d'ensemble
Azure Active Directory B2C est une solution de gestion des identités de cloud pour applications web et mobiles grand public. Vous pouvez l’utiliser portail des développeurs tooyour toomanage accès. Montre de ce guide vous hello configuration requise dans votre toointegrate du service de gestion des API avec Azure Active Directory B2C. Pour plus d’informations sur l’activation du portail des développeurs toohello accès à l’aide de classique Azure Active Directory, voir [comment tooauthorize développeur comptes à l’aide Azure Active Directory].

> [!NOTE]
> toocomplete hello étapes décrites dans ce guide, vous devez avoir un toocreate de locataire Azure Active Directory B2C une application. En outre, vous devez les stratégies d’inscription et connexion toohave prêt. Pour plus d’informations, consultez la [Vue d’ensemble d’Azure Active Directory B2C].

## <a name="authorize-developer-accounts-by-using-azure-active-directory-b2c"></a>Autoriser des comptes de développeurs avec Azure Active Directory B2C

1. tooget démarré, cliquez sur **portail de publication** Bonjour portail Azure pour votre service de gestion des API. Cela vous prend un portail de publication de gestion des API toohello.

   ![Portail des éditeurs][api-management-management-console]

   > [!NOTE]
   > Si vous n’avez pas encore créé une instance de service de gestion des API, consultez [de créer une instance de service de gestion des API] [ Create an API Management service instance] Bonjour [prise en main le didacticiel de gestion des API Azure][Get started with Azure API Management].

2. Sur hello **gestion des API** menu, cliquez sur **sécurité**. Sur hello **identités** , onglet choisir **Azure Active Directory B2C**.

  ![Identités externes 1][api-management-howto-aad-b2c-security-tab]

3. Prenez note de hello **URL de redirection** et basculer tooAzure Active Directory B2C Bonjour portail Azure.

  ![Identités externes 2][api-management-howto-aad-b2c-security-tab-reply-url]

4. Cliquez sur hello **Applications** bouton.

  ![Inscrire une nouvelle application 1][api-management-howto-aad-b2c-portal-menu]

5. Cliquez sur hello **ajouter** bouton toocreate un B2C à Active Directory Azure nouvelle application.

  ![Inscrire une nouvelle application 2][api-management-howto-aad-b2c-add-button]

6. Bonjour **nouvelle application** panneau, entrez un nom pour l’application hello. Choisissez **Oui** sous **Application web/API web**, puis choisissez **Oui** sous **Autoriser un flux implicite**. Puis hello de copie **URL de redirection** de hello **Azure Active Directory B2C** section Hello **identités** onglet dans le portail de publication hello et collez-le dans hello **URL de réponse** zone de texte.

  ![Inscrire une nouvelle application 3][api-management-howto-aad-b2c-app-details]

7. Cliquez sur hello **créer** bouton. Lorsque l’application hello est créée, elle apparaît dans hello **Applications** panneau. Cliquez sur toosee de nom d’application hello ses détails.

  ![Inscrire une nouvelle application 4][api-management-howto-aad-b2c-app-created]

8. À partir de hello **propriétés** panneau, hello de copie **ID d’Application** toohello Presse-papiers.

  ![ID d’application 1][api-management-howto-aad-b2c-app-id]

9. Basculer le portail de publication toohello précédent et collez hello ID hello **Id Client** zone de texte.

  ![ID d’application 2][api-management-howto-aad-b2c-client-id]

10. Commutateur précédent toohello portail Azure, cliquez sur hello **clés** bouton, puis cliquez sur **générer une clé**. Cliquez sur **enregistrer** hello de configuration et l’affichage de hello toosave **clé application**. Copier le Presse-papiers toohello clé hello.

  ![Clé d’application 1][api-management-howto-aad-b2c-app-key]

11. Commutateur toohello précédent portal et la coller hello clé publisher dans hello **clé secrète Client** zone de texte.

  ![Clé d’application 2][api-management-howto-aad-b2c-client-secret]

12. Spécifiez le nom de domaine hello du client hello Azure Active Directory B2C dans **autorisé le client**.

  ![Client autorisé][api-management-howto-aad-b2c-allowed-tenant]

13. Spécifiez hello **stratégie d’inscription** et **Signin stratégie**. Si vous le souhaitez, vous pouvez également fournir hello **stratégie de modification de profil** et **stratégie de réinitialisation du mot de passe**.

  ![Stratégies][api-management-howto-aad-b2c-policies]

  > [!NOTE]
  > Pour plus d’informations sur les stratégies, consultez [Azure Active Directory B2C : infrastructure de stratégie extensible].

14. Une fois que vous avez spécifié la configuration souhaitée de hello, cliquez sur **enregistrer**.

  Après avoir enregistrement les modifications de hello, les développeurs seront être toocreate en mesure de nouveaux comptes et se connecter à l’aide d’Azure Active Directory B2C toohello portail des développeurs.

## <a name="sign-up-for-a-developer-account-by-using-azure-active-directory-b2c"></a>Inscrire un compte de développeur avec Azure Active Directory B2C

1. toosign pour un compte de développeur à l’aide de B2C d’Active Directory Azure, ouvrez une nouvelle fenêtre de navigateur et accédez toohello portail des développeurs. Cliquez sur hello **inscrire** bouton.

   ![Portail des développeurs 1][api-management-howto-aad-b2c-dev-portal]

2. Cliquez sur toosign avec **Azure Active Directory B2C**.

   ![Portail des développeurs 2][api-management-howto-aad-b2c-dev-portal-b2c-button]

3. Vous êtes redirigé toohello inscription stratégie que vous avez configuré dans la section précédente de hello. Choisir toosign à l’aide de votre adresse de messagerie ou l’un de vos comptes sociaux existants.

   > [!NOTE]
   > Si Azure Active Directory B2C est hello seule option qui est activée sur hello **identités** onglet dans le portail de publication hello, vous serez redirigé toohello inscription stratégie directement.

   ![Portail des développeurs][api-management-howto-aad-b2c-dev-portal-b2c-options]

   Lors de l’inscription de hello est terminée, vous êtes redirigé toohello arrière portail des développeurs. Vous êtes désormais connecté toohello portail des développeurs pour votre instance de service de gestion des API.

    ![Référencement terminé][api-management-registration-complete]

## <a name="next-steps"></a>Étapes suivantes

*  [Vue d’ensemble d’Azure Active Directory B2C]
*  [Azure Active Directory B2C : infrastructure de stratégie extensible]
*  [Utiliser un compte Microsoft comme fournisseur d’identité dans Azure Active Directory B2C]
*  [Utiliser un compte Google comme fournisseur d’identité dans Azure Active Directory B2C]
*  [Utiliser un compte LinkedIn comme fournisseur d’identité dans Azure Active Directory B2C]
*  [Utiliser un compte Facebook comme fournisseur d’identité dans Azure Active Directory B2C]




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
