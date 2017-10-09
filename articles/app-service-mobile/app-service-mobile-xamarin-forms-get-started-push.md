---
title: application de Xamarin.Forms aaaAdd push notifications tooyour | Documents Microsoft
description: "Découvrez comment toouse Azure services toosend multi-plateforme push notifications tooyour Xamarin.Forms applications."
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
ms.openlocfilehash: 9133a0b6dd99c01def525607c20ce5a9c19b9502
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-xamarinforms-app"></a><span data-ttu-id="14584-103">Ajouter une application de Xamarin.Forms de tooyour de notifications push</span><span class="sxs-lookup"><span data-stu-id="14584-103">Add push notifications tooyour Xamarin.Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="14584-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="14584-104">Overview</span></span>
<span data-ttu-id="14584-105">Dans ce didacticiel, vous ajoutez des projets push notifications tooall hello résultant hello [démarrage rapide de Xamarin.Forms](app-service-mobile-xamarin-forms-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="14584-105">In this tutorial, you add push notifications tooall hello projects that resulted from hello [Xamarin.Forms quick start](app-service-mobile-xamarin-forms-get-started.md).</span></span> <span data-ttu-id="14584-106">Cela signifie qu’une notification push est envoyée clients d’inter-plateformes tooall chaque fois qu’un enregistrement est inséré.</span><span class="sxs-lookup"><span data-stu-id="14584-106">This means that a push notification is sent tooall cross-platform clients every time a record is inserted.</span></span>

<span data-ttu-id="14584-107">Si vous n’utilisez pas hello téléchargé le projet de démarrage rapide de serveur, vous devez serez hello package d’extension de notification push.</span><span class="sxs-lookup"><span data-stu-id="14584-107">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="14584-108">Pour plus d’informations, consultez [fonctionne avec serveur principal de .NET hello SDK pour les applications mobiles Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="14584-108">For more information, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="14584-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="14584-109">Prerequisites</span></span>
<span data-ttu-id="14584-110">Pour iOS, vous avez besoin d’une [appartenance au programme pour développeurs Apple](https://developer.apple.com/programs/ios/) et d’un appareil iOS physique.</span><span class="sxs-lookup"><span data-stu-id="14584-110">For iOS, you will need an [Apple Developer Program membership](https://developer.apple.com/programs/ios/) and a physical iOS device.</span></span> <span data-ttu-id="14584-111">Hello [simulateur iOS ne prend pas en charge des notifications push](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span><span class="sxs-lookup"><span data-stu-id="14584-111">hello [iOS simulator does not support push notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span></span>

## <span data-ttu-id="14584-112"><a name="configure-hub"></a>Configurer un hub de notification</span><span class="sxs-lookup"><span data-stu-id="14584-112"><a name="configure-hub"></a>Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="update-hello-server-project-toosend-push-notifications"></a><span data-ttu-id="14584-113">Mettre à jour des notifications push de hello serveur projet toosend</span><span class="sxs-lookup"><span data-stu-id="14584-113">Update hello server project toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-and-run-hello-android-project-optional"></a><span data-ttu-id="14584-114">Configurer et exécuter le projet Android de hello (facultatif)</span><span class="sxs-lookup"><span data-stu-id="14584-114">Configure and run hello Android project (optional)</span></span>
<span data-ttu-id="14584-115">Effectuez cette section tooenable des notifications push pour hello Xamarin.Forms Droid projet pour Android.</span><span class="sxs-lookup"><span data-stu-id="14584-115">Complete this section tooenable push notifications for hello Xamarin.Forms Droid project for Android.</span></span>

### <a name="enable-firebase-cloud-messaging-fcm"></a><span data-ttu-id="14584-116">Activation de Firebase Cloud Messaging (FCM)</span><span class="sxs-lookup"><span data-stu-id="14584-116">Enable Firebase Cloud Messaging (FCM)</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

### <a name="configure-hello-mobile-apps-back-end-toosend-push-requests-by-using-fcm"></a><span data-ttu-id="14584-117">Configurer les demandes de transmission toosend hello Mobile Apps back-end à l’aide de FCM</span><span class="sxs-lookup"><span data-stu-id="14584-117">Configure hello Mobile Apps back end toosend push requests by using FCM</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

### <a name="add-push-notifications-toohello-android-project"></a><span data-ttu-id="14584-118">Ajouter le projet Android des toohello des notifications push</span><span class="sxs-lookup"><span data-stu-id="14584-118">Add push notifications toohello Android project</span></span>
<span data-ttu-id="14584-119">Avec hello serveur principal configuré avec FCM, vous pouvez ajouter des composants et des codes tooregister de client toohello avec FCM.</span><span class="sxs-lookup"><span data-stu-id="14584-119">With hello back end configured with FCM, you can add components and codes toohello client tooregister with FCM.</span></span> <span data-ttu-id="14584-120">Vous pouvez également vous inscrire pour les notifications push avec Azure Notification Hubs via hello dans les applications mobiles se termine et recevoir des notifications.</span><span class="sxs-lookup"><span data-stu-id="14584-120">You can also register for push notifications with Azure Notification Hubs through hello Mobile Apps back end, and receive notifications.</span></span>

1. <span data-ttu-id="14584-121">Bonjour **Droid** de projet, avec le bouton droit hello **composants** dossier, puis cliquez sur **obtenir plusieurs composants...** . Puis recherchez hello **Client de messagerie Cloud Google** composant et l’ajouter toohello projet.</span><span class="sxs-lookup"><span data-stu-id="14584-121">In hello **Droid** project, right-click hello **Components** folder, and click **Get More Components...**. Then search for hello **Google Cloud Messaging Client** component and add it toohello project.</span></span> <span data-ttu-id="14584-122">Ce composant prend en charge les notifications Push pour un projet Xamarin Android.</span><span class="sxs-lookup"><span data-stu-id="14584-122">This component supports push notifications for a Xamarin Android project.</span></span>
2. <span data-ttu-id="14584-123">Ouvrez le fichier de projet MainActivity.cs hello et ajoutez hello après l’instruction de haut hello du fichier de hello :</span><span class="sxs-lookup"><span data-stu-id="14584-123">Open hello MainActivity.cs project file, and add hello following statement at hello top of hello file:</span></span>

        using Gcm.Client;
3. <span data-ttu-id="14584-124">Ajouter hello suivant code toohello **OnCreate** méthode après hello appeler trop**LoadApplication**:</span><span class="sxs-lookup"><span data-stu-id="14584-124">Add hello following code toohello **OnCreate** method after hello call too**LoadApplication**:</span></span>

        try
        {
            // Check tooensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);

            // Register for push notifications
            System.Diagnostics.Debug.WriteLine("Registering...");
            GcmClient.Register(this, PushHandlerBroadcastReceiver.SENDER_IDS);
        }
        catch (Java.Net.MalformedURLException)
        {
            CreateAndShowDialog("There was an error creating hello client. Verify hello URL.", "Error");
        }
        catch (Exception e)
        {
            CreateAndShowDialog(e.Message, "Error");
        }
4. <span data-ttu-id="14584-125">Ajoutez une nouvelle méthode d’assistance **CreateAndShowDialog** , comme suit :</span><span class="sxs-lookup"><span data-stu-id="14584-125">Add a new **CreateAndShowDialog** helper method, as follows:</span></span>

        private void CreateAndShowDialog(String message, String title)
        {
            AlertDialog.Builder builder = new AlertDialog.Builder(this);

            builder.SetMessage (message);
            builder.SetTitle (title);
            builder.Create().Show ();
        }
5. <span data-ttu-id="14584-126">Ajouter hello suivant code toohello **MainActivity** classe :</span><span class="sxs-lookup"><span data-stu-id="14584-126">Add hello following code toohello **MainActivity** class:</span></span>

        // Create a new instance field for this activity.
        static MainActivity instance = null;

        // Return hello current activity instance.
        public static MainActivity CurrentActivity
        {
            get
            {
                return instance;
            }
        }

    <span data-ttu-id="14584-127">Cela expose hello actuel **MainActivity** de l’instance, donc nous pouvons exécuter sur le thread d’interface utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="14584-127">This exposes hello current **MainActivity** instance, so we can execute on hello main UI thread.</span></span>
6. <span data-ttu-id="14584-128">Initialiser hello `instance` variable au début de hello Hello **OnCreate** méthode, comme suit.</span><span class="sxs-lookup"><span data-stu-id="14584-128">Initialize hello `instance` variable at hello beginning of hello **OnCreate** method, as follows.</span></span>

        // Set hello current instance of MainActivity.
        instance = this;
7. <span data-ttu-id="14584-129">Ajouter un nouveau toohello de fichier de classe **Droid** projet nommé `GcmService.cs`et assurez-vous que suivant de hello **à l’aide de** instructions figurent en haut de hello du fichier de hello :</span><span class="sxs-lookup"><span data-stu-id="14584-129">Add a new class file toohello **Droid** project named `GcmService.cs`, and make sure hello following **using** statements are present at hello top of hello file:</span></span>

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
8. <span data-ttu-id="14584-130">Ajouter hello suivant des demandes d’autorisations haut hello du fichier hello après hello **à l’aide de** instructions et avant hello **espace de noms** déclaration.</span><span class="sxs-lookup"><span data-stu-id="14584-130">Add hello following permission requests at hello top of hello file, after hello **using** statements and before hello **namespace** declaration.</span></span>

        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
        //GET_ACCOUNTS is only needed for android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
9. <span data-ttu-id="14584-131">Ajoutez hello suivant toohello de définition de classe namespace.</span><span class="sxs-lookup"><span data-stu-id="14584-131">Add hello following class definition toohello namespace.</span></span>

       [BroadcastReceiver(Permission = Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY }, Categories = new string[] { "@PACKAGE_NAME@" })]
       public class PushHandlerBroadcastReceiver : GcmBroadcastReceiverBase<GcmService>
       {
           public static string[] SENDER_IDS = new string[] { "<PROJECT_NUMBER>" };
       }

   > [!NOTE]
   > <span data-ttu-id="14584-132">Remplacez **<PROJECT_NUMBER>** par le numéro de projet noté précédemment.</span><span class="sxs-lookup"><span data-stu-id="14584-132">Replace **<PROJECT_NUMBER>** with your project number you noted earlier.</span></span>    
   >
   >
10. <span data-ttu-id="14584-133">Remplacez hello vide **GcmService** classe avec hello suivant de code, qui utilise un récepteur de diffusion nouvelle hello :</span><span class="sxs-lookup"><span data-stu-id="14584-133">Replace hello empty **GcmService** class with hello following code, which uses hello new broadcast receiver:</span></span>

         [Service]
         public class GcmService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }

             public GcmService()
                 : base(PushHandlerBroadcastReceiver.SENDER_IDS){}
         }
11. <span data-ttu-id="14584-134">Ajouter hello suivant code toohello **GcmService** classe.</span><span class="sxs-lookup"><span data-stu-id="14584-134">Add hello following code toohello **GcmService** class.</span></span> <span data-ttu-id="14584-135">Cela remplace hello **OnRegistered** Gestionnaire d’événements et met en œuvre un **inscrire** (méthode).</span><span class="sxs-lookup"><span data-stu-id="14584-135">This overrides hello **OnRegistered** event handler and implements a **Register** method.</span></span>

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

    <span data-ttu-id="14584-136">Notez que ce code utilise hello `messageParam` paramètre dans l’inscription de modèle hello.</span><span class="sxs-lookup"><span data-stu-id="14584-136">Note that this code uses hello `messageParam` parameter in hello template registration.</span></span>
12. <span data-ttu-id="14584-137">Ajouter hello suivant le code qui implémente **OnMessage**:</span><span class="sxs-lookup"><span data-stu-id="14584-137">Add hello following code that implements **OnMessage**:</span></span>

        protected override void OnMessage(Context context, Intent intent)
        {
            Log.Info("PushHandlerBroadcastReceiver", "GCM Message Received!");

            var msg = new StringBuilder();

            if (intent != null && intent.Extras != null)
            {
                foreach (var key in intent.Extras.KeySet())
                    msg.AppendLine(key + "=" + intent.Extras.Get(key).ToString());
            }

            //Store hello message
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

            //Create an intent tooshow ui
            var uiIntent = new Intent(this, typeof(MainActivity));

            //Use Notification Builder
            NotificationCompat.Builder builder = new NotificationCompat.Builder(this);

            //Create hello notification
            //we use hello pending intent, passing our ui intent over which will get called
            //when hello notification is tapped.
            var notification = builder.SetContentIntent(PendingIntent.GetActivity(this, 0, uiIntent, 0))
                    .SetSmallIcon(Android.Resource.Drawable.SymActionEmail)
                    .SetTicker(title)
                    .SetContentTitle(title)
                    .SetContentText(desc)

                    //Set hello notification sound
                    .SetSound(RingtoneManager.GetDefaultUri(RingtoneType.Notification))

                    //Auto cancel will remove hello notification once hello user touches it
                    .SetAutoCancel(true).Build();

            //Show hello notification
            notificationManager.Notify(1, notification);
        }

    <span data-ttu-id="14584-138">Cela gère les notifications entrantes et les envoie toohello notification manager toobe est affiché.</span><span class="sxs-lookup"><span data-stu-id="14584-138">This handles incoming notifications and sends them toohello notification manager toobe displayed.</span></span>
13. <span data-ttu-id="14584-139">**GcmServiceBase** nécessite également que vous tooimplement hello **OnUnRegistered** et **OnError** les méthodes de gestionnaire, vous pouvez procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="14584-139">**GcmServiceBase** also requires you tooimplement hello **OnUnRegistered** and **OnError** handler methods, which you can do as follows:</span></span>

        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "Unregistered RegisterationId : " + registrationId);
        }

        protected override void OnError(Context context, string errorId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "GCM Error: " + errorId);
        }

<span data-ttu-id="14584-140">Maintenant, vous test prêt des notifications push dans l’application hello en cours d’exécution sur un appareil Android ou hello émulateur.</span><span class="sxs-lookup"><span data-stu-id="14584-140">Now, you are ready test push notifications in hello app running on an Android device or hello emulator.</span></span>

### <a name="test-push-notifications-in-your-android-app"></a><span data-ttu-id="14584-141">Tester les notifications Push dans votre application Android</span><span class="sxs-lookup"><span data-stu-id="14584-141">Test push notifications in your Android app</span></span>
<span data-ttu-id="14584-142">Hello deux premières étapes sont requis uniquement lorsque vous testez sur un émulateur.</span><span class="sxs-lookup"><span data-stu-id="14584-142">hello first two steps are required only when you're testing on an emulator.</span></span>

1. <span data-ttu-id="14584-143">Assurez-vous que vous déployez tooor débogage sur un périphérique virtuel qui a APIs Google définir comme cible de hello, comme indiqué ci-dessous dans le Gestionnaire d’appareil virtuel Android hello.</span><span class="sxs-lookup"><span data-stu-id="14584-143">Make sure that you are deploying tooor debugging on a virtual device that has Google APIs set as hello target, as shown below in hello Android Virtual Device manager.</span></span>
2. <span data-ttu-id="14584-144">Ajouter un appareil Android de Google compte toohello en cliquant sur **applications** > **paramètres** > **Ajouter compte**.</span><span class="sxs-lookup"><span data-stu-id="14584-144">Add a Google account toohello Android device by clicking **Apps** > **Settings** > **Add account**.</span></span> <span data-ttu-id="14584-145">Suivez ensuite hello invites tooadd une unité de toohello compte Google ou toocreate un nouveau.</span><span class="sxs-lookup"><span data-stu-id="14584-145">Then follow hello prompts tooadd an existing Google account toohello device, or toocreate a new one.</span></span>
3. <span data-ttu-id="14584-146">Dans Visual Studio ou Xamarin Studio, avec le bouton droit hello **Droid** projet puis cliquez sur **définir comme projet de démarrage**.</span><span class="sxs-lookup"><span data-stu-id="14584-146">In Visual Studio or Xamarin Studio, right-click hello **Droid** project and click **Set as startup project**.</span></span>
4. <span data-ttu-id="14584-147">Cliquez sur **exécuter** toobuild hello du projet et démarrer l’application hello sur votre appareil Android ou l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="14584-147">Click **Run** toobuild hello project and start hello app on your Android device or emulator.</span></span>
5. <span data-ttu-id="14584-148">Dans l’application hello, une tâche, puis tapez Bonjour signe plu (**+**) icône.</span><span class="sxs-lookup"><span data-stu-id="14584-148">In hello app, type a task, and then click hello plus (**+**) icon.</span></span>
6. <span data-ttu-id="14584-149">Vérifiez qu’une notification est reçue lorsqu’un élément est ajouté.</span><span class="sxs-lookup"><span data-stu-id="14584-149">Verify that a notification is received when an item is added.</span></span>

## <a name="configure-and-run-hello-ios-project-optional"></a><span data-ttu-id="14584-150">Configurer et exécuter le projet iOS de hello (facultatif)</span><span class="sxs-lookup"><span data-stu-id="14584-150">Configure and run hello iOS project (optional)</span></span>
<span data-ttu-id="14584-151">Cette section est de projet d’iOS Xamarin hello pour les appareils iOS en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="14584-151">This section is for running hello Xamarin iOS project for iOS devices.</span></span> <span data-ttu-id="14584-152">Vous pouvez ignorer cette section si vous n’utilisez pas d’appareils iOS.</span><span class="sxs-lookup"><span data-stu-id="14584-152">You can skip this section if you are not working with iOS devices.</span></span>

[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

#### <a name="configure-hello-notification-hub-for-apns"></a><span data-ttu-id="14584-153">Configuration d’un concentrateur de notification hello pour APNS</span><span class="sxs-lookup"><span data-stu-id="14584-153">Configure hello notification hub for APNS</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

<span data-ttu-id="14584-154">Ensuite, vous allez configurer des paramètres de projet iOS hello dans Xamarin Studio ou Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="14584-154">Next, you will configure hello iOS project setting in Xamarin Studio or Visual Studio.</span></span>

[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

#### <a name="add-push-notifications-tooyour-ios-app"></a><span data-ttu-id="14584-155">Ajouter une application iOS de push notifications tooyour</span><span class="sxs-lookup"><span data-stu-id="14584-155">Add push notifications tooyour iOS app</span></span>
1. <span data-ttu-id="14584-156">Bonjour **iOS** de projet, ouvrez AppDelegate.cs et ajoutez hello suivant en haut de toohello instruction hello du fichier de code.</span><span class="sxs-lookup"><span data-stu-id="14584-156">In hello **iOS** project, open AppDelegate.cs and add hello following statement toohello top of hello code file.</span></span>

        using Newtonsoft.Json.Linq;
2. <span data-ttu-id="14584-157">Bonjour **AppDelegate** de classe, ajoutez un remplacement pour hello **RegisteredForRemoteNotifications** tooregister d’événements pour les notifications :</span><span class="sxs-lookup"><span data-stu-id="14584-157">In hello **AppDelegate** class, add an override for hello **RegisteredForRemoteNotifications** event tooregister for notifications:</span></span>

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
3. <span data-ttu-id="14584-158">Dans **AppDelegate**, ajoutez également hello après remplacement de hello **DidReceiveRemoteNotification** Gestionnaire d’événements :</span><span class="sxs-lookup"><span data-stu-id="14584-158">In **AppDelegate**, also add hello following override for hello **DidReceiveRemoteNotification** event handler:</span></span>

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

    <span data-ttu-id="14584-159">Cette méthode gère les notifications entrantes pendant que l’application hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="14584-159">This method handles incoming notifications while hello app is running.</span></span>
4. <span data-ttu-id="14584-160">Bonjour **AppDelegate** de classe, ajoutez hello suivant code toohello **FinishedLaunching** méthode :</span><span class="sxs-lookup"><span data-stu-id="14584-160">In hello **AppDelegate** class, add hello following code toohello **FinishedLaunching** method:</span></span>

        // Register for push notifications.
        var settings = UIUserNotificationSettings.GetSettingsForTypes(
            UIUserNotificationType.Alert
            | UIUserNotificationType.Badge
            | UIUserNotificationType.Sound,
            new NSSet());

        UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
        UIApplication.SharedApplication.RegisterForRemoteNotifications();

    <span data-ttu-id="14584-161">Cela permet la prise en charge de l’enregistrement Push des notifications et des demandes à distance.</span><span class="sxs-lookup"><span data-stu-id="14584-161">This enables support for remote notifications and requests push registration.</span></span>

<span data-ttu-id="14584-162">Votre application est maintenant des notifications push de toosupport mis à jour.</span><span class="sxs-lookup"><span data-stu-id="14584-162">Your app is now updated toosupport push notifications.</span></span>

#### <a name="test-push-notifications-in-your-ios-app"></a><span data-ttu-id="14584-163">Tester les notifications Push dans votre application iOS</span><span class="sxs-lookup"><span data-stu-id="14584-163">Test push notifications in your iOS app</span></span>
1. <span data-ttu-id="14584-164">Droit hello iOS projet, puis cliquez sur **définir comme projet de démarrage**.</span><span class="sxs-lookup"><span data-stu-id="14584-164">Right-click hello iOS project, and click **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="14584-165">Hello de presse **exécuter** bouton ou **F5** dans Visual Studio toobuild hello du projet et démarrer l’application hello dans un appareil iOS.</span><span class="sxs-lookup"><span data-stu-id="14584-165">Press hello **Run** button or **F5** in Visual Studio toobuild hello project and start hello app in an iOS device.</span></span> <span data-ttu-id="14584-166">Puis cliquez sur **OK** tooaccept les notifications push.</span><span class="sxs-lookup"><span data-stu-id="14584-166">Then click **OK** tooaccept push notifications.</span></span>

   > [!NOTE]
   > <span data-ttu-id="14584-167">Vous devez accepter explicitement les notifications Push de votre application.</span><span class="sxs-lookup"><span data-stu-id="14584-167">You must explicitly accept push notifications from your app.</span></span> <span data-ttu-id="14584-168">Cette demande produit uniquement hello première fois que hello application s’exécute.</span><span class="sxs-lookup"><span data-stu-id="14584-168">This request only occurs hello first time that hello app runs.</span></span>
   >
   >
3. <span data-ttu-id="14584-169">Dans l’application hello, une tâche, puis tapez Bonjour signe plu (**+**) icône.</span><span class="sxs-lookup"><span data-stu-id="14584-169">In hello app, type a task, and then click hello plus (**+**) icon.</span></span>
4. <span data-ttu-id="14584-170">Vérifiez qu’une notification est reçue, puis cliquez sur **OK** toodismiss hello notification.</span><span class="sxs-lookup"><span data-stu-id="14584-170">Verify that a notification is received, and then click **OK** toodismiss hello notification.</span></span>

## <a name="configure-and-run-windows-projects-optional"></a><span data-ttu-id="14584-171">Configurer et exécuter des projets Windows (facultatif)</span><span class="sxs-lookup"><span data-stu-id="14584-171">Configure and run Windows projects (optional)</span></span>
<span data-ttu-id="14584-172">Cette section est pour l’exécution de projets Xamarin.Forms WinApp et WinPhone81 pour les appareils Windows hello.</span><span class="sxs-lookup"><span data-stu-id="14584-172">This section is for running hello Xamarin.Forms WinApp and WinPhone81 projects for Windows devices.</span></span> <span data-ttu-id="14584-173">Ces étapes prennent également en charge les projets de plateforme Windows universelle (UWP).</span><span class="sxs-lookup"><span data-stu-id="14584-173">These steps also support Universal Windows Platform (UWP) projects.</span></span> <span data-ttu-id="14584-174">Vous pouvez ignorer cette section si vous n’utilisez pas d’appareils Windows.</span><span class="sxs-lookup"><span data-stu-id="14584-174">You can skip this section if you are not working with Windows devices.</span></span>

#### <a name="register-your-windows-app-for-push-notifications-with-windows-notification-service-wns"></a><span data-ttu-id="14584-175">Inscrire votre application Windows aux notifications Push avec le service de notification Windows (Windows Notification Service, WNS)</span><span class="sxs-lookup"><span data-stu-id="14584-175">Register your Windows app for push notifications with Windows Notification Service (WNS)</span></span>
[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

#### <a name="configure-hello-notification-hub-for-wns"></a><span data-ttu-id="14584-176">Configuration d’un concentrateur de notification hello pour WNS</span><span class="sxs-lookup"><span data-stu-id="14584-176">Configure hello notification hub for WNS</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="add-push-notifications-tooyour-windows-app"></a><span data-ttu-id="14584-177">Ajouter une application Windows de push notifications tooyour</span><span class="sxs-lookup"><span data-stu-id="14584-177">Add push notifications tooyour Windows app</span></span>
1. <span data-ttu-id="14584-178">Dans Visual Studio, ouvrez **App.xaml.cs** dans une fenêtre de projet, puis ajouter hello suivant les instructions.</span><span class="sxs-lookup"><span data-stu-id="14584-178">In Visual Studio, open **App.xaml.cs** in a Windows project, and add hello following statements.</span></span>

        using Newtonsoft.Json.Linq;
        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
        using <your_TodoItemManager_portable_class_namespace>;

    <span data-ttu-id="14584-179">Remplacez `<your_TodoItemManager_portable_class_namespace>` avec espace de noms hello de votre projet portable contenant hello `TodoItemManager` classe.</span><span class="sxs-lookup"><span data-stu-id="14584-179">Replace `<your_TodoItemManager_portable_class_namespace>` with hello namespace of your portable project that contains hello `TodoItemManager` class.</span></span>
2. <span data-ttu-id="14584-180">Dans App.xaml.cs, ajoutez hello qui suit **InitNotificationsAsync** méthode :</span><span class="sxs-lookup"><span data-stu-id="14584-180">In App.xaml.cs, add hello following **InitNotificationsAsync** method:</span></span>

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

    <span data-ttu-id="14584-181">Cette méthode obtient le canal de notification push hello et enregistre un modèle tooreceive modèle les notifications à partir de votre concentrateur de notification.</span><span class="sxs-lookup"><span data-stu-id="14584-181">This method gets hello push notification channel, and registers a template tooreceive template notifications from your notification hub.</span></span> <span data-ttu-id="14584-182">Une notification de modèle qui prend en charge *messageParam* toothis client sera remis.</span><span class="sxs-lookup"><span data-stu-id="14584-182">A template notification that supports *messageParam* will be delivered toothis client.</span></span>
3. <span data-ttu-id="14584-183">Mettre à jour App.xaml.cs, hello **OnLaunched** définition de méthode de gestionnaire événement en ajoutant hello `async` modificateur.</span><span class="sxs-lookup"><span data-stu-id="14584-183">In App.xaml.cs, update hello **OnLaunched** event handler method definition by adding hello `async` modifier.</span></span> <span data-ttu-id="14584-184">Ajoutez ensuite hello suivant la ligne de code à fin hello de méthode hello :</span><span class="sxs-lookup"><span data-stu-id="14584-184">Then add hello following line of code at hello end of hello method:</span></span>

        await InitNotificationsAsync();

    <span data-ttu-id="14584-185">Cela garantit que l’enregistrement des notifications push hello est créé ou actualisé chaque fois que l’application hello est lancée.</span><span class="sxs-lookup"><span data-stu-id="14584-185">This ensures that hello push notification registration is created or refreshed every time hello app is launched.</span></span> <span data-ttu-id="14584-186">Il est important toodo cette tooguarantee qui hello de canal WNS push est toujours actif.</span><span class="sxs-lookup"><span data-stu-id="14584-186">It's important toodo this tooguarantee that hello WNS push channel is always active.</span></span>  
4. <span data-ttu-id="14584-187">Dans l’Explorateur de solutions pour Visual Studio, ouvrez hello **Package.appxmanifest** de fichiers et définissez **compatible Toast** trop**Oui** sous **Notifications**.</span><span class="sxs-lookup"><span data-stu-id="14584-187">In Solution Explorer for Visual Studio, open hello **Package.appxmanifest** file, and set **Toast Capable** too**Yes** under **Notifications**.</span></span>
5. <span data-ttu-id="14584-188">Générez l’application hello et assurez-vous de que ne avoir aucune erreur.</span><span class="sxs-lookup"><span data-stu-id="14584-188">Build hello app and verify you have no errors.</span></span> <span data-ttu-id="14584-189">Votre application cliente doit désormais s’inscrire pour les notifications de modèle hello de hello de fin dans les applications mobiles.</span><span class="sxs-lookup"><span data-stu-id="14584-189">Your client app should now register for hello template notifications from hello Mobile Apps back end.</span></span> <span data-ttu-id="14584-190">Répétez cette section pour chaque projet Windows dans votre solution.</span><span class="sxs-lookup"><span data-stu-id="14584-190">Repeat this section for every Windows project in your solution.</span></span>

#### <a name="test-push-notifications-in-your-windows-app"></a><span data-ttu-id="14584-191">Tester les notifications Push dans votre application Windows</span><span class="sxs-lookup"><span data-stu-id="14584-191">Test push notifications in your Windows app</span></span>
1. <span data-ttu-id="14584-192">Dans Visual Studio, cliquez avec le bouton droit sur un projet Windows, puis cliquez sur **Définir comme projet de démarrage**.</span><span class="sxs-lookup"><span data-stu-id="14584-192">In Visual Studio, right-click a Windows project, and click **Set as startup project**.</span></span>
2. <span data-ttu-id="14584-193">Hello de presse **exécuter** bouton projet de hello toobuild et démarrer l’application hello.</span><span class="sxs-lookup"><span data-stu-id="14584-193">Press hello **Run** button toobuild hello project and start hello app.</span></span>
3. <span data-ttu-id="14584-194">Dans l’application hello, tapez un nom pour un nouveau todoitem, puis cliquez sur hello signe plu (**+**) icône tooadd il.</span><span class="sxs-lookup"><span data-stu-id="14584-194">In hello app, type a name for a new todoitem, and then click hello plus (**+**) icon tooadd it.</span></span>
4. <span data-ttu-id="14584-195">Vérifiez qu’une notification est reçue lors de l’élément de hello est ajouté.</span><span class="sxs-lookup"><span data-stu-id="14584-195">Verify that a notification is received when hello item is added.</span></span>

## <a name="next-steps"></a><span data-ttu-id="14584-196">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="14584-196">Next steps</span></span>
<span data-ttu-id="14584-197">Apprenez-en plus sur les notifications Push :</span><span class="sxs-lookup"><span data-stu-id="14584-197">You can learn more about push notifications:</span></span>

* [<span data-ttu-id="14584-198">Diagnostiquer les problèmes de notification Push</span><span class="sxs-lookup"><span data-stu-id="14584-198">Diagnose push notification issues</span></span>](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  <span data-ttu-id="14584-199">Il existe différentes raisons pour lesquelles les notifications peuvent être perdues ou n’arrivent pas sur les appareils.</span><span class="sxs-lookup"><span data-stu-id="14584-199">There are various reasons why notifications may get dropped or do not end up on devices.</span></span> <span data-ttu-id="14584-200">Cette rubrique vous montre comment tooanalyze et déterminer la racine de hello provoquent des erreurs de notification push.</span><span class="sxs-lookup"><span data-stu-id="14584-200">This topic shows you how tooanalyze and figure out hello root cause of push notification failures.</span></span>

<span data-ttu-id="14584-201">Vous pouvez également continuer sur tooone Hello suivant didacticiels :</span><span class="sxs-lookup"><span data-stu-id="14584-201">You can also continue on tooone of hello following tutorials:</span></span>

* [<span data-ttu-id="14584-202">Ajouter une application de tooyour d’authentification</span><span class="sxs-lookup"><span data-stu-id="14584-202">Add authentication tooyour app </span></span>](app-service-mobile-xamarin-forms-get-started-users.md)  
  <span data-ttu-id="14584-203">Découvrez comment tooauthenticate les utilisateurs de votre application avec un fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="14584-203">Learn how tooauthenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="14584-204">Activer la synchronisation hors connexion pour votre application</span><span class="sxs-lookup"><span data-stu-id="14584-204">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  <span data-ttu-id="14584-205">Découvrez comment tooadd la prise en charge en mode hors connexion pour votre application à l’aide d’un Mobile Apps back-end.</span><span class="sxs-lookup"><span data-stu-id="14584-205">Learn how tooadd offline support for your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="14584-206">La synchronisation hors connexion permet aux utilisateurs d’interagir avec une application mobile &mdash;pour afficher, ajouter ou modifier des données&mdash;, même lorsqu’il n’existe aucune connexion réseau.</span><span class="sxs-lookup"><span data-stu-id="14584-206">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Images. -->

<!-- URLs. -->
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[Xcode]: https://go.microsoft.com/fwLink/?LinkID=266532
[apns object]: http://go.microsoft.com/fwlink/p/?LinkId=272333
