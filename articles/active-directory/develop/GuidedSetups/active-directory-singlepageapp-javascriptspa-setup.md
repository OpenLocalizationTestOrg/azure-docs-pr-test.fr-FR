---
title: "aaaAzure AD v2 JS SPA guidée par le programme d’installation - installation | Documents Microsoft"
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
ms.openlocfilehash: 19e15c6c8db8bea2975f30e7505af79ccad17e02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
## <a name="setting-up-your-web-server-or-project"></a>Configuration du serveur web ou du projet

> Vous préférez toodownload de projet de cet exemple à la place ? 
> - [Télécharger le projet de Visual Studio hello](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/VisualStudio.zip)
>
> ou
> - [Télécharger les fichiers de projet hello](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/core.zip) pour un serveur web local, tels que Python
>
> Puis passez toohello [étape de Configuration](#create-an-application-express) exemple de code hello tooconfigure avant son exécution.

## <a name="prerequisites"></a>Composants requis
Un serveur web local comme [Python http.server](https://www.python.org/downloads/), [http-serveur](https://www.npmjs.com/package/http-server/), [.NET Core](https://www.microsoft.com/net/core), ou l’intégration d’IIS Express avec [Visual Studio 2017](https://www.visualstudio.com/downloads/) Cet Assistant d’installation n’est requise toorun. 

Instructions de ce guide sont basées sur Python et Visual Studio 2017, mais semble toouse libre de tout autre environnement de développement ou un serveur Web.

## <a name="create-your-project"></a>Créer votre projet 

> ### <a name="option-1-visual-studio"></a>Option 1 : Visual Studio 
> Si vous utilisez Visual Studio et créez un nouveau projet, suivez les étapes de hello ci-dessous toocreate une solution Visual Studio :
> 1.    Dans Visual Studio : `File` > `New` > `Project`
> 2.    Sous `Visual C#\Web`, sélectionnez `ASP.NET Web Application (.NET Framework)`
> 3.    Donnez un nom à votre application et cliquez sur *OK*.
> 4.    Sous `New ASP.NET Web Application`, sélectionnez `Empty`

<p/><!-- -->

> ### <a name="option-2-python-other-web-servers"></a>Option 2 : Python / autres serveurs web
> Vérifiez que vous avez installé [Python](https://www.python.org/downloads/), puis suivez les étapes hello ci-dessous :
> - Créer un dossier toohost votre application.


## <a name="create-your-single-page-applications-ui"></a>Créer l’interface utilisateur de votre application à page unique (SPA)
1.  Créez un fichier *index.html* pour votre application SPA JavaScript. Si vous utilisez un projet Visual Studio, sélectionnez hello (dossier racine du projet), cliquez droit et sélectionnez : `Add`  >  `New Item`  >  `HTML page` et nommez-le index.html
2.  Ajoutez hello après la page de codes tooyour :
```html
<!DOCTYPE html>
<html>
<head>
    <!-- bootstrap reference used for styling hello page -->
    <link href="//maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
    <title>JavaScript SPA Guided Setup</title>
</head>
<body style="margin: 40px">
    <button id="callGraphButton" type="button" class="btn btn-primary" onclick="callGraphApi()">Call Microsoft Graph API</button>
    <div id="errorMessage" class="text-danger"></div>
    <div class="hidden">
        <h3>Graph API Call Response</h3>
        <pre class="well" id="graphResponse"></pre>
    </div>
    <div class="hidden">
        <h3>Access Token</h3>
        <pre class="well" id="accessToken"></pre>
    </div>
    <div class="hidden">
        <h3>ID Token Claims</h3>
        <pre class="well" id="userInfo"></pre>
    </div>
    <button id="signOutButton" type="button" class="btn btn-primary hidden" onclick="signOut()">Sign out</button>

    <!-- This app uses cdn tooreference msal.js (recommended). 
         You can also download it from: https://github.com/AzureAD/microsoft-authentication-library-for-js -->
    <script src="https://secure.aadcdn.microsoftonline-p.com/lib/0.1.1/js/msal.min.js"></script>

    <!-- hello 'bluebird' and 'fetch' references below are required if you need toorun this application on Internet Explorer -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/bluebird/3.3.4/bluebird.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/fetch/2.0.3/fetch.min.js"></script>

    <script type="text/javascript" src="msalconfig.js"></script>
    <script type="text/javascript" src="app.js"></script>
</body>
</html>
````
