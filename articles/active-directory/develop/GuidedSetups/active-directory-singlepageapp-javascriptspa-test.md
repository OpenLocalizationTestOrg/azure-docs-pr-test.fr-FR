---
title: "aaaAzure AD v2 JS SPA guidée par le programme d’installation - Test | Documents Microsoft"
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
ms.openlocfilehash: b2339431a070b5c4ad4058e6c1a9b19b83c84c1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a><span data-ttu-id="4046b-103">Test de votre code</span><span class="sxs-lookup"><span data-stu-id="4046b-103">Test your code</span></span>

> ### <a name="testing-with-visual-studio"></a><span data-ttu-id="4046b-104">Test avec Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4046b-104">Testing with Visual Studio</span></span>
> <span data-ttu-id="4046b-105">Si vous utilisez Visual Studio, appuyez sur `F5` toorun votre projet : navigateur de hello s’ouvre et vous dirige trop*http://localhost : {port}* où vous voyez hello *appeler l’API Microsoft Graph* bouton.</span><span class="sxs-lookup"><span data-stu-id="4046b-105">If you are using Visual Studio, press `F5` toorun your project: hello browser opens and directs you too*http://localhost:{port}* where you see hello *Call Microsoft Graph API* button.</span></span>

<p/><!-- -->

> ### <a name="testing-with-python-or-another-web-server"></a><span data-ttu-id="4046b-106">Test avec Python ou un autre serveur web</span><span class="sxs-lookup"><span data-stu-id="4046b-106">Testing with Python or another web server</span></span>
> <span data-ttu-id="4046b-107">Si vous n’utilisez pas Visual Studio, assurez-vous que votre serveur web est démarré et il est configuré le port TCP toolisten tooa selon hello dossier contenant votre *index.html* fichier.</span><span class="sxs-lookup"><span data-stu-id="4046b-107">If you are not using Visual Studio, make sure your web server is started and it is configured toolisten tooa TCP port based on hello folder containing your *index.html* file.</span></span> <span data-ttu-id="4046b-108">Pour Python, vous pouvez démarrer l’écoute port toohello en exécutant hello dans la commande hello invite / Terminal Server, à partir du dossier de l’application hello :</span><span class="sxs-lookup"><span data-stu-id="4046b-108">For Python, you can start listening toohello port by running hello in hello command prompt/ terminal, from hello app's folder:</span></span>
> 
> ```bash
> python -m http.server 8080
> ```
>  <span data-ttu-id="4046b-109">Ensuite, ouvrez le navigateur de hello et tapez *http://localhost : 8080* ou *http://localhost : {port}* - où hello *port* correspond toohello port de votre serveur web écoute.</span><span class="sxs-lookup"><span data-stu-id="4046b-109">Then, open hello browser and type *http://localhost:8080* or *http://localhost:{port}* - where hello *port* corresponds toohello port that your web server is listening to.</span></span> <span data-ttu-id="4046b-110">Vous devez voir le contenu de hello de votre page index.html avec hello *appeler l’API Microsoft Graph* bouton.</span><span class="sxs-lookup"><span data-stu-id="4046b-110">You should see hello contents of your index.html page with hello *Call Microsoft Graph API* button.</span></span>

## <a name="test-your-application"></a><span data-ttu-id="4046b-111">Tester votre application</span><span class="sxs-lookup"><span data-stu-id="4046b-111">Test your application</span></span>

<span data-ttu-id="4046b-112">Après avoir browser de hello charge votre *index.html*, cliquez sur hello *appeler l’API Microsoft Graph* bouton.</span><span class="sxs-lookup"><span data-stu-id="4046b-112">After hello browser loads your *index.html*, click hello *Call Microsoft Graph API* button.</span></span> <span data-ttu-id="4046b-113">S’il s’agit hello première fois, redirections du navigateur hello vous toohello Microsoft Azure Active Directory v2 point de terminaison, dans lequel vous êtes invité à entrer toosign dans.</span><span class="sxs-lookup"><span data-stu-id="4046b-113">If this is hello first time, hello browser redirects you toohello Microsoft Azure Active Directory v2 endpoint, where you are  prompted toosign in.</span></span>
 
![Exemple d’écran](media/active-directory-singlepageapp-javascriptspa-test/javascriptspascreenshot1.png)


### <a name="consent"></a><span data-ttu-id="4046b-115">Consentement</span><span class="sxs-lookup"><span data-stu-id="4046b-115">Consent</span></span>
<span data-ttu-id="4046b-116">Hello première fois que vous vous connectez tooyour application, vous sont présentées avec un consentement écran similaire toohello qui suit, où vous avez besoin de tooaccept :</span><span class="sxs-lookup"><span data-stu-id="4046b-116">hello very first time you sign in tooyour application, you are presented with a consent screen similar toohello following, where you need tooaccept:</span></span>

 ![Écran de consentement](media/active-directory-singlepageapp-javascriptspa-test/javascriptspaconsent.png)


### <a name="expected-results"></a><span data-ttu-id="4046b-118">Résultats attendus</span><span class="sxs-lookup"><span data-stu-id="4046b-118">Expected results</span></span>
<span data-ttu-id="4046b-119">Vous devez voir les informations de profil utilisateur retournées par hello réponse à un appel API Graph de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4046b-119">You should see user profile information returned by hello Microsoft Graph API call response.</span></span>
 
 ![Résultats](media/active-directory-singlepageapp-javascriptspa-test/javascriptsparesults.png)

<span data-ttu-id="4046b-121">Vous voyez également les informations de base sur le jeton hello acquis Bonjour *jeton d’accès* et *revendications de jeton d’ID* cases.</span><span class="sxs-lookup"><span data-stu-id="4046b-121">You also see basic information about hello token acquired in hello *Access Token* and *ID Token Claims* boxes.</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="4046b-122">Informations supplémentaires sur les étendues et les autorisations déléguées</span><span class="sxs-lookup"><span data-stu-id="4046b-122">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="4046b-123">Hello Microsoft Graph API nécessite hello `user.read` étendue tooread hello profil utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4046b-123">hello Microsoft Graph API requires hello `user.read` scope tooread hello user's profile.</span></span> <span data-ttu-id="4046b-124">Par défaut, cette étendue est automatiquement ajoutée à toutes les applications inscrites dans notre portail d’inscription.</span><span class="sxs-lookup"><span data-stu-id="4046b-124">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="4046b-125">D’autres API pour Microsoft Graph ainsi que des API personnalisées pour votre serveur principal peuvent nécessiter des étendues supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="4046b-125">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="4046b-126">Par exemple, pour Microsoft Graph, hello étendue `Calendars.Read` est calendriers de l’utilisateur requise toolist hello.</span><span class="sxs-lookup"><span data-stu-id="4046b-126">For example, for Microsoft Graph, hello scope `Calendars.Read` is required toolist hello user’s calendars.</span></span> <span data-ttu-id="4046b-127">Dans l’ordre tooaccess hello calendrier de l’utilisateur dans le contexte de hello d’une application, vous devez tooadd hello `Calendars.Read` délégation des informations d’inscription d’autorisation toohello application, puis ajoutez hello `Calendars.Read` étendue toohello `acquireTokenSilent` appeler.</span><span class="sxs-lookup"><span data-stu-id="4046b-127">In order tooaccess hello user’s calendar in hello context of an application, you need tooadd hello `Calendars.Read` delegated permission toohello application registration’s information and then add hello `Calendars.Read` scope toohello `acquireTokenSilent` call.</span></span> <span data-ttu-id="4046b-128">utilisateur de Hello peut être invité pour les autorisations supplémentaires lorsque vous augmentez le nombre de hello d’étendues.</span><span class="sxs-lookup"><span data-stu-id="4046b-128">hello user may be prompted for additional consents as you increase hello number of scopes.</span></span>

<span data-ttu-id="4046b-129">Si une API de service principal ne requiert pas une étendue (non recommandée), vous pouvez utiliser hello `clientId` comme étendue hello Bonjour `acquireTokenSilent` et/ou `acquireTokenRedirect` appels.</span><span class="sxs-lookup"><span data-stu-id="4046b-129">If a backend API does not require a scope (not recommended), you can use hello `clientId` as hello scope in hello `acquireTokenSilent` and/or `acquireTokenRedirect` calls.</span></span>

<!--end-collapse-->
