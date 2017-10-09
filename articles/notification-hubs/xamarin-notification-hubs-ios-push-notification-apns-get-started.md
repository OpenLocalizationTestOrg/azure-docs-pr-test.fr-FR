---
title: aaaiOS des Notifications Push avec Notification Hubs pour les applications Xamarin | Documents Microsoft
description: "Dans ce didacticiel, vous découvrez comment toouse Azure Notification Hubs toosend push application iOS de notifications tooa Xamarin."
services: notification-hubs
keywords: notifications push iOS, messages push, notifications push, envoi de messages
documentationcenter: xamarin
author: ysxu
manager: erikre
editor: 
ms.assetid: 4d4dfd42-c5a5-4360-9d70-7812f96924d2
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 8db60338047dd53074b4d3d4bb127aa6d9f13a25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="ios-push-notifications-with-notification-hubs-for-xamarin-apps"></a><span data-ttu-id="1b82c-104">Notifications Push iOS à l’aide des hubs de notification pour applications Xamarin</span><span class="sxs-lookup"><span data-stu-id="1b82c-104">iOS Push Notifications with Notification Hubs for Xamarin apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="1b82c-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="1b82c-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1b82c-106">toocomplete ce didacticiel, vous devez disposer d’un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="1b82c-106">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="1b82c-107">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="1b82c-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="1b82c-108">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="1b82c-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="1b82c-109">Ce didacticiel vous montre comment toouse Azure Notification Hubs toosend push application iOS de tooan des notifications.</span><span class="sxs-lookup"><span data-stu-id="1b82c-109">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooan iOS application.</span></span>
<span data-ttu-id="1b82c-110">Vous allez créer une application Xamarin.iOS vide qui reçoit des notifications push à l’aide de hello [services de notifications Push Apple (APN)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html).</span><span class="sxs-lookup"><span data-stu-id="1b82c-110">You'll create a blank Xamarin.iOS app that receives push notifications by using hello [Apple Push Notification Service (APNs)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html).</span></span> <span data-ttu-id="1b82c-111">Lorsque vous avez terminé, vous serez en mesure de toouse votre toobroadcast de concentrateur de notification push des appareils de hello notifications tooall votre application en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="1b82c-111">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span> <span data-ttu-id="1b82c-112">Hello code terminé est disponible dans hello [NotificationHubs application] [ GitHub] exemple.</span><span class="sxs-lookup"><span data-stu-id="1b82c-112">hello finished code is available in hello [NotificationHubs app][GitHub] sample.</span></span>

<span data-ttu-id="1b82c-113">Ce didacticiel illustre un scénario diffusion de messages hello simple push avec Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="1b82c-113">This tutorial demonstrates hello simple push message broadcast scenario with Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b82c-114">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1b82c-114">Prerequisites</span></span>
<span data-ttu-id="1b82c-115">Ce didacticiel requiert hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="1b82c-115">This tutorial requires hello following:</span></span>

* <span data-ttu-id="1b82c-116">[Xcode 6.0][Install Xcode]</span><span class="sxs-lookup"><span data-stu-id="1b82c-116">[Xcode 6.0][Install Xcode]</span></span>
* <span data-ttu-id="1b82c-117">Un appareil compatible iOS 7.0 (ou version ultérieure)</span><span class="sxs-lookup"><span data-stu-id="1b82c-117">An iOS 7.0 (or later version) compatible device</span></span>
* <span data-ttu-id="1b82c-118">Un abonnement au programme pour développeurs iOS</span><span class="sxs-lookup"><span data-stu-id="1b82c-118">iOS Developer Program membership</span></span>
* <span data-ttu-id="1b82c-119">[Xamarin Studio]</span><span class="sxs-lookup"><span data-stu-id="1b82c-119">[Xamarin Studio]</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="1b82c-120">En raison de la configuration requise pour les notifications de push iOS, vous devez déployer et tester l’application d’exemple hello sur un appareil physique iOS (iPhone ou iPad) au lieu de dans le simulateur de hello.</span><span class="sxs-lookup"><span data-stu-id="1b82c-120">Because of configuration requirements for iOS push notifications, you must deploy and test hello sample application on a physical iOS device (iPhone or iPad) instead of in hello simulator.</span></span>
  > 
  > 

<span data-ttu-id="1b82c-121">Vous devez suivre ce didacticiel avant de pouvoir suivre tous les autres didacticiels dédiés aux hubs de notification pour applications Xamarin iOS.</span><span class="sxs-lookup"><span data-stu-id="1b82c-121">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Xamarin iOS apps.</span></span>

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub"></a><span data-ttu-id="1b82c-122">Configuration de votre hub de notification</span><span class="sxs-lookup"><span data-stu-id="1b82c-122">Configure your notification hub</span></span>
<span data-ttu-id="1b82c-123">Cette section présente la création d’un concentrateur de notification et de configuration de l’authentification avec APNS à l’aide de hello **.p12** : certificat push que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="1b82c-123">This section walks you through creating a new notification hub and configuring authentication with APNS using hello **.p12** push certificate that you created.</span></span> <span data-ttu-id="1b82c-124">Si vous voulez toouse un concentrateur de notification que vous avez déjà créé, vous pouvez ignorer toostep 5.</span><span class="sxs-lookup"><span data-stu-id="1b82c-124">If you want toouse a notification hub that you have already created, you can skip toostep 5.</span></span>

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li>

<p><span data-ttu-id="1b82c-125">Comme nous voulons tooconfigure hello APNS connexion, hello portail Azure, ouvrir les paramètres de Notification Hub, ande cliquez sur <b>Notification Services</b>, puis cliquez sur hello <b>Apple (APN)</b> élément de liste de hello.</span><span class="sxs-lookup"><span data-stu-id="1b82c-125">As we want tooconfigure hello APNS connection, in hello Azure Portal, open your Notification Hub settings, ande click on <b>Notification Services</b>, and then click hello <b>Apple (APNS)</b> item in hello list.</span></span> <span data-ttu-id="1b82c-126">Une fois terminé, cliquez sur <b>télécharger un certificat</b> et sélectionnez hello <b>.p12</b> certificat que vous avez exporté précédemment, ainsi que d’un mot de passe hello pour les certificats hello.</span><span class="sxs-lookup"><span data-stu-id="1b82c-126">Once done, click on <b>Upload Certificate</b> and select hello <b>.p12</b> certificate that you exported earlier, as well as hello password for hello certificate.</span></span></p>

<p><span data-ttu-id="1b82c-127">Assurez-vous que tooselect <b>Sandbox</b> mode étant donné que vous allez envoyer par émission de données des messages dans un environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="1b82c-127">Make sure tooselect <b>Sandbox</b> mode since you will be sending push messages in a development environment.</span></span> <span data-ttu-id="1b82c-128">Utilisez uniquement hello <b>Production</b> paramètre si vous souhaitez toousers de notifications push toosend qui ont déjà acheté votre application à partir du magasin de hello.</span><span class="sxs-lookup"><span data-stu-id="1b82c-128">Only use hello <b>Production</b> setting if you want toosend push notifications toousers who already purchased your app from hello store.</span></span></p>
</li>
</ol>
<span data-ttu-id="1b82c-129">&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)</span><span class="sxs-lookup"><span data-stu-id="1b82c-129">&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)</span></span>

&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-sandbox.png)

<span data-ttu-id="1b82c-130">Votre concentrateur de notification est maintenant configuré toowork avec APNS, et vous avez tooregister de chaînes de connexion hello votre application et envoyez des notifications push.</span><span class="sxs-lookup"><span data-stu-id="1b82c-130">Your notification hub is now configured toowork with APNS, and you have hello connection strings tooregister your app and send push notifications.</span></span>

## <a name="connect-your-app-toohello-notification-hub"></a><span data-ttu-id="1b82c-131">Se connecter à votre hub de notification d’application toohello</span><span class="sxs-lookup"><span data-stu-id="1b82c-131">Connect your app toohello notification hub</span></span>
#### <a name="create-a-new-project"></a><span data-ttu-id="1b82c-132">Création d'un projet</span><span class="sxs-lookup"><span data-stu-id="1b82c-132">Create a new project</span></span>
1. <span data-ttu-id="1b82c-133">Dans Xamarin Studio, créez un projet iOS et sélectionnez hello **API unifiée** > **Application vue unique** modèle.</span><span class="sxs-lookup"><span data-stu-id="1b82c-133">In Xamarin Studio, create a new iOS project and select hello **Unified API** > **Single View Application** template.</span></span>
   
     ![Xamarin Studio - Sélectionner le type d’application][31]
2. <span data-ttu-id="1b82c-135">Ajouter un composant de messagerie Azure toohello référence.</span><span class="sxs-lookup"><span data-stu-id="1b82c-135">Add a reference toohello Azure Messaging component.</span></span> <span data-ttu-id="1b82c-136">Bonjour vue de solutions, cliquez sur hello **composants** dossier de votre projet et choisissez **obtenir plusieurs composants**.</span><span class="sxs-lookup"><span data-stu-id="1b82c-136">In hello Solution view, right-click hello **Components** folder for your project and choose **Get More Components**.</span></span> <span data-ttu-id="1b82c-137">Recherchez hello **messagerie Azure** composant et ajoutez le projet tooyour hello.</span><span class="sxs-lookup"><span data-stu-id="1b82c-137">Search for hello **Azure Messaging** component and add hello component tooyour project.</span></span>
3. <span data-ttu-id="1b82c-138">Dans **AppDelegate.cs**, ajoutez hello qui suit à l’aide d’instruction :</span><span class="sxs-lookup"><span data-stu-id="1b82c-138">In **AppDelegate.cs**, add hello following using statement:</span></span>
   
        using WindowsAzure.Messaging;
4. <span data-ttu-id="1b82c-139">Déclarez une instance de **SBNotificationHub**:</span><span class="sxs-lookup"><span data-stu-id="1b82c-139">Declare an instance of **SBNotificationHub**:</span></span>
   
        private SBNotificationHub Hub { get; set; }
5. <span data-ttu-id="1b82c-140">Créer un **Constants.cs** classe avec hello suivant variables :</span><span class="sxs-lookup"><span data-stu-id="1b82c-140">Create a **Constants.cs** class with hello following variables:</span></span>
   
        // Azure app-specific connection string and hub path
        public const string ConnectionString = "<Azure connection string>";
        public const string NotificationHubPath = "<Azure hub path>";
6. <span data-ttu-id="1b82c-141">Dans **AppDelegate.cs**, mettre à jour **FinishedLaunching()** suivant de hello toomatch :</span><span class="sxs-lookup"><span data-stu-id="1b82c-141">In **AppDelegate.cs**, update **FinishedLaunching()** toomatch hello following:</span></span>
   
        public override bool FinishedLaunching(UIApplication application, NSDictionary launchOptions)
        {
            if (UIDevice.CurrentDevice.CheckSystemVersion (8, 0)) {
                var pushSettings = UIUserNotificationSettings.GetSettingsForTypes (
                       UIUserNotificationType.Alert | UIUserNotificationType.Badge | UIUserNotificationType.Sound,
                       new NSSet ());
   
                UIApplication.SharedApplication.RegisterUserNotificationSettings (pushSettings);
                UIApplication.SharedApplication.RegisterForRemoteNotifications ();
            } else {
                UIRemoteNotificationType notificationTypes = UIRemoteNotificationType.Alert | UIRemoteNotificationType.Badge | UIRemoteNotificationType.Sound;
                UIApplication.SharedApplication.RegisterForRemoteNotificationTypes (notificationTypes);
            }
   
            return true;
        }
7. <span data-ttu-id="1b82c-142">Remplacer hello **RegisteredForRemoteNotifications()** méthode dans **AppDelegate.cs**:</span><span class="sxs-lookup"><span data-stu-id="1b82c-142">Override hello **RegisteredForRemoteNotifications()** method in **AppDelegate.cs**:</span></span>
   
        public override void RegisteredForRemoteNotifications(UIApplication application, NSData deviceToken)
        {
            Hub = new SBNotificationHub(Constants.ConnectionString, Constants.NotificationHubPath);
   
            Hub.UnregisterAllAsync (deviceToken, (error) => {
                if (error != null)
                {
                    Console.WriteLine("Error calling Unregister: {0}", error.ToString());
                    return;
                }
   
                NSSet tags = null; // create tags if you want
                Hub.RegisterNativeAsync(deviceToken, tags, (errorCallback) => {
                    if (errorCallback != null)
                        Console.WriteLine("RegisterNativeAsync error: " + errorCallback.ToString());
                });
            });
        }
8. <span data-ttu-id="1b82c-143">Remplacer hello **ReceivedRemoteNotification()** méthode dans **AppDelegate.cs**:</span><span class="sxs-lookup"><span data-stu-id="1b82c-143">Override hello **ReceivedRemoteNotification()** method in **AppDelegate.cs**:</span></span>
   
        public override void ReceivedRemoteNotification(UIApplication application, NSDictionary userInfo)
        {
            ProcessNotification(userInfo, false);
        }
9. <span data-ttu-id="1b82c-144">Créer hello **ProcessNotification()** méthode dans **AppDelegate.cs**:</span><span class="sxs-lookup"><span data-stu-id="1b82c-144">Create hello following **ProcessNotification()** method in **AppDelegate.cs**:</span></span>
   
        void ProcessNotification(NSDictionary options, bool fromFinishedLaunching)
        {
            // Check toosee if hello dictionary has hello aps key.  This is hello notification payload you would have sent
            if (null != options && options.ContainsKey(new NSString("aps")))
            {
                //Get hello aps dictionary
                NSDictionary aps = options.ObjectForKey(new NSString("aps")) as NSDictionary;
   
                string alert = string.Empty;
   
                //Extract hello alert text
                // NOTE: If you're using hello simple alert by just specifying
                // "  aps:{alert:"alert msg here"}  ", this will work fine.
                // But if you're using a complex alert with Localization keys, etc.,
                // your "alert" object from hello aps dictionary will be another NSDictionary.
                // Basically hello JSON gets dumped right into a NSDictionary,
                // so keep that in mind.
                if (aps.ContainsKey(new NSString("alert")))
                    alert = (aps [new NSString("alert")] as NSString).ToString();
   
                //If this came from hello ReceivedRemoteNotification while hello app was running,
                // we of course need toomanually process things like hello sound, badge, and alert.
                if (!fromFinishedLaunching)
                {
                    //Manually show an alert
                    if (!string.IsNullOrEmpty(alert))
                    {
                        UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                        avAlert.Show();
                    }
                }
            }
        }
   
   > [!NOTE]
   > <span data-ttu-id="1b82c-145">Vous pouvez choisir toooverride **FailedToRegisterForRemoteNotifications()** toohandle cas d’aucune connexion réseau.</span><span class="sxs-lookup"><span data-stu-id="1b82c-145">You can choose toooverride **FailedToRegisterForRemoteNotifications()** toohandle situations such as no network connection.</span></span> <span data-ttu-id="1b82c-146">Cela est particulièrement important lorsque les utilisateur hello peuvent démarrer votre application en mode hors connexion (par exemple, avion) et que vous souhaitez push toohandle application tooyour spécifique de scénarios de messagerie.</span><span class="sxs-lookup"><span data-stu-id="1b82c-146">This is especially important where hello user might start your application in offline mode (e.g. Airplane) and you want toohandle push messaging scenarios specific tooyour app.</span></span>
   > 
   > 
10. <span data-ttu-id="1b82c-147">Exécutez l’application hello sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="1b82c-147">Run hello app on your device.</span></span>

## <a name="sending-push-notifications"></a><span data-ttu-id="1b82c-148">Envoi de notifications Push</span><span class="sxs-lookup"><span data-stu-id="1b82c-148">Sending Push Notifications</span></span>
<span data-ttu-id="1b82c-149">Vous pouvez tester de recevoir des notifications push dans votre application en envoyant des notifications Bonjour [Azure Portal] via hello **envoi Test** fonctionnalité Bonjour **dépannage** ensemble d’outils, à droite dans la page hello notification hub, comme indiqué dans l’écran hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="1b82c-149">You can test receiving push notifications in your app by sending notifications in hello [Azure Portal] via hello **Test Send** capability in hello **Troubleshooting** toolset, right in hello notification hub page, as shown in hello screen below.</span></span>

![](./media/notification-hubs-ios-get-started/notification-hubs-test-send.png)

<span data-ttu-id="1b82c-150">Les notifications Push sont normalement envoyées via un service principal tel que Mobile Services ou ASP.NET à l’aide d’une bibliothèque compatible.</span><span class="sxs-lookup"><span data-stu-id="1b82c-150">Push notifications are normally sent through a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="1b82c-151">Vous pouvez également utiliser hello API REST directement toosend push des messages si une bibliothèque n’est pas disponible dans votre scénario.</span><span class="sxs-lookup"><span data-stu-id="1b82c-151">You can also use hello REST API directly toosend push messages if a library is not available in your scenario.</span></span> 

<span data-ttu-id="1b82c-152">Dans ce didacticiel, nous plus de simplicité et simplement montrent le test de votre application cliente en envoyant des notifications à l’aide de hello SDK .NET pour les concentrateurs de notification dans une application console à la place d’un service principal.</span><span class="sxs-lookup"><span data-stu-id="1b82c-152">In this tutorial, we will keep it simple and just demonstrate testing your client app by sending notifications using hello .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="1b82c-153">Nous vous recommandons de hello [utiliser Notification Hubs toopush notifications toousers](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) didacticiel en tant qu’étape suivante de hello pour envoyer des notifications à partir d’un serveur principal d’ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="1b82c-153">We recommend hello [Use Notification Hubs toopush notifications toousers](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial as hello next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="1b82c-154">Toutefois, hello méthodes suivantes peut servir pour envoyer des notifications :</span><span class="sxs-lookup"><span data-stu-id="1b82c-154">However, hello following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="1b82c-155">**Interface REST**: vous pouvez prendre en charge les notifications push sur toute plateforme principale à l’aide de hello [interface REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="1b82c-155">**REST Interface**:  You can support push notification on any backend platform using  hello [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="1b82c-156">**Kit de développement logiciel Microsoft Azure Notification Hubs .NET**: Bonjour Gestionnaire de Package Nuget pour Visual Studio, exécutez [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="1b82c-156">**Microsoft Azure Notification Hubs .NET SDK**: In hello Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="1b82c-157">**Node.js** : [comment toouse concentrateurs de Notification à partir de Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="1b82c-157">**Node.js** : [How toouse Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>

<span data-ttu-id="1b82c-158">**Applications mobiles**: pour obtenir un exemple de notifications toosend à partir d’un serveur principal Azure App Service Mobile Apps intégré avec Notification Hubs, consultez [ajouter push notifications tooyour application mobile](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="1b82c-158">**Mobile Apps**: For an example of how toosend notifications from an Azure App Service Mobile Apps backend that's integrated with Notification Hubs, see [Add push notifications tooyour mobile app](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span></span>

* <span data-ttu-id="1b82c-159">**Java / PHP**: pour obtenir un exemple de comment toosend les notifications push à l’aide de hello API REST, consultez « Comment toouse concentrateurs de Notification à partir de Java/PHP » ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span><span class="sxs-lookup"><span data-stu-id="1b82c-159">**Java / PHP**: For an example of how toosend push notifications by using hello REST APIs, see "How toouse Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

#### <a name="optional-send-push-notifications-from-a-net-console-app"></a><span data-ttu-id="1b82c-160">(Facultatif) Envoi de notifications Push à partir d’une application de console .NET</span><span class="sxs-lookup"><span data-stu-id="1b82c-160">(Optional) Send Push Notifications from a .NET Console App</span></span>
<span data-ttu-id="1b82c-161">Dans cette section, nous allons envoyer des notifications Push à l’aide d’une simple application de console .NET.</span><span class="sxs-lookup"><span data-stu-id="1b82c-161">In this section, we will send push notifications by using a simple .NET console app.</span></span> <span data-ttu-id="1b82c-162">Pour des raisons de hello de cet exemple, nous changeons environnement de développement Windows tooa qui a déjà installé Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1b82c-162">For hello purposes of this example, we will switch tooa Windows development environment that has Visual Studio already installed.</span></span>

1. <span data-ttu-id="1b82c-163">Dans Visual Studio, créez une application de console Visual C# :</span><span class="sxs-lookup"><span data-stu-id="1b82c-163">In Visual Studio, create a new Visual C# console application:</span></span>
   
       ![Visual Studio - Create a new console application][213]
2. <span data-ttu-id="1b82c-164">Dans Visual Studio, cliquez successivement sur **Outils**, **Gestionnaire de package NuGet** et **Console du gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="1b82c-164">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="1b82c-165">console du Gestionnaire de package Hello doit apparaître bas toohello ancrée de votre espace de travail de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1b82c-165">hello package manager console should appear docked toohello bottom of your Visual Studio workspace.</span></span>
3. <span data-ttu-id="1b82c-166">Dans la fenêtre de Console du Gestionnaire de Package de hello, définissez hello **projet par défaut** tooyour nouveau projet d’application console et puis, dans la fenêtre de console hello, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1b82c-166">In hello Package Manager Console window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="1b82c-167">Cette opération ajoute une référence de toohello Azure Notification Hubs SDK à l’aide de hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">package NuGet de concentrateurs Microsoft.Azure.Notification</a>.</span><span class="sxs-lookup"><span data-stu-id="1b82c-167">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="1b82c-168">Ouvrez hello `Program.cs` et ajoutez les suivant hello `using` instruction, garantissant que nous pouvons utiliser les classes Azure et des fonctions dans votre classe principale :</span><span class="sxs-lookup"><span data-stu-id="1b82c-168">Open hello `Program.cs` file and add hello following `using` statement, ensuring that we can use Azure classes and functions within your main class:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="1b82c-169">Dans votre `Program` de classe, ajoutez hello suivant (méthode) (n’oubliez pas tooreplace hello **chaîne de connexion** et **nom de hub**) :</span><span class="sxs-lookup"><span data-stu-id="1b82c-169">In your `Program` class, add hello following method (don't forget tooreplace hello **connection string** and **hub name**):</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var alert = "{\"aps\":{\"alert\":\"Hello from .NET!\"}}";
            await hub.SendAppleNativeNotificationAsync(alert);
        }
6. <span data-ttu-id="1b82c-170">Ajouter hello suivant des lignes dans votre `Main` méthode :</span><span class="sxs-lookup"><span data-stu-id="1b82c-170">Add hello following lines in your `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="1b82c-171">Appuyez sur la touche application de hello toorun clé hello F5.</span><span class="sxs-lookup"><span data-stu-id="1b82c-171">Press hello F5 key toorun hello app.</span></span> <span data-ttu-id="1b82c-172">En quelques secondes, une notification Push devrait s’afficher sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="1b82c-172">Within seconds, you should see a push notification appear on your device.</span></span> <span data-ttu-id="1b82c-173">Si vous utilisez le Wi-Fi ou un réseau cellulaire de données, assurez-vous que vous avez une connexion internet active sur l’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="1b82c-173">Whether you are using Wi-Fi or a cellular data network, make sure that you have an active internet connection on hello device.</span></span>

<span data-ttu-id="1b82c-174">Vous pouvez trouver toutes les charges utiles de possibles hello Bonjour Apple [Local et le Guide de programmation de Notification Push].</span><span class="sxs-lookup"><span data-stu-id="1b82c-174">You can find all hello possible payloads in hello Apple [Local and Push Notification Programming Guide].</span></span>

#### <a name="optional-send-notifications-from-a-mobile-service"></a><span data-ttu-id="1b82c-175">(Facultatif) Envoi de notifications depuis un service mobile</span><span class="sxs-lookup"><span data-stu-id="1b82c-175">(Optional) Send Notifications from a Mobile Service</span></span>
<span data-ttu-id="1b82c-176">Dans cette section, nous allons envoyer des notifications Push à l’aide d’un service mobile via un script de nœud.</span><span class="sxs-lookup"><span data-stu-id="1b82c-176">In this section, we will send push notifications using a mobile service through a node script.</span></span>

<span data-ttu-id="1b82c-177">toosend une notification à l’aide d’un service mobile, procédez comme [prise en main des Services mobiles], puis :</span><span class="sxs-lookup"><span data-stu-id="1b82c-177">toosend a notification by using a mobile service, follow [Get started with Mobile Services], and then:</span></span>

1. <span data-ttu-id="1b82c-178">Connectez-vous à toohello [portail classique Azure], puis sélectionnez votre service mobile.</span><span class="sxs-lookup"><span data-stu-id="1b82c-178">Sign in toohello [Azure Classic Portal], and select your mobile service.</span></span>
2. <span data-ttu-id="1b82c-179">Sélectionnez hello **planificateur** onglet en haut de hello.</span><span class="sxs-lookup"><span data-stu-id="1b82c-179">Select hello **Scheduler** tab on hello top.</span></span>
   
       ![Azure Classic Portal - Scheduler][215]
3. <span data-ttu-id="1b82c-180">Créez un travail planifié, insérez un nom, puis sélectionnez **On demand**.</span><span class="sxs-lookup"><span data-stu-id="1b82c-180">Create a new scheduled job, insert a name, and select **On demand**.</span></span>
   
       ![Azure Classic Portal - Create new job][216]
4. <span data-ttu-id="1b82c-181">Lorsque le travail de hello est créé, cliquez sur le nom de la tâche hello.</span><span class="sxs-lookup"><span data-stu-id="1b82c-181">When hello job is created, click hello job name.</span></span> <span data-ttu-id="1b82c-182">Puis cliquez sur hello **Script** onglet sur la barre supérieure de hello.</span><span class="sxs-lookup"><span data-stu-id="1b82c-182">Then click hello **Script** tab on hello top bar.</span></span>
5. <span data-ttu-id="1b82c-183">Insérez hello script à l’intérieur de votre fonction Planificateur suivant.</span><span class="sxs-lookup"><span data-stu-id="1b82c-183">Insert hello following script inside your scheduler function.</span></span> <span data-ttu-id="1b82c-184">Rendre des espaces réservés de hello tooreplace vraiment avec votre notification hub hello et nom de chaîne de connexion pour *DefaultFullSharedAccessSignature* que vous avez obtenu précédemment.</span><span class="sxs-lookup"><span data-stu-id="1b82c-184">Make sure tooreplace hello placeholders with your notification hub name and hello connection string for *DefaultFullSharedAccessSignature* that you obtained earlier.</span></span> <span data-ttu-id="1b82c-185">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="1b82c-185">Click **Save**.</span></span>
   
        var azure = require('azure');
        var notificationHubService = azure.createNotificationHubService('<Hubname>', '<SAS Full access >');
        notificationHubService.apns.send(
            null,
            {"aps":
                {
                  "alert": "Hello from Mobile Services!"
                }
            },
            function (error)
            {
                if (!error) {
                    console.warn("Notification successful");
                }
            }
        );
6. <span data-ttu-id="1b82c-186">Cliquez sur **exécuter une fois** sur la barre inférieure de hello.</span><span class="sxs-lookup"><span data-stu-id="1b82c-186">Click **Run Once** on hello bottom bar.</span></span> <span data-ttu-id="1b82c-187">Vous devez recevoir une alerte sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="1b82c-187">You should receive an alert on your device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b82c-188">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1b82c-188">Next steps</span></span>
<span data-ttu-id="1b82c-189">Dans cet exemple simple, vous diffusées tooall de notifications push à vos appareils iOS.</span><span class="sxs-lookup"><span data-stu-id="1b82c-189">In this simple example, you broadcasted push notifications tooall your iOS devices.</span></span> <span data-ttu-id="1b82c-190">Dans l’ordre tootarget des utilisateurs spécifiques, consultez le didacticiel de toohello [utiliser Notification Hubs toopush notifications toousers].</span><span class="sxs-lookup"><span data-stu-id="1b82c-190">In order tootarget specific users, refer toohello tutorial [Use Notification Hubs toopush notifications toousers].</span></span> <span data-ttu-id="1b82c-191">Si vous souhaitez toosegment vos utilisateurs en groupes d’intérêt, vous pouvez lire [toosend utiliser Notification Hubs actualités].</span><span class="sxs-lookup"><span data-stu-id="1b82c-191">If you want toosegment your users by interest groups, you can read [Use Notification Hubs toosend breaking news].</span></span> <span data-ttu-id="1b82c-192">En savoir plus sur la façon toouse Notification Hubs dans [des conseils de concentrateurs de Notification] et Bonjour [iOS de concentrateurs de Notification procédure-toofor].</span><span class="sxs-lookup"><span data-stu-id="1b82c-192">Learn more about how toouse Notification Hubs in [Notification Hubs Guidance] and in hello [Notification Hubs How-toofor iOS].</span></span>

<!-- Images. -->

[213]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-create-console-app.png

[215]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-scheduler1.png
[216]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-scheduler2.png


[31]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-create-ios-app.png




<!-- URLs. -->
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[prise en main des Services mobiles]: /develop/mobile/tutorials/get-started-xamarin-ios
[portail classique Azure]: https://manage.windowsazure.com/
[des conseils de concentrateurs de Notification]: http://msdn.microsoft.com/library/jj927170.aspx
[iOS de concentrateurs de Notification procédure-toofor]: http://msdn.microsoft.com/library/jj927168.aspx
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[utiliser Notification Hubs toopush notifications toousers]: /manage/services/notification-hubs/notify-users-aspnet
[toosend utiliser Notification Hubs actualités]: /manage/services/notification-hubs/breaking-news-dotnet

[Local et le Guide de programmation de Notification Push]:https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1
[Apple Push Notification Service]: http://go.microsoft.com/fwlink/p/?LinkId=272584

[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
[Xamarin Studio]: http://xamarin.com/download
[WindowsAzure.Messaging]: https://github.com/infosupport/WindowsAzure.Messaging.iOS
[Azure Portal]: https://portal.azure.com
