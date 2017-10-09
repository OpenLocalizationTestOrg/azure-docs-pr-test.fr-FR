---
title: "comptes de développeur aaaAuthorize à l’aide d’Azure Active Directory - gestion des API Azure | Documents Microsoft"
description: "Découvrez comment les utilisateurs de tooauthorize à l’aide d’Azure Active Directory dans la gestion des API."
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
ms.openlocfilehash: ebf5447a509a47df35e4262138bfcf423cb1dd5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-using-azure-active-directory-in-azure-api-management"></a>Comment les développeurs tooauthorize comptes à l’aide Azure Active Directory dans la gestion des API Azure
## <a name="overview"></a>Vue d'ensemble
Ce guide vous explique comment tooenable accéder au portail des développeurs toohello pour les utilisateurs d’Azure Active Directory. Ce guide vous montre également comment toomanage des groupes d’utilisateurs d’Azure Active Directory en ajoutant des groupes externes qui contiennent hello utilisateurs d’Azure Active Directory.

> les étapes toocomplete hello dans ce guide vous devez avoir un annuaire Azure Active Directory dans le toocreate une application.
> 
> 

## <a name="how-tooauthorize-developer-accounts-using-azure-active-directory"></a>Comment les développeurs tooauthorize comptes à l’aide Azure Active Directory
tooget démarré, cliquez sur **portail de publication** Bonjour portail Azure pour votre service de gestion des API. Cela vous prend un portail de publication de gestion des API toohello.

![Portail des éditeurs][api-management-management-console]

> Si vous n’avez pas encore créé une instance de service de gestion des API, consultez [de créer une instance de service de gestion des API] [ Create an API Management service instance] Bonjour [prise en main Azure API Management] [ Get started with Azure API Management] didacticiel.
> 
> 

Cliquez sur **sécurité** de hello **gestion des API** menu hello gauche et cliquez sur **les identités externes**.

![Identités externes][api-management-security-external-identities]

Cliquez sur **Azure Active Directory**. Prenez note de hello **URL de redirection** et basculer tooyour Azure Active Directory Bonjour portail classique Azure.

![Identités externes][api-management-security-aad-new]

Cliquez sur hello **ajouter** bouton toocreate une application Azure Active Directory, puis choisissez **ajouter une application développée par mon organisation**.

![Ajouter de nouvelles applications Azure Active Directory][api-management-new-aad-application-menu]

Entrez un nom pour l’application hello, sélectionnez **Web application et/ou API Web**, puis cliquez sur le bouton suivant de hello.

![Nouvelle application Azure Active Directory][api-management-new-aad-application-1]

Pour **URL de connexion**, entrez hello l’authentification sur l’URL de votre portail des développeurs. Dans cet exemple, hello **URL de connexion** est `https://aad03.portal.current.int-azure-api.net/signin`. 

Pourquoi **URL ID d’application**, entrez le domaine par défaut de hello ou un domaine personnalisé pour hello Azure Active Directory et ajouter un tooit de chaîne unique. Dans cet exemple, hello domaine par défaut de **https://contoso5api.onmicrosoft.com** est utilisé avec le suffixe hello **/API** spécifié.

![Propriétés de la nouvelle application Azure Active Directory][api-management-new-aad-application-2]

Cliquez sur toosave de bouton de vérification hello et créer l’application hello basculer toohello **configurer** onglet nouvelle application de tooconfigure hello.

![Nouvelle application Azure Active Directory créée][api-management-new-aad-app-created]

Si plusieurs annuaires Azure Active Directory vont toobe utilisée pour cette application, cliquez sur **Oui** pour **Application est mutualisée**. valeur par défaut Hello est **non**.

![Application mutualisée][api-management-aad-app-multi-tenant]

Hello de copie **URL de redirection** de hello **Azure Active Directory** section Hello **les identités externes** onglet dans le portail de publication hello et collez-le dans hello **URL de réponse** zone de texte. 

![URL de réponse][api-management-aad-reply-url]

Défiler vers le bas de hello toohello configurer onglet, sélectionnez hello **autorisations d’Application** liste déroulante, puis vérifiez **lire les données d’annuaire**.

![Autorisations de l’application][api-management-aad-app-permissions]

Sélectionnez hello **déléguer des autorisations** liste déroulante, puis vérifiez **activer l’authentification et de lire les profils utilisateurs**.

![Autorisations déléguées][api-management-aad-delegated-permissions]

> Pour plus d’informations sur l’application et des autorisations déléguées, consultez [hello d’accès à l’API Graph][Accessing hello Graph API].
> 
> 

Hello de copie **Id Client** toohello Presse-papiers.

![ID de client][api-management-aad-app-client-id]

Basculer le portail de publication toohello différé et la coller dans hello **Id Client** copiés à partir de la configuration de l’application hello Azure Active Directory.

![ID de client][api-management-client-id]

Configuration d’Azure Active Directory toohello arrière du commutateur, puis cliquez sur hello **sélectionner une durée** déroulante Bonjour **clés** section et spécifiez un intervalle. Dans cet exemple, la valeur **1 an** est utilisée.

![Clé][api-management-aad-key-before-save]

Cliquez sur **enregistrer** clé hello toosave hello configuration et l’affichage. Copier le Presse-papiers toohello clé hello.

> Notez sa valeur. Une fois que vous fermez la fenêtre de configuration d’Azure Active Directory hello, clé de hello Impossible d’afficher à nouveau.
> 
> 

![Clé][api-management-aad-key-after-save]

Commutateur toohello précédent portal et la coller hello clé publisher dans hello **clé secrète Client** zone de texte.

![Clé secrète client][api-management-client-secret]

**Autorisé locataires** spécifie les répertoires qui ont accès toohello API d’instance de service de gestion des API hello. Spécifier les domaines hello Hello toowhich d’instances Azure Active Directory vous souhaitez toogrant accéder. Vous pouvez séparer plusieurs domaines par des sauts de ligne, des espaces ou des virgules.

![Locataires autorisés][api-management-client-allowed-tenants]


Une fois hello souhaitée de configuration est spécifiée, cliquez sur **enregistrer**.

![Enregistrer][api-management-client-allowed-tenants-save]

Une fois que l’enregistrement des modifications de hello, les utilisateurs de hello Bonjour spécifiés Azure Active Directory peuvent se connecter dans le portail des développeurs toohello en suivant les étapes de hello dans [connectez-vous au portail des développeurs toohello à l’aide d’un compte Azure Active Directory] [Log in toohello Developer portal using an Azure Active Directory account].

Plusieurs domaines peuvent être spécifiés dans hello **autorisé de locataires** section. Avant de n’importe quel utilisateur peut se connecter à partir d’un autre domaine que hello d’origine où l’application hello a été enregistrée, un administrateur global de domaine différent de hello doit autoriser pour hello application tooaccess données d’annuaire. autorisation de toogrant, administrateur global de hello doit devenir trop`https://<URL of your developer portal>/aadadminconsent` (par exemple, https://contoso.portal.azure-api.net/aadadminconsent), type de nom de domaine hello Hello client Active Directory qu’ils souhaitent toogive accès tooand, cliquez sur Envoyer. Suivant de hello exemple, un administrateur global de `miaoaad.onmicrosoft.com` tente de portail de développement particulier toothis toogive autorisation. 

![Autorisations][api-management-aad-consent]

Dans l’écran suivant de hello, administrateur global de hello sera invité à tooconfirm hello si vous autorisez. 

![Autorisations][api-management-permissions-form]

> Si un administrateur non global tente toolog dans avant les autorisations sont accordées par un administrateur global, tentative de connexion hello échoue et un écran d’erreur s’affiche.
> 
> 

## <a name="how-tooadd-an-external-azure-active-directory-group"></a>Comment tooadd groupe externe Azure Active Directory
Après l’activation de l’accès pour les utilisateurs dans Azure Active Directory, vous pouvez ajouter les groupes Azure Active Directory dans la gestion des API toomore gérer facilement l’association hello de hello les développeurs hello groupe avec les produits hello souhaité.

> tooconfigure un groupe Azure Active Directory externe, hello Azure Active Directory doit d’abord être configuré dans l’onglet d’identités hello en suivant la procédure hello dans la section précédente de hello. 
> 
> 

Les groupes Azure Active Directory externes sont ajoutés à partir de hello **visibilité** onglet du produit hello pour laquelle vous souhaitez au groupe toohello toogrant accès. Cliquez sur **produits**, puis cliquez sur nom hello de produit de votre choix hello.

![Configure product][api-management-configure-product]

Commutateur toohello **visibilité** onglet, puis cliquez sur **ajouter des groupes à partir d’Azure Active Directory**.

![Ajouter des groupes][api-management-add-groups]

Sélectionnez hello **client Azure Active Directory** de liste de déroulante hello, puis hello nom de type groupe hello Bonjour **groupes** toobe ajouté la zone de texte.

![Sélectionner un groupe][api-management-select-group]

Ce nom de groupe se trouvent dans hello **groupes** liste pour Azure Active Directory, comme indiqué dans hello l’exemple suivant.

![Liste des groupes Azure Active Directory][api-management-aad-groups-list]

Cliquez sur **ajouter** toovalidate hello nom du groupe et ajouter un groupe hello. Dans cet exemple, hello **les développeurs de Contoso 5** groupe externe est ajouté. 

![Group added][api-management-aad-group-added]

Cliquez sur **enregistrer** toosave hello nouvelle sélection de groupe.

Une fois qu’un groupe Azure Active Directory a été configuré à partir d’un produit, il est disponible toobe vérifiée sur hello **visibilité** onglet hello autres produits dans l’instance de service de gestion des API hello.

tooreview et configurer les propriétés de hello pour les groupes externes une fois qu’ils ont été ajoutés, cliquez sur nom hello du groupe hello de hello **groupes** onglet.

![Gérer les groupes][api-management-groups]

À partir d’ici, vous pouvez modifier hello **nom** et hello **Description** du groupe de hello.

![Modifier un groupe][api-management-edit-group]

Les utilisateurs de hello configuré Azure Active Directory peuvent se connecter en mode et le portail des développeurs toohello et d’abonnement tooany les groupes pour lesquels ils disposent de visibilité en suivant les instructions de hello Bonjour suivant la section.

## <a name="how-toolog-in-toohello-developer-portal-using-an-azure-active-directory-account"></a>Comment toolog dans le portail des développeurs toohello à l’aide d’un compte Azure Active Directory
toolog portail des développeurs hello à l’aide d’un compte Azure Active Directory configuré dans les sections précédentes hello, ouvrez une nouvelle fenêtre de navigateur à l’aide de hello **URL de connexion** à partir de la configuration de l’application hello Active Directory, puis cliquez sur **Azure Active Directory**.

![Portail des développeurs][api-management-dev-portal-signin]

Entrez les informations d’identification hello de l’un des utilisateurs de hello dans Azure Active Directory, puis cliquez sur **connectez-vous**.

![de connexion][api-management-aad-signin]

Un formulaire d’inscription peut vous être présenté si certaines informations supplémentaires sont requises. Complétez le formulaire d’inscription de hello et cliquez sur **inscrire**.

![Inscription][api-management-complete-registration]

Votre utilisateur est maintenant connecté dans le portail des développeurs hello pour votre instance de service de gestion des API.

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

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

[Log in toohello Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account

