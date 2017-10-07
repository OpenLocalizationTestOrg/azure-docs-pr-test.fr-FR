---
title: aaaAzure Active Directory v2.0 application Native .NET | Documents Microsoft
description: Comment toobuild une application native .NET qui connecte aux utilisateurs avec les deux Account personnel de Microsoft et comptes professionnels ou scolaires.
services: active-directory
documentationcenter: 
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 46d81e09-bad0-44ce-9026-881805976e72
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/30/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 9418eeba02b800feee5cb00219574eb16506f0a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooa-windows-desktop-app"></a>Ajouter une application de bureau Windows de connexion tooa
Avec le point de terminaison hello hello v2.0, vous pouvez ajouter rapidement des applications de bureau tooyour l’authentification avec prise en charge pour les deux comptes personnels de Microsoft et comptes professionnels ou scolaires.  Elle aussi Active toosecurely de votre application communiquer avec un service principal web api, ainsi que [hello Microsoft Graph](https://graph.microsoft.io) et quelques exemples de hello [les API Office 365 unifiée](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2).

> [!NOTE]
> Pas toutes les fonctionnalités et scénarios d’Azure Active Directory (AD) sont pris en charge par le point de terminaison hello v2.0.  toodetermine si vous devez utiliser le point de terminaison hello v2.0, en savoir plus sur [v2.0 limitations](active-directory-v2-limitations.md).
> 
> 

Pour [.NET des applications natives qui s’exécutent sur un appareil](active-directory-v2-flows.md#mobile-and-native-apps), Azure AD fournit hello bibliothèque d’authentification d’identité ou MSAL.  Seul but de MSAL vie est toomake tooget de votre application plus facilement des jetons pour appeler des services web.  toodemonstrate facilité il s’agit, ici nous allons construire une application de liste de tâches WPF .NET :

* Signes hello utilisateur dans & obtient accéder aux jetons à l’aide de hello [protocole d’authentification OAuth 2.0](active-directory-v2-protocols.md).
* appel sécurisé d’un service Web principal de liste de tâches, qui est également sécurisé par OAuth 2.0 ;
* Utilisateur se connecte hello out.

## <a name="download-sample-code"></a>Télécharger l’exemple de code
code Hello pour ce didacticiel est maintenue [sur GitHub](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet).  toofollow le long, vous pouvez [structure de l’application hello en tant qu’un fichier ZIP de téléchargement](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip) ou un clone hello squelette :

    git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git

application Hello terminée est fournie à des fin de hello de ce didacticiel également.

## <a name="register-an-app"></a>Inscription d’une application
Créez une application à l’adresse [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou suivez cette [procédure détaillée](active-directory-v2-app-registration.md).  Veillez à respecter les points suivants :

* Copie vers le bas hello **Id d’Application** affecté tooyour application, vous en aurez besoin plus rapidement.
* Ajouter hello **Mobile** plate-forme pour votre application.

## <a name="install--configure-msal"></a>Installation et configuration de la bibliothèque MSAL
Maintenant que vous disposez d’une application enregistrée auprès de Microsoft, vous pouvez installer la bibliothèque MSAL et écrire votre code associé aux identités.  Point de terminaison MSAL toobe toocommunicate en mesure de hello v2.0, vous devez tooprovide avec des informations sur l’inscription de votre application.

* Commencez par ajouter le projet de TodoListClient toohello MSAL à l’aide de la Console du Gestionnaire de Package de hello.

```
PM> Install-Package Microsoft.Identity.Client -ProjectName TodoListClient -IncludePrerelease
```

* Dans le projet de TodoListClient hello, ouvrez `app.config`.  Remplacez les valeurs hello d’éléments hello Bonjour `<appSettings>` hello tooreflect de section les valeurs d’entrée dans le portail de l’enregistrement d’application hello.  Votre code se réfère à ces valeurs chaque fois qu’il utilise la bibliothèque MSAL.
  
  * Hello `ida:ClientId` est hello **Id d’Application** de votre application que vous avez copié à partir du portail de hello.
* Dans le projet de hello TodoList-Service, ouvrez `web.config` dans racine hello du projet de hello.  
  
  * Remplacez hello `ida:Audience` valeur hello même **Id de l’Application** à partir du portail de hello.

## <a name="use-msal-tooget-tokens"></a>Utiliser des jetons de tooget MSAL
Bonjour derrière MSAL principe de base est que chaque fois que votre application a besoin d’un jeton d’accès, il suffit d’appeler `app.AcquireToken(...)`, et MSAL hello rest.  

* Bonjour `TodoListClient` projet, ouvrez `MainWindow.xaml.cs` et recherchez hello `OnInitialized(...)` (méthode).  première étape de Hello est tooinitialize de votre application `PublicClientApplication` -classe de principal du MSAL représentant des applications natives.  Il s’agit d’où vous passez MSAL hello coordonnées nécessaires toocommunicate avec Azure AD et d’indiquer comment les jetons toocache.

```C#
protected override async void OnInitialized(EventArgs e)
{
        base.OnInitialized(e);

        app = new PublicClientApplication(new FileCache());
        AuthenticationResult result = null;
        ...
}
```

* Lors de l’application hello démarre, toocheck et nous voir si hello utilisateur est déjà connecté à application hello.  Toutefois, nous ne voulons pas encore tooinvoke une interface utilisateur de l’authentification : nous allons effectuer les utilisateur hello cliquez sur « Sign In » toodo donc.  Également dans hello `OnInitialized(...)` méthode :

```C#
// As hello app starts, we want toocheck toosee if hello user is already signed in.
// You can do so by trying tooget a token from MSAL, using hello method
// AcquireTokenSilent.  This forces MSAL toothrow an exception if it cannot
// get a token for hello user without showing a UI.
try
{
    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
    // If we got here, a valid token is in hello cache - or MSAL was able tooget a new oen via refresh token.
    // Proceed toofetch hello user's tasks from hello TodoListService via hello GetTodoList() method.

    SignInButton.Content = "Clear Cache";
    GetTodoList();
}
catch (MsalException ex)
{
    if (ex.ErrorCode == "user_interaction_required")
    {
        // If user interaction is required, hello app should take no action,
        // and simply show hello user hello sign in button.
    }
    else
    {
        // Here, we catch all other MsalExceptions
        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }
        MessageBox.Show(message);
    }
}

```

* Si l’utilisateur de hello n’est pas connecté et ils cliquent sur hello » bouton se connecter », nous tooinvoke une interface utilisateur de connexion et souhaitez utilisateur de hello entrer leurs informations d’identification.  Implémenter le Gestionnaire du bouton hello-In :

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // TODO: Sign hello user out if they clicked hello "Clear Cache" button

// If hello user clicked hello 'Sign-In' button, force
// MSAL tooprompt hello user for credentials by using
// AcquireTokenAsync, a method that is guaranteed tooshow a prompt toohello user.
// MSAL will get a token for hello TodoListService and cache it for you.

AuthenticationResult result = null;
try
{
    result = await app.AcquireTokenAsync(new string[] { clientId });
    SignInButton.Content = "Clear Cache";
    GetTodoList();
}
catch (MsalException ex)
{
    // If MSAL cannot get a token, it will throw an exception.
    // If hello user canceled hello login, it will result in the
    // error code 'authentication_canceled'.

    if (ex.ErrorCode == "authentication_canceled")
    {
        MessageBox.Show("Sign in was canceled by hello user");
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


}
```

* Si hello correctement les signes de l’utilisateur, MSAL recevra et mettre en cache un jeton pour vous et vous pouvez passer toocall hello `GetTodoList()` méthode en toute confiance.  Tout ce qui l’a laissé tooget les tâches d’un utilisateur est tooimplement hello `GetTodoList()` (méthode).

```C#
private async void GetTodoList()
{

AuthenticationResult result = null;
try
{
    // Here, we try tooget an access token toocall hello TodoListService
    // without invoking any UI prompt.  AcquireTokenSilentAsync forces
    // MSAL toothrow an exception if it cannot get a token silently.


    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
}
catch (MsalException ex)
{
    // MSAL couldn't get a token silently, so show hello user a message
    // and let them click hello Sign-In button.

    if (ex.ErrorCode == "user_interaction_required")
    {
        MessageBox.Show("Please sign in first");
        SignInButton.Content = "Sign In";
    }
    else
    {
        // In any other case, an unexpected error occurred.

        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }
        MessageBox.Show(message);
    }

    return;
}

// Once hello token has been returned by MSAL,
// add it toohello http authorization header,
// before making hello call tooaccess hello tooDo list service.

httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);


        ...
...


- When hello user is done managing their To-Do List, they may finally sign out of hello app by clicking hello "Clear Cache" button.

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // If hello user clicked hello 'clear cache' button,
        // clear hello MSAL token cache and show hello user as signed out.
        // It's also necessary tooclear hello cookies from hello browser
        // control so hello next user has a chance toosign in.

        if (SignInButton.Content.ToString() == "Clear Cache")
        {
                TodoList.ItemsSource = string.Empty;
                app.UserTokenCache.Clear(app.ClientId);
                ClearCookies();
                SignInButton.Content = "Sign In";
                return;
        }

        ...
```

## <a name="run"></a>Exécuter
Félicitations ! Vous maintenant disposerez d’une application WPF .NET qui a des utilisateurs tooauthenticate hello capacité & appelez en toute sécurité des API Web à l’aide d’OAuth 2.0.  Exécutez vos projets et connectez-vous avec un compte Microsoft personnel ou un compte professionnel ou scolaire.  Ajouter la liste des tâches de l’utilisateur toothat de tâches.  Déconnectez-vous et reconnectez-vous en tant qu’un autre utilisateur tooview leur liste de tâches.  Fermez l’application hello et réexécutez-la.  Notez comment de hello session reste intacte, c’est parce que l’application hello met en cache des jetons dans un fichier local.

MSAL rend fonctionnalités d’identité commune tooincorporate facile dans votre application, à l’aide des comptes personnels et professionnels.  Il s’occupe de tout le travail dirty hello vous - gestion du cache, la prise en charge de protocole d’OAuth, présentant les utilisateur hello avec une connexion de l’interface utilisateur, l’actualisation des jetons expirés et bien plus encore.  Vous devez vraiment tooknow est un simple appel d’API `app.AcquireTokenAsync(...)`.

Pour référence, hello effectuée exemple (sans les valeurs de configuration) [est fournie en tant qu’un fichier zip ici](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip), ou vous pouvez le cloner à partir de GitHub :

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git```

## <a name="next-steps"></a>Étapes suivantes
Vous pouvez maintenant aborder des rubriques plus sophistiquées.  Vous souhaiterez peut-être tootry :

* [Sécurisation de hello TodoListService Web API avec le point de terminaison hello v2.0](active-directory-v2-devquickstarts-dotnet-api.md)

Pour obtenir des ressources supplémentaires, consultez :  

* [guide du développeur v2.0 Hello >>](active-directory-appmodel-v2-overview.md)
* [Balise « msal » StackOverflow &gt;&gt;](http://stackoverflow.com/questions/tagged/msal)

## <a name="get-security-updates-for-our-products"></a>Obtenir les mises à jour de sécurité de nos produits
Nous vous conseillons de notifications tooget les incidents de sécurité se produire en vous rendant sur [cette page](https://technet.microsoft.com/security/dd252948) et l’abonnement d’alerte tooSecurity.

