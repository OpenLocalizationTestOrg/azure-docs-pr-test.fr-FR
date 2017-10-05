---
title: "Application Microsoft Authenticator pour les téléphones mobiles | Microsoft Docs"
description: "Découvrez comment effectuer une mise à niveau vers la dernière version d’Azure Authenticator."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 3065a1ee-f253-41f0-a68d-2bd84af5ffba
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: H1Hack27Feb2017, end-user
ms.openlocfilehash: 6bcb6d9f7a1e9b241fa70690016b03d6eb5887ab
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-the-microsoft-authenticator-app"></a><span data-ttu-id="20bee-103">Prise en main de l’application Microsoft Authenticator</span><span class="sxs-lookup"><span data-stu-id="20bee-103">Get started with the Microsoft Authenticator app</span></span>
<span data-ttu-id="20bee-104">L’application Microsoft Authenticator fournit un niveau supplémentaire de sécurité dans votre compte professionnel ou scolaire (p. ex. bsimon@contoso.com) ou votre compte Microsoft (p. ex. bsimon@outlook.com).</span><span class="sxs-lookup"><span data-stu-id="20bee-104">The Microsoft Authenticator app provides an additional level of security in your work or school account (for example, bsimon@contoso.com) or your Microsoft account (for example, bsimon@outlook.com).</span></span>

<span data-ttu-id="20bee-105">L’application fonctionne de l’une des deux façons suivantes :</span><span class="sxs-lookup"><span data-stu-id="20bee-105">The app works in one of two ways:</span></span>

* <span data-ttu-id="20bee-106">**Notification**.</span><span class="sxs-lookup"><span data-stu-id="20bee-106">**Notification**.</span></span> <span data-ttu-id="20bee-107">L’application peut aider à empêcher tout accès non autorisé aux comptes et à arrêter les transactions frauduleuses en envoyant une notification à votre smartphone ou tablette.</span><span class="sxs-lookup"><span data-stu-id="20bee-107">The app can help prevent unauthorized access to accounts and stop fraudulent transactions by pushing a notification to your smartphone or tablet.</span></span> <span data-ttu-id="20bee-108">Affichez simplement la notification et si elle est légitime, sélectionnez **Vérifier**.</span><span class="sxs-lookup"><span data-stu-id="20bee-108">Simply view the notification, and if it's legitimate, select **Verify**.</span></span> <span data-ttu-id="20bee-109">Sinon, vous pouvez sélectionner **Refuser**.</span><span class="sxs-lookup"><span data-stu-id="20bee-109">Otherwise, you can select **Deny**.</span></span> 
* <span data-ttu-id="20bee-110">**Code de vérification**.</span><span class="sxs-lookup"><span data-stu-id="20bee-110">**Verification code**.</span></span> <span data-ttu-id="20bee-111">L’application peut être utilisée comme jeton logiciel pour générer un code de vérification OAuth.</span><span class="sxs-lookup"><span data-stu-id="20bee-111">The app can be used as a software token to generate an OAuth verification code.</span></span> <span data-ttu-id="20bee-112">Après avoir entré votre nom d’utilisateur et votre mot de passe, vous entrez le code fourni par l’application dans l’écran de connexion.</span><span class="sxs-lookup"><span data-stu-id="20bee-112">After you enter your username and password, you enter the code provided by the app into the sign-in screen.</span></span> <span data-ttu-id="20bee-113">Le code de vérification fournit un deuxième formulaire d’authentification.</span><span class="sxs-lookup"><span data-stu-id="20bee-113">The verification code provides a second form of authentication.</span></span>

<span data-ttu-id="20bee-114">L’application Microsoft Authenticator remplace l’application Azure Authenticator.</span><span class="sxs-lookup"><span data-stu-id="20bee-114">The Microsoft Authenticator app replaces the Azure Authenticator app.</span></span> <span data-ttu-id="20bee-115">L’application Azure Authenticator continue de fonctionner, mais cet article peut vous aider si vous décidez d’adopter la nouvelle application Azure Authenticator.</span><span class="sxs-lookup"><span data-stu-id="20bee-115">The Azure Authenticator app still works, but if you decide to move to the new Microsoft Authenticator app, this article can assist you.</span></span>  

## <a name="opt-in-for-two-step-verification"></a><span data-ttu-id="20bee-116">Abonnement à la vérification en deux étapes</span><span class="sxs-lookup"><span data-stu-id="20bee-116">Opt in for two-step verification</span></span>

<span data-ttu-id="20bee-117">L’application Microsoft Authenticator ne fonctionne pas toute seule.</span><span class="sxs-lookup"><span data-stu-id="20bee-117">The Microsoft Authenticator app doesn't work by itself.</span></span> <span data-ttu-id="20bee-118">Configurez chacun de vos comptes pour être invité à exécuter une deuxième méthode de vérification après vous être connecté avec votre nom d’utilisateur et votre mot de passe.</span><span class="sxs-lookup"><span data-stu-id="20bee-118">Configure each of your accounts to prompt you for a second verification method after you sign in with your username and password.</span></span> 

<span data-ttu-id="20bee-119">En général, pour un compte professionnel ou scolaire, vous ne pouvez pas prendre cette décision vous-même.</span><span class="sxs-lookup"><span data-stu-id="20bee-119">For a work or school account, you don't usually get to choose this feature for yourself.</span></span> <span data-ttu-id="20bee-120">Un administrateur de sécurité s’abonne à votre place et vous avertit que vous devez inscrire les méthodes de vérification pour votre compte.</span><span class="sxs-lookup"><span data-stu-id="20bee-120">Instead, a security administrator opts in on your behalf and then notifies you to register verification methods for your account.</span></span> <span data-ttu-id="20bee-121">Si ce scénario vous concerne, reportez-vous à [Présentation concrète de Multi-Factor Authentication Azure](multi-factor-authentication-end-user.md).</span><span class="sxs-lookup"><span data-stu-id="20bee-121">If this scenario applies to you, learn more in [What does Azure Multi-Factor Authentication mean for me](multi-factor-authentication-end-user.md).</span></span>

<span data-ttu-id="20bee-122">Pour un compte personnel, vous devez configurer la vérification en deux étapes vous-même.</span><span class="sxs-lookup"><span data-stu-id="20bee-122">For a personal account, you need to set up two-step verification for yourself.</span></span> <span data-ttu-id="20bee-123">Si vous avez un compte Microsoft, ces étapes sont disponibles dans [À propos de la vérification en deux étapes](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification).</span><span class="sxs-lookup"><span data-stu-id="20bee-123">If you have a Microsoft account, those steps are available in [About two-step verification](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification).</span></span> 

<span data-ttu-id="20bee-124">Vous pouvez également utiliser Microsoft Authenticator avec des comptes non-Microsoft.</span><span class="sxs-lookup"><span data-stu-id="20bee-124">You can also use the Microsoft Authenticator with non-Microsoft accounts.</span></span> <span data-ttu-id="20bee-125">La fonction peut ne pas s’appeler « vérification en deux étapes », mais vous devez pouvoir la trouver dans les paramètres de sécurité ou de connexion.</span><span class="sxs-lookup"><span data-stu-id="20bee-125">They may call the feature something other than two-step verification, but you should be able to find it under security or sign-in settings.</span></span> 

## <a name="install-the-app"></a><span data-ttu-id="20bee-126">Installer l’application</span><span class="sxs-lookup"><span data-stu-id="20bee-126">Install the app</span></span>
<span data-ttu-id="20bee-127">L’application Microsoft Authenticator est disponible pour [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072) et [iOS](http://go.microsoft.com/fwlink/?Linkid=825073).</span><span class="sxs-lookup"><span data-stu-id="20bee-127">The Microsoft Authenticator app is available for [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), and [iOS](http://go.microsoft.com/fwlink/?Linkid=825073).</span></span>

## <a name="add-accounts-to-the-app"></a><span data-ttu-id="20bee-128">Ajouter des comptes à l’application</span><span class="sxs-lookup"><span data-stu-id="20bee-128">Add accounts to the app</span></span>
<span data-ttu-id="20bee-129">Pour chaque compte que vous souhaitez ajouter à l’application Microsoft Authenticator, utilisez l’une des procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="20bee-129">For each account that you want to add to the Microsoft Authenticator app, use one of the following procedures:</span></span>

### <a name="add-a-personal-microsoft-account-to-the-app"></a><span data-ttu-id="20bee-130">Ajouter un compte Microsoft personnel à l’application</span><span class="sxs-lookup"><span data-stu-id="20bee-130">Add a personal Microsoft account to the app</span></span>

<span data-ttu-id="20bee-131">Pour un compte Microsoft personnel (celui qui vous permet de vous connecter à Outlook.com, Xbox, Skype, etc.), il vous suffit de vous connecter à votre compte dans l’application Microsoft Authenticator.</span><span class="sxs-lookup"><span data-stu-id="20bee-131">For a personal Microsoft account (one that you use to sign in to Outlook.com, Xbox, Skype, etc.), all you have to do is sign in to your account in the Microsoft Authenticator app.</span></span>

### <a name="add-a-work-or-school-account-to-the-app-using-the-qr-code-scanner"></a><span data-ttu-id="20bee-132">Ajouter un compte professionnel ou scolaire à l’application à l’aide du scanneur de code QR</span><span class="sxs-lookup"><span data-stu-id="20bee-132">Add a work or school account to the app using the QR code scanner</span></span>
1. <span data-ttu-id="20bee-133">Accédez à l’écran des paramètres de vérification de la sécurité.</span><span class="sxs-lookup"><span data-stu-id="20bee-133">Go to the security verification settings screen.</span></span>  <span data-ttu-id="20bee-134">Pour savoir comment accéder à cet écran, consultez [Problèmes avec Azure Multi-Factor Authentication](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page).</span><span class="sxs-lookup"><span data-stu-id="20bee-134">For information on how to get to this screen, see [Changing your security settings](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page).</span></span>
2. <span data-ttu-id="20bee-135">Cochez la case **Application Authenticator**, puis sélectionnez **Configurer**.</span><span class="sxs-lookup"><span data-stu-id="20bee-135">Check the box next to **Authenticator app** then select **Configure**.</span></span>

    ![Le bouton Configurer sur l’écran des paramètres de vérification de la sécurité.](./media/authenticator-app-how-to/azureauthe.png)

    <span data-ttu-id="20bee-137">Cela fait apparaître un écran avec un code QR dessus.</span><span class="sxs-lookup"><span data-stu-id="20bee-137">This brings up a screen with a QR code on it.</span></span>

    ![Écran qui fournit le code QR](./media/authenticator-app-how-to/barcode2.png)
3. <span data-ttu-id="20bee-139">Ouvrez l’application Microsoft Authenticator</span><span class="sxs-lookup"><span data-stu-id="20bee-139">Open the Microsoft Authenticator app.</span></span> <span data-ttu-id="20bee-140">Sur l’écran des **comptes**, sélectionnez **+**, puis indiquez que vous souhaitez ajouter un compte professionnel ou scolaire.</span><span class="sxs-lookup"><span data-stu-id="20bee-140">On the **accounts** screen, select **+**, and then specify that you want to add a work or school account.</span></span>
4. <span data-ttu-id="20bee-141">Utilisez l’appareil photo pour scanner le code QR, puis sélectionnez **Terminé** pour fermer l’écran de code QR.</span><span class="sxs-lookup"><span data-stu-id="20bee-141">Use the camera to scan the QR code, and then select **Done** to close the QR code screen.</span></span>

    <span data-ttu-id="20bee-142">Si votre appareil photo ne fonctionne pas correctement, vous pouvez [entrer manuellement le code QR et l’URL](#add-an-account-to-the-app-manually).</span><span class="sxs-lookup"><span data-stu-id="20bee-142">If your camera is not working properly, you can [enter the QR code and URL manually](#add-an-account-to-the-app-manually).</span></span>

5. <span data-ttu-id="20bee-143">Lorsque l’application affiche le nom de votre compte souligné d’un code à six chiffres, c’est que vous avez terminé.</span><span class="sxs-lookup"><span data-stu-id="20bee-143">When the app shows your account name with a six-digit code underneath it, you're done.</span></span> 

    ![Écran de comptes](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-to-the-app-manually"></a><span data-ttu-id="20bee-145">Ajouter manuellement un compte à l’application</span><span class="sxs-lookup"><span data-stu-id="20bee-145">Add an account to the app manually</span></span>
1. <span data-ttu-id="20bee-146">Accédez à l’écran des paramètres de vérification de la sécurité.</span><span class="sxs-lookup"><span data-stu-id="20bee-146">Go to the security verification settings screen.</span></span>  <span data-ttu-id="20bee-147">Pour savoir comment accéder à cet écran, consultez [Problèmes avec Azure Multi-Factor Authentication](multi-factor-authentication-end-user-manage-settings.md).</span><span class="sxs-lookup"><span data-stu-id="20bee-147">For information on how to get to this screen, see [Changing your security settings](multi-factor-authentication-end-user-manage-settings.md).</span></span>
2. <span data-ttu-id="20bee-148">Sélectionnez **Configurer**.</span><span class="sxs-lookup"><span data-stu-id="20bee-148">Select **Configure**.</span></span>

    ![Le bouton Configurer sur l’écran des paramètres de vérification de la sécurité.](./media/authenticator-app-how-to/azureauthe.png)

    <span data-ttu-id="20bee-150">Cela fait apparaître un écran avec un code QR dessus.</span><span class="sxs-lookup"><span data-stu-id="20bee-150">This brings up a screen with a QR code on it.</span></span>  <span data-ttu-id="20bee-151">Notez le code et l’URL.</span><span class="sxs-lookup"><span data-stu-id="20bee-151">Note the code and URL.</span></span>

    ![Écran qui fournit le code QR et l’URL](./media/authenticator-app-how-to/barcode2.png)
3. <span data-ttu-id="20bee-153">Ouvrez l’application Microsoft Authenticator</span><span class="sxs-lookup"><span data-stu-id="20bee-153">Open the Microsoft Authenticator app.</span></span> <span data-ttu-id="20bee-154">Sur l’écran des **comptes**, sélectionnez **+**, puis indiquez que vous souhaitez ajouter un compte professionnel ou scolaire.</span><span class="sxs-lookup"><span data-stu-id="20bee-154">On the **accounts** screen, select **+**, and then specify that you want to add a work or school account.</span></span>

4. <span data-ttu-id="20bee-155">Dans le scanner, sélectionnez **enter code manually**(entrer le code manuellement).</span><span class="sxs-lookup"><span data-stu-id="20bee-155">In the scanner, select **enter code manually**.</span></span>

    ![Écran pour scanner un code QR](./media/multi-factor-authentication-end-user-first-time/scan2.png)
5. <span data-ttu-id="20bee-157">Entrez le code et l’URL dans les zones appropriées de l’application, puis sélectionnez **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="20bee-157">Enter the code and the URL in the appropriate boxes in the app, then select **Finish**.</span></span>

    ![Écran pour saisir le code et de l’URL](./media/authenticator-app-how-to/manual.png)

6. <span data-ttu-id="20bee-159">Lorsque l’application affiche le nom de votre compte souligné d’un code à six chiffres, c’est que vous avez terminé.</span><span class="sxs-lookup"><span data-stu-id="20bee-159">When the app shows your account name with a six-digit code underneath it, you're done.</span></span>

    ![Écran de comptes](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-to-the-app-using-touch-id"></a><span data-ttu-id="20bee-161">Ajouter un compte à l’application à l’aide de Touch ID</span><span class="sxs-lookup"><span data-stu-id="20bee-161">Add an account to the app using Touch ID</span></span>
<span data-ttu-id="20bee-162">L’application Microsoft Authenticator sur iOS prend en charge Touch ID.</span><span class="sxs-lookup"><span data-stu-id="20bee-162">The Microsoft Authenticator app on iOS supports Touch ID.</span></span>  <span data-ttu-id="20bee-163">Azure Multi-Factor Authentication permet aux organisations de demander un code confidentiel pour les appareils.</span><span class="sxs-lookup"><span data-stu-id="20bee-163">Azure Multi-Factor Authentication allows organizations to require a PIN for devices.</span></span> <span data-ttu-id="20bee-164">Avec Touch ID, les utilisateurs iOS n’ont pas besoin d’entrer de code confidentiel.</span><span class="sxs-lookup"><span data-stu-id="20bee-164">With Touch ID, iOS users don’t need to enter a PIN.</span></span> <span data-ttu-id="20bee-165">Au lieu de cela, ils peuvent analyser leur empreinte digitale et sélectionner **Approuver**.</span><span class="sxs-lookup"><span data-stu-id="20bee-165">Instead, they can scan their fingerprint and select **Approve**.</span></span>

<span data-ttu-id="20bee-166">La configuration de Touch ID avec Microsoft Authenticator est simple.</span><span class="sxs-lookup"><span data-stu-id="20bee-166">Setting up Touch ID with Microsoft Authenticator is simple.</span></span> <span data-ttu-id="20bee-167">Vous effectuez une vérification normale avec un code confidentiel.</span><span class="sxs-lookup"><span data-stu-id="20bee-167">You complete a normal verification challenge with a PIN.</span></span> <span data-ttu-id="20bee-168">Si votre appareil prend en charge Touch ID, Microsoft Authenticator le configure automatiquement pour ce compte.</span><span class="sxs-lookup"><span data-stu-id="20bee-168">If your device supports Touch ID, Microsoft Authenticator sets it up automatically for that account.</span></span>

![Vérification de la configuration de Touch ID](./media/authenticator-app-how-to/touchid1.png)

<span data-ttu-id="20bee-170">À partir de là, lorsque vous êtes invité à vérifier votre connexion, vous sélectionnez la notification Push reçue et vous scannez votre empreinte digitale au lieu d’entrer votre code confidentiel.</span><span class="sxs-lookup"><span data-stu-id="20bee-170">From that point forward, when you're required to verify your sign-in, you select the received push notification and scan your fingerprint instead of entering your PIN.</span></span>

![Notification Push](./media/authenticator-app-how-to/touchid2.png)

## <a name="use-the-app-when-you-sign-in"></a><span data-ttu-id="20bee-172">Utilisation de l’application lors de la connexion</span><span class="sxs-lookup"><span data-stu-id="20bee-172">Use the app when you sign in</span></span>

<span data-ttu-id="20bee-173">Une fois que votre compte est ajouté à l’application, vous pouvez être invité à effectuer une vérification du test pour vous assurer que tout a été correctement configuré.</span><span class="sxs-lookup"><span data-stu-id="20bee-173">Once your account is added to the app, you may be prompted to do a test verification to make sure everything was configured correctly.</span></span> <span data-ttu-id="20bee-174">Après cela, vous avez terminé !</span><span class="sxs-lookup"><span data-stu-id="20bee-174">After that, you're done!</span></span> <span data-ttu-id="20bee-175">Vous n’avez rien d’autre à faire avant la prochaine connexion.</span><span class="sxs-lookup"><span data-stu-id="20bee-175">You don't need to do anything else until the next time you sign in.</span></span>

<span data-ttu-id="20bee-176">Si vous avez choisi d’utiliser des codes de vérification dans l’application, ils s’affichent sur la page d’accueil.</span><span class="sxs-lookup"><span data-stu-id="20bee-176">If you chose to use verification codes in the app, you start to see them on the home page.</span></span> <span data-ttu-id="20bee-177">Ils changent toutes les 30 secondes, de sorte que vous ayez toujours un nouveau code lorsque vous en avez besoin.</span><span class="sxs-lookup"><span data-stu-id="20bee-177">They change every 30 seconds so that you always have a new code when you need one.</span></span> <span data-ttu-id="20bee-178">Mais vous n’avez rien à faire tant que vous n’êtes pas connecté et invité à saisir un code de vérification.</span><span class="sxs-lookup"><span data-stu-id="20bee-178">But you don't need to do anything with them until you sign in and are prompted to enter a verification code.</span></span>  