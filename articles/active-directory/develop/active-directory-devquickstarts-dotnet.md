---
title: .NET aaaAzure AD prise en main | Documents Microsoft
description: "Comment toobuild une application de bureau Windows de .NET qui s’intègre à Azure AD pour l’authentification dans Azure AD qui appelle protégé API en utilisant OAuth."
services: active-directory
documentationcenter: .net
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: ed33574f-6fa3-402c-b030-fae76fba84e1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: c09b358f24c7bfb371b34cf72ca48c0a45042f5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-a-windows-desktop-wpf-app"></a>Intégration d’Azure AD dans une application WPF de bureau Windows
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Si vous développez une application de bureau, Azure AD rend très simple pour vous tooauthenticate vos utilisateurs avec leurs comptes Active Directory.  Il permet également de votre application toosecurely consommer n’importe quel web API protégée par Azure AD, comme la hello API Office 365 ou hello API Azure.

Pour .NET native les clients qui ont besoin de ressources de tooaccess protégé, Azure AD fournit hello bibliothèque d’authentification Active Directory, ou la bibliothèque ADAL.  Seul objectif la bibliothèque ADAL de durée de vie est toomake plus facile pour les jetons d’accès tooget votre application.  toodemonstrate facilité il s’agit, ici nous allons créer une application de liste de tâches WPF .NET :

* Obtient les jetons pour l’appel d’API d’Azure AD Graph hello à l’aide de hello d’accès [protocole d’authentification OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* recherche, dans un répertoire, d’utilisateurs correspondant à un alias donné ;
* déconnexion des utilisateurs.

toobuild hello travail application complète, vous devez :

1. inscrire votre application auprès d’Azure AD ;
2. installer et configurer la bibliothèque ADAL ;
3. Utiliser des jetons tooget ADAL d’Azure AD.

tooget démarré, [télécharger squelette d’application hello](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) ou [télécharger l’exemple hello terminée](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).  Vous avez également besoin d’un client Azure AD dans lequel vous pouvez créer des utilisateurs et inscrire une application.  Si vous n’avez pas encore un client, [apprendre comment tooget un](active-directory-howto-tenant.md).

## <a name="1-register-hello-directorysearcher-application"></a>1. Inscrire hello DirectorySearcher Application
tooenable vos jetons tooget d’application, vous devez tout d’abord tooregister dans votre annuaire Azure AD de client et de lui accorder hello de tooaccess d’autorisation Azure AD Graph API :

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Sur la barre supérieure de hello, cliquez sur votre compte et sous hello **répertoire** , sélectionnez le client Active Directory de hello où vous souhaitez tooregister votre application.
3. Cliquez sur **plus Services** dans hello de navigation de gauche, puis choisissez **Azure Active Directory**.
4. Cliquez sur **Inscriptions des applications**, puis sur **Ajouter**.
5. Suivez les invites hello et créer un nouveau **Application cliente Native**.
  * Hello **nom** Hello application décrivent tooend-utilisateurs de votre application
  * Hello **Uri de redirection** est une combinaison de schéma et de la chaîne que Azure AD utilise des réponses de jeton tooreturn.  Entrez une application tooyour spécifique de la valeur, par exemple, `http://DirectorySearcher`.
6. Une fois l’inscription terminée, AAD affecte un ID d’application unique à votre application.  Vous aurez besoin de cette valeur dans les sections suivantes hello, par conséquent, copiez-le à partir de la page de l’application hello.
7. À partir de hello **paramètres** choisissez **autorisations requises** et choisissez **ajouter**. Sélectionnez hello **Microsoft Graph** comme hello API et ajouter hello **les données d’annuaire en lecture** autorisation sous **autorisations déléguées**.  Cette opération activera votre hello de tooquery d’application API Graph pour les utilisateurs.

## <a name="2-install--configure-adal"></a>2. Installez et configurez ADAL
Maintenant que vous disposez d’une application dans Azure AD, vous pouvez installer la bibliothèque ADAL et écrire votre code lié à l’identité.  Toocommunicate en mesure de toobe ADAL avec Azure AD, vous devez tooprovide avec des informations sur l’inscription de votre application.

* Commencez par ajouter le projet de DirectorySearcher toohello ADAL à l’aide de la Console du Gestionnaire de Package de hello.

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* Dans le projet de DirectorySearcher hello, ouvrez `app.config`.  Remplacez les valeurs hello d’éléments hello Bonjour `<appSettings>` hello tooreflect de section les valeurs d’entrée en hello portail Azure.  Votre code se réfère à ces valeurs chaque fois qu’il utilise la bibliothèque ADAL.
  * Hello `ida:Tenant` est domaine hello de votre client Azure AD, par exemple, contoso.onmicrosoft.com
  * Hello `ida:ClientId` est clientId hello de votre application que vous avez copié à partir du portail de hello.
  * Hello `ida:RedirectUri` est hello rediriger l’url que vous avez enregistré dans le portail de hello.

## <a name="3----use-adal-tooget-tokens-from-aad"></a>3.    Utiliser des jetons tooGet ADAL d’AAD
Bonjour principe de base derrière la bibliothèque ADAL est que chaque fois que votre application a besoin d’un jeton d’accès, il appelle simplement `authContext.AcquireTokenAsync(...)`, et la bibliothèque ADAL hello rest.  

* Bonjour `DirectorySearcher` projet, ouvrez `MainWindow.xaml.cs` et recherchez hello `MainWindow()` (méthode).  première étape de Hello est tooinitialize de votre application `AuthenticationContext` -ADAL de la classe principale.  Il s’agit d’où vous passez la bibliothèque ADAL hello coordonnées nécessaires toocommunicate avec Azure AD et d’indiquer comment les jetons toocache.

```C#
public MainWindow()
{
    InitializeComponent();

    authContext = new AuthenticationContext(authority, new FileCache());

    CheckForCachedToken();
}
```

* Maintenant recherchez hello `Search(...)` (méthode), qui sera appelé lorsque hello utilisateur cliks hello « Rechercher » un bouton dans l’interface utilisateur de l’application hello.  Cette méthode rend un tooquery toohello API Azure AD Graph de demande GET pour les utilisateurs dont les UPN commence par hello donné du terme de recherche.  Mais dans hello tooquery de commande API Graph, vous devez tooinclude un access_token Bonjour `Authorization` en-tête Hello demande - il s’agit là qu’intervient la bibliothèque ADAL.

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    // Validate hello Input String
    if (string.IsNullOrEmpty(SearchText.Text))
    {
        MessageBox.Show("Please enter a value for hello tooDo item name");
        return;
    }

    // Get an Access Token for hello Graph API
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Auto));
        UserNameLabel.Content = result.UserInfo.DisplayableId;
        SignOutButton.Visibility = Visibility.Visible;
    }
    catch (AdalException ex)
    {
        // An unexpected error occurred, or user canceled hello sign in.
        if (ex.ErrorCode != "access_denied")
            MessageBox.Show(ex.Message);

        return;
    }

    ...
}
```
* Lorsque votre application demande un jeton en appelant `AcquireTokenAsync(...)`, la bibliothèque ADAL va tenter de tooreturn un jeton sans demander hello pour les informations d’identification.  Si la bibliothèque ADAL détermine que l’utilisateur hello doit toosign dans tooget un jeton, s’afficher une boîte de dialogue de connexion, collecter des informations d’identification de l’utilisateur hello et retourne un jeton après une authentification réussie.  Si la bibliothèque ADAL est impossible de tooreturn un jeton pour une raison quelconque, elle lève une `AdalException`.
* Notez que hello `AuthenticationResult` objet contient un `UserInfo` objet qui peut être informations toocollect utilisé votre application peut avoir besoin.  Bonjour DirectorySearcher, `UserInfo` est l’interface utilisateur de l’application de hello toocustomize utilisé avec l’id de l’utilisateur hello.
* Utilisateur de hello clique sur bouton « Déconnexion » hello, nous souhaitons tooensure qui hello prochain appel trop`AcquireTokenAsync(...)` demandera toosign d’utilisateur hello dans.  Avec la bibliothèque ADAL, il est aussi simple que l’effacement du cache de jetons hello :

```C#
private void SignOut(object sender = null, RoutedEventArgs args = null)
{
    // Clear hello token cache
    authContext.TokenCache.Clear();

    ...
}
```

* Toutefois, si l’utilisateur de hello ne cliquez pas sur bouton « Déconnexion » hello, vous pouvez toomaintain hello de session pour hello leur exécution suivante hello DirectorySearcher.  Lors de l’application hello démarre, vous pouvez vérifier le cache de jeton de la bibliothèque ADAL pour un jeton existant et mettre à jour de l’interface utilisateur de hello en conséquence.  Bonjour `CheckForCachedToken()` (méthode), effectuer un autre appel trop`AcquireTokenAsync(...)`, cette fois en passant hello `PromptBehavior.Never` paramètre.  `PromptBehavior.Never`Indique à la bibliothèque ADAL qu’utilisateur de hello ne doit pas être invité pour la connexion et la bibliothèque ADAL doit plutôt lever une exception s’il est impossible de tooreturn un jeton.

```C#
public async void CheckForCachedToken() 
{
    // As hello application starts, try tooget an access token without prompting hello user.  If one exists, show hello user as signed in.
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Never));
    }
    catch (AdalException ex)
    {
        if (ex.ErrorCode != "user_interaction_required")
        {
            // An unexpected error occurred.
            MessageBox.Show(ex.Message);
        }

        // If user interaction is required, proceed toomain page without singing hello user in.
        return;
    }

    // A valid token is in hello cache
    SignOutButton.Visibility = Visibility.Visible;
    UserNameLabel.Content = result.UserInfo.DisplayableId;
}
```

Félicitations ! Vous avez une application WPF .NET qui a des utilisateurs tooauthenticate hello capacité, en toute sécurité appelez des API Web à l’aide d’OAuth 2.0 et obtenez des informations de base sur l’utilisateur de hello.  Si vous n’avez pas encore, est à présent hello temps toopopulate votre locataire avec certains utilisateurs.  Exécutez votre application DirectorySearcher et connectez-vous avec l’un de ces utilisateurs.  Recherchez d’autres utilisateurs en fonction de leur UPN.  Fermez l’application hello et réexécutez-la.  Notez que la session de l’utilisateur hello reste intacte.  Déconnectez-vous et reconnectez-vous sous le nom d’un autre utilisateur.

ADAL rend facile tooincorporate toutes ces fonctionnalités d’identité commune dans votre application.  Il s’occupe de tout le travail dirty hello vous - gestion du cache, la prise en charge de protocole d’OAuth, présentant les utilisateur hello avec une connexion de l’interface utilisateur, l’actualisation des jetons expirés et bien plus encore.  Vous devez vraiment tooknow est un simple appel d’API `authContext.AcquireTokenAsync(...)`.

Pour référence, exemple hello terminée (sans les valeurs de configuration) est fourni [ici](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).  Vous pouvez maintenant déplacer sur les scénarios de tooadditional.  Vous souhaiterez peut-être tootry :

[Sécurisation d’une API web .NET avec Azure AD &gt;&gt;](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

