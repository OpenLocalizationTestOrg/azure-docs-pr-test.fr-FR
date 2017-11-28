---
title: "aaaGet main d’Azure Notification Hubs pour les applications Kindle | Documents Microsoft"
description: "Dans ce didacticiel, vous découvrez comment toouse Azure Notification Hubs toosend push application de notifications de Kindle tooa."
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 346fc8e5-294b-4e4f-9f27-7a82d9626e93
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-kindle
ms.devlang: Java
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 7c28d64372cd2d90bab9cd9bf818d333f3478f7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-for-kindle-apps"></a><span data-ttu-id="ef398-103">Prendre en main Notification Hubs pour les applications Kindle</span><span class="sxs-lookup"><span data-stu-id="ef398-103">Get started with Notification Hubs for Kindle apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="ef398-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="ef398-104">Overview</span></span>
<span data-ttu-id="ef398-105">Ce didacticiel vous montre comment toouse Azure Notification Hubs toosend push application de notifications de Kindle tooa.</span><span class="sxs-lookup"><span data-stu-id="ef398-105">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa Kindle application.</span></span>
<span data-ttu-id="ef398-106">Dans ce didacticiel, vous allez créer une application Kindle vierge recevant des notifications Push à l’aide d’Amazon Device Messaging (ADM).</span><span class="sxs-lookup"><span data-stu-id="ef398-106">You'll create a blank Kindle app that receives push notifications by using Amazon Device Messaging (ADM).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ef398-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ef398-107">Prerequisites</span></span>
<span data-ttu-id="ef398-108">Ce didacticiel requiert hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="ef398-108">This tutorial requires hello following:</span></span>

* <span data-ttu-id="ef398-109">Obtenir hello Android SDK (nous supposons que vous allez utiliser Eclipse) à partir de hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">site Android</a>.</span><span class="sxs-lookup"><span data-stu-id="ef398-109">Get hello Android SDK (we assume that you will use Eclipse) from hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android site</a>.</span></span>
* <span data-ttu-id="ef398-110">Suivez les étapes de hello dans <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">paramètre votre environnement de développement</a> tooset de votre environnement de développement pour Kindle.</span><span class="sxs-lookup"><span data-stu-id="ef398-110">Follow hello steps in <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">Setting Up Your Development Environment</a> tooset up your development environment for Kindle.</span></span>

## <a name="add-a-new-app-toohello-developer-portal"></a><span data-ttu-id="ef398-111">Ajouter un nouveau portail des développeurs toohello application</span><span class="sxs-lookup"><span data-stu-id="ef398-111">Add a new app toohello developer portal</span></span>
1. <span data-ttu-id="ef398-112">Tout d’abord, créez une application dans hello [portail des développeurs Amazon].</span><span class="sxs-lookup"><span data-stu-id="ef398-112">First, create an app in hello [Amazon developer portal].</span></span>
   
    ![][0]
2. <span data-ttu-id="ef398-113">Hello de copie **clé d’Application**.</span><span class="sxs-lookup"><span data-stu-id="ef398-113">Copy hello **Application Key**.</span></span>
   
    ![][1]
3. <span data-ttu-id="ef398-114">Dans le portail hello, cliquez sur le nom hello de votre application, puis cliquez sur hello **Device Messaging** onglet.</span><span class="sxs-lookup"><span data-stu-id="ef398-114">In hello portal, click hello name of your app, and then click hello **Device Messaging** tab.</span></span>
   
    ![][2]
4. <span data-ttu-id="ef398-115">Cliquez sur **Create a New Security Profile** (Créer un profil de sécurité), puis créez un profil de sécurité (par exemple, le **profil de sécurité TestAdm**).</span><span class="sxs-lookup"><span data-stu-id="ef398-115">Click **Create a New Security Profile**, and then create a new security profile (for example, **TestAdm security profile**).</span></span> <span data-ttu-id="ef398-116">Cliquez ensuite sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="ef398-116">Then click **Save**.</span></span>
   
    ![][3]
5. <span data-ttu-id="ef398-117">Cliquez sur **profils de sécurité** tooview hello sécurité profil que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="ef398-117">Click **Security Profiles** tooview hello security profile that you just created.</span></span> <span data-ttu-id="ef398-118">Hello de copie **ID Client** et **clé secrète Client** valeurs pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="ef398-118">Copy hello **Client ID** and **Client Secret** values for later use.</span></span>
   
    ![][4]

## <a name="create-an-api-key"></a><span data-ttu-id="ef398-119">Création d'une clé API</span><span class="sxs-lookup"><span data-stu-id="ef398-119">Create an API key</span></span>
1. <span data-ttu-id="ef398-120">Ouvrez une invite de commandes avec les privilèges Administrateur.</span><span class="sxs-lookup"><span data-stu-id="ef398-120">Open a command prompt with administrator privileges.</span></span>
2. <span data-ttu-id="ef398-121">Parcourir le dossier du Kit de développement logiciel Android toohello.</span><span class="sxs-lookup"><span data-stu-id="ef398-121">Navigate toohello Android SDK folder.</span></span>
3. <span data-ttu-id="ef398-122">Entrez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ef398-122">Enter hello following command:</span></span>
   
        keytool -list -v -alias androiddebugkey -keystore ./debug.keystore
   
    ![][5]
4. <span data-ttu-id="ef398-123">Pourquoi **keystore** mot de passe, tapez **android**.</span><span class="sxs-lookup"><span data-stu-id="ef398-123">For hello **keystore** password, type **android**.</span></span>
5. <span data-ttu-id="ef398-124">Hello de copie **MD5** empreintes digitales.</span><span class="sxs-lookup"><span data-stu-id="ef398-124">Copy hello **MD5** fingerprint.</span></span>
6. <span data-ttu-id="ef398-125">Dans le portail des développeurs hello, sur hello **messagerie** , cliquez sur **Android/Kindle** et entrez le nom hello du package de hello pour votre application (par exemple, **com.sample.notificationhubtest**) et hello **MD5** valeur, puis cliquez sur **générer une clé API**.</span><span class="sxs-lookup"><span data-stu-id="ef398-125">Back in hello developer portal, on hello **Messaging** tab, click **Android/Kindle** and enter hello name of hello package for your app (for example, **com.sample.notificationhubtest**) and hello **MD5** value, and then click **Generate API Key**.</span></span>

## <a name="add-credentials-toohello-hub"></a><span data-ttu-id="ef398-126">Ajouter le concentrateur toohello d’informations d’identification</span><span class="sxs-lookup"><span data-stu-id="ef398-126">Add credentials toohello hub</span></span>
<span data-ttu-id="ef398-127">Dans le portail hello, ajouter hello client secret et le client ID toohello **configurer** onglet de votre concentrateur de notification.</span><span class="sxs-lookup"><span data-stu-id="ef398-127">In hello portal, add hello client secret and client ID toohello **Configure** tab of your notification hub.</span></span>

## <a name="set-up-your-application"></a><span data-ttu-id="ef398-128">Configuration de votre application</span><span class="sxs-lookup"><span data-stu-id="ef398-128">Set up your application</span></span>
> [!NOTE]
> <span data-ttu-id="ef398-129">Lors de la création d’une application, utilisez au moins l’API de niveau 17.</span><span class="sxs-lookup"><span data-stu-id="ef398-129">When you're creating an application, use at least API Level 17.</span></span>
> 
> 

<span data-ttu-id="ef398-130">Ajouter le projet Eclipse tooyour hello ADM bibliothèques :</span><span class="sxs-lookup"><span data-stu-id="ef398-130">Add hello ADM libraries tooyour Eclipse project:</span></span>

1. <span data-ttu-id="ef398-131">bibliothèque de tooobtain hello ADM, [télécharger hello SDK].</span><span class="sxs-lookup"><span data-stu-id="ef398-131">tooobtain hello ADM library, [download hello SDK].</span></span> <span data-ttu-id="ef398-132">Extrayez le fichier zip du SDK hello.</span><span class="sxs-lookup"><span data-stu-id="ef398-132">Extract hello SDK zip file.</span></span>
2. <span data-ttu-id="ef398-133">Dans Eclipse, cliquez avec le bouton droit sur votre projet, puis cliquez sur **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="ef398-133">In Eclipse, right-click your project, and then click **Properties**.</span></span> <span data-ttu-id="ef398-134">Sélectionnez **chemin d’accès de Build Java** sur hello gauche, puis sélectionnez hello ** bibliothèques ** onglet en haut de hello.</span><span class="sxs-lookup"><span data-stu-id="ef398-134">Select **Java Build Path** on hello left, and then select hello **Libraries **tab at hello top.</span></span> <span data-ttu-id="ef398-135">Cliquez sur **ajouter le Jar externe**et sélectionnez hello fichier `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` à partir du répertoire hello dans lequel vous avez extrait hello Amazon SDK.</span><span class="sxs-lookup"><span data-stu-id="ef398-135">Click **Add External Jar**, and select hello file `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` from hello directory in which you extracted hello Amazon SDK.</span></span>
3. <span data-ttu-id="ef398-136">Téléchargez hello NotificationHubs Android SDK (lien).</span><span class="sxs-lookup"><span data-stu-id="ef398-136">Download hello NotificationHubs Android SDK (link).</span></span>
4. <span data-ttu-id="ef398-137">Décompressez le package de hello, puis faites glisser le fichier de hello `notification-hubs-sdk.jar` dans hello `libs` dossier dans Eclipse.</span><span class="sxs-lookup"><span data-stu-id="ef398-137">Unzip hello package, and then drag hello file `notification-hubs-sdk.jar` into hello `libs` folder in Eclipse.</span></span>

<span data-ttu-id="ef398-138">Modifiez votre toosupport de manifeste d’application ADM :</span><span class="sxs-lookup"><span data-stu-id="ef398-138">Edit your app manifest toosupport ADM:</span></span>

1. <span data-ttu-id="ef398-139">Ajoutez hello Amazon espace de noms dans l’élément de manifeste hello racine :</span><span class="sxs-lookup"><span data-stu-id="ef398-139">Add hello Amazon namespace in hello root manifest element:</span></span>

        xmlns:amazon="http://schemas.amazon.com/apk/res/android"

1. <span data-ttu-id="ef398-140">Ajouter des autorisations en tant que premier élément de hello sous l’élément manifeste hello.</span><span class="sxs-lookup"><span data-stu-id="ef398-140">Add permissions as hello first element under hello manifest element.</span></span> <span data-ttu-id="ef398-141">Substitution **[votre nom de PACKAGE]** avec package hello que vous avez utilisé toocreate votre application.</span><span class="sxs-lookup"><span data-stu-id="ef398-141">Substitute **[YOUR PACKAGE NAME]** with hello package that you used toocreate your app.</span></span>
   
        <permission
         android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE"
         android:protectionLevel="signature" />
   
        <uses-permission android:name="android.permission.INTERNET"/>
   
        <uses-permission android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE" />
   
        <!-- This permission allows your app access tooreceive push notifications
        from ADM. -->
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE" />
   
        <!-- ADM uses WAKE_LOCK tookeep hello processor from sleeping when a message is received. -->
        <uses-permission android:name="android.permission.WAKE_LOCK" />
2. <span data-ttu-id="ef398-142">Insérez hello suit l’élément en tant que premier enfant de hello hello d’élément d’application.</span><span class="sxs-lookup"><span data-stu-id="ef398-142">Insert hello following element as hello first child of hello application element.</span></span> <span data-ttu-id="ef398-143">N’oubliez pas de toosubstitute **[votre nom de SERVICE]** avec nom hello de votre gestionnaire de messages ADM qui vous créez dans la section suivante de hello (package de hello, y compris), puis remplacez **[votre nom de PACKAGE]** avec hello nom du package avec lequel vous avez créé votre application.</span><span class="sxs-lookup"><span data-stu-id="ef398-143">Remember toosubstitute **[YOUR SERVICE NAME]** with hello name of your ADM message handler that you create in hello next section (including hello package), and replace **[YOUR PACKAGE NAME]** with hello package name with which you created your app.</span></span>
   
        <amazon:enable-feature
              android:name="com.amazon.device.messaging"
                     android:required="true"/>
        <service
            android:name="[YOUR SERVICE NAME]"
            android:exported="false" />
   
        <receiver
            android:name="[YOUR SERVICE NAME]$Receiver" />
   
            <!-- This permission ensures that only ADM can send your app registration broadcasts. -->
            android:permission="com.amazon.device.messaging.permission.SEND" >
   
            <!-- toointeract with ADM, your app must listen for hello following intents. -->
            <intent-filter>
          <action android:name="com.amazon.device.messaging.intent.REGISTRATION" />
          <action android:name="com.amazon.device.messaging.intent.RECEIVE" />
   
          <!-- Replace hello name in hello category tag with your app's package name. -->
          <category android:name="[YOUR PACKAGE NAME]" />
            </intent-filter>
        </receiver>

## <a name="create-your-adm-message-handler"></a><span data-ttu-id="ef398-144">Création de votre gestionnaire de messages ADM</span><span class="sxs-lookup"><span data-stu-id="ef398-144">Create your ADM message handler</span></span>
1. <span data-ttu-id="ef398-145">Créez une classe qui hérite de `com.amazon.device.messaging.ADMMessageHandlerBase` et nommez-le `MyADMMessageHandler`, comme illustré dans la figure suivante de hello :</span><span class="sxs-lookup"><span data-stu-id="ef398-145">Create a new class that inherits from `com.amazon.device.messaging.ADMMessageHandlerBase` and name it `MyADMMessageHandler`, as shown in hello following figure:</span></span>
   
    ![][6]
2. <span data-ttu-id="ef398-146">Ajoutez hello suit `import` instructions :</span><span class="sxs-lookup"><span data-stu-id="ef398-146">Add hello following `import` statements:</span></span>
   
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.support.v4.app.NotificationCompat;
        import com.amazon.device.messaging.ADMMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub
3. <span data-ttu-id="ef398-147">Ajoutez hello suivant le code de classe hello que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="ef398-147">Add hello following code in hello class that you created.</span></span> <span data-ttu-id="ef398-148">N’oubliez pas de toosubstitute hello hub nom et une connexion chaîne (écoute) :</span><span class="sxs-lookup"><span data-stu-id="ef398-148">Remember toosubstitute hello hub name and connection string (listen):</span></span>
   
        public static final int NOTIFICATION_ID = 1;
        private NotificationManager mNotificationManager;
        NotificationCompat.Builder builder;
          private static NotificationHub hub;
        public static NotificationHub getNotificationHub(Context context) {
            Log.v("com.wa.hellokindlefire", "getNotificationHub");
            if (hub == null) {
                hub = new NotificationHub("[hub name]", "[listen connection string]", context);
            }
            return hub;
        }
   
        public MyADMMessageHandler() {
                super("MyADMMessageHandler");
            }
   
            public static class Receiver extends ADMMessageReceiver
            {
                public Receiver()
                {
                    super(MyADMMessageHandler.class);
                }
            }
   
            private void sendNotification(String msg) {
                Context ctx = getApplicationContext();
   
                mNotificationManager = (NotificationManager)
                    ctx.getSystemService(Context.NOTIFICATION_SERVICE);
   
            PendingIntent contentIntent = PendingIntent.getActivity(ctx, 0,
                  new Intent(ctx, MainActivity.class), 0);
   
            NotificationCompat.Builder mBuilder =
                  new NotificationCompat.Builder(ctx)
                  .setSmallIcon(R.mipmap.ic_launcher)
                  .setContentTitle("Notification Hub Demo")
                  .setStyle(new NotificationCompat.BigTextStyle()
                         .bigText(msg))
                  .setContentText(msg);
   
             mBuilder.setContentIntent(contentIntent);
             mNotificationManager.notify(NOTIFICATION_ID, mBuilder.build());
        }
4. <span data-ttu-id="ef398-149">Ajouter hello suivant code toohello `OnMessage()` méthode :</span><span class="sxs-lookup"><span data-stu-id="ef398-149">Add hello following code toohello `OnMessage()` method:</span></span>
   
        String nhMessage = intent.getExtras().getString("msg");
        sendNotification(nhMessage);
5. <span data-ttu-id="ef398-150">Ajouter hello suivant code toohello `OnRegistered` méthode :</span><span class="sxs-lookup"><span data-stu-id="ef398-150">Add hello following code toohello `OnRegistered` method:</span></span>
   
            try {
        getNotificationHub(getApplicationContext()).register(registrationId);
            } catch (Exception e) {
        Log.e("[your package name]", "Fail onRegister: " + e.getMessage(), e);
            }
6. <span data-ttu-id="ef398-151">Ajouter hello suivant code toohello `OnUnregistered` méthode :</span><span class="sxs-lookup"><span data-stu-id="ef398-151">Add hello following code toohello `OnUnregistered` method:</span></span>
   
         try {
             getNotificationHub(getApplicationContext()).unregister();
         } catch (Exception e) {
             Log.e("[your package name]", "Fail onUnregister: " + e.getMessage(), e);
         }
7. <span data-ttu-id="ef398-152">Bonjour `MainActivity` (méthode), ajouter hello après l’instruction d’importation :</span><span class="sxs-lookup"><span data-stu-id="ef398-152">In hello `MainActivity` method, add hello following import statement:</span></span>
   
        import com.amazon.device.messaging.ADM;
8. <span data-ttu-id="ef398-153">Ajouter hello suivant du code à la fin de hello de hello `OnCreate` méthode :</span><span class="sxs-lookup"><span data-stu-id="ef398-153">Add hello following code at hello end of hello `OnCreate` method:</span></span>
   
        final ADM adm = new ADM(this);
        if (adm.getRegistrationId() == null)
        {
           adm.startRegister();
        } else {
            new AsyncTask() {
                  @Override
                  protected Object doInBackground(Object... params) {
                     try {                         MyADMMessageHandler.getNotificationHub(getApplicationContext()).register(adm.getRegistrationId());
                     } catch (Exception e) {
                         Log.e("com.wa.hellokindlefire", "Failed registration with hub", e);
                         return e;
                     }
                     return null;
                 }
               }.execute(null, null, null);
        }

## <a name="add-your-api-key-tooyour-app"></a><span data-ttu-id="ef398-154">Ajouter votre application de tooyour clé API</span><span class="sxs-lookup"><span data-stu-id="ef398-154">Add your API key tooyour app</span></span>
1. <span data-ttu-id="ef398-155">Dans Eclipse, créez un nouveau fichier nommé **api_key.txt** dans les ressources de répertoire hello de votre projet.</span><span class="sxs-lookup"><span data-stu-id="ef398-155">In Eclipse, create a new file named **api_key.txt** in hello directory assets of your project.</span></span>
2. <span data-ttu-id="ef398-156">Ouvrez hello fichier et copiez hello clé d’API que vous avez généré dans le portail des développeurs Amazon hello.</span><span class="sxs-lookup"><span data-stu-id="ef398-156">Open hello file and copy hello API key that you generated in hello Amazon developer portal.</span></span>

## <a name="run-hello-app"></a><span data-ttu-id="ef398-157">Exécutez l’application hello</span><span class="sxs-lookup"><span data-stu-id="ef398-157">Run hello app</span></span>
1. <span data-ttu-id="ef398-158">Démarrer l’émulateur de hello.</span><span class="sxs-lookup"><span data-stu-id="ef398-158">Start hello emulator.</span></span>
2. <span data-ttu-id="ef398-159">Dans l’émulateur de hello, faites glisser à partir du haut de hello et cliquez sur **paramètres**, puis cliquez sur **mon compte** et l’inscrire avec un compte Amazon valide.</span><span class="sxs-lookup"><span data-stu-id="ef398-159">In hello emulator, swipe from hello top and click **Settings**, and then click **My account** and register with a valid Amazon account.</span></span>
3. <span data-ttu-id="ef398-160">Dans Eclipse, exécutez l’application hello.</span><span class="sxs-lookup"><span data-stu-id="ef398-160">In Eclipse, run hello app.</span></span>

> [!NOTE]
> <span data-ttu-id="ef398-161">Si un problème se produit, vérifie hello d’émulateur de hello (ou périphérique).</span><span class="sxs-lookup"><span data-stu-id="ef398-161">If a problem occurs, check hello time of hello emulator (or device).</span></span> <span data-ttu-id="ef398-162">valeur d’heure Hello doit être exact.</span><span class="sxs-lookup"><span data-stu-id="ef398-162">hello time value must be accurate.</span></span> <span data-ttu-id="ef398-163">temps de hello toochange de l’émulateur de Kindle hello, vous pouvez exécuter hello commande à partir de votre répertoire d’outils de plateforme du SDK Android suivante :</span><span class="sxs-lookup"><span data-stu-id="ef398-163">toochange hello time of hello Kindle emulator, you can run hello following command from your Android SDK platform-tools directory:</span></span>
> 
> 

        adb shell  date -s "yyyymmdd.hhmmss"

## <a name="send-a-message"></a><span data-ttu-id="ef398-164">Envoyer un message</span><span class="sxs-lookup"><span data-stu-id="ef398-164">Send a message</span></span>
<span data-ttu-id="ef398-165">toosend un message à l’aide de .NET :</span><span class="sxs-lookup"><span data-stu-id="ef398-165">toosend a message by using .NET:</span></span>

        static void Main(string[] args)
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("[conn string]", "[hub name]");

            hub.SendAdmNativeNotificationAsync("{\"data\":{\"msg\" : \"Hello from .NET!\"}}").Wait();
        }

![][7]

<!-- URLs. -->
[portail des développeurs Amazon]: https://developer.amazon.com/home.html
[télécharger hello SDK]: https://developer.amazon.com/public/resources/development-tools/sdk

[0]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal1.png
[1]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal2.png
[2]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal3.png
[3]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal4.png
[4]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal5.png
[5]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-cmd-window.png
[6]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-new-java-class.png
[7]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-notification.png
