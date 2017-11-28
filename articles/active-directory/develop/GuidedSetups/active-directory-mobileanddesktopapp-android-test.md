---
title: "Prise en main d’Azure AD v2 Android - Test | Microsoft Docs"
description: "Cet article explique comment une application Android peut obtenir un jeton d’accès et appeler une ou plusieurs API Microsoft Graph qui nécessitent des jetons d’accès à partir du point de terminaison Azure Active Directory v2"
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
ms.openlocfilehash: 6df64f4820f8409bd8897d5ac24f81bffeeef102
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
## <a name="test-your-code"></a><span data-ttu-id="cf73c-103">Test de votre code</span><span class="sxs-lookup"><span data-stu-id="cf73c-103">Test your code</span></span>

1. <span data-ttu-id="cf73c-104">Déployez votre code sur votre appareil/émulateur.</span><span class="sxs-lookup"><span data-stu-id="cf73c-104">Deploy your code to your device/emulator.</span></span>
2. <span data-ttu-id="cf73c-105">Lorsque vous êtes prêt pour le test, utilisez un compte Microsoft Azure Active Directory (compte de société) ou un compte Microsoft (live.com, outlook.com) pour vous connecter.</span><span class="sxs-lookup"><span data-stu-id="cf73c-105">When you're ready to test, use a Microsoft Azure Active Directory (organizational account) or a Microsoft Account (live.com, outlook.com) account to sign in.</span></span> 

<span data-ttu-id="cf73c-106">![Exemple d’écran](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
</span><span class="sxs-lookup"><span data-stu-id="cf73c-106">![Sample screen shot](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
</span></span><br/><br/><span data-ttu-id="cf73c-107">
![Connexion](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)</span><span class="sxs-lookup"><span data-stu-id="cf73c-107">
![Sign-in](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)</span></span>

### <a name="consent"></a><span data-ttu-id="cf73c-108">Consentement</span><span class="sxs-lookup"><span data-stu-id="cf73c-108">Consent</span></span>
<span data-ttu-id="cf73c-109">La première fois qu’un utilisateur se connecte à votre application, un écran de consentement semblable à ce qui suit s’affiche. L’utilisateur doit accepter explicitement :</span><span class="sxs-lookup"><span data-stu-id="cf73c-109">The first time a user signs in to your application, they will be presented with a consent screen similar to the below, where they need to explicitly accept:</span></span> 

![Consentement](media/active-directory-mobileanddesktopapp-android-test/androidconsent.png)


### <a name="expected-results"></a><span data-ttu-id="cf73c-111">Résultats attendus</span><span class="sxs-lookup"><span data-stu-id="cf73c-111">Expected results</span></span>
<span data-ttu-id="cf73c-112">Vous devez voir les résultats d’un appel au point de terminaison me de l’API Microsoft Graph pour obtenir le profil utilisateur : https://graph.microsoft.com/v1.0/me.</span><span class="sxs-lookup"><span data-stu-id="cf73c-112">You should see the results of a call to Microsoft Graph API ‘me’ endpoint used to to obtain the user profile - https://graph.microsoft.com/v1.0/me.</span></span> <span data-ttu-id="cf73c-113">Pour obtenir la liste des points de terminaison Microsoft Graph les plus courants, consultez cet [article](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).</span><span class="sxs-lookup"><span data-stu-id="cf73c-113">For a list of common Microsoft Graph endpoints, please see this [article](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="cf73c-114">Informations supplémentaires sur les étendues et les autorisations déléguées</span><span class="sxs-lookup"><span data-stu-id="cf73c-114">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="cf73c-115">L’API Microsoft Graph nécessite l’étendue `user.read` pour lire le profil de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="cf73c-115">The Microsoft Graph API requires the `user.read` scope to read the user's profile.</span></span> <span data-ttu-id="cf73c-116">Par défaut, cette étendue est automatiquement ajoutée à toutes les applications inscrites dans notre portail d’inscription.</span><span class="sxs-lookup"><span data-stu-id="cf73c-116">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="cf73c-117">D’autres API pour Microsoft Graph ainsi que des API personnalisées pour votre serveur principal peuvent nécessiter des étendues supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="cf73c-117">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="cf73c-118">Par exemple, pour Microsoft Graph, l’étendue `Calendars.Read` est nécessaire pour dresser la liste des calendriers de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="cf73c-118">For example, for Microsoft Graph, the scope `Calendars.Read` is required to list the user’s calendars.</span></span> <span data-ttu-id="cf73c-119">Pour accéder au calendrier de l’utilisateur dans le contexte d’une application, vous devez ajouter l’autorisation déléguée `Calendars.Read` aux informations d’inscription de l’application, puis ajouter l’étendue `Calendars.Read` à l’appel `acquireTokenSilentAsync`.</span><span class="sxs-lookup"><span data-stu-id="cf73c-119">In order to access the user’s calendar in a context of an application, you need to add the `Calendars.Read` delegated permission to the application registration’s information and then add the `Calendars.Read` scope to the `acquireTokenSilentAsync` call.</span></span> <span data-ttu-id="cf73c-120">L’utilisateur peut être invité à donner des consentements supplémentaires à mesure que vous augmentez le nombre d’étendues.</span><span class="sxs-lookup"><span data-stu-id="cf73c-120">The user may be prompted for additional consents as you increase the number of scopes.</span></span>

<!--end-collapse-->
