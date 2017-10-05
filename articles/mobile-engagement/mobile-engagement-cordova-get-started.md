---
title: Prise en main d'Azure Mobile Engagement pour Cordova/Phonegap
description: "Découvrez comment utiliser Azure Mobile Engagement avec les analyses et les notifications push pour les applications Cordova/Phonegap."
services: mobile-engagement
documentationcenter: Mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 54fe9113-e239-4ed7-9fd1-a502d7ac7f47
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-phonegap
ms.devlang: js
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: d7a761310782faab1dda023785f93cf90742e2ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-cordovaphonegap"></a><span data-ttu-id="1bc2b-103">Prise en main d'Azure Mobile Engagement pour Cordova/Phonegap</span><span class="sxs-lookup"><span data-stu-id="1bc2b-103">Get Started with Azure Mobile Engagement for Cordova/Phonegap</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="1bc2b-104">Cette rubrique explique comment utiliser Azure Mobile Engagement pour analyser l’utilisation de votre application et envoyer des notifications push à des segments d’utilisateurs d’une application développée avec Cordova.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users for a mobile application developed with Cordova.</span></span>

<span data-ttu-id="1bc2b-105">Dans ce didacticiel, nous allons créer une application Cordova vide à l'aide de Mac et intégrer le Kit de développement logiciel (SDK) Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-105">In this tutorial, we will create a blank Cordova app using Mac and then integrate Mobile Engagement SDK.</span></span> <span data-ttu-id="1bc2b-106">Elle collectera des données d'analyse de base et recevra des notifications push à l'aide du système de notifications push Apple (APNS) pour iOS et de Google Cloud Messaging (GCM) pour Android.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-106">It collects basic analytics data and receives push notifications using Apple Push Notification System (APNS) for iOS and Google Cloud Messaging (GCM) for Android.</span></span> <span data-ttu-id="1bc2b-107">Nous déploierons cette application sur un appareil iOS ou Android pour le test.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-107">We will deploy this to an iOS or Android device for testing.</span></span> 

> [!NOTE]
> <span data-ttu-id="1bc2b-108">Pour suivre ce didacticiel, vous avez besoin d'un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-108">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="1bc2b-109">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-109">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="1bc2b-110">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started).</span><span class="sxs-lookup"><span data-stu-id="1bc2b-110">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started).</span></span>
> 
> 

<span data-ttu-id="1bc2b-111">Ce didacticiel requiert les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1bc2b-111">This tutorial requires the following:</span></span>

* <span data-ttu-id="1bc2b-112">Xcode, que vous pouvez installer depuis le Mac App Store (pour un déploiement sur iOS)</span><span class="sxs-lookup"><span data-stu-id="1bc2b-112">XCode, which you can install from Mac App Store (for deploying to iOS)</span></span>
* <span data-ttu-id="1bc2b-113">[Kit de développement logiciel (SDK) et émulateur Android](http://developer.android.com/sdk/installing/index.html) (pour un déploiement sur Android)</span><span class="sxs-lookup"><span data-stu-id="1bc2b-113">[Android SDK & Emulator](http://developer.android.com/sdk/installing/index.html) (for deploying to Android)</span></span>
* <span data-ttu-id="1bc2b-114">Certificat de notification Push (.p12) que vous pouvez obtenir dans votre centre de développement Apple pour l’APNS</span><span class="sxs-lookup"><span data-stu-id="1bc2b-114">Push notification certificate (.p12) that you can obtain from Apple Dev Center for APNS</span></span>
* <span data-ttu-id="1bc2b-115">Numéro du projet GCM que vous pouvez obtenir à partir de votre Console de développement Google pour GCM</span><span class="sxs-lookup"><span data-stu-id="1bc2b-115">GCM Project number that you can obtain from your Google Developer Console for GCM</span></span>
* [<span data-ttu-id="1bc2b-116">Plug-in Mobile Engagement Cordova</span><span class="sxs-lookup"><span data-stu-id="1bc2b-116">Mobile Engagement Cordova Plugin</span></span>](https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-engagement)

> [!NOTE]
> <span data-ttu-id="1bc2b-117">Vous trouverez le code source et le fichier Lisez-moi du plug-in Cordova sur [GitHub](https://github.com/Azure/azure-mobile-engagement-cordova)</span><span class="sxs-lookup"><span data-stu-id="1bc2b-117">You can find the source code and the ReadMe for the Cordova plugin on [GitHub](https://github.com/Azure/azure-mobile-engagement-cordova)</span></span>
> 
> 

## <span data-ttu-id="1bc2b-118"><a id="setup-azme"></a>Configuration de Mobile Engagement pour votre application</span><span class="sxs-lookup"><span data-stu-id="1bc2b-118"><a id="setup-azme"></a>Setup Mobile Engagement for your Cordova app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="1bc2b-119"><a id="connecting-app"></a>Connexion de votre application au serveur principal Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="1bc2b-119"><a id="connecting-app"></a>Connecting your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="1bc2b-120">Ce didacticiel aborde l'intégration de base qui correspond aux éléments nécessaires à la collection de données et à l'envoi de notifications push.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-120">This tutorial presents a "basic integration" which is the minimal set required to collect data and send a push notification.</span></span> 

<span data-ttu-id="1bc2b-121">Nous allons créer une application de base à l’aide de Cordova afin d’illustrer l’intégration :</span><span class="sxs-lookup"><span data-stu-id="1bc2b-121">We will create a basic app with Cordova to demonstrate the integration:</span></span>

### <a name="create-a-new-cordova-project"></a><span data-ttu-id="1bc2b-122">Création d’un nouveau projet Cordova</span><span class="sxs-lookup"><span data-stu-id="1bc2b-122">Create a new Cordova project</span></span>
1. <span data-ttu-id="1bc2b-123">Ouvrez la fenêtre *Terminal* sur votre ordinateur Mac et saisissez les lignes suivantes pour créer un projet Cordova à partir du modèle par défaut.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-123">Launch *Terminal* window on your Mac machine and type the following which will create a new Cordova project from the default template.</span></span> <span data-ttu-id="1bc2b-124">Assurez-vous que le profil de publication que vous utilisez pour déployer votre application iOS utilise « com.mycompany.myapp » comme ID d’application.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-124">Make sure that the publishing profile you eventually use to deploy your iOS app is using 'com.mycompany.myapp' as the App ID.</span></span> 
   
        $ cordova create azme-cordova com.mycompany.myapp
        $ cd azme-cordova
2. <span data-ttu-id="1bc2b-125">Exécutez l’instruction suivante pour configurer votre projet pour **iOS** , puis exécutez celui-ci dans le simulateur iOS :</span><span class="sxs-lookup"><span data-stu-id="1bc2b-125">Execute the following to configure your project for **iOS** and run it in the iOS Simulator:</span></span>
   
        $ cordova platform add ios 
        $ cordova run ios
3. <span data-ttu-id="1bc2b-126">Exécutez l’instruction suivante pour configurer votre projet pour **Android** et l’exécuter dans l’émulateur Android.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-126">Execute the following to configure your project for **Android** and run it in the Android emulator.</span></span> <span data-ttu-id="1bc2b-127">Assurez-vous que dans les paramètres de votre émulateur de Kit de développement logiciel Android la cible est définie sur API Google (Google Inc.) et CPU/ABI sur Google APIs ARM.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-127">Make sure that your Android SDK Emulator settings have its Target as Google APIs (Google Inc.) with the CPU / ABI as Google APIs ARM.</span></span>  
   
        $ cordova platform add android
        $ cordova run android
4. <span data-ttu-id="1bc2b-128">Ajout du plug-in Cordova Console.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-128">Add the Cordova Console plugin.</span></span> 

    ```
    $ cordova plugin add cordova-plugin-console
    ``` 

### <a name="connect-your-app-to-mobile-engagement-backend"></a><span data-ttu-id="1bc2b-129">Connexion de votre application au serveur principal Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="1bc2b-129">Connect your app to Mobile Engagement backend</span></span>
1. <span data-ttu-id="1bc2b-130">Installez le plug-in Azure Mobile Engagement Cordova tout en fournissant les valeurs des variables pour configurer le plug-in :</span><span class="sxs-lookup"><span data-stu-id="1bc2b-130">Install the Azure Mobile Engagement Cordova plugin while providing the variable values to configure the plugin:</span></span>
   
        cordova plugin add cordova-plugin-ms-azure-mobile-engagement    
             --variable AZME_IOS_CONNECTION_STRING=<iOS Connection String> 
            --variable AZME_IOS_REACH_ICON=... (icon name WITH extension) 
            --variable AZME_ANDROID_CONNECTION_STRING=<Android Connection String> 
            --variable AZME_ANDROID_REACH_ICON=... (icon name WITHOUT extension)       
            --variable AZME_ANDROID_GOOGLE_PROJECT_NUMBER=... (From your Google Cloud console for sending push notifications) 
            --variable AZME_ACTION_URL =... (URL scheme which triggers the app for deep linking)
            --variable AZME_ENABLE_NATIVE_LOG=true|false
            --variable AZME_ENABLE_PLUGIN_LOG=true|false

<span data-ttu-id="1bc2b-131">*Icône Android Reach* : doit être le nom de la ressource sans extension ni préfixe dessinable (ex : mynotificationicon), et le fichier icône doit être copié dans votre projet android (platforms/android/res/drawable)</span><span class="sxs-lookup"><span data-stu-id="1bc2b-131">*Android Reach Icon* : must be the name of the resource without any extension, nor drawable prefix (ex: mynotificationicon), and the icon file must be copied into your android project (platforms/android/res/drawable)</span></span>

<span data-ttu-id="1bc2b-132">*Icône iOS Reach* : doit être le nom de la ressource avec son extension (ex : mynotificationicon.png), et le fichier icône doit être ajouté à votre projet iOS avec XCode (en utilisant le menu d’ajout de fichiers)</span><span class="sxs-lookup"><span data-stu-id="1bc2b-132">*iOS Reach Icon*  : must be the name of the resource with its extension (ex:  mynotificationicon.png), and the icon file must be added into your iOS project with XCode (using the Add Files Menu)</span></span>

## <span data-ttu-id="1bc2b-133"><a id="monitor"></a>Activation de la surveillance en temps réel</span><span class="sxs-lookup"><span data-stu-id="1bc2b-133"><a id="monitor"></a>Enabling real-time monitoring</span></span>
1. <span data-ttu-id="1bc2b-134">Dans le projet Cordova, modifiez **www/js/index.js** pour ajouter l’appel de Mobile Engagement afin de déclarer une nouvelle activité à la réception de l’événement *deviceReady* .</span><span class="sxs-lookup"><span data-stu-id="1bc2b-134">In the Cordova project - edit **www/js/index.js** to add the call to Mobile Engagement to declare a new activity once the *deviceReady* event is received.</span></span>
   
         onDeviceReady: function() {
                Engagement.startActivity("myPage",{});
            }
2. <span data-ttu-id="1bc2b-135">Exécutez l'application :</span><span class="sxs-lookup"><span data-stu-id="1bc2b-135">Run the application:</span></span>
   
   * <span data-ttu-id="1bc2b-136">**Pour iOS**</span><span class="sxs-lookup"><span data-stu-id="1bc2b-136">**For iOS**</span></span>
     
       <span data-ttu-id="1bc2b-137">Dans la fenêtre `Terminal` , exécutez votre application dans une nouvelle instance de simulateur en exécutant le code suivant :</span><span class="sxs-lookup"><span data-stu-id="1bc2b-137">In `Terminal` window launch your app in a new Simulator instance by executing the following:</span></span>
     
           cordova run ios
   * <span data-ttu-id="1bc2b-138">**Pour Android**</span><span class="sxs-lookup"><span data-stu-id="1bc2b-138">**For Android**</span></span>
     
       <span data-ttu-id="1bc2b-139">Dans la fenêtre `Terminal` , exécutez votre application dans une nouvelle instance d’émulateur en exécutant le code suivant :</span><span class="sxs-lookup"><span data-stu-id="1bc2b-139">In `Terminal` window launch your app in a new emulator instance by executing the following:</span></span>
     
           cordova run android
3. <span data-ttu-id="1bc2b-140">Les éléments suivants s’affichent dans les journaux de la console :</span><span class="sxs-lookup"><span data-stu-id="1bc2b-140">You can see the following in the console logs:</span></span>
   
        [Engagement] Agent: Session started
        [Engagement] Agent: Activity 'myPage' started
        [Engagement] Connection: Established
        [Engagement] Connection: Sent: appInfo
        [Engagement] Connection: Sent: startSession
        [Engagement] Connection: Sent: activity name='myPage'

## <span data-ttu-id="1bc2b-141"><a id="monitor"></a>Connexion d’application avec l’analyse en temps réel</span><span class="sxs-lookup"><span data-stu-id="1bc2b-141"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="1bc2b-142"><a id="integrate-push"></a>Activation des notifications Push et de la messagerie intégrée à l’application</span><span class="sxs-lookup"><span data-stu-id="1bc2b-142"><a id="integrate-push"></a>Enabling Push Notifications and in-app messaging</span></span>
<span data-ttu-id="1bc2b-143">Mobile Engagement vous permet d'interagir avec vos utilisateurs à l'aide de notifications push et de la messagerie dans l'application, dans le cadre d'une campagne.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-143">Mobile Engagement allows you to interact with your users using Push Notifications and in-app messaging in the context of campaigns.</span></span> <span data-ttu-id="1bc2b-144">Ce module s'appelle Couverture dans le portail Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-144">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="1bc2b-145">Les sections suivantes vous permettront de configurer votre application pour la réception des notifications.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-145">The following sections will setup your app to receive them.</span></span>

### <a name="configure-push-credentials-for-mobile-engagement"></a><span data-ttu-id="1bc2b-146">Configuration des informations d'identification Push pour Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="1bc2b-146">Configure Push credentials for Mobile Engagement</span></span>
<span data-ttu-id="1bc2b-147">Pour permettre à Mobile Engagement d'envoyer des notifications push en votre nom, vous devez lui accorder l'accès à votre certificat Apple iOS ou à votre clé d’API serveur GCM.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-147">To allow Mobile Engagement to send Push Notifications on your behalf, you need to grant it access to your Apple iOS certificate or GCM Server API Key.</span></span> 

1. <span data-ttu-id="1bc2b-148">Accédez au portail Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-148">Navigate to your Mobile Engagement portal.</span></span> <span data-ttu-id="1bc2b-149">Vérifiez que vous vous trouvez dans l’application utilisée pour ce projet, puis cliquez sur le bouton **Activer** situé en bas :</span><span class="sxs-lookup"><span data-stu-id="1bc2b-149">Ensure you're in the app we're using for this project and then click on the **Engage** button at the bottom:</span></span>
   
    ![][1]
2. <span data-ttu-id="1bc2b-150">Vous accédez à la page de paramètres via le portail Engagement.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-150">You will land in the settings page in your Engagement Portal.</span></span> <span data-ttu-id="1bc2b-151">À partir de là, cliquez sur la section **Native Push** :</span><span class="sxs-lookup"><span data-stu-id="1bc2b-151">From there click on the **Native Push** section:</span></span>
   
    ![][2]
3. <span data-ttu-id="1bc2b-152">Configuration du certificat iOS/de la clé d’API serveur GCM</span><span class="sxs-lookup"><span data-stu-id="1bc2b-152">Configure iOS Certificate/GCM Server API Key</span></span>
   
    <span data-ttu-id="1bc2b-153">**[iOS]**</span><span class="sxs-lookup"><span data-stu-id="1bc2b-153">**[iOS]**</span></span>
   
    <span data-ttu-id="1bc2b-154">a.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-154">a.</span></span> <span data-ttu-id="1bc2b-155">Sélectionnez votre .p12, téléchargez-le et tapez votre mot de passe :</span><span class="sxs-lookup"><span data-stu-id="1bc2b-155">Select your .p12, upload it and type your password:</span></span>
   
    ![][3]
   
    <span data-ttu-id="1bc2b-156">**[Android]**</span><span class="sxs-lookup"><span data-stu-id="1bc2b-156">**[Android]**</span></span>
   
    <span data-ttu-id="1bc2b-157">a.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-157">a.</span></span> <span data-ttu-id="1bc2b-158">Dans la section Paramètres GCM, cliquez sur l’icône de modification devant **Clé API**. Ensuite, dans le menu contextuel qui s’affiche, collez la clé du serveur GCM, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-158">Click the edit icon in front of **API Key** in the GCM Settings section and in the popup which shows up, paste the GCM Server Key and click **OK**.</span></span> 
   
    ![][4]

### <a name="enable-push-notifications-in-the-cordova-app"></a><span data-ttu-id="1bc2b-159">Activation des notifications push dans l'application Cordova</span><span class="sxs-lookup"><span data-stu-id="1bc2b-159">Enable push notifications in the Cordova app</span></span>
<span data-ttu-id="1bc2b-160">Modifiez **www/js/index.js** pour ajouter l’appel de Mobile Engagement afin de demander des notifications push et de déclarer un gestionnaire :</span><span class="sxs-lookup"><span data-stu-id="1bc2b-160">Edit **www/js/index.js** to add the call to Mobile Engagement to request push notifications and declare a handler:</span></span>

     onDeviceReady: function() {
           Engagement.initializeReach(  
                 // on OpenUrl  
                 function(_url) {   
                 alert(_url);   
                 });  
            Engagement.startActivity("myPage",{});  
        }

### <a name="run-the-app"></a><span data-ttu-id="1bc2b-161">Exécution de l'application</span><span class="sxs-lookup"><span data-stu-id="1bc2b-161">Run the app</span></span>
<span data-ttu-id="1bc2b-162">**[iOS]**</span><span class="sxs-lookup"><span data-stu-id="1bc2b-162">**[iOS]**</span></span>

1. <span data-ttu-id="1bc2b-163">Nous allons utiliser XCode pour créer et déployer l'application sur l’appareil afin de tester les notifications push, car iOS autorise uniquement ces notifications sur un appareil réel.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-163">We will use XCode to build and deploy the app on the device to test push notifications since iOS only allows push notifications to an actual device.</span></span> <span data-ttu-id="1bc2b-164">Accédez à l’emplacement où votre projet Cordova a été créé, puis accédez à l’emplacement  **...\platforms\ios**.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-164">Go to the location where your Cordova project is created and navigate to **...\platforms\ios** location.</span></span> <span data-ttu-id="1bc2b-165">Ouvrez le fichier .xcodeproj natif dans XCode.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-165">Open up the native .xcodeproj file in XCode.</span></span> 
2. <span data-ttu-id="1bc2b-166">Générez et déployez l'application Cordova sur l’appareil iOS en utilisant le compte ayant le profil d’approvisionnement contenant le certificat que vous avez téléchargé vers le portail Mobile Engagement et l'ID d'application correspondant à celui fourni lors de la création de l'application Cordova.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-166">Build and deploy the Cordova app to the iOS device using the account which has the provisioning profile containing the certificate you just uploaded to the Mobile Engagement portal and the App Id which matches the one you provided while creating the Cordova app.</span></span> <span data-ttu-id="1bc2b-167">Vous pouvez extraire l’*identificateur d’offres groupées* dans votre fichier **Resources\*-info.plist** dans XCode pour déterminer s’il correspond.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-167">You can check out the *Bundle identifier* in your **Resources\*-info.plist** file in XCode to match it up.</span></span> 
3. <span data-ttu-id="1bc2b-168">La fenêtre contextuelle iOS standard apparaîtra sur votre appareil pour indiquer que l'application demande l'autorisation d'envoyer des notifications.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-168">You will see the standard iOS popup on your device saying that the app requests permission to send notifications.</span></span> <span data-ttu-id="1bc2b-169">Accordez l'autorisation.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-169">Grant the permission.</span></span> 

<span data-ttu-id="1bc2b-170">**[Android]**</span><span class="sxs-lookup"><span data-stu-id="1bc2b-170">**[Android]**</span></span>

<span data-ttu-id="1bc2b-171">Vous pouvez utiliser l'émulateur pour exécuter l'application Android, car les notifications GCM sont prises en charge par l'émulateur Android.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-171">You can simply use the emulator to run the Android app as GCM notifications are supported on the Android emulator.</span></span> 

    cordova run android

## <span data-ttu-id="1bc2b-172"><a id="send"></a>Envoi d’une notification vers votre application</span><span class="sxs-lookup"><span data-stu-id="1bc2b-172"><a id="send"></a>Send a notification to your app</span></span>
<span data-ttu-id="1bc2b-173">Nous allons maintenant créer une campagne simple de notification Push qui enverra une notification Push à votre application en cours d’exécution sur l’appareil :</span><span class="sxs-lookup"><span data-stu-id="1bc2b-173">We will now create a simple Push Notification campaign that will send a push to your app running on the device:</span></span>

1. <span data-ttu-id="1bc2b-174">Accédez à l’onglet **REACH** de votre portail Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-174">Navigate to the **Reach** tab in your Mobile Engagement portal</span></span>
2. <span data-ttu-id="1bc2b-175">Cliquez sur **Nouvelle annonce** pour créer votre campagne Push.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-175">Click **New Announcement** to create your push campaign</span></span>
   
    ![][6]
3. <span data-ttu-id="1bc2b-176">Entrez les informations nécessaires pour créer votre campagne **[Android]**</span><span class="sxs-lookup"><span data-stu-id="1bc2b-176">Provide inputs to create your campaign **[Android]**</span></span>
   
   * <span data-ttu-id="1bc2b-177">Entrez un **nom** pour votre campagne.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-177">Provide a **Name** for your campaign.</span></span> 
   * <span data-ttu-id="1bc2b-178">Sélectionnez le **Type de distribution** *Notification système* *Simple*.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-178">Select the **Delivery Type** as *System notification* *Simple*</span></span>
   * <span data-ttu-id="1bc2b-179">Sélectionnez le **délai de livraison**  *N’importe quand*</span><span class="sxs-lookup"><span data-stu-id="1bc2b-179">Select the **Delivery time** as *"Any Time"*</span></span>
   * <span data-ttu-id="1bc2b-180">Entrez un **Titre** pour votre notification, qui constituera la première ligne de la diffusion.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-180">Provide a **Title** for your notification which will be the first line in the push.</span></span>
   * <span data-ttu-id="1bc2b-181">Entrez un **Message** pour votre notification, qui constituera le corps du message.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-181">Provide a **Message** for your notification which will serve as the message body.</span></span> 
     
     ![][11]
4. <span data-ttu-id="1bc2b-182">Entrez les informations nécessaires pour créer votre campagne **[iOS]**</span><span class="sxs-lookup"><span data-stu-id="1bc2b-182">Provide inputs to create your campaign **[iOS]**</span></span>
   
   * <span data-ttu-id="1bc2b-183">Entrez un **nom** pour votre campagne.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-183">Provide a **Name** for your campaign.</span></span> 
   * <span data-ttu-id="1bc2b-184">Sélectionnez le **délai de livraison**  *Hors de l’application uniquement*</span><span class="sxs-lookup"><span data-stu-id="1bc2b-184">Select the **Delivery time** as *"Out of app only"*</span></span>
   * <span data-ttu-id="1bc2b-185">Entrez un **Titre** pour votre notification, qui constituera la première ligne de la diffusion.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-185">Provide a **Title** for your notification which will be the first line in the push.</span></span>
   * <span data-ttu-id="1bc2b-186">Entrez un **Message** pour votre notification, qui constituera le corps du message.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-186">Provide a **Message** for your notification which will serve as the message body.</span></span> 
     
     ![][12]
5. <span data-ttu-id="1bc2b-187">Faites défiler l’écran vers le bas et, dans la section Contenu, sélectionnez **Notification uniquement**</span><span class="sxs-lookup"><span data-stu-id="1bc2b-187">Scroll down, and in the content section select **Notification only**</span></span>
   
    ![][8]
6. <span data-ttu-id="1bc2b-188">[Facultatif] Vous pouvez également fournir une URL d’action.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-188">[Optional] You can also provide an Action URL.</span></span> <span data-ttu-id="1bc2b-189">Assurez-vous qu’elle utilise un schéma d’URL fourni lors de la configuration de la variable **AZME\_REDIRECT\_URL** du plug-in, par exemple *myapp://test*.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-189">Make sure that it uses a URL scheme provided while configuring the plugin's **AZME\_REDIRECT\_URL** variable e.g. *myapp://test*.</span></span>  
7. <span data-ttu-id="1bc2b-190">Vous avez terminé de définir la campagne de base la plus simple possible.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-190">You're done setting the most basic campaign possible.</span></span> <span data-ttu-id="1bc2b-191">Faites maintenant défiler vers le bas, puis cliquez sur le bouton **Créer** pour enregistrer votre campagne.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-191">Now scroll down again and click the **Create** button to save your campaign.</span></span>
8. <span data-ttu-id="1bc2b-192">Enfin, dernière étape, **activez** votre campagne.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-192">Finally **Activate** your campaign</span></span>
   
    ![][10]
9. <span data-ttu-id="1bc2b-193">Vous devriez maintenant voir une notification Push sur votre appareil ou votre émulateur dans le cadre de cette campagne.</span><span class="sxs-lookup"><span data-stu-id="1bc2b-193">You should now see a push notification on your device or emulator as part of this campaign.</span></span> 

## <span data-ttu-id="1bc2b-194"><a id="next-steps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1bc2b-194"><a id="next-steps"></a>Next Steps</span></span>
[<span data-ttu-id="1bc2b-195">Vue d'ensemble de toutes les méthodes disponibles avec le Kit de développement logiciel (SDK) Cordova Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="1bc2b-195">Overview of all methods available with Cordova Mobile Engagement SDK</span></span>](https://github.com/Azure/azure-mobile-engagement-cordova)

<!-- Images. -->

[1]: ./media/mobile-engagement-cordova-get-started/engage-button.png
[2]: ./media/mobile-engagement-cordova-get-started/engagement-portal.png
[3]: ./media/mobile-engagement-cordova-get-started/native-push-settings.png
[4]: ./media/mobile-engagement-cordova-get-started/api-key.png
[6]: ./media/mobile-engagement-cordova-get-started/new-announcement.png
[8]: ./media/mobile-engagement-cordova-get-started/campaign-content.png
[10]: ./media/mobile-engagement-cordova-get-started/campaign-activate.png
[11]: ./media/mobile-engagement-cordova-get-started/campaign-first-params-android.png
[12]: ./media/mobile-engagement-cordova-get-started/campaign-first-params-ios.png

