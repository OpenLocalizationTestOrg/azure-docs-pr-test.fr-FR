---
title: aaaAzure AD v2 ASP.NET Web Server mise en route - Test | Documents Microsoft
description: "Implémentation de la connexion Microsoft dans une solution ASP.NET avec une application basée sur un navigateur web traditionnel utilisant le standard OpenID Connect"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 99c7525b9146605142180962fc2a61b3c953c064
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a>Test de votre code

Appuyez sur `F5` toorun votre projet dans Visual Studio. Hello navigateur s’ouvre et vous diriger trop*http://localhost : {port}* où vous verrez hello *connectez-vous avec Microsoft* bouton. Continuez et cliquez dessus toosign dans.

Lorsque vous êtes prêt tootest, utilisez toosign dans le compte professionnel ou scolaire (Azure Active Directory) ou personnelle (live.com, outlook.com). 

![Connexion à l’aide de la fenêtre de navigateur Microsoft](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin.png)

![Connexion à l’aide de la fenêtre de navigateur Microsoft](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin2.png)

#### <a name="expected-results"></a>Résultats attendus
Après la connexion, utilisateur de hello est redirigé toohello page d’accueil de votre site web qui est hello URL HTTPS spécifié dans votre application d’enregistrement de hello portail de l’enregistrement des applications Microsoft. Cette page affiche maintenant *Hello {User}* et une lien toosign montée et revendications de lien toosee hello d’un utilisateur : qui est un contrôleur de Authorize toohello lien créé précédemment.

### <a name="see-users-claims"></a>Afficher les revendications de l’utilisateur
Sélectionnez l’utilisateur hello hello hyperlink toosee. Cela nous mène toohello contrôleur et la vue qui est uniquement disponible toousers qui sont authentifiés.

#### <a name="expected-results"></a>Résultats attendus
 Vous devez voir une table qui contient les propriétés de base hello d’utilisateur de hello connecté :

| Propriété | Valeur | Description|
|---|---|---|
| Nom | {Nom complet de l’utilisateur} | utilisateur de Hello prénom et nom
|Nom d’utilisateur | <span>user@domain.com</span>| nom d’utilisateur Hello utilisé utilisateur hello connecté de tooidentify
| Objet| {Objet}|Une chaîne de toouniquely identifier d’ouverture de session utilisateur hello sur le web de hello|
| ID client| {Guid}| A *guid* toouniquely représentent l’organisation Azure Active Directory de l’utilisateur hello.|

En outre, vous verrez une table contenant toutes les revendications de l’utilisateur incluses dans la demande d’authentification. Pour obtenir la liste des revendications dans un jeton d’ID et des informations complémentaires, consultez l’[article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "Liste des revendications dans un jeton d’ID").


### <a name="test-accessing-a-method-that-has-an-authorize-attribute-optional"></a>Test de l’accès à une méthode disposant d’un attribut *[Authorize]* (facultatif)
Dans cette étape, vous allez tester l’accès au contrôleur d’authentifié hello en tant qu’utilisateur anonyme :<br/>
Sélectionnez hello lier toosign montée hello un utilisateur et les processus de déconnexion hello terminée.<br/>
Désormais, dans votre navigateur, tapez http://localhost : {port} / authentifié tooaccess votre contrôleur qui est protégé par hello `[Authorize]` attribut

#### <a name="expected-results"></a>Résultats attendus
Vous devez recevoir le message hello vous demandant de vue de hello tooauthenticate toosee.

## <a name="additional-information"></a>Informations supplémentaires

<!--start-collapse-->
### <a name="protect-your-entire-web-site"></a>Protéger l’ensemble de votre site web
tooprotect votre site web, ajoutez hello `AuthorizeAttribute` trop`GlobalFilters` dans `Global.asax` `Application_Start` méthode :

```csharp
GlobalFilters.Filters.Add(new AuthorizeAttribute());
```
<!--end-collapse-->

<div></div>
<br/>

> [!NOTE]
> **Comment toorestrict les utilisateurs à partir de toosign qu’une organisation dans l’application de tooyour**

> Par défaut, des comptes personnels (y compris outlook.com, live.com et autres), ainsi que des comptes professionnels et scolaires à partir de toute entreprise ou d’une organisation qui a intégré à Azure Active Directory peuvent se connecter au tooyour application. 

> Si vous souhaitez que votre application tooaccept connexions à partir d’une seule organisation Azure Active Directory, remplacez hello `Tenant` paramètre dans *web.config* de `Common` toohello nom du client de l’organisation de hello – exemple, *contoso.onmicrosoft.com*. Après cela, modifiez hello `ValidateIssuer` argument dans votre *classe de démarrage OWIN* trop`true`.

> tooallow des utilisateurs à partir d’une liste d’organisations spécifiques, définissez `ValidateIssuer` tootrue et utilisation hello `ValidIssuers` paramètre toospecify une liste des organisations.

> Une autre option est une méthode personnalisée de tooimplement émetteurs de hello toovalidate à l’aide du paramètre de IssuerValidator. Pour en savoir plus sur `TokenValidationParameters`, consultez [l’](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "article MSDN sur la propriété TokenValidationParameters").

