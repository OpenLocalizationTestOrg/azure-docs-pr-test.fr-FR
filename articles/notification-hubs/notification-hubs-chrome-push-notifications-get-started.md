---
title: notifications push aaaSend tooChrome les applications avec Azure Notification Hubs | Documents Microsoft
description: "Découvrez comment toouse Azure Notification Hubs toosend push notifications tooa Chrome application."
services: notification-hubs
keywords: notifications push mobiles, notifications push, notification push, notifications push chrome
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 75d4ff59-d04a-455f-bd44-0130a68e641f
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-chrome
ms.devlang: JavaScript
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 7dec8ab02622563bc3730a2e96820da8932d22f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="send-push-notifications-toochrome-apps-with-azure-notification-hubs"></a><span data-ttu-id="365f2-104">Envoyer des notifications d’applications tooChrome avec Azure Notification Hubs push</span><span class="sxs-lookup"><span data-stu-id="365f2-104">Send push notifications tooChrome apps with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

<span data-ttu-id="365f2-105">Cette rubrique vous montre comment toouse Azure Notification Hubs toosend push notifications tooa application Chrome qui sera affiché dans le contexte de hello Hello navigateur Google Chrome.</span><span class="sxs-lookup"><span data-stu-id="365f2-105">This topic shows you how toouse Azure Notification Hubs toosend push notifications tooa Chrome App, which will be displayed within hello context of hello Google Chrome browser.</span></span> <span data-ttu-id="365f2-106">Dans ce didacticiel, nous allons créer une application Chrome qui reçoit des notifications push à l’aide de [Google Cloud Messaging (GCM)](https://developers.google.com/cloud-messaging/).</span><span class="sxs-lookup"><span data-stu-id="365f2-106">In this tutorial, we will create a Chrome app that receives push notifications by using [Google Cloud Messaging (GCM)](https://developers.google.com/cloud-messaging/).</span></span> 

> [!NOTE]
> <span data-ttu-id="365f2-107">toocomplete ce didacticiel, vous devez disposer d’un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="365f2-107">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="365f2-108">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="365f2-108">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="365f2-109">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%notification-hubs-chrome-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="365f2-109">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%notification-hubs-chrome-get-started%2F).</span></span>
> 
> 

<span data-ttu-id="365f2-110">didacticiel de Hello vous guide tout au long de ces notifications de push tooenable étapes de base :</span><span class="sxs-lookup"><span data-stu-id="365f2-110">hello tutorial walks you through these basic steps tooenable push notifications:</span></span>

* [<span data-ttu-id="365f2-111">Activation de Google Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="365f2-111">Enable Google Cloud Messaging</span></span>](#register)
* [<span data-ttu-id="365f2-112">Configuration de votre hub de notification</span><span class="sxs-lookup"><span data-stu-id="365f2-112">Configure your notification hub</span></span>](#configure-hub)
* [<span data-ttu-id="365f2-113">Se connecter à votre hub de notification d’application de Chrome toohello</span><span class="sxs-lookup"><span data-stu-id="365f2-113">Connect your Chrome App toohello notification hub</span></span>](#connect-app)
* [<span data-ttu-id="365f2-114">Envoyer un tooyour de notification push Chrome application</span><span class="sxs-lookup"><span data-stu-id="365f2-114">Send a push notification tooyour Chrome App</span></span>](#send)
* [<span data-ttu-id="365f2-115">Fonctionnalités et capacités supplémentaires</span><span class="sxs-lookup"><span data-stu-id="365f2-115">Additional functionality & capabilities</span></span>](#next-steps)

> [!NOTE]
> <span data-ttu-id="365f2-116">Notifications push de l’application chrome ne sont pas des notifications dans un navigateur génériques - ils sont le modèle d’extensibilité de navigateur toohello spécifique (consultez [vue d’ensemble des applications de Chrome] pour plus d’informations).</span><span class="sxs-lookup"><span data-stu-id="365f2-116">Chrome app push notifications are not generic in-browser notifications - they are specific toohello browser extensibility model (see [Chrome Apps Overview] for details).</span></span> <span data-ttu-id="365f2-117">En outre toohello navigateur de bureau, Chrome applications s’exécutent sur mobile (Android et iOS) via Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="365f2-117">In addition toohello desktop browser, Chrome apps run on mobile (Android and iOS) through Apache Cordova.</span></span> <span data-ttu-id="365f2-118">Consultez [applications Chrome sur Mobile] toolearn plus.</span><span class="sxs-lookup"><span data-stu-id="365f2-118">See [Chrome Apps on Mobile] toolearn more.</span></span>
> 
> 

<span data-ttu-id="365f2-119">Configuration GCM et Azure Notification Hubs est identiques tooconfiguring pour Android, car [de messagerie Cloud Google Chrome] a été déconseillée et hello GCM même prend désormais en charge les appareils Android et instances de Chrome.</span><span class="sxs-lookup"><span data-stu-id="365f2-119">Configuring GCM and Azure Notification Hubs is identical tooconfiguring for Android, since [Google Cloud Messaging for Chrome] has been deprecated and hello same GCM now supports both Android devices and Chrome instances.</span></span>

## <span data-ttu-id="365f2-120"><a id="register"></a>Activer Google Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="365f2-120"><a id="register"></a>Enable Google Cloud Messaging</span></span>
1. <span data-ttu-id="365f2-121">Accédez toohello [Google Cloud Console] site Web, connectez-vous avec vos informations d’identification du compte Google, puis cliquez sur hello **créer un projet** bouton.</span><span class="sxs-lookup"><span data-stu-id="365f2-121">Navigate toohello [Google Cloud Console] website, sign in with your Google account credentials, and then click hello **Create Project** button.</span></span> <span data-ttu-id="365f2-122">Fournir un **nom du projet**, puis cliquez sur hello **créer** bouton.</span><span class="sxs-lookup"><span data-stu-id="365f2-122">Provide an appropriate **Project Name**, and then click hello **Create** button.</span></span>
   
       ![Google Cloud Console - Create Project][1]
2. <span data-ttu-id="365f2-123">Prenez note de hello **numéro de projet** sur hello **projets** page hello projet que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="365f2-123">Make a note of hello **Project Number** on hello **Projects** page for hello project that you just created.</span></span> <span data-ttu-id="365f2-124">Vous allez utiliser comme hello **ID de l’expéditeur GCM** dans tooregister de Chrome application hello avec GCM.</span><span class="sxs-lookup"><span data-stu-id="365f2-124">You will use this as hello **GCM Sender ID** in hello Chrome App tooregister with GCM.</span></span>
   
       ![Google Cloud Console - Project Number][2]
3. <span data-ttu-id="365f2-125">Dans le volet gauche de hello, cliquez sur **API & auth**et faites défiler vers le bas, puis cliquez sur hello bascule tooenable **Google Cloud Messaging pour Android**.</span><span class="sxs-lookup"><span data-stu-id="365f2-125">In hello left pane, click **APIs & auth**, and then scroll down and click hello toggle tooenable **Google Cloud Messaging for Android**.</span></span> <span data-ttu-id="365f2-126">Vous n’avez pas tooenable **de messagerie Cloud Google Chrome**.</span><span class="sxs-lookup"><span data-stu-id="365f2-126">You don't have tooenable **Google Cloud Messaging for Chrome**.</span></span>
   
       ![Google Cloud Console - Server Key][3]
4. <span data-ttu-id="365f2-127">Dans le volet gauche de hello, cliquez sur **informations d’identification** > **créer une nouvelle clé** > **clé serveur** > **créer**.</span><span class="sxs-lookup"><span data-stu-id="365f2-127">In hello left pane, click **Credentials** > **Create New Key** > **Server Key** > **Create**.</span></span>
   
       ![Google Cloud Console - Credentials][4]
5. <span data-ttu-id="365f2-128">Prenez note du serveur de hello **clé API**.</span><span class="sxs-lookup"><span data-stu-id="365f2-128">Make a note of hello server **API Key**.</span></span> <span data-ttu-id="365f2-129">Vous allez configurer cela dans votre tooenable suivant, concentrateur de notification Il tooGCM de notifications push toosend.</span><span class="sxs-lookup"><span data-stu-id="365f2-129">You will configure this in your notification hub next, tooenable it toosend push notifications tooGCM.</span></span>
   
       ![Google Cloud Console - API Key][5]

## <span data-ttu-id="365f2-130"><a id="configure-hub"></a>Configuration de votre hub de notification</span><span class="sxs-lookup"><span data-stu-id="365f2-130"><a id="configure-hub"></a>Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<span data-ttu-id="365f2-131">&emsp;&emsp;6.</span><span class="sxs-lookup"><span data-stu-id="365f2-131">&emsp;&emsp;6.</span></span>   <span data-ttu-id="365f2-132">Bonjour **paramètres** panneau, sélectionnez **Notification Services** , puis **Google (GCM)**.</span><span class="sxs-lookup"><span data-stu-id="365f2-132">In hello **Settings** blade, select **Notification Services** and then **Google (GCM)**.</span></span> <span data-ttu-id="365f2-133">Entrez la clé d’API hello et enregistrer.</span><span class="sxs-lookup"><span data-stu-id="365f2-133">Enter hello API key and save.</span></span>

&emsp;&emsp;![Azure Notification Hubs - Google (GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

## <span data-ttu-id="365f2-135"><a id="connect-app"></a>Se connecter à votre hub de notification d’application de Chrome toohello</span><span class="sxs-lookup"><span data-stu-id="365f2-135"><a id="connect-app"></a>Connect your Chrome App toohello notification hub</span></span>
<span data-ttu-id="365f2-136">Votre concentrateur de notification est maintenant configuré toowork avec GCM, et vous avez tooregister de chaînes de connexion hello tooboth de votre application de réception et envoyer des notifications push.</span><span class="sxs-lookup"><span data-stu-id="365f2-136">Your notification hub is now configured toowork with GCM, and you have hello connection strings tooregister your app tooboth receive and send push notifications.</span></span> <span data-ttu-id="365f2-137">LK</span><span class="sxs-lookup"><span data-stu-id="365f2-137">LK</span></span>

### <a name="create-a-new-chrome-app"></a><span data-ttu-id="365f2-138">Création d’une application Chrome</span><span class="sxs-lookup"><span data-stu-id="365f2-138">Create a new Chrome App</span></span>
<span data-ttu-id="365f2-139">exemple Hello ci-dessous est basé sur hello [Chrome application GCM exemple] et utilise hello recommandé toocreate de la façon dont une application de Chrome.</span><span class="sxs-lookup"><span data-stu-id="365f2-139">hello sample below is based on hello [Chrome App GCM Sample] and uses hello recommended way toocreate a Chrome App.</span></span> <span data-ttu-id="365f2-140">Il met en surbrillance hello étapes tooAzure concernant spécifiquement concentrateurs de Notification.</span><span class="sxs-lookup"><span data-stu-id="365f2-140">We will highlight hello steps specifically related tooAzure Notification Hubs.</span></span> 

> [!NOTE]
> <span data-ttu-id="365f2-141">Nous vous conseillons de télécharger la source de hello pour cette application de Chrome de [exemple Hub de Notification d’application Chrome].</span><span class="sxs-lookup"><span data-stu-id="365f2-141">We recommend that you download hello source for this Chrome App from [Chrome App Notification Hub Sample].</span></span>
> 
> 

<span data-ttu-id="365f2-142">Hello Chrome application est créé via JavaScript, et vous pouvez utiliser tous vos éditeurs word par défaut pour sa création.</span><span class="sxs-lookup"><span data-stu-id="365f2-142">hello Chrome App is created via JavaScript, and you can use any of your preferred word editors for creating it.</span></span> <span data-ttu-id="365f2-143">Voici à quoi ressemblera cette application Chrome.</span><span class="sxs-lookup"><span data-stu-id="365f2-143">Below is what this Chrome App will look like.</span></span>

![Application Google Chrome][15]

1. <span data-ttu-id="365f2-145">Créez un dossier et nommez-le `ChromePushApp`.</span><span class="sxs-lookup"><span data-stu-id="365f2-145">Create a folder and name it `ChromePushApp`.</span></span> <span data-ttu-id="365f2-146">Bien entendu, le nom de hello est arbitraire - si vous lui donner un nommez différent, assurez-vous que vous remplacez chemin hello dans les segments de code hello requis.</span><span class="sxs-lookup"><span data-stu-id="365f2-146">Of course, hello name is arbitrary - if you name it something different, make sure you substitute hello path in hello required code segments.</span></span>
2. <span data-ttu-id="365f2-147">Télécharger hello [crypto-js bibliothèque] dans le dossier hello créé à l’étape de deuxième hello.</span><span class="sxs-lookup"><span data-stu-id="365f2-147">Download hello [crypto-js library] in hello folder you created in hello second step.</span></span> <span data-ttu-id="365f2-148">Ce dossier contiendra deux sous-dossiers : `components` et `rollups`.</span><span class="sxs-lookup"><span data-stu-id="365f2-148">This library folder will contain two subfolders: `components` and `rollups`.</span></span>
3. <span data-ttu-id="365f2-149">Créez un fichier `manifest.json` .</span><span class="sxs-lookup"><span data-stu-id="365f2-149">Create a `manifest.json` file.</span></span> <span data-ttu-id="365f2-150">Toutes les applications de Chrome sont soutenues par un fichier manifeste qui contient les métadonnées de l’application hello et, le plus important encore, toutes les autorisations accordées toohello application lorsque l’utilisateur de hello l’installe.</span><span class="sxs-lookup"><span data-stu-id="365f2-150">All Chrome Apps are backed by a manifest file that contains hello app metadata and, most importantly, all permissions that are granted toohello app when hello user installs it.</span></span>
   
        {
          "name": "NH-GCM Notifications",
          "description": "Chrome platform app.",
          "manifest_version": 2,
          "version": "0.1",
          "app": {
            "background": {
              "scripts": ["background.js"]
            }
          },
          "permissions": ["gcm", "storage", "notifications", "https://*.servicebus.windows.net/*"],
          "icons": { "128": "gcm_128.png" }
        }
   
    <span data-ttu-id="365f2-151">Hello d’avis `permissions` élément, ce qui indique que cette application Chrome sera en mesure de tooreceive notifications push GCM.</span><span class="sxs-lookup"><span data-stu-id="365f2-151">Notice hello `permissions` element, which specifies that this Chrome App will be able tooreceive push notifications from GCM.</span></span> <span data-ttu-id="365f2-152">Il doit également spécifier hello Azure Notification Hubs URI où hello Chrome application fera une tooregister d’appel REST.</span><span class="sxs-lookup"><span data-stu-id="365f2-152">It must also specify hello Azure Notification Hubs URI where hello Chrome App will make a REST call tooregister.</span></span>
    <span data-ttu-id="365f2-153">Notre exemple d’application utilise également un fichier icône, `gcm_128.png`, que vous trouverez sur source hello qui est réutilisé à partir de l’exemple GCM hello d’origine.</span><span class="sxs-lookup"><span data-stu-id="365f2-153">Our sample app also uses an icon file, `gcm_128.png`, that you will find at hello source that's reused from hello original GCM sample.</span></span> <span data-ttu-id="365f2-154">Vous pouvez le remplacer pour toute image qui correspond à hello [critères d’icône](https://developer.chrome.com/apps/manifest/icons).</span><span class="sxs-lookup"><span data-stu-id="365f2-154">You can substitute it for any image that fits hello [icon criteria](https://developer.chrome.com/apps/manifest/icons).</span></span>
4. <span data-ttu-id="365f2-155">Créez un fichier appelé `background.js` avec hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="365f2-155">Create a file called `background.js` with hello following code:</span></span>
   
        // Returns a new notification ID used in hello notification.
        function getNotificationId() {
          var id = Math.floor(Math.random() * 9007199254740992) + 1;
          return id.toString();
        }
   
        function messageReceived(message) {
          // A message is an object with a data property that
          // consists of key-value pairs.
   
          // Concatenate all key-value pairs tooform a display string.
          var messageString = "";
          for (var key in message.data) {
            if (messageString != "")
              messageString += ", "
            messageString += key + ":" + message.data[key];
          }
          console.log("Message received: " + messageString);
   
          // Pop up a notification tooshow hello GCM message.
          chrome.notifications.create(getNotificationId(), {
            title: 'GCM Message',
            iconUrl: 'gcm_128.png',
            type: 'basic',
            message: messageString
          }, function() {});
        }
   
        var registerWindowCreated = false;
   
        function firstTimeRegistration() {
          chrome.storage.local.get("registered", function(result) {
   
            registerWindowCreated = true;
            chrome.app.window.create(
              "register.html",
              {  width: 520,
                 height: 500,
                 frame: 'chrome'
              },
              function(appWin) {}
            );
          });
        }
   
        // Set up a listener for GCM message event.
        chrome.gcm.onMessage.addListener(messageReceived);
   
        // Set up listeners tootrigger hello first-time registration.
        chrome.runtime.onInstalled.addListener(firstTimeRegistration);
        chrome.runtime.onStartup.addListener(firstTimeRegistration);
   
    <span data-ttu-id="365f2-156">Il s’agit des fichiers hello qui s’affiche la fenêtre d’application de Chrome hello HTML (**register.html**) et définit également le Gestionnaire de hello **messageReceived** toohandle hello entrants de notifications push.</span><span class="sxs-lookup"><span data-stu-id="365f2-156">This is hello file that pops up hello Chrome App window HTML (**register.html**) and also defines hello handler **messageReceived** toohandle hello incoming push notification.</span></span>
5. <span data-ttu-id="365f2-157">Créez un fichier appelé `register.html` -définit hello l’interface utilisateur de hello Chrome application.</span><span class="sxs-lookup"><span data-stu-id="365f2-157">Create a file called `register.html` - this defines hello UI of hello Chrome App.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="365f2-158">Cet exemple utilise **CryptoJS v3.1.2**.</span><span class="sxs-lookup"><span data-stu-id="365f2-158">This sample uses **CryptoJS v3.1.2**.</span></span> <span data-ttu-id="365f2-159">Si vous avez téléchargé une autre version de la bibliothèque de hello, assurez-vous que vous remplacez correctement version hello Bonjour `src` chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="365f2-159">If you downloaded another version of hello library, make sure you properly substitute hello version in hello `src` path.</span></span>
   > 
   > 
   
        <html>
   
        <head>
        <title>GCM Registration</title>
        <script src="register.js"></script>
        <script src="CryptoJS v3.1.2/rollups/hmac-sha256.js"></script>
        <script src="CryptoJS v3.1.2/components/enc-base64-min.js"></script>
        </head>
   
        <body>
   
        Sender ID:<br/><input id="senderId" type="TEXT" size="20"><br/>
        <button id="registerWithGCM">Register with GCM</button>
        <br/>
        <br/>
        <br/>
   
        Notification Hub Name:<br/><input id="hubName" type="TEXT" style="width:400px"><br/><br/>
        Connection String:<br/><textarea id="connectionString" type="TEXT" style="width:400px;height:60px"></textarea>
   
        <br/>
   
        <button id="registerWithNH" disabled="true">Register with Azure Notification Hubs</button>
   
        <br/>
        <br/>
   
        <textarea id="console" type="TEXT" readonly style="width:500px;height:200px;background-color:#e5e5e5;padding:5px"></textarea>
   
        </body>
   
        </html>
6. <span data-ttu-id="365f2-160">Créez un fichier appelé `register.js` avec le code hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="365f2-160">Create a file called `register.js` with hello code below.</span></span> <span data-ttu-id="365f2-161">Ce fichier Spécifie le script hello derrière `register.html`.</span><span class="sxs-lookup"><span data-stu-id="365f2-161">This file specifies hello script behind `register.html`.</span></span> <span data-ttu-id="365f2-162">Applications de chrome n’autorisent pas l’exécution inline, afin que vous ayez toocreate un script de sauvegarde distinct pour votre interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="365f2-162">Chrome Apps do not allow inline execution, so you have toocreate a separate backing script for your UI.</span></span>
   
        var registrationId = "";
        var hubName        = "", connectionString = "";
        var originalUri    = "", targetUri = "", endpoint = "", sasKeyName = "", sasKeyValue = "", sasToken = "";
   
        window.onload = function() {
           document.getElementById("registerWithGCM").onclick = registerWithGCM;  
           document.getElementById("registerWithNH").onclick = registerWithNH;
           updateLog("You have not registered yet. Please provider sender ID and register with GCM and then with  Notification Hubs.");
        }
   
        function updateLog(status) {
          currentStatus = document.getElementById("console").innerHTML;
          if (currentStatus != "") {
            currentStatus = currentStatus + "\n\n";
          }
   
          document.getElementById("console").innerHTML = currentStatus  + status;
        }
   
        function registerWithGCM() {
          var senderId = document.getElementById("senderId").value.trim();
          chrome.gcm.register([senderId], registerCallback);
   
          // Prevent register button from being clicked again before hello registration finishes.
          document.getElementById("registerWithGCM").disabled = true;
        }
   
        function registerCallback(regId) {
          registrationId = regId;
          document.getElementById("registerWithGCM").disabled = false;
   
          if (chrome.runtime.lastError) {
            // When hello registration fails, handle hello error and retry the
            // registration later.
            updateLog("Registration failed: " + chrome.runtime.lastError.message);
            return;
          }
   
          updateLog("Registration with GCM succeeded.");
          document.getElementById("registerWithNH").disabled = false;
   
          // Mark that hello first-time registration is done.
          chrome.storage.local.set({registered: true});
        }
   
        function registerWithNH() {
          hubName = document.getElementById("hubName").value.trim();
          connectionString = document.getElementById("connectionString").value.trim();
          splitConnectionString();
          generateSaSToken();
          sendNHRegistrationRequest();
        }
   
        // From http://msdn.microsoft.com/library/dn495627.aspx
        function splitConnectionString()
        {
          var parts = connectionString.split(';');
          if (parts.length != 3)
          throw "Error parsing connection string";
   
          parts.forEach(function(part) {
            if (part.indexOf('Endpoint') == 0) {
            endpoint = 'https' + part.substring(11);
            } else if (part.indexOf('SharedAccessKeyName') == 0) {
            sasKeyName = part.substring(20);
            } else if (part.indexOf('SharedAccessKey') == 0) {
            sasKeyValue = part.substring(16);
            }
          });
   
          originalUri = endpoint + hubName;
        }
   
        function generateSaSToken()
        {
          targetUri = encodeURIComponent(originalUri.toLowerCase()).toLowerCase();
          var expiresInMins = 10; // 10 minute expiration
   
          // Set expiration in seconds.
          var expireOnDate = new Date();
          expireOnDate.setMinutes(expireOnDate.getMinutes() + expiresInMins);
          var expires = Date.UTC(expireOnDate.getUTCFullYear(), expireOnDate
            .getUTCMonth(), expireOnDate.getUTCDate(), expireOnDate
            .getUTCHours(), expireOnDate.getUTCMinutes(), expireOnDate
            .getUTCSeconds()) / 1000;
          var tosign = targetUri + '\n' + expires;
   
          // Using CryptoJS.
          var signature = CryptoJS.HmacSHA256(tosign, sasKeyValue);
          var base64signature = signature.toString(CryptoJS.enc.Base64);
          var base64UriEncoded = encodeURIComponent(base64signature);
   
          // Construct authorization string.
          sasToken = "SharedAccessSignature sr=" + targetUri + "&sig="
                          + base64UriEncoded + "&se=" + expires + "&skn=" + sasKeyName;
        }
   
        function sendNHRegistrationRequest()
        {
          var registrationPayload =
          "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
          "<entry xmlns=\"http://www.w3.org/2005/Atom\">" +
              "<content type=\"application/xml\">" +
                  "<GcmRegistrationDescription xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/netservices/2010/10/servicebus/connect\">" +
                      "<GcmRegistrationId>{GCMRegistrationId}</GcmRegistrationId>" +
                  "</GcmRegistrationDescription>" +
              "</content>" +
          "</entry>";
   
          // Update hello payload with hello registration ID obtained earlier.
          registrationPayload = registrationPayload.replace("{GCMRegistrationId}", registrationId);
   
          var url = originalUri + "/registrations/?api-version=2014-09";
          var client = new XMLHttpRequest();
   
          client.onload = function () {
            if (client.readyState == 4) {
              if (client.status == 200) {
                updateLog("Notification Hub Registration succesful!");
                updateLog(client.responseText);
              } else {
                updateLog("Notification Hub Registration did not succeed!");
                updateLog("HTTP Status: " + client.status + " : " + client.statusText);
                updateLog("HTTP Response: " + "\n" + client.responseText);
              }
            }
          };
   
          client.onerror = function () {
                updateLog("ERROR - Notification Hub Registration did not succeed!");
          }
   
          client.open("POST", url, true);
          client.setRequestHeader("Content-Type", "application/atom+xml;type=entry;charset=utf-8");
          client.setRequestHeader("Authorization", sasToken);
          client.setRequestHeader("x-ms-version", "2014-09");
   
          try {
              client.send(registrationPayload);
          }
          catch(err) {
              updateLog(err.message);
          }
        }
   
    <span data-ttu-id="365f2-163">Hello au-dessus de script a hello paramètres clés suivants :</span><span class="sxs-lookup"><span data-stu-id="365f2-163">hello above script has hello following key parameters:</span></span>
   
   * <span data-ttu-id="365f2-164">**Window.OnLoad** définit les événements de clic de bouton hello des boutons de hello deux sur hello l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="365f2-164">**window.onload** defines hello button-click events of hello two buttons on hello UI.</span></span> <span data-ttu-id="365f2-165">Un inscrit avec GCM et hello autres utilise l’ID d’inscription hello qui est retournée après l’inscription avec tooregister GCM avec Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="365f2-165">One registers with GCM, and hello other uses hello registration ID that's returned after registration with GCM tooregister with Azure Notification Hubs.</span></span>
   * <span data-ttu-id="365f2-166">**updateLog** est fonction hello qui nous permet de toohandle des fonctions d’enregistrement simple.</span><span class="sxs-lookup"><span data-stu-id="365f2-166">**updateLog** is hello function that allows us toohandle simple logging capabilities.</span></span>
   * <span data-ttu-id="365f2-167">**registerWithGCM** est le Gestionnaire de clic de bouton premier hello, ce qui rend hello `chrome.gcm.register` appel tooGCM tooregister hello Chrome application instance en cours.</span><span class="sxs-lookup"><span data-stu-id="365f2-167">**registerWithGCM** is hello first button-click handler, which makes hello `chrome.gcm.register` call tooGCM tooregister hello current Chrome App instance.</span></span>
   * <span data-ttu-id="365f2-168">**registerCallback** est fonction de rappel hello qui est appelée lorsque hello appel d’inscription GCM retourne.</span><span class="sxs-lookup"><span data-stu-id="365f2-168">**registerCallback** is hello callback function that gets called when hello GCM registration call returns.</span></span>
   * <span data-ttu-id="365f2-169">**registerWithNH** est le Gestionnaire de clic de bouton deuxième hello, qui inscrit avec Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="365f2-169">**registerWithNH** is hello second button-click handler, which registers with Notification Hubs.</span></span> <span data-ttu-id="365f2-170">Il obtient `hubName` et `connectionString` (utilisateur hello a spécifié) et les travaux manuels hello appel d’API REST de Notification Hubs d’inscription.</span><span class="sxs-lookup"><span data-stu-id="365f2-170">It gets `hubName` and `connectionString` (which hello user has specified) and crafts hello Notification Hubs Registration REST API call.</span></span>
   * <span data-ttu-id="365f2-171">**splitConnectionString** et **generateSaSToken** sont des programmes d’assistance qui représentent l’implémentation JavaScript de hello d’un processus de création d’un jeton SaS, qui doit être utilisé dans tous les appels d’API REST.</span><span class="sxs-lookup"><span data-stu-id="365f2-171">**splitConnectionString** and **generateSaSToken** are helpers that represent hello JavaScript implementation of a SaS token creation process, that must be used in all REST API calls.</span></span> <span data-ttu-id="365f2-172">Pour plus d’informations, consultez la page [Concepts courants](http://msdn.microsoft.com/library/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="365f2-172">For more information, see [Common Concepts](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
   * <span data-ttu-id="365f2-173">**sendNHRegistrationRequest** appel de fonction hello qui rend un HTTP REST est tooAzure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="365f2-173">**sendNHRegistrationRequest** is hello function that makes a HTTP REST call tooAzure Notification Hubs.</span></span>
   * <span data-ttu-id="365f2-174">**registrationPayload** définit la charge utile de hello d’enregistrement XML.</span><span class="sxs-lookup"><span data-stu-id="365f2-174">**registrationPayload** defines hello registration XML payload.</span></span> <span data-ttu-id="365f2-175">Pour plus d’informations, voir [Création de l’API REST NH d’inscription].</span><span class="sxs-lookup"><span data-stu-id="365f2-175">For more information, see [Create Registration NH REST API].</span></span> <span data-ttu-id="365f2-176">Nous mettre à jour l’ID d’inscription hello qu’elle contient avec ce que nous avons reçu de GCM.</span><span class="sxs-lookup"><span data-stu-id="365f2-176">We update hello registration ID in it with what we received from GCM.</span></span>
   * <span data-ttu-id="365f2-177">**client** est une instance de **XMLHttpRequest** que nous utilisons demande de requête HTTP POST toomake hello.</span><span class="sxs-lookup"><span data-stu-id="365f2-177">**client** is an instance of **XMLHttpRequest** that we use toomake hello HTTP POST request.</span></span> <span data-ttu-id="365f2-178">Notez que nous mettre à jour hello `Authorization` en-tête avec `sasToken`.</span><span class="sxs-lookup"><span data-stu-id="365f2-178">Note that we update hello `Authorization` header with `sasToken`.</span></span> <span data-ttu-id="365f2-179">La réussite de cet appel enregistre cette instance de l’application Chrome auprès d’Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="365f2-179">Successful completion of this call will register this Chrome App instance with Azure Notification Hubs.</span></span>

<span data-ttu-id="365f2-180">Hello globale structure de dossiers pour ce projet doit ressembler à ceci : ![Google Chrome application - Structure de dossiers][21]</span><span class="sxs-lookup"><span data-stu-id="365f2-180">hello overall folder structure for this project should resemble this: ![Google Chrome App - Folder Structure][21]</span></span>

### <a name="set-up-and-test-your-chrome-app"></a><span data-ttu-id="365f2-181">Installation et test de votre application Chrome</span><span class="sxs-lookup"><span data-stu-id="365f2-181">Set up and test your Chrome App</span></span>
1. <span data-ttu-id="365f2-182">Ouvrez votre navigateur Chrome.</span><span class="sxs-lookup"><span data-stu-id="365f2-182">Open your Chrome browser.</span></span> <span data-ttu-id="365f2-183">Ouvrez la page **Extensions** de Chrome et activez **Mode développeur**.</span><span class="sxs-lookup"><span data-stu-id="365f2-183">Open **Chrome extensions** and enable **Developer mode**.</span></span>
   
       ![Google Chrome - Enable Developer Mode][16]
2. <span data-ttu-id="365f2-184">Cliquez sur **de charger l’extension décompressée** et accédez dossier toohello où vous avez créé des fichiers de hello.</span><span class="sxs-lookup"><span data-stu-id="365f2-184">Click **Load unpacked extension** and navigate toohello folder where you created hello files.</span></span> <span data-ttu-id="365f2-185">Vous pouvez également utiliser hello **Chrome applications et outils de développement d’Extensions**.</span><span class="sxs-lookup"><span data-stu-id="365f2-185">You can also optionally use hello **Chrome Apps & Extensions Developer Tool**.</span></span> <span data-ttu-id="365f2-186">Cet outil est une application de Chrome en soi (installée à partir de hello Chrome Web Store) et fournit des fonctionnalités de débogage avancées pour le développement de vos applications de Chrome.</span><span class="sxs-lookup"><span data-stu-id="365f2-186">This tool is a Chrome App in itself (installed from hello Chrome Web Store) and provides advanced debugging capabilities for your Chrome App development.</span></span>
   
       ![Google Chrome - Load Unpacked Extension][17]
3. <span data-ttu-id="365f2-187">Si hello Chrome application est créé sans erreur, puis vous verrez votre application Chrome s’affichent.</span><span class="sxs-lookup"><span data-stu-id="365f2-187">If hello Chrome App is created without any errors, then you will see your Chrome App show up.</span></span>
   
       ![Google Chrome - Chrome App Display][18]
4. <span data-ttu-id="365f2-188">Entrez hello **numéro de projet** que vous avez obtenu précédemment hello **Google Cloud Console** en tant qu’ID d’expéditeur hello, puis cliquez sur **inscrire auprès de GCM**.</span><span class="sxs-lookup"><span data-stu-id="365f2-188">Enter hello **Project Number** that you got earlier from hello **Google Cloud Console** as hello sender ID, and click **Register with GCM**.</span></span> <span data-ttu-id="365f2-189">Vous devez voir le message de type hello **inscription GCM a réussi.**</span><span class="sxs-lookup"><span data-stu-id="365f2-189">You must see hello message **Registration with GCM succeeded.**</span></span>
   
       ![Google Chrome - Chrome App Customization][19]
5. <span data-ttu-id="365f2-190">Entrez votre **nom du concentrateur de Notification** et hello **DefaultListenSharedAccessSignature** que vous avez obtenu de portail hello précédemment, puis cliquez sur **inscrire auprès d’Azure Notification Hub**.</span><span class="sxs-lookup"><span data-stu-id="365f2-190">Enter your **Notification Hub Name** and hello **DefaultListenSharedAccessSignature** that you obtained from hello portal earlier, and click **Register with Azure Notification Hub**.</span></span> <span data-ttu-id="365f2-191">Vous devez voir le message de type hello **inscription de concentrateur de Notification réussie !**</span><span class="sxs-lookup"><span data-stu-id="365f2-191">You must see hello message **Notification Hub Registration successful!**</span></span> <span data-ttu-id="365f2-192">ID de détails hello de réponse d’inscription de hello, qui contient les hello d’inscription d’Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="365f2-192">and hello details of hello registration response, which contains hello Azure Notification Hubs registration ID.</span></span>
   
       ![Google Chrome - Specify Notification Hub Details][20]  

## <span data-ttu-id="365f2-193"><a name="send"></a>Envoyer une notification de tooyour Chrome application</span><span class="sxs-lookup"><span data-stu-id="365f2-193"><a name="send"></a>Send a notification tooyour Chrome App</span></span>
<span data-ttu-id="365f2-194">À des fins de test, nous envoyons des notifications push Chrome à l’aide d’une application de console .NET.</span><span class="sxs-lookup"><span data-stu-id="365f2-194">For testing purposes, we will send Chrome push notifications by using a .NET console application.</span></span> 

> [!NOTE]
> <span data-ttu-id="365f2-195">Vous pouvez envoyer des notifications push en utilisant Notification Hubs à partir d’un serveur principal utilisant notre <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">interface REST</a> publique.</span><span class="sxs-lookup"><span data-stu-id="365f2-195">You can send push notifications with Notification Hubs from any backend via our public <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST interface</a>.</span></span> <span data-ttu-id="365f2-196">Découvrez notre [portail de documentation](https://azure.microsoft.com/documentation/services/notification-hubs/) pour plus d’exemples interplateformes.</span><span class="sxs-lookup"><span data-stu-id="365f2-196">Check out our [documentation portal](https://azure.microsoft.com/documentation/services/notification-hubs/) for more cross-platform examples.</span></span>
> 
> 

1. <span data-ttu-id="365f2-197">Dans Visual Studio, à partir de hello **fichier** menu, sélectionnez **nouveau** , puis **projet**.</span><span class="sxs-lookup"><span data-stu-id="365f2-197">In Visual Studio, from hello **File** menu, select **New** and then **Project**.</span></span> <span data-ttu-id="365f2-198">Sous **Visual C#**, cliquez sur **Windows** et **Application Console**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="365f2-198">Under **Visual C#**, click **Windows** and **Console Application**, and then click **OK**.</span></span>  <span data-ttu-id="365f2-199">Un projet d'application console est créé.</span><span class="sxs-lookup"><span data-stu-id="365f2-199">This creates a new console application project.</span></span>
2. <span data-ttu-id="365f2-200">À partir de hello **outils** menu, cliquez sur **Gestionnaire de Package de bibliothèque** , puis **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="365f2-200">From hello **Tools** menu, click **Library Package Manager** and then **Package Manager Console**.</span></span> <span data-ttu-id="365f2-201">Cette opération affiche hello Console du Gestionnaire de Package.</span><span class="sxs-lookup"><span data-stu-id="365f2-201">This displays hello Package Manager Console.</span></span>
3. <span data-ttu-id="365f2-202">Dans la fenêtre de console hello, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="365f2-202">In hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
       This adds a reference toohello Azure Service Bus SDK with hello <a href="http://nuget.org/packages/  WindowsAzure.ServiceBus/">WindowsAzure.ServiceBus NuGet package</a>.
4. <span data-ttu-id="365f2-203">Ouvrez `Program.cs` et ajoutez hello suit `using` instruction :</span><span class="sxs-lookup"><span data-stu-id="365f2-203">Open `Program.cs` and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="365f2-204">Bonjour `Program` de classe, ajoutez hello suivant de méthode :</span><span class="sxs-lookup"><span data-stu-id="365f2-204">In hello `Program` class, add hello following method:</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            String message = "{\"data\":{\"message\":\"Hello Chrome from Azure Notification Hubs\"}}";
            await hub.SendGcmNativeNotificationAsync(message);
        }
   
       Make sure tooreplace hello `<hub name>` placeholder with hello name of hello notification hub that appears in hello [portal](https://portal.azure.com) in your Notification Hub blade. Also, replace hello connection string placeholder with hello connection string called `DefaultFullSharedAccessSignature` that you obtained in hello notification hub configuration section.
   
   > [!NOTE]
   > <span data-ttu-id="365f2-205">Assurez-vous que vous utilisez avec la chaîne de connexion de hello **complète** accéder, pas **écouter** accès.</span><span class="sxs-lookup"><span data-stu-id="365f2-205">Make sure that you use hello connection string with **Full** access, not **Listen** access.</span></span> <span data-ttu-id="365f2-206">Hello **écouter** chaîne de connexion d’accès à ne pas accorde des autorisations des notifications push de toosend.</span><span class="sxs-lookup"><span data-stu-id="365f2-206">hello **Listen** access connection string does not grant permissions toosend push notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="365f2-207">Ajouter hello suite à des appels Bonjour `Main` méthode :</span><span class="sxs-lookup"><span data-stu-id="365f2-207">Add hello following calls in hello `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="365f2-208">Vérifiez que Chrome est en cours d’exécution et exécuter l’application de console hello.</span><span class="sxs-lookup"><span data-stu-id="365f2-208">Make sure that Chrome is running, and run hello console application.</span></span>
8. <span data-ttu-id="365f2-209">Vous devez voir s’afficher hello notification contextuelle sur votre bureau.</span><span class="sxs-lookup"><span data-stu-id="365f2-209">You should see hello following notification pop up on your desktop.</span></span>
   
       ![Google Chrome - Notification][13]
9. <span data-ttu-id="365f2-210">Vous pouvez également voir toutes vos notifications (dans Windows) à l’aide de la fenêtre de Notifications de Chrome hello dans la barre des tâches hello lorsque Chrome est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="365f2-210">You can also see all your notifications by using hello Chrome Notifications window in hello taskbar (in Windows) when Chrome is running.</span></span>
   
       ![Google Chrome - Notifications List][14]

> [!NOTE]
> <span data-ttu-id="365f2-211">Vous n’avez pas besoin toohave hello Chrome application en cours d’exécution ou ouvrir dans le navigateur hello (même si le navigateur Chrome de hello lui-même doit être en cours d’exécution).</span><span class="sxs-lookup"><span data-stu-id="365f2-211">You don't need toohave hello Chrome App running or open in hello browser (though hello Chrome browser itself must be running).</span></span> <span data-ttu-id="365f2-212">Vous obtenez également une vue consolidée de toutes vos notifications dans la fenêtre de Notifications de Chrome hello.</span><span class="sxs-lookup"><span data-stu-id="365f2-212">You also get a consolidated view of all your notifications in hello Chrome Notifications window.</span></span>
> 
> 

## <span data-ttu-id="365f2-213"><a name="next-steps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="365f2-213"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="365f2-214">En savoir plus sur Notification Hubs dans la [Vue d’ensemble de Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="365f2-214">Learn more about Notification Hubs in [Notification Hubs Overview].</span></span>

<span data-ttu-id="365f2-215">tootarget des utilisateurs spécifiques, consultez toohello [Azure Notification Hubs notifier utilisateurs] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="365f2-215">tootarget specific users, refer toohello [Azure Notification Hubs Notify Users] tutorial.</span></span> 

<span data-ttu-id="365f2-216">Si vous souhaitez toosegment vos utilisateurs en groupes d’intérêt, vous pouvez suivre hello [Azure Notification Hubs actualités] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="365f2-216">If you want toosegment your users by interest groups, you can follow hello [Azure Notification Hubs breaking news] tutorial.</span></span>

<!-- Images. -->
[1]: ./media/notification-hubs-chrome-get-started/GoogleConsoleCreateProject.PNG
[2]: ./media/notification-hubs-chrome-get-started/GoogleProjectNumber.png
[3]: ./media/notification-hubs-chrome-get-started/EnableGCM.png
[4]: ./media/notification-hubs-chrome-get-started/CreateServerKey.png
[5]: ./media/notification-hubs-chrome-get-started/ServerKey.png
[6]: ./media/notification-hubs-chrome-get-started/CreateNH.png
[7]: ./media/notification-hubs-chrome-get-started/NHNamespace.png
[8]: ./media/notification-hubs-chrome-get-started/NamespaceConfigure.png
[9]: ./media/notification-hubs-chrome-get-started/NHConfigure.png
[10]: ./media/notification-hubs-chrome-get-started/NHConfigureGCM.png
[11]: ./media/notification-hubs-chrome-get-started/NHDashboard.png
[12]: ./media/notification-hubs-chrome-get-started/NHConnString.png
[13]: ./media/notification-hubs-chrome-get-started/ChromeNotification.png
[14]: ./media/notification-hubs-chrome-get-started/ChromeNotificationWindow.png
[15]: ./media/notification-hubs-chrome-get-started/ChromeApp.png
[16]: ./media/notification-hubs-chrome-get-started/ChromeExtensions.png
[17]: ./media/notification-hubs-chrome-get-started/ChromeLoadExtension.png
[18]: ./media/notification-hubs-chrome-get-started/ChromeAppLoaded.png
[19]: ./media/notification-hubs-chrome-get-started/ChromeAppGCM.png
[20]: ./media/notification-hubs-chrome-get-started/ChromeAppNH.png
[21]: ./media/notification-hubs-chrome-get-started/FinalFolderView.png

<!-- URLs. -->
[exemple Hub de Notification d’application Chrome]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToChromeApps
[Google Cloud Console]: http://cloud.google.com/console
[Azure Classic Portal]: https://manage.windowsazure.com/
[Vue d’ensemble de Notification Hubs]: notification-hubs-push-notification-overview.md
[vue d’ensemble des applications de Chrome]: https://developer.chrome.com/apps/about_apps
[Chrome application GCM exemple]: https://github.com/GoogleChrome/chrome-app-samples/tree/master/samples/gcm-notifications
[Installable Web Apps]: https://developers.google.com/chrome/apps/docs/
[applications Chrome sur Mobile]: https://developer.chrome.com/apps/chrome_apps_on_mobile
[Création de l’API REST NH d’inscription]: http://msdn.microsoft.com/library/azure/dn223265.aspx
[crypto-js bibliothèque]: http://code.google.com/p/crypto-js/
[GCM with Chrome Apps]: https://developer.chrome.com/apps/cloudMessaging
[de messagerie Cloud Google Chrome]: https://developer.chrome.com/apps/cloudMessagingV1
[Azure Notification Hubs notifier utilisateurs]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[Azure Notification Hubs actualités]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md
