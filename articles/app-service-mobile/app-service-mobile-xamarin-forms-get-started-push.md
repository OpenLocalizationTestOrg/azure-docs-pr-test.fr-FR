---
title: "Ajout de notifications Push à votre application Xamarin.Forms | Microsoft Docs"
description: "Découvrez comment utiliser les services Azure pour envoyer des notifications Push multiplateforme à vos applications Xamarin.Forms."
services: app-service\mobile
documentationcenter: xamarin
author: ysxu
manager: syntaxc4
editor: 
ms.assetid: d9b1ba9a-b3f2-4d12-affc-2ee34311538b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: 912367636f1b26b3b07fbd5fe3fe8ed053218fd5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-xamarinforms-app"></a><span data-ttu-id="41e1b-103">Ajout de notifications Push à votre application Xamarin.Forms</span><span class="sxs-lookup"><span data-stu-id="41e1b-103">Add push notifications to your Xamarin.Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="41e1b-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="41e1b-104">Overview</span></span>
<span data-ttu-id="41e1b-105">Dans ce didacticiel, vous ajoutez des notifications Push à tous les projets qui résultent du [démarrage rapide Xamarin.Forms](app-service-mobile-xamarin-forms-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="41e1b-105">In this tutorial, you add push notifications to all the projects that resulted from the [Xamarin.Forms quick start](app-service-mobile-xamarin-forms-get-started.md).</span></span> <span data-ttu-id="41e1b-106">Cela signifie qu’une notification Push est envoyée à tous les clients inter-plateformes à chaque fois qu’un enregistrement est inséré.</span><span class="sxs-lookup"><span data-stu-id="41e1b-106">This means that a push notification is sent to all cross-platform clients every time a record is inserted.</span></span>

<span data-ttu-id="41e1b-107">Si vous n’utilisez pas le projet de serveur du démarrage rapide téléchargé, vous devrez ajouter le package d’extension de notification Push.</span><span class="sxs-lookup"><span data-stu-id="41e1b-107">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="41e1b-108">Consultez [Fonctionnement avec le Kit de développement logiciel (SDK) du serveur principal .NET pour Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="41e1b-108">For more information, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41e1b-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="41e1b-109">Prerequisites</span></span>
<span data-ttu-id="41e1b-110">Pour iOS, vous avez besoin d’une [appartenance au programme pour développeurs Apple](https://developer.apple.com/programs/ios/) et d’un appareil iOS physique.</span><span class="sxs-lookup"><span data-stu-id="41e1b-110">For iOS, you will need an [Apple Developer Program membership](https://developer.apple.com/programs/ios/) and a physical iOS device.</span></span> <span data-ttu-id="41e1b-111">Les [notifications Push ne sont pas prises en charge par le simulateur iOS](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span><span class="sxs-lookup"><span data-stu-id="41e1b-111">The [iOS simulator does not support push notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span></span>

## <span data-ttu-id="41e1b-112"><a name="configure-hub"></a>Configurer un hub de notification</span><span class="sxs-lookup"><span data-stu-id="41e1b-112"><a name="configure-hub"></a>Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="update-the-server-project-to-send-push-notifications"></a><span data-ttu-id="41e1b-113">Mettre à jour le projet de serveur pour l'envoi de notifications Push</span><span class="sxs-lookup"><span data-stu-id="41e1b-113">Update the server project to send push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-and-run-the-android-project-optional"></a><span data-ttu-id="41e1b-114">Configurer et exécuter le projet Android (facultatif)</span><span class="sxs-lookup"><span data-stu-id="41e1b-114">Configure and run the Android project (optional)</span></span>
<span data-ttu-id="41e1b-115">Terminez cette section pour activer les notifications Push pour le projet Android Xamarin.Forms pour Android.</span><span class="sxs-lookup"><span data-stu-id="41e1b-115">Complete this section to enable push notifications for the Xamarin.Forms Droid project for Android.</span></span>

### <a name="enable-firebase-cloud-messaging-fcm"></a><span data-ttu-id="41e1b-116">Activation de Firebase Cloud Messaging (FCM)</span><span class="sxs-lookup"><span data-stu-id="41e1b-116">Enable Firebase Cloud Messaging (FCM)</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

### <a name="configure-the-mobile-apps-back-end-to-send-push-requests-by-using-fcm"></a><span data-ttu-id="41e1b-117">Configurer le serveur principal Mobile Apps pour l’envoi de demandes de notifications Push à l’aide de FCM</span><span class="sxs-lookup"><span data-stu-id="41e1b-117">Configure the Mobile Apps back end to send push requests by using FCM</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

### <a name="add-push-notifications-to-the-android-project"></a><span data-ttu-id="41e1b-118">Ajouter les notifications Push au projet Android</span><span class="sxs-lookup"><span data-stu-id="41e1b-118">Add push notifications to the Android project</span></span>
<span data-ttu-id="41e1b-119">Une fois le serveur principal configuré avec FCM, vous pouvez ajouter des codes et des composants au client pour vous inscrire auprès de FCM.</span><span class="sxs-lookup"><span data-stu-id="41e1b-119">With the back end configured with FCM, you can add components and codes to the client to register with FCM.</span></span> <span data-ttu-id="41e1b-120">Vous pouvez également vous inscrire aux notifications Push avec Azure Notification Hubs via le serveur principal Mobile Apps et recevoir des notifications.</span><span class="sxs-lookup"><span data-stu-id="41e1b-120">You can also register for push notifications with Azure Notification Hubs through the Mobile Apps back end, and receive notifications.</span></span>

1. <span data-ttu-id="41e1b-121">Dans le projet **Droid**, cliquez avec le bouton droit sur le dossier **Composants**, puis cliquez sur **Get More Components...** (Obtenir davantage de composants).</span><span class="sxs-lookup"><span data-stu-id="41e1b-121">In the **Droid** project, right-click the **Components** folder, and click **Get More Components...**.</span></span> <span data-ttu-id="41e1b-122">Recherchez ensuite le composant **Client Google Cloud Messaging** et ajoutez-le au projet.</span><span class="sxs-lookup"><span data-stu-id="41e1b-122">Then search for the **Google Cloud Messaging Client** component and add it to the project.</span></span> <span data-ttu-id="41e1b-123">Ce composant prend en charge les notifications Push pour un projet Xamarin Android.</span><span class="sxs-lookup"><span data-stu-id="41e1b-123">This component supports push notifications for a Xamarin Android project.</span></span>
2. <span data-ttu-id="41e1b-124">Ouvrez le fichier de projet MainActivity.cs et ajoutez l’instruction suivante au début du fichier :</span><span class="sxs-lookup"><span data-stu-id="41e1b-124">Open the MainActivity.cs project file, and add the following statement at the top of the file:</span></span>

        using Gcm.Client;
3. <span data-ttu-id="41e1b-125">Ajoutez le code suivant à la méthode **OnCreate** après l’appel à **LoadApplication** :</span><span class="sxs-lookup"><span data-stu-id="41e1b-125">Add the following code to the **OnCreate** method after the call to **LoadApplication**:</span></span>

        try
        {
            // Check to ensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);

            // Register for push notifications
            System.Diagnostics.Debug.WriteLine("Registering...");
            GcmClient.Register(this, PushHandlerBroadcastReceiver.SENDER_IDS);
        }
        catch (Java.Net.MalformedURLException)
        {
            CreateAndShowDialog("There was an error creating the client. Verify the URL.", "Error");
        }
        catch (Exception e)
        {
            CreateAndShowDialog(e.Message, "Error");
        }
4. <span data-ttu-id="41e1b-126">Ajoutez une nouvelle méthode d’assistance **CreateAndShowDialog** , comme suit :</span><span class="sxs-lookup"><span data-stu-id="41e1b-126">Add a new **CreateAndShowDialog** helper method, as follows:</span></span>

        private void CreateAndShowDialog(String message, String title)
        {
            AlertDialog.Builder builder = new AlertDialog.Builder(this);

            builder.SetMessage (message);
            builder.SetTitle (title);
            builder.Create().Show ();
        }
5. <span data-ttu-id="41e1b-127">Ajoutez le code suivant à la classe **MainActivity** :</span><span class="sxs-lookup"><span data-stu-id="41e1b-127">Add the following code to the **MainActivity** class:</span></span>

        // Create a new instance field for this activity.
        static MainActivity instance = null;

        // Return the current activity instance.
        public static MainActivity CurrentActivity
        {
            get
            {
                return instance;
            }
        }

    <span data-ttu-id="41e1b-128">Cela expose l’instance **MainActivity** actuelle afin que nous puissions l’exécuter sur le thread de l’interface utilisateur principale.</span><span class="sxs-lookup"><span data-stu-id="41e1b-128">This exposes the current **MainActivity** instance, so we can execute on the main UI thread.</span></span>
6. <span data-ttu-id="41e1b-129">Initialisez la variable `instance` au début de la méthode **OnCreate**, comme suit.</span><span class="sxs-lookup"><span data-stu-id="41e1b-129">Initialize the `instance` variable at the beginning of the **OnCreate** method, as follows.</span></span>

        // Set the current instance of MainActivity.
        instance = this;
7. <span data-ttu-id="41e1b-130">Ajoutez un nouveau fichier de classe au projet **Droid** nommé `GcmService.cs`, et assurez-vous que les instructions **using** suivantes figurent en haut du fichier :</span><span class="sxs-lookup"><span data-stu-id="41e1b-130">Add a new class file to the **Droid** project named `GcmService.cs`, and make sure the following **using** statements are present at the top of the file:</span></span>

        using Android.App;
        using Android.Content;
        using Android.Media;
        using Android.Support.V4.App;
        using Android.Util;
        using Gcm.Client;
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.Text;
8. <span data-ttu-id="41e1b-131">Ajoutez les demandes d’autorisation suivantes au début du fichier, après les instructions **using** et avant la déclaration **namespace**.</span><span class="sxs-lookup"><span data-stu-id="41e1b-131">Add the following permission requests at the top of the file, after the **using** statements and before the **namespace** declaration.</span></span>

        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
        //GET_ACCOUNTS is only needed for android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
9. <span data-ttu-id="41e1b-132">Ajoutez la définition de classe suivante à l’espace de noms.</span><span class="sxs-lookup"><span data-stu-id="41e1b-132">Add the following class definition to the namespace.</span></span>

       [BroadcastReceiver(Permission = Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY }, Categories = new string[] { "@PACKAGE_NAME@" })]
       public class PushHandlerBroadcastReceiver : GcmBroadcastReceiverBase<GcmService>
       {
           public static string[] SENDER_IDS = new string[] { "<PROJECT_NUMBER>" };
       }

   > [!NOTE]
   > <span data-ttu-id="41e1b-133">Remplacez **<PROJECT_NUMBER>** par le numéro de projet noté précédemment.</span><span class="sxs-lookup"><span data-stu-id="41e1b-133">Replace **<PROJECT_NUMBER>** with your project number you noted earlier.</span></span>    
   >
   >
10. <span data-ttu-id="41e1b-134">Remplacez la classe **GcmService** vide par le code suivant, qui utilise le nouveau récepteur de diffusion :</span><span class="sxs-lookup"><span data-stu-id="41e1b-134">Replace the empty **GcmService** class with the following code, which uses the new broadcast receiver:</span></span>

         [Service]
         public class GcmService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }

             public GcmService()
                 : base(PushHandlerBroadcastReceiver.SENDER_IDS){}
         }
11. <span data-ttu-id="41e1b-135">Ajoutez le code suivant à la classe **GcmService**.</span><span class="sxs-lookup"><span data-stu-id="41e1b-135">Add the following code to the **GcmService** class.</span></span> <span data-ttu-id="41e1b-136">Cela remplace le gestionnaire d’événements **OnRegistered** et met en œuvre une méthode **Register**.</span><span class="sxs-lookup"><span data-stu-id="41e1b-136">This overrides the **OnRegistered** event handler and implements a **Register** method.</span></span>

        protected override void OnRegistered(Context context, string registrationId)
        {
            Log.Verbose("PushHandlerBroadcastReceiver", "GCM Registered: " + registrationId);
            RegistrationID = registrationId;

            var push = TodoItemManager.DefaultManager.CurrentClient.GetPush();

            MainActivity.CurrentActivity.RunOnUiThread(() => Register(push, null));
        }

        public async void Register(Microsoft.WindowsAzure.MobileServices.Push push, IEnumerable<string> tags)
        {
            try
            {
                const string templateBodyGCM = "{\"data\":{\"message\":\"$(messageParam)\"}}";

                JObject templates = new JObject();
                templates["genericMessage"] = new JObject
                {
                    {"body", templateBodyGCM}
                };

                await push.RegisterAsync(RegistrationID, templates);
                Log.Info("Push Installation Id", push.InstallationId.ToString());
            }
            catch (Exception ex)
            {
                System.Diagnostics.Debug.WriteLine(ex.Message);
                Debugger.Break();
            }
        }

    <span data-ttu-id="41e1b-137">Notez que ce code utilise le paramètre `messageParam` pour l’inscription du modèle.</span><span class="sxs-lookup"><span data-stu-id="41e1b-137">Note that this code uses the `messageParam` parameter in the template registration.</span></span>
12. <span data-ttu-id="41e1b-138">Ajoutez le code suivant qui implémente **OnMessage**:</span><span class="sxs-lookup"><span data-stu-id="41e1b-138">Add the following code that implements **OnMessage**:</span></span>

        protected override void OnMessage(Context context, Intent intent)
        {
            Log.Info("PushHandlerBroadcastReceiver", "GCM Message Received!");

            var msg = new StringBuilder();

            if (intent != null && intent.Extras != null)
            {
                foreach (var key in intent.Extras.KeySet())
                    msg.AppendLine(key + "=" + intent.Extras.Get(key).ToString());
            }

            //Store the message
            var prefs = GetSharedPreferences(context.PackageName, FileCreationMode.Private);
            var edit = prefs.Edit();
            edit.PutString("last_msg", msg.ToString());
            edit.Commit();

            string message = intent.Extras.GetString("message");
            if (!string.IsNullOrEmpty(message))
            {
                createNotification("New todo item!", "Todo item: " + message);
                return;
            }

            string msg2 = intent.Extras.GetString("msg");
            if (!string.IsNullOrEmpty(msg2))
            {
                createNotification("New hub message!", msg2);
                return;
            }

            createNotification("Unknown message details", msg.ToString());
        }

        void createNotification(string title, string desc)
        {
            //Create notification
            var notificationManager = GetSystemService(Context.NotificationService) as NotificationManager;

            //Create an intent to show ui
            var uiIntent = new Intent(this, typeof(MainActivity));

            //Use Notification Builder
            NotificationCompat.Builder builder = new NotificationCompat.Builder(this);

            //Create the notification
            //we use the pending intent, passing our ui intent over which will get called
            //when the notification is tapped.
            var notification = builder.SetContentIntent(PendingIntent.GetActivity(this, 0, uiIntent, 0))
                    .SetSmallIcon(Android.Resource.Drawable.SymActionEmail)
                    .SetTicker(title)
                    .SetContentTitle(title)
                    .SetContentText(desc)

                    //Set the notification sound
                    .SetSound(RingtoneManager.GetDefaultUri(RingtoneType.Notification))

                    //Auto cancel will remove the notification once the user touches it
                    .SetAutoCancel(true).Build();

            //Show the notification
            notificationManager.Notify(1, notification);
        }

    <span data-ttu-id="41e1b-139">Cela gère les notifications entrantes et les envoie dans le Gestionnaire de notifications pour les afficher.</span><span class="sxs-lookup"><span data-stu-id="41e1b-139">This handles incoming notifications and sends them to the notification manager to be displayed.</span></span>
13. <span data-ttu-id="41e1b-140">**GcmServiceBase** requiert également la mise en œuvre des méthodes d’assistance **OnUnRegistered** et **OnError** que vous pouvez effectuer comme suit :</span><span class="sxs-lookup"><span data-stu-id="41e1b-140">**GcmServiceBase** also requires you to implement the **OnUnRegistered** and **OnError** handler methods, which you can do as follows:</span></span>

        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "Unregistered RegisterationId : " + registrationId);
        }

        protected override void OnError(Context context, string errorId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "GCM Error: " + errorId);
        }

<span data-ttu-id="41e1b-141">Vous êtes maintenant prêt à tester les notifications Push dans l’application exécutée sur un appareil Android ou sur l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="41e1b-141">Now, you are ready test push notifications in the app running on an Android device or the emulator.</span></span>

### <a name="test-push-notifications-in-your-android-app"></a><span data-ttu-id="41e1b-142">Tester les notifications Push dans votre application Android</span><span class="sxs-lookup"><span data-stu-id="41e1b-142">Test push notifications in your Android app</span></span>
<span data-ttu-id="41e1b-143">Les deux premières étapes sont requises uniquement lorsque vous testez sur un émulateur.</span><span class="sxs-lookup"><span data-stu-id="41e1b-143">The first two steps are required only when you're testing on an emulator.</span></span>

1. <span data-ttu-id="41e1b-144">Assurez-vous de procéder au déploiement ou au débogage sur un appareil virtuel sur lequel les API Google sont définies comme cible, comme indiqué ci-dessous dans le Gestionnaire d’appareil virtuel Android.</span><span class="sxs-lookup"><span data-stu-id="41e1b-144">Make sure that you are deploying to or debugging on a virtual device that has Google APIs set as the target, as shown below in the Android Virtual Device manager.</span></span>
2. <span data-ttu-id="41e1b-145">Ajoutez un compte Google à l’appareil Android en cliquant sur **Applications** > **Paramètres** > **Ajouter un compte**.</span><span class="sxs-lookup"><span data-stu-id="41e1b-145">Add a Google account to the Android device by clicking **Apps** > **Settings** > **Add account**.</span></span> <span data-ttu-id="41e1b-146">Puis suivez les invites pour ajouter un compte Google existant sur l’appareil ou pour en créer un nouveau.</span><span class="sxs-lookup"><span data-stu-id="41e1b-146">Then follow the prompts to add an existing Google account to the device, or to create a new one.</span></span>
3. <span data-ttu-id="41e1b-147">Dans Visual Studio ou Xamarin Studio, cliquez avec le bouton droit sur le projet **Droid**, puis cliquez sur **Définir comme projet de démarrage**.</span><span class="sxs-lookup"><span data-stu-id="41e1b-147">In Visual Studio or Xamarin Studio, right-click the **Droid** project and click **Set as startup project**.</span></span>
4. <span data-ttu-id="41e1b-148">Cliquez sur **Exécuter** pour générer le projet et lancer l’application sur votre appareil ou émulateur Android.</span><span class="sxs-lookup"><span data-stu-id="41e1b-148">Click **Run** to build the project and start the app on your Android device or emulator.</span></span>
5. <span data-ttu-id="41e1b-149">Dans l’application, tapez une tâche, puis cliquez sur l’icône plus (**+**).</span><span class="sxs-lookup"><span data-stu-id="41e1b-149">In the app, type a task, and then click the plus (**+**) icon.</span></span>
6. <span data-ttu-id="41e1b-150">Vérifiez qu’une notification est reçue lorsqu’un élément est ajouté.</span><span class="sxs-lookup"><span data-stu-id="41e1b-150">Verify that a notification is received when an item is added.</span></span>

## <a name="configure-and-run-the-ios-project-optional"></a><span data-ttu-id="41e1b-151">Configurer et exécuter le projet iOS (facultatif)</span><span class="sxs-lookup"><span data-stu-id="41e1b-151">Configure and run the iOS project (optional)</span></span>
<span data-ttu-id="41e1b-152">Cette section est dédiée à l’exécution du projet Xamarin iOS pour les appareils iOS.</span><span class="sxs-lookup"><span data-stu-id="41e1b-152">This section is for running the Xamarin iOS project for iOS devices.</span></span> <span data-ttu-id="41e1b-153">Vous pouvez ignorer cette section si vous n’utilisez pas d’appareils iOS.</span><span class="sxs-lookup"><span data-stu-id="41e1b-153">You can skip this section if you are not working with iOS devices.</span></span>

[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

#### <a name="configure-the-notification-hub-for-apns"></a><span data-ttu-id="41e1b-154">Configurer le Notification Hub pour APNS</span><span class="sxs-lookup"><span data-stu-id="41e1b-154">Configure the notification hub for APNS</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

<span data-ttu-id="41e1b-155">Ensuite, vous allez configurer le paramètre de projet iOS dans Xamarin Studio ou Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="41e1b-155">Next, you will configure the iOS project setting in Xamarin Studio or Visual Studio.</span></span>

[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

#### <a name="add-push-notifications-to-your-ios-app"></a><span data-ttu-id="41e1b-156">Ajout de notifications Push à votre application iOS</span><span class="sxs-lookup"><span data-stu-id="41e1b-156">Add push notifications to your iOS app</span></span>
1. <span data-ttu-id="41e1b-157">Dans le projet **iOS**, ouvrez AppDelegate.cs et ajoutez l’instruction suivante en haut du fichier de code.</span><span class="sxs-lookup"><span data-stu-id="41e1b-157">In the **iOS** project, open AppDelegate.cs and add the following statement to the top of the code file.</span></span>

        using Newtonsoft.Json.Linq;
2. <span data-ttu-id="41e1b-158">Dans la classe **AppDelegate**, ajoutez également un remplacement pour l’événement **RegisteredForRemoteNotifications** afin de vous inscrire pour les notifications :</span><span class="sxs-lookup"><span data-stu-id="41e1b-158">In the **AppDelegate** class, add an override for the **RegisteredForRemoteNotifications** event to register for notifications:</span></span>

        public override void RegisteredForRemoteNotifications(UIApplication application,
            NSData deviceToken)
        {
            const string templateBodyAPNS = "{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
                {
                  {"body", templateBodyAPNS}
                };

            // Register for push with your mobile app
            Push push = TodoItemManager.DefaultManager.CurrentClient.GetPush();
            push.RegisterAsync(deviceToken, templates);
        }
3. <span data-ttu-id="41e1b-159">Dans **AppDelegate**, ajoutez également la substitution suivante pour le Gestionnaire d’événements **DidReceiveRemoteNotification** :</span><span class="sxs-lookup"><span data-stu-id="41e1b-159">In **AppDelegate**, also add the following override for the **DidReceiveRemoteNotification** event handler:</span></span>

        public override void DidReceiveRemoteNotification(UIApplication application,
            NSDictionary userInfo, Action<UIBackgroundFetchResult> completionHandler)
        {
            NSDictionary aps = userInfo.ObjectForKey(new NSString("aps")) as NSDictionary;

            string alert = string.Empty;
            if (aps.ContainsKey(new NSString("alert")))
                alert = (aps[new NSString("alert")] as NSString).ToString();

            //show alert
            if (!string.IsNullOrEmpty(alert))
            {
                UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                avAlert.Show();
            }
        }

    <span data-ttu-id="41e1b-160">Cette méthode gère les notifications entrantes pendant que l’application est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="41e1b-160">This method handles incoming notifications while the app is running.</span></span>
4. <span data-ttu-id="41e1b-161">Dans la classe **AppDelegate**, ajoutez le code suivant à la méthode **FinishedLaunching** :</span><span class="sxs-lookup"><span data-stu-id="41e1b-161">In the **AppDelegate** class, add the following code to the **FinishedLaunching** method:</span></span>

        // Register for push notifications.
        var settings = UIUserNotificationSettings.GetSettingsForTypes(
            UIUserNotificationType.Alert
            | UIUserNotificationType.Badge
            | UIUserNotificationType.Sound,
            new NSSet());

        UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
        UIApplication.SharedApplication.RegisterForRemoteNotifications();

    <span data-ttu-id="41e1b-162">Cela permet la prise en charge de l’enregistrement Push des notifications et des demandes à distance.</span><span class="sxs-lookup"><span data-stu-id="41e1b-162">This enables support for remote notifications and requests push registration.</span></span>

<span data-ttu-id="41e1b-163">L’application est mise à jour et prend en charge les notifications Push.</span><span class="sxs-lookup"><span data-stu-id="41e1b-163">Your app is now updated to support push notifications.</span></span>

#### <a name="test-push-notifications-in-your-ios-app"></a><span data-ttu-id="41e1b-164">Tester les notifications Push dans votre application iOS</span><span class="sxs-lookup"><span data-stu-id="41e1b-164">Test push notifications in your iOS app</span></span>
1. <span data-ttu-id="41e1b-165">Cliquez avec le bouton droit sur le projet iOS et cliquez sur **Définir comme projet de démarrage**.</span><span class="sxs-lookup"><span data-stu-id="41e1b-165">Right-click the iOS project, and click **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="41e1b-166">Cliquez sur le bouton **Exécuter** ou sur **F5** dans Visual Studio pour générer le projet et démarrer l’application sur un appareil iOS.</span><span class="sxs-lookup"><span data-stu-id="41e1b-166">Press the **Run** button or **F5** in Visual Studio to build the project and start the app in an iOS device.</span></span> <span data-ttu-id="41e1b-167">Ensuite, cliquez sur **OK** pour accepter les notifications Push.</span><span class="sxs-lookup"><span data-stu-id="41e1b-167">Then click **OK** to accept push notifications.</span></span>

   > [!NOTE]
   > <span data-ttu-id="41e1b-168">Vous devez accepter explicitement les notifications Push de votre application.</span><span class="sxs-lookup"><span data-stu-id="41e1b-168">You must explicitly accept push notifications from your app.</span></span> <span data-ttu-id="41e1b-169">Cette demande s’effectue uniquement lors du premier démarrage de l’application.</span><span class="sxs-lookup"><span data-stu-id="41e1b-169">This request only occurs the first time that the app runs.</span></span>
   >
   >
3. <span data-ttu-id="41e1b-170">Dans l’application, tapez une tâche, puis cliquez sur l’icône plus (**+**).</span><span class="sxs-lookup"><span data-stu-id="41e1b-170">In the app, type a task, and then click the plus (**+**) icon.</span></span>
4. <span data-ttu-id="41e1b-171">Vérifiez que vous avez reçu une notification, puis cliquez sur **OK** pour fermer celle-ci.</span><span class="sxs-lookup"><span data-stu-id="41e1b-171">Verify that a notification is received, and then click **OK** to dismiss the notification.</span></span>

## <a name="configure-and-run-windows-projects-optional"></a><span data-ttu-id="41e1b-172">Configurer et exécuter des projets Windows (facultatif)</span><span class="sxs-lookup"><span data-stu-id="41e1b-172">Configure and run Windows projects (optional)</span></span>
<span data-ttu-id="41e1b-173">Cette section s’applique à l’exécution des projets Xamarin.Forms WinApp et WinPhone81 pour les appareils Windows.</span><span class="sxs-lookup"><span data-stu-id="41e1b-173">This section is for running the Xamarin.Forms WinApp and WinPhone81 projects for Windows devices.</span></span> <span data-ttu-id="41e1b-174">Ces étapes prennent également en charge les projets de plateforme Windows universelle (UWP).</span><span class="sxs-lookup"><span data-stu-id="41e1b-174">These steps also support Universal Windows Platform (UWP) projects.</span></span> <span data-ttu-id="41e1b-175">Vous pouvez ignorer cette section si vous n’utilisez pas d’appareils Windows.</span><span class="sxs-lookup"><span data-stu-id="41e1b-175">You can skip this section if you are not working with Windows devices.</span></span>

#### <a name="register-your-windows-app-for-push-notifications-with-windows-notification-service-wns"></a><span data-ttu-id="41e1b-176">Inscrire votre application Windows aux notifications Push avec le service de notification Windows (Windows Notification Service, WNS)</span><span class="sxs-lookup"><span data-stu-id="41e1b-176">Register your Windows app for push notifications with Windows Notification Service (WNS)</span></span>
[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

#### <a name="configure-the-notification-hub-for-wns"></a><span data-ttu-id="41e1b-177">Configurer le Notification Hub pour WNS</span><span class="sxs-lookup"><span data-stu-id="41e1b-177">Configure the notification hub for WNS</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="add-push-notifications-to-your-windows-app"></a><span data-ttu-id="41e1b-178">Ajouter des notifications Push à votre application Windows</span><span class="sxs-lookup"><span data-stu-id="41e1b-178">Add push notifications to your Windows app</span></span>
1. <span data-ttu-id="41e1b-179">Dans Visual Studio, ouvrez le fichier **App.xaml.cs** dans un projet Windows et ajoutez les instructions suivantes.</span><span class="sxs-lookup"><span data-stu-id="41e1b-179">In Visual Studio, open **App.xaml.cs** in a Windows project, and add the following statements.</span></span>

        using Newtonsoft.Json.Linq;
        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
        using <your_TodoItemManager_portable_class_namespace>;

    <span data-ttu-id="41e1b-180">Remplacez `<your_TodoItemManager_portable_class_namespace>` par l’espace de noms de votre projet portable qui contient la classe `TodoItemManager`.</span><span class="sxs-lookup"><span data-stu-id="41e1b-180">Replace `<your_TodoItemManager_portable_class_namespace>` with the namespace of your portable project that contains the `TodoItemManager` class.</span></span>
2. <span data-ttu-id="41e1b-181">Dans le fichier App.xaml.cs, ajoutez la méthode **InitNotificationsAsync** suivante :</span><span class="sxs-lookup"><span data-stu-id="41e1b-181">In App.xaml.cs, add the following **InitNotificationsAsync** method:</span></span>

        private async Task InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager
                .CreatePushNotificationChannelForApplicationAsync();

            const string templateBodyWNS =
                "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(messageParam)</text></binding></visual></toast>";

            JObject headers = new JObject();
            headers["X-WNS-Type"] = "wns/toast";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
            {
                {"body", templateBodyWNS},
                {"headers", headers} // Needed for WNS.
            };

            await TodoItemManager.DefaultManager.CurrentClient.GetPush()
                .RegisterAsync(channel.Uri, templates);
        }

    <span data-ttu-id="41e1b-182">Cette méthode récupère le canal des notifications Push et inscrit un modèle pour recevoir les notifications de modèle à partir de votre Notification Hub.</span><span class="sxs-lookup"><span data-stu-id="41e1b-182">This method gets the push notification channel, and registers a template to receive template notifications from your notification hub.</span></span> <span data-ttu-id="41e1b-183">Un modèle de notification prenant en charge *messageParam* sera transmis à ce client.</span><span class="sxs-lookup"><span data-stu-id="41e1b-183">A template notification that supports *messageParam* will be delivered to this client.</span></span>
3. <span data-ttu-id="41e1b-184">Dans le fichier App.xaml.cs, mettez à jour la définition de méthode du gestionnaire d’événements **OnLaunched** en ajoutant le modificateur `async`.</span><span class="sxs-lookup"><span data-stu-id="41e1b-184">In App.xaml.cs, update the **OnLaunched** event handler method definition by adding the `async` modifier.</span></span> <span data-ttu-id="41e1b-185">Puis, ajoutez la ligne de code suivante à la fin de la méthode :</span><span class="sxs-lookup"><span data-stu-id="41e1b-185">Then add the following line of code at the end of the method:</span></span>

        await InitNotificationsAsync();

    <span data-ttu-id="41e1b-186">Cela permet de s’assurer que l’inscription aux notifications Push est créée ou actualisée à chaque lancement de l’application.</span><span class="sxs-lookup"><span data-stu-id="41e1b-186">This ensures that the push notification registration is created or refreshed every time the app is launched.</span></span> <span data-ttu-id="41e1b-187">Il est important d’effectuer cette opération pour vous assurer que le canal Push WNS est toujours actif.</span><span class="sxs-lookup"><span data-stu-id="41e1b-187">It's important to do this to guarantee that the WNS push channel is always active.</span></span>  
4. <span data-ttu-id="41e1b-188">Dans l’Explorateur de solutions pour Visual Studio, ouvrez le fichier **Package.appxmanifest**, puis définissez **Compatible toast** sur **Oui** sous **Notifications**.</span><span class="sxs-lookup"><span data-stu-id="41e1b-188">In Solution Explorer for Visual Studio, open the **Package.appxmanifest** file, and set **Toast Capable** to **Yes** under **Notifications**.</span></span>
5. <span data-ttu-id="41e1b-189">Générez l’application et vérifiez l’absence d’erreurs.</span><span class="sxs-lookup"><span data-stu-id="41e1b-189">Build the app and verify you have no errors.</span></span> <span data-ttu-id="41e1b-190">Votre application cliente doit désormais s’inscrire pour les notifications de modèle du serveur principal Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="41e1b-190">Your client app should now register for the template notifications from the Mobile Apps back end.</span></span> <span data-ttu-id="41e1b-191">Répétez cette section pour chaque projet Windows dans votre solution.</span><span class="sxs-lookup"><span data-stu-id="41e1b-191">Repeat this section for every Windows project in your solution.</span></span>

#### <a name="test-push-notifications-in-your-windows-app"></a><span data-ttu-id="41e1b-192">Tester les notifications Push dans votre application Windows</span><span class="sxs-lookup"><span data-stu-id="41e1b-192">Test push notifications in your Windows app</span></span>
1. <span data-ttu-id="41e1b-193">Dans Visual Studio, cliquez avec le bouton droit sur un projet Windows, puis cliquez sur **Définir comme projet de démarrage**.</span><span class="sxs-lookup"><span data-stu-id="41e1b-193">In Visual Studio, right-click a Windows project, and click **Set as startup project**.</span></span>
2. <span data-ttu-id="41e1b-194">Appuyez sur le bouton **Exécuter** pour générer le projet et démarrer l'application.</span><span class="sxs-lookup"><span data-stu-id="41e1b-194">Press the **Run** button to build the project and start the app.</span></span>
3. <span data-ttu-id="41e1b-195">Dans l’application, tapez un nom pour un nouvel élément todoitem, puis cliquez sur l’icône de signe plus (**+**) pour l’ajouter.</span><span class="sxs-lookup"><span data-stu-id="41e1b-195">In the app, type a name for a new todoitem, and then click the plus (**+**) icon to add it.</span></span>
4. <span data-ttu-id="41e1b-196">Vérifiez qu’une notification est reçue lorsque l’élément est ajouté.</span><span class="sxs-lookup"><span data-stu-id="41e1b-196">Verify that a notification is received when the item is added.</span></span>

## <a name="next-steps"></a><span data-ttu-id="41e1b-197">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="41e1b-197">Next steps</span></span>
<span data-ttu-id="41e1b-198">Apprenez-en plus sur les notifications Push :</span><span class="sxs-lookup"><span data-stu-id="41e1b-198">You can learn more about push notifications:</span></span>

* [<span data-ttu-id="41e1b-199">Diagnostiquer les problèmes de notification Push</span><span class="sxs-lookup"><span data-stu-id="41e1b-199">Diagnose push notification issues</span></span>](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  <span data-ttu-id="41e1b-200">Il existe différentes raisons pour lesquelles les notifications peuvent être perdues ou n’arrivent pas sur les appareils.</span><span class="sxs-lookup"><span data-stu-id="41e1b-200">There are various reasons why notifications may get dropped or do not end up on devices.</span></span> <span data-ttu-id="41e1b-201">Cette rubrique vous explique comment analyser et déterminer la cause première des défaillances de notification Push.</span><span class="sxs-lookup"><span data-stu-id="41e1b-201">This topic shows you how to analyze and figure out the root cause of push notification failures.</span></span>

<span data-ttu-id="41e1b-202">Vous pouvez poursuivre avec l’un des didacticiels suivants :</span><span class="sxs-lookup"><span data-stu-id="41e1b-202">You can also continue on to one of the following tutorials:</span></span>

* [<span data-ttu-id="41e1b-203">Ajouter l’authentification à votre application </span><span class="sxs-lookup"><span data-stu-id="41e1b-203">Add authentication to your app </span></span>](app-service-mobile-xamarin-forms-get-started-users.md)  
  <span data-ttu-id="41e1b-204">Découvrez comment authentifier les utilisateurs de votre application avec un fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="41e1b-204">Learn how to authenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="41e1b-205">Activer la synchronisation hors connexion pour votre application</span><span class="sxs-lookup"><span data-stu-id="41e1b-205">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  <span data-ttu-id="41e1b-206">Découvrez comment ajouter une prise en charge hors connexion à votre application à l’aide d’un serveur principal Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="41e1b-206">Learn how to add offline support for your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="41e1b-207">La synchronisation hors connexion permet aux utilisateurs d’interagir avec une application mobile &mdash;pour afficher, ajouter ou modifier des données&mdash;, même lorsqu’il n’existe aucune connexion réseau.</span><span class="sxs-lookup"><span data-stu-id="41e1b-207">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Images. -->

<!-- URLs. -->
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[Xcode]: https://go.microsoft.com/fwLink/?LinkID=266532
[apns object]: http://go.microsoft.com/fwlink/p/?LinkId=272333
