---
title: tooApache de Notifications Push aaaAdd application Cordova avec les applications mobiles Azure | Documents Microsoft
description: "Découvrez comment toouse Azure Mobile Apps toosend push notifications tooyour Apache Cordova application."
services: app-service\mobile
documentationcenter: javascript
manager: syntaxc4
editor: 
author: ggailey777
ms.assetid: 92c596a9-875c-4840-b0e1-69198817576f
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 8e1b23d6145b446b6f01599337b677e2f2b31d7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-apache-cordova-app"></a><span data-ttu-id="86d5f-103">Ajouter une application de push notifications tooyour Apache Cordova</span><span class="sxs-lookup"><span data-stu-id="86d5f-103">Add push notifications tooyour Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="86d5f-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="86d5f-104">Overview</span></span>
<span data-ttu-id="86d5f-105">Dans ce didacticiel, vous ajoutez le projet toohello [démarrage rapide de Apache Cordova] de notifications push afin qu’une notification push est envoyée toohello périphérique chaque fois qu’un enregistrement est inséré.</span><span class="sxs-lookup"><span data-stu-id="86d5f-105">In this tutorial, you add push notifications toohello [Apache Cordova quick start] project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="86d5f-106">Si vous n’utilisez pas hello téléchargé le projet de démarrage rapide de serveur, vous devez hello package d’extension de notification push.</span><span class="sxs-lookup"><span data-stu-id="86d5f-106">If you do not use hello downloaded quick start server project, you need hello push notification extension package.</span></span> <span data-ttu-id="86d5f-107">Pour plus d’informations, consultez [fonctionne avec serveur principal de .NET hello SDK pour les applications mobiles Azure][1].</span><span class="sxs-lookup"><span data-stu-id="86d5f-107">For more information, see [Work with hello .NET backend server SDK for Azure Mobile Apps][1].</span></span>

## <span data-ttu-id="86d5f-108"><a name="prerequisites"></a>Configuration requise</span><span class="sxs-lookup"><span data-stu-id="86d5f-108"><a name="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="86d5f-109">Ce didacticiel décrit une application Apache Cordova développée avec Visual Studio 2015 qui s’exécute sur hello émulateur Android de Google, un appareil Android, un périphérique Windows et un appareil iOS.</span><span class="sxs-lookup"><span data-stu-id="86d5f-109">This tutorial covers an Apache Cordova application developed with Visual Studio 2015 that runs on hello Google Android Emulator, an Android device, a Windows device, and an iOS device.</span></span>

<span data-ttu-id="86d5f-110">toocomplete ce didacticiel, vous devez :</span><span class="sxs-lookup"><span data-stu-id="86d5f-110">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="86d5f-111">Un PC avec [Visual Studio Community 2015][2] ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="86d5f-111">A PC with [Visual Studio Community 2015][2] or later versions.</span></span>
* <span data-ttu-id="86d5f-112">[Visual Studio Tools pour Apache Cordova][4].</span><span class="sxs-lookup"><span data-stu-id="86d5f-112">[Visual Studio Tools for Apache Cordova][4].</span></span>
* <span data-ttu-id="86d5f-113">Un [compte Azure actif][3].</span><span class="sxs-lookup"><span data-stu-id="86d5f-113">An [active Azure account][3].</span></span>
* <span data-ttu-id="86d5f-114">Un projet [Démarrage rapide Apache Cordova][5] .</span><span class="sxs-lookup"><span data-stu-id="86d5f-114">A completed [Apache Cordova quick start][5] project.</span></span>
* <span data-ttu-id="86d5f-115">Un [compte Google][6] avec une adresse électronique vérifiée.</span><span class="sxs-lookup"><span data-stu-id="86d5f-115">(Android) A [Google account][6] with a verified email address.</span></span>
* <span data-ttu-id="86d5f-116">(iOS) Un [abonnement au programme pour développeurs Apple][7] et un appareil iOS (le simulateur iOS ne prend pas en charge les notifications Push).</span><span class="sxs-lookup"><span data-stu-id="86d5f-116">(iOS) An [Apple Developer Program membership][7] and an iOS device (iOS Simulator does not support push).</span></span>
* <span data-ttu-id="86d5f-117">(Windows) Un [compte de développeur Windows Store][8] et un appareil Windows 10.</span><span class="sxs-lookup"><span data-stu-id="86d5f-117">(Windows) A [Windows Store Developer Account][8] and a Windows 10 device.</span></span>

## <span data-ttu-id="86d5f-118"><a name="configure-hub"></a>Configurer un hub de notification</span><span class="sxs-lookup"><span data-stu-id="86d5f-118"><a name="configure-hub"></a>Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

<span data-ttu-id="86d5f-119">[Regarder une vidéo illustrant les étapes de cette section][9]</span><span class="sxs-lookup"><span data-stu-id="86d5f-119">[Watch a video showing steps in this section][9]</span></span>

## <a name="update-hello-server-project"></a><span data-ttu-id="86d5f-120">Mettre à jour le projet de serveur hello</span><span class="sxs-lookup"><span data-stu-id="86d5f-120">Update hello server project</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <span data-ttu-id="86d5f-121"><a name="add-push-to-app"></a>Modification de votre application Cordova</span><span class="sxs-lookup"><span data-stu-id="86d5f-121"><a name="add-push-to-app"></a>Modify your Cordova app</span></span>
<span data-ttu-id="86d5f-122">Assurez-vous que votre projet d’application Apache Cordova est prêt toohandle des notifications de push par plug-in du push de Cordova hello lors de l’installation ainsi que tous les services par émission de données spécifiques à la plateforme.</span><span class="sxs-lookup"><span data-stu-id="86d5f-122">Ensure your Apache Cordova app project is ready toohandle push notifications by installing hello Cordova push plugin plus any platform-specific push services.</span></span>

#### <a name="update-hello-cordova-version-in-your-project"></a><span data-ttu-id="86d5f-123">Mettre à jour la version de Cordova hello dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="86d5f-123">Update hello Cordova version in your project.</span></span>
<span data-ttu-id="86d5f-124">Si votre projet utilise une version antérieure à v6.1.1 d’Apache Cordova, mettre à jour le projet de client hello.</span><span class="sxs-lookup"><span data-stu-id="86d5f-124">If your project uses a version of Apache Cordova earlier than v6.1.1, update hello client project.</span></span> <span data-ttu-id="86d5f-125">projet de hello tooupdate :</span><span class="sxs-lookup"><span data-stu-id="86d5f-125">tooupdate hello project:</span></span>

* <span data-ttu-id="86d5f-126">Avec le bouton droit `config.xml` Concepteur de configuration tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="86d5f-126">Right-click `config.xml` tooopen hello configuration designer.</span></span>
* <span data-ttu-id="86d5f-127">Sélectionnez l’onglet de plateformes hello.</span><span class="sxs-lookup"><span data-stu-id="86d5f-127">Select hello Platforms tab.</span></span>
* <span data-ttu-id="86d5f-128">Choisissez 6.1.1 Bonjour **Cordova CLI** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="86d5f-128">Choose 6.1.1 in hello **Cordova CLI** text box.</span></span>
* <span data-ttu-id="86d5f-129">Choisissez **générer**, puis **générer la Solution** projet hello de tooupdate.</span><span class="sxs-lookup"><span data-stu-id="86d5f-129">Choose **Build**, then **Build Solution** tooupdate hello project.</span></span>

#### <a name="install-hello-push-plugin"></a><span data-ttu-id="86d5f-130">Installez le plug-in de hello push</span><span class="sxs-lookup"><span data-stu-id="86d5f-130">Install hello push plugin</span></span>
<span data-ttu-id="86d5f-131">En mode natif, les applications Apache Cordova ne gèrent pas les fonctionnalités de réseau ou d’appareils.</span><span class="sxs-lookup"><span data-stu-id="86d5f-131">Apache Cordova applications do not natively handle device or network capabilities.</span></span>  <span data-ttu-id="86d5f-132">Ces fonctionnalités sont fournies par des plug-ins publiés sur [npm][10] ou sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="86d5f-132">These capabilities are provided by plugins that are published either on [npm][10] or on GitHub.</span></span>  <span data-ttu-id="86d5f-133">Hello `phonegap-plugin-push` plug-in est toohandle utilisé réseau les notifications push.</span><span class="sxs-lookup"><span data-stu-id="86d5f-133">hello `phonegap-plugin-push` plugin is used toohandle network push notifications.</span></span>

<span data-ttu-id="86d5f-134">Vous pouvez installer le plug-in de hello par émission de données dans une des manières suivantes :</span><span class="sxs-lookup"><span data-stu-id="86d5f-134">You can install hello push plugin in one of these ways:</span></span>

<span data-ttu-id="86d5f-135">**À partir de hello d’invite de commandes :**</span><span class="sxs-lookup"><span data-stu-id="86d5f-135">**From hello command-prompt:**</span></span>

<span data-ttu-id="86d5f-136">Exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="86d5f-136">Execute hello following command:</span></span>

    cordova plugin add phonegap-plugin-push

<span data-ttu-id="86d5f-137">**À partir de Visual Studio :**</span><span class="sxs-lookup"><span data-stu-id="86d5f-137">**From within Visual Studio:**</span></span>

1. <span data-ttu-id="86d5f-138">Dans l’Explorateur de solutions, ouvrez hello `config.xml` fichier, cliquez sur **plug-ins** > **personnalisé**, sélectionnez **Git** comme source d’installation, puis entrez `https://github.com/phonegap/phonegap-plugin-push`en tant que source de hello.</span><span class="sxs-lookup"><span data-stu-id="86d5f-138">In Solution Explorer, open hello `config.xml` file click **Plugins** > **Custom**, select **Git** as the  installation source, then enter `https://github.com/phonegap/phonegap-plugin-push` as hello source.</span></span>

   ![][img1]

2. <span data-ttu-id="86d5f-139">Cliquez sur source d’installation toohello suivant hello flèche.</span><span class="sxs-lookup"><span data-stu-id="86d5f-139">Click hello arrow next toohello installation source.</span></span>
3. <span data-ttu-id="86d5f-140">Dans **SENDER_ID**, si vous avez déjà un ID numérique de projet pour le projet de Console des développeurs Google hello, vous pouvez l’ajouter ici.</span><span class="sxs-lookup"><span data-stu-id="86d5f-140">In **SENDER_ID**, if you already have a numeric project ID for hello Google Developer Console project, you can add it here.</span></span> <span data-ttu-id="86d5f-141">Entrez temporairement une valeur d’espace réservé, par exemple, 777777.</span><span class="sxs-lookup"><span data-stu-id="86d5f-141">Otherwise, enter a placeholder value, like 777777.</span></span>  <span data-ttu-id="86d5f-142">Si vous ciblez Android, vous pourrez modifier cette valeur dans le fichier config.xml ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="86d5f-142">If you are targeting Android, you can update this value in config.xml later.</span></span>
4. <span data-ttu-id="86d5f-143">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="86d5f-143">Click **Add**.</span></span>

<span data-ttu-id="86d5f-144">le plug-in de Hello push est maintenant installé.</span><span class="sxs-lookup"><span data-stu-id="86d5f-144">hello push plugin is now installed.</span></span>

#### <a name="install-hello-device-plugin"></a><span data-ttu-id="86d5f-145">Installez le plug-in de hello appareil</span><span class="sxs-lookup"><span data-stu-id="86d5f-145">Install hello device plugin</span></span>
<span data-ttu-id="86d5f-146">Suivez hello même procédure que vous avez utilisé le plug-in de tooinstall hello par émission de données.</span><span class="sxs-lookup"><span data-stu-id="86d5f-146">Follow hello same procedure you used tooinstall hello push plugin.</span></span>  <span data-ttu-id="86d5f-147">Ajouter le plug-in de hello appareil à partir de la liste de plug-ins hello Core (cliquez sur **plug-ins** > **Core** toofind il).</span><span class="sxs-lookup"><span data-stu-id="86d5f-147">Add hello Device plugin from hello Core plugins list (click **Plugins** > **Core** toofind it).</span></span> <span data-ttu-id="86d5f-148">Vous avez besoin de ce nom de la plateforme plug-in tooobtain hello.</span><span class="sxs-lookup"><span data-stu-id="86d5f-148">You need this plugin tooobtain hello platform name.</span></span>

#### <a name="register-your-device-on-application-start-up"></a><span data-ttu-id="86d5f-149">Inscription de votre appareil au démarrage de l’application</span><span class="sxs-lookup"><span data-stu-id="86d5f-149">Register your device on application start-up</span></span>
<span data-ttu-id="86d5f-150">Initialement, nous proposons un code minimal pour Android.</span><span class="sxs-lookup"><span data-stu-id="86d5f-150">Initially, we include some minimal code for Android.</span></span> <span data-ttu-id="86d5f-151">Par la suite, modifiez toorun d’application hello sur iOS ou Windows 10.</span><span class="sxs-lookup"><span data-stu-id="86d5f-151">Later, modify hello app toorun on iOS or Windows 10.</span></span>

1. <span data-ttu-id="86d5f-152">Ajoutez un appel trop**registerForPushNotifications** pendant le rappel hello pour le processus de connexion hello ou bas hello hello **onDeviceReady** méthode :</span><span class="sxs-lookup"><span data-stu-id="86d5f-152">Add a call too**registerForPushNotifications** during hello callback for hello login process, or at hello bottom of  hello **onDeviceReady** method:</span></span>

        // Login toohello service.
        client.login('google')
            .then(function () {
                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh hello todoItems
                refreshDisplay();

                // Wire up hello UI Event Handler for hello Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                    // Added tooregister for push notifications.
                registerForPushNotifications();

            }, handleError);

    <span data-ttu-id="86d5f-153">Cet exemple montre l’appel de **registerForPushNotifications** après une authentification réussie.</span><span class="sxs-lookup"><span data-stu-id="86d5f-153">This example shows calling **registerForPushNotifications** after authentication succeeds.</span></span>  <span data-ttu-id="86d5f-154">Vous pouvez appeler `registerForPushNotifications()` aussi souvent que nécessaire.</span><span class="sxs-lookup"><span data-stu-id="86d5f-154">You can call `registerForPushNotifications()` as often as is required.</span></span>

2. <span data-ttu-id="86d5f-155">Ajouter hello nouvelle **registerForPushNotifications** méthode comme suit :</span><span class="sxs-lookup"><span data-stu-id="86d5f-155">Add hello new **registerForPushNotifications** method as follows:</span></span>

        // Register for Push Notifications. Requires that phonegap-plugin-push be installed.
        var pushRegistration = null;
        function registerForPushNotifications() {
          pushRegistration = PushNotification.init({
              android: { senderID: 'Your_Project_ID' },
              ios: { alert: 'true', badge: 'true', sound: 'true' },
              wns: {}
          });

        // Handle hello registration event.
        pushRegistration.on('registration', function (data) {
          // Get hello native platform of hello device.
          var platform = device.platform;
          // Get hello handle returned during registration.
          var handle = data.registrationId;
          // Set hello device-specific message template.
          if (platform == 'android' || platform == 'Android') {
              // Register for GCM notifications.
              client.push.register('gcm', handle, {
                  mytemplate: { body: { data: { message: "{$(messageParam)}" } } }
              });
          } else if (device.platform === 'iOS') {
              // Register for notifications.
              client.push.register('apns', handle, {
                  mytemplate: { body: { aps: { alert: "{$(messageParam)}" } } }
              });
          } else if (device.platform === 'windows') {
              // Register for WNS notifications.
              client.push.register('wns', handle, {
                  myTemplate: {
                      body: '<toast><visual><binding template="ToastText01"><text id="1">$(messageParam)</text></binding></visual></toast>',
                      headers: { 'X-WNS-Type': 'wns/toast' } }
              });
          }
        });

        pushRegistration.on('notification', function (data, d2) {
          alert('Push Received: ' + data.message);
        });

        pushRegistration.on('error', handleError);
        }
3. <span data-ttu-id="86d5f-156">(Android) Bonjour précédant le code, remplacez `Your_Project_ID` avec numérique de hello ID du projet pour votre application à partir de la [Console des développeurs Google][18].</span><span class="sxs-lookup"><span data-stu-id="86d5f-156">(Android) In hello preceding code, replace `Your_Project_ID` with hello numeric project ID for your app from the  [Google Developer Console][18].</span></span>

## <a name="optional-configure-and-run-hello-app-on-android"></a><span data-ttu-id="86d5f-157">(Facultatif) Configurer et exécuter l’application hello sur Android</span><span class="sxs-lookup"><span data-stu-id="86d5f-157">(Optional) Configure and run hello app on Android</span></span>
<span data-ttu-id="86d5f-158">Effectuez cette section tooenable push les notifications pour Android.</span><span class="sxs-lookup"><span data-stu-id="86d5f-158">Complete this section tooenable push notifications for Android.</span></span>

#### <span data-ttu-id="86d5f-159"><a name="enable-gcm"></a>Activation de Firebase Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="86d5f-159"><a name="enable-gcm"></a>Enable Firebase Cloud Messaging</span></span>
<span data-ttu-id="86d5f-160">Étant donné que nous prévoyons initialement hello plateforme de Google Android, vous devez activer Firebase de messagerie Cloud.</span><span class="sxs-lookup"><span data-stu-id="86d5f-160">Since we are targeting hello Google Android platform initially, you must enable Firebase Cloud Messaging.</span></span>

[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

#### <span data-ttu-id="86d5f-161"><a name="configure-backend"></a>Configurer hello à l’aide de FCM des demandes par l’application Mobile back-end toosend par émission de données</span><span class="sxs-lookup"><span data-stu-id="86d5f-161"><a name="configure-backend"></a>Configure hello Mobile App backend toosend push requests using FCM</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

#### <a name="configure-your-cordova-app-for-android"></a><span data-ttu-id="86d5f-162">Configuration de votre application Cordova pour Android</span><span class="sxs-lookup"><span data-stu-id="86d5f-162">Configure your Cordova app for Android</span></span>
<span data-ttu-id="86d5f-163">Dans votre application Cordova, ouvrez le fichier config.xml et remplacez `Your_Project_ID` avec numérique de hello ID du projet pour votre application à partir de hello [Console des développeurs Google][18].</span><span class="sxs-lookup"><span data-stu-id="86d5f-163">In your Cordova app, open config.xml and replace `Your_Project_ID` with hello numeric project ID for your app from hello [Google Developer Console][18].</span></span>

        <plugin name="phonegap-plugin-push" version="1.7.1" src="https://github.com/phonegap/phonegap-plugin-push.git">
            <variable name="SENDER_ID" value="Your_Project_ID" />
        </plugin>

<span data-ttu-id="86d5f-164">Ouvrez index.js et mettre à jour toouse de code hello votre ID de projet numérique.</span><span class="sxs-lookup"><span data-stu-id="86d5f-164">Open index.js and update hello code toouse your numeric project ID.</span></span>

        pushRegistration = PushNotification.init({
            android: { senderID: 'Your_Project_ID' },
            ios: { alert: 'true', badge: 'true', sound: 'true' },
            wns: {}
        });

#### <span data-ttu-id="86d5f-165"><a name="configure-device"></a>Configuration de votre appareil Android pour le débogage USB</span><span class="sxs-lookup"><span data-stu-id="86d5f-165"><a name="configure-device"></a>Configure your Android device for USB debugging</span></span>
<span data-ttu-id="86d5f-166">Avant de déployer votre application de tooyour appareil Android, vous devez tooenable débogage USB.</span><span class="sxs-lookup"><span data-stu-id="86d5f-166">Before you can deploy your application tooyour Android Device, you need tooenable USB Debugging.</span></span>  <span data-ttu-id="86d5f-167">Sur votre téléphone Android, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="86d5f-167">Perform the following steps on your Android phone:</span></span>

1. <span data-ttu-id="86d5f-168">Accédez trop**paramètres** > **propos du téléphone**, puis appuyez sur hello **numéro de Build** jusqu'à ce que le mode développeur est activé (environ sept fois).</span><span class="sxs-lookup"><span data-stu-id="86d5f-168">Go too**Settings** > **About phone**, then tap hello **Build number** until developer mode is enabled  (about seven times).</span></span>
2. <span data-ttu-id="86d5f-169">Dans les **paramètres** > **Developer Options** activer **débogage USB**, puis connectez votre PC de développement tooyour téléphone Android avec un câble USB.</span><span class="sxs-lookup"><span data-stu-id="86d5f-169">Back in **Settings** > **Developer Options** enable **USB debugging**, then connect your Android phone  tooyour development PC with a USB Cable.</span></span>

<span data-ttu-id="86d5f-170">Nous avons testé cette procédure à l’aide d’un appareil Google Nexus 5 X exécutant Android 6.0 (Marshmallow).</span><span class="sxs-lookup"><span data-stu-id="86d5f-170">We tested this using a Google Nexus 5X device running Android 6.0 (Marshmallow).</span></span>  <span data-ttu-id="86d5f-171">Toutefois, les techniques de hello sont communs à n’importe quelle version d’Android moderne.</span><span class="sxs-lookup"><span data-stu-id="86d5f-171">However, hello techniques are common across any modern Android release.</span></span>

#### <a name="install-google-play-services"></a><span data-ttu-id="86d5f-172">Installation des services Google Play</span><span class="sxs-lookup"><span data-stu-id="86d5f-172">Install Google Play Services</span></span>
<span data-ttu-id="86d5f-173">le plug-in de Hello push s’appuie sur Android Services Google Play pour des notifications push.</span><span class="sxs-lookup"><span data-stu-id="86d5f-173">hello push plugin relies on Android Google Play Services for push notifications.</span></span>

1. <span data-ttu-id="86d5f-174">Dans Visual Studio, cliquez sur **outils** > **Android** > **Android SDK Manager**, développez hello **Extras** dossier et vérifiez hello boîte toomake que chacun des hello suivant des kits de développement logiciel est installé.</span><span class="sxs-lookup"><span data-stu-id="86d5f-174">In Visual Studio, click **Tools** > **Android** > **Android SDK Manager**, expand hello **Extras** folder and  check hello box toomake sure that each of hello following SDKs is installed.</span></span>

   * <span data-ttu-id="86d5f-175">Android 2.3 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="86d5f-175">Android 2.3 or higher</span></span>
   * <span data-ttu-id="86d5f-176">Révision du référentiel Google 27 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="86d5f-176">Google Repository revision 27 or higher</span></span>
   * <span data-ttu-id="86d5f-177">Google Play Services 9.0.2 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="86d5f-177">Google Play Services 9.0.2 or higher</span></span>

2. <span data-ttu-id="86d5f-178">Cliquez sur **installer les Packages** et attendez hello installation toocomplete.</span><span class="sxs-lookup"><span data-stu-id="86d5f-178">Click **Install Packages** and wait for hello installation toocomplete.</span></span>

<span data-ttu-id="86d5f-179">Hello actuel requis bibliothèques sont répertoriées dans hello [la documentation d’installation du plug-in-push phonegap][19].</span><span class="sxs-lookup"><span data-stu-id="86d5f-179">hello current required libraries are listed in hello [phonegap-plugin-push installation documentation][19].</span></span>

#### <a name="test-push-notifications-in-hello-app-on-android"></a><span data-ttu-id="86d5f-180">Notifications push de test dans une application hello sur Android</span><span class="sxs-lookup"><span data-stu-id="86d5f-180">Test push notifications in hello app on Android</span></span>
<span data-ttu-id="86d5f-181">Vous pouvez à présent des notifications push de test en exécutant hello application et l’insertion d’éléments dans la table TodoItem de hello.</span><span class="sxs-lookup"><span data-stu-id="86d5f-181">You can now test push notifications by running hello app and inserting items in hello TodoItem table.</span></span> <span data-ttu-id="86d5f-182">Vous pouvez tester de hello même appareil ou à partir d’un deuxième appareil, tant que vous utilisez hello même principal.</span><span class="sxs-lookup"><span data-stu-id="86d5f-182">You can test from hello same device or from a second device, as long as you are using hello same backend.</span></span> <span data-ttu-id="86d5f-183">Tester votre application Cordova sur la plateforme Android de hello dans un des hello suivant façons :</span><span class="sxs-lookup"><span data-stu-id="86d5f-183">Test your Cordova app on hello Android platform in one of hello following ways:</span></span>

* <span data-ttu-id="86d5f-184">**Sur un appareil physique :** attacher votre ordinateur de développement tooyour appareil Android avec un câble USB.</span><span class="sxs-lookup"><span data-stu-id="86d5f-184">**On a physical device:** Attach your Android device tooyour development computer with a USB cable.</span></span>  <span data-ttu-id="86d5f-185">Au lieu de **l’Émulateur Google Android**, sélectionnez **Appareil**.</span><span class="sxs-lookup"><span data-stu-id="86d5f-185">Instead of **Google Android Emulator**, select **Device**.</span></span> <span data-ttu-id="86d5f-186">Visual Studio déploie l’appareil de toohello application hello, puis exécute application hello.</span><span class="sxs-lookup"><span data-stu-id="86d5f-186">Visual Studio deploys hello application toohello device and then runs hello application.</span></span>  <span data-ttu-id="86d5f-187">Ensuite, vous pouvez interagir avec l’application hello sur l’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="86d5f-187">You can then interact with hello application on hello device.</span></span>

  <span data-ttu-id="86d5f-188">Améliorez votre expérience du développement.</span><span class="sxs-lookup"><span data-stu-id="86d5f-188">Improve your development experience.</span></span>  <span data-ttu-id="86d5f-189">Les applications de partage d’écran telles que [Mobizen] [20] peuvent vous aider à développer une application Android.</span><span class="sxs-lookup"><span data-stu-id="86d5f-189">Screen sharing applications such as [Mobizen][20] can assist you in developing an Android application.</span></span>  <span data-ttu-id="86d5f-190">Mobizen projette votre navigateur web de tooa écran Android sur votre PC.</span><span class="sxs-lookup"><span data-stu-id="86d5f-190">Mobizen projects your Android screen tooa web browser on your PC.</span></span>

* <span data-ttu-id="86d5f-191">**Sur un émulateur Android :** des étapes de configuration supplémentaires sont requises lors de l’exécution sur un émulateur.</span><span class="sxs-lookup"><span data-stu-id="86d5f-191">**On an Android emulator:** There are additional configuration steps required when running on an emulator.</span></span>

    <span data-ttu-id="86d5f-192">Assurez-vous que vous déployez un périphérique virtuel tooa disposant APIs Google défini en tant que cible de hello, comme indiqué dans le Gestionnaire de périphériques virtuels Android (AVD) hello.</span><span class="sxs-lookup"><span data-stu-id="86d5f-192">Make sure you are deploying tooa virtual device that has Google APIs set as hello target, as shown in hello Android Virtual Device (AVD) manager.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/google-apis-avd-settings.png)

    <span data-ttu-id="86d5f-193">Si vous souhaitez un x86 plus rapide que toouse émulateur, vous [installer le pilote HAXM à hello] [ 11] et configurer hello émulateur toouse il.</span><span class="sxs-lookup"><span data-stu-id="86d5f-193">If you want toouse a faster x86 emulator, you [install hello HAXM driver][11] and configure hello emulator toouse it.</span></span>

    <span data-ttu-id="86d5f-194">Ajouter un appareil Android de Google compte toohello en cliquant sur **applications** > **paramètres** > **Ajouter compte**, puis suivez les invites hello.</span><span class="sxs-lookup"><span data-stu-id="86d5f-194">Add a Google account toohello Android device by clicking **Apps** > **Settings** > **Add account**, then follow hello prompts.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/add-google-account.png)

    <span data-ttu-id="86d5f-195">Exécutez hello d’application todolist comme avant et insérer un nouvel élément de tâche.</span><span class="sxs-lookup"><span data-stu-id="86d5f-195">Run hello todolist app as before and insert a new todo item.</span></span> <span data-ttu-id="86d5f-196">Cette fois-ci, une icône de notification s’affiche dans la zone de notification hello.</span><span class="sxs-lookup"><span data-stu-id="86d5f-196">This time, a notification icon is displayed in hello notification area.</span></span> <span data-ttu-id="86d5f-197">Vous pouvez ouvrir hello notification tiroir tooview hello texte intégral de la notification de hello.</span><span class="sxs-lookup"><span data-stu-id="86d5f-197">You can open hello notification drawer tooview hello full text of hello notification.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/android-notifications.png)

## <a name="optional-configure-and-run-on-ios"></a><span data-ttu-id="86d5f-198">(Facultatif) Configurer et exécuter sur iOS</span><span class="sxs-lookup"><span data-stu-id="86d5f-198">(Optional) Configure and run on iOS</span></span>
<span data-ttu-id="86d5f-199">Cette section est de projet Cordova de hello en cours d’exécution sur les appareils iOS.</span><span class="sxs-lookup"><span data-stu-id="86d5f-199">This section is for running hello Cordova project on iOS devices.</span></span> <span data-ttu-id="86d5f-200">Vous pouvez ignorer cette section si vous n'utilisez pas d'appareils iOS.</span><span class="sxs-lookup"><span data-stu-id="86d5f-200">If you are not working with iOS devices, you can skip this section.</span></span>

#### <a name="install-and-run-hello-ios-remote-build-agent-on-a-mac-or-cloud-service"></a><span data-ttu-id="86d5f-201">Installer et iOS hello exécution à distance de l’agent de build sur un Mac ou un service cloud</span><span class="sxs-lookup"><span data-stu-id="86d5f-201">Install and run hello iOS remote build agent on a Mac or cloud service</span></span>
<span data-ttu-id="86d5f-202">Avant de pouvoir exécuter une application Cordova sur iOS à l’aide de Visual Studio, ouvrez hello de hello [Guide d’installation iOS] [ 12] tooinstall et hello exécution à distance de l’agent de build.</span><span class="sxs-lookup"><span data-stu-id="86d5f-202">Before you can run a Cordova app on iOS using Visual Studio, go through hello steps in hello [iOS Setup Guide][12] tooinstall and run hello remote build agent.</span></span>

<span data-ttu-id="86d5f-203">Assurez-vous que vous pouvez créer des application hello pour iOS.</span><span class="sxs-lookup"><span data-stu-id="86d5f-203">Make sure you can build hello app for iOS.</span></span> <span data-ttu-id="86d5f-204">Hello étapes hello guide d’installation sont requis toobuild pour iOS depuis Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="86d5f-204">hello steps in hello setup guide are required toobuild for iOS from Visual Studio.</span></span> <span data-ttu-id="86d5f-205">Si vous n’avez pas d’un Mac, vous pouvez générer pour iOS à l’aide de l’agent de build distante hello sur un service comme MacInCloud.</span><span class="sxs-lookup"><span data-stu-id="86d5f-205">If you do not have a Mac, you can build for iOS using hello remote build agent on a service like MacInCloud.</span></span> <span data-ttu-id="86d5f-206">Pour plus d’informations, consultez [exécuter votre application iOS dans le cloud de hello][21].</span><span class="sxs-lookup"><span data-stu-id="86d5f-206">For more info, see [Run your iOS app in hello cloud][21].</span></span>

> [!NOTE]
> <span data-ttu-id="86d5f-207">XCode 7 ou version ultérieure est plug-in de push de hello toouse requis sur iOS.</span><span class="sxs-lookup"><span data-stu-id="86d5f-207">XCode 7 or greater is required toouse hello push plugin on iOS.</span></span>

#### <a name="find-hello-id-toouse-as-your-app-id"></a><span data-ttu-id="86d5f-208">Trouver hello ID toouse en tant que votre ID d’application</span><span class="sxs-lookup"><span data-stu-id="86d5f-208">Find hello ID toouse as your App ID</span></span>
<span data-ttu-id="86d5f-209">Avant d’inscrire votre application pour les notifications push, ouvrez le fichier config.xml dans votre application Cordova, recherche hello `id` valeur dans l’élément de widget hello d’attribut et le copier pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="86d5f-209">Before you register your app for push notifications, open config.xml in your Cordova app, find hello `id` attribute value in hello widget element, and copy it for later use.</span></span> <span data-ttu-id="86d5f-210">Bonjour XML suivant, ID de hello est `io.cordova.myapp7777777`.</span><span class="sxs-lookup"><span data-stu-id="86d5f-210">In hello following XML, hello ID is `io.cordova.myapp7777777`.</span></span>

        <widget defaultlocale="en-US" id="io.cordova.myapp7777777"
          version="1.0.0" windows-packageVersion="1.1.0.0" xmlns="http://www.w3.org/ns/widgets"
            xmlns:cdv="http://cordova.apache.org/ns/1.0" xmlns:vs="http://schemas.microsoft.com/appx/2014/htmlapps">

<span data-ttu-id="86d5f-211">Vous utiliserez cet identifiant ultérieurement lors de la création d’un ID d’application sur le portail des développeurs d’Apple.</span><span class="sxs-lookup"><span data-stu-id="86d5f-211">Later, use this identifier when you create an App ID on Apple's developer portal.</span></span> <span data-ttu-id="86d5f-212">Si vous créez un autre ID d’application sur le portail des développeurs hello, vous devez prendre quelques étapes supplémentaires plus loin dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="86d5f-212">If you create a different App ID on hello developer portal, you must take a few extra steps later in this tutorial.</span></span> <span data-ttu-id="86d5f-213">ID de Hello dans l’élément widget doit correspondre à hello ID d’application sur le portail des développeurs hello.</span><span class="sxs-lookup"><span data-stu-id="86d5f-213">hello ID in the widget element must match hello App ID on hello developer portal.</span></span>

#### <a name="register-hello-app-for-push-notifications-on-apples-developer-portal"></a><span data-ttu-id="86d5f-214">Inscrire l’application hello pour les notifications push sur le portail des développeurs d’Apple</span><span class="sxs-lookup"><span data-stu-id="86d5f-214">Register hello app for push notifications on Apple's developer portal</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

[<span data-ttu-id="86d5f-215">Regarder une vidéo montrant des étapes similaires</span><span class="sxs-lookup"><span data-stu-id="86d5f-215">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-5-Set-up-apns-for-push)

#### <a name="configure-azure-toosend-push-notifications"></a><span data-ttu-id="86d5f-216">Configurer des notifications push de toosend Azure</span><span class="sxs-lookup"><span data-stu-id="86d5f-216">Configure Azure toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

#### <a name="verify-that-your-app-id-matches-your-cordova-app"></a><span data-ttu-id="86d5f-217">Vérifier que votre ID d’application correspond à votre application Cordova</span><span class="sxs-lookup"><span data-stu-id="86d5f-217">Verify that your App ID matches your Cordova app</span></span>
<span data-ttu-id="86d5f-218">Si hello déjà créés dans votre compte de développeur Apple ID d’application correspond à hello des ID d’élément de widget hello dans le fichier config.xml, vous pouvez ignorer cette étape.</span><span class="sxs-lookup"><span data-stu-id="86d5f-218">If hello App ID you created in your Apple Developer Account already matches hello ID of hello widget element in config.xml, you can skip this step.</span></span> <span data-ttu-id="86d5f-219">Toutefois, si les identificateurs hello ne correspondent pas, prendre hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="86d5f-219">However, if hello IDs don't match, take hello following steps:</span></span>

1. <span data-ttu-id="86d5f-220">Supprimer le dossier de plateformes hello de votre projet.</span><span class="sxs-lookup"><span data-stu-id="86d5f-220">Delete hello platforms folder from your project.</span></span>
2. <span data-ttu-id="86d5f-221">Supprimer le dossier de plug-ins hello de votre projet.</span><span class="sxs-lookup"><span data-stu-id="86d5f-221">Delete hello plugins folder from your project.</span></span>
3. <span data-ttu-id="86d5f-222">Supprimez le dossier node_modules hello votre projet.</span><span class="sxs-lookup"><span data-stu-id="86d5f-222">Delete hello node_modules folder from your project.</span></span>
4. <span data-ttu-id="86d5f-223">Mettre à jour d’attribut d’id hello d’élément de widget hello dans config.xml toouse hello ID d’application que vous avez créé dans votre compte de développeur Apple.</span><span class="sxs-lookup"><span data-stu-id="86d5f-223">Update hello id attribute of hello widget element in config.xml toouse hello App ID that you created in your  Apple Developer Account.</span></span>
5. <span data-ttu-id="86d5f-224">Régénérez votre projet.</span><span class="sxs-lookup"><span data-stu-id="86d5f-224">Rebuild your project.</span></span>

##### <a name="test-push-notifications-in-your-ios-app"></a><span data-ttu-id="86d5f-225">Tester les notifications Push dans votre application iOS</span><span class="sxs-lookup"><span data-stu-id="86d5f-225">Test push notifications in your iOS app</span></span>
1. <span data-ttu-id="86d5f-226">Dans Visual Studio, assurez-vous que **iOS** est sélectionné comme cible de déploiement hello, puis choisissez **périphérique** toorun sur votre appareil iOS connecté.</span><span class="sxs-lookup"><span data-stu-id="86d5f-226">In Visual Studio, make sure that **iOS** is selected as hello deployment target, and then choose **Device** toorun on your connected iOS device.</span></span>

    <span data-ttu-id="86d5f-227">Vous pouvez exécuter sur un tooyour de périphérique connecté iOS PC à l’aide d’iTunes.</span><span class="sxs-lookup"><span data-stu-id="86d5f-227">You can run on an iOS device connected tooyour PC using iTunes.</span></span> <span data-ttu-id="86d5f-228">Hello, iOS Simulator ne prend pas en charge des notifications push.</span><span class="sxs-lookup"><span data-stu-id="86d5f-228">hello iOS Simulator does not support push notifications.</span></span>

2. <span data-ttu-id="86d5f-229">Hello de presse **exécuter** bouton ou **F5** dans Visual Studio toobuild projet de hello début hello application dans un appareil iOS, puis cliquez sur **OK** tooaccept les notifications push.</span><span class="sxs-lookup"><span data-stu-id="86d5f-229">Press hello **Run** button or **F5** in Visual Studio toobuild hello project and start hello app in an iOS  device, then click **OK** tooaccept push notifications.</span></span>

   > [!NOTE]
   > <span data-ttu-id="86d5f-230">application Hello demande confirmation pour les notifications push pendant hello première exécution.</span><span class="sxs-lookup"><span data-stu-id="86d5f-230">hello app requests confirmation for push notifications during hello first run.</span></span>

3. <span data-ttu-id="86d5f-231">Dans l’application hello, une tâche, puis tapez hello plus (+) icône.</span><span class="sxs-lookup"><span data-stu-id="86d5f-231">In hello app, type a task, and then click hello plus (+) icon.</span></span>
4. <span data-ttu-id="86d5f-232">Vérifiez qu’une notification est reçue, puis cliquez sur OK toodismiss hello notification.</span><span class="sxs-lookup"><span data-stu-id="86d5f-232">Verify that a notification is received, then click OK toodismiss hello notification.</span></span>

## <a name="optional-configure-and-run-on-windows"></a><span data-ttu-id="86d5f-233">(Facultatif) Configurer et exécuter sur Windows</span><span class="sxs-lookup"><span data-stu-id="86d5f-233">(Optional) Configure and run on Windows</span></span>
<span data-ttu-id="86d5f-234">Cette section est pour l’exécution du projet d’application hello Apache Cordova sur les appareils Windows 10 (plug-in de hello PhoneGap push est pris en charge sur Windows 10).</span><span class="sxs-lookup"><span data-stu-id="86d5f-234">This section is for running hello Apache Cordova app project on Windows 10 devices (hello PhoneGap push plugin is supported on Windows 10).</span></span> <span data-ttu-id="86d5f-235">Vous pouvez ignorer cette section si vous n'utilisez pas d'appareils Windows.</span><span class="sxs-lookup"><span data-stu-id="86d5f-235">If you are not working with Windows devices, you can skip this section.</span></span>

#### <a name="register-your-windows-app-for-push-notifications-with-wns"></a><span data-ttu-id="86d5f-236">Inscrire votre application Windows pour les notifications Push avec WNS</span><span class="sxs-lookup"><span data-stu-id="86d5f-236">Register your Windows app for push notifications with WNS</span></span>
<span data-ttu-id="86d5f-237">options du magasin toouse hello dans Visual Studio, sélectionnez une cible de Windows à partir de la liste des plateformes de Solution hello, tel que **Windows-x64** ou **Windows-x86** (éviter **Windows-AnyCPU** pour les notifications push).</span><span class="sxs-lookup"><span data-stu-id="86d5f-237">toouse hello Store options in Visual Studio, select a Windows target from hello Solution Platforms list, like **Windows-x64** or **Windows-x86** (avoid **Windows-AnyCPU** for push notifications).</span></span>

[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

<span data-ttu-id="86d5f-238">[Regarder une vidéo montrant des étapes similaires][13]</span><span class="sxs-lookup"><span data-stu-id="86d5f-238">[Watch a video showing similar steps][13]</span></span>

#### <a name="configure-hello-notification-hub-for-wns"></a><span data-ttu-id="86d5f-239">Configuration d’un concentrateur de notification hello pour WNS</span><span class="sxs-lookup"><span data-stu-id="86d5f-239">Configure hello notification hub for WNS</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="configure-your-cordova-app-toosupport-windows-push-notifications"></a><span data-ttu-id="86d5f-240">Configurer votre application Cordova toosupport Windows push notifications</span><span class="sxs-lookup"><span data-stu-id="86d5f-240">Configure your Cordova app toosupport Windows push notifications</span></span>
<span data-ttu-id="86d5f-241">Concepteur de configuration Open hello (avec le bouton droit sur le fichier config.xml et sélectionnez **Concepteur de vue**), sélectionnez hello **Windows** onglet, puis choisissez **Windows 10** sous **Windows ciblent la Version**.</span><span class="sxs-lookup"><span data-stu-id="86d5f-241">Open hello configuration designer (right-click on config.xml and select **View Designer**), select hello **Windows** tab, and choose **Windows 10** under **Windows Target Version**.</span></span>

<span data-ttu-id="86d5f-242">toosupport des notifications de push de la valeur par défaut (debug) génère, ouvrez build.json fichier.</span><span class="sxs-lookup"><span data-stu-id="86d5f-242">toosupport push notifications in your default (debug) builds, open build.json file.</span></span> <span data-ttu-id="86d5f-243">Copier la configuration de débogage de tooyour de configuration « release ».</span><span class="sxs-lookup"><span data-stu-id="86d5f-243">Copy the "release" configuration tooyour debug configuration.</span></span>

        "windows": {
            "release": {
                "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
                "publisherId": "CN=yourpublisherID"
            }
        }

<span data-ttu-id="86d5f-244">Après la mise à jour de hello, hello build.json doit contenir hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="86d5f-244">After hello update, hello build.json should contain hello following code:</span></span>

    "windows": {
        "release": {
            "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
            "publisherId": "CN=yourpublisherID"
            },
        "debug": {
            "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
            "publisherId": "CN=yourpublisherID"
            }
        }

<span data-ttu-id="86d5f-245">Générez l’application hello et vérifiez que vous ne disposez d’aucune erreur.</span><span class="sxs-lookup"><span data-stu-id="86d5f-245">Build hello app and verify that you have no errors.</span></span> <span data-ttu-id="86d5f-246">Votre application cliente doit désormais s’inscrire aux notifications de hello à partir de la principal de l’application Mobile hello.</span><span class="sxs-lookup"><span data-stu-id="86d5f-246">Your client app should now register for hello notifications from hello Mobile App backend.</span></span> <span data-ttu-id="86d5f-247">Répétez cette section pour chaque projet Windows dans votre solution.</span><span class="sxs-lookup"><span data-stu-id="86d5f-247">Repeat this section for every Windows project in your solution.</span></span>

#### <a name="test-push-notifications-in-your-windows-app"></a><span data-ttu-id="86d5f-248">Tester les notifications Push dans votre application Windows</span><span class="sxs-lookup"><span data-stu-id="86d5f-248">Test push notifications in your Windows app</span></span>
<span data-ttu-id="86d5f-249">Dans Visual Studio, assurez-vous qu’une plateforme Windows est sélectionnée comme cible de déploiement hello, tel que **Windows-x64** ou **Windows-x86**.</span><span class="sxs-lookup"><span data-stu-id="86d5f-249">In Visual Studio, make sure that a Windows platform is selected as hello deployment target, such as **Windows-x64** or **Windows-x86**.</span></span> <span data-ttu-id="86d5f-250">application de hello toorun sur un PC Windows 10 qui héberge Visual Studio, choisissez **ordinateur Local**.</span><span class="sxs-lookup"><span data-stu-id="86d5f-250">toorun hello app on a Windows 10 PC hosting Visual Studio, choose **Local Machine**.</span></span>

<span data-ttu-id="86d5f-251">Hello de presse exécuter bouton toobuild hello projet et démarrer l’application hello.</span><span class="sxs-lookup"><span data-stu-id="86d5f-251">Press hello Run button toobuild hello project and start hello app.</span></span>

<span data-ttu-id="86d5f-252">Dans l’application hello, tapez un nom pour un nouveau todoitem, puis cliquez sur hello plus (+) icône tooadd il.</span><span class="sxs-lookup"><span data-stu-id="86d5f-252">In hello app, type a name for a new todoitem, and then click hello plus (+) icon tooadd it.</span></span>

<span data-ttu-id="86d5f-253">Vérifiez qu’une notification est reçue lors de l’élément de hello est ajouté.</span><span class="sxs-lookup"><span data-stu-id="86d5f-253">Verify that a notification is received when hello item is added.</span></span>

## <span data-ttu-id="86d5f-254"><a name="next-steps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="86d5f-254"><a name="next-steps"></a>Next Steps</span></span>
* <span data-ttu-id="86d5f-255">En savoir plus sur [concentrateurs de Notification] [ 17] toolearn à propos des notifications push.</span><span class="sxs-lookup"><span data-stu-id="86d5f-255">Read about [Notification Hubs][17] toolearn about push notifications.</span></span>
* <span data-ttu-id="86d5f-256">Si vous ne le n'avez pas déjà fait, continuer le didacticiel hello par [Ajout de l’authentification] [ 14] tooyour Apache Cordova application.</span><span class="sxs-lookup"><span data-stu-id="86d5f-256">If you have not already done so, continue hello tutorial by [Adding Authentication][14] tooyour Apache Cordova app.</span></span>

<span data-ttu-id="86d5f-257">Découvrez comment toouse hello kits de développement logiciel.</span><span class="sxs-lookup"><span data-stu-id="86d5f-257">Learn how toouse hello SDKs.</span></span>

* <span data-ttu-id="86d5f-258">[Kit de développement logiciel (SDK) Apache Cordova][15]</span><span class="sxs-lookup"><span data-stu-id="86d5f-258">[Apache Cordova SDK][15]</span></span>
* <span data-ttu-id="86d5f-259">[Kit de développement logiciel du serveur ASP.NET][1]</span><span class="sxs-lookup"><span data-stu-id="86d5f-259">[ASP.NET Server SDK][1]</span></span>
* <span data-ttu-id="86d5f-260">[Kit de développement logiciel du serveur Node.js][16]</span><span class="sxs-lookup"><span data-stu-id="86d5f-260">[Node.js Server SDK][16]</span></span>

<!-- Images -->
[img1]: ./media/app-service-mobile-cordova-get-started-push/add-push-plugin.png

<!-- URLs -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: http://www.visualstudio.com/
[3]: https://azure.microsoft.com/pricing/free-trial/
[4]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[5]: app-service-mobile-cordova-get-started.md
[6]: http://go.microsoft.com/fwlink/p/?LinkId=268302
[7]: https://developer.apple.com/programs/
[8]: https://developer.microsoft.com/en-us/store/register
[9]: https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-3-Create-azure-notification-hub
[10]: https://www.npmjs.com/
[11]: https://taco.visualstudio.com/en-us/docs/run-app-apache/#HAXM
[12]: http://taco.visualstudio.com/en-us/docs/ios-guide/
[13]: https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-6-Set-up-wns-for-push
[14]: app-service-mobile-cordova-get-started-users.md
[15]: app-service-mobile-cordova-how-to-use-client-library.md
[16]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[17]: ../notification-hubs/notification-hubs-push-notification-overview.md
[18]: https://console.developers.google.com/home/dashboard
[19]: https://github.com/phonegap/phonegap-plugin-push/blob/master/docs/INSTALLATION.md
[20]: https://www.mobizen.com/
[21]: http://taco.visualstudio.com/en-us/docs/build_ios_cloud/
