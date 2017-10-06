---
title: aaaAzure AD Windows Phone prise en main | Documents Microsoft
description: "Comment toobuild une application Windows Phone qui s’intègre à Azure AD pour l’authentification dans Azure AD qui appelle protégé API en utilisant OAuth."
services: active-directory
documentationcenter: windows
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 66f5ac20-5e1f-4b9d-bb99-9b3305e26416
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: e766bfcdfae10483772154f4b5facdec05fc846f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-a-windows-phone-app"></a>Intégration d’Azure AD avec une application Windows Phone
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> Les projets du Windows Phone 8.1 et des versions antérieures ne sont pas pris en charge dans Visual Studio 2017.  Pour en savoir plus, consultez [Plateforme cible et compatibilité dans Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).

Si vous développez une application Windows Phone 8.1, Azure AD rend très simple pour vous tooauthenticate vos utilisateurs avec leurs comptes Active Directory.  Il permet également de votre application toosecurely consommer n’importe quel web API protégée par Azure AD, comme la hello API Office 365 ou hello API Azure.

> [!NOTE]
> Cet exemple de code utilise la bibliothèque ADAL v2.0.  Pour la dernière technologie de hello, vous souhaiterez peut-être tooinstead Essayez notre [didacticiel universelle de Windows à l’aide de la version 3.0 de la bibliothèque ADAL](active-directory-devquickstarts-windowsstore.md).  Si vous créez en fait une application pour Windows Phone 8.1, il s’agit ici de hello.  ADAL v2.0 est toujours entièrement compatible avec, et est hello recommandée de développement agianst d’applications Windows Phone 8.1 à l’aide de Azure AD.
> 
> 

Pour .NET native les clients qui ont besoin de ressources de tooaccess protégé, Azure AD fournit hello bibliothèque d’authentification Active Directory, ou la bibliothèque ADAL.  Seul objectif la bibliothèque ADAL de durée de vie est toomake plus facile pour les jetons d’accès tooget votre application.  toodemonstrate facilité il s’agit, ici, nous créerons une application Windows Phone 8.1 « répertoire de recherche » qui :

* Obtient les jetons pour l’appel d’API d’Azure AD Graph hello à l’aide de hello d’accès [protocole d’authentification OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* recherche, dans un répertoire, d’utilisateurs correspondant à un UPN (nom d’utilisateur principal) donné.
* déconnexion des utilisateurs.

toobuild hello travail application complète, vous devez :

1. inscrire votre application auprès d’Azure AD ;
2. installer et configurer la bibliothèque ADAL ;
3. Utiliser des jetons tooget ADAL d’Azure AD.

tooget démarré, [télécharger un projet de squelette](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) ou [télécharger l’exemple hello terminée](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).  Chaque option est une solution Visual Studio 2013.  Vous avez également besoin d’un client Azure AD dans lequel vous pouvez créer des utilisateurs et inscrire une application.  Si vous n’avez pas encore un client, [apprendre comment tooget un](active-directory-howto-tenant.md).

## <a name="1-register-hello-directory-searcher-application"></a>1. Inscrire hello Application recherche de répertoire
tooenable vos jetons tooget d’application, vous devez tout d’abord tooregister dans votre annuaire Azure AD de client et de lui accorder hello de tooaccess d’autorisation Azure AD Graph API :

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Sur la barre supérieure de hello, cliquez sur votre compte et sous hello **répertoire** , sélectionnez le client Active Directory de hello où vous souhaitez tooregister votre application.
3. Cliquez sur **plus Services** dans hello de navigation de gauche, puis choisissez **Azure Active Directory**.
4. Cliquez sur **Inscriptions des applications**, puis sur **Ajouter**.
5. Suivez les invites hello et créer un nouveau **Application cliente Native**.
  * Hello **nom** Hello application décrivent tooend-utilisateurs de votre application
  * Hello **Uri de redirection** est une combinaison de schéma et de la chaîne que Azure AD utilise des réponses de jeton tooreturn.  Entrez temporairement une valeur d’espace réservé, par exemple, `http://DirectorySearcher`.  Nous remplacerons cette valeur ultérieurement.
6. Une fois l’inscription terminée, AAD affecte un ID d’application unique à votre application.  Vous aurez besoin de cette valeur dans les sections suivantes hello, par conséquent, copiez-le à partir de l’onglet de l’application hello.
7. À partir de hello **paramètres** choisissez **autorisations requises** et choisissez **ajouter**. Sélectionnez hello **Microsoft Graph** comme hello API et ajouter hello **les données d’annuaire en lecture** autorisation sous **autorisations déléguées**.  Cette opération activera votre hello de tooquery d’application API Graph pour les utilisateurs.

## <a name="2-install--configure-adal"></a>2. Installez et configurez ADAL
Maintenant que vous disposez d’une application dans Azure AD, vous pouvez installer la bibliothèque ADAL et écrire votre code lié à l’identité.  Toocommunicate en mesure de toobe ADAL avec Azure AD, vous devez tooprovide avec des informations sur l’inscription de votre application.

* Commencez par ajouter le projet de DirectorySearcher toohello ADAL à l’aide de la Console du Gestionnaire de Package de hello.

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* Dans le projet de DirectorySearcher hello, ouvrez `MainPage.xaml.cs`.  Remplacez les valeurs de hello en hello `Config Values` hello tooreflect de région les valeurs d’entrée en hello portail Azure.  Votre code se réfère à ces valeurs chaque fois qu’il utilise la bibliothèque ADAL.
  * Hello `tenant` est domaine hello de votre client Azure AD, par exemple, contoso.onmicrosoft.com
  * Hello `clientId` est clientId hello de votre application que vous avez copié à partir du portail de hello.
* Vous devez maintenant uri de rappel toodiscover hello pour votre application Windows Phone.  Définir un point d’arrêt sur cette ligne de hello `MainPage` méthode :

```
redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
```
* Exécutez l’application hello et copiez mis de côté valeur hello `redirectUri` lorsque hello point d’arrêt.  Le résultat suivant doit s’afficher :

```
ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
```

* Retour sur hello **configurer** onglet de votre application Bonjour portail de gestion Azure, remplacez la valeur hello hello **RedirectUri** avec cette valeur.  

## <a name="3-use-adal-tooget-tokens-from-aad"></a>3. Utiliser des jetons tooGet ADAL d’AAD
Bonjour principe de base derrière la bibliothèque ADAL est que chaque fois que votre application a besoin d’un jeton d’accès, il appelle simplement `authContext.AcquireToken(…)`, et la bibliothèque ADAL hello rest.  

* première étape de Hello est tooinitialize de votre application `AuthenticationContext` -ADAL de la classe principale.  Il s’agit d’où vous passez la bibliothèque ADAL hello coordonnées nécessaires toocommunicate avec Azure AD et d’indiquer comment les jetons toocache.

```C#
public MainPage()
{
    ...

    // ADAL for Windows Phone 8.1 builds AuthenticationContext instances through a factory
    authContext = AuthenticationContext.CreateAsync(authority).GetResults();
}
```

* Maintenant recherchez hello `Search(...)` (méthode), qui sera appelé lorsque hello utilisateur cliks hello « Rechercher » un bouton dans l’interface utilisateur de l’application hello.  Cette méthode rend un tooquery toohello API Azure AD Graph de demande GET pour les utilisateurs dont les UPN commence par hello donné du terme de recherche.  Mais dans hello tooquery de commande API Graph, vous devez tooinclude un access_token Bonjour `Authorization` en-tête Hello demande - il s’agit là qu’intervient la bibliothèque ADAL.

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    ...

    // Try tooget a token without triggering any user prompt.
    // ADAL will check whether hello requested token is in ADAL's token cache or can otherwise be obtained without user interaction.
    AuthenticationResult result = await authContext.AcquireTokenSilentAsync(graphResourceId, clientId);
    if (result != null && result.Status == AuthenticationStatus.Success)
    {
        // A token was successfully retrieved.
        QueryGraph(result);
    }
    else
    {
        // Acquiring a token without user interaction was not possible.
        // Trigger an authentication experience and specify that once a token has been obtained hello QueryGraph method should be called
        authContext.AcquireTokenAndContinue(graphResourceId, clientId, redirectURI, QueryGraph);
    }
}
```
* Si l’authentification interactive est nécessaire, la bibliothèque ADAL utilise du Windows Phone Web d’authentification Service Broker (carnet d’adresses) et [modèle de continuation](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) page de connexion toodisplay hello Azure AD.  Lorsque l’utilisateur de hello se connecte, votre application doit toopass les résultats de la bibliothèque ADAL hello d’interaction de carnet d’adresses Windows hello.  Il est aussi simple que l’implémentation hello `ContinueWebAuthentication` interface :

```C#
// This method is automatically invoked when hello application
// is reactivated after an authentication interaction through WebAuthenticationBroker.
public async void ContinueWebAuthentication(WebAuthenticationBrokerContinuationEventArgs args)
{
    // pass hello authentication interaction results tooADAL, which will
    // conclude hello token acquisition operation and invoke hello callback specified in AcquireTokenAndContinue.
    await authContext.ContinueAcquireTokenAsync(args);
}
```

* À présent, il hello toouse de temps `AuthenticationResult` que la bibliothèque ADAL retournée tooyour application.  Bonjour `QueryGraph(...)` rappel, attacher access_token hello acquis de demande GET de toohello dans l’en-tête d’autorisation hello :

```C#
private async void QueryGraph(AuthenticationResult result)
{
    if (result.Status != AuthenticationStatus.Success)
    {
        MessageDialog dialog = new MessageDialog(string.Format("If hello error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", result.Error, result.ErrorDescription), "Sorry, an error occurred while signing you in.");
        await dialog.ShowAsync();
    }

    // Add hello access token toohello Authorization Header of hello call toohello Graph API, and call hello Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);

    ...
}
```
* Vous pouvez également utiliser hello `AuthenticationResult` toodisplay informations utilisateur hello dans votre application de l’objet. Bonjour `QueryGraph(...)` méthode, utilisez hello résultat tooshow hello id de l’utilisateur sur la page de hello :

```C#
// Update hello Page UI toorepresent hello signed in user
ActiveUser.Text = result.UserInfo.DisplayableId;
```
* Enfin, vous pouvez utiliser utilisateur hello toosign ADAL ainsi l’application.  Utilisateur de hello clique sur bouton « Déconnexion » hello, nous souhaitons tooensure qui hello prochain appel trop`AcquireTokenSilentAsync(...)` échoue.  Avec la bibliothèque ADAL, il est aussi simple que l’effacement du cache de jetons hello :

```C#
private void SignOut()
{
    // Clear session state from hello token cache.
    authContext.TokenCache.Clear();

    ...
}
```

Félicitations ! Vous avez une application Windows Phone qui a des utilisateurs tooauthenticate hello capacité, en toute sécurité appelez des API Web à l’aide d’OAuth 2.0 et obtenez des informations de base sur l’utilisateur de hello.  Si vous n’avez pas encore, est à présent hello temps toopopulate votre locataire avec certains utilisateurs.  Exécutez votre application DirectorySearcher et connectez-vous avec l’un de ces utilisateurs.  Recherchez d’autres utilisateurs en fonction de leur UPN.  Fermez l’application hello et réexécutez-la.  Notez que la session de l’utilisateur hello reste intacte.  Déconnectez-vous et reconnectez-vous sous le nom d’un autre utilisateur.

ADAL rend facile tooincorporate toutes ces fonctionnalités d’identité commune dans votre application.  Il s’occupe de tout le travail dirty hello vous - gestion du cache, la prise en charge de protocole d’OAuth, présentant les utilisateur hello avec une connexion de l’interface utilisateur, l’actualisation des jetons expirés et bien plus encore.  Vous devez vraiment tooknow est un simple appel d’API `authContext.AcquireToken*(…)`.

Pour référence, exemple hello terminée (sans les valeurs de configuration) est fourni [ici](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).  Vous pouvez maintenant déplacer sur les scénarios d’identité tooadditional.  Vous souhaiterez peut-être tootry :

[Sécurisation d’une API web .NET avec Azure AD &gt;&gt;](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

