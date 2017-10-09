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
## <a name="setting-up-your-web-server-or-project"></a><span data-ttu-id="33c08-103">Configuration du serveur web ou du projet</span><span class="sxs-lookup"><span data-stu-id="33c08-103">Setting up your web server or project</span></span>

> <span data-ttu-id="33c08-104">Vous préférez toodownload de projet de cet exemple à la place ?</span><span class="sxs-lookup"><span data-stu-id="33c08-104">Prefer toodownload this sample's project instead?</span></span> 
> - [<span data-ttu-id="33c08-105">Télécharger le projet de Visual Studio hello</span><span class="sxs-lookup"><span data-stu-id="33c08-105">Download hello Visual Studio project</span></span>](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/VisualStudio.zip)
>
> <span data-ttu-id="33c08-106">ou</span><span class="sxs-lookup"><span data-stu-id="33c08-106">or</span></span>
> - <span data-ttu-id="33c08-107">[Télécharger les fichiers de projet hello](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/core.zip) pour un serveur web local, tels que Python</span><span class="sxs-lookup"><span data-stu-id="33c08-107">[Download hello project files](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/core.zip) for a local web server, such as Python</span></span>
>
> <span data-ttu-id="33c08-108">Puis passez toohello [étape de Configuration](#create-an-application-express) exemple de code hello tooconfigure avant son exécution.</span><span class="sxs-lookup"><span data-stu-id="33c08-108">And then  skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing it.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33c08-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="33c08-109">Prerequisites</span></span>
<span data-ttu-id="33c08-110">Un serveur web local comme [Python http.server](https://www.python.org/downloads/), [http-serveur](https://www.npmjs.com/package/http-server/), [.NET Core](https://www.microsoft.com/net/core), ou l’intégration d’IIS Express avec [Visual Studio 2017](https://www.visualstudio.com/downloads/) Cet Assistant d’installation n’est requise toorun.</span><span class="sxs-lookup"><span data-stu-id="33c08-110">A local web server such as [Python http.server](https://www.python.org/downloads/), [http-server](https://www.npmjs.com/package/http-server/), [.NET Core](https://www.microsoft.com/net/core), or IIS Express integration with [Visual Studio 2017](https://www.visualstudio.com/downloads/) is required toorun this guided setup.</span></span> 

<span data-ttu-id="33c08-111">Instructions de ce guide sont basées sur Python et Visual Studio 2017, mais semble toouse libre de tout autre environnement de développement ou un serveur Web.</span><span class="sxs-lookup"><span data-stu-id="33c08-111">Instructions in this guide are based on both Python and Visual Studio 2017, but feel free toouse any other development environment or Web Server.</span></span>

## <a name="create-your-project"></a><span data-ttu-id="33c08-112">Créer votre projet</span><span class="sxs-lookup"><span data-stu-id="33c08-112">Create your project</span></span> 

> ### <a name="option-1-visual-studio"></a><span data-ttu-id="33c08-113">Option 1 : Visual Studio</span><span class="sxs-lookup"><span data-stu-id="33c08-113">Option 1: Visual Studio</span></span> 
> <span data-ttu-id="33c08-114">Si vous utilisez Visual Studio et créez un nouveau projet, suivez les étapes de hello ci-dessous toocreate une solution Visual Studio :</span><span class="sxs-lookup"><span data-stu-id="33c08-114">If you are using Visual Studio and are creating a new project, follow hello steps below toocreate a new Visual Studio solution:</span></span>
> 1.    <span data-ttu-id="33c08-115">Dans Visual Studio : `File` > `New` > `Project`</span><span class="sxs-lookup"><span data-stu-id="33c08-115">In Visual Studio:  `File` > `New` > `Project`</span></span>
> 2.    <span data-ttu-id="33c08-116">Sous `Visual C#\Web`, sélectionnez `ASP.NET Web Application (.NET Framework)`</span><span class="sxs-lookup"><span data-stu-id="33c08-116">Under `Visual C#\Web`, select `ASP.NET Web Application (.NET Framework)`</span></span>
> 3.    <span data-ttu-id="33c08-117">Donnez un nom à votre application et cliquez sur *OK*.</span><span class="sxs-lookup"><span data-stu-id="33c08-117">Name your application and click *OK*</span></span>
> 4.    <span data-ttu-id="33c08-118">Sous `New ASP.NET Web Application`, sélectionnez `Empty`</span><span class="sxs-lookup"><span data-stu-id="33c08-118">Under `New ASP.NET Web Application`, select `Empty`</span></span>

<p/><!-- -->

> ### <a name="option-2-python-other-web-servers"></a><span data-ttu-id="33c08-119">Option 2 : Python / autres serveurs web</span><span class="sxs-lookup"><span data-stu-id="33c08-119">Option 2: Python/ other web servers</span></span>
> <span data-ttu-id="33c08-120">Vérifiez que vous avez installé [Python](https://www.python.org/downloads/), puis suivez les étapes hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="33c08-120">Make sure you have installed [Python](https://www.python.org/downloads/), then follow hello step below:</span></span>
> - <span data-ttu-id="33c08-121">Créer un dossier toohost votre application.</span><span class="sxs-lookup"><span data-stu-id="33c08-121">Create a folder toohost your application.</span></span>


## <a name="create-your-single-page-applications-ui"></a><span data-ttu-id="33c08-122">Créer l’interface utilisateur de votre application à page unique (SPA)</span><span class="sxs-lookup"><span data-stu-id="33c08-122">Create your single page application’s UI</span></span>
1.  <span data-ttu-id="33c08-123">Créez un fichier *index.html* pour votre application SPA JavaScript.</span><span class="sxs-lookup"><span data-stu-id="33c08-123">Create an *index.html* file for your JavaScript SPA.</span></span> <span data-ttu-id="33c08-124">Si vous utilisez un projet Visual Studio, sélectionnez hello (dossier racine du projet), cliquez droit et sélectionnez : `Add`  >  `New Item`  >  `HTML page` et nommez-le index.html</span><span class="sxs-lookup"><span data-stu-id="33c08-124">If you are using Visual Studio, select hello project (project root folder), right click and select: `Add` > `New Item` > `HTML page` and name it index.html</span></span>
2.  <span data-ttu-id="33c08-125">Ajoutez hello après la page de codes tooyour :</span><span class="sxs-lookup"><span data-stu-id="33c08-125">Add hello following code tooyour page:</span></span>
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
