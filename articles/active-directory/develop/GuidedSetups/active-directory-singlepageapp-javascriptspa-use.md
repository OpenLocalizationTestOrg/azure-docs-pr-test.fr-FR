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
## <a name="use-hello-microsoft-authentication-library-msal-toosign-in-hello-user"></a>Utilisez hello bibliothèque d’authentification Microsoft (MSAL) dans toosign hello utilisateur

1.  Créez un fichier appelé `app.js`. Si vous utilisez un projet Visual Studio, sélectionnez hello (dossier racine du projet), cliquez droit et sélectionnez : `Add`  >  `New Item`  >  `JavaScript File`:
2.  Ajouter hello suivant code tooyour `app.js` fichier :

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
### <a name="more-information"></a>Informations complémentaires

Quand un utilisateur clique sur hello *'Appeler l’API Microsoft Graph'* bouton pour hello première fois, `callGraphApi` les appels de méthode `loginRedirect` toosign utilisateur de hello. Cette méthode entraîne redirection hello utilisateur toohello *point de terminaison Microsoft Azure Active Directory v2* tooprompt et valider les informations d’identification de l’utilisateur hello. À la suite d’une réussite sign-in, utilisateur de hello est redirigé toohello arrière d’origine *index.html* page et un jeton est reçu, traité par `msal.js` et les informations de hello contenues dans le jeton de hello sont mis en cache. Ce jeton est appelé hello *le jeton d’ID* et contient des informations sur l’utilisateur hello, telles que nom d’affichage utilisateur hello. Si vous envisagez de toouse toutes les données fournies par ce jeton à des fins, vous devez toomake que ce jeton est validé par votre tooguarantee de serveur principal qui hello jeton a été émises tooa les utilisateurs valides pour votre application.

Hello SPA généré par ce guide ne rend pas utiliser directement du jeton d’ID hello – au lieu de cela, il appelle `acquireTokenSilent` et/ou `acquireTokenRedirect` tooacquire un *jeton d’accès* utilisé tooquery hello Microsoft Graph API. Si vous avez besoin d’un exemple qui valide le jeton d’ID hello, examinons [cela](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2 "exemple active-directory-javascript-singlepageapp-dotnet-webapi-v2 de Github") exemple d’application dans GitHub – exemple hello utilise une API Web ASP.NET pour la validation du jeton.

#### <a name="getting-a-user-token-interactively"></a>Obtention d’un jeton d’utilisateur de manière interactive

Après hello initiale de connexion, vous ne souhaitez pas hello poser tooreauthenticate des utilisateurs chaque fois qu’ils ont besoin toorequest un jeton tooaccess une ressource : par conséquent, *acquireTokenSilent* doivent être utilisées la plupart des jetons de tooacquire temps hello. Il existe cependant des situations que vous avez besoin de tooforce les utilisateurs interagissent avec le point de terminaison Azure Active Directory v2, voici quelques exemples :
-   Utilisateurs auront peut-être besoin tooreenter leurs informations d’identification, car le mot de passe hello a expiré
-   Votre application demande une ressource tooa accès hello tooconsent de besoins utilisateur pour
-   Une authentification à 2 facteurs est demandée.

Appel hello *acquireTokenRedirect(scope)* entraîner de redirection du point de terminaison toohello Azure Active Directory v2 utilisateurs (ou *acquireTokenPopup(scope)* résultat dans une fenêtre contextuelle) où les utilisateurs ont besoin toointeract avec par soit confirmer leurs informations d’identification, en donnant hello consentement toohello requis de ressource ou authentification à deux facteurs hello fin.

#### <a name="getting-a-user-token-silently"></a>Obtention d’un jeton d’utilisateur en mode silencieux
Hello ` acquireTokenSilent` méthode gère l’acquisition de jeton et renouvellement sans intervention de l’utilisateur. Après avoir `loginRedirect` (ou `loginPopup`) est exécuté pour hello première fois, `acquireTokenSilent` est hello méthode couramment utilisée tooobtain jetons utilisés tooaccess protégée des ressources pour les appels suivants - en tant qu’appels toorequest ou renouveler des jetons sont effectuées en mode silencieux.
`acquireTokenSilent`peut échouer dans certains cas, par exemple, hello mot de passe a expiré. Votre application peut gérer cette exception de deux manières :

1.  Effectuer un appel trop`acquireTokenRedirect` immédiatement, ce qui aboutit à l’invite hello toosign utilisateur dans. Ce modèle est couramment utilisé dans les applications en ligne où il n’existe aucun contenu non authentifié dans utilisateur toohello disponibles de l’application hello. exemple Hello généré par cet Assistant d’installation utilise ce modèle.

2. Les applications peuvent également faire d’un utilisateur de toohello d’indication visuelle qui une connexion à interactive étant requise, hello utilisateur sélectionne toosign du moment opportun hello dans ou application hello peut réessayer `acquireTokenSilent` ultérieurement. Elle est couramment utilisée lors de l’utilisateur de hello peut utiliser d’autres fonctionnalités de l’application hello sans dérangement - par exemple, il est contenu non authentifié disponibles dans l’application hello. Dans ce cas, les utilisateur hello peuvent décider quand ils veulent toosign dans la ressource de hello protégé tooaccess ou toorefresh hello des informations obsolètes.

<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a>Appeler l’API Microsoft Graph hello à l’aide du jeton hello que simplement obtenu

Ajouter hello suivant code tooyour `app.js` fichier :

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

### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a>Plus d’informations sur l’envoi d’un appel REST à une API protégée

Dans l’application d’exemple hello créée par ce guide, hello `callWebApiWithToken()` méthode est utilisée toomake HTTP `GET` demande par rapport à une ressource protégée qui requiert un appelant de contenu toohello hello jeton, puis de retourner. Cette méthode ajoute un jeton de hello acquis Bonjour *en-tête d’autorisation HTTP*. Pour l’application d’exemple hello créée par ce guide, les ressources hello sont hello Microsoft Graph API *me* endpoint – qui affiche des informations de profil de l’utilisateur hello.

<!--end-collapse-->

## <a name="add-a-method-toosign-out-hello-user"></a>Ajouter un toosign méthode utilisateur de hello

Ajouter hello suivant code tooyour `app.js` fichier :

```javascript
/**
 * Sign-out hello user
 */
function signOut() {
    userAgentApplication.logout();
}
```
