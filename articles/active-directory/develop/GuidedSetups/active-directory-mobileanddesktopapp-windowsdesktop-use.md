---
title: aaaAzure AD v2 Windows Desktop mise en route - utilisez | Documents Microsoft
description: "Cet article explique comment les applications de bureau Windows .NET (XAML) peuvent appeler une API qui nécessite des jetons d’accès à partir d’un point de terminaison Azure Active Directory v2."
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
ms.openlocfilehash: bb258fe5f523ec727ca02716fd823d853d3349b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a>Utilisez hello bibliothèque d’authentification Microsoft (MSAL) tooget un jeton pour hello Microsoft Graph API

Cette section montre comment toouse MSAL tooget un jeton hello Microsoft Graph API.

1.  Dans `MainWindow.xaml.cs`, ajouter une référence de hello pour la classe de toohello MSAL bibliothèque :

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
Remplacez le code de classe <code>MainWindow</code> par :
</li>
</ol>

```csharp
public partial class MainWindow : Window
{
    //Set hello API Endpoint tooGraph 'me' endpoint
    string _graphAPIEndpoint = "https://graph.microsoft.com/v1.0/me";

    //Set hello scope for API call toouser.read
    string[] _scopes = new string[] { "user.read" };


    public MainWindow()
    {
        InitializeComponent();
    }

    /// <summary>
    /// Call AcquireTokenAsync - tooacquire a token requiring user toosign-in
    /// </summary>
    private async void CallGraphButton_Click(object sender, RoutedEventArgs e)
    {
        AuthenticationResult authResult = null;

        try
        {
            authResult = await App.PublicClientApp.AcquireTokenSilentAsync(_scopes, App.PublicClientApp.Users.FirstOrDefault());
        }
        catch (MsalUiRequiredException ex)
        {
            // A MsalUiRequiredException happened on AcquireTokenSilentAsync. This indicates you need toocall AcquireTokenAsync tooacquire a token
            System.Diagnostics.Debug.WriteLine($"MsalUiRequiredException: {ex.Message}");

            try
            {
                authResult = await App.PublicClientApp.AcquireTokenAsync(_scopes);
            }
            catch (MsalException msalex)
            {
                ResultText.Text = $"Error Acquiring Token:{System.Environment.NewLine}{msalex}";
            }
        }
        catch (Exception ex)
        {
            ResultText.Text = $"Error Acquiring Token Silently:{System.Environment.NewLine}{ex}";
            return;
        }

        if (authResult != null)
        {
            ResultText.Text = await GetHttpContentWithToken(_graphAPIEndpoint, authResult.AccessToken);
            DisplayBasicTokenInfo(authResult);
            this.SignOutButton.Visibility = Visibility.Visible;
        }
    }
}
```

<!--start-collapse-->
### <a name="more-information"></a>Informations complémentaires
#### <a name="getting-a-user-token-interactive"></a>Obtention d’un jeton d’utilisateur de manière interactive
Appel hello `AcquireTokenAsync` dans une invite de la fenêtre Résultats de la méthode hello toosign utilisateur dans. Applications nécessitent généralement un utilisateur toosign interactivement Bonjour première dont ils ont besoin tooaccess une ressource protégée, ou lorsqu’un tooacquire silencieux un jeton échoue (par exemple hello mot de passe expiré).

#### <a name="getting-a-user-token-silently"></a>Obtention d’un jeton d’utilisateur en mode silencieux
`AcquireTokenSilentAsync` gère les acquisitions et renouvellements de jetons sans aucune interaction de l’utilisateur. Après avoir `AcquireTokenAsync` est exécuté pour hello première fois, `AcquireTokenSilentAsync` est hello méthode habituelle utilisé tooobtain jetons utilisés tooaccess protégée des ressources pour les appels suivants - en tant qu’appels toorequest ou renouveler des jetons sont effectuées en mode silencieux.
Finalement, `AcquireTokenSilentAsync` échoue, par exemple hello utilisateur s’est déconnecté, ou a modifié son mot de passe sur un autre périphérique. Lorsque MSAL détecte que hello peut être résolu en demandant une action interactive, il déclenche une `MsalUiRequiredException`. Votre application peut gérer cette exception de deux manières :

1.  Effectuer un appel sur `AcquireTokenAsync` immédiatement, ce qui aboutit à demander à l’utilisateur de hello dans toosign. Ce modèle est généralement utilisé dans les applications en ligne où il n’existe aucun contenu hors connexion dans l’application hello hello utilisateur. Hello générés par cet Assistant d’installation utilise ce modèle : vous pouvez voir dans hello d’action première fois que vous exécutez l’exemple hello : car aucun utilisateur n’a jamais n’utilisé l’application hello, `PublicClientApp.Users.FirstOrDefault()` contient une valeur null et un `MsalUiRequiredException` exception sera levée. Hello code dans l’exemple hello puis handles hello exception en appelant `AcquireTokenAsync` résultant d’inviter l’utilisateur hello dans toosign.

2.  Les applications peuvent également faire d’un utilisateur de toohello d’indication visuelle qui une connexion à interactive étant requise, hello utilisateur sélectionne toosign du moment opportun hello dans ou application hello peut réessayer `AcquireTokenSilentAsync` ultérieurement. Cela est généralement utilisé lorsque l’utilisateur de hello peut utiliser d’autres fonctionnalités de l’application hello sans dérangement - par exemple, il est contenu hors connexion disponible dans l’application hello. Dans ce cas, hello utilisateur peut décider quand ils veulent toosign dans la ressource de hello protégé tooaccess, ou toorefresh hello des informations obsolètes, ou votre application peut décider tooretry `AcquireTokenSilentAsync` lorsque le réseau est restauré après n’est pas disponible temporairement.
<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a>Appeler l’API Microsoft Graph hello à l’aide du jeton hello que simplement obtenu

1. Ajouter nouvelle méthode de hello ci-dessous tooyour `MainWindow.xaml.cs`. méthode Hello est toomake utilisé un `GET` demande par rapport à l’API Graph à l’aide d’un en-tête Authorize :

```csharp
/// <summary>
/// Perform an HTTP GET request tooa URL using an HTTP Authorization header
/// </summary>
/// <param name="url">hello URL</param>
/// <param name="token">hello token</param>
/// <returns>String containing hello results of hello GET operation</returns>
public async Task<string> GetHttpContentWithToken(string url, string token)
{
    var httpClient = new System.Net.Http.HttpClient();
    System.Net.Http.HttpResponseMessage response;
    try
    {
        var request = new System.Net.Http.HttpRequestMessage(System.Net.Http.HttpMethod.Get, url);
        //Add hello token in Authorization header
        request.Headers.Authorization = new System.Net.Http.Headers.AuthenticationHeaderValue("Bearer", token);
        response = await httpClient.SendAsync(request);
        var content = await response.Content.ReadAsStringAsync();
        return content;
    }
    catch (Exception ex)
    {
        return ex.ToString();
    }
}
```
<!--start-collapse-->
### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a>Plus d’informations sur l’envoi d’un appel REST à une API protégée

Dans cet exemple d’application, hello `GetHttpContentWithToken` méthode est utilisée toomake HTTP `GET` demande par rapport à une ressource protégée qui requiert un appelant de contenu toohello hello jeton, puis de retourner. Cette méthode ajoute un jeton de hello acquis Bonjour *en-tête d’autorisation HTTP*. Pour cet exemple, les ressources hello sont hello Microsoft Graph API *me* endpoint – qui affiche des informations de profil de l’utilisateur hello.
<!--end-collapse-->

## <a name="add-a-method-toosign-out-hello-user"></a>Ajouter un toosign méthode utilisateur de hello

1. Ajouter hello suivant de méthode tooyour `MainWindow.xaml.cs` toosign utilisateur de hello :

```csharp
/// <summary>
/// Sign out hello current user
/// </summary>
private void SignOutButton_Click(object sender, RoutedEventArgs e)
{
    if (App.PublicClientApp.Users.Any())
    {
        try
        {
            App.PublicClientApp.Remove(App.PublicClientApp.Users.FirstOrDefault());
            this.ResultText.Text = "User has signed-out";
            this.CallGraphButton.Visibility = Visibility.Visible;
            this.SignOutButton.Visibility = Visibility.Collapsed;
        }
        catch (MsalException ex)
        {
            ResultText.Text = $"Error signing-out user: {ex.Message}";
        }
    }
}
```
<!--start-collapse-->
### <a name="more-info-on-sign-out"></a>Plus d’informations sur la déconnexion

`SignOutButton_Click`Supprime hello utilisateur à partir du cache MSAL utilisateur : Ceci donnera efficacement l’utilisateur actuel MSAL tooforget hello pour une demande ultérieure de tooacquire un jeton réussira uniquement si elle est rendue toobe interactive.
Bien que l’application hello dans cet exemple prend en charge un seul utilisateur, MSAL prend en charge les scénarios où plusieurs comptes peuvent être signé en hello simultanément et obtenir un exemple est une application de messagerie où un utilisateur possède plusieurs comptes.
<!--end-collapse-->

## <a name="display-basic-token-information"></a>Afficher les informations de base du jeton

1. Ajouter hello suivant de méthode tootooyour `MainWindow.xaml.cs` toodisplay les informations de base sur le jeton de hello :

```csharp
/// <summary>
/// Display basic information contained in hello token
/// </summary>
private void DisplayBasicTokenInfo(AuthenticationResult authResult)
{
    TokenInfoText.Text = "";
    if (authResult != null)
    {
        TokenInfoText.Text += $"Name: {authResult.User.Name}" + Environment.NewLine;
        TokenInfoText.Text += $"Username: {authResult.User.DisplayableId}" + Environment.NewLine;
        TokenInfoText.Text += $"Token Expires: {authResult.ExpiresOn.ToLocalTime()}" + Environment.NewLine;
        TokenInfoText.Text += $"Access Token: {authResult.AccessToken}" + Environment.NewLine;
    }
}
```
<!--start-collapse-->
### <a name="more-information"></a>Informations complémentaires

Jetons acquis *OpenID Connect* également contenir un petit sous-ensemble des informations toohello pertinentes de l’utilisateur. `DisplayBasicTokenInfo`Affiche des informations de base contenues dans le jeton de hello : par exemple, l’utilisateur hello affiche le nom et l’ID, ainsi que hello chaîne de date et d’hello d’expiration du jeton représentant le jeton d’accès hello lui-même. Cette information s’affiche pour vous toosee. Vous pouvez appuyer sur hello *appeler l’API Microsoft Graph* bouton plusieurs fois et de voir ce hello même jeton a été réutilisé pour les demandes suivantes. Vous pouvez également voir la date d’expiration de hello lorsque MSAL décide de que temps toorenew hello jeton est étendu.
<!--end-collapse-->

