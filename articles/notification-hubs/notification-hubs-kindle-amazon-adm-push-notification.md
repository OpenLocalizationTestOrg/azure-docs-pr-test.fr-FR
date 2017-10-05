---
title: "Bien démarrer avec Azure Notification Hubs pour les applications Kindle | Microsoft Docs"
description: Ce didacticiel montre comment utiliser Azure Notification Hubs pour envoyer des notifications Push vers une application Kindle.
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
ms.openlocfilehash: 7206f152ed7270abc62536a9ee164f7227833bcc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-notification-hubs-for-kindle-apps"></a><span data-ttu-id="cf915-103">Prendre en main Notification Hubs pour les applications Kindle</span><span class="sxs-lookup"><span data-stu-id="cf915-103">Get started with Notification Hubs for Kindle apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="cf915-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="cf915-104">Overview</span></span>
<span data-ttu-id="cf915-105">Ce didacticiel vous montre comment utiliser Azure Notification Hubs pour envoyer des notifications Push vers une application Kindle.</span><span class="sxs-lookup"><span data-stu-id="cf915-105">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a Kindle application.</span></span>
<span data-ttu-id="cf915-106">Dans ce didacticiel, vous allez créer une application Kindle vierge recevant des notifications Push à l’aide d’Amazon Device Messaging (ADM).</span><span class="sxs-lookup"><span data-stu-id="cf915-106">You'll create a blank Kindle app that receives push notifications by using Amazon Device Messaging (ADM).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cf915-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="cf915-107">Prerequisites</span></span>
<span data-ttu-id="cf915-108">Ce didacticiel requiert les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="cf915-108">This tutorial requires the following:</span></span>

* <span data-ttu-id="cf915-109">Obtenir le Kit de développement logiciel Android (nous supposons que vous utiliserez Eclipse) depuis le <a href="http://go.microsoft.com/fwlink/?LinkId=389797">site Android</a>.</span><span class="sxs-lookup"><span data-stu-id="cf915-109">Get the Android SDK (we assume that you will use Eclipse) from the <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android site</a>.</span></span>
* <span data-ttu-id="cf915-110">Suivez les étapes de <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">Configuration de votre environnement de développement</a> pour configurer votre environnement de développement pour Kindle.</span><span class="sxs-lookup"><span data-stu-id="cf915-110">Follow the steps in <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">Setting Up Your Development Environment</a> to set up your development environment for Kindle.</span></span>

## <a name="add-a-new-app-to-the-developer-portal"></a><span data-ttu-id="cf915-111">Ajout d'une nouvelle application au portail des développeurs</span><span class="sxs-lookup"><span data-stu-id="cf915-111">Add a new app to the developer portal</span></span>
1. <span data-ttu-id="cf915-112">Tout d’abord, créez une application dans le [portail des développeurs Amazon].</span><span class="sxs-lookup"><span data-stu-id="cf915-112">First, create an app in the [Amazon developer portal].</span></span>
   
    ![][0]
2. <span data-ttu-id="cf915-113">Copiez la **clé d'application**.</span><span class="sxs-lookup"><span data-stu-id="cf915-113">Copy the **Application Key**.</span></span>
   
    ![][1]
3. <span data-ttu-id="cf915-114">Dans le portail, cliquez sur le nom de votre application, puis cliquez sur l’onglet **Device Messaging** .</span><span class="sxs-lookup"><span data-stu-id="cf915-114">In the portal, click the name of your app, and then click the **Device Messaging** tab.</span></span>
   
    ![][2]
4. <span data-ttu-id="cf915-115">Cliquez sur **Create a New Security Profile** (Créer un profil de sécurité), puis créez un profil de sécurité (par exemple, le **profil de sécurité TestAdm**).</span><span class="sxs-lookup"><span data-stu-id="cf915-115">Click **Create a New Security Profile**, and then create a new security profile (for example, **TestAdm security profile**).</span></span> <span data-ttu-id="cf915-116">Cliquez ensuite sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="cf915-116">Then click **Save**.</span></span>
   
    ![][3]
5. <span data-ttu-id="cf915-117">Cliquez sur **Profils de sécurité** pour afficher le profil de sécurité que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="cf915-117">Click **Security Profiles** to view the security profile that you just created.</span></span> <span data-ttu-id="cf915-118">Copiez les valeurs des champs **Client ID** (ID client) et **Client Secret** (Clé secrète client) pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="cf915-118">Copy the **Client ID** and **Client Secret** values for later use.</span></span>
   
    ![][4]

## <a name="create-an-api-key"></a><span data-ttu-id="cf915-119">Création d'une clé API</span><span class="sxs-lookup"><span data-stu-id="cf915-119">Create an API key</span></span>
1. <span data-ttu-id="cf915-120">Ouvrez une invite de commandes avec les privilèges Administrateur.</span><span class="sxs-lookup"><span data-stu-id="cf915-120">Open a command prompt with administrator privileges.</span></span>
2. <span data-ttu-id="cf915-121">Accédez au dossier du Kit de développement logiciel (SDK) Android</span><span class="sxs-lookup"><span data-stu-id="cf915-121">Navigate to the Android SDK folder.</span></span>
3. <span data-ttu-id="cf915-122">Entrez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="cf915-122">Enter the following command:</span></span>
   
        keytool -list -v -alias androiddebugkey -keystore ./debug.keystore
   
    ![][5]
4. <span data-ttu-id="cf915-123">Pour le mot de passe **keystore**, tapez **android**.</span><span class="sxs-lookup"><span data-stu-id="cf915-123">For the **keystore** password, type **android**.</span></span>
5. <span data-ttu-id="cf915-124">Copiez l'empreinte digitale **MD5** .</span><span class="sxs-lookup"><span data-stu-id="cf915-124">Copy the **MD5** fingerprint.</span></span>
6. <span data-ttu-id="cf915-125">De retour dans le portail des développeurs, sous l’onglet **Messaging** (Messagerie), cliquez sur **Android/Kindle** et entrez le nom du package correspondant à votre application (par exemple, **com.sample.notificationhubtest**) ainsi que la valeur **MD5**, puis cliquez sur **Generate API Key** (Générer la clé API).</span><span class="sxs-lookup"><span data-stu-id="cf915-125">Back in the developer portal, on the **Messaging** tab, click **Android/Kindle** and enter the name of the package for your app (for example, **com.sample.notificationhubtest**) and the **MD5** value, and then click **Generate API Key**.</span></span>

## <a name="add-credentials-to-the-hub"></a><span data-ttu-id="cf915-126">Ajout d’informations d’identification au hub</span><span class="sxs-lookup"><span data-stu-id="cf915-126">Add credentials to the hub</span></span>
<span data-ttu-id="cf915-127">Dans le portail, ajoutez la clé secrète client et l’ID client à l’onglet **Configurer** de votre Notification Hub.</span><span class="sxs-lookup"><span data-stu-id="cf915-127">In the portal, add the client secret and client ID to the **Configure** tab of your notification hub.</span></span>

## <a name="set-up-your-application"></a><span data-ttu-id="cf915-128">Configuration de votre application</span><span class="sxs-lookup"><span data-stu-id="cf915-128">Set up your application</span></span>
> [!NOTE]
> <span data-ttu-id="cf915-129">Lors de la création d’une application, utilisez au moins l’API de niveau 17.</span><span class="sxs-lookup"><span data-stu-id="cf915-129">When you're creating an application, use at least API Level 17.</span></span>
> 
> 

<span data-ttu-id="cf915-130">Ajoutez les bibliothèques ADM à votre projet Eclipse :</span><span class="sxs-lookup"><span data-stu-id="cf915-130">Add the ADM libraries to your Eclipse project:</span></span>

1. <span data-ttu-id="cf915-131">Pour obtenir la bibliothèque ADM, [téléchargez le Kit de développement logiciel (SDK)].</span><span class="sxs-lookup"><span data-stu-id="cf915-131">To obtain the ADM library, [download the SDK].</span></span> <span data-ttu-id="cf915-132">Extrayez le fichier zip du Kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="cf915-132">Extract the SDK zip file.</span></span>
2. <span data-ttu-id="cf915-133">Dans Eclipse, cliquez avec le bouton droit sur votre projet, puis cliquez sur **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="cf915-133">In Eclipse, right-click your project, and then click **Properties**.</span></span> <span data-ttu-id="cf915-134">Sélectionnez **chemin d’accès de Build Java** sur la gauche, puis sélectionnez le ** bibliothèques ** onglet en haut.</span><span class="sxs-lookup"><span data-stu-id="cf915-134">Select **Java Build Path** on the left, and then select the **Libraries **tab at the top.</span></span> <span data-ttu-id="cf915-135">Cliquez sur **Add External Jar** (Ajouter un fichier Jar externe) et sélectionnez le fichier `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` dans le répertoire dans lequel vous avez extrait le SDK Amazon.</span><span class="sxs-lookup"><span data-stu-id="cf915-135">Click **Add External Jar**, and select the file `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` from the directory in which you extracted the Amazon SDK.</span></span>
3. <span data-ttu-id="cf915-136">Téléchargez le Kit de développement logiciel (SDK) Android Notification Hubs (lien).</span><span class="sxs-lookup"><span data-stu-id="cf915-136">Download the NotificationHubs Android SDK (link).</span></span>
4. <span data-ttu-id="cf915-137">Décompressez le package, puis faites glisser le fichier `notification-hubs-sdk.jar` dans le dossier `libs` dans Eclipse.</span><span class="sxs-lookup"><span data-stu-id="cf915-137">Unzip the package, and then drag the file `notification-hubs-sdk.jar` into the `libs` folder in Eclipse.</span></span>

<span data-ttu-id="cf915-138">Modifiez le manifeste de l'application afin qu'il prenne en charge ADM :</span><span class="sxs-lookup"><span data-stu-id="cf915-138">Edit your app manifest to support ADM:</span></span>

1. <span data-ttu-id="cf915-139">Ajoutez l'espace de noms Amazon dans l'élément du manifeste racine :</span><span class="sxs-lookup"><span data-stu-id="cf915-139">Add the Amazon namespace in the root manifest element:</span></span>

        xmlns:amazon="http://schemas.amazon.com/apk/res/android"

1. <span data-ttu-id="cf915-140">Ajoutez les autorisations comme le premier élément sous l'élément du manifeste.</span><span class="sxs-lookup"><span data-stu-id="cf915-140">Add permissions as the first element under the manifest element.</span></span> <span data-ttu-id="cf915-141">Remplacez **[VOTRE NOM DE PACKAGE]** par le package utilisé pour créer votre application.</span><span class="sxs-lookup"><span data-stu-id="cf915-141">Substitute **[YOUR PACKAGE NAME]** with the package that you used to create your app.</span></span>
   
        <permission
         android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE"
         android:protectionLevel="signature" />
   
        <uses-permission android:name="android.permission.INTERNET"/>
   
        <uses-permission android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE" />
   
        <!-- This permission allows your app access to receive push notifications
        from ADM. -->
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE" />
   
        <!-- ADM uses WAKE_LOCK to keep the processor from sleeping when a message is received. -->
        <uses-permission android:name="android.permission.WAKE_LOCK" />
2. <span data-ttu-id="cf915-142">Insérez l'élément suivant comme le premier enfant de l'élément de l'application.</span><span class="sxs-lookup"><span data-stu-id="cf915-142">Insert the following element as the first child of the application element.</span></span> <span data-ttu-id="cf915-143">N’oubliez pas de remplacer **[YOUR SERVICE NAME]** par le nom de votre gestionnaire de messages ADM que vous créez dans la section suivante (y compris le package), puis remplacez **[YOUR PACKAGE NAME]** par le nom de package avec lequel vous avez créé votre application.</span><span class="sxs-lookup"><span data-stu-id="cf915-143">Remember to substitute **[YOUR SERVICE NAME]** with the name of your ADM message handler that you create in the next section (including the package), and replace **[YOUR PACKAGE NAME]** with the package name with which you created your app.</span></span>
   
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
   
            <!-- To interact with ADM, your app must listen for the following intents. -->
            <intent-filter>
          <action android:name="com.amazon.device.messaging.intent.REGISTRATION" />
          <action android:name="com.amazon.device.messaging.intent.RECEIVE" />
   
          <!-- Replace the name in the category tag with your app's package name. -->
          <category android:name="[YOUR PACKAGE NAME]" />
            </intent-filter>
        </receiver>

## <a name="create-your-adm-message-handler"></a><span data-ttu-id="cf915-144">Création de votre gestionnaire de messages ADM</span><span class="sxs-lookup"><span data-stu-id="cf915-144">Create your ADM message handler</span></span>
1. <span data-ttu-id="cf915-145">Créez une classe qui hérite de `com.amazon.device.messaging.ADMMessageHandlerBase` et nommez-la `MyADMMessageHandler`, comme indiqué dans la figure suivante :</span><span class="sxs-lookup"><span data-stu-id="cf915-145">Create a new class that inherits from `com.amazon.device.messaging.ADMMessageHandlerBase` and name it `MyADMMessageHandler`, as shown in the following figure:</span></span>
   
    ![][6]
2. <span data-ttu-id="cf915-146">Ajoutez les instructions `import` suivantes :</span><span class="sxs-lookup"><span data-stu-id="cf915-146">Add the following `import` statements:</span></span>
   
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.support.v4.app.NotificationCompat;
        import com.amazon.device.messaging.ADMMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub
3. <span data-ttu-id="cf915-147">Ajoutez le code suivant dans la classe que vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="cf915-147">Add the following code in the class that you created.</span></span> <span data-ttu-id="cf915-148">N’oubliez pas de remplacer le nom du hub et la chaîne de connexion (écoute) :</span><span class="sxs-lookup"><span data-stu-id="cf915-148">Remember to substitute the hub name and connection string (listen):</span></span>
   
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
4. <span data-ttu-id="cf915-149">Ajoutez le code suivant à la méthode `OnMessage()` :</span><span class="sxs-lookup"><span data-stu-id="cf915-149">Add the following code to the `OnMessage()` method:</span></span>
   
        String nhMessage = intent.getExtras().getString("msg");
        sendNotification(nhMessage);
5. <span data-ttu-id="cf915-150">Ajoutez le code suivant à la méthode `OnRegistered` :</span><span class="sxs-lookup"><span data-stu-id="cf915-150">Add the following code to the `OnRegistered` method:</span></span>
   
            try {
        getNotificationHub(getApplicationContext()).register(registrationId);
            } catch (Exception e) {
        Log.e("[your package name]", "Fail onRegister: " + e.getMessage(), e);
            }
6. <span data-ttu-id="cf915-151">Ajoutez le code suivant à la méthode `OnUnregistered` :</span><span class="sxs-lookup"><span data-stu-id="cf915-151">Add the following code to the `OnUnregistered` method:</span></span>
   
         try {
             getNotificationHub(getApplicationContext()).unregister();
         } catch (Exception e) {
             Log.e("[your package name]", "Fail onUnregister: " + e.getMessage(), e);
         }
7. <span data-ttu-id="cf915-152">Dans la méthode `MainActivity` , ajoutez ensuite l’instruction d’importation suivante :</span><span class="sxs-lookup"><span data-stu-id="cf915-152">In the `MainActivity` method, add the following import statement:</span></span>
   
        import com.amazon.device.messaging.ADM;
8. <span data-ttu-id="cf915-153">Ajoutez le code suivant à la fin de la méthode `OnCreate` :</span><span class="sxs-lookup"><span data-stu-id="cf915-153">Add the following code at the end of the `OnCreate` method:</span></span>
   
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

## <a name="add-your-api-key-to-your-app"></a><span data-ttu-id="cf915-154">Ajout de la clé API à votre application</span><span class="sxs-lookup"><span data-stu-id="cf915-154">Add your API key to your app</span></span>
1. <span data-ttu-id="cf915-155">Dans Eclipse, créez un fichier nommé **api_key.txt** dans les composants de répertoire de votre projet.</span><span class="sxs-lookup"><span data-stu-id="cf915-155">In Eclipse, create a new file named **api_key.txt** in the directory assets of your project.</span></span>
2. <span data-ttu-id="cf915-156">Ouvrez le fichier et copiez la clé API que vous avez générée dans le portail des développeurs Amazon.</span><span class="sxs-lookup"><span data-stu-id="cf915-156">Open the file and copy the API key that you generated in the Amazon developer portal.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="cf915-157">Exécution de l'application</span><span class="sxs-lookup"><span data-stu-id="cf915-157">Run the app</span></span>
1. <span data-ttu-id="cf915-158">Démarrez l'émulateur.</span><span class="sxs-lookup"><span data-stu-id="cf915-158">Start the emulator.</span></span>
2. <span data-ttu-id="cf915-159">Dans l’émulateur, balayez l’écran à partir du haut et cliquez sur **Settings** (Paramètres), puis sur **My account** (Mon compte), et inscrivez-vous avec un compte Amazon valide.</span><span class="sxs-lookup"><span data-stu-id="cf915-159">In the emulator, swipe from the top and click **Settings**, and then click **My account** and register with a valid Amazon account.</span></span>
3. <span data-ttu-id="cf915-160">Dans Eclipse, exécutez l'application.</span><span class="sxs-lookup"><span data-stu-id="cf915-160">In Eclipse, run the app.</span></span>

> [!NOTE]
> <span data-ttu-id="cf915-161">Si un problème se produit, vérifiez l'heure de l'émulateur (ou de l'appareil).</span><span class="sxs-lookup"><span data-stu-id="cf915-161">If a problem occurs, check the time of the emulator (or device).</span></span> <span data-ttu-id="cf915-162">L'heure doit être exacte.</span><span class="sxs-lookup"><span data-stu-id="cf915-162">The time value must be accurate.</span></span> <span data-ttu-id="cf915-163">Pour modifier l'heure de l'émulateur Kindle, vous pouvez exécuter la commande suivante depuis le répertoire des outils de plateforme du Kit de développement logiciel (SDK) Android :</span><span class="sxs-lookup"><span data-stu-id="cf915-163">To change the time of the Kindle emulator, you can run the following command from your Android SDK platform-tools directory:</span></span>
> 
> 

        adb shell  date -s "yyyymmdd.hhmmss"

## <a name="send-a-message"></a><span data-ttu-id="cf915-164">Envoi d'un message</span><span class="sxs-lookup"><span data-stu-id="cf915-164">Send a message</span></span>
<span data-ttu-id="cf915-165">Pour envoyer un message avec .NET :</span><span class="sxs-lookup"><span data-stu-id="cf915-165">To send a message by using .NET:</span></span>

        static void Main(string[] args)
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("[conn string]", "[hub name]");

            hub.SendAdmNativeNotificationAsync("{\"data\":{\"msg\" : \"Hello from .NET!\"}}").Wait();
        }

![][7]

<!-- URLs. -->
<span data-ttu-id="cf915-166">[portail des développeurs Amazon]: https://developer.amazon.com/home.html</span><span class="sxs-lookup"><span data-stu-id="cf915-166">[Amazon developer portal]: https://developer.amazon.com/home.html</span></span>
<span data-ttu-id="cf915-167">[téléchargez le Kit de développement logiciel (SDK)]: https://developer.amazon.com/public/resources/development-tools/sdk</span><span class="sxs-lookup"><span data-stu-id="cf915-167">[download the SDK]: https://developer.amazon.com/public/resources/development-tools/sdk</span></span>

[0]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal1.png
[1]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal2.png
[2]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal3.png
[3]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal4.png
[4]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal5.png
[5]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-cmd-window.png
[6]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-new-java-class.png
[7]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-notification.png
