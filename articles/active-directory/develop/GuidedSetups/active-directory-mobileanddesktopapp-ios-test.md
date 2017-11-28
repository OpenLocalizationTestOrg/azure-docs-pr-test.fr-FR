---
title: "Bien démarrer avec Azure AD v2 iOS - Test | Microsoft Docs"
description: "Cet article explique comment les applications iOS (Swift) peuvent appeler une API qui nécessite des jetons d’accès à partir d’un point de terminaison Azure Active Directory v2."
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
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: 4a88096d2b0a23708acdbc1798eac528599b4f71
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
## <a name="test-querying-the-microsoft-graph-api-from-your-ios-application"></a><span data-ttu-id="1764a-103">Tester l’interrogation de l’API Microsoft Graph à partir de votre application iOS</span><span class="sxs-lookup"><span data-stu-id="1764a-103">Test querying the Microsoft Graph API from your iOS application</span></span>

<span data-ttu-id="1764a-104">Appuyez sur `Command` + `R` pour exécuter le code dans le simulateur.</span><span class="sxs-lookup"><span data-stu-id="1764a-104">Press `Command` + `R` to run the code in the simulator.</span></span>

![Exemple d’écran](media/active-directory-mobileanddesktopapp-ios-test/iostestscreenshot.png)

<span data-ttu-id="1764a-106">Quand vous êtes prêt à tester, appuyez sur *Appeler l’API Microsoft Graph* et vous serez invité à taper votre nom d’utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="1764a-106">When you're ready to test, tap *‘Call Microsoft Graph API’* and you will be prompted to type your username and password.</span></span>

### <a name="consent"></a><span data-ttu-id="1764a-107">Consentement</span><span class="sxs-lookup"><span data-stu-id="1764a-107">Consent</span></span>
<span data-ttu-id="1764a-108">La première fois que vous vous connectez à votre application, un écran de consentement semblable à ce qui suit, où vous devez accepter explicitement ce qui est indiqué, s’affiche :</span><span class="sxs-lookup"><span data-stu-id="1764a-108">The first time you sign in to your application, you will be presented with a consent screen similar to the below, where you need to explicitly accept:</span></span>

![Écran de consentement](media/active-directory-mobileanddesktopapp-ios-test/iosconsentscreen.png)

### <a name="expected-results"></a><span data-ttu-id="1764a-110">Résultats attendus</span><span class="sxs-lookup"><span data-stu-id="1764a-110">Expected results</span></span>
<span data-ttu-id="1764a-111">Vous devez voir les informations de profil utilisateur renvoyées par l’appel de l’API Microsoft Graph dans la section *Journalisation*.</span><span class="sxs-lookup"><span data-stu-id="1764a-111">You should see user profile information returned by the Microsoft Graph API call in the *Logging* section.</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="1764a-112">Informations supplémentaires sur les étendues et les autorisations déléguées</span><span class="sxs-lookup"><span data-stu-id="1764a-112">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="1764a-113">L’API Microsoft Graph nécessite l’étendue `user.read` pour lire le profil de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1764a-113">The Microsoft Graph API requires the `user.read` scope to read the user's profile.</span></span> <span data-ttu-id="1764a-114">Par défaut, cette étendue est automatiquement ajoutée à toutes les applications inscrites dans notre portail d’inscription.</span><span class="sxs-lookup"><span data-stu-id="1764a-114">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="1764a-115">D’autres API pour Microsoft Graph ainsi que des API personnalisées pour votre serveur principal peuvent nécessiter des étendues supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="1764a-115">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="1764a-116">Par exemple, pour Microsoft Graph, l’étendue `Calendars.Read` est nécessaire pour dresser la liste des calendriers de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1764a-116">For example, for Microsoft Graph, the scope `Calendars.Read` is required to list the user’s calendars.</span></span> <span data-ttu-id="1764a-117">Pour accéder au calendrier de l’utilisateur dans le contexte d’une application, vous devez ajouter l’autorisation déléguée `Calendars.Read` aux informations d’inscription de l’application, puis ajouter l’étendue `Calendars.Read` à l’appel `acquireTokenSilent`.</span><span class="sxs-lookup"><span data-stu-id="1764a-117">In order to access the user’s calendar in a context of an application, you need to add the `Calendars.Read` delegated permission to the application registration’s information and then add the `Calendars.Read` scope to the `acquireTokenSilent` call.</span></span> <span data-ttu-id="1764a-118">L’utilisateur peut être invité à donner des consentements supplémentaires à mesure que vous augmentez le nombre d’étendues.</span><span class="sxs-lookup"><span data-stu-id="1764a-118">The user may be prompted for additional consents as you increase the number of scopes.</span></span>

<!--end-collapse-->



