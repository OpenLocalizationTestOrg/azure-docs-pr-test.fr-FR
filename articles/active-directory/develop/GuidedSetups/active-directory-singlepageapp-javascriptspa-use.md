---
title: "aaaAzure AD v2 JS SPA guidée par le programme d’installation - utilisez | Documents Microsoft"
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
ms.openlocfilehash: 4f7f824ed787d998dc4aea3dc21c95d7dfe70ae0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
## <a name="use-hello-microsoft-authentication-library-msal-toosign-in-hello-user"></a><span data-ttu-id="596b8-103">Utilisez hello bibliothèque d’authentification Microsoft (MSAL) dans toosign hello utilisateur</span><span class="sxs-lookup"><span data-stu-id="596b8-103">Use hello Microsoft Authentication Library (MSAL) toosign-in hello user</span></span>

1.  <span data-ttu-id="596b8-104">Créez un fichier appelé `app.js`.</span><span class="sxs-lookup"><span data-stu-id="596b8-104">Create a file named `app.js`.</span></span> <span data-ttu-id="596b8-105">Si vous utilisez un projet Visual Studio, sélectionnez hello (dossier racine du projet), cliquez droit et sélectionnez : `Add`  >  `New Item`  >  `JavaScript File`:</span><span class="sxs-lookup"><span data-stu-id="596b8-105">If you are using Visual Studio, select hello project (project root folder), right click and select: `Add` > `New Item` > `JavaScript File`:</span></span>
2.  <span data-ttu-id="596b8-106">Ajouter hello suivant code tooyour `app.js` fichier :</span><span class="sxs-lookup"><span data-stu-id="596b8-106">Add hello following code tooyour `app.js` file:</span></span>

```javascript
// Graph API endpoint tooshow user profile
var graphApiEndpoint = "https://graph.microsoft.com/v1.0/me";

// Graph API scope used tooobtain hello access token tooread user profile
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
    // If page is refreshed, continue toodisplay user info
    if (!userAgentApplication.isCallback(window.location.hash) && window.parent === window && !window.opener) {
        var user = userAgentApplication.getUser();
        if (user) {
            callGraphApi();
        }
    }
}

/**
 * Call hello Microsoft Graph API and display hello results on hello page. Sign hello user in if necessary
 */
function callGraphApi() {
    var user = userAgentApplication.getUser();
    if (!user) {
        // If user is not signed in, then prompt user toosign in via loginRedirect.
        // This will redirect user toohello Azure Active Directory v2 Endpoint
        userAgentApplication.loginRedirect(graphAPIScopes);
        // hello call toologinRedirect above frontloads hello consent tooquery Graph API during hello sign-in.
        // If you want toouse dynamic consent, just remove hello graphAPIScopes from loginRedirect call.
        // As such, user will be prompted toogive consent when requested access tooa resource that 
        // he/she hasn't consented before. In hello case of this application - 
        // hello first time hello Graph API call tooobtain user's profile is executed.
    } else {
        // If user is already signed in, display hello user info
        var userInfoElement = document.getElementById("userInfo");
        userInfoElement.parentElement.classList.remove("hidden");
        userInfoElement.innerHTML = JSON.stringify(user, null, 4);

        // Show Sign-Out button
        document.getElementById("signOutButton").classList.remove("hidden");

        // Now Call Graph API tooshow hello user profile information:
        var graphCallResponseElement = document.getElementById("graphResponse");
        graphCallResponseElement.parentElement.classList.remove("hidden");
        graphCallResponseElement.innerText = "Calling Graph ...";

        // In order toocall hello Graph API, an access token needs toobe acquired.
        // Try tooacquire hello token used tooquery Graph API silently first:
        userAgentApplication.acquireTokenSilent(graphAPIScopes)
            .then(function (token) {
                //After hello access token is acquired, call hello Web API, sending hello acquired token
                callWebApiWithToken(graphApiEndpoint, token, graphCallResponseElement, document.getElementById("accessToken"));

            }, function (error) {
                // If hello acquireTokenSilent() method fails, then acquire hello token interactively via acquireTokenRedirect().
                // In this case, hello browser will redirect user back toohello Azure Active Directory v2 Endpoint so hello user 
                // can reenter hello current username/ password and/ or give consent toonew permissions your application is requesting.
                // After authentication/ authorization completes, this page will be reloaded again and callGraphApi() will be executed on page load.
                // Then, acquireTokenSilent will then get hello token silently, hello Graph API call results will be made and results will be displayed in hello page.
                if (error) {
                    userAgentApplication.acquireTokenRedirect(graphAPIScopes);
                }
            });

    }
}

/**
 * Callback method from sign-in: if no errors, call callGraphApi() tooshow results.
 * @param {string} errorDesc - If error occur, hello error message
 * @param {object} token - hello token received from login
 * @param {object} error - hello error string
 * @param {string} tokenType - hello token type: usually id_token
 */
function loginCallback(errorDesc, token, error, tokenType) {
    if (errorDesc) {
        showError(msal.authority, error, errorDesc);
    } else {
        callGraphApi();
    }
}

/**
 * Show an error message in hello page
 * @param {string} endpoint - hello endpoint used for hello error message
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
### <a name="more-information"></a><span data-ttu-id="596b8-107">Informations complémentaires</span><span class="sxs-lookup"><span data-stu-id="596b8-107">More Information</span></span>

<span data-ttu-id="596b8-108">Quand un utilisateur clique sur hello *'Appeler l’API Microsoft Graph'* bouton pour hello première fois, `callGraphApi` les appels de méthode `loginRedirect` toosign utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="596b8-108">After a user clicks hello *‘Call Microsoft Graph API’* button for hello first time, `callGraphApi` method calls `loginRedirect` toosign in hello user.</span></span> <span data-ttu-id="596b8-109">Cette méthode entraîne redirection hello utilisateur toohello *point de terminaison Microsoft Azure Active Directory v2* tooprompt et valider les informations d’identification de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="596b8-109">This method results in redirecting hello user toohello *Microsoft Azure Active Directory v2 endpoint* tooprompt and validate hello user's credentials.</span></span> <span data-ttu-id="596b8-110">À la suite d’une réussite sign-in, utilisateur de hello est redirigé toohello arrière d’origine *index.html* page et un jeton est reçu, traité par `msal.js` et les informations de hello contenues dans le jeton de hello sont mis en cache.</span><span class="sxs-lookup"><span data-stu-id="596b8-110">As a result of a successful sign-in, hello user is redirected back toohello original *index.html* page, and a token is received, processed by `msal.js` and hello information contained in hello token is cached.</span></span> <span data-ttu-id="596b8-111">Ce jeton est appelé hello *le jeton d’ID* et contient des informations sur l’utilisateur hello, telles que nom d’affichage utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="596b8-111">This token is known as hello *ID token* and contains basic information about hello user, such as hello user display name.</span></span> <span data-ttu-id="596b8-112">Si vous envisagez de toouse toutes les données fournies par ce jeton à des fins, vous devez toomake que ce jeton est validé par votre tooguarantee de serveur principal qui hello jeton a été émises tooa les utilisateurs valides pour votre application.</span><span class="sxs-lookup"><span data-stu-id="596b8-112">If you plan toouse any data provided by this token for any purposes, you need toomake sure this token is validated by your backend server tooguarantee that hello token was issued tooa valid user for your application.</span></span>

<span data-ttu-id="596b8-113">Hello SPA généré par ce guide ne rend pas utiliser directement du jeton d’ID hello – au lieu de cela, il appelle `acquireTokenSilent` et/ou `acquireTokenRedirect` tooacquire un *jeton d’accès* utilisé tooquery hello Microsoft Graph API.</span><span class="sxs-lookup"><span data-stu-id="596b8-113">hello SPA generated by this guide does not make use directly of hello ID token – instead, it calls `acquireTokenSilent` and/or `acquireTokenRedirect` tooacquire an *access token* used tooquery hello Microsoft Graph API.</span></span> <span data-ttu-id="596b8-114">Si vous avez besoin d’un exemple qui valide le jeton d’ID hello, examinons [cela](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2 "exemple active-directory-javascript-singlepageapp-dotnet-webapi-v2 de Github") exemple d’application dans GitHub – exemple hello utilise une API Web ASP.NET pour la validation du jeton.</span><span class="sxs-lookup"><span data-stu-id="596b8-114">If you need a sample that validates hello ID token, take a look at [this](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2 "Github active-directory-javascript-singlepageapp-dotnet-webapi-v2 sample") sample application in GitHub – hello sample uses an ASP.NET Web API for token validation.</span></span>

#### <a name="getting-a-user-token-interactively"></a><span data-ttu-id="596b8-115">Obtention d’un jeton d’utilisateur de manière interactive</span><span class="sxs-lookup"><span data-stu-id="596b8-115">Getting a user token interactively</span></span>

<span data-ttu-id="596b8-116">Après hello initiale de connexion, vous ne souhaitez pas hello poser tooreauthenticate des utilisateurs chaque fois qu’ils ont besoin toorequest un jeton tooaccess une ressource : par conséquent, *acquireTokenSilent* doivent être utilisées la plupart des jetons de tooacquire temps hello.</span><span class="sxs-lookup"><span data-stu-id="596b8-116">After hello initial sign-in, you do not want hello ask users tooreauthenticate every time they need toorequest a token tooaccess a resource – so *acquireTokenSilent* should be used most of hello time tooacquire tokens.</span></span> <span data-ttu-id="596b8-117">Il existe cependant des situations que vous avez besoin de tooforce les utilisateurs interagissent avec le point de terminaison Azure Active Directory v2, voici quelques exemples :</span><span class="sxs-lookup"><span data-stu-id="596b8-117">There are situations however that you need tooforce users interact with Azure Active Directory v2 endpoint – some examples include:</span></span>
-   <span data-ttu-id="596b8-118">Utilisateurs auront peut-être besoin tooreenter leurs informations d’identification, car le mot de passe hello a expiré</span><span class="sxs-lookup"><span data-stu-id="596b8-118">Users may need tooreenter their credentials because hello password has expired</span></span>
-   <span data-ttu-id="596b8-119">Votre application demande une ressource tooa accès hello tooconsent de besoins utilisateur pour</span><span class="sxs-lookup"><span data-stu-id="596b8-119">Your application is requesting access tooa resource that hello user needs tooconsent to</span></span>
-   <span data-ttu-id="596b8-120">Une authentification à 2 facteurs est demandée.</span><span class="sxs-lookup"><span data-stu-id="596b8-120">Two factor authentication is required</span></span>

<span data-ttu-id="596b8-121">Appel hello *acquireTokenRedirect(scope)* entraîner de redirection du point de terminaison toohello Azure Active Directory v2 utilisateurs (ou *acquireTokenPopup(scope)* résultat dans une fenêtre contextuelle) où les utilisateurs ont besoin toointeract avec par soit confirmer leurs informations d’identification, en donnant hello consentement toohello requis de ressource ou authentification à deux facteurs hello fin.</span><span class="sxs-lookup"><span data-stu-id="596b8-121">Calling hello *acquireTokenRedirect(scope)* result in redirecting users toohello Azure Active Directory v2 endpoint (or *acquireTokenPopup(scope)* result on a popup window) where users need toointeract with by either confirming their credentials, giving hello consent toohello required resource, or completing hello two factor authentication.</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="596b8-122">Obtention d’un jeton d’utilisateur en mode silencieux</span><span class="sxs-lookup"><span data-stu-id="596b8-122">Getting a user token silently</span></span>
<span data-ttu-id="596b8-123">Hello ` acquireTokenSilent` méthode gère l’acquisition de jeton et renouvellement sans intervention de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="596b8-123">hello ` acquireTokenSilent` method handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="596b8-124">Après avoir `loginRedirect` (ou `loginPopup`) est exécuté pour hello première fois, `acquireTokenSilent` est hello méthode couramment utilisée tooobtain jetons utilisés tooaccess protégée des ressources pour les appels suivants - en tant qu’appels toorequest ou renouveler des jetons sont effectuées en mode silencieux.</span><span class="sxs-lookup"><span data-stu-id="596b8-124">After `loginRedirect` (or `loginPopup`) is executed for hello first time, `acquireTokenSilent` is hello method commonly used tooobtain tokens used tooaccess protected resources for subsequent calls - as calls toorequest or renew tokens are made silently.</span></span>
<span data-ttu-id="596b8-125">`acquireTokenSilent`peut échouer dans certains cas, par exemple, hello mot de passe a expiré.</span><span class="sxs-lookup"><span data-stu-id="596b8-125">`acquireTokenSilent` may fail in some cases – for example, hello user's password has expired.</span></span> <span data-ttu-id="596b8-126">Votre application peut gérer cette exception de deux manières :</span><span class="sxs-lookup"><span data-stu-id="596b8-126">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="596b8-127">Effectuer un appel trop`acquireTokenRedirect` immédiatement, ce qui aboutit à l’invite hello toosign utilisateur dans.</span><span class="sxs-lookup"><span data-stu-id="596b8-127">Make a call too`acquireTokenRedirect` immediately, which results in prompting hello user toosign in.</span></span> <span data-ttu-id="596b8-128">Ce modèle est couramment utilisé dans les applications en ligne où il n’existe aucun contenu non authentifié dans utilisateur toohello disponibles de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="596b8-128">This pattern is commonly used in online applications where there is no unauthenticated content in hello application available toohello user.</span></span> <span data-ttu-id="596b8-129">exemple Hello généré par cet Assistant d’installation utilise ce modèle.</span><span class="sxs-lookup"><span data-stu-id="596b8-129">hello sample generated by this guided setup uses this pattern.</span></span>

2. <span data-ttu-id="596b8-130">Les applications peuvent également faire d’un utilisateur de toohello d’indication visuelle qui une connexion à interactive étant requise, hello utilisateur sélectionne toosign du moment opportun hello dans ou application hello peut réessayer `acquireTokenSilent` ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="596b8-130">Applications can also make a visual indication toohello user that an interactive sign-in is required, so hello user can select hello right time toosign in, or hello application can retry `acquireTokenSilent` at a later time.</span></span> <span data-ttu-id="596b8-131">Elle est couramment utilisée lors de l’utilisateur de hello peut utiliser d’autres fonctionnalités de l’application hello sans dérangement - par exemple, il est contenu non authentifié disponibles dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="596b8-131">This is commonly used when hello user can use other functionality of hello application without being disrupted - for example, there is unauthenticated content available in hello application.</span></span> <span data-ttu-id="596b8-132">Dans ce cas, les utilisateur hello peuvent décider quand ils veulent toosign dans la ressource de hello protégé tooaccess ou toorefresh hello des informations obsolètes.</span><span class="sxs-lookup"><span data-stu-id="596b8-132">In this case, hello user can decide when they want toosign in tooaccess hello protected resource, or toorefresh hello outdated information.</span></span>

<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a><span data-ttu-id="596b8-133">Appeler l’API Microsoft Graph hello à l’aide du jeton hello que simplement obtenu</span><span class="sxs-lookup"><span data-stu-id="596b8-133">Call hello Microsoft Graph API using hello token you just obtained</span></span>

<span data-ttu-id="596b8-134">Ajouter hello suivant code tooyour `app.js` fichier :</span><span class="sxs-lookup"><span data-stu-id="596b8-134">Add hello following code tooyour `app.js` file:</span></span>

```javascript
/**
 * Call a Web API using an access token.
 * @param {any} endpoint - Web API endpoint
 * @param {any} token - Access token
 * @param {object} responseElement - HTML element used toodisplay hello results
 * @param {object} showTokenElement = HTML element used toodisplay hello RAW access token
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
                        // Display response in hello page
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
                        // Display response as error in hello page
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

### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="596b8-135">Plus d’informations sur l’envoi d’un appel REST à une API protégée</span><span class="sxs-lookup"><span data-stu-id="596b8-135">More information on making a REST call against a protected API</span></span>

<span data-ttu-id="596b8-136">Dans l’application d’exemple hello créée par ce guide, hello `callWebApiWithToken()` méthode est utilisée toomake HTTP `GET` demande par rapport à une ressource protégée qui requiert un appelant de contenu toohello hello jeton, puis de retourner.</span><span class="sxs-lookup"><span data-stu-id="596b8-136">In hello sample application created by this guide, hello `callWebApiWithToken()` method is used toomake an HTTP `GET` request against a protected resource that requires a token and then return hello content toohello caller.</span></span> <span data-ttu-id="596b8-137">Cette méthode ajoute un jeton de hello acquis Bonjour *en-tête d’autorisation HTTP*.</span><span class="sxs-lookup"><span data-stu-id="596b8-137">This method adds hello acquired token in hello *HTTP Authorization header*.</span></span> <span data-ttu-id="596b8-138">Pour l’application d’exemple hello créée par ce guide, les ressources hello sont hello Microsoft Graph API *me* endpoint – qui affiche des informations de profil de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="596b8-138">For hello sample application created by this guide, hello resource is hello Microsoft Graph API *me* endpoint – which displays hello user's profile information.</span></span>

<!--end-collapse-->

## <a name="add-a-method-toosign-out-hello-user"></a><span data-ttu-id="596b8-139">Ajouter un toosign méthode utilisateur de hello</span><span class="sxs-lookup"><span data-stu-id="596b8-139">Add a method toosign out hello user</span></span>

<span data-ttu-id="596b8-140">Ajouter hello suivant code tooyour `app.js` fichier :</span><span class="sxs-lookup"><span data-stu-id="596b8-140">Add hello following code tooyour `app.js` file:</span></span>

```javascript
/**
 * Sign-out hello user
 */
function signOut() {
    userAgentApplication.logout();
}
```
