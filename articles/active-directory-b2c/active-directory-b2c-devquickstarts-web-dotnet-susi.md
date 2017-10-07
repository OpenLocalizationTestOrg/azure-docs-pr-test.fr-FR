---
title: aaaAzure Active Directory B2C | Documents Microsoft
description: "Comment toobuild une application web avec connexion-haut/connectez-vous, Profiler, de modification et mot de passe réinitialisé à l’aide d’Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: barbaraselden
ms.assetid: 30261336-d7a5-4a6d-8c1a-7943ad76ed25
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: 187f99a8dd50d212de4f0517f552cdbbe5a8edf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-web-app-with-azure-active-directory-b2c-sign-up-sign-in-profile-edit-and-password-reset"></a>Créer une application web ASP.NET avec inscription, connexion, modification du profil et réinitialisation du mot de passe Azure Active Directory B2C

Ce didacticiel vous explique les procédures suivantes :

> [!div class="checklist"]
> * Ajouter une application web de Azure AD B2C identité fonctionnalités tooyour
> * Inscrire votre application web auprès de votre répertoire Azure AD B2C
> * Créer une stratégie d’inscription/de connexion d’utilisateur, de modification du profil et de réinitialisation du mot de passe pour votre application web

## <a name="prerequisites"></a>Composants requis

- Vous devez connecter votre tooan B2C locataire compte Azure. Vous pouvez créer un compte Azure gratuit [ici](https://azure.microsoft.com/en-us/).
- Vous devez [Microsoft Visual Studio](https://www.visualstudio.com/) ou un programme tooview et modifier l’exemple de code hello similaires.

## <a name="create-an-azure-ad-b2c-directory"></a>Créer un répertoire Azure AD B2C

Avant de pouvoir utiliser Azure AD B2C, vous devez créer un répertoire ou un client. Un répertoire est un conteneur destiné à recevoir tous vos utilisateurs, applications, groupes et autres. Si vous n’en possédez pas déjà un, créez un répertoire B2C avant d’aller plus loin dans ce guide.

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

> [!NOTE]
> 
> Vous devez tooconnect hello B2C locataire tooyour abonnement Azure. Après avoir sélectionné **créer**, sélectionnez hello **lien un B2C d’AD Azure existant locataire toomy abonnement Azure** option, puis dans hello **locataire d’Azure AD B2C** liste déroulante, sélectionnez client Hello souhaité tooassociate.

## <a name="create-and-register-an-application"></a>Créer et inscrire une application

Ensuite, vous devez toocreate et inscrivez l’application hello dans votre répertoire B2C. Fournit des informations qu’Azure AD B2C doit toosecurely communiquer avec votre application. 

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

Lorsque vous avez terminé, vous aurez une API et une application native dans vos paramètres d’application.

## <a name="create-policies-on-your-b2c-tenant"></a>Créer des stratégies dans votre locataire B2C

Dans Azure AD B2C, chaque expérience utilisateur est définie par une [stratégie](active-directory-b2c-reference-policies.md). Cet exemple de code contient trois expériences liées à l’identité : **l’inscription et la connexion**, la **modification du profil** et la **réinitialisation du mot de passe**.  Vous devez toocreate une stratégie de chaque type, comme décrit dans hello [article de référence de stratégie](active-directory-b2c-reference-policies.md). Pour chaque stratégie, être toocopy nom hello de votre stratégie pour une utilisation ultérieure ou revendication et attribut de nom d’affichage tooselect hello.

### <a name="add-your-identity-providers"></a>Ajouter vos fournisseurs d’identité

À partir de vos paramètres, sélectionnez **Fournisseurs d’identité** et choisissez Abonnement par nom d’utilisateur ou Abonnement par e-mail.

### <a name="create-a-sign-up-and-sign-in-policy"></a>Créer une stratégie d’inscription et de connexion

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

### <a name="create-a-profile-editing-policy"></a>Création d’une stratégie de modification de profil

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

### <a name="create-a-password-reset-policy"></a>Création d’une stratégie de réinitialisation du mot de passe

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

Après avoir créé vos stratégies, vous êtes prêt toobuild votre application.

## <a name="download-hello-sample-code"></a>Télécharger l’exemple de code hello

code Hello pour ce didacticiel est conservée sur [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi). Vous pouvez cloner l’exemple hello en exécutant :

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

Après avoir téléchargé l’exemple de code hello, ouvrez hello tooget du fichier .sln de Visual Studio a démarré. fichier de solution Hello contient deux projets : `TaskWebApp` et `TaskService`. `TaskWebApp`est hello application web MVC hello utilisateur interagit avec. `TaskService`est web principal API de l’application hello qui stocke la liste des actions de chaque utilisateur. Cet article traite uniquement hello `TaskWebApp` application. toolearn comment toobuild `TaskService` à l’aide d’Azure AD B2C, consultez [notre didacticiel de l’api web .NET](active-directory-b2c-devquickstarts-api-dotnet.md).

## <a name="update-code-toouse-your-tenant-and-policies"></a>Mettre à jour du code toouse votre locataire et les stratégies

Notre exemple est configuré toouse hello stratégies et ID de client de notre client de démonstration. tooconnect il tooyour de locataire propre, vous devez tooopen `web.config` Bonjour `TaskWebApp` de projet et remplacez hello valeurs suivantes :

* `ida:Tenant` par le nom de votre locataire
* `ida:ClientId` par votre ID d’application web
* `ida:ClientSecret` par votre clé secrète d’application web
* `ida:SignUpSignInPolicyId` par votre nom de stratégie d’inscription ou de connexion
* `ida:EditProfilePolicyId` par votre nom de stratégie « Modifier le profil »
* `ida:ResetPasswordPolicyId` par votre nom de stratégie « Réinitialiser le mot de passe »

## <a name="launch-hello-app"></a>Lancer l’application hello
À partir de Visual Studio, lancez application hello. Accédez onglet de liste de tâches toohello et hello Remarque URl est : https://login.microsoftonline.com/*YourTenantName*/oauth2/v2.0/authorize?p=*YourSignUpPolicyName*& client_id = *YourclientID*...

Inscrivez-vous pour une application hello à l’aide de votre nom d’utilisateur ou une adresse de messagerie. Déconnectez-vous, puis reconnectez-vous et modifier le profil de hello ou réinitialiser le mot de passe hello. Déconnectez-vous et connectez-vous en tant qu’autre utilisateur. 

## <a name="add-social-idps"></a>Ajout d’IDP sociaux

Actuellement, application hello prend en charge uniquement les utilisateurs d’abonnement et de connexion à l’aide de **comptes locaux**; les comptes stockés dans votre répertoire B2C qui utilisent un nom d’utilisateur et un mot de passe. Avec Azure AD B2C, vous pouvez ajouter la prise en charge d’autres **fournisseurs d’identité** sans modifier votre code.

tooadd sociaux IDPs tooyour application, commencez par suivre hello des instructions dans ces articles. Pour chaque IDP vous toosupport, vous devez tooregister une application de ce système et obtenez un ID client.

* [Définir Facebook en tant qu’IDP](active-directory-b2c-setup-fb-app.md)
* [Définir Google en tant qu’IDP](active-directory-b2c-setup-goog-app.md)
* [Définir Amazon en tant qu’IDP](active-directory-b2c-setup-amzn-app.md)
* [Définir LinkedIn en tant qu’IDP](active-directory-b2c-setup-li-app.md)

Après avoir ajouté tooyour de fournisseurs d’identité hello directory B2C, modification de votre tooinclude trois stratégies hello IDPs nouveau, comme décrit dans hello [article de référence de stratégie](active-directory-b2c-reference-policies.md). Après avoir enregistré vos stratégies, exécutez à nouveau application hello.  Vous devez voir hello Qu'idps nouveau ajoutés en tant qu’options de connexion et d’inscription dans chacun de vos expériences d’identité.

Vous pouvez faire des essais avec vos stratégies et observez l’effet hello sur votre exemple d’application. Ajoutez ou supprimez des fournisseurs d’identité, manipulez des revendications d’application ou modifiez des attributs d’inscription. Faites des essais jusqu’à ce que vous compreniez la façon dont les stratégies, les requêtes d’authentification et la bibliothèque OWIN sont liées.

## <a name="sample-code-walkthrough"></a>Exemple de code de procédure pas à pas
Hello les sections suivantes vous montre comment le code de l’application exemple hello est configuré. Vous pouvez les utiliser comme guide pour le développement de vos futures applications.

### <a name="add-authentication-support"></a>Ajouter le support de l’authentification

Vous pouvez maintenant configurer votre toouse application Azure AD B2C. Votre application communique avec Azure AD B2C en envoyant des demandes d’authentification OpenID Connect. l’expérience utilisateur hello dictent Hello demandes votre application veut tooexecute en spécifiant une stratégie hello. Vous pouvez utiliser toosend de bibliothèque de Microsoft OWIN ces demandes, exécution des stratégies, gérer les sessions utilisateur et bien plus encore.

#### <a name="install-owin"></a>Installer OWIN

toobegin, ajouter le projet toohello des packages de NuGet hello OWIN intergiciel (middleware) à l’aide de hello Console du Gestionnaire de Package Visual Studio.

```Console
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
PM> Install-Package Microsoft.Owin.Security.Cookies
PM> Install-Package Microsoft.Owin.Host.SystemWeb
```

#### <a name="add-an-owin-startup-class"></a>Ajouter une classe de démarrage OWIN

Ajouter un toohello de classe de démarrage OWIN API appelée `Startup.cs`.  Avec le bouton droit sur le projet hello, sélectionnez **ajouter** et **un nouvel élément**, puis recherchez OWIN. intergiciel (middleware) OWIN de Hello appellera hello `Configuration(…)` méthode au démarrage de votre application.

Dans notre exemple, nous avons modifié trop déclaration de classe hello`public partial class Startup` et implémenté hello autre partie de la classe hello dans `App_Start\Startup.Auth.cs`. À l’intérieur hello `Configuration` (méthode), nous avons ajouté un appel trop`ConfigureAuth`, qui est défini dans `Startup.Auth.cs`. Après modification de hello, `Startup.cs` ressemble à hello qui suit :

```CSharp
// Startup.cs

public partial class Startup
{
    // hello OWIN middleware will invoke this method when hello app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of hello class
        ConfigureAuth(app);
    }
}
```

#### <a name="configure-hello-authentication-middleware"></a>Configurer hello intergiciel d’authentification

Les fichiers ouverts hello `App_Start\Startup.Auth.cs` et implémenter hello `ConfigureAuth(...)` (méthode). Hello les paramètres que vous fournissez dans `OpenIdConnectAuthenticationOptions` servent de coordonnées pour toocommunicate de votre application avec Azure Active Directory B2C. Si vous ne spécifiez pas de certains paramètres, il utilisera la valeur par défaut de hello. Par exemple, nous ne spécifiez pas hello `ResponseType` dans l’exemple hello, donc hello valeur par défaut `code id_token` seront utilisées dans chaque tooAzure demande sortante AD B2C.

Vous devez également tooset l’authentification de cookie. intergiciel (middleware) Hello OpenID Connect utilise les sessions utilisateur toomaintain les cookies, entre autres choses.

```CSharp
// App_Start\Startup.Auth.cs

public partial class Startup
{
    // Initialize variables ...

    // Configure hello OWIN middleware
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseCookieAuthentication(new CookieAuthenticationOptions());
        app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

        app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                // Generate hello metadata address using hello tenant and policy information
                MetadataAddress = String.Format(AadInstance, Tenant, DefaultPolicy),

                // These are standard OpenID Connect parameters, with values pulled from web.config
                ClientId = ClientId,
                RedirectUri = RedirectUri,
                PostLogoutRedirectUri = RedirectUri,

                // Specify hello callbacks for each type of notifications
                Notifications = new OpenIdConnectAuthenticationNotifications
                {
                    RedirectToIdentityProvider = OnRedirectToIdentityProvider,
                    AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    AuthenticationFailed = OnAuthenticationFailed,
                },

                // Specify hello claims toovalidate
                TokenValidationParameters = new TokenValidationParameters
                {
                    NameClaimType = "name"
                },

                // Specify hello scope by appending all of hello scopes requested into one string (seperated by a blank space)
                Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
            }
        );
    }

    // Implement hello "Notification" methods...
}
```

Dans `OpenIdConnectAuthenticationOptions` ci-dessus, nous définissons un ensemble de fonctions de rappel pour les notifications spécifiques qui sont reçues par un intergiciel (middleware) hello OpenID Connect. Ces comportements sont définis en utilisant un `OpenIdConnectAuthenticationNotifications` de l’objet et stocké dans hello `Notifications` variable. Dans notre exemple, nous définissons trois rappels différents en fonction de l’événement de hello.

### <a name="using-different-policies"></a>Utilisation de différentes stratégies

Hello `RedirectToIdentityProvider` notification est déclenchée chaque fois qu’une demande est faite tooAzure AD B2C. Dans la fonction de rappel hello `OnRedirectToIdentityProvider`, nous vérifions Bonjour sortant appel si nous voulons que toouse une autre stratégie. Dans l’ordre toodo réinitialisation de mot de passe ou modifier un profil, vous avez besoin de stratégie correspondante de hello toouse telles que la stratégie au lieu de la stratégie de « S’inscrire ou signe » hello par défaut de réinitialisation de mot de passe hello.

Dans notre exemple, lorsqu’un utilisateur souhaite que le mot de passe tooreset hello ou modifier le profil de hello, nous ajoutons stratégie hello nous préférons toouse dans le contexte OWIN de hello. Cela peut se faire de manière hello suivante :

```CSharp
    // Let hello middleware know you are trying toouse hello edit profile policy
    HttpContext.GetOwinContext().Set("Policy", EditProfilePolicyId);
```

Et vous pouvez implémenter la fonction de rappel hello `OnRedirectToIdentityProvider` de manière hello suivante :

```CSharp
/*
*  On each call tooAzure AD B2C, check if a policy (e.g. hello profile edit or password reset policy) has been specified in hello OWIN context.
*  If so, use that policy when making hello call. Also, don't request a code (since it won't be needed).
*/
private Task OnRedirectToIdentityProvider(RedirectToIdentityProviderNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    var policy = notification.OwinContext.Get<string>("Policy");

    if (!string.IsNullOrEmpty(policy) && !policy.Equals(DefaultPolicy))
    {
        notification.ProtocolMessage.Scope = OpenIdConnectScopes.OpenId;
        notification.ProtocolMessage.ResponseType = OpenIdConnectResponseTypes.IdToken;
        notification.ProtocolMessage.IssuerAddress = notification.ProtocolMessage.IssuerAddress.Replace(DefaultPolicy, policy);
    }

    return Task.FromResult(0);
}
```

### <a name="handling-authorization-codes"></a>Gestion des codes d’autorisation

Hello `AuthorizationCodeReceived` notification est déclenchée lors de la réception d’un code d’autorisation. intergiciel (middleware) Hello OpenID Connect ne prend pas en charge les codes d’échange pour les jetons d’accès. Vous pouvez échanger manuellement les code hello pour le jeton hello dans une fonction de rappel. Pour plus d’informations, consultez hello [documentation](active-directory-b2c-devquickstarts-web-api-dotnet.md) qui explique comment.

### <a name="handling-errors"></a>Gestion des erreurs

Hello `AuthenticationFailed` notification est déclenchée lorsque l’authentification échoue. Dans sa méthode de rappel, vous pouvez gérer les erreurs de hello comme vous le souhaitez. Toutefois, vous devez ajouter une vérification pour le code d’erreur hello `AADB2C90118`. Pendant l’exécution de hello Hello stratégie « S’inscrire ou se connecter », utilisateur de hello a hello opportunité tooselect un **votre mot de passe oublié ?** lien. Dans ce cas, Azure AD B2C envoie votre application de ce code d’erreur indiquant que votre application doit effectuer une demande à l’aide de stratégie de réinitialisation du mot de passe hello à la place.

```CSharp
/*
* Catch any failures received by hello authentication middleware and handle appropriately
*/
private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    notification.HandleResponse();

    // Handle hello error code that Azure AD B2C throws when trying tooreset a password from hello login page
    // because password reset is not supported by a "sign-up or sign-in policy"
    if (notification.ProtocolMessage.ErrorDescription != null && notification.ProtocolMessage.ErrorDescription.Contains("AADB2C90118"))
    {
        // If hello user clicked hello reset password link, redirect toohello reset password route
        notification.Response.Redirect("/Account/ResetPassword");
    }
    else if (notification.Exception.Message == "access_denied")
    {
        notification.Response.Redirect("/");
    }
    else
    {
        notification.Response.Redirect("/Home/Error?message=" + notification.Exception.Message);
    }

    return Task.FromResult(0);
}
```

### <a name="send-authentication-requests-tooazure-ad"></a>Envoyer tooAzure de demandes d’authentification Active Directory

Votre application est maintenant toocommunicate correctement configuré avec Azure AD B2C à l’aide du protocole d’authentification OpenID Connect hello. OWIN gère les détails de hello d’élaborer des messages d’authentification, la validation des jetons d’Azure AD B2C et la gestion de session utilisateur. Tout ce qui reste est tooinitiate les flux de chaque utilisateur.

Lorsqu’un utilisateur sélectionne **connexion à distance et à la connexion**, **modifier le profil**, ou **réinitialisation de mot de passe** dans hello web app, action de hello associé est appelée dans `Controllers\AccountController.cs`:

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting toosign up or sign in
*/
public void SignUpSignIn()
{
    // Use hello default policy tooprocess hello sign up / sign in flow
    if (!Request.IsAuthenticated)
    {
        HttpContext.GetOwinContext().Authentication.Challenge();
        return;
    }

    Response.Redirect("/");
}

/*
*  Called when requesting tooedit a profile
*/
public void EditProfile()
{
    if (Request.IsAuthenticated)
    {
        // Let hello middleware know you are trying toouse hello edit profile policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
        HttpContext.GetOwinContext().Set("Policy", Startup.EditProfilePolicyId);

        // Set hello page tooredirect tooafter editing hello profile
        var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
        HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

        return;
    }

    Response.Redirect("/");

}

/*
*  Called when requesting tooreset a password
*/
public void ResetPassword()
{
    // Let hello middleware know you are trying toouse hello reset password policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
    HttpContext.GetOwinContext().Set("Policy", Startup.ResetPasswordPolicyId);

    // Set hello page tooredirect tooafter changing passwords
    var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
    HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

    return;
}
```

Vous pouvez également utiliser toosign OWIN utilisateur hello à partir de l’application hello. Dans `Controllers\AccountController.cs`, voici ce que nous obtenons :

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting toosign out
*/
public void SignOut()
{
    // toosign out hello user, you should issue an OpenIDConnect sign out request.
    if (Request.IsAuthenticated)
    {
        IEnumerable<AuthenticationDescription> authTypes = HttpContext.GetOwinContext().Authentication.GetAuthenticationTypes();
        HttpContext.GetOwinContext().Authentication.SignOut(authTypes.Select(t => t.AuthenticationType).ToArray());
        Request.GetOwinContext().Authentication.GetAuthenticationTypes();
    }
}
```

Dans tooexplicitly plus appel d’une stratégie, vous pouvez utiliser un `[Authorize]` sur vos contrôleurs de balise qui s’exécute une stratégie si l’utilisateur de hello n’est pas connecté. Ouvrez `Controllers\HomeController.cs` et ajoutez hello `[Authorize]` balise toohello revendications contrôleur.  OWIN sélectionne hello dernière stratégie configurée lorsque hello `[Authorize]` balise est atteint.

```CSharp
// Controllers\HomeController.cs

// You can use hello Authorize decorator tooexecute a certain policy if hello user is not already signed into hello app.
[Authorize]
public ActionResult Claims()
{
  ...
```

### <a name="display-user-information"></a>Afficher les informations utilisateur

Lorsque vous authentifiez des utilisateurs à l’aide de OpenID Connect, Azure AD B2C retourne une application de jeton toohello ID contenant **revendications**. Il s’agit des assertions sur l’utilisateur de hello. Vous pouvez utiliser les revendications toopersonalize votre application.

Ouvrez hello `Controllers\HomeController.cs` fichier. Vous pouvez accéder aux revendications d’utilisateur dans vos contrôleurs via hello `ClaimsPrincipal.Current` objet principal de sécurité.

```CSharp
// Controllers\HomeController.cs

[Authorize]
public ActionResult Claims()
{
    Claim displayName = ClaimsPrincipal.Current.FindFirst(ClaimsPrincipal.Current.Identities.First().NameClaimType);
    ViewBag.DisplayName = displayName != null ? displayName.Value : string.Empty;
    return View();
}
```

Vous pouvez accéder à toute revendication que votre application reçoit Bonjour même façon.  Une liste de toutes les revendications hello application hello reçoit est disponible pour vous sur hello **revendications** page.
