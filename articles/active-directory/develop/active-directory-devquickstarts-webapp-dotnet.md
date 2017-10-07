---
title: "prise en main d’application web .NET aaaAzure AD | Documents Microsoft"
description: "Créez une application web MVC .NET qui s’intègre avec Azure AD pour la connexion."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e15a41a4-dc5d-4c90-b3fe-5dc33b9a1e96
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 6d3098c9e3d7e1916ccb110c703f501ae52e788f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-web-app-sign-in-and-sign-out-with-azure-ad"></a>Connexion et déconnexion à une application web ASP.NET avec Azure AD
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

En fournissant une seule connexion et déconnexion avec seulement quelques lignes de code, Azure Active Directory (Azure AD) simplifie vous toooutsource-application web gestion des identités. Vous pouvez signer les utilisateurs et les applications web ASP.NET à l’aide de la mise en œuvre de Microsoft hello de l’Interface Web ouverte pour .NET (OWIN) intergiciel (middleware). L’intergiciel OWIN communautaire est inclus dans .NET Framework 4.5. Cet article explique comment toouse OWIN à :

* Connecter les utilisateurs dans les applications à l’aide d’Azure AD en tant que fournisseur d’identité hello tooweb.
* afficher certaines informations utilisateur ;
* Connecter les utilisateurs en dehors des applications de hello.

## <a name="before-you-get-started"></a>Avant de commencer
* Télécharger hello [squelette d’application](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) ou télécharger hello [exemple terminé](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).
* Vous devez également un locataire Azure AD dans l’application hello tooregister. Si vous n’avez pas déjà un locataire Azure AD, [apprendre comment tooget un](active-directory-howto-tenant.md).

Lorsque vous êtes prêt, suivez les procédures de hello dans hello quatre sections.

## <a name="step-1-register-hello-new-app-with-azure-ad"></a>Étape 1 : Inscrire hello nouvelle application avec Azure AD
tooset des utilisateurs de tooauthenticate application hello, inscrire tout d’abord dans votre client en effectuant des opérations hello suivantes :

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Sur la barre supérieure de hello, cliquez sur le nom de votre compte. Sous hello **répertoire** liste, le client d’Active Directory hello sélectionnez où vous souhaitez tooregister hello application.
3. Cliquez sur **plus Services** dans hello du volet gauche, puis sélectionnez **Azure Active Directory**.
4. Cliquez sur **Inscriptions des applications**, puis sélectionnez **Ajouter**.
5. Suivez hello invite toocreate un nouveau **Application Web et/ou WebAPI**.
  * **Nom** décrit hello application toousers.
  * **URL de connexion** est hello les URL de base de l’application hello. URL de valeur par défaut du squelette Hello est https://localhost:44320 /.
6. Une fois que vous avez terminé l’inscription de hello, Azure AD assigne application hello un ID d’application unique. Copiez les valeur hello de toouse de page application hello dans les sections suivantes hello.
7. À partir de hello **paramètres** -> **propriétés** page de votre application, la mise à jour de hello URI ID d’application. Hello **URI ID d’application** est un identificateur unique pour l’application hello. Bonjour convention d’affectation de noms est `https://<tenant-domain>/<app-name>` (par exemple, `https://contoso.onmicrosoft.com/my-first-aad-app`).

## <a name="step-2-set-up-hello-app-toouse-hello-owin-authentication-pipeline"></a>Étape 2 : Configurer de pipeline de hello application toouse hello OWIN d’authentification
Dans cette étape, vous configurez hello OWIN intergiciel (middleware) toouse hello OpenID Connect protocole d’authentification. Vous utilisez des demandes de connexion et de déconnexion de tooissue OWIN, gérez les sessions utilisateur, obtenez des informations utilisateur et ainsi de suite.

1. toobegin, ajouter des projets toohello des packages de NuGet hello OWIN intergiciel (middleware) à l’aide de hello Console du Gestionnaire de Package.

     ```
     PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
     PM> Install-Package Microsoft.Owin.Security.Cookies
     PM> Install-Package Microsoft.Owin.Host.SystemWeb
     ```

2. tooadd un projet de démarrage OWIN de toohello de classes appelé `Startup.cs`, cliquez sur le projet de hello, sélectionnez **ajouter**, sélectionnez **un nouvel élément**, puis recherchez **OWIN**. intergiciel (middleware) OWIN de Hello appelle hello **Configuration(...)**  méthode au démarrage de l’application hello.
3. Modifier trop de déclaration de classe hello`public partial class Startup`. Nous avons déjà mis en œuvre une partie de cette classe pour vous dans un autre fichier. Bonjour **Configuration(...)**  (méthode), effectuer un appel trop**ConfgureAuth(...)**  tooset authentification pour l’application hello.  

     ```C#
     public partial class Startup
     {
         public void Configuration(IAppBuilder app)
         {
             ConfigureAuth(app);
         }
     }
     ```

4. Ouvrez le fichier de App_Start\Startup.Auth.cs hello et implémentez hello **ConfigureAuth(...)**  (méthode). Hello les paramètres que vous fournissez dans *OpenIDConnectAuthenticationOptions* servent de coordonnées pour toocommunicate d’application hello avec Azure AD. Vous devez également tooset l’authentification de cookie, étant donné que l’intergiciel (middleware) hello OpenID Connect utilise des cookies en arrière-plan de hello.

     ```C#
     public void ConfigureAuth(IAppBuilder app)
     {
         app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

         app.UseCookieAuthentication(new CookieAuthenticationOptions());

         app.UseOpenIdConnectAuthentication(
             new OpenIdConnectAuthenticationOptions
             {
                 ClientId = clientId,
                 Authority = authority,
                 PostLogoutRedirectUri = postLogoutRedirectUri,
                 Notifications = new OpenIdConnectAuthenticationNotifications
                    {
                        AuthenticationFailed = context =>
                        {
                            context.HandleResponse();
                            context.Response.Redirect("/Error?message=" + context.Exception.Message);
                            return Task.FromResult(0);
                        }
                    }
             });
     }
     ```

5. Ouvrez le fichier web.config dans hello dans racine hello du projet de hello, puis entrez les valeurs de configuration hello Bonjour `<appSettings>` section.
  * `ida:ClientId`: hello GUID que vous avez copié à partir de hello portail Azure dans « étape 1 : inscrire l’application hello nouvelle auprès d’Azure AD. »
  * `ida:Tenant`: nom hello de votre client Azure AD (par exemple, contoso.onmicrosoft.com).
  * `ida:PostLogoutRedirectUri`: indicateur hello qui indique à Azure AD où un utilisateur doit être redirigé après une demande de déconnexion est terminée avec succès.

## <a name="step-3-use-owin-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a>Étape 3 : Utiliser OWIN tooissue connexion et déconnexion demande tooAzure AD
application Hello est désormais toocommunicate correctement configuré avec Azure AD à l’aide du protocole d’authentification OpenID Connect hello. OWIN a traité tous les détails de hello de personnalisation des messages d’authentification, la validation des jetons d’Azure AD et la gestion des sessions utilisateur. Tout ce qui reste est toogive vos utilisateurs un toosign moyen dans et la déconnexion.

1. Vous pouvez utiliser autoriser des balises dans votre toosign d’utilisateurs toorequire contrôleurs dans avant accéder à certaines pages. toodo, ouvrez Controllers\HomeController.cs et ajoutez hello `[Authorize]` toohello sur un contrôleur de balise.

     ```C#
     [Authorize]
     public ActionResult About()
     {
       ...
     ```

2. Vous pouvez également utiliser des demandes d’authentification OWIN toodirectly problème dans votre code. toodo, ouvrez Controllers\AccountController.cs. Dans actions de SignIn() et SignOut() hello, émettre OpenID Connect de challenge et de demandes de déconnexion.

     ```C#
     public void SignIn()
     {
         // Send an OpenID Connect sign-in request.
         if (!Request.IsAuthenticated)
         {
             HttpContext.GetOwinContext().Authentication.Challenge(new AuthenticationProperties { RedirectUri = "/" }, OpenIdConnectAuthenticationDefaults.AuthenticationType);
         }
     }
     public void SignOut()
     {
         // Send an OpenID Connect sign-out request.
         HttpContext.GetOwinContext().Authentication.SignOut(
              OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType);
     }
     ```

3. Ouvrez Views\Shared\_LoginPartial.cshtml tooshow hello utilisateur hello application connexion et déconnexion des liens et tooprint nom de l’utilisateur hello dans une vue.

    ```HTML
    @if (Request.IsAuthenticated)
    {
     <text>
         <ul class="nav navbar-nav navbar-right">
             <li class="navbar-text">
                 Hello, @User.Identity.Name!
             </li>
             <li>
                 @Html.ActionLink("Sign out", "SignOut", "Account")
             </li>
         </ul>
     </text>
    }
    else
    {
     <ul class="nav navbar-nav navbar-right">
         <li>@Html.ActionLink("Sign in", "SignIn", "Account", routeValues: null, htmlAttributes: new { id = "loginLink" })</li>
     </ul>
    }
    ```

## <a name="step-4-display-user-information"></a>Étape 4 : Afficher les informations utilisateur
Lors de l’authentification des utilisateurs avec OpenID Connect, Azure AD renvoie une application toohello id_token qui contient « revendications », ou assertions sur l’utilisateur de hello. Vous pouvez utiliser ces applications de hello toopersonalize revendications de manière hello suivante :

1. Ouvrez le fichier Controllers\HomeController.cs de hello. Vous pouvez accéder à l’utilisateur hello dans vos contrôleurs via hello `ClaimsPrincipal.Current` objet principal de sécurité.

 ```C#
 public ActionResult About()
 {
     ViewBag.Name = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Name).Value;
     ViewBag.ObjectId = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
     ViewBag.GivenName = ClaimsPrincipal.Current.FindFirst(ClaimTypes.GivenName).Value;
     ViewBag.Surname = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Surname).Value;
     ViewBag.UPN = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Upn).Value;

     return View();
 }
 ```

2. Générez et exécutez l’application hello. Si vous n’avez pas déjà créé un nouvel utilisateur dans votre client à un domaine onmicrosoft.com, est désormais hello temps toodo donc. Voici comment procéder :

  a. Connectez-vous à cet utilisateur et notez comment l’identité d’utilisateur hello est répercutée sur la barre supérieure de hello.

  b. Déconnectez-vous, puis reconnectez-vous sous le nom d’un autre utilisateur de votre client.

  c. Si vous vous sentez particulièrement ambitieux, enregistrez et exécutez une autre instance de cette application (avec son propre ID de client) et observez le fonctionnement de la connexion unique.

## <a name="next-steps"></a>Étapes suivantes
Pour référence, consultez [exemple hello terminée](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (sans les valeurs de configuration).

Vous pouvez maintenant passer toomore rubriques avancées. Par exemple, essayez de [Sécuriser une API web avec Azure AD](active-directory-devquickstarts-webapi-dotnet.md).

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
