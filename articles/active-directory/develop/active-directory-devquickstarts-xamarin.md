---
title: aaaAzure AD Xamarin prise en main | Documents Microsoft
description: "Créez des applications Xamarin qui s’intègrent avec Azure AD pour la connexion et appellent des API protégées par Azure AD en utilisant OAuth."
services: active-directory
documentationcenter: xamarin
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 198cd2c3-f7c8-4ec2-b59d-dfdea9fe7d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 6a0d189648b7071558ac1cf2b908808668960a4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-xamarin-apps"></a>Intégrer Azure AD avec des applications Xamarin
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Avec Xamarin, vous pouvez écrire des applications mobiles en C# qui peuvent s’exécuter sous iOS, Android et Windows (appareils mobiles et PC). Si vous créez une application à l’aide de Xamarin, Azure Active Directory (Azure AD) rend tooauthenticate simple des utilisateurs avec leurs comptes Azure AD. application Hello peut consommer également en toute sécurité les API web qui est protégé par Azure AD, par exemple hello API Office 365 ou hello API Azure.

Pour les applications Xamarin ont besoin de ressources de tooaccess protégé, Azure AD fournit hello Active Directory Authentication Library (ADAL). Hello seul but de la bibliothèque ADAL est toomake plus facile pour les jetons d’accès aux applications tooget. toodemonstrate facilement est, cet article explique comment les applications DirectorySearcher toobuild qui :

* exécution sous iOS, Android, Windows Desktop, Windows Phone et Windows Store ;
* Utiliser une seule classe portable bibliothèque (PCL) tooauthenticate utilisateurs et obtenir des jetons pour hello API Azure AD Graph.
* recherche, dans un annuaire, d’utilisateurs correspondant à un UPN (nom d’utilisateur principal) donné.

## <a name="before-you-get-started"></a>Avant de commencer
* Télécharger hello [projet squelette](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip), ou télécharger hello [exemple terminé](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip). Chaque téléchargement est une solution Visual Studio 2013.
* Vous devez également un locataire Azure AD dans lequel les utilisateurs de toocreate et inscrire l’application hello. Si vous n’avez pas encore un client, [apprendre comment tooget un](active-directory-howto-tenant.md).

Lorsque vous êtes prêt, suivez les procédures de hello dans hello quatre sections.

## <a name="step-1-set-up-your-xamarin-development-environment"></a>Étape 1 : Configurer votre environnement de développement Xamarin
Étant donné que ce didacticiel inclut des projets pour iOS, Android et Windows, il vous faut à la fois Visual Studio et Xamarin. environnement nécessaires de toocreate hello, processus hello complète dans [définir configurer et installer Visual Studio et Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) sur MSDN. instructions de Hello incluent des documents que vous pouvez consulter toolearn plus sur Xamarin pendant que vous patientez pour hello installations toobe est terminée.

Après avoir terminé le programme d’installation Bonjour, ouvrir la solution de hello dans Visual Studio. Vous y trouverez six projets : cinq projets propres à la plateforme et une PCL, DirectorySearcher.cs, partagée par toutes les plateformes.

## <a name="step-2-register-hello-directorysearcher-app"></a>Étape 2 : Inscrire l’application DirectorySearcher hello
jetons de tooget tooenable hello application, vous devez tout d’abord tooregister dans votre annuaire Azure AD de client et de lui accorder hello de tooaccess autorisation API Azure AD Graph. Voici comment procéder :

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Sur la barre supérieure de hello, cliquez sur votre compte. Ensuite, sous hello **répertoire** liste, le client d’Active Directory hello sélectionnez où vous souhaitez tooregister hello application.
3. Cliquez sur **plus Services** dans hello du volet gauche, puis sélectionnez **Azure Active Directory**.
4. Cliquez sur **Inscriptions des applications**, puis sélectionnez **Ajouter**.
5. toocreate un nouveau **Application cliente Native**, suivez les invites hello.
  * **Nom** décrit hello application toousers.
  * **URI de redirection** est une combinaison de schéma et de la chaîne que Azure AD utilise des réponses de jeton tooreturn. Entrez une valeur (par exemple, http://DirectorySearcher).
6. Une fois que vous avez terminé l’inscription, Azure AD assigne application hello un ID d’application unique. Copier la valeur de hello de hello **Application** sous l’onglet, car vous en aurez besoin ultérieurement.
7. Sur hello **paramètres** page, sélectionnez **autorisations requises**, puis sélectionnez **ajouter**.
8. Sélectionnez **Microsoft Graph** comme hello API. Sous **autorisations déléguées**, ajouter hello **les données d’annuaire en lecture** autorisation.  
Cette action active tooquery hello API Graph de hello application pour les utilisateurs.

## <a name="step-3-install-and-configure-adal"></a>Étape 3 : Installer et configurer la bibliothèque ADAL
Maintenant que vous disposez d’une application dans Azure AD, vous pouvez installer la bibliothèque ADAL et écrire votre code lié à l’identité. tooenable toocommunicate ADAL avec Azure AD, lui donner des informations sur l’inscription d’une application hello.

1. Ajouter la bibliothèque ADAL toohello DirectorySearcher projet à l’aide de hello Console du Gestionnaire de Package.

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirectorySearcherLib
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Android
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Desktop
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-iOS
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Universal
    `

    Notez que les deux références de bibliothèque sont ajoutées tooeach projet : hello PCL partie ADAL et une partie spécifique à la plateforme.
2. Dans le projet de DirectorySearcherLib hello, ouvrez DirectorySearcher.cs.
3. Remplacez les valeurs de membre de classe hello avec des valeurs hello que vous avez entré dans hello portail Azure. Votre code fait référence à des valeurs de toothese chaque fois qu’il utilise la bibliothèque ADAL.

  * Hello *client* est domaine hello de votre client Azure AD (par exemple, contoso.onmicrosoft.com).
  * Hello *clientId* est l’ID de client hello de l’application hello, que vous avez copié à partir du portail de hello.
  * Hello *returnUri* est l’URI que vous avez entré dans le portail hello (par exemple, http://DirectorySearcher) de la redirection hello.

## <a name="step-4-use-adal-tooget-tokens-from-azure-ad"></a>Étape 4 : Utiliser la bibliothèque ADAL tooget des jetons d’Azure AD
Quasi-totalité de la logique d’authentification de l’application hello se trouve `DirectorySearcher.SearchByAlias(...)`. Tout ce qui est nécessaire dans les projets spécifiques à une plateforme hello est toopass un toohello paramètre contextuelles `DirectorySearcher` PCL.

1. Ouvrez DirectorySearcher.cs et ajoutez un nouveau toohello de paramètre `SearchByAlias(...)` (méthode). `IPlatformParameters`est l’authentification ADAL besoins tooperform hello des objets de paramètre hello contextuelles qui encapsule hello spécifique à la plateforme.

    ```C#
    public static async Task<List<User>> SearchByAlias(string alias, IPlatformParameters parent)
    {
    ```

2. Initialiser `AuthenticationContext`, qui est la classe principale hello de la bibliothèque ADAL.  
Cette hello ADAL de passes action il coordonne toocommunicate besoins avec Azure AD.
3. Appelez `AcquireTokenAsync(...)`, qui accepte hello `IPlatformParameters` de l’objet et appelle les flux d’authentification hello sont nécessaire tooreturn une application toohello de jeton.

    ```C#
    ...
        AuthenticationResult authResult = null;
        try
        {
            AuthenticationContext authContext = new AuthenticationContext(authority);
            authResult = await authContext.AcquireTokenAsync(graphResourceUri, clientId, returnUri, parent);
        }
        catch (Exception ee)
        {
            results.Add(new User { error = ee.Message });
            return results;
        }
    ...
    ```

    `AcquireTokenAsync(...)`première tentatives tooreturn un jeton pour hello la ressource (hello API Graph dans ce cas) demandée sans invite les utilisateurs tooenter leurs informations d’identification (via la mise en cache ou l’actualisation des jetons ancien). Si nécessaire, il affiche les utilisateurs hello Azure AD-page de connexion avant d’acquérir le jeton demandé de hello.
4. Attacher la demande d’API Graph hello accès toohello jeton Bonjour **autorisation** en-tête :

    ```C#
    ...
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", authResult.AccessToken);
    ...
    ```

C’est pourquoi `DirectorySearcher` le code de bibliothèque de classes portables et hello application associées à l’identité. Il ne reste que toocall hello `SearchByAlias(...)` méthode dans les vues de chaque plateforme et, le cas échéant, le code tooadd pour gérer correctement hello cycle de vie de l’interface utilisateur.

### <a name="android"></a>Android
1. Dans MainActivity.cs, ajoutez un appel trop`SearchByAlias(...)` du bouton hello Gestionnaire click :

    ```C#
    List<User> results = await DirectorySearcher.SearchByAlias(searchTermText.Text, new PlatformParameters(this));
    ```
2. Remplacer hello `OnActivityResult` tooforward de méthode du cycle de vie d’authentification redirige la méthode appropriée de toohello précédent. La bibliothèque ADAL fournit une méthode d’assistance pour cela dans Android :

    ```C#
    ...
    protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
    {
        base.OnActivityResult(requestCode, resultCode, data);
        AuthenticationAgentContinuationHelper.SetAuthenticationAgentContinuationEventArgs(requestCode, resultCode, data);
    }
    ...
    ```

### <a name="windows-desktop"></a>Windows Desktop
Dans MainWindow.xaml.cs, effectuez un appel trop`SearchByAlias(...)` en passant un `WindowInteropHelper` dans desktop hello `PlatformParameters` objet :

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

#### <a name="ios"></a>iOS
Dans DirSearchClient_iOSViewController.cs, hello iOS `PlatformParameters` objet prend un toohello référence View Controller :

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

### <a name="windows-universal"></a>Windows Universal
Dans l’application Windows universelle, ouvrez MainPage.xaml.cs et implémentez hello `Search` (méthode). Cette méthode utilise une méthode d’assistance dans une interface utilisateur de tooupdate projet partagé si nécessaire.

```C#
...
List<User> results = await DirectorySearcherLib.DirectorySearcher.SearchByAlias(SearchTermText.Text, new PlatformParameters(PromptBehavior.Auto, false));
...
```

## <a name="whats-next"></a>Étapes suivantes
Vous disposez maintenant d’une application Xamarin fonctionnelle capable d’authentifier les utilisateurs et d’appeler en toute sécurité les API web à l’aide d’OAuth 2.0 sur cinq plateformes différentes.

Si vous n’avez pas déjà renseigné votre client avec les utilisateurs, est à présent hello temps toodo donc.

1. Exécuter votre application DirectorySearcher, puis connectez-vous avec l’un des utilisateurs de hello.
2. Recherchez d’autres utilisateurs en fonction de leur UPN.

La bibliothèque ADAL facilite fonctionnalités d’identité commune tooincorporate facile dans une application hello. Il s’occupe de tout le travail dirty hello, telles que la gestion du cache, prise en charge de protocole d’OAuth, présentant les utilisateur hello avec une connexion de l’interface utilisateur, et l’actualisation a expiré de jetons. Vous devez tooknow uniquement une seule API appel, `authContext.AcquireToken*(…)`.

Pour référence, téléchargez hello [exemple terminé](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip) (sans les valeurs de configuration).

Vous pouvez maintenant déplacer sur les scénarios d’identité tooadditional. Par exemple, essayez de [Sécuriser une API web .NET avec Azure AD](active-directory-devquickstarts-webapi-dotnet.md).

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
