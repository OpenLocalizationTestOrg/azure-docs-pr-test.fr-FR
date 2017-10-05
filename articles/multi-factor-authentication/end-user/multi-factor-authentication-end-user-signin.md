---
title: "Connexion Azure MFA à l’aide de la vérification en deux étapes | Microsoft Docs"
description: "Cette page vous fournit des conseils pour consulter les différentes méthodes de connexion disponibles avec Azure MFA."
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
ms.openlocfilehash: d12115be61ca00dfb86dd822ccae9f9096fa796a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="the-sign-in-experience-with-azure-multi-factor-authentication"></a><span data-ttu-id="d8d23-104">Expérience de connexion avec Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="d8d23-104">The sign-in experience with Azure Multi-Factor Authentication</span></span>
> [!NOTE]
> <span data-ttu-id="d8d23-105">Cet article vise à présenter de manière détaillée une expérience de connexion classique.</span><span class="sxs-lookup"><span data-stu-id="d8d23-105">The purpose of this article is to walk through a typical sign-in experience.</span></span> <span data-ttu-id="d8d23-106">Pour obtenir de l’aide concernant la connexion ou pour résoudre des problèmes, voir [Difficultés avec la vérification en deux étapes](multi-factor-authentication-end-user-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="d8d23-106">For help with signing in, or to troubleshoot problems, see [Having trouble with Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span></span>

## <a name="what-will-your-sign-in-experience-be"></a><span data-ttu-id="d8d23-107">Quelle sera votre expérience de connexion ?</span><span class="sxs-lookup"><span data-stu-id="d8d23-107">What will your sign-in experience be?</span></span>
<span data-ttu-id="d8d23-108">Votre expérience d’authentification diffère selon ce que vous choisissez d’utiliser comme second facteur : un appel téléphonique, une application d’authentification ou des messages texte.</span><span class="sxs-lookup"><span data-stu-id="d8d23-108">Your sign-in experience differs depending on what you choose to use as your second factor: a phone call, an authentication app, or texts.</span></span> <span data-ttu-id="d8d23-109">Choisissez l’option qui décrit le mieux votre utilisation :</span><span class="sxs-lookup"><span data-stu-id="d8d23-109">Choose the option that best describes what you are doing:</span></span>

| <span data-ttu-id="d8d23-110">Comment vous connectez-vous ?</span><span class="sxs-lookup"><span data-stu-id="d8d23-110">How do you sign in?</span></span> | 
| --- |
| [<span data-ttu-id="d8d23-111">Avec un appel téléphonique sur mon téléphone mobile ou de bureau</span><span class="sxs-lookup"><span data-stu-id="d8d23-111">With a phone call to my mobile or office phone</span></span>](#signing-in-with-a-phone-call) |
| [<span data-ttu-id="d8d23-112">Avec un message texte sur mon téléphone mobile</span><span class="sxs-lookup"><span data-stu-id="d8d23-112">With a text to my mobile phone</span></span>](#signing-in-with-a-text-message)
| [<span data-ttu-id="d8d23-113">Avec des notifications envoyées par l’application Microsoft Authenticator</span><span class="sxs-lookup"><span data-stu-id="d8d23-113">With notifications from the Microsoft Authenticator app</span></span>](#signing-in-with-the-microsoft-authenticator-app-using-notification) |
| [<span data-ttu-id="d8d23-114">Avec des codes de vérification envoyés par l’application Microsoft Authenticator</span><span class="sxs-lookup"><span data-stu-id="d8d23-114">With verification codes from the Microsoft Authenticator app</span></span>](#signing-in-with-the-microsoft-authenticator-app-using-verification-code) |
| [<span data-ttu-id="d8d23-115">Avec une autre méthode, car je ne peux pas utiliser ma méthode préférée à l’heure actuelle</span><span class="sxs-lookup"><span data-stu-id="d8d23-115">With an alternate method, because I can't use my preferred method right now</span></span>](#signing-in-with-an-alternate-method) |

## <a name="signing-in-with-a-phone-call"></a><span data-ttu-id="d8d23-116">Connexion avec un appel téléphonique</span><span class="sxs-lookup"><span data-stu-id="d8d23-116">Signing in with a phone call</span></span>
<span data-ttu-id="d8d23-117">Les informations suivantes décrivent l’expérience de vérification en deux étapes avec un appel sur votre téléphone mobile ou de bureau.</span><span class="sxs-lookup"><span data-stu-id="d8d23-117">The following information describes the two-step verification experience with a call to your mobile or office phone.</span></span>

1. <span data-ttu-id="d8d23-118">Connectez-vous à une application ou un service comme Office 365 à l’aide de votre nom d’utilisateur et votre mot de passe.</span><span class="sxs-lookup"><span data-stu-id="d8d23-118">Sign in to an application or service such as Office 365 using your username and password.</span></span>  
2. <span data-ttu-id="d8d23-119">Microsoft vous appelle.</span><span class="sxs-lookup"><span data-stu-id="d8d23-119">Microsoft calls you.</span></span>  
3. <span data-ttu-id="d8d23-120">Répondez au téléphone et appuyez sur la touche #.</span><span class="sxs-lookup"><span data-stu-id="d8d23-120">Answer the phone and hit the # key.</span></span>  

## <a name="signing-in-with-a-text-message"></a><span data-ttu-id="d8d23-121">Connexion avec un message texte</span><span class="sxs-lookup"><span data-stu-id="d8d23-121">Signing in with a text message</span></span>
<span data-ttu-id="d8d23-122">Les informations suivantes décrivent l’expérience de vérification en deux étapes avec un message texte sur votre téléphone mobile :</span><span class="sxs-lookup"><span data-stu-id="d8d23-122">The following information describes the two-step verification experience with a text message to your mobile phone:</span></span>

1. <span data-ttu-id="d8d23-123">Connectez-vous à une application ou un service comme Office 365 à l’aide de votre nom d’utilisateur et votre mot de passe.</span><span class="sxs-lookup"><span data-stu-id="d8d23-123">Sign in to an application or service such as Office 365 using your username and password.</span></span> 
2. <span data-ttu-id="d8d23-124">Microsoft vous envoie un message texte qui contient un code à chiffres.</span><span class="sxs-lookup"><span data-stu-id="d8d23-124">Microsoft sends you a text message that contains a number code.</span></span> 
3. <span data-ttu-id="d8d23-125">Entrez le code dans la zone appropriée sur la page de connexion.</span><span class="sxs-lookup"><span data-stu-id="d8d23-125">Enter the code in the box provided on the sign-in page.</span></span> 

## <a name="signing-in-with-the-microsoft-authenticator-app"></a><span data-ttu-id="d8d23-126">Connexion avec l’application Microsoft Authenticator</span><span class="sxs-lookup"><span data-stu-id="d8d23-126">Signing in with the Microsoft Authenticator app</span></span> 
<span data-ttu-id="d8d23-127">Les informations suivantes décrivent l’utilisation de l’application Microsoft Authenticator pour les vérifications en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="d8d23-127">The following information describes the experience of using the Microsoft Authenticator app for two-step verifications.</span></span> <span data-ttu-id="d8d23-128">Il existe deux façons différentes d’utiliser l’application.</span><span class="sxs-lookup"><span data-stu-id="d8d23-128">There are two different ways to use the app.</span></span> <span data-ttu-id="d8d23-129">Vous pouvez recevoir des notifications Push sur votre appareil ou ouvrir l’application pour obtenir un code de vérification.</span><span class="sxs-lookup"><span data-stu-id="d8d23-129">You can receive push notifications on your device, or you can open the app to get a verification code.</span></span>

### <a name="to-sign-in-with-a-notification-from-the-microsoft-authenticator-app"></a><span data-ttu-id="d8d23-130">Pour vous connecter avec des notifications envoyées par l’application Microsoft Authenticator</span><span class="sxs-lookup"><span data-stu-id="d8d23-130">To sign in with a notification from the Microsoft Authenticator app</span></span>
1. <span data-ttu-id="d8d23-131">Connectez-vous à une application ou un service comme Office 365 à l’aide de votre nom d’utilisateur et votre mot de passe.</span><span class="sxs-lookup"><span data-stu-id="d8d23-131">Sign in to an application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="d8d23-132">Microsoft envoie une notification à l’application Microsoft Authenticator sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="d8d23-132">Microsoft sends a notification to the Microsoft Authenticator app on your device.</span></span>

  ![Microsoft envoie une notification](./media/multi-factor-authentication-end-user-signin/notify.png)

3. <span data-ttu-id="d8d23-134">Ouvrez la notification sur votre téléphone, puis sélectionnez la clé **Vérifier**.</span><span class="sxs-lookup"><span data-stu-id="d8d23-134">Open the notification on your phone and select the **Verify** key.</span></span> <span data-ttu-id="d8d23-135">Si votre entreprise requiert un code confidentiel, vous pouvez l’entrer ici.</span><span class="sxs-lookup"><span data-stu-id="d8d23-135">If your company requires a PIN, enter it here.</span></span>
4. <span data-ttu-id="d8d23-136">Vous devez maintenant être connecté.</span><span class="sxs-lookup"><span data-stu-id="d8d23-136">You should now be signed in.</span></span>

### <a name="to-sign-in-using-a-verification-code-with-the-microsoft-authenticator-app"></a><span data-ttu-id="d8d23-137">Pour vous connecter à l’application Microsoft Authenticator à l’aide d’un code de vérification</span><span class="sxs-lookup"><span data-stu-id="d8d23-137">To sign in using a verification code with the Microsoft Authenticator app</span></span>

<span data-ttu-id="d8d23-138">Si vous utilisez l’application Microsoft Authenticator pour obtenir des codes de vérification, lorsque vous ouvrez l’application vous voyez un nombre sous le nom de votre compte.</span><span class="sxs-lookup"><span data-stu-id="d8d23-138">If you use the Microsoft Authenticator app to get verification codes, then when you open the app you see a number under your account name.</span></span> <span data-ttu-id="d8d23-139">Ce nombre change toutes les 30 secondes afin que vous n’utilisiez pas deux fois le même.</span><span class="sxs-lookup"><span data-stu-id="d8d23-139">This number changes every 30 seconds so that you don't use the same number twice.</span></span> <span data-ttu-id="d8d23-140">Lorsque vous êtes invité à entrer un code de vérification, ouvrez l’application et utilisez le nombre qui est actuellement affiché.</span><span class="sxs-lookup"><span data-stu-id="d8d23-140">When you're asked for a verification code, open the app and use whatever number is currently displayed.</span></span> 

1. <span data-ttu-id="d8d23-141">Connectez-vous à une application ou un service comme Office 365 à l’aide de votre nom d’utilisateur et votre mot de passe.</span><span class="sxs-lookup"><span data-stu-id="d8d23-141">Sign in to an application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="d8d23-142">Microsoft vous demande un code de vérification.</span><span class="sxs-lookup"><span data-stu-id="d8d23-142">Microsoft prompts you for a verification code.</span></span>

  ![Entrer le code de vérification](./media/multi-factor-authentication-end-user-signin/verify3.png)

3. <span data-ttu-id="d8d23-144">Ouvrez l’application Microsoft Authenticator sur votre téléphone et entrez le code dans la zone où vous vous connectez.</span><span class="sxs-lookup"><span data-stu-id="d8d23-144">Open the Microsoft Authenticator app on your phone and enter the code in the box where you are signing in.</span></span>

## <a name="signing-in-with-an-alternate-method"></a><span data-ttu-id="d8d23-145">Connexion avec une autre méthode</span><span class="sxs-lookup"><span data-stu-id="d8d23-145">Signing in with an alternate method</span></span>
<span data-ttu-id="d8d23-146">Parfois, vous n’avez pas le téléphone ou l’appareil que vous avez configuré en tant que méthode de vérification par défaut avec vous.</span><span class="sxs-lookup"><span data-stu-id="d8d23-146">Sometimes you don't have the phone or device that you set up as your preferred verification method.</span></span> <span data-ttu-id="d8d23-147">C’est la raison pour laquelle nous vous recommandons de définir des méthodes de sauvegarde pour votre compte.</span><span class="sxs-lookup"><span data-stu-id="d8d23-147">This situation is why we recommend that you set up backup methods for your account.</span></span> <span data-ttu-id="d8d23-148">La section suivante vous montre comment vous connecter avec une autre méthode quand votre méthode principale n’est pas disponible.</span><span class="sxs-lookup"><span data-stu-id="d8d23-148">The following section shows you how to sign in with an alternate method when your primary method may not be available.</span></span>

1. <span data-ttu-id="d8d23-149">Connectez-vous à une application ou un service comme Office 365 à l’aide de votre nom d’utilisateur et votre mot de passe.</span><span class="sxs-lookup"><span data-stu-id="d8d23-149">Sign in to an application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="d8d23-150">Sélectionnez **Utiliser une autre option de vérification**.</span><span class="sxs-lookup"><span data-stu-id="d8d23-150">Select **Use a different verification option**.</span></span> <span data-ttu-id="d8d23-151">Vous voyez autant d’options de vérification que vous en avez configurées.</span><span class="sxs-lookup"><span data-stu-id="d8d23-151">You see different verification options based on how many you have setup.</span></span>
3. <span data-ttu-id="d8d23-152">Choisissez une autre méthode et connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="d8d23-152">Choose an alternate method and sign in.</span></span>

  ![Utiliser une autre méthode](./media/multi-factor-authentication-end-user-signin/alt.png)

## <a name="next-steps"></a><span data-ttu-id="d8d23-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d8d23-154">Next steps</span></span>

<span data-ttu-id="d8d23-155">Si vous rencontrez des problèmes de connexion avec la vérification en deux étapes, obtenez plus d’informations sur la page [Difficultés avec la vérification en deux étapes](multi-factor-authentication-end-user-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="d8d23-155">If you have problems signing in with two-step verification, get more information at [Having trouble with Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span></span>

<span data-ttu-id="d8d23-156">Apprenez comment [gérer les paramètres de la vérification en deux étapes](multi-factor-authentication-end-user-manage-settings.md).</span><span class="sxs-lookup"><span data-stu-id="d8d23-156">Learn how to [Manage your two-step verification settings](multi-factor-authentication-end-user-manage-settings.md).</span></span>

<span data-ttu-id="d8d23-157">Découvrez comment [prendre en main l’application Microsoft Authenticator](microsoft-authenticator-app-how-to.md) afin que vous puissiez utiliser les notifications pour vous connecter, plutôt que des SMS et des appels téléphoniques.</span><span class="sxs-lookup"><span data-stu-id="d8d23-157">Find out how to [Get started with the Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) so that you can use notifications to sign in, instead of texts and phone calls.</span></span> 