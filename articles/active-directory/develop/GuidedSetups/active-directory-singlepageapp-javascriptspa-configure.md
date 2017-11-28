---
title: "Azure AD v2 JS SPA guidée par le programme d’installation : configuration | Documents Microsoft"
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
ms.openlocfilehash: adff529bfdc40006666cc643d49a302d7f1d09ad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
## <a name="register-your-application"></a><span data-ttu-id="62cf0-103">Inscrivez votre application</span><span class="sxs-lookup"><span data-stu-id="62cf0-103">Register your application</span></span>

<span data-ttu-id="62cf0-104">Il existe plusieurs manières de créer une application, sélectionnez un d’eux :</span><span class="sxs-lookup"><span data-stu-id="62cf0-104">There are multiple ways to create an application, please select one of them:</span></span>

### <a name="option-1-register-your-application-express-mode"></a><span data-ttu-id="62cf0-105">Option 1 : Inscrire votre application (mode Express)</span><span class="sxs-lookup"><span data-stu-id="62cf0-105">Option 1: Register your application (Express mode)</span></span>
<span data-ttu-id="62cf0-106">Maintenant, vous devez inscrire votre application dans le *portail d’inscription des applications de Microsoft* :</span><span class="sxs-lookup"><span data-stu-id="62cf0-106">Now you need to register your application in the *Microsoft Application Registration Portal*:</span></span>

1.  <span data-ttu-id="62cf0-107">Inscrivez votre application via le [portail d’inscription des applications de Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=singlePageApp&appTech=javascriptSpa&step=configure).</span><span class="sxs-lookup"><span data-stu-id="62cf0-107">Register your application via the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=singlePageApp&appTech=javascriptSpa&step=configure)</span></span>
2.  <span data-ttu-id="62cf0-108">Entrez un nom pour votre application, ainsi que votre adresse e-mail.</span><span class="sxs-lookup"><span data-stu-id="62cf0-108">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="62cf0-109">Vérifiez que l’option *Guided Setup* (Installation guidée) est bien cochée.</span><span class="sxs-lookup"><span data-stu-id="62cf0-109">Make sure the option for *Guided Setup* is checked</span></span>
4.  <span data-ttu-id="62cf0-110">Suivez les instructions à l’écran pour obtenir l’ID de l’application et collez-le dans votre code.</span><span class="sxs-lookup"><span data-stu-id="62cf0-110">Follow the instructions to obtain the application ID and paste it into your code</span></span>

### <a name="option-2-register-your-application-advanced-mode"></a><span data-ttu-id="62cf0-111">Option 2 : Inscrire votre application (mode avancé)</span><span class="sxs-lookup"><span data-stu-id="62cf0-111">Option 2: Register your application (Advanced mode)</span></span>

1. <span data-ttu-id="62cf0-112">Accédez au [portail d’inscription des applications de Microsoft](https://apps.dev.microsoft.com/portal/register-app) pour inscrire une application.</span><span class="sxs-lookup"><span data-stu-id="62cf0-112">Go to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) to register an application</span></span>
2. <span data-ttu-id="62cf0-113">Entrez un nom pour votre application, ainsi que votre adresse e-mail.</span><span class="sxs-lookup"><span data-stu-id="62cf0-113">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="62cf0-114">Vérifiez que l’option *Guided Setup* (Installation guidée) n’est pas cochée.</span><span class="sxs-lookup"><span data-stu-id="62cf0-114">Make sure the option for *Guided Setup* is unchecked</span></span>
4.  <span data-ttu-id="62cf0-115">Cliquez sur `Add Platform`, puis sélectionnez `Web`.</span><span class="sxs-lookup"><span data-stu-id="62cf0-115">Click `Add Platform`, then select `Web`</span></span>
5. <span data-ttu-id="62cf0-116">Ajouter le `Redirect URL` qui correspondent à des URL de l’application en fonction de votre serveur web.</span><span class="sxs-lookup"><span data-stu-id="62cf0-116">Add the `Redirect URL` that correspond to the application's URL based on your web server.</span></span> <span data-ttu-id="62cf0-117">Consultez les sections ci-dessous pour obtenir des instructions sur la façon de définir / obtenir l’URL de redirection dans Visual Studio et Python.</span><span class="sxs-lookup"><span data-stu-id="62cf0-117">See the sections below for instructions on how to set/ obtain the redirect URL in Visual Studio and Python.</span></span>
6. <span data-ttu-id="62cf0-118">Cliquez sur *Enregistrer*.</span><span class="sxs-lookup"><span data-stu-id="62cf0-118">Click *Save*</span></span>

> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a><span data-ttu-id="62cf0-119">Instructions Visual Studio pour obtenir l’URL de redirection</span><span class="sxs-lookup"><span data-stu-id="62cf0-119">Visual Studio instructions for obtaining redirect URL</span></span>
> <span data-ttu-id="62cf0-120">Suivez les instructions pour obtenir l’URL de redirection :</span><span class="sxs-lookup"><span data-stu-id="62cf0-120">Follow the instructions to obtain your redirect URL:</span></span>
> 1.    <span data-ttu-id="62cf0-121">Dans *l’Explorateur de solutions*, sélectionnez le projet et examinez la fenêtre `Properties` (si vous ne voyez pas une fenêtre de propriétés, appuyez sur `F4`).</span><span class="sxs-lookup"><span data-stu-id="62cf0-121">In *Solution Explorer*, select the project and look at the `Properties` window (if you don’t see a Properties window, press `F4`)</span></span>
> 2.    <span data-ttu-id="62cf0-122">Copiez la valeur de `URL` dans le Presse-papiers :</span><span class="sxs-lookup"><span data-stu-id="62cf0-122">Copy the value from `URL` to the clipboard:</span></span><br/> <span data-ttu-id="62cf0-123">![Propriétés du projet](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span><span class="sxs-lookup"><span data-stu-id="62cf0-123">![Project properties](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span></span><br />
> 3.    <span data-ttu-id="62cf0-124">Revenez à la *portail de l’enregistrement d’Application* et collez la valeur comme un `Redirect URL` et cliquez sur « Enregistrer »</span><span class="sxs-lookup"><span data-stu-id="62cf0-124">Switch back to the *Application Registration Portal* and paste the value as a `Redirect URL` and click 'Save'</span></span>

<p/>

> #### <a name="setting-redirect-url-for-python"></a><span data-ttu-id="62cf0-125">Configuration d’une URL de redirection pour Python</span><span class="sxs-lookup"><span data-stu-id="62cf0-125">Setting Redirect URL for Python</span></span>
> <span data-ttu-id="62cf0-126">Pour Python, vous pouvez définir le port du serveur web via la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="62cf0-126">For Python, you can set the web server port via command line.</span></span> <span data-ttu-id="62cf0-127">Cette configuration guidée utilise le port 8080 pour référence, vous pouvez utiliser tout autre port disponible.</span><span class="sxs-lookup"><span data-stu-id="62cf0-127">This guided setup uses the port 8080 for reference but feel free to use any other port available.</span></span> <span data-ttu-id="62cf0-128">Dans tous les cas, suivez les instructions ci-dessous pour configurer une URL de redirection dans les informations d’inscription de l’application :</span><span class="sxs-lookup"><span data-stu-id="62cf0-128">In any case, follow the instructions below to set up a redirect URL in the application registration information:</span></span><br/>
> - <span data-ttu-id="62cf0-129">Revenez à la *portail de l’enregistrement d’Application* et définissez `http://localhost:8080/` comme un `Redirect URL`, ou utilisez `http://localhost:[port]/` si vous utilisez un port TCP personnalisé (où *[port]* est le port TCP personnalisé nombre) et cliquez sur « Enregistrer »</span><span class="sxs-lookup"><span data-stu-id="62cf0-129">Switch back to the *Application Registration Portal* and set `http://localhost:8080/` as a `Redirect URL`, or use `http://localhost:[port]/` if you are using a custom TCP port (where *[port]* is the custom TCP port number) and click 'Save'</span></span>


#### <a name="configure-your-javascript-spa"></a><span data-ttu-id="62cf0-130">Configurer votre JavaScript SPA</span><span class="sxs-lookup"><span data-stu-id="62cf0-130">Configure your JavaScript SPA</span></span>

1.  <span data-ttu-id="62cf0-131">Créez un fichier nommé `msalconfig.js` contenant les informations d’inscription de l’application.</span><span class="sxs-lookup"><span data-stu-id="62cf0-131">Create a file named `msalconfig.js` containing the application registration information.</span></span> <span data-ttu-id="62cf0-132">Si vous utilisez Visual Studio, sélectionnez le projet (dossier racine du projet), cliquez avec le bouton droit, puis sélectionnez : `Add` > `New Item` > `JavaScript File`.</span><span class="sxs-lookup"><span data-stu-id="62cf0-132">If you are using Visual Studio, select the project (project root folder), right-click and select: `Add` > `New Item` > `JavaScript File`.</span></span> <span data-ttu-id="62cf0-133">Nommez-le `msalconfig.js`.</span><span class="sxs-lookup"><span data-stu-id="62cf0-133">Name it `msalconfig.js`</span></span>
2.  <span data-ttu-id="62cf0-134">Ajoutez le code suivant à votre fichier `msalconfig.js` :</span><span class="sxs-lookup"><span data-stu-id="62cf0-134">Add the following code to your `msalconfig.js` file:</span></span>

```javascript
var msalconfig = {
    clientID: "Enter_the_Application_Id_here",
    redirectUri: location.origin
};
```
<ol start="3">
<li>
<span data-ttu-id="62cf0-135">Remplacez <code>Enter_the_Application_Id_here</code> par l’ID d’application que vous venez d’enregistrer</span><span class="sxs-lookup"><span data-stu-id="62cf0-135">Replace <code>Enter_the_Application_Id_here</code> with the Application Id you just registered</span></span>
</li>
</ol>
