---
title: "aaaAzure glossaire de développeur Active Directory | Documents Microsoft"
description: "Liste de termes liés aux concepts et fonctionnalités de développeur Azure Active Directory couramment utilisés."
services: active-directory
documentationcenter: 
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 551512df-46fb-4219-a14b-9c9fc23998ba
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 32a6a6194b8d01409159a2b60263bb66a87a843c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-developer-glossary"></a>Glossaire du développeur Azure Active Directory
Cet article contient les définitions de certains des concepts de développement Azure Active Directory (AD) hello core, sont utiles lorsque vous apprenez à développer des applications pour Azure AD.

## <a name="access-token"></a>access token
Un type de [jeton de sécurité](#security-token) émis par une [serveur d’autorisation](#authorization-server)et utilisé par un [application cliente](#client-application) dans l’ordre tooaccess un [ressource serveur protégé ](#resource-server). En général sous forme de hello d’un [JSON Web Token (JWT)][JWT], jeton de hello personnifie autorisation hello bénéficie toohello client hello [propriétaire de la ressource](#resource-owner), pour un niveau demandé d’accès. Hello jeton contient tous les applicable [revendications](#claim) sur le sujet de hello, l’activation de hello client application toouse sous la forme d’un formulaire d’informations d’identification lorsqu’ils accèdent à une ressource donnée. Cela élimine également besoin hello client toohello des informations d’identification de tooexpose hello ressource propriétaire.

Les jetons d’accès sont parfois tooas référencé « Utilisateur + App » ou « Application uniquement », en fonction de hello les informations d’identification qui est représenté. Par exemple, lorsqu’une application cliente utilise :

* [Octroi d’autorisation de « Code d’autorisation »](#authorization-grant), hello utilisateur s’authentifie tout d’abord en tant que propriétaire de la ressource hello, la délégation d’autorisation toohello client tooaccess hello ressource. Hello client authentifie par la suite lors de l’obtention du jeton d’accès hello. Hello jeton peut parfois être référencé toomore précisément comme un jeton « Utilisateur + App », car il représente les deux utilisateur hello autorisé hello client d’application hello.
* [Octroi d’autorisation de « Informations d’identification du client »](#authorization-grant), client de hello fournit une authentification unique hello, fonctionne sans d’authentification/autorisation hello-du propriétaire des ressources, donc le jeton de hello peut parfois être tooas auxquels un jeton « Application uniquement ».

Pour plus d’informations, consultez [Azure AD Token Reference (Référence de jeton Azure AD)][AAD-Tokens-Claims].

## <a name="application-manifest"></a>manifeste d’application
Une fonctionnalité fournie par hello [portail Azure][AZURE-portal], ce qui donne une représentation JSON de configuration d’identité de l’application hello, utilisée comme un mécanisme de mise à jour qui lui est associée [ Application] [ AAD-Graph-App-Entity] et [ServicePrincipal] [ AAD-Graph-Sp-Entity] entités. Consultez [manifeste d’application Azure Active Directory compréhension hello] [ AAD-App-Manifest] pour plus d’informations.

## <a name="application-object"></a>objet application
Lorsque vous inscrire/mettre à jour une application Bonjour [portail Azure][AZURE-portal], portail de hello créations/mises à jour à la fois un objet d’application et une [objet principal de service](#service-principal-object)pour ce client. objet de l’application Hello *définit* hello configuration d’identité de l’application global (sur tous les locataires dans lequel il a accès), en fournissant un modèle à partir de laquelle sont ses objets de principal de service correspondant  *dérivés* à utiliser localement au moment de l’exécution (dans un client spécifique).

Pour plus d’informations, consultez [Application and Service Principal Objects (Objets application et principaux du service)][AAD-App-SP-Objects].

## <a name="application-registration"></a>inscription d’application
Dans commande tooallow une toointegrate application avec et le délégué tooAzure de fonctions de gestion des identités et l’accès AD, il doit être inscrit auprès d’un Azure AD [client](#tenant). Lorsque vous inscrivez votre application auprès d’Azure AD, vous fournissez une configuration d’identité pour votre application, ce qui permet de toointegrate avec Azure AD et utiliser des fonctionnalités telles que :

* Gestion robuste de l’authentification unique à l’aide de la gestion d’Azure AD Identity Management et de l’implémentation du protocole [OpenID Connect][OpenIDConnect] ;
* Répartie accès trop[des ressources protégées](#resource-server) par [les applications clientes](#client-application), par le biais OAuth 2.0 d’Azure AD [serveur d’autorisation](#authorization-server) implémentation
* [Infrastructure de consentement](#consent) pour la gestion des ressources de tooprotected accès client, en fonction de l’autorisation de propriétaire de la ressource.

Pour plus d’informations, consultez [Integrating applications with Azure Active Directory (Intégration d’applications dans Azure Active Directory)][AAD-Integrating-Apps].

## <a name="authentication"></a>authentication
Hello consistant à une partie des informations d’identification légitimes, en fournissant de la base de hello pour la création d’un toobe de principal de sécurité utilisé pour l’identité et contrôle d’accès se révéler difficile. Pendant une [OAuth2 d’octroi de](#authorization-grant) , par exemple, les tiers hello l’authentification se remplit rôle hello du [propriétaire de la ressource](#resource-owner) ou [application cliente](#client-application), en fonction de grant Hello utilisé.

## <a name="authorization"></a>autorisation
act Hello d’octroi d’une toodo autorisation principal de sécurité authentifié quelque chose. Il existe deux cas d’utilisation principal dans le modèle de programmation hello Azure AD :

* Pendant une [OAuth2 d’octroi de](#authorization-grant) flux : hello lorsque [propriétaire de la ressource](#resource-owner) accorde l’autorisation toohello [application cliente](#client-application), ce qui permet de client de hello tooaccess hello ressources du propriétaire des ressources.
* Lors de l’accès aux ressources par le client de hello : implémenté par hello [serveur de ressources](#resource-server), à l’aide de hello [revendication](#claim) valeurs présentes dans hello [jeton d’accès](#access-token) toomake le contrôle d’accès en vous basant sur elles.

## <a name="authorization-code"></a>code d’autorisation
Une courte durée de vie « token » fourni tooa [application cliente](#client-application) par hello [point de terminaison d’autorisation](#authorization-endpoint), dans le cadre du flux de « code d’autorisation » hello, un des hello OAuth2 quatre [d’autorisation accorde ](#authorization-grant). code de Hello est retourné application cliente de toohello dans tooauthentication de réponse d’un [propriétaire de la ressource](#resource-owner), indiquant le propriétaire de la ressource hello a délégué hello de tooaccess d’autorisation des ressources demandées. Dans le cadre du flux de hello, le code de hello est plus tard échangé pour une [jeton d’accès](#access-token).

## <a name="authorization-endpoint"></a>point de terminaison d’autorisation
Un des points de terminaison hello implémentées par hello [serveur d’autorisation](#authorization-server), utilisé toointeract avec hello [propriétaire de la ressource](#resource-owner) dans l’ordre tooprovide un [octroi d’autorisation](#authorization-grant) pendant un flux d’octroi d’autorisation OAuth2. En fonction de l’autorisation de hello flux d’octroi utilisé, hello réel grant fournie peut varier, y compris un [code d’autorisation](#authorization-code) ou [jeton de sécurité](#security-token).

Consultez la spécification hello OAuth2 [types accorder l’autorisation] [ OAuth2-AuthZ-Grant-Types] et [point de terminaison d’autorisation] [ OAuth2-AuthZ-Endpoint] sections et hello [OpenIDConnect spécification] [ OpenIDConnect-AuthZ-Endpoint] pour plus d’informations.

## <a name="authorization-grant"></a>octroi d’autorisation
Informations d’identification représentant hello [du propriétaire des ressources](#resource-owner) [autorisation](#authorization) tooaccess ses ressources protégées, accordés tooa [application cliente](#client-application). Une application cliente peut utiliser un des hello [quatre accorder les types définis par hello OAuth2 Authorization Framework] [ OAuth2-AuthZ-Grant-Types] tooobtain une instruction grant, selon le type de client/configuration requise : « octroi d’un code d’autorisation, » » accorder des informations d’identification du client », « implicit grant » et « transmission des informations d’identification de mot de passe de propriétaire de la ressource ». informations d’identification Hello retourné toohello client est un [jeton d’accès](#access-token), ou un [code d’autorisation](#authorization-code) (échangés ultérieurement pour un jeton d’accès), en fonction de type hello d’octroi d’autorisation utilisé.

## <a name="authorization-server"></a>serveur d’autorisation
Comme défini par hello [OAuth2 Authorization Framework][OAuth2-Role-Def], serveur hello responsable de l’émission d’accès jetons toohello [client](#client-application) après une authentification réussie Hello [propriétaire de la ressource](#resource-owner) et l’obtention de l’autorisation. A [application cliente](#client-application) interagit avec le serveur d’autorisation de hello lors de l’exécution via sa [autorisation](#authorization-endpoint) et [jeton](#token-endpoint) points de terminaison, conformément aux hello OAuth2 défini [d’autorisation accorde](#authorization-grant).

Dans le cas de hello d’intégration d’application Azure AD, Azure AD implémente rôle de serveur d’autorisation hello pour les applications Azure AD et le service Microsoft API, par exemple [Microsoft Graph API][Microsoft-Graph].

## <a name="claim"></a>revendication
A [jeton de sécurité](#security-token) contient les revendications, qui fournissent des assertions sur une seule entité (comme un [application cliente](#client-application) ou [propriétaire de la ressource](#resource-owner)) entité tooanother (par exemple hello [serveur de ressources](#resource-server)). Les revendications sont des paires nom/valeur qui faits relatifs à l’objet du jeton hello de relais (par exemple, hello entité de sécurité a été authentifiée par hello [serveur d’autorisation](#authorization-server)). Hello revendications présentes dans un jeton donné sont dépendantes de plusieurs variables, y compris de type hello de jeton, de type hello des informations d’identification utilisées tooauthenticate hello sujet, configuration de l’application hello, etc..

Pour plus d’informations, consultez [Azure AD token reference (Référence de jeton Azure AD)][AAD-Tokens-Claims].

## <a name="client-application"></a>d’application cliente
Comme défini par hello [OAuth2 Authorization Framework][OAuth2-Role-Def], une application qui rend protégé par des demandes de ressources pour le compte hello [propriétaire de la ressource](#resource-owner). le terme Hello « client » n’implique pas des caractéristiques de mise en œuvre matérielle particulière (par exemple, si de l’application hello s’exécute sur un serveur, d’un ordinateur de bureau ou d’autres périphériques).  

Une application cliente demande [autorisation](#authorization) à partir d’un tooparticipate du propriétaire de la ressource dans un [OAuth2 d’octroi de](#authorization-grant) flux et peut accéder aux données de l’API/procuration du propriétaire des ressources hello. Hello OAuth2 Authorization Framework [définit deux types de clients][OAuth2-Client-Types], « confidentiel » et « public », en fonction de la confidentialité du client hello capacité toomaintain hello de ses informations d’identification. Les applications peuvent implémenter un [client web (confidentiel)](#web-client) s’exécutant sur un serveur web, un [client natif (public)](#native-client) installé sur un appareil ou un [client basé sur un agent utilisateur (public)](#user-agent-based-client) s’exécutant dans le navigateur d’un appareil.

## <a name="consent"></a>consentement
Hello du processus d’un [propriétaire de la ressource](#resource-owner) l’octroi d’autorisation tooa [application cliente](#client-application), tooaccess protégé des ressources spécifiques [autorisations](#permissions), pour le compte hello propriétaire de la ressource. En fonction des autorisations hello demandées par le client de hello, un administrateur ou un utilisateur sera invité à entrer données organisation/individuels de consentement tooallow access tootheir respectivement. Notez que, dans un [mutualisée](#multi-tenant-application) scénario, l’application hello [principal du service](#service-principal-object) est également enregistrée dans le locataire hello d’utilisateur de terme autorisation hello.

## <a name="id-token"></a>Jeton d’ID
Un [OpenID Connect] [ OpenIDConnect-ID-Token] [jeton de sécurité](#security-token) fournie par un [du serveur d’autorisation](#authorization-server) [point de terminaison d’autorisation](#authorization-endpoint), qui contient [revendications](#claim) correspondantes toohello l’authentification de l’utilisateur final [propriétaire de la ressource](#resource-owner). Comme un jeton d’accès, un jeton d’ID est représenté sous forme de jeton [JSON Web Token (JWT)][JWT] signé numériquement. Contrairement à un jeton d’accès, les revendications d’un jeton d’ID ne servent pas pour l’accès à des fins tooresource connexes et spécifiquement le contrôle d’accès.

Pour plus d’informations, consultez [Azure AD token reference (Référence de jeton Azure AD)][AAD-Tokens-Claims].

## <a name="multi-tenant-application"></a>application mutualisée
Une classe d’application qui permet de se connecter et [consentement](#consent) par les utilisateurs configurés dans n’importe quel Azure AD [client](#tenant), y compris les locataires que hello où le client de hello est inscrit. [Native client](#native-client) mutualisées par défaut, les applications sont alors que [client web](#web-client) et [web API des ressources](#resource-server) applications ont tooselect de capacité hello entre unique ou mutualisée. En revanche, une application web inscrit en tant que locataire unique, permet uniquement les connexions depuis des comptes d’utilisateur configurés dans hello même locataire en tant que hello une où l’application hello est inscrit.

Consultez [comment toosign dans n’importe quel utilisateur Azure AD à l’aide hello modèle d’application de l’architecture mutualisée] [ AAD-Multi-Tenant-Overview] pour plus d’informations.

## <a name="native-client"></a>client natif
Type d’ [application cliente](#client-application) installé en mode natif sur un appareil. Étant donné que tout le code est exécuté sur un appareil, il est considéré comme un client « public » en raison de tooits incapacité toostore informations d’identification en privé/confidentielle. Pour plus d’informations, consultez les [types et profils de clients OAuth2][OAuth2-Client-Types].

## <a name="permissions"></a>Autorisations
A [application cliente](#client-application) accède tooa [serveur de ressources](#resource-server) en déclarant des demandes d’autorisation. Deux types sont disponibles :

* « Délégué » les autorisations, spécifient [étendue](#scopes) à l’aide de l’accès délégué autorisation hello connecté [propriétaire de la ressource](#resource-owner), sont présentées toohello ressource au moment de l’exécution en tant que [« scp « revendications](#claim) dans du client hello [jeton d’accès](#access-token).
* Les autorisations « Application », qui spécifient [en fonction du rôle](#roles) accéder à l’aide des informations d’identification d’ou l’identité l’application hello client, sont présentées toohello ressource au moment de l’exécution en tant que [les revendications « rôles »](#claim) Bonjour jeton d’accès du client.

Ils surface également pendant hello [consentement](#consent) processus, en accordant l’administrateur de hello ressource propriétaire hello opportunité toogrant/deny hello client accès tooresources dans leur locataire.

Demandes d’autorisations sont configurées sur hello « Applications » / « Paramètres » onglet hello [portail Azure][AZURE-portal], sous « Autorisations requises », en sélectionnant hello souhaité « Autorisations déléguées » et » Autorisations d’application » (hello cette dernière nécessite l’appartenance au rôle d’administrateur général hello). Car un [client public](#client-application) ne peut pas mettre à jour en toute sécurité les informations d’identification, elle peut seulement demander des autorisations déléguées, pendant un [client confidentiel](#client-application) a hello capacité toorequest déléguée et application autorisations. client Hello [objet application](#application-object) hello magasins déclarées autorisations dans son [requiredResourceAccess propriété][AAD-Graph-App-Entity].

## <a name="resource-owner"></a>propriétaire de la ressource
Comme défini par hello [OAuth2 Authorization Framework][OAuth2-Role-Def], une entité capable d’octroi d’accès tooa une ressource protégée. Lorsque le propriétaire de la ressource hello est une personne, il est tooas auxquels un utilisateur final. Par exemple, quand un [application cliente](#client-application) veut tooaccess boîte aux lettres d’un utilisateur via hello [Microsoft Graph API][Microsoft-Graph], elle nécessite l’autorisation de propriétaire de la ressource de hello boîte aux lettres de Hello.

## <a name="resource-server"></a>serveur de ressources
Comme défini par hello [OAuth2 Authorization Framework][OAuth2-Role-Def], un serveur que les hôtes des ressources protégées, capables d’accepte et répond tooprotected ressource demande par [client applications](#client-application) qui présente une [jeton d’accès](#access-token). Également appelé serveur de ressources protégées ou application de ressources.

Un serveur de ressources expose les API et met en œuvre d’accéder aux ressources de tooits protégé via [étendues](#scopes) et [rôles](#roles), à l’aide de hello OAuth 2.0 Authorization Framework. Exemples d’API d’Azure AD Graph hello qui fournit des accès aux données de client tooAzure AD et hello API Office 365 qui fournissent des toodata d’accès telles que la messagerie et de calendrier. Ces deux éléments sont également accessibles via hello [Microsoft Graph API][Microsoft-Graph].  

Tout comme une application cliente, la configuration d’identité de l’application de ressource est établie [inscription](#application-registration) dans un locataire Azure AD, en fournissant l’application hello et objet principal de service. Certaines API fournie par Microsoft, par exemple hello API Azure AD Graph, avoir pré-enregistré principaux de service mis à disposition dans tous les clients lors de la configuration.

## <a name="roles"></a>roles
Comme [étendues](#scopes), les rôles fournissent un moyen pour un [serveur de ressources](#resource-server) toogovern accès tooits des ressources protégées. Il existe deux types : un rôle « user » implémente le contrôle d’accès basé sur un rôle pour les utilisateurs/groupes qui nécessitent l’accès toohello ressource, tandis que d’un rôle de « application » implémente hello même pour [les applications clientes](#client-application) qui requièrent l’accès.

Les rôles sont des chaînes de ressource définie (par exemple « approbateur dépenses, » « En lecture seule », « Directory.ReadWrite.All »), et géré dans hello [portail Azure] [ AZURE-portal] par le biais de la ressource hello [application manifeste](#application-manifest)et stockées dans la ressource hello [appRoles propriété][AAD-Graph-Sp-Entity]. Hello portail Azure est également utilisé tooassign utilisateurs trop les rôles « user » et la configuration client [autorisations d’application](#permissions) tooaccess un rôle de « application ».

Pour obtenir une présentation détaillée des rôles d’application hello exposées par l’API d’Azure AD Graph, consultez [étendues d’autorisation Graph API][AAD-Graph-Perm-Scopes]. Pour un exemple d’implémentation étape par étape, consultez [Role based access control in cloud applications using Azure AD (Contrôle d’accès en fonction du rôle basé dans les applications cloud à l’aide d’Azure AD)][Duyshant-Role-Blog].

## <a name="scopes"></a>étendues
Comme [rôles](#roles), étendues offrent un moyen d’un [serveur de ressources](#resource-server) toogovern accès tooits des ressources protégées. Étendues sont utilisée tooimplement [étendue] [ OAuth2-Access-Token-Scopes] contrôle d’accès, pour un [application cliente](#client-application) qui a reçu l’accès délégué toohello ressource par son propriétaire.

Étendues sont définis sur les ressources des chaînes (par exemple « Mail.Read », « Directory.ReadWrite.All »), gérés dans hello [portail Azure] [ AZURE-portal] par le biais de la ressource hello [manifeste d’application](#application-manifest)et stockées dans la ressource hello [oauth2Permissions propriété][AAD-Graph-Sp-Entity]. Hello portail Azure est également utilisé tooconfigure application cliente [autorisations déléguées](#permissions) tooaccess une étendue.

Une convention de dénomination meilleure pratique, est toouse un format « ressource.opération.contrainte ». Pour obtenir une présentation détaillée des étendues hello exposées par l’API d’Azure AD Graph, consultez [étendues d’autorisation Graph API][AAD-Graph-Perm-Scopes]. Pour les portées exposées par les services Office 365, consultez [Office 365 API permissions reference (Référence sur les autorisations des API Office 365)][O365-Perm-Ref].

## <a name="security-token"></a>jeton de sécurité
Document signé contenant des revendications, tel qu’un jeton OAuth2 ou une assertion SAML 2.0. Pour un [octroi d’autorisation](#authorization-grant) OAuth2, un [jeton d’accès](#access-token) (OAuth2) et un [jeton d’ID](http://openid.net/specs/openid-connect-core-1_0.html#IDToken) sont des types de jetons de sécurité, qui sont tous deux implémentés sous forme de jetons [JSON Web Token (JWT)][JWT].

## <a name="service-principal-object"></a>objet principal du service
Lorsque vous inscrire/mettre à jour une application Bonjour [portail Azure][AZURE-portal], portail de hello créations/mises à jour à la fois un [objet application](#application-object) et un principal de service correspondant objet pour ce client. objet de l’application Hello *définit* hello configuration d’identité de l’application globale (entre tous les locataires où application hello associé a été accordée l’accès), et est le modèle hello à partir de laquelle son service correspondant objets principales sont *dérivée* à utiliser localement au moment de l’exécution (dans un client spécifique).

Pour plus d’informations, consultez [Application and Service Principal Objects (Objets application et principaux du service)][AAD-App-SP-Objects].

## <a name="sign-in"></a>connexion
Hello du processus d’un [application cliente](#client-application) lance authentification de l’utilisateur final et la capture liées état, à des fins de hello d’acquisition d’un [jeton de sécurité](#security-token) et la portée hello application session toothat état. L’état peut inclure des artefacts tels que les informations de profil utilisateur et des informations dérivées des revendications de jeton.

fonction Hello d’authentification d’une application est généralement utilisé tooimplement single-sign-on (SSO). Il peut également être précédé d’une fonction « inscription », en tant que point d’entrée hello pour une utilisateur final toogain accès tooan application (lors de la première connexion de). Hello fonction d’inscription est utilisé toogather et conserver l’état supplémentaires l’utilisateur toohello spécifique et peut nécessiter [consentement de l’utilisateur](#consent).

## <a name="sign-out"></a>déconnexion
Hello processus d’authentification non à un utilisateur final, le détachement de l’état utilisateur hello associé hello [application cliente](#client-application) session pendant [connectez-vous](#sign-in)

## <a name="tenant"></a>locataire
Une instance d’un annuaire Azure AD est tooas auxquels un client Azure AD. Elle offre une multitude de fonctionnalités, notamment :

* un service de registre pour les applications intégrées
* l’authentification des comptes utilisateurs et des applications enregistrées
* Points de terminaison REST requis toosupport différents protocoles, y compris OAuth2 et SAML, y compris hello [point de terminaison d’autorisation](#authorization-endpoint), [point de terminaison de jeton](#token-endpoint) et hello du point de terminaison « commune » utilisé par [ applications mutualisées](#multi-tenant-application).

Un locataire est également associé à un répertoire Azure AD ou abonnement Office 365 lors de la configuration de l’abonnement hello, fournissant des fonctionnalités d’identité et gestion des accès pour l’abonnement de hello. Consultez [comment tooget Azure Active Directory locataire] [ AAD-How-To-Tenant] pour plus d’informations sur hello de différentes façons d’obtenir tooa d’accès client. Consultez [les abonnements Azure sont associés à Azure Active Directory] [ AAD-How-Subscriptions-Assoc] pour plus d’informations sur la relation hello entre les abonnements et un locataire Azure AD.

## <a name="token-endpoint"></a>point de terminaison de jeton
Un des points de terminaison hello implémentées par hello [serveur d’autorisation](#authorization-server) toosupport OAuth2 [d’autorisation accorde](#authorization-grant). En fonction de l’instruction grant de hello, il peut être utilisé tooacquire un [jeton d’accès](#access-token) (et associés jeton « Actualiser ») tooa [client](#client-application), ou [le jeton d’ID](#ID-token) lorsqu’il est utilisé avec hello [ OpenID Connect] [ OpenIDConnect] protocole.

## <a name="user-agent-based-client"></a>Client basé sur un agent utilisateur
Type [d’application cliente](#client-application) qui télécharge du code depuis un serveur web et s’exécute au sein d’un agent utilisateur (par exemple, un navigateur web), telle qu’une application à page unique (SPA). Étant donné que tout le code est exécuté sur un appareil, il est considéré comme un client « public » en raison de tooits incapacité toostore informations d’identification en privé/confidentielle. Pour plus d’informations, consultez les [types et profils de clients OAuth2][OAuth2-Client-Types].

## <a name="user-principal"></a>principal de l’utilisateur
Toohello comme un objet principal de service est utilisé toorepresent une instance d’application, un objet principal d’utilisateur est un autre type d’entité de sécurité, qui représente un utilisateur. Bonjour Azure AD Graph [entité utilisateur] [ AAD-Graph-User-Entity] définit le schéma hello pour un objet utilisateur, y compris les relatifs à l’utilisateur des propriétés telles que le nom et prénom, nom d’utilisateur principal, l’appartenance au rôle de répertoire, etc.. Cela fournit la configuration de l’identité utilisateur hello pour Azure AD tooestablish un utilisateur principal au moment de l’exécution. Bonjour principal de l’utilisateur est utilisé toorepresent un utilisateur authentifié pour Single Sign-On, l’enregistrement des [consentement](#consent) délégation, qui effectue les décisions du contrôle d’accès, etc..

## <a name="web-client"></a>clientes web
Un type de [application cliente](#client-application) qui exécute tout le code sur un serveur web et en mesure de toofunction en tant que « confidentiel » client stocker ses informations d’identification de façon sécurisée sur le serveur de hello. Pour plus d’informations, consultez les [types et profils de clients OAuth2][OAuth2-Client-Types].

## <a name="next-steps"></a>Étapes suivantes
Hello [Guide du développeur Azure AD] [ AAD-Dev-Guide] est toouse de portail hello pour le développement de Azure AD tous les rubriques, y compris une vue d’ensemble de connexes [intégration d’application] [ AAD-How-To-Integrate] et concepts hello de [d’authentification Azure AD et les scénarios d’authentification pris en charge][AAD-Auth-Scenarios].

Utilisez hello suivant tooprovide des commentaires de la section commentaires et nous aider à affiner et mettre en forme notre contenu, y compris les demandes de nouvelles définitions ou mise à jour existantes.

<!--Image references-->

<!--Reference style links -->
[AAD-App-Manifest]: ./active-directory-application-manifest.md
[AAD-App-SP-Objects]: ./active-directory-application-objects.md
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Graph-Perm-Scopes]: https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-graph-api-permission-scopes
[AAD-Graph-App-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[AAD-Graph-Sp-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity
[AAD-Graph-User-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity
[AAD-How-Subscriptions-Assoc]: ../active-directory-how-subscriptions-associated-directory.md
[AAD-How-To-Integrate]: ./active-directory-how-to-integrate.md
[AAD-How-To-Tenant]: active-directory-howto-tenant.md
[AAD-Integrating-Apps]: ./active-directory-integrating-applications.md
[AAD-Multi-Tenant-Overview]: active-directory-devhowto-multi-tenant-overview.md
[AAD-Security-Token-Claims]: ./active-directory-authentication-scenarios/#claims-in-azure-ad-security-tokens
[AAD-Tokens-Claims]: ./active-directory-token-and-claims.md
[AZURE-portal]: https://portal.azure.com
[Duyshant-Role-Blog]: http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/
[JWT]: https://tools.ietf.org/html/draft-ietf-oauth-json-web-token-32
[Microsoft-Graph]: https://graph.microsoft.io
[O365-Perm-Ref]: https://msdn.microsoft.com/en-us/office/office365/howto/application-manifest
[OAuth2-Access-Token-Scopes]: https://tools.ietf.org/html/rfc6749#section-3.3
[OAuth2-AuthZ-Endpoint]: https://tools.ietf.org/html/rfc6749#section-3.1
[OAuth2-AuthZ-Grant-Types]: https://tools.ietf.org/html/rfc6749#section-1.3
[OAuth2-Client-Types]: https://tools.ietf.org/html/rfc6749#section-2.1
[OAuth2-Role-Def]: https://tools.ietf.org/html/rfc6749#page-6
[OpenIDConnect]: http://openid.net/specs/openid-connect-core-1_0.html
[OpenIDConnect-AuthZ-Endpoint]: http://openid.net/specs/openid-connect-core-1_0.html#AuthorizationEndpoint
[OpenIDConnect-ID-Token]: http://openid.net/specs/openid-connect-core-1_0.html#IDToken
