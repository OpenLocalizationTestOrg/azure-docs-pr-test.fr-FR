---
title: "Prise en main d’Azure AD v2 avec les applications de bureau Windows - Test | Documents Microsoft"
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
ms.openlocfilehash: 972cc48057c13271d725b0c973c3ccf651ad27c4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
## <a name="test-your-code"></a><span data-ttu-id="c6ab0-103">Test de votre code</span><span class="sxs-lookup"><span data-stu-id="c6ab0-103">Test your code</span></span>

<span data-ttu-id="c6ab0-104">Pour tester votre application, appuyez sur `F5` afin d’exécuter votre projet dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c6ab0-104">In order to test your application, press `F5` to run your project in Visual Studio.</span></span> <span data-ttu-id="c6ab0-105">Votre fenêtre principale doit alors s’afficher :</span><span class="sxs-lookup"><span data-stu-id="c6ab0-105">Your Main Window should appear:</span></span>

![Exemple d’écran](media/active-directory-mobileanddesktopapp-windowsdesktop-test/samplescreenshot.png)

<span data-ttu-id="c6ab0-107">Lorsque vous êtes prêt pour le test, cliquez sur *Call Microsoft Graph API* (Appeler l’API Microsoft Graph) et utilisez un compte Microsoft Azure Active Directory (compte de société) ou un compte Microsoft (live.com, outlook.com) pour vous connecter.</span><span class="sxs-lookup"><span data-stu-id="c6ab0-107">When you're ready to test, click *Call Microsoft Graph API* and use a Microsoft Azure Active Directory (organizational account) or a Microsoft Account (live.com, outlook.com) account to sign in.</span></span> <span data-ttu-id="c6ab0-108">S’il s’agit de la première fois, une fenêtre vous invitant à vous connecter s’affiche :</span><span class="sxs-lookup"><span data-stu-id="c6ab0-108">It it is the first time, you will see a window asking user to sign in:</span></span>

![Connexion](media/active-directory-mobileanddesktopapp-windowsdesktop-test/signinscreenshot.png)

### <a name="consent"></a><span data-ttu-id="c6ab0-110">Consentement</span><span class="sxs-lookup"><span data-stu-id="c6ab0-110">Consent</span></span>
<span data-ttu-id="c6ab0-111">La première fois que vous vous connectez à votre application, un écran de consentement semblable à ce qui suit, où vous devez accepter explicitement ce qui est indiqué, s’affiche :</span><span class="sxs-lookup"><span data-stu-id="c6ab0-111">The first time you sign in to your application, you will be presented with a consent screen similar to the below, where you need to explicitly accept:</span></span>

![Écran de consentement](media/active-directory-mobileanddesktopapp-windowsdesktop-test/consentscreen.png)

### <a name="expected-results"></a><span data-ttu-id="c6ab0-113">Résultats attendus</span><span class="sxs-lookup"><span data-stu-id="c6ab0-113">Expected results</span></span>
<span data-ttu-id="c6ab0-114">Vous devez voir les informations de profil utilisateur renvoyées par l’appel de l’API Microsoft Graph dans l’écran API Call Results (Résultats de l’appel d’API).</span><span class="sxs-lookup"><span data-stu-id="c6ab0-114">You should see user profile information returned by the Microsoft Graph API call on the API Call Results screen.</span></span>

<span data-ttu-id="c6ab0-115">Des informations de base sur le jeton obtenu via `AcquireTokenAsync` ou `AcquireTokenSilentAsync` doivent également s’afficher dans la zone Token Info (Informations sur le jeton) :</span><span class="sxs-lookup"><span data-stu-id="c6ab0-115">You  should also see basic information about the token acquired via `AcquireTokenAsync` or `AcquireTokenSilentAsync` in the Token Info box:</span></span>

|<span data-ttu-id="c6ab0-116">Propriété</span><span class="sxs-lookup"><span data-stu-id="c6ab0-116">Property</span></span>  |<span data-ttu-id="c6ab0-117">Format</span><span class="sxs-lookup"><span data-stu-id="c6ab0-117">Format</span></span>  |<span data-ttu-id="c6ab0-118">Description</span><span class="sxs-lookup"><span data-stu-id="c6ab0-118">Description</span></span> |
|---------|---------|---------|
|<span data-ttu-id="c6ab0-119">Nom</span><span class="sxs-lookup"><span data-stu-id="c6ab0-119">Name</span></span> | <span data-ttu-id="c6ab0-120">{Nom complet de l’utilisateur}</span><span class="sxs-lookup"><span data-stu-id="c6ab0-120">{User Full name}</span></span> |<span data-ttu-id="c6ab0-121">Prénom et nom de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c6ab0-121">The user’s first and last name</span></span>|
|<span data-ttu-id="c6ab0-122">Nom d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="c6ab0-122">Username</span></span> |<span>user@domain.com</span> |<span data-ttu-id="c6ab0-123">Nom d’utilisateur employé pour identifier l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c6ab0-123">The username used to identify the user</span></span>|
|<span data-ttu-id="c6ab0-124">Token Expires (Expiration du jeton)</span><span class="sxs-lookup"><span data-stu-id="c6ab0-124">Token Expires</span></span> |<span data-ttu-id="c6ab0-125">{DateHeure}</span><span class="sxs-lookup"><span data-stu-id="c6ab0-125">{DateTime}</span></span>         |<span data-ttu-id="c6ab0-126">Heure à laquelle le jeton expire.</span><span class="sxs-lookup"><span data-stu-id="c6ab0-126">The time on which the token expires.</span></span> <span data-ttu-id="c6ab0-127">MSAL étend la date d’expiration pour vous en renouvelant le jeton dès que nécessaire.</span><span class="sxs-lookup"><span data-stu-id="c6ab0-127">MSAL will extend the expiration date for you by renewing the token when necessary</span></span>|
|<span data-ttu-id="c6ab0-128">Access token (Jeton d’accès)</span><span class="sxs-lookup"><span data-stu-id="c6ab0-128">Access token</span></span> |<span data-ttu-id="c6ab0-129">{Chaîne}</span><span class="sxs-lookup"><span data-stu-id="c6ab0-129">{String}</span></span>         |<span data-ttu-id="c6ab0-130">Chaîne de jeton qui sera envoyée aux requêtes HTTP qui nécessitent un en-tête d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="c6ab0-130">The token string sent that will be sent to HTTP requests that require an authorization header</span></span>|

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="c6ab0-131">Informations supplémentaires sur les étendues et les autorisations déléguées</span><span class="sxs-lookup"><span data-stu-id="c6ab0-131">More information about scopes and delegated permissions</span></span>
<span data-ttu-id="c6ab0-132">L’API Graph nécessite que l’étendue `user.read` lise le profil utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c6ab0-132">Graph API requires the `user.read` scope to read user profile.</span></span> <span data-ttu-id="c6ab0-133">Par défaut, cette étendue est automatiquement ajoutée à toutes les applications inscrites dans notre portail d’inscription.</span><span class="sxs-lookup"><span data-stu-id="c6ab0-133">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="c6ab0-134">D’autres API Graph ainsi que des API personnalisées pour votre serveur principal nécessitent des étendues supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="c6ab0-134">Some other Graph APIs as well as custom APIs for your backend server require additional scopes.</span></span> <span data-ttu-id="c6ab0-135">Par exemple, pour Graph, `Calendars.Read` est requis afin de répertorier les calendriers de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c6ab0-135">For example, for Graph, `Calendars.Read` is required to list user’s calendars.</span></span> <span data-ttu-id="c6ab0-136">Pour accéder au calendrier de l’utilisateur dans le contexte d’une application, vous devez ajouter les informations d’inscription de l’application déléguée `Calendars.Read`, puis ajouter `Calendars.Read` à l’appel `AcquireTokenAsync`.</span><span class="sxs-lookup"><span data-stu-id="c6ab0-136">In order to access the user’s calendar in a context of an application, you need to add `Calendars.Read` delegated application registration’s information and then add `Calendars.Read` to the `AcquireTokenAsync` call.</span></span> <span data-ttu-id="c6ab0-137">L’utilisateur peut être invité à donner des consentements supplémentaires lorsque vous augmentez le nombre d’étendues.</span><span class="sxs-lookup"><span data-stu-id="c6ab0-137">User may be prompted for additional consents as you increase the number of scopes.</span></span>

<!--end-collapse-->



