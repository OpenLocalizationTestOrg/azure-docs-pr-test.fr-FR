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
# <a name="add-push-notifications-tooyour-xamarinforms-app"></a>Ajouter une application de Xamarin.Forms de tooyour de notifications push
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Vue d'ensemble
Dans ce didacticiel, vous ajoutez des projets push notifications tooall hello résultant hello [démarrage rapide de Xamarin.Forms](app-service-mobile-xamarin-forms-get-started.md). Cela signifie qu’une notification push est envoyée clients d’inter-plateformes tooall chaque fois qu’un enregistrement est inséré.

Si vous n’utilisez pas hello téléchargé le projet de démarrage rapide de serveur, vous devez serez hello package d’extension de notification push. Pour plus d’informations, consultez [fonctionne avec serveur principal de .NET hello SDK pour les applications mobiles Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

## <a name="prerequisites"></a>Composants requis
Pour iOS, vous avez besoin d’une [appartenance au programme pour développeurs Apple](https://developer.apple.com/programs/ios/) et d’un appareil iOS physique. Hello [simulateur iOS ne prend pas en charge des notifications push](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).

## <a name="configure-hub"></a>Configurer un hub de notification
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="update-hello-server-project-toosend-push-notifications"></a>Mettre à jour des notifications push de hello serveur projet toosend
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-and-run-hello-android-project-optional"></a>Configurer et exécuter le projet Android de hello (facultatif)
Effectuez cette section tooenable des notifications push pour hello Xamarin.Forms Droid projet pour Android.

### <a name="enable-firebase-cloud-messaging-fcm"></a>Activation de Firebase Cloud Messaging (FCM)
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

### <a name="configure-hello-mobile-apps-back-end-toosend-push-requests-by-using-fcm"></a>Configurer les demandes de transmission toosend hello Mobile Apps back-end à l’aide de FCM
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

### <a name="add-push-notifications-toohello-android-project"></a>Ajouter le projet Android des toohello des notifications push
Avec hello serveur principal configuré avec FCM, vous pouvez ajouter des composants et des codes tooregister de client toohello avec FCM. Vous pouvez également vous inscrire pour les notifications push avec Azure Notification Hubs via hello dans les applications mobiles se termine et recevoir des notifications.

1. Bonjour **Droid** de projet, avec le bouton droit hello **composants** dossier, puis cliquez sur **obtenir plusieurs composants...** . Puis recherchez hello **Client de messagerie Cloud Google** composant et l’ajouter toohello projet. Ce composant prend en charge les notifications Push pour un projet Xamarin Android.
2. Ouvrez le fichier de projet MainActivity.cs hello et ajoutez hello après l’instruction de haut hello du fichier de hello :

        using Gcm.Client;
3. Ajouter hello suivant code toohello **OnCreate** méthode après hello appeler trop**LoadApplication**:

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
4. Ajoutez une nouvelle méthode d’assistance **CreateAndShowDialog** , comme suit :

        private void CreateAndShowDialog(String message, String title)
        {
            AlertDialog.Builder builder = new AlertDialog.Builder(this);

            builder.SetMessage (message);
            builder.SetTitle (title);
            builder.Create().Show ();
        }
5. Ajouter hello suivant code toohello **MainActivity** classe :

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

    Cela expose hello actuel **MainActivity** de l’instance, donc nous pouvons exécuter sur le thread d’interface utilisateur hello.
6. Initialiser hello `instance` variable au début de hello Hello **OnCreate** méthode, comme suit.

        // Set hello current instance of MainActivity.
        instance = this;
7. Ajouter un nouveau toohello de fichier de classe **Droid** projet nommé `GcmService.cs`et assurez-vous que suivant de hello **à l’aide de** instructions figurent en haut de hello du fichier de hello :

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
8. Ajouter hello suivant des demandes d’autorisations haut hello du fichier hello après hello **à l’aide de** instructions et avant hello **espace de noms** déclaration.

        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
        //GET_ACCOUNTS is only needed for android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
9. Ajoutez hello suivant toohello de définition de classe namespace.

       [BroadcastReceiver(Permission = Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY }, Categories = new string[] { "@PACKAGE_NAME@" })]
       public class PushHandlerBroadcastReceiver : GcmBroadcastReceiverBase<GcmService>
       {
           public static string[] SENDER_IDS = new string[] { "<PROJECT_NUMBER>" };
       }

   > [!NOTE]
   > Remplacez **<PROJECT_NUMBER>** par le numéro de projet noté précédemment.    
   >
   >
10. Remplacez hello vide **GcmService** classe avec hello suivant de code, qui utilise un récepteur de diffusion nouvelle hello :

         [Service]
         public class GcmService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }

             public GcmService()
                 : base(PushHandlerBroadcastReceiver.SENDER_IDS){}
         }
11. Ajouter hello suivant code toohello **GcmService** classe. Cela remplace hello **OnRegistered** Gestionnaire d’événements et met en œuvre un **inscrire** (méthode).

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

    Notez que ce code utilise hello `messageParam` paramètre dans l’inscription de modèle hello.
12. Ajouter hello suivant le code qui implémente **OnMessage**:

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

    Cela gère les notifications entrantes et les envoie toohello notification manager toobe est affiché.
13. **GcmServiceBase** nécessite également que vous tooimplement hello **OnUnRegistered** et **OnError** les méthodes de gestionnaire, vous pouvez procédez comme suit :

        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "Unregistered RegisterationId : " + registrationId);
        }

        protected override void OnError(Context context, string errorId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "GCM Error: " + errorId);
        }

Maintenant, vous test prêt des notifications push dans l’application hello en cours d’exécution sur un appareil Android ou hello émulateur.

### <a name="test-push-notifications-in-your-android-app"></a>Tester les notifications Push dans votre application Android
Hello deux premières étapes sont requis uniquement lorsque vous testez sur un émulateur.

1. Assurez-vous que vous déployez tooor débogage sur un périphérique virtuel qui a APIs Google définir comme cible de hello, comme indiqué ci-dessous dans le Gestionnaire d’appareil virtuel Android hello.
2. Ajouter un appareil Android de Google compte toohello en cliquant sur **applications** > **paramètres** > **Ajouter compte**. Suivez ensuite hello invites tooadd une unité de toohello compte Google ou toocreate un nouveau.
3. Dans Visual Studio ou Xamarin Studio, avec le bouton droit hello **Droid** projet puis cliquez sur **définir comme projet de démarrage**.
4. Cliquez sur **exécuter** toobuild hello du projet et démarrer l’application hello sur votre appareil Android ou l’émulateur.
5. Dans l’application hello, une tâche, puis tapez Bonjour signe plu (**+**) icône.
6. Vérifiez qu’une notification est reçue lorsqu’un élément est ajouté.

## <a name="configure-and-run-hello-ios-project-optional"></a>Configurer et exécuter le projet iOS de hello (facultatif)
Cette section est de projet d’iOS Xamarin hello pour les appareils iOS en cours d’exécution. Vous pouvez ignorer cette section si vous n’utilisez pas d’appareils iOS.

[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

#### <a name="configure-hello-notification-hub-for-apns"></a>Configuration d’un concentrateur de notification hello pour APNS
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

Ensuite, vous allez configurer des paramètres de projet iOS hello dans Xamarin Studio ou Visual Studio.

[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

#### <a name="add-push-notifications-tooyour-ios-app"></a>Ajouter une application iOS de push notifications tooyour
1. Bonjour **iOS** de projet, ouvrez AppDelegate.cs et ajoutez hello suivant en haut de toohello instruction hello du fichier de code.

        using Newtonsoft.Json.Linq;
2. Bonjour **AppDelegate** de classe, ajoutez un remplacement pour hello **RegisteredForRemoteNotifications** tooregister d’événements pour les notifications :

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
3. Dans **AppDelegate**, ajoutez également hello après remplacement de hello **DidReceiveRemoteNotification** Gestionnaire d’événements :

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

    Cette méthode gère les notifications entrantes pendant que l’application hello est en cours d’exécution.
4. Bonjour **AppDelegate** de classe, ajoutez hello suivant code toohello **FinishedLaunching** méthode :

        // Register for push notifications.
        var settings = UIUserNotificationSettings.GetSettingsForTypes(
            UIUserNotificationType.Alert
            | UIUserNotificationType.Badge
            | UIUserNotificationType.Sound,
            new NSSet());

        UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
        UIApplication.SharedApplication.RegisterForRemoteNotifications();

    Cela permet la prise en charge de l’enregistrement Push des notifications et des demandes à distance.

Votre application est maintenant des notifications push de toosupport mis à jour.

#### <a name="test-push-notifications-in-your-ios-app"></a>Tester les notifications Push dans votre application iOS
1. Droit hello iOS projet, puis cliquez sur **définir comme projet de démarrage**.
2. Hello de presse **exécuter** bouton ou **F5** dans Visual Studio toobuild hello du projet et démarrer l’application hello dans un appareil iOS. Puis cliquez sur **OK** tooaccept les notifications push.

   > [!NOTE]
   > Vous devez accepter explicitement les notifications Push de votre application. Cette demande produit uniquement hello première fois que hello application s’exécute.
   >
   >
3. Dans l’application hello, une tâche, puis tapez Bonjour signe plu (**+**) icône.
4. Vérifiez qu’une notification est reçue, puis cliquez sur **OK** toodismiss hello notification.

## <a name="configure-and-run-windows-projects-optional"></a>Configurer et exécuter des projets Windows (facultatif)
Cette section est pour l’exécution de projets Xamarin.Forms WinApp et WinPhone81 pour les appareils Windows hello. Ces étapes prennent également en charge les projets de plateforme Windows universelle (UWP). Vous pouvez ignorer cette section si vous n’utilisez pas d’appareils Windows.

#### <a name="register-your-windows-app-for-push-notifications-with-windows-notification-service-wns"></a>Inscrire votre application Windows aux notifications Push avec le service de notification Windows (Windows Notification Service, WNS)
[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

#### <a name="configure-hello-notification-hub-for-wns"></a>Configuration d’un concentrateur de notification hello pour WNS
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="add-push-notifications-tooyour-windows-app"></a>Ajouter une application Windows de push notifications tooyour
1. Dans Visual Studio, ouvrez **App.xaml.cs** dans une fenêtre de projet, puis ajouter hello suivant les instructions.

        using Newtonsoft.Json.Linq;
        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
        using <your_TodoItemManager_portable_class_namespace>;

    Remplacez `<your_TodoItemManager_portable_class_namespace>` avec espace de noms hello de votre projet portable contenant hello `TodoItemManager` classe.
2. Dans App.xaml.cs, ajoutez hello qui suit **InitNotificationsAsync** méthode :

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

    Cette méthode obtient le canal de notification push hello et enregistre un modèle tooreceive modèle les notifications à partir de votre concentrateur de notification. Une notification de modèle qui prend en charge *messageParam* toothis client sera remis.
3. Mettre à jour App.xaml.cs, hello **OnLaunched** définition de méthode de gestionnaire événement en ajoutant hello `async` modificateur. Ajoutez ensuite hello suivant la ligne de code à fin hello de méthode hello :

        await InitNotificationsAsync();

    Cela garantit que l’enregistrement des notifications push hello est créé ou actualisé chaque fois que l’application hello est lancée. Il est important toodo cette tooguarantee qui hello de canal WNS push est toujours actif.  
4. Dans l’Explorateur de solutions pour Visual Studio, ouvrez hello **Package.appxmanifest** de fichiers et définissez **compatible Toast** trop**Oui** sous **Notifications**.
5. Générez l’application hello et assurez-vous de que ne avoir aucune erreur. Votre application cliente doit désormais s’inscrire pour les notifications de modèle hello de hello de fin dans les applications mobiles. Répétez cette section pour chaque projet Windows dans votre solution.

#### <a name="test-push-notifications-in-your-windows-app"></a>Tester les notifications Push dans votre application Windows
1. Dans Visual Studio, cliquez avec le bouton droit sur un projet Windows, puis cliquez sur **Définir comme projet de démarrage**.
2. Hello de presse **exécuter** bouton projet de hello toobuild et démarrer l’application hello.
3. Dans l’application hello, tapez un nom pour un nouveau todoitem, puis cliquez sur hello signe plu (**+**) icône tooadd il.
4. Vérifiez qu’une notification est reçue lors de l’élément de hello est ajouté.

## <a name="next-steps"></a>Étapes suivantes
Apprenez-en plus sur les notifications Push :

* [Diagnostiquer les problèmes de notification Push](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  Il existe différentes raisons pour lesquelles les notifications peuvent être perdues ou n’arrivent pas sur les appareils. Cette rubrique vous montre comment tooanalyze et déterminer la racine de hello provoquent des erreurs de notification push.

Vous pouvez également continuer sur tooone Hello suivant didacticiels :

* [Ajouter une application de tooyour d’authentification](app-service-mobile-xamarin-forms-get-started-users.md)  
  Découvrez comment tooauthenticate les utilisateurs de votre application avec un fournisseur d’identité.
* [Activer la synchronisation hors connexion pour votre application](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  Découvrez comment tooadd la prise en charge en mode hors connexion pour votre application à l’aide d’un Mobile Apps back-end. La synchronisation hors connexion permet aux utilisateurs d’interagir avec une application mobile &mdash;pour afficher, ajouter ou modifier des données&mdash;, même lorsqu’il n’existe aucune connexion réseau.

<!-- Images. -->

<!-- URLs. -->
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[Xcode]: https://go.microsoft.com/fwLink/?LinkID=266532
[apns object]: http://go.microsoft.com/fwlink/p/?LinkId=272333
