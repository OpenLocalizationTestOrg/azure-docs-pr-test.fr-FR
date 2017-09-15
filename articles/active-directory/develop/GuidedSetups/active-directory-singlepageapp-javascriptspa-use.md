---
title: "Configuration guidée d’Azure AD v2 JS SPA - Utilisation | Microsoft Docs"
description: "Comment les applications JavaScript SPA peuvent appeler une API qui nécessite des jetons d’accès à partir d’un point de terminaison Azure Active Directory v2"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: f52157df298ddfc1c1b29a18dc9a54aae59b52a3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
## <a name="use-the-microsoft-authentication-library-msal-to-sign-in-the-user"></a><span data-ttu-id="03ddd-103">Utiliser Microsoft Authentication Library (MSAL) pour connecter l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="03ddd-103">Use the Microsoft Authentication Library (MSAL) to sign-in the user</span></span>

1.  <span data-ttu-id="03ddd-104">Créez un fichier appelé `app.js`.</span><span class="sxs-lookup"><span data-stu-id="03ddd-104">Create a file named `app.js`.</span></span> <span data-ttu-id="03ddd-105">Si vous utilisez Visual Studio, sélectionnez le projet (dossier racine du projet), cliquez avec le bouton droit, puis sélectionnez `Add` > `New Item` > `JavaScript File` :</span><span class="sxs-lookup"><span data-stu-id="03ddd-105">If you are using Visual Studio, select the project (project root folder), right click and select: `Add` > `New Item` > `JavaScript File`:</span></span>
2.  <span data-ttu-id="03ddd-106">Ajoutez le code suivant à votre fichier `app.js` :</span><span class="sxs-lookup"><span data-stu-id="03ddd-106">Add the following code to your `app.js` file:</span></span>

```javascript
// Graph API endpoint to show user profile
var graphApiEndpoint = "https://graph.microsoft.com/v1.0/me";

// Graph API scope used to obtain the access token to read user profile
var graphAPIScopes = ["https://graph.microsoft.com/user.read"];

// Initialize application
var userAgentApplication = new Msal.UserAgentApplication(msalconfig.clientID, null, loginCallback, {
    redirectUri: msalconfig.redirectUri
});

//Previous version of msal uses redirect url via a property
if (userAgentApplication.redirectUri) {
    userAgentApplication.redirectUri = msalconfig.redirectUri;
}

window.onload = function () {
    // If page is refreshed, continue to display user info
    if (!userAgentApplication.isCallback(window.location.hash) && window.parent === window && !window.opener) {
        var user = userAgentApplication.getUser();
        if (user) {
            callGraphApi();
        }
    }
}

/**
 * Call the Microsoft Graph API and display the results on the page. Sign the user in if necessary
 */
function callGraphApi() {
    var user = userAgentApplication.getUser();
    if (!user) {
        // If user is not signed in, then prompt user to sign in via loginRedirect.
        // This will redirect user to the Azure Active Directory v2 Endpoint
        userAgentApplication.loginRedirect(graphAPIScopes);
        // The call to loginRedirect above frontloads the consent to query Graph API during the sign-in.
        // If you want to use dynamic consent, just remove the graphAPIScopes from loginRedirect call.
        // As such, user will be prompted to give consent when requested access to a resource that 
        // he/she hasn't consented before. In the case of this application - 
        // the first time the Graph API call to obtain user's profile is executed.
    } else {
        // If user is already signed in, display the user info
        var userInfoElement = document.getElementById("userInfo");
        userInfoElement.parentElement.classList.remove("hidden");
        userInfoElement.innerHTML = JSON.stringify(user, null, 4);

        // Show Sign-Out button
        document.getElementById("signOutButton").classList.remove("hidden");

        // Now Call Graph API to show the user profile information:
        var graphCallResponseElement = document.getElementById("graphResponse");
        graphCallResponseElement.parentElement.classList.remove("hidden");
        graphCallResponseElement.innerText = "Calling Graph ...";

        // In order to call the Graph API, an access token needs to be acquired.
        // Try to acquire the token used to query Graph API silently first:
        userAgentApplication.acquireTokenSilent(graphAPIScopes)
            .then(function (token) {
                //After the access token is acquired, call the Web API, sending the acquired token
                callWebApiWithToken(graphApiEndpoint, token, graphCallResponseElement, document.getElementById("accessToken"));

            }, function (error) {
                // If the acquireTokenSilent() method fails, then acquire the token interactively via acquireTokenRedirect().
                // In this case, the browser will redirect user back to the Azure Active Directory v2 Endpoint so the user 
                // can reenter the current username/ password and/ or give consent to new permissions your application is requesting.
                // After authentication/ authorization completes, this page will be reloaded again and callGraphApi() will be executed on page load.
                // Then, acquireTokenSilent will then get the token silently, the Graph API call results will be made and results will be displayed in the page.
                if (error) {
                    userAgentApplication.acquireTokenRedirect(graphAPIScopes);
                }
            });

    }
}

/**
 * Callback method from sign-in: if no errors, call callGraphApi() to show results.
 * @param {string} errorDesc - If error occur, the error message
 * @param {object} token - The token received from login
 * @param {object} error - The error string
 * @param {string} tokenType - the token type: usually id_token
 */
function loginCallback(errorDesc, token, error, tokenType) {
    if (errorDesc) {
        showError(msal.authority, error, errorDesc);
    } else {
        callGraphApi();
    }
}

/**
 * Show an error message in the page
 * @param {string} endpoint - the endpoint used for the error message
 * @param {string} error - Error string
 * @param {string} errorDesc - Error description
 */
function showError(endpoint, error, errorDesc) {
    var formattedError = JSON.stringify(error, null, 4);
    if (formattedError.length < 3) {
        formattedError = error;
    }
    document.getElementById("errorMessage").innerHTML = "An error has occurred:<br/>Endpoint: " + endpoint + "<br/>Error: " + formattedError + "<br/>" + errorDesc;
    console.error(error);
}

```

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="03ddd-107">Informations complémentaires</span><span class="sxs-lookup"><span data-stu-id="03ddd-107">More Information</span></span>

<span data-ttu-id="03ddd-108">Quand un utilisateur clique sur le bouton *Call Microsoft Graph API* (Appeler l’API Graph Microsoft) pour la première fois, la méthode `callGraphApi` appelle `loginRedirect` pour connecter l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="03ddd-108">After a user clicks the *‘Call Microsoft Graph API’* button for the first time, `callGraphApi` method calls `loginRedirect` to sign in the user.</span></span> <span data-ttu-id="03ddd-109">Cette méthode redirige l’utilisateur vers le *point de terminaison Microsoft Azure Active Directory v2* afin de demander et valider les informations d’identification de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="03ddd-109">This method results in redirecting the user to the *Microsoft Azure Active Directory v2 endpoint* to prompt and validate the user's credentials.</span></span> <span data-ttu-id="03ddd-110">Une fois connecté, l’utilisateur est redirigé vers la page *index.html* d’origine. Ensuite, un jeton est reçu, puis traité par `msal.js`, et les informations contenues dans le jeton sont mises en cache.</span><span class="sxs-lookup"><span data-stu-id="03ddd-110">As a result of a successful sign-in, the user is redirected back to the original *index.html* page, and a token is received, processed by `msal.js` and the information contained in the token is cached.</span></span> <span data-ttu-id="03ddd-111">Ce jeton est le *jeton d’ID* et contient des informations de base sur l’utilisateur, telles que son nom d’affichage.</span><span class="sxs-lookup"><span data-stu-id="03ddd-111">This token is known as the *ID token* and contains basic information about the user, such as the user display name.</span></span> <span data-ttu-id="03ddd-112">Si vous envisagez d’utiliser les données fournies par ce jeton à toutes fins que ce soit, vous devez vous assurer que ce jeton est validé par le serveur principal afin de garantir qu’il a été émis pour un utilisateur valide de votre application.</span><span class="sxs-lookup"><span data-stu-id="03ddd-112">If you plan to use any data provided by this token for any purposes, you need to make sure this token is validated by your backend server to guarantee that the token was issued to a valid user for your application.</span></span>

<span data-ttu-id="03ddd-113">L’application SPA créée dans ce guide n’utilise pas directement le jeton d’ID. En effet, elle appelle `acquireTokenSilent` et/ou `acquireTokenRedirect` pour acquérir un *jeton d’accès* utilisé pour interroger l’API Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="03ddd-113">The SPA generated by this guide does not make use directly of the ID token – instead, it calls `acquireTokenSilent` and/or `acquireTokenRedirect` to acquire an *access token* used to query the Microsoft Graph API.</span></span> <span data-ttu-id="03ddd-114">Si vous avez besoin d’un exemple qui valide le jeton d’ID, regardez [cet exemple d’application](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2 "exemple Github active-directory-javascript-singlepageapp-dotnet-webapi-v2") dans GitHub. Cet exemple utilise une API web ASP.NET pour la validation du jeton.</span><span class="sxs-lookup"><span data-stu-id="03ddd-114">If you need a sample that validates the ID token, take a look at [this](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2 "Github active-directory-javascript-singlepageapp-dotnet-webapi-v2 sample") sample application in GitHub – the sample uses an ASP.NET Web API for token validation.</span></span>

#### <a name="getting-a-user-token-interactively"></a><span data-ttu-id="03ddd-115">Obtention d’un jeton d’utilisateur de manière interactive</span><span class="sxs-lookup"><span data-stu-id="03ddd-115">Getting a user token interactively</span></span>

<span data-ttu-id="03ddd-116">Après la première connexion, il n’est pas souhaitable de demander aux utilisateurs de se réauthentifier chaque fois qu’ils ont besoin d’un jeton pour accéder à une ressource. Par conséquent, *acquireTokenSilent* doit être utilisé pour acquérir des jetons dans la plupart des situations.</span><span class="sxs-lookup"><span data-stu-id="03ddd-116">After the initial sign-in, you do not want the ask users to reauthenticate every time they need to request a token to access a resource – so *acquireTokenSilent* should be used most of the time to acquire tokens.</span></span> <span data-ttu-id="03ddd-117">Il existe cependant des situations dans lesquelles vous devez forcer les utilisateurs à interagir avec le point de terminaison Azure Active Directory v2. Voici quelques exemples de telles situations :</span><span class="sxs-lookup"><span data-stu-id="03ddd-117">There are situations however that you need to force users interact with Azure Active Directory v2 endpoint – some examples include:</span></span>
-   <span data-ttu-id="03ddd-118">Les utilisateurs doivent réentrer leurs informations d’identification, car le mot de passe a expiré.</span><span class="sxs-lookup"><span data-stu-id="03ddd-118">Users may need to reenter their credentials because the password has expired</span></span>
-   <span data-ttu-id="03ddd-119">Votre application demande l’accès à une ressource pour laquelle l’utilisateur doit donner son consentement.</span><span class="sxs-lookup"><span data-stu-id="03ddd-119">Your application is requesting access to a resource that the user needs to consent to</span></span>
-   <span data-ttu-id="03ddd-120">Une authentification à 2 facteurs est demandée.</span><span class="sxs-lookup"><span data-stu-id="03ddd-120">Two factor authentication is required</span></span>

<span data-ttu-id="03ddd-121">Le fait d’appeler *acquireTokenRedirect(scope)* entraîne la redirection des utilisateurs vers le point de terminaison Azure Active Directory v2 (ou l’appel de *acquireTokenPopup(scope)* entraîne l’affichage d’une fenêtre contextuelle) avec lequel ils doivent interagir en confirmant leurs informations d’identification, en consentant à ce que l’application accède à la ressource ou en effectuant l’authentification à 2 facteurs.</span><span class="sxs-lookup"><span data-stu-id="03ddd-121">Calling the *acquireTokenRedirect(scope)* result in redirecting users to the Azure Active Directory v2 endpoint (or *acquireTokenPopup(scope)* result on a popup window) where users need to interact with by either confirming their credentials, giving the consent to the required resource, or completing the two factor authentication.</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="03ddd-122">Obtention d’un jeton d’utilisateur en mode silencieux</span><span class="sxs-lookup"><span data-stu-id="03ddd-122">Getting a user token silently</span></span>
<span data-ttu-id="03ddd-123">La méthode ` acquireTokenSilent` gère les acquisitions et renouvellements de jetons sans aucune interaction de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="03ddd-123">The ` acquireTokenSilent` method handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="03ddd-124">Quand `loginRedirect` (ou `loginPopup`) est exécuté pour la première fois, c’est en général la méthode `acquireTokenSilent` qui est utilisée pour obtenir les jetons permettant d’accéder aux ressources protégées pour les appels suivants, car les appels de demande ou de renouvellement des jetons sont émis de manière silencieuse.</span><span class="sxs-lookup"><span data-stu-id="03ddd-124">After `loginRedirect` (or `loginPopup`) is executed for the first time, `acquireTokenSilent` is the method commonly used to obtain tokens used to access protected resources for subsequent calls - as calls to request or renew tokens are made silently.</span></span>
<span data-ttu-id="03ddd-125">`acquireTokenSilent` risque d’échouer dans certains cas (par exemple, si le mot de passe a expiré).</span><span class="sxs-lookup"><span data-stu-id="03ddd-125">`acquireTokenSilent` may fail in some cases – for example, the user's password has expired.</span></span> <span data-ttu-id="03ddd-126">Votre application peut gérer cette exception de deux manières :</span><span class="sxs-lookup"><span data-stu-id="03ddd-126">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="03ddd-127">En appelant immédiatement `acquireTokenRedirect` pour que l’utilisateur soit invité à se connecter.</span><span class="sxs-lookup"><span data-stu-id="03ddd-127">Make a call to `acquireTokenRedirect` immediately, which results in prompting the user to sign in.</span></span> <span data-ttu-id="03ddd-128">Cette méthode est couramment employée avec les applications en ligne dans lesquelles aucun contenu non authentifié n’est disponible pour l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="03ddd-128">This pattern is commonly used in online applications where there is no unauthenticated content in the application available to the user.</span></span> <span data-ttu-id="03ddd-129">L’exemple créé avec cette installation guidée utilise ce modèle.</span><span class="sxs-lookup"><span data-stu-id="03ddd-129">The sample generated by this guided setup uses this pattern.</span></span>

2. <span data-ttu-id="03ddd-130">Les applications peuvent également signaler à l’utilisateur qu’une connexion interactive est requise afin qu’il puisse choisir le bon moment pour se connecter ou que l’application puisse réessayer d’exécuter `acquireTokenSilent` ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="03ddd-130">Applications can also make a visual indication to the user that an interactive sign-in is required, so the user can select the right time to sign in, or the application can retry `acquireTokenSilent` at a later time.</span></span> <span data-ttu-id="03ddd-131">Cette solution est couramment retenue lorsque l’utilisateur peut utiliser d’autres fonctionnalités de l’application sans être perturbé, notamment lorsque du contenu non authentifié est disponible dans l’application.</span><span class="sxs-lookup"><span data-stu-id="03ddd-131">This is commonly used when the user can use other functionality of the application without being disrupted - for example, there is unauthenticated content available in the application.</span></span> <span data-ttu-id="03ddd-132">Dans ce cas, l’utilisateur peut décider de se connecter pour accéder à la ressource protégée ou pour actualiser les informations obsolètes.</span><span class="sxs-lookup"><span data-stu-id="03ddd-132">In this case, the user can decide when they want to sign in to access the protected resource, or to refresh the outdated information.</span></span>

<!--end-collapse-->

## <a name="call-the-microsoft-graph-api-using-the-token-you-just-obtained"></a><span data-ttu-id="03ddd-133">Appeler l’API Microsoft Graph à l’aide du jeton que vous venez d’obtenir</span><span class="sxs-lookup"><span data-stu-id="03ddd-133">Call the Microsoft Graph API using the token you just obtained</span></span>

<span data-ttu-id="03ddd-134">Ajoutez le code suivant à votre fichier `app.js` :</span><span class="sxs-lookup"><span data-stu-id="03ddd-134">Add the following code to your `app.js` file:</span></span>

```javascript
/**
 * Call a Web API using an access token.
 * @param {any} endpoint - Web API endpoint
 * @param {any} token - Access token
 * @param {object} responseElement - HTML element used to display the results
 * @param {object} showTokenElement = HTML element used to display the RAW access token
 */
function callWebApiWithToken(endpoint, token, responseElement, showTokenElement) {
    var headers = new Headers();
    var bearer = "Bearer " + token;
    headers.append("Authorization", bearer);
    var options = {
        method: "GET",
        headers: headers
    };

    fetch(endpoint, options)
        .then(function (response) {
            var contentType = response.headers.get("content-type");
            if (response.status === 200 && contentType && contentType.indexOf("application/json") !== -1) {
                response.json()
                    .then(function (data) {
                        // Display response in the page
                        console.log(data);
                        responseElement.innerHTML = JSON.stringify(data, null, 4);
                        if (showTokenElement) {
                            showTokenElement.parentElement.classList.remove("hidden");
                            showTokenElement.innerHTML = token;
                        }
                    })
                    .catch(function (error) {
                        showError(endpoint, error);
                    });
            } else {
                response.json()
                    .then(function (data) {
                        // Display response as error in the page
                        showError(endpoint, data);
                    })
                    .catch(function (error) {
                        showError(endpoint, error);
                    });
            }
        })
        .catch(function (error) {
            showError(endpoint, error);
        });
}
```
<!--start-collapse-->

### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="03ddd-135">Plus d’informations sur l’envoi d’un appel REST à une API protégée</span><span class="sxs-lookup"><span data-stu-id="03ddd-135">More information on making a REST call against a protected API</span></span>

<span data-ttu-id="03ddd-136">Dans l’exemple d’application créé par ce guide, la méthode `callWebApiWithToken()` est utilisée pour envoyer une demande HTTP `GET` à une ressource protégée qui nécessite un jeton, puis pour retourner le contenu à l’appelant.</span><span class="sxs-lookup"><span data-stu-id="03ddd-136">In the sample application created by this guide, the `callWebApiWithToken()` method is used to make an HTTP `GET` request against a protected resource that requires a token and then return the content to the caller.</span></span> <span data-ttu-id="03ddd-137">Cette méthode ajoute le jeton acquis à l’*en-tête d’autorisation HTTP*.</span><span class="sxs-lookup"><span data-stu-id="03ddd-137">This method adds the acquired token in the *HTTP Authorization header*.</span></span> <span data-ttu-id="03ddd-138">Dans l’exemple d’application créé par ce guide, la ressource est le point de terminaison *me* de l’API Microsoft Graph, qui affiche les informations de profil de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="03ddd-138">For the sample application created by this guide, the resource is the Microsoft Graph API *me* endpoint – which displays the user's profile information.</span></span>

<!--end-collapse-->

## <a name="add-a-method-to-sign-out-the-user"></a><span data-ttu-id="03ddd-139">Ajouter une méthode pour déconnecter l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="03ddd-139">Add a method to sign out the user</span></span>

<span data-ttu-id="03ddd-140">Ajoutez le code suivant à votre fichier `app.js` :</span><span class="sxs-lookup"><span data-stu-id="03ddd-140">Add the following code to your `app.js` file:</span></span>

```javascript
/**
 * Sign-out the user
 */
function signOut() {
    userAgentApplication.logout();
}
```
