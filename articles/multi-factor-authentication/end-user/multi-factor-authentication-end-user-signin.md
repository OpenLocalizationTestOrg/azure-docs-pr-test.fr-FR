---
title: "aaaAzure MFA connectez-vous avec vérification en deux étapes | Documents Microsoft"
description: "Cette page vous fournira des conseils sur où toogo toosee hello différentes méthodes de connexion disponibles avec l’authentification Multifacteur Azure."
keywords: "authentification de l'utilisateur, expérience de connexion, connexion avec un téléphone mobile, connexion avec le téléphone de bureau"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: b310b762-471b-4b26-887a-a321c9e81d46
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/02/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: end-user
ms.openlocfilehash: fcd5eb5e8426eda537db9e099bf247bde29c195b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-sign-in-experience-with-azure-multi-factor-authentication"></a><span data-ttu-id="556c6-104">expérience Hello de connexion avec l’authentification multifacteur Azure</span><span class="sxs-lookup"><span data-stu-id="556c6-104">hello sign-in experience with Azure Multi-Factor Authentication</span></span>
> [!NOTE]
> <span data-ttu-id="556c6-105">Hello cet article vise toowalk via une expérience d’authentification classique.</span><span class="sxs-lookup"><span data-stu-id="556c6-105">hello purpose of this article is toowalk through a typical sign-in experience.</span></span> <span data-ttu-id="556c6-106">Pour plus d’informations la signature ou des problèmes de tootroubleshoot, consultez [rencontre des problèmes avec l’authentification multifacteur Azure](multi-factor-authentication-end-user-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="556c6-106">For help with signing in, or tootroubleshoot problems, see [Having trouble with Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span></span>

## <a name="what-will-your-sign-in-experience-be"></a><span data-ttu-id="556c6-107">Quelle sera votre expérience de connexion ?</span><span class="sxs-lookup"><span data-stu-id="556c6-107">What will your sign-in experience be?</span></span>
<span data-ttu-id="556c6-108">Votre expérience de connexion diffère selon que vous choisissez toouse comme votre second facteur : un appel téléphonique, d’une application d’authentification ou de textes.</span><span class="sxs-lookup"><span data-stu-id="556c6-108">Your sign-in experience differs depending on what you choose toouse as your second factor: a phone call, an authentication app, or texts.</span></span> <span data-ttu-id="556c6-109">Choisissez l’option hello qui décrit le mieux ce que vous faites :</span><span class="sxs-lookup"><span data-stu-id="556c6-109">Choose hello option that best describes what you are doing:</span></span>

| <span data-ttu-id="556c6-110">Comment vous connectez-vous ?</span><span class="sxs-lookup"><span data-stu-id="556c6-110">How do you sign in?</span></span> | 
| --- |
| [<span data-ttu-id="556c6-111">Avec un téléphone mobile ou bureau de toomy appel téléphonique</span><span class="sxs-lookup"><span data-stu-id="556c6-111">With a phone call toomy mobile or office phone</span></span>](#signing-in-with-a-phone-call) |
| [<span data-ttu-id="556c6-112">Avec un texte toomy un téléphone mobile</span><span class="sxs-lookup"><span data-stu-id="556c6-112">With a text toomy mobile phone</span></span>](#signing-in-with-a-text-message)
| [<span data-ttu-id="556c6-113">Des notifications à partir de l’application de Microsoft Authenticator hello</span><span class="sxs-lookup"><span data-stu-id="556c6-113">With notifications from hello Microsoft Authenticator app</span></span>](#signing-in-with-the-microsoft-authenticator-app-using-notification) |
| [<span data-ttu-id="556c6-114">Avec les codes de vérification à partir de l’application de Microsoft Authenticator hello</span><span class="sxs-lookup"><span data-stu-id="556c6-114">With verification codes from hello Microsoft Authenticator app</span></span>](#signing-in-with-the-microsoft-authenticator-app-using-verification-code) |
| [<span data-ttu-id="556c6-115">Avec une autre méthode, car je ne peux pas utiliser ma méthode préférée à l’heure actuelle</span><span class="sxs-lookup"><span data-stu-id="556c6-115">With an alternate method, because I can't use my preferred method right now</span></span>](#signing-in-with-an-alternate-method) |

## <a name="signing-in-with-a-phone-call"></a><span data-ttu-id="556c6-116">Connexion avec un appel téléphonique</span><span class="sxs-lookup"><span data-stu-id="556c6-116">Signing in with a phone call</span></span>
<span data-ttu-id="556c6-117">Hello informations suivantes décrit l’expérience de vérification en deux étapes hello avec un appareil mobile tooyour d’appel ou de téléphone de bureau.</span><span class="sxs-lookup"><span data-stu-id="556c6-117">hello following information describes hello two-step verification experience with a call tooyour mobile or office phone.</span></span>

1. <span data-ttu-id="556c6-118">Se connecter tooan application ou service tel qu’Office 365 à l’aide de votre nom d’utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="556c6-118">Sign in tooan application or service such as Office 365 using your username and password.</span></span>  
2. <span data-ttu-id="556c6-119">Microsoft vous appelle.</span><span class="sxs-lookup"><span data-stu-id="556c6-119">Microsoft calls you.</span></span>  
3. <span data-ttu-id="556c6-120">Répondre hello téléphone et appuyez sur touche # de hello.</span><span class="sxs-lookup"><span data-stu-id="556c6-120">Answer hello phone and hit hello # key.</span></span>  

## <a name="signing-in-with-a-text-message"></a><span data-ttu-id="556c6-121">Connexion avec un message texte</span><span class="sxs-lookup"><span data-stu-id="556c6-121">Signing in with a text message</span></span>
<span data-ttu-id="556c6-122">Hello informations suivantes décrit l’expérience de vérification en deux étapes hello avec un message texte tooyour un téléphone mobile :</span><span class="sxs-lookup"><span data-stu-id="556c6-122">hello following information describes hello two-step verification experience with a text message tooyour mobile phone:</span></span>

1. <span data-ttu-id="556c6-123">Se connecter tooan application ou service tel qu’Office 365 à l’aide de votre nom d’utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="556c6-123">Sign in tooan application or service such as Office 365 using your username and password.</span></span> 
2. <span data-ttu-id="556c6-124">Microsoft vous envoie un message texte qui contient un code à chiffres.</span><span class="sxs-lookup"><span data-stu-id="556c6-124">Microsoft sends you a text message that contains a number code.</span></span> 
3. <span data-ttu-id="556c6-125">Entrez les code hello dans zone hello fournie sur la page de connexion hello.</span><span class="sxs-lookup"><span data-stu-id="556c6-125">Enter hello code in hello box provided on hello sign-in page.</span></span> 

## <a name="signing-in-with-hello-microsoft-authenticator-app"></a><span data-ttu-id="556c6-126">Connecter à l’application de Microsoft Authenticator hello</span><span class="sxs-lookup"><span data-stu-id="556c6-126">Signing in with hello Microsoft Authenticator app</span></span> 
<span data-ttu-id="556c6-127">Hello ci-après décrit le hello expérience de l’utilisation d’application de Microsoft Authenticator hello pour les vérifications en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="556c6-127">hello following information describes hello experience of using hello Microsoft Authenticator app for two-step verifications.</span></span> <span data-ttu-id="556c6-128">Il existe deux façons différentes toouse hello application.</span><span class="sxs-lookup"><span data-stu-id="556c6-128">There are two different ways toouse hello app.</span></span> <span data-ttu-id="556c6-129">Vous pouvez recevoir des notifications push sur votre appareil, ou vous pouvez ouvrir hello application tooget un code de vérification.</span><span class="sxs-lookup"><span data-stu-id="556c6-129">You can receive push notifications on your device, or you can open hello app tooget a verification code.</span></span>

### <a name="toosign-in-with-a-notification-from-hello-microsoft-authenticator-app"></a><span data-ttu-id="556c6-130">toosign avec une notification à partir de l’application de Microsoft Authenticator hello</span><span class="sxs-lookup"><span data-stu-id="556c6-130">toosign in with a notification from hello Microsoft Authenticator app</span></span>
1. <span data-ttu-id="556c6-131">Se connecter tooan application ou service tel qu’Office 365 à l’aide de votre nom d’utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="556c6-131">Sign in tooan application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="556c6-132">Microsoft envoie une application de Microsoft Authenticator toohello notification sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="556c6-132">Microsoft sends a notification toohello Microsoft Authenticator app on your device.</span></span>

  ![Microsoft envoie une notification](./media/multi-factor-authentication-end-user-signin/notify.png)

3. <span data-ttu-id="556c6-134">Notification hello ouvert sur votre téléphone et les sélectionner hello **Vérifiez** clé.</span><span class="sxs-lookup"><span data-stu-id="556c6-134">Open hello notification on your phone and select hello **Verify** key.</span></span> <span data-ttu-id="556c6-135">Si votre entreprise requiert un code confidentiel, vous pouvez l’entrer ici.</span><span class="sxs-lookup"><span data-stu-id="556c6-135">If your company requires a PIN, enter it here.</span></span>
4. <span data-ttu-id="556c6-136">Vous devez maintenant être connecté.</span><span class="sxs-lookup"><span data-stu-id="556c6-136">You should now be signed in.</span></span>

### <a name="toosign-in-using-a-verification-code-with-hello-microsoft-authenticator-app"></a><span data-ttu-id="556c6-137">toosign à l’aide d’un code de vérification avec application de Microsoft Authenticator hello</span><span class="sxs-lookup"><span data-stu-id="556c6-137">toosign in using a verification code with hello Microsoft Authenticator app</span></span>

<span data-ttu-id="556c6-138">Si vous utilisez des codes de vérification hello tooget de l’application Microsoft Authenticator, lorsque vous ouvrez l’application hello, vous consultez un nombre sous le nom de votre compte.</span><span class="sxs-lookup"><span data-stu-id="556c6-138">If you use hello Microsoft Authenticator app tooget verification codes, then when you open hello app you see a number under your account name.</span></span> <span data-ttu-id="556c6-139">Ce nombre change toutes les 30 secondes afin que vous n’utilisez pas hello même nombre à deux reprises.</span><span class="sxs-lookup"><span data-stu-id="556c6-139">This number changes every 30 seconds so that you don't use hello same number twice.</span></span> <span data-ttu-id="556c6-140">Lorsque vous êtes invité à entrer un code de vérification, ouvrez l’application hello et utiliser le nombre est actuellement affiché.</span><span class="sxs-lookup"><span data-stu-id="556c6-140">When you're asked for a verification code, open hello app and use whatever number is currently displayed.</span></span> 

1. <span data-ttu-id="556c6-141">Se connecter tooan application ou service tel qu’Office 365 à l’aide de votre nom d’utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="556c6-141">Sign in tooan application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="556c6-142">Microsoft vous demande un code de vérification.</span><span class="sxs-lookup"><span data-stu-id="556c6-142">Microsoft prompts you for a verification code.</span></span>

  ![Entrer le code de vérification](./media/multi-factor-authentication-end-user-signin/verify3.png)

3. <span data-ttu-id="556c6-144">Ouvrez l’application de Microsoft Authenticator hello sur votre téléphone et entrez les code de hello dans zone hello où vous vous connectez.</span><span class="sxs-lookup"><span data-stu-id="556c6-144">Open hello Microsoft Authenticator app on your phone and enter hello code in hello box where you are signing in.</span></span>

## <a name="signing-in-with-an-alternate-method"></a><span data-ttu-id="556c6-145">Connexion avec une autre méthode</span><span class="sxs-lookup"><span data-stu-id="556c6-145">Signing in with an alternate method</span></span>
<span data-ttu-id="556c6-146">Parfois, vous n’avez hello téléphone ou un périphérique que vous avez configurée comme méthode de vérification préférée.</span><span class="sxs-lookup"><span data-stu-id="556c6-146">Sometimes you don't have hello phone or device that you set up as your preferred verification method.</span></span> <span data-ttu-id="556c6-147">C’est la raison pour laquelle nous vous recommandons de définir des méthodes de sauvegarde pour votre compte.</span><span class="sxs-lookup"><span data-stu-id="556c6-147">This situation is why we recommend that you set up backup methods for your account.</span></span> <span data-ttu-id="556c6-148">Hello section suivante vous montre comment toosign avec une autre méthode de votre méthode principale n’est peut-être pas disponible.</span><span class="sxs-lookup"><span data-stu-id="556c6-148">hello following section shows you how toosign in with an alternate method when your primary method may not be available.</span></span>

1. <span data-ttu-id="556c6-149">Se connecter tooan application ou service tel qu’Office 365 à l’aide de votre nom d’utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="556c6-149">Sign in tooan application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="556c6-150">Sélectionnez **Utiliser une autre option de vérification**.</span><span class="sxs-lookup"><span data-stu-id="556c6-150">Select **Use a different verification option**.</span></span> <span data-ttu-id="556c6-151">Vous voyez autant d’options de vérification que vous en avez configurées.</span><span class="sxs-lookup"><span data-stu-id="556c6-151">You see different verification options based on how many you have setup.</span></span>
3. <span data-ttu-id="556c6-152">Choisissez une autre méthode et connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="556c6-152">Choose an alternate method and sign in.</span></span>

  ![Utiliser une autre méthode](./media/multi-factor-authentication-end-user-signin/alt.png)

## <a name="next-steps"></a><span data-ttu-id="556c6-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="556c6-154">Next steps</span></span>

<span data-ttu-id="556c6-155">Si vous rencontrez des problèmes de connexion avec la vérification en deux étapes, obtenez plus d’informations sur la page [Difficultés avec la vérification en deux étapes](multi-factor-authentication-end-user-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="556c6-155">If you have problems signing in with two-step verification, get more information at [Having trouble with Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span></span>

<span data-ttu-id="556c6-156">Découvrez comment trop[gérer vos paramètres de vérification en deux étapes](multi-factor-authentication-end-user-manage-settings.md).</span><span class="sxs-lookup"><span data-stu-id="556c6-156">Learn how too[Manage your two-step verification settings](multi-factor-authentication-end-user-manage-settings.md).</span></span>

<span data-ttu-id="556c6-157">Découvrez comment trop[prise en main hello Microsoft Authenticator application](microsoft-authenticator-app-how-to.md) afin que vous puissiez utiliser les notifications toosign, au lieu de textes et les appels téléphoniques.</span><span class="sxs-lookup"><span data-stu-id="556c6-157">Find out how too[Get started with hello Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) so that you can use notifications toosign in, instead of texts and phone calls.</span></span> 
