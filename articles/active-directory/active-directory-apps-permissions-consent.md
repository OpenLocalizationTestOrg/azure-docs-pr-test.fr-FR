---
title: Applications, autorisations et consentement dans Azure Active Directory | Microsoft Docs
description: "Azure AD Connect intègre vos répertoires locaux à Azure Active Directory. Cela vous permet de tooprovide une identité commune pour les applications Office 365, Azure et SaaS intégrée à Azure AD."
keywords: Introduction tooAzure AD, les applications, ce qui est Azure AD Connect, installer active directory
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 25897cc4-7687-49b6-b0d5-71f51302b6b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/31/2017
ms.author: billmath
ms.reviewer: jesakowi
ms.custom: oldportal;it-pro;
ms.openlocfilehash: af0c2669199736fdb41e85876a7e3a7064e80770
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="apps-permissions-and-consent-in-azure-active-directory"></a>Applications, autorisations et consentement dans Azure Active Directory
Dans Azure Active Directory, vous pouvez ajouter le répertoire tooyour des applications.  les applications Hello peuvent varier en fonction de type hello d’application.  applications tooview dans le portail classique hello, sélectionnez un répertoire et choisir les applications.

![](media/active-directory-apps-permissions-consent/apps1.png)

> [!IMPORTANT]
> Microsoft recommande de gérer Azure AD en utilisant hello [centre d’administration Azure AD](https://aad.portal.azure.com) Bonjour portail Azure au lieu d’utiliser hello portail Azure classic référencée dans cet article.

## <a name="types-of-apps"></a>Types d’applications

1. **Applications à locataire unique** </br>
    - **Applications du locataire unique** -communément tooas les applications line of business (LOB). Il s’agit de cas de hello où une personne au sein de votre organisation développe leur propre application et souhaitez que les utilisateurs de hello organisation toobe en mesure de toosign dans toohello application.
    ![](media/active-directory-apps-permissions-consent/apps2.png)
    - **Applications du Proxy d’application** - lorsque vous exposez une application locale avec le Proxy d’application Azure AD, une application à locataire unique est enregistrée dans votre client (dans Ajout toohello service de Proxy d’application). Cette application représente votre application locale pour toutes les interactions du cloud (par exemple, l’authentification). (Le proxy d’application nécessite Azure AD Standard ou une version ultérieure.)


2. **Applications multi-locataires**
    - **Applications mutualisées auxquelles d’autres peuvent donner son consentement à** - similaire trop « applications locataire unique qui se développe de votre organisation ». Hello principale différence (en plus de logique hello dans l’application hello lui-même) fait que les utilisateurs à partir d’autres clients peuvent également de consentement tooand toohello application de connexion.</br>
    ![](media/active-directory-apps-permissions-consent/apps4.png)
    - **Applications multi-locataires développées par d’autres personnes, pour lesquelles Contoso peut donner son consentement** (ou « applications consenties », en version courte). Il s’agit d’inconvénient hello des « applications mutualisées que développe de votre organisation ». Lorsqu’une autre organisation développe une application mutualisée, les utilisateurs de votre organisation peuvent donner son consentement toohello application et connectez-vous à tooit.
    - **Applications internes Microsoft** : applications représentant des services Microsoft. Consentement est piloté par le fait de hello que vous vous inscrivez pour le service de hello. Il est parfois spéciaux UX et la logique pour certaines applications de tiers qui est souvent utilisée lors de l’établissement des stratégies autour de l’accès toohello application.</br>
    ![](media/active-directory-apps-permissions-consent/apps3.png)
    - **Les applications pré-intégrées** -applications disponibles dans la galerie d’applications Azure AD, que vous pouvez ajouter de hello tooyour Active tooprovide single sign-on (et dans certains cas, l’approvisionnement) toopopular les applications SaaS.
    - **Authentification unique Azure AD** : authentification unique « réelle ». Concerne les applications qui peuvent être intégrées à Azure AD via un protocole de connexion pris en charge, comme SAML 2.0 ou OpenID Connect. Assistant de Hello vous guide tout au long de sa configuration.
    - **Mot de passe l’authentification unique sur**: Azure AD stocke en toute sécurité les informations d’identification de l’utilisateur hello pour application hello et informations d’identification hello sont « injectées » dans le formulaire de connexion hello par hello extension de navigateur d’accéder à l’application Azure AD. Également appelée « mise au coffre des mots de passe ».

## <a name="permissions"></a>Autorisations

Lorsqu’une application est inscrite, utilisateur hello effectuant l’inscription d’une application hello (autrement dit, le développeur hello) définit les autorisations hello application a besoin d’accéder à et les ressources. (hello les ressources sont, eux-mêmes, définis en tant que d’autres applications.) Par exemple, un utilisateur de création d’une application de lecture du courrier, indiquerait que leur application requiert l’autorisation de « Accès aux boîtes aux lettres en tant qu’utilisateur connecté hello » hello Bonjour ressource « Office 365 Exchange Online » :
    
![](media/active-directory-apps-permissions-consent/apps6.png)

Dans l’ordre pour une application de (client hello) toorequest certaines autorisations à partir d’une autre application (ressource hello), développeur hello de l’application de ressource hello définit les autorisations de hello qui existent. Dans notre exemple, Microsoft, propriétaire hello de l’application de ressource « Office 365 Exchange Online » hello, ont défini une autorisation nommée « Accès aux boîtes aux lettres en tant qu’utilisateur connecté hello ».

Lorsque vous définissez des autorisations, le développeur d’application hello doit définir si hello autorisation peut être consentie, ou s’il requiert le consentement de l’administrateur. Cela permet aux développeurs tooallow utilisateurs tooconsent sur leurs propres tooapps demande des autorisations de faible sensibilité uniquement, mais nécessitent des autorisations d’administrateurs tooconsent toomore sensibles. Par exemple, hello application de ressource « Azure Active Directory », a été défini pour les utilisateurs peuvent accepter tooapps, demandant des autorisations limitées en lecture seule.  Toutefois, le consentement de l’administrateur est requis pour les autorisations de lecture complète et toutes les autorisations d’écriture.

Dans la mesure où les clients natifs ne sont pas authentifiés, une application définie comme application cliente native peut seulement demander des autorisations déléguées. Cela signifie qu’il doit toujours y avoir un utilisateur réel impliqué lors de l’obtention d’un jeton. Les applications web et les API web (clients confidentiels) doivent toujours s’authentifier auprès d’Azure AD lors de l’obtention d’un jeton d’accès. Ce qui signifie qu’ils ont également la possibilité de hello de demander des autorisations d’application uniquement. Par exemple, si le service principal de tooanother tooauthenticate a besoin d’un service principal. Les applications demandant des autorisations application seule nécessitent toujours le consentement de l’administrateur.

En résumé :



- Une application (client) indique que les autorisations hello dont il a besoin pour d’autres applications (ressources).
- Une application (ressource) indique quelles autorisations sont exposés tooother applications (clients).
- Une autorisation peut être une autorisation application seule ou une autorisation déléguée.
- Une autorisation déléguée peut être marquée comme « autorise le consentement de l’utilisateur », ou « requiert le consentement de l’administrateur ».
- Une application peut se comporter comme un client (en déclarant qu’il nécessite de ressource d’autorisations tooa), sous la forme d’une ressource (en déclarant les autorisations qu’il expose) ou les deux.

## <a name="controls"></a>Commandes

Hello Voici une liste de contrôles d’administration différents hello disponibles pour tous les ce comportement. admin Hello contrôles accessibles dans le portail classique de hello de configurer sous le répertoire de hello.

![](media/active-directory-apps-permissions-consent/apps7.png)

Bonjour Azure portail, sous **gérer**, **paramètres utilisateur**.

![](media/active-directory-apps-permissions-consent/apps11.png)



- Vous pouvez contrôler si les utilisateurs peuvent accepter les tooapps :

Dans le portail classique de hello, sélectionnez **les utilisateurs peuvent donner des applications autorisations tooaccess leurs données.**
![](media/active-directory-apps-permissions-consent/apps8.png)

Bonjour portail Azure, sélectionnez **les utilisateurs peuvent autoriser des applications tooaccess leurs données**.
![](media/active-directory-apps-permissions-consent/apps12.png)



- Vous pouvez contrôler si les utilisateurs peuvent inscrire leurs propres applications métier de locataire unique : dans, sélectionnez portail classique hello **les utilisateurs peuvent ajouter des applications intégrées.**
![](media/active-directory-apps-permissions-consent/apps9.png)

Bonjour portail Azure, sélectionnez **les utilisateurs peuvent autoriser des applications tooaccess leurs données**.
![](media/active-directory-apps-permissions-consent/apps13.png)

>[!NOTE]
>Même si vous autorisez les utilisateurs des applications métier tooregister locataire unique, il existe des limites toowhat peuvent être inscrits.  
>Par exemple, les développeurs qui ne sont pas des administrateurs de répertoires.
>
>- Les utilisateurs ne peuvent pas transformer une application à locataire unique en application multi-locataire.
>- Lors de l’inscription des applications métier locataire unique, les utilisateurs ne peuvent pas demander des autorisations d’application uniquement tooother applications.
>- Lors de l’inscription des applications métier locataire unique, les utilisateurs ne peuvent pas demander des autorisations déléguées tooother applications si ces autorisations requièrent le consentement de l’administrateur.
>- Les utilisateurs ne peuvent pas faire tooapps de modifications qu’ils ne sont pas propriétaires de.



- Vous pouvez décider si les utilisateurs peuvent eux-mêmes ajouter des applications pré-intégrées qui utilisent l’authentification unique par mot de passe (également appelée « mise au coffre des mots de passe ») ![](media/active-directory-apps-permissions-consent/apps10.png)



- Vous pouvez contrôler dans quelles conditions les applications sont accessibles (c’est-à-dire, définir un accès conditionnel). Sachez que cela s’applique à la fois toohello client application et application de ressource toohello. Par conséquent, supposons que vous définissez une stratégie d’accès conditionnel qui indique que cette application « Office 365 Exchange Online » hello est accessible uniquement à partir d’ordinateurs qui sont conformes.  Cette stratégie sera également entrer en action lorsqu’un utilisateur tente de toouse une application cliente qui demande tooExchange d’autorisations en ligne.



- Vous disposez de visibilité dans lequel les applications ont été consenti tooand celles qui est utilisés.

1.  Quand un utilisateur a consenti tooan application, un objet de principal du service est créé dans le locataire de hello. Création de principal du service est incluse dans le rapport d’audit de hello.
2.  Rapports d’activité de connexion utilisateur vous indiquent quels utilisateurs de hello application se connecte à. 

## <a name="example"></a>Exemple

Par exemple, prenons l’application hello « FabrikamMail pour Office 365 », qui vous avez remarqué des utilisateurs dans votre locataire sont connectent. « FabrikamMail » est une application de lecture de courriers pour Android, publiée par « Fabrikam, Inc. ». Cela ne tombe hello « applications mutualisées autres développer, Contoso peut donner son consentement à ».

Si les utilisateurs sont autorisés à tooconsent, ils Obtient un Bonjour invite de consentement première fois, qu'ils se connectent :![](media/active-directory-apps-permissions-consent/apps14.png)

« Accéder à vos boîtes aux lettres » est la chaîne de consentement hello orientés utilisateur pour obtenir l’autorisation « Accès aux boîtes aux lettres en tant qu’utilisateur connecté hello » hello exposée par « Office 365 Exchange Online » (autrement dit, Exchange).

Vous pouvez voir les autorisations hello en recherchant des objets de principal du service hello Exchange (ressource hello), qui a été ajouté lorsque vous vous abonnez à Office 365. Vous pouvez considérer d’objet de principal du service hello d’une « instance » de l’application hello dans votre client, qui est utilisé pour enregistrer les configurations et les différentes options.  Vous pouvez le voir à l’aide de hello `Get-AzureADServicePrincipal` dans PowerShell.

    PS C:\> Get-AzureADServicePrincipal -ObjectId 383f7b97-6754-4d3d-9474-3908ebcba1c6 | fl *
    
    DeletionTimeStamp         : 
    ObjectId                  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    ObjectType                : ServicePrincipal
    AccountEnabled            : True
    AppDisplayName            : Office 365 Exchange Online
    AppId                     : 00000002-0000-0ff1-ce00-000000000000
    AppOwnerTenantId          : 
    AppRoleAssignmentRequired : False
    AppRoles                  : {...}
    DisplayName               : Microsoft.Exchange
    ErrorUrl                  : 
    Homepage                  : 
    KeyCredentials            : {}
    LogoutUrl                 : 
    Oauth2Permissions         : {...
                                , class OAuth2Permission {
                                  AdminConsentDescription : Allows hello app toohave hello same access toomailboxes as hello signed-in user via Exchange Web Services.
                                  AdminConsentDisplayName : Access mailboxes as hello signed-in user via Exchange Web Services
                                  Id                      : 3b5f3d61-589b-4a3c-a359-5dd4b5ee5bd5
                                  IsEnabled               : True
                                  Type                    : User
                                  UserConsentDescription  : Allows hello app full access tooyour mailboxes on your behalf.
                                  UserConsentDisplayName  : Access your mailboxes
                                  Value                   : full_access_as_user
                                },
                                ...}
    PasswordCredentials       : {}
    PublisherName             : 
    ReplyUrl                  : 
    SamlMetadataUrl           : 
    ServicePrincipalNames     : {00000002-0000-0ff1-ce00-000000000000/outlook.office365.com, 00000002-0000-0ff1-ce00-000000000000/mail.office365.com, 00000002-0000-0ff1-ce00-000000000000/outlook.com, 
                                00000002-0000-0ff1-ce00-000000000000/*.outlook.com...}
    Tags                      : {}

Consentement est lancé lorsque l’utilisateur de hello clique sur « Accepter ». Tout d’abord, un objet de principal du service pour « FabrikamMail pour Office 365 » est créé dans le locataire de hello. Hello principal du service ressemble à ceci :

    PS C:\> Get-AzureADServicePrincipal -SearchString "FabrikamMail for Office 365" | fl *
    
    DeletionTimeStamp         : 
    ObjectId                  : a8b16333-851d-42e8-acd2-eac155849b37
    ObjectType                : ServicePrincipal
    AccountEnabled            : True
    AppDisplayName            : FabrikamMail for Office 365
    AppId                     : aba7c072-2267-4031-8960-e7a2db6e0590
    AppOwnerTenantId          : 4a4076e0-a70f-41c6-b819-6f9c4a86df89
    AppRoleAssignmentRequired : False
    AppRoles                  : {}
    DisplayName               : FabrikamMail for Office 365
    ErrorUrl                  : 
    Homepage                  : 
    KeyCredentials            : {}
    LogoutUrl                 : 
    Oauth2Permissions         : {}
    PasswordCredentials       : {}
    PublisherName             : Fabrikam, Inc.
    ReplyUrl                  : 
    SamlMetadataUrl           : 
    ServicePrincipalNames     : {aba7c072-2267-4031-8960-e7a2db6e0590}
    Tags                      : {WindowsAzureActiveDirectoryIntegratedApp}

Terme autorisation tooan application crée un lien Oauth2PermissionGrant entre les éléments suivants de hello :
  
- objet d’utilisateur Hello
- applications clientes Hello ServicePrincipalName (SPN)
- applications de ressources Hello ServicePrincipalName (SPN)
- autorisations dans l’application de ressource hello.  

Dans les cas de hello de FabrikamMail, il ressemble à ceci :

    PS C:\> Get-AzureADUserOAuth2PermissionGrant -ObjectId ddiggle@aadpremiumlab.onmicrosoft.com | fl *
    
    ClientId    : a8b16333-851d-42e8-acd2-eac155849b37
    ConsentType : Principal
    ExpiryTime  : 05/15/2017 07:02:39 AM
    ObjectId    : M2OxqB2F6EKs0urBVYSbN5d7PzhUZz1NlH25COvLocbJjoxkUFfRQauryBKwBWet
    PrincipalId : 648c8ec9-5750-41d1-abab-c812b00567ad
    ResourceId  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    Scope       : full_access_as_user
    StartTime   : 01/01/0001 12:00:00 AM

(**ClientId** est l’ID d’objet principal du FabrikamMail service (hello celui créé uniquement), **PrincipalId** est l’ID d’objet utilisateur hello (de hello utilisateur qui a donné son consentement), **ResourceId**est service d’Exchange ID d’objet principal, l’étendue est l’autorisation hello dans Exchange a consenti à).

Si les utilisateurs ne sont pas autorisés tooconsent, ils verront un écran indiquant que cette autorisation est requis.

