---
title: "Notifications Push iOS à l’aide des hubs de notification pour applications Xamarin | Microsoft Docs"
description: "Ce didacticiel vous apprend à utiliser Azure Notification Hubs pour envoyer des notifications Push vers une application Xamarin iOS."
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
ms.openlocfilehash: 72a81fa0deb34ace77b8fb9b1a4e6b24ee164b35
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="ios-push-notifications-with-notification-hubs-for-xamarin-apps"></a><span data-ttu-id="7f996-104">Notifications Push iOS à l’aide des hubs de notification pour applications Xamarin</span><span class="sxs-lookup"><span data-stu-id="7f996-104">iOS Push Notifications with Notification Hubs for Xamarin apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="7f996-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="7f996-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7f996-106">Pour suivre ce didacticiel, vous avez besoin d'un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="7f996-106">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="7f996-107">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="7f996-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="7f996-108">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="7f996-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="7f996-109">Ce didacticiel vous montre comment utiliser Azure Notification Hubs pour envoyer des notifications Push vers une application iOS.</span><span class="sxs-lookup"><span data-stu-id="7f996-109">This tutorial shows you how to use Azure Notification Hubs to send push notifications to an iOS application.</span></span>
<span data-ttu-id="7f996-110">Vous allez créer une application Xamarin.iOS vide qui reçoit des notifications Push à l’aide du [service de notification Push Apple (APN, Apple Push Notification)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html).</span><span class="sxs-lookup"><span data-stu-id="7f996-110">You'll create a blank Xamarin.iOS app that receives push notifications by using the [Apple Push Notification Service (APNs)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html).</span></span> <span data-ttu-id="7f996-111">Une fois l’opération terminée, vous pouvez utiliser votre hub de notification pour diffuser des notifications Push sur tous les appareils exécutant votre application.</span><span class="sxs-lookup"><span data-stu-id="7f996-111">When you're finished, you'll be able to use your notification hub to broadcast push notifications to all the devices running your app.</span></span> <span data-ttu-id="7f996-112">Le code finalisé est disponible dans l’exemple [Application NotificationHubs][GitHub].</span><span class="sxs-lookup"><span data-stu-id="7f996-112">The finished code is available in the [NotificationHubs app][GitHub] sample.</span></span>

<span data-ttu-id="7f996-113">Ce didacticiel présente un scénario de simple diffusion de messages Push utilisant les hubs de notification.</span><span class="sxs-lookup"><span data-stu-id="7f996-113">This tutorial demonstrates the simple push message broadcast scenario with Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f996-114">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7f996-114">Prerequisites</span></span>
<span data-ttu-id="7f996-115">Ce didacticiel requiert les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="7f996-115">This tutorial requires the following:</span></span>

* <span data-ttu-id="7f996-116">[Xcode 6.0][Install Xcode]</span><span class="sxs-lookup"><span data-stu-id="7f996-116">[Xcode 6.0][Install Xcode]</span></span>
* <span data-ttu-id="7f996-117">Un appareil compatible iOS 7.0 (ou version ultérieure)</span><span class="sxs-lookup"><span data-stu-id="7f996-117">An iOS 7.0 (or later version) compatible device</span></span>
* <span data-ttu-id="7f996-118">Un abonnement au programme pour développeurs iOS</span><span class="sxs-lookup"><span data-stu-id="7f996-118">iOS Developer Program membership</span></span>
* <span data-ttu-id="7f996-119">[Xamarin Studio]</span><span class="sxs-lookup"><span data-stu-id="7f996-119">[Xamarin Studio]</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="7f996-120">En raison des exigences de configuration requise pour les notifications Push iOS, vous devez déployer et tester l’exemple d’application sur un appareil iOS physique (iPhone ou iPad) au lieu d’un simulateur.</span><span class="sxs-lookup"><span data-stu-id="7f996-120">Because of configuration requirements for iOS push notifications, you must deploy and test the sample application on a physical iOS device (iPhone or iPad) instead of in the simulator.</span></span>
  > 
  > 

<span data-ttu-id="7f996-121">Vous devez suivre ce didacticiel avant de pouvoir suivre tous les autres didacticiels dédiés aux hubs de notification pour applications Xamarin iOS.</span><span class="sxs-lookup"><span data-stu-id="7f996-121">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Xamarin iOS apps.</span></span>

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub"></a><span data-ttu-id="7f996-122">Configuration de votre hub de notification</span><span class="sxs-lookup"><span data-stu-id="7f996-122">Configure your notification hub</span></span>
<span data-ttu-id="7f996-123">Cette section vous guide dans la création d’un hub de notification et la configuration APNS à l’aide du certificat Push **.p12** que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="7f996-123">This section walks you through creating a new notification hub and configuring authentication with APNS using the **.p12** push certificate that you created.</span></span> <span data-ttu-id="7f996-124">Si vous souhaitez utiliser un hub de notification que vous avez déjà créé, vous pouvez passer directement à l’étape 5.</span><span class="sxs-lookup"><span data-stu-id="7f996-124">If you want to use a notification hub that you have already created, you can skip to step 5.</span></span>

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li>

<p><span data-ttu-id="7f996-125">Pour configurer la connexion APNS, accédez au portail Azure, ouvrez les paramètres du hub de notification et cliquez sur <b>Services de notification</b>, puis sur l’élément <b>Apple (APNS)</b> de la liste.</span><span class="sxs-lookup"><span data-stu-id="7f996-125">As we want to configure the APNS connection, in the Azure Portal, open your Notification Hub settings, ande click on <b>Notification Services</b>, and then click the <b>Apple (APNS)</b> item in the list.</span></span> <span data-ttu-id="7f996-126">Cliquez ensuite sur <b>Télécharger le certificat</b> et sélectionnez le certificat <b>.p12</b> exporté précédemment, ainsi que le mot de passe du certificat.</span><span class="sxs-lookup"><span data-stu-id="7f996-126">Once done, click on <b>Upload Certificate</b> and select the <b>.p12</b> certificate that you exported earlier, as well as the password for the certificate.</span></span></p>

<p><span data-ttu-id="7f996-127">Veillez à sélectionner le mode <b>Bac à sable (sandbox)</b> étant donné que vous allez envoyer des messages Push dans un environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="7f996-127">Make sure to select <b>Sandbox</b> mode since you will be sending push messages in a development environment.</span></span> <span data-ttu-id="7f996-128">Utilisez uniquement le paramètre <b>Production</b> si vous souhaitez envoyer des notifications Push aux utilisateurs ayant déjà acheté votre application dans Windows store.</span><span class="sxs-lookup"><span data-stu-id="7f996-128">Only use the <b>Production</b> setting if you want to send push notifications to users who already purchased your app from the store.</span></span></p>
</li>
</ol>
<span data-ttu-id="7f996-129">&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)</span><span class="sxs-lookup"><span data-stu-id="7f996-129">&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)</span></span>

&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-sandbox.png)

<span data-ttu-id="7f996-130">Votre hub de notification est maintenant configuré pour APNS, et vous disposez des chaînes de connexion pour inscrire votre application et envoyer des notifications Push.</span><span class="sxs-lookup"><span data-stu-id="7f996-130">Your notification hub is now configured to work with APNS, and you have the connection strings to register your app and send push notifications.</span></span>

## <a name="connect-your-app-to-the-notification-hub"></a><span data-ttu-id="7f996-131">Connexion de votre application au hub de notification</span><span class="sxs-lookup"><span data-stu-id="7f996-131">Connect your app to the notification hub</span></span>
#### <a name="create-a-new-project"></a><span data-ttu-id="7f996-132">Création d'un projet</span><span class="sxs-lookup"><span data-stu-id="7f996-132">Create a new project</span></span>
1. <span data-ttu-id="7f996-133">Dans Xamarin Studio, créez un projet iOS et sélectionnez le modèle **Unified API** > **Single View Application**.</span><span class="sxs-lookup"><span data-stu-id="7f996-133">In Xamarin Studio, create a new iOS project and select the **Unified API** > **Single View Application** template.</span></span>
   
     ![Xamarin Studio - Sélectionner le type d’application][31]
2. <span data-ttu-id="7f996-135">Ajoutez une référence au composant Azure Messaging.</span><span class="sxs-lookup"><span data-stu-id="7f996-135">Add a reference to the Azure Messaging component.</span></span> <span data-ttu-id="7f996-136">Dans la vue Solution, cliquez avec le bouton droit sur le dossier **Components** de votre projet, puis choisissez **Get More Components**.</span><span class="sxs-lookup"><span data-stu-id="7f996-136">In the Solution view, right-click the **Components** folder for your project and choose **Get More Components**.</span></span> <span data-ttu-id="7f996-137">Recherchez le composant **Azure Messaging** et ajoutez-le à votre projet.</span><span class="sxs-lookup"><span data-stu-id="7f996-137">Search for the **Azure Messaging** component and add the component to your project.</span></span>
3. <span data-ttu-id="7f996-138">Dans **AppDelegate.cs**, ajoutez l'instruction using suivante :</span><span class="sxs-lookup"><span data-stu-id="7f996-138">In **AppDelegate.cs**, add the following using statement:</span></span>
   
        using WindowsAzure.Messaging;
4. <span data-ttu-id="7f996-139">Déclarez une instance de **SBNotificationHub**:</span><span class="sxs-lookup"><span data-stu-id="7f996-139">Declare an instance of **SBNotificationHub**:</span></span>
   
        private SBNotificationHub Hub { get; set; }
5. <span data-ttu-id="7f996-140">Créez une classe **Constants.cs** avec les variables suivantes :</span><span class="sxs-lookup"><span data-stu-id="7f996-140">Create a **Constants.cs** class with the following variables:</span></span>
   
        // Azure app-specific connection string and hub path
        public const string ConnectionString = "<Azure connection string>";
        public const string NotificationHubPath = "<Azure hub path>";
6. <span data-ttu-id="7f996-141">Dans **AppDelegate.cs**, mettez à jour **FinishedLaunching()** afin qu’il corresponde à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="7f996-141">In **AppDelegate.cs**, update **FinishedLaunching()** to match the following:</span></span>
   
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
7. <span data-ttu-id="7f996-142">Remplacez la méthode **RegisteredForRemoteNotifications()** dans **AppDelegate.cs** :</span><span class="sxs-lookup"><span data-stu-id="7f996-142">Override the **RegisteredForRemoteNotifications()** method in **AppDelegate.cs**:</span></span>
   
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
8. <span data-ttu-id="7f996-143">Remplacez la méthode **ReceivedRemoteNotification()** dans **AppDelegate.cs** :</span><span class="sxs-lookup"><span data-stu-id="7f996-143">Override the **ReceivedRemoteNotification()** method in **AppDelegate.cs**:</span></span>
   
        public override void ReceivedRemoteNotification(UIApplication application, NSDictionary userInfo)
        {
            ProcessNotification(userInfo, false);
        }
9. <span data-ttu-id="7f996-144">Créez la méthode **ProcessNotification()** dans **AppDelegate.cs** :</span><span class="sxs-lookup"><span data-stu-id="7f996-144">Create the following **ProcessNotification()** method in **AppDelegate.cs**:</span></span>
   
        void ProcessNotification(NSDictionary options, bool fromFinishedLaunching)
        {
            // Check to see if the dictionary has the aps key.  This is the notification payload you would have sent
            if (null != options && options.ContainsKey(new NSString("aps")))
            {
                //Get the aps dictionary
                NSDictionary aps = options.ObjectForKey(new NSString("aps")) as NSDictionary;
   
                string alert = string.Empty;
   
                //Extract the alert text
                // NOTE: If you're using the simple alert by just specifying
                // "  aps:{alert:"alert msg here"}  ", this will work fine.
                // But if you're using a complex alert with Localization keys, etc.,
                // your "alert" object from the aps dictionary will be another NSDictionary.
                // Basically the JSON gets dumped right into a NSDictionary,
                // so keep that in mind.
                if (aps.ContainsKey(new NSString("alert")))
                    alert = (aps [new NSString("alert")] as NSString).ToString();
   
                //If this came from the ReceivedRemoteNotification while the app was running,
                // we of course need to manually process things like the sound, badge, and alert.
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
   > <span data-ttu-id="7f996-145">Vous pouvez choisir de remplacer **FailedToRegisterForRemoteNotifications()** pour gérer les situations, par exemple, l’absence de connexion réseau, etc.</span><span class="sxs-lookup"><span data-stu-id="7f996-145">You can choose to override **FailedToRegisterForRemoteNotifications()** to handle situations such as no network connection.</span></span> <span data-ttu-id="7f996-146">Ceci est particulièrement important lorsque l’utilisateur cherche à démarrer votre application en mode hors connexion (par exemple, en mode avion) et que vous souhaitez gérer les scénarios de messagerie Push propres à votre application.</span><span class="sxs-lookup"><span data-stu-id="7f996-146">This is especially important where the user might start your application in offline mode (e.g. Airplane) and you want to handle push messaging scenarios specific to your app.</span></span>
   > 
   > 
10. <span data-ttu-id="7f996-147">Exécutez l'application sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="7f996-147">Run the app on your device.</span></span>

## <a name="sending-push-notifications"></a><span data-ttu-id="7f996-148">Envoi de notifications Push</span><span class="sxs-lookup"><span data-stu-id="7f996-148">Sending Push Notifications</span></span>
<span data-ttu-id="7f996-149">Vous pouvez tester la réception de notifications Push dans votre application en envoyant des notifications dans le portail [Azure Portal] à l’aide de la fonctionnalité **Test d’envoi** de la suite d’outils **Dépannage** située à droite de la page du hub de notification, comme indiqué dans l’écran ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="7f996-149">You can test receiving push notifications in your app by sending notifications in the [Azure Portal] via the **Test Send** capability in the **Troubleshooting** toolset, right in the notification hub page, as shown in the screen below.</span></span>

![](./media/notification-hubs-ios-get-started/notification-hubs-test-send.png)

<span data-ttu-id="7f996-150">Les notifications Push sont normalement envoyées via un service principal tel que Mobile Services ou ASP.NET à l’aide d’une bibliothèque compatible.</span><span class="sxs-lookup"><span data-stu-id="7f996-150">Push notifications are normally sent through a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="7f996-151">Vous pouvez également utiliser directement l’API REST pour envoyer des messages Push si aucune bibliothèque n’est disponible pour votre scénario.</span><span class="sxs-lookup"><span data-stu-id="7f996-151">You can also use the REST API directly to send push messages if a library is not available in your scenario.</span></span> 

<span data-ttu-id="7f996-152">Dans ce didacticiel, nous nous contenterons pour plus de simplicité de tester votre application cliente en envoyant des notifications à l'aide du Kit de développement logiciel (SDK) .NET pour Notification Hubs dans une application de console au lieu d'un service principal.</span><span class="sxs-lookup"><span data-stu-id="7f996-152">In this tutorial, we will keep it simple and just demonstrate testing your client app by sending notifications using the .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="7f996-153">Nous vous recommandons de consulter le didacticiel [Utiliser Notification Hubs pour envoyer des notifications Push aux utilisateurs](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) comme prochaine étape pour envoyer des notifications à partir d’un serveur principal ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="7f996-153">We recommend the [Use Notification Hubs to push notifications to users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial as the next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="7f996-154">Toutefois, les approches suivantes peuvent servir à envoyer des notifications :</span><span class="sxs-lookup"><span data-stu-id="7f996-154">However, the following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="7f996-155">**Interface REST**: vous pouvez prendre en charge les notifications Push sur n’importe quel serveur principal à l’aide de l’[interface REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="7f996-155">**REST Interface**:  You can support push notification on any backend platform using  the [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="7f996-156">**SDK .NET Microsoft Azure Notification Hubs**: dans le Gestionnaire de package Nuget pour Visual Studio, exécutez [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="7f996-156">**Microsoft Azure Notification Hubs .NET SDK**: In the Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="7f996-157">**Node.js** : [Utilisation de Notification Hubs à partir de Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="7f996-157">**Node.js** : [How to use Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>

<span data-ttu-id="7f996-158">**Applications mobiles Azure**: pour découvrir un exemple de la procédure d’envoi de notifications à partir d’une application mobile Azure intégrée à Notification Hubs, consultez l’article [Add push notifications for Mobile Apps](../app-service-mobile/app-service-mobile-ios-get-started-push.md) (Ajouter des notifications Push pour Mobile Apps).</span><span class="sxs-lookup"><span data-stu-id="7f996-158">**Mobile Apps**: For an example of how to send notifications from an Azure App Service Mobile Apps backend that's integrated with Notification Hubs, see [Add push notifications to your mobile app](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span></span>

* <span data-ttu-id="7f996-159">**Java / PHP** : pour voir un exemple d’envoi de notifications Push au moyen des API REST, consultez « Utilisation de Notification Hubs à partir de Java/PHP » ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span><span class="sxs-lookup"><span data-stu-id="7f996-159">**Java / PHP**: For an example of how to send push notifications by using the REST APIs, see "How to use Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

#### <a name="optional-send-push-notifications-from-a-net-console-app"></a><span data-ttu-id="7f996-160">(Facultatif) Envoi de notifications Push à partir d’une application de console .NET</span><span class="sxs-lookup"><span data-stu-id="7f996-160">(Optional) Send Push Notifications from a .NET Console App</span></span>
<span data-ttu-id="7f996-161">Dans cette section, nous allons envoyer des notifications Push à l’aide d’une simple application de console .NET.</span><span class="sxs-lookup"><span data-stu-id="7f996-161">In this section, we will send push notifications by using a simple .NET console app.</span></span> <span data-ttu-id="7f996-162">Dans cet exemple, nous allons basculer vers un environnement de développement Windows dans lequel est déjà installé Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7f996-162">For the purposes of this example, we will switch to a Windows development environment that has Visual Studio already installed.</span></span>

1. <span data-ttu-id="7f996-163">Dans Visual Studio, créez une application de console Visual C# :</span><span class="sxs-lookup"><span data-stu-id="7f996-163">In Visual Studio, create a new Visual C# console application:</span></span>
   
       ![Visual Studio - Create a new console application][213]
2. <span data-ttu-id="7f996-164">Dans Visual Studio, cliquez successivement sur **Outils**, **Gestionnaire de package NuGet** et **Console du gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="7f996-164">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="7f996-165">La console du gestionnaire de package doit apparaître ancrée au bas de votre espace de travail Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7f996-165">The package manager console should appear docked to the bottom of your Visual Studio workspace.</span></span>
3. <span data-ttu-id="7f996-166">Dans la fenêtre Console du gestionnaire de package, choisissez **Projet par défaut** comme nouveau projet d’application console, puis exécutez la commande suivante dans la fenêtre de console :</span><span class="sxs-lookup"><span data-stu-id="7f996-166">In the Package Manager Console window, set the **Default project** to your new console application project, and then in the console window, execute the following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="7f996-167">Cette opération ajoute une référence au Kit de développement logiciel (SDK) Azure Notification Hubs à l’aide du <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">package NuGet Microsoft.Azure.Notification Hubs</a>.</span><span class="sxs-lookup"><span data-stu-id="7f996-167">This adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="7f996-168">Ouvrez le fichier `Program.cs` et ajoutez l’instruction `using` suivante pour garantir que nous pouvons utiliser les classes et les fonctions Azure dans notre classe principale :</span><span class="sxs-lookup"><span data-stu-id="7f996-168">Open the `Program.cs` file and add the following `using` statement, ensuring that we can use Azure classes and functions within your main class:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="7f996-169">Dans votre classe `Program`, ajoutez la méthode suivante (n’oubliez pas de remplacer la **chaîne de connexion** et le **nom du hub**) :</span><span class="sxs-lookup"><span data-stu-id="7f996-169">In your `Program` class, add the following method (don't forget to replace the **connection string** and **hub name**):</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var alert = "{\"aps\":{\"alert\":\"Hello from .NET!\"}}";
            await hub.SendAppleNativeNotificationAsync(alert);
        }
6. <span data-ttu-id="7f996-170">Ajoutez ensuite les lignes suivantes dans votre méthode `Main` :</span><span class="sxs-lookup"><span data-stu-id="7f996-170">Add the following lines in your `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="7f996-171">Appuyez sur la touche F5 pour exécuter l'application.</span><span class="sxs-lookup"><span data-stu-id="7f996-171">Press the F5 key to run the app.</span></span> <span data-ttu-id="7f996-172">En quelques secondes, une notification Push devrait s’afficher sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="7f996-172">Within seconds, you should see a push notification appear on your device.</span></span> <span data-ttu-id="7f996-173">Que vous utilisiez le Wi-Fi ou un réseau cellulaire, assurez-vous que votre appareil dispose bien d’une connexion Internet.</span><span class="sxs-lookup"><span data-stu-id="7f996-173">Whether you are using Wi-Fi or a cellular data network, make sure that you have an active internet connection on the device.</span></span>

<span data-ttu-id="7f996-174">Vous trouverez toutes les charges utiles possibles dans le [Guide de programmation des notifications locales et Push]d'Apple.</span><span class="sxs-lookup"><span data-stu-id="7f996-174">You can find all the possible payloads in the Apple [Local and Push Notification Programming Guide].</span></span>

#### <a name="optional-send-notifications-from-a-mobile-service"></a><span data-ttu-id="7f996-175">(Facultatif) Envoi de notifications depuis un service mobile</span><span class="sxs-lookup"><span data-stu-id="7f996-175">(Optional) Send Notifications from a Mobile Service</span></span>
<span data-ttu-id="7f996-176">Dans cette section, nous allons envoyer des notifications Push à l’aide d’un service mobile via un script de nœud.</span><span class="sxs-lookup"><span data-stu-id="7f996-176">In this section, we will send push notifications using a mobile service through a node script.</span></span>

<span data-ttu-id="7f996-177">Pour envoyer une notification à l’aide d’un service mobile, suivez les instructions de la rubrique [Prise en main de Mobile Services], puis :</span><span class="sxs-lookup"><span data-stu-id="7f996-177">To send a notification by using a mobile service, follow [Get started with Mobile Services], and then:</span></span>

1. <span data-ttu-id="7f996-178">Connectez-vous au [portail Azure Classic], puis sélectionnez votre service mobile.</span><span class="sxs-lookup"><span data-stu-id="7f996-178">Sign in to the [Azure Classic Portal], and select your mobile service.</span></span>
2. <span data-ttu-id="7f996-179">Sélectionnez l’onglet **Scheduler** dans la partie supérieure.</span><span class="sxs-lookup"><span data-stu-id="7f996-179">Select the **Scheduler** tab on the top.</span></span>
   
       ![Azure Classic Portal - Scheduler][215]
3. <span data-ttu-id="7f996-180">Créez un travail planifié, insérez un nom, puis sélectionnez **On demand**.</span><span class="sxs-lookup"><span data-stu-id="7f996-180">Create a new scheduled job, insert a name, and select **On demand**.</span></span>
   
       ![Azure Classic Portal - Create new job][216]
4. <span data-ttu-id="7f996-181">Lorsque le travail est créé, cliquez sur son nom.</span><span class="sxs-lookup"><span data-stu-id="7f996-181">When the job is created, click the job name.</span></span> <span data-ttu-id="7f996-182">Cliquez ensuite sur l’onglet **Script** dans la barre supérieure.</span><span class="sxs-lookup"><span data-stu-id="7f996-182">Then click the **Script** tab on the top bar.</span></span>
5. <span data-ttu-id="7f996-183">Insérez le script suivant dans votre fonction Scheduler.</span><span class="sxs-lookup"><span data-stu-id="7f996-183">Insert the following script inside your scheduler function.</span></span> <span data-ttu-id="7f996-184">Remplacez les espaces réservés par le nom de votre concentrateur de notification et la chaîne de connexion pour *DefaultFullSharedAccessSignature* obtenue précédemment.</span><span class="sxs-lookup"><span data-stu-id="7f996-184">Make sure to replace the placeholders with your notification hub name and the connection string for *DefaultFullSharedAccessSignature* that you obtained earlier.</span></span> <span data-ttu-id="7f996-185">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="7f996-185">Click **Save**.</span></span>
   
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
6. <span data-ttu-id="7f996-186">Cliquez sur **Exécuter une fois** sur la barre inférieure.</span><span class="sxs-lookup"><span data-stu-id="7f996-186">Click **Run Once** on the bottom bar.</span></span> <span data-ttu-id="7f996-187">Vous devez recevoir une alerte sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="7f996-187">You should receive an alert on your device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f996-188">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7f996-188">Next steps</span></span>
<span data-ttu-id="7f996-189">Dans cet exemple simple, vous avez envoyé des notifications Push à tous vos appareils iOS.</span><span class="sxs-lookup"><span data-stu-id="7f996-189">In this simple example, you broadcasted push notifications to all your iOS devices.</span></span> <span data-ttu-id="7f996-190">Pour cibler certains utilisateurs, reportez-vous au didacticiel [Utilisation des Notification Hubs pour envoyer des notifications Push aux utilisateurs].</span><span class="sxs-lookup"><span data-stu-id="7f996-190">In order to target specific users, refer to the tutorial [Use Notification Hubs to push notifications to users].</span></span> <span data-ttu-id="7f996-191">Pour segmenter vos utilisateurs par groupes d'intérêt, consultez la page [Utilisation des Notification Hubs pour diffuser les dernières nouvelles].</span><span class="sxs-lookup"><span data-stu-id="7f996-191">If you want to segment your users by interest groups, you can read [Use Notification Hubs to send breaking news].</span></span> <span data-ttu-id="7f996-192">Pour plus d’informations sur l’utilisation de Notification Hubs, consultez les pages [Vue d’ensemble de Notifications Hubs] et [Procédures Notification Hubs pour iOS].</span><span class="sxs-lookup"><span data-stu-id="7f996-192">Learn more about how to use Notification Hubs in [Notification Hubs Guidance] and in the [Notification Hubs How-To for iOS].</span></span>

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

<span data-ttu-id="7f996-193">[Prise en main de Mobile Services]: /develop/mobile/tutorials/get-started-xamarin-ios</span><span class="sxs-lookup"><span data-stu-id="7f996-193">[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-xamarin-ios</span></span>
<span data-ttu-id="7f996-194">[portail Azure Classic]: https://manage.windowsazure.com/</span><span class="sxs-lookup"><span data-stu-id="7f996-194">[Azure Classic Portal]: https://manage.windowsazure.com/</span></span>
<span data-ttu-id="7f996-195">[Vue d’ensemble de Notifications Hubs]: http://msdn.microsoft.com/library/jj927170.aspx</span><span class="sxs-lookup"><span data-stu-id="7f996-195">[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx</span></span>
<span data-ttu-id="7f996-196">[Procédures Notification Hubs pour iOS]: http://msdn.microsoft.com/library/jj927168.aspx</span><span class="sxs-lookup"><span data-stu-id="7f996-196">[Notification Hubs How-To for iOS]: http://msdn.microsoft.com/library/jj927168.aspx</span></span>
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

<span data-ttu-id="7f996-197">[Utilisation des Notification Hubs pour envoyer des notifications Push aux utilisateurs]: /manage/services/notification-hubs/notify-users-aspnet</span><span class="sxs-lookup"><span data-stu-id="7f996-197">[Use Notification Hubs to push notifications to users]: /manage/services/notification-hubs/notify-users-aspnet</span></span>
<span data-ttu-id="7f996-198">[Utilisation des Notification Hubs pour diffuser les dernières nouvelles]: /manage/services/notification-hubs/breaking-news-dotnet</span><span class="sxs-lookup"><span data-stu-id="7f996-198">[Use Notification Hubs to send breaking news]: /manage/services/notification-hubs/breaking-news-dotnet</span></span>

<span data-ttu-id="7f996-199">[Guide de programmation des notifications locales et Push]:https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1</span><span class="sxs-lookup"><span data-stu-id="7f996-199">[Local and Push Notification Programming Guide]:https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1</span></span>
[Apple Push Notification Service]: http://go.microsoft.com/fwlink/p/?LinkId=272584

[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
<span data-ttu-id="7f996-200">[Xamarin Studio]: http://xamarin.com/download</span><span class="sxs-lookup"><span data-stu-id="7f996-200">[Xamarin Studio]: http://xamarin.com/download</span></span>
[WindowsAzure.Messaging]: https://github.com/infosupport/WindowsAzure.Messaging.iOS
<span data-ttu-id="7f996-201">[Azure Portal]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="7f996-201">[Azure Portal]: https://portal.azure.com</span></span>
