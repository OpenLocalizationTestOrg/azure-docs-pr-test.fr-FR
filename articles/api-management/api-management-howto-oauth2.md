---
title: "comptes de développeur aaaAuthorize à l’aide d’OAuth 2.0 dans Gestion des API Azure | Documents Microsoft"
description: "Découvrez comment les utilisateurs de tooauthorize à l’aide d’OAuth 2.0 dans Gestion des API."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 78c48247-64f0-4708-b2d0-98b61a821283
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 934901dd6df399470a3257bf7a3a9b9fb5f40d5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-using-oauth-20-in-azure-api-management"></a>Comment les développeurs tooauthorize comptes à l’aide OAuth 2.0 dans Gestion des API Azure
Prend en charge de nombreuses API [OAuth 2.0](http://oauth.net/2/) toosecure hello API et garantir que seuls les utilisateurs autorisés ont accès, et ils peuvent accéder uniquement aux ressources toowhich auxquelles ils ont droit. Dans interactive Console de commande toouse Azure API Management de développement avec ces API, hello service vous permet de tooconfigure votre toowork d’instance de service avec votre OAuth 2.0 activé API.

## <a name="prerequisites"></a>Configuration requise
Ce guide vous montre comment tooconfigure votre toouse instance du service Gestion des API d’autorisation d’OAuth 2.0 pour développeur comptes, mais ne pas vous montre comment le fournisseur de tooconfigure un OAuth 2.0. configuration de Hello pour chaque fournisseur est différent, même si hello étapes sont semblables, et nombre hello requis d’informations de configuration d’OAuth 2.0 dans votre instance de service de gestion des API de OAuth 2.0 hello identiques. Cette rubrique inclut des exemples d'utilisation de Azure Active Directory en tant que fournisseur OAuth 2.0.

> [!NOTE]
> Pour plus d’informations sur la configuration d’OAuth 2.0 à l’aide d’Azure Active Directory, consultez hello [WebApp-GraphAPI-DotNet] [ WebApp-GraphAPI-DotNet] exemple.
> 
> 

## <a name="step1"></a>Configuration du serveur d’autorisation OAuth 2.0 dans Gestion des API
tooget démarré, cliquez sur **portail de publication** Bonjour portail Azure pour votre service de gestion des API.

![Portail des éditeurs][api-management-management-console]

> [!NOTE]
> Si vous n’avez pas encore créé une instance de service de gestion des API, consultez [de créer une instance de service de gestion des API] [ Create an API Management service instance] Bonjour [prise en main Azure API Management] [ Get started with Azure API Management] didacticiel.
> 
> 

Cliquez sur **sécurité** de hello **gestion des API** menu de gauche, cliquez sur à hello **OAuth 2.0**, puis cliquez sur **ajouter un serveur d’autorisation**.

![OAuth 2.0][api-management-oauth2]

Après avoir cliqué sur **ajouter un serveur d’autorisation**, nouveau formulaire de serveur d’autorisation hello s’affiche.

![Nouveau serveur][api-management-oauth2-server-1]

Entrez un nom et une description facultative dans hello **nom** et **Description** champs. 

> [!NOTE]
> Ces champs sont le serveur de d’autorisation hello OAuth 2.0 tooidentify utilisés au sein de l’instance de service de gestion des API actuelle hello et leurs valeurs ne proviennent pas de serveur de hello OAuth 2.0.
> 
> 

Entrez hello **URL de la page d’inscription Client**. Cette page est où les utilisateurs peuvent créer et gérer leurs comptes et varie en fonction du fournisseur de hello OAuth 2.0. Hello **URL de la page d’inscription Client** points toohello page que les utilisateurs peuvent utiliser toocreate et configurer leurs propres comptes pour les fournisseurs OAuth 2.0 qui prennent en charge la gestion des comptes d’utilisateur. Certaines organisations ne configurer ou utiliser cette fonctionnalité, même si le fournisseur de hello OAuth 2.0 prend en charge. Si votre fournisseur OAuth 2.0 n’a pas de gestion des utilisateurs de comptes configurés, entrez une URL d’espace réservé en ici, par exemple hello URL de votre société, ou comme `https://placeholder.contoso.com`.

section suivante de Hello sous forme de hello contient hello **types d’octroi de code d’autorisation**, **URL de point de terminaison d’autorisation**, et **méthode de demande d’autorisation** paramètres.

![Nouveau serveur][api-management-oauth2-server-2]

Spécifiez hello **types d’octroi de code d’autorisation** en vérifiant les types hello souhaité. **code d'autorisation** est spécifié par défaut.

Entrez hello **URL de point de terminaison d’autorisation**. Pour Azure Active Directory, cette URL sera similaire toohello suivant URL, où `<client_id>` est remplacée par l’id de client hello qui identifie votre serveur d’applications toohello OAuth 2.0.

`https://login.microsoftonline.com/<client_id>/oauth2/authorize`

Hello **méthode de demande d’autorisation** spécifie comment la demande d’autorisation de hello est envoyée toohello OAuth 2.0 server. Par défaut, la méthode **GET** est sélectionnée.

la section suivante Hello est où hello **URL de point de terminaison de jeton**, **méthodes d’authentification Client**, **jeton d’accès méthode d’envoi**, et **étenduepardéfaut** sont spécifiés.

![Nouveau serveur][api-management-oauth2-server-3]

Pour un serveur Azure Active Directory OAuth 2.0, hello **URL de point de terminaison de jeton** aura hello suivant le format, où `<APPID>` a le format hello de `yourapp.onmicrosoft.com`.

`https://login.microsoftonline.com/<APPID>/oauth2/token`

Hello du paramètre par défaut pour **méthodes d’authentification Client** est **base**, et **jeton d’accès méthode d’envoi** est **l’en-tête d’autorisation**. Ces valeurs sont configurés sur cette section du formulaire hello, ainsi que de hello **étendue par défaut**.

Hello **informations d’identification Client** section contient hello **ID Client** et **clé secrète Client**, qui sont obtenu au cours hello les processus de création et la configuration de votre OAuth 2.0 serveur. Une fois hello **ID Client** et **clé secrète Client** sont spécifiés, hello **redirect_uri** pour hello **code d’autorisation** est généré. Cet URI est l’URL de réponse hello tooconfigure utilisés dans votre configuration de serveur OAuth 2.0.

![Nouveau serveur][api-management-oauth2-server-4]

Si **types d’octroi de code d’autorisation** est défini trop**mot de passe de propriétaire de la ressource**, hello **informations d’identification de mot de passe de propriétaire de la ressource** section est toospecify utilisé les informations d’identification ; Sinon, vous pouvez laisser vide.

![Nouveau serveur][api-management-oauth2-server-5]

Une fois le formulaire de hello est terminée, cliquez sur **enregistrer** configuration du serveur d’autorisation toosave hello API Management OAuth 2.0. Une fois la configuration du serveur hello est enregistrée, vous pouvez configurer API toouse cette configuration, comme indiqué dans la section suivante de hello.

## <a name="step2"></a>Configurer un toouse API autorisation de l’utilisateur OAuth 2.0
Cliquez sur **API** de hello **gestion des API** hello menu gauche, cliquez sur nom hello de hello souhaité API **sécurité**, puis activez case hello pour **OAuth 2.0**.

![Autorisation utilisateur][api-management-user-authorization]

Sélectionnez hello souhaité **serveur d’autorisation** à partir de la liste déroulante de hello, puis cliquez sur **enregistrer**.

![Autorisation utilisateur][api-management-user-authorization-save]

## <a name="step3"></a>Tester l’autorisation de l’utilisateur hello OAuth 2.0 Bonjour portail des développeurs
Après avoir configuré votre serveur d’autorisation OAuth 2.0 et configuré votre toouse API ce serveur, vous pouvez le tester en accédant toohello portail des développeurs et en appelant une API.  Cliquez sur **portail des développeurs** dans le menu supérieur droit de hello.

![Portail des développeurs][api-management-developer-portal-menu]

Cliquez sur **API** dans le menu du haut hello et sélectionnez **Echo API**.

![API Echo][api-management-apis-echo-api]

> [!NOTE]
> Si vous n'avez qu’une seule API configurée ou tooyour visible compte, puis en cliquant sur API vous amène directement operations toohello pour cette API.
> 
> 

Sélectionnez hello **obtenir une ressource** opération, cliquez sur **ouvrir la Console**, puis sélectionnez **code d’autorisation** dans hello de liste déroulante.

![Open console][api-management-open-console]

Lorsque **code d’autorisation** est sélectionnée, une fenêtre contextuelle s’affiche avec hello-formulaire de connexion du fournisseur de hello OAuth 2.0. Dans cet exemple hello-formulaire de connexion est fournie par Azure Active Directory.

> [!NOTE]
> Si vous avez les fenêtres contextuelles désactivée, vous serez invité à entrer tooenable par le navigateur de hello. Une fois que vous les activez, sélectionnez **code d’autorisation** hello et nouveau formulaire de connexion s’affichera.
> 
> 

![de connexion][api-management-oauth2-signin]

Une fois que vous êtes connecté, hello **en-têtes de demande** sont renseignées avec une `Authorization : Bearer` en-tête qui autorise la demande de hello.

![Jeton d'en-tête de demande][api-management-request-header-token]

À ce stade, vous pouvez configurer les valeurs hello souhaité pour hello restant de paramètres et soumettre la demande de hello. 

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur l’utilisation de OAuth 2.0 et gestion des API, voir hello vidéo et d’accompagnement [article](api-management-howto-protect-backend-with-aad.md).

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-oauth2/api-management-management-console.png
[api-management-oauth2]: ./media/api-management-howto-oauth2/api-management-oauth2.png
[api-management-user-authorization]: ./media/api-management-howto-oauth2/api-management-user-authorization.png
[api-management-user-authorization-save]: ./media/api-management-howto-oauth2/api-management-user-authorization-save.png
[api-management-oauth2-signin]: ./media/api-management-howto-oauth2/api-management-oauth2-signin.png
[api-management-request-header-token]: ./media/api-management-howto-oauth2/api-management-request-header-token.png
[api-management-developer-portal-menu]: ./media/api-management-howto-oauth2/api-management-developer-portal-menu.png
[api-management-open-console]: ./media/api-management-howto-oauth2/api-management-open-console.png
[api-management-oauth2-server-1]: ./media/api-management-howto-oauth2/api-management-oauth2-server-1.png
[api-management-oauth2-server-2]: ./media/api-management-howto-oauth2/api-management-oauth2-server-2.png
[api-management-oauth2-server-3]: ./media/api-management-howto-oauth2/api-management-oauth2-server-3.png
[api-management-oauth2-server-4]: ./media/api-management-howto-oauth2/api-management-oauth2-server-4.png
[api-management-oauth2-server-5]: ./media/api-management-howto-oauth2/api-management-oauth2-server-5.png
[api-management-apis-echo-api]: ./media/api-management-howto-oauth2/api-management-apis-echo-api.png


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

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

