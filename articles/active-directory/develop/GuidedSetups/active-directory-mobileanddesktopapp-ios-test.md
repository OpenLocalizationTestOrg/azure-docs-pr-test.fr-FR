---
title: aaaAzure AD v2 iOS route - Test | Documents Microsoft
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
ms.openlocfilehash: 98c73eddabf9664feb19ac6878e9d7315b9aa79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
## <a name="test-querying-hello-microsoft-graph-api-from-your-ios-application"></a><span data-ttu-id="1b18b-103">Test d’interrogation hello Microsoft Graph API à partir de votre application iOS</span><span class="sxs-lookup"><span data-stu-id="1b18b-103">Test querying hello Microsoft Graph API from your iOS application</span></span>

<span data-ttu-id="1b18b-104">Appuyez sur `Command`  +  `R` code hello toorun simulateur de hello.</span><span class="sxs-lookup"><span data-stu-id="1b18b-104">Press `Command` + `R` toorun hello code in hello simulator.</span></span>

![Exemple d’écran](media/active-directory-mobileanddesktopapp-ios-test/iostestscreenshot.png)

<span data-ttu-id="1b18b-106">Quand vous êtes prêt tootest, appuyez sur *'Appeler l’API Microsoft Graph'* et vous est demandée tootype votre nom d’utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="1b18b-106">When you're ready tootest, tap *‘Call Microsoft Graph API’* and you will be prompted tootype your username and password.</span></span>

### <a name="consent"></a><span data-ttu-id="1b18b-107">Consentement</span><span class="sxs-lookup"><span data-stu-id="1b18b-107">Consent</span></span>
<span data-ttu-id="1b18b-108">Hello première fois que vous vous connectez tooyour application, vous aurez un consentement écran similaire toohello ci-dessous, où vous devez accepter les tooexplicitly :</span><span class="sxs-lookup"><span data-stu-id="1b18b-108">hello first time you sign in tooyour application, you will be presented with a consent screen similar toohello below, where you need tooexplicitly accept:</span></span>

![Écran de consentement](media/active-directory-mobileanddesktopapp-ios-test/iosconsentscreen.png)

### <a name="expected-results"></a><span data-ttu-id="1b18b-110">Résultats attendus</span><span class="sxs-lookup"><span data-stu-id="1b18b-110">Expected results</span></span>
<span data-ttu-id="1b18b-111">Vous devez voir les informations de profil utilisateur retournées par l’appel de l’API Microsoft Graph hello Bonjour *journalisation* section.</span><span class="sxs-lookup"><span data-stu-id="1b18b-111">You should see user profile information returned by hello Microsoft Graph API call in hello *Logging* section.</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="1b18b-112">Informations supplémentaires sur les étendues et les autorisations déléguées</span><span class="sxs-lookup"><span data-stu-id="1b18b-112">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="1b18b-113">Hello Microsoft Graph API nécessite hello `user.read` étendue tooread hello profil utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1b18b-113">hello Microsoft Graph API requires hello `user.read` scope tooread hello user's profile.</span></span> <span data-ttu-id="1b18b-114">Par défaut, cette étendue est automatiquement ajoutée à toutes les applications inscrites dans notre portail d’inscription.</span><span class="sxs-lookup"><span data-stu-id="1b18b-114">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="1b18b-115">D’autres API pour Microsoft Graph ainsi que des API personnalisées pour votre serveur principal peuvent nécessiter des étendues supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="1b18b-115">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="1b18b-116">Par exemple, pour Microsoft Graph, hello étendue `Calendars.Read` est calendriers de l’utilisateur requise toolist hello.</span><span class="sxs-lookup"><span data-stu-id="1b18b-116">For example, for Microsoft Graph, hello scope `Calendars.Read` is required toolist hello user’s calendars.</span></span> <span data-ttu-id="1b18b-117">Dans l’ordre tooaccess hello calendrier de l’utilisateur dans un contexte d’une application, vous devez tooadd hello `Calendars.Read` délégation des informations d’inscription d’autorisation toohello application, puis ajoutez hello `Calendars.Read` étendue toohello `acquireTokenSilent` appeler.</span><span class="sxs-lookup"><span data-stu-id="1b18b-117">In order tooaccess hello user’s calendar in a context of an application, you need tooadd hello `Calendars.Read` delegated permission toohello application registration’s information and then add hello `Calendars.Read` scope toohello `acquireTokenSilent` call.</span></span> <span data-ttu-id="1b18b-118">utilisateur de Hello peut être invité pour les autorisations supplémentaires lorsque vous augmentez le nombre de hello d’étendues.</span><span class="sxs-lookup"><span data-stu-id="1b18b-118">hello user may be prompted for additional consents as you increase hello number of scopes.</span></span>

<!--end-collapse-->



