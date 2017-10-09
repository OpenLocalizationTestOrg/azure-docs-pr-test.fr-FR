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
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a><span data-ttu-id="f8ffb-103">Utilisez hello bibliothèque d’authentification Microsoft (MSAL) tooget un jeton pour hello Microsoft Graph API</span><span class="sxs-lookup"><span data-stu-id="f8ffb-103">Use hello Microsoft Authentication Library (MSAL) tooget a token for hello Microsoft Graph API</span></span>

<span data-ttu-id="f8ffb-104">Cette section montre comment toouse MSAL tooget un jeton hello Microsoft Graph API.</span><span class="sxs-lookup"><span data-stu-id="f8ffb-104">This section shows how toouse MSAL tooget a token hello Microsoft Graph API.</span></span>

1.  <span data-ttu-id="f8ffb-105">Dans `MainWindow.xaml.cs`, ajouter une référence de hello pour la classe de toohello MSAL bibliothèque :</span><span class="sxs-lookup"><span data-stu-id="f8ffb-105">In `MainWindow.xaml.cs`, add hello reference for MSAL library toohello class:</span></span>

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="f8ffb-106">Remplacez le code de classe <code>MainWindow</code> par :</span><span class="sxs-lookup"><span data-stu-id="f8ffb-106">Replace <code>MainWindow</code> class code with:</span></span>
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
### <a name="more-information"></a><span data-ttu-id="f8ffb-107">Informations complémentaires</span><span class="sxs-lookup"><span data-stu-id="f8ffb-107">More Information</span></span>
#### <a name="getting-a-user-token-interactive"></a><span data-ttu-id="f8ffb-108">Obtention d’un jeton d’utilisateur de manière interactive</span><span class="sxs-lookup"><span data-stu-id="f8ffb-108">Getting a user token interactive</span></span>
<span data-ttu-id="f8ffb-109">Appel hello `AcquireTokenAsync` dans une invite de la fenêtre Résultats de la méthode hello toosign utilisateur dans.</span><span class="sxs-lookup"><span data-stu-id="f8ffb-109">Calling hello `AcquireTokenAsync` method results in a window prompting hello user toosign in.</span></span> <span data-ttu-id="f8ffb-110">Applications nécessitent généralement un utilisateur toosign interactivement Bonjour première dont ils ont besoin tooaccess une ressource protégée, ou lorsqu’un tooacquire silencieux un jeton échoue (par exemple hello mot de passe expiré).</span><span class="sxs-lookup"><span data-stu-id="f8ffb-110">Applications usually require a user toosign in interactively hello first time they need tooaccess a protected resource, or when a silent operation tooacquire a token fails (e.g. hello user’s password expired).</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="f8ffb-111">Obtention d’un jeton d’utilisateur en mode silencieux</span><span class="sxs-lookup"><span data-stu-id="f8ffb-111">Getting a user token silently</span></span>
<span data-ttu-id="f8ffb-112">`AcquireTokenSilentAsync` gère les acquisitions et renouvellements de jetons sans aucune interaction de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f8ffb-112">`AcquireTokenSilentAsync` handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="f8ffb-113">Après avoir `AcquireTokenAsync` est exécuté pour hello première fois, `AcquireTokenSilentAsync` est hello méthode habituelle utilisé tooobtain jetons utilisés tooaccess protégée des ressources pour les appels suivants - en tant qu’appels toorequest ou renouveler des jetons sont effectuées en mode silencieux.</span><span class="sxs-lookup"><span data-stu-id="f8ffb-113">After `AcquireTokenAsync` is executed for hello first time, `AcquireTokenSilentAsync` is hello usual method used tooobtain tokens used tooaccess protected resources for subsequent calls - as calls toorequest or renew tokens are made silently.</span></span>
<span data-ttu-id="f8ffb-114">Finalement, `AcquireTokenSilentAsync` échoue, par exemple hello utilisateur s’est déconnecté, ou a modifié son mot de passe sur un autre périphérique.</span><span class="sxs-lookup"><span data-stu-id="f8ffb-114">Eventually, `AcquireTokenSilentAsync` will fail – e.g. hello user has signed out, or has changed their password on another device.</span></span> <span data-ttu-id="f8ffb-115">Lorsque MSAL détecte que hello peut être résolu en demandant une action interactive, il déclenche une `MsalUiRequiredException`.</span><span class="sxs-lookup"><span data-stu-id="f8ffb-115">When MSAL detects that hello issue can be resolved by requiring an interactive action, it fires an `MsalUiRequiredException`.</span></span> <span data-ttu-id="f8ffb-116">Votre application peut gérer cette exception de deux manières :</span><span class="sxs-lookup"><span data-stu-id="f8ffb-116">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="f8ffb-117">Effectuer un appel sur `AcquireTokenAsync` immédiatement, ce qui aboutit à demander à l’utilisateur de hello dans toosign.</span><span class="sxs-lookup"><span data-stu-id="f8ffb-117">Make a call against `AcquireTokenAsync` immediately, which results in prompting hello user toosign-in.</span></span> <span data-ttu-id="f8ffb-118">Ce modèle est généralement utilisé dans les applications en ligne où il n’existe aucun contenu hors connexion dans l’application hello hello utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f8ffb-118">This pattern is usually used in online applications where there is no offline content in hello application available for hello user.</span></span> <span data-ttu-id="f8ffb-119">Hello générés par cet Assistant d’installation utilise ce modèle : vous pouvez voir dans hello d’action première fois que vous exécutez l’exemple hello : car aucun utilisateur n’a jamais n’utilisé l’application hello, `PublicClientApp.Users.FirstOrDefault()` contient une valeur null et un `MsalUiRequiredException` exception sera levée.</span><span class="sxs-lookup"><span data-stu-id="f8ffb-119">hello sample generated by this guided setup uses this pattern: you can see it in action hello first time you execute hello sample: because no user ever used hello application, `PublicClientApp.Users.FirstOrDefault()` will contain a null value, and an `MsalUiRequiredException` exception will be thrown.</span></span> <span data-ttu-id="f8ffb-120">Hello code dans l’exemple hello puis handles hello exception en appelant `AcquireTokenAsync` résultant d’inviter l’utilisateur hello dans toosign.</span><span class="sxs-lookup"><span data-stu-id="f8ffb-120">hello code in hello sample then handles hello exception by calling `AcquireTokenAsync` resulting in prompting hello user toosign-in.</span></span>

2.  <span data-ttu-id="f8ffb-121">Les applications peuvent également faire d’un utilisateur de toohello d’indication visuelle qui une connexion à interactive étant requise, hello utilisateur sélectionne toosign du moment opportun hello dans ou application hello peut réessayer `AcquireTokenSilentAsync` ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="f8ffb-121">Applications can also make a visual indication toohello user that an interactive sign-in is required, so hello user can select hello right time toosign in, or hello application can retry `AcquireTokenSilentAsync` at a later time.</span></span> <span data-ttu-id="f8ffb-122">Cela est généralement utilisé lorsque l’utilisateur de hello peut utiliser d’autres fonctionnalités de l’application hello sans dérangement - par exemple, il est contenu hors connexion disponible dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="f8ffb-122">This is usually used when hello user can use other functionality of hello application without being disrupted - for example, there is offline content available in hello application.</span></span> <span data-ttu-id="f8ffb-123">Dans ce cas, hello utilisateur peut décider quand ils veulent toosign dans la ressource de hello protégé tooaccess, ou toorefresh hello des informations obsolètes, ou votre application peut décider tooretry `AcquireTokenSilentAsync` lorsque le réseau est restauré après n’est pas disponible temporairement.</span><span class="sxs-lookup"><span data-stu-id="f8ffb-123">In this case, hello user can decide when they want toosign in tooaccess hello protected resource, or toorefresh hello outdated information, or your application can decide tooretry `AcquireTokenSilentAsync` when network is restored after being unavailable temporarily.</span></span>
<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a><span data-ttu-id="f8ffb-124">Appeler l’API Microsoft Graph hello à l’aide du jeton hello que simplement obtenu</span><span class="sxs-lookup"><span data-stu-id="f8ffb-124">Call hello Microsoft Graph API using hello token you just obtained</span></span>

1. <span data-ttu-id="f8ffb-125">Ajouter nouvelle méthode de hello ci-dessous tooyour `MainWindow.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="f8ffb-125">Add hello new method below tooyour `MainWindow.xaml.cs`.</span></span> <span data-ttu-id="f8ffb-126">méthode Hello est toomake utilisé un `GET` demande par rapport à l’API Graph à l’aide d’un en-tête Authorize :</span><span class="sxs-lookup"><span data-stu-id="f8ffb-126">hello method is used toomake a `GET` request against Graph API using an Authorize header:</span></span>

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
### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="f8ffb-127">Plus d’informations sur l’envoi d’un appel REST à une API protégée</span><span class="sxs-lookup"><span data-stu-id="f8ffb-127">More information on making a REST call against a protected API</span></span>

<span data-ttu-id="f8ffb-128">Dans cet exemple d’application, hello `GetHttpContentWithToken` méthode est utilisée toomake HTTP `GET` demande par rapport à une ressource protégée qui requiert un appelant de contenu toohello hello jeton, puis de retourner.</span><span class="sxs-lookup"><span data-stu-id="f8ffb-128">In this sample application, hello `GetHttpContentWithToken` method is used toomake an HTTP `GET` request against a protected resource that requires a token and then return hello content toohello caller.</span></span> <span data-ttu-id="f8ffb-129">Cette méthode ajoute un jeton de hello acquis Bonjour *en-tête d’autorisation HTTP*.</span><span class="sxs-lookup"><span data-stu-id="f8ffb-129">This method adds hello acquired token in hello *HTTP Authorization header*.</span></span> <span data-ttu-id="f8ffb-130">Pour cet exemple, les ressources hello sont hello Microsoft Graph API *me* endpoint – qui affiche des informations de profil de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="f8ffb-130">For this sample, hello resource is hello Microsoft Graph API *me* endpoint – which displays hello user's profile information.</span></span>
<!--end-collapse-->

## <a name="add-a-method-toosign-out-hello-user"></a><span data-ttu-id="f8ffb-131">Ajouter un toosign méthode utilisateur de hello</span><span class="sxs-lookup"><span data-stu-id="f8ffb-131">Add a method toosign out hello user</span></span>

1. <span data-ttu-id="f8ffb-132">Ajouter hello suivant de méthode tooyour `MainWindow.xaml.cs` toosign utilisateur de hello :</span><span class="sxs-lookup"><span data-stu-id="f8ffb-132">Add hello following method tooyour `MainWindow.xaml.cs` toosign out hello user:</span></span>

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
### <a name="more-info-on-sign-out"></a><span data-ttu-id="f8ffb-133">Plus d’informations sur la déconnexion</span><span class="sxs-lookup"><span data-stu-id="f8ffb-133">More info on Sign-Out</span></span>

<span data-ttu-id="f8ffb-134">`SignOutButton_Click`Supprime hello utilisateur à partir du cache MSAL utilisateur : Ceci donnera efficacement l’utilisateur actuel MSAL tooforget hello pour une demande ultérieure de tooacquire un jeton réussira uniquement si elle est rendue toobe interactive.</span><span class="sxs-lookup"><span data-stu-id="f8ffb-134">`SignOutButton_Click` removes hello user from MSAL user cache – this will effectively tell MSAL tooforget hello current user so a future request tooacquire a token will only succeed if it is made toobe interactive.</span></span>
<span data-ttu-id="f8ffb-135">Bien que l’application hello dans cet exemple prend en charge un seul utilisateur, MSAL prend en charge les scénarios où plusieurs comptes peuvent être signé en hello simultanément et obtenir un exemple est une application de messagerie où un utilisateur possède plusieurs comptes.</span><span class="sxs-lookup"><span data-stu-id="f8ffb-135">Although hello application in this sample supports a single user, MSAL supports scenarios where multiple accounts can be signed-in at hello same time – an example is an email application where a user has multiple accounts.</span></span>
<!--end-collapse-->

## <a name="display-basic-token-information"></a><span data-ttu-id="f8ffb-136">Afficher les informations de base du jeton</span><span class="sxs-lookup"><span data-stu-id="f8ffb-136">Display Basic Token Information</span></span>

1. <span data-ttu-id="f8ffb-137">Ajouter hello suivant de méthode tootooyour `MainWindow.xaml.cs` toodisplay les informations de base sur le jeton de hello :</span><span class="sxs-lookup"><span data-stu-id="f8ffb-137">Add hello following method tootooyour `MainWindow.xaml.cs` toodisplay basic information about hello token:</span></span>

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
### <a name="more-information"></a><span data-ttu-id="f8ffb-138">Informations complémentaires</span><span class="sxs-lookup"><span data-stu-id="f8ffb-138">More Information</span></span>

<span data-ttu-id="f8ffb-139">Jetons acquis *OpenID Connect* également contenir un petit sous-ensemble des informations toohello pertinentes de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f8ffb-139">Tokens acquired via *OpenID Connect* also contain a small subset of information pertinent toohello user.</span></span> <span data-ttu-id="f8ffb-140">`DisplayBasicTokenInfo`Affiche des informations de base contenues dans le jeton de hello : par exemple, l’utilisateur hello affiche le nom et l’ID, ainsi que hello chaîne de date et d’hello d’expiration du jeton représentant le jeton d’accès hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="f8ffb-140">`DisplayBasicTokenInfo` displays basic information contained in hello token: for example, hello user's display name and ID, as well as hello token expiration date and hello string representing hello access token itself.</span></span> <span data-ttu-id="f8ffb-141">Cette information s’affiche pour vous toosee.</span><span class="sxs-lookup"><span data-stu-id="f8ffb-141">This information is displayed for you toosee.</span></span> <span data-ttu-id="f8ffb-142">Vous pouvez appuyer sur hello *appeler l’API Microsoft Graph* bouton plusieurs fois et de voir ce hello même jeton a été réutilisé pour les demandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="f8ffb-142">You can hit hello *Call Microsoft Graph API* button multiple times and see that hello same token was reused for subsequent requests.</span></span> <span data-ttu-id="f8ffb-143">Vous pouvez également voir la date d’expiration de hello lorsque MSAL décide de que temps toorenew hello jeton est étendu.</span><span class="sxs-lookup"><span data-stu-id="f8ffb-143">You can also see hello expiration date being extended when MSAL decides it is time toorenew hello token.</span></span>
<!--end-collapse-->

