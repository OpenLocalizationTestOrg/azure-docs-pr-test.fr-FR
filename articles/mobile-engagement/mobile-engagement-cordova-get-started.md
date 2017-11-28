---
title: "aaaGet main d’Azure Mobile Engagement pour Cordova/Phonegap"
description: "Découvrez comment toouse Azure Mobile Engagement avec Analytique et les Notifications Push pour les applications Cordova/Phonegap."
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
ms.openlocfilehash: e67dabbdf7886802bb058f38964e558d5ae6854c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-cordovaphonegap"></a><span data-ttu-id="4c674-103">Prise en main d'Azure Mobile Engagement pour Cordova/Phonegap</span><span class="sxs-lookup"><span data-stu-id="4c674-103">Get Started with Azure Mobile Engagement for Cordova/Phonegap</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="4c674-104">Cette rubrique vous montre comment toounderstand d’Azure Mobile Engagement toouse développées par votre application d’utilisation et d’envoi push notifications toosegmented les utilisateurs d’une application mobile avec Cordova.</span><span class="sxs-lookup"><span data-stu-id="4c674-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users for a mobile application developed with Cordova.</span></span>

<span data-ttu-id="4c674-105">Dans ce didacticiel, nous allons créer une application Cordova vide à l'aide de Mac et intégrer le Kit de développement logiciel (SDK) Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="4c674-105">In this tutorial, we will create a blank Cordova app using Mac and then integrate Mobile Engagement SDK.</span></span> <span data-ttu-id="4c674-106">Elle collectera des données d'analyse de base et recevra des notifications push à l'aide du système de notifications push Apple (APNS) pour iOS et de Google Cloud Messaging (GCM) pour Android.</span><span class="sxs-lookup"><span data-stu-id="4c674-106">It collects basic analytics data and receives push notifications using Apple Push Notification System (APNS) for iOS and Google Cloud Messaging (GCM) for Android.</span></span> <span data-ttu-id="4c674-107">Nous déploiera ce tooan appareil iOS ou Android pour le test.</span><span class="sxs-lookup"><span data-stu-id="4c674-107">We will deploy this tooan iOS or Android device for testing.</span></span> 

> [!NOTE]
> <span data-ttu-id="4c674-108">toocomplete ce didacticiel, vous devez disposer d’un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="4c674-108">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="4c674-109">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="4c674-109">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="4c674-110">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started).</span><span class="sxs-lookup"><span data-stu-id="4c674-110">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started).</span></span>
> 
> 

<span data-ttu-id="4c674-111">Ce didacticiel requiert hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="4c674-111">This tutorial requires hello following:</span></span>

* <span data-ttu-id="4c674-112">XCode, que vous pouvez installer à partir de Mac App Store (pour le déploiement tooiOS)</span><span class="sxs-lookup"><span data-stu-id="4c674-112">XCode, which you can install from Mac App Store (for deploying tooiOS)</span></span>
* <span data-ttu-id="4c674-113">[Android SDK & émulateur](http://developer.android.com/sdk/installing/index.html) (pour le déploiement tooAndroid)</span><span class="sxs-lookup"><span data-stu-id="4c674-113">[Android SDK & Emulator](http://developer.android.com/sdk/installing/index.html) (for deploying tooAndroid)</span></span>
* <span data-ttu-id="4c674-114">Certificat de notification Push (.p12) que vous pouvez obtenir dans votre centre de développement Apple pour l’APNS</span><span class="sxs-lookup"><span data-stu-id="4c674-114">Push notification certificate (.p12) that you can obtain from Apple Dev Center for APNS</span></span>
* <span data-ttu-id="4c674-115">Numéro du projet GCM que vous pouvez obtenir à partir de votre Console de développement Google pour GCM</span><span class="sxs-lookup"><span data-stu-id="4c674-115">GCM Project number that you can obtain from your Google Developer Console for GCM</span></span>
* [<span data-ttu-id="4c674-116">Plug-in Mobile Engagement Cordova</span><span class="sxs-lookup"><span data-stu-id="4c674-116">Mobile Engagement Cordova Plugin</span></span>](https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-engagement)

> [!NOTE]
> <span data-ttu-id="4c674-117">Vous pouvez trouver le code source de hello et hello fichier Lisezmoi pour le plug-in de hello Cordova sur [GitHub](https://github.com/Azure/azure-mobile-engagement-cordova)</span><span class="sxs-lookup"><span data-stu-id="4c674-117">You can find hello source code and hello ReadMe for hello Cordova plugin on [GitHub](https://github.com/Azure/azure-mobile-engagement-cordova)</span></span>
> 
> 

## <span data-ttu-id="4c674-118"><a id="setup-azme"></a>Configuration de Mobile Engagement pour votre application</span><span class="sxs-lookup"><span data-stu-id="4c674-118"><a id="setup-azme"></a>Setup Mobile Engagement for your Cordova app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="4c674-119"><a id="connecting-app"></a>Connexion de votre serveur principal d’application toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="4c674-119"><a id="connecting-app"></a>Connecting your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="4c674-120">Ce didacticiel présente une « intégration de base « hello minimale définie les données de toocollect requis et envoyer une notification push.</span><span class="sxs-lookup"><span data-stu-id="4c674-120">This tutorial presents a "basic integration" which is hello minimal set required toocollect data and send a push notification.</span></span> 

<span data-ttu-id="4c674-121">Nous allons créer une application de base avec l’intégration de hello toodemonstrate Cordova :</span><span class="sxs-lookup"><span data-stu-id="4c674-121">We will create a basic app with Cordova toodemonstrate hello integration:</span></span>

### <a name="create-a-new-cordova-project"></a><span data-ttu-id="4c674-122">Création d’un nouveau projet Cordova</span><span class="sxs-lookup"><span data-stu-id="4c674-122">Create a new Cordova project</span></span>
1. <span data-ttu-id="4c674-123">Lancez *Terminal* fenêtre sur votre hello Mac machine et le type suivant qui créera un nouveau projet Cordova à partir du modèle par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="4c674-123">Launch *Terminal* window on your Mac machine and type hello following which will create a new Cordova project from hello default template.</span></span> <span data-ttu-id="4c674-124">Assurez-vous que la publication hello profil vous finalement toodeploy d’utiliser votre application iOS est à l’aide de 'com.mycompany.myapp' comme hello identifiant d’application.</span><span class="sxs-lookup"><span data-stu-id="4c674-124">Make sure that hello publishing profile you eventually use toodeploy your iOS app is using 'com.mycompany.myapp' as hello App ID.</span></span> 
   
        $ cordova create azme-cordova com.mycompany.myapp
        $ cd azme-cordova
2. <span data-ttu-id="4c674-125">Exécutez hello suivant tooconfigure votre projet pour **iOS** et exécutez-la dans hello, iOS Simulator :</span><span class="sxs-lookup"><span data-stu-id="4c674-125">Execute hello following tooconfigure your project for **iOS** and run it in hello iOS Simulator:</span></span>
   
        $ cordova platform add ios 
        $ cordova run ios
3. <span data-ttu-id="4c674-126">Exécutez hello suivant tooconfigure votre projet pour **Android** et l’exécuter dans l’émulateur Android de hello.</span><span class="sxs-lookup"><span data-stu-id="4c674-126">Execute hello following tooconfigure your project for **Android** and run it in hello Android emulator.</span></span> <span data-ttu-id="4c674-127">Vérifiez vos paramètres de l’émulateur Kit de développement logiciel Android que sa cible en tant que Google APIs (Google Inc.) avec hello CPU / ABI sous forme de Google APIs ARM.</span><span class="sxs-lookup"><span data-stu-id="4c674-127">Make sure that your Android SDK Emulator settings have its Target as Google APIs (Google Inc.) with hello CPU / ABI as Google APIs ARM.</span></span>  
   
        $ cordova platform add android
        $ cordova run android
4. <span data-ttu-id="4c674-128">Ajoutez hello plug-in Cordova Console.</span><span class="sxs-lookup"><span data-stu-id="4c674-128">Add hello Cordova Console plugin.</span></span> 

    ```
    $ cordova plugin add cordova-plugin-console
    ``` 

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="4c674-129">Se connecter à votre serveur principal d’application tooMobile Engagement</span><span class="sxs-lookup"><span data-stu-id="4c674-129">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="4c674-130">Installez le plug-in de hello Azure Mobile Engagement Cordova tout en offrant hello valeurs des variables tooconfigure hello plug-in :</span><span class="sxs-lookup"><span data-stu-id="4c674-130">Install hello Azure Mobile Engagement Cordova plugin while providing hello variable values tooconfigure hello plugin:</span></span>
   
        cordova plugin add cordova-plugin-ms-azure-mobile-engagement    
             --variable AZME_IOS_CONNECTION_STRING=<iOS Connection String> 
            --variable AZME_IOS_REACH_ICON=... (icon name WITH extension) 
            --variable AZME_ANDROID_CONNECTION_STRING=<Android Connection String> 
            --variable AZME_ANDROID_REACH_ICON=... (icon name WITHOUT extension)       
            --variable AZME_ANDROID_GOOGLE_PROJECT_NUMBER=... (From your Google Cloud console for sending push notifications) 
            --variable AZME_ACTION_URL =... (URL scheme which triggers hello app for deep linking)
            --variable AZME_ENABLE_NATIVE_LOG=true|false
            --variable AZME_ENABLE_PLUGIN_LOG=true|false

<span data-ttu-id="4c674-131">*Icône d’atteindre Android* : doit être nom hello de ressource hello sans toute extension ni le préfixe drawable (ex : mynotificationicon), et le fichier d’icône hello doit être copié dans votre projet android (plateformes/android/res/drawable)</span><span class="sxs-lookup"><span data-stu-id="4c674-131">*Android Reach Icon* : must be hello name of hello resource without any extension, nor drawable prefix (ex: mynotificationicon), and hello icon file must be copied into your android project (platforms/android/res/drawable)</span></span>

<span data-ttu-id="4c674-132">*iOS atteindre une icône* : doit être nom hello de ressource hello avec l’extension (ex : mynotificationicon.png), et le fichier d’icône hello doit être ajouté à votre projet iOS avec XCode (à l’aide de hello Ajouter fichiers Menu)</span><span class="sxs-lookup"><span data-stu-id="4c674-132">*iOS Reach Icon*  : must be hello name of hello resource with its extension (ex:  mynotificationicon.png), and hello icon file must be added into your iOS project with XCode (using hello Add Files Menu)</span></span>

## <span data-ttu-id="4c674-133"><a id="monitor"></a>Activation de la surveillance en temps réel</span><span class="sxs-lookup"><span data-stu-id="4c674-133"><a id="monitor"></a>Enabling real-time monitoring</span></span>
1. <span data-ttu-id="4c674-134">Dans le projet de Cordova hello - modifier **www/js/index.js** appel de hello tooadd tooMobile Engagement toodeclare une nouvelle activité une fois hello *deviceReady* événement est reçu.</span><span class="sxs-lookup"><span data-stu-id="4c674-134">In hello Cordova project - edit **www/js/index.js** tooadd hello call tooMobile Engagement toodeclare a new activity once hello *deviceReady* event is received.</span></span>
   
         onDeviceReady: function() {
                Engagement.startActivity("myPage",{});
            }
2. <span data-ttu-id="4c674-135">Exécutez l’application hello :</span><span class="sxs-lookup"><span data-stu-id="4c674-135">Run hello application:</span></span>
   
   * <span data-ttu-id="4c674-136">**Pour iOS**</span><span class="sxs-lookup"><span data-stu-id="4c674-136">**For iOS**</span></span>
     
       <span data-ttu-id="4c674-137">Dans `Terminal` fenêtre lancez votre application dans une nouvelle instance de simulateur en exécutant hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="4c674-137">In `Terminal` window launch your app in a new Simulator instance by executing hello following:</span></span>
     
           cordova run ios
   * <span data-ttu-id="4c674-138">**Pour Android**</span><span class="sxs-lookup"><span data-stu-id="4c674-138">**For Android**</span></span>
     
       <span data-ttu-id="4c674-139">Dans `Terminal` fenêtre lancez votre application dans une nouvelle instance de l’émulateur en exécutant hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="4c674-139">In `Terminal` window launch your app in a new emulator instance by executing hello following:</span></span>
     
           cordova run android
3. <span data-ttu-id="4c674-140">Vous pouvez voir suivant hello dans les journaux de la console hello :</span><span class="sxs-lookup"><span data-stu-id="4c674-140">You can see hello following in hello console logs:</span></span>
   
        [Engagement] Agent: Session started
        [Engagement] Agent: Activity 'myPage' started
        [Engagement] Connection: Established
        [Engagement] Connection: Sent: appInfo
        [Engagement] Connection: Sent: startSession
        [Engagement] Connection: Sent: activity name='myPage'

## <span data-ttu-id="4c674-141"><a id="monitor"></a>Connexion d’application avec l’analyse en temps réel</span><span class="sxs-lookup"><span data-stu-id="4c674-141"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="4c674-142"><a id="integrate-push"></a>Activation des notifications Push et de la messagerie intégrée à l’application</span><span class="sxs-lookup"><span data-stu-id="4c674-142"><a id="integrate-push"></a>Enabling Push Notifications and in-app messaging</span></span>
<span data-ttu-id="4c674-143">Mobile Engagement vous permet de toointeract avec vos utilisateurs à l’aide de Notifications Push et les messages dans le contexte de hello de campagnes dans l’application.</span><span class="sxs-lookup"><span data-stu-id="4c674-143">Mobile Engagement allows you toointeract with your users using Push Notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="4c674-144">Ce module est appelé portée dans le portail Mobile Engagement de hello.</span><span class="sxs-lookup"><span data-stu-id="4c674-144">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="4c674-145">Hello sections suivantes va installer votre application tooreceive les.</span><span class="sxs-lookup"><span data-stu-id="4c674-145">hello following sections will setup your app tooreceive them.</span></span>

### <a name="configure-push-credentials-for-mobile-engagement"></a><span data-ttu-id="4c674-146">Configuration des informations d'identification Push pour Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="4c674-146">Configure Push credentials for Mobile Engagement</span></span>
<span data-ttu-id="4c674-147">tooallow Mobile Engagement toosend des Notifications Push à votre place, vous devez toogrant il accéder au certificat de tooyour Apple iOS ou de la clé d’API GCM serveur.</span><span class="sxs-lookup"><span data-stu-id="4c674-147">tooallow Mobile Engagement toosend Push Notifications on your behalf, you need toogrant it access tooyour Apple iOS certificate or GCM Server API Key.</span></span> 

1. <span data-ttu-id="4c674-148">Accédez portail Mobile Engagement de tooyour.</span><span class="sxs-lookup"><span data-stu-id="4c674-148">Navigate tooyour Mobile Engagement portal.</span></span> <span data-ttu-id="4c674-149">Vérifiez dans l’application hello que nous utilisons pour ce projet et que vous cliquez ensuite sur hello **Engage** bouton bas hello :</span><span class="sxs-lookup"><span data-stu-id="4c674-149">Ensure you're in hello app we're using for this project and then click on hello **Engage** button at hello bottom:</span></span>
   
    ![][1]
2. <span data-ttu-id="4c674-150">Vous allez arriver dans la page des paramètres hello dans votre portail d’Engagement.</span><span class="sxs-lookup"><span data-stu-id="4c674-150">You will land in hello settings page in your Engagement Portal.</span></span> <span data-ttu-id="4c674-151">À partir de là, cliquez sur hello **le Push natif** section :</span><span class="sxs-lookup"><span data-stu-id="4c674-151">From there click on hello **Native Push** section:</span></span>
   
    ![][2]
3. <span data-ttu-id="4c674-152">Configuration du certificat iOS/de la clé d’API serveur GCM</span><span class="sxs-lookup"><span data-stu-id="4c674-152">Configure iOS Certificate/GCM Server API Key</span></span>
   
    <span data-ttu-id="4c674-153">**[iOS]**</span><span class="sxs-lookup"><span data-stu-id="4c674-153">**[iOS]**</span></span>
   
    <span data-ttu-id="4c674-154">a.</span><span class="sxs-lookup"><span data-stu-id="4c674-154">a.</span></span> <span data-ttu-id="4c674-155">Sélectionnez votre .p12, téléchargez-le et tapez votre mot de passe :</span><span class="sxs-lookup"><span data-stu-id="4c674-155">Select your .p12, upload it and type your password:</span></span>
   
    ![][3]
   
    <span data-ttu-id="4c674-156">**[Android]**</span><span class="sxs-lookup"><span data-stu-id="4c674-156">**[Android]**</span></span>
   
    <span data-ttu-id="4c674-157">a.</span><span class="sxs-lookup"><span data-stu-id="4c674-157">a.</span></span> <span data-ttu-id="4c674-158">Cliquez sur icône d’édition hello devant **clé API** Bonjour section GCM paramètres et dans la fenêtre contextuelle hello qui s’affiche, collez hello GCM clé du serveur, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="4c674-158">Click hello edit icon in front of **API Key** in hello GCM Settings section and in hello popup which shows up, paste hello GCM Server Key and click **OK**.</span></span> 
   
    ![][4]

### <a name="enable-push-notifications-in-hello-cordova-app"></a><span data-ttu-id="4c674-159">Activer les notifications push dans l’application de Cordova hello</span><span class="sxs-lookup"><span data-stu-id="4c674-159">Enable push notifications in hello Cordova app</span></span>
<span data-ttu-id="4c674-160">Modifier **www/js/index.js** tooadd hello appel tooMobile Engagement toorequest des notifications push et déclarer un gestionnaire :</span><span class="sxs-lookup"><span data-stu-id="4c674-160">Edit **www/js/index.js** tooadd hello call tooMobile Engagement toorequest push notifications and declare a handler:</span></span>

     onDeviceReady: function() {
           Engagement.initializeReach(  
                 // on OpenUrl  
                 function(_url) {   
                 alert(_url);   
                 });  
            Engagement.startActivity("myPage",{});  
        }

### <a name="run-hello-app"></a><span data-ttu-id="4c674-161">Exécutez l’application hello</span><span class="sxs-lookup"><span data-stu-id="4c674-161">Run hello app</span></span>
<span data-ttu-id="4c674-162">**[iOS]**</span><span class="sxs-lookup"><span data-stu-id="4c674-162">**[iOS]**</span></span>

1. <span data-ttu-id="4c674-163">Nous utilise XCode toobuild et déploiement d’une application de hello sur des notifications push de hello appareil tootest comme iOS permet uniquement le périphérique réel du tooan des notifications push.</span><span class="sxs-lookup"><span data-stu-id="4c674-163">We will use XCode toobuild and deploy hello app on hello device tootest push notifications since iOS only allows push notifications tooan actual device.</span></span> <span data-ttu-id="4c674-164">Atteindre l’emplacement toohello où votre projet Cordova est créé et accédez trop**...\platforms\ios** emplacement.</span><span class="sxs-lookup"><span data-stu-id="4c674-164">Go toohello location where your Cordova project is created and navigate too**...\platforms\ios** location.</span></span> <span data-ttu-id="4c674-165">Ouvrez le fichier .xcodeproj natif de hello dans XCode.</span><span class="sxs-lookup"><span data-stu-id="4c674-165">Open up hello native .xcodeproj file in XCode.</span></span> 
2. <span data-ttu-id="4c674-166">Générez et déployez hello Cordova application toohello l’appareil iOS à l’aide du compte hello hello contenant le certificat hello que vous venez de télécharger portail Mobile Engagement de toohello et hello Id d’application qui correspond à hello vous fourni lors de la création de profil de configuration Hello d’application Cordova.</span><span class="sxs-lookup"><span data-stu-id="4c674-166">Build and deploy hello Cordova app toohello iOS device using hello account which has hello provisioning profile containing hello certificate you just uploaded toohello Mobile Engagement portal and hello App Id which matches hello one you provided while creating hello Cordova app.</span></span> <span data-ttu-id="4c674-167">Vous pouvez extraire hello *identificateur de lot* dans votre **ressources\*-info.plist** fichier dans XCode toomatch haut.</span><span class="sxs-lookup"><span data-stu-id="4c674-167">You can check out hello *Bundle identifier* in your **Resources\*-info.plist** file in XCode toomatch it up.</span></span> 
3. <span data-ttu-id="4c674-168">Vous verrez la fenêtre contextuelle des e/s standard hello sur votre appareil indiquant que cette application hello demande notifications toosend d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="4c674-168">You will see hello standard iOS popup on your device saying that hello app requests permission toosend notifications.</span></span> <span data-ttu-id="4c674-169">Accordez l’autorisation de hello.</span><span class="sxs-lookup"><span data-stu-id="4c674-169">Grant hello permission.</span></span> 

<span data-ttu-id="4c674-170">**[Android]**</span><span class="sxs-lookup"><span data-stu-id="4c674-170">**[Android]**</span></span>

<span data-ttu-id="4c674-171">Vous pouvez simplement utiliser hello émulateur toorun hello application Android comme émulateur Android de hello prennent en charge les notifications GCM.</span><span class="sxs-lookup"><span data-stu-id="4c674-171">You can simply use hello emulator toorun hello Android app as GCM notifications are supported on hello Android emulator.</span></span> 

    cordova run android

## <span data-ttu-id="4c674-172"><a id="send"></a>Envoi d’une application tooyour de notification</span><span class="sxs-lookup"><span data-stu-id="4c674-172"><a id="send"></a>Send a notification tooyour app</span></span>
<span data-ttu-id="4c674-173">Nous allons maintenant créer une campagne de Notification Push simple qui envoie une application de tooyour par émission de données en cours d’exécution sur l’appareil de hello :</span><span class="sxs-lookup"><span data-stu-id="4c674-173">We will now create a simple Push Notification campaign that will send a push tooyour app running on hello device:</span></span>

1. <span data-ttu-id="4c674-174">Accédez toohello **atteindre** onglet dans votre portail Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="4c674-174">Navigate toohello **Reach** tab in your Mobile Engagement portal</span></span>
2. <span data-ttu-id="4c674-175">Cliquez sur **nouvelle annonce** toocreate votre campagne push</span><span class="sxs-lookup"><span data-stu-id="4c674-175">Click **New Announcement** toocreate your push campaign</span></span>
   
    ![][6]
3. <span data-ttu-id="4c674-176">Fournir des entrées toocreate votre campagne **[Android]**</span><span class="sxs-lookup"><span data-stu-id="4c674-176">Provide inputs toocreate your campaign **[Android]**</span></span>
   
   * <span data-ttu-id="4c674-177">Entrez un **nom** pour votre campagne.</span><span class="sxs-lookup"><span data-stu-id="4c674-177">Provide a **Name** for your campaign.</span></span> 
   * <span data-ttu-id="4c674-178">Sélectionnez hello **Type de remise** en tant que *notification système* *Simple*</span><span class="sxs-lookup"><span data-stu-id="4c674-178">Select hello **Delivery Type** as *System notification* *Simple*</span></span>
   * <span data-ttu-id="4c674-179">Sélectionnez hello **heure de remise** comme *« Any Time »*</span><span class="sxs-lookup"><span data-stu-id="4c674-179">Select hello **Delivery time** as *"Any Time"*</span></span>
   * <span data-ttu-id="4c674-180">Fournir un **titre** pour votre notification qui sera hello première ligne de commande de hello.</span><span class="sxs-lookup"><span data-stu-id="4c674-180">Provide a **Title** for your notification which will be hello first line in hello push.</span></span>
   * <span data-ttu-id="4c674-181">Fournir un **Message** pour votre notification qui servira de corps du message hello.</span><span class="sxs-lookup"><span data-stu-id="4c674-181">Provide a **Message** for your notification which will serve as hello message body.</span></span> 
     
     ![][11]
4. <span data-ttu-id="4c674-182">Fournir des entrées toocreate votre campagne **[e]**</span><span class="sxs-lookup"><span data-stu-id="4c674-182">Provide inputs toocreate your campaign **[iOS]**</span></span>
   
   * <span data-ttu-id="4c674-183">Entrez un **nom** pour votre campagne.</span><span class="sxs-lookup"><span data-stu-id="4c674-183">Provide a **Name** for your campaign.</span></span> 
   * <span data-ttu-id="4c674-184">Sélectionnez hello **heure de remise** comme *« hors de l’application »*</span><span class="sxs-lookup"><span data-stu-id="4c674-184">Select hello **Delivery time** as *"Out of app only"*</span></span>
   * <span data-ttu-id="4c674-185">Fournir un **titre** pour votre notification qui sera hello première ligne de commande de hello.</span><span class="sxs-lookup"><span data-stu-id="4c674-185">Provide a **Title** for your notification which will be hello first line in hello push.</span></span>
   * <span data-ttu-id="4c674-186">Fournir un **Message** pour votre notification qui servira de corps du message hello.</span><span class="sxs-lookup"><span data-stu-id="4c674-186">Provide a **Message** for your notification which will serve as hello message body.</span></span> 
     
     ![][12]
5. <span data-ttu-id="4c674-187">Faites défiler et Bonjour section de contenu, sélectionnez **Notification uniquement**</span><span class="sxs-lookup"><span data-stu-id="4c674-187">Scroll down, and in hello content section select **Notification only**</span></span>
   
    ![][8]
6. <span data-ttu-id="4c674-188">[Facultatif] Vous pouvez également fournir une URL d’action.</span><span class="sxs-lookup"><span data-stu-id="4c674-188">[Optional] You can also provide an Action URL.</span></span> <span data-ttu-id="4c674-189">Assurez-vous qu’il utilise un modèle d’URL fourni lors de la configuration du plug-in de hello **AZME\_rediriger\_URL** variable, par exemple *myapp://test*.</span><span class="sxs-lookup"><span data-stu-id="4c674-189">Make sure that it uses a URL scheme provided while configuring hello plugin's **AZME\_REDIRECT\_URL** variable e.g. *myapp://test*.</span></span>  
7. <span data-ttu-id="4c674-190">Vous avez terminé possible de campagne paramètre hello plus simple.</span><span class="sxs-lookup"><span data-stu-id="4c674-190">You're done setting hello most basic campaign possible.</span></span> <span data-ttu-id="4c674-191">Maintenant défiler à nouveau vers le bas et cliquez sur hello **créer** bouton toosave votre campagne.</span><span class="sxs-lookup"><span data-stu-id="4c674-191">Now scroll down again and click hello **Create** button toosave your campaign.</span></span>
8. <span data-ttu-id="4c674-192">Enfin, dernière étape, **activez** votre campagne.</span><span class="sxs-lookup"><span data-stu-id="4c674-192">Finally **Activate** your campaign</span></span>
   
    ![][10]
9. <span data-ttu-id="4c674-193">Vous devriez maintenant voir une notification Push sur votre appareil ou votre émulateur dans le cadre de cette campagne.</span><span class="sxs-lookup"><span data-stu-id="4c674-193">You should now see a push notification on your device or emulator as part of this campaign.</span></span> 

## <span data-ttu-id="4c674-194"><a id="next-steps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4c674-194"><a id="next-steps"></a>Next Steps</span></span>
[<span data-ttu-id="4c674-195">Vue d'ensemble de toutes les méthodes disponibles avec le Kit de développement logiciel (SDK) Cordova Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="4c674-195">Overview of all methods available with Cordova Mobile Engagement SDK</span></span>](https://github.com/Azure/azure-mobile-engagement-cordova)

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

