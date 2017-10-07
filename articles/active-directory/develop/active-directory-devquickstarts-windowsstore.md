---
title: aaaAzure AD du Windows Store prise en main | Documents Microsoft
description: "Créez des applications Windows Store qui s’intègrent avec Azure AD pour la connexion et appellent des API protégées par Azure AD en utilisant OAuth."
services: active-directory
documentationcenter: windows
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 3b96a6d1-270b-4ac1-b9b5-58070c896a68
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 09/16/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 1d12c7b928bc0e94fb823f8db4a09ff416205e2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-windows-store-apps"></a>Intégration d’Azure AD avec des applications Windows Store
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> Les projets du Windows Store 8.1 et des versions antérieures ne sont pas pris en charge dans Visual Studio 2017.  Pour en savoir plus, consultez [Plateforme cible et compatibilité dans Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).

Si vous développez des applications pour hello du Windows Store, Azure Active Directory (Azure AD) rend très simple tooauthenticate vos utilisateurs avec leurs comptes Active Directory. En intégrant avec Azure AD, une application peut utiliser en toute sécurité de toutes les API qui est protégé par Azure AD, telles que hello API Office 365 ou hello Azure API web.

Pour les applications bureautiques Windows Store qui ont besoin de ressources de tooaccess protégé, Azure AD fournit hello Active Directory Authentication Library (ADAL). Hello seul but de la bibliothèque ADAL est toomake plus facile pour les jetons d’accès tooget application hello. toodemonstrate il s’agit, cet article explique comment toobuild un DirectorySearcher Windows Store facilement application qui :

* Obtient les jetons pour l’appel d’API d’Azure AD Graph hello à l’aide de hello d’accès [protocole d’authentification OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* recherche, dans un répertoire, d’utilisateurs correspondant à un nom d’utilisateur principal (UPN) donné ;
* déconnexion des utilisateurs.

## <a name="before-you-get-started"></a>Avant de commencer
* Télécharger hello [projet squelette](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip), ou télécharger hello [exemple terminé](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip). Chaque téléchargement est une solution Visual Studio 2015.
* Vous devez également un locataire Azure AD dans lequel les utilisateurs de toocreate et inscrire l’application hello. Si vous n’avez pas encore un client, [apprendre comment tooget un](active-directory-howto-tenant.md).

Lorsque vous êtes prêt, suivez les procédures de hello dans hello trois sections suivantes.

## <a name="step-1-register-hello-directorysearcher-app"></a>Étape 1 : Inscrire l’application DirectorySearcher hello
jetons de tooget tooenable hello application, vous devez tout d’abord tooregister dans votre annuaire Azure AD de client et de lui accorder hello de tooaccess autorisation API Azure AD Graph. Voici comment procéder :

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Sur la barre supérieure de hello, cliquez sur votre compte. Ensuite, sous hello **répertoire** liste, le client d’Active Directory hello sélectionnez où vous souhaitez tooregister hello application.
3. Cliquez sur **plus Services** dans hello du volet gauche, puis sélectionnez **Azure Active Directory**.
4. Cliquez sur **Inscriptions des applications**, puis sélectionnez **Ajouter**.
5. Suivez hello invites toocreate un **Application cliente Native**.
  * **Nom** décrit hello application toousers.
  * **URI de redirection** est une combinaison de schéma et de la chaîne que Azure AD utilise des réponses de jeton tooreturn. Entrez une valeur d’espace réservé pour l’instant (par exemple, **http://DirectorySearcher**). Vous allez remplacer les valeur hello plus tard.
6. Une fois que vous avez terminé l’inscription de hello, Azure AD assigne application hello un ID d’application unique. Copier la valeur hello sur hello **Application** sous l’onglet, car vous en aurez besoin ultérieurement.
7. Sur hello **paramètres** page, sélectionnez **autorisations requises**, puis sélectionnez **ajouter**.
8. Pourquoi **Azure Active Directory** application, sélectionnez **Microsoft Graph** comme hello API.
9. Sous **autorisations déléguées**, ajouter hello **répertoire de hello Access en tant qu’utilisateur connecté hello** autorisation. Ainsi, tooquery hello API Graph de hello application pour les utilisateurs.

## <a name="step-2-install-and-configure-adal"></a>Étape 2 : Installer et configurer la bibliothèque ADAL
Maintenant que vous disposez d’une application dans Azure AD, vous pouvez installer la bibliothèque ADAL et écrire votre code lié à l’identité. tooenable toocommunicate ADAL avec Azure AD, lui donner des informations sur l’inscription d’une application hello.

1. Ajouter la bibliothèque ADAL toohello DirectorySearcher projet à l’aide de hello Console du Gestionnaire de Package.

    ```
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
    ```

2. Dans le projet de DirectorySearcher hello, ouvrez MainPage.xaml.cs.
3. Remplacez les valeurs de hello en hello **les valeurs de configuration** région avec des valeurs hello que vous avez entré dans hello portail Azure. Votre code fait référence à des valeurs de toothese chaque fois qu’il utilise la bibliothèque ADAL.
  * Hello *client* est domaine hello de votre client Azure AD (par exemple, contoso.onmicrosoft.com).
  * Hello *clientId* est l’ID de client hello de l’application hello, que vous avez copié à partir du portail de hello.
4. Vous devez maintenant URI de rappel toodiscover hello pour votre application du Windows Store. Définir un point d’arrêt sur cette ligne de hello `MainPage` méthode :
    ```
    redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
    ```
5. Générer la solution hello, s’assurer que toutes les références de package sont restaurés. Si tous les packages sont manquants, ouvrez le Gestionnaire de Package NuGet de hello et les restaurer.
6. Exécuter l’application hello et copiez la valeur hello `redirectUri` lorsque hello point d’arrêt. valeur de Hello doit ressembler à hello qui suit :

    ```
    ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
    ```

7. Retour sur hello **paramètres** onglet de l’application hello Bonjour portail Azure, ajoutez un **RedirectUri** avec hello précédant la valeur.  

## <a name="step-3-use-adal-tooget-tokens-from-azure-ad"></a>Étape 3 : Utiliser la bibliothèque ADAL tooget des jetons d’Azure AD
Bonjour principe de base derrière la bibliothèque ADAL est que chaque fois que l’application hello a besoin d’un jeton d’accès, il appelle simplement `authContext.AcquireToken(…)`, et la bibliothèque ADAL hello rest.  

1. Initialiser l’application hello `AuthenticationContext`, qui est la classe principale hello de la bibliothèque ADAL. Cette action transmet les coordonnées hello ADAL il doit toocommunicate avec Azure AD et d’indiquer comment les jetons toocache.

    ```C#
    public MainPage()
    {
        ...

        authContext = new AuthenticationContext(authority);
    }
    ```

2. Recherchez hello `Search(...)` (méthode), qui est appelé lorsque les utilisateurs cliquent sur hello **recherche** bouton sur l’interface utilisateur de l’application hello. Cette méthode rend un tooquery toohello API Azure AD Graph de demande get pour les utilisateurs dont les UPN commence par hello donné du terme de recherche. tooquery hello API Graph, inclure un jeton d’accès dans la demande hello **autorisation** en-tête. C’est là où la bibliothèque ADAL entre en jeu.

    ```C#
    private async void Search(object sender, RoutedEventArgs e)
    {
        ...
        AuthenticationResult result = null;
        try
        {
            result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectURI, new PlatformParameters(PromptBehavior.Auto, false));
        }
        catch (AdalException ex)
        {
            if (ex.ErrorCode != "authentication_canceled")
            {
                ShowAuthError(string.Format("If hello error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", ex.ErrorCode, ex.Message));
            }
            return;
        }
        ...
    }
    ```
    Lorsque application hello demande un jeton en appelant `AcquireTokenAsync(...)`, la bibliothèque ADAL tente tooreturn un jeton sans demander hello pour les informations d’identification. Si la bibliothèque ADAL détermine que l’utilisateur hello doit toosign dans tooget un jeton, il affiche une boîte de dialogue de connexion, collecte des informations d’identification de l’utilisateur hello et retourne un jeton après que l’authentification réussit. Si la bibliothèque ADAL est impossible de tooreturn un jeton pour une raison quelconque, hello *AuthenticationResult* état est une erreur.
3. Il est maintenant de jeton d’accès hello toouse temps que vous venez d’acquérir. Également dans hello `Search(...)` (méthode), joindre toohello de jeton hello demande d’obtention de l’API Graph Bonjour **autorisation** en-tête :

    ```C#
    // Add hello access token toohello Authorization header of hello call toohello Graph API, and call hello Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new HttpCredentialsHeaderValue("Bearer", result.AccessToken);

    ```
4. Vous pouvez utiliser hello `AuthenticationResult` toodisplay informations utilisateur hello dans l’application hello, par exemple hello ID de l’utilisateur de l’objet :

    ```C#
    // Update hello page UI toorepresent hello signed-in user
    ActiveUser.Text = result.UserInfo.DisplayableId;
    ```
5. Vous pouvez également utiliser la bibliothèque ADAL toosign des utilisateurs en dehors de l’application hello. Lorsque hello utilisateur clique sur hello **se déconnecter** bouton, assurez-vous qu’appel suivant hello trop`AcquireTokenAsync(...)` montre une vue de connexion. La bibliothèque ADAL, cette action est aussi simple que l’effacement du cache de jetons hello :

    ```C#
    private void SignOut()
    {
        // Clear session state from hello token cache.
        authContext.TokenCache.Clear();

        ...
    }
    ```

## <a name="whats-next"></a>Étapes suivantes
Vous disposez maintenant d’un application du Windows Store qui peut authentifier les utilisateurs, en toute sécurité appeler web API à l’aide d’OAuth 2.0 et obtenir des informations de base sur l’utilisateur de hello du travail.

Si vous n’avez pas déjà renseigné votre client avec les utilisateurs, est à présent hello temps toodo donc.
1. Exécuter votre application DirectorySearcher, puis connectez-vous avec l’un des utilisateurs de hello.
2. Recherchez d’autres utilisateurs en fonction de leur UPN.
3. Fermez l’application hello et réexécutez-le. Notez que la session de l’utilisateur hello reste intacte.
4. Se déconnecter en cliquant sur la barre inférieure de hello toodisplay et reconnectez-vous en tant qu’un autre utilisateur.

ADAL rend facile tooincorporate toutes ces fonctionnalités identité commune dans une application hello. Il s’occupe de tout le travail dirty hello, telles que la gestion du cache, prise en charge de protocole d’OAuth, présentant les utilisateur hello avec une connexion de l’interface utilisateur, et l’actualisation a expiré de jetons. Vous devez tooknow uniquement une seule API appel, `authContext.AcquireToken*(…)`.

Pour référence, téléchargez hello [exemple terminé](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (sans les valeurs de configuration).

Vous pouvez maintenant déplacer sur les scénarios d’identité tooadditional. Par exemple, essayez de [Sécuriser une API web .NET avec Azure AD](active-directory-devquickstarts-webapi-dotnet.md).

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
