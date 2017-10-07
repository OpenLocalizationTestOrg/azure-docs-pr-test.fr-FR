---
title: "aaaGet a démarré avec des concentrateurs de Notification pour les applications de Xamarin.Android | Documents Microsoft"
description: "Dans ce didacticiel, vous découvrez comment toouse Azure Notification Hubs toosend push notifications tooa les applications Xamarin Android."
author: ysxu
manager: erikre
editor: 
services: notification-hubs
documentationcenter: xamarin
ms.assetid: 0be600fe-d5f3-43a5-9e5e-3135c9743e54
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: c5c7ead9a9381ab9fb6bbe86e930a8a9254813d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-with-xamarin-for-android"></a>Prendre en main Notification Hubs avec Xamarin pour Android
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Vue d'ensemble
Ce didacticiel vous montre comment toouse Azure Notification Hubs toosend push application de notifications de Xamarin.Android tooa.
Vous allez créer une application Xamarin.Android vide recevant des notifications Push via Google Cloud Messaging (GCM). Lorsque vous avez terminé, vous serez en mesure de toouse votre toobroadcast de concentrateur de notification push des appareils de hello notifications tooall votre application en cours d’exécution. Hello code terminé est disponible dans hello [NotificationHubs application] [ GitHub] exemple.

Ce didacticiel présente un scénario de diffusion simple hello dans à l’aide de concentrateurs de Notification.

## <a name="before-you-begin"></a>Avant de commencer
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

code Hello terminée pour ce didacticiel se trouve sur GitHub [ici](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/Xamarin/GetStartedXamarinAndroid).

## <a name="prerequisites"></a>Composants requis
Ce didacticiel requiert hello qui suit :

* Visual Studio avec Xamarin sur Windows ou Xamarin Studio sur Mac OS X. Des instructions d’installation complètes sont disponibles dans [Configurer et installer Visual Studio et Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).
* Un compte Google actif
* [Composant Azure Messaging]
* [Composant Client Google Cloud Messaging]

Vous devez suivre ce didacticiel avant de pouvoir suivre tous les autres didacticiels de Notification Hubs pour les applications Xamarin.Android.

> [!IMPORTANT]
> toocomplete ce didacticiel, vous devez disposer d’un compte Azure actif. Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A9C9624B5&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-android-get-started%2F).
> 
> 

## <a name="enable-google-cloud-messaging"></a>Activation de Google Cloud Messaging
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-your-notification-hub"></a>Configuration de votre hub de notification
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li><p>Cliquez sur hello <b>configurer</b> haut hello, entrez hello <b>clé API</b> valeur vous avez obtenu dans la section précédente de hello, puis cliquez sur <b>enregistrer</b>.</p>
</li>
</ol>
&emsp;&emsp;![](./media/notification-hubs-android-get-started/notification-hub-configure-android.png)

Votre concentrateur de notification est maintenant configuré toowork avec GCM, et vous disposez tooboth de chaînes de connexion hello enregistrer vos notifications tooreceive de l’application et les notifications de push toosend.

## <a name="connect-your-app-toohello-notification-hub"></a>Se connecter à votre hub de notification d’application toohello
### <a name="create-a-new-project"></a>Création d'un projet
1. Dans Xamarin Studio, cliquez sur **Nouvelle solution**, cliquez sur **Application Android**, puis sur **Suivant**.
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project1.png)

2. Saisissez le **Nom** et l’**Identificateur** de l’application. Cliquez sur hello **les plateformes cibles** toosupport et puis cliquez sur **suivant** et **créer**.
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project2.png)

    Un projet Android est créé.

1. Ouvrez les propriétés du projet hello en double-cliquant sur votre nouveau projet Bonjour affichage de solutions et en choisissant **Options**. Sélectionnez hello **Application Android** élément Bonjour **générer** section.
   
    Vérifiez cette première lettre de hello de votre **nom du Package** est en minuscules.
   
   > [!IMPORTANT]
   > Hello première lettre du nom du package hello doit être en minuscule. Sinon, vous recevrez des erreurs du manifeste d’application lors de l’inscription de vos **BroadcastReceiver** et **IntentFilter** pour les notifications Push ci-dessous.
   > 
   > 
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub--xamarin-android-app-options.png)
2. Si vous le souhaitez, jeu hello **version minimale Android** tooanother niveau de l’API.
3. Si vous le souhaitez, jeu hello **cible Android version** toohello une autre version de l’API que vous souhaitez tootarget (doit être au niveau d’API 8 ou version ultérieure).

Cliquez sur **OK** et boîte de dialogue Options du projet hello fermer.

### <a name="add-hello-required-components-tooyour-project"></a>Ajouter un projet de tooyour hello composants requis
Hello Google Cloud Messaging Client disponible sur hello magasin de composants Xamarin simplifie hello prise en charge des notifications push dans Xamarin.Android.

1. Cliquez sur le dossier composants hello Xamarin.Android application et choisissez **obtenir plusieurs composants**.
2. Recherchez hello **messagerie Azure** composant et l’ajouter toohello projet.
3. Recherchez hello **Client de messagerie Cloud Google** composant et l’ajouter toohello projet.

### <a name="set-up-notification-hubs-in-your-project"></a>Configuration de hubs de notification dans votre projet
1. Collectez hello informations pour votre application et notification votre hub Android suivantes :
   
   * **GoogleProjectNumber**: obtenir cette valeur de numéro de projet à partir de la vue d’ensemble de hello de votre application sur hello portail des développeurs Google. Vous avez notée précédemment cette valeur lorsque vous avez créé l’application hello sur le portail hello.
   * **Écouter la chaîne de connexion**: tableau de bord hello Bonjour [portail classique Azure], cliquez sur **afficher les chaînes de connexion**. Hello de copie *DefaultListenSharedAccessSignature* chaîne de connexion pour cette valeur.
   * **Nom du Hub**: nom de hello de votre concentrateur hello [portail classique Azure]. Par exemple, *mynotificationhub2*.
     
     Créer un **Constants.cs** classe pour votre projet Xamarin et définir hello suivant de valeurs constantes dans la classe hello. Remplacez les espaces réservés de hello avec vos valeurs.
     
       public static class Constants   {
     
           public const string SenderID = "<GoogleProjectNumber>"; // Google API Project Number
           public const string ListenConnectionString = "<Listen connection string>";
           public const string NotificationHubName = "<hub name>";
       }
2. Ajoutez hello qui suit à l’aide d’instructions trop**MainActivity.cs**:
   
        using Android.Util;
        using Gcm.Client;
3. Ajouter un toohello de variable d’instance `MainActivity` classe qui sera utilisé tooshow une boîte de dialogue alerte lors de l’application hello est en cours d’exécution :
   
        public static MainActivity instance;
4. Créer hello méthode Bonjour **MainActivity** classe :
   
        private void RegisterWithGCM()
        {
            // Check tooensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);
   
            // Register for push notifications
            Log.Info("MainActivity", "Registering...");
            GcmClient.Register(this, Constants.SenderID);
        }
5. Bonjour `OnCreate` méthode **MainActivity.cs**, initialiser hello `instance` variable et ajoutez un appel trop`RegisterWithGCM`:
   
        protected override void OnCreate (Bundle bundle)
        {
            instance = this;
   
            base.OnCreate (bundle);
   
            // Set your view from hello "main" layout resource
            SetContentView (Resource.Layout.Main);
   
            // Get your button from hello layout resource,
            // and attach an event tooit
            Button button = FindViewById<Button> (Resource.Id.myButton);
   
            RegisterWithGCM();
        }
6. Créez la classe **MyBroadcastReceiver**.
   
   > [!NOTE]
   > Nous allons décrire la procédure à suivre pour créer une classe **BroadcastReceiver** de toutes pièces. Toutefois, une création rapide toomanually autre **MyBroadcastReceiver.cs** est toorefer toohello **GcmService.cs** fichier trouvé dans hello exemple de projet Xamarin.Android inclus avec hello [NotificationHubs exemples][GitHub]. Duplication de **GcmService.cs** et la modification des noms de classe peut être un toostart idéal également.
   > 
   > 
7. Ajoutez hello qui suit à l’aide d’instructions trop**MyBroadcastReceiver.cs** (référence toohello composant et l’assembly que vous avez ajouté précédemment) :
   
        using System.Collections.Generic;
        using System.Text;
        using Android.App;
        using Android.Content;
        using Android.Util;
        using Gcm.Client;
        using WindowsAzure.Messaging;
8. Dans **MyBroadcastReceiver.cs**, ajouter hello suivant des demandes d’autorisations entre hello **à l’aide de** instructions et hello **espace de noms** déclaration :
   
        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
   
        //GET_ACCOUNTS is needed only for Android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
9. Dans **MyBroadcastReceiver.cs**, modifiez hello **MyBroadcastReceiver** suivant de hello toomatch de classe :
   
        [BroadcastReceiver(Permission=Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        public class MyBroadcastReceiver : GcmBroadcastReceiverBase<PushHandlerService>
        {
            public static string[] SENDER_IDS = new string[] { Constants.SenderID };
   
            public const string TAG = "MyBroadcastReceiver-GCM";
        }
10. Dans **MyBroadcastReceiver.cs**, ajoutez une classe nommée **PushHandlerService** dérivée de **GcmServiceBase**. Assurez-vous que tooapply hello **Service** toohello classe d’attributs :
    
         [Service] // Must use hello service tag
         public class PushHandlerService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }
             private NotificationHub Hub { get; set; }
    
             public PushHandlerService() : base(Constants.SenderID)
                {
                 Log.Info(MyBroadcastReceiver.TAG, "PushHandlerService() constructor");
             }
         }
11. **GcmServiceBase** implémente les méthodes **OnRegistered()**, **OnUnRegistered()**, **OnMessage()**, **OnRecoverableError()** et **OnError()**. Notre **PushHandlerService** classe d’implémentation doit substituer ces méthodes et ces méthodes déclenchent dans toointeracting de réponse avec un concentrateur de notification hello.
12. Remplacer hello **OnRegistered()** méthode dans **PushHandlerService** à l’aide de hello suivant de code :
    
         protected override void OnRegistered(Context context, string registrationId)
         {
             Log.Verbose(MyBroadcastReceiver.TAG, "GCM Registered: " + registrationId);
             RegistrationID = registrationId;
    
             createNotification("PushHandlerService-GCM Registered...",
                                 "hello device has been Registered!");
    
             Hub = new NotificationHub(Constants.NotificationHubName, Constants.ListenConnectionString,
                                         context);
             try
             {
                 Hub.UnregisterAll(registrationId);
             }
             catch (Exception ex)
             {
                 Log.Error(MyBroadcastReceiver.TAG, ex.Message);
             }
    
             //var tags = new List<string>() { "falcons" }; // create tags if you want
             var tags = new List<string>() {};
    
             try
             {
                 var hubRegistration = Hub.Register(registrationId, tags.ToArray());
             }
             catch (Exception ex)
             {
                 Log.Error(MyBroadcastReceiver.TAG, ex.Message);
             }
         }
    
    > [!NOTE]
    > Bonjour **OnRegistered()** de code ci-dessus, vous devez noter hello capacité toospecify balises tooregister pour les canaux de messagerie spécifiques.
    > 
    > 
13. Remplacer hello **OnMessage** méthode dans **PushHandlerService** à l’aide de hello suivant de code :
    
        protected override void OnMessage(Context context, Intent intent)
        {
            Log.Info(MyBroadcastReceiver.TAG, "GCM Message Received!");
    
            var msg = new StringBuilder();
    
            if (intent != null && intent.Extras != null)
            {
                foreach (var key in intent.Extras.KeySet())
                    msg.AppendLine(key + "=" + intent.Extras.Get(key).ToString());
            }
    
            string messageText = intent.Extras.GetString("message");
            if (!string.IsNullOrEmpty (messageText))
            {
                createNotification ("New hub message!", messageText);
            }
            else
            {
                createNotification ("Unknown message details", msg.ToString ());
            }
        }
14. Ajoutez hello suivant **createNotification** et **dialogNotify** méthodes trop**PushHandlerService** pour avertir les utilisateurs lorsqu’une notification est reçue.
    
    > [!NOTE]
    > La conception des notifications dans Android version 5.0 et ultérieure est radicalement différente de celle des versions précédentes. Si vous testez cette sur Android 5.0 ou version ultérieure, application hello devez toobe notification de hello tooreceive en cours d’exécution. Pour plus d’informations, consultez [Notifications Android](http://go.microsoft.com/fwlink/?LinkId=615880).
    > 
    > 
    
        void createNotification(string title, string desc)
        {
            //Create notification
            var notificationManager = GetSystemService(Context.NotificationService) as NotificationManager;
    
            //Create an intent tooshow UI
            var uiIntent = new Intent(this, typeof(MainActivity));
    
            //Create hello notification
            var notification = new Notification(Android.Resource.Drawable.SymActionEmail, title);
    
            //Auto-cancel will remove hello notification once hello user touches it
            notification.Flags = NotificationFlags.AutoCancel;
    
            //Set hello notification info
            //we use hello pending intent, passing our ui intent over, which will get called
            //when hello notification is tapped.
            notification.SetLatestEventInfo(this, title, desc, PendingIntent.GetActivity(this, 0, uiIntent, 0));
    
            //Show hello notification
            notificationManager.Notify(1, notification);
            dialogNotify (title, desc);
        }
    
        protected void dialogNotify(String title, String message)
        {
    
            MainActivity.instance.RunOnUiThread(() => {
                AlertDialog.Builder dlg = new AlertDialog.Builder(MainActivity.instance);
                AlertDialog alert = dlg.Create();
                alert.SetTitle(title);
                alert.SetButton("Ok", delegate {
                    alert.Dismiss();
                });
                alert.SetMessage(message);
                alert.Show();
            });
        }
15. Remplacez les membres abstraits **OnUnRegistered()**, **OnRecoverableError()** et **OnError()** pour pouvoir compiler votre code :
    
        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Verbose(MyBroadcastReceiver.TAG, "GCM Unregistered: " + registrationId);
    
            createNotification("GCM Unregistered...", "hello device has been unregistered!");
        }
    
        protected override bool OnRecoverableError(Context context, string errorId)
        {
            Log.Warn(MyBroadcastReceiver.TAG, "Recoverable Error: " + errorId);
    
            return base.OnRecoverableError (context, errorId);
        }
    
        protected override void OnError(Context context, string errorId)
        {
            Log.Error(MyBroadcastReceiver.TAG, "GCM Error: " + errorId);
        }

## <a name="run-your-app-in-hello-emulator"></a>Exécuter votre application dans l’émulateur de hello
Si vous exécutez cette application dans l’émulateur de hello, assurez-vous que vous utilisez un virtuel appareil (Android) qui prend en charge APIs de Google.

> [!IMPORTANT]
> Dans les notifications de push de tooreceive de commande, vous devez configurer un compte Google sur votre appareil virtuel Android. (Dans l’émulateur de hello, accédez trop**paramètres** et cliquez sur **ajouter un compte**.) En outre, assurez-vous qu’émulateur hello est connecté toohello Internet.
> 
> [!NOTE]
> La conception des notifications dans Android version 5.0 et ultérieure est radicalement différente de celle des versions précédentes. Pour plus d’informations, consultez [Notifications Android](http://go.microsoft.com/fwlink/?LinkId=615880).
> 
> 

1. Dans **Outils**, cliquez sur **Open Android Emulator Manager**, sélectionnez votre appareil, puis cliquez sur **Modifier**.
   
      ![][18]
2. Sélectionnez **API Google** dans **Cible**, puis cliquez sur **OK**.
   
      ![][19]
3. Dans la barre d’outils supérieure hello, cliquez sur **exécuter**, puis sélectionnez votre application. Cela démarre l’émulateur hello et exécute l’application hello.
   
   application Hello récupère hello *registrationId* GCM et inscrit avec le hub de notification hello.

## <a name="send-notifications-from-your-backend"></a>Envoi de notifications à partir de votre serveur principal
Vous pouvez tester la réception de notifications dans votre application en envoyant des notifications Bonjour [portail classique Azure] via hello debug onglet concentrateur de notification hello, comme indiqué dans l’écran hello ci-dessous.

![][30]

Les notifications Push sont normalement envoyées dans un service principal tel que Mobile Services ou ASP.NET par le biais d’une bibliothèque compatible. Vous pouvez également utiliser les API REST de hello directement les messages de notification de toosend si une bibliothèque n’est pas disponible pour votre serveur principal.

Voici une liste de certains autres didacticiels que vous pourriez vouloir tooreview pour envoyer des notifications :

* ASP.NET : Consultez [utiliser Notification Hubs toopush notifications toousers].
* Java de concentrateurs de Notification Azure SDK : consultez [comment toouse concentrateurs de Notification à partir de Java](notification-hubs-java-push-notification-tutorial.md) pour envoyer des notifications à partir de Java. Il a été testé dans Eclipse pour le développement Android.
* PHP : Consultez [comment toouse concentrateurs de Notification à partir de PHP](notification-hubs-php-push-notification-tutorial.md).

Dans hello suivant sous-sections suivantes du didacticiel de hello, vous envoyez des notifications à l’aide d’une application de console .NET et à l’aide d’un service mobile via un script de nœud.

#### <a name="optional-send-notifications-by-using-a-net-app"></a>(Facultatif) Pour envoyer des notifications en utilisant une application .NET :
Dans cette section, nous allons envoyer des notifications à l’aide d’une application de console .NET.

1. Créez une application console Visual C# :
   
      ![][20]
2. Dans Visual Studio, cliquez successivement sur **Outils**, **Gestionnaire de package NuGet** et **Console du gestionnaire de package**.
   
    Cela affiche hello Package Manager Console dans Visual Studio.
3. Dans la fenêtre de Console du Gestionnaire de Package de hello, définissez hello **projet par défaut** tooyour nouveau projet d’application console et puis, dans la fenêtre de console hello, exécutez hello de commande suivante :
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    Cette opération ajoute une référence de toohello Azure Notification Hubs SDK à l’aide de hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">package NuGet de concentrateurs Microsoft.Azure.Notification</a>.
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. Ouvrez le fichier Program.cs de hello et ajoutez hello suit `using` instruction :
   
        using Microsoft.Azure.NotificationHubs;
5. Dans votre `Program` de classe, ajoutez hello suivant de méthode. Mettre à jour le texte d’espace réservé hello avec votre *DefaultFullSharedAccessSignature* nom de hub et la chaîne de connexion à partir de hello [portail classique Azure].
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            await hub.SendGcmNativeNotificationAsync("{ \"data\" : {\"message\":\"Hello from Azure!\"}}");
        }
6. Ajouter hello suivant des lignes dans votre **Main** méthode :
   
         SendNotificationAsync();
         Console.ReadLine();
7. Appuyez sur la touche application de hello toorun clé hello F5. Vous devriez recevoir une notification dans l’application hello.
   
      ![][21]

#### <a name="optional-send-notifications-by-using-a-mobile-service"></a>(Facultatif) Envoyer une notification à l’aide d’un service mobile
1. Suivez les procédures [Prise en main de Mobile Services].
2. Connectez-vous à toohello [portail classique Azure], puis sélectionnez votre service mobile.
3. Sélectionnez hello **planificateur** onglet en haut de hello.
   
      ![][22]
4. Créez un travail planifié, insérez un nom, puis sélectionnez **On demand**.
   
      ![][23]
5. Lorsque le travail de hello est créé, cliquez sur le nom de la tâche hello. Puis cliquez sur hello **Script** onglet sur la barre supérieure de hello.
6. Insérez hello script à l’intérieur de votre fonction Planificateur suivant. Rendre des espaces réservés de hello tooreplace vraiment avec votre notification hub hello et nom de chaîne de connexion pour *DefaultFullSharedAccessSignature* que vous avez obtenu précédemment. Cliquez sur **Enregistrer**.
   
        var azure = require('azure');
        var notificationHubService = azure.createNotificationHubService('<hub name>', '<connection string>');
        notificationHubService.gcm.send(null,'{"data":{"message" : "Hello from Mobile Services!"}}',
          function (error)
          {
            if (!error) {
               console.warn("Notification successful");
            }
            else
            {
              console.warn("Notification failed" + error);
            }
          }
        );
7. Cliquez sur **exécuter une fois** sur la barre inférieure de hello. Vous devez recevoir une notification toast.

## <a name="next-steps"></a>Étapes suivantes
Dans cet exemple simple, diffusées notifications tooall vos appareils Android. Dans l’ordre tootarget des utilisateurs spécifiques, consultez le didacticiel de toohello [utiliser Notification Hubs toopush notifications toousers]. Si vous souhaitez toosegment vos utilisateurs en groupes d’intérêt, vous pouvez lire [toosend utiliser Notification Hubs actualités]. En savoir plus sur la façon toouse Notification Hubs dans [des conseils de concentrateurs de Notification] et Bonjour [concentrateurs de Notification toofor de façon Android].

<!-- Anchors. -->
[Enable Google Cloud Messaging]: #register
[Configure your Notification Hub]: #configure-hub
[Connecting your app toohello Notification Hub]: #connecting-app
[Run your app with hello emulator]: #run-app
[Send notifications from your back-end]: #send
[Next steps]:#next-steps

<!-- Images. -->

[11]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-configure-android.png

[13]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-app1.png
[15]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-app3.png

[18]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-android-app7.png
[19]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-android-app8.png

[20]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-console-app.png
[21]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-android-toast.png
[22]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-scheduler1.png
[23]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-scheduler2.png

[30]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hubs-debug-hub-gcm.png


<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Prise en main de Mobile Services]: /develop/mobile/tutorials/get-started-xamarin-android/#create-new-service
[JavaScript and HTML]: /develop/mobile/tutorials/get-started-with-push-js

[portail classique Azure]: https://manage.windowsazure.com/
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[des conseils de concentrateurs de Notification]: http://msdn.microsoft.com/library/jj927170.aspx
[concentrateurs de Notification toofor de façon Android]: http://msdn.microsoft.com/library/dn282661.aspx

[utiliser Notification Hubs toopush notifications toousers]: /manage/services/notification-hubs/notify-users-aspnet
[toosend utiliser Notification Hubs actualités]: /manage/services/notification-hubs/breaking-news-dotnet
[GCMClient Component page]: http://components.xamarin.com/view/GCMClient
[Xamarin.NotificationHub GitHub page]: https://github.com/SaschaDittmann/Xamarin.NotificationHub
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
[Composant Client Google Cloud Messaging]: http://components.xamarin.com/view/GCMClient/
[Composant Azure Messaging]: http://components.xamarin.com/view/azure-messaging
