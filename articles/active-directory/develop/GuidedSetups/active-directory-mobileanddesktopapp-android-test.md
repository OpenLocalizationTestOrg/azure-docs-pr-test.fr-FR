---
title: aaaAzure AD v2 Android prise en main - Test | Documents Microsoft
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
ms.openlocfilehash: 499f32b46fd44cca0e52179bced49b311135d8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a><span data-ttu-id="90f47-103">Test de votre code</span><span class="sxs-lookup"><span data-stu-id="90f47-103">Test your code</span></span>

1. <span data-ttu-id="90f47-104">Déployer votre code tooyour/émulateur d’appareil.</span><span class="sxs-lookup"><span data-stu-id="90f47-104">Deploy your code tooyour device/emulator.</span></span>
2. <span data-ttu-id="90f47-105">Lorsque vous êtes prêt tootest, utilisez un Microsoft Azure Active Directory (compte professionnel) ou un toosign de compte Account Microsoft (live.com, outlook.com) dans.</span><span class="sxs-lookup"><span data-stu-id="90f47-105">When you're ready tootest, use a Microsoft Azure Active Directory (organizational account) or a Microsoft Account (live.com, outlook.com) account toosign in.</span></span> 

<span data-ttu-id="90f47-106">![Exemple d’écran](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
</span><span class="sxs-lookup"><span data-stu-id="90f47-106">![Sample screen shot](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
</span></span><br/><br/><span data-ttu-id="90f47-107">
![Connexion](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)</span><span class="sxs-lookup"><span data-stu-id="90f47-107">
![Sign-in](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)</span></span>

### <a name="consent"></a><span data-ttu-id="90f47-108">Consentement</span><span class="sxs-lookup"><span data-stu-id="90f47-108">Consent</span></span>
<span data-ttu-id="90f47-109">Hello première fois, qu'un utilisateur se connecte à l’application de tooyour, ils seront afficheront avec un consentement écran similaire toohello ci-dessous, où ils doivent accepter les tooexplicitly :</span><span class="sxs-lookup"><span data-stu-id="90f47-109">hello first time a user signs in tooyour application, they will be presented with a consent screen similar toohello below, where they need tooexplicitly accept:</span></span> 

![Consentement](media/active-directory-mobileanddesktopapp-android-test/androidconsent.png)


### <a name="expected-results"></a><span data-ttu-id="90f47-111">Résultats attendus</span><span class="sxs-lookup"><span data-stu-id="90f47-111">Expected results</span></span>
<span data-ttu-id="90f47-112">Vous devez voir les résultats de hello d’un tooMicrosoft d’appel de l’API Graph 'me' point de terminaison utilisé profil_utilisateur hello tootooobtain - https://graph.microsoft.com/v1.0/me.</span><span class="sxs-lookup"><span data-stu-id="90f47-112">You should see hello results of a call tooMicrosoft Graph API ‘me’ endpoint used tootooobtain hello user profile - https://graph.microsoft.com/v1.0/me.</span></span> <span data-ttu-id="90f47-113">Pour obtenir la liste des points de terminaison Microsoft Graph les plus courants, consultez cet [article](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).</span><span class="sxs-lookup"><span data-stu-id="90f47-113">For a list of common Microsoft Graph endpoints, please see this [article](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="90f47-114">Informations supplémentaires sur les étendues et les autorisations déléguées</span><span class="sxs-lookup"><span data-stu-id="90f47-114">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="90f47-115">Hello Microsoft Graph API nécessite hello `user.read` étendue tooread hello profil utilisateur.</span><span class="sxs-lookup"><span data-stu-id="90f47-115">hello Microsoft Graph API requires hello `user.read` scope tooread hello user's profile.</span></span> <span data-ttu-id="90f47-116">Par défaut, cette étendue est automatiquement ajoutée à toutes les applications inscrites dans notre portail d’inscription.</span><span class="sxs-lookup"><span data-stu-id="90f47-116">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="90f47-117">D’autres API pour Microsoft Graph ainsi que des API personnalisées pour votre serveur principal peuvent nécessiter des étendues supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="90f47-117">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="90f47-118">Par exemple, pour Microsoft Graph, hello étendue `Calendars.Read` est calendriers de l’utilisateur requise toolist hello.</span><span class="sxs-lookup"><span data-stu-id="90f47-118">For example, for Microsoft Graph, hello scope `Calendars.Read` is required toolist hello user’s calendars.</span></span> <span data-ttu-id="90f47-119">Dans l’ordre tooaccess hello calendrier de l’utilisateur dans un contexte d’une application, vous devez tooadd hello `Calendars.Read` délégation des informations d’inscription d’autorisation toohello application, puis ajoutez hello `Calendars.Read` étendue toohello `acquireTokenSilentAsync` appeler.</span><span class="sxs-lookup"><span data-stu-id="90f47-119">In order tooaccess hello user’s calendar in a context of an application, you need tooadd hello `Calendars.Read` delegated permission toohello application registration’s information and then add hello `Calendars.Read` scope toohello `acquireTokenSilentAsync` call.</span></span> <span data-ttu-id="90f47-120">utilisateur de Hello peut être invité pour les autorisations supplémentaires lorsque vous augmentez le nombre de hello d’étendues.</span><span class="sxs-lookup"><span data-stu-id="90f47-120">hello user may be prompted for additional consents as you increase hello number of scopes.</span></span>

<!--end-collapse-->
