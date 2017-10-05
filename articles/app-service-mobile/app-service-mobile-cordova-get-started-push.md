---
title: "Ajouter des notifications Push à l’application Apache Cordova à l’aide d’Azure Mobile Apps | Microsoft Docs"
description: "Découvrez comment utiliser Azure Mobile Apps pour envoyer des notifications Push à votre application Apache Cordova."
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
ms.openlocfilehash: dc3cab0a6a8b4a56ab0fba1a02e5bba9d0ed1b1f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-apache-cordova-app"></a><span data-ttu-id="772e2-103">Ajout de notifications Push à votre application Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="772e2-103">Add push notifications to your Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="772e2-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="772e2-104">Overview</span></span>
<span data-ttu-id="772e2-105">Dans ce didacticiel, vous ajoutez des notifications Push au projet [Démarrage rapide Apache Cordova] afin qu'une notification Push soit envoyée chaque fois qu'un enregistrement est inséré.</span><span class="sxs-lookup"><span data-stu-id="772e2-105">In this tutorial, you add push notifications to the [Apache Cordova quick start] project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="772e2-106">Si vous n’utilisez pas le projet de serveur du démarrage rapide téléchargé, vous devrez ajouter le package d’extension de notification Push.</span><span class="sxs-lookup"><span data-stu-id="772e2-106">If you do not use the downloaded quick start server project, you need the push notification extension package.</span></span> <span data-ttu-id="772e2-107">Consultez [Fonctionnement avec le Kit de développement logiciel (SDK) du serveur principal .NET pour Azure Mobile Apps][1] pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="772e2-107">For more information, see [Work with the .NET backend server SDK for Azure Mobile Apps][1].</span></span>

## <span data-ttu-id="772e2-108"><a name="prerequisites"></a>Configuration requise</span><span class="sxs-lookup"><span data-stu-id="772e2-108"><a name="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="772e2-109">Ce didacticiel est dédié aux applications Apache Cordova développées dans Visual Studio 2015 et s’exécutant sur l’Émulateur Google Android, un appareil Android, Windows ou iOS.</span><span class="sxs-lookup"><span data-stu-id="772e2-109">This tutorial covers an Apache Cordova application developed with Visual Studio 2015 that runs on the Google Android Emulator, an Android device, a Windows device, and an iOS device.</span></span>

<span data-ttu-id="772e2-110">Pour suivre ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="772e2-110">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="772e2-111">Un PC avec [Visual Studio Community 2015][2] ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="772e2-111">A PC with [Visual Studio Community 2015][2] or later versions.</span></span>
* <span data-ttu-id="772e2-112">[Visual Studio Tools pour Apache Cordova][4].</span><span class="sxs-lookup"><span data-stu-id="772e2-112">[Visual Studio Tools for Apache Cordova][4].</span></span>
* <span data-ttu-id="772e2-113">Un [compte Azure actif][3].</span><span class="sxs-lookup"><span data-stu-id="772e2-113">An [active Azure account][3].</span></span>
* <span data-ttu-id="772e2-114">Un projet [Démarrage rapide Apache Cordova][5] .</span><span class="sxs-lookup"><span data-stu-id="772e2-114">A completed [Apache Cordova quick start][5] project.</span></span>
* <span data-ttu-id="772e2-115">Un [compte Google][6] avec une adresse électronique vérifiée.</span><span class="sxs-lookup"><span data-stu-id="772e2-115">(Android) A [Google account][6] with a verified email address.</span></span>
* <span data-ttu-id="772e2-116">(iOS) Un [abonnement au programme pour développeurs Apple][7] et un appareil iOS (le simulateur iOS ne prend pas en charge les notifications Push).</span><span class="sxs-lookup"><span data-stu-id="772e2-116">(iOS) An [Apple Developer Program membership][7] and an iOS device (iOS Simulator does not support push).</span></span>
* <span data-ttu-id="772e2-117">(Windows) Un [compte de développeur Windows Store][8] et un appareil Windows 10.</span><span class="sxs-lookup"><span data-stu-id="772e2-117">(Windows) A [Windows Store Developer Account][8] and a Windows 10 device.</span></span>

## <span data-ttu-id="772e2-118"><a name="configure-hub"></a>Configurer un hub de notification</span><span class="sxs-lookup"><span data-stu-id="772e2-118"><a name="configure-hub"></a>Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

<span data-ttu-id="772e2-119">[Regarder une vidéo illustrant les étapes de cette section][9]</span><span class="sxs-lookup"><span data-stu-id="772e2-119">[Watch a video showing steps in this section][9]</span></span>

## <a name="update-the-server-project"></a><span data-ttu-id="772e2-120">Mettre à jour le projet de serveur</span><span class="sxs-lookup"><span data-stu-id="772e2-120">Update the server project</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <span data-ttu-id="772e2-121"><a name="add-push-to-app"></a>Modification de votre application Cordova</span><span class="sxs-lookup"><span data-stu-id="772e2-121"><a name="add-push-to-app"></a>Modify your Cordova app</span></span>
<span data-ttu-id="772e2-122">Vérifiez que votre projet d’application Apache Cordova est prêt à gérer les notifications push en installant le plug-in de notification push Cordova ainsi que tous les services spécifiques à la plateforme push.</span><span class="sxs-lookup"><span data-stu-id="772e2-122">Ensure your Apache Cordova app project is ready to handle push notifications by installing the Cordova push plugin plus any platform-specific push services.</span></span>

#### <a name="update-the-cordova-version-in-your-project"></a><span data-ttu-id="772e2-123">Mise à jour de la version de Cordova dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="772e2-123">Update the Cordova version in your project.</span></span>
<span data-ttu-id="772e2-124">Si votre projet utilise une version d’Apache Cordova antérieure à la v6.1.1, mettez à jour le projet client.</span><span class="sxs-lookup"><span data-stu-id="772e2-124">If your project uses a version of Apache Cordova earlier than v6.1.1, update the client project.</span></span> <span data-ttu-id="772e2-125">Pour mettre à jour le projet :</span><span class="sxs-lookup"><span data-stu-id="772e2-125">To update the project:</span></span>

* <span data-ttu-id="772e2-126">Faites un clic droit sur `config.xml` pour ouvrir le concepteur de configuration.</span><span class="sxs-lookup"><span data-stu-id="772e2-126">Right-click `config.xml` to open the configuration designer.</span></span>
* <span data-ttu-id="772e2-127">Sélectionnez l’onglet PLATEFORMES.</span><span class="sxs-lookup"><span data-stu-id="772e2-127">Select the Platforms tab.</span></span>
* <span data-ttu-id="772e2-128">Choisissez 6.1.1 dans la zone de texte **Cordova CLI**.</span><span class="sxs-lookup"><span data-stu-id="772e2-128">Choose 6.1.1 in the **Cordova CLI** text box.</span></span>
* <span data-ttu-id="772e2-129">Cliquez sur **Générer**, puis sur **Générer la solution** pour mettre à jour le projet.</span><span class="sxs-lookup"><span data-stu-id="772e2-129">Choose **Build**, then **Build Solution** to update the project.</span></span>

#### <a name="install-the-push-plugin"></a><span data-ttu-id="772e2-130">Installation du plug-in Push</span><span class="sxs-lookup"><span data-stu-id="772e2-130">Install the push plugin</span></span>
<span data-ttu-id="772e2-131">En mode natif, les applications Apache Cordova ne gèrent pas les fonctionnalités de réseau ou d’appareils.</span><span class="sxs-lookup"><span data-stu-id="772e2-131">Apache Cordova applications do not natively handle device or network capabilities.</span></span>  <span data-ttu-id="772e2-132">Ces fonctionnalités sont fournies par des plug-ins publiés sur [npm][10] ou sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="772e2-132">These capabilities are provided by plugins that are published either on [npm][10] or on GitHub.</span></span>  <span data-ttu-id="772e2-133">Le plug-in `phonegap-plugin-push` est utilisé pour gérer les notifications Push du réseau.</span><span class="sxs-lookup"><span data-stu-id="772e2-133">The `phonegap-plugin-push` plugin is used to handle network push notifications.</span></span>

<span data-ttu-id="772e2-134">Vous pouvez installer le plug-in de notification Push de l’une des façons suivantes :</span><span class="sxs-lookup"><span data-stu-id="772e2-134">You can install the push plugin in one of these ways:</span></span>

<span data-ttu-id="772e2-135">**À partir de l'invite de commandes :**</span><span class="sxs-lookup"><span data-stu-id="772e2-135">**From the command-prompt:**</span></span>

<span data-ttu-id="772e2-136">Exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="772e2-136">Execute the following command:</span></span>

    cordova plugin add phonegap-plugin-push

<span data-ttu-id="772e2-137">**À partir de Visual Studio :**</span><span class="sxs-lookup"><span data-stu-id="772e2-137">**From within Visual Studio:**</span></span>

1. <span data-ttu-id="772e2-138">Dans l’Explorateur de solutions, ouvrez le fichier `config.xml`, cliquez sur **Plug-ins** > **Personnalisé**, sélectionnez **Git** comme source d’installation, puis entrez `https://github.com/phonegap/phonegap-plugin-push` en tant que source.</span><span class="sxs-lookup"><span data-stu-id="772e2-138">In Solution Explorer, open the `config.xml` file click **Plugins** > **Custom**, select **Git** as the  installation source, then enter `https://github.com/phonegap/phonegap-plugin-push` as the source.</span></span>

   ![][img1]

2. <span data-ttu-id="772e2-139">Cliquez sur la flèche en regard de la source d’installation.</span><span class="sxs-lookup"><span data-stu-id="772e2-139">Click the arrow next to the installation source.</span></span>
3. <span data-ttu-id="772e2-140">Si vous avez déjà un ID de projet numérique pour le projet de Console de développement Google, ajoutez-le dans **SENDER_ID**.</span><span class="sxs-lookup"><span data-stu-id="772e2-140">In **SENDER_ID**, if you already have a numeric project ID for the Google Developer Console project, you can add it here.</span></span> <span data-ttu-id="772e2-141">Entrez temporairement une valeur d’espace réservé, par exemple, 777777.</span><span class="sxs-lookup"><span data-stu-id="772e2-141">Otherwise, enter a placeholder value, like 777777.</span></span>  <span data-ttu-id="772e2-142">Si vous ciblez Android, vous pourrez modifier cette valeur dans le fichier config.xml ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="772e2-142">If you are targeting Android, you can update this value in config.xml later.</span></span>
4. <span data-ttu-id="772e2-143">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="772e2-143">Click **Add**.</span></span>

<span data-ttu-id="772e2-144">Le plug-in de notification Push est maintenant installé.</span><span class="sxs-lookup"><span data-stu-id="772e2-144">The push plugin is now installed.</span></span>

#### <a name="install-the-device-plugin"></a><span data-ttu-id="772e2-145">Installation du plug-in Appareil</span><span class="sxs-lookup"><span data-stu-id="772e2-145">Install the device plugin</span></span>
<span data-ttu-id="772e2-146">Suivez la même procédure que celle utilisée pour installer le plug-in de notification Push.</span><span class="sxs-lookup"><span data-stu-id="772e2-146">Follow the same procedure you used to install the push plugin.</span></span>  <span data-ttu-id="772e2-147">Ajoutez le plug-in d’appareil dans la liste principale des plug-ins (cliquez sur **Plug-ins** > **Principale** pour la trouver).</span><span class="sxs-lookup"><span data-stu-id="772e2-147">Add the Device plugin from the Core plugins list (click **Plugins** > **Core** to find it).</span></span> <span data-ttu-id="772e2-148">Vous avez besoin de ce plug-in pour obtenir le nom de la plateforme.</span><span class="sxs-lookup"><span data-stu-id="772e2-148">You need this plugin to obtain the platform name.</span></span>

#### <a name="register-your-device-on-application-start-up"></a><span data-ttu-id="772e2-149">Inscription de votre appareil au démarrage de l’application</span><span class="sxs-lookup"><span data-stu-id="772e2-149">Register your device on application start-up</span></span>
<span data-ttu-id="772e2-150">Initialement, nous proposons un code minimal pour Android.</span><span class="sxs-lookup"><span data-stu-id="772e2-150">Initially, we include some minimal code for Android.</span></span> <span data-ttu-id="772e2-151">Plus tard, modifiez l’application pour qu’elle s’exécute sur iOS ou Windows 10.</span><span class="sxs-lookup"><span data-stu-id="772e2-151">Later, modify the app to run on iOS or Windows 10.</span></span>

1. <span data-ttu-id="772e2-152">Ajoutez un appel à **registerForPushNotifications** durant le rappel du processus de connexion, ou en bas de la méthode **onDeviceReady** :</span><span class="sxs-lookup"><span data-stu-id="772e2-152">Add a call to **registerForPushNotifications** during the callback for the login process, or at the bottom of  the **onDeviceReady** method:</span></span>

        // Login to the service.
        client.login('google')
            .then(function () {
                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh the todoItems
                refreshDisplay();

                // Wire up the UI Event Handler for the Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                    // Added to register for push notifications.
                registerForPushNotifications();

            }, handleError);

    <span data-ttu-id="772e2-153">Cet exemple montre l’appel de **registerForPushNotifications** après une authentification réussie.</span><span class="sxs-lookup"><span data-stu-id="772e2-153">This example shows calling **registerForPushNotifications** after authentication succeeds.</span></span>  <span data-ttu-id="772e2-154">Vous pouvez appeler `registerForPushNotifications()` aussi souvent que nécessaire.</span><span class="sxs-lookup"><span data-stu-id="772e2-154">You can call `registerForPushNotifications()` as often as is required.</span></span>

2. <span data-ttu-id="772e2-155">Ajoutez la nouvelle méthode **registerForPushNotifications** comme suit :</span><span class="sxs-lookup"><span data-stu-id="772e2-155">Add the new **registerForPushNotifications** method as follows:</span></span>

        // Register for Push Notifications. Requires that phonegap-plugin-push be installed.
        var pushRegistration = null;
        function registerForPushNotifications() {
          pushRegistration = PushNotification.init({
              android: { senderID: 'Your_Project_ID' },
              ios: { alert: 'true', badge: 'true', sound: 'true' },
              wns: {}
          });

        // Handle the registration event.
        pushRegistration.on('registration', function (data) {
          // Get the native platform of the device.
          var platform = device.platform;
          // Get the handle returned during registration.
          var handle = data.registrationId;
          // Set the device-specific message template.
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
3. <span data-ttu-id="772e2-156">(Android) Dans le code précédent, remplacez `Your_Project_ID` par l’ID de projet numérique associé à votre application dans la [Console de développement Google][18].</span><span class="sxs-lookup"><span data-stu-id="772e2-156">(Android) In the preceding code, replace `Your_Project_ID` with the numeric project ID for your app from the  [Google Developer Console][18].</span></span>

## <a name="optional-configure-and-run-the-app-on-android"></a><span data-ttu-id="772e2-157">(Facultatif) Configurer et exécuter l’application sur Android</span><span class="sxs-lookup"><span data-stu-id="772e2-157">(Optional) Configure and run the app on Android</span></span>
<span data-ttu-id="772e2-158">Terminez cette section pour activer les notifications Push pour Android.</span><span class="sxs-lookup"><span data-stu-id="772e2-158">Complete this section to enable push notifications for Android.</span></span>

#### <span data-ttu-id="772e2-159"><a name="enable-gcm"></a>Activation de Firebase Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="772e2-159"><a name="enable-gcm"></a>Enable Firebase Cloud Messaging</span></span>
<span data-ttu-id="772e2-160">Dans la mesure où nous ciblons la plateforme Google Android en premier lieu, vous devez activer Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="772e2-160">Since we are targeting the Google Android platform initially, you must enable Firebase Cloud Messaging.</span></span>

[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

#### <span data-ttu-id="772e2-161"><a name="configure-backend"></a>Configurer le serveur principal d’applications mobiles pour l’envoi de demandes de notifications Push à l’aide de FCM</span><span class="sxs-lookup"><span data-stu-id="772e2-161"><a name="configure-backend"></a>Configure the Mobile App backend to send push requests using FCM</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

#### <a name="configure-your-cordova-app-for-android"></a><span data-ttu-id="772e2-162">Configuration de votre application Cordova pour Android</span><span class="sxs-lookup"><span data-stu-id="772e2-162">Configure your Cordova app for Android</span></span>
<span data-ttu-id="772e2-163">Dans votre application Cordova, ouvrez le fichier config.xml et remplacez `Your_Project_ID` par l’ID de projet numérique associé à votre application dans la [Console de développement Google][18].</span><span class="sxs-lookup"><span data-stu-id="772e2-163">In your Cordova app, open config.xml and replace `Your_Project_ID` with the numeric project ID for your app from the [Google Developer Console][18].</span></span>

        <plugin name="phonegap-plugin-push" version="1.7.1" src="https://github.com/phonegap/phonegap-plugin-push.git">
            <variable name="SENDER_ID" value="Your_Project_ID" />
        </plugin>

<span data-ttu-id="772e2-164">Ouvrez le fichier index.js et mettez à jour le code pour utiliser votre ID de projet numérique.</span><span class="sxs-lookup"><span data-stu-id="772e2-164">Open index.js and update the code to use your numeric project ID.</span></span>

        pushRegistration = PushNotification.init({
            android: { senderID: 'Your_Project_ID' },
            ios: { alert: 'true', badge: 'true', sound: 'true' },
            wns: {}
        });

#### <span data-ttu-id="772e2-165"><a name="configure-device"></a>Configuration de votre appareil Android pour le débogage USB</span><span class="sxs-lookup"><span data-stu-id="772e2-165"><a name="configure-device"></a>Configure your Android device for USB debugging</span></span>
<span data-ttu-id="772e2-166">Pour pouvoir déployer votre application sur votre appareil Android, vous devez activer le débogage USB.</span><span class="sxs-lookup"><span data-stu-id="772e2-166">Before you can deploy your application to your Android Device, you need to enable USB Debugging.</span></span>  <span data-ttu-id="772e2-167">Sur votre téléphone Android, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="772e2-167">Perform the following steps on your Android phone:</span></span>

1. <span data-ttu-id="772e2-168">Accédez à **Paramètres** >**À propos du téléphone**, puis cliquez sur **Numéro de build** jusqu’à ce que le mode développeur soit activé (environ sept fois).</span><span class="sxs-lookup"><span data-stu-id="772e2-168">Go to **Settings** > **About phone**, then tap the **Build number** until developer mode is enabled  (about seven times).</span></span>
2. <span data-ttu-id="772e2-169">De retour dans **Paramètres** > **Options développeurs**, activez **Débogage USB**, puis connectez votre téléphone Android à votre PC de développement à l’aide d’un câble USB.</span><span class="sxs-lookup"><span data-stu-id="772e2-169">Back in **Settings** > **Developer Options** enable **USB debugging**, then connect your Android phone  to your development PC with a USB Cable.</span></span>

<span data-ttu-id="772e2-170">Nous avons testé cette procédure à l’aide d’un appareil Google Nexus 5 X exécutant Android 6.0 (Marshmallow).</span><span class="sxs-lookup"><span data-stu-id="772e2-170">We tested this using a Google Nexus 5X device running Android 6.0 (Marshmallow).</span></span>  <span data-ttu-id="772e2-171">Toutefois, les techniques sont communes à l’ensemble des versions Android modernes.</span><span class="sxs-lookup"><span data-stu-id="772e2-171">However, the techniques are common across any modern Android release.</span></span>

#### <a name="install-google-play-services"></a><span data-ttu-id="772e2-172">Installation des services Google Play</span><span class="sxs-lookup"><span data-stu-id="772e2-172">Install Google Play Services</span></span>
<span data-ttu-id="772e2-173">Le plug-in Push sollicite les services Google Play pour les notifications Push.</span><span class="sxs-lookup"><span data-stu-id="772e2-173">The push plugin relies on Android Google Play Services for push notifications.</span></span>

1. <span data-ttu-id="772e2-174">Dans Visual Studio, cliquez sur **Outils** > **Android** > **Gestionnaire du Kit de développement logiciel (SDK) Android**, développez le dossier **Extras**, puis cochez la case correspondante pour vous assurer que chacun des Kits de développement logiciel suivants est installé.</span><span class="sxs-lookup"><span data-stu-id="772e2-174">In Visual Studio, click **Tools** > **Android** > **Android SDK Manager**, expand the **Extras** folder and  check the box to make sure that each of the following SDKs is installed.</span></span>

   * <span data-ttu-id="772e2-175">Android 2.3 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="772e2-175">Android 2.3 or higher</span></span>
   * <span data-ttu-id="772e2-176">Révision du référentiel Google 27 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="772e2-176">Google Repository revision 27 or higher</span></span>
   * <span data-ttu-id="772e2-177">Google Play Services 9.0.2 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="772e2-177">Google Play Services 9.0.2 or higher</span></span>

2. <span data-ttu-id="772e2-178">Cliquez sur **Packages d’installation** et attendez que l’installation se termine.</span><span class="sxs-lookup"><span data-stu-id="772e2-178">Click **Install Packages** and wait for the installation to complete.</span></span>

<span data-ttu-id="772e2-179">Les bibliothèques actuellement requises figurent dans la [documentation d’installation phonegap-plugin-push][19].</span><span class="sxs-lookup"><span data-stu-id="772e2-179">The current required libraries are listed in the [phonegap-plugin-push installation documentation][19].</span></span>

#### <a name="test-push-notifications-in-the-app-on-android"></a><span data-ttu-id="772e2-180">Test des notifications Push dans l’application sur Android</span><span class="sxs-lookup"><span data-stu-id="772e2-180">Test push notifications in the app on Android</span></span>
<span data-ttu-id="772e2-181">Vous pouvez désormais tester les notifications Push en exécutant l’application et en insérant des éléments dans la table TodoItem.</span><span class="sxs-lookup"><span data-stu-id="772e2-181">You can now test push notifications by running the app and inserting items in the TodoItem table.</span></span> <span data-ttu-id="772e2-182">Vous pouvez tester à partir du même appareil ou à partir d’un deuxième appareil, à condition d’utiliser le même serveur principal.</span><span class="sxs-lookup"><span data-stu-id="772e2-182">You can test from the same device or from a second device, as long as you are using the same backend.</span></span> <span data-ttu-id="772e2-183">Testez votre application Cordova sur la plateforme Android de l’une des manières suivantes :</span><span class="sxs-lookup"><span data-stu-id="772e2-183">Test your Cordova app on the Android platform in one of the following ways:</span></span>

* <span data-ttu-id="772e2-184">**Sur un appareil physique :** connectez votre appareil Android à votre ordinateur de développement avec un câble USB.</span><span class="sxs-lookup"><span data-stu-id="772e2-184">**On a physical device:** Attach your Android device to your development computer with a USB cable.</span></span>  <span data-ttu-id="772e2-185">Au lieu de **l’Émulateur Google Android**, sélectionnez **Appareil**.</span><span class="sxs-lookup"><span data-stu-id="772e2-185">Instead of **Google Android Emulator**, select **Device**.</span></span> <span data-ttu-id="772e2-186">Visual Studio déploie l’application sur l’appareil, puis l’exécute.</span><span class="sxs-lookup"><span data-stu-id="772e2-186">Visual Studio deploys the application to the device and then runs the application.</span></span>  <span data-ttu-id="772e2-187">Vous pouvez alors interagir avec l’application sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="772e2-187">You can then interact with the application on the device.</span></span>

  <span data-ttu-id="772e2-188">Améliorez votre expérience du développement.</span><span class="sxs-lookup"><span data-stu-id="772e2-188">Improve your development experience.</span></span>  <span data-ttu-id="772e2-189">Les applications de partage d’écran telles que [Mobizen] [20] peuvent vous aider à développer une application Android.</span><span class="sxs-lookup"><span data-stu-id="772e2-189">Screen sharing applications such as [Mobizen][20] can assist you in developing an Android application.</span></span>  <span data-ttu-id="772e2-190">Mobizen projette votre écran Android sur un navigateur web de votre PC.</span><span class="sxs-lookup"><span data-stu-id="772e2-190">Mobizen projects your Android screen to a web browser on your PC.</span></span>

* <span data-ttu-id="772e2-191">**Sur un émulateur Android :** des étapes de configuration supplémentaires sont requises lors de l’exécution sur un émulateur.</span><span class="sxs-lookup"><span data-stu-id="772e2-191">**On an Android emulator:** There are additional configuration steps required when running on an emulator.</span></span>

    <span data-ttu-id="772e2-192">Assurez-vous de procéder au déploiement sur un périphérique virtuel sur lequel les API Google sont définis comme cible, comme indiqué dans le Gestionnaire d’appareil virtuel Android (AVD).</span><span class="sxs-lookup"><span data-stu-id="772e2-192">Make sure you are deploying to a virtual device that has Google APIs set as the target, as shown in the Android Virtual Device (AVD) manager.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/google-apis-avd-settings.png)

    <span data-ttu-id="772e2-193">Si vous souhaitez utiliser un émulateur x86 plus rapide, [installez le pilote HAXM][11] et configurez l’émulateur pour l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="772e2-193">If you want to use a faster x86 emulator, you [install the HAXM driver][11] and configure the emulator to use it.</span></span>

    <span data-ttu-id="772e2-194">Ajouter un compte Google à l’appareil Android en cliquant sur **Applications** > **Paramètres** > **Ajouter un compte**, puis suivez les invites.</span><span class="sxs-lookup"><span data-stu-id="772e2-194">Add a Google account to the Android device by clicking **Apps** > **Settings** > **Add account**, then follow the prompts.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/add-google-account.png)

    <span data-ttu-id="772e2-195">Exécutez normalement l’application todolist et insérez un nouvel élément todo.</span><span class="sxs-lookup"><span data-stu-id="772e2-195">Run the todolist app as before and insert a new todo item.</span></span> <span data-ttu-id="772e2-196">Cette fois, une icône de notification s’affiche dans la zone de notification.</span><span class="sxs-lookup"><span data-stu-id="772e2-196">This time, a notification icon is displayed in the notification area.</span></span> <span data-ttu-id="772e2-197">Vous pouvez ouvrir le tiroir de notification pour afficher le texte intégral de la notification.</span><span class="sxs-lookup"><span data-stu-id="772e2-197">You can open the notification drawer to view the full text of the notification.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/android-notifications.png)

## <a name="optional-configure-and-run-on-ios"></a><span data-ttu-id="772e2-198">(Facultatif) Configurer et exécuter sur iOS</span><span class="sxs-lookup"><span data-stu-id="772e2-198">(Optional) Configure and run on iOS</span></span>
<span data-ttu-id="772e2-199">Cette section est dédiée à l’exécution du projet Cordova sur les appareils iOS.</span><span class="sxs-lookup"><span data-stu-id="772e2-199">This section is for running the Cordova project on iOS devices.</span></span> <span data-ttu-id="772e2-200">Vous pouvez ignorer cette section si vous n'utilisez pas d'appareils iOS.</span><span class="sxs-lookup"><span data-stu-id="772e2-200">If you are not working with iOS devices, you can skip this section.</span></span>

#### <a name="install-and-run-the-ios-remote-build-agent-on-a-mac-or-cloud-service"></a><span data-ttu-id="772e2-201">Installer et exécuter l’agent remote build iOS sur un Mac ou un service cloud</span><span class="sxs-lookup"><span data-stu-id="772e2-201">Install and run the iOS remote build agent on a Mac or cloud service</span></span>
<span data-ttu-id="772e2-202">Avant de pouvoir exécuter une application Cordova sur iOS à l’aide de Visual Studio, suivez les étapes décrites dans le [Guide d’installation iOS][12] pour installer et exécuter l’agent remote build.</span><span class="sxs-lookup"><span data-stu-id="772e2-202">Before you can run a Cordova app on iOS using Visual Studio, go through the steps in the [iOS Setup Guide][12] to install and run the remote build agent.</span></span>

<span data-ttu-id="772e2-203">Assurez-vous que vous pouvez générer l’application pour iOS.</span><span class="sxs-lookup"><span data-stu-id="772e2-203">Make sure you can build the app for iOS.</span></span> <span data-ttu-id="772e2-204">Les étapes décrites dans le guide d’installation sont obligatoires pour générer des applications pour iOS à partir de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="772e2-204">The steps in the setup guide are required to build for iOS from Visual Studio.</span></span> <span data-ttu-id="772e2-205">Si vous n’avez pas de Mac, vous pouvez générer des applications pour iOS à l’aide de l’agent remote build sur un service comme MacInCloud.</span><span class="sxs-lookup"><span data-stu-id="772e2-205">If you do not have a Mac, you can build for iOS using the remote build agent on a service like MacInCloud.</span></span> <span data-ttu-id="772e2-206">Pour plus d’informations, reportez-vous à la page relative à [l’exécution de votre application iOS dans le cloud][21].</span><span class="sxs-lookup"><span data-stu-id="772e2-206">For more info, see [Run your iOS app in the cloud][21].</span></span>

> [!NOTE]
> <span data-ttu-id="772e2-207">XCode 7 ou version ultérieure est requis pour utiliser le plug-in Push sur iOS.</span><span class="sxs-lookup"><span data-stu-id="772e2-207">XCode 7 or greater is required to use the push plugin on iOS.</span></span>

#### <a name="find-the-id-to-use-as-your-app-id"></a><span data-ttu-id="772e2-208">Rechercher l’ID à utiliser en tant qu’ID de l’application</span><span class="sxs-lookup"><span data-stu-id="772e2-208">Find the ID to use as your App ID</span></span>
<span data-ttu-id="772e2-209">Avant d’inscrire votre application pour les notifications Push, ouvrez le fichier config.xml dans votre application Cordova, recherchez la valeur d’attribut `id` dans l’élément de widget et copiez-la pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="772e2-209">Before you register your app for push notifications, open config.xml in your Cordova app, find the `id` attribute value in the widget element, and copy it for later use.</span></span> <span data-ttu-id="772e2-210">Dans le code XML suivant, l’ID est `io.cordova.myapp7777777`.</span><span class="sxs-lookup"><span data-stu-id="772e2-210">In the following XML, the ID is `io.cordova.myapp7777777`.</span></span>

        <widget defaultlocale="en-US" id="io.cordova.myapp7777777"
          version="1.0.0" windows-packageVersion="1.1.0.0" xmlns="http://www.w3.org/ns/widgets"
            xmlns:cdv="http://cordova.apache.org/ns/1.0" xmlns:vs="http://schemas.microsoft.com/appx/2014/htmlapps">

<span data-ttu-id="772e2-211">Vous utiliserez cet identifiant ultérieurement lors de la création d’un ID d’application sur le portail des développeurs d’Apple.</span><span class="sxs-lookup"><span data-stu-id="772e2-211">Later, use this identifier when you create an App ID on Apple's developer portal.</span></span> <span data-ttu-id="772e2-212">Si vous créez un autre ID d’application sur le portail des développeurs, vous devrez effectuer quelques étapes supplémentaires plus tard dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="772e2-212">If you create a different App ID on the developer portal, you must take a few extra steps later in this tutorial.</span></span> <span data-ttu-id="772e2-213">L’ID de l’élément de widget doit correspondre à l’ID d’application sur le portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="772e2-213">The ID in the widget element must match the App ID on the developer portal.</span></span>

#### <a name="register-the-app-for-push-notifications-on-apples-developer-portal"></a><span data-ttu-id="772e2-214">Inscrire l'application pour les notifications push dans le portail de développeurs d'Apple</span><span class="sxs-lookup"><span data-stu-id="772e2-214">Register the app for push notifications on Apple's developer portal</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

[<span data-ttu-id="772e2-215">Regarder une vidéo montrant des étapes similaires</span><span class="sxs-lookup"><span data-stu-id="772e2-215">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-5-Set-up-apns-for-push)

#### <a name="configure-azure-to-send-push-notifications"></a><span data-ttu-id="772e2-216">Configurer Azure pour l’envoi de notifications Push</span><span class="sxs-lookup"><span data-stu-id="772e2-216">Configure Azure to send push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

#### <a name="verify-that-your-app-id-matches-your-cordova-app"></a><span data-ttu-id="772e2-217">Vérifier que votre ID d’application correspond à votre application Cordova</span><span class="sxs-lookup"><span data-stu-id="772e2-217">Verify that your App ID matches your Cordova app</span></span>
<span data-ttu-id="772e2-218">Si l’ID d’application que vous avez créé dans votre compte de développeur Apple correspond déjà à l’ID de l’élément de widget dans le fichier config.xml, vous pouvez ignorer cette étape.</span><span class="sxs-lookup"><span data-stu-id="772e2-218">If the App ID you created in your Apple Developer Account already matches the ID of the widget element in config.xml, you can skip this step.</span></span> <span data-ttu-id="772e2-219">Toutefois, si les ID ne correspondent pas, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="772e2-219">However, if the IDs don't match, take the following steps:</span></span>

1. <span data-ttu-id="772e2-220">Supprimez le dossier platforms de votre projet.</span><span class="sxs-lookup"><span data-stu-id="772e2-220">Delete the platforms folder from your project.</span></span>
2. <span data-ttu-id="772e2-221">Supprimez le dossier plugins de votre projet.</span><span class="sxs-lookup"><span data-stu-id="772e2-221">Delete the plugins folder from your project.</span></span>
3. <span data-ttu-id="772e2-222">Supprimez le dossier node_modules de votre projet.</span><span class="sxs-lookup"><span data-stu-id="772e2-222">Delete the node_modules folder from your project.</span></span>
4. <span data-ttu-id="772e2-223">Mettez à jour l’attribut id de l’élément de widget dans le fichier config.xml pour utiliser l’ID d’application que vous avez créé dans votre compte de développeur Apple.</span><span class="sxs-lookup"><span data-stu-id="772e2-223">Update the id attribute of the widget element in config.xml to use the App ID that you created in your  Apple Developer Account.</span></span>
5. <span data-ttu-id="772e2-224">Régénérez votre projet.</span><span class="sxs-lookup"><span data-stu-id="772e2-224">Rebuild your project.</span></span>

##### <a name="test-push-notifications-in-your-ios-app"></a><span data-ttu-id="772e2-225">Tester les notifications Push dans votre application iOS</span><span class="sxs-lookup"><span data-stu-id="772e2-225">Test push notifications in your iOS app</span></span>
1. <span data-ttu-id="772e2-226">Dans Visual Studio, assurez-vous que **iOS** est sélectionné comme cible de déploiement, puis choisissez **Appareil** pour exécuter votre appareil iOS connecté.</span><span class="sxs-lookup"><span data-stu-id="772e2-226">In Visual Studio, make sure that **iOS** is selected as the deployment target, and then choose **Device** to run on your connected iOS device.</span></span>

    <span data-ttu-id="772e2-227">Vous pouvez exécuter un appareil iOS connecté à votre PC à l’aide d’iTunes.</span><span class="sxs-lookup"><span data-stu-id="772e2-227">You can run on an iOS device connected to your PC using iTunes.</span></span> <span data-ttu-id="772e2-228">Les notifications Push ne sont pas prises en charge par le simulateur iOS.</span><span class="sxs-lookup"><span data-stu-id="772e2-228">The iOS Simulator does not support push notifications.</span></span>

2. <span data-ttu-id="772e2-229">Cliquez sur le bouton **Exécuter** ou sur **F5** dans Visual Studio afin de développer le projet et de démarrer l’application dans un appareil iOS, puis cliquez sur **OK** afin d’accepter les notifications Push.</span><span class="sxs-lookup"><span data-stu-id="772e2-229">Press the **Run** button or **F5** in Visual Studio to build the project and start the app in an iOS  device, then click **OK** to accept push notifications.</span></span>

   > [!NOTE]
   > <span data-ttu-id="772e2-230">L’application demande confirmation pour les notifications push lors de la première exécution.</span><span class="sxs-lookup"><span data-stu-id="772e2-230">The app requests confirmation for push notifications during the first run.</span></span>

3. <span data-ttu-id="772e2-231">Dans l'application, tapez une tâche, puis cliquez sur l'icône plus (+).</span><span class="sxs-lookup"><span data-stu-id="772e2-231">In the app, type a task, and then click the plus (+) icon.</span></span>
4. <span data-ttu-id="772e2-232">Vérifiez que vous avez reçu une notification, puis cliquez sur OK pour la fermer.</span><span class="sxs-lookup"><span data-stu-id="772e2-232">Verify that a notification is received, then click OK to dismiss the notification.</span></span>

## <a name="optional-configure-and-run-on-windows"></a><span data-ttu-id="772e2-233">(Facultatif) Configurer et exécuter sur Windows</span><span class="sxs-lookup"><span data-stu-id="772e2-233">(Optional) Configure and run on Windows</span></span>
<span data-ttu-id="772e2-234">Cette section est dédiée à l’exécution du projet d’application Apache Cordova sur les appareils Windows 10 (le plug-in push PhoneGap est pris en charge sur Windows 10).</span><span class="sxs-lookup"><span data-stu-id="772e2-234">This section is for running the Apache Cordova app project on Windows 10 devices (the PhoneGap push plugin is supported on Windows 10).</span></span> <span data-ttu-id="772e2-235">Vous pouvez ignorer cette section si vous n'utilisez pas d'appareils Windows.</span><span class="sxs-lookup"><span data-stu-id="772e2-235">If you are not working with Windows devices, you can skip this section.</span></span>

#### <a name="register-your-windows-app-for-push-notifications-with-wns"></a><span data-ttu-id="772e2-236">Inscrire votre application Windows pour les notifications Push avec WNS</span><span class="sxs-lookup"><span data-stu-id="772e2-236">Register your Windows app for push notifications with WNS</span></span>
<span data-ttu-id="772e2-237">Pour utiliser les options de stockage dans Visual Studio, sélectionnez une cible de Windows à partir de la liste des plateformes de solution, par exemple **Windows-x64** ou **Windows-x86** (évitez **Windows-AnyCPU** pour les notifications Push).</span><span class="sxs-lookup"><span data-stu-id="772e2-237">To use the Store options in Visual Studio, select a Windows target from the Solution Platforms list, like **Windows-x64** or **Windows-x86** (avoid **Windows-AnyCPU** for push notifications).</span></span>

[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

<span data-ttu-id="772e2-238">[Regarder une vidéo montrant des étapes similaires][13]</span><span class="sxs-lookup"><span data-stu-id="772e2-238">[Watch a video showing similar steps][13]</span></span>

#### <a name="configure-the-notification-hub-for-wns"></a><span data-ttu-id="772e2-239">Configurer le Notification Hub pour WNS</span><span class="sxs-lookup"><span data-stu-id="772e2-239">Configure the notification hub for WNS</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="configure-your-cordova-app-to-support-windows-push-notifications"></a><span data-ttu-id="772e2-240">Configurer votre application Cordova pour prendre en charge les notifications Push Windows</span><span class="sxs-lookup"><span data-stu-id="772e2-240">Configure your Cordova app to support Windows push notifications</span></span>
<span data-ttu-id="772e2-241">Ouvrez le concepteur de configuration (cliquez avec le bouton droit sur le fichier config.xml, puis sélectionnez **Concepteur de vue**), sélectionnez l’onglet **Windows**, puis cliquez sur **Windows 10** sous **Version cible de Windows**.</span><span class="sxs-lookup"><span data-stu-id="772e2-241">Open the configuration designer (right-click on config.xml and select **View Designer**), select the **Windows** tab, and choose **Windows 10** under **Windows Target Version**.</span></span>

<span data-ttu-id="772e2-242">Pour prendre en charge les notifications Push dans vos versions (de débogage) par défaut, ouvrez le fichier build.json.</span><span class="sxs-lookup"><span data-stu-id="772e2-242">To support push notifications in your default (debug) builds, open build.json file.</span></span> <span data-ttu-id="772e2-243">Copiez la configuration de « lancement » dans votre configuration de débogage.</span><span class="sxs-lookup"><span data-stu-id="772e2-243">Copy the "release" configuration to your debug configuration.</span></span>

        "windows": {
            "release": {
                "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
                "publisherId": "CN=yourpublisherID"
            }
        }

<span data-ttu-id="772e2-244">Après la mise à jour, build.json doit contenir le code suivant :</span><span class="sxs-lookup"><span data-stu-id="772e2-244">After the update, the build.json should contain the following code:</span></span>

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

<span data-ttu-id="772e2-245">Générez l’application et vérifiez l’absence d’erreurs.</span><span class="sxs-lookup"><span data-stu-id="772e2-245">Build the app and verify that you have no errors.</span></span> <span data-ttu-id="772e2-246">Votre application cliente doit désormais s’inscrire pour les notifications du serveur principal d’application mobile.</span><span class="sxs-lookup"><span data-stu-id="772e2-246">Your client app should now register for the notifications from the Mobile App backend.</span></span> <span data-ttu-id="772e2-247">Répétez cette section pour chaque projet Windows dans votre solution.</span><span class="sxs-lookup"><span data-stu-id="772e2-247">Repeat this section for every Windows project in your solution.</span></span>

#### <a name="test-push-notifications-in-your-windows-app"></a><span data-ttu-id="772e2-248">Tester les notifications Push dans votre application Windows</span><span class="sxs-lookup"><span data-stu-id="772e2-248">Test push notifications in your Windows app</span></span>
<span data-ttu-id="772e2-249">Dans Visual Studio, assurez-vous qu’une plateforme Windows est sélectionnée comme cible de déploiement, telle que **Windows-x64** ou **Windows-x86**.</span><span class="sxs-lookup"><span data-stu-id="772e2-249">In Visual Studio, make sure that a Windows platform is selected as the deployment target, such as **Windows-x64** or **Windows-x86**.</span></span> <span data-ttu-id="772e2-250">Pour exécuter l’application sur un PC Windows 10 hébergeant Visual Studio, choisissez **Ordinateur local**.</span><span class="sxs-lookup"><span data-stu-id="772e2-250">To run the app on a Windows 10 PC hosting Visual Studio, choose **Local Machine**.</span></span>

<span data-ttu-id="772e2-251">Cliquez sur le bouton Exécuter pour générer le projet et démarrer l’application.</span><span class="sxs-lookup"><span data-stu-id="772e2-251">Press the Run button to build the project and start the app.</span></span>

<span data-ttu-id="772e2-252">Dans l’application, tapez un nom pour un nouvel élément todoitem, puis cliquez sur l’icône de signe plus (+) pour l’ajouter.</span><span class="sxs-lookup"><span data-stu-id="772e2-252">In the app, type a name for a new todoitem, and then click the plus (+) icon to add it.</span></span>

<span data-ttu-id="772e2-253">Vérifiez qu’une notification est reçue lorsque l’élément est ajouté.</span><span class="sxs-lookup"><span data-stu-id="772e2-253">Verify that a notification is received when the item is added.</span></span>

## <span data-ttu-id="772e2-254"><a name="next-steps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="772e2-254"><a name="next-steps"></a>Next Steps</span></span>
* <span data-ttu-id="772e2-255">Consultez la documentation relative à [Notification Hubs][17] afin d’en découvrir davantage sur les notifications Push.</span><span class="sxs-lookup"><span data-stu-id="772e2-255">Read about [Notification Hubs][17] to learn about push notifications.</span></span>
* <span data-ttu-id="772e2-256">Si vous ne l’avez pas encore fait, continuez le didacticiel en [ajoutant l’authentification][14] à votre application Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="772e2-256">If you have not already done so, continue the tutorial by [Adding Authentication][14] to your Apache Cordova app.</span></span>

<span data-ttu-id="772e2-257">Découvrez comment utiliser les Kits de développement logiciel.</span><span class="sxs-lookup"><span data-stu-id="772e2-257">Learn how to use the SDKs.</span></span>

* <span data-ttu-id="772e2-258">[Kit de développement logiciel (SDK) Apache Cordova][15]</span><span class="sxs-lookup"><span data-stu-id="772e2-258">[Apache Cordova SDK][15]</span></span>
* <span data-ttu-id="772e2-259">[Kit de développement logiciel du serveur ASP.NET][1]</span><span class="sxs-lookup"><span data-stu-id="772e2-259">[ASP.NET Server SDK][1]</span></span>
* <span data-ttu-id="772e2-260">[Kit de développement logiciel du serveur Node.js][16]</span><span class="sxs-lookup"><span data-stu-id="772e2-260">[Node.js Server SDK][16]</span></span>

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
