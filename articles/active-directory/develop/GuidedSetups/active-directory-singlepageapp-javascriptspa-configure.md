---
title: "Interactive d’Active Directory v2 JS SPA aaaAzure configuration - configurer | Documents Microsoft"
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
ms.openlocfilehash: 1b93298d4bd4e17dd261dbb75502a122c30aac97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
## <a name="register-your-application"></a><span data-ttu-id="c7377-103">Inscrivez votre application</span><span class="sxs-lookup"><span data-stu-id="c7377-103">Register your application</span></span>

<span data-ttu-id="c7377-104">Il existe plusieurs façons toocreate une application, sélectionnez un d’eux :</span><span class="sxs-lookup"><span data-stu-id="c7377-104">There are multiple ways toocreate an application, please select one of them:</span></span>

### <a name="option-1-register-your-application-express-mode"></a><span data-ttu-id="c7377-105">Option 1 : Inscrire votre application (mode Express)</span><span class="sxs-lookup"><span data-stu-id="c7377-105">Option 1: Register your application (Express mode)</span></span>
<span data-ttu-id="c7377-106">Maintenant vous devez tooregister votre application Bonjour *portail de l’enregistrement d’Application Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="c7377-106">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>

1.  <span data-ttu-id="c7377-107">Inscrire votre application via hello [portail de l’enregistrement d’Application Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=singlePageApp&appTech=javascriptSpa&step=configure)</span><span class="sxs-lookup"><span data-stu-id="c7377-107">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=singlePageApp&appTech=javascriptSpa&step=configure)</span></span>
2.  <span data-ttu-id="c7377-108">Entrez un nom pour votre application, ainsi que votre adresse e-mail.</span><span class="sxs-lookup"><span data-stu-id="c7377-108">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="c7377-109">Assurez-vous qu’option de hello *guidée par le programme d’installation* est activée</span><span class="sxs-lookup"><span data-stu-id="c7377-109">Make sure hello option for *Guided Setup* is checked</span></span>
4.  <span data-ttu-id="c7377-110">Suivez l’ID de l’application hello instructions tooobtain hello et collez-le dans votre code</span><span class="sxs-lookup"><span data-stu-id="c7377-110">Follow hello instructions tooobtain hello application ID and paste it into your code</span></span>

### <a name="option-2-register-your-application-advanced-mode"></a><span data-ttu-id="c7377-111">Option 2 : Inscrire votre application (mode Avancé)</span><span class="sxs-lookup"><span data-stu-id="c7377-111">Option 2: Register your application (Advanced mode)</span></span>

1. <span data-ttu-id="c7377-112">Accédez toohello [portail de l’enregistrement d’Application Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister une application</span><span class="sxs-lookup"><span data-stu-id="c7377-112">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) tooregister an application</span></span>
2. <span data-ttu-id="c7377-113">Entrez un nom pour votre application, ainsi que votre adresse e-mail.</span><span class="sxs-lookup"><span data-stu-id="c7377-113">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="c7377-114">Assurez-vous qu’option de hello *guidée par le programme d’installation* est désactivée</span><span class="sxs-lookup"><span data-stu-id="c7377-114">Make sure hello option for *Guided Setup* is unchecked</span></span>
4.  <span data-ttu-id="c7377-115">Cliquez sur `Add Platform`, puis sélectionnez `Web`.</span><span class="sxs-lookup"><span data-stu-id="c7377-115">Click `Add Platform`, then select `Web`</span></span>
5. <span data-ttu-id="c7377-116">Ajouter hello `Redirect URL` qui correspondent aux URL de l’application toohello basée sur votre serveur web.</span><span class="sxs-lookup"><span data-stu-id="c7377-116">Add hello `Redirect URL` that correspond toohello application's URL based on your web server.</span></span> <span data-ttu-id="c7377-117">Consultez les sections hello ci-dessous pour obtenir des instructions sur la façon de tooset / obtenir l’URL de redirection hello dans Visual Studio et Python.</span><span class="sxs-lookup"><span data-stu-id="c7377-117">See hello sections below for instructions on how tooset/ obtain hello redirect URL in Visual Studio and Python.</span></span>
6. <span data-ttu-id="c7377-118">Cliquez sur *Enregistrer*.</span><span class="sxs-lookup"><span data-stu-id="c7377-118">Click *Save*</span></span>

> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a><span data-ttu-id="c7377-119">Instructions Visual Studio pour obtenir l’URL de redirection</span><span class="sxs-lookup"><span data-stu-id="c7377-119">Visual Studio instructions for obtaining redirect URL</span></span>
> <span data-ttu-id="c7377-120">Suivez hello instructions tooobtain votre URL de redirection :</span><span class="sxs-lookup"><span data-stu-id="c7377-120">Follow hello instructions tooobtain your redirect URL:</span></span>
> 1.    <span data-ttu-id="c7377-121">Dans *l’Explorateur de solutions*, sélectionnez le projet de hello et examinez hello `Properties` fenêtre (si vous ne voyez pas une fenêtre de propriétés, appuyez sur `F4`)</span><span class="sxs-lookup"><span data-stu-id="c7377-121">In *Solution Explorer*, select hello project and look at hello `Properties` window (if you don’t see a Properties window, press `F4`)</span></span>
> 2.    <span data-ttu-id="c7377-122">Copier la valeur hello à partir de `URL` toohello Presse-papiers :</span><span class="sxs-lookup"><span data-stu-id="c7377-122">Copy hello value from `URL` toohello clipboard:</span></span><br/> <span data-ttu-id="c7377-123">![Propriétés du projet](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span><span class="sxs-lookup"><span data-stu-id="c7377-123">![Project properties](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span></span><br />
> 3.    <span data-ttu-id="c7377-124">Commutateur arrière toohello *portail de l’enregistrement d’Application* et collez la valeur hello en tant qu’un `Redirect URL` et cliquez sur « Enregistrer »</span><span class="sxs-lookup"><span data-stu-id="c7377-124">Switch back toohello *Application Registration Portal* and paste hello value as a `Redirect URL` and click 'Save'</span></span>

<p/>

> #### <a name="setting-redirect-url-for-python"></a><span data-ttu-id="c7377-125">Configuration d’une URL de redirection pour Python</span><span class="sxs-lookup"><span data-stu-id="c7377-125">Setting Redirect URL for Python</span></span>
> <span data-ttu-id="c7377-126">Pour Python, vous pouvez définir le port du serveur web hello via la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="c7377-126">For Python, you can set hello web server port via command line.</span></span> <span data-ttu-id="c7377-127">Cet Assistant d’installation utilise le port 8080 hello pour référence, mais vous êtes libre toouse tout port disponible.</span><span class="sxs-lookup"><span data-stu-id="c7377-127">This guided setup uses hello port 8080 for reference but feel free toouse any other port available.</span></span> <span data-ttu-id="c7377-128">Dans tous les cas, suivez les instructions de hello sous tooset une URL de redirection dans les informations d’inscription de l’application hello :</span><span class="sxs-lookup"><span data-stu-id="c7377-128">In any case, follow hello instructions below tooset up a redirect URL in hello application registration information:</span></span><br/>
> - <span data-ttu-id="c7377-129">Commutateur toohello arrière *portail de l’enregistrement d’Application* et définissez `http://localhost:8080/` comme un `Redirect URL`, ou utilisez `http://localhost:[port]/` si vous utilisez un port TCP personnalisé (où *[port]* est le port TCP personnalisé hello nombre) et cliquez sur « Enregistrer »</span><span class="sxs-lookup"><span data-stu-id="c7377-129">Switch back toohello *Application Registration Portal* and set `http://localhost:8080/` as a `Redirect URL`, or use `http://localhost:[port]/` if you are using a custom TCP port (where *[port]* is hello custom TCP port number) and click 'Save'</span></span>


#### <a name="configure-your-javascript-spa"></a><span data-ttu-id="c7377-130">Configurer une application SPA JavaScript</span><span class="sxs-lookup"><span data-stu-id="c7377-130">Configure your JavaScript SPA</span></span>

1.  <span data-ttu-id="c7377-131">Créez un fichier nommé `msalconfig.js` contenant les informations d’inscription de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="c7377-131">Create a file named `msalconfig.js` containing hello application registration information.</span></span> <span data-ttu-id="c7377-132">Si vous utilisez un projet Visual Studio, sélectionnez hello (dossier racine du projet), avec le bouton droit et sélectionnez : `Add`  >  `New Item`  >  `JavaScript File`.</span><span class="sxs-lookup"><span data-stu-id="c7377-132">If you are using Visual Studio, select hello project (project root folder), right-click and select: `Add` > `New Item` > `JavaScript File`.</span></span> <span data-ttu-id="c7377-133">Nommez-le `msalconfig.js`.</span><span class="sxs-lookup"><span data-stu-id="c7377-133">Name it `msalconfig.js`</span></span>
2.  <span data-ttu-id="c7377-134">Ajouter hello suivant code tooyour `msalconfig.js` fichier :</span><span class="sxs-lookup"><span data-stu-id="c7377-134">Add hello following code tooyour `msalconfig.js` file:</span></span>

```javascript
var msalconfig = {
    clientID: "Enter_the_Application_Id_here",
    redirectUri: location.origin
};
```
<ol start="3">
<li>
<span data-ttu-id="c7377-135">Remplacez <code>Enter_the_Application_Id_here</code> par hello Id d’Application vous venez d’enregistrer</span><span class="sxs-lookup"><span data-stu-id="c7377-135">Replace <code>Enter_the_Application_Id_here</code> with hello Application Id you just registered</span></span>
</li>
</ol>
