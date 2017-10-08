---
title: aaaAzure Active Directory B2C | Documents Microsoft
description: "Comment toobuild une application de bureau Windows qui inclut la connexion, d’inscription et gestion de profil à l’aide d’Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 9da14362-8216-4485-960e-af17cd5ba3bd
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.openlocfilehash: f22b0299ff74bfba2f3fea88f006da609859dda5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-build-a-windows-desktop-app"></a>Azure AD B2C : création d’une application de bureau Windows
À l’aide de B2C d’Azure Active Directory (Azure AD), vous pouvez ajouter des identités en libre-service puissantes fonctionnalités tooyour bureau application de gestion dans quelques étapes. Cet article vous indiquent comment toocreate une application .NET Windows Presentation Foundation (WPF) « liste de tâches » qui inclut l’utilisateur d’abonnement, connectez-vous et la gestion de profil. application Hello inclut la prise en charge pour l’inscription et connectez-vous à l’aide d’un nom d’utilisateur ou un e-mail. Elle prendra également en charge l’inscription et la connexion à l’aide d’un compte de réseau social comme Facebook et Google.

## <a name="get-an-azure-ad-b2c-directory"></a>Obtention d'un répertoire Azure AD B2C
Avant de pouvoir utiliser Azure AD B2C, vous devez créer un répertoire ou un client.  Un répertoire est un conteneur destiné à recevoir tous vos utilisateurs, applications, groupes, etc. Si vous n’en possédez pas déjà un, [créez un répertoire B2C](active-directory-b2c-get-started.md) avant d’aller plus loin dans ce guide.

## <a name="create-an-application"></a>Création d'une application
Ensuite, vous devez toocreate une application dans votre répertoire B2C. Cela fournit des informations AD Azure qu’il a besoin toosecurely communiquer avec votre application. toocreate une application, procédez comme [ces instructions](active-directory-b2c-app-registration.md).  Veillez à effectuer les opérations suivantes :

* Inclure un **native client** dans l’application hello.
* Hello de copie **URI de redirection** `urn:ietf:wg:oauth:2.0:oob`. Il s’agit d’URL par défaut de hello pour cet exemple de code.
* Hello de copie **ID d’Application** qui est attribué tooyour application. Vous en aurez besoin ultérieurement.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Création de vos stratégies
Dans Azure AD B2C, chaque expérience utilisateur est définie par une [stratégie](active-directory-b2c-reference-policies.md). Cet exemple de code contient trois expériences liées à l’identité : l’inscription, la connexion et la modification du profil. Vous devez toocreate une stratégie pour chaque type, comme décrit dans la [article de référence de stratégie](active-directory-b2c-reference-policies.md#create-a-sign-up-policy). Lorsque vous créez trois stratégies de hello, veillez à :

* Choisissez **ID d’utilisateur d’abonnement** ou **par courrier électronique d’abonnement** dans le panneau de fournisseurs d’identité hello.
* Choisir **Nom d’affichage** et d’autres attributs d’inscription dans votre stratégie d’inscription.
* Choisir les revendications **Nom d’affichage** et **ID d’objet** comme revendications d’application pour chaque stratégie. Vous pouvez aussi choisir d'autres revendications.
* Hello de copie **nom** de chaque stratégie après l’avoir créée. Il doit avoir le préfixe de hello `b2c_1_`.  Vous aurez besoin des noms de ces stratégies ultérieurement.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Une fois que vous avez créé hello trois stratégies, vous êtes prêt toobuild votre application.

## <a name="download-hello-code"></a>Télécharger le code de hello
Hello du code pour ce didacticiel [est conservée sur GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet). exemple de hello toobuild en tant que vous accédez, vous pouvez [télécharger un projet sous forme de fichier .zip de squelette](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip). Vous pouvez également dupliquer le squelette de hello :

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git
```

application Hello terminée est également [disponible sous forme de fichier .zip](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) ou sur hello `complete` branche Hello même référentiel.

Après avoir téléchargé l’exemple de code hello, ouvrez hello tooget du fichier .sln de Visual Studio a démarré. Hello `TaskClient` projet est hello application de bureau WPF hello utilisateur interagit avec. Pour des raisons de hello de ce didacticiel, il appelle une tâche de back-end API web, hébergé dans Azure, qui stocke la liste des actions de chaque utilisateur.  Vous n’avez pas besoin de toobuild hello web API, nous avons déjà qu’il est en cours d’exécution pour vous.

toolearn comment une API web authentifie en toute sécurité les requêtes à l’aide d’Azure AD B2C, consultez le [API web mise en route article](active-directory-b2c-devquickstarts-api-dotnet.md).

## <a name="execute-policies"></a>Exécuter des stratégies
Votre application communique avec Azure AD B2C en envoyant des messages d’authentification qui spécifient la stratégie hello qu’ils souhaitent tooexecute dans le cadre de la demande de hello HTTP. Pour les applications de bureau .NET, vous pouvez utiliser hello afficher un aperçu des messages d’authentification de bibliothèque d’authentification Microsoft (MSAL) toosend OAuth 2.0, exécution des stratégies et obtenir des jetons qui appellent des API web.

### <a name="install-msal"></a>Installation de la bibliothèque MSAL
Ajouter MSAL toohello `TaskClient` projet à l’aide de hello Console du Gestionnaire de Package Visual Studio.

```
PM> Install-Package Microsoft.Identity.Client -IncludePrerelease
```

### <a name="enter-your-b2c-details"></a>saisissez les informations B2C
Les fichiers ouverts hello `Globals.cs` et chacune des valeurs de propriété hello remplacer par les vôtres. Cette classe est utilisée tout au long de `TaskClient` les valeurs tooreference couramment utilisée.

```C#
public static class Globals
{
    ...

    // TODO: Replace these five default with your own configuration values
    public static string tenant = "fabrikamb2c.onmicrosoft.com";
    public static string clientId = "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6";
    public static string signInPolicy = "b2c_1_sign_in";
    public static string signUpPolicy = "b2c_1_sign_up";
    public static string editProfilePolicy = "b2c_1_edit_profile";

    ...
}
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="create-hello-publicclientapplication"></a>Créer hello PublicClientApplication
Hello la classe principale de MSAL est `PublicClientApplication`. Cette classe représente votre application dans le système de hello Azure Active Directory B2C. Lorsque hello initialise de l’application, créez une instance de `PublicClientApplication` dans `MainWindow.xaml.cs`. Cela peut être utilisé dans la fenêtre hello.

```C#
protected async override void OnInitialized(EventArgs e)
{
    base.OnInitialized(e);

    pca = new PublicClientApplication(Globals.clientId)
    {
        // MSAL implements an in-memory cache by default.  Since we want tokens toopersist when hello user closes hello app,
        // we've extended hello MSAL TokenCache and created a simple FileCache in this app.
        UserTokenCache = new FileCache(),
    };

    ...
```

### <a name="initiate-a-sign-up-flow"></a>Lancement d’un flux d'inscription
Lorsqu’un utilisateur choisit toosigns haut, vous souhaitez tooinitiate un flux d’abonnement qui utilise la stratégie d’inscription de hello que vous avez créé. À l’aide de la bibliothèque MSAL, il vous suffit d’appeler `pca.AcquireTokenAsync(...)`. Hello les paramètres que vous transmettez trop`AcquireTokenAsync(...)` déterminer quel jeton vous recevez, stratégie de hello utilisée dans la demande d’authentification hello et bien plus encore.

```C#
private async void SignUp(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        // Use hello app's clientId here as hello scope parameter, indicating that
        // you want a token toohello your app's backend web API (represented by
        // hello cloud hosted task API).  Use hello UiOptions.ForceLogin flag to
        // indicate tooMSAL that it should show a sign-up UI no matter what.
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                Globals.signUpPolicy);

        // Upon success, indicate in hello app that hello user is signed in.
        SignInButton.Visibility = Visibility.Collapsed;
        SignUpButton.Visibility = Visibility.Collapsed;
        EditProfileButton.Visibility = Visibility.Visible;
        SignOutButton.Visibility = Visibility.Visible;

        // When hello request completes successfully, you can get user
        // information from hello AuthenticationResult
        UsernameLabel.Content = result.User.Name;

        // After hello sign up successfully completes, display hello user's To-Do List
        GetTodoList();
    }

    // Handle any exeptions that occurred during execution of hello policy.
    catch (MsalException ex)
    {
        if (ex.ErrorCode != "authentication_canceled")
        {
            // An unexpected error occurred.
            string message = ex.Message;
            if (ex.InnerException != null)
            {
                message += "Inner Exception : " + ex.InnerException.Message;
            }

            MessageBox.Show(message);
        }

        return;
    }
}
```

### <a name="initiate-a-sign-in-flow"></a>Lancement d’un flux de connexion
Vous pouvez lancer un flux de connexion Bonjour même façon que vous lancez un flux d’inscription. Lorsqu’un utilisateur se connecte, rendre hello même appeler tooMSAL, cette fois à l’aide de votre stratégie d’authentification :

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
    AuthenticationResult result = null;
    try
    {
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                    string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                    Globals.signInPolicy);
        ...
```

### <a name="initiate-an-edit-profile-flow"></a>Lancement d’un flux de modification de profil
Là encore, vous pouvez exécuter une stratégie de modifier le profil Bonjour même manière :

```C#
private async void EditProfile(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                    string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                    Globals.editProfilePolicy);
```

Dans tous ces cas, la bibliothèque MSAL retourne un jeton dans `AuthenticationResult` ou lève une exception. Chaque fois que vous obtenez un jeton à partir de MSAL, vous pouvez utiliser hello `AuthenticationResult.User` tooupdate hello données utilisateur contenues dans application hello, par exemple hello l’interface utilisateur de l’objet. La bibliothèque ADAL également les caches hello jeton pour l’utiliser dans d’autres parties de l’application hello.

### <a name="check-for-tokens-on-app-start"></a>Vérification des jetons sur le démarrage de l’application
Vous pouvez également utiliser le suivi de tookeep MSAL de l’état de connexion de l’utilisateur hello.  Dans cette application, nous souhaitons hello utilisateur tooremain est signé le même après leur fermer l’application hello et ouvrez à nouveau.  Retour à l’intérieur de hello `OnInitialized` remplacer, utilisez de MSAL `AcquireTokenSilent` toocheck de méthode pour les jetons mis en cache :

```C#
AuthenticationResult result = null;
try
{
    // If hello user has has a token cached with any policy, we'll display them as signed-in.
    TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
    string existingPolicy = tci == null ? null : tci.Policy;
    result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    SignInButton.Visibility = Visibility.Collapsed;
    SignUpButton.Visibility = Visibility.Collapsed;
    EditProfileButton.Visibility = Visibility.Visible;
    SignOutButton.Visibility = Visibility.Visible;
    UsernameLabel.Content = result.User.Name;
    GetTodoList();
}
catch (MsalException ex)
{
    if (ex.ErrorCode == "failed_to_acquire_token_silently")
    {
        // There are no tokens in hello cache.  Proceed without calling hello tooDo list service.
    }
    else
    {
        // An unexpected error occurred.
        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }
        MessageBox.Show(message);
    }
    return;
}
```

## <a name="call-hello-task-api"></a>Appeler des API de tâche hello
Vous avez utilisé stratégies de tooexecute MSAL et obtenez des jetons.  Lorsque vous souhaitez toouse une ces API de tâche de jetons toocall hello, vous pouvez réutiliser du MSAL `AcquireTokenSilent` toocheck de méthode pour les jetons mis en cache :

```C#
private async void GetTodoList()
{
    AuthenticationResult result = null;
    try
    {
        // Here we want toocheck for a cached token, independent of whatever policy was used tooacquire it.
        TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
        string existingPolicy = tci == null ? null : tci.Policy;

        // Use AcquireTokenSilent tooindicate that MSAL should throw an exception if a token cannot be acquired
        result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    }
    // If a token could not be acquired silently, we'll catch hello exception and show hello user a message.
    catch (MsalException ex)
    {
        // There is no access token in hello cache, so prompt hello user toosign-in.
        if (ex.ErrorCode == "failed_to_acquire_token_silently")
        {
            MessageBox.Show("Please sign up or sign in first");
            SignInButton.Visibility = Visibility.Visible;
            SignUpButton.Visibility = Visibility.Visible;
            EditProfileButton.Visibility = Visibility.Collapsed;
            SignOutButton.Visibility = Visibility.Collapsed;
            UsernameLabel.Content = string.Empty;
        }
        else
        {
            // An unexpected error occurred.
            string message = ex.Message;
            if (ex.InnerException != null)
            {
                message += "Inner Exception : " + ex.InnerException.Message;
            }
            MessageBox.Show(message);
        }

        return;
    }
    ...
```

Lorsque de trop hello appel`AcquireTokenSilentAsync(...)` réussit et un jeton est trouvé dans le cache de hello, vous pouvez ajouter toohello de jeton hello `Authorization` en-tête de demande de hello HTTP. API web de tâche Hello utilisera la liste de tâches en-tête tooauthenticate hello demande tooread hello de cet utilisateur :

```C#
    ...
    // Once hello token has been returned by MSAL, add it toohello http authorization header, before making hello call tooaccess hello tooDo list service.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);

    // Call hello tooDo list service.
    HttpResponseMessage response = await httpClient.GetAsync(Globals.taskServiceUrl + "/api/tasks");
    ...
```

## <a name="sign-hello-user-out"></a>Utilisateur de hello signe out
Enfin, vous pouvez utiliser MSAL tooend une session de l’utilisateur avec l’application hello lorsque hello utilisateur sélectionne **se déconnecter**.  Lorsque vous utilisez MSAL, cela s’effectue en effaçant tous les jetons hello à partir du cache de jetons hello de :

```C#
private void SignOut(object sender, RoutedEventArgs e)
{
    // Clear any remnants of hello user's session.
    pca.UserTokenCache.Clear(Globals.clientId);

    // This is a helper method that clears browser cookies in hello browser control that MSAL uses, it is not part of MSAL.
    ClearCookies();

    // Update hello UI tooshow hello user as signed out.
    TaskList.ItemsSource = string.Empty;
    SignInButton.Visibility = Visibility.Visible;
    SignUpButton.Visibility = Visibility.Visible;
    EditProfileButton.Visibility = Visibility.Collapsed;
    SignOutButton.Visibility = Visibility.Collapsed;
    return;
}
```

## <a name="run-hello-sample-app"></a>Exécutez l’exemple d’application hello
Enfin, générez et exécutez l’exemple hello.  Inscrivez-vous pour une application hello à l’aide d’un nom d’utilisateur ou une adresse de messagerie. Se déconnecter et reconnecter en tant que hello même utilisateur. Modifiez le profil de cet utilisateur. Déconnectez-vous et connectez-vous en utilisant un utilisateur différent.

## <a name="add-social-idps"></a>Ajout d’IDP sociaux
Actuellement, application hello prend en charge uniquement inscription de l’utilisateur et de connexion qui utilisent **comptes locaux**. Il s’agit de comptes stockés dans votre répertoire B2C qui utilisent un nom d’utilisateur et un mot de passe. Avec Azure AD B2C, vous pouvez ajouter la prise en charge d’autres fournisseurs d’identité sans modifier votre code.

tooadd sociaux IDPs tooyour application, commencez par suivre hello des instructions dans ces articles. Pour chaque IDP vous toosupport, vous devez tooregister une application de ce système et obtenez un ID client.

* [Définir Facebook en tant qu’IDP](active-directory-b2c-setup-fb-app.md)
* [Définir Google en tant qu’IDP](active-directory-b2c-setup-goog-app.md)
* [Définir Amazon en tant qu’IDP](active-directory-b2c-setup-amzn-app.md)
* [Définir LinkedIn en tant qu’IDP](active-directory-b2c-setup-li-app.md)

Après avoir ajouté le répertoire de tooyour B2C hello identité fournisseurs, vous devez tooedit chacun de vos trois stratégies tooinclude hello IDPs nouveau, comme décrit dans hello [article de référence de stratégie](active-directory-b2c-reference-policies.md). Après avoir enregistré vos stratégies, exécutez à nouveau application hello. Vous devez voir hello Qu'idps nouveau ajoutés en tant qu’options de connexion et d’inscription dans chacun de vos expériences d’identité.

Vous pouvez faire des essais avec vos stratégies et observer les effets de hello sur votre exemple d’application. Ajoutez ou supprimez des fournisseurs d’identité, manipulez des revendications d’application ou modifiez des attributs d’inscription. Faites des essais jusqu’à ce que vous compreniez la façon dont les stratégies, les demandes d’authentification et la bibliothèque MSAL sont liées.

Pour référence, hello effectuée exemple [est fournie comme un fichier .zip](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip). Vous pouvez également le cloner à partir de GitHub :

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git```
