---
title: aaaAzure AD v2 Windows Desktop mise en route - Test | Documents Microsoft
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
ms.openlocfilehash: 0ae9612e1585c54a3fe35ba9d18f92554099b2c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a><span data-ttu-id="a9026-103">Test de votre code</span><span class="sxs-lookup"><span data-stu-id="a9026-103">Test your code</span></span>

<span data-ttu-id="a9026-104">Dans commande tootest votre application, appuyez sur `F5` toorun votre projet dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a9026-104">In order tootest your application, press `F5` toorun your project in Visual Studio.</span></span> <span data-ttu-id="a9026-105">Votre fenêtre principale doit alors s’afficher :</span><span class="sxs-lookup"><span data-stu-id="a9026-105">Your Main Window should appear:</span></span>

![Exemple d’écran](media/active-directory-mobileanddesktopapp-windowsdesktop-test/samplescreenshot.png)

<span data-ttu-id="a9026-107">Lorsque vous êtes prêt tootest, cliquez sur *appeler l’API Microsoft Graph* et utiliser un annuaire Microsoft Azure Active Directory (compte professionnel) ou un toosign de compte Account Microsoft (live.com, outlook.com) dans.</span><span class="sxs-lookup"><span data-stu-id="a9026-107">When you're ready tootest, click *Call Microsoft Graph API* and use a Microsoft Azure Active Directory (organizational account) or a Microsoft Account (live.com, outlook.com) account toosign in.</span></span> <span data-ttu-id="a9026-108">Il c’est hello la première fois, vous verrez une fenêtre demandant toosign utilisateur dans :</span><span class="sxs-lookup"><span data-stu-id="a9026-108">It it is hello first time, you will see a window asking user toosign in:</span></span>

![Connexion](media/active-directory-mobileanddesktopapp-windowsdesktop-test/signinscreenshot.png)

### <a name="consent"></a><span data-ttu-id="a9026-110">Consentement</span><span class="sxs-lookup"><span data-stu-id="a9026-110">Consent</span></span>
<span data-ttu-id="a9026-111">Hello première fois que vous vous connectez tooyour application, vous aurez un consentement écran similaire toohello ci-dessous, où vous devez accepter les tooexplicitly :</span><span class="sxs-lookup"><span data-stu-id="a9026-111">hello first time you sign in tooyour application, you will be presented with a consent screen similar toohello below, where you need tooexplicitly accept:</span></span>

![Écran de consentement](media/active-directory-mobileanddesktopapp-windowsdesktop-test/consentscreen.png)

### <a name="expected-results"></a><span data-ttu-id="a9026-113">Résultats attendus</span><span class="sxs-lookup"><span data-stu-id="a9026-113">Expected results</span></span>
<span data-ttu-id="a9026-114">Vous devez voir les informations de profil utilisateur retournées par l’appel de l’API Microsoft Graph hello sur l’écran des résultats d’appels API hello.</span><span class="sxs-lookup"><span data-stu-id="a9026-114">You should see user profile information returned by hello Microsoft Graph API call on hello API Call Results screen.</span></span>

<span data-ttu-id="a9026-115">Vous devez également voir les informations de base sur le jeton hello acquis `AcquireTokenAsync` ou `AcquireTokenSilentAsync` dans la zone des informations de jeton hello :</span><span class="sxs-lookup"><span data-stu-id="a9026-115">You  should also see basic information about hello token acquired via `AcquireTokenAsync` or `AcquireTokenSilentAsync` in hello Token Info box:</span></span>

|<span data-ttu-id="a9026-116">Propriété</span><span class="sxs-lookup"><span data-stu-id="a9026-116">Property</span></span>  |<span data-ttu-id="a9026-117">Format</span><span class="sxs-lookup"><span data-stu-id="a9026-117">Format</span></span>  |<span data-ttu-id="a9026-118">Description</span><span class="sxs-lookup"><span data-stu-id="a9026-118">Description</span></span> |
|---------|---------|---------|
|<span data-ttu-id="a9026-119">Nom</span><span class="sxs-lookup"><span data-stu-id="a9026-119">Name</span></span> | <span data-ttu-id="a9026-120">{Nom complet de l’utilisateur}</span><span class="sxs-lookup"><span data-stu-id="a9026-120">{User Full name}</span></span> |<span data-ttu-id="a9026-121">utilisateur de Hello prénom et nom</span><span class="sxs-lookup"><span data-stu-id="a9026-121">hello user’s first and last name</span></span>|
|<span data-ttu-id="a9026-122">Nom d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="a9026-122">Username</span></span> |<span>user@domain.com</span> |<span data-ttu-id="a9026-123">nom d’utilisateur Hello utilisé utilisateur de hello tooidentify</span><span class="sxs-lookup"><span data-stu-id="a9026-123">hello username used tooidentify hello user</span></span>|
|<span data-ttu-id="a9026-124">Token Expires (Expiration du jeton)</span><span class="sxs-lookup"><span data-stu-id="a9026-124">Token Expires</span></span> |<span data-ttu-id="a9026-125">{DateHeure}</span><span class="sxs-lookup"><span data-stu-id="a9026-125">{DateTime}</span></span>         |<span data-ttu-id="a9026-126">Hello expiration sur le hello jeton.</span><span class="sxs-lookup"><span data-stu-id="a9026-126">hello time on which hello token expires.</span></span> <span data-ttu-id="a9026-127">MSAL étendra date d’expiration de hello pour vous par le renouvellement de jeton hello lorsque cela est nécessaire</span><span class="sxs-lookup"><span data-stu-id="a9026-127">MSAL will extend hello expiration date for you by renewing hello token when necessary</span></span>|
|<span data-ttu-id="a9026-128">Access token (Jeton d’accès)</span><span class="sxs-lookup"><span data-stu-id="a9026-128">Access token</span></span> |<span data-ttu-id="a9026-129">{Chaîne}</span><span class="sxs-lookup"><span data-stu-id="a9026-129">{String}</span></span>         |<span data-ttu-id="a9026-130">chaîne de jeton Hello envoyé des demandes de tooHTTP qui nécessitent un en-tête d’autorisation qui sera envoyé</span><span class="sxs-lookup"><span data-stu-id="a9026-130">hello token string sent that will be sent tooHTTP requests that require an authorization header</span></span>|

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="a9026-131">Informations supplémentaires sur les étendues et les autorisations déléguées</span><span class="sxs-lookup"><span data-stu-id="a9026-131">More information about scopes and delegated permissions</span></span>
<span data-ttu-id="a9026-132">L’API Graph requiert hello `user.read` tooread profil_utilisateur d’étendue.</span><span class="sxs-lookup"><span data-stu-id="a9026-132">Graph API requires hello `user.read` scope tooread user profile.</span></span> <span data-ttu-id="a9026-133">Par défaut, cette étendue est automatiquement ajoutée à toutes les applications inscrites dans notre portail d’inscription.</span><span class="sxs-lookup"><span data-stu-id="a9026-133">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="a9026-134">D’autres API Graph ainsi que des API personnalisées pour votre serveur principal nécessitent des étendues supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="a9026-134">Some other Graph APIs as well as custom APIs for your backend server require additional scopes.</span></span> <span data-ttu-id="a9026-135">Par exemple, pour un graphique, `Calendars.Read` est calendriers de l’utilisateur toolist requis.</span><span class="sxs-lookup"><span data-stu-id="a9026-135">For example, for Graph, `Calendars.Read` is required toolist user’s calendars.</span></span> <span data-ttu-id="a9026-136">Dans l’ordre tooaccess hello calendrier de l’utilisateur dans un contexte d’une application, vous devez tooadd `Calendars.Read` délégation des informations d’inscription de l’application, puis ajoutez `Calendars.Read` toohello `AcquireTokenAsync` appeler.</span><span class="sxs-lookup"><span data-stu-id="a9026-136">In order tooaccess hello user’s calendar in a context of an application, you need tooadd `Calendars.Read` delegated application registration’s information and then add `Calendars.Read` toohello `AcquireTokenAsync` call.</span></span> <span data-ttu-id="a9026-137">Utilisateur demandera peut-être d’autorisations supplémentaires lorsque vous augmentez le nombre de hello d’étendues.</span><span class="sxs-lookup"><span data-stu-id="a9026-137">User may be prompted for additional consents as you increase hello number of scopes.</span></span>

<!--end-collapse-->



